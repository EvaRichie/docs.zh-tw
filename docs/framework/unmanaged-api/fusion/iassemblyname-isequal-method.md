---
title: IAssemblyName::IsEqual 方法
ms.date: 03/30/2017
api_name:
- IAssemblyName.IsEqual
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IAssemblyName::IsEqual
helpviewer_keywords:
- IsEqual method [.NET Framework fusion]
- IAssemblyName::IsEqual method [.NET Framework fusion]
ms.assetid: 6dfc220f-d0d4-45b3-bfce-5829f817766f
topic_type:
- apiref
ms.openlocfilehash: 0fabf8159c2626d4e1716e3be60baaf1ec834032
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95712972"
---
# <a name="iassemblynameisequal-method"></a><span data-ttu-id="119f5-102">IAssemblyName::IsEqual 方法</span><span class="sxs-lookup"><span data-stu-id="119f5-102">IAssemblyName::IsEqual Method</span></span>

<span data-ttu-id="119f5-103">[IAssemblyName](iassemblyname-interface.md) `IAssemblyName` 根據指定的比較旗標，判斷指定的 IAssemblyName 物件是否等於這個。</span><span class="sxs-lookup"><span data-stu-id="119f5-103">Determines whether a specified [IAssemblyName](iassemblyname-interface.md) object is equal to this `IAssemblyName`, based on the specified comparison flags.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="119f5-104">語法</span><span class="sxs-lookup"><span data-stu-id="119f5-104">Syntax</span></span>  
  
```cpp  
HRESULT IsEqual (  
    [in] IAssemblyName  *pName,  
    [in] DWORD          dwCmpFlags  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="119f5-105">參數</span><span class="sxs-lookup"><span data-stu-id="119f5-105">Parameters</span></span>  

 `pName`  
 <span data-ttu-id="119f5-106">在要與 `IAssemblyName` 這個比較的物件 `IAssemblyName` 。</span><span class="sxs-lookup"><span data-stu-id="119f5-106">[in] The `IAssemblyName` object to which to compare this `IAssemblyName`.</span></span>  
  
 `dwCmpFlags`  
 <span data-ttu-id="119f5-107">在 [ASM_CMP_FLAGS](asm-cmp-flags-enumeration.md) 值的位元組合，這些值會影響比較。</span><span class="sxs-lookup"><span data-stu-id="119f5-107">[in] A bitwise combination of [ASM_CMP_FLAGS](asm-cmp-flags-enumeration.md) values that influence the comparison.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="119f5-108">需求</span><span class="sxs-lookup"><span data-stu-id="119f5-108">Requirements</span></span>  

 <span data-ttu-id="119f5-109">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="119f5-109">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="119f5-110">**標頭：** 融合。h</span><span class="sxs-lookup"><span data-stu-id="119f5-110">**Header:** Fusion.h</span></span>  
  
 <span data-ttu-id="119f5-111">**.Net Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="119f5-111">**NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="119f5-112">另請參閱</span><span class="sxs-lookup"><span data-stu-id="119f5-112">See also</span></span>

- [<span data-ttu-id="119f5-113">IAssemblyName 介面</span><span class="sxs-lookup"><span data-stu-id="119f5-113">IAssemblyName Interface</span></span>](iassemblyname-interface.md)
- [<span data-ttu-id="119f5-114">融合列舉</span><span class="sxs-lookup"><span data-stu-id="119f5-114">Fusion Enumerations</span></span>](fusion-enumerations.md)
