---
title: ICLRRuntimeInfo::GetVersionString 方法
ms.date: 03/30/2017
api_name:
- ICLRRuntimeInfo.GetVersionString
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeInfo::GetVersionString
helpviewer_keywords:
- ICLRRuntimeInfo::GetVersionString method [.NET Framework hosting]
- GetVersionString method, ICLRRuntimeInfo interface [.NET Framework hosting]
ms.assetid: 98b097ef-2276-4dd9-8551-b03c972e8179
topic_type:
- apiref
ms.openlocfilehash: ccf48b6aea25bd602b55727c2e5958811702f6bf
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/21/2020
ms.locfileid: "83762574"
---
# <a name="iclrruntimeinfogetversionstring-method"></a><span data-ttu-id="44f98-102">ICLRRuntimeInfo::GetVersionString 方法</span><span class="sxs-lookup"><span data-stu-id="44f98-102">ICLRRuntimeInfo::GetVersionString Method</span></span>
<span data-ttu-id="44f98-103">取得與指定的[ICLRRuntimeInfo](iclrruntimeinfo-interface.md)介面相關聯的 common language RUNTIME （CLR）版本資訊。</span><span class="sxs-lookup"><span data-stu-id="44f98-103">Gets common language runtime (CLR) version information associated with a given [ICLRRuntimeInfo](iclrruntimeinfo-interface.md) interface.</span></span>  
  
 <span data-ttu-id="44f98-104">這個方法會取代下列函數：</span><span class="sxs-lookup"><span data-stu-id="44f98-104">This method supersedes the following functions:</span></span>  
  
- [<span data-ttu-id="44f98-105">GetRequestedRuntimeInfo</span><span class="sxs-lookup"><span data-stu-id="44f98-105">GetRequestedRuntimeInfo</span></span>](getrequestedruntimeinfo-function.md)  
  
- [<span data-ttu-id="44f98-106">GetRequestedRuntimeVersion</span><span class="sxs-lookup"><span data-stu-id="44f98-106">GetRequestedRuntimeVersion</span></span>](getrequestedruntimeversion-function.md)  
  
## <a name="syntax"></a><span data-ttu-id="44f98-107">語法</span><span class="sxs-lookup"><span data-stu-id="44f98-107">Syntax</span></span>  
  
```cpp  
HRESULT GetVersionString(  
    [out, size_is(*pcchBuffer)] LPWSTR pwzBuffer,  
    [in, out]  DWORD *pcchBuffer);  
```  
  
## <a name="parameters"></a><span data-ttu-id="44f98-108">參數</span><span class="sxs-lookup"><span data-stu-id="44f98-108">Parameters</span></span>  
 `pwzBuffer`  
 <span data-ttu-id="44f98-109">脫銷.NET Framework 的編譯版本，格式為 "v*A*。*B*[。*X*] "。</span><span class="sxs-lookup"><span data-stu-id="44f98-109">[out] The .NET Framework compilation version in the format "v*A*.*B*[.*X*]".</span></span> <span data-ttu-id="44f98-110">*A*、 *B*和*X*是對應至主要版本、次要版本和組建編號的十進位數。</span><span class="sxs-lookup"><span data-stu-id="44f98-110">*A*, *B*, and *X* are decimal numbers that correspond to the major version, the minor version, and the build number.</span></span> <span data-ttu-id="44f98-111">*X*是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="44f98-111">*X* is optional.</span></span> <span data-ttu-id="44f98-112">如果*X*不存在，則沒有尾端句點。</span><span class="sxs-lookup"><span data-stu-id="44f98-112">If *X* is not present, there is no trailing period.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="44f98-113">這個參數必須符合 .NET Framework 版本的目錄名稱，因為它出現在 C:\Windows\Microsoft.NET\Framework。</span><span class="sxs-lookup"><span data-stu-id="44f98-113">This parameter must match the directory name for the .NET Framework version, as it appears under C:\Windows\Microsoft.NET\Framework.</span></span>  
  
 <span data-ttu-id="44f98-114">範例值為 "v v1.0.3705"、"v 1.1.4322"、"v 2.0.50727" 和 "v4.0"。*x*"，其中*x*取決於安裝的組建編號。</span><span class="sxs-lookup"><span data-stu-id="44f98-114">Example values are "v1.0.3705", "v1.1.4322", "v2.0.50727", and "v4.0.*x*", where *x* depends on the build number installed.</span></span> <span data-ttu-id="44f98-115">請注意，"v" 前置詞是強制的。</span><span class="sxs-lookup"><span data-stu-id="44f98-115">Note that the "v" prefix is mandatory.</span></span>  
  
 `pchBuffer`  
 <span data-ttu-id="44f98-116">[in、out]指定的大小 `pwzBuffer` ，以避免緩衝區溢位。</span><span class="sxs-lookup"><span data-stu-id="44f98-116">[in, out] Specifies the size of `pwzBuffer` to avoid buffer overruns.</span></span> <span data-ttu-id="44f98-117">如果 `pwzBuffer` 為，則會傳回 `null` `pchBuffer` 所需的大小 `pwzBuffer` 以允許預先配置。</span><span class="sxs-lookup"><span data-stu-id="44f98-117">If `pwzBuffer` is `null`, `pchBuffer` returns the required size of `pwzBuffer` to allow preallocation.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="44f98-118">傳回值</span><span class="sxs-lookup"><span data-stu-id="44f98-118">Return Value</span></span>  
 <span data-ttu-id="44f98-119">這個方法會傳回下列特定的 HRESULT，以及表示方法失敗的 HRESULT 錯誤。</span><span class="sxs-lookup"><span data-stu-id="44f98-119">This method returns the following specific HRESULTs as well as HRESULT errors that indicate method failure.</span></span>  
  
