---
title: ICLRDataTarget3::GetExceptionContextRecord 方法
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICLRDataTarget3.GetContextRecord
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 66076ed5-f05c-4114-9788-94cb143abb8a
topic_type:
- apiref
ms.openlocfilehash: 87065b83e0b28eafdf5099f99fd188e2e21e7a12
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95723619"
---
# <a name="iclrdatatarget3getexceptioncontextrecord-method"></a><span data-ttu-id="dc2e8-102">ICLRDataTarget3::GetExceptionContextRecord 方法</span><span class="sxs-lookup"><span data-stu-id="dc2e8-102">ICLRDataTarget3::GetExceptionContextRecord Method</span></span>

<span data-ttu-id="dc2e8-103">由通用語言執行平台 (CLR) 資料存取服務呼叫，用於擷取與目標處理序相關聯的內容記錄。</span><span class="sxs-lookup"><span data-stu-id="dc2e8-103">Called by the common language runtime (CLR) data access services to retrieve the context record associated with the target process.</span></span> <span data-ttu-id="dc2e8-104">例如，針對傾印目標，這相當於透過 `ExceptionParam` Windows Debug Help Library 中 [MiniDumpWriteDump](/windows/desktop/api/minidumpapiset/nf-minidumpapiset-minidumpwritedump) 函式的引數傳入的內容記錄 (DbgHelp) 。</span><span class="sxs-lookup"><span data-stu-id="dc2e8-104">For example, for a dump target, this would be equivalent to the context record passed in via the `ExceptionParam` argument to the [MiniDumpWriteDump](/windows/desktop/api/minidumpapiset/nf-minidumpapiset-minidumpwritedump) function in the Windows Debug Help Library (DbgHelp).</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="dc2e8-105">語法</span><span class="sxs-lookup"><span data-stu-id="dc2e8-105">Syntax</span></span>  
  
