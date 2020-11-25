---
title: ICorProfilerInfo3::RequestProfilerDetach 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo3.RequestProfilerDetach Method
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo3::RequestProfilerDetach
helpviewer_keywords:
- RequestProfilerDetach method [.NET Framework profiling]
- ICorProfilerInfo3::RequestProfilerDetach method [.NET Framework profiling]
ms.assetid: ea102e62-0454-4477-bcf3-126773acd184
topic_type:
- apiref
ms.openlocfilehash: 2ea39c94a5a0f3d24d4123d6405115ac75105e26
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95721578"
---
# <a name="icorprofilerinfo3requestprofilerdetach-method"></a>ICorProfilerInfo3::RequestProfilerDetach 方法

指示該執行階段中斷與分析工具的連結。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT RequestProfilerDetach(  
   [in] DWORD    dwExpectedCompletionMilliseconds);  
```  
  
## <a name="parameters"></a>參數  

 `dwExpectedCompletionMilliseconds`  
 [in] 時間長度，以毫秒為單位，Common Language Runtime (CLR) 應該在檢查之前等待，以查看它是否能安全卸載分析工具 。  
  
## <a name="return-value"></a>傳回值  

 這個方法會傳回下列特定的 HRESULT，以及表示方法失敗的 HRESULT 錯誤。  
  
|HRESULT|描述|  
|-------------|-----------------|  
|S_OK|中斷連結要求有效，而且現在中斷連結程序會在另一個執行緒上繼續。 中斷連結全部完成時，會發生 `ProfilerDetachSucceeded` 事件。|  
|E_CORPROF_E_CALLBACK3_REQUIRED|分析工具失敗[ICorProfilerCallback3](icorprofilercallback3-interface.md)介面的[IUnknown：： QueryInterface](/windows/win32/api/unknwn/nf-unknwn-iunknown-queryinterface(q))嘗試，它必須實作為支援卸離作業。 未嘗試中斷連結。|  
|CORPROF_E_IMMUTABLE_FLAGS_SET|因為分析工具在啟動時將旗標設定為不可變，造成無法中斷連結。 未嘗試中斷連結；分析工具仍然完整連結。|  
|CORPROF_E_IRREVERSIBLE_INSTRUMENTATION_PRESENT|表示中斷連結是不可能的，因為分析工具使用了檢測的 Microsoft 中繼語言 (MSIL) 程式碼，或插入的攔截器 `enter` / `leave` 。 未嘗試中斷連結；分析工具仍然完整連結。<br /><br /> **注意** 已檢測的 MSIL 是程式碼，程式碼是由程式碼剖析工具使用 [SetILFunctionBody](icorprofilerinfo-setilfunctionbody-method.md) 方法所提供。|  
|CORPROF_E_RUNTIME_UNINITIALIZED|在受管理的應用程式中，執行階段尚未初始化。  (也就是，執行時間尚未完全載入。 ) 在分析工具回呼的 [ICorProfilerCallback：： Initialize](icorprofilercallback-initialize-method.md) 方法內要求表示中斷連結時，可能會傳回此錯誤碼。|  
|CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT|`RequestProfilerDetach` 在不支援的時間呼叫。 如果方法是在 managed 執行緒上呼叫，而不是從 [ICorProfilerCallback](icorprofilercallback-interface.md) 方法內，或是無法容許垃圾收集的 [ICorProfilerCallback](icorprofilercallback-interface.md) 方法內呼叫，就會發生這種情況。 如需詳細資訊，請參閱 [CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT](corprof-e-unsupported-call-sequence-hresult.md)。|  
  
## <a name="remarks"></a>備註  

 在中斷連結程序中，中斷連結的執行緒 (專為對分析工具中斷連結所建立的執行緒) 偶爾會檢查是否所有執行緒都結束分析工具的程式碼。 分析工具應該透過 `dwExpectedCompletionMilliseconds` 參數提供所需時間的估計。 要使用的理想值是分析工具花在任何指定的 `ICorProfilerCallback*` 方法上所需的典型時間量；此值不應小於分析工具預期所需最大時間量的一半。  
  
 中斷連結執行緒使用 `dwExpectedCompletionMilliseconds` 來決定睡眠多久之後，再檢查分析工具回呼程式碼是否已迅速卸離所有堆疊。 雖然下列演算法的詳細資料可能會在未來版本中的 CLR 有所變更，它也說明了一種 `dwExpectedCompletionMilliseconds` 能夠用來判斷何時可安全卸載分析工具的方式。 中斷連結執行緒先睡眠 `dwExpectedCompletionMilliseconds` 毫秒。 從睡眠喚醒之後，如果 CLR 發現分析工具回呼程式碼仍然存在，中斷連結線程會再次睡眠，這次是兩次 `dwExpectedCompletionMilliseconds` 毫秒。 從這個第二個睡眠狀態喚醒後，如果卸離執行緒發現分析工具回呼程式碼仍然存在，它會睡眠 10 分鐘後再檢查一次。 中斷連結執行緒會每隔 10 分鐘重新檢查一次。  
  
 如果分析工具指定 `dwExpectedCompletionMilliseconds` 為 0 (零) 時，CLR 會使用預設值為 5000，這表示它會在 5 秒後執行檢查，接著 10 秒後再次檢查，然後之後每隔 10 分鐘一次。  
  
## <a name="requirements"></a>需求  

 **平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorProf.idl、CorProf.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICorProfilerInfo3 介面](icorprofilerinfo3-interface.md)
- [分析介面](profiling-interfaces.md)
- [程式碼剖析](index.md)
