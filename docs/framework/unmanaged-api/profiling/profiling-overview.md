---
title: 分析概觀
ms.date: 03/30/2017
helpviewer_keywords:
- managed code, profiling API support
- unmanaged code, combining with managed code in profiling
- notification threads [.NET Framework profiling]
- unmanaged code, profiling
- profiling API [.NET Framework], and COM
- profiling API [.NET Framework], unmanaged code profiling
- profilers, writing
- profiling API [.NET Framework], call stacks
- code profilers, writing
- profiling API [.NET Framework], security considerations
- profiling API [.NET Framework], managed code support
- common language runtime, profiling
- profiling API [.NET Framework], notification threads
- call stacks [.NET Framework profiling]
- profiling API [.NET Framework], stack depth
- common language runtime, writing a profiler
- profiling API [.NET Framework], information retrieval interfaces
- shadow stacks [.NET Framework profiling]
- COM, using in the profiling API
- stack snapshots [.NET Framework profiling]
- profiling API [.NET Framework], supported features
- profiling API [.NET Framework], overview
- security, profiling API considerations
- stack depth [.NET Framework profiling]
ms.assetid: 864c2344-71dc-46f9-96b2-ed59fb6427a8
ms.openlocfilehash: cf29260c36437aaf679498f648d0fcac5d65f321
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90558325"
---
# <a name="profiling-overview"></a>分析概觀

分析工具是監視另一個應用程式執行狀況的工具。 Common Language Runtime (CLR) 分析工具是動態連結程式庫 (DLL) 由數個函式所組成，可使用分析 API，從 CLR 接收訊息，以及傳送訊息至 CLR。 CLR 會在執行階段載入分析工具 DLL。

傳統的分析工具著重在測量應用程式的執行。 也就是說，它們會測量花費在每個函式的時間，或是應用程式經過一段時間的記憶體使用量。 分析 API 的目標是更廣泛的診斷工具類別，例如程式碼涵蓋範圍公用程式，甚至進階偵錯輔助工具。 這些用途在本質上都是診斷。 分析 API 不僅會測量，也會監視應用程式的執行。 基於這個理由，應用程式本身應該永遠都不要使用分析 API，而且應用程式的執行不應該依賴分析工具 (或受其影響)。

分析 CLR 應用程式所需的支援，比依照慣例分析已編譯的機器碼更多。 這是因為 CLR 導入了下列概念：應用程式定義域、記憶體回收、Managed 例外狀況處理、程式碼的 Just-In-Time (JIT) 編譯 (將 Microsoft 中繼語言或 MSIL 程式碼轉換為原生機器碼) 之類的功能。 傳統分析機制無法識別或提供關於這些功能的有用資訊。 分析 API 有效地提供這項遺漏的資訊，而幾乎不會影響 CLR 和已分析之應用程式的效能。

執行階段的 JIT 編譯為分析提供很好的機會。 分析 API 可讓分析工具先變更常式的記憶體中 MSIL 程式碼資料流，再進行 JIT 編譯。 以這種方式，分析工具可以將檢測程式碼動態加入需要更深入調查的特定常式。 雖然這種方法在傳統案例中是可行的，但是使用分析 API 來為 CLR 實作會更加容易。

## <a name="the-profiling-api"></a>程式碼剖析 API

程式碼剖析 API 通常是用來撰寫程式 *代碼*分析工具，這是監視 managed 應用程式執行的程式。

分析工具 DLL 會使用分析 API，它會載入與所分析之應用程式相同的程序中。 分析工具 DLL 會在1.0 版和1.1 版中 ([ICorProfilerCallback](icorprofilercallback-interface.md) ，在2.0 版和更新版本 .NET Framework 的 [ICorProfilerCallback2](icorprofilercallback2-interface.md) 中，) 中執行回呼介面。 CLR 會在該介面中呼叫方法，以通知分析工具所分析之程序中的事件。 分析工具可以使用 [ICorProfilerInfo](icorprofilerinfo-interface.md) 和 [ICorProfilerInfo2](icorprofilerinfo2-interface.md) 介面中的方法回呼回執行時間，以取得已分析之應用程式狀態的相關資訊。

> [!NOTE]
> 只有分析工具解決方案的資料蒐集部分，應該要在與所分析之應用程式相同的程序中執行。 所有使用者介面和資料分析都應該在分開的處理序中執行。

