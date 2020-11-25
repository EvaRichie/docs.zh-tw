---
title: StrongNameHashSize 函式
ms.date: 03/30/2017
api_name:
- StrongNameHashSize
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- StrongNameHashSize
helpviewer_keywords:
- StrongNameHashSize function [.NET Framework strong naming]
ms.assetid: 738c98d7-a60c-45fe-a296-220af05e6991
topic_type:
- apiref
ms.openlocfilehash: 1116fcde754f966a783f4fdca85df8bd3ca1b0ba
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95724425"
---
# <a name="strongnamehashsize-function"></a><span data-ttu-id="4dac1-102">StrongNameHashSize 函式</span><span class="sxs-lookup"><span data-stu-id="4dac1-102">StrongNameHashSize Function</span></span>

<span data-ttu-id="4dac1-103">使用指定的雜湊演算法取得雜湊所需的緩衝區大小。</span><span class="sxs-lookup"><span data-stu-id="4dac1-103">Gets the buffer size required for a hash, using the specified hash algorithm.</span></span>  
  
 <span data-ttu-id="4dac1-104">此函數已被取代。</span><span class="sxs-lookup"><span data-stu-id="4dac1-104">This function has been deprecated.</span></span> <span data-ttu-id="4dac1-105">請改用 [ICLRStrongName：： StrongNameHashSize](../hosting/iclrstrongname-strongnamehashsize-method.md) 方法。</span><span class="sxs-lookup"><span data-stu-id="4dac1-105">Use the [ICLRStrongName::StrongNameHashSize](../hosting/iclrstrongname-strongnamehashsize-method.md) method instead.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="4dac1-106">語法</span><span class="sxs-lookup"><span data-stu-id="4dac1-106">Syntax</span></span>  
  
```cpp  
BOOLEAN StrongNameHashSize (  
    [in]  ULONG   ulHashAlg,  
    [out] DWORD   *pcbSize  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="4dac1-107">參數</span><span class="sxs-lookup"><span data-stu-id="4dac1-107">Parameters</span></span>  

 `ulHashAlg`  
 <span data-ttu-id="4dac1-108">在用來計算緩衝區大小的雜湊演算法。</span><span class="sxs-lookup"><span data-stu-id="4dac1-108">[in] The hash algorithm used to compute the buffer size.</span></span>  
  
 `pcbSize`  
 <span data-ttu-id="4dac1-109">擴展傳回的緩衝區大小（以位元組為單位）。</span><span class="sxs-lookup"><span data-stu-id="4dac1-109">[out] The returned buffer size, in bytes.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="4dac1-110">傳回值</span><span class="sxs-lookup"><span data-stu-id="4dac1-110">Return Value</span></span>  

 <span data-ttu-id="4dac1-111">`true` 成功完成時;否則為 `false` 。</span><span class="sxs-lookup"><span data-stu-id="4dac1-111">`true` on successful completion; otherwise, `false`.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="4dac1-112">備註</span><span class="sxs-lookup"><span data-stu-id="4dac1-112">Remarks</span></span>  

 <span data-ttu-id="4dac1-113">如果函式 `StrongNameHashSize` 未順利完成，請呼叫 [StrongNameErrorInfo](strongnameerrorinfo-function.md) 函式來取出最後產生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="4dac1-113">If the `StrongNameHashSize` function does not complete successfully, call the [StrongNameErrorInfo](strongnameerrorinfo-function.md) function to retrieve the last generated error.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="4dac1-114">需求</span><span class="sxs-lookup"><span data-stu-id="4dac1-114">Requirements</span></span>  

 <span data-ttu-id="4dac1-115">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="4dac1-115">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="4dac1-116">**標頭：** Stackexchange.redis.strongname。h</span><span class="sxs-lookup"><span data-stu-id="4dac1-116">**Header:** StrongName.h</span></span>  
  
 <span data-ttu-id="4dac1-117">連結 **庫：** 以資源的形式包含在 MsCorEE.dll 中</span><span class="sxs-lookup"><span data-stu-id="4dac1-117">**Library:** Included as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="4dac1-118">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="4dac1-118">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="4dac1-119">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4dac1-119">See also</span></span>

- [<span data-ttu-id="4dac1-120">StrongNameHashSize 方法</span><span class="sxs-lookup"><span data-stu-id="4dac1-120">StrongNameHashSize Method</span></span>](../hosting/iclrstrongname-strongnamehashsize-method.md)
- [<span data-ttu-id="4dac1-121">ICLRStrongName 介面</span><span class="sxs-lookup"><span data-stu-id="4dac1-121">ICLRStrongName Interface</span></span>](../hosting/iclrstrongname-interface.md)
