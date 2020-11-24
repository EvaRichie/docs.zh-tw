---
title: CreateApplicationContext 函式
ms.date: 03/30/2017
api_name:
- CreateApplicationContext
api_location:
- fusion.dll
api_type:
- DLLExport
f1_keywords:
- CreateApplicationContext
helpviewer_keywords:
- CreateApplicationContext function [.NET Framework fusion]
ms.assetid: 7bf8a141-b2c0-4058-9885-1cef7dcaa811
topic_type:
- apiref
ms.openlocfilehash: 9418be85f5b72bac8eed7f5ea4af4fc42439b01f
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95683223"
---
# <a name="createapplicationcontext-function"></a><span data-ttu-id="3f824-102">CreateApplicationContext 函式</span><span class="sxs-lookup"><span data-stu-id="3f824-102">CreateApplicationContext Function</span></span>

<span data-ttu-id="3f824-103">此函式支援 .NET Framework 基礎結構，而且不適合直接從程式碼使用。</span><span class="sxs-lookup"><span data-stu-id="3f824-103">This function supports the .NET Framework infrastructure and is not intended to be used directly from your code.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="3f824-104">語法</span><span class="sxs-lookup"><span data-stu-id="3f824-104">Syntax</span></span>  
  
```cpp  
HRESULT CreateApplicationContext (  
    [in]  IAssemblyName  *pName,  
    [out] LPPAPPLICATIONCONTEXT  *ppCtx  
 );  
```  
  
## <a name="parameters"></a><span data-ttu-id="3f824-105">參數</span><span class="sxs-lookup"><span data-stu-id="3f824-105">Parameters</span></span>  

 `pName`  
 <span data-ttu-id="3f824-106">在易記名稱的指標。</span><span class="sxs-lookup"><span data-stu-id="3f824-106">[in] A pointer to a friendly name.</span></span>  
  
 `ppCtx`  
 <span data-ttu-id="3f824-107">擴展應用程式內容的指標。</span><span class="sxs-lookup"><span data-stu-id="3f824-107">[out] A pointer to an application context.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="3f824-108">需求</span><span class="sxs-lookup"><span data-stu-id="3f824-108">Requirements</span></span>  

 <span data-ttu-id="3f824-109">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="3f824-109">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="3f824-110">**標頭：** 融合。h</span><span class="sxs-lookup"><span data-stu-id="3f824-110">**Header:** Fusion.h</span></span>  
  
 <span data-ttu-id="3f824-111">連結 **庫：** 以資源的形式包含在 Fusion.dll 中</span><span class="sxs-lookup"><span data-stu-id="3f824-111">**Library:** Included as a resource in Fusion.dll</span></span>  
  
 <span data-ttu-id="3f824-112">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="3f824-112">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3f824-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3f824-113">See also</span></span>

- [<span data-ttu-id="3f824-114">IAssemblyCache 介面</span><span class="sxs-lookup"><span data-stu-id="3f824-114">IAssemblyCache Interface</span></span>](iassemblycache-interface.md)
- [<span data-ttu-id="3f824-115">融合全域靜態函式</span><span class="sxs-lookup"><span data-stu-id="3f824-115">Fusion Global Static Functions</span></span>](fusion-global-static-functions.md)
- [<span data-ttu-id="3f824-116">全域組件快取</span><span class="sxs-lookup"><span data-stu-id="3f824-116">Global Assembly Cache</span></span>](../../app-domains/gac.md)