下圖顯示分析工具 DLL 如何與正在分析的應用程式和 CLR 互動。

![顯示程式碼剖析架構的螢幕擷取畫面。](./media/profiling-overview/profiling-architecture.png)

### <a name="the-notification-interfaces"></a>通知介面

[ICorProfilerCallback](icorprofilercallback-interface.md) 和 [ICorProfilerCallback2](icorprofilercallback2-interface.md) 可視為通知介面。 這些介面包含 [ClassLoadStarted](icorprofilercallback-classloadstarted-method.md)、 [ClassLoadFinished](icorprofilercallback-classloadfinished-method.md)和 [JITCompilationStarted](icorprofilercallback-jitcompilationstarted-method.md)之類的方法。 每當 CLR 載入或卸載類別、編譯函式等等，都會在分析工具的 `ICorProfilerCallback` 或 `ICorProfilerCallback2` 介面上呼叫對應的方法。

例如，分析工具可以透過兩個通知函式來測量程式碼效能： [FunctionEnter2](functionenter2-function.md) 和 [FunctionLeave2](functionleave2-function.md)。 它會即時戳記每個通知、彙總結果，並輸出一個清單，指出在應用程式執行期間，哪些函式耗用最多 CPU 或時鐘時間。

### <a name="the-information-retrieval-interfaces"></a>資訊擷取介面

與分析相關的其他主要介面為 [ICorProfilerInfo](icorprofilerinfo-interface.md) 和 [ICorProfilerInfo2](icorprofilerinfo2-interface.md)。 分析工具會視需要呼叫這些介面，以取得更多資訊來協助進行分析。 例如，每當 CLR 呼叫 [FunctionEnter2](functionenter2-function.md) 函式時，它就會提供函數識別碼。 分析工具可以呼叫 [ICorProfilerInfo2：： GetFunctionInfo2](icorprofilerinfo2-getfunctioninfo2-method.md) 方法來取得該函式的詳細資訊，以探索函式的父類別、其名稱等等。

## <a name="supported-features"></a>支援的功能

分析 API 會提供 Common Language Runtime 中發生之各種事件和動作的相關資訊。 您可以使用這項資訊來監視處理序的內部運作方式，以及分析 .NET Framework 應用程式的效能。

分析 API 會擷取 CLR 中發生之下列動作和事件的相關資訊：

- CLR 啟動和關閉事件。

- 應用程式定義域建立和關閉事件。

- 組件載入與卸載事件。

- 模組載入與卸載事件。

- COM vtable 建立和解構事件。

- Just-In-Time (JIT) 編譯和 code-pitching 事件。

- 類別載入和卸載事件。

- 執行緒建立和解構事件。

- 函式進入和結束事件。

- 例外狀況。

- Managed 和 Unmanaged 程式碼執行之間的轉換。

- 不同執行階段內容之間的轉換。

- 執行階段暫止的相關資訊。

- 執行階段記憶體堆積和記憶體回收活動的相關資訊。

您可以從任何 (非 Managed) COM 相容語言呼叫分析 API 。

在 CPU 和記憶體耗用量方面，此 API 很有效率。 分析並不會對所分析的應用程式造成足以誤導結果的變更。

分析 API 對取樣和非取樣分析工具都非常有用。 *取樣*分析工具會定期檢查設定檔（例如，在5毫秒內）。 *非取樣*分析工具會與引發事件的執行緒同步通知事件。

### <a name="unsupported-functionality"></a>不支援的功能

分析 API 不支援下列功能：

- Unmanaged 程式碼，這必須使用傳統 Win32 方法來分析。 不過，CLR 分析工具包含轉換事件，可判斷 Managed 與 Unmanaged 程式碼之間的界限。

- 自我修改的應用程式，它會針對外觀導向程式設計之類的目的，修改自己的程式碼。

- 繫結檢查，因為分析 API 並未提供這項資訊。 CLR 為所有 Managed 程式碼的繫結檢查提供內建支援。

- 遠端分析，不支援的原因如下：

  - 遠端分析會延長執行時間。 當您使用分析介面時，您必須盡量減少執行時間，使分析結果不要受到過度影響。 當執行效能受到監視時，特別是這樣。 不過，使用分析介面來監視記憶體使用量，或取得有關堆疊框架、物件等等的執行階段資訊時，遠端分析並不是個限制。

  - CLR 程式碼分析工具必須向執行所分析應用程式之本機電腦上的執行階段，註冊一個或多個回呼介面。 這會限制建立遠端程式碼分析工具的能力。

