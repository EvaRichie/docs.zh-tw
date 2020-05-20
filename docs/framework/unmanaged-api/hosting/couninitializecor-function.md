---
title: CoUninitializeCor 函式
ms.date: 03/30/2017
api_name:
- CoUninitializeCor
api_location:
- mscoree.dll
- mscorsvr.dll
api_type:
- DLLExport
f1_keywords:
- CoUninitializeCor
helpviewer_keywords:
- CoUninitializeCor function [.NET Framework hosting]
ms.assetid: 50a95b8b-9766-470e-bb29-2c7ecddfd4a1
topic_type:
- apiref
ms.openlocfilehash: 8a8c2764398d737192190f91646d45f4edf3a0e4
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83616474"
---
# <a name="couninitializecor-function"></a><span data-ttu-id="98482-102">CoUninitializeCor 函式</span><span class="sxs-lookup"><span data-stu-id="98482-102">CoUninitializeCor Function</span></span>
<span data-ttu-id="98482-103">`CoUninitializeCor` 已經過時。</span><span class="sxs-lookup"><span data-stu-id="98482-103">`CoUninitializeCor` is obsolete.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="98482-104">語法</span><span class="sxs-lookup"><span data-stu-id="98482-104">Syntax</span></span>  
  
```cpp  
STDAPI_(void) CoUninitializeCor(void);  
```  
  
## <a name="remarks"></a><span data-ttu-id="98482-105">備註</span><span class="sxs-lookup"><span data-stu-id="98482-105">Remarks</span></span>  
 <span data-ttu-id="98482-106">無法從進程中卸載通用語言執行時間。</span><span class="sxs-lookup"><span data-stu-id="98482-106">The common language runtime cannot be unloaded from a process.</span></span> <span data-ttu-id="98482-107">若要從執行中的進程完全移除執行時間，您必須關閉該進程。</span><span class="sxs-lookup"><span data-stu-id="98482-107">To completely remove the runtime from a running process, you must shut down that process.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="98482-108">另請參閱</span><span class="sxs-lookup"><span data-stu-id="98482-108">See also</span></span>

- [<span data-ttu-id="98482-109">中繼資料全域靜態函式</span><span class="sxs-lookup"><span data-stu-id="98482-109">Metadata Global Static Functions</span></span>](../metadata/metadata-global-static-functions.md)
