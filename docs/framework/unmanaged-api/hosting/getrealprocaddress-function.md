---
title: GetRealProcAddress 函式
ms.date: 03/30/2017
api_name:
- GetRealProcAddress
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- GetRealProcAddress
helpviewer_keywords:
- GetRealProcAddress function [.NET Framework hosting]
ms.assetid: f1f2fab1-400b-488f-95f2-d49c4fca3556
topic_type:
- apiref
ms.openlocfilehash: 6bbf8366054c58543444a4b710a687198f365e6e
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83617187"
---
# <a name="getrealprocaddress-function"></a><span data-ttu-id="c1cd9-102">GetRealProcAddress 函式</span><span class="sxs-lookup"><span data-stu-id="c1cd9-102">GetRealProcAddress Function</span></span>
<span data-ttu-id="c1cd9-103">取得從通用語言執行時間（CLR）最新安裝的版本匯出之指定函式的位址。</span><span class="sxs-lookup"><span data-stu-id="c1cd9-103">Gets the address of the specified function that is exported from the latest installed version of the common language runtime (CLR).</span></span>  
  
 <span data-ttu-id="c1cd9-104">此函式在 .NET Framework 4 中已被取代。</span><span class="sxs-lookup"><span data-stu-id="c1cd9-104">This function has been deprecated in the .NET Framework 4.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="c1cd9-105">語法</span><span class="sxs-lookup"><span data-stu-id="c1cd9-105">Syntax</span></span>  
  
```cpp  
HRESULT GetRealProcAddress (  
    [in]  LPCSTR  pwszProcName,
    [out] VOID  **ppv  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="c1cd9-106">參數</span><span class="sxs-lookup"><span data-stu-id="c1cd9-106">Parameters</span></span>  
 `pwszProcName`  
 <span data-ttu-id="c1cd9-107">在函式的名稱。</span><span class="sxs-lookup"><span data-stu-id="c1cd9-107">[in] The name of the function.</span></span>  
  
 `ppv`  
 <span data-ttu-id="c1cd9-108">脫銷接收函式位址指標的位置。</span><span class="sxs-lookup"><span data-stu-id="c1cd9-108">[out] The location that receives a pointer to the address of the function.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="c1cd9-109">傳回值</span><span class="sxs-lookup"><span data-stu-id="c1cd9-109">Return Value</span></span>  
 <span data-ttu-id="c1cd9-110">這個方法會傳回標準元件物件模型（COM）錯誤碼（如 Winerror.h 中所定義），以及 Corerror.h 中所定義的下列值。</span><span class="sxs-lookup"><span data-stu-id="c1cd9-110">This method returns standard Component Object Model (COM) error codes, as defined in WinError.h, in addition to the following values defined in CorError.h.</span></span>  
  
|<span data-ttu-id="c1cd9-111">傳回碼</span><span class="sxs-lookup"><span data-stu-id="c1cd9-111">Return code</span></span>|<span data-ttu-id="c1cd9-112">說明</span><span class="sxs-lookup"><span data-stu-id="c1cd9-112">Description</span></span>|  
|-----------------|-----------------|  
|<span data-ttu-id="c1cd9-113">S_OK</span><span class="sxs-lookup"><span data-stu-id="c1cd9-113">S_OK</span></span>|<span data-ttu-id="c1cd9-114">已成功完成命令。</span><span class="sxs-lookup"><span data-stu-id="c1cd9-114">The method completed successfully.</span></span>|  
|<span data-ttu-id="c1cd9-115">E_POINTER</span><span class="sxs-lookup"><span data-stu-id="c1cd9-115">E_POINTER</span></span>|<span data-ttu-id="c1cd9-116">`ppv` 無效。</span><span class="sxs-lookup"><span data-stu-id="c1cd9-116">`ppv` is not valid.</span></span>|  
|<span data-ttu-id="c1cd9-117">CLR_E_SHIM_RUNTIMEEXPORT</span><span class="sxs-lookup"><span data-stu-id="c1cd9-117">CLR_E_SHIM_RUNTIMEEXPORT</span></span>|<span data-ttu-id="c1cd9-118">函數不會從執行時間匯出。</span><span class="sxs-lookup"><span data-stu-id="c1cd9-118">The function is not exported from the runtime.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="c1cd9-119">需求</span><span class="sxs-lookup"><span data-stu-id="c1cd9-119">Requirements</span></span>  
 <span data-ttu-id="c1cd9-120">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="c1cd9-120">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="c1cd9-121">**標頭：** Mscoree.dll. h</span><span class="sxs-lookup"><span data-stu-id="c1cd9-121">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="c1cd9-122">連結**庫：** Mscoree.dll .dll</span><span class="sxs-lookup"><span data-stu-id="c1cd9-122">**Library:** MSCorEE.dll</span></span>  
  
 <span data-ttu-id="c1cd9-123">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="c1cd9-123">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c1cd9-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c1cd9-124">See also</span></span>

- [<span data-ttu-id="c1cd9-125">已被取代的 CLR 裝載函式</span><span class="sxs-lookup"><span data-stu-id="c1cd9-125">Deprecated CLR Hosting Functions</span></span>](deprecated-clr-hosting-functions.md)
