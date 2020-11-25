---
title: ASM_CACHE_FLAGS 列舉
ms.date: 03/30/2017
api_name:
- ASM_CACHE_FLAGS
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- ASM_CACHE_FLAGS
helpviewer_keywords:
- ASM_CACHE_FLAGS enumeration [.NET Framework fusion]
ms.assetid: 82e9a7da-321b-48b8-b239-52eaffda6be8
topic_type:
- apiref
ms.openlocfilehash: 6c6fab627f21977e85f9885ca4b49a0276faa5ce
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95732160"
---
# <a name="asm_cache_flags-enumeration"></a><span data-ttu-id="13188-102">ASM_CACHE_FLAGS 列舉</span><span class="sxs-lookup"><span data-stu-id="13188-102">ASM_CACHE_FLAGS Enumeration</span></span>

<span data-ttu-id="13188-103">表示全域組件快取中 [IAssemblyCacheItem](iassemblycacheitem-interface.md) 所代表之元件的來源。</span><span class="sxs-lookup"><span data-stu-id="13188-103">Indicates the source of an assembly that is represented by [IAssemblyCacheItem](iassemblycacheitem-interface.md) in the global assembly cache.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="13188-104">語法</span><span class="sxs-lookup"><span data-stu-id="13188-104">Syntax</span></span>  
  
```cpp  
typedef enum {  
    ASM_CACHE_ZAP       = 0x01,  
    ASM_CACHE_GAC       = 0x02,  
    ASM_CACHE_DOWNLOAD  = 0x04,  
    ASM_CACHE_ROOT      = 0x08,  
    ASM_CACHE_ROOT_EX   = 0x80  
} ASM_CACHE_FLAGS;  
```  
  
## <a name="members"></a><span data-ttu-id="13188-105">成員</span><span class="sxs-lookup"><span data-stu-id="13188-105">Members</span></span>  
  
|<span data-ttu-id="13188-106">member</span><span class="sxs-lookup"><span data-stu-id="13188-106">Member</span></span>|<span data-ttu-id="13188-107">描述</span><span class="sxs-lookup"><span data-stu-id="13188-107">Description</span></span>|  
|------------|-----------------|  
|`ASM_CACHE_ZAP`|<span data-ttu-id="13188-108">使用 Ngen.exe 來列舉先行編譯元件的快取。</span><span class="sxs-lookup"><span data-stu-id="13188-108">Enumerates the cache of precompiled assemblies by using Ngen.exe.</span></span>|  
|`ASM_CACHE_GAC`|<span data-ttu-id="13188-109">列舉全域組件快取。</span><span class="sxs-lookup"><span data-stu-id="13188-109">Enumerates the global assembly cache.</span></span>|  
|`ASM_CACHE_DOWNLOAD`|<span data-ttu-id="13188-110">列舉視需要下載或已陰影複製的元件。</span><span class="sxs-lookup"><span data-stu-id="13188-110">Enumerates the assemblies that have been downloaded on demand or that have been shadow-copied.</span></span>|  
|`ASM_CACHE_ROOT`|<span data-ttu-id="13188-111">指出 [GetCachePath](getcachepath-function.md) 函式應該會傳回 common language RUNTIME (CLR) 2.0 版的全域組件快取的路徑。</span><span class="sxs-lookup"><span data-stu-id="13188-111">Indicates that the [GetCachePath](getcachepath-function.md) function should return the path to the global assembly cache for the common language runtime (CLR) version 2.0.</span></span> <span data-ttu-id="13188-112">只有在呼叫 [GetCachePath](getcachepath-function.md)的內容中有意義。</span><span class="sxs-lookup"><span data-stu-id="13188-112">Meaningful only in the context of a call to [GetCachePath](getcachepath-function.md).</span></span>|  
|`ASM_CACHE_ROOT_EX`|<span data-ttu-id="13188-113">指出 [GetCachePath](getcachepath-function.md) 函式應傳回 CLR 第4版全域組件快取的路徑。</span><span class="sxs-lookup"><span data-stu-id="13188-113">Indicates that the [GetCachePath](getcachepath-function.md) function should return the path to the global assembly cache for CLR version 4.</span></span> <span data-ttu-id="13188-114">只有在呼叫 [GetCachePath](getcachepath-function.md)的內容中有意義。</span><span class="sxs-lookup"><span data-stu-id="13188-114">Meaningful only in the context of a call to [GetCachePath](getcachepath-function.md).</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="13188-115">需求</span><span class="sxs-lookup"><span data-stu-id="13188-115">Requirements</span></span>  

 <span data-ttu-id="13188-116">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="13188-116">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="13188-117">**標頭：** 融合。h</span><span class="sxs-lookup"><span data-stu-id="13188-117">**Header:** Fusion.h</span></span>  
  
 <span data-ttu-id="13188-118">連結 **庫：** 以資源的形式包含在 MsCorEE.dll 中</span><span class="sxs-lookup"><span data-stu-id="13188-118">**Library:** Included as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="13188-119">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="13188-119">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="13188-120">另請參閱</span><span class="sxs-lookup"><span data-stu-id="13188-120">See also</span></span>

- [<span data-ttu-id="13188-121">GetCachePath 函式</span><span class="sxs-lookup"><span data-stu-id="13188-121">GetCachePath Function</span></span>](getcachepath-function.md)
- [<span data-ttu-id="13188-122">IAssemblyCacheItem 介面</span><span class="sxs-lookup"><span data-stu-id="13188-122">IAssemblyCacheItem Interface</span></span>](iassemblycacheitem-interface.md)
- [<span data-ttu-id="13188-123">融合列舉</span><span class="sxs-lookup"><span data-stu-id="13188-123">Fusion Enumerations</span></span>](fusion-enumerations.md)
