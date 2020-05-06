---
title: ICLRDataTarget3::GetExceptionRecord 方法
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICLRDataTarget3.GetExceptionRecord
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 6643c2af-2ee6-4789-aa25-1d8eaf500c94
topic_type:
- apiref
ms.openlocfilehash: 0ea4546dcde4afa0a9db2e64ae34415d0973391b
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2020
ms.locfileid: "82860433"
---
# <a name="iclrdatatarget3getexceptionrecord-method"></a><span data-ttu-id="2e92b-102">ICLRDataTarget3::GetExceptionRecord 方法</span><span class="sxs-lookup"><span data-stu-id="2e92b-102">ICLRDataTarget3::GetExceptionRecord Method</span></span>
<span data-ttu-id="2e92b-103">由通用語言執行平台 (CLR) 資料存取服務呼叫，用於擷取與目標處理序相關聯的例外狀況記錄。</span><span class="sxs-lookup"><span data-stu-id="2e92b-103">Called by the common language runtime (CLR) data access services to retrieve the exception record associated with the target process.</span></span> <span data-ttu-id="2e92b-104">例如，針對傾印目標，這等同于透過`ExceptionParam`引數傳遞至 Windows Debug Help Library （DbgHelp）中[MiniDumpWriteDump](/windows/desktop/api/minidumpapiset/nf-minidumpapiset-minidumpwritedump)函式的例外狀況記錄。</span><span class="sxs-lookup"><span data-stu-id="2e92b-104">For example, for a dump target, this would be equivalent to the exception record passed in via the `ExceptionParam` argument to the [MiniDumpWriteDump](/windows/desktop/api/minidumpapiset/nf-minidumpapiset-minidumpwritedump) function in the Windows Debug Help Library (DbgHelp).</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="2e92b-105">語法</span><span class="sxs-lookup"><span data-stu-id="2e92b-105">Syntax</span></span>  
  
