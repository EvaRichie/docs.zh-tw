---
title: invalidFunctionPointerInDelegate MDA
description: 檢查 invalidFunctionPointerInDelegate managed 偵錯工具 (MDA) ，如果傳入不正確函式指標以建立委派，則會叫用此功能。
ms.date: 03/30/2017
helpviewer_keywords:
- invalidFunctionPointerInDelegate MDA
- managed debugging assistants (MDAs), invalid function pointer to delegates
- MDAs (managed debugging assistants), invalid function pointer to delegates
- function pointers, invalid
- marshaling, run-time errors
- managed debugging assistants (MDAs), marshaling
- MDAs (managed debugging assistants), marshaling
- invalid function pointers
ms.assetid: 99ae44f1-783e-49a9-9009-24f54bbd0f09
ms.openlocfilehash: 8072d35a45cb1e0590aa5533210d0e0f86913164
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96272614"
---
# <a name="invalidfunctionpointerindelegate-mda"></a>invalidFunctionPointerInDelegate MDA

當無效的函式指標傳入，以建構取代原生函式指標的委派時，就會啟用 `invalidFunctionPointerInDelegate` Managed 偵錯助理 (MDA)。  
  
## <a name="symptoms"></a>徵狀  

 使用委派來取代函式指標時，發生存取違規或非預期的記憶體損毀。  
  
## <a name="cause"></a>原因  

 所指定的函式指標無效。  
  
## <a name="resolution"></a>解決方法  

 指定有效的函式指標  
  
## <a name="effect-on-the-runtime"></a>對執行階段的影響  

 此 MDA 對 CLR 沒有影響。  
  
## <a name="output"></a>輸出  

 無效的函式指標。  
  
## <a name="configuration"></a>設定  
  
```xml  
<mdaConfig>  
  <assistants>  
    <invalidFunctionPointerInDelegate />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [診斷 Managed 偵錯助理的錯誤](diagnosing-errors-with-managed-debugging-assistants.md)
- [Interop 封送處理](../interop/interop-marshaling.md)
