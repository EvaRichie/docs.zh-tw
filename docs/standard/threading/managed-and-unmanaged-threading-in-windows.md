---
title: Windows 中的 Managed 和 Unmanaged 執行緒處理
ms.date: 10/24/2018
elpviewer_keywords:
- threading [.NET], unmanaged
- threading [.NET], managed
- threading [.NET], managed
- threads and fibers [.NET]
- managed threading
ms.assetid: 4fb6452f-c071-420d-9e71-da16dee7a1eb
ms.openlocfilehash: 67d8fdb5f2e49930b25328c1dfd30a6105fd636f
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94826322"
---
# <a name="managed-and-unmanaged-threading-in-windows"></a>Windows 中的受控與非受控執行緒處理

所有執行緒的管理都會透過 <xref:System.Threading.Thread> 類別進行，包括 Common Language Runtime 建立的執行緒，以及在執行階段外部建立但進入 Managed 環境執行程式碼的執行緒。 執行階段會監視在其處理序中所有曾在 Managed 執行環境中執行程式碼的執行緒， 但不會追蹤其他任何執行緒。 執行緒可透過 COM Interop (因為執行階段會將 Managed 物件當做 COM 物件公開給 Unmanaged 世界)、COM [DllGetClassObject](/windows/desktop/api/combaseapi/nf-combaseapi-dllgetclassobject) 函式和平台叫用來進入 Managed 執行環境。  
  
 當 Unmanaged 執行緒透過類似 COM 可呼叫包裝函式來進入執行階段時，系統會檢查此執行緒的執行緒本機存放區，以尋找內部 Managed <xref:System.Threading.Thread> 物件。 如果找到一個物件，表示執行階段已感知此執行緒。 但是，如果找不到任何 <xref:System.Threading.Thread> 物件，執行階段會建置新物件並安裝到此執行緒的執行緒本機存放區中。  
  
 在 Managed 執行緒中， <xref:System.Threading.Thread.GetHashCode%2A?displayProperty=nameWithType> 是穩定的 Managed 執行緒識別。 在執行緒的存留期間，此值不會與其他任何執行緒的值相衝突，不論您是從哪一個應用程式定義域取得此值。  
  
## <a name="mapping-from-win32-threading-to-managed-threading"></a>從 Win32 執行緒處理對應至受控執行緒處理

 下表將 Win32 執行緒項目對應至其近似的執行階段對等項目。 請注意，此對應並不代表功能完全一樣。 例如，**TerminateThread** 不會執行 **finally** 子句或釋放資源，並且無法防止。 但是， <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> 會執行所有復原程式碼、回收所有資源，並且可使用 <xref:System.Threading.Thread.ResetAbort%2A>加以拒絕。 在揣測功能之前，請務必仔細閱讀相關文件。  
  
|在 Win32 中|在 Common Language Runtime 中|  
|--------------|------------------------------------|  
|**CreateThread**|**Thread** 和 <xref:System.Threading.ThreadStart>的組合|  
|**TerminateThread**|<xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType>|  
|**SuspendThread**|<xref:System.Threading.Thread.Suspend%2A?displayProperty=nameWithType>|  
|**ResumeThread**|<xref:System.Threading.Thread.Resume%2A?displayProperty=nameWithType>|  
|**睡眠**|<xref:System.Threading.Thread.Sleep%2A?displayProperty=nameWithType>|  
|執行緒控制代碼上的 **WaitForSingleObject**|<xref:System.Threading.Thread.Join%2A?displayProperty=nameWithType>|  
|**ExitThread**|沒有對等項目|  
|**GetCurrentThread**|<xref:System.Threading.Thread.CurrentThread%2A?displayProperty=nameWithType>|  
|**SetThreadPriority**|<xref:System.Threading.Thread.Priority%2A?displayProperty=nameWithType>|  
|沒有對等項目|<xref:System.Threading.Thread.Name%2A?displayProperty=nameWithType>|  
|沒有對等項目|<xref:System.Threading.Thread.IsBackground%2A?displayProperty=nameWithType>|  
|近似 **CoInitializeEx** (OLE32.DLL)|<xref:System.Threading.Thread.ApartmentState%2A?displayProperty=nameWithType>|  
  
## <a name="managed-threads-and-com-apartments"></a>受控執行緒與 COM Apartment

