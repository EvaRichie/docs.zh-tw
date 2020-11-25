---
title: 設定程式碼剖析環境
ms.date: 03/30/2017
helpviewer_keywords:
- environment variables, profiling API
- profiling API [.NET Framework], setting up environment
- COR_PROFILER environment variable
- Windows Service applications, profiling
- profiling API [.NET Framework], Windows Service applications
- COR_ENABLE_PROFILING environment variable
- profiling API [.NET Framework], enabling
ms.assetid: fefca07f-7555-4e77-be86-3c542e928312
ms.openlocfilehash: 9c712c5efe8d6d79454b70d0bf4f3ca2fa83b637
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95722475"
---
# <a name="setting-up-a-profiling-environment"></a>設定程式碼剖析環境

> [!NOTE]
> 在 .NET Framework 4 中，分析已有大量的變更。  
  
 當 Managed 處理序 (應用程式或服務) 啟動時，會載入 Common Language Runtime (CLR)。 初始化 CLR 時，會評估下列兩個環境變數來決定程序是否應該連接至程式碼剖析工具：  
  
- COR_ENABLE_PROFILING：只有在此環境變數存在，而且設為 1 時，CLR 才會連接到程式碼剖析工具。  
  
- COR_PROFILER：若 COR_ENABLE_PROFILING 檢查都通過，則 CLR 會連接到具有此 CLSID 或 ProgID 的程式碼剖析工具，該工具必須先前已儲存在登錄中。 將 COR_PROFILER 環境變數定義為字串，如下列兩個範例所示。  
  
    ```cpp  
    set COR_PROFILER={32E2F4DA-1BEA-47ea-88F9-C5DAF691C94A}  
    set COR_PROFILER="MyProfiler"  
    ```  
  
 若要分析 CLR 應用程式，您必須先設定 COR_ENABLE_PROFILING 和 COR_PROFILER 環境變數，才能執行應用程式。 您也必須確認已註冊程式碼剖析工具 DLL。  
  
> [!NOTE]
> 從 .NET Framework 4 開始，不需要註冊分析工具。  
  
> [!NOTE]
> 若要在 .NET Framework 4 和更新版本中使用 .NET Framework 版本2.0、3.0 和3.5 分析工具，您必須設定 COMPLUS_ProfAPI_ProfilerCompatibilitySetting 的環境變數。  
  
## <a name="environment-variable-scope"></a>環境變數範圍  

 您設定 COR_ENABLE_PROFILING 和 COR_PROFILER 環境變數的方式將會決定其影響範圍。 您可以使用下列其中一種方式來設定這些變數：  
  
- 如果您在 [ICorDebug：： CreateProcess](../debugging/icordebug-createprocess-method.md) 呼叫中設定變數，它們只會套用到您當時執行的應用程式。 (它們也會套用到繼承此環境之應用程式所啟動的其他應用程式。)  
  
- 如果您在 [命令提示字元] 視窗中設定變數，則變數會套用到從該視窗啟動的所有應用程式。  
  
