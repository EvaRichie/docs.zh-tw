---
title: 偵錯介面
ms.date: 02/07/2019
helpviewer_keywords:
- unmanaged interfaces [.NET Framework], debugging
- debugging interfaces [.NET Framework]
- interfaces [.NET Framework debugging]
ms.assetid: b6297c26-7624-4431-8af4-14112d07bcd5
ms.openlocfilehash: a3dd81ceaab2ba467d4c8ca091c1c2219040a273
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95676292"
---
# <a name="debugging-interfaces"></a>偵錯介面

本節說明 Unmanaged 介面，這類介面會處理通用語言執行平台 (CLR) 中所執行之程式的偵錯。  
  
## <a name="in-this-section"></a>本節內容  

 [ICLRDataEnumMemoryRegions 介面](iclrdataenummemoryregions-interface.md)\
 提供方法來列舉呼叫端所指定的記憶體區域。  
  
 [ICLRDataEnumMemoryRegionsCallback 介面](iclrdataenummemoryregionscallback-interface.md)\
 提供回呼方法，讓 `EnumMemoryRegions` 向偵錯工具報告嘗試列舉指定之記憶體區域的結果。  
  
 [ICLRDataTarget 介面](iclrdatatarget-interface.md)\
 提供方法與目標 CLR 處理序互動。  
  
 [ICLRDataTarget2 介面](iclrdatatarget2-interface.md)\
 `ICLRDataTarget` 的子類別，資料存取服務層會使用它來管理目標處理序中的虛擬記憶體區域。  
  
 [ICLRDataTarget3 介面](iclrdatatarget3-interface.md)\
 [ICLRDataTarget2](iclrdatatarget2-interface.md)的子類別，可存取例外狀況資訊。  
  
 [ICLRDebugging 介面](iclrdebugging-interface.md)\
 提供處理載入及卸載模組以進行偵錯的方法。  
  
 [ICLRDebuggingLibraryProvider 介面](iclrdebugginglibraryprovider-interface.md)\
 包含 [ProvideLibrary 方法](iclrdebugginglibraryprovider-providelibrary-method.md) 方法，這個方法會取得程式庫提供者回呼介面，以便視需要尋找並載入 common language runtime 版本特定的偵錯工具庫。  
  
 [ICLRMetadataLocator 介面](iclrmetadatalocator-interface.md)\
 由資料存取服務層用來尋找目標處理序中之組件中繼資料的介面。  
  
 [ICorDebug 介面](icordebug-interface.md)\
 提供方法讓開發人員於 CLR 環境中為應用程式偵錯。  
  
 [ICorDebugAppDomain 介面](icordebugappdomain-interface.md)\
 提供偵錯應用程式定義域的方法。  
  
 [ICorDebugAppDomain2 介面](icordebugappdomain2-interface.md)\
 提供方法來使用陣列、指標、函式指標和 ByRef 類型。 這個介面是 `ICorDebugAppDomain` 介面的擴充。  
  
 [ICorDebugAppDomain3 介面](icordebugappdomain3-interface.md)\
 提供在應用程式域中使用 Windows 執行階段類型的方法。 這個介面是 `ICorDebugAppDomain` 和 `ICorDebugAppDomain2` 介面的擴充。  
  
 [ICorDebugAppDomain4 介面](icordebugappdomain4-interface.md)\
 以邏輯方式擴充 [ICorDebugAppDomain](icordebugappdomain-interface.md) 介面，以從 COM 可呼叫包裝函式取得 managed 物件。  
  
 [ICorDebugAppDomainEnum 介面](icordebugappdomainenum-interface.md)\
 提供方法，此方法會傳回指定數目的 `ICorDebugAppDomain` 值 (從列舉類型中的下一個位置開始)。  
  
 [ICorDebugArrayValue 介面](icordebugarrayvalue-interface.md)\
 表示一維或多維陣列之 `ICorDebugHeapValue` 的子類別。  
  
 [ICorDebugAssembly 介面](icordebugassembly-interface.md)\
 表示組件。  
  
 [ICorDebugAssembly2 介面](icordebugassembly2-interface.md)\
 表示組件。 這個介面是 `ICorDebugAssembly` 介面的擴充。  
  
 [ICorDebugAssembly3 介面](icordebugassembly3-interface.md)\
 以邏輯方式擴充 [ICorDebugAssembly](icordebugassembly-interface.md) 介面，以提供容器元件及其包含元件的支援。 **僅適用於 .NET 原生。**  
  
 [ICorDebugAssemblyEnum 介面](icordebugassemblyenum-interface.md)\
 實作 `ICorDebugEnum` 方法，並列舉 `ICorDebugAssembly` 陣列。  
  
 [ICorDebugBlockingObjectEnum 介面](icordebugblockingobjectenum-interface.md)\
 提供 [CorDebugBlockingObject](cordebugblockingobject-structure.md) 結構清單的列舉值。  
  
 [ICorDebugBoxValue 介面](icordebugboxvalue-interface.md)\
 `ICorDebugHeapValue` 的子類別，表示 Boxed 值的類別物件。  
  
 [ICorDebugBreakpoint 介面](icordebugbreakpoint-interface.md)\
 表示函式中的中斷點，或是某個值上的監看點。  
  
 [ICorDebugBreakpointEnum 介面](icordebugbreakpointenum-interface.md)\
 實作 `ICorDebugEnum` 方法，並列舉 `ICorDebugBreakpoint` 陣列。  
  
 [ICorDebugChain 介面](icordebugchain-interface.md)\
 表示實體或邏輯呼叫堆疊的區段。  
  
 [ICorDebugChainEnum 介面](icordebugchainenum-interface.md)\
 實作 `ICorDebugEnum` 方法，並列舉 `ICorDebugChain` 陣列。  
  
 [ICorDebugClass 介面](icordebugclass-interface.md)\
 表示類型，可以是基本類型或複雜類型 (亦即，使用者定義類型)。 如果是泛型類型，則 `ICorDebugClass` 表示未具現化的泛型類型。  
  
 [ICorDebugClass2 介面](icordebugclass2-interface.md)\
 表示泛型類別，或是具有 <xref:System.Type> 類型之方法參數的類別。 這個介面延伸 `ICorDebugClass`。  
  
 [ICorDebugCode 介面](icordebugcode-interface1.md)\
 表示 Microsoft Intermediate Language (MSIL) 程式碼或機器碼的區段。  
  
 [ICorDebugCode2 介面](icordebugcode2-interface.md)\
 提供方法來擴充 `ICorDebugCode` 的功能。  
  
 [ICorDebugCode3 介面](icordebugcode3-interface.md)\
 提供擴充 [ICorDebugCode](icordebugcode-interface1.md) 和 [ICorDebugCode2](icordebugcode2-interface.md) 的方法，以提供 managed 傳回值的相關資訊。  
  
 [ICorDebugCode4 介面](icordebugcode4-interface.md)\
 提供方法，此方法可讓偵錯工具列舉函數中的區域變數和引數。  
  
 [ICorDebugCodeEnum 介面](icordebugcodeenum-interface.md)\
 實作 `ICorDebugEnum` 方法，並列舉 `ICorDebugCode` 陣列。  
  
 [ICorDebugComObjectValue 介面](icordebugcomobjectvalue-interface.md)\
 提供擷取快取介面物件的方法。  
  
 [ICorDebugCoNtext 介面](icordebugcontext-interface.md)\
 表示內容物件。 尚未實作這個介面。  
  
 [ICorDebugController 介面](icordebugcontroller-interface.md)\
 表示可以控制程式碼執行內容的範圍 (<xref:System.Diagnostics.Process> 或 <xref:System.AppDomain> 其中一項)。  
  
 [ICorDebugDataTarget 介面](icordebugdatatarget-interface.md)\
 提供回呼介面，該介面可供存取特定的目標處理序。  
  
 [ICorDebugDataTarget2 介面](icordebugdatatarget2-interface.md)\
 以邏輯方式擴充 [ICorDebugDataTarget](icordebugdatatarget-interface.md) 介面。 **僅適用於 .NET 原生。**  
  
 [ICorDebugDataTarget3 介面](icordebugdatatarget3-interface.md)\
 以邏輯方式擴充 [ICorDebugDataTarget](icordebugdatatarget-interface.md) 介面，以提供已載入模組的相關資訊。 **僅適用於 .NET 原生。**  
  
 [ICorDebugDebugEvent 介面](icordebugdebugevent-interface.md)\
 定義所有 `ICorDebug` 偵錯事件衍生的來源基底介面。 **僅適用於 .NET 原生。**  
  
 [ICorDebugEditAndContinueErrorInfo 介面](icordebugeditandcontinueerrorinfo-interface.md)\
 已過時。 請勿使用這個介面。  
  
 [ICorDebugEditAndContinueSnapshot 介面](icordebugeditandcontinuesnapshot-interface.md)\
 已過時。 請勿使用這個介面。  
  
 [ICorDebugEnum 介面](icordebugenum-interface1.md)\
 當做抽象基底介面來偵錯列舉值。  
  
 [ICorDebugErrorInfoEnum 介面](icordebugerrorinfoenum-interface.md)\
 已過時。 請勿使用這個介面。  
  
 [ICorDebugEval 介面](icordebugeval-interface.md)\
 提供方法讓偵錯工具執行所偵錯的程式碼內容中的程式碼。  
  
 [ICorDebugEval2 介面](icordebugeval2-interface.md)\
 擴充 `ICorDebugEval` 來提供泛型類型的支援。  
  
 [ICorDebugExceptionDebugEvent 介面](icordebugexceptiondebugevent-interface.md)\
 擴充 [ICorDebugDebugEvent](icordebugdebugevent-interface.md) 介面以支援例外狀況事件。 **僅適用於 .NET 原生。**  
  
 [ICorDebugExceptionObjectCallStackEnum 介面](icordebugexceptionobjectcallstackenum-interface.md)\
 提供例外狀況物件中內嵌之呼叫堆疊資訊的列舉值。  
  
 [ICorDebugExceptionObjectValue 介面](icordebugexceptionobjectvalue-interface.md)\
 擴充 [ICorDebugObjectValue](icordebugobjectvalue-interface.md) 介面，以從 managed 例外狀況物件提供堆疊追蹤資訊。  
  
 [ICorDebugFrame 介面](icordebugframe-interface.md)\
 表示目前堆疊上的框架。  
  
 [ICorDebugFrameEnum 介面](icordebugframeenum-interface.md)\
 實作 `ICorDebugEnum` 方法，並列舉 `ICorDebugFrame` 陣列。  
  
 [ICorDebugFunction 介面](icordebugfunction-interface1.md)\
 表示 Managed 函式或方法。  
  
 [ICorDebugFunction2 介面](icordebugfunction2-interface.md)\
 以邏輯方式擴充 `ICorDebugFunction`，為 Just My Code 逐步執行的偵錯提供支援。  
  
 [ICorDebugFunction3 介面](icordebugfunction3-interface.md)\
 以邏輯方式擴充 [ICorDebugFunction](icordebugfunction-interface1.md) 介面，以提供從 ReJIT 要求存取程式碼的許可權。  
  
 [ICorDebugFunctionBreakpoint 介面](icordebugfunctionbreakpoint-interface.md)\
 擴充 `ICorDebugBreakpoint` 來支援函式內的中斷點。  
  
 [ICorDebugGCReferenceEnum 介面](icordebuggcreferenceenum-interface.md)\
 為將要記憶體回收的物件提供列舉值。  
  
 [ICorDebugGenericValue 介面](icordebuggenericvalue-interface.md)\
 套用至所有值之 `ICorDebugValue` 的子類別。 這個介面提供值的 Get 和 Set 方法。  
  
 [ICorDebugGuidToTypeEnum 介面](icordebugguidtotypeenum-interface.md)\
 為對應 GUID 和其相應 `ICorDebugType` 物件的物件提供列舉值。  
  
 [ICorDebugHandleValue 介面](icordebughandlevalue-interface.md)\
 `ICorDebugReferenceValue` 的子類別，表示偵錯工具已建立記憶體回收控制代碼的參考值。  
  
 [ICorDebugHeapEnum 介面](icordebugheapenum-interface.md)\
 為 Managed 堆積上的物件提供列舉值。  
  
 [ICorDebugHeapSegmentEnum 介面](icordebugheapsegmentenum-interface.md)\
 為 Managed 堆積的記憶體區域提供列舉值。  
  
 [ICorDebugHeapValue 介面](icordebugheapvalue-interface.md)\
 `ICorDebugValue` 的子類別，表示 CLR 記憶體回收行程所回收的物件。  
  
 [ICorDebugHeapValue2 介面](icordebugheapvalue2-interface1.md)\
 `ICorDebugHeapValue` 的擴充，其支援執行階段控制代碼。  
  
 [ICorDebugHeapValue3 介面](icordebugheapvalue3-interface.md)\
 公開物件的監視器鎖定屬性。  
  
 [ICorDebugILCode 介面](icordebugilcode-interface.md)\
 代表中繼語言 (IL) 程式碼的區段。  
  
 [ICorDebugILCode2 介面](icordebugilcode2-interface.md)\
 以邏輯方式擴充 [ICorDebugILCode](icordebugilcode-interface.md) 介面，以提供方法來傳回函式區域變數簽章的標記，以及將分析工具的檢測中繼語言 (IL) 位移對應至原始方法 IL 位移。  
  
 [ICorDebugILFrame 介面](icordebugilframe-interface.md)\
 表示 MSIL 程式碼的堆疊框架。  
  
 [ICorDebugILFrame2 介面](icordebugilframe2-interface.md)\
 `ICorDebugILFrame` 的邏輯擴充。  
  
 [ICorDebugILFrame3 介面](icordebugilframe3-interface.md)\
 提供封裝函式傳回值的方法。  
  
 [ICorDebugILFrame4 介面](icordebugilframe4-interface.md)\
 提供的方法可讓您在中繼語言 (IL) 程式碼的框架中，存取區域變數和程式碼。 參數可指定偵錯工具是否能夠存取在分析工具 ReJIT 檢測中加入的變數和程式碼。  
  
 [ICorDebugInstanceFieldSymbol 介面](icordebuginstancefieldsymbol-interface.md)\
 代表執行個體欄位的偵錯符號資訊。 **僅適用於 .NET 原生。**  
  
 [ICorDebugInternalFrame 介面](icordebuginternalframe-interface.md)\
 識別偵錯工具的框架類型。  
  
 [ICorDebugInternalFrame2 介面](icordebuginternalframe2-interface.md)\
 提供內部框架的相關資訊，包括堆疊位址和相對於 [ICorDebugFrame](icordebugframe-interface.md) 物件的位置。  
  
 [ICorDebugLoadedModule 介面](icordebugloadedmodule-interface.md)\
 提供載入模組的相關資訊。 **僅適用於 .NET 原生。**  
  
 [ICorDebugManagedCallback 介面](icordebugmanagedcallback-interface.md)\
 提供方法來處理偵錯工具回呼。  
  
 [ICorDebugManagedCallback2 介面](icordebugmanagedcallback2-interface.md)\
 提供方法來支援偵錯工具例外狀況處理和 Managed 偵錯助理 (MDA)。 `ICorDebugManagedCallback2` 是 `ICorDebugManagedCallback` 的邏輯擴充。  
  
 [ICorDebugManagedCallback3 介面](icordebugmanagedcallback3-interface.md)\
 提供回呼方法，表示已引發啟用的自訂偵錯工具通知。  
  
 [ICorDebugMDA 介面](icordebugmda-interface.md)\
 表示 Managed 偵錯助理 (MDA) 訊息。  
  
 [ICorDebugMemoryBuffer 介面](icordebugmemorybuffer-interface.md)\
 代表記憶體內部緩衝區。 **僅適用於 .NET 原生。**  
  
 [ICorDebugMergedAssemblyRecord 介面](icordebugmergedassemblyrecord-interface.md)\
 提供合併組件的相關資訊。 **僅適用於 .NET 原生。**  
  
 [ICorDebugMetaDataLocator 介面](icordebugmetadatalocator-interface.md)\
 提供中繼資料資訊給偵錯工具。  
  
 [ICorDebugModule 介面](icordebugmodule-interface.md)\
 表示 CLR 模組，其為可執行檔或動態連結程式庫 (DLL)。  
  
 [ICorDebugModule2 介面](icordebugmodule2-interface.md)\
 當做 `ICorDebugModule` 的邏輯擴充。  
  
 [ICorDebugModule3 介面](icordebugmodule3-interface.md)\
 建立動態模組的符號讀取器。  
  
 [ICorDebugModuleBreakpoint 介面](icordebugmodulebreakpoint-interface.md)\
 擴充 `ICorDebugBreakpoint`，以提供特定模組的存取權。  
  
 [ICorDebugModuleDebugEvent 介面](icordebugmoduledebugevent-interface.md)\
 擴充 [ICorDebugDebugEvent](icordebugdebugevent-interface.md) 介面，以支援模組層級的事件。 **僅適用於 .NET 原生。**  
  
 [ICorDebugModuleEnum 介面](icordebugmoduleenum-interface.md)\
 實作 `ICorDebugEnum` 方法，並列舉 `ICorDebugModule` 陣列。  
  
 [ICorDebugMutableDataTarget 介面](icordebugmutabledatatarget-interface.md)\
 擴充 [ICorDebugDataTarget](icordebugdatatarget-interface.md) 介面，以支援可變數據目標。  
  
 [ICorDebugNativeFrame 介面](icordebugnativeframe-interface.md)\
 用於原生框架的 `ICorDebugFrame` 特定實作。  
  
 [ICorDebugNativeFrame2 介面](icordebugnativeframe2-interface.md)\
 提供測試父子框架關聯的方法。  
  
 [ICorDebugObjectEnum 介面](icordebugobjectenum-interface.md)\
 實作 `ICorDebugEnum` 方法，並根據物件陣列的相對虛擬位址 (RVA) 來列舉物件陣列。  
  
 [ICorDebugObjectValue 介面](icordebugobjectvalue-interface.md)\
 `ICorDebugValue` 的子類別，表示包含物件的值。  
  
 [ICorDebugObjectValue2 介面](icordebugobjectvalue2-interface.md)\
 擴充 `ICorDebugObjectValue` 來支援繼承和覆寫。  
  
 [ICorDebugProcess 介面](icordebugprocess-interface.md)\
 表示執行 Managed 程式碼的處理序。  
  
 [ICorDebugProcess2 介面](icordebugprocess2-interface1.md)\
 `ICorDebugProcess` 的邏輯擴充。  
  
 [ICorDebugProcess3 介面](icordebugprocess3-interface.md)\
 控制自訂偵錯工具通知。

 [ICorDebugProcess4 介面](icordebugprocess4-interface.md)\
 提供進程外執行控制的支援。
  
 [ICorDebugProcess5 介面](icordebugprocess5-interface.md)\
 擴充 [ICorDebugProcess](icordebugprocess-interface.md) 介面以支援存取 managed 堆積，以提供 managed 物件的垃圾收集資訊，以及判斷偵錯工具是否從應用程式的本機原生映射快取載入映射。  
  
 [ICorDebugProcess6 介面](icordebugprocess6-interface.md)\
 以邏輯方式擴充 [ICorDebugProcess](icordebugprocess-interface.md) 介面，以啟用功能，例如對原生例外狀況偵錯工具事件和虛擬模組分割中編碼的 managed debug 事件進行解碼。 **僅適用於 .NET 原生。**  
  
 [ICorDebugProcess7 介面](icordebugprocess7-interface.md)\
 提供用來設定偵錯工具的方法，以控制代碼目標處理序中的記憶體中中繼資料更新。  
  
 [ICorDebugProcess8 介面](icordebugprocess8-interface.md)\
 以邏輯方式擴充 [ICorDebugProcess](icordebugprocess-interface.md) 介面，以啟用或停用特定類型的 [ICorDebugManagedCallback2](icordebugmanagedcallback2-interface.md) 例外狀況回呼。  
  
 [ICorDebugProcessEnum 介面](icordebugprocessenum-interface.md)\
 實作 `ICorDebugEnum` 方法，並列舉 `ICorDebugProcess` 陣列。  
  
 [ICorDebugReferenceValue 介面](icordebugreferencevalue-interface.md)\
 支援參考類型的 `ICorDebugValue` 子類別。  
  
 [ICorDebugRegisterSet 介面](icordebugregisterset-interface.md)\
 表示目前在機器上執行程式碼的可用暫存器集合。  
  
 [ICorDebugRegisterSet2 介面](icordebugregisterset2-interface.md)\
 為具有 64 個以上暫存器的硬體平台，擴充 `ICorDebugRegisterSet` 的功能。  
  
 [ICorDebugRemote 介面](icordebugremote-interface.md)\
 提供啟動或附加 Managed 偵錯工具至遠端目標處理序的功能。  
  
 [ICorDebugRemoteTarget 介面](icordebugremotetarget-interface.md)\
 提供可讓您對 CLR 環境中的 Silverlight 應用程式進行偵錯的方法。  
  
 [ICorDebugRuntimeUnwindableFrame 介面](icordebugruntimeunwindableframe-interface.md)\
 提供 Unmanaged 方法的支援，這些方法需要通用語言執行平台 (CLR) 才能回溯框架。  
  
 [ICorDebugStackWalk 介面](icordebugstackwalk-interface.md)\
 提供用來在執行緒堆疊上取得 Managed 方法或框架的方法。  
  
 [ICorDebugStaticFieldSymbol 介面](icordebugstaticfieldsymbol-interface.md)\
 代表靜態欄位的偵錯符號資訊。 **僅適用於 .NET 原生。**  
  
 [ICorDebugStepper 介面](icordebugstepper-interface.md)\
 表示偵錯工具在程式碼執行作業中所執行的步驟，做為命令的發出和完成之間的識別項，並可提供方法來取消步驟。  
  
 [ICorDebugStepper2 介面](icordebugstepper2-interface1.md)\
 提供 Just My Code (JMC) 偵錯的支援。  
  
 [ICorDebugStepperEnum 介面](icordebugstepperenum-interface.md)\
 實作 `ICorDebugEnum` 方法，並列舉 `ICorDebugStepper` 陣列。  
  
 [ICorDebugStringValue 介面](icordebugstringvalue-interface.md)\
 套用至字串值之 `ICorDebugHeapValue` 的子類別。  
  
 [ICorDebugSymbolProvider 介面](icordebugsymbolprovider-interface.md)\
 提供可用來擷取偵錯符號資訊的方法。 **僅適用於 .NET 原生。**  
  
 [ICorDebugSymbolProvider2 介面](icordebugsymbolprovider2-interface.md)\
 以邏輯方式擴充 [ICorDebugSymbolProvider](icordebugsymbolprovider-interface.md) 介面，以取得其他的 debug 符號資訊。 **僅適用於 .NET 原生。**  
  
 [ICorDebugThread 介面](icordebugthread-interface.md)\
 表示處理序中的執行緒。 `ICorDebugThread` 執行個體的存留期與其所表示的執行緒之存留期相同。  
  
 [ICorDebugThread2 介面](icordebugthread2-interface.md)\
 當做 `ICorDebugThread` 的邏輯擴充。  
  
 [ICorDebugThread3 介面](icordebugthread3-interface.md)\
 提供 [ICorDebugStackWalk](icordebugstackwalk-interface.md) 和對應介面的進入點。  
  
 [ICorDebugThread4 介面](icordebugthread4-interface.md)\
 提供執行緒封鎖資訊。  
  
 [ICorDebugThreadEnum 介面](icordebugthreadenum-interface1.md)\
 實作 `ICorDebugEnum` 方法，並列舉 `ICorDebugThread` 陣列。  
  
 [ICorDebugType 介面](icordebugtype-interface.md)\
 表示類型，可以是基本類型或複雜類型 (亦即，使用者定義類型)。 如果是泛型類型，則 `ICorDebugType` 表示具現化的泛型類型。  
  
 [ICorDebugType2 介面](icordebugtype2-interface.md)\
 擴充 [ICorDebugType](icordebugtype-interface.md) 介面，以取得基底類型或複雜 (使用者定義) 類型的類型識別碼。  
  
 [ICorDebugTypeEnum 介面](icordebugtypeenum-interface.md)\
 實作 `ICorDebugEnum` 方法，並列舉 `ICorDebugType` 陣列。  
  
 [ICorDebugUnmanagedCallback 介面](icordebugunmanagedcallback-interface.md)\
 提供未直接與 CLR 有關之原生事件的告知。  
  
 [ICorDebugValue](icordebugvalue-interface.md)\
 表示所偵錯之處理序中的讀取或寫入值。  
  
 [ICorDebugValue2](icordebugvalue2-interface.md)\
 擴充 `ICorDebugValue` 來提供 `ICorDebugType` 的支援。  
  
 [ICorDebugValue3 介面](icordebugvalue3-interface.md)\
 擴充 "ICorDebugValue" 和 "ICorDebugValue2" 介面，以提供大於 2 GB 的陣列支援。  
  
 [ICorDebugValueBreakpoint](icordebugvaluebreakpoint-interface.md)\
 擴充 `ICorDebugBreakpoint`，以提供特定值的存取權。  
  
 [ICorDebugValueEnum](icordebugvalueenum-interface.md)\
 實作 `ICorDebugEnum` 方法，並列舉 `ICorDebugValue` 陣列。  
  
 [ICorDebugVariableHome 介面](icordebugvariablehome-interface.md)\
 表示函數的區域變數或引數。  
  
 [ICorDebugVariableHomeEnum 介面](icordebugvariablehomeenum-interface.md)\
 提供函數中區域變數和引數的列舉值。  
  
 [ICorDebugVariableSymbol 介面](icordebugvariablesymbol-interface.md)\
 擷取變數的偵錯符號資訊。 **僅適用於 .NET 原生。**  
  
 [ICorDebugVirtualUnwinder 介面](icordebugvirtualunwinder-interface.md)\
 提供可協助堆疊回溯的方法。 **僅適用於 .NET 原生。**  
  
 [ICorPublish 介面](icorpublish-interface.md)\
 當做發行處理序的一般介面。  
  
 [ICorPublishAppDomain 介面](icorpublishappdomain-interface.md)\
 表示及提供與應用程式定義域有關的資訊。  
  
 [ICorPublishAppDomainEnum 介面](icorpublishappdomainenum-interface.md)\
 提供方法來周遊目前存在於處理序中之 `ICorPublishAppDomain` 物件的集合。  
  
 [ICorPublishEnum 介面](icorpublishenum-interface.md)\
 當做發行列舉值的抽象基底。  
  
 [ICorPublishProcess 介面](icorpublishprocess-interface.md)\
 提供存取處理序相關資訊的方法。  
  
 [ICorPublishProcessEnum 介面](icorpublishprocessenum-interface.md)\
 提供方法來周遊 `ICorPublishProcess` 物件的集合。  

 [ISOSDacInterface 介面](isosdacinterface-interface.md)\
 提供 helper 方法來存取資料 `SOS` 。

 [IXCLRDataMethodDefinition 介面](ixclrdatamethoddefinition-interface.md)\
 提供查詢方法定義相關資訊的方法。

 [IXCLRDataMethodInstance 介面](ixclrdatamethodinstance-interface.md)\
 提供查詢方法實例相關資訊的方法。

 [IXCLRDataModule 介面](ixclrdatamodule-interface.md)\
 提供方法來查詢已載入模組的相關資訊。

 [IXCLRDataProcess 介面](ixclrdataprocess-interface.md)\
 提供查詢進程相關資訊的方法。
  
## <a name="related-sections"></a>相關章節  

 [調試 Coclass](debugging-coclasses.md)\
 [調試全域靜態函式](debugging-global-static-functions.md)\
 [調試列舉](debugging-enumerations.md)\
 [調試結構](debugging-structures.md)\
