---
title: ICorDebugChain::GetStackRange 方法
ms.date: 03/30/2017
api_name:
- ICorDebugChain.GetStackRange
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugChain::GetStackRange
helpviewer_keywords:
- ICorDebugChain::GetStackRange method [.NET Framework debugging]
- GetStackRange method, ICorDebugChain interface [.NET Framework debugging]
ms.assetid: 554284e7-3f6c-4d40-8da5-1c9317fbd484
topic_type:
- apiref
ms.openlocfilehash: 841e3ca608d20a4b8618508e69195de0b1da1341
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95724386"
---
# <a name="icordebugchaingetstackrange-method"></a><span data-ttu-id="a3085-102">ICorDebugChain::GetStackRange 方法</span><span class="sxs-lookup"><span data-stu-id="a3085-102">ICorDebugChain::GetStackRange Method</span></span>

<span data-ttu-id="a3085-103">取得此鏈之堆疊區段的位址範圍。</span><span class="sxs-lookup"><span data-stu-id="a3085-103">Gets the address range of the stack segment for this chain.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="a3085-104">語法</span><span class="sxs-lookup"><span data-stu-id="a3085-104">Syntax</span></span>  
  
```cpp  
HRESULT GetStackRange (  
    [out] CORDB_ADDRESS      *pStart,
    [out] CORDB_ADDRESS      *pEnd  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="a3085-105">參數</span><span class="sxs-lookup"><span data-stu-id="a3085-105">Parameters</span></span>  

 `pStart`  
 <span data-ttu-id="a3085-106">擴展值的指標，此 `CORDB_ADDRESS` 值是堆疊區段的起始位址。</span><span class="sxs-lookup"><span data-stu-id="a3085-106">[out] A pointer to a `CORDB_ADDRESS` value that is the starting address of the stack segment.</span></span>  
  
 `pEnd`  
 <span data-ttu-id="a3085-107">擴展值的指標，此 `CORDB_ADDRESS` 值是堆疊區段的結束位址。</span><span class="sxs-lookup"><span data-stu-id="a3085-107">[out] A pointer to a `CORDB_ADDRESS` value that is the ending address of the stack segment.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="a3085-108">備註</span><span class="sxs-lookup"><span data-stu-id="a3085-108">Remarks</span></span>  

 <span data-ttu-id="a3085-109">只有在比較堆疊框架位置時，數值範圍才有意義。</span><span class="sxs-lookup"><span data-stu-id="a3085-109">The numeric range is meaningful only for comparison of stack frame locations.</span></span> <span data-ttu-id="a3085-110">您無法對實際儲存在堆疊上的內容做出任何假設。</span><span class="sxs-lookup"><span data-stu-id="a3085-110">You cannot make any assumptions about what is actually stored on the stack.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="a3085-111">需求</span><span class="sxs-lookup"><span data-stu-id="a3085-111">Requirements</span></span>  

 <span data-ttu-id="a3085-112">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="a3085-112">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="a3085-113">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="a3085-113">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="a3085-114">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="a3085-114">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="a3085-115">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="a3085-115">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>
