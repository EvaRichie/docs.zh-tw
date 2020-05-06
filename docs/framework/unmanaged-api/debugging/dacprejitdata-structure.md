---
title: DacpReJitData Structure
ms.date: 02/01/2019
api.name:
- DacpReJitData Structure
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- DacpReJitData Structure
helpviewer.keywords:
- DacpReJitData Structure [.NET Framework debugging]
topic_type:
- apiref
author: hoyosjs
ms.author: juhoyosa
ms.openlocfilehash: 4436ece72b0a6a405fc41cba5413093fc42ce750
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2020
ms.locfileid: "82860774"
---
# <a name="dacprejitdata-structure"></a><span data-ttu-id="cd597-102">DacpReJitData Structure</span><span class="sxs-lookup"><span data-stu-id="cd597-102">DacpReJitData Structure</span></span>

<span data-ttu-id="cd597-103">定義指定之分析工具檢測方法的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="cd597-103">Defines the basic information about a given profiler-instrumented method.</span></span>

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a><span data-ttu-id="cd597-104">語法</span><span class="sxs-lookup"><span data-stu-id="cd597-104">Syntax</span></span>

```cpp
struct MSLAYOUT DacpReJitData
{
    enum Flags
    {
        kUnknown,
        kRequested,
        kActive,
        kReverted,
    };

    CLRDATA_ADDRESS                 rejitID;
    Flags                           flags;
    CLRDATA_ADDRESS                 NativeCodeAddr;
};
```

## <a name="members"></a><span data-ttu-id="cd597-105">成員</span><span class="sxs-lookup"><span data-stu-id="cd597-105">Members</span></span>

| <span data-ttu-id="cd597-106">member</span><span class="sxs-lookup"><span data-stu-id="cd597-106">Member</span></span>           | <span data-ttu-id="cd597-107">描述</span><span class="sxs-lookup"><span data-stu-id="cd597-107">Description</span></span>                                                                                      |
| ---------------- | ------------------------------------------------------------------------------------------------ |
| `rejitID`        | <span data-ttu-id="cd597-108">方法的 ReJit 修訂編號。</span><span class="sxs-lookup"><span data-stu-id="cd597-108">The ReJit revision number for a method.</span></span>                                                          |
| `flags`          | <span data-ttu-id="cd597-109">旗標，指出方法的 ReJit 檢測在指定版本中的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="cd597-109">A flag indicating the current state of the method's ReJit instrumentation for the given version.</span></span> |
| `NativeCodeAddr` | <span data-ttu-id="cd597-110">方法的 rejitted 實址的基底位址。</span><span class="sxs-lookup"><span data-stu-id="cd597-110">The base address of the method's rejitted implementation.</span></span>                                         |

## <a name="remarks"></a><span data-ttu-id="cd597-111">備註</span><span class="sxs-lookup"><span data-stu-id="cd597-111">Remarks</span></span>

<span data-ttu-id="cd597-112">這個結構存在於執行時間中，而且不會透過任何標頭或程式庫檔案來公開。</span><span class="sxs-lookup"><span data-stu-id="cd597-112">This structure lives inside the runtime and is not exposed through any headers or library files.</span></span> <span data-ttu-id="cd597-113">若要使用它，請依照上面的指定定義結構。</span><span class="sxs-lookup"><span data-stu-id="cd597-113">To use it, define the structure as specified above.</span></span> <span data-ttu-id="cd597-114">如果未使用 Microsoft 編譯器，則`ms_struct`也必須使用封裝來定義結構。</span><span class="sxs-lookup"><span data-stu-id="cd597-114">The structure must also be defined using `ms_struct` packing if not using the Microsoft compilers.</span></span>

## <a name="requirements"></a><span data-ttu-id="cd597-115">需求</span><span class="sxs-lookup"><span data-stu-id="cd597-115">Requirements</span></span>
<span data-ttu-id="cd597-116">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="cd597-116">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
<span data-ttu-id="cd597-117">**標頭：** 無</span><span class="sxs-lookup"><span data-stu-id="cd597-117">**Header:** None</span></span>  
<span data-ttu-id="cd597-118">連結**庫：** 無</span><span class="sxs-lookup"><span data-stu-id="cd597-118">**Library:** None</span></span>  
<span data-ttu-id="cd597-119">**.NET Framework 版本：**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]</span><span class="sxs-lookup"><span data-stu-id="cd597-119">**.NET Framework Versions:** [!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]</span></span>  

## <a name="see-also"></a><span data-ttu-id="cd597-120">請參閱</span><span class="sxs-lookup"><span data-stu-id="cd597-120">See also</span></span>

- [<span data-ttu-id="cd597-121">偵錯</span><span class="sxs-lookup"><span data-stu-id="cd597-121">Debugging</span></span>](index.md)
- [<span data-ttu-id="cd597-122">偵錯結構</span><span class="sxs-lookup"><span data-stu-id="cd597-122">Debugging Structures</span></span>](debugging-structures.md)
