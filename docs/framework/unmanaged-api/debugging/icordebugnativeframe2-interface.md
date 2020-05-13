---
title: ICorDebugNativeFrame2 介面
ms.date: 03/30/2017
api_name:
- ICorDebugNativeFrame2
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugNativeFrame2
helpviewer_keywords:
- ICorDebugNativeFrame2 interface [.NET Framework debugging]
ms.assetid: 52a80838-af36-4399-bc97-d8a4c6d76df2
topic_type:
- apiref
ms.openlocfilehash: cd2a2821128ad9265e8a831f7b02792e6453b1ee
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213786"
---
# <a name="icordebugnativeframe2-interface"></a><span data-ttu-id="e7496-102">ICorDebugNativeFrame2 介面</span><span class="sxs-lookup"><span data-stu-id="e7496-102">ICorDebugNativeFrame2 Interface</span></span>
<span data-ttu-id="e7496-103">提供測試父子框架關聯的方法。</span><span class="sxs-lookup"><span data-stu-id="e7496-103">Provides methods that test for child and parent frame relationships.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="e7496-104">方法</span><span class="sxs-lookup"><span data-stu-id="e7496-104">Methods</span></span>  
  
|<span data-ttu-id="e7496-105">方法</span><span class="sxs-lookup"><span data-stu-id="e7496-105">Method</span></span>|<span data-ttu-id="e7496-106">描述</span><span class="sxs-lookup"><span data-stu-id="e7496-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="e7496-107">IsChild 方法</span><span class="sxs-lookup"><span data-stu-id="e7496-107">IsChild Method</span></span>](icordebugnativeframe2-ischild-method.md)|<span data-ttu-id="e7496-108">判斷目前的框架是否為子框架。</span><span class="sxs-lookup"><span data-stu-id="e7496-108">Determines whether the current frame is a child frame.</span></span>|  
|[<span data-ttu-id="e7496-109">IsMatchingParentFrame 方法</span><span class="sxs-lookup"><span data-stu-id="e7496-109">IsMatchingParentFrame Method</span></span>](icordebugnativeframe2-ismatchingparentframe-method.md)|<span data-ttu-id="e7496-110">判斷指定的框架是否為目前框架的父系。</span><span class="sxs-lookup"><span data-stu-id="e7496-110">Determines whether the specified frame is the parent of the current frame.</span></span>|  
|[<span data-ttu-id="e7496-111">GetStackParameterSize 方法</span><span class="sxs-lookup"><span data-stu-id="e7496-111">GetStackParameterSize Method</span></span>](icordebugnativeframe2-getstackparametersize-method.md)|<span data-ttu-id="e7496-112">傳回 x86 作業系統上堆疊上的參數累計大小。</span><span class="sxs-lookup"><span data-stu-id="e7496-112">Returns the cumulative size of the parameters on the stack on x86 operating systems.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="e7496-113">備註</span><span class="sxs-lookup"><span data-stu-id="e7496-113">Remarks</span></span>  
 <span data-ttu-id="e7496-114">此介面會以邏輯方式擴充 "ICorDebugNativeFrame" 介面。</span><span class="sxs-lookup"><span data-stu-id="e7496-114">This interface logically extends the "ICorDebugNativeFrame" interface.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="e7496-115">這個介面不支援跨電腦或跨處理序的遠端呼叫。</span><span class="sxs-lookup"><span data-stu-id="e7496-115">This interface does not support being called remotely, either cross-machine or cross-process.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="e7496-116">需求</span><span class="sxs-lookup"><span data-stu-id="e7496-116">Requirements</span></span>  
 <span data-ttu-id="e7496-117">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="e7496-117">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="e7496-118">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="e7496-118">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="e7496-119">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="e7496-119">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="e7496-120">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="e7496-120">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e7496-121">請參閱</span><span class="sxs-lookup"><span data-stu-id="e7496-121">See also</span></span>

- [<span data-ttu-id="e7496-122">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="e7496-122">Debugging Interfaces</span></span>](debugging-interfaces.md)
- [<span data-ttu-id="e7496-123">偵錯</span><span class="sxs-lookup"><span data-stu-id="e7496-123">Debugging</span></span>](index.md)
