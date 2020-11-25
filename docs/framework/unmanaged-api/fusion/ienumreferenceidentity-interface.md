---
title: IEnumReferenceIdentity 介面
ms.date: 03/30/2017
api_name:
- IEnumReferenceIdentity
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IEnumReferenceIdentity
helpviewer_keywords:
- IEnumReferenceIdentity interface [.NET Framework fusion]
ms.assetid: a17b3155-7216-4e16-8c9f-abce21f549e7
topic_type:
- apiref
ms.openlocfilehash: bea357fe9a154ffb8f69228c7332c026dc2759e9
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95728964"
---
# <a name="ienumreferenceidentity-interface"></a><span data-ttu-id="61b70-102">IEnumReferenceIdentity 介面</span><span class="sxs-lookup"><span data-stu-id="61b70-102">IEnumReferenceIdentity Interface</span></span>

<span data-ttu-id="61b70-103">作為物件集合的列舉值 `IReferenceIdentity` 。</span><span class="sxs-lookup"><span data-stu-id="61b70-103">Serves as an enumerator for a collection of `IReferenceIdentity` objects.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="61b70-104">方法</span><span class="sxs-lookup"><span data-stu-id="61b70-104">Methods</span></span>  
  
|<span data-ttu-id="61b70-105">方法</span><span class="sxs-lookup"><span data-stu-id="61b70-105">Method</span></span>|<span data-ttu-id="61b70-106">描述</span><span class="sxs-lookup"><span data-stu-id="61b70-106">Description</span></span>|  
|------------|-----------------|  
|`IEnumReferenceIdentity::Clone`|<span data-ttu-id="61b70-107">取得新的介面指標， `IEnumReferenceIdentity` 其中包含與這個相同的成員 `IEnumReferenceIdentity` 。</span><span class="sxs-lookup"><span data-stu-id="61b70-107">Gets an interface pointer to a new `IEnumReferenceIdentity` that contains the same members as this `IEnumReferenceIdentity`.</span></span>|  
|`IEnumReferenceIdentity::Next`|<span data-ttu-id="61b70-108">`IReferenceIdentity`從目前位置開始取得指定數目的物件。</span><span class="sxs-lookup"><span data-stu-id="61b70-108">Gets the specified number of `IReferenceIdentity` objects, starting at the current position.</span></span>|  
|`IEnumReferenceIdentity::Reset`|<span data-ttu-id="61b70-109">將指令指標移至這個的開頭 `IEnumReferenceIdentity` 。</span><span class="sxs-lookup"><span data-stu-id="61b70-109">Moves the instruction pointer to the beginning of this `IEnumReferenceIdentity`.</span></span>|  
|`IEnumReferenceIdentity::Skip`|<span data-ttu-id="61b70-110">從目前位置開始，將指令指標向下移動指定數目的元素。</span><span class="sxs-lookup"><span data-stu-id="61b70-110">Moves the instruction pointer forward by the specified number of elements, starting at the current position.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="61b70-111">需求</span><span class="sxs-lookup"><span data-stu-id="61b70-111">Requirements</span></span>  

 <span data-ttu-id="61b70-112">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="61b70-112">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="61b70-113">**標頭：** 隔離。h</span><span class="sxs-lookup"><span data-stu-id="61b70-113">**Header:** Isolation.h</span></span>  
  
 <span data-ttu-id="61b70-114">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="61b70-114">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="61b70-115">另請參閱</span><span class="sxs-lookup"><span data-stu-id="61b70-115">See also</span></span>

- [<span data-ttu-id="61b70-116">融合介面</span><span class="sxs-lookup"><span data-stu-id="61b70-116">Fusion Interfaces</span></span>](fusion-interfaces.md)
- [<span data-ttu-id="61b70-117">IReferenceIdentity 介面</span><span class="sxs-lookup"><span data-stu-id="61b70-117">IReferenceIdentity Interface</span></span>](ireferenceidentity-interface.md)