```cpp  
HRESULT GetExceptionContextRecord(  
    [in] ULONG32 bufferSize,  
    [out] ULONG32* bufferUsed,  
    [out, size_is(bufferSize)] BYTE* buffer  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="dc2e8-106">參數</span><span class="sxs-lookup"><span data-stu-id="dc2e8-106">Parameters</span></span>  

 `bufferSize`  
 <span data-ttu-id="dc2e8-107">[in] 輸入緩衝區大小 (位元組)。</span><span class="sxs-lookup"><span data-stu-id="dc2e8-107">[in] The input buffer size, in bytes.</span></span> <span data-ttu-id="dc2e8-108">這必須夠大，以容納內容記錄。</span><span class="sxs-lookup"><span data-stu-id="dc2e8-108">This must be large enough to accommodate the context record.</span></span>  
  
 `bufferUsed`  
 <span data-ttu-id="dc2e8-109">[out] `ULONG32` 類型的指標，此類型會接收實際寫入緩衝區的位元組數目。</span><span class="sxs-lookup"><span data-stu-id="dc2e8-109">[out] A pointer to a `ULONG32` type that receives the number of bytes actually written to the buffer.</span></span>  
  
 `buffer`  
 <span data-ttu-id="dc2e8-110">[out] 接收內容記錄複本之記憶體緩衝區的指標。</span><span class="sxs-lookup"><span data-stu-id="dc2e8-110">[out] A pointer to a memory buffer that receives a copy of the context record.</span></span> <span data-ttu-id="dc2e8-111">例外狀況記錄會以 [內容](/windows/win32/api/winnt/ns-winnt-arm64_nt_context) 類型的形式傳回。</span><span class="sxs-lookup"><span data-stu-id="dc2e8-111">The exception record is returned as a [CONTEXT](/windows/win32/api/winnt/ns-winnt-arm64_nt_context) type.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="dc2e8-112">傳回值</span><span class="sxs-lookup"><span data-stu-id="dc2e8-112">Return Value</span></span>  

 <span data-ttu-id="dc2e8-113">如果成功，傳回值為 `S_OK`，如果失敗，則傳回失敗 `HRESULT` 程式碼。</span><span class="sxs-lookup"><span data-stu-id="dc2e8-113">The return value is `S_OK` on success, or a failure `HRESULT` code on failure.</span></span> <span data-ttu-id="dc2e8-114">`HRESULT` 程式碼可以包括 (但不限於) 下列項目：</span><span class="sxs-lookup"><span data-stu-id="dc2e8-114">The `HRESULT` codes can include but are not limited to the following:</span></span>  
  
|<span data-ttu-id="dc2e8-115">傳回碼</span><span class="sxs-lookup"><span data-stu-id="dc2e8-115">Return code</span></span>|<span data-ttu-id="dc2e8-116">描述</span><span class="sxs-lookup"><span data-stu-id="dc2e8-116">Description</span></span>|  
|-----------------|-----------------|  
|`S_OK`|<span data-ttu-id="dc2e8-117">方法成功。</span><span class="sxs-lookup"><span data-stu-id="dc2e8-117">Method succeeded.</span></span> <span data-ttu-id="dc2e8-118">內容記錄已複製到輸出緩衝區。</span><span class="sxs-lookup"><span data-stu-id="dc2e8-118">The context record has been copied to the output buffer.</span></span>|  
|`HRESULT_FROM_WIN32(ERROR_NOT_FOUND)`|<span data-ttu-id="dc2e8-119">沒有與目標相關聯的內容記錄。</span><span class="sxs-lookup"><span data-stu-id="dc2e8-119">No context record is associated with the target.</span></span>|  
|`HRESULT_FROM_WIN32(ERROR_BAD_LENGTH)`|<span data-ttu-id="dc2e8-120">輸入緩衝區大小不夠大，無法容納內容記錄。</span><span class="sxs-lookup"><span data-stu-id="dc2e8-120">The input buffer size is not large enough to accommodate the context record.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="dc2e8-121">備註</span><span class="sxs-lookup"><span data-stu-id="dc2e8-121">Remarks</span></span>  

 <span data-ttu-id="dc2e8-122">[內容](/windows/win32/api/winnt/ns-winnt-arm64_nt_context) 是在 Windows SDK 所提供的標頭中定義的平臺特定結構。</span><span class="sxs-lookup"><span data-stu-id="dc2e8-122">[CONTEXT](/windows/win32/api/winnt/ns-winnt-arm64_nt_context) is a platform-specific structure defined in headers provided by the Windows SDK.</span></span>  
  
 <span data-ttu-id="dc2e8-123">此方法是由偵錯應用程式的作者來實作。</span><span class="sxs-lookup"><span data-stu-id="dc2e8-123">This method is implemented by the writer of the debugging application.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="dc2e8-124">需求</span><span class="sxs-lookup"><span data-stu-id="dc2e8-124">Requirements</span></span>  

 <span data-ttu-id="dc2e8-125">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="dc2e8-125">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="dc2e8-126">**標頭：** ClrData .idl、ClrData。h</span><span class="sxs-lookup"><span data-stu-id="dc2e8-126">**Header:** ClrData.idl, ClrData.h</span></span>  
  
 <span data-ttu-id="dc2e8-127">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="dc2e8-127">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="dc2e8-128">**.NET Framework 版本：**[!INCLUDE[v451_update](../../../../includes/net-current-v451-nov-plus.md)]</span><span class="sxs-lookup"><span data-stu-id="dc2e8-128">**.NET Framework Versions:** [!INCLUDE[v451_update](../../../../includes/net-current-v451-nov-plus.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="dc2e8-129">另請參閱</span><span class="sxs-lookup"><span data-stu-id="dc2e8-129">See also</span></span>

- [<span data-ttu-id="dc2e8-130">ICLRDataTarget3 介面</span><span class="sxs-lookup"><span data-stu-id="dc2e8-130">ICLRDataTarget3 Interface</span></span>](iclrdatatarget3-interface.md)
- [<span data-ttu-id="dc2e8-131">GetExceptionRecord 方法</span><span class="sxs-lookup"><span data-stu-id="dc2e8-131">GetExceptionRecord Method</span></span>](iclrdatatarget3-getexceptionrecord-method.md)
- [<span data-ttu-id="dc2e8-132">GetExceptionThreadID 方法</span><span class="sxs-lookup"><span data-stu-id="dc2e8-132">GetExceptionThreadID Method</span></span>](iclrdatatarget3-getexceptionthreadid-method.md)