## <a name="notification-threads"></a>通知執行緒

在大部分情況下，產生事件的執行緒也會執行通知。 這類通知 (例如， [FunctionEnter](functionenter-function.md) 和 [FunctionLeave](functionleave-function.md)) 不需要提供明確的 `ThreadID` 。 此外，根據受影響執行緒的 `ThreadID`，分析工具可能會決定使用執行緒區域儲存區來儲存和更新其分析區塊，而不是在全域儲存體中將分析區塊編製索引。

請注意，這些回呼不會序列化。 使用者必須藉由下列方式保護他們的程式碼：建立執行緒安全資料結構，並且鎖定分析工具程式碼，進而防止從多個執行緒進行平行存取。 因此，在某些情況下，您會收到不尋常的回呼序列。 例如，假設 Managed 應用程式正在繁衍兩個正在執行相同程式碼的執行緒。 在這種情況下，您可能會在[ICorProfilerCallback::JITCompilationStarted](icorprofilercallback-jitcompilationstarted-method.md)收到 `FunctionEnter` [ICorProfilerCallback：： JITCompilationFinished](icorprofilercallback-jitcompilationfinished-method.md)回呼之前，從一個執行緒接收某個函式的 ICorProfilerCallback：： JITCompilationStarted 事件，並從另一個執行緒接收回呼。 在此情況下，使用者將會因為可能尚未完全 Just-In-Time (JIT) 編譯的函式，而收到 `FunctionEnter` 回呼。

## <a name="security"></a>安全性

分析工具 DLL 是 Unmanaged 的 DLL，它會當做 Common Language Runtime 執行引擎的一部分來執行。 因此，分析工具 DLL 中的程式碼不受 Managed 程式碼存取安全性的限制。 分析工具 DLL 的唯一限制，只有作業系統針對執行所分析應用程式的使用者施加的那些限制。

分析工具作者應該採取適當的預防措施，以避免安全性相關問題。 例如，在安裝期間，應該將分析工具 DLL 加入存取控制清單 (ACL)，如此惡意使用者就無法加以修改。

## <a name="combining-managed-and-unmanaged-code-in-a-code-profiler"></a>將 Managed 和 Unmanaged 程式碼合併在程式碼分析工具中

撰寫不正確的分析工具可能會造成對本身循環參考，導致無法預期的行為。

檢閱 CLR 分析 API 可能會造成一個印象，認為您可以撰寫一個分析工具，其中包含 Managed 和 Unmanaged 元件，而它們可以透過 COM Interop 或間接呼叫來彼此呼叫。

雖然從設計的觀點來看，這是可行的，但是分析 API 並不支援 Managed 元件。 CLR 分析工具必須是完全 Unmanaged。 嘗試將 Managed 和 Unmanaged 程式碼結合在 CLR 分析工具中，可能會造成存取違規、程式失敗或死結。 分析工具的 Managed 元件會引發事件回到其 Unmanaged 元件，Unmanaged 元件接著又會呼叫 Managed 的元件，而導致循環參考。

CLR 分析工具可以安全呼叫 Managed 程式碼的唯一位置，是在方法的 Microsoft 中繼語言 (MSIL) 主體中。 修改 MSIL 主體的建議作法是在 [ICorProfilerCallback4](icorprofilercallback4-interface.md) 介面中使用 JIT 重新編譯方法。

另外也可以使用較舊的檢測方法修改 MSIL。 在即時 (JIT) 函式的編譯完成之前，分析工具可以在方法的 MSIL 主體中插入 managed 呼叫，然後再進行 JIT 編譯 (請參閱 [ICorProfilerInfo：： GetILFunctionBody](icorprofilerinfo-getilfunctionbody-method.md) 方法) 。 這項技術可以成功用於選擇性的 Managed 程式碼檢測，或是用來收集 JIT 的相關統計資料和效能資料。

或者，程式碼分析工具在呼叫 Unmanaged 程式碼之每個 Managed 函式的 MSIL 主體中，插入原生攔截程序。 這項技術可以用於檢測和涵蓋範圍。 例如，程式碼分析工具可以在每個 MSIL 區塊後面，插入檢測攔截程序，以確保該區塊已被執行。 方法的 MSIL 主體修改是非常精細的作業，而且有許多應該列入考量的因素。

