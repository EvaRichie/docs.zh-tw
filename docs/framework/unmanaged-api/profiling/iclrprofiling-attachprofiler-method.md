---
title: ICLRProfiling::AttachProfiler 方法
ms.date: 03/30/2017
api_name:
- IClrProfiling.AttachProfiler Method
api_location:
- Mscorwks.dll
api_type:
- COM
f1_keywords:
- IClrProfiling::AttachProfiler
helpviewer_keywords:
- AttachProfiler method [.NET Framework profiling]
- IClrProfiling::AttachProfiler method [.NET Framework profiling]
ms.assetid: 535a6839-c443-405b-a6f4-e2af90725d5b
topic_type:
- apiref
ms.openlocfilehash: 48ac09e1862ae58e79707235e891f72920de1251
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500555"
---
# <a name="iclrprofilingattachprofiler-method"></a>ICLRProfiling::AttachProfiler 方法
將指定的程式碼剖析工具附加至指定的處理序。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT AttachProfiler(  
  [in] DWORD dwProfileeProcessID,  
  [in] DWORD dwMillisecondsMax,                     // optional  
  [in] const CLSID * pClsidProfiler,  
  [in] LPCWSTR wszProfilerPath,                     // optional  
  [in] size_is(cbClientData)] void * pvClientData,  // optional  
  [in] UINT cbClientData);                          // optional  
```  
  
## <a name="parameters"></a>參數

- `dwProfileeProcessID`

  \[in] 程式碼剖析工具應附加至進程的處理序識別碼。 在 64 位元電腦上，已剖析程式碼的處理序的位元必須符合正在呼叫 `AttachProfiler` 的觸發處理序的位元。 如果呼叫 `AttachProfiler` 用的使用者帳戶具有系統管理權限，則目標處理序可以是系統上的任何處理序。 否則目標處理序必須由相同的使用者帳戶所擁有。

- `dwMillisecondsMax`

  \[in] 完成的持續時間（以毫秒為單位） `AttachProfiler` 。 觸發處理序應該傳遞已知足以讓特定程式碼剖析工具完成初始化的逾時值。
  
- `pClsidProfiler`

  \[in] 要載入之 profiler 的 CLSID 指標。 `AttachProfiler` 傳回之後，觸發處理序可以重複使用此記憶體。

- `wszProfilerPath`

  \[in] 要載入的分析工具 DLL 檔案的完整路徑。 此字串應該包含不超過 260 個字元，包括 null 結束字元。 如果 `wszProfilerPath` 是 null 或空字串，Common Language Runtime (CLR) 會嘗試在登錄中尋找 `pClsidProfiler` 指向的 CLSID，以尋找程式碼剖析工具 DLL 檔的位置。

- `pvClientData`

  \[in] [ICorProfilerCallback3：： InitializeForAttach](icorprofilercallback3-initializeforattach-method.md)方法傳遞至分析工具的資料指標。 `AttachProfiler` 傳回之後，觸發處理序可以重複使用此記憶體。 如果 `pvClientData` 為 null，則 `cbClientData` 必須是 0 (零)。

- `cbClientData`

  \[in] 指向的資料大小（以位元組為單位） `pvClientData` 。

## <a name="return-value"></a>傳回值  
 這個方法會傳回下列 HRESULT。  
  
|HRESULT|說明|  
|-------------|-----------------|  
|S_OK|指定的程式碼剖析工具已經成功附加至目標處理序。|  
|CORPROF_E_PROFILER_ALREADY_ACTIVE|已經有程式碼剖析工具在作用中或附加至目標處理序。|  
|CORPROF_E_PROFILER_NOT_ATTACHABLE|指定的程式碼剖析工具不支援附加作業。 觸發處理序可能會嘗試附加不同的程式碼剖析工具。|  
|CORPROF_E_PROFILEE_INCOMPATIBLE_WITH_TRIGGER|無法要求執行程式碼剖析工具附加，因為目標處理序的版本與目前正在呼叫 `AttachProfiler` 的處理序不相容。|  
|HRESULT_FROM_WIN32(ERROR_ACCESS_DENIED)|觸發處理序的使用者無法存取目標處理序。|  
|HRESULT_FROM_WIN32(ERROR_PRIVILEGE_NOT_HELD)|觸發處理序的使用者沒有將程式碼剖析工具附加至指定目標處理序的必要權限。 應用程式事件記錄檔可能包含更多的資訊。|  
|CORPROF_E_IPC_FAILED|與目標處理序通訊時發生失敗。 這通常發生於目標處理序正在關閉的時候。|  
|HRESULT_FROM_WIN32(ERROR_FILE_NOT_FOUND)|目標處理序不存在或未執行支援附加作業的 CLR。 這可能表示在呼叫執行階段列舉方法之後，CLR 已卸載。|  
|HRESULT_FROM_WIN32(ERROR_TIMEOUT)|逾時已過期但未開始載入程式碼剖析工具。 您可以重試附加作業。 目標處理序中的完成項執行時間超過逾時值時，就會發生逾時。|  
|E_INVALIDARG|一或多個參數具有無效的值。|  
|E_FAIL|發生某個其他未指定的失敗。|  
|其他錯誤碼|如果 profiler 的[ICorProfilerCallback3：： InitializeForAttach](icorprofilercallback3-initializeforattach-method.md)方法傳回表示失敗的 HRESULT，則 `AttachProfiler` 會傳回相同的 hresult。 在此情況下，E_NOTIMPL 會轉換成 CORPROF_E_PROFILER_NOT_ATTACHABLE。|  
  
## <a name="remarks"></a>備註  
  
## <a name="memory-management"></a>記憶體管理  
 保持 COM 慣例，`AttachProfiler` 的呼叫端 (例如，程式碼剖析工具開發人員撰寫的觸發程序程式碼) 會負責配置與取消配置 `pvClientData` 參數所指向資料的記憶體。 當 CLR 執行 `AttachProfiler` 呼叫時，它會建立一份 `pvClientData` 指向的記憶體，並將其傳送至目標處理序。 當目標處理序內的 CLR 收到自己的 `pvClientData` 區塊複本時，它會將區塊透過 `InitializeForAttach` 方法傳遞給程式碼剖析工具，然後再從目標處理序取消配置其 `pvClientData` 區塊複本。  
  
## <a name="requirements"></a>規格需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorProf.idl、CorProf.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICorProfilerCallback 介面](icorprofilercallback-interface.md)
- [ICorProfilerInfo3 介面](icorprofilerinfo3-interface.md)
- [分析介面](profiling-interfaces.md)
- [程式碼剖析](index.md)
