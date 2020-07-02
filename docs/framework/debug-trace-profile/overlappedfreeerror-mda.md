---
title: overlappedFreeError MDA
description: 請參閱 .NET 中的 overlappedFreeError managed 偵錯工具（MDA），這可能會在存取違規或垃圾收集堆積發生損毀時啟用。
ms.date: 03/30/2017
helpviewer_keywords:
- OverlappedFreeError MDA
- overlapped free method call error
- managed debugging assistants (MDAs), overlapped structures
- overlapped structures
- MDAs (managed debugging assistants), overlapped structures
- freeing overlapped structures
ms.assetid: b6ab2d48-6eee-4bab-97a3-046b3b0a5470
ms.openlocfilehash: 9be33c59723ecb2743f2bc610d7fb69d24ff388c
ms.sourcegitcommit: c23d9666ec75b91741da43ee3d91c317d68c7327
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85803908"
---
# <a name="overlappedfreeerror-mda"></a>overlappedFreeError MDA
重疊作業完成之前，呼叫 <xref:System.Threading.Overlapped.Free%28System.Threading.NativeOverlapped%2A%29?displayProperty=nameWithType> 方法時，會啟用 `overlappedFreeError` Managed 偵錯助理 (MDA)。  
  
## <a name="symptoms"></a>徵狀  
 已進行記憶體回收之堆積的存取違規或損毀。  
  
## <a name="cause"></a>原因  
 作業完成之前，已釋放重疊結構。 使用重疊指標的函式稍後可能會在釋出之後寫入結構中。 這可能會造成堆積損毀，因為另一個物件現在可能會佔用該區域。  
  
 如果未成功啟動重疊的作業，則此 MDA 可能不會呈現錯誤。  
  
## <a name="resolution"></a>解決方案  
 請確定使用重疊結構的 I/O 作業完成，再呼叫 <xref:System.Threading.Overlapped.Free%28System.Threading.NativeOverlapped%2A%29> 方法。  
  
## <a name="effect-on-the-runtime"></a>對執行階段的影響  
 此 MDA 對 CLR 沒有影響。  
  
## <a name="output"></a>輸出  
 以下是此 MDA 的範例輸出。  
  
 `An overlapped pointer (0x00ea3430) that was not allocated on the GC heap was passed via Pinvoke to the win32 function 'WriteFile' in module 'KERNEL32.DLL'. If the AppDomain is shut down, this can cause heap corruption when the async I/O completes. The best solution is to pass a NativeOverlappedStructure retrieved from a call to System.Threading.Overlapped.Pack(). If the AppDomain exits, the CLR will keep this structure alive and pinned until the I/O completes.`  
  
## <a name="configuration"></a>組態  
  
```xml  
<mdaConfig>  
  <assistants>  
    <overlappedFreeError/>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [使用 Managed 偵錯助理診斷錯誤](diagnosing-errors-with-managed-debugging-assistants.md)
- [Interop 封送處理](../interop/interop-marshaling.md)
