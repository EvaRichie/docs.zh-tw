---
title: IMetaDataEmit::DefineEvent 方法
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.DefineEvent
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::DefineEvent
helpviewer_keywords:
- IMetaDataEmit::DefineEvent method [.NET Framework metadata]
- DefineEvent method [.NET Framework metadata]
ms.assetid: cf064bac-9a9f-41c5-9e1d-108ff7af3afe
topic_type:
- apiref
ms.openlocfilehash: 7babd0a90b9882acb03b6360753f55c57a399b9e
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "84005620"
---
# <a name="imetadataemitdefineevent-method"></a><span data-ttu-id="f4d14-102">IMetaDataEmit::DefineEvent 方法</span><span class="sxs-lookup"><span data-stu-id="f4d14-102">IMetaDataEmit::DefineEvent Method</span></span>
<span data-ttu-id="f4d14-103">使用指定的中繼資料簽章建立事件的定義，並取得該事件定義的 token。</span><span class="sxs-lookup"><span data-stu-id="f4d14-103">Creates a definition for an event with the specified metadata signature, and gets a token to that event definition.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="f4d14-104">語法</span><span class="sxs-lookup"><span data-stu-id="f4d14-104">Syntax</span></span>  
  
```cpp  
HRESULT DefineEvent (
    [in]  mdTypeDef    td,
    [in]  LPCWSTR      szEvent,
    [in]  DWORD        dwEventFlags,
    [in]  mdToken      tkEventType,
    [in]  mdMethodDef  mdAddOn,
    [in]  mdMethodDef  mdRemoveOn,
    [in]  mdMethodDef  mdFire,
    [in]  mdMethodDef  rmdOtherMethods[],
    [out] mdEvent      *pmdEvent
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="f4d14-105">參數</span><span class="sxs-lookup"><span data-stu-id="f4d14-105">Parameters</span></span>  
 `td`  
 <span data-ttu-id="f4d14-106">在目標類別或介面的 token。</span><span class="sxs-lookup"><span data-stu-id="f4d14-106">[in] The token for the target class or interface.</span></span> <span data-ttu-id="f4d14-107">這可能是 `mdTypeDef` 或 `mdTypeDefNil` token。</span><span class="sxs-lookup"><span data-stu-id="f4d14-107">This is either a `mdTypeDef` or `mdTypeDefNil` token.</span></span>  
  
 `szEvent`  
 <span data-ttu-id="f4d14-108">在事件的名稱。</span><span class="sxs-lookup"><span data-stu-id="f4d14-108">[in] The name of the event.</span></span>  
  
 `dwEventFlags`  
 <span data-ttu-id="f4d14-109">在事件旗標。</span><span class="sxs-lookup"><span data-stu-id="f4d14-109">[in] Event flags.</span></span>  
  
 `tkEventType`  
 <span data-ttu-id="f4d14-110">在事件類別的 token。</span><span class="sxs-lookup"><span data-stu-id="f4d14-110">[in] The token for the event class.</span></span> <span data-ttu-id="f4d14-111">這是 `mdTypeDef` 、 `mdTypeRef` 或 `mdTokenNil` 權杖。</span><span class="sxs-lookup"><span data-stu-id="f4d14-111">This is a `mdTypeDef`, a `mdTypeRef`, or a `mdTokenNil` token.</span></span>  
  
 `mdAddOn`  
 <span data-ttu-id="f4d14-112">在用來訂閱事件的方法，或 null。</span><span class="sxs-lookup"><span data-stu-id="f4d14-112">[in] The method used to subscribe to the event, or null.</span></span>  
  
 `mdRemoveOn`  
 <span data-ttu-id="f4d14-113">在用來取消訂閱事件的方法，或 null。</span><span class="sxs-lookup"><span data-stu-id="f4d14-113">[in] The method used to unsubscribe to the event, or null.</span></span>  
  
 `mdFire`  
 <span data-ttu-id="f4d14-114">在用來引發事件的方法（由衍生類別）。</span><span class="sxs-lookup"><span data-stu-id="f4d14-114">[in] The method used (by a derived class) to raise the event.</span></span>  
  
 `rmdOtherMethods[]`  
 <span data-ttu-id="f4d14-115">在與事件相關聯之其他方法的權杖陣列。</span><span class="sxs-lookup"><span data-stu-id="f4d14-115">[in] An array of tokens for other methods associated with the event.</span></span> <span data-ttu-id="f4d14-116">陣列以 `mdMethodDefNil` 標記終止。</span><span class="sxs-lookup"><span data-stu-id="f4d14-116">The array is terminated with a `mdMethodDefNil` token.</span></span>  
  
 `pmdEvent`  
 <span data-ttu-id="f4d14-117">脫銷指派給事件的元資料標記。</span><span class="sxs-lookup"><span data-stu-id="f4d14-117">[out] The metadata token assigned to the event.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="f4d14-118">需求</span><span class="sxs-lookup"><span data-stu-id="f4d14-118">Requirements</span></span>  
 <span data-ttu-id="f4d14-119">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="f4d14-119">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="f4d14-120">**標頭：** Cor。h</span><span class="sxs-lookup"><span data-stu-id="f4d14-120">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="f4d14-121">連結**庫：** 做為 Mscoree.dll 中的資源使用</span><span class="sxs-lookup"><span data-stu-id="f4d14-121">**Library:** Used as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="f4d14-122">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="f4d14-122">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f4d14-123">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f4d14-123">See also</span></span>

- [<span data-ttu-id="f4d14-124">IMetaDataEmit 介面</span><span class="sxs-lookup"><span data-stu-id="f4d14-124">IMetaDataEmit Interface</span></span>](imetadataemit-interface.md)
- [<span data-ttu-id="f4d14-125">IMetaDataEmit2 介面</span><span class="sxs-lookup"><span data-stu-id="f4d14-125">IMetaDataEmit2 Interface</span></span>](imetadataemit2-interface.md)
