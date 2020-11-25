---
title: ICorProfilerInfo::GetEventMask 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.GetEventMask
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::GetEventMask
helpviewer_keywords:
- GetEventMask method [.NET Framework profiling]
- ICorProfilerInfo::GetEventMask method [.NET Framework profiling]
ms.assetid: ec34cc13-45a3-4695-abc3-b3347d4e6fc2
topic_type:
- apiref
ms.openlocfilehash: 16bd8b09d5118171e669e9c428fb444384b5867d
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95722560"
---
# <a name="icorprofilerinfogeteventmask-method"></a><span data-ttu-id="4c718-102">ICorProfilerInfo::GetEventMask 方法</span><span class="sxs-lookup"><span data-stu-id="4c718-102">ICorProfilerInfo::GetEventMask Method</span></span>

<span data-ttu-id="4c718-103">取得分析工具想要從 Common Language Runtime (CLR) 接收事件通知的目前事件分類。</span><span class="sxs-lookup"><span data-stu-id="4c718-103">Gets the current event categories for which the profiler wants to receive event notifications from the common language runtime (CLR).</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="4c718-104">語法</span><span class="sxs-lookup"><span data-stu-id="4c718-104">Syntax</span></span>  
  
```cpp  
HRESULT GetEventMask(  
    [out] DWORD *pdwEvents);  
```  
  
## <a name="parameters"></a><span data-ttu-id="4c718-105">參數</span><span class="sxs-lookup"><span data-stu-id="4c718-105">Parameters</span></span>  

 `pdwEvents`  
 <span data-ttu-id="4c718-106">[out] 指定事件分類的 4 位元組值的指標。</span><span class="sxs-lookup"><span data-stu-id="4c718-106">[out] A pointer to a 4-byte value that specifies the categories of events.</span></span> <span data-ttu-id="4c718-107">每個位元各控制事件的不同功能、行為或類型。</span><span class="sxs-lookup"><span data-stu-id="4c718-107">Each bit controls a different capability, behavior, or type of event.</span></span> <span data-ttu-id="4c718-108">[COR_PRF_MONITOR](cor-prf-monitor-enumeration.md)列舉中會說明這些位。</span><span class="sxs-lookup"><span data-stu-id="4c718-108">The bits are described in the [COR_PRF_MONITOR](cor-prf-monitor-enumeration.md) enumeration.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="4c718-109">備註</span><span class="sxs-lookup"><span data-stu-id="4c718-109">Remarks</span></span>  
  
> [!NOTE]
> <span data-ttu-id="4c718-110">您應呼叫 [GetEventMask2](icorprofilerinfo5-geteventmask2-method.md) 方法，而不是此方法。</span><span class="sxs-lookup"><span data-stu-id="4c718-110">You should call the [GetEventMask2](icorprofilerinfo5-geteventmask2-method.md) method instead of this method.</span></span> <span data-ttu-id="4c718-111">雖然此 `SetEventMask` 方法會繼續受到支援，但 [GetEventMask2](icorprofilerinfo5-geteventmask2-method.md) 會提供額外的功能。</span><span class="sxs-lookup"><span data-stu-id="4c718-111">Although the `SetEventMask` method continues to be supported, [GetEventMask2](icorprofilerinfo5-geteventmask2-method.md) provides additional functionality.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="4c718-112">需求</span><span class="sxs-lookup"><span data-stu-id="4c718-112">Requirements</span></span>  

 <span data-ttu-id="4c718-113">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="4c718-113">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="4c718-114">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="4c718-114">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="4c718-115">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="4c718-115">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="4c718-116">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="4c718-116">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="4c718-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4c718-117">See also</span></span>

- [<span data-ttu-id="4c718-118">GetEventMask2 方法</span><span class="sxs-lookup"><span data-stu-id="4c718-118">GetEventMask2 Method</span></span>](icorprofilerinfo5-geteventmask2-method.md)
- [<span data-ttu-id="4c718-119">ICorProfilerInfo 介面</span><span class="sxs-lookup"><span data-stu-id="4c718-119">ICorProfilerInfo Interface</span></span>](icorprofilerinfo-interface.md)
