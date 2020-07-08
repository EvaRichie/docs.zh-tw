---
title: invalidIUnknown MDA
description: 檢查 invalidIUnknown managed 偵錯工具（MDA），這會在不正確 IUnknown 指標從機器碼傳遞至 managed 程式碼時啟用。
ms.date: 03/30/2017
helpviewer_keywords:
- MDAs (managed debugging assistants), invalid IUnknown pointer
- InvalidIUnknown MDA
- invalid IUnknown pointers
- IUnknown pointers
- managed debugging assistants (MDAs), invalid IUnknown pointer
ms.assetid: c7924771-a16b-40fe-b337-ce51dcdf6a12
ms.openlocfilehash: 65d704463ed746390ff1710b590bf080013bf53d
ms.sourcegitcommit: 0edbeb66d71b8df10fcb374cfca4d731b58ccdb2
ms.contentlocale: zh-TW
ms.lasthandoff: 07/07/2020
ms.locfileid: "86051723"
---
# <a name="invalidiunknown-mda"></a><span data-ttu-id="737bc-103">invalidIUnknown MDA</span><span class="sxs-lookup"><span data-stu-id="737bc-103">invalidIUnknown MDA</span></span>
<span data-ttu-id="737bc-104">當無效的 `IUnknown` 指標從原生程式碼傳遞至 Managed 程式碼時，會啟動 `invalidIUnknown` Managed 偵錯助理 (MDA)。</span><span class="sxs-lookup"><span data-stu-id="737bc-104">The `invalidIUnknown` managed debugging assistant (MDA) is activated when an invalid `IUnknown` pointer is passed to managed code from native code.</span></span> <span data-ttu-id="737bc-105">查詢 `IUnknown` 介面時，`IUnknown` 無法成功傳回。</span><span class="sxs-lookup"><span data-stu-id="737bc-105">The `IUnknown` fails to return success when queried for the `IUnknown` interface.</span></span>  
  
## <a name="symptoms"></a><span data-ttu-id="737bc-106">徵狀</span><span class="sxs-lookup"><span data-stu-id="737bc-106">Symptoms</span></span>  
 <span data-ttu-id="737bc-107">引數封送處理期間，在封送處理 COM 介面指標時，發生未預期的錯誤。</span><span class="sxs-lookup"><span data-stu-id="737bc-107">An unexpected error occurs when marshaling a COM interface pointer during argument marshaling.</span></span>  
  
## <a name="cause"></a><span data-ttu-id="737bc-108">原因</span><span class="sxs-lookup"><span data-stu-id="737bc-108">Cause</span></span>  
 <span data-ttu-id="737bc-109">對於傳遞至 CLR 的 COM 介面進行了不正確的 `QueryInterface` 實作。</span><span class="sxs-lookup"><span data-stu-id="737bc-109">An incorrect `QueryInterface` implementation on the COM interface passed to the CLR.</span></span>  
  
## <a name="resolution"></a><span data-ttu-id="737bc-110">解決方案</span><span class="sxs-lookup"><span data-stu-id="737bc-110">Resolution</span></span>  
 <span data-ttu-id="737bc-111">更正 `QueryInterface` 實作。</span><span class="sxs-lookup"><span data-stu-id="737bc-111">Correct the `QueryInterface` implementation.</span></span>  
  
## <a name="effect-on-the-runtime"></a><span data-ttu-id="737bc-112">對執行階段的影響</span><span class="sxs-lookup"><span data-stu-id="737bc-112">Effect on the Runtime</span></span>  
 <span data-ttu-id="737bc-113">此 MDA 對 CLR 沒有影響。</span><span class="sxs-lookup"><span data-stu-id="737bc-113">This MDA has no effect on the CLR.</span></span>  
  
## <a name="output"></a><span data-ttu-id="737bc-114">輸出</span><span class="sxs-lookup"><span data-stu-id="737bc-114">Output</span></span>  
 <span data-ttu-id="737bc-115">錯誤的描述。</span><span class="sxs-lookup"><span data-stu-id="737bc-115">The description of the error.</span></span>  
  
## <a name="configuration"></a><span data-ttu-id="737bc-116">組態</span><span class="sxs-lookup"><span data-stu-id="737bc-116">Configuration</span></span>  
  
```xml  
<mdaConfig>  
  <assistants>  
    <invalidIUnknown />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a><span data-ttu-id="737bc-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="737bc-117">See also</span></span>

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [<span data-ttu-id="737bc-118">使用 Managed 偵錯助理診斷錯誤</span><span class="sxs-lookup"><span data-stu-id="737bc-118">Diagnosing Errors with Managed Debugging Assistants</span></span>](diagnosing-errors-with-managed-debugging-assistants.md)
- [<span data-ttu-id="737bc-119">Interop 封送處理</span><span class="sxs-lookup"><span data-stu-id="737bc-119">Interop Marshaling</span></span>](../interop/interop-marshaling.md)
