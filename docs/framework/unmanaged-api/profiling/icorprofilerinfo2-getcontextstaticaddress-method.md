---
title: ICorProfilerInfo2::GetContextStaticAddress 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.GetContextStaticAddress
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::GetContextStaticAddress
helpviewer_keywords:
- GetContextStaticAddress method [.NET Framework profiling]
- ICorProfilerInfo2::GetContextStaticAddress method [.NET Framework profiling]
ms.assetid: 2b374116-0972-416a-8cf5-79213129be9a
topic_type:
- apiref
ms.openlocfilehash: 7550caaa7cb4d7ed77dc36ecf0ce0e0cbc541db7
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84497058"
---
# <a name="icorprofilerinfo2getcontextstaticaddress-method"></a><span data-ttu-id="0dc3b-102">ICorProfilerInfo2::GetContextStaticAddress 方法</span><span class="sxs-lookup"><span data-stu-id="0dc3b-102">ICorProfilerInfo2::GetContextStaticAddress Method</span></span>
<span data-ttu-id="0dc3b-103">取得位於指定內容約制內指定內容靜態欄位的位址。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-103">Gets the address for the specified context-static field that is in the scope of the specified context.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="0dc3b-104">語法</span><span class="sxs-lookup"><span data-stu-id="0dc3b-104">Syntax</span></span>  
  
```cpp  
HRESULT GetContextStaticAddress(  
    [in] ClassID classId,  
    [in] mdFieldDef fieldToken,  
    [in] ContextID contextId,  
    [out] void **ppAddress);  
```  
  
## <a name="parameters"></a><span data-ttu-id="0dc3b-105">參數</span><span class="sxs-lookup"><span data-stu-id="0dc3b-105">Parameters</span></span>  
 `classId`  
 <span data-ttu-id="0dc3b-106">在包含所要求內容靜態欄位之類別的識別碼。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-106">[in] The ID of the class that contains the requested context-static field.</span></span>  
  
 `fieldToken`  
 <span data-ttu-id="0dc3b-107">在所要求內容靜態欄位的元資料標記。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-107">[in] The metadata token for the requested context-static field.</span></span>  
  
 `contextId`  
 <span data-ttu-id="0dc3b-108">在內容的識別碼，這是所要求內容靜態欄位的範圍。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-108">[in] The ID of the context that is the scope for the requested context-static field.</span></span>  
  
 `ppAddress`  
 <span data-ttu-id="0dc3b-109">脫銷位於指定內容內之靜態欄位位址的指標。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-109">[out] A pointer to the address of the static field that is within the specified context.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="0dc3b-110">備註</span><span class="sxs-lookup"><span data-stu-id="0dc3b-110">Remarks</span></span>  
 <span data-ttu-id="0dc3b-111">`GetContextStaticAddress`方法可能會傳回下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="0dc3b-111">The `GetContextStaticAddress` method may return one of the following:</span></span>  
  
- <span data-ttu-id="0dc3b-112">如果未在指定的內容中指派位址給給定的靜態欄位，CORPROF_E_DATAINCOMPLETE HRESULT。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-112">A CORPROF_E_DATAINCOMPLETE HRESULT if the given static field has not been assigned an address in the specified context.</span></span>  
  
- <span data-ttu-id="0dc3b-113">可能位於垃圾收集堆積中之物件的位址。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-113">The addresses of objects that may be in the garbage collection heap.</span></span> <span data-ttu-id="0dc3b-114">這些位址在垃圾收集後可能會變成無效，因此在垃圾收集之後，分析工具不應假設它們是有效的。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-114">These addresses may become invalid after garbage collection, so after garbage collection, profilers should not assume that they are valid.</span></span>  
  
 <span data-ttu-id="0dc3b-115">在類別的類別的函式完成之前， `GetContextStaticAddress` 會傳回其所有靜態欄位的 CORPROF_E_DATAINCOMPLETE，雖然某些靜態欄位可能已經初始化，並且會對垃圾收集物件進行根。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-115">Before a class’s class constructor is completed, `GetContextStaticAddress` will return CORPROF_E_DATAINCOMPLETE for all its static fields, although some of the static fields may already be initialized and rooting garbage collection objects.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="0dc3b-116">規格需求</span><span class="sxs-lookup"><span data-stu-id="0dc3b-116">Requirements</span></span>  
 <span data-ttu-id="0dc3b-117">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-117">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="0dc3b-118">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="0dc3b-118">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="0dc3b-119">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="0dc3b-119">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="0dc3b-120">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="0dc3b-120">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="0dc3b-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0dc3b-121">See also</span></span>

- [<span data-ttu-id="0dc3b-122">ICorProfilerInfo 介面</span><span class="sxs-lookup"><span data-stu-id="0dc3b-122">ICorProfilerInfo Interface</span></span>](icorprofilerinfo-interface.md)
- [<span data-ttu-id="0dc3b-123">ICorProfilerInfo2 介面</span><span class="sxs-lookup"><span data-stu-id="0dc3b-123">ICorProfilerInfo2 Interface</span></span>](icorprofilerinfo2-interface.md)
