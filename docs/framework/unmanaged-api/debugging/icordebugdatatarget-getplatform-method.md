---
title: ICorDebugDataTarget::GetPlatform 方法
ms.date: 03/30/2017
api_name:
- ICorDebugDataTarget.GetPlatform Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugDataTarget::GetPlatform
helpviewer_keywords:
- GetPlatform method [.NET Framework debugging]
- ICorDebugDataTarget::GetPlatform method [.NET Framework debugging]
ms.assetid: 9ee96c9d-7a3d-4129-a6cc-7675c7f2dda4
topic_type:
- apiref
ms.openlocfilehash: e8612b23cbfa506fddb2fad712848b285b9ac28e
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95679789"
---
# <a name="icordebugdatatargetgetplatform-method"></a><span data-ttu-id="d94d0-102">ICorDebugDataTarget::GetPlatform 方法</span><span class="sxs-lookup"><span data-stu-id="d94d0-102">ICorDebugDataTarget::GetPlatform Method</span></span>

<span data-ttu-id="d94d0-103">提供目標進程執行所在平臺的相關資訊，包括處理器架構和作業系統。</span><span class="sxs-lookup"><span data-stu-id="d94d0-103">Provides information about the platform, including processor architecture and operating system, on which the target process is running.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="d94d0-104">語法</span><span class="sxs-lookup"><span data-stu-id="d94d0-104">Syntax</span></span>  
  
```cpp  
HRESULT GetPlatform([out] CorDebugPlatform * pTargetPlatform);  
```  
  
## <a name="parameters"></a><span data-ttu-id="d94d0-105">參數</span><span class="sxs-lookup"><span data-stu-id="d94d0-105">Parameters</span></span>  

 `pTargetPlatform`  
 <span data-ttu-id="d94d0-106">擴展描述目標平臺之 [CorDebugPlatformEnum](cordebugplatform-enumeration.md) 列舉的指標。</span><span class="sxs-lookup"><span data-stu-id="d94d0-106">[out] A pointer to a [CorDebugPlatformEnum](cordebugplatform-enumeration.md) enumeration that describes the target platform.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="d94d0-107">備註</span><span class="sxs-lookup"><span data-stu-id="d94d0-107">Remarks</span></span>  

 <span data-ttu-id="d94d0-108">`CorDebugPlatformEnum` [ICorDebug](icordebug-interface.md)介面會使用列舉傳回值來判斷目標進程的詳細資料，例如它的指標大小、位址空間配置、暫存器集、指令格式、內容配置和呼叫慣例。</span><span class="sxs-lookup"><span data-stu-id="d94d0-108">The `CorDebugPlatformEnum` enumeration return value is used by the [ICorDebug](icordebug-interface.md) interface to determine details of the target process such as its pointer size, address space layout, register set, instruction format, context layout, and calling conventions.</span></span>  
  
 <span data-ttu-id="d94d0-109">此 `pTargetPlatform` 值可能會參考針對目標模擬的平臺，而不是指定實際使用的硬體。</span><span class="sxs-lookup"><span data-stu-id="d94d0-109">The `pTargetPlatform` value may refer to a platform that is being emulated for the target instead of specifying the actual hardware in use.</span></span> <span data-ttu-id="d94d0-110">例如，在 windows on windows 上執行的處理常式，在64位版本的 Windows 作業系統上 (WOW) 環境應該使用 `CORDB_PLATFORM_WINDOWS_X86` [CorDebugPlatformEnum](cordebugplatform-enumeration.md) 列舉的值。</span><span class="sxs-lookup"><span data-stu-id="d94d0-110">For example, a process that is running in the Windows on Windows (WOW) environment on a 64-bit edition of the Windows operating system should use the `CORDB_PLATFORM_WINDOWS_X86` value of the [CorDebugPlatformEnum](cordebugplatform-enumeration.md) enumeration.</span></span>  
  
 <span data-ttu-id="d94d0-111">此方法必須成功。</span><span class="sxs-lookup"><span data-stu-id="d94d0-111">This method must succeed.</span></span> <span data-ttu-id="d94d0-112">如果失敗，則無法使用目標平臺。</span><span class="sxs-lookup"><span data-stu-id="d94d0-112">If it fails, the target platform is unusable.</span></span> <span data-ttu-id="d94d0-113">方法可能會因為下列原因而失敗：</span><span class="sxs-lookup"><span data-stu-id="d94d0-113">The method may fail for the following reasons:</span></span>  
  
- <span data-ttu-id="d94d0-114">針對目標模擬的平臺無法使用。</span><span class="sxs-lookup"><span data-stu-id="d94d0-114">The platform that is being emulated for the target is unusable.</span></span>  
  
- <span data-ttu-id="d94d0-115">目標平臺上的實際硬體無法使用。</span><span class="sxs-lookup"><span data-stu-id="d94d0-115">The actual hardware on the target platform is unusable.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="d94d0-116">需求</span><span class="sxs-lookup"><span data-stu-id="d94d0-116">Requirements</span></span>  

 <span data-ttu-id="d94d0-117">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="d94d0-117">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="d94d0-118">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="d94d0-118">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="d94d0-119">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="d94d0-119">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="d94d0-120">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="d94d0-120">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d94d0-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d94d0-121">See also</span></span>

- [<span data-ttu-id="d94d0-122">ICorDebugDataTarget 介面</span><span class="sxs-lookup"><span data-stu-id="d94d0-122">ICorDebugDataTarget Interface</span></span>](icordebugdatatarget-interface.md)
- [<span data-ttu-id="d94d0-123">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="d94d0-123">Debugging Interfaces</span></span>](debugging-interfaces.md)
- [<span data-ttu-id="d94d0-124">偵錯</span><span class="sxs-lookup"><span data-stu-id="d94d0-124">Debugging</span></span>](index.md)
