---
title: dirtyCastAndCallOnInterface MDA
description: 檢查 dirtyCastAndCallOnInterface managed 偵錯工具，這是在晚期繫結的類別介面上進行早期繫結的 vtable 呼叫時所叫用的協助工具。
ms.date: 03/30/2017
helpviewer_keywords:
- managed debugging assistants (MDAs), early bound calls AutoDispatch
- dispatch-only mode
- dirtyCastAndCallOnInterface
- early-bound managed classes
- early bound calls on AutoDispatch
- MDAs (managed debugging assistants), early bound calls AutoDispatch
- EarlyBoundCallOnAutorDispatchClassInteface MDA
ms.assetid: aa388ed3-7e3d-48ea-a0b5-c47ae19cec38
ms.openlocfilehash: 49a2930d91e76856436480512360e8b9f9fd3d7a
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96273577"
---
# <a name="dirtycastandcalloninterface-mda"></a>dirtyCastAndCallOnInterface MDA

在已標記為僅限晚期繫結的類別介面上，嘗試透過 vtable 進行早期繫結呼叫時，會啟動 `dirtyCastAndCallOnInterface` Managed 偵錯助理 (MDA)。  
  
## <a name="symptoms"></a>徵狀  

 將經由 COM 進行的早期繫結呼叫置入 CLR 時，應用程式會擲回存取違規或發生未預期的行為。  
  
## <a name="cause"></a>原因  

 程式碼嘗試經由僅限晚期繫結的類別介面，透過 vtable 進行早期繫結呼叫。 請注意，預設會將類別介面識別為僅限晚期繫結。 使用 <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> 屬性搭配 <xref:System.Runtime.InteropServices.ClassInterfaceType.AutoDispatch> 值 (`[ClassInterface(ClassInterfaceType.AutoDispatch)]`)，也可能將類別介面識別為晚期繫結。  
  
## <a name="resolution"></a>解決方法  

 建議的解決方式是定義明確介面以供 COM 使用，並讓 COM 用戶端透過這個介面 (而不是透過自動產生的類別介面) 進行呼叫。 或者，從 COM 的呼叫也可以轉換成經由 `IDispatch` 的晚期繫結程序呼叫。  
  
 最後，您可以將類別識別為 <xref:System.Runtime.InteropServices.ClassInterfaceType.AutoDual> (`[ClassInterface(ClassInterfaceType.AutoDual)]`)，以允許從 COM 發出早期繫結呼叫；不過由於 <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> 中所述的版本控制限制，強烈不建議使用 <xref:System.Runtime.InteropServices.ClassInterfaceType.AutoDual>。  
  
## <a name="effect-on-the-runtime"></a>對執行階段的影響  

 此 MDA 對 CLR 沒有影響。 它只會報告有關晚期繫結介面上之早期繫結呼叫的資料。  
  
## <a name="output"></a>輸出  

 以早期繫結存取之方法或欄位的名稱。  
  
## <a name="configuration"></a>設定  
  
```xml  
<mdaConfig>  
  <assistants>  
    <dirtyCastAndCallOnInterface />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Runtime.InteropServices.ClassInterfaceAttribute>
- [診斷 Managed 偵錯助理的錯誤](diagnosing-errors-with-managed-debugging-assistants.md)