## <a name="profiling-unmanaged-code"></a>分析 Unmanaged 程式碼

Common Language Runtime (CLR) 分析 API 為分析 Unmanaged 程式碼提供最小支援。 提供下列功能：

- 堆疊鏈結的列舉。 這項功能可讓程式碼分析工具判斷 Managed 程式碼與 Unmanaged 程式碼之間的界限。

- 判斷堆疊鏈結是對應至 Managed 程式碼或原生程式碼。

在 .NET Framework 1.0 和 1.1 版中，這些方法可用於 CLR 偵錯 API 的整個同處理序子集。 其定義在 CorDebug.idl 檔案中。

在 .NET Framework 2.0 和更新版本中，您可以針對這項功能使用 [ICorProfilerInfo2：:D ostacksnapshot](icorprofilerinfo2-dostacksnapshot-method.md) 方法。

## <a name="using-com"></a>使用 COM

雖然分析介面被定義為 COM 介面，但是 Common Language Runtime (CLR) 並不會實際初始化 COM 來使用這些介面。 原因是為了避免在 managed 應用程式有機會指定其所需的執行緒模型之前，使用 [CoInitialize](/windows/desktop/api/objbase/nf-objbase-coinitialize) 函數來設定執行緒模型。 同樣地，分析工具本身也不應該呼叫 `CoInitialize`，因為它所選擇的執行緒模型可能會與正在分析的應用程式不相容，而導致應用程式失敗。

## <a name="call-stacks"></a>呼叫堆疊

分析 API 提供兩種取得呼叫堆疊的方式：堆疊快照方法，可啟用呼叫堆疊的疏鬆收集；以及陰影堆疊方法，可追蹤每個時刻的呼叫堆疊。

### <a name="stack-snapshot"></a>堆疊快照

堆疊快照是執行緒堆疊的即時追蹤。 分析 API 支援追蹤堆疊上的 Managed 函式，但會將 Unmanaged 函式的追蹤交由分析工具本身的堆疊查核器處理。

如需如何設計程式碼剖析工具以逐步執行 managed 堆疊的詳細資訊，請參閱此檔集中的 [ICorProfilerInfo2：:D ostacksnapshot](icorprofilerinfo2-dostacksnapshot-method.md) 方法，以及分析工具 [堆疊 .NET Framework 2.0：基本概念和更](/previous-versions/dotnet/articles/bb264782(v=msdn.10))高範圍的逐步解說。

### <a name="shadow-stack"></a>陰影堆疊

過於頻繁使用快照方法，很快就會產生效能問題。 如果您想要頻繁地取得堆疊追蹤，您的分析工具應該改為使用 [FunctionEnter2](functionenter2-function.md)、 [FunctionLeave2](functionleave2-function.md)、 [FunctionTailcall2](functiontailcall2-function.md)和 [ICorProfilerCallback2](icorprofilercallback2-interface.md) 例外狀況回呼來建立陰影堆疊。 每當需要堆疊快照時，陰影堆疊一定都是當前的，而且可以快速複製到儲存體。

陰影堆疊可能會取得函式引數、傳回值，以及泛型具現化的相關資訊。 此資訊只能透過陰影堆疊來使用，並且可以在將控制權交給函式時取得。 不過，之後在函式執行期間，可能無法使用這項資訊。

## <a name="callbacks-and-stack-depth"></a>回呼和堆疊深度

分析工具回呼可能會在堆疊極為受限的情況下發出，而分析工具回呼中的堆疊溢位將會導致處理序立即結束。 分析工具在回應回呼，應該要確保儘可能少用堆疊。 如果分析工具是為了用於防止堆疊溢位的穩固處理序，則分析工具本身也應該避免觸發堆疊溢位。

## <a name="related-topics"></a>[相關主題]

|標題|描述|
|-----------|-----------------|
|[設定程式碼剖析環境](setting-up-a-profiling-environment.md)|說明如何初始化分析工具、設定事件通知，以及為 Windows 服務進行分析。|
|[分析介面](profiling-interfaces.md)|說明分析 API 所使用的 Unmanaged 介面。|
|[分析全域靜態函式](profiling-global-static-functions.md)|說明分析 API 所使用的 Unmanaged 全域靜態函式。|
|[分析列舉](profiling-enumerations.md)|說明分析 API 所使用的 Unmanaged 列舉。|
|[分析結構](profiling-structures.md)|說明分析 API 所使用的 Unmanaged 結構。|
