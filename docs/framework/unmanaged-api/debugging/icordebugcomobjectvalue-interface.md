---
title: ICorDebugComObjectValue 介面
ms.date: 03/30/2017
api_name:
- ICorDebugComObjectValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugComObjectValue
helpviewer_keywords:
- ICorDebugComObjectValue interface [.NET Framework debugging]
ms.assetid: 505a7f6c-d92b-42b4-b539-433f5102ea9b
topic_type:
- apiref
ms.openlocfilehash: 528db447df4d71d67441b05ad29e6a900c59afbb
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82892815"
---
# <a name="icordebugcomobjectvalue-interface"></a><span data-ttu-id="15871-102">ICorDebugComObjectValue 介面</span><span class="sxs-lookup"><span data-stu-id="15871-102">ICorDebugComObjectValue Interface</span></span>
<span data-ttu-id="15871-103">提供方法來取得與執行時間可呼叫包裝函式（RCW）相關聯的資訊。</span><span class="sxs-lookup"><span data-stu-id="15871-103">Provides methods to retrieve information associated with a runtime callable wrapper (RCW).</span></span>  
  
## <a name="methods"></a><span data-ttu-id="15871-104">方法</span><span class="sxs-lookup"><span data-stu-id="15871-104">Methods</span></span>  
  
|<span data-ttu-id="15871-105">方法</span><span class="sxs-lookup"><span data-stu-id="15871-105">Method</span></span>|<span data-ttu-id="15871-106">描述</span><span class="sxs-lookup"><span data-stu-id="15871-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="15871-107">GetCachedInterfacePointers 方法</span><span class="sxs-lookup"><span data-stu-id="15871-107">GetCachedInterfacePointers Method</span></span>](icordebugcomobjectvalue-getcachedinterfacepointers-method.md)|<span data-ttu-id="15871-108">取得目前 RCW 上快取的原始介面指標。</span><span class="sxs-lookup"><span data-stu-id="15871-108">Gets the raw interface pointers cached on the current RCW.</span></span>|  
|[<span data-ttu-id="15871-109">GetCachedInterfaceTypes 方法</span><span class="sxs-lookup"><span data-stu-id="15871-109">GetCachedInterfaceTypes Method</span></span>](icordebugcomobjectvalue-getcachedinterfacetypes-method.md)|<span data-ttu-id="15871-110">提供目前物件已做為大小寫或當做使用之介面類別型的列舉值。</span><span class="sxs-lookup"><span data-stu-id="15871-110">Provides an enumerator for the interface types that the current object has been cased to or used as.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="15871-111">備註</span><span class="sxs-lookup"><span data-stu-id="15871-111">Remarks</span></span>  
 <span data-ttu-id="15871-112">若要檢查 "ICorDebugValue" 介面的實例是否代表 RCW，偵錯工具會使用`QueryInterface` `IID_ICorDebugComObjectValue`呼叫 "ICorDebugValue"。</span><span class="sxs-lookup"><span data-stu-id="15871-112">To check whether an instance of an "ICorDebugValue" interface represents an RCW, a debugger calls `QueryInterface` on "ICorDebugValue" with `IID_ICorDebugComObjectValue`.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="15871-113">需求</span><span class="sxs-lookup"><span data-stu-id="15871-113">Requirements</span></span>  
 <span data-ttu-id="15871-114">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="15871-114">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="15871-115">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="15871-115">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="15871-116">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="15871-116">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="15871-117">**.NET Framework 版本：**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="15871-117">**.NET Framework Versions:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="15871-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="15871-118">See also</span></span>

- [<span data-ttu-id="15871-119">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="15871-119">Debugging Interfaces</span></span>](debugging-interfaces.md)
- [<span data-ttu-id="15871-120">偵錯</span><span class="sxs-lookup"><span data-stu-id="15871-120">Debugging</span></span>](index.md)
