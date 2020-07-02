---
title: nonComVisibleBaseClass MDA
description: 請參閱 nonComVisibleBaseClass managed 偵錯工具（MDA），這是從機器碼的 QueryInterface 呼叫所叫用，而此輔助程式會因 COR_E_INVALIDOPERATION 而失敗。
ms.date: 03/30/2017
helpviewer_keywords:
- visible classes
- managed debugging assistants (MDAs), COM visible classes
- nonComVisibleBaseClass MDA
- COM visible classes
- QueryInterface call failures
- MDAs (managed debugging assistants), COM visible classes
ms.assetid: 9ec1af27-604b-477e-9ee2-e833eb10d3ce
ms.openlocfilehash: 9f32b2c57f50fcd900b1fd78f4f8df1ec656a6db
ms.sourcegitcommit: c23d9666ec75b91741da43ee3d91c317d68c7327
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85803912"
---
# <a name="noncomvisiblebaseclass-mda"></a>nonComVisibleBaseClass MDA
在由 COM 可見 Managed 類別 (衍生自不是 COM 可見的基底類別) 的可呼叫包裝函式 (CCW) 上的原生或 Unmanaged 程式碼呼叫 `QueryInterface` 時，會啟動 `nonComVisibleBaseClass` Managed 偵錯助理 (MDA)。  `QueryInterface` 呼叫會導致只有在呼叫要求類別介面或預設 COM 可見 Managed 類別的 `IDispatch` 情況下才啟用 MDA。  當 `QueryInterface` 是套用 <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> 屬性且會由 COM 可見的類別明確實作的明確介面時，則不啟動 MDA。  
  
## <a name="symptoms"></a>徵狀  
 `QueryInterface` 會由使用 COR_E_INVALIDOPERATION HRESULT 失敗的原生程式碼所呼叫。  HRESULT 可能是因為執行階段不允許會導致此 MDA 啟動的 `QueryInterface` 呼叫。  
  
## <a name="cause"></a>原因  
 執行階段不允許 `QueryInterface` 呼叫類別介面，或呼叫 COM 可見類別 (因潛在的版本控制問題而衍生自不是 COM 可見的類別) 之預設 `IDispatch` 介面。  例如，如果加入任何公用成員至不是 COM 可見的基底類別時，則可能會中斷現有使用衍生類別的 COM 用戶端，因為這類變更可能會更改此衍生類別的 vtable ，其中包含基底類別成員。  公開給 COM 的明確介面並沒有這個問題，因為在 vtable 中不包含介面的基底成員。  
  
## <a name="resolution"></a>解決方案  
 不要公開類別介面。 定義明確的介面，並套用 <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> 屬性。  
  
## <a name="effect-on-the-runtime"></a>對執行階段的影響  
 此 MDA 對 CLR 沒有影響。  
  
## <a name="output"></a>輸出  
 下列是在 COM 可見類別 `Derived` (衍生自不是 COM 可見的類別 `Base` ) 上呼叫 `QueryInterface` 的範例訊息。  
  
```output
A QueryInterface call was made requesting the class interface of COM
visible managed class 'Derived'. However since this class derives from
non COM visible class 'Base', the QueryInterface call will fail. This
is done to prevent the non COM visible base class from being
constrained by the COM versioning rules.
```  
  
## <a name="configuration"></a>組態  
  
```xml  
<mdaConfig>  
  <assistants>  
    <nonComVisibleBaseClass />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [使用 Managed 偵錯助理診斷錯誤](diagnosing-errors-with-managed-debugging-assistants.md)
- [Interop 封送處理](../interop/interop-marshaling.md)
