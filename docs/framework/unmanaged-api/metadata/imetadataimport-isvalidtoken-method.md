---
title: IMetaDataImport::IsValidToken 方法
ms.date: 03/30/2017
api_name:
- IMetaDataImport.IsValidToken
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::IsValidToken
helpviewer_keywords:
- IMetaDataImport::IsValidToken method [.NET Framework metadata]
- IsValidToken method [.NET Framework metadata]
ms.assetid: aeb0fc63-9eff-4384-9284-cb9900572d74
topic_type:
- apiref
ms.openlocfilehash: b4dc1e60f3d29e2671882d1900a1c49e56969601
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95702856"
---
# <a name="imetadataimportisvalidtoken-method"></a><span data-ttu-id="1d1e9-102">IMetaDataImport::IsValidToken 方法</span><span class="sxs-lookup"><span data-stu-id="1d1e9-102">IMetaDataImport::IsValidToken Method</span></span>

<span data-ttu-id="1d1e9-103">取得一個值，用來表示指定語彙基元是否包含程式碼物件的有效參考。</span><span class="sxs-lookup"><span data-stu-id="1d1e9-103">Gets a value indicating whether the specified token holds a valid reference to a code object.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="1d1e9-104">語法</span><span class="sxs-lookup"><span data-stu-id="1d1e9-104">Syntax</span></span>  
  
```cpp  
BOOL IsValidToken (  
   [in] mdToken     tk  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="1d1e9-105">參數</span><span class="sxs-lookup"><span data-stu-id="1d1e9-105">Parameters</span></span>  

 `tk`  
 <span data-ttu-id="1d1e9-106">在要檢查參考有效性的標記。</span><span class="sxs-lookup"><span data-stu-id="1d1e9-106">[in] The token to check the reference validity for.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="1d1e9-107">傳回值</span><span class="sxs-lookup"><span data-stu-id="1d1e9-107">Return Value</span></span>  

 <span data-ttu-id="1d1e9-108">`true` 如果在 `tk` 目前範圍內是有效的元資料標記，則為。</span><span class="sxs-lookup"><span data-stu-id="1d1e9-108">`true` if `tk` is a valid metadata token within the current scope.</span></span> <span data-ttu-id="1d1e9-109">否則為 `false`。</span><span class="sxs-lookup"><span data-stu-id="1d1e9-109">Otherwise, `false`.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="1d1e9-110">需求</span><span class="sxs-lookup"><span data-stu-id="1d1e9-110">Requirements</span></span>  

 <span data-ttu-id="1d1e9-111">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="1d1e9-111">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="1d1e9-112">**標頭：** Cor。h</span><span class="sxs-lookup"><span data-stu-id="1d1e9-112">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="1d1e9-113">連結 **庫：** 以資源的形式包含在 MsCorEE.dll 中</span><span class="sxs-lookup"><span data-stu-id="1d1e9-113">**Library:** Included as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="1d1e9-114">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="1d1e9-114">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="1d1e9-115">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1d1e9-115">See also</span></span>

- [<span data-ttu-id="1d1e9-116">IMetaDataImport 介面</span><span class="sxs-lookup"><span data-stu-id="1d1e9-116">IMetaDataImport Interface</span></span>](imetadataimport-interface.md)
- [<span data-ttu-id="1d1e9-117">IMetaDataImport2 介面</span><span class="sxs-lookup"><span data-stu-id="1d1e9-117">IMetaDataImport2 Interface</span></span>](imetadataimport2-interface.md)
