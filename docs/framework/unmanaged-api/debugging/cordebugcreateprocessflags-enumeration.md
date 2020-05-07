---
title: CorDebugCreateProcessFlags 列舉
ms.date: 03/30/2017
api_name:
- CorDebugCreateProcessFlags
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugCreateProcessFlags
helpviewer_keywords:
- CorDebugCreateProcessFlags enumeration [.NET Framework debugging]
ms.assetid: e709acce-6a17-4346-b38a-467dba567358
topic_type:
- apiref
ms.openlocfilehash: c0e4c43ac18b5e214d38dd7a57452a3871e4b43d
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82796024"
---
# <a name="cordebugcreateprocessflags-enumeration"></a><span data-ttu-id="d7c40-102">CorDebugCreateProcessFlags 列舉</span><span class="sxs-lookup"><span data-stu-id="d7c40-102">CorDebugCreateProcessFlags Enumeration</span></span>
<span data-ttu-id="d7c40-103">提供可在[ICorDebug：： CreateProcess](icordebug-createprocess-method.md)方法的呼叫中使用的其他偵錯工具選項。</span><span class="sxs-lookup"><span data-stu-id="d7c40-103">Provides additional debugging options that can be used in a call to the [ICorDebug::CreateProcess](icordebug-createprocess-method.md) method.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="d7c40-104">語法</span><span class="sxs-lookup"><span data-stu-id="d7c40-104">Syntax</span></span>  
  
```cpp  
typedef enum CorDebugCreateProcessFlags {  
    DEBUG_NO_SPECIAL_OPTIONS    = 0x0000  
} CorDebugCreateProcessFlags;  
```  
  
## <a name="members"></a><span data-ttu-id="d7c40-105">成員</span><span class="sxs-lookup"><span data-stu-id="d7c40-105">Members</span></span>  
  
|<span data-ttu-id="d7c40-106">member</span><span class="sxs-lookup"><span data-stu-id="d7c40-106">Member</span></span>|<span data-ttu-id="d7c40-107">說明</span><span class="sxs-lookup"><span data-stu-id="d7c40-107">Description</span></span>|  
|------------|-----------------|  
|`DEBUG_NO_SPECIAL_OPTIONS`|<span data-ttu-id="d7c40-108">未設定任何特殊選項。</span><span class="sxs-lookup"><span data-stu-id="d7c40-108">No special options are set.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="d7c40-109">需求</span><span class="sxs-lookup"><span data-stu-id="d7c40-109">Requirements</span></span>  
 <span data-ttu-id="d7c40-110">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="d7c40-110">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="d7c40-111">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="d7c40-111">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="d7c40-112">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="d7c40-112">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="d7c40-113">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="d7c40-113">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d7c40-114">請參閱</span><span class="sxs-lookup"><span data-stu-id="d7c40-114">See also</span></span>

- [<span data-ttu-id="d7c40-115">偵錯列舉</span><span class="sxs-lookup"><span data-stu-id="d7c40-115">Debugging Enumerations</span></span>](debugging-enumerations.md)
