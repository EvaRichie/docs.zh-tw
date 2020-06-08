---
title: IMetaDataImport::GetFieldProps 方法
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetFieldProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetFieldProps
helpviewer_keywords:
- IMetaDataImport::GetFieldProps method [.NET Framework metadata]
- GetFieldProps method [.NET Framework metadata]
ms.assetid: 7b0e9b10-8cef-4ba6-8432-40bf63e65ab1
topic_type:
- apiref
ms.openlocfilehash: 2bd05b49c3d51ac13865997910c99cc0cd5ca2d9
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84491239"
---
# <a name="imetadataimportgetfieldprops-method"></a><span data-ttu-id="c9ee7-102">IMetaDataImport::GetFieldProps 方法</span><span class="sxs-lookup"><span data-stu-id="c9ee7-102">IMetaDataImport::GetFieldProps Method</span></span>
<span data-ttu-id="c9ee7-103">取得與指定 FieldDef 語彙基元所參考欄位相關聯的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="c9ee7-103">Gets metadata associated with the field referenced by the specified FieldDef token.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="c9ee7-104">語法</span><span class="sxs-lookup"><span data-stu-id="c9ee7-104">Syntax</span></span>  
  
```cpp  
HRESULT GetFieldProps (  
   [in]  mdFieldDef        mb,
   [out] mdTypeDef         *pClass,  
   [out] LPWSTR            szField,  
   [in]  ULONG             cchField,
   [out] ULONG             *pchField,  
   [out] DWORD             *pdwAttr,  
   [in]  PCCOR_SIGNATURE   *ppvSigBlob,
   [out] ULONG             *pcbSigBlob,
   [out] DWORD             *pdwCPlusTypeFlag,
   [out] UVCP_CONSTANT     *ppValue,  
   [out] ULONG             *pcchValue  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="c9ee7-105">參數</span><span class="sxs-lookup"><span data-stu-id="c9ee7-105">Parameters</span></span>  
 `mb`  
 <span data-ttu-id="c9ee7-106">在FieldDef token，表示要取得相關聯中繼資料的欄位。</span><span class="sxs-lookup"><span data-stu-id="c9ee7-106">[in] A FieldDef token that represents the field to get associated metadata for.</span></span>  
  
 `pClass`  
 <span data-ttu-id="c9ee7-107">脫銷TypeDef token 的指標，代表欄位所屬類別的型別。</span><span class="sxs-lookup"><span data-stu-id="c9ee7-107">[out] A pointer to a TypeDef token that represents the type of the class that the field belongs to.</span></span>  
  
 `szField`  
 <span data-ttu-id="c9ee7-108">脫銷欄位的名稱。</span><span class="sxs-lookup"><span data-stu-id="c9ee7-108">[out] The name of the field.</span></span>  
  
 `cchField`  
 <span data-ttu-id="c9ee7-109">在*SzField*緩衝區的大小（以寬字元為單位）。</span><span class="sxs-lookup"><span data-stu-id="c9ee7-109">[in] The size in wide characters of the buffer for *szField*.</span></span>  
  
 `pchField`  
 <span data-ttu-id="c9ee7-110">脫銷所傳回緩衝區的實際大小。</span><span class="sxs-lookup"><span data-stu-id="c9ee7-110">[out] The actual size of the returned buffer.</span></span>  
  
 `pdwAttr`  
 <span data-ttu-id="c9ee7-111">脫銷與欄位的中繼資料相關聯的旗標。</span><span class="sxs-lookup"><span data-stu-id="c9ee7-111">[out] Flags associated with the field's metadata.</span></span>  
  
 `ppvSigBlob`  
 <span data-ttu-id="c9ee7-112">在描述欄位之二進位中繼資料值的指標。</span><span class="sxs-lookup"><span data-stu-id="c9ee7-112">[in] A pointer to the binary metadata value that describes the field.</span></span>  
  
 `pcbSigBlob`  
 <span data-ttu-id="c9ee7-113">脫銷的大小（以位元組為單位） `ppvSigBlob` 。</span><span class="sxs-lookup"><span data-stu-id="c9ee7-113">[out] The size in bytes of `ppvSigBlob`.</span></span>  
  
 `pdwCPlusTypeFlag`  
 <span data-ttu-id="c9ee7-114">脫銷指定欄位之數值型別的旗標。</span><span class="sxs-lookup"><span data-stu-id="c9ee7-114">[out] A flag that specifies the value type of the field.</span></span>  
  
 `ppValue`  
 <span data-ttu-id="c9ee7-115">脫銷欄位的常數值。</span><span class="sxs-lookup"><span data-stu-id="c9ee7-115">[out] A constant value for the field.</span></span>  
  
 `pcchValue`  
 <span data-ttu-id="c9ee7-116">脫銷的大小（以字元為單位 `ppValue` ），如果不存在任何字串，則為零。</span><span class="sxs-lookup"><span data-stu-id="c9ee7-116">[out] The size in chars of `ppValue`, or zero if no string exists.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="c9ee7-117">規格需求</span><span class="sxs-lookup"><span data-stu-id="c9ee7-117">Requirements</span></span>  
 <span data-ttu-id="c9ee7-118">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="c9ee7-118">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="c9ee7-119">**標頭：** Cor。h</span><span class="sxs-lookup"><span data-stu-id="c9ee7-119">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="c9ee7-120">連結**庫：** 包含為 Mscoree.dll 中的資源</span><span class="sxs-lookup"><span data-stu-id="c9ee7-120">**Library:** Included as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="c9ee7-121">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="c9ee7-121">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c9ee7-122">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c9ee7-122">See also</span></span>

- [<span data-ttu-id="c9ee7-123">IMetaDataImport 介面</span><span class="sxs-lookup"><span data-stu-id="c9ee7-123">IMetaDataImport Interface</span></span>](imetadataimport-interface.md)
- [<span data-ttu-id="c9ee7-124">IMetaDataImport2 介面</span><span class="sxs-lookup"><span data-stu-id="c9ee7-124">IMetaDataImport2 Interface</span></span>](imetadataimport2-interface.md)
