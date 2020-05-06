---
title: EnumerateCLRs 函式
ms.date: 03/30/2017
api_name:
- EnumerateCLRs
api_location:
- dbgshim.dll
api_type:
- COM
f1_keywords:
- EnumerateCLRs
helpviewer_keywords:
- debugging API [Silverlight]
- Silverlight, debugging
- EnumerateCLRs function
ms.assetid: f8d50cb3-ec4f-4529-8fe3-bd61fd28e13c
topic_type:
- apiref
ms.openlocfilehash: 1f33fb98712939d1e687798547b784819f164d63
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2020
ms.locfileid: "82860718"
---
# <a name="enumerateclrs-function"></a><span data-ttu-id="9a135-102">EnumerateCLRs 函式</span><span class="sxs-lookup"><span data-stu-id="9a135-102">EnumerateCLRs Function</span></span>
<span data-ttu-id="9a135-103">提供在處理程序中列舉 CLRs 的機制。</span><span class="sxs-lookup"><span data-stu-id="9a135-103">Provides a mechanism for enumerating the CLRs in a process.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="9a135-104">語法</span><span class="sxs-lookup"><span data-stu-id="9a135-104">Syntax</span></span>  
  
```cpp  
HRESULT EnumerateCLRs (  
    [in]  DWORD      debuggeePID,  
    [out] HANDLE**   ppHandleArrayOut,  
    [out] LPWSTR**   ppStringArrayOut,  
    [out] DWORD*     pdwArrayLengthOut  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="9a135-105">參數</span><span class="sxs-lookup"><span data-stu-id="9a135-105">Parameters</span></span>  
 `debuggeePID`  
 <span data-ttu-id="9a135-106">[in] 將列舉從 CLRs 載入之程序的處理序識別碼。</span><span class="sxs-lookup"><span data-stu-id="9a135-106">[in] Process identifier of the process from which loaded CLRs will be enumerated.</span></span>  
  
 `ppHandleArrayOut`  
 <span data-ttu-id="9a135-107">[out] 使用於繼續 CLR 啟動，包含事件控制代碼的陣列的指標。</span><span class="sxs-lookup"><span data-stu-id="9a135-107">[out] Pointer to an array containing event handles that are used to continue a CLR startup.</span></span> <span data-ttu-id="9a135-108">不保證在陣列中的每個控點是有效的。</span><span class="sxs-lookup"><span data-stu-id="9a135-108">Each handle in the array is not guaranteed to be valid.</span></span> <span data-ttu-id="9a135-109">如果有效，控制代碼將做為相對應執行階段位於`ppStringArrayOut` 的相同索引中的繼續啟動事件。</span><span class="sxs-lookup"><span data-stu-id="9a135-109">If valid, the handle is to be used as the continue-startup event for the corresponding runtime located in the same index of `ppStringArrayOut`.</span></span>  
  
 `ppStringArrayOut`  
 <span data-ttu-id="9a135-110">[out] 處理序中載入 CLRs 的指定完整路徑的字串陣列的指標。</span><span class="sxs-lookup"><span data-stu-id="9a135-110">[out] Pointer to an array of strings that specify full paths to CLRs loaded in the process.</span></span>  
  
 `pdwArrayLengthOut`  
 <span data-ttu-id="9a135-111">[out] DWORD 指標，其中包含大小相等的 `ppHandleArrayOut` 和 `pdwArrayLengthOut` 長度。</span><span class="sxs-lookup"><span data-stu-id="9a135-111">[out] Pointer to a DWORD that contains the length of the equally sized `ppHandleArrayOut` and `pdwArrayLengthOut`.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="9a135-112">傳回值</span><span class="sxs-lookup"><span data-stu-id="9a135-112">Return Value</span></span>  
 <span data-ttu-id="9a135-113">S_OK</span><span class="sxs-lookup"><span data-stu-id="9a135-113">S_OK</span></span>  
 <span data-ttu-id="9a135-114">已成功確定處理序中的 CLR 數目，並且已正確填入對應的控制代碼和路徑陣列。</span><span class="sxs-lookup"><span data-stu-id="9a135-114">The number of CLRs in the process was successfully determined, and the corresponding handle and path arrays were properly filled.</span></span>  
  
 <span data-ttu-id="9a135-115">E_INVALIDARG</span><span class="sxs-lookup"><span data-stu-id="9a135-115">E_INVALIDARG</span></span>  
 <span data-ttu-id="9a135-116">可能是 `ppHandleArrayOut` 或 `ppStringArrayOut` 為 null，或 `pdwArrayLengthOut` 為 null。</span><span class="sxs-lookup"><span data-stu-id="9a135-116">Either `ppHandleArrayOut` or `ppStringArrayOut` is null, or `pdwArrayLengthOut` is null.</span></span>  
  
 <span data-ttu-id="9a135-117">E_OUTOFMEMORY</span><span class="sxs-lookup"><span data-stu-id="9a135-117">E_OUTOFMEMORY</span></span>  
 <span data-ttu-id="9a135-118">函式無法為控制代碼和路徑陣列配置足夠的記憶體。</span><span class="sxs-lookup"><span data-stu-id="9a135-118">The function is unable to allocate enough memory for the handle and path arrays.</span></span>  
  
 <span data-ttu-id="9a135-119">E_FAIL (或其他 E_ 傳回碼)</span><span class="sxs-lookup"><span data-stu-id="9a135-119">E_FAIL (or other E_ return codes)</span></span>  
 <span data-ttu-id="9a135-120">無法列舉載入的 CLRs。</span><span class="sxs-lookup"><span data-stu-id="9a135-120">Unable to enumerate loaded CLRs.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="9a135-121">備註</span><span class="sxs-lookup"><span data-stu-id="9a135-121">Remarks</span></span>  
 <span data-ttu-id="9a135-122">所識別之目標處理序 `debuggeePID`，此函式會傳回路徑的陣列，`ppStringArrayOut`，至 CLRs 載入到處理序；事件控制代碼陣列 `ppHandleArrayOut`，其中可能包含在相同的索引為 CLR 的繼續啟動事件；以及陣列的大小，`pdwArrayLengthOut`，指定 CLRs 載入的數目。</span><span class="sxs-lookup"><span data-stu-id="9a135-122">For a target process that is identified by `debuggeePID`, the function returns an array of paths, `ppStringArrayOut`, to CLRs loaded in the process; an array of event handles, `ppHandleArrayOut`, which may contain a continue-startup event for the CLR at the same index; and the size of the arrays, `pdwArrayLengthOut`, which specifies the number of CLRs that are loaded.</span></span>  
  
 <span data-ttu-id="9a135-123">在 Windows 作業系統上，`debuggeePID` 對應至 OS 處理序識別碼。</span><span class="sxs-lookup"><span data-stu-id="9a135-123">On the Windows operating system, `debuggeePID` maps to an OS process identifier.</span></span>  
  
 <span data-ttu-id="9a135-124">記憶體 `ppHandleArrayOut` 和 `ppStringArrayOut` 由此函式所配置。</span><span class="sxs-lookup"><span data-stu-id="9a135-124">The memory for `ppHandleArrayOut` and `ppStringArrayOut` are allocated by this function.</span></span> <span data-ttu-id="9a135-125">若要釋放配置的記憶體，您必須呼叫[CloseCLREnumeration](closeclrenumeration-function.md)函式。</span><span class="sxs-lookup"><span data-stu-id="9a135-125">To free the memory allocated, you must call [CloseCLREnumeration Function](closeclrenumeration-function.md).</span></span>  
  
 <span data-ttu-id="9a135-126">參數設定為 null 的兩個陣列都可以呼叫此函式，以傳回目標處理序中的 CLRs 計數。</span><span class="sxs-lookup"><span data-stu-id="9a135-126">This function can be called with both array parameters set to null in order to return the count of CLRs in the target process.</span></span> <span data-ttu-id="9a135-127">從這個計數，呼叫端可以推斷將建立的緩衝區大小：`(sizeof(HANDLE) * count) + (sizeof(LPWSTR) * count) + (sizeof(WCHAR*) * count * MAX_PATH)`。</span><span class="sxs-lookup"><span data-stu-id="9a135-127">From this count, a caller can infer the size of the buffer that will be created: `(sizeof(HANDLE) * count) + (sizeof(LPWSTR) * count) + (sizeof(WCHAR*) * count * MAX_PATH)`.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="9a135-128">需求</span><span class="sxs-lookup"><span data-stu-id="9a135-128">Requirements</span></span>  
 <span data-ttu-id="9a135-129">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="9a135-129">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="9a135-130">**標頭：** dbgshim。h</span><span class="sxs-lookup"><span data-stu-id="9a135-130">**Header:** dbgshim.h</span></span>  
  
 <span data-ttu-id="9a135-131">連結**庫：** dbgshim</span><span class="sxs-lookup"><span data-stu-id="9a135-131">**Library:** dbgshim.dll</span></span>  
  
 <span data-ttu-id="9a135-132">**.NET Framework 版本：** 3.5 SP1</span><span class="sxs-lookup"><span data-stu-id="9a135-132">**.NET Framework Versions:** 3.5 SP1</span></span>
