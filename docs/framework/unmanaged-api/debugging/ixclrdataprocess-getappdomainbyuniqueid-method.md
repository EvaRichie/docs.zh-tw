---
title: IXCLRDataProcess：： GetAppDomainByUniqueId 方法
ms.date: 01/16/2019
api.name:
- IXCLRDataProcess::GetAppDomainByUniqueId Method
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- IXCLRDataProcess::GetAppDomainByUniqueId Method
helpviewer.keywords:
- IXCLRDataProcess::GetAppDomainByUniqueId Method [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: bb02ffed09cbcc31e653bfd3165050c247908c5d
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83420776"
---
# <a name="ixclrdataprocessgetappdomainbyuniqueid-method"></a><span data-ttu-id="6bc6c-102">IXCLRDataProcess：： GetAppDomainByUniqueId 方法</span><span class="sxs-lookup"><span data-stu-id="6bc6c-102">IXCLRDataProcess::GetAppDomainByUniqueId Method</span></span>

<span data-ttu-id="6bc6c-103">根據程式的 `AppDomain` 唯一識別碼，在進程中取得。</span><span class="sxs-lookup"><span data-stu-id="6bc6c-103">Gets an `AppDomain` in a process based on its unique identifier.</span></span>

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a><span data-ttu-id="6bc6c-104">語法</span><span class="sxs-lookup"><span data-stu-id="6bc6c-104">Syntax</span></span>

```cpp
HRESULT GetAppDomainByUniqueID(
    [in] ULONG64               id,
    [out] IXCLRDataAppDomain **appDomain
);
```

## <a name="parameters"></a><span data-ttu-id="6bc6c-105">參數</span><span class="sxs-lookup"><span data-stu-id="6bc6c-105">Parameters</span></span>

`id`\
<span data-ttu-id="6bc6c-106">在AppDomain 的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="6bc6c-106">[in] The unique identifier of the AppDomain</span></span>

`appDomain`\
<span data-ttu-id="6bc6c-107">脫銷AppDomain</span><span class="sxs-lookup"><span data-stu-id="6bc6c-107">[out] The AppDomain</span></span>

## <a name="remarks"></a><span data-ttu-id="6bc6c-108">備註</span><span class="sxs-lookup"><span data-stu-id="6bc6c-108">Remarks</span></span>

<span data-ttu-id="6bc6c-109">提供的方法是介面的一部分 `IXCLRDataProcess` ，而且會對應至虛擬方法資料表的第20個位置。</span><span class="sxs-lookup"><span data-stu-id="6bc6c-109">The provided method is part of the `IXCLRDataProcess` interface and corresponds to the 20th slot of the virtual method table.</span></span> <span data-ttu-id="6bc6c-110">`IXCLRDataAppDomain*`傳回的是用來與其他 api 互動。</span><span class="sxs-lookup"><span data-stu-id="6bc6c-110">The `IXCLRDataAppDomain*` returned is used for interaction with other APIs.</span></span>

## <a name="requirements"></a><span data-ttu-id="6bc6c-111">需求</span><span class="sxs-lookup"><span data-stu-id="6bc6c-111">Requirements</span></span>

<span data-ttu-id="6bc6c-112">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="6bc6c-112">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>
<span data-ttu-id="6bc6c-113">**標頭：** 無**媒體櫃：** 無 **.NET Framework 版本：**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]</span><span class="sxs-lookup"><span data-stu-id="6bc6c-113">**Header:** None **Library:** None **.NET Framework Versions:** [!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]</span></span>

## <a name="see-also"></a><span data-ttu-id="6bc6c-114">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6bc6c-114">See also</span></span>

- [<span data-ttu-id="6bc6c-115">偵錯</span><span class="sxs-lookup"><span data-stu-id="6bc6c-115">Debugging</span></span>](index.md)
- [<span data-ttu-id="6bc6c-116">IXCLRDataProcess 介面</span><span class="sxs-lookup"><span data-stu-id="6bc6c-116">IXCLRDataProcess Interface</span></span>](ixclrdataprocess-interface.md)
