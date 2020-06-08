---
title: ICorProfilerCallback::COMClassicVTableCreated 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.COMClassicVTableCreated
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::COMClassicVTableCreated
helpviewer_keywords:
- COMClassicVTableCreated method [.NET Framework profiling]
- ICorProfilerCallback::COMClassicVTableCreated method [.NET Framework profiling]
ms.assetid: 6e1834ab-c359-498a-b10b-984ae23cdda4
topic_type:
- apiref
ms.openlocfilehash: 6c9ec6af90cc47c3c01621563a9813789c25aa1d
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500334"
---
# <a name="icorprofilercallbackcomclassicvtablecreated-method"></a><span data-ttu-id="336b8-102">ICorProfilerCallback::COMClassicVTableCreated 方法</span><span class="sxs-lookup"><span data-stu-id="336b8-102">ICorProfilerCallback::COMClassicVTableCreated Method</span></span>
<span data-ttu-id="336b8-103">通知分析工具，指定之 IID 和類別的 COM Interop vtable 已建立。</span><span class="sxs-lookup"><span data-stu-id="336b8-103">Notifies the profiler that a COM interop vtable for the specified IID and class has been created.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="336b8-104">語法</span><span class="sxs-lookup"><span data-stu-id="336b8-104">Syntax</span></span>  
  
```cpp  
HRESULT COMClassicVTableCreated(  
    [in] ClassID wrappedClassId,  
    [in] REFGUID implementedIID,  
    [in] void    *pVTable,  
    [in] ULONG   cSlots);  
```  
  
## <a name="parameters"></a><span data-ttu-id="336b8-105">參數</span><span class="sxs-lookup"><span data-stu-id="336b8-105">Parameters</span></span>

- `wrappedClasId`

  <span data-ttu-id="336b8-106">\[in] 已建立 vtable 之類別的識別碼。</span><span class="sxs-lookup"><span data-stu-id="336b8-106">\[in] The ID of the class for which the vtable has been created.</span></span>

- `implementedIID`

  <span data-ttu-id="336b8-107">\[in] 類別所實作為介面的識別碼。</span><span class="sxs-lookup"><span data-stu-id="336b8-107">\[in] The ID of the interface implemented by the class.</span></span> <span data-ttu-id="336b8-108">如果介面僅供內部用，這個值可能會是 Null。</span><span class="sxs-lookup"><span data-stu-id="336b8-108">This value may be NULL if the interface is internal only.</span></span>

- `pVTable`

  <span data-ttu-id="336b8-109">\[in] vtable 開頭的指標。</span><span class="sxs-lookup"><span data-stu-id="336b8-109">\[in] A pointer to the start of the vtable.</span></span>

- `cSlots`

  <span data-ttu-id="336b8-110">\[in] vtable 中的插槽數目。</span><span class="sxs-lookup"><span data-stu-id="336b8-110">\[in] The number of slots that are in the vtable.</span></span>

## <a name="remarks"></a><span data-ttu-id="336b8-111">備註</span><span class="sxs-lookup"><span data-stu-id="336b8-111">Remarks</span></span>  
 <span data-ttu-id="336b8-112">分析工具不應在此方法的執行中封鎖，因為堆疊可能不是處於允許垃圾收集的狀態，因此無法啟用「搶先垃圾收集」。</span><span class="sxs-lookup"><span data-stu-id="336b8-112">The profiler should not block in its implementation of this method because the stack may not be in a state that allows garbage collection, and therefore preemptive garbage collection cannot be enabled.</span></span> <span data-ttu-id="336b8-113">如果分析工具在此處封鎖並嘗試垃圾收集，執行時間將會封鎖，直到這個回呼傳回為止。</span><span class="sxs-lookup"><span data-stu-id="336b8-113">If the profiler blocks here and garbage collection is attempted, the runtime will block until this callback returns.</span></span>  
  
 <span data-ttu-id="336b8-114">分析工具的此方法的執行不應呼叫 managed 程式碼，或以任何方式進行，以造成 managed 記憶體配置。</span><span class="sxs-lookup"><span data-stu-id="336b8-114">The profiler's implementation of this method should not call into managed code or in any way cause a managed-memory allocation.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="336b8-115">規格需求</span><span class="sxs-lookup"><span data-stu-id="336b8-115">Requirements</span></span>  
 <span data-ttu-id="336b8-116">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="336b8-116">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="336b8-117">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="336b8-117">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="336b8-118">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="336b8-118">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="336b8-119">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="336b8-119">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="336b8-120">另請參閱</span><span class="sxs-lookup"><span data-stu-id="336b8-120">See also</span></span>

- [<span data-ttu-id="336b8-121">ICorProfilerCallback 介面</span><span class="sxs-lookup"><span data-stu-id="336b8-121">ICorProfilerCallback Interface</span></span>](icorprofilercallback-interface.md)
- [<span data-ttu-id="336b8-122">COMClassicVTableDestroyed 方法</span><span class="sxs-lookup"><span data-stu-id="336b8-122">COMClassicVTableDestroyed Method</span></span>](icorprofilercallback-comclassicvtabledestroyed-method.md)
