---
title: ICorDebugManagedCallback::Exception 方法
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback.Exception
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback::Exception
helpviewer_keywords:
- Exception method, ICorDebugManagedCallback interface [.NET Framework debugging]
- ICorDebugManagedCallback::Exception method [.NET Framework debugging]
ms.assetid: ab18a509-dff3-4930-b585-bd15e0414176
topic_type:
- apiref
ms.openlocfilehash: 2d0461709accf1a9300c072b62bd58734cb33fb8
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83209808"
---
# <a name="icordebugmanagedcallbackexception-method"></a><span data-ttu-id="5814b-102">ICorDebugManagedCallback::Exception 方法</span><span class="sxs-lookup"><span data-stu-id="5814b-102">ICorDebugManagedCallback::Exception Method</span></span>
<span data-ttu-id="5814b-103">通知偵錯工具，已從 managed 程式碼擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="5814b-103">Notifies the debugger that an exception has been thrown from managed code.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="5814b-104">語法</span><span class="sxs-lookup"><span data-stu-id="5814b-104">Syntax</span></span>  
  
```cpp  
HRESULT Exception (  
    [in] ICorDebugAppDomain *pAppDomain,  
    [in] ICorDebugThread    *pThread,  
    [in] BOOL                unhandled  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="5814b-105">參數</span><span class="sxs-lookup"><span data-stu-id="5814b-105">Parameters</span></span>  
 `pAppDomain`  
 <span data-ttu-id="5814b-106">在ICorDebugAppDomain 物件的指標，表示擲回例外狀況的應用程式域。</span><span class="sxs-lookup"><span data-stu-id="5814b-106">[in] A pointer to an ICorDebugAppDomain object that represents the application domain in which the exception was thrown.</span></span>  
  
 `pThread`  
 <span data-ttu-id="5814b-107">在ICorDebugThread 物件的指標，表示擲回例外狀況的執行緒。</span><span class="sxs-lookup"><span data-stu-id="5814b-107">[in] A pointer to an ICorDebugThread object that represents the thread in which the exception was thrown.</span></span>  
  
 `unhandled`  
 <span data-ttu-id="5814b-108">在如果這個值為 `false` ，則應用程式尚未處理此例外狀況，否則，例外狀況會被處理，並終止進程。</span><span class="sxs-lookup"><span data-stu-id="5814b-108">[in] If this value is `false`, the exception has not yet been processed by the application; otherwise, the exception is unhandled and will terminate the process.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="5814b-109">備註</span><span class="sxs-lookup"><span data-stu-id="5814b-109">Remarks</span></span>  
 <span data-ttu-id="5814b-110">您可以從 thread 物件中抓取特定的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="5814b-110">The specific exception can be retrieved from the thread object.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="5814b-111">需求</span><span class="sxs-lookup"><span data-stu-id="5814b-111">Requirements</span></span>  
 <span data-ttu-id="5814b-112">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="5814b-112">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="5814b-113">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="5814b-113">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="5814b-114">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="5814b-114">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="5814b-115">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="5814b-115">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="5814b-116">請參閱</span><span class="sxs-lookup"><span data-stu-id="5814b-116">See also</span></span>

- [<span data-ttu-id="5814b-117">ICorDebugManagedCallback 介面</span><span class="sxs-lookup"><span data-stu-id="5814b-117">ICorDebugManagedCallback Interface</span></span>](icordebugmanagedcallback-interface.md)
