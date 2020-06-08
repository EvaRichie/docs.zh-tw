---
title: COR_PRF_ASSEMBLY_REFERENCE_INFO 結構
ms.date: 03/30/2017
dev_langs:
- cpp
ms.assetid: c8c1d916-8d1a-4f82-8128-9fd3732383fc
ms.openlocfilehash: 861b31e5621e9a7b40403d249c6a5c8c4ac25db8
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501036"
---
# <a name="cor_prf_assembly_reference_info-structure"></a>COR_PRF_ASSEMBLY_REFERENCE_INFO 結構
[.NET Framework 4.5.2 與更新版本提供支援]  
  
 提供執行組件參考關閉查核時應考量之組件參考的相關資訊給 Common Language Runtime。  
  
## <a name="syntax"></a>語法  
  
```cpp  
typedef struct _COR_PRF_ASSEMBLY_REFERENCE_INFO {  
    void* pbPublicKeyOrToken;  
    ULONG cbPublicKeyOrToken;  
    LPCWSTR szName;  
    ASSEMBLYMETADATA* pMetaData;  
    void* pbHashValue;  
    ULONG cbHashValue;  
    DWORD dwAssemblyRefFlags;  
} COR_PRF_EX_CLAUSE_INFO;  
```  
  
## <a name="members"></a>成員  
  
|成員|說明|  
|------------|-----------------|  
|`pbPublicKeyOrToken`|組件的公開金鑰或語彙基元的指標。|  
|`cbPublicKeyOrToken`|公開金鑰或語彙基元中的位元組數。|  
|`szName`|參考之組件的名稱。|  
|`pMetaData`|組件中繼資料的指標。|  
|`pbHashValue`|雜湊二進位大型物件 (BLOB) 的指標。|  
|`cbHashValue`|雜湊 BLOB 中的位元組數。|  
|`dwAssemblyRefFlags`|組件的旗標。|  
  
## <a name="remarks"></a>備註  
 `COR_PRF_EX_CLAUSE_INFO` 結構會在其宣告 Common Language Runtime 在執行組件參考關閉查核時應考量的其他組件參考時，由分析工具填入。  
  
 如果分析工具註冊[ICorProfilerCallback6：： GetAssemblyReferences](icorprofilercallback6-getassemblyreferences-method.md)回呼方法，執行時間會傳遞要載入之元件的路徑和名稱，以及指向該方法的[ICorProfilerAssemblyReferenceProvider](icorprofilerassemblyreferenceprovider-interface.md)介面物件指標。 然後，分析工具可以[ICorProfilerAssemblyReferenceProvider::AddAssemblyReference](icorprofilerassemblyreferenceprovider-addassemblyreference-method.md) `COR_PRF_ASSEMBLY_REFERENCE_INFO` 針對計畫要從[ICorProfilerCallback6：： GetAssemblyReferences](icorprofilercallback6-getassemblyreferences-method.md)回呼中指定的元件參考的每個目標群組件，使用物件來呼叫 ICorProfilerAssemblyReferenceProvider：： AddAssemblyReference 方法。  
  
## <a name="requirements"></a>規格需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorProf.idl、CorProf.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [分析結構](profiling-structures.md)
- [GetAssemblyReferences 方法](icorprofilercallback6-getassemblyreferences-method.md)
- [AddAssemblyReference 方法](icorprofilerassemblyreferenceprovider-addassemblyreference-method.md)
