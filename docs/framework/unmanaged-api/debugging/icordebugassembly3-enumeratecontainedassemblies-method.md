---
title: ICorDebugAssembly3::EnumerateContainedAssemblies 方法
ms.date: 03/30/2017
ms.assetid: 98f15b05-afad-4616-9e2a-1a9af31948b6
ms.openlocfilehash: 1e040453d5eb7a312f2e665974486492b99de16d
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95719680"
---
# <a name="icordebugassembly3enumeratecontainedassemblies-method"></a><span data-ttu-id="65ebd-102">ICorDebugAssembly3::EnumerateContainedAssemblies 方法</span><span class="sxs-lookup"><span data-stu-id="65ebd-102">ICorDebugAssembly3::EnumerateContainedAssemblies Method</span></span>

<span data-ttu-id="65ebd-103">取得這個組件所包含之組件的列舉值。</span><span class="sxs-lookup"><span data-stu-id="65ebd-103">Gets an enumerator for the assemblies contained in this assembly.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="65ebd-104">語法</span><span class="sxs-lookup"><span data-stu-id="65ebd-104">Syntax</span></span>  
  
```cpp  
HRESULT EnumerateContainedAssemblies(  
    ICorDebugAssemblyEnum **ppAssemblies  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="65ebd-105">參數</span><span class="sxs-lookup"><span data-stu-id="65ebd-105">Parameters</span></span>  

 `ppAssemblies`  
 <span data-ttu-id="65ebd-106">[out] 代表列舉值之 ICorDebugAssemblyEnum 介面物件的位址指標。</span><span class="sxs-lookup"><span data-stu-id="65ebd-106">[out] A pointer to the address of an ICorDebugAssemblyEnum interface object that is the enumerator.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="65ebd-107">傳回值</span><span class="sxs-lookup"><span data-stu-id="65ebd-107">Return Value</span></span>  

 <span data-ttu-id="65ebd-108">如果這個 `S_OK` 物件是容器，則為 `ICorDebugAssembly3`；否則為 `S_FALSE` 且列舉是空的。</span><span class="sxs-lookup"><span data-stu-id="65ebd-108">`S_OK` if this `ICorDebugAssembly3` object is a container; otherwise, `S_FALSE`, and the enumeration is empty.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="65ebd-109">備註</span><span class="sxs-lookup"><span data-stu-id="65ebd-109">Remarks</span></span>  

 <span data-ttu-id="65ebd-110">需要符號才能列舉所包含的組件。</span><span class="sxs-lookup"><span data-stu-id="65ebd-110">Symbols are needed to enumerate the contained assemblies.</span></span> <span data-ttu-id="65ebd-111">如果不存在，則這個方法會傳回 `S_FALSE` 並且不會提供任何有效的列舉值。</span><span class="sxs-lookup"><span data-stu-id="65ebd-111">If they aren't present, the method returns `S_FALSE`, and no valid enumerator is provided.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="65ebd-112">這個方法僅適用於 .NET Native。</span><span class="sxs-lookup"><span data-stu-id="65ebd-112">This method is available with .NET Native only.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="65ebd-113">需求</span><span class="sxs-lookup"><span data-stu-id="65ebd-113">Requirements</span></span>  

 <span data-ttu-id="65ebd-114">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="65ebd-114">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="65ebd-115">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="65ebd-115">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="65ebd-116">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="65ebd-116">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="65ebd-117">**.NET Framework 版本：**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span><span class="sxs-lookup"><span data-stu-id="65ebd-117">**.NET Framework Versions:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="65ebd-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="65ebd-118">See also</span></span>

- [<span data-ttu-id="65ebd-119">ICorDebugAssembly3 介面</span><span class="sxs-lookup"><span data-stu-id="65ebd-119">ICorDebugAssembly3 Interface</span></span>](icordebugassembly3-interface.md)
- [<span data-ttu-id="65ebd-120">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="65ebd-120">Debugging Interfaces</span></span>](debugging-interfaces.md)
