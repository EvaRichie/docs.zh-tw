---
title: _EFN_StackTrace 函式
ms.date: 03/30/2017
api_name:
- _EFN_StackTrace
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- _EFN_StackTrace
helpviewer_keywords:
- _EFN_StackTrace function [.NET Framework debugging]
ms.assetid: caea7754-867c-4360-a65c-5ced4408fd9d
topic_type:
- apiref
ms.openlocfilehash: a725aa2c0f1fdea523bbf7cba880bc805f855782
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2020
ms.locfileid: "82860742"
---
# <a name="_efn_stacktrace-function"></a><span data-ttu-id="10f89-102">\_EFN\_StackTrace 函式</span><span class="sxs-lookup"><span data-stu-id="10f89-102">\_EFN\_StackTrace Function</span></span>
<span data-ttu-id="10f89-103">提供 Managed 堆疊追蹤以及 `CONTEXT` 記錄之陣列的文字表示，再各提供一個文字表示給 Unmanaged 和 Managed 程式碼之間的每個轉換。</span><span class="sxs-lookup"><span data-stu-id="10f89-103">Provides a text representation of a managed stack trace and an array of `CONTEXT` records, one for each transition between unmanaged and managed code.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="10f89-104">語法</span><span class="sxs-lookup"><span data-stu-id="10f89-104">Syntax</span></span>  
  