- 如果您在使用者層次上設定變數，它們會套用至您使用 [檔案總管] 啟動的所有應用程式。 您在設定變數之後所開啟的 [命令提示字元] 視窗中會有這些環境設定，您從該視窗所啟動的任何應用程式也是。 若要在使用者層級設定環境變數，請以滑鼠右鍵按一下 [ **我的電腦**，按一下 [ **屬性**]，按一下 [ **Advanced** ] 索引標籤，按一下 [ **環境變數**]，然後將變數新增至 [ **使用者變數** ] 清單。  
  
- 如果您在電腦層級設定變數，變數會套用到該電腦啟動的所有應用程式。 您在該電腦開啟的 [命令提示字元] 視窗會有這些環境設定，從該視窗啟動的任何應用程式也是。 這表示在該電腦上的每個 Managed 處理序將以您的程式碼剖析工具做為起始。 若要在電腦層級設定環境變數，請在 [ **我的電腦**] **上按一下滑鼠** 右鍵，按一下 [內容]，按一下 [ **Advanced** ] 索引標籤，按一下 [ **環境變數**]，將變數新增至 **系統變數** 清單，然後重新開機電腦。 重新啟動後，變數就可供系統範圍使用。  
  
 如果您正在程式碼剖析 Windows 服務，您必須在設定環境變數及註冊程式碼剖析工具 DLL 之後重新啟動電腦。 如需有關這些考慮的詳細資訊，請參閱程式碼 [剖析 Windows 服務](#windows_service)一節。  
  
## <a name="additional-considerations"></a>其他考量  
  
- Profiler 類別會執行 [ICorProfilerCallback](icorprofilercallback-interface.md) 和 [ICorProfilerCallback2](icorprofilercallback2-interface.md) 介面。 在 .NET Framework 2.0 版中，程式碼剖析工具必須實作 `ICorProfilerCallback2`。 如果沒有實作，就不會載入 `ICorProfilerCallback2`。  
  
- 在指定環境中一次只能使用一個程式碼剖析工具來分析處理序。 您可以在不同環境中註冊兩個不同的程式碼剖析工具，但這兩個工具必須分析不同的處理序。 程式碼剖析工具必須實作為同處理序 COM 伺服器 DLL (其與剖析中之處理序的相同位址空間對應)。 這表示程式碼剖析工具執行同處理序。 .NET Framework 不支援任何其他類型的 COM 伺服器。 例如，如果程式碼剖析工具想要從遠端電腦監視應用程式，就必須在每一部電腦上實作收集器代理程式。 這些代理程式將會批次結果，並讓結果與中央資料收集電腦通訊。  
  
- 由於程式碼剖析工具是可具現化同處理序的 COM 物件，所以每個經剖析的應用程式會有自己的程式碼剖析工具複本。 因此，單一程式碼剖析工具執行個體不須處理來自多個應用程式的資料。 不過，您必須將邏輯加入程式碼剖析工具的記錄程式碼，以防止記錄檔從其他經剖析的應用程式覆寫。  
  
## <a name="initializing-the-profiler"></a>初始化程式碼剖析工具  

 當這兩個環境變數都檢查通過時，CLR 會以與 COM `CoCreateInstance` 函式類似的方式建立程式碼剖析工具的執行個體。 程式碼剖析工具不會透過直接呼叫載入至 `CoCreateInstance`。 因此會避免呼叫必須設定執行緒模型的 `CoInitialize`。 然後，CLR 會在分析工具中呼叫 [ICorProfilerCallback：： Initialize](icorprofilercallback-initialize-method.md) 方法。 這個方法的簽章如下所示。  
  
```cpp  
HRESULT Initialize(IUnknown *pICorProfilerInfoUnk)  
```  
  
 分析工具必須查詢 `pICorProfilerInfoUnk` [ICorProfilerInfo](icorprofilerinfo-interface.md) 或 [ICorProfilerInfo2](icorprofilerinfo2-interface.md) 介面指標，並加以儲存，以便稍後在分析期間要求更多資訊。  
  
## <a name="setting-event-notifications"></a>設定事件通知  

 分析工具接著會呼叫 [ICorProfilerInfo：： SetEventMask](icorprofilerinfo-seteventmask-method.md) 方法，以指定其感興趣的通知類別。 例如，如果程式碼剖析工具只對函式進入及離開通知和記憶體回收通知感興趣，會指定下列項目。  
  
```cpp  
ICorProfilerInfo* pInfo;  
pICorProfilerInfoUnk->QueryInterface(IID_ICorProfilerInfo, (void**)&pInfo);  
pInfo->SetEventMask(COR_PRF_MONITOR_ENTERLEAVE | COR_PRF_MONITOR_GC)  
```  
  
 藉由以這種方式設定通知遮罩，程式碼剖析工具可以限制所接收的通知。 這種方法可協助使用者建置簡單或特殊用途的程式碼剖析工具。 它也會減少浪費在程式碼剖析工具會略過之傳送通知的 CPU 時間。  
  
 某些程式碼剖析工具事件為不可變。 這表示，只要這些事件是在 `ICorProfilerCallback::Initialize` 回呼中設定，就無法關閉這些事件，也無法開啟新的事件。 嘗試變更不可變的事件將會導致 `ICorProfilerInfo::SetEventMask` 傳回失敗的 HRESULT。  
  
<a name="windows_service"></a>

## <a name="profiling-a-windows-service"></a>程式碼剖析 Windows 服務  

 程式碼剖析 Windows 服務就像是在程式碼剖析通用語言執行階段應用程式。 這兩種程式碼剖析作業皆會透過環境變數啟用。 因為作業系統啟動時會啟動 Windows 服務，所以本主題先前所討論的環境變數在系統啟動前必須存在並設為所需的值。 此外，程式碼剖析的 DLL 必須已登錄在系統上。  
  
 設定完 COR_ENABLE_PROFILING 和 COR_PROFILER 環境變數，並註冊分析工具 DLL 之後，應該重新啟動目標電腦，使 Windows 服務偵測到這些變更。  
  
 請注意這些變更將會啟用以系統範圍為基礎的程式碼剖析。 若要防止進行後續執行之所有 Managed 應用程式的程式碼剖析，您應該在重新啟動目標電腦之後刪除系統環境變數。  
  
 這項技術也會使每個 CLR 程序進行程式碼剖析。 分析工具應該將邏輯新增至其 [ICorProfilerCallback：： Initialize](icorprofilercallback-initialize-method.md) 回呼，以偵測目前的進程是否感興趣。 如果不是，程式碼剖析工具可以使回呼失敗，而不需執行初始化。  
  
## <a name="see-also"></a>另請參閱

- [分析概觀](profiling-overview.md)
