---
title: COR_ACTIVE_FUNCTION 結構
ms.date: 03/30/2017
api_name:
- COR_ACTIVE_FUNCTION
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_ACTIVE_FUNCTION
helpviewer_keywords:
- COR_ACTIVE_FUNCTION structure [.NET Framework debugging]
ms.assetid: ed86185f-2152-459c-961f-10c06d62e83f
topic_type:
- apiref
ms.openlocfilehash: c50ba530d78296ebb956329b2f34b4f1e5cae94c
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95727415"
---
# <a name="cor_active_function-structure"></a><span data-ttu-id="4ffb5-102">COR_ACTIVE_FUNCTION 結構</span><span class="sxs-lookup"><span data-stu-id="4ffb5-102">COR_ACTIVE_FUNCTION Structure</span></span>

<span data-ttu-id="4ffb5-103">包含目前執行緒框架中正在作用的函式相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4ffb5-103">Contains information about the functions that are currently active in a thread's frames.</span></span> <span data-ttu-id="4ffb5-104">此結構是由 [ICorDebugThread2：： GetActiveFunctions](icordebugthread2-getactivefunctions-method.md) 方法所使用。</span><span class="sxs-lookup"><span data-stu-id="4ffb5-104">This structure is used by the [ICorDebugThread2::GetActiveFunctions](icordebugthread2-getactivefunctions-method.md) method.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="4ffb5-105">語法</span><span class="sxs-lookup"><span data-stu-id="4ffb5-105">Syntax</span></span>  
  
```cpp  
typedef struct  _COR_ACTIVE_FUNCTION {  
    ICorDebugAppDomain   *pAppDomain;  
    ICorDebugModule      *pModule;  
    ICorDebugFunction2   *pFunction;  
    ULONG32              ilOffset;  
    ULONG32              flags;  
} COR_ACTIVE_FUNCTION;  
```  
  
## <a name="members"></a><span data-ttu-id="4ffb5-106">成員</span><span class="sxs-lookup"><span data-stu-id="4ffb5-106">Members</span></span>  
  
|<span data-ttu-id="4ffb5-107">member</span><span class="sxs-lookup"><span data-stu-id="4ffb5-107">Member</span></span>|<span data-ttu-id="4ffb5-108">描述</span><span class="sxs-lookup"><span data-stu-id="4ffb5-108">Description</span></span>|  
|------------|-----------------|  
|`pAppDomain`|<span data-ttu-id="4ffb5-109">欄位之應用程式域擁有者的指標 `ilOffset` 。</span><span class="sxs-lookup"><span data-stu-id="4ffb5-109">Pointer to the application domain owner of the `ilOffset` field.</span></span>|  
|`pModule`|<span data-ttu-id="4ffb5-110">欄位之模組擁有者的指標 `ilOffset` 。</span><span class="sxs-lookup"><span data-stu-id="4ffb5-110">Pointer to the module owner of the `ilOffset` field.</span></span>|  
|`pFunction`|<span data-ttu-id="4ffb5-111">欄位之函式擁有者的指標 `ilOffset` 。</span><span class="sxs-lookup"><span data-stu-id="4ffb5-111">Pointer to the function owner of the `ilOffset` field.</span></span>|  
|`ilOffset`|<span data-ttu-id="4ffb5-112">Microsoft 中繼語言 (MSIL) 框架位移。</span><span class="sxs-lookup"><span data-stu-id="4ffb5-112">The Microsoft intermediate language (MSIL) offset of the frame.</span></span>|  
|`flags`|<span data-ttu-id="4ffb5-113">保留供未來擴充性之用。</span><span class="sxs-lookup"><span data-stu-id="4ffb5-113">Reserved for future extensibility.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="4ffb5-114">需求</span><span class="sxs-lookup"><span data-stu-id="4ffb5-114">Requirements</span></span>  

 <span data-ttu-id="4ffb5-115">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="4ffb5-115">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="4ffb5-116">**標頭：** Cordebug.h .idl</span><span class="sxs-lookup"><span data-stu-id="4ffb5-116">**Header:** CorDebug.idl</span></span>  
  
 <span data-ttu-id="4ffb5-117">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="4ffb5-117">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="4ffb5-118">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="4ffb5-118">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="4ffb5-119">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4ffb5-119">See also</span></span>

- [<span data-ttu-id="4ffb5-120">偵錯結構</span><span class="sxs-lookup"><span data-stu-id="4ffb5-120">Debugging Structures</span></span>](debugging-structures.md)
- [<span data-ttu-id="4ffb5-121">偵錯</span><span class="sxs-lookup"><span data-stu-id="4ffb5-121">Debugging</span></span>](index.md)
