---
title: IMetaDataEmit::Save 方法
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.Save
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::Save
helpviewer_keywords:
- Save method, IMetaDataEmit interface [.NET Framework metadata]
- IMetaDataEmit::Save method [.NET Framework metadata]
ms.assetid: c1de8400-adfe-4a71-b828-a1d0cc1ea505
topic_type:
- apiref
ms.openlocfilehash: cef238239417a0a30cd94eaa8bd60968cfa78859
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95721994"
---
# <a name="imetadataemitsave-method"></a><span data-ttu-id="e0c76-102">IMetaDataEmit::Save 方法</span><span class="sxs-lookup"><span data-stu-id="e0c76-102">IMetaDataEmit::Save Method</span></span>

<span data-ttu-id="e0c76-103">將目前範圍中的所有中繼資料儲存至檔案的指定位址。</span><span class="sxs-lookup"><span data-stu-id="e0c76-103">Saves all metadata in the current scope to the file at the specified address.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="e0c76-104">語法</span><span class="sxs-lookup"><span data-stu-id="e0c76-104">Syntax</span></span>  
  
```cpp  
HRESULT Save (
    [in]  LPCWSTR     szFile,
    [in]  DWORD       dwSaveFlags  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="e0c76-105">參數</span><span class="sxs-lookup"><span data-stu-id="e0c76-105">Parameters</span></span>  

 `wzFile`  
 <span data-ttu-id="e0c76-106">在要儲存的檔案名。</span><span class="sxs-lookup"><span data-stu-id="e0c76-106">[in] The name of the file to save to.</span></span> <span data-ttu-id="e0c76-107">如果這個值為 null，記憶體中的複本將會儲存到最後使用的位置。</span><span class="sxs-lookup"><span data-stu-id="e0c76-107">If this value is null, the in-memory copy will be saved to the last location that was used.</span></span>  
  
 `dwSaveFlags`  
 <span data-ttu-id="e0c76-108">[in] 保留。</span><span class="sxs-lookup"><span data-stu-id="e0c76-108">[in] Reserved.</span></span> <span data-ttu-id="e0c76-109">必須為零。</span><span class="sxs-lookup"><span data-stu-id="e0c76-109">Must be zero.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="e0c76-110">需求</span><span class="sxs-lookup"><span data-stu-id="e0c76-110">Requirements</span></span>  

 <span data-ttu-id="e0c76-111">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="e0c76-111">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="e0c76-112">**標頭：** Cor。h</span><span class="sxs-lookup"><span data-stu-id="e0c76-112">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="e0c76-113">連結 **庫：** 當做 MSCorEE.dll 中的資源使用</span><span class="sxs-lookup"><span data-stu-id="e0c76-113">**Library:** Used as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="e0c76-114">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="e0c76-114">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e0c76-115">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e0c76-115">See also</span></span>

- [<span data-ttu-id="e0c76-116">IMetaDataEmit 介面</span><span class="sxs-lookup"><span data-stu-id="e0c76-116">IMetaDataEmit Interface</span></span>](imetadataemit-interface.md)
- [<span data-ttu-id="e0c76-117">IMetaDataEmit2 介面</span><span class="sxs-lookup"><span data-stu-id="e0c76-117">IMetaDataEmit2 Interface</span></span>](imetadataemit2-interface.md)
