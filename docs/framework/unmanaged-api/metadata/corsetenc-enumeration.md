---
title: CorSetENC 列舉
ms.date: 03/30/2017
api_name:
- CorSetENC
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorSetENC
helpviewer_keywords:
- CorSetENC enumeration [.NET Framework metadata]
ms.assetid: fe4150e8-071d-43fb-8e06-c3c616dbeed2
topic_type:
- apiref
ms.openlocfilehash: df945803f2d56d04ccc68f314eb55665579ed7fd
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95705978"
---
# <a name="corsetenc-enumeration"></a><span data-ttu-id="8416e-102">CorSetENC 列舉</span><span class="sxs-lookup"><span data-stu-id="8416e-102">CorSetENC Enumeration</span></span>

<span data-ttu-id="8416e-103">包含值，可用來在中繼資料產生期間影響行為。</span><span class="sxs-lookup"><span data-stu-id="8416e-103">Contains values used to influence behavior during the generation of metadata.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="8416e-104">語法</span><span class="sxs-lookup"><span data-stu-id="8416e-104">Syntax</span></span>  
  
```cpp  
typedef enum CorSetENC {  
  
    MDSetENCOn                  = 0x00000001,  
    MDSetENCOff                 = 0x00000002,  
  
    MDUpdateENC                 = 0x00000001,  
    MDUpdateFull                = 0x00000002,  
    MDUpdateExtension           = 0x00000003,  
    MDUpdateIncremental         = 0x00000004,  
    MDUpdateDelta               = 0x00000005,  
    MDUpdateMask                = 0x00000007  
  
} CorSetENC;  
```  
  
## <a name="members"></a><span data-ttu-id="8416e-105">成員</span><span class="sxs-lookup"><span data-stu-id="8416e-105">Members</span></span>  
  
|<span data-ttu-id="8416e-106">member</span><span class="sxs-lookup"><span data-stu-id="8416e-106">Member</span></span>|<span data-ttu-id="8416e-107">描述</span><span class="sxs-lookup"><span data-stu-id="8416e-107">Description</span></span>|  
|------------|-----------------|  
|`MDSetENCOn`|<span data-ttu-id="8416e-108">已過時。</span><span class="sxs-lookup"><span data-stu-id="8416e-108">Obsolete.</span></span>|  
|`MDSetENCOff`|<span data-ttu-id="8416e-109">已過時。</span><span class="sxs-lookup"><span data-stu-id="8416e-109">Obsolete.</span></span>|  
|`MDUpdateENC`|<span data-ttu-id="8416e-110">指出中繼資料可以更新，而無法移動 token。</span><span class="sxs-lookup"><span data-stu-id="8416e-110">Indicates that whereas metadata can be updated, tokens cannot be moved.</span></span>|  
|`MDUpdateFull`|<span data-ttu-id="8416e-111">指出權杖可以在更新期間移動。</span><span class="sxs-lookup"><span data-stu-id="8416e-111">Indicates that tokens can be moved during updates.</span></span>|  
|`MDUpdateExtension`|<span data-ttu-id="8416e-112">表示更新只能包含新增專案。</span><span class="sxs-lookup"><span data-stu-id="8416e-112">Indicates that updates can consist only of additions.</span></span> <span data-ttu-id="8416e-113">無法移動標記。</span><span class="sxs-lookup"><span data-stu-id="8416e-113">Tokens cannot be moved.</span></span>|  
|`MDUpdateIncremental`|<span data-ttu-id="8416e-114">表示編譯為累加式。</span><span class="sxs-lookup"><span data-stu-id="8416e-114">Indicates that compilation is incremental.</span></span>|  
|`MDUpdateDelta`|<span data-ttu-id="8416e-115">指出只應儲存變更的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="8416e-115">Indicates that only changed metadata should be saved.</span></span>|  
|`MDUpdateMask`|<span data-ttu-id="8416e-116">包含 `MDUpdateENC` 、 `MDUpdateFull` 和 `MDUpdateIncremental` 。</span><span class="sxs-lookup"><span data-stu-id="8416e-116">Includes `MDUpdateENC`, `MDUpdateFull` and `MDUpdateIncremental`.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="8416e-117">需求</span><span class="sxs-lookup"><span data-stu-id="8416e-117">Requirements</span></span>  

 <span data-ttu-id="8416e-118">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="8416e-118">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="8416e-119">**標頭：** Corhdr.h。h</span><span class="sxs-lookup"><span data-stu-id="8416e-119">**Header:** CorHdr.h</span></span>  
  
 <span data-ttu-id="8416e-120">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="8416e-120">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8416e-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8416e-121">See also</span></span>

- [<span data-ttu-id="8416e-122">中繼資料列舉</span><span class="sxs-lookup"><span data-stu-id="8416e-122">Metadata Enumerations</span></span>](metadata-enumerations.md)
