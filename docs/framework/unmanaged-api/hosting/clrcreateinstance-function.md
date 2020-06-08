---
title: CLRCreateInstance 函式
ms.date: 03/30/2017
api_name:
- CLRCreateInstance
api_location:
- mscoree.dll
- mscoreei.dll
api_type:
- COM
f1_keywords:
- CLRCreateInstance
helpviewer_keywords:
- CLRCreateInstance function [.NET Framework hosting]
ms.assetid: 5de13327-96c6-4697-a89e-b8bf40717855
topic_type:
- apiref
ms.openlocfilehash: 4aeacc718632c133550ed8de6649716c5d8b7423
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504438"
---
# <a name="clrcreateinstance-function"></a><span data-ttu-id="2faaf-102">CLRCreateInstance 函式</span><span class="sxs-lookup"><span data-stu-id="2faaf-102">CLRCreateInstance Function</span></span>
<span data-ttu-id="2faaf-103">提供三種介面的其中一個： [ICLRMetaHost](iclrmetahost-interface.md)、 [ICLRMetaHostPolicy](iclrmetahostpolicy-interface.md)或[ICLRDebugging](../debugging/iclrdebugging-interface.md)。</span><span class="sxs-lookup"><span data-stu-id="2faaf-103">Provides one of three interfaces: [ICLRMetaHost](iclrmetahost-interface.md), [ICLRMetaHostPolicy](iclrmetahostpolicy-interface.md), or [ICLRDebugging](../debugging/iclrdebugging-interface.md).</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="2faaf-104">語法</span><span class="sxs-lookup"><span data-stu-id="2faaf-104">Syntax</span></span>  
  
