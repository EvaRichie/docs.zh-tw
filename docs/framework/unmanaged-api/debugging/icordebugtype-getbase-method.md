---
title: ICorDebugType::GetBase 方法
ms.date: 03/30/2017
api_name:
- ICorDebugType.GetBase
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugType::GetBase
helpviewer_keywords:
- ICorDebugType::GetBase method [.NET Framework debugging]
- GetBase method [.NET Framework debugging]
ms.assetid: f24e1af9-c220-4f79-ae62-4153ec17ea81
topic_type:
- apiref
ms.openlocfilehash: fc406f6e87e5b2be48c6fe7d5fc988774ac5cd11
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379992"
---
# <a name="icordebugtypegetbase-method"></a><span data-ttu-id="5bfcf-102">ICorDebugType::GetBase 方法</span><span class="sxs-lookup"><span data-stu-id="5bfcf-102">ICorDebugType::GetBase Method</span></span>
<span data-ttu-id="5bfcf-103">取得 ICorDebugType 的介面指標，表示這個所表示之類型的基底類型（如果有的話） `ICorDebugType` 。</span><span class="sxs-lookup"><span data-stu-id="5bfcf-103">Gets an interface pointer to an ICorDebugType that represents the base type, if one exists, of the type represented by this `ICorDebugType`.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="5bfcf-104">語法</span><span class="sxs-lookup"><span data-stu-id="5bfcf-104">Syntax</span></span>  
  
```cpp  
HRESULT GetBase (  
    [out] ICorDebugType   **pBase  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="5bfcf-105">參數</span><span class="sxs-lookup"><span data-stu-id="5bfcf-105">Parameters</span></span>  
 `pBase`  
 <span data-ttu-id="5bfcf-106">脫銷`ICorDebugType`代表基底類型之物件位址的指標。</span><span class="sxs-lookup"><span data-stu-id="5bfcf-106">[out] A pointer to the address of an `ICorDebugType` object that represents the base type.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="5bfcf-107">備註</span><span class="sxs-lookup"><span data-stu-id="5bfcf-107">Remarks</span></span>  
 <span data-ttu-id="5bfcf-108">查閱類型的基底類型對於執行一般偵錯工具功能很有用，例如，列印出物件或其父類別的所有欄位。</span><span class="sxs-lookup"><span data-stu-id="5bfcf-108">Looking up the base type for a type is useful to implement common debugger functionality, such as printing out all the fields of an object or its parent classes.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="5bfcf-109">需求</span><span class="sxs-lookup"><span data-stu-id="5bfcf-109">Requirements</span></span>  
 <span data-ttu-id="5bfcf-110">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="5bfcf-110">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="5bfcf-111">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="5bfcf-111">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="5bfcf-112">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="5bfcf-112">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="5bfcf-113">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="5bfcf-113">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>
