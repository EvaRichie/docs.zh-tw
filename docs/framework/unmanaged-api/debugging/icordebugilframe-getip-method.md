---
title: ICorDebugILFrame::GetIP 方法
ms.date: 03/30/2017
api_name:
- ICorDebugILFrame.GetIP
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugILFrame::GetIP
helpviewer_keywords:
- GetIP method, ICorDebugILFrame interface [.NET Framework debugging]
- ICorDebugILFrame::GetIP method [.NET Framework debugging]
ms.assetid: 18217ba1-1776-4297-a3b9-f77e64b0fead
topic_type:
- apiref
ms.openlocfilehash: 314d2a06c8e246a42b315690dc9fe4b507db285a
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95703167"
---
# <a name="icordebugilframegetip-method"></a><span data-ttu-id="45b33-102">ICorDebugILFrame::GetIP 方法</span><span class="sxs-lookup"><span data-stu-id="45b33-102">ICorDebugILFrame::GetIP Method</span></span>

<span data-ttu-id="45b33-103">取得指令指標的值，以及描述如何取得指令指標值的位組合值。</span><span class="sxs-lookup"><span data-stu-id="45b33-103">Gets the value of the instruction pointer and a bitwise combination value that describes how the value of the instruction pointer was obtained.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="45b33-104">語法</span><span class="sxs-lookup"><span data-stu-id="45b33-104">Syntax</span></span>  
  
```cpp  
HRESULT GetIP (  
    [out] ULONG32               *pnOffset,
    [out] CorDebugMappingResult *pMappingResult  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="45b33-105">參數</span><span class="sxs-lookup"><span data-stu-id="45b33-105">Parameters</span></span>  

 `pnOffset`  
 <span data-ttu-id="45b33-106">擴展指令指標的值。</span><span class="sxs-lookup"><span data-stu-id="45b33-106">[out] The value of the instruction pointer.</span></span>  
  
 `pMappingResult`  
 <span data-ttu-id="45b33-107">擴展CorDebugMappingResult 列舉值的位元組合指標，描述如何取得指令指標的值。</span><span class="sxs-lookup"><span data-stu-id="45b33-107">[out] A pointer to a bitwise combination of the CorDebugMappingResult enumeration values that describe how the value of the instruction pointer was obtained.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="45b33-108">備註</span><span class="sxs-lookup"><span data-stu-id="45b33-108">Remarks</span></span>  

 <span data-ttu-id="45b33-109">指令指標的值為函式之 Microsoft 中繼語言 (MSIL) 程式碼的堆疊框架位移。</span><span class="sxs-lookup"><span data-stu-id="45b33-109">The value of the instruction pointer is the stack frame's offset into the function's Microsoft intermediate language (MSIL) code.</span></span> <span data-ttu-id="45b33-110">如果堆疊框架為使用中，則此位址是下一個要執行的指令。</span><span class="sxs-lookup"><span data-stu-id="45b33-110">If the stack frame is active, this address is the next instruction to execute.</span></span> <span data-ttu-id="45b33-111">如果堆疊框架不在使用中，此位址是在堆疊框架重新開機時要執行的下一個指令。</span><span class="sxs-lookup"><span data-stu-id="45b33-111">If the stack frame is not active, this address is the next instruction to execute when the stack frame is reactivated.</span></span>  
  
 <span data-ttu-id="45b33-112">如果這個框架是即時 (JIT) 編譯的框架，指令指標的值將會由從實際的原生指令指標反向對應來決定，因此值可能只是近似。</span><span class="sxs-lookup"><span data-stu-id="45b33-112">If this frame is a just-in-time (JIT) compiled frame, the value of the instruction pointer will be determined by mapping backwards from the actual native instruction pointer, so the value may be only approximate.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="45b33-113">需求</span><span class="sxs-lookup"><span data-stu-id="45b33-113">Requirements</span></span>  

 <span data-ttu-id="45b33-114">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="45b33-114">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="45b33-115">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="45b33-115">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="45b33-116">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="45b33-116">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="45b33-117">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="45b33-117">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>