```cpp  
HRESULT CALLBACK _EFN_StackTrace(  
    [in]  PDEBUG_CLIENT  Client,  
    [out] WCHAR          wszTextOut[],  
    [out] size_t         *puiTextLength,  
    [out] LPVOID         pTransitionContexts,  
    [out] size_t         *puiTransitionContextCount,  
    [in]  size_t         uiSizeOfContext,  
    [in]  DWORD          Flags  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="10f89-105">參數</span><span class="sxs-lookup"><span data-stu-id="10f89-105">Parameters</span></span>  
 `Client`  
 <span data-ttu-id="10f89-106">在正在進行調試的用戶端。</span><span class="sxs-lookup"><span data-stu-id="10f89-106">[in] The client being debugged.</span></span>  
  
 `wszTextOut`  
 <span data-ttu-id="10f89-107">脫銷堆疊追蹤的文字表示。</span><span class="sxs-lookup"><span data-stu-id="10f89-107">[out] The text representation of the stack trace.</span></span>  
  
 `puiTextLength`  
 <span data-ttu-id="10f89-108">脫銷中`wszTextOut`的字元數指標。</span><span class="sxs-lookup"><span data-stu-id="10f89-108">[out] A pointer to the number of characters in `wszTextOut`.</span></span>  
  
 `pTransitionContexts`  
 <span data-ttu-id="10f89-109">脫銷轉換內容的陣列。</span><span class="sxs-lookup"><span data-stu-id="10f89-109">[out] The array of transition contexts.</span></span>  
  
 `puiTransitionContextCount`  
 <span data-ttu-id="10f89-110">脫銷陣列中轉換內容數目的指標。</span><span class="sxs-lookup"><span data-stu-id="10f89-110">[out] A pointer to the number of transition contexts in the array.</span></span>  
  
 `uiSizeOfContext`  
 <span data-ttu-id="10f89-111">在內容結構的大小。</span><span class="sxs-lookup"><span data-stu-id="10f89-111">[in] The size of the context structure.</span></span>  
  
 `Flags`  
 <span data-ttu-id="10f89-112">在設定為0或 SOS_STACKTRACE_SHOWADDRESSES （0x01）以顯示 EBP 暫存器，以及每`module!functionname`一行前面的輸入堆疊指標（ESP）。</span><span class="sxs-lookup"><span data-stu-id="10f89-112">[in] Set to either 0 or SOS_STACKTRACE_SHOWADDRESSES (0x01) to show the EBP register and the enter stack pointer (ESP) in front of each `module!functionname` line.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="10f89-113">備註</span><span class="sxs-lookup"><span data-stu-id="10f89-113">Remarks</span></span>  
 <span data-ttu-id="10f89-114">您`_EFN_StackTrace`可以從 WinDbg 程式設計介面呼叫結構。</span><span class="sxs-lookup"><span data-stu-id="10f89-114">The `_EFN_StackTrace` structure can be called from a WinDbg programmatic interface.</span></span> <span data-ttu-id="10f89-115">參數的使用方式如下：</span><span class="sxs-lookup"><span data-stu-id="10f89-115">Parameters are used as follows:</span></span>  
  
- <span data-ttu-id="10f89-116">如果`wszTextOut`為 null 且`puiTextLength`不是 null，則函式會傳回中`puiTextLength`的字串長度。</span><span class="sxs-lookup"><span data-stu-id="10f89-116">If `wszTextOut` is null and `puiTextLength` is not null, the function returns the string length in `puiTextLength`.</span></span>  
  
- <span data-ttu-id="10f89-117">如果`wszTextOut`不是 null，函式會將文字`wszTextOut`儲存在所指定的位置`puiTextLength`。</span><span class="sxs-lookup"><span data-stu-id="10f89-117">If `wszTextOut` is not null, the function stores text in `wszTextOut` up to the location indicated by `puiTextLength`.</span></span> <span data-ttu-id="10f89-118">如果緩衝區中有足夠的空間，它會傳回成功，如果緩衝區不夠長，則會傳回 E_OUTOFMEMORY。</span><span class="sxs-lookup"><span data-stu-id="10f89-118">It returns successfully if there was enough room in the buffer, or returns E_OUTOFMEMORY if the buffer was not long enough.</span></span>  
  
- <span data-ttu-id="10f89-119">如果`pTransitionContexts`和`puiTransitionContextCount`都是 null，則會忽略函數的轉換部分。</span><span class="sxs-lookup"><span data-stu-id="10f89-119">The transition portion of the function is ignored if `pTransitionContexts` and `puiTransitionContextCount` are both null.</span></span> <span data-ttu-id="10f89-120">在此情況下，函式會為呼叫端提供只有函數名稱的文字輸出。</span><span class="sxs-lookup"><span data-stu-id="10f89-120">In this case, the function provides callers with text output of only the function names.</span></span>  
  
- <span data-ttu-id="10f89-121">如果`pTransitionContexts`為 null 且`puiTransitionContextCount`不是 null，則函式會傳回中`puiTransitionContextCount`所需的內容專案數目。</span><span class="sxs-lookup"><span data-stu-id="10f89-121">If `pTransitionContexts` is null and `puiTransitionContextCount` is not null, the function returns the necessary number of context entries in `puiTransitionContextCount`.</span></span>  
  
- <span data-ttu-id="10f89-122">如果`pTransitionContexts`不是 null，函式會將它視為長度`puiTransitionContextCount`的結構陣列。</span><span class="sxs-lookup"><span data-stu-id="10f89-122">If `pTransitionContexts` is not null, the function treats it as an array of structures of length `puiTransitionContextCount`.</span></span> <span data-ttu-id="10f89-123">結構大小是由`uiSizeOfContext`所提供，而且必須是[SimpleCoNtext](stacktrace-simplecontext-structure.md)或`CONTEXT`架構的大小。</span><span class="sxs-lookup"><span data-stu-id="10f89-123">The structure size is given by `uiSizeOfContext`, and must be the size of [SimpleContext](stacktrace-simplecontext-structure.md) or `CONTEXT` for the architecture.</span></span>  
  
- <span data-ttu-id="10f89-124">`wszTextOut`會以下列格式寫入：</span><span class="sxs-lookup"><span data-stu-id="10f89-124">`wszTextOut` is written in the following format:</span></span>  
  
    ```output  
    "<ModuleName>!<Function Name>[+<offset in hex>]  
    ...  
    (TRANSITION)  
    ..."  
    ```  
  
- <span data-ttu-id="10f89-125">如果 hex 中的位移是0x0，則不會寫入位移。</span><span class="sxs-lookup"><span data-stu-id="10f89-125">If the offset in hex is 0x0, no offset is written.</span></span>  
  
- <span data-ttu-id="10f89-126">如果目前在內容中的執行緒上沒有 managed 程式碼，此函數會傳回 SOS_E_NOMANAGEDCODE。</span><span class="sxs-lookup"><span data-stu-id="10f89-126">If there is no managed code on the thread currently in context, the function returns SOS_E_NOMANAGEDCODE.</span></span>  
  
- <span data-ttu-id="10f89-127">`Flags`參數為0或 SOS_STACKTRACE_SHOWADDRESSES，以查看每`module!functionname`一行前面的 EBP 和 ESP。</span><span class="sxs-lookup"><span data-stu-id="10f89-127">The `Flags` parameter is either 0 or SOS_STACKTRACE_SHOWADDRESSES to see EBP and ESP in front of each `module!functionname` line.</span></span> <span data-ttu-id="10f89-128">根據預設，它是0。</span><span class="sxs-lookup"><span data-stu-id="10f89-128">By default, it is 0.</span></span>  
  
    ```cpp  
    #define SOS_STACKTRACE_SHOWADDRESSES   0x00000001  
    ```  
  
## <a name="requirements"></a><span data-ttu-id="10f89-129">需求</span><span class="sxs-lookup"><span data-stu-id="10f89-129">Requirements</span></span>  
 <span data-ttu-id="10f89-130">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="10f89-130">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="10f89-131">**標頭：** SOS_Stacktrace。h</span><span class="sxs-lookup"><span data-stu-id="10f89-131">**Header:** SOS_Stacktrace.h</span></span>  
  
 <span data-ttu-id="10f89-132">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="10f89-132">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="10f89-133">請參閱</span><span class="sxs-lookup"><span data-stu-id="10f89-133">See also</span></span>

- [<span data-ttu-id="10f89-134">偵錯全域靜態函式</span><span class="sxs-lookup"><span data-stu-id="10f89-134">Debugging Global Static Functions</span></span>](debugging-global-static-functions.md)
