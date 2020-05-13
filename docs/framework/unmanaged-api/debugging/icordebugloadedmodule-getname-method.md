---
title: ICorDebugLoadedModule::GetName 方法
ms.date: 03/30/2017
ms.assetid: 88c304d5-edaa-4c0e-a8e1-144e8a76877e
ms.openlocfilehash: 4a0c4e99f23dc949b0bbaa8bbda35cff1537cf3c
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83209860"
---
# <a name="icordebugloadedmodulegetname-method"></a><span data-ttu-id="e07ad-102">ICorDebugLoadedModule::GetName 方法</span><span class="sxs-lookup"><span data-stu-id="e07ad-102">ICorDebugLoadedModule::GetName Method</span></span>
<span data-ttu-id="e07ad-103">取得載入模組的名稱。</span><span class="sxs-lookup"><span data-stu-id="e07ad-103">Gets the name of the loaded module.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="e07ad-104">語法</span><span class="sxs-lookup"><span data-stu-id="e07ad-104">Syntax</span></span>  
  
```cpp  
HRESULT GetName(  
   [in] ULONG32 cchName,  
   [out] ULONG32 *pcchName,  
   [out, size_is(cchName),  
   length_is(*pcchName)] WCHAR szName[]  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="e07ad-105">參數</span><span class="sxs-lookup"><span data-stu-id="e07ad-105">Parameters</span></span>  
 `cchName`  
 <span data-ttu-id="e07ad-106">[in] `szName` 緩衝區中的字元數。</span><span class="sxs-lookup"><span data-stu-id="e07ad-106">[in] The number of characters in the `szName` buffer.</span></span>  
  
 `pcchName`  
 <span data-ttu-id="e07ad-107">[out] 實際寫入 `szName` 緩衝區的字元數指標。</span><span class="sxs-lookup"><span data-stu-id="e07ad-107">[out] A pointer to the number of characters actually written to the `szName` buffer.</span></span>  
  
 `szName`  
 <span data-ttu-id="e07ad-108">[out] 包含載入模組名稱的字元陣列。</span><span class="sxs-lookup"><span data-stu-id="e07ad-108">[out] An array of characters that contain the name of the loaded module.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="e07ad-109">備註</span><span class="sxs-lookup"><span data-stu-id="e07ad-109">Remarks</span></span>  
  
> [!NOTE]
> <span data-ttu-id="e07ad-110">這個方法僅適用於 .NET Native。</span><span class="sxs-lookup"><span data-stu-id="e07ad-110">This method is available with .NET Native only.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="e07ad-111">需求</span><span class="sxs-lookup"><span data-stu-id="e07ad-111">Requirements</span></span>  
 <span data-ttu-id="e07ad-112">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="e07ad-112">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="e07ad-113">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="e07ad-113">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="e07ad-114">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="e07ad-114">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="e07ad-115">**.NET Framework 版本：**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span><span class="sxs-lookup"><span data-stu-id="e07ad-115">**.NET Framework Versions:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e07ad-116">請參閱</span><span class="sxs-lookup"><span data-stu-id="e07ad-116">See also</span></span>

- [<span data-ttu-id="e07ad-117">ICorDebugLoadedModule 介面</span><span class="sxs-lookup"><span data-stu-id="e07ad-117">ICorDebugLoadedModule Interface</span></span>](icordebugloadedmodule-interface.md)
- [<span data-ttu-id="e07ad-118">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="e07ad-118">Debugging Interfaces</span></span>](debugging-interfaces.md)
