---
title: ICorDebugSymbolProvider::GetInstanceFieldSymbols 方法
ms.date: 03/30/2017
ms.assetid: a29b9233-ee67-4b53-b8bc-c00b281e7edb
ms.openlocfilehash: 1a74b355b695f65166d0fe63bbdd41d789db5cfe
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95730860"
---
# <a name="icordebugsymbolprovidergetinstancefieldsymbols-method"></a><span data-ttu-id="5c894-102">ICorDebugSymbolProvider::GetInstanceFieldSymbols 方法</span><span class="sxs-lookup"><span data-stu-id="5c894-102">ICorDebugSymbolProvider::GetInstanceFieldSymbols Method</span></span>

<span data-ttu-id="5c894-103">取得對應 TypeSpec 簽章的執行個體欄位符號。</span><span class="sxs-lookup"><span data-stu-id="5c894-103">Gets the instance field symbols that correspond to a typespec signature.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="5c894-104">語法</span><span class="sxs-lookup"><span data-stu-id="5c894-104">Syntax</span></span>  
  
```cpp  
HRESULT GetInstanceFieldSymbols(  
   [in] ULONG32 cbSignature,  
   [in, size_is(cbSignature)]  BYTE typeSig[],  
   [in] ULONG32 cRequestedSymbols,  
   [out] ULONG32 *pcFetchedSymbols,  
   [out, size_is(cRequestedSymbols), length_is(*pcFetchedSymbols)] ICorDebugInstanceFieldSymbol *pSymbols[]  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="5c894-105">參數</span><span class="sxs-lookup"><span data-stu-id="5c894-105">Parameters</span></span>  

 `cbSignature`  
 <span data-ttu-id="5c894-106">[in] `typeSig` 陣列中的位元組數。</span><span class="sxs-lookup"><span data-stu-id="5c894-106">[in] The number of bytes in the `typeSig` array.</span></span>  
  
 `typeSig`  
 <span data-ttu-id="5c894-107">[in] 包含 `typespec` 簽章的位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="5c894-107">[in] A byte array that contains the `typespec` signature.</span></span>  
  
 `cRequestedSymbols`  
 <span data-ttu-id="5c894-108">[in] 要求的符號數目。</span><span class="sxs-lookup"><span data-stu-id="5c894-108">[in] The number of symbols requested.</span></span>  
  
 `pcFetchedSymbols`  
 <span data-ttu-id="5c894-109">[out] 方法所擷取之符號數的指標。</span><span class="sxs-lookup"><span data-stu-id="5c894-109">[out] A pointer to the number of symbols retrieved by the method.</span></span>  
  
 `pSymbols`  
 <span data-ttu-id="5c894-110">擴展 [ICorDebugStaticFieldSymbol](icordebugstaticfieldsymbol-interface.md) 陣列的指標，其中包含所要求的實例欄位符號。</span><span class="sxs-lookup"><span data-stu-id="5c894-110">[out] A pointer to an [ICorDebugStaticFieldSymbol](icordebugstaticfieldsymbol-interface.md) array that contains the requested instance field symbols.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="5c894-111">備註</span><span class="sxs-lookup"><span data-stu-id="5c894-111">Remarks</span></span>  
  
> [!NOTE]
> <span data-ttu-id="5c894-112">這個方法僅適用於 .NET Native。</span><span class="sxs-lookup"><span data-stu-id="5c894-112">This method is available with .NET Native only.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="5c894-113">需求</span><span class="sxs-lookup"><span data-stu-id="5c894-113">Requirements</span></span>  

 <span data-ttu-id="5c894-114">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="5c894-114">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="5c894-115">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="5c894-115">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="5c894-116">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="5c894-116">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="5c894-117">**.NET Framework 版本：**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span><span class="sxs-lookup"><span data-stu-id="5c894-117">**.NET Framework Versions:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="5c894-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5c894-118">See also</span></span>

- [<span data-ttu-id="5c894-119">GetStaticFieldSymbols 方法</span><span class="sxs-lookup"><span data-stu-id="5c894-119">GetStaticFieldSymbols Method</span></span>](icordebugsymbolprovider-getstaticfieldsymbols-method.md)
- [<span data-ttu-id="5c894-120">ICorDebugSymbolProvider 介面</span><span class="sxs-lookup"><span data-stu-id="5c894-120">ICorDebugSymbolProvider Interface</span></span>](icordebugsymbolprovider-interface.md)
- [<span data-ttu-id="5c894-121">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="5c894-121">Debugging Interfaces</span></span>](debugging-interfaces.md)
