---
title: nonComVisibleBaseClass MDA
description: 請參閱 nonComVisibleBaseClass managed 偵錯工具 (MDA) ，其會在透過 COR_E_INVALIDOPERATION 的機器碼失敗的 QueryInterface 呼叫上叫用。
ms.date: 03/30/2017
helpviewer_keywords:
- visible classes
- managed debugging assistants (MDAs), COM visible classes
- nonComVisibleBaseClass MDA
- COM visible classes
- QueryInterface call failures
- MDAs (managed debugging assistants), COM visible classes
ms.assetid: 9ec1af27-604b-477e-9ee2-e833eb10d3ce
ms.openlocfilehash: c13d05d04c75d6b4f1be4a5f338fd7246fed8db4
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96254567"
---
# <a name="noncomvisiblebaseclass-mda"></a><span data-ttu-id="f20b7-103">nonComVisibleBaseClass MDA</span><span class="sxs-lookup"><span data-stu-id="f20b7-103">nonComVisibleBaseClass MDA</span></span>

<span data-ttu-id="f20b7-104">在由 COM 可見 Managed 類別 (衍生自不是 COM 可見的基底類別) 的可呼叫包裝函式 (CCW) 上的原生或 Unmanaged 程式碼呼叫 `QueryInterface` 時，會啟動 `nonComVisibleBaseClass` Managed 偵錯助理 (MDA)。</span><span class="sxs-lookup"><span data-stu-id="f20b7-104">The `nonComVisibleBaseClass` managed debugging assistant (MDA) is activated when a `QueryInterface` call is made by native or unmanaged code on the COM callable wrapper (CCW) of a COM-visible managed class that derives from a base class that is not COM visible.</span></span>  <span data-ttu-id="f20b7-105">`QueryInterface` 呼叫會導致只有在呼叫要求類別介面或預設 COM 可見 Managed 類別的 `IDispatch` 情況下才啟用 MDA。</span><span class="sxs-lookup"><span data-stu-id="f20b7-105">The `QueryInterface` call causes the MDA to activate only in cases where call requests the class interface or default `IDispatch` of the COM-visible managed class.</span></span>  <span data-ttu-id="f20b7-106">當 `QueryInterface` 是套用 <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> 屬性且會由 COM 可見的類別明確實作的明確介面時，則不啟動 MDA。</span><span class="sxs-lookup"><span data-stu-id="f20b7-106">The MDA is not activated when the `QueryInterface` is for an explicit interface that has the <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> attribute applied and is explicitly implemented by the COM-visible class.</span></span>  
  
## <a name="symptoms"></a><span data-ttu-id="f20b7-107">徵狀</span><span class="sxs-lookup"><span data-stu-id="f20b7-107">Symptoms</span></span>  

 <span data-ttu-id="f20b7-108">`QueryInterface` 會由使用 COR_E_INVALIDOPERATION HRESULT 失敗的原生程式碼所呼叫。</span><span class="sxs-lookup"><span data-stu-id="f20b7-108">A `QueryInterface` call made from native code that is failing with a COR_E_INVALIDOPERATION HRESULT.</span></span>  <span data-ttu-id="f20b7-109">HRESULT 可能是因為執行階段不允許會導致此 MDA 啟動的 `QueryInterface` 呼叫。</span><span class="sxs-lookup"><span data-stu-id="f20b7-109">The HRESULT might be due to the runtime disallowing `QueryInterface` calls that would cause the activation of this MDA.</span></span>  
  
