---
title: ICorDebugLoadedModule 介面
ms.date: 03/30/2017
ms.assetid: 34be6369-2e75-4a95-a538-3b29ac97cf6d
ms.openlocfilehash: d9b8245d8c37867971aa48ed3befb9cf22bd5b04
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83210159"
---
# <a name="icordebugloadedmodule-interface"></a><span data-ttu-id="eef30-102">ICorDebugLoadedModule 介面</span><span class="sxs-lookup"><span data-stu-id="eef30-102">ICorDebugLoadedModule Interface</span></span>
<span data-ttu-id="eef30-103">提供載入模組的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="eef30-103">Provides information about a loaded module.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="eef30-104">方法</span><span class="sxs-lookup"><span data-stu-id="eef30-104">Methods</span></span>  
  
|<span data-ttu-id="eef30-105">方法</span><span class="sxs-lookup"><span data-stu-id="eef30-105">Method</span></span>|<span data-ttu-id="eef30-106">描述</span><span class="sxs-lookup"><span data-stu-id="eef30-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="eef30-107">GetBaseAddress 方法</span><span class="sxs-lookup"><span data-stu-id="eef30-107">GetBaseAddress Method</span></span>](icordebugloadedmodule-getbaseaddress-method.md)|<span data-ttu-id="eef30-108">取得載入模組的基底位址。</span><span class="sxs-lookup"><span data-stu-id="eef30-108">Gets the base address of the loaded module.</span></span>|  
|[<span data-ttu-id="eef30-109">GetName 方法</span><span class="sxs-lookup"><span data-stu-id="eef30-109">GetName Method</span></span>](icordebugloadedmodule-getname-method.md)|<span data-ttu-id="eef30-110">取得載入模組的名稱。</span><span class="sxs-lookup"><span data-stu-id="eef30-110">Gets the name of the loaded module.</span></span>|  
|[<span data-ttu-id="eef30-111">GetSize 方法</span><span class="sxs-lookup"><span data-stu-id="eef30-111">GetSize Method</span></span>](icordebugloadedmodule-getsize-method.md)|<span data-ttu-id="eef30-112">取得載入模組的大小 (以位元組為單位)。</span><span class="sxs-lookup"><span data-stu-id="eef30-112">Gets the size in bytes of the loaded module.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="eef30-113">備註</span><span class="sxs-lookup"><span data-stu-id="eef30-113">Remarks</span></span>  
 <span data-ttu-id="eef30-114">`ICorDebugLoadedModule` 介面是由偵錯工具實作，並由 CLR 偵錯介面用以從偵錯工具取得載入模組的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="eef30-114">The `ICorDebugLoadedModule` interface is implemented by a debugger and is used by the CLR debugging interfaces to get information about the loaded module from the debugger.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="eef30-115">這個介面僅適用於 .NET 原生。</span><span class="sxs-lookup"><span data-stu-id="eef30-115">This interface is available with .NET Native only.</span></span> <span data-ttu-id="eef30-116">如果您在 .NET 原生之外針對 ICorDebug 案例實作這個介面，Common Language Runtime 會忽略這個介面。</span><span class="sxs-lookup"><span data-stu-id="eef30-116">If you implement this interface for ICorDebug scenarios outside of .NET Native, the common language runtime will ignore this interface.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="eef30-117">需求</span><span class="sxs-lookup"><span data-stu-id="eef30-117">Requirements</span></span>  
 <span data-ttu-id="eef30-118">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="eef30-118">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="eef30-119">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="eef30-119">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="eef30-120">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="eef30-120">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="eef30-121">**.NET Framework 版本：**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span><span class="sxs-lookup"><span data-stu-id="eef30-121">**.NET Framework Versions:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="eef30-122">請參閱</span><span class="sxs-lookup"><span data-stu-id="eef30-122">See also</span></span>

- [<span data-ttu-id="eef30-123">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="eef30-123">Debugging Interfaces</span></span>](debugging-interfaces.md)
- [<span data-ttu-id="eef30-124">偵錯</span><span class="sxs-lookup"><span data-stu-id="eef30-124">Debugging</span></span>](index.md)
