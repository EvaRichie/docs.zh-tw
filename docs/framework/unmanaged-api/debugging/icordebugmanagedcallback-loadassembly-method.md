---
title: ICorDebugManagedCallback::LoadAssembly 方法
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback.LoadAssembly
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback::LoadAssembly
helpviewer_keywords:
- LoadAssembly method [.NET Framework debugging]
- ICorDebugManagedCallback::LoadAssembly method [.NET Framework debugging]
ms.assetid: 55cb673a-e240-43a6-a406-6912e7c0fe66
topic_type:
- apiref
ms.openlocfilehash: 8cb8699c103f48b42694449a2bb2bbd25c42d3c6
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212722"
---
# <a name="icordebugmanagedcallbackloadassembly-method"></a><span data-ttu-id="d3663-102">ICorDebugManagedCallback::LoadAssembly 方法</span><span class="sxs-lookup"><span data-stu-id="d3663-102">ICorDebugManagedCallback::LoadAssembly Method</span></span>
<span data-ttu-id="d3663-103">通知偵錯工具已成功載入 common language runtime （CLR）元件。</span><span class="sxs-lookup"><span data-stu-id="d3663-103">Notifies the debugger that a common language runtime (CLR) assembly has been successfully loaded.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="d3663-104">語法</span><span class="sxs-lookup"><span data-stu-id="d3663-104">Syntax</span></span>  
  
```cpp  
HRESULT LoadAssembly (  
    [in] ICorDebugAppDomain *pAppDomain,  
    [in] ICorDebugAssembly  *pAssembly  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="d3663-105">參數</span><span class="sxs-lookup"><span data-stu-id="d3663-105">Parameters</span></span>  
 `pAppDomain`  
 <span data-ttu-id="d3663-106">在ICorDebugAppDomain 物件的指標，表示已載入元件的應用程式域。</span><span class="sxs-lookup"><span data-stu-id="d3663-106">[in] A pointer to an ICorDebugAppDomain object that represents the application domain into which the assembly has been loaded.</span></span>  
  
 `pAssembly`  
 <span data-ttu-id="d3663-107">在表示元件之 ICorDebugAssembly 物件的指標。</span><span class="sxs-lookup"><span data-stu-id="d3663-107">[in] A pointer to an ICorDebugAssembly object that represents the assembly.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="d3663-108">需求</span><span class="sxs-lookup"><span data-stu-id="d3663-108">Requirements</span></span>  
 <span data-ttu-id="d3663-109">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="d3663-109">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="d3663-110">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="d3663-110">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="d3663-111">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="d3663-111">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="d3663-112">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="d3663-112">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d3663-113">請參閱</span><span class="sxs-lookup"><span data-stu-id="d3663-113">See also</span></span>

- [<span data-ttu-id="d3663-114">UnloadAssembly 方法</span><span class="sxs-lookup"><span data-stu-id="d3663-114">UnloadAssembly Method</span></span>](icordebugmanagedcallback-unloadassembly-method.md)
- [<span data-ttu-id="d3663-115">ICorDebugManagedCallback 介面</span><span class="sxs-lookup"><span data-stu-id="d3663-115">ICorDebugManagedCallback Interface</span></span>](icordebugmanagedcallback-interface.md)
