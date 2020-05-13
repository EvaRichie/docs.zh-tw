---
title: ICorDebugManagedCallback::CreateAppDomain 方法
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback.CreateAppDomain
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback::CreateAppDomain
helpviewer_keywords:
- CreateAppDomain method [.NET Framework debugging]
- ICorDebugManagedCallback::CreateAppDomain method [.NET Framework debugging]
ms.assetid: 48d410d7-6749-4125-a8fd-f9562c7088e9
topic_type:
- apiref
ms.openlocfilehash: 89fba6af9b76f729ca40d4ee63f525611bdf43a9
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83205638"
---
# <a name="icordebugmanagedcallbackcreateappdomain-method"></a><span data-ttu-id="3075e-102">ICorDebugManagedCallback::CreateAppDomain 方法</span><span class="sxs-lookup"><span data-stu-id="3075e-102">ICorDebugManagedCallback::CreateAppDomain Method</span></span>
<span data-ttu-id="3075e-103">通知偵錯工具已建立應用程式域。</span><span class="sxs-lookup"><span data-stu-id="3075e-103">Notifies the debugger that an application domain has been created.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="3075e-104">語法</span><span class="sxs-lookup"><span data-stu-id="3075e-104">Syntax</span></span>  
  
```cpp  
HRESULT CreateAppDomain (  
    [in] ICorDebugProcess   *pProcess,  
    [in] ICorDebugAppDomain *pAppDomain  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="3075e-105">參數</span><span class="sxs-lookup"><span data-stu-id="3075e-105">Parameters</span></span>  
 `pProcess`  
 <span data-ttu-id="3075e-106">在ICorDebugProcess 物件的指標，表示在其中建立應用程式域的進程。</span><span class="sxs-lookup"><span data-stu-id="3075e-106">[in] A pointer to an ICorDebugProcess object that represents the process in which the application domain was created.</span></span>  
  
 `pAppDomain`  
 <span data-ttu-id="3075e-107">在ICorDebugAppDomain 物件的指標，表示已建立的應用程式域。</span><span class="sxs-lookup"><span data-stu-id="3075e-107">[in] A pointer to an ICorDebugAppDomain object that represents the application domain that has been created.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="3075e-108">需求</span><span class="sxs-lookup"><span data-stu-id="3075e-108">Requirements</span></span>  
 <span data-ttu-id="3075e-109">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="3075e-109">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="3075e-110">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="3075e-110">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="3075e-111">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="3075e-111">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="3075e-112">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="3075e-112">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3075e-113">請參閱</span><span class="sxs-lookup"><span data-stu-id="3075e-113">See also</span></span>

- [<span data-ttu-id="3075e-114">ICorDebugManagedCallback 介面</span><span class="sxs-lookup"><span data-stu-id="3075e-114">ICorDebugManagedCallback Interface</span></span>](icordebugmanagedcallback-interface.md)
