---
title: ICorDebugBreakpoint::IsActive 方法
ms.date: 03/30/2017
api_name:
- ICorDebugBreakpoint.IsActive
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugBreakpoint::IsActive
helpviewer_keywords:
- ICorDebugBreakpoint::IsActive method [.NET Framework debugging]
- IsActive method, ICorDebugBreakpoint interface [.NET Framework debugging]
ms.assetid: 06e583d6-d88a-4ff5-bb95-5c48618a461c
topic_type:
- apiref
ms.openlocfilehash: 064f9727b221dd64a58f8cd5e103271e37020786
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95730171"
---
# <a name="icordebugbreakpointisactive-method"></a><span data-ttu-id="3fc8f-102">ICorDebugBreakpoint::IsActive 方法</span><span class="sxs-lookup"><span data-stu-id="3fc8f-102">ICorDebugBreakpoint::IsActive Method</span></span>

<span data-ttu-id="3fc8f-103">取得值，這個值表示這是否 `ICorDebugBreakpoint` 為使用中。</span><span class="sxs-lookup"><span data-stu-id="3fc8f-103">Gets a value that indicates whether this `ICorDebugBreakpoint` is active.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="3fc8f-104">語法</span><span class="sxs-lookup"><span data-stu-id="3fc8f-104">Syntax</span></span>  
  
```cpp  
HRESULT IsActive (  
    [out] BOOL *pbActive  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="3fc8f-105">參數</span><span class="sxs-lookup"><span data-stu-id="3fc8f-105">Parameters</span></span>  

 `pbActive`  
 <span data-ttu-id="3fc8f-106">[out] `true` 如果這個中斷點作用中;否則為 `false` 。</span><span class="sxs-lookup"><span data-stu-id="3fc8f-106">[out] `true` if this breakpoint is active; otherwise, `false`.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="3fc8f-107">需求</span><span class="sxs-lookup"><span data-stu-id="3fc8f-107">Requirements</span></span>  

 <span data-ttu-id="3fc8f-108">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="3fc8f-108">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="3fc8f-109">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="3fc8f-109">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="3fc8f-110">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="3fc8f-110">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="3fc8f-111">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="3fc8f-111">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>
