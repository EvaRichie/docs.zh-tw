---
title: CorDebugNGenPolicy 列舉
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- CorDebugNGenPolicy
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugNGenPolicy
helpviewer_keywords:
- CorDebugNgenPolicy enumeration [.NET Framework debugging]
ms.assetid: edb4e4d2-3166-44d4-8b17-bf302f7ea093
topic_type:
- apiref
ms.openlocfilehash: b64de0fa2ecbddd2decf69a4099d9897ec42a563
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95696423"
---
# <a name="cordebugngenpolicy-enumeration"></a><span data-ttu-id="3a0d2-102">CorDebugNGenPolicy 列舉</span><span class="sxs-lookup"><span data-stu-id="3a0d2-102">CorDebugNGenPolicy Enumeration</span></span>

<span data-ttu-id="3a0d2-103">提供用來判定偵錯工具是否從原生影像快取載入原生 (NGen) 影像的值。</span><span class="sxs-lookup"><span data-stu-id="3a0d2-103">Provides a value that determines whether a debugger loads native (NGen) images from the native image cache.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="3a0d2-104">語法</span><span class="sxs-lookup"><span data-stu-id="3a0d2-104">Syntax</span></span>  
  
```cpp
enum CorDebugNGENPolicy {  
    DISABLE_LOCAL_NIC = 1  
} CorDebugNGENPolicy;  
```  
  
## <a name="members"></a><span data-ttu-id="3a0d2-105">成員</span><span class="sxs-lookup"><span data-stu-id="3a0d2-105">Members</span></span>  
  
|<span data-ttu-id="3a0d2-106">成員名稱</span><span class="sxs-lookup"><span data-stu-id="3a0d2-106">Member name</span></span>|<span data-ttu-id="3a0d2-107">描述</span><span class="sxs-lookup"><span data-stu-id="3a0d2-107">Description</span></span>|  
|-----------------|-----------------|  
|`DISABLE_LOCAL_NIC`|<span data-ttu-id="3a0d2-108">在 Windows 8. x 存放區應用程式中，會停用本機原生映射快取中的映射。</span><span class="sxs-lookup"><span data-stu-id="3a0d2-108">In a Windows 8.x Store app, the use of images from the local native image cache is disabled.</span></span> <span data-ttu-id="3a0d2-109">在桌面應用程式中，此設定沒有任何作用。</span><span class="sxs-lookup"><span data-stu-id="3a0d2-109">In a desktop app, this setting has no effect.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="3a0d2-110">備註</span><span class="sxs-lookup"><span data-stu-id="3a0d2-110">Remarks</span></span>  

 <span data-ttu-id="3a0d2-111">`CorDebugNGENPolicy` [ICorDebugProcess5：： EnableNGENPolicy](icordebugprocess5-enablengenpolicy-method.md)方法會使用列舉。</span><span class="sxs-lookup"><span data-stu-id="3a0d2-111">The `CorDebugNGENPolicy` enumeration is used by the [ICorDebugProcess5::EnableNGENPolicy](icordebugprocess5-enablengenpolicy-method.md) method.</span></span> <span data-ttu-id="3a0d2-112">停用本機原生映射快取中的映射使用，可確保偵錯工具載入可調試的 JIT 編譯影像，而不是優化的原生映射，以提供一致的偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="3a0d2-112">Disabling the use of images from the local native image cache provides for a consistent debugging experience by ensuring that the debugger loads debuggable JIT-compiled images instead of optimized native images.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="3a0d2-113">需求</span><span class="sxs-lookup"><span data-stu-id="3a0d2-113">Requirements</span></span>  

 <span data-ttu-id="3a0d2-114">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="3a0d2-114">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="3a0d2-115">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="3a0d2-115">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="3a0d2-116">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="3a0d2-116">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="3a0d2-117">**.NET Framework 版本：**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="3a0d2-117">**.NET Framework Versions:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3a0d2-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3a0d2-118">See also</span></span>

- [<span data-ttu-id="3a0d2-119">偵錯列舉</span><span class="sxs-lookup"><span data-stu-id="3a0d2-119">Debugging Enumerations</span></span>](debugging-enumerations.md)
