---
title: ICorDebugObjectEnum::Next 方法
ms.date: 03/30/2017
api_name:
- ICorDebugObjectEnum.Next
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugObjectEnum::Next
helpviewer_keywords:
- Next method, ICorDebugObjectEnum interface [.NET Framework debugging]
- ICorDebugObjectEnum::Next method [.NET Framework debugging]
ms.assetid: 10093e3d-26b6-4ad7-8ef3-bbf66243fc02
topic_type:
- apiref
ms.openlocfilehash: 70514464f27d6123a4de1d5800ed016a39541287
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83207548"
---
# <a name="icordebugobjectenumnext-method"></a><span data-ttu-id="a8391-102">ICorDebugObjectEnum::Next 方法</span><span class="sxs-lookup"><span data-stu-id="a8391-102">ICorDebugObjectEnum::Next Method</span></span>
<span data-ttu-id="a8391-103">從目前位置開始，取得列舉中指定物件數目的相對虛擬位址（Rva）。</span><span class="sxs-lookup"><span data-stu-id="a8391-103">Gets the relative virtual addresses (RVAs) of the specified number of objects from the enumeration, starting at the current position.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="a8391-104">語法</span><span class="sxs-lookup"><span data-stu-id="a8391-104">Syntax</span></span>  
  
```cpp  
HRESULT Next (  
    [in] ULONG celt,  
    [out, size_is(celt), length_is(*pceltFetched)]
        CORDB_ADDRESS objects[],  
    [out] ULONG *pceltFetched  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="a8391-105">參數</span><span class="sxs-lookup"><span data-stu-id="a8391-105">Parameters</span></span>  
 `celt`  
 <span data-ttu-id="a8391-106">[in] 要擷取的物件數目。</span><span class="sxs-lookup"><span data-stu-id="a8391-106">[in] The number of objects to be retrieved.</span></span>  
  
 `objects`  
 <span data-ttu-id="a8391-107">脫銷指標陣列，其中每一個都會指向 CORDB_ADDRESS 物件。</span><span class="sxs-lookup"><span data-stu-id="a8391-107">[out] An array of pointers, each of which points to a CORDB_ADDRESS object.</span></span>  
  
 `pceltFetched`  
 <span data-ttu-id="a8391-108">脫銷實際傳回之物件數目的指標。</span><span class="sxs-lookup"><span data-stu-id="a8391-108">[out] Pointer to the number of objects actually returned.</span></span> <span data-ttu-id="a8391-109">如果是一個，這個值可能會是 null `celt` 。</span><span class="sxs-lookup"><span data-stu-id="a8391-109">This value may be null if `celt` is one.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="a8391-110">需求</span><span class="sxs-lookup"><span data-stu-id="a8391-110">Requirements</span></span>  
 <span data-ttu-id="a8391-111">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="a8391-111">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="a8391-112">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="a8391-112">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="a8391-113">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="a8391-113">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="a8391-114">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="a8391-114">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a8391-115">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a8391-115">See also</span></span>
