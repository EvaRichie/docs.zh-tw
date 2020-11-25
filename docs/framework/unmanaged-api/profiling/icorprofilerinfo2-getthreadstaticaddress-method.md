---
title: ICorProfilerInfo2::GetThreadStaticAddress 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.GetThreadStaticAddress
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::GetThreadStaticAddress
helpviewer_keywords:
- GetThreadStaticAddress method [.NET Framework profiling]
- ICorProfilerInfo2::GetThreadStaticAddress method [.NET Framework profiling]
ms.assetid: 8e7dbf14-98a2-4384-a950-58a7640e59df
topic_type:
- apiref
ms.openlocfilehash: 8b9b76fd58d8b3ec5c2d98156b7935051aff074b
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95731214"
---
# <a name="icorprofilerinfo2getthreadstaticaddress-method"></a><span data-ttu-id="7657f-102">ICorProfilerInfo2::GetThreadStaticAddress 方法</span><span class="sxs-lookup"><span data-stu-id="7657f-102">ICorProfilerInfo2::GetThreadStaticAddress Method</span></span>

<span data-ttu-id="7657f-103">取得指定執行緒的範圍中指定之執行緒靜態欄位的位址。</span><span class="sxs-lookup"><span data-stu-id="7657f-103">Gets the address of the specified thread-static field that is in the scope of the specified thread.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="7657f-104">語法</span><span class="sxs-lookup"><span data-stu-id="7657f-104">Syntax</span></span>  
  
```cpp  
HRESULT GetThreadStaticAddress(  
    [in] ClassID     classId,  
    [in] mdFieldDef  fieldToken,  
    [in] ThreadID    threadId,  
    [out] void       **ppAddress);  
```  
  
## <a name="parameters"></a><span data-ttu-id="7657f-105">參數</span><span class="sxs-lookup"><span data-stu-id="7657f-105">Parameters</span></span>  

 `classId`  
 <span data-ttu-id="7657f-106">在包含所要求之執行緒靜態欄位之類別的識別碼。</span><span class="sxs-lookup"><span data-stu-id="7657f-106">[in] The ID of the class that contains the requested thread-static field.</span></span>  
  
 `fieldToken`  
 <span data-ttu-id="7657f-107">在所要求之執行緒靜態欄位的元資料標記。</span><span class="sxs-lookup"><span data-stu-id="7657f-107">[in] The metadata token for the requested thread-static field.</span></span>  
  
 `threadId`  
 <span data-ttu-id="7657f-108">在屬於所要求靜態欄位範圍之執行緒的識別碼。</span><span class="sxs-lookup"><span data-stu-id="7657f-108">[in] The ID of the thread that is the scope for the requested static field.</span></span>  
  
 `ppAddress`  
 <span data-ttu-id="7657f-109">擴展指定執行緒中靜態欄位的位址指標。</span><span class="sxs-lookup"><span data-stu-id="7657f-109">[out] A pointer to the address of the static field that is within the specified thread.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="7657f-110">備註</span><span class="sxs-lookup"><span data-stu-id="7657f-110">Remarks</span></span>  

 <span data-ttu-id="7657f-111">`GetThreadStaticAddress`方法可能會傳回下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="7657f-111">The `GetThreadStaticAddress` method may return one of the following:</span></span>  
  
- <span data-ttu-id="7657f-112">如果指定的靜態欄位未在指定的內容中指派位址，則為 CORPROF_E_DATAINCOMPLETE HRESULT。</span><span class="sxs-lookup"><span data-stu-id="7657f-112">A CORPROF_E_DATAINCOMPLETE HRESULT if the given static field has not been assigned an address in the specified context.</span></span>  
  
- <span data-ttu-id="7657f-113">可能位於垃圾收集堆積中之物件的位址。</span><span class="sxs-lookup"><span data-stu-id="7657f-113">The addresses of objects that may be in the garbage collection heap.</span></span> <span data-ttu-id="7657f-114">這些位址在垃圾收集之後可能會失效，因此在垃圾收集分析工具不應假設它們是有效的。</span><span class="sxs-lookup"><span data-stu-id="7657f-114">These addresses may become invalid after garbage collection, so after garbage collection profilers should not assume that they are valid.</span></span>  
  
 <span data-ttu-id="7657f-115">在類別的類別的函式完成之前， `GetThreadStaticAddress` 將會傳回其所有靜態欄位的 CORPROF_E_DATAINCOMPLETE，雖然某些靜態欄位可能已經初始化，並且會將垃圾收集物件的根。</span><span class="sxs-lookup"><span data-stu-id="7657f-115">Before a class’s class constructor is completed, `GetThreadStaticAddress` will return CORPROF_E_DATAINCOMPLETE for all its static fields, although some of the static fields may already be initialized and rooting garbage collection objects.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="7657f-116">需求</span><span class="sxs-lookup"><span data-stu-id="7657f-116">Requirements</span></span>  

 <span data-ttu-id="7657f-117">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="7657f-117">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="7657f-118">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="7657f-118">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="7657f-119">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="7657f-119">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="7657f-120">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="7657f-120">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="7657f-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="7657f-121">See also</span></span>

- [<span data-ttu-id="7657f-122">ICorProfilerInfo 介面</span><span class="sxs-lookup"><span data-stu-id="7657f-122">ICorProfilerInfo Interface</span></span>](icorprofilerinfo-interface.md)
- [<span data-ttu-id="7657f-123">ICorProfilerInfo2 介面</span><span class="sxs-lookup"><span data-stu-id="7657f-123">ICorProfilerInfo2 Interface</span></span>](icorprofilerinfo2-interface.md)
