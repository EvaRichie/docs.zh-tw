---
title: ICorProfilerModuleEnum 介面
ms.date: 03/30/2017
api_name:
- ICorProfilerModuleEnum
api_location:
- mscorwks.cll
api_type:
- COM
f1_keywords:
- ICorProfilerModuleEnum
helpviewer_keywords:
- ICorProfilerModuleEnum interface [.NET Framework profiling]
ms.assetid: 24d0fcfa-1601-4fba-868f-da8c97303467
topic_type:
- apiref
ms.openlocfilehash: 98b64289b7d512c4e73cf4d40e89319532c6704a
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95722813"
---
# <a name="icorprofilermoduleenum-interface"></a>ICorProfilerModuleEnum 介面

提供方法，以循序逐一查看由應用程式或分析工具所載入的模組集合。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[Clone 方法](icorprofilermoduleenum-clone-method.md)|取得這個 `ICorProfilerModuleEnum` 介面複本的介面指標。|  
|[GetCount 方法](icorprofilermoduleenum-getcount-method.md)|取得已載入至應用程式之 Managed 模組的數目。|  
|[下一個方法](icorprofilermoduleenum-next-method.md)|從循序物件集合中取得指定的連續模組數目，從序列中列舉值的目前位置開始。|  
|[Reset 方法](icorprofilermoduleenum-reset-method.md)|將列舉值的資料指標移至序列的開始位置。|  
|[Skip 方法](icorprofilermoduleenum-skip-method.md)|將列舉值的資料指標位置前移，以略過指定數目的項目。|  
  
## <a name="remarks"></a>備註  

 `ICorProfilerModuleEnum` 介面是列舉值。 它可讓陣列的接收端以適合接收端的速率，從傳送端提取項目。 換句話說，接收端能夠明確控制陣列項目的流程，因此可避免與傳遞大型陣列做為方法參數相關的問題發生。  
  
## <a name="requirements"></a>需求  

 **平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorProf.idl、CorProf.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICorProfilerInfo 介面](icorprofilerinfo-interface.md)
- [分析介面](profiling-interfaces.md)
- [EnumModules 方法](icorprofilerinfo3-enummodules-method.md)
