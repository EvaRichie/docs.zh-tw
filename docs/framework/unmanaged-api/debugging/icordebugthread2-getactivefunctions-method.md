---
title: ICorDebugThread2::GetActiveFunctions 方法
ms.date: 03/30/2017
api_name:
- ICorDebugThread2.GetActiveFunctions
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread2::GetActiveFunctions
helpviewer_keywords:
- GetActiveFunctions method [.NET Framework debugging]
- ICorDebugThread2::GetActiveFunctions method [.NET Framework debugging]
ms.assetid: 27fae01a-ecec-423a-973e-24f8de55826c
topic_type:
- apiref
ms.openlocfilehash: e064a7db131a671adc4d0b6df522f3456e3a31d5
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/13/2020
ms.locfileid: "83377158"
---
# <a name="icordebugthread2getactivefunctions-method"></a><span data-ttu-id="74131-102">ICorDebugThread2::GetActiveFunctions 方法</span><span class="sxs-lookup"><span data-stu-id="74131-102">ICorDebugThread2::GetActiveFunctions Method</span></span>
<span data-ttu-id="74131-103">取得此執行緒每個框架中作用中函式的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="74131-103">Gets information about the active function in each of this thread's frames.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="74131-104">語法</span><span class="sxs-lookup"><span data-stu-id="74131-104">Syntax</span></span>  
  
```cpp  
HRESULT GetActiveFunctions (  
    [in]   ULONG32             cFunctions,  
    [out]  ULONG32             *pcFunctions,  
    [in, out, size_is(cFunctions), length_is(*pcFunctions)]  
        COR_ACTIVE_FUNCTION    pFunctions[]  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="74131-105">參數</span><span class="sxs-lookup"><span data-stu-id="74131-105">Parameters</span></span>  
 `cFunctions`  
 <span data-ttu-id="74131-106">[in] `pFunctions` 陣列的大小。</span><span class="sxs-lookup"><span data-stu-id="74131-106">[in] The size of the `pFunctions` array.</span></span>  
  
 `pcFunctions`  
 <span data-ttu-id="74131-107">脫銷陣列中傳回之物件數目的指標 `pFunctions` 。</span><span class="sxs-lookup"><span data-stu-id="74131-107">[out] A pointer to the number of objects returned in the `pFunctions` array.</span></span> <span data-ttu-id="74131-108">傳回的物件數目將等於堆疊上的受控框架數目。</span><span class="sxs-lookup"><span data-stu-id="74131-108">The number of objects returned will be equal to the number of managed frames on the stack.</span></span>  
  
 `pFunctions`  
 <span data-ttu-id="74131-109">[in、out]COR_ACTIVE_FUNCTION 物件的陣列，其中每一個都包含此執行緒框架中作用中函式的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="74131-109">[in, out] An array of COR_ACTIVE_FUNCTION objects, each of which contains information about the active functions in this thread's frames.</span></span>  
  
 <span data-ttu-id="74131-110">第一個元素將用於分葉框架，依此類推到堆疊的根目錄。</span><span class="sxs-lookup"><span data-stu-id="74131-110">The first element will be used for the leaf frame, and so on back to the root of the stack.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="74131-111">備註</span><span class="sxs-lookup"><span data-stu-id="74131-111">Remarks</span></span>  
 <span data-ttu-id="74131-112">如果 `pFunctions` 輸入上的是 null，則 `GetActiveFunctions` 只會傳回堆疊上的函式數目。</span><span class="sxs-lookup"><span data-stu-id="74131-112">If `pFunctions` is null on input, `GetActiveFunctions` returns only the number of functions that are on the stack.</span></span> <span data-ttu-id="74131-113">也就是說，如果 `pFunctions` 輸入上的是 null，則 `GetActiveFunctions` 只會在中傳回值 `pcFunctions` 。</span><span class="sxs-lookup"><span data-stu-id="74131-113">That is, If `pFunctions` is null on input, `GetActiveFunctions` returns a value only in `pcFunctions`.</span></span>  
  
 <span data-ttu-id="74131-114">`GetActiveFunctions`方法的目的是要在堆疊追蹤中從框架取得相同資訊的優化，而且只會包含在完整堆疊追蹤中已有 ICorDebugILFrame 物件的框架。</span><span class="sxs-lookup"><span data-stu-id="74131-114">The `GetActiveFunctions` method is intended as an optimization over getting the same information from frames in a stack trace, and includes only frames that would have had an ICorDebugILFrame object for them in the full stack trace.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="74131-115">需求</span><span class="sxs-lookup"><span data-stu-id="74131-115">Requirements</span></span>  
 <span data-ttu-id="74131-116">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="74131-116">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="74131-117">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="74131-117">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="74131-118">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="74131-118">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="74131-119">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="74131-119">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>
