---
title: COR_SEGMENT 結構
ms.date: 03/30/2017
api_name:
- COR_SEGMENT
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_SEGMENT
helpviewer_keywords:
- COR_SEGMENT structure [.NET Framework debugging]
ms.assetid: 93aeecb9-7fef-4545-8daf-f566dfc47084
topic_type:
- apiref
ms.openlocfilehash: 738e29fa15340c76b055b608140f3c3bfbd29611
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95726349"
---
# <a name="cor_segment-structure"></a>COR_SEGMENT 結構

包含 Managed 堆積中記憶體區域的相關資訊。  
  
## <a name="syntax"></a>語法  
  
```cpp  
typedef struct _COR_SEGMENT {  
    CORDB_ADDRESS start;
    CORDB_ADDRESS end;
    CorDebugGenerationTypes gen;
    ULONG heap;
} COR_SEGMENT;  
```  
  
## <a name="members"></a>成員  
  
|member|描述|  
|------------|-----------------|  
|`start`|記憶體區域的起始位址。|  
|`end`|記憶體區域的結束位址。|  
|`gen`|[CorDebugGenerationTypes](cordebuggenerationtypes-enumeration.md) 列舉成員，表示記憶體區域的層代。|  
|`heap`|記憶體區域所在的堆積號碼。 如需詳細資訊，請參閱＜備註＞一節。|  
  
## <a name="remarks"></a>備註  

 `COR_SEGMENTS` 結構代表受空控堆積中的記憶體區域。  `COR_SEGMENTS` 物件是 [ICorDebugHeapRegionEnum](icordebugheapsegmentenum-interface.md) 集合物件的成員，集合物件的填入是藉由呼叫 [icordebugprocess5:: Enumerateheapregions](icordebugprocess5-enumerateheapregions-method.md) 方法。  
  
 `heap` 欄位是處理器號碼，其對應到正在回報的堆積。 針對工作站記憶體回收行程，其值一律為零，因為工作站只有一個記憶體回收堆積。 針對伺服器記憶體回收行程，其值對應至堆積附加的處理器。 請注意，可能會有比實際處理器更多或更少記憶體回收堆積，這是因為記憶體回收行程的實作詳細資料所致。  
  
## <a name="requirements"></a>需求  

 **平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、CorDebug.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [偵錯結構](debugging-structures.md)
- [偵錯](index.md)
