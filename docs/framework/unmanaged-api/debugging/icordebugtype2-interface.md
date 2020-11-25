---
title: ICorDebugType2 介面
ms.date: 03/30/2017
api_name:
- ICorDebugType2
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugType2
helpviewer_keywords:
- ICorDebugType2 interface
ms.assetid: 376fb03f-f1ef-4107-baa4-4d9d55884862
topic_type:
- apiref
ms.openlocfilehash: 0d5fffe4350cc1f58acf588f288db3bdb7e213d0
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95725664"
---
# <a name="icordebugtype2-interface"></a><span data-ttu-id="d352a-102">ICorDebugType2 介面</span><span class="sxs-lookup"><span data-stu-id="d352a-102">ICorDebugType2 Interface</span></span>

<span data-ttu-id="d352a-103">擴充 ICorDebugType 介面，以取得基底類型或複雜 (使用者定義) 類型的類型識別碼。</span><span class="sxs-lookup"><span data-stu-id="d352a-103">Extends the ICorDebugType interface to retrieve the type identifier  of a base type or complex (user-defined) type.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="d352a-104">方法</span><span class="sxs-lookup"><span data-stu-id="d352a-104">Methods</span></span>  
  
|<span data-ttu-id="d352a-105">方法</span><span class="sxs-lookup"><span data-stu-id="d352a-105">Method</span></span>||  
|------------|-|  
|[<span data-ttu-id="d352a-106">GetTypeID 方法</span><span class="sxs-lookup"><span data-stu-id="d352a-106">GetTypeID Method</span></span>](icordebugtype2-gettypeid-method.md)|<span data-ttu-id="d352a-107">取得此類型的 [COR_TYPEID](cor-typeid-structure.md) 。</span><span class="sxs-lookup"><span data-stu-id="d352a-107">Gets a [COR_TYPEID](cor-typeid-structure.md) for this type.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="d352a-108">備註</span><span class="sxs-lookup"><span data-stu-id="d352a-108">Remarks</span></span>  

 <span data-ttu-id="d352a-109">此介面是 ICorDebugType 介面的邏輯擴充。</span><span class="sxs-lookup"><span data-stu-id="d352a-109">This interface is a logical extension of the ICorDebugType interface.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="d352a-110">這個介面不支援跨電腦或跨處理序的遠端呼叫。</span><span class="sxs-lookup"><span data-stu-id="d352a-110">This interface does not support being called remotely, either cross-machine or cross-process.</span></span>  
  
## <a name="example"></a><span data-ttu-id="d352a-111">範例</span><span class="sxs-lookup"><span data-stu-id="d352a-111">Example</span></span>  

 <span data-ttu-id="d352a-112">下列程式碼片段說明如何使用 [ICorDebugType2：： GetTypeID](icordebugtype2-gettypeid-method.md) 方法。</span><span class="sxs-lookup"><span data-stu-id="d352a-112">The following code fragment illustrates the use of the [ICorDebugType2::GetTypeID](icordebugtype2-gettypeid-method.md) method.</span></span>  
  
```cpp  
// (error checking omitted for brevity)  
// given an ICorDebugType *pType  
  
ICorDebugType2 *pType2 = NULL;  
pType->QueryInterface(IID_ICorDebugType2, &pType);  
  
COR_TYPEID id;  
pType2->GetTypeID(&id);  
  
// now we can use existing APIs to get information about this COR_TYPEID  
```  
  
## <a name="requirements"></a><span data-ttu-id="d352a-113">需求</span><span class="sxs-lookup"><span data-stu-id="d352a-113">Requirements</span></span>  

 <span data-ttu-id="d352a-114">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="d352a-114">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="d352a-115">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="d352a-115">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="d352a-116">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="d352a-116">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="d352a-117">**.NET Framework 版本：**[!INCLUDE[net_current_v462plus](../../../../includes/net-current-v462plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="d352a-117">**.NET Framework Versions:** [!INCLUDE[net_current_v462plus](../../../../includes/net-current-v462plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d352a-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d352a-118">See also</span></span>

- [<span data-ttu-id="d352a-119">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="d352a-119">Debugging Interfaces</span></span>](debugging-interfaces.md)
