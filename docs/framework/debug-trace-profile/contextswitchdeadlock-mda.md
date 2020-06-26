---
title: contextSwitchDeadlock MDA
description: 瞭解 .NET 中的 coNtextSwitchDeadlock managed 偵錯工具（MDA），這是在 COM 內容轉換期間偵測到鎖死時啟動的。
ms.date: 03/30/2017
helpviewer_keywords:
- deadlocks [.NET Framework]
- pumping messages
- STA message pumping
- single-threaded COM components
- MDAs (managed debugging assistants), context switching deadlocks
- managed debugging assistants (MDAs), context switching deadlocks
- ContextSwitchDeadlock MDA
- message pumping
- context switching deadlocks
ms.assetid: 26dfaa15-9ddb-4b0a-b6da-999bba664fa6
ms.openlocfilehash: 52db4f2c88bac4e8cac621cca989fa10acb43f94
ms.sourcegitcommit: a2c8b19e813a52b91facbb5d7e3c062c7188b457
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85416014"
---
# <a name="contextswitchdeadlock-mda"></a><span data-ttu-id="b9267-103">contextSwitchDeadlock MDA</span><span class="sxs-lookup"><span data-stu-id="b9267-103">contextSwitchDeadlock MDA</span></span>

<span data-ttu-id="b9267-104">試圖進行 COM 內容轉換期間，偵測到死結時，會啟用 `contextSwitchDeadlock` Managed 偵錯助理 (MDA)。</span><span class="sxs-lookup"><span data-stu-id="b9267-104">The `contextSwitchDeadlock` managed debugging assistant (MDA) is activated when a deadlock is detected during an attempted COM context transition.</span></span>

## <a name="symptoms"></a><span data-ttu-id="b9267-105">徵狀</span><span class="sxs-lookup"><span data-stu-id="b9267-105">Symptoms</span></span>

<span data-ttu-id="b9267-106">最常見的徵兆是，在 Unmanaged COM 元件上從 Managed 程式碼進行的呼叫未傳回。</span><span class="sxs-lookup"><span data-stu-id="b9267-106">The most common symptom is that a call on an unmanaged COM component from managed code does not return.</span></span>  <span data-ttu-id="b9267-107">另一個徵兆是記憶體使用量隨著時間增加。</span><span class="sxs-lookup"><span data-stu-id="b9267-107">Another symptom is memory usage increasing over time.</span></span>

## <a name="cause"></a><span data-ttu-id="b9267-108">原因</span><span class="sxs-lookup"><span data-stu-id="b9267-108">Cause</span></span>

<span data-ttu-id="b9267-109">最有可能的原因是，單一執行緒 Apartment (STA) 執行緒沒有提取訊息。</span><span class="sxs-lookup"><span data-stu-id="b9267-109">The most probable cause is that a single-threaded apartment (STA) thread is not pumping messages.</span></span> <span data-ttu-id="b9267-110">STA 執行緒可能正在等待而沒有提取訊息，或是正在執行長時間作業，不允許訊息佇列提取。</span><span class="sxs-lookup"><span data-stu-id="b9267-110">The STA thread is either waiting without pumping messages or is performing lengthy operations and is not allowing the message queue to pump.</span></span>

<span data-ttu-id="b9267-111">記憶體使用量隨著時間增加的原因，是因為完成項執行緒試圖在 Unmanaged COM 元件上呼叫 `Release`，而該元件未傳回。</span><span class="sxs-lookup"><span data-stu-id="b9267-111">Memory usage increasing over time is caused by the finalizer thread attempting to call `Release` on an unmanaged COM component and that component is not returning.</span></span>  <span data-ttu-id="b9267-112">這會導致完成項無法回收其他物件。</span><span class="sxs-lookup"><span data-stu-id="b9267-112">This prevents the finalizer from reclaiming other objects.</span></span>

<span data-ttu-id="b9267-113">根據預設，Visual Basic 主控台應用程式主要執行緒的執行緒模型為 STA。</span><span class="sxs-lookup"><span data-stu-id="b9267-113">By default, the threading model for the main thread of Visual Basic console applications is STA.</span></span> <span data-ttu-id="b9267-114">如果 STA 執行緒直接或間接透過通用語言執行平台或協力廠商控制項來使用 COM 互通性，就會啟用此 MDA。</span><span class="sxs-lookup"><span data-stu-id="b9267-114">This MDA is activated if an STA thread uses COM interoperability either directly or indirectly through the common language runtime or a third-party control.</span></span>  <span data-ttu-id="b9267-115">若要避免在 Visual Basic 主控台應用程式中啟用此 MDA，請將 <xref:System.MTAThreadAttribute> 屬性套用至 Main 方法，或修改應用程式來提取訊問。</span><span class="sxs-lookup"><span data-stu-id="b9267-115">To avoid activating this MDA in a Visual Basic console application, apply the <xref:System.MTAThreadAttribute> attribute to the main method or modify the application to pump messages.</span></span>