```cpp  
HRESULT CLRCreateInstance(  
    [in]  REFCLSID  clsid,  
    [in]  REFIID     riid,  
    [out] LPVOID  * ppInterface  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="2faaf-105">參數</span><span class="sxs-lookup"><span data-stu-id="2faaf-105">Parameters</span></span>  
 `clsid`  
 <span data-ttu-id="2faaf-106">在三個類別識別碼的其中一個： CLSID_CLRMetaHost、CLSID_CLRMetaHostPolicy 或 CLSID_CLRDebugging。</span><span class="sxs-lookup"><span data-stu-id="2faaf-106">[in] One of three class identifiers: CLSID_CLRMetaHost, CLSID_CLRMetaHostPolicy, or CLSID_CLRDebugging.</span></span>  
  
 `riid`  
 <span data-ttu-id="2faaf-107">在三個介面識別碼（Iid）中的其中一個： IID_ICLRMetaHost、IID_ICLRMetaHostPolicy 或 IID_ICLRDebugging。</span><span class="sxs-lookup"><span data-stu-id="2faaf-107">[in] One of three interface identifiers (IIDs): IID_ICLRMetaHost, IID_ICLRMetaHostPolicy, or IID_ICLRDebugging.</span></span>  
  
 `ppInterface`  
 <span data-ttu-id="2faaf-108">脫銷三個介面的其中一個： [ICLRMetaHost](iclrmetahost-interface.md)、 [ICLRMetaHostPolicy](iclrmetahostpolicy-interface.md)或[ICLRDebugging](../debugging/iclrdebugging-interface.md)。</span><span class="sxs-lookup"><span data-stu-id="2faaf-108">[out] One of three interfaces: [ICLRMetaHost](iclrmetahost-interface.md), [ICLRMetaHostPolicy](iclrmetahostpolicy-interface.md), or [ICLRDebugging](../debugging/iclrdebugging-interface.md).</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="2faaf-109">傳回值</span><span class="sxs-lookup"><span data-stu-id="2faaf-109">Return Value</span></span>  
 <span data-ttu-id="2faaf-110">這個方法會傳回下列特定的 HRESULT，以及表示方法失敗的 HRESULT 錯誤。</span><span class="sxs-lookup"><span data-stu-id="2faaf-110">This method returns the following specific HRESULTs as well as HRESULT errors that indicate method failure.</span></span>  
  
|<span data-ttu-id="2faaf-111">HRESULT</span><span class="sxs-lookup"><span data-stu-id="2faaf-111">HRESULT</span></span>|<span data-ttu-id="2faaf-112">說明</span><span class="sxs-lookup"><span data-stu-id="2faaf-112">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="2faaf-113">S_OK</span><span class="sxs-lookup"><span data-stu-id="2faaf-113">S_OK</span></span>|<span data-ttu-id="2faaf-114">已成功完成命令。</span><span class="sxs-lookup"><span data-stu-id="2faaf-114">The method completed successfully.</span></span>|  
|<span data-ttu-id="2faaf-115">E_POINTER</span><span class="sxs-lookup"><span data-stu-id="2faaf-115">E_POINTER</span></span>|<span data-ttu-id="2faaf-116">`ppInterface` 為 null。</span><span class="sxs-lookup"><span data-stu-id="2faaf-116">`ppInterface` is null.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="2faaf-117">備註</span><span class="sxs-lookup"><span data-stu-id="2faaf-117">Remarks</span></span>  
 <span data-ttu-id="2faaf-118">下表顯示和支援的組合 `clsid` `riid` 。</span><span class="sxs-lookup"><span data-stu-id="2faaf-118">The following table shows the supported combinations for `clsid` and `riid`.</span></span>  
  
|`clsid`|`riid`|  
|--------------|------------|  
|<span data-ttu-id="2faaf-119">CLSID_CLRMetaHost</span><span class="sxs-lookup"><span data-stu-id="2faaf-119">CLSID_CLRMetaHost</span></span>|<span data-ttu-id="2faaf-120">IID_ICLRMetaHost</span><span class="sxs-lookup"><span data-stu-id="2faaf-120">IID_ICLRMetaHost</span></span>|  
|<span data-ttu-id="2faaf-121">CLSID_CLRMetaHostPolicy</span><span class="sxs-lookup"><span data-stu-id="2faaf-121">CLSID_CLRMetaHostPolicy</span></span>|<span data-ttu-id="2faaf-122">IID_ICLRMetaHostPolicy</span><span class="sxs-lookup"><span data-stu-id="2faaf-122">IID_ICLRMetaHostPolicy</span></span>|  
|<span data-ttu-id="2faaf-123">CLSID_CLRDebugging</span><span class="sxs-lookup"><span data-stu-id="2faaf-123">CLSID_CLRDebugging</span></span>|<span data-ttu-id="2faaf-124">IID_ICLRDebugging</span><span class="sxs-lookup"><span data-stu-id="2faaf-124">IID_ICLRDebugging</span></span>|  
  
 <span data-ttu-id="2faaf-125">下列程式碼示範如何使用 `CLRCreateInstance` 來取得全部三個介面：</span><span class="sxs-lookup"><span data-stu-id="2faaf-125">The following code shows how to use `CLRCreateInstance` to get all three interfaces:</span></span>  
  
```cpp  
#include <metahost.h>  
#pragma comment(lib, "mscoree.lib")  
  
ICLRMetaHost       *pMetaHost       = NULL;  
ICLRMetaHostPolicy *pMetaHostPolicy = NULL;  
ICLRDebugging      *pCLRDebugging   = NULL;  
HRESULT hr;  
hr = CLRCreateInstance(CLSID_CLRMetaHost, IID_ICLRMetaHost,  
                    (LPVOID*)&pMetaHost);  
hr = CLRCreateInstance (CLSID_CLRMetaHostPolicy, IID_ICLRMetaHostPolicy,  
                    (LPVOID*)&pMetaHostPolicy);  
hr = CLRCreateInstance (CLSID_CLRDebugging, IID_ICLRDebugging,  
                    (LPVOID*)&pCLRDebugging);  
```  
  
## <a name="requirements"></a><span data-ttu-id="2faaf-126">規格需求</span><span class="sxs-lookup"><span data-stu-id="2faaf-126">Requirements</span></span>  
 <span data-ttu-id="2faaf-127">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="2faaf-127">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="2faaf-128">**標頭：** MetaHost。h</span><span class="sxs-lookup"><span data-stu-id="2faaf-128">**Header:** MetaHost.h</span></span>  
  
 <span data-ttu-id="2faaf-129">連結**庫：** 包含為 Mscoree.dll 中的資源</span><span class="sxs-lookup"><span data-stu-id="2faaf-129">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="2faaf-130">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="2faaf-130">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="2faaf-131">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2faaf-131">See also</span></span>

- [<span data-ttu-id="2faaf-132">Hosting</span><span class="sxs-lookup"><span data-stu-id="2faaf-132">Hosting</span></span>](index.md)
