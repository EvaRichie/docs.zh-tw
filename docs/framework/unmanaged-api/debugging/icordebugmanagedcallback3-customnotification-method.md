---
title: ICorDebugManagedCallback3::CustomNotification 方法
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback3.CustomNotification Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback3::CustomNotification
helpviewer_keywords:
- ICorDebugManagedCallback3::CustomNotification method [.NET Framework debugging]
- CustomNotification method [.NET Framework debugging]
ms.assetid: 5e5422ac-afa1-403d-a894-2d7348673e38
topic_type:
- apiref
ms.openlocfilehash: 8a4620e591cc80efb5c0fd53b0edf3a35849c421
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83209756"
---
# <a name="icordebugmanagedcallback3customnotification-method"></a><span data-ttu-id="73f43-102">ICorDebugManagedCallback3::CustomNotification 方法</span><span class="sxs-lookup"><span data-stu-id="73f43-102">ICorDebugManagedCallback3::CustomNotification Method</span></span>
<span data-ttu-id="73f43-103">表示已引發自訂偵錯工具通知。</span><span class="sxs-lookup"><span data-stu-id="73f43-103">Indicates that a custom debugger notification has been raised.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="73f43-104">語法</span><span class="sxs-lookup"><span data-stu-id="73f43-104">Syntax</span></span>  
  
```cpp  
HRESULT CustomNotification(ICorDebugThread *    pThread,  
                           ICorDebugAppDomain * pAppDomain);  
```  
  
## <a name="parameters"></a><span data-ttu-id="73f43-105">參數</span><span class="sxs-lookup"><span data-stu-id="73f43-105">Parameters</span></span>  
 `pThread`  
 <span data-ttu-id="73f43-106">在引發通知之執行緒的指標。</span><span class="sxs-lookup"><span data-stu-id="73f43-106">[in] A pointer to the thread that raised the notification.</span></span>  
  
 `pAppDomain`  
 <span data-ttu-id="73f43-107">在應用程式域的指標，其中包含引發通知的執行緒。</span><span class="sxs-lookup"><span data-stu-id="73f43-107">[in] A pointer to the application domain that contains the thread that raised the notification.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="73f43-108">傳回值</span><span class="sxs-lookup"><span data-stu-id="73f43-108">Return Value</span></span>  
 <span data-ttu-id="73f43-109">這個方法會傳回下列特定的 HRESULT，以及表示方法失敗的 HRESULT 錯誤。</span><span class="sxs-lookup"><span data-stu-id="73f43-109">This method returns the following specific HRESULTs as well as HRESULT errors that indicate method failure.</span></span>  
  
|<span data-ttu-id="73f43-110">HRESULT</span><span class="sxs-lookup"><span data-stu-id="73f43-110">HRESULT</span></span>|<span data-ttu-id="73f43-111">描述</span><span class="sxs-lookup"><span data-stu-id="73f43-111">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="73f43-112">S_OK</span><span class="sxs-lookup"><span data-stu-id="73f43-112">S_OK</span></span>|<span data-ttu-id="73f43-113">已成功完成命令。</span><span class="sxs-lookup"><span data-stu-id="73f43-113">The method completed successfully.</span></span>|  
  
## <a name="exceptions"></a><span data-ttu-id="73f43-114">例外狀況</span><span class="sxs-lookup"><span data-stu-id="73f43-114">Exceptions</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="73f43-115">備註</span><span class="sxs-lookup"><span data-stu-id="73f43-115">Remarks</span></span>  
 <span data-ttu-id="73f43-116">後續呼叫[ICorDebugThread4：： GetCurrentCustomDebuggerNotification](icordebugthread4-getcurrentcustomdebuggernotification-method.md)方法，會抓取傳遞至方法的 thread 物件 <xref:System.Diagnostics.Debugger.NotifyOfCrossThreadDependency%2A?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="73f43-116">A subsequent call to the [ICorDebugThread4::GetCurrentCustomDebuggerNotification](icordebugthread4-getcurrentcustomdebuggernotification-method.md) method retrieves the thread object that was passed to the <xref:System.Diagnostics.Debugger.NotifyOfCrossThreadDependency%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="73f43-117">執行緒物件的類型必須先前已藉由呼叫[ICorDebugProcess3：： SetEnableCustomNotification](icordebugprocess3-setenablecustomnotification-method.md)方法來啟用。</span><span class="sxs-lookup"><span data-stu-id="73f43-117">The thread object's type must have been previously enabled by calling the [ICorDebugProcess3::SetEnableCustomNotification](icordebugprocess3-setenablecustomnotification-method.md) method.</span></span> <span data-ttu-id="73f43-118">偵錯工具可以從 thread 物件的欄位讀取特定類型的參數，並可將回應儲存到欄位中。</span><span class="sxs-lookup"><span data-stu-id="73f43-118">The debugger can read type-specific parameters from the fields of the thread object, and can store responses into fields.</span></span>  
  
 <span data-ttu-id="73f43-119">[ICorDebug](icordebug-interface.md)介面不會對通知類型或其內容施加任何原則，而通知的語義會嚴格成為偵錯工具、應用程式和 .NET Framework 之間的合約。</span><span class="sxs-lookup"><span data-stu-id="73f43-119">The [ICorDebug](icordebug-interface.md) interface imposes no policy on the types of notifications or their contents, and the semantics of the notifications are strictly a contract between debuggers, applications, and the .NET Framework.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="73f43-120">需求</span><span class="sxs-lookup"><span data-stu-id="73f43-120">Requirements</span></span>  
 <span data-ttu-id="73f43-121">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="73f43-121">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="73f43-122">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="73f43-122">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="73f43-123">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="73f43-123">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="73f43-124">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="73f43-124">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="73f43-125">請參閱</span><span class="sxs-lookup"><span data-stu-id="73f43-125">See also</span></span>

- [<span data-ttu-id="73f43-126">ICorDebugManagedCallback3 介面</span><span class="sxs-lookup"><span data-stu-id="73f43-126">ICorDebugManagedCallback3 Interface</span></span>](icordebugmanagedcallback3-interface.md)
- [<span data-ttu-id="73f43-127">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="73f43-127">Debugging Interfaces</span></span>](debugging-interfaces.md)
- [<span data-ttu-id="73f43-128">偵錯</span><span class="sxs-lookup"><span data-stu-id="73f43-128">Debugging</span></span>](index.md)
