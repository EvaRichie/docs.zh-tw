---
title: CorMethodImpl 列舉
ms.date: 03/30/2017
api_name:
- CorMethodImpl
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorMethodImpl
helpviewer_keywords:
- CorMethodImpl enumeration [.NET Framework metadata]
ms.assetid: ffbb3caf-20da-4a4b-8983-77376e72b990
topic_type:
- apiref
ms.openlocfilehash: b32e8f0b03ef6d550c384f3d932cc295a7270028
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "84007659"
---
# <a name="cormethodimpl-enumeration"></a><span data-ttu-id="8185f-102">CorMethodImpl 列舉</span><span class="sxs-lookup"><span data-stu-id="8185f-102">CorMethodImpl Enumeration</span></span>
<span data-ttu-id="8185f-103">包含值，這些值描述方法實作功能。</span><span class="sxs-lookup"><span data-stu-id="8185f-103">Contains values that describe method implementation features.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="8185f-104">語法</span><span class="sxs-lookup"><span data-stu-id="8185f-104">Syntax</span></span>  
  
```cpp  
typedef enum CorMethodImpl {  
  
    miCodeTypeMask      =   0x0003,  
    miIL                =   0x0000,  
    miNative            =   0x0001,  
    miOPTIL             =   0x0002,  
    miRuntime           =   0x0003,  
  
    miManagedMask       =   0x0004,  
    miUnmanaged         =   0x0004,  
    miManaged           =   0x0000,  
  
    miForwardRef        =   0x0010,  
    miPreserveSig       =   0x0080,  
  
    miInternalCall      =   0x1000,  
    miSynchronized      =   0x0020,  
    miNoInlining        =   0x0008,  
    miAggressiveInlining =  0x0100,  
    miNoOptimization     =  0x0040,  
    miMaxMethodImplVal  =   0xffff  
  
} CorMethodImpl;  
```  
  
## <a name="members"></a><span data-ttu-id="8185f-105">成員</span><span class="sxs-lookup"><span data-stu-id="8185f-105">Members</span></span>  
  
|<span data-ttu-id="8185f-106">成員</span><span class="sxs-lookup"><span data-stu-id="8185f-106">Member</span></span>|<span data-ttu-id="8185f-107">描述</span><span class="sxs-lookup"><span data-stu-id="8185f-107">Description</span></span>|  
|------------|-----------------|  
|`miCodeTypeMask`|<span data-ttu-id="8185f-108">描述程式碼類型的旗標。</span><span class="sxs-lookup"><span data-stu-id="8185f-108">Flags that describe code type.</span></span>|  
|`miIL`|<span data-ttu-id="8185f-109">指定方法實作為 Microsoft 中繼語言（MSIL）。</span><span class="sxs-lookup"><span data-stu-id="8185f-109">Specifies that the method implementation is Microsoft intermediate language (MSIL).</span></span>|  
|`miNative`|<span data-ttu-id="8185f-110">指定方法實作為原生。</span><span class="sxs-lookup"><span data-stu-id="8185f-110">Specifies that the method implementation is native.</span></span>|  
|`miOPTIL`|<span data-ttu-id="8185f-111">指定方法實作為 OPTIL。</span><span class="sxs-lookup"><span data-stu-id="8185f-111">Specifies that the method implementation is OPTIL.</span></span>|  
|`miRuntime`|<span data-ttu-id="8185f-112">指定方法實作為 common language runtime 所提供。</span><span class="sxs-lookup"><span data-stu-id="8185f-112">Specifies that the method implementation is provided by the common language runtime.</span></span>|  
|`miManagedMask`|<span data-ttu-id="8185f-113">旗標，指出程式碼為 managed 或非受控。</span><span class="sxs-lookup"><span data-stu-id="8185f-113">Flags that indicate whether the code is managed or unmanaged.</span></span>|  
|`miUnmanaged`|<span data-ttu-id="8185f-114">指定方法實作為未受管理。</span><span class="sxs-lookup"><span data-stu-id="8185f-114">Specifies that the method implementation is unmanaged.</span></span>|  
|`miManaged`|<span data-ttu-id="8185f-115">指定方法的實作為管理。</span><span class="sxs-lookup"><span data-stu-id="8185f-115">Specifies that the method implementation is managed.</span></span>|  
|`miForwardRef`|<span data-ttu-id="8185f-116">指定方法已定義。</span><span class="sxs-lookup"><span data-stu-id="8185f-116">Specifies that the method is defined.</span></span> <span data-ttu-id="8185f-117">這個旗標主要用於合併案例中。</span><span class="sxs-lookup"><span data-stu-id="8185f-117">This flag is used primarily in merge scenarios.</span></span>|  
|`miPreserveSig`|<span data-ttu-id="8185f-118">指定方法簽章不能因 HRESULT 轉換而改變。</span><span class="sxs-lookup"><span data-stu-id="8185f-118">Specifies that the method signature cannot be mangled for an HRESULT conversion.</span></span>|  
|`miInternalCall`|<span data-ttu-id="8185f-119">保留供 common language runtime 內部使用。</span><span class="sxs-lookup"><span data-stu-id="8185f-119">Reserved for internal use by the common language runtime.</span></span>|  
|`miSynchronized`|<span data-ttu-id="8185f-120">指定方法是透過其主體的單一執行緒。</span><span class="sxs-lookup"><span data-stu-id="8185f-120">Specifies that the method is single-threaded through its body.</span></span>|  
|`miNoInlining`|<span data-ttu-id="8185f-121">指定方法無法內嵌。</span><span class="sxs-lookup"><span data-stu-id="8185f-121">Specifies that the method cannot be inlined.</span></span>|  
|`miAggressiveInlining`|<span data-ttu-id="8185f-122">指定方法應該盡可能內嵌。</span><span class="sxs-lookup"><span data-stu-id="8185f-122">Specifies that the method should be inlined if possible.</span></span>|  
|`miNoOptimization`|<span data-ttu-id="8185f-123">指定不應該優化方法。</span><span class="sxs-lookup"><span data-stu-id="8185f-123">Specifies that the method should not be optimized.</span></span>|  
|`miMaxMethodImplVal`|<span data-ttu-id="8185f-124">的最大有效值 `CorMethodImpl` 。</span><span class="sxs-lookup"><span data-stu-id="8185f-124">The maximum valid value for a `CorMethodImpl`.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="8185f-125">需求</span><span class="sxs-lookup"><span data-stu-id="8185f-125">Requirements</span></span>  
 <span data-ttu-id="8185f-126">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="8185f-126">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="8185f-127">**標頭：** Corhdr.h。h</span><span class="sxs-lookup"><span data-stu-id="8185f-127">**Header:** CorHdr.h</span></span>  
  
 <span data-ttu-id="8185f-128">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="8185f-128">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8185f-129">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8185f-129">See also</span></span>

- [<span data-ttu-id="8185f-130">中繼資料列舉</span><span class="sxs-lookup"><span data-stu-id="8185f-130">Metadata Enumerations</span></span>](metadata-enumerations.md)
