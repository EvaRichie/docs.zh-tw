---
title: ICorDebug::CreateProcess 方法
ms.date: 03/30/2017
api_name:
- ICorDebug.CreateProcess
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebug::CreateProcess
helpviewer_keywords:
- ICorDebug::CreateProcess method [.NET Framework debugging]
- CreateProcess method, ICorDebugProcess interface [.NET Framework debugging]
ms.assetid: b6128694-11ed-46e7-bd4e-49ea1914c46a
topic_type:
- apiref
ms.openlocfilehash: b9ae2b36bff9b4a6c048a8de99fa7d09350b1401
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2020
ms.locfileid: "82859704"
---
# <a name="icordebugcreateprocess-method"></a><span data-ttu-id="f7367-102">ICorDebug::CreateProcess 方法</span><span class="sxs-lookup"><span data-stu-id="f7367-102">ICorDebug::CreateProcess Method</span></span>
<span data-ttu-id="f7367-103">在偵錯工具的控制項底下啟動進程和其主要執行緒。</span><span class="sxs-lookup"><span data-stu-id="f7367-103">Launches a process and its primary thread under the control of the debugger.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="f7367-104">語法</span><span class="sxs-lookup"><span data-stu-id="f7367-104">Syntax</span></span>  
  
```cpp  
HRESULT CreateProcess (  
    [in]  LPCWSTR                     lpApplicationName,  
    [in]  LPWSTR                      lpCommandLine,  
    [in]  LPSECURITY_ATTRIBUTES       lpProcessAttributes,  
    [in]  LPSECURITY_ATTRIBUTES       lpThreadAttributes,  
    [in]  BOOL                        bInheritHandles,  
    [in]  DWORD                       dwCreationFlags,  
    [in]  PVOID                       lpEnvironment,  
    [in]  LPCWSTR                     lpCurrentDirectory,  
    [in]  LPSTARTUPINFOW              lpStartupInfo,  
    [in]  LPPROCESS_INFORMATION       lpProcessInformation,  
    [in]  CorDebugCreateProcessFlags  debuggingFlags,  
    [out] ICorDebugProcess            **ppProcess  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="f7367-105">參數</span><span class="sxs-lookup"><span data-stu-id="f7367-105">Parameters</span></span>  
 `lpApplicationName`  
 <span data-ttu-id="f7367-106">在以 null 結束的字串指標，指定啟動的進程所要執行的模組。</span><span class="sxs-lookup"><span data-stu-id="f7367-106">[in] Pointer to a null-terminated string that specifies the module to be executed by the launched process.</span></span> <span data-ttu-id="f7367-107">模組會在呼叫進程的安全性內容中執行。</span><span class="sxs-lookup"><span data-stu-id="f7367-107">The module is executed in the security context of the calling process.</span></span>  
  
 `lpCommandLine`  
 <span data-ttu-id="f7367-108">在以 null 結束的字串指標，指定啟動的進程所要執行的命令列。</span><span class="sxs-lookup"><span data-stu-id="f7367-108">[in] Pointer to a null-terminated string that specifies the command line to be executed by the launched process.</span></span> <span data-ttu-id="f7367-109">應用程式名稱（例如，"SomeApp"）必須是第一個引數。</span><span class="sxs-lookup"><span data-stu-id="f7367-109">The application name (for example, "SomeApp.exe") must be the first argument.</span></span>  
  
 `lpProcessAttributes`  
 <span data-ttu-id="f7367-110">在Win32 `SECURITY_ATTRIBUTES`結構的指標，指定進程的安全描述項。</span><span class="sxs-lookup"><span data-stu-id="f7367-110">[in] Pointer to a Win32 `SECURITY_ATTRIBUTES` structure that specifies the security descriptor for the process.</span></span> <span data-ttu-id="f7367-111">如果`lpProcessAttributes`為 null，進程會取得預設的安全描述項。</span><span class="sxs-lookup"><span data-stu-id="f7367-111">If `lpProcessAttributes` is null, the process gets a default security descriptor.</span></span>  
  
 `lpThreadAttributes`  
 <span data-ttu-id="f7367-112">在Win32 `SECURITY_ATTRIBUTES`結構的指標，指定進程主要執行緒的安全描述項。</span><span class="sxs-lookup"><span data-stu-id="f7367-112">[in] Pointer to a Win32 `SECURITY_ATTRIBUTES` structure that specifies the security descriptor for the primary thread of the process.</span></span> <span data-ttu-id="f7367-113">如果`lpThreadAttributes`為 null，則執行緒會取得預設的安全描述項。</span><span class="sxs-lookup"><span data-stu-id="f7367-113">If `lpThreadAttributes` is null, the thread gets a default security descriptor.</span></span>  
  
 `bInheritHandles`  
 <span data-ttu-id="f7367-114">在設定為`true` ，表示已啟動的進程會繼承呼叫進程中的每個可繼承控制碼`false` ，或表示不會繼承控制碼。</span><span class="sxs-lookup"><span data-stu-id="f7367-114">[in] Set to `true` to indicate that each inheritable handle in the calling process is inherited by the launched process, or `false` to indicate that the handles are not inherited.</span></span> <span data-ttu-id="f7367-115">繼承的控制碼與原始控制碼具有相同的值和存取權限。</span><span class="sxs-lookup"><span data-stu-id="f7367-115">The inherited handles have the same value and access rights as the original handles.</span></span>  
  
 `dwCreationFlags`  
 <span data-ttu-id="f7367-116">在[Win32 進程建立旗標](/windows/win32/procthread/process-creation-flags)的位元組合，可控制優先順序類別和已啟動進程的行為。</span><span class="sxs-lookup"><span data-stu-id="f7367-116">[in] A bitwise combination of the [Win32 Process Creation Flags](/windows/win32/procthread/process-creation-flags) that control the priority class and the behavior of the launched process.</span></span>  
  
 `lpEnvironment`  
 <span data-ttu-id="f7367-117">在新進程之環境區塊的指標。</span><span class="sxs-lookup"><span data-stu-id="f7367-117">[in] Pointer to an environment block for the new process.</span></span>  
  
 `lpCurrentDirectory`  
 <span data-ttu-id="f7367-118">在以 null 結束的字串指標，指定進程目前目錄的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="f7367-118">[in] Pointer to a null-terminated string that specifies the full path to the current directory for the process.</span></span> <span data-ttu-id="f7367-119">如果此參數為 null，新的進程將會具有與呼叫進程相同的目前磁片磁碟機和目錄。</span><span class="sxs-lookup"><span data-stu-id="f7367-119">If this parameter is null, the new process will have the same current drive and directory as the calling process.</span></span>  
  
 `lpStartupInfo`  
 <span data-ttu-id="f7367-120">在Win32 `STARTUPINFOW`結構的指標，指定視窗站、桌面、標準控制碼，以及啟動之進程的主視窗外觀。</span><span class="sxs-lookup"><span data-stu-id="f7367-120">[in] Pointer to a Win32 `STARTUPINFOW` structure that specifies the window station, desktop, standard handles, and appearance of the main window for the launched process.</span></span>  
  
 `lpProcessInformation`  
 <span data-ttu-id="f7367-121">在Win32 `PROCESS_INFORMATION`結構的指標，指定要啟動之進程的識別資訊。</span><span class="sxs-lookup"><span data-stu-id="f7367-121">[in] Pointer to a Win32 `PROCESS_INFORMATION` structure that specifies the identification information about the process to be launched.</span></span>  
  
 `debuggingFlags`  
 <span data-ttu-id="f7367-122">在指定偵錯工具選項的 CorDebugCreateProcessFlags 列舉值。</span><span class="sxs-lookup"><span data-stu-id="f7367-122">[in] A value of the CorDebugCreateProcessFlags enumeration that specifies the debugging options.</span></span>  
  
 `ppProcess`  
 <span data-ttu-id="f7367-123">脫銷代表進程之 ICorDebugProcess 物件的位址指標。</span><span class="sxs-lookup"><span data-stu-id="f7367-123">[out] A pointer to the address of a ICorDebugProcess object that represents the process.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="f7367-124">備註</span><span class="sxs-lookup"><span data-stu-id="f7367-124">Remarks</span></span>  
 <span data-ttu-id="f7367-125">這個方法的參數與 Win32 `CreateProcess`方法的參數相同。</span><span class="sxs-lookup"><span data-stu-id="f7367-125">The parameters of this method are the same as those of the Win32 `CreateProcess` method.</span></span>  
  
 <span data-ttu-id="f7367-126">若要啟用非受控混合模式的調試`dwCreationFlags` ，請將設定為 DEBUG_PROCESS &#124; DEBUG_ONLY_THIS_PROCESS。</span><span class="sxs-lookup"><span data-stu-id="f7367-126">To enable unmanaged mixed-mode debugging, set `dwCreationFlags` to DEBUG_PROCESS &#124; DEBUG_ONLY_THIS_PROCESS.</span></span> <span data-ttu-id="f7367-127">如果您只想要使用受管理的調試，請勿設定這些旗標。</span><span class="sxs-lookup"><span data-stu-id="f7367-127">If you want to use only managed debugging, do not set these flags.</span></span>  
  
 <span data-ttu-id="f7367-128">若偵錯工具和要進行調試的進程（附加的進程）共用單一主控台，而且使用 interop 偵錯工具，則附加的進程可能會保留主控台鎖定，並在 debug 事件停止。</span><span class="sxs-lookup"><span data-stu-id="f7367-128">If the debugger and the process to be debugged (the attached process) share a single console, and if interop debugging is used, it is possible for the attached process to hold console locks and stop at a debug event.</span></span> <span data-ttu-id="f7367-129">然後偵錯工具會封鎖任何使用主控台的嘗試。</span><span class="sxs-lookup"><span data-stu-id="f7367-129">The debugger will then block any attempt to use the console.</span></span> <span data-ttu-id="f7367-130">若要避免這個問題，請在`dwCreationFlags`參數中設定 CREATE_NEW_CONSOLE 旗標。</span><span class="sxs-lookup"><span data-stu-id="f7367-130">To avoid this problem, set the CREATE_NEW_CONSOLE flag in the `dwCreationFlags` parameter.</span></span>  
  
 <span data-ttu-id="f7367-131">在 Win9x 和非 x86 平臺（例如 IA-64 型和以 AMD64 為基礎的平臺）上不支援 Interop 調試。</span><span class="sxs-lookup"><span data-stu-id="f7367-131">Interop debugging is not supported on Win9x and non-x86 platforms such as IA-64-based and AMD64-based platforms.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="f7367-132">需求</span><span class="sxs-lookup"><span data-stu-id="f7367-132">Requirements</span></span>  
 <span data-ttu-id="f7367-133">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="f7367-133">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="f7367-134">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="f7367-134">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="f7367-135">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="f7367-135">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="f7367-136">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="f7367-136">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f7367-137">請參閱</span><span class="sxs-lookup"><span data-stu-id="f7367-137">See also</span></span>

- [<span data-ttu-id="f7367-138">ICorDebug 介面</span><span class="sxs-lookup"><span data-stu-id="f7367-138">ICorDebug Interface</span></span>](icordebug-interface.md)
