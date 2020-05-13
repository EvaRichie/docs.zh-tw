---
title: ICorDebugProcess::SetThreadContext 方法
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.SetThreadContext
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::SetThreadContext
helpviewer_keywords:
- ICorDebugProcess::SetThreadContext method [.NET Framework debugging]
- SetThreadContext method, ICorDebugProcess interface [.NET Framework debugging]
ms.assetid: a7b50175-2bf1-40be-8f65-64aec7aa1247
topic_type:
- apiref
ms.openlocfilehash: c9e403dc8cbb75a1e93c426a9e0b3a2083f1f10e
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83210458"
---
# <a name="icordebugprocesssetthreadcontext-method"></a><span data-ttu-id="8b16c-102">ICorDebugProcess::SetThreadContext 方法</span><span class="sxs-lookup"><span data-stu-id="8b16c-102">ICorDebugProcess::SetThreadContext Method</span></span>
<span data-ttu-id="8b16c-103">設定這個進程中指定執行緒的內容。</span><span class="sxs-lookup"><span data-stu-id="8b16c-103">Sets the context for the given thread in this process.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="8b16c-104">語法</span><span class="sxs-lookup"><span data-stu-id="8b16c-104">Syntax</span></span>  
  
```cpp  
HRESULT SetThreadContext(  
    [in] DWORD threadID,  
    [in] ULONG32 contextSize,  
    [in, length_is(contextSize), size_is(contextSize)]  
    BYTE context[]);  
```  
  
## <a name="parameters"></a><span data-ttu-id="8b16c-105">參數</span><span class="sxs-lookup"><span data-stu-id="8b16c-105">Parameters</span></span>  
 `threadID`  
 <span data-ttu-id="8b16c-106">在要設定內容的執行緒識別碼。</span><span class="sxs-lookup"><span data-stu-id="8b16c-106">[in] The ID of the thread for which to set the context.</span></span>  
  
 `contextSize`  
 <span data-ttu-id="8b16c-107">[in] `context` 陣列的大小。</span><span class="sxs-lookup"><span data-stu-id="8b16c-107">[in] The size of the `context` array.</span></span>  
  
 `context`  
 <span data-ttu-id="8b16c-108">在描述執行緒內容的位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="8b16c-108">[in] An array of bytes that describe the thread's context.</span></span>  
  
 <span data-ttu-id="8b16c-109">內容會指定執行緒在其上執行的處理器架構。</span><span class="sxs-lookup"><span data-stu-id="8b16c-109">The context specifies the architecture of the processor on which the thread is executing.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="8b16c-110">備註</span><span class="sxs-lookup"><span data-stu-id="8b16c-110">Remarks</span></span>  
 <span data-ttu-id="8b16c-111">偵錯工具應該呼叫這個方法，而不是 Win32 函式 `SetThreadContext` ，因為執行緒實際上可能處於「被攔截」狀態，而其內容已暫時變更。</span><span class="sxs-lookup"><span data-stu-id="8b16c-111">The debugger should call this method rather than the Win32 `SetThreadContext` function, because the thread may actually be in a "hijacked" state, in which its context has been temporarily changed.</span></span> <span data-ttu-id="8b16c-112">只有線上程是機器碼時，才應該使用這個方法。</span><span class="sxs-lookup"><span data-stu-id="8b16c-112">This method should be used only when a thread is in native code.</span></span> <span data-ttu-id="8b16c-113">針對 managed 程式碼中的執行緒使用[ICorDebugRegisterSet](icordebugregisterset-interface.md) 。</span><span class="sxs-lookup"><span data-stu-id="8b16c-113">Use [ICorDebugRegisterSet](icordebugregisterset-interface.md) for threads in managed code.</span></span> <span data-ttu-id="8b16c-114">您應該永遠不需要在頻外（OOB） debug 事件期間修改執行緒的內容。</span><span class="sxs-lookup"><span data-stu-id="8b16c-114">You should never need to modify the context of a thread during an out-of-band (OOB) debug event.</span></span>  
  
 <span data-ttu-id="8b16c-115">傳遞的資料必須是目前平臺的內容結構。</span><span class="sxs-lookup"><span data-stu-id="8b16c-115">The data passed must be a context structure for the current platform.</span></span>  
  
 <span data-ttu-id="8b16c-116">如果未正確使用，這個方法可能會損毀執行時間。</span><span class="sxs-lookup"><span data-stu-id="8b16c-116">This method can corrupt the runtime if used improperly.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="8b16c-117">需求</span><span class="sxs-lookup"><span data-stu-id="8b16c-117">Requirements</span></span>  
 <span data-ttu-id="8b16c-118">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="8b16c-118">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="8b16c-119">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="8b16c-119">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="8b16c-120">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="8b16c-120">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="8b16c-121">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="8b16c-121">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>