```cpp  
HRESULT GetExceptionRecord(  
    [in] ULONG32 bufferSize,  
    [out] ULONG32* bufferUsed,  
    [out, size_is(bufferSize] BYTE* buffer  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="2e92b-106">參數</span><span class="sxs-lookup"><span data-stu-id="2e92b-106">Parameters</span></span>  
 `bufferSize`  
 <span data-ttu-id="2e92b-107">[in] 輸入緩衝區大小 (位元組)。</span><span class="sxs-lookup"><span data-stu-id="2e92b-107">[in] The input buffer size, in bytes.</span></span> <span data-ttu-id="2e92b-108">這必須等於`sizeof(` [MINIDUMP_EXCEPTION](/windows/win32/api/minidumpapiset/ns-minidumpapiset-minidump_exception)`)`。</span><span class="sxs-lookup"><span data-stu-id="2e92b-108">This must be equal to `sizeof(`[MINIDUMP_EXCEPTION](/windows/win32/api/minidumpapiset/ns-minidumpapiset-minidump_exception)`)`.</span></span>  
  
 `bufferUsed`  
 <span data-ttu-id="2e92b-109">[out] `ULONG32` 類型的指標，此類型會接收實際寫入緩衝區的位元組數目。</span><span class="sxs-lookup"><span data-stu-id="2e92b-109">[out] A pointer to a `ULONG32` type that receives the number of bytes actually written to the buffer.</span></span>  
  
 `buffer`  
 <span data-ttu-id="2e92b-110">[out] 接收例外狀況記錄複本之記憶體緩衝區的指標。</span><span class="sxs-lookup"><span data-stu-id="2e92b-110">[out] A pointer to a memory buffer that receives a copy of the exception record.</span></span> <span data-ttu-id="2e92b-111">例外狀況記錄會以[MINIDUMP_EXCEPTION](/windows/win32/api/minidumpapiset/ns-minidumpapiset-minidump_exception)類型的形式傳回。</span><span class="sxs-lookup"><span data-stu-id="2e92b-111">The exception record is returned as a [MINIDUMP_EXCEPTION](/windows/win32/api/minidumpapiset/ns-minidumpapiset-minidump_exception) type.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="2e92b-112">傳回值</span><span class="sxs-lookup"><span data-stu-id="2e92b-112">Return Value</span></span>  
 <span data-ttu-id="2e92b-113">如果成功，傳回值為 `S_OK`，如果失敗，則傳回失敗 `HRESULT` 程式碼。</span><span class="sxs-lookup"><span data-stu-id="2e92b-113">The return value is `S_OK` on success, or a failure `HRESULT` code on failure.</span></span> <span data-ttu-id="2e92b-114">`HRESULT` 程式碼可以包括 (但不限於) 下列項目：</span><span class="sxs-lookup"><span data-stu-id="2e92b-114">The `HRESULT` codes can include but are not limited to the following:</span></span>  
  
|<span data-ttu-id="2e92b-115">傳回碼</span><span class="sxs-lookup"><span data-stu-id="2e92b-115">Return code</span></span>|<span data-ttu-id="2e92b-116">描述</span><span class="sxs-lookup"><span data-stu-id="2e92b-116">Description</span></span>|  
|-----------------|-----------------|  
|`S_OK`|<span data-ttu-id="2e92b-117">方法成功。</span><span class="sxs-lookup"><span data-stu-id="2e92b-117">Method succeeded.</span></span> <span data-ttu-id="2e92b-118">例外狀況記錄已複製到輸出緩衝區。</span><span class="sxs-lookup"><span data-stu-id="2e92b-118">The exception record has been copied to the output buffer.</span></span>|  
|`HRESULT_FROM_WIN32(ERROR_NOT_FOUND)`|<span data-ttu-id="2e92b-119">沒有與目標相關聯的例外狀況記錄。</span><span class="sxs-lookup"><span data-stu-id="2e92b-119">No exception record is associated with the target.</span></span>|  
|`HRESULT_FROM_WIN32(ERROR_BAD_LENGTH)`|<span data-ttu-id="2e92b-120">輸入緩衝區大小等於 `sizeof(MINIDUMP_EXCEPTION)`。</span><span class="sxs-lookup"><span data-stu-id="2e92b-120">The input buffer size is not equal to `sizeof(MINIDUMP_EXCEPTION)`.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="2e92b-121">備註</span><span class="sxs-lookup"><span data-stu-id="2e92b-121">Remarks</span></span>  
 <span data-ttu-id="2e92b-122">[MINIDUMP_EXCEPTION](/windows/win32/api/minidumpapiset/ns-minidumpapiset-minidump_exception)是在 Windows SDK 中定義于 dbghelp 和 imagehlp.dll 中的結構。</span><span class="sxs-lookup"><span data-stu-id="2e92b-122">[MINIDUMP_EXCEPTION](/windows/win32/api/minidumpapiset/ns-minidumpapiset-minidump_exception) is a structure defined in dbghelp.h and imagehlp.h in the Windows SDK.</span></span>  
  
 <span data-ttu-id="2e92b-123">此方法是由偵錯應用程式的作者來實作。</span><span class="sxs-lookup"><span data-stu-id="2e92b-123">This method is implemented by the writer of the debugging application.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="2e92b-124">需求</span><span class="sxs-lookup"><span data-stu-id="2e92b-124">Requirements</span></span>  
 <span data-ttu-id="2e92b-125">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="2e92b-125">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="2e92b-126">**標頭：** ClrData .idl，ClrData。h</span><span class="sxs-lookup"><span data-stu-id="2e92b-126">**Header:** ClrData.idl, ClrData.h</span></span>  
  
 <span data-ttu-id="2e92b-127">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="2e92b-127">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="2e92b-128">**.NET Framework 版本：**[!INCLUDE[v451_update](../../../../includes/net-current-v451-nov-plus.md)]</span><span class="sxs-lookup"><span data-stu-id="2e92b-128">**.NET Framework Versions:** [!INCLUDE[v451_update](../../../../includes/net-current-v451-nov-plus.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="2e92b-129">請參閱</span><span class="sxs-lookup"><span data-stu-id="2e92b-129">See also</span></span>

- [<span data-ttu-id="2e92b-130">ICLRDataTarget3 介面</span><span class="sxs-lookup"><span data-stu-id="2e92b-130">ICLRDataTarget3 Interface</span></span>](iclrdatatarget3-interface.md)
- [<span data-ttu-id="2e92b-131">GetExceptionContextRecord 方法</span><span class="sxs-lookup"><span data-stu-id="2e92b-131">GetExceptionContextRecord Method</span></span>](iclrdatatarget3-getexceptioncontextrecord-method.md)
- [<span data-ttu-id="2e92b-132">GetExceptionThreadID 方法</span><span class="sxs-lookup"><span data-stu-id="2e92b-132">GetExceptionThreadID Method</span></span>](iclrdatatarget3-getexceptionthreadid-method.md)
