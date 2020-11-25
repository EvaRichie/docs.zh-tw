---
title: IMetaDataImport2::EnumGenericParams 方法
ms.date: 03/30/2017
api_name:
- IMetaDataImport2.EnumGenericParams
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport2::EnumGenericParams
helpviewer_keywords:
- EnumGenericParams method [.NET Framework metadata]
- IMetaDataImport2::EnumGenericParams method [.NET Framework metadata]
ms.assetid: b50488a5-3cf0-483c-82dc-2892a3ec61ac
topic_type:
- apiref
ms.openlocfilehash: 6b1a8e66eea6caec9dfc8d99e343c987cefa1b0c
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95702754"
---
# <a name="imetadataimport2enumgenericparams-method"></a><span data-ttu-id="e75d1-102">IMetaDataImport2::EnumGenericParams 方法</span><span class="sxs-lookup"><span data-stu-id="e75d1-102">IMetaDataImport2::EnumGenericParams Method</span></span>

<span data-ttu-id="e75d1-103">取得與指定的 TypeDef 或 MethodDef token 相關聯之泛型參數標記陣列的列舉值。</span><span class="sxs-lookup"><span data-stu-id="e75d1-103">Gets an enumerator for an array of generic parameter tokens associated with the specified TypeDef or MethodDef token.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="e75d1-104">語法</span><span class="sxs-lookup"><span data-stu-id="e75d1-104">Syntax</span></span>  
  
```cpp
HRESULT EnumGenericParams (  
   [in, out] HCORENUM     *phEnum,
   [in]  mdToken          tk,  
   [out] mdGenericParam   rGenericParams[],
   [in]  ULONG            cMax,
   [out] ULONG            *pcGenericParams  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="e75d1-105">參數</span><span class="sxs-lookup"><span data-stu-id="e75d1-105">Parameters</span></span>  

 `phEnum`  
 <span data-ttu-id="e75d1-106">[in，out]列舉值的指標。</span><span class="sxs-lookup"><span data-stu-id="e75d1-106">[in, out] A pointer to the enumerator.</span></span>  
  
 `tk`  
 <span data-ttu-id="e75d1-107">在要列舉其泛型參數的 TypeDef 或 MethodDef 標記。</span><span class="sxs-lookup"><span data-stu-id="e75d1-107">[in] The TypeDef or MethodDef token whose generic parameters are to be enumerated.</span></span>  
  
 `rGenericParams`  
 <span data-ttu-id="e75d1-108">擴展要列舉之泛型參數的陣列。</span><span class="sxs-lookup"><span data-stu-id="e75d1-108">[out] The array of generic parameters to enumerate.</span></span>  
  
 `cMax`  
 <span data-ttu-id="e75d1-109">在要求的最大權杖數目 `rGenericParams` 。</span><span class="sxs-lookup"><span data-stu-id="e75d1-109">[in] The requested maximum number of tokens to place in `rGenericParams`.</span></span>  
  
 `pcGenericParams`  
 <span data-ttu-id="e75d1-110">擴展所傳回的權杖數目 `rGenericParams` 。</span><span class="sxs-lookup"><span data-stu-id="e75d1-110">[out] The returned number of tokens placed in `rGenericParams`.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="e75d1-111">傳回值</span><span class="sxs-lookup"><span data-stu-id="e75d1-111">Return Value</span></span>  
  
|<span data-ttu-id="e75d1-112">HRESULT</span><span class="sxs-lookup"><span data-stu-id="e75d1-112">HRESULT</span></span>|<span data-ttu-id="e75d1-113">描述</span><span class="sxs-lookup"><span data-stu-id="e75d1-113">Description</span></span>|  
|-------------|-----------------|  
|`S_OK`|<span data-ttu-id="e75d1-114">`EnumGenericParams` 傳回成功。</span><span class="sxs-lookup"><span data-stu-id="e75d1-114">`EnumGenericParams` returned successfully.</span></span>|  
|`S_FALSE`|<span data-ttu-id="e75d1-115">`phEnum` 沒有成員元素。</span><span class="sxs-lookup"><span data-stu-id="e75d1-115">`phEnum` has no member elements.</span></span> <span data-ttu-id="e75d1-116">在此情況下， `pcGenericParams` 會設定為 0 (零) 。</span><span class="sxs-lookup"><span data-stu-id="e75d1-116">In this case, `pcGenericParams` is set to 0 (zero).</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="e75d1-117">需求</span><span class="sxs-lookup"><span data-stu-id="e75d1-117">Requirements</span></span>  

 <span data-ttu-id="e75d1-118">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="e75d1-118">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="e75d1-119">**標頭：** Cor。h</span><span class="sxs-lookup"><span data-stu-id="e75d1-119">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="e75d1-120">連結 **庫：** 當做 MsCorEE.dll 中的資源使用</span><span class="sxs-lookup"><span data-stu-id="e75d1-120">**Library:** Used as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="e75d1-121">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="e75d1-121">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e75d1-122">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e75d1-122">See also</span></span>

- [<span data-ttu-id="e75d1-123">IMetaDataImport2 介面</span><span class="sxs-lookup"><span data-stu-id="e75d1-123">IMetaDataImport2 Interface</span></span>](imetadataimport2-interface.md)
- [<span data-ttu-id="e75d1-124">IMetaDataImport 介面</span><span class="sxs-lookup"><span data-stu-id="e75d1-124">IMetaDataImport Interface</span></span>](imetadataimport-interface.md)
