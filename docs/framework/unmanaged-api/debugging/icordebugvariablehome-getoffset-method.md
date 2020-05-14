---
title: ICorDebugVariableHome：： GetOffset 方法
ms.date: 03/30/2017
api_name:
- ICorDebugVariableHome.GetOffset
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugVariableHome::GetOffset
helpviewer_keywords:
- ICorDebugVariableHome::GetOffset method [.NET Framework debugging]
- GetOffset method, ICorDebugVariableHome interface [.NET Framework debugging]
ms.assetid: f025c2e5-3f6c-4be8-9ffe-c8b214617dfe
topic_type:
- apiref
ms.openlocfilehash: 75a165e2fd517f36d779a934a5bdd9c41956411a
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/14/2020
ms.locfileid: "83396758"
---
# <a name="icordebugvariablehomegetoffset-method"></a><span data-ttu-id="6539c-102">ICorDebugVariableHome：： GetOffset 方法</span><span class="sxs-lookup"><span data-stu-id="6539c-102">ICorDebugVariableHome::GetOffset Method</span></span>
<span data-ttu-id="6539c-103">取得變數基底暫存器的位移。</span><span class="sxs-lookup"><span data-stu-id="6539c-103">Gets the offset from the base register for a variable.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="6539c-104">語法</span><span class="sxs-lookup"><span data-stu-id="6539c-104">Syntax</span></span>  
  
```cpp  
HRESULT GetOffset(  
    [out] LONG *pOffset  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="6539c-105">參數</span><span class="sxs-lookup"><span data-stu-id="6539c-105">Parameters</span></span>  
 `pOffset`  
 <span data-ttu-id="6539c-106">脫銷基底暫存器的位移。</span><span class="sxs-lookup"><span data-stu-id="6539c-106">[out] The offset from the base register.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="6539c-107">傳回值</span><span class="sxs-lookup"><span data-stu-id="6539c-107">Return Value</span></span>  
 <span data-ttu-id="6539c-108">方法會傳回下列值：</span><span class="sxs-lookup"><span data-stu-id="6539c-108">The method returns the following values:</span></span>  
  
|<span data-ttu-id="6539c-109">值</span><span class="sxs-lookup"><span data-stu-id="6539c-109">Value</span></span>|<span data-ttu-id="6539c-110">說明</span><span class="sxs-lookup"><span data-stu-id="6539c-110">Description</span></span>|  
|-----------|-----------------|  
|`S_OK`|<span data-ttu-id="6539c-111">變數位於暫存器相對的記憶體位置。</span><span class="sxs-lookup"><span data-stu-id="6539c-111">The variable is in a register-relative memory location.</span></span>|  
|`E_FAIL`|<span data-ttu-id="6539c-112">變數不在暫存器相對的記憶體位置。</span><span class="sxs-lookup"><span data-stu-id="6539c-112">The variable is not in a register-relative memory location.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="6539c-113">需求</span><span class="sxs-lookup"><span data-stu-id="6539c-113">Requirements</span></span>  
 <span data-ttu-id="6539c-114">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="6539c-114">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="6539c-115">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="6539c-115">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="6539c-116">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="6539c-116">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="6539c-117">**.NET Framework 版本：**[!INCLUDE[net_current_v462plus](../../../../includes/net-current-v462plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="6539c-117">**.NET Framework Versions:** [!INCLUDE[net_current_v462plus](../../../../includes/net-current-v462plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="6539c-118">請參閱</span><span class="sxs-lookup"><span data-stu-id="6539c-118">See also</span></span>

- [<span data-ttu-id="6539c-119">ICorDebugVariableHome 介面</span><span class="sxs-lookup"><span data-stu-id="6539c-119">ICorDebugVariableHome Interface</span></span>](icordebugvariablehome-interface.md)
