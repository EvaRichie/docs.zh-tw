---
title: ICorPublishEnum::Clone 方法
ms.date: 03/30/2017
api_name:
- ICorPublishEnum.Clone
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorPublishEnum::Clone
helpviewer_keywords:
- Clone method, ICorPublishEnum interface [.NET Framework debugging]
- ICorPublishEnum::Clone method [.NET Framework debugging]
ms.assetid: c9a26ea3-b8eb-4b8e-854f-9a2ca26b3b39
topic_type:
- apiref
ms.openlocfilehash: 38f49e8fe632e9b38ede8815de6d8865278351f9
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83421198"
---
# <a name="icorpublishenumclone-method"></a><span data-ttu-id="637cd-102">ICorPublishEnum::Clone 方法</span><span class="sxs-lookup"><span data-stu-id="637cd-102">ICorPublishEnum::Clone Method</span></span>
<span data-ttu-id="637cd-103">建立這個[ICorPublishEnum](icorpublishenum-interface.md)物件的複本。</span><span class="sxs-lookup"><span data-stu-id="637cd-103">Creates a copy of this [ICorPublishEnum](icorpublishenum-interface.md) object.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="637cd-104">語法</span><span class="sxs-lookup"><span data-stu-id="637cd-104">Syntax</span></span>  
  
```cpp  
HRESULT Clone (  
    [out] ICorPublishEnum   **ppEnum  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="637cd-105">參數</span><span class="sxs-lookup"><span data-stu-id="637cd-105">Parameters</span></span>  
 `ppEnum`  
 <span data-ttu-id="637cd-106">脫銷物件位址的指標，該 `ICorPublishEnum` 物件為此物件的複本 `ICorPublishEnum` 。</span><span class="sxs-lookup"><span data-stu-id="637cd-106">[out] A pointer to the address of an `ICorPublishEnum` object that is a copy of this `ICorPublishEnum` object.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="637cd-107">需求</span><span class="sxs-lookup"><span data-stu-id="637cd-107">Requirements</span></span>  
 <span data-ttu-id="637cd-108">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="637cd-108">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="637cd-109">**標頭：** CorPub .idl，CorPub。h</span><span class="sxs-lookup"><span data-stu-id="637cd-109">**Header:** CorPub.idl, CorPub.h</span></span>  
  
 <span data-ttu-id="637cd-110">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="637cd-110">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="637cd-111">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="637cd-111">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="637cd-112">另請參閱</span><span class="sxs-lookup"><span data-stu-id="637cd-112">See also</span></span>

- [<span data-ttu-id="637cd-113">ICorPublishEnum 介面</span><span class="sxs-lookup"><span data-stu-id="637cd-113">ICorPublishEnum Interface</span></span>](icorpublishenum-interface.md)
