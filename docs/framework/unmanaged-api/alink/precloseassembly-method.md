---
title: PreCloseAssembly 方法
ms.date: 03/30/2017
api_name:
- IALink.PreCloseAssembly
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- PreCloseAssembly
helpviewer_keywords:
- PreCloseAssembly method
ms.assetid: 6d23ac54-15ea-4027-a172-9ebef43e8f56
topic_type:
- apiref
ms.openlocfilehash: 31c0c5e23d1a985c2005693e25ca91379037482a
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95728676"
---
# <a name="precloseassembly-method"></a><span data-ttu-id="fe0cf-102">PreCloseAssembly 方法</span><span class="sxs-lookup"><span data-stu-id="fe0cf-102">PreCloseAssembly Method</span></span>

<span data-ttu-id="fe0cf-103">關閉元件檔案。</span><span class="sxs-lookup"><span data-stu-id="fe0cf-103">Closes the assembly file.</span></span> <span data-ttu-id="fe0cf-104">請在關閉所有其他檔案之後，但在關閉元件檔之前，呼叫這個方法。</span><span class="sxs-lookup"><span data-stu-id="fe0cf-104">Call this method after closing all other files, but before closing the assembly file.</span></span> <span data-ttu-id="fe0cf-105">請勿針對未系結的模組呼叫這個方法。</span><span class="sxs-lookup"><span data-stu-id="fe0cf-105">Do not call this method for unbound modules.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="fe0cf-106">語法</span><span class="sxs-lookup"><span data-stu-id="fe0cf-106">Syntax</span></span>  
  
```cpp  
HRESULT PreCloseAssembly(  
    mdAssembly AssemblyID  
) PURE;  
```  
  
## <a name="parameters"></a><span data-ttu-id="fe0cf-107">參數</span><span class="sxs-lookup"><span data-stu-id="fe0cf-107">Parameters</span></span>  

 `AssemblyID`  
 <span data-ttu-id="fe0cf-108">元件的識別碼。</span><span class="sxs-lookup"><span data-stu-id="fe0cf-108">ID of the assembly.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="fe0cf-109">傳回值</span><span class="sxs-lookup"><span data-stu-id="fe0cf-109">Return Value</span></span>  

 <span data-ttu-id="fe0cf-110">如果方法成功，則傳回 S_OK。</span><span class="sxs-lookup"><span data-stu-id="fe0cf-110">Returns S_OK if the method succeeds.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="fe0cf-111">需求</span><span class="sxs-lookup"><span data-stu-id="fe0cf-111">Requirements</span></span>  

 <span data-ttu-id="fe0cf-112">需要 alink. h。</span><span class="sxs-lookup"><span data-stu-id="fe0cf-112">Requires alink.h.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="fe0cf-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fe0cf-113">See also</span></span>

- [<span data-ttu-id="fe0cf-114">IALink 介面</span><span class="sxs-lookup"><span data-stu-id="fe0cf-114">IALink Interface</span></span>](ialink-interface.md)
- [<span data-ttu-id="fe0cf-115">IALink2 介面</span><span class="sxs-lookup"><span data-stu-id="fe0cf-115">IALink2 Interface</span></span>](ialink2-interface.md)
- [<span data-ttu-id="fe0cf-116">ALink API</span><span class="sxs-lookup"><span data-stu-id="fe0cf-116">ALink API</span></span>](index.md)
