---
title: ICLRStrongName::GetHashFromFileW 方法
ms.date: 03/30/2017
api_name:
- ICLRStrongName.GetHashFromFileW
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::GetHashFromFileW
helpviewer_keywords:
- GetHashFromFileW method, ICLRStrongName interface [.NET Framework hosting]
- ICLRStrongName::GetHashFromFileW method [.NET Framework hosting]
ms.assetid: c6ff45fc-905d-4c6e-b00c-97c6c7c55d99
topic_type:
- apiref
ms.openlocfilehash: eda78976f175230cc2405b9cb151993e63697e48
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95685756"
---
# <a name="iclrstrongnamegethashfromfilew-method"></a><span data-ttu-id="2d879-102">ICLRStrongName::GetHashFromFileW 方法</span><span class="sxs-lookup"><span data-stu-id="2d879-102">ICLRStrongName::GetHashFromFileW Method</span></span>

<span data-ttu-id="2d879-103">產生以 Unicode 字串指定之檔案內容的雜湊。</span><span class="sxs-lookup"><span data-stu-id="2d879-103">Generates a hash over the contents of the file specified by a Unicode string.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="2d879-104">語法</span><span class="sxs-lookup"><span data-stu-id="2d879-104">Syntax</span></span>  
  
```cpp  
HRESULT GetHashFromFileW (
    [in]  LPCWSTR   wszFilePath,  
    [in, out] unsigned int   *piHashAlg,  
    [out] BYTE      *pbHash,  
    [in]  DWORD     cchHash,  
    [out] DWORD     *pchHash  
);
```  
  
## <a name="parameters"></a><span data-ttu-id="2d879-105">參數</span><span class="sxs-lookup"><span data-stu-id="2d879-105">Parameters</span></span>  

 `wszFilePath`  
 <span data-ttu-id="2d879-106">在要雜湊之檔案的 Unicode 名稱。</span><span class="sxs-lookup"><span data-stu-id="2d879-106">[in] The Unicode name of the file to hash.</span></span>  
  
 `piHashAlg`  
 <span data-ttu-id="2d879-107">[in，out]產生雜湊時要使用的演算法。</span><span class="sxs-lookup"><span data-stu-id="2d879-107">[in, out] The algorithm to use when generating the hash.</span></span> <span data-ttu-id="2d879-108">有效的演算法是由 Win32 CryptoAPI 定義的演算法。</span><span class="sxs-lookup"><span data-stu-id="2d879-108">Valid algorithms are those defined by the Win32 CryptoAPI.</span></span> <span data-ttu-id="2d879-109">如果 `piHashAlg` 設定為0，則會使用預設的演算法 CALG_SHA-1。</span><span class="sxs-lookup"><span data-stu-id="2d879-109">If `piHashAlg` is set to 0, the default algorithm CALG_SHA-1 is used.</span></span>  
  
 `pbHash`  
 <span data-ttu-id="2d879-110">擴展位元組陣列，其中包含產生的雜湊。</span><span class="sxs-lookup"><span data-stu-id="2d879-110">[out] A byte array containing the generated hash.</span></span>  
  
 `cchHash`  
 <span data-ttu-id="2d879-111">在所指向之緩衝區的大小上限 `pbHash` 。</span><span class="sxs-lookup"><span data-stu-id="2d879-111">[in] The maximum size of the buffer pointed to by `pbHash`.</span></span>  
  
 `pchHash`  
 <span data-ttu-id="2d879-112">擴展的大小（以位元組為單位） `pbHash` 。</span><span class="sxs-lookup"><span data-stu-id="2d879-112">[out] The size, in bytes, of `pbHash`.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="2d879-113">傳回值</span><span class="sxs-lookup"><span data-stu-id="2d879-113">Return Value</span></span>  

 <span data-ttu-id="2d879-114">`S_OK` 如果方法成功完成，則為，否則，表示失敗 (的 HRESULT 值會看到清單) 的 [一般 HRESULT 值](/windows/win32/seccrypto/common-hresult-values) 。</span><span class="sxs-lookup"><span data-stu-id="2d879-114">`S_OK` if the method completed successfully; otherwise, an HRESULT value that indicates failure (see [Common HRESULT Values](/windows/win32/seccrypto/common-hresult-values) for a list).</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="2d879-115">備註</span><span class="sxs-lookup"><span data-stu-id="2d879-115">Remarks</span></span>  

 <span data-ttu-id="2d879-116">此方法與 [ICLRStrongName：： GetHashFromFile](iclrstrongname-gethashfromfile-method.md) 方法相同，不同之處在于檔案名規格是 Unicode 而非 ANSI。</span><span class="sxs-lookup"><span data-stu-id="2d879-116">This method is the same as the [ICLRStrongName::GetHashFromFile](iclrstrongname-gethashfromfile-method.md) method, except that the file name specification is Unicode instead of ANSI.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="2d879-117">需求</span><span class="sxs-lookup"><span data-stu-id="2d879-117">Requirements</span></span>  

 <span data-ttu-id="2d879-118">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="2d879-118">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="2d879-119">**標頭：** MetaHost。h</span><span class="sxs-lookup"><span data-stu-id="2d879-119">**Header:** MetaHost.h</span></span>  
  
 <span data-ttu-id="2d879-120">連結 **庫：** 以資源的形式包含在 MSCorEE.dll 中</span><span class="sxs-lookup"><span data-stu-id="2d879-120">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="2d879-121">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="2d879-121">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="2d879-122">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2d879-122">See also</span></span>

- [<span data-ttu-id="2d879-123">GetHashFromFile 方法</span><span class="sxs-lookup"><span data-stu-id="2d879-123">GetHashFromFile Method</span></span>](iclrstrongname-gethashfromfile-method.md)
- [<span data-ttu-id="2d879-124">ICLRStrongName 介面</span><span class="sxs-lookup"><span data-stu-id="2d879-124">ICLRStrongName Interface</span></span>](iclrstrongname-interface.md)
