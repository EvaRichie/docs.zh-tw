---
title: ICorDebugDataTarget::ReadVirtual 方法
ms.date: 03/30/2017
api_name:
- ICorDebugDataTarget.ReadVirtual Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugDataTarget::ReadVirtual
helpviewer_keywords:
- ICorDebugDataTarget::ReadVirtual method [.NET Framework debugging]
- ReadVirtual method, ICorDebugDataTarget interface [.NET Framework debugging]
ms.assetid: 55e57640-b3d2-413d-b4f4-fbc27fb8e37c
topic_type:
- apiref
ms.openlocfilehash: 36a18d92f05db55957bba55de84490c0da1a1f86
ms.sourcegitcommit: fff146ba3fd1762c8c432d95c8b877825ae536fc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/08/2020
ms.locfileid: "82976508"
---
# <a name="icordebugdatatargetreadvirtual-method"></a><span data-ttu-id="d0802-102">ICorDebugDataTarget::ReadVirtual 方法</span><span class="sxs-lookup"><span data-stu-id="d0802-102">ICorDebugDataTarget::ReadVirtual Method</span></span>
<span data-ttu-id="d0802-103">從指定的位址開始，取得連續記憶體的區塊，並將它傳回給提供的緩衝區。</span><span class="sxs-lookup"><span data-stu-id="d0802-103">Gets a block of contiguous memory starting at the specified address, and returns it in the supplied buffer.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="d0802-104">語法</span><span class="sxs-lookup"><span data-stu-id="d0802-104">Syntax</span></span>  
  
```cpp  
HRESULT ReadVirtual(  
    [in] CORDB_ADDRESS   address,  
    [out, size_is(bytesRequested), length_is(*pBytesRead)]  
          BYTE *     pBuffer,  
    [in]  ULONG32    bytesRequested,  
    [out] ULONG32 *  pBytesRead);  
```  
  
## <a name="parameters"></a><span data-ttu-id="d0802-105">參數</span><span class="sxs-lookup"><span data-stu-id="d0802-105">Parameters</span></span>  
 `address`  
 <span data-ttu-id="d0802-106">在要求之記憶體的起始位址。</span><span class="sxs-lookup"><span data-stu-id="d0802-106">[in] The start address of requested memory.</span></span>  
  
 `pbuffer`  
 <span data-ttu-id="d0802-107">脫銷將儲存記憶體的緩衝區。</span><span class="sxs-lookup"><span data-stu-id="d0802-107">[out] The buffer where the memory will be stored.</span></span>  
  
 `bytesRequested`  
 <span data-ttu-id="d0802-108">在要從目標位址取得的位元組數目。</span><span class="sxs-lookup"><span data-stu-id="d0802-108">[in] The number of bytes to get from the target address.</span></span>  
  
 `pBytesRead`  
 <span data-ttu-id="d0802-109">脫銷實際從目標位址讀取的位元組數目。</span><span class="sxs-lookup"><span data-stu-id="d0802-109">[out] The number of bytes actually read from the target address.</span></span> <span data-ttu-id="d0802-110">這可能少於`bytesRequested`。</span><span class="sxs-lookup"><span data-stu-id="d0802-110">This can be fewer than `bytesRequested`.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="d0802-111">備註</span><span class="sxs-lookup"><span data-stu-id="d0802-111">Remarks</span></span>  
 <span data-ttu-id="d0802-112">如果可以讀取第一個位元組（在指定的起始位址），則呼叫應該會傳回 success （以支援有效率地讀取具有自我描述長度的資料結構，例如以 null 終止的字串）。</span><span class="sxs-lookup"><span data-stu-id="d0802-112">If the first byte (at the specified start address) can be read, the call should return success (to support efficient reading of data structures with self-describing length, like null-terminated strings).</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="d0802-113">需求</span><span class="sxs-lookup"><span data-stu-id="d0802-113">Requirements</span></span>  
 <span data-ttu-id="d0802-114">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="d0802-114">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="d0802-115">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="d0802-115">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="d0802-116">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="d0802-116">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="d0802-117">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="d0802-117">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d0802-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d0802-118">See also</span></span>

- [<span data-ttu-id="d0802-119">ICorDebugDataTarget 介面</span><span class="sxs-lookup"><span data-stu-id="d0802-119">ICorDebugDataTarget Interface</span></span>](icordebugdatatarget-interface.md)
- [<span data-ttu-id="d0802-120">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="d0802-120">Debugging Interfaces</span></span>](debugging-interfaces.md)
- [<span data-ttu-id="d0802-121">偵錯</span><span class="sxs-lookup"><span data-stu-id="d0802-121">Debugging</span></span>](index.md)
