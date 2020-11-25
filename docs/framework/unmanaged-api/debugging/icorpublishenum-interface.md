---
title: ICorPublishEnum 介面
ms.date: 03/30/2017
api_name:
- ICorPublishEnum
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorPublishEnum
helpviewer_keywords:
- ICorPublishEnum interface [.NET Framework debugging]
ms.assetid: 76a136b5-e444-417a-8ade-f1596d597dc7
topic_type:
- apiref
ms.openlocfilehash: 492d4b727ce507340fec47d30a791aa49d0cecb6
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95693342"
---
# <a name="icorpublishenum-interface"></a><span data-ttu-id="b80d9-102">ICorPublishEnum 介面</span><span class="sxs-lookup"><span data-stu-id="b80d9-102">ICorPublishEnum Interface</span></span>

<span data-ttu-id="b80d9-103">作為列舉值的抽象基底介面，用於發行有關處理常式和應用程式域的資訊。</span><span class="sxs-lookup"><span data-stu-id="b80d9-103">Serves as the abstract base interface for the enumerators that are used in the publishing of information about processes and application domains.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="b80d9-104">方法</span><span class="sxs-lookup"><span data-stu-id="b80d9-104">Methods</span></span>  
  
|<span data-ttu-id="b80d9-105">方法</span><span class="sxs-lookup"><span data-stu-id="b80d9-105">Method</span></span>|<span data-ttu-id="b80d9-106">描述</span><span class="sxs-lookup"><span data-stu-id="b80d9-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="b80d9-107">Clone 方法</span><span class="sxs-lookup"><span data-stu-id="b80d9-107">Clone Method</span></span>](icorpublishenum-clone-method.md)|<span data-ttu-id="b80d9-108">建立這個 `ICorPublishEnum` 物件的複本。</span><span class="sxs-lookup"><span data-stu-id="b80d9-108">Creates a copy of this `ICorPublishEnum` object.</span></span>|  
|[<span data-ttu-id="b80d9-109">GetCount 方法</span><span class="sxs-lookup"><span data-stu-id="b80d9-109">GetCount Method</span></span>](icorpublishenum-getcount-method.md)|<span data-ttu-id="b80d9-110">取得列舉中的專案數。</span><span class="sxs-lookup"><span data-stu-id="b80d9-110">Gets the number of items in the enumeration.</span></span>|  
|[<span data-ttu-id="b80d9-111">Reset 方法</span><span class="sxs-lookup"><span data-stu-id="b80d9-111">Reset Method</span></span>](icorpublishenum-reset-method.md)|<span data-ttu-id="b80d9-112">將游標移至列舉的開頭。</span><span class="sxs-lookup"><span data-stu-id="b80d9-112">Moves the cursor of to the beginning of the enumeration.</span></span>|  
|[<span data-ttu-id="b80d9-113">Skip 方法</span><span class="sxs-lookup"><span data-stu-id="b80d9-113">Skip Method</span></span>](icorpublishenum-skip-method.md)|<span data-ttu-id="b80d9-114">依指定的專案數將游標向前移動至列舉。</span><span class="sxs-lookup"><span data-stu-id="b80d9-114">Moves the cursor forward in the enumeration by the specified number of items.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="b80d9-115">備註</span><span class="sxs-lookup"><span data-stu-id="b80d9-115">Remarks</span></span>  

 <span data-ttu-id="b80d9-116">下列列舉值衍生自 `ICorPublishEnum` ：</span><span class="sxs-lookup"><span data-stu-id="b80d9-116">The following enumerators derive from `ICorPublishEnum`:</span></span>  
  
- [<span data-ttu-id="b80d9-117">ICorPublishAppDomainEnum</span><span class="sxs-lookup"><span data-stu-id="b80d9-117">ICorPublishAppDomainEnum</span></span>](icorpublishappdomainenum-interface.md)  
  
- [<span data-ttu-id="b80d9-118">ICorPublishProcessEnum</span><span class="sxs-lookup"><span data-stu-id="b80d9-118">ICorPublishProcessEnum</span></span>](icorpublishprocessenum-interface.md)  
  
## <a name="requirements"></a><span data-ttu-id="b80d9-119">需求</span><span class="sxs-lookup"><span data-stu-id="b80d9-119">Requirements</span></span>  

 <span data-ttu-id="b80d9-120">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="b80d9-120">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="b80d9-121">**標頭：** CorPub .idl、CorPub。h</span><span class="sxs-lookup"><span data-stu-id="b80d9-121">**Header:** CorPub.idl, CorPub.h</span></span>  
  
 <span data-ttu-id="b80d9-122">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="b80d9-122">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="b80d9-123">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="b80d9-123">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b80d9-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b80d9-124">See also</span></span>

- [<span data-ttu-id="b80d9-125">CorpubPublish Coclass</span><span class="sxs-lookup"><span data-stu-id="b80d9-125">CorpubPublish Coclass</span></span>](corpubpublish-coclass.md)
- [<span data-ttu-id="b80d9-126">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="b80d9-126">Debugging Interfaces</span></span>](debugging-interfaces.md)
