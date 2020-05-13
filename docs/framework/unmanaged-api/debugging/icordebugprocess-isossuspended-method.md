---
title: ICorDebugProcess::IsOSSuspended 方法
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.IsOSSuspended
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::IsOSSuspended
helpviewer_keywords:
- IsOSSuspended method [.NET Framework debugging]
- ICorDebugProcess::IsOSSuspended method [.NET Framework debugging]
ms.assetid: 83406cb2-5797-4402-872d-89c9516aefec
topic_type:
- apiref
ms.openlocfilehash: 9452f238bd84c9c185ca8e007acac563474d29df
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212057"
---
# <a name="icordebugprocessisossuspended-method"></a><span data-ttu-id="02744-102">ICorDebugProcess::IsOSSuspended 方法</span><span class="sxs-lookup"><span data-stu-id="02744-102">ICorDebugProcess::IsOSSuspended Method</span></span>
<span data-ttu-id="02744-103">取得值，指出指定的執行緒是否因偵錯工具停止這個進程而暫停。</span><span class="sxs-lookup"><span data-stu-id="02744-103">Gets a value that indicates whether the specified thread has been suspended as a result of the debugger stopping this process.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="02744-104">語法</span><span class="sxs-lookup"><span data-stu-id="02744-104">Syntax</span></span>  
  
```cpp  
HRESULT IsOSSuspended(  
    [in]  DWORD threadID,  
    [out] BOOL  *pbSuspended);  
```  
  
## <a name="parameters"></a><span data-ttu-id="02744-105">參數</span><span class="sxs-lookup"><span data-stu-id="02744-105">Parameters</span></span>  
 `threadID`  
 <span data-ttu-id="02744-106">在有問題的執行緒識別碼。</span><span class="sxs-lookup"><span data-stu-id="02744-106">[in] The ID of thread in question.</span></span>  
  
 `pbSuspended`  
 <span data-ttu-id="02744-107">脫銷布林值的指標，如果指定的執行緒已暫止，則為， `true` 否則 `pbSuspended` 為 \* `false` 。</span><span class="sxs-lookup"><span data-stu-id="02744-107">[out] A pointer to a Boolean value that is `true` if the specified thread has been suspended; otherwise \*`pbSuspended` is `false`.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="02744-108">備註</span><span class="sxs-lookup"><span data-stu-id="02744-108">Remarks</span></span>  
 <span data-ttu-id="02744-109">當指定的執行緒因偵錯工具停止這個進程而暫停時，指定的執行緒 Win32 暫停計數會遞增一。</span><span class="sxs-lookup"><span data-stu-id="02744-109">When the specified thread has been suspended as a result of the debugger stopping this process, the specified thread's Win32 suspend count is incremented by one.</span></span> <span data-ttu-id="02744-110">如果偵錯工具使用者介面（UI）向使用者顯示執行緒的作業系統（OS）暫停計數，可能會想要將這項資訊列入考慮。</span><span class="sxs-lookup"><span data-stu-id="02744-110">The debugger user interface (UI) may want to take this information into account if it displays the operating system (OS) suspend count of the thread to the user.</span></span>  
  
 <span data-ttu-id="02744-111">`IsOSSuspended`方法只有在非受控的調試內容中才有意義。</span><span class="sxs-lookup"><span data-stu-id="02744-111">The `IsOSSuspended` method makes sense only in the context of unmanaged debugging.</span></span> <span data-ttu-id="02744-112">在受管理的調試過程中，執行緒會以合作方式暫停，而不是由 OS 暫停。</span><span class="sxs-lookup"><span data-stu-id="02744-112">During managed debugging, threads are cooperatively suspended rather than OS-suspended.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="02744-113">需求</span><span class="sxs-lookup"><span data-stu-id="02744-113">Requirements</span></span>  
 <span data-ttu-id="02744-114">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="02744-114">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="02744-115">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="02744-115">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="02744-116">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="02744-116">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="02744-117">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="02744-117">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>
