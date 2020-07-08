---
title: invalidOverlappedToPinvoke MDA
description: 請參閱 .NET 中的 invalidOverlappedToPinvoke managed 偵錯工具（MDA），這可能會在當機或無法解釋堆積損毀期間啟用。
ms.date: 03/30/2017
helpviewer_keywords:
- overlapped pointers
- managed debugging assistants (MDAs), overlapped pointers
- invalid overlapped pointer to platform invoke
- InvalidOverlappedToPinvoke MDA
- MDAs (managed debugging assistants), overlapped pointers
- pointers, overlapped
ms.assetid: 28876047-58bd-4fed-9452-c7da346d67c0
ms.openlocfilehash: 162efd55bf636cf2e8698706bd011379f2f6f11f
ms.sourcegitcommit: 0edbeb66d71b8df10fcb374cfca4d731b58ccdb2
ms.contentlocale: zh-TW
ms.lasthandoff: 07/07/2020
ms.locfileid: "86051697"
---
# <a name="invalidoverlappedtopinvoke-mda"></a>invalidOverlappedToPinvoke MDA
當不是在記憶體回收堆積上建立的重疊指標傳遞至特定的 Win32 函式時，就會啟動 `invalidOverlappedToPinvoke` Managed 偵錯助理 (MDA)。  
  
> [!NOTE]
> 根據預設，只有在程式碼中定義了平台叫用呼叫，而且偵錯工具報告每一個方法的 JustMyCode 狀態時，才會啟用這個 MDA。 不了解 JustMyCode (例如 MDbg.exe 沒有副檔名) 的偵錯工具，不會啟動此 MDA。 使用組態檔和在 .mda.config 檔案 `(<invalidOverlappedToPinvoke enable="true" justMyCode="false"/>`) 中明確設定 `justMyCode="false"`，可針對這些偵錯工具啟用此 MDA。  
  
## <a name="symptoms"></a>徵狀  
 當機或無法解釋的堆積損毀。  
  
## <a name="cause"></a>原因  
 不是在記憶體回收堆積建立的重疊指標，會傳遞給特定的作業系統函式。  
  
 下表會顯示這個 MDA 追蹤的函式。  
  
|模組|函式|  
|------------|--------------|  
|HttpApi.dll|`HttpReceiveHttpRequest`|  
|IpHlpApi.dll|`NotifyAddrChange`|  
|kernel32.dll|`ReadFile`|  
|kernel32.dll|`ReadFileEx`|  
|kernel32.dll|`WriteFile`|  
|kernel32.dll|`WriteFileEx`|  
|kernel32.dll|`ReadDirectoryChangesW`|  
|kernel32.dll|`PostQueuedCompletionStatus`|  
|MSWSock.dll|`ConnectEx`|  
|WS2_32.dll|`WSASend`|  
|WS2_32.dll|`WSASendTo`|  
|WS2_32.dll|`WSARecv`|  
|WS2_32.dll|`WSARecvFrom`|  
|MQRT.dll|`MQReceiveMessage`|  
  
 這種狀況的堆積損毀可能性很高，因為可能會卸載 <xref:System.AppDomain> 進行的呼叫。 如果 <xref:System.AppDomain> 卸載，則應用程式程式碼會釋放重疊指標的記憶體，在作業完成時導致損毀，或程式碼將流失記憶體，造成後來的問題。  
  
## <a name="resolution"></a>解決方案  
 使用 <xref:System.Threading.Overlapped> 物件，呼叫 <xref:System.Threading.Overlapped.Pack%2A> 方法以取得可以傳遞至函式的 <xref:System.Threading.NativeOverlapped> 結構。 如果 <xref:System.AppDomain> 卸載，CLR 會等到非同步作業完成後再釋放指標。  
  
## <a name="effect-on-the-runtime"></a>對執行階段的影響  
 此 MDA 以前對 CLR 沒有影響。  
  
## <a name="output"></a>輸出  
 以下是此 MDA 輸出的範例。  
  
 `An overlapped pointer (0x00ea3430) that was not allocated on the GC heap was passed via Pinvoke to the Win32 function 'WriteFile' in module 'KERNEL32.DLL'. If the AppDomain is shut down, this can cause heap corruption when the async I/O completes. The best solution is to pass a NativeOverlapped structure retrieved from a call to System.Threading.Overlapped.Pack(). If the AppDomain exits, the CLR will keep this structure alive and pinned until the I/O completes.`  
  
## <a name="configuration"></a>組態  
  
```xml  
<mdaConfig>  
  <assistants>  
    <invalidOverlappedToPinvoke/>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [使用 Managed 偵錯助理診斷錯誤](diagnosing-errors-with-managed-debugging-assistants.md)
- [Interop 封送處理](../interop/interop-marshaling.md)
