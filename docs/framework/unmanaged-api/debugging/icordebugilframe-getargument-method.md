---
title: ICorDebugILFrame::GetArgument 方法
ms.date: 03/30/2017
api_name:
- ICorDebugILFrame.GetArgument
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugILFrame::GetArgument
helpviewer_keywords:
- GetArgument method [.NET Framework debugging]
- ICorDebugILFrame::GetArgument method [.NET Framework debugging]
ms.assetid: 4e2fd423-f643-4c27-ba5f-41b5ebc3b416
topic_type:
- apiref
ms.openlocfilehash: d17179dbeb9564b16c0c95a43502a53a67d3b9b8
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95703157"
---
# <a name="icordebugilframegetargument-method"></a><span data-ttu-id="09315-102">ICorDebugILFrame::GetArgument 方法</span><span class="sxs-lookup"><span data-stu-id="09315-102">ICorDebugILFrame::GetArgument Method</span></span>

<span data-ttu-id="09315-103">取得此 Microsoft 中繼語言 (MSIL) 堆疊框架中指定之引數的值。</span><span class="sxs-lookup"><span data-stu-id="09315-103">Gets the value of the specified argument in this Microsoft intermediate language (MSIL) stack frame.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="09315-104">語法</span><span class="sxs-lookup"><span data-stu-id="09315-104">Syntax</span></span>  
  
```cpp  
HRESULT GetArgument (  
    [in] DWORD                  dwIndex,  
    [out] ICorDebugValue        **ppValue  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="09315-105">參數</span><span class="sxs-lookup"><span data-stu-id="09315-105">Parameters</span></span>  

 `dwIndex`  
 <span data-ttu-id="09315-106">在這個 MSIL 堆疊框架中的引數索引。</span><span class="sxs-lookup"><span data-stu-id="09315-106">[in] The index of the argument in this MSIL stack frame.</span></span>  
  
 `ppValue`  
 <span data-ttu-id="09315-107">[out] 代表擷取值之 ICorDebugValue 物件的位置指標。</span><span class="sxs-lookup"><span data-stu-id="09315-107">[out] A pointer to the address of an ICorDebugValue object that represents the retrieved value.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="09315-108">備註</span><span class="sxs-lookup"><span data-stu-id="09315-108">Remarks</span></span>  

 <span data-ttu-id="09315-109">`GetArgument`方法可以在 MSIL 堆疊框架中或在即時 (JIT) 編譯的框架中使用。</span><span class="sxs-lookup"><span data-stu-id="09315-109">The `GetArgument` method can be used either in an MSIL stack frame or in a just-in-time (JIT) compiled frame.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="09315-110">需求</span><span class="sxs-lookup"><span data-stu-id="09315-110">Requirements</span></span>  

 <span data-ttu-id="09315-111">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="09315-111">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="09315-112">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="09315-112">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="09315-113">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="09315-113">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="09315-114">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="09315-114">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>
