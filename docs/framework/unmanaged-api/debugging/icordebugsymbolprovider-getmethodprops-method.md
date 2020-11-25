---
title: ICorDebugSymbolProvider::GetMethodProps 方法
ms.date: 03/30/2017
ms.assetid: 8f836b80-b7a5-460b-bf76-5f0e45652aea
ms.openlocfilehash: 5412b2f06445627c1240d6c8f4efb3ce6bbbec54
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95730821"
---
# <a name="icordebugsymbolprovidergetmethodprops-method"></a><span data-ttu-id="3ff3a-102">ICorDebugSymbolProvider::GetMethodProps 方法</span><span class="sxs-lookup"><span data-stu-id="3ff3a-102">ICorDebugSymbolProvider::GetMethodProps Method</span></span>

<span data-ttu-id="3ff3a-103">傳回方法屬性的相關資訊，例如方法的中繼資料語彙基元，以及其泛型參數的相關資訊 (假設該方法中有相對虛擬位址 (RVA))。</span><span class="sxs-lookup"><span data-stu-id="3ff3a-103">Returns information about method properties, such as the method's metadata token and information about its generic parameters, given a relative virtual address (RVA) in that method.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="3ff3a-104">語法</span><span class="sxs-lookup"><span data-stu-id="3ff3a-104">Syntax</span></span>  
  
```cpp  
HRESULT GetMethodProps(  
   [in]  ULONG32 codeRva,  
   [out] mdToken *pMethodToken,  
   [out] ULONG32 *pcGenericParams,  
   [in]  ULONG32 cbSignature,  
   [out] ULONG32 *pcbSignature,  
   [out, size_is(cbSignature), length_is(*pcbSignature)] BYTE signature[]  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="3ff3a-105">參數</span><span class="sxs-lookup"><span data-stu-id="3ff3a-105">Parameters</span></span>  

 `codeRVA`  
 <span data-ttu-id="3ff3a-106">[in] 方法中的相對虛擬位址，將會擷取其相關資訊。</span><span class="sxs-lookup"><span data-stu-id="3ff3a-106">[in] A relative virtual address in the method about which information is to be retrieved.</span></span>  
  
 `pMethodToken`  
 <span data-ttu-id="3ff3a-107">[out] 方法的中繼資料語彙基元指標。</span><span class="sxs-lookup"><span data-stu-id="3ff3a-107">[out] A pointer to the method's metadata token.</span></span>  
  
 `pcGenericParams`  
 <span data-ttu-id="3ff3a-108">[out] 與這個方法相關聯之泛型參數的數目指標。</span><span class="sxs-lookup"><span data-stu-id="3ff3a-108">[out] A pointer to the number of generic parameters associated with this method.</span></span>  
  
 `cbSignature`  
 <span data-ttu-id="3ff3a-109">[in] `signature` 陣列的大小。</span><span class="sxs-lookup"><span data-stu-id="3ff3a-109">[in] The size of the `signature` array.</span></span> <span data-ttu-id="3ff3a-110">請參閱＜備註＞一節。</span><span class="sxs-lookup"><span data-stu-id="3ff3a-110">See the Remarks section.</span></span>  
  
 `pcbSignature`  
 <span data-ttu-id="3ff3a-111">[out] 所傳回之 `signature` 陣列的大小指標。</span><span class="sxs-lookup"><span data-stu-id="3ff3a-111">[out] A pointer to the size of the returned `signature` array.</span></span>  
  
 `signature`  
 <span data-ttu-id="3ff3a-112">[out] 保留所有泛型參數之 TypeSpec 簽章的緩衝區。</span><span class="sxs-lookup"><span data-stu-id="3ff3a-112">[out] A buffer that holds the typespec signatures of all generic parameters.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="3ff3a-113">備註</span><span class="sxs-lookup"><span data-stu-id="3ff3a-113">Remarks</span></span>  

 <span data-ttu-id="3ff3a-114">若要取得方法陣列的所需大小 `signature` ，請將 `cbSignature` 引數設定為0，並將設定 `signature` 為 **null**。</span><span class="sxs-lookup"><span data-stu-id="3ff3a-114">To get the required size of the method's `signature` array, set the `cbSignature` argument to 0 and `signature` to **null**.</span></span> <span data-ttu-id="3ff3a-115">當這個方法傳回時，`pcbSignature` 會包含 `signature` 陣列所需的位元組數目。</span><span class="sxs-lookup"><span data-stu-id="3ff3a-115">When the method returns, `pcbSignature` will contain the number of bytes required for the `signature` array.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="3ff3a-116">這個方法僅適用於 .NET Native。</span><span class="sxs-lookup"><span data-stu-id="3ff3a-116">This method is available with .NET Native only.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="3ff3a-117">需求</span><span class="sxs-lookup"><span data-stu-id="3ff3a-117">Requirements</span></span>  

 <span data-ttu-id="3ff3a-118">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="3ff3a-118">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="3ff3a-119">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="3ff3a-119">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="3ff3a-120">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="3ff3a-120">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="3ff3a-121">**.NET Framework 版本：**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span><span class="sxs-lookup"><span data-stu-id="3ff3a-121">**.NET Framework Versions:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3ff3a-122">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3ff3a-122">See also</span></span>

- [<span data-ttu-id="3ff3a-123">GetTypeProps 方法</span><span class="sxs-lookup"><span data-stu-id="3ff3a-123">GetTypeProps Method</span></span>](icordebugsymbolprovider-gettypeprops-method.md)
- [<span data-ttu-id="3ff3a-124">ICorDebugSymbolProvider 介面</span><span class="sxs-lookup"><span data-stu-id="3ff3a-124">ICorDebugSymbolProvider Interface</span></span>](icordebugsymbolprovider-interface.md)
- [<span data-ttu-id="3ff3a-125">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="3ff3a-125">Debugging Interfaces</span></span>](debugging-interfaces.md)