<span data-ttu-id="b9267-116">在符合下列所有條件的情況下，有可能會錯誤地啟用此 MDA：</span><span class="sxs-lookup"><span data-stu-id="b9267-116">It is possible for this MDA to be falsely activated when all of the following conditions are met:</span></span>

- <span data-ttu-id="b9267-117">應用程式直接或間接透過程式庫，從 STA 執行緒建立 COM 元件。</span><span class="sxs-lookup"><span data-stu-id="b9267-117">An application creates COM components from STA threads either directly or indirectly through libraries.</span></span>

- <span data-ttu-id="b9267-118">已在偵錯工具中停止應用程式，而使用者繼續應用程式，或執行步驟作業。</span><span class="sxs-lookup"><span data-stu-id="b9267-118">The application was stopped in the debugger and the user either continued the application or performed a step operation.</span></span>

- <span data-ttu-id="b9267-119">未啟用 Unmanaged 偵錯。</span><span class="sxs-lookup"><span data-stu-id="b9267-119">Unmanaged debugging is not enabled.</span></span>

<span data-ttu-id="b9267-120">若要判斷是否錯誤地啟用 MDA，請停用所有中斷點、重新啟動應用程式，並且讓它不間斷地執行。</span><span class="sxs-lookup"><span data-stu-id="b9267-120">To determine if the MDA is being falsely activated, disable all breakpoints, restart the application, and allow it to run without stopping.</span></span> <span data-ttu-id="b9267-121">如果未啟用 MDA，則可能初始啟用時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="b9267-121">If the MDA is not activated, it is likely the initial activation was false.</span></span> <span data-ttu-id="b9267-122">若是如此，請停用 MDA，以避免阻礙偵錯工作階段。</span><span class="sxs-lookup"><span data-stu-id="b9267-122">In this case, disable the MDA to avoid interference with the debugging session.</span></span>

> [!NOTE]
> <span data-ttu-id="b9267-123">此 MDA 位於 Visual Studio 的預設集合中。</span><span class="sxs-lookup"><span data-stu-id="b9267-123">This MDA is in the default set for Visual Studio.</span></span> <span data-ttu-id="b9267-124">如需如何停用 Mda 的詳細資訊，請參閱[診斷 Managed 偵錯工具的錯誤](diagnosing-errors-with-managed-debugging-assistants.md#enable-and-disable-mdas)。</span><span class="sxs-lookup"><span data-stu-id="b9267-124">For information about how to disable MDAs, see [Diagnosing Errors with Managed Debugging Assistants](diagnosing-errors-with-managed-debugging-assistants.md#enable-and-disable-mdas).</span></span>

## <a name="resolution"></a><span data-ttu-id="b9267-125">解決方案</span><span class="sxs-lookup"><span data-stu-id="b9267-125">Resolution</span></span>

<span data-ttu-id="b9267-126">遵循有關 STA 訊息幫浦的 COM 規則。</span><span class="sxs-lookup"><span data-stu-id="b9267-126">Follow COM rules regarding STA message pumping.</span></span>

## <a name="effect-on-the-runtime"></a><span data-ttu-id="b9267-127">對執行階段的影響</span><span class="sxs-lookup"><span data-stu-id="b9267-127">Effect on the Runtime</span></span>

<span data-ttu-id="b9267-128">此 MDA 對 CLR 沒有影響。</span><span class="sxs-lookup"><span data-stu-id="b9267-128">This MDA has no effect on the CLR.</span></span> <span data-ttu-id="b9267-129">它只會提報 COM 內容的相關資料。</span><span class="sxs-lookup"><span data-stu-id="b9267-129">It only reports data about COM contexts.</span></span>

## <a name="output"></a><span data-ttu-id="b9267-130">輸出</span><span class="sxs-lookup"><span data-stu-id="b9267-130">Output</span></span>

<span data-ttu-id="b9267-131">描述目前內容和目標內容的訊息。</span><span class="sxs-lookup"><span data-stu-id="b9267-131">A message describing the current context and the target context.</span></span>

## <a name="configuration"></a><span data-ttu-id="b9267-132">設定</span><span class="sxs-lookup"><span data-stu-id="b9267-132">Configuration</span></span>

```xml
<mdaConfig>
  <assistants>
    <contextSwitchDeadlock />
  </assistants>
</mdaConfig>
```

## <a name="see-also"></a><span data-ttu-id="b9267-133">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b9267-133">See also</span></span>

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [<span data-ttu-id="b9267-134">使用 Managed 偵錯助理診斷錯誤</span><span class="sxs-lookup"><span data-stu-id="b9267-134">Diagnosing Errors with Managed Debugging Assistants</span></span>](diagnosing-errors-with-managed-debugging-assistants.md)
- [<span data-ttu-id="b9267-135">Interop 封送處理</span><span class="sxs-lookup"><span data-stu-id="b9267-135">Interop Marshaling</span></span>](../interop/interop-marshaling.md)
