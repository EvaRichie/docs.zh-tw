---
title: IMetaDataEmit::ApplyEditAndContinue 方法
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.ApplyEditAndContinue
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::ApplyEditAndContinue
helpviewer_keywords:
- ApplyEditAndContinue method [.NET Framework metadata]
- IMetaDataEmit::ApplyEditAndContinue method [.NET Framework metadata]
ms.assetid: 35991289-f389-495d-8caa-a6384fb1d557
topic_type:
- apiref
ms.openlocfilehash: 0cc84893c4937bf6b23eae0d63b92b3b871901dd
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95700570"
---
# <a name="imetadataemitapplyeditandcontinue-method"></a><span data-ttu-id="8a450-102">IMetaDataEmit::ApplyEditAndContinue 方法</span><span class="sxs-lookup"><span data-stu-id="8a450-102">IMetaDataEmit::ApplyEditAndContinue Method</span></span>

<span data-ttu-id="8a450-103">使用指定的中繼資料所做的變更，更新目前的元件範圍。</span><span class="sxs-lookup"><span data-stu-id="8a450-103">Updates the current assembly scope with the changes made in the specified metadata.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="8a450-104">語法</span><span class="sxs-lookup"><span data-stu-id="8a450-104">Syntax</span></span>  
  
```cpp  
HRESULT ApplyEditAndContinue (
    [in]  IUnknown    *pImport  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="8a450-105">參數</span><span class="sxs-lookup"><span data-stu-id="8a450-105">Parameters</span></span>  

 `pImport`  
 <span data-ttu-id="8a450-106">\[在 \] 代表可攜式可執行檔的 delta 中繼資料之 [IUnknown](/cpp/atl/iunknown) 物件的指標， (PE) 檔。</span><span class="sxs-lookup"><span data-stu-id="8a450-106">\[in\] Pointer to an [IUnknown](/cpp/atl/iunknown) object that represents the delta metadata from the portable executable (PE) file.</span></span>
  
 <span data-ttu-id="8a450-107">差異中繼資料是中繼資料的區塊，其中包含對模組的實際中繼資料複本所做的變更。</span><span class="sxs-lookup"><span data-stu-id="8a450-107">The delta metadata is the block of metadata that includes the changes that were made to the copy of the module's actual metadata.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="8a450-108">需求</span><span class="sxs-lookup"><span data-stu-id="8a450-108">Requirements</span></span>  

 <span data-ttu-id="8a450-109">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="8a450-109">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="8a450-110">**標頭：** Cor。h</span><span class="sxs-lookup"><span data-stu-id="8a450-110">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="8a450-111">連結 **庫：** 當做 MSCorEE.dll 中的資源使用</span><span class="sxs-lookup"><span data-stu-id="8a450-111">**Library:** Used as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="8a450-112">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="8a450-112">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8a450-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8a450-113">See also</span></span>

- [<span data-ttu-id="8a450-114">IMetaDataEmit 介面</span><span class="sxs-lookup"><span data-stu-id="8a450-114">IMetaDataEmit Interface</span></span>](imetadataemit-interface.md)
- [<span data-ttu-id="8a450-115">IMetaDataEmit2 介面</span><span class="sxs-lookup"><span data-stu-id="8a450-115">IMetaDataEmit2 Interface</span></span>](imetadataemit2-interface.md)
