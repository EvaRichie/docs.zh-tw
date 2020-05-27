---
title: IMetaDataAssemblyImport::GetAssemblyProps 方法
ms.date: 03/30/2017
api_name:
- IMetaDataAssemblyImport.GetAssemblyProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataAssemblyImport::GetAssemblyProps
helpviewer_keywords:
- GetAssemblyProps method [.NET Framework metadata]
- IMetaDataAssemblyImport::GetAssemblyProps method [.NET Framework metadata]
ms.assetid: 0eaa4aa9-9441-444a-920c-e4b2a2db899e
topic_type:
- apiref
ms.openlocfilehash: a90deaf3e9ddf326c6fca558cbb4681fc40e022d
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "84009050"
---
# <a name="imetadataassemblyimportgetassemblyprops-method"></a><span data-ttu-id="9089a-102">IMetaDataAssemblyImport::GetAssemblyProps 方法</span><span class="sxs-lookup"><span data-stu-id="9089a-102">IMetaDataAssemblyImport::GetAssemblyProps Method</span></span>
<span data-ttu-id="9089a-103">取得具有指定之中繼資料簽章之元件的屬性集。</span><span class="sxs-lookup"><span data-stu-id="9089a-103">Gets the set of properties for the assembly with the specified metadata signature.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="9089a-104">語法</span><span class="sxs-lookup"><span data-stu-id="9089a-104">Syntax</span></span>  
  
```cpp  
HRESULT GetAssemblyProps (  
    [in]  mdAssembly          mda,  
    [out] const void          **ppbPublicKey,
    [out] ULONG               *pcbPublicKey,  
    [out] ULONG               *pulHashAlgId,  
    [out] LPWSTR              szName,  
    [in] ULONG                cchName,  
    [out] ULONG               *pchName,  
    [out] ASSEMBLYMETADATA    *pMetaData,  
    [out] DWORD               *pdwAssemblyFlags  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="9089a-105">參數</span><span class="sxs-lookup"><span data-stu-id="9089a-105">Parameters</span></span>  
 `mda`  
 <span data-ttu-id="9089a-106">[in]。</span><span class="sxs-lookup"><span data-stu-id="9089a-106">[in].</span></span> <span data-ttu-id="9089a-107">`mdAssembly`表示要取得屬性之元件的元資料標記。</span><span class="sxs-lookup"><span data-stu-id="9089a-107">The `mdAssembly` metadata token that represents the assembly for which to get the properties.</span></span>  
  
 `ppbPublicKey`  
 <span data-ttu-id="9089a-108">脫銷公用金鑰或元資料標記的指標。</span><span class="sxs-lookup"><span data-stu-id="9089a-108">[out] A pointer to the public key or the metadata token.</span></span>  
  
 `pcbPublicKey`  
 <span data-ttu-id="9089a-109">脫銷傳回的公開金鑰中的位元組數目。</span><span class="sxs-lookup"><span data-stu-id="9089a-109">[out] The number of bytes in the returned public key.</span></span>  
  
 `pulHashAlgId`  
 <span data-ttu-id="9089a-110">脫銷用來雜湊元件中之檔案的演算法指標。</span><span class="sxs-lookup"><span data-stu-id="9089a-110">[out] A pointer to the algorithm used to hash the files in the assembly.</span></span>  
  
 `szName`  
 <span data-ttu-id="9089a-111">脫銷元件的簡單名稱。</span><span class="sxs-lookup"><span data-stu-id="9089a-111">[out] The simple name of the assembly.</span></span>  
  
 `cchName`  
 <span data-ttu-id="9089a-112">在的大小（以寬字元為單位） `szName` 。</span><span class="sxs-lookup"><span data-stu-id="9089a-112">[in] The size, in wide chars, of `szName`.</span></span>  
  
 `pchName`  
 <span data-ttu-id="9089a-113">脫銷中實際傳回的寬字元數 `szName` 。</span><span class="sxs-lookup"><span data-stu-id="9089a-113">[out] The number of wide chars actually returned in `szName`.</span></span>  
  
 `pMetaData`  
 <span data-ttu-id="9089a-114">脫銷包含元件中繼資料之 ASSEMBLYMETADATA 結構的指標。</span><span class="sxs-lookup"><span data-stu-id="9089a-114">[out] A pointer to an ASSEMBLYMETADATA structure that contains the assembly metadata.</span></span>  
  
 `pdwAssemblyFlags`  
 <span data-ttu-id="9089a-115">脫銷描述套用至元件之中繼資料的旗標。</span><span class="sxs-lookup"><span data-stu-id="9089a-115">[out] Flags that describe the metadata applied to an assembly.</span></span> <span data-ttu-id="9089a-116">這個值是一個或多個[CorAssemblyFlags](corassemblyflags-enumeration.md)值的組合。</span><span class="sxs-lookup"><span data-stu-id="9089a-116">This value is a combination of one or more [CorAssemblyFlags](corassemblyflags-enumeration.md) values.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="9089a-117">需求</span><span class="sxs-lookup"><span data-stu-id="9089a-117">Requirements</span></span>  
 <span data-ttu-id="9089a-118">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="9089a-118">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="9089a-119">**標頭：** Cor。h</span><span class="sxs-lookup"><span data-stu-id="9089a-119">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="9089a-120">連結**庫：** 做為 Mscoree.dll 中的資源使用</span><span class="sxs-lookup"><span data-stu-id="9089a-120">**Library:** Used as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="9089a-121">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="9089a-121">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="9089a-122">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9089a-122">See also</span></span>

- [<span data-ttu-id="9089a-123">IMetaDataAssemblyImport 介面</span><span class="sxs-lookup"><span data-stu-id="9089a-123">IMetaDataAssemblyImport Interface</span></span>](imetadataassemblyimport-interface.md)