|<span data-ttu-id="44f98-120">HRESULT</span><span class="sxs-lookup"><span data-stu-id="44f98-120">HRESULT</span></span>|<span data-ttu-id="44f98-121">Description</span><span class="sxs-lookup"><span data-stu-id="44f98-121">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="44f98-122">S_OK</span><span class="sxs-lookup"><span data-stu-id="44f98-122">S_OK</span></span>|<span data-ttu-id="44f98-123">已成功完成命令。</span><span class="sxs-lookup"><span data-stu-id="44f98-123">The method completed successfully.</span></span>|  
|<span data-ttu-id="44f98-124">E_POINTER</span><span class="sxs-lookup"><span data-stu-id="44f98-124">E_POINTER</span></span>|<span data-ttu-id="44f98-125">`pwzBuffer` 或 `pchBuffer` 為 null。</span><span class="sxs-lookup"><span data-stu-id="44f98-125">`pwzBuffer` or `pchBuffer` is null.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="44f98-126">規格需求</span><span class="sxs-lookup"><span data-stu-id="44f98-126">Requirements</span></span>  
 <span data-ttu-id="44f98-127">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="44f98-127">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="44f98-128">**標頭：** MetaHost。h</span><span class="sxs-lookup"><span data-stu-id="44f98-128">**Header:** MetaHost.h</span></span>  
  
 <span data-ttu-id="44f98-129">連結**庫：** 包含為 Mscoree.dll 中的資源</span><span class="sxs-lookup"><span data-stu-id="44f98-129">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="44f98-130">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="44f98-130">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="44f98-131">另請參閱</span><span class="sxs-lookup"><span data-stu-id="44f98-131">See also</span></span>

- [<span data-ttu-id="44f98-132">ICLRRuntimeInfo 介面</span><span class="sxs-lookup"><span data-stu-id="44f98-132">ICLRRuntimeInfo Interface</span></span>](iclrruntimeinfo-interface.md)
- [<span data-ttu-id="44f98-133">裝載介面</span><span class="sxs-lookup"><span data-stu-id="44f98-133">Hosting Interfaces</span></span>](hosting-interfaces.md)
- [<span data-ttu-id="44f98-134">.NET Framework 4 和 4.5 中新增的 CLR 裝載介面</span><span class="sxs-lookup"><span data-stu-id="44f98-134">CLR Hosting Interfaces Added in the .NET Framework 4 and 4.5</span></span>](clr-hosting-interfaces-added-in-the-net-framework-4-and-4-5.md)
- [<span data-ttu-id="44f98-135">裝載</span><span class="sxs-lookup"><span data-stu-id="44f98-135">Hosting</span></span>](index.md)
