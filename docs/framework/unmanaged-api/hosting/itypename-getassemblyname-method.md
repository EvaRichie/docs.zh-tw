---
title: ITypeName::GetAssemblyName 方法
ms.date: 03/30/2017
api_name:
- ITypeName.GetAssemblyName
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- GetAssemblyName
helpviewer_keywords:
- ITypeName::GetAssemblyName method [.NET Framework hosting]
- GetAssemblyName method [.NET Framework hosting]
ms.assetid: 97801d99-f5f1-4a30-882f-959827093fac
topic_type:
- apiref
ms.openlocfilehash: 256c0ccf7a39992ebb14adfd820729f8351e1990
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95725114"
---
# <a name="itypenamegetassemblyname-method"></a><span data-ttu-id="5d52b-102">ITypeName::GetAssemblyName 方法</span><span class="sxs-lookup"><span data-stu-id="5d52b-102">ITypeName::GetAssemblyName Method</span></span>

<span data-ttu-id="5d52b-103">此方法支援 .NET Framework 結構而且並非設計直接從程式碼使用。</span><span class="sxs-lookup"><span data-stu-id="5d52b-103">This method supports the .NET Framework infrastructure and is not intended to be used directly from your code.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="5d52b-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="5d52b-104">Syntax</span></span>  
  
```cpp  
HRESULT GetAssemblyName (  
    [out, retval] BSTR* rgbszAssemblyNames  
);  
```  
  
## <a name="requirements"></a><span data-ttu-id="5d52b-105">需求</span><span class="sxs-lookup"><span data-stu-id="5d52b-105">Requirements</span></span>  

 <span data-ttu-id="5d52b-106">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="5d52b-106">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="5d52b-107">**標頭：** Mscoree.dll</span><span class="sxs-lookup"><span data-stu-id="5d52b-107">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="5d52b-108">連結 **庫：** 以資源的形式包含在 MSCorEE.dll 中</span><span class="sxs-lookup"><span data-stu-id="5d52b-108">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="5d52b-109">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="5d52b-109">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="5d52b-110">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5d52b-110">See also</span></span>

- [<span data-ttu-id="5d52b-111">裝載介面</span><span class="sxs-lookup"><span data-stu-id="5d52b-111">Hosting Interfaces</span></span>](hosting-interfaces.md)
