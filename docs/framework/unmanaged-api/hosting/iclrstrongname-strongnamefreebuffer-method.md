---
title: ICLRStrongName::StrongNameFreeBuffer 方法
ms.date: 03/30/2017
api_name:
- ICLRStrongName.StrongNameFreeBuffer
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameFreeBuffer
helpviewer_keywords:
- StrongNameFreeBuffer method, ICLRStrongName interface [.NET Framework hosting]
- ICLRStrongName::StrongNameFreeBuffer method [.NET Framework hosting]
ms.assetid: 6148c508-bd1d-4a37-85c3-06ecb09cc857
topic_type:
- apiref
ms.openlocfilehash: 7aed3e6877bfcd83754d462cdba81ccc229d002f
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504000"
---
# <a name="iclrstrongnamestrongnamefreebuffer-method"></a><span data-ttu-id="32784-102">ICLRStrongName::StrongNameFreeBuffer 方法</span><span class="sxs-lookup"><span data-stu-id="32784-102">ICLRStrongName::StrongNameFreeBuffer Method</span></span>
<span data-ttu-id="32784-103">釋放先前呼叫強式名稱方法所配置的記憶體，例如[ICLRStrongName：： StrongNameGetPublicKey](iclrstrongname-strongnamegetpublickey-method.md)、 [ICLRStrongName：： StrongNameTokenFromPublicKey](iclrstrongname-strongnametokenfrompublickey-method.md)或[ICLRStrongName：： StrongNameSignatureGeneration](iclrstrongname-strongnamesignaturegeneration-method.md)。</span><span class="sxs-lookup"><span data-stu-id="32784-103">Frees memory that was allocated with a previous call to a strong name method such as [ICLRStrongName::StrongNameGetPublicKey](iclrstrongname-strongnamegetpublickey-method.md), [ICLRStrongName::StrongNameTokenFromPublicKey](iclrstrongname-strongnametokenfrompublickey-method.md), or [ICLRStrongName::StrongNameSignatureGeneration](iclrstrongname-strongnamesignaturegeneration-method.md).</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="32784-104">語法</span><span class="sxs-lookup"><span data-stu-id="32784-104">Syntax</span></span>  
  
```cpp  
HRESULT StrongNameFreeBuffer (
   [in] BYTE   *pbMemory  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="32784-105">參數</span><span class="sxs-lookup"><span data-stu-id="32784-105">Parameters</span></span>  
 `pbMemory`  
 <span data-ttu-id="32784-106">在要釋放之記憶體的指標。</span><span class="sxs-lookup"><span data-stu-id="32784-106">[in] A pointer to the memory to free.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="32784-107">傳回值</span><span class="sxs-lookup"><span data-stu-id="32784-107">Return Value</span></span>  
 <span data-ttu-id="32784-108">`S_OK`如果方法已成功完成，則為，否則，就是表示失敗的 HRESULT 值（請參閱清單的[一般 HRESULT 值](/windows/win32/seccrypto/common-hresult-values)）。</span><span class="sxs-lookup"><span data-stu-id="32784-108">`S_OK` if the method completed successfully; otherwise, an HRESULT value that indicates failure (see [Common HRESULT Values](/windows/win32/seccrypto/common-hresult-values) for a list).</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="32784-109">規格需求</span><span class="sxs-lookup"><span data-stu-id="32784-109">Requirements</span></span>  
 <span data-ttu-id="32784-110">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="32784-110">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="32784-111">**標頭：** MetaHost。h</span><span class="sxs-lookup"><span data-stu-id="32784-111">**Header:** MetaHost.h</span></span>  
  
 <span data-ttu-id="32784-112">連結**庫：** 包含為 Mscoree.dll 中的資源</span><span class="sxs-lookup"><span data-stu-id="32784-112">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="32784-113">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="32784-113">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="32784-114">另請參閱</span><span class="sxs-lookup"><span data-stu-id="32784-114">See also</span></span>

- [<span data-ttu-id="32784-115">ICLRStrongName 介面</span><span class="sxs-lookup"><span data-stu-id="32784-115">ICLRStrongName Interface</span></span>](iclrstrongname-interface.md)