## <a name="cause"></a><span data-ttu-id="f20b7-110">原因</span><span class="sxs-lookup"><span data-stu-id="f20b7-110">Cause</span></span>  

 <span data-ttu-id="f20b7-111">執行階段不允許 `QueryInterface` 呼叫類別介面，或呼叫 COM 可見類別 (因潛在的版本控制問題而衍生自不是 COM 可見的類別) 之預設 `IDispatch` 介面。</span><span class="sxs-lookup"><span data-stu-id="f20b7-111">The runtime cannot allow `QueryInterface` calls for the class interface or default `IDispatch` interface of a COM-visible class that derives from a class that is not COM-visible because of potential versioning problems.</span></span>  <span data-ttu-id="f20b7-112">例如，如果加入任何公用成員至不是 COM 可見的基底類別時，則可能會中斷現有使用衍生類別的 COM 用戶端，因為這類變更可能會更改此衍生類別的 vtable ，其中包含基底類別成員。</span><span class="sxs-lookup"><span data-stu-id="f20b7-112">For example, if any public members were added to the base class that is not COM-visible, existing COM clients using the derived class could potentially break because the vtable of the derived class, which contains the base class members, would be altered by such a change.</span></span>  <span data-ttu-id="f20b7-113">公開給 COM 的明確介面並沒有這個問題，因為在 vtable 中不包含介面的基底成員。</span><span class="sxs-lookup"><span data-stu-id="f20b7-113">Explicit interfaces exposed to COM do not have this problem because they do not include the base members of interfaces in the vtable.</span></span>  
  
## <a name="resolution"></a><span data-ttu-id="f20b7-114">解決方法</span><span class="sxs-lookup"><span data-stu-id="f20b7-114">Resolution</span></span>  

 <span data-ttu-id="f20b7-115">不要公開類別介面。</span><span class="sxs-lookup"><span data-stu-id="f20b7-115">Do not expose the class interface.</span></span> <span data-ttu-id="f20b7-116">定義明確的介面，並套用 <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> 屬性。</span><span class="sxs-lookup"><span data-stu-id="f20b7-116">Define an explicit interface and apply the <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> attribute to it.</span></span>  
  
## <a name="effect-on-the-runtime"></a><span data-ttu-id="f20b7-117">對執行階段的影響</span><span class="sxs-lookup"><span data-stu-id="f20b7-117">Effect on the Runtime</span></span>  

 <span data-ttu-id="f20b7-118">此 MDA 對 CLR 沒有影響。</span><span class="sxs-lookup"><span data-stu-id="f20b7-118">This MDA has no effect on the CLR.</span></span>  
  
## <a name="output"></a><span data-ttu-id="f20b7-119">輸出</span><span class="sxs-lookup"><span data-stu-id="f20b7-119">Output</span></span>  

 <span data-ttu-id="f20b7-120">下列是在 COM 可見類別 `Derived` (衍生自不是 COM 可見的類別 `Base` ) 上呼叫 `QueryInterface` 的範例訊息。</span><span class="sxs-lookup"><span data-stu-id="f20b7-120">The following is an example message for a `QueryInterface` call on a COM-visible class `Derived` that derives from a non-COM-visible class `Base`.</span></span>  
  
```output
A QueryInterface call was made requesting the class interface of COM
visible managed class 'Derived'. However since this class derives from
non COM visible class 'Base', the QueryInterface call will fail. This
is done to prevent the non COM visible base class from being
constrained by the COM versioning rules.
```  
  
## <a name="configuration"></a><span data-ttu-id="f20b7-121">設定</span><span class="sxs-lookup"><span data-stu-id="f20b7-121">Configuration</span></span>  
  
```xml  
<mdaConfig>  
  <assistants>  
    <nonComVisibleBaseClass />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a><span data-ttu-id="f20b7-122">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f20b7-122">See also</span></span>

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [<span data-ttu-id="f20b7-123">診斷 Managed 偵錯助理的錯誤</span><span class="sxs-lookup"><span data-stu-id="f20b7-123">Diagnosing Errors with Managed Debugging Assistants</span></span>](diagnosing-errors-with-managed-debugging-assistants.md)
- [<span data-ttu-id="f20b7-124">Interop 封送處理</span><span class="sxs-lookup"><span data-stu-id="f20b7-124">Interop Marshaling</span></span>](../interop/interop-marshaling.md)
