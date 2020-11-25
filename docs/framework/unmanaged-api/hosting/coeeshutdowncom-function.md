---
title: CoEEShutDownCOM 函式
ms.date: 03/30/2017
api_name:
- CoEEShutDownCOM
api_location:
- mscoree.dll
- clr.dll
- mscorwks.dll
- mscoreei.dll
- mscorsvr.dll
api_type:
- DLLExport
f1_keywords:
- CoEEShutDownCOM
helpviewer_keywords:
- CoEEShutDownCOM function [.NET Framework hosting]
ms.assetid: b634cae2-632f-4737-9be4-92d0652844d7
topic_type:
- apiref
ms.openlocfilehash: 774704698f92d546d6bafa61c65d18d083c65f89
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95716755"
---
# <a name="coeeshutdowncom-function"></a><span data-ttu-id="2f961-102">CoEEShutDownCOM 函式</span><span class="sxs-lookup"><span data-stu-id="2f961-102">CoEEShutDownCOM Function</span></span>

<span data-ttu-id="2f961-103">強制 common language runtime (CLR) 釋放它在執行時間可呼叫包裝函式中的所有介面指標 (RCW) 。</span><span class="sxs-lookup"><span data-stu-id="2f961-103">Forces the common language runtime (CLR) to release all interface pointers it holds inside runtime callable wrappers (RCW).</span></span> <span data-ttu-id="2f961-104">這有釋放所有 RCW 快取的效果。</span><span class="sxs-lookup"><span data-stu-id="2f961-104">This has the effect of releasing all RCW caches.</span></span> <span data-ttu-id="2f961-105">此全域函式已在 .NET Framework 4 中淘汰。</span><span class="sxs-lookup"><span data-stu-id="2f961-105">This global function is deprecated in the .NET Framework 4.</span></span> <span data-ttu-id="2f961-106">相反地，請使用特定執行時間的進入點。</span><span class="sxs-lookup"><span data-stu-id="2f961-106">Instead, use the entry point for a specific runtime.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="2f961-107">語法</span><span class="sxs-lookup"><span data-stu-id="2f961-107">Syntax</span></span>  
  
```cpp  
void CoEEShutDownCOM ();  
```  
  
## <a name="remarks"></a><span data-ttu-id="2f961-108">備註</span><span class="sxs-lookup"><span data-stu-id="2f961-108">Remarks</span></span>  

 <span data-ttu-id="2f961-109">此函式會 `CoEEShutDownCOM` 先釋出所有內容和所有快取中的所有 rcw，然後移除安裝程式中現有的任何終止通知。</span><span class="sxs-lookup"><span data-stu-id="2f961-109">The `CoEEShutDownCOM` function first releases all the RCWs in all contexts and in all caches, and then removes any tear-down notification existing in setup.</span></span> <span data-ttu-id="2f961-110">不會卸載任何 DLL。</span><span class="sxs-lookup"><span data-stu-id="2f961-110">No DLL unloading occurs.</span></span>  
  
> [!CAUTION]
> <span data-ttu-id="2f961-111">此函式會影響載入至進程的所有執行時間。</span><span class="sxs-lookup"><span data-stu-id="2f961-111">This function affects all runtimes that are loaded into the process.</span></span>  
  
 <span data-ttu-id="2f961-112">從 .NET Framework 4 開始，請在您想要影響的特定執行時間上，呼叫此函式的進入點。</span><span class="sxs-lookup"><span data-stu-id="2f961-112">Beginning with the .NET Framework 4, call the entry point for this function on the specific runtime you want to affect.</span></span> <span data-ttu-id="2f961-113">若要取得進入點，請呼叫 [ICLRRuntimeInfo：： GetProcAddress](iclrruntimeinfo-getprocaddress-method.md) 方法，並指定 "CoEEShutDownCOM"。</span><span class="sxs-lookup"><span data-stu-id="2f961-113">To get the entry point, call the [ICLRRuntimeInfo::GetProcAddress](iclrruntimeinfo-getprocaddress-method.md) method and specify "CoEEShutDownCOM".</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="2f961-114">需求</span><span class="sxs-lookup"><span data-stu-id="2f961-114">Requirements</span></span>  

 <span data-ttu-id="2f961-115">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="2f961-115">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="2f961-116">**標頭：** Cor。h</span><span class="sxs-lookup"><span data-stu-id="2f961-116">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="2f961-117">連結 **庫：** 以資源的形式包含在 MsCorEE.dll 中</span><span class="sxs-lookup"><span data-stu-id="2f961-117">**Library:** Included as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="2f961-118">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="2f961-118">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="2f961-119">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2f961-119">See also</span></span>

- [<span data-ttu-id="2f961-120">中繼資料全域靜態函式</span><span class="sxs-lookup"><span data-stu-id="2f961-120">Metadata Global Static Functions</span></span>](../metadata/metadata-global-static-functions.md)
