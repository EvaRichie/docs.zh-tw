---
title: disconnectedContext MDA
description: 請參閱 .NET 中的 disconnectedCoNtext managed 偵錯工具，它是在 CLR 嘗試轉換成中斷連接的單元或內容時叫用。
ms.date: 03/30/2017
helpviewer_keywords:
- DisconnectedContext MDA
- MDAs (managed debugging assistants), disconnected context
- dead context
- transitioning disconnected apartment or context
- context disconnections
- managed debugging assistants (MDAs), disconnected context
ms.assetid: 1887d31d-7006-4491-93b3-68fd5b05f71d
ms.openlocfilehash: 0b24aadefab7a7cb2a5294f25e674d188beec814
ms.sourcegitcommit: a2c8b19e813a52b91facbb5d7e3c062c7188b457
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85416079"
---
# <a name="disconnectedcontext-mda"></a>disconnectedContext MDA
如果 CLR 在服務有關 COM 物件的要求時，試圖轉換至中斷連接的 Apartment 或內容，就會啟動 `disconnectedContext` Managed 偵錯助理 (MDA)。  
  
## <a name="symptoms"></a>徵狀  
 在[執行階段可呼叫包裝函式](../../standard/native-interop/runtime-callable-wrapper.md) (RCW) 上執行的呼叫會傳遞至目前 Apartment 或內容中的基礎 COM 元件，而不是其所在的 Apartment 或內容中。 如果 COM 元件不是多執行緒，這可能會導致損毀及/或資料遺失，就像在單一執行緒 Apartment (STA) 元件的案例一樣。 或者，如果 RCW 本身是 Proxy，則呼叫可能會導致擲回 <xref:System.Runtime.InteropServices.COMException>，且 HRESULT 為 RPC_E_WRONG_THREAD。  
  
## <a name="cause"></a>原因  
 當 CLR 試圖轉換至 OLE Apartment 或內容時，其已關閉。 最常見的原因，就是在 Apartment 擁有的所有 COM 元件都完成發行之前，STA Apartment 即已關閉。從 RCW 上的使用者程式碼進行明確呼叫，或是 CLR 本身在操作 COM 元件時，就可能會導致這種情況發生，例如當相關聯的 RCW 已進行記憶體回收，而 CLR 還在發行 COM 元件時。  
  
## <a name="resolution"></a>解決方案  
 若要避免此問題，請確定在應用程式完成 Apartment 中留存的所有物件之前，擁有 STA 的執行緒不會終止。 對內容也是套用一樣的方式；請確定在應用程式完成內容中留存的任何 COM 元件之前，內容未關閉。  
  
## <a name="effect-on-the-runtime"></a>對執行階段的影響  
 此 MDA 對 CLR 沒有影響。 它只會提報中斷連接之內容的相關資料。  
  
## <a name="output"></a>輸出  
 提報中斷連接的 Apartment 或內容的內容 Cookie。  
  
## <a name="configuration"></a>設定  
  
```xml  
<mdaConfig>  
  <assistants>  
    <disconnectedContext />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [使用 Managed 偵錯助理診斷錯誤](diagnosing-errors-with-managed-debugging-assistants.md)
- [Interop 封送處理](../interop/interop-marshaling.md)
