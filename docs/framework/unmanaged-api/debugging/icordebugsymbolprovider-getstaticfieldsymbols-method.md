---
title: ICorDebugSymbolProvider::GetStaticFieldSymbols 方法
ms.date: 03/30/2017
ms.assetid: b178367f-a6e4-413c-b06f-daf3804b456b
ms.openlocfilehash: 09e68c751da6500c5580f4945e8dd1c486a09217
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95698659"
---
# <a name="icordebugsymbolprovidergetstaticfieldsymbols-method"></a><span data-ttu-id="30120-102">ICorDebugSymbolProvider::GetStaticFieldSymbols 方法</span><span class="sxs-lookup"><span data-stu-id="30120-102">ICorDebugSymbolProvider::GetStaticFieldSymbols Method</span></span>

<span data-ttu-id="30120-103">取得對應至 TypeSpec 簽章的靜態欄位符號。</span><span class="sxs-lookup"><span data-stu-id="30120-103">Gets the static field symbols that correspond to a typespec signature.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="30120-104">語法</span><span class="sxs-lookup"><span data-stu-id="30120-104">Syntax</span></span>  
  
```cpp  
HRESULT GetStaticFieldSymbols(  
   [in] ULONG32 cbSignature,  
   [in, size_is(cbSignature)]  BYTE typeSig[],  
   [in] ULONG32 cRequestedSymbols,  
   [out] ULONG32 *pcFetchedSymbols,  
   [out, size_is(cRequestedSymbols), length_is(*pcFetchedSymbols)] ICorDebugStaticFieldSymbol *pSymbols[]  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="30120-105">參數</span><span class="sxs-lookup"><span data-stu-id="30120-105">Parameters</span></span>  

 `cbSignature`  
 <span data-ttu-id="30120-106">[in] `typeSig` 陣列中的位元組數。</span><span class="sxs-lookup"><span data-stu-id="30120-106">[in] The number of bytes in the `typeSig` array.</span></span>  
  
 `typeSig`  
 <span data-ttu-id="30120-107">[in] 包含 `typespec` 簽章的位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="30120-107">[in] A byte array that contains the `typespec` signature.</span></span>  
  
 `cRequestedSymbols`  
 <span data-ttu-id="30120-108">[in] 要求的符號數目。</span><span class="sxs-lookup"><span data-stu-id="30120-108">[in] The number of symbols requested.</span></span>  
  
 `pcFetchedSymbols`  
 <span data-ttu-id="30120-109">[out] 方法所擷取之符號數的指標。</span><span class="sxs-lookup"><span data-stu-id="30120-109">[out] A pointer to the number of symbols retrieved by the method.</span></span>  
  
 `pSymbols`  
 <span data-ttu-id="30120-110">擴展 [ICorDebugStaticFieldSymbol](icordebugstaticfieldsymbol-interface.md) 陣列的指標，其中包含所要求的靜態欄位符號。</span><span class="sxs-lookup"><span data-stu-id="30120-110">[out] A pointer to an [ICorDebugStaticFieldSymbol](icordebugstaticfieldsymbol-interface.md) array that contains the requested static field symbols.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="30120-111">備註</span><span class="sxs-lookup"><span data-stu-id="30120-111">Remarks</span></span>  
  
> [!NOTE]
> <span data-ttu-id="30120-112">這個方法僅適用於 .NET Native。</span><span class="sxs-lookup"><span data-stu-id="30120-112">This method is available with .NET Native only.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="30120-113">需求</span><span class="sxs-lookup"><span data-stu-id="30120-113">Requirements</span></span>  

 <span data-ttu-id="30120-114">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="30120-114">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="30120-115">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="30120-115">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="30120-116">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="30120-116">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="30120-117">**.NET Framework 版本：**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span><span class="sxs-lookup"><span data-stu-id="30120-117">**.NET Framework Versions:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="30120-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="30120-118">See also</span></span>

- [<span data-ttu-id="30120-119">GetInstanceFieldSymbols 方法</span><span class="sxs-lookup"><span data-stu-id="30120-119">GetInstanceFieldSymbols Method</span></span>](icordebugsymbolprovider-getinstancefieldsymbols-method.md)
- [<span data-ttu-id="30120-120">ICorDebugSymbolProvider 介面</span><span class="sxs-lookup"><span data-stu-id="30120-120">ICorDebugSymbolProvider Interface</span></span>](icordebugsymbolprovider-interface.md)
- [<span data-ttu-id="30120-121">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="30120-121">Debugging Interfaces</span></span>](debugging-interfaces.md)
