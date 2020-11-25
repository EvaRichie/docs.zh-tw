---
title: COR_TYPEID 結構
ms.date: 03/30/2017
api_name:
- COR_TYPEID
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_TYPEID
helpviewer_keywords:
- COR_TYPEID structure [.NET Framework debugging]
ms.assetid: 1e172b14-ee22-4943-b3b8-3740e7bdcd2e
topic_type:
- apiref
ms.openlocfilehash: 5eeb5aef7edaa23385190a309144e1477da741e8
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95697437"
---
# <a name="cor_typeid-structure"></a><span data-ttu-id="e9ec4-102">COR_TYPEID 結構</span><span class="sxs-lookup"><span data-stu-id="e9ec4-102">COR_TYPEID Structure</span></span>

<span data-ttu-id="e9ec4-103">包含類型識別項。</span><span class="sxs-lookup"><span data-stu-id="e9ec4-103">Contains a type identifier.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="e9ec4-104">語法</span><span class="sxs-lookup"><span data-stu-id="e9ec4-104">Syntax</span></span>  
  
```cpp  
typedef struct COR_TYPEID{  
    UINT64 token1;  
    UINT64 token2;  
} COR_TYPEID;  
```  
  
## <a name="members"></a><span data-ttu-id="e9ec4-105">成員</span><span class="sxs-lookup"><span data-stu-id="e9ec4-105">Members</span></span>  
  
|<span data-ttu-id="e9ec4-106">member</span><span class="sxs-lookup"><span data-stu-id="e9ec4-106">Member</span></span>|<span data-ttu-id="e9ec4-107">描述</span><span class="sxs-lookup"><span data-stu-id="e9ec4-107">Description</span></span>|  
|------------|-----------------|  
|`token1`|<span data-ttu-id="e9ec4-108">第一個 token。</span><span class="sxs-lookup"><span data-stu-id="e9ec4-108">The first token.</span></span>|  
|`token2`|<span data-ttu-id="e9ec4-109">第二個 token。</span><span class="sxs-lookup"><span data-stu-id="e9ec4-109">The second token.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="e9ec4-110">備註</span><span class="sxs-lookup"><span data-stu-id="e9ec4-110">Remarks</span></span>  

 <span data-ttu-id="e9ec4-111">此 `COR_TYPEID` 結構是由許多偵錯工具方法所傳回，這些方法提供要進行垃圾收集之物件的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="e9ec4-111">The `COR_TYPEID` structure is returned by a number of debugging methods that provide information about objects to be garbage-collected.</span></span> <span data-ttu-id="e9ec4-112">然後，您可以將它當作引數傳遞給其他的偵錯工具，以提供該專案的其他相關資訊。</span><span class="sxs-lookup"><span data-stu-id="e9ec4-112">It can then be passed as an argument to other debugging methods that provide additional information about that item.</span></span> <span data-ttu-id="e9ec4-113">例如，藉由列舉 [ICorDebugHeapEnum](icordebugheapenum-interface.md) 物件，您可以取得個別 [COR_HEAPOBJECT](cor-heapobject-structure.md) 物件，這些物件代表 managed 堆積上的個別物件。</span><span class="sxs-lookup"><span data-stu-id="e9ec4-113">For example, by enumerating an [ICorDebugHeapEnum](icordebugheapenum-interface.md) object, you can retrieve individual [COR_HEAPOBJECT](cor-heapobject-structure.md) objects that represent individual objects on the managed heap.</span></span> <span data-ttu-id="e9ec4-114">然後，您可以將此 `COR_TYPEID` 值從 `COR_HEAPOBJECT.type` 欄位傳遞到 [ICorDebugProcess5：： GetTypeForTypeID](icordebugprocess5-gettypefortypeid-method.md) 方法，以取得提供物件類型資訊的 ICorDebugType 物件。</span><span class="sxs-lookup"><span data-stu-id="e9ec4-114">You can then pass the `COR_TYPEID` value from the `COR_HEAPOBJECT.type` field to the [ICorDebugProcess5::GetTypeForTypeID](icordebugprocess5-gettypefortypeid-method.md) method to retrieve an ICorDebugType object that provides type information about the object.</span></span>  
  
 <span data-ttu-id="e9ec4-115">物件應為 `COR_TYPEID` 不透明。</span><span class="sxs-lookup"><span data-stu-id="e9ec4-115">A `COR_TYPEID` object is intended to be opaque.</span></span> <span data-ttu-id="e9ec4-116">不應存取或操作其個別欄位。</span><span class="sxs-lookup"><span data-stu-id="e9ec4-116">Its individual fields should not be accessed or manipulated.</span></span> <span data-ttu-id="e9ec4-117">其唯一用途是做為方法呼叫中的參數提供的識別碼， `out` 而且可以傳遞給其他方法以提供其他資訊。</span><span class="sxs-lookup"><span data-stu-id="e9ec4-117">Its sole use is as an identifier that is provided as an `out` parameter in a method call and that can, in turn, be passed to other methods to provide additional information.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="e9ec4-118">需求</span><span class="sxs-lookup"><span data-stu-id="e9ec4-118">Requirements</span></span>  

 <span data-ttu-id="e9ec4-119">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="e9ec4-119">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="e9ec4-120">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="e9ec4-120">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="e9ec4-121">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="e9ec4-121">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="e9ec4-122">**.NET Framework 版本：**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="e9ec4-122">**.NET Framework Versions:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e9ec4-123">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e9ec4-123">See also</span></span>

- [<span data-ttu-id="e9ec4-124">偵錯結構</span><span class="sxs-lookup"><span data-stu-id="e9ec4-124">Debugging Structures</span></span>](debugging-structures.md)
- [<span data-ttu-id="e9ec4-125">偵錯</span><span class="sxs-lookup"><span data-stu-id="e9ec4-125">Debugging</span></span>](index.md)
