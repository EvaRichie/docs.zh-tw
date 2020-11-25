---
title: IMetaDataImport::EnumProperties 方法
ms.date: 03/30/2017
api_name:
- IMetaDataImport.EnumProperties
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::EnumProperties
helpviewer_keywords:
- IMetaDataImport::EnumProperties method [.NET Framework metadata]
- EnumProperties method [.NET Framework metadata]
ms.assetid: 60573ad7-8821-4721-a068-3f7a6d25926a
topic_type:
- apiref
ms.openlocfilehash: 24ee37a36e34c74258e1c750ba424640c0496f0a
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95728247"
---
# <a name="imetadataimportenumproperties-method"></a><span data-ttu-id="1f72a-102">IMetaDataImport::EnumProperties 方法</span><span class="sxs-lookup"><span data-stu-id="1f72a-102">IMetaDataImport::EnumProperties Method</span></span>

<span data-ttu-id="1f72a-103">列舉 PropertyDef 語彙基元，其代表指定的 TypeDef 語彙基元所參考的類型屬性。</span><span class="sxs-lookup"><span data-stu-id="1f72a-103">Enumerates PropertyDef tokens representing the properties of the type referenced by the specified TypeDef token.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="1f72a-104">語法</span><span class="sxs-lookup"><span data-stu-id="1f72a-104">Syntax</span></span>  
  
```cpp  
HRESULT EnumProperties (  
   [in, out] HCORENUM    *phEnum,  
   [in]      mdTypeDef   td,  
   [out]     mdProperty  rProperties[],  
   [in]      ULONG       cMax,  
   [out]     ULONG       *pcProperties  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="1f72a-105">參數</span><span class="sxs-lookup"><span data-stu-id="1f72a-105">Parameters</span></span>  

 `phEnum`  
 <span data-ttu-id="1f72a-106">[in，out]列舉值的指標。</span><span class="sxs-lookup"><span data-stu-id="1f72a-106">[in, out] A pointer to the enumerator.</span></span> <span data-ttu-id="1f72a-107">此方法的第一個呼叫必須是 Null。</span><span class="sxs-lookup"><span data-stu-id="1f72a-107">This must be NULL for the first call of this method.</span></span>  
  
 `td`  
 <span data-ttu-id="1f72a-108">在表示具有要列舉屬性之類型的 TypeDef 標記。</span><span class="sxs-lookup"><span data-stu-id="1f72a-108">[in] A TypeDef token representing the type with properties to enumerate.</span></span>  
  
 `rProperties`  
 <span data-ttu-id="1f72a-109">擴展用來儲存 PropertyDef 標記的陣列。</span><span class="sxs-lookup"><span data-stu-id="1f72a-109">[out] The array used to store the PropertyDef tokens.</span></span>  
  
 `cMax`  
 <span data-ttu-id="1f72a-110">[in] `rProperties` 陣列的大小上限。</span><span class="sxs-lookup"><span data-stu-id="1f72a-110">[in] The maximum size of the `rProperties` array.</span></span>  
  
 `pcProperties`  
 <span data-ttu-id="1f72a-111">擴展傳回的 PropertyDef 權杖數目 `rProperties` 。</span><span class="sxs-lookup"><span data-stu-id="1f72a-111">[out] The number of PropertyDef tokens returned in `rProperties`.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="1f72a-112">傳回值</span><span class="sxs-lookup"><span data-stu-id="1f72a-112">Return Value</span></span>  
  
|<span data-ttu-id="1f72a-113">HRESULT</span><span class="sxs-lookup"><span data-stu-id="1f72a-113">HRESULT</span></span>|<span data-ttu-id="1f72a-114">描述</span><span class="sxs-lookup"><span data-stu-id="1f72a-114">Description</span></span>|  
|-------------|-----------------|  
|`S_OK`|<span data-ttu-id="1f72a-115">`EnumProperties` 傳回成功。</span><span class="sxs-lookup"><span data-stu-id="1f72a-115">`EnumProperties` returned successfully.</span></span>|  
|`S_FALSE`|<span data-ttu-id="1f72a-116">沒有要列舉的權杖。</span><span class="sxs-lookup"><span data-stu-id="1f72a-116">There are no tokens to enumerate.</span></span> <span data-ttu-id="1f72a-117">在此情況下， `pcProperties` 是零。</span><span class="sxs-lookup"><span data-stu-id="1f72a-117">In that case, `pcProperties` is zero.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="1f72a-118">需求</span><span class="sxs-lookup"><span data-stu-id="1f72a-118">Requirements</span></span>  

 <span data-ttu-id="1f72a-119">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="1f72a-119">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="1f72a-120">**標頭：** Cor。h</span><span class="sxs-lookup"><span data-stu-id="1f72a-120">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="1f72a-121">連結 **庫：** 以資源的形式包含在 MsCorEE.dll 中</span><span class="sxs-lookup"><span data-stu-id="1f72a-121">**Library:** Included as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="1f72a-122">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="1f72a-122">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="1f72a-123">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1f72a-123">See also</span></span>

- [<span data-ttu-id="1f72a-124">IMetaDataImport 介面</span><span class="sxs-lookup"><span data-stu-id="1f72a-124">IMetaDataImport Interface</span></span>](imetadataimport-interface.md)
- [<span data-ttu-id="1f72a-125">IMetaDataImport2 介面</span><span class="sxs-lookup"><span data-stu-id="1f72a-125">IMetaDataImport2 Interface</span></span>](imetadataimport2-interface.md)
