---
title: IMetaDataImport2::GetVersionString 方法
ms.date: 03/30/2017
api_name:
- IMetaDataImport2.GetVersionString
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport2::GetVersionString
helpviewer_keywords:
- GetVersionString method, IMetaDataImport2 interface [.NET Framework metadata]
- IMetaDataImport2::GetVersionString method [.NET Framework metadata]
ms.assetid: 308183ee-fd44-4432-9d86-ef00d181b49b
topic_type:
- apiref
ms.openlocfilehash: 84cf5ac9eab5749d3bdc63670fe5c31bfb62abcd
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84490400"
---
# <a name="imetadataimport2getversionstring-method"></a><span data-ttu-id="e91da-102">IMetaDataImport2::GetVersionString 方法</span><span class="sxs-lookup"><span data-stu-id="e91da-102">IMetaDataImport2::GetVersionString Method</span></span>
<span data-ttu-id="e91da-103">取得用來建立元件之執行時間的版本號碼。</span><span class="sxs-lookup"><span data-stu-id="e91da-103">Gets the version number of the runtime that was used to build the assembly.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="e91da-104">語法</span><span class="sxs-lookup"><span data-stu-id="e91da-104">Syntax</span></span>  
  
```cpp  
HRESULT GetVersionString (  
   [out] LPWSTR      pwzBuf,  
   [in]  DWORD       ccBufSize,  
   [out] DWORD       *pccBufSize  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="e91da-105">參數</span><span class="sxs-lookup"><span data-stu-id="e91da-105">Parameters</span></span>  
 `pwzBuf`  
 <span data-ttu-id="e91da-106">脫銷陣列，用來儲存指定版本的字串。</span><span class="sxs-lookup"><span data-stu-id="e91da-106">[out] An array to store the string that specifies the version.</span></span>  
  
 `ccBufSize`  
 <span data-ttu-id="e91da-107">在陣列的大小（以寬字元為單位） `pwzBuf` 。</span><span class="sxs-lookup"><span data-stu-id="e91da-107">[in] The size, in wide characters, of the `pwzBuf` array.</span></span>  
  
 `pccBufSize`  
 <span data-ttu-id="e91da-108">脫銷陣列中傳回的寬字元數，包括 null 結束字元 `pwzBuf` 。</span><span class="sxs-lookup"><span data-stu-id="e91da-108">[out] The number of wide characters, including a null terminator, returned in the `pwzBuf` array.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="e91da-109">備註</span><span class="sxs-lookup"><span data-stu-id="e91da-109">Remarks</span></span>  
 <span data-ttu-id="e91da-110">`GetVersionString`方法會取得目前中繼資料範圍的內建版本。</span><span class="sxs-lookup"><span data-stu-id="e91da-110">The `GetVersionString` method gets the built-for version of the current metadata scope.</span></span> <span data-ttu-id="e91da-111">如果從未儲存過範圍，它就不會有內建的版本，而且會傳回空字串。</span><span class="sxs-lookup"><span data-stu-id="e91da-111">If the scope has never been saved, it will not have a built-for version, and an empty string will be returned.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="e91da-112">規格需求</span><span class="sxs-lookup"><span data-stu-id="e91da-112">Requirements</span></span>  
 <span data-ttu-id="e91da-113">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="e91da-113">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="e91da-114">**標頭：** Cor。h</span><span class="sxs-lookup"><span data-stu-id="e91da-114">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="e91da-115">連結**庫：** 做為 Mscoree.dll 中的資源使用</span><span class="sxs-lookup"><span data-stu-id="e91da-115">**Library:** Used as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="e91da-116">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="e91da-116">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e91da-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e91da-117">See also</span></span>

- [<span data-ttu-id="e91da-118">IMetaDataImport2 介面</span><span class="sxs-lookup"><span data-stu-id="e91da-118">IMetaDataImport2 Interface</span></span>](imetadataimport2-interface.md)
- [<span data-ttu-id="e91da-119">IMetaDataImport 介面</span><span class="sxs-lookup"><span data-stu-id="e91da-119">IMetaDataImport Interface</span></span>](imetadataimport-interface.md)
