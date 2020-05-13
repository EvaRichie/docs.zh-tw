---
title: ICorDebugFrame::GetFunctionToken 方法
ms.date: 03/30/2017
api_name:
- ICorDebugFrame.GetFunctionToken
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugFrame::GetFunctionToken
helpviewer_keywords:
- ICorDebugFrame::GetFunctionToken method [.NET Framework debugging]
- GetFunctionToken method [.NET Framework debugging]
ms.assetid: a46925b3-3bf8-404f-9f30-a86ae41032c1
topic_type:
- apiref
ms.openlocfilehash: 6e214131aeb2d6d17ea4b0a730b5fc77428a7ca8
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213682"
---
# <a name="icordebugframegetfunctiontoken-method"></a><span data-ttu-id="ff427-102">ICorDebugFrame::GetFunctionToken 方法</span><span class="sxs-lookup"><span data-stu-id="ff427-102">ICorDebugFrame::GetFunctionToken Method</span></span>
<span data-ttu-id="ff427-103">取得包含與此堆疊框架相關聯之程式碼的函式的元資料標記。</span><span class="sxs-lookup"><span data-stu-id="ff427-103">Gets the metadata token for the function that contains the code associated with this stack frame.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="ff427-104">語法</span><span class="sxs-lookup"><span data-stu-id="ff427-104">Syntax</span></span>  
  
```cpp  
HRESULT GetFunctionToken (  
    [out] mdMethodDef        *pToken  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="ff427-105">參數</span><span class="sxs-lookup"><span data-stu-id="ff427-105">Parameters</span></span>  
 `pToken`  
 <span data-ttu-id="ff427-106">脫銷參考函式 `mdMethodDef` 中繼資料之標記的指標。</span><span class="sxs-lookup"><span data-stu-id="ff427-106">[out] A pointer to an `mdMethodDef` token that references the metadata for the function.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="ff427-107">需求</span><span class="sxs-lookup"><span data-stu-id="ff427-107">Requirements</span></span>  
 <span data-ttu-id="ff427-108">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="ff427-108">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="ff427-109">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="ff427-109">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="ff427-110">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="ff427-110">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="ff427-111">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="ff427-111">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>
