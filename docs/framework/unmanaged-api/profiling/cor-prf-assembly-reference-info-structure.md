---
title: COR_PRF_ASSEMBLY_REFERENCE_INFO 結構
ms.date: 03/30/2017
dev_langs:
- cpp
ms.assetid: c8c1d916-8d1a-4f82-8128-9fd3732383fc
ms.openlocfilehash: 7c7d447afcb5a8617aa92212f3325719d5f43bf5
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95718614"
---
# <a name="cor_prf_assembly_reference_info-structure"></a><span data-ttu-id="2fa85-102">COR_PRF_ASSEMBLY_REFERENCE_INFO 結構</span><span class="sxs-lookup"><span data-stu-id="2fa85-102">COR_PRF_ASSEMBLY_REFERENCE_INFO Structure</span></span>

<span data-ttu-id="2fa85-103">[.NET Framework 4.5.2 與更新版本提供支援]</span><span class="sxs-lookup"><span data-stu-id="2fa85-103">[Supported in the .NET Framework 4.5.2 and later versions]</span></span>  
  
 <span data-ttu-id="2fa85-104">提供執行組件參考關閉查核時應考量之組件參考的相關資訊給 Common Language Runtime。</span><span class="sxs-lookup"><span data-stu-id="2fa85-104">Provides the common language runtime with information about an assembly reference that it should consider when performing an assembly reference closure walk.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="2fa85-105">語法</span><span class="sxs-lookup"><span data-stu-id="2fa85-105">Syntax</span></span>  
  
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
  
## <a name="members"></a><span data-ttu-id="2fa85-106">成員</span><span class="sxs-lookup"><span data-stu-id="2fa85-106">Members</span></span>  
  
|<span data-ttu-id="2fa85-107">member</span><span class="sxs-lookup"><span data-stu-id="2fa85-107">Member</span></span>|<span data-ttu-id="2fa85-108">描述</span><span class="sxs-lookup"><span data-stu-id="2fa85-108">Description</span></span>|  
|------------|-----------------|  
|`pbPublicKeyOrToken`|<span data-ttu-id="2fa85-109">組件的公開金鑰或語彙基元的指標。</span><span class="sxs-lookup"><span data-stu-id="2fa85-109">A pointer to the public key or token of the assembly.</span></span>|  
|`cbPublicKeyOrToken`|<span data-ttu-id="2fa85-110">公開金鑰或語彙基元中的位元組數。</span><span class="sxs-lookup"><span data-stu-id="2fa85-110">The number of bytes in the public key or token.</span></span>|  
|`szName`|<span data-ttu-id="2fa85-111">參考之組件的名稱。</span><span class="sxs-lookup"><span data-stu-id="2fa85-111">The name of the assembly that is referenced.</span></span>|  
|`pMetaData`|<span data-ttu-id="2fa85-112">組件中繼資料的指標。</span><span class="sxs-lookup"><span data-stu-id="2fa85-112">A pointer to the assembly's metadata.</span></span>|  
|`pbHashValue`|<span data-ttu-id="2fa85-113">雜湊二進位大型物件 (BLOB) 的指標。</span><span class="sxs-lookup"><span data-stu-id="2fa85-113">A pointer to a hash binary large object (BLOB).</span></span>|  
|`cbHashValue`|<span data-ttu-id="2fa85-114">雜湊 BLOB 中的位元組數。</span><span class="sxs-lookup"><span data-stu-id="2fa85-114">The number of bytes in the hash BLOB.</span></span>|  
|`dwAssemblyRefFlags`|<span data-ttu-id="2fa85-115">組件的旗標。</span><span class="sxs-lookup"><span data-stu-id="2fa85-115">The assembly's flags.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="2fa85-116">備註</span><span class="sxs-lookup"><span data-stu-id="2fa85-116">Remarks</span></span>  

 <span data-ttu-id="2fa85-117">`COR_PRF_EX_CLAUSE_INFO` 結構會在其宣告 Common Language Runtime 在執行組件參考關閉查核時應考量的其他組件參考時，由分析工具填入。</span><span class="sxs-lookup"><span data-stu-id="2fa85-117">The `COR_PRF_EX_CLAUSE_INFO` structure is populated by the profiler when it declares additional assembly references that the common language runtime should consider when performing an assembly reference closure walk.</span></span>  
  
 <span data-ttu-id="2fa85-118">如果 profiler 登錄 [ICorProfilerCallback6：： GetAssemblyReferences](icorprofilercallback6-getassemblyreferences-method.md) 回呼方法，則執行時間會傳遞要載入之元件的路徑和名稱，以及指向該方法的 [ICorProfilerAssemblyReferenceProvider](icorprofilerassemblyreferenceprovider-interface.md) 介面物件的指標。</span><span class="sxs-lookup"><span data-stu-id="2fa85-118">If the profiler registers for the [ICorProfilerCallback6::GetAssemblyReferences](icorprofilercallback6-getassemblyreferences-method.md) callback method, the runtime passes the path and name of the assembly to be loaded, along with a pointer to an [ICorProfilerAssemblyReferenceProvider](icorprofilerassemblyreferenceprovider-interface.md) interface object to that method.</span></span> <span data-ttu-id="2fa85-119">然後，分析工具可以[ICorProfilerAssemblyReferenceProvider::AddAssemblyReference](icorprofilerassemblyreferenceprovider-addassemblyreference-method.md) `COR_PRF_ASSEMBLY_REFERENCE_INFO` 針對其計畫從[ICorProfilerCallback6：： GetAssemblyReferences](icorprofilercallback6-getassemblyreferences-method.md)回呼中指定的元件參考的每個目標群組件，使用物件呼叫 ICorProfilerAssemblyReferenceProvider：： AddAssemblyReference 方法。</span><span class="sxs-lookup"><span data-stu-id="2fa85-119">The profiler can then call the [ICorProfilerAssemblyReferenceProvider::AddAssemblyReference](icorprofilerassemblyreferenceprovider-addassemblyreference-method.md) method with a `COR_PRF_ASSEMBLY_REFERENCE_INFO` object for each target assembly it plans to reference from the assembly specified in the [ICorProfilerCallback6::GetAssemblyReferences](icorprofilercallback6-getassemblyreferences-method.md) callback.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="2fa85-120">需求</span><span class="sxs-lookup"><span data-stu-id="2fa85-120">Requirements</span></span>  

 <span data-ttu-id="2fa85-121">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="2fa85-121">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="2fa85-122">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="2fa85-122">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="2fa85-123">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="2fa85-123">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="2fa85-124">**.NET Framework 版本：**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="2fa85-124">**.NET Framework Versions:** [!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="2fa85-125">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2fa85-125">See also</span></span>

- [<span data-ttu-id="2fa85-126">分析結構</span><span class="sxs-lookup"><span data-stu-id="2fa85-126">Profiling Structures</span></span>](profiling-structures.md)
- [<span data-ttu-id="2fa85-127">GetAssemblyReferences 方法</span><span class="sxs-lookup"><span data-stu-id="2fa85-127">GetAssemblyReferences Method</span></span>](icorprofilercallback6-getassemblyreferences-method.md)
- [<span data-ttu-id="2fa85-128">AddAssemblyReference 方法</span><span class="sxs-lookup"><span data-stu-id="2fa85-128">AddAssemblyReference Method</span></span>](icorprofilerassemblyreferenceprovider-addassemblyreference-method.md)
