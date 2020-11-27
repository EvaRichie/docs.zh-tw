---
title: invalidGCHandleCookie MDA
description: 請參閱 invalidGCHandleCookie managed 偵錯工具 (MDA) ，這會在嘗試從無效 IntPtr cookie 轉換成 GCHandle 時啟用。
ms.date: 03/30/2017
helpviewer_keywords:
- MDAs (managed debugging assistants), invalid cookies
- cookies, invalid
- managed debugging assistants (MDAs), invalid cookies
- InvalidGCHandleCookie MDA
- invalid cookies
ms.assetid: 613ad742-3c11-401d-a6b3-893ceb8de4f8
ms.openlocfilehash: 36806498445da78c8d9dd5c51c1903b253a39da0
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96272601"
---
# <a name="invalidgchandlecookie-mda"></a>invalidGCHandleCookie MDA

當嘗試從無效的 <xref:System.IntPtr> Cookie 轉換成 <xref:System.Runtime.InteropServices.GCHandle> 時，就會啟動 `invalidGCHandleCookie` Managed 偵錯助理 (MDA)。  
  
## <a name="symptoms"></a>徵狀  

 未定義的行為，例如嘗試使用或擷取 <xref:System.IntPtr> 的 <xref:System.Runtime.InteropServices.GCHandle> 時的存取違規與記憶體損毀。  
  
## <a name="cause"></a>原因  

 Cookie 可能無效，因為它原本不是從代表已經釋放之 <xref:System.Runtime.InteropServices.GCHandle> 的 <xref:System.Runtime.InteropServices.GCHandle> 中建立的，它是不同應用程式網域中之 <xref:System.Runtime.InteropServices.GCHandle> 的 Cookie，或曾封送處理到原生程式碼當成 <xref:System.Runtime.InteropServices.GCHandle>，但傳遞回 CLR 當成在其中嘗試轉型的 <xref:System.IntPtr>，。  
  
## <a name="resolution"></a>解決方法  

 為 <xref:System.Runtime.InteropServices.GCHandle> 指定有效的 <xref:System.IntPtr> Cookie。  
  
## <a name="effect-on-the-runtime"></a>對執行階段的影響  

 啟用此 MDA 時，偵錯工具即不再能夠追蹤回其物件的根，因為傳回的 Cookie 值和未啟用 MDA 時傳回的 Cookie 值不同。  
  
## <a name="output"></a>輸出  

 已報告無效的 <xref:System.IntPtr> Cookie 值。  
  
## <a name="configuration"></a>設定  
  
```xml  
<mdaConfig>  
  <assistants>  
    <invalidGCHandleCookie />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Runtime.InteropServices.GCHandle.FromIntPtr%2A>
- <xref:System.Runtime.InteropServices.GCHandle>
- [診斷 Managed 偵錯助理的錯誤](diagnosing-errors-with-managed-debugging-assistants.md)
