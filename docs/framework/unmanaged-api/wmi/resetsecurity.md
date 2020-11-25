---
title: 'ResetSecurity 函式 (非受控 API 參考) '
description: ResetSecurity 函式會將模擬 token 指派給目前的執行緒。
ms.date: 11/06/2017
api_name:
- ResetSecurity
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- ResetSecurity
helpviewer_keywords:
- ResetSecurity function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 259bef74356f16221f1453dd4086e2fbb26faa83
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95721110"
---
# <a name="resetsecurity-function"></a><span data-ttu-id="3d1f2-103">ResetSecurity 函式</span><span class="sxs-lookup"><span data-stu-id="3d1f2-103">ResetSecurity function</span></span>

<span data-ttu-id="3d1f2-104">將提供的模擬權杖指派給目前的執行緒。</span><span class="sxs-lookup"><span data-stu-id="3d1f2-104">Assigns the supplied impersonation token to the current thread.</span></span>
  
[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a><span data-ttu-id="3d1f2-105">語法</span><span class="sxs-lookup"><span data-stu-id="3d1f2-105">Syntax</span></span>  
  
```cpp  
HRESULT ResetSecurity (
   [in] HANDLE token
);
```  

## <a name="parameters"></a><span data-ttu-id="3d1f2-106">參數</span><span class="sxs-lookup"><span data-stu-id="3d1f2-106">Parameters</span></span>

`token`  
<span data-ttu-id="3d1f2-107">在要與目前線程相關聯的模擬權杖。</span><span class="sxs-lookup"><span data-stu-id="3d1f2-107">[in] The impersonation token to associate with the current thread.</span></span> <span data-ttu-id="3d1f2-108">其值可以是 `null`。</span><span class="sxs-lookup"><span data-stu-id="3d1f2-108">Its value can be `null`.</span></span>

## <a name="return-value"></a><span data-ttu-id="3d1f2-109">傳回值</span><span class="sxs-lookup"><span data-stu-id="3d1f2-109">Return value</span></span>

<span data-ttu-id="3d1f2-110">如果函式成功，則傳回值為 `S_OK` (0) 。</span><span class="sxs-lookup"><span data-stu-id="3d1f2-110">If the function succeeds, the return value is `S_OK` (0).</span></span>

<span data-ttu-id="3d1f2-111">如果函式失敗，則傳回值為非零的錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="3d1f2-111">If the function fails, the return value is a non-zero error code.</span></span> <span data-ttu-id="3d1f2-112">若要取得延伸錯誤資訊，請呼叫 [GetErrorInfo](geterrorinfo.md) 函數。</span><span class="sxs-lookup"><span data-stu-id="3d1f2-112">To get extended error information, call the [GetErrorInfo](geterrorinfo.md) function.</span></span>
  
## <a name="requirements"></a><span data-ttu-id="3d1f2-113">需求</span><span class="sxs-lookup"><span data-stu-id="3d1f2-113">Requirements</span></span>  

 <span data-ttu-id="3d1f2-114">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="3d1f2-114">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="3d1f2-115">**標頭：** WMINet_Utils .idl</span><span class="sxs-lookup"><span data-stu-id="3d1f2-115">**Header:** WMINet_Utils.idl</span></span>  
  
 <span data-ttu-id="3d1f2-116">**.NET Framework 版本：**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]</span><span class="sxs-lookup"><span data-stu-id="3d1f2-116">**.NET Framework Versions:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3d1f2-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3d1f2-117">See also</span></span>

- [<span data-ttu-id="3d1f2-118">WMI 與效能計數器 (非受控 API 參考)</span><span class="sxs-lookup"><span data-stu-id="3d1f2-118">WMI and Performance Counters (Unmanaged API Reference)</span></span>](index.md)
