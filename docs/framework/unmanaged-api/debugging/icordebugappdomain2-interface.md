---
title: ICorDebugAppDomain2 介面
ms.date: 03/30/2017
api_name:
- ICorDebugAppDomain2
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugAppDomain2
helpviewer_keywords:
- ICorDebugAppDomain2 interface [.NET Framework debugging]
ms.assetid: 314d29f3-feb0-4a92-9530-b569c280cc31
topic_type:
- apiref
ms.openlocfilehash: 1643d91f373ff233540026440ee21aa4c146f3e3
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82895140"
---
# <a name="icordebugappdomain2-interface"></a><span data-ttu-id="98101-102">ICorDebugAppDomain2 介面</span><span class="sxs-lookup"><span data-stu-id="98101-102">ICorDebugAppDomain2 Interface</span></span>

<span data-ttu-id="98101-103">提供使用陣列、指標、函式指標和參考型別的方法。</span><span class="sxs-lookup"><span data-stu-id="98101-103">Provides methods to work with arrays, pointers, function pointers, and reference types.</span></span> <span data-ttu-id="98101-104">這個介面是 ICorDebugAppDomain 介面的延伸。</span><span class="sxs-lookup"><span data-stu-id="98101-104">This interface is an extension of the ICorDebugAppDomain interface.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="98101-105">方法</span><span class="sxs-lookup"><span data-stu-id="98101-105">Methods</span></span>  
  
|<span data-ttu-id="98101-106">方法</span><span class="sxs-lookup"><span data-stu-id="98101-106">Method</span></span>|<span data-ttu-id="98101-107">描述</span><span class="sxs-lookup"><span data-stu-id="98101-107">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="98101-108">GetArrayOrPointerType 方法</span><span class="sxs-lookup"><span data-stu-id="98101-108">GetArrayOrPointerType Method</span></span>](icordebugappdomain2-getarrayorpointertype-method.md)|<span data-ttu-id="98101-109">取得指定類型的陣列，或指定之類型的指標或參考。</span><span class="sxs-lookup"><span data-stu-id="98101-109">Gets an array of the specified type, or a pointer or reference to the specified type.</span></span>|  
|[<span data-ttu-id="98101-110">GetFunctionPointerType</span><span class="sxs-lookup"><span data-stu-id="98101-110">GetFunctionPointerType</span></span>](icordebugappdomain2-getfunctionpointertype-method.md)|<span data-ttu-id="98101-111">取得具有指定簽章之函式的指標。</span><span class="sxs-lookup"><span data-stu-id="98101-111">Gets a pointer to a function that has a given signature.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="98101-112">備註</span><span class="sxs-lookup"><span data-stu-id="98101-112">Remarks</span></span>  
  
> [!NOTE]
> <span data-ttu-id="98101-113">這個介面不支援跨電腦或跨處理序的遠端呼叫。</span><span class="sxs-lookup"><span data-stu-id="98101-113">This interface does not support being called remotely, either cross-machine or cross-process.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="98101-114">需求</span><span class="sxs-lookup"><span data-stu-id="98101-114">Requirements</span></span>  
 <span data-ttu-id="98101-115">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="98101-115">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="98101-116">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="98101-116">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="98101-117">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="98101-117">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="98101-118">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="98101-118">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="98101-119">另請參閱</span><span class="sxs-lookup"><span data-stu-id="98101-119">See also</span></span>

- [<span data-ttu-id="98101-120">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="98101-120">Debugging Interfaces</span></span>](debugging-interfaces.md)
