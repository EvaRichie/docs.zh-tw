---
title: IMetaDataEmit::TranslateSigWithScope 方法
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.TranslateSigWithScope
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::TranslateSigWithScope
helpviewer_keywords:
- TranslateSigWithScope method [.NET Framework metadata]
- IMetaDataEmit::TranslateSigWithScope method [.NET Framework metadata]
ms.assetid: 47915d33-b7bf-409e-b484-4ee1df15de22
topic_type:
- apiref
ms.openlocfilehash: 80d33da2eb2a7f0cfbe5dcb7279fff9973dada2e
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95712920"
---
# <a name="imetadataemittranslatesigwithscope-method"></a><span data-ttu-id="2a8f5-102">IMetaDataEmit::TranslateSigWithScope 方法</span><span class="sxs-lookup"><span data-stu-id="2a8f5-102">IMetaDataEmit::TranslateSigWithScope Method</span></span>

<span data-ttu-id="2a8f5-103">將元件匯入到目前的範圍，並為合併的範圍取得新的中繼資料簽章。</span><span class="sxs-lookup"><span data-stu-id="2a8f5-103">Imports an assembly into the current scope and gets a new metadata signature for the merged scope.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="2a8f5-104">語法</span><span class="sxs-lookup"><span data-stu-id="2a8f5-104">Syntax</span></span>  
  
```cpp  
HRESULT TranslateSigWithScope (
    [in]  IMetaDataAssemblyImport   *pAssemImport,
    [in]  const void                *pbHashValue,
    [in]  ULONG                     cbHashValue,
    [in]  IMetaDataImport           *import,
    [in]  PCCOR_SIGNATURE           pbSigBlob,
    [in]  ULONG                     cbSigBlob,  
    [in]  IMetaDataAssemblyEmit     *pAssemEmit,
    [in]  IMetaDataEmit             *emit,
    [out] PCOR_SIGNATURE            pvTranslatedSig,
    [in]  ULONG                     cbTranslatedSigMax,
    [out] ULONG                     *pcbTranslatedSig
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="2a8f5-105">參數</span><span class="sxs-lookup"><span data-stu-id="2a8f5-105">Parameters</span></span>  

 `pAssemImport`  
 <span data-ttu-id="2a8f5-106">在匯入元件 (的介面) 定義簽章的位置。</span><span class="sxs-lookup"><span data-stu-id="2a8f5-106">[in] The interface for import assembly (where the signature is defined).</span></span>  
  
 `pbHashValue`  
 <span data-ttu-id="2a8f5-107">在元件的雜湊 blob。</span><span class="sxs-lookup"><span data-stu-id="2a8f5-107">[in] The hash blob for the assembly.</span></span>  
  
 `cbHashValue`  
 <span data-ttu-id="2a8f5-108">在中的位元組計數 `pbHashValue` 。</span><span class="sxs-lookup"><span data-stu-id="2a8f5-108">[in] The count of bytes in `pbHashValue`.</span></span>  
  
 `import`  
 <span data-ttu-id="2a8f5-109">在匯入中繼資料範圍的介面。</span><span class="sxs-lookup"><span data-stu-id="2a8f5-109">[in] The interface for import metadata scope.</span></span>  
  
 `pbSigBlob`  
 <span data-ttu-id="2a8f5-110">在要匯入的簽章。</span><span class="sxs-lookup"><span data-stu-id="2a8f5-110">[in] The signature to be imported.</span></span>  
  
 `cbSigBlob`  
 <span data-ttu-id="2a8f5-111">在的大小（以位元組為單位） `pbSigBlob` 。</span><span class="sxs-lookup"><span data-stu-id="2a8f5-111">[in] The size, in bytes, of `pbSigBlob`.</span></span>  
  
 `pAssemEmit`  
 <span data-ttu-id="2a8f5-112">在匯出元件的介面。</span><span class="sxs-lookup"><span data-stu-id="2a8f5-112">[in] The interface for export assembly.</span></span>  
  
 `emit`  
 <span data-ttu-id="2a8f5-113">在匯出中繼資料範圍的介面。</span><span class="sxs-lookup"><span data-stu-id="2a8f5-113">[in] The interface for export metadata scope.</span></span>  
  
 `pvTranslatedSig`  
 <span data-ttu-id="2a8f5-114">擴展保存已轉譯之簽章 blob 的緩衝區。</span><span class="sxs-lookup"><span data-stu-id="2a8f5-114">[out] The buffer to hold the translated signature blob.</span></span>  
  
 `cbTranslatedSigMax`  
 <span data-ttu-id="2a8f5-115">在的容量（以位元組為單位） `pvTranslatedSig` 。</span><span class="sxs-lookup"><span data-stu-id="2a8f5-115">[in] The capacity, in bytes, of `pvTranslatedSig`.</span></span>  
  
 `pcbTranslatedSig`  
 <span data-ttu-id="2a8f5-116">擴展轉譯簽章中的實際位元組數目。</span><span class="sxs-lookup"><span data-stu-id="2a8f5-116">[out] The number of actual bytes in the translated signature.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="2a8f5-117">需求</span><span class="sxs-lookup"><span data-stu-id="2a8f5-117">Requirements</span></span>  

 <span data-ttu-id="2a8f5-118">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="2a8f5-118">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="2a8f5-119">**標頭：** Cor。h</span><span class="sxs-lookup"><span data-stu-id="2a8f5-119">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="2a8f5-120">連結 **庫：** 當做 MSCorEE.dll 中的資源使用</span><span class="sxs-lookup"><span data-stu-id="2a8f5-120">**Library:** Used as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="2a8f5-121">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="2a8f5-121">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="2a8f5-122">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2a8f5-122">See also</span></span>

- [<span data-ttu-id="2a8f5-123">IMetaDataAssemblyEmit 介面</span><span class="sxs-lookup"><span data-stu-id="2a8f5-123">IMetaDataAssemblyEmit Interface</span></span>](imetadataassemblyemit-interface.md)
- [<span data-ttu-id="2a8f5-124">IMetaDataAssemblyImport 介面</span><span class="sxs-lookup"><span data-stu-id="2a8f5-124">IMetaDataAssemblyImport Interface</span></span>](imetadataassemblyimport-interface.md)
- [<span data-ttu-id="2a8f5-125">IMetaDataEmit 介面</span><span class="sxs-lookup"><span data-stu-id="2a8f5-125">IMetaDataEmit Interface</span></span>](imetadataemit-interface.md)
- [<span data-ttu-id="2a8f5-126">IMetaDataEmit2 介面</span><span class="sxs-lookup"><span data-stu-id="2a8f5-126">IMetaDataEmit2 Interface</span></span>](imetadataemit2-interface.md)
- [<span data-ttu-id="2a8f5-127">IMetaDataImport 介面</span><span class="sxs-lookup"><span data-stu-id="2a8f5-127">IMetaDataImport Interface</span></span>](imetadataimport-interface.md)
