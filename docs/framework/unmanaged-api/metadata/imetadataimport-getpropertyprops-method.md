---
title: IMetaDataImport::GetPropertyProps 方法
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetPropertyProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetPropertyProps
helpviewer_keywords:
- GetPropertyProps method [.NET Framework metadata]
- IMetaDataImport::GetPropertyProps method [.NET Framework metadata]
ms.assetid: dc0ff3e6-7e7d-4f6c-948d-52b28f5cb78c
topic_type:
- apiref
ms.openlocfilehash: aded23e190de18d76bb2b9e2ffbae51cf2325419
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95729222"
---
# <a name="imetadataimportgetpropertyprops-method"></a><span data-ttu-id="07495-102">IMetaDataImport::GetPropertyProps 方法</span><span class="sxs-lookup"><span data-stu-id="07495-102">IMetaDataImport::GetPropertyProps Method</span></span>

<span data-ttu-id="07495-103">取得指定標記所表示之屬性的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="07495-103">Gets the metadata for the property represented by the specified token.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="07495-104">語法</span><span class="sxs-lookup"><span data-stu-id="07495-104">Syntax</span></span>  
  
```cpp  
HRESULT GetPropertyProps (  
   [in]  mdProperty        prop,  
   [out] mdTypeDef         *pClass,
   [out] LPCWSTR           szProperty,
   [in]  ULONG             cchProperty,
   [out] ULONG             *pchProperty,
   [out] DWORD             *pdwPropFlags,
   [out] PCCOR_SIGNATURE   *ppvSig,
   [out] ULONG             *pbSig,
   [out] DWORD             *pdwCPlusTypeFlag,
   [out] UVCP_CONSTANT     *ppDefaultValue,  
   [out] ULONG             *pcchDefaultValue,  
   [out] mdMethodDef       *pmdSetter,
   [out] mdMethodDef       *pmdGetter,
   [out] mdMethodDef       rmdOtherMethod[],  
   [in]  ULONG             cMax,
   [out] ULONG             *pcOtherMethod
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="07495-105">參數</span><span class="sxs-lookup"><span data-stu-id="07495-105">Parameters</span></span>  

 `prop`  
 <span data-ttu-id="07495-106">在表示傳回中繼資料之屬性的 token。</span><span class="sxs-lookup"><span data-stu-id="07495-106">[in] A token that represents the property to return metadata for.</span></span>  
  
 `pClass`  
 <span data-ttu-id="07495-107">擴展TypeDef token 的指標，代表實作為屬性的型別。</span><span class="sxs-lookup"><span data-stu-id="07495-107">[out] A pointer to the TypeDef token that represents the type that implements the property.</span></span>  
  
 `szProperty`  
 <span data-ttu-id="07495-108">擴展保存屬性名稱的緩衝區。</span><span class="sxs-lookup"><span data-stu-id="07495-108">[out] A buffer to hold the property name.</span></span>  
  
 `cchProperty`  
 <span data-ttu-id="07495-109">在的大小（以寬字元為單位） `szProperty` 。</span><span class="sxs-lookup"><span data-stu-id="07495-109">[in] The size in wide characters of `szProperty`.</span></span>  
  
 `pchProperty`  
 <span data-ttu-id="07495-110">擴展傳回的寬字元數 `szProperty` 。</span><span class="sxs-lookup"><span data-stu-id="07495-110">[out] The number of wide characters returned in `szProperty`.</span></span>  
  
 `pdwPropFlags`  
 <span data-ttu-id="07495-111">擴展套用至屬性之任何屬性旗標的指標。</span><span class="sxs-lookup"><span data-stu-id="07495-111">[out] A pointer to any attribute flags applied to the property.</span></span> <span data-ttu-id="07495-112">這個值是 [CorPropertyAttr](corpropertyattr-enumeration.md) 列舉的位元遮罩。</span><span class="sxs-lookup"><span data-stu-id="07495-112">This value is a bitmask from the [CorPropertyAttr](corpropertyattr-enumeration.md) enumeration.</span></span>  
  
 `ppvSig`  
 <span data-ttu-id="07495-113">擴展屬性之中繼資料簽章的指標。</span><span class="sxs-lookup"><span data-stu-id="07495-113">[out] A pointer to the metadata signature of the property.</span></span>  
  
 `pbSig`  
 <span data-ttu-id="07495-114">擴展傳回的位元組數目 `ppvSig` 。</span><span class="sxs-lookup"><span data-stu-id="07495-114">[out] The number of bytes returned in `ppvSig`.</span></span>  
  
 `pdwCPlusTypeFlag`  
 <span data-ttu-id="07495-115">擴展旗標，指定屬於屬性預設值的常數型別。</span><span class="sxs-lookup"><span data-stu-id="07495-115">[out] A flag specifying the type of the constant that is the default value of the property.</span></span> <span data-ttu-id="07495-116">此值來自 CorElementType 列舉。</span><span class="sxs-lookup"><span data-stu-id="07495-116">This value is from the CorElementType enumeration.</span></span>  
  
 `ppDefaultValue`  
 <span data-ttu-id="07495-117">擴展儲存這個屬性之預設值的位元組指標。</span><span class="sxs-lookup"><span data-stu-id="07495-117">[out] A pointer to the bytes that store the default value for this property.</span></span>  
  
 `pcchDefaultValue`  
 <span data-ttu-id="07495-118">擴展如果 ELEMENT_TYPE_STRING，則為寬字元的大小 `ppDefaultValue` `pdwCPlusTypeFlag` ; 否則，此值不相關。</span><span class="sxs-lookup"><span data-stu-id="07495-118">[out] The size in wide characters of `ppDefaultValue`, if `pdwCPlusTypeFlag` is ELEMENT_TYPE_STRING; otherwise, this value is not relevant.</span></span> <span data-ttu-id="07495-119">在此情況下，的長度 `ppDefaultValue` 是從所指定的型別推斷而來 `pdwCPlusTypeFlag` 。</span><span class="sxs-lookup"><span data-stu-id="07495-119">In that case, the length of `ppDefaultValue` is inferred from the type that is specified by `pdwCPlusTypeFlag`.</span></span>  
  
 `pmdSetter`  
 <span data-ttu-id="07495-120">擴展MethodDef token 的指標，代表屬性的 set 存取子方法。</span><span class="sxs-lookup"><span data-stu-id="07495-120">[out] A pointer to the MethodDef token that represents the set accessor method for the property.</span></span>  
  
 `pmdGetter`  
 <span data-ttu-id="07495-121">擴展MethodDef token 的指標，代表屬性的 get 存取子方法。</span><span class="sxs-lookup"><span data-stu-id="07495-121">[out] A pointer to the MethodDef token that represents the get accessor method for the property.</span></span>  
  
 `rmdOtherMethod`  
 <span data-ttu-id="07495-122">擴展MethodDef token 的陣列，表示與屬性相關聯的其他方法。</span><span class="sxs-lookup"><span data-stu-id="07495-122">[out] An array of MethodDef tokens that represent other methods associated with the property.</span></span>  
  
 `cMax`  
 <span data-ttu-id="07495-123">[in] `rmdOtherMethod` 陣列的大小上限。</span><span class="sxs-lookup"><span data-stu-id="07495-123">[in] The maximum size of the `rmdOtherMethod` array.</span></span> <span data-ttu-id="07495-124">如果您未提供夠大的陣列來容納所有方法，則會略過，而不發出警告。</span><span class="sxs-lookup"><span data-stu-id="07495-124">If you do not provide an array large enough to hold all the methods, they are skipped without warning.</span></span>  
  
 `pcOtherMethod`  
 <span data-ttu-id="07495-125">擴展中傳回的 MethodDef 權杖數目 `rmdOtherMethod` 。</span><span class="sxs-lookup"><span data-stu-id="07495-125">[out] The number of MethodDef tokens returned in `rmdOtherMethod`.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="07495-126">需求</span><span class="sxs-lookup"><span data-stu-id="07495-126">Requirements</span></span>  

 <span data-ttu-id="07495-127">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="07495-127">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="07495-128">**標頭：** Cor。h</span><span class="sxs-lookup"><span data-stu-id="07495-128">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="07495-129">連結 **庫：** 以資源的形式包含在 MsCorEE.dll 中</span><span class="sxs-lookup"><span data-stu-id="07495-129">**Library:** Included as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="07495-130">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="07495-130">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="07495-131">另請參閱</span><span class="sxs-lookup"><span data-stu-id="07495-131">See also</span></span>

- [<span data-ttu-id="07495-132">IMetaDataImport 介面</span><span class="sxs-lookup"><span data-stu-id="07495-132">IMetaDataImport Interface</span></span>](imetadataimport-interface.md)
- [<span data-ttu-id="07495-133">IMetaDataImport2 介面</span><span class="sxs-lookup"><span data-stu-id="07495-133">IMetaDataImport2 Interface</span></span>](imetadataimport2-interface.md)
