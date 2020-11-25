---
title: ICorDebugInstanceFieldSymbol::GetSize 方法
ms.date: 03/30/2017
ms.assetid: a4af1e3b-6a9f-4855-95ba-5317565c8e2b
ms.openlocfilehash: c4b193b45e30b0eba3367f18cb1e4c2b4e108fa8
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95724906"
---
# <a name="icordebuginstancefieldsymbolgetsize-method"></a><span data-ttu-id="40c23-102">ICorDebugInstanceFieldSymbol::GetSize 方法</span><span class="sxs-lookup"><span data-stu-id="40c23-102">ICorDebugInstanceFieldSymbol::GetSize Method</span></span>

<span data-ttu-id="40c23-103">取得執行個體欄位的大小 (以位元組為單位)。</span><span class="sxs-lookup"><span data-stu-id="40c23-103">Gets the size in bytes of the instance field.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="40c23-104">語法</span><span class="sxs-lookup"><span data-stu-id="40c23-104">Syntax</span></span>  
  
```cpp  
HRESULT GetSize(  
   [out] ULONG32 *pcbSize  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="40c23-105">參數</span><span class="sxs-lookup"><span data-stu-id="40c23-105">Parameters</span></span>  

 `pcbSize`  
 <span data-ttu-id="40c23-106">[out] 欄位長度的指標。</span><span class="sxs-lookup"><span data-stu-id="40c23-106">[out] A pointer to length of the field.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="40c23-107">備註</span><span class="sxs-lookup"><span data-stu-id="40c23-107">Remarks</span></span>  
  
> [!NOTE]
> <span data-ttu-id="40c23-108">這個方法僅適用於 .NET Native。</span><span class="sxs-lookup"><span data-stu-id="40c23-108">This method is available with .NET Native only.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="40c23-109">需求</span><span class="sxs-lookup"><span data-stu-id="40c23-109">Requirements</span></span>  

 <span data-ttu-id="40c23-110">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="40c23-110">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="40c23-111">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="40c23-111">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="40c23-112">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="40c23-112">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="40c23-113">**.NET Framework 版本：**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span><span class="sxs-lookup"><span data-stu-id="40c23-113">**.NET Framework Versions:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="40c23-114">另請參閱</span><span class="sxs-lookup"><span data-stu-id="40c23-114">See also</span></span>

- [<span data-ttu-id="40c23-115">ICorDebugInstanceFieldSymbol 介面</span><span class="sxs-lookup"><span data-stu-id="40c23-115">ICorDebugInstanceFieldSymbol Interface</span></span>](icordebuginstancefieldsymbol-interface.md)
- [<span data-ttu-id="40c23-116">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="40c23-116">Debugging Interfaces</span></span>](debugging-interfaces.md)
