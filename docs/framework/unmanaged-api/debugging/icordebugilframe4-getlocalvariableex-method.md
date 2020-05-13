---
title: ICorDebugILFrame4::GetLocalVariableEx 方法
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICorDebugILFrame4.GetCodeEx
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 0c8676f8-ca0d-4998-b64d-fefac7e38912
topic_type:
- apiref
ms.openlocfilehash: 8d6ef550309ea7f8bae616a5f7e5c41b4f07374a
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213721"
---
# <a name="icordebugilframe4getlocalvariableex-method"></a><span data-ttu-id="a7da4-102">ICorDebugILFrame4::GetLocalVariableEx 方法</span><span class="sxs-lookup"><span data-stu-id="a7da4-102">ICorDebugILFrame4::GetLocalVariableEx Method</span></span>
<span data-ttu-id="a7da4-103">[.NET Framework 4.5.2 與更新版本提供支援]</span><span class="sxs-lookup"><span data-stu-id="a7da4-103">[Supported in the .NET Framework 4.5.2 and later versions]</span></span>  
  
 <span data-ttu-id="a7da4-104">從此中繼語言 (IL) 堆疊框架中取得指定區域變數的值，並選擇是否要存取加入分析工具 ReJIT 測試設備中的變數。</span><span class="sxs-lookup"><span data-stu-id="a7da4-104">Gets the value of the specified local variable in this intermediate language (IL) stack frame, and optionally accesses a variable added in profiler ReJIT instrumentation.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="a7da4-105">語法</span><span class="sxs-lookup"><span data-stu-id="a7da4-105">Syntax</span></span>  
  
```cpp
HRESULT GetLocalVariableEx(  
   [in] ILCodeKind flags,
   [in] DWORD dwIndex,
   [out] ICorDebugValue **ppValue  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="a7da4-106">參數</span><span class="sxs-lookup"><span data-stu-id="a7da4-106">Parameters</span></span>  
 `flags`  
 <span data-ttu-id="a7da4-107">在[ILCodeKind](ilcodekind-enumeration.md)列舉成員，指定在 profiler ReJIT 檢測中加入的變數是否包含在框架中。</span><span class="sxs-lookup"><span data-stu-id="a7da4-107">[in] An [ILCodeKind](ilcodekind-enumeration.md) enumeration member that specifies whether a variable added in profiler ReJIT instrumentation is included in the frame.</span></span>  
  
 `dwIndex`  
 <span data-ttu-id="a7da4-108">[in] IL 堆疊框架中之區域變數的索引。</span><span class="sxs-lookup"><span data-stu-id="a7da4-108">[in] The index of the local variable in the IL stack frame.</span></span>  
  
 `ppValue`  
 <span data-ttu-id="a7da4-109">脫銷代表所抓取值之 "ICorDebugValue" 物件位址的指標。</span><span class="sxs-lookup"><span data-stu-id="a7da4-109">[out] A pointer to the address of an "ICorDebugValue" object that represents the retrieved value.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="a7da4-110">備註</span><span class="sxs-lookup"><span data-stu-id="a7da4-110">Remarks</span></span>  
 <span data-ttu-id="a7da4-111">這個方法類似于[GetLocalVariable](icordebugilframe-getlocalvariable-method.md)方法，不同之處在于它會選擇性地存取在 profiler ReJIT 檢測中加入的變數。</span><span class="sxs-lookup"><span data-stu-id="a7da4-111">This method is similar to the [GetLocalVariable](icordebugilframe-getlocalvariable-method.md) method, except that it optionally accesses a variable added in profiler ReJIT instrumentation.</span></span> <span data-ttu-id="a7da4-112">使用的值呼叫此方法 `flags` `ILCODE_ORIGINAL_IL` 相當於呼叫[GetLocalVariable](icordebugilframe-getlocalvariable-method.md); 如果方法是以其他區域變數檢測，則無法存取這些變數。</span><span class="sxs-lookup"><span data-stu-id="a7da4-112">Calling this method with a `flags` value of `ILCODE_ORIGINAL_IL` is equivalent to calling [GetLocalVariable](icordebugilframe-getlocalvariable-method.md); if the method is instrumented with additional local variables, those variables cannot be accessed.</span></span> <span data-ttu-id="a7da4-113">`ILCODE_REJIT_IL` 允許偵錯程式存取加入分析工具 ReJIT 測試設備中的區域變數。</span><span class="sxs-lookup"><span data-stu-id="a7da4-113">`ILCODE_REJIT_IL` allows the debugger to access the local variables added in profiler ReJIT instrumentation.</span></span> <span data-ttu-id="a7da4-114">若測試設備不是 IL，此方法會傳回 `E_INVALIDARG`。</span><span class="sxs-lookup"><span data-stu-id="a7da4-114">If the IL is not instrumented, the method returns `E_INVALIDARG`.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="a7da4-115">需求</span><span class="sxs-lookup"><span data-stu-id="a7da4-115">Requirements</span></span>  
 <span data-ttu-id="a7da4-116">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="a7da4-116">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="a7da4-117">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="a7da4-117">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="a7da4-118">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="a7da4-118">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="a7da4-119">**.NET Framework 版本：**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="a7da4-119">**.NET Framework Versions:** [!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a7da4-120">請參閱</span><span class="sxs-lookup"><span data-stu-id="a7da4-120">See also</span></span>

- [<span data-ttu-id="a7da4-121">ICorDebugILFrame4 介面</span><span class="sxs-lookup"><span data-stu-id="a7da4-121">ICorDebugILFrame4 Interface</span></span>](icordebugilframe4-interface.md)
- [<span data-ttu-id="a7da4-122">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="a7da4-122">Debugging Interfaces</span></span>](debugging-interfaces.md)
- [<span data-ttu-id="a7da4-123">ReJIT：使用說明指南</span><span class="sxs-lookup"><span data-stu-id="a7da4-123">ReJIT: A How-To Guide</span></span>](https://docs.microsoft.com/archive/blogs/davbr/rejit-a-how-to-guide)
