---
title: fatalExecutionEngineError MDA
description: 請參閱 .NET 中的 fatalExecutionEngineError managed 偵錯工具 (MDA) ，因為未預期的進程終止，可能會啟用此功能。
ms.date: 03/30/2017
helpviewer_keywords:
- corrupted CLR
- fatal execution error
- terminated processes
- unexpected terminations
- fatal errors
- MDAs (managed debugging assistants), fatal errors
- process termination
- FatalExecutionEngineError MDA
- managed debugging assistants (MDAs), fatal errors
ms.assetid: 8b559e44-2393-4e4e-8160-7558d37a4a89
ms.openlocfilehash: a9347338d53755b74b3ff291f75cb6b221134130
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96244271"
---
# <a name="fatalexecutionengineerror-mda"></a>fatalExecutionEngineError MDA

在 Common Language Runtime (CLR) 中偵測到嚴重錯誤時，就會啟動 `fatalExecutionEngineError` Managed 偵錯助理 (MDA)。 處理程序會終止。  
  
## <a name="symptoms"></a>徵狀  

 未預期的處理序終止。 因為 CLR 失敗的發生原因各種各樣，所以無法判斷其他症狀。  
  
## <a name="cause"></a>原因  

 CLR 已受創損毀。 這通常是因為資料損毀所致，造成此狀況的問題很多，例如呼叫格式不正確的平台叫用函式，以及將無效的資料傳遞至 CLR。  
  
## <a name="resolution"></a>解決方法  

 啟用額外的 MDA 可能有助於找出問題。 下列 MDA 在診斷此問題方面特別有幫助：  
  
- [invalidOverlappedToPinvoke](invalidoverlappedtopinvoke-mda.md)  
  
- [overlappedFreeError](overlappedfreeerror-mda.md)  
  
- [pInvokeStackImbalance](pinvokestackimbalance-mda.md)  
  
- [gcUnmanagedToManaged](gcunmanagedtomanaged-mda.md)  
  
- [gcManagedToUnmanaged](gcmanagedtounmanaged-mda.md)  
  
- [callbackOnCollectedDelegate](callbackoncollecteddelegate-mda.md)  
  
- [reportAvOnComRelease](reportavoncomrelease-mda.md)  
  
- [invalidVariant](invalidvariant-mda.md)  
  
- [invalidIUnknown](invalidiunknown-mda.md)  
  
- [raceOnRCWCleanup](raceonrcwcleanup-mda.md)  
  
- [invalidFunctionPointerInDelegate](invalidfunctionpointerindelegate-mda.md)  
  
- [invalidGCHandleCookie](invalidgchandlecookie-mda.md)  
  
## <a name="effect-on-the-runtime"></a>對執行階段的影響  

 此 MDA 對執行階段行為沒有影響。  
  
## <a name="output"></a>輸出  

 造成嚴重錯誤的 CLR 函式位址、發生錯誤的執行緒識別碼，以及錯誤碼。  
  
## <a name="configuration"></a>設定  
  
```xml  
<mdaConfig>  
  <assistants>  
    <fatalExecutionEngineError />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareMethod%2A>
- <xref:System.Runtime.ConstrainedExecution.Cer>
- [診斷 Managed 偵錯助理的錯誤](diagnosing-errors-with-managed-debugging-assistants.md)
