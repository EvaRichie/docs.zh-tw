---
title: IMetaDataEmit::DefineParam 方法
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.DefineParam
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::DefineParam
helpviewer_keywords:
- IMetaDataEmit::DefineParam method [.NET Framework metadata]
- DefineParam method [.NET Framework metadata]
ms.assetid: d86a3d14-4796-4909-9591-dfafe3de5ce4
topic_type:
- apiref
ms.openlocfilehash: a58e03875ec021b41479085fa9e27a4321ae965e
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "84004344"
---
# <a name="imetadataemitdefineparam-method"></a><span data-ttu-id="f6fe0-102">IMetaDataEmit::DefineParam 方法</span><span class="sxs-lookup"><span data-stu-id="f6fe0-102">IMetaDataEmit::DefineParam Method</span></span>
<span data-ttu-id="f6fe0-103">針對指定之標記所參考的方法，使用指定的簽章建立參數定義，並取得該參數定義的 token。</span><span class="sxs-lookup"><span data-stu-id="f6fe0-103">Creates a parameter definition with the specified signature for the method referenced by the specified token, and gets a token for that parameter definition.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="f6fe0-104">語法</span><span class="sxs-lookup"><span data-stu-id="f6fe0-104">Syntax</span></span>  
  
```cpp  
HRESULT DefineParam (  
    [in]  mdMethodDef md,
    [in]  ULONG       ulParamSeq,
    [in]  LPCWSTR     szName,
    [in]  DWORD       dwParamFlags,
    [in]  DWORD       dwCPlusTypeFlag,
    [in]  void const  *pValue,  
    [in]  ULONG       cchValue,
    [out] mdParamDef  *ppd
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="f6fe0-105">參數</span><span class="sxs-lookup"><span data-stu-id="f6fe0-105">Parameters</span></span>  
 `md`  
 <span data-ttu-id="f6fe0-106">在要定義其參數之方法的 token。</span><span class="sxs-lookup"><span data-stu-id="f6fe0-106">[in] The token for the method whose parameter is being defined.</span></span>  
  
 `ulParamSeq`  
 <span data-ttu-id="f6fe0-107">在參數序號。</span><span class="sxs-lookup"><span data-stu-id="f6fe0-107">[in] The parameter sequence number.</span></span>  
  
 `szName`  
 <span data-ttu-id="f6fe0-108">在Unicode 中的參數名稱。</span><span class="sxs-lookup"><span data-stu-id="f6fe0-108">[in] The name of the parameter in Unicode.</span></span>  
  
 `dwParamFlags`  
 <span data-ttu-id="f6fe0-109">在參數的旗標。</span><span class="sxs-lookup"><span data-stu-id="f6fe0-109">[in] Flags for the parameter.</span></span> <span data-ttu-id="f6fe0-110">這是值的位元遮罩 `CorParamAttr` 。</span><span class="sxs-lookup"><span data-stu-id="f6fe0-110">This is a bitmask of `CorParamAttr` values.</span></span>  
  
 `dwCPlusTypeFlag`  
 <span data-ttu-id="f6fe0-111">[in] `ELEMENT_TYPE_` *\** 作為常數值。</span><span class="sxs-lookup"><span data-stu-id="f6fe0-111">[in] `ELEMENT_TYPE_`*\** for the constant value.</span></span>  
  
 `pValue`  
 <span data-ttu-id="f6fe0-112">在參數的常數值。</span><span class="sxs-lookup"><span data-stu-id="f6fe0-112">[in] The constant value for the parameter.</span></span>  
  
 `cchValue`  
 <span data-ttu-id="f6fe0-113">在的大小，以 Unicode 字元為單位 `pValue` 。</span><span class="sxs-lookup"><span data-stu-id="f6fe0-113">[in] The size, in Unicode characters, of `pValue`.</span></span>  
  
 `ppd`  
 <span data-ttu-id="f6fe0-114">脫銷`mdParamDef`指派的 token。</span><span class="sxs-lookup"><span data-stu-id="f6fe0-114">[out] The `mdParamDef` token assigned.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="f6fe0-115">備註</span><span class="sxs-lookup"><span data-stu-id="f6fe0-115">Remarks</span></span>  
 <span data-ttu-id="f6fe0-116">參數的順序值 `ulParamSeq` 開頭為1。</span><span class="sxs-lookup"><span data-stu-id="f6fe0-116">The sequence values in `ulParamSeq` begin with 1 for parameters.</span></span> <span data-ttu-id="f6fe0-117">傳回值的序號為0。</span><span class="sxs-lookup"><span data-stu-id="f6fe0-117">A return value has a sequence number of 0.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="f6fe0-118">需求</span><span class="sxs-lookup"><span data-stu-id="f6fe0-118">Requirements</span></span>  
 <span data-ttu-id="f6fe0-119">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="f6fe0-119">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="f6fe0-120">**標頭：** Cor。h</span><span class="sxs-lookup"><span data-stu-id="f6fe0-120">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="f6fe0-121">連結**庫：** 做為 Mscoree.dll 中的資源使用</span><span class="sxs-lookup"><span data-stu-id="f6fe0-121">**Library:** Used as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="f6fe0-122">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="f6fe0-122">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f6fe0-123">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f6fe0-123">See also</span></span>

- [<span data-ttu-id="f6fe0-124">IMetaDataEmit 介面</span><span class="sxs-lookup"><span data-stu-id="f6fe0-124">IMetaDataEmit Interface</span></span>](imetadataemit-interface.md)
- [<span data-ttu-id="f6fe0-125">IMetaDataEmit2 介面</span><span class="sxs-lookup"><span data-stu-id="f6fe0-125">IMetaDataEmit2 Interface</span></span>](imetadataemit2-interface.md)
