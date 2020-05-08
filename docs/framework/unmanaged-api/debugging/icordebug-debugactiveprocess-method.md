---
title: ICorDebug::DebugActiveProcess 方法
ms.date: 03/30/2017
api_name:
- ICorDebug.DebugActiveProcess
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebug::DebugActiveProcess
helpviewer_keywords:
- DebugActiveProcess method [.NET Framework debugging]
- ICorDebug::DebugActiveProcess method [.NET Framework debugging]
ms.assetid: fdab0ade-7f56-4fa2-b3ef-f7a1d2852bba
topic_type:
- apiref
ms.openlocfilehash: 3630e25b6c24edaa366f1b0fae088e760e851fa4
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82895413"
---
# <a name="icordebugdebugactiveprocess-method"></a><span data-ttu-id="38add-102">ICorDebug::DebugActiveProcess 方法</span><span class="sxs-lookup"><span data-stu-id="38add-102">ICorDebug::DebugActiveProcess Method</span></span>
<span data-ttu-id="38add-103">將偵錯工具附加至現有的進程。</span><span class="sxs-lookup"><span data-stu-id="38add-103">Attaches the debugger to an existing process.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="38add-104">語法</span><span class="sxs-lookup"><span data-stu-id="38add-104">Syntax</span></span>  
  
```cpp  
HRESULT DebugActiveProcess (  
    [in]  DWORD               id,  
    [in]  BOOL                win32Attach,  
    [out] ICorDebugProcess    **ppProcess  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="38add-105">參數</span><span class="sxs-lookup"><span data-stu-id="38add-105">Parameters</span></span>  
 `id`  
 <span data-ttu-id="38add-106">在要附加偵錯工具之進程的識別碼。</span><span class="sxs-lookup"><span data-stu-id="38add-106">[in] The ID of the process to which the debugger is to be attached.</span></span>  
  
 `win32Attach`  
 <span data-ttu-id="38add-107">在布林值，如果偵錯工具`true`應該做為進程的 Win32 偵錯工具，並分派非受控回呼，則設定為。否則為`false`。</span><span class="sxs-lookup"><span data-stu-id="38add-107">[in] Boolean value that is set to `true` if the debugger should behave as the Win32 debugger for the process and dispatch the unmanaged callbacks; otherwise, `false`.</span></span>  
  
 `ppProcess`  
 <span data-ttu-id="38add-108">脫銷"ICorDebugProcess" 物件位址的指標，表示已附加偵錯工具的進程。</span><span class="sxs-lookup"><span data-stu-id="38add-108">[out] A pointer to the address of an "ICorDebugProcess" object that represents the process to which the debugger has been attached.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="38add-109">備註</span><span class="sxs-lookup"><span data-stu-id="38add-109">Remarks</span></span>  
 <span data-ttu-id="38add-110">在 Win9x 和非 x86 平臺（例如，IA-64 型和以 AMD64 為基礎的平臺）上不支援 Interop 調試。</span><span class="sxs-lookup"><span data-stu-id="38add-110">Interop debugging is not supported on Win9x and non-x86 platforms, such as IA-64-based and AMD64-based platforms.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="38add-111">需求</span><span class="sxs-lookup"><span data-stu-id="38add-111">Requirements</span></span>  
 <span data-ttu-id="38add-112">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="38add-112">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="38add-113">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="38add-113">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="38add-114">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="38add-114">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="38add-115">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="38add-115">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="38add-116">另請參閱</span><span class="sxs-lookup"><span data-stu-id="38add-116">See also</span></span>

- [<span data-ttu-id="38add-117">ICorDebug 介面</span><span class="sxs-lookup"><span data-stu-id="38add-117">ICorDebug Interface</span></span>](icordebug-interface.md)