可標記 Managed 執行緒，以表示它將裝載[單一執行緒](/windows/desktop/com/single-threaded-apartments)或[多執行緒](/windows/desktop/com/multithreaded-apartments) Apartment。  (如需 COM 執行緒架構的詳細資訊，請參閱 [進程、執行緒和單元](/windows/desktop/com/processes--threads--and-apartments)。 ) 的 <xref:System.Threading.Thread.GetApartmentState%2A> 、 <xref:System.Threading.Thread.SetApartmentState%2A> 和方法會傳回 <xref:System.Threading.Thread.TrySetApartmentState%2A> <xref:System.Threading.Thread> 並指派執行緒的單元狀態。 如果尚未設定此狀態，則 <xref:System.Threading.Thread.GetApartmentState%2A> 會傳回 <xref:System.Threading.ApartmentState.Unknown?displayProperty=nameWithType>。  
  
 只有在執行緒處於 <xref:System.Threading.ThreadState.Unstarted?displayProperty=nameWithType> 狀態時，才能設定此屬性；每個執行緒只能設定此屬性一次。  
  
 如果啟動執行緒之前未設定 Apartment 狀態，則會將執行緒初始化為多執行緒 Apartment (MTA)。 受到 <xref:System.Threading.ThreadPool> 控制的完成項執行緒及所有執行緒都是 MTA。  
  
> [!IMPORTANT]
> 對於應用程式啟動程式碼而言，控制 Apartment 狀態的唯一方式是將 <xref:System.MTAThreadAttribute> 或 <xref:System.STAThreadAttribute> 套用至進入點程序。
  
 公開至 COM 之 Managed 物件的行為會像是已彙總無限制執行緒封送處理器。 換句話說，您可以使用無限制執行緒方式從任何 COM Apartment 呼叫 Managed 物件。 只有衍生自 <xref:System.EnterpriseServices.ServicedComponent> 或 <xref:System.Runtime.InteropServices.StandardOleMarshalObject> 的 Managed 物件才不會表現出無限制執行緒行為。  
  
 在 Managed 世界中，除非您使用內容及內容繫結 Managed 執行個體，否則不支援 <xref:System.Runtime.Remoting.Contexts.SynchronizationAttribute> 。 如果您正在使用 Enterprise Services，則您的物件必須衍生自 <xref:System.EnterpriseServices.ServicedComponent> (其本身係衍生自 <xref:System.ContextBoundObject>)。  
  
 當 Managed 程式碼呼叫 COM 物件時，一律會遵循 COM 規則。 換句話說，程式碼會依照 OLE32 指示，透過 COM Apartment Proxy 和 COM+ 1.0 內容包裝函式來呼叫。  
  
## <a name="blocking-issues"></a>封鎖問題  

如果執行緒對作業系統發出 Unmanaged 呼叫，而此呼叫在 Unmanaged 程式碼中封鎖了執行緒，則執行階段將不會針對 <xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType> 或 <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType>取得其控制權。 如果是 <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType>，執行階段會為 **Abort** 標記執行緒，並在它重新進入 Managed 程式碼時取得其控制權。 建議您使用 Managed 封鎖，而不要使用 Unmanaged 封鎖。 <xref:System.Threading.WaitHandle.WaitOne%2A?displayProperty=nameWithType>、<xref:System.Threading.WaitHandle.WaitAny%2A?displayProperty=nameWithType>, <xref:System.Threading.WaitHandle.WaitAll%2A?displayProperty=nameWithType>, <xref:System.Threading.Monitor.Enter%2A?displayProperty=nameWithType>, <xref:System.Threading.Monitor.TryEnter%2A?displayProperty=nameWithType>, <xref:System.Threading.Thread.Join%2A?displayProperty=nameWithType>, <xref:System.GC.WaitForPendingFinalizers%2A?displayProperty=nameWithType>等對於 <xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType> 和 <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType>都會有回應。 此外，如果執行緒位在單一執行緒 Apartment 中，則當執行緒被封鎖時，所有這些 Managed 封鎖作業都會正確提取 Apartment 中的訊息。  

## <a name="threads-and-fibers"></a>執行緒與 Fiber

.NET 執行緒模式不支援 [Fiber](/windows/desktop/procthread/fibers)。 您不應該呼叫至使用 Fiber 實作的任何非受控函式。 此類呼叫可能會導致 .NET 執行階段當掉。

## <a name="see-also"></a>另請參閱

- <xref:System.Threading.Thread.ApartmentState%2A?displayProperty=nameWithType>
- <xref:System.Threading.ThreadState>
- <xref:System.EnterpriseServices.ServicedComponent>
- <xref:System.Threading.Thread>
- <xref:System.Threading.Monitor>
