---
title: ICLRStrongName::StrongNameSignatureSize 方法
ms.date: 03/30/2017
api_name:
- ICLRStrongName.StrongNameSignatureSize
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameSignatureSize
helpviewer_keywords:
- ICLRStrongName::StrongNameSignatureSize method [.NET Framework hosting]
- StrongNameSignatureSize method, ICLRStrongName interface [.NET Framework hosting]
ms.assetid: 76d4f93a-5e25-4399-abcc-a1389549481d
topic_type:
- apiref
ms.openlocfilehash: edce771b3c36f2c56637aa2a21fe524be0ae12c8
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/21/2020
ms.locfileid: "83763016"
---
# <a name="iclrstrongnamestrongnamesignaturesize-method"></a><span data-ttu-id="8f1ce-102">ICLRStrongName::StrongNameSignatureSize 方法</span><span class="sxs-lookup"><span data-stu-id="8f1ce-102">ICLRStrongName::StrongNameSignatureSize Method</span></span>
<span data-ttu-id="8f1ce-103">傳回強式名稱簽章的大小。</span><span class="sxs-lookup"><span data-stu-id="8f1ce-103">Returns the size of the strong name signature.</span></span> <span data-ttu-id="8f1ce-104">編譯器通常會使用這個方法，在建立延遲簽署的元件時，決定要在檔案中保留多少空間。</span><span class="sxs-lookup"><span data-stu-id="8f1ce-104">This method is typically used by compilers to determine how much space to reserve in the file when creating a delay-signed assembly.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="8f1ce-105">語法</span><span class="sxs-lookup"><span data-stu-id="8f1ce-105">Syntax</span></span>  
  
```cpp  
HRESULT StrongNameSignatureSize (
    [in]  BYTE   *pbPublicKeyBlob,  
    [in]  ULONG  cbPublicKeyBlob,
    [in]  DWORD  *pcbSize  
);
```  
  
## <a name="parameters"></a><span data-ttu-id="8f1ce-106">參數</span><span class="sxs-lookup"><span data-stu-id="8f1ce-106">Parameters</span></span>  
 `pbPublicKeyBlob`  
 <span data-ttu-id="8f1ce-107">在[PublicKeyBlob](../strong-naming/publickeyblob-structure.md)類型的結構，其中包含用來產生強式名稱簽章之金鑰組的公開部分。</span><span class="sxs-lookup"><span data-stu-id="8f1ce-107">[in] A structure of type [PublicKeyBlob](../strong-naming/publickeyblob-structure.md) that contains the public portion of the key pair used to generate the strong name signature.</span></span>  
  
 `cbPublicKeyBlob`  
 <span data-ttu-id="8f1ce-108">在的大小（以位元組為單位） `pbPublicKeyBlob` 。</span><span class="sxs-lookup"><span data-stu-id="8f1ce-108">[in] The size, in bytes, of `pbPublicKeyBlob`.</span></span>  
  
 `pcbSize`  
 <span data-ttu-id="8f1ce-109">在儲存強式名稱簽章所需的位元組數目。</span><span class="sxs-lookup"><span data-stu-id="8f1ce-109">[in] The number of bytes required to store the strong name signature.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="8f1ce-110">傳回值</span><span class="sxs-lookup"><span data-stu-id="8f1ce-110">Return Value</span></span>  
 <span data-ttu-id="8f1ce-111">`S_OK`如果方法已成功完成，則為，否則，就是表示失敗的 HRESULT 值（請參閱清單的[一般 HRESULT 值](/windows/win32/seccrypto/common-hresult-values)）。</span><span class="sxs-lookup"><span data-stu-id="8f1ce-111">`S_OK` if the method completed successfully; otherwise, an HRESULT value that indicates failure (see [Common HRESULT Values](/windows/win32/seccrypto/common-hresult-values) for a list).</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="8f1ce-112">規格需求</span><span class="sxs-lookup"><span data-stu-id="8f1ce-112">Requirements</span></span>  
 <span data-ttu-id="8f1ce-113">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="8f1ce-113">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="8f1ce-114">**標頭：** MetaHost。h</span><span class="sxs-lookup"><span data-stu-id="8f1ce-114">**Header:** MetaHost.h</span></span>  
  
 <span data-ttu-id="8f1ce-115">連結**庫：** 包含為 Mscoree.dll 中的資源</span><span class="sxs-lookup"><span data-stu-id="8f1ce-115">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="8f1ce-116">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="8f1ce-116">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8f1ce-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8f1ce-117">See also</span></span>

- [<span data-ttu-id="8f1ce-118">ICLRStrongName 介面</span><span class="sxs-lookup"><span data-stu-id="8f1ce-118">ICLRStrongName Interface</span></span>](iclrstrongname-interface.md)
