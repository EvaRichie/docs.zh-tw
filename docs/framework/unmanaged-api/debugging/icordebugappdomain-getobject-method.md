---
title: ICorDebugAppDomain::GetObject 方法
ms.date: 03/30/2017
api_name:
- ICorDebugAppDomain.GetObject
api_location:
- corguids.lib
api_type:
- COM
f1_keywords:
- ICorDebugAppDomain::GetObject
helpviewer_keywords:
- ICorDebugAppDomain::GetObject method [.NET Framework debugging]
- GetObject method, ICorDebugAppDomain interface [.NET Framework debugging]
ms.assetid: 78232e6f-ae18-4cfa-a6cd-e79471cf9d76
topic_type:
- apiref
ms.openlocfilehash: a21f3b36e418bbde5dcb90f25a39dae03fde77c9
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82895216"
---
# <a name="icordebugappdomaingetobject-method"></a><span data-ttu-id="447f1-102">ICorDebugAppDomain::GetObject 方法</span><span class="sxs-lookup"><span data-stu-id="447f1-102">ICorDebugAppDomain::GetObject Method</span></span>
<span data-ttu-id="447f1-103">取得 common language runtime （CLR）應用程式域的介面指標。</span><span class="sxs-lookup"><span data-stu-id="447f1-103">Gets an interface pointer to the common language runtime (CLR) application domain.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="447f1-104">語法</span><span class="sxs-lookup"><span data-stu-id="447f1-104">Syntax</span></span>  
  
```cpp  
HRESULT GetObject (  
    [out] ICorDebugValue   **ppObject  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="447f1-105">參數</span><span class="sxs-lookup"><span data-stu-id="447f1-105">Parameters</span></span>  
 `ppObject`  
 <span data-ttu-id="447f1-106">脫銷表示 CLR 應用程式域之 ICorDebugValue 介面物件的位址指標。</span><span class="sxs-lookup"><span data-stu-id="447f1-106">[out] A pointer to the address of an ICorDebugValue interface object that represents the CLR application domain.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="447f1-107">傳回值</span><span class="sxs-lookup"><span data-stu-id="447f1-107">Return Value</span></span>  
 <span data-ttu-id="447f1-108">如果尚未針對<xref:System.AppDomain?displayProperty=nameWithType>這個應用程式域建立 managed 物件，則方法會傳回`S_FALSE` ，並`NULL`將`*ppObject`位置放入中。</span><span class="sxs-lookup"><span data-stu-id="447f1-108">If a managed <xref:System.AppDomain?displayProperty=nameWithType> object hasn't been constructed for this application domain, the method returns `S_FALSE` and places `NULL` in `*ppObject`.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="447f1-109">備註</span><span class="sxs-lookup"><span data-stu-id="447f1-109">Remarks</span></span>  
 <span data-ttu-id="447f1-110">進程中的每個應用程式域在代表<xref:System.AppDomain?displayProperty=nameWithType>它的執行時間中可能會有一個 managed 物件。</span><span class="sxs-lookup"><span data-stu-id="447f1-110">Each application domain in a process may have a managed <xref:System.AppDomain?displayProperty=nameWithType> object in the runtime that represents it.</span></span> <span data-ttu-id="447f1-111">此函式會取得對應至這個 managed <xref:System.AppDomain?displayProperty=nameWithType>物件的 ICorDebugValue 介面物件。</span><span class="sxs-lookup"><span data-stu-id="447f1-111">This function gets an ICorDebugValue interface object that corresponds to this managed <xref:System.AppDomain?displayProperty=nameWithType> object.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="447f1-112">需求</span><span class="sxs-lookup"><span data-stu-id="447f1-112">Requirements</span></span>  
 <span data-ttu-id="447f1-113">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="447f1-113">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="447f1-114">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="447f1-114">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="447f1-115">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="447f1-115">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="447f1-116">**.NET Framework 版本：**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="447f1-116">**.NET Framework Versions:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span></span>
