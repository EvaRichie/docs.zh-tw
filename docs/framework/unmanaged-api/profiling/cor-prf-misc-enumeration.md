---
title: COR_PRF_MISC 列舉
ms.date: 03/30/2017
api_name:
- COR_PRF_MISC
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_MISC
helpviewer_keywords:
- COR_PRF_MISC enumeration [.NET Framework profiling]
ms.assetid: 619bb5de-e309-48b6-a3af-32d935a0ff46
topic_type:
- apiref
ms.openlocfilehash: 7b8f2845589a8372f62c95ef1a82eae3ed602c1f
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500828"
---
# <a name="cor_prf_misc-enumeration"></a>COR_PRF_MISC 列舉
包含指定特定識別項的常數值。  
  
## <a name="syntax"></a>語法  
  
```cpp  
typedef enum {  
    PROFILER_PARENT_UNKNOWN = 0xFFFFFFFD,  
    PROFILER_GLOBAL_CLASS   = 0xFFFFFFFE,  
    PROFILER_GLOBAL_MODULE  = 0xFFFFFFFF  
} COR_PRF_MISC;  
```  
  
## <a name="members"></a>成員  
  
|成員|說明|  
|------------|-----------------|  
|`PROFILER_PARENT_UNKNOWN`|尚未附加至元件之模組的[ICorProfilerInfo：： GetModuleInfo](icorprofilerinfo-getmoduleinfo-method.md)所使用的預設識別碼。|  
|`PROFILER_GLOBAL_CLASS`|不屬於類別之全域常數的預設類別識別碼。|  
|`PROFILER_GLOBAL_MODULE`|不屬於模組之全域物件的預設模組識別碼。|  
  
## <a name="requirements"></a>規格需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorProf.idl、CorProf.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [分析列舉](profiling-enumerations.md)
