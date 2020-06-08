---
title: FunctionTailcall 函式
ms.date: 03/30/2017
api_name:
- FunctionTailcall
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- FunctionTailcall
helpviewer_keywords:
- FunctionTailcall function [.NET Framework profiling]
ms.assetid: 66347e03-9a97-41e8-8f9d-89b80803f7b5
topic_type:
- apiref
ms.openlocfilehash: 42ea497bdcab71518bec08514b827d76f0317d57
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500594"
---
# <a name="functiontailcall-function"></a>FunctionTailcall 函式
通知分析工具，目前正在執行的函式即將對另一個函式執行 tail 呼叫。  
  
> [!NOTE]
> 函式 `FunctionTailcall` 在 .NET Framework 版本2.0 中已被取代。 它會繼續工作，但會造成效能上的負面影響。 請改用[FunctionTailcall2](functiontailcall2-function.md)函數。  
  
## <a name="syntax"></a>語法  
  
```cpp
void __stdcall FunctionTailcall (  
    [in] FunctionID funcID  
);  
```  
  
## <a name="parameters"></a>參數

- `funcID`

  \[in] 目前正在執行之函式的識別碼，即將進行 tail 呼叫。

## <a name="remarks"></a>備註  
 Tail 呼叫的目標函式會使用目前的堆疊框架，並會直接傳回呼叫端呼叫之函式的呼叫端。 這表示不會針對做為 tail 呼叫目標的函式發出[FunctionLeave](functionleave-function.md)回呼。  
  
 函式 `FunctionTailcall` 是回呼; 您必須加以執行。 此執行必須使用 `__declspec` （ `naked` ）儲存類別屬性。  
  
 在呼叫此函式之前，執行引擎不會儲存任何暫存器。  
  
- 輸入時，您必須儲存您所使用的所有暫存器，包括浮點單位（FPU）中的暫存器。  
  
- 結束時，您必須透過關閉其呼叫者推送的所有參數來還原堆疊。  
  
 的執行 `FunctionTailcall` 不應該封鎖，因為它會延遲垃圾收集。 執行不應嘗試垃圾收集，因為堆疊可能不會處於垃圾收集的唯讀狀態。 如果嘗試垃圾收集，執行時間將會封鎖，直到傳回為止 `FunctionTailcall` 。  
  
 此外，函式 `FunctionTailcall` 不能呼叫 managed 程式碼，或以任何方式執行 managed 記憶體配置。  
  
## <a name="requirements"></a>規格需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** Corprof.idl .idl  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：** 1.1、1。0  
  
## <a name="see-also"></a>另請參閱

- [FunctionEnter2 函式](functionenter2-function.md)
- [FunctionLeave2 函式](functionleave2-function.md)
- [SetEnterLeaveFunctionHooks2 方法](icorprofilerinfo2-setenterleavefunctionhooks2-method.md)
- [分析全域靜態函式](profiling-global-static-functions.md)
