---
title: ICLRDataTarget::GetTLSValue 方法
ms.date: 03/30/2017
api_name:
- ICLRDataTarget.GetTLSValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDataTarget::GetTLSValue
helpviewer_keywords:
- GetTLSValue method [.NET Framework debugging]
- ICLRDataTarget::GetTLSValue method [.NET Framework debugging]
ms.assetid: 0d8a7730-edc9-4728-898f-41b219cf5a28
topic_type:
- apiref
ms.openlocfilehash: f6066774961b3fba2c466e156296907efc2e53df
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95703404"
---
# <a name="iclrdatatargetgettlsvalue-method"></a><span data-ttu-id="fac01-102">ICLRDataTarget::GetTLSValue 方法</span><span class="sxs-lookup"><span data-stu-id="fac01-102">ICLRDataTarget::GetTLSValue Method</span></span>

<span data-ttu-id="fac01-103">從執行緒區域儲存區取得值， (目標進程中指定之執行緒的 TLS) 。</span><span class="sxs-lookup"><span data-stu-id="fac01-103">Gets a value from the thread local storage (TLS) of the specified thread in the target process.</span></span> <span data-ttu-id="fac01-104">Common language runtime (CLR) 資料存取服務會呼叫這個方法。</span><span class="sxs-lookup"><span data-stu-id="fac01-104">This method is called by the common language runtime (CLR) data access services.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="fac01-105">語法</span><span class="sxs-lookup"><span data-stu-id="fac01-105">Syntax</span></span>  
  
```cpp  
HRESULT GetTLSValue (  
    [in] ULONG32            threadID,  
    [in] ULONG32            index,  
    [out] CLRDATA_ADDRESS   *value  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="fac01-106">參數</span><span class="sxs-lookup"><span data-stu-id="fac01-106">Parameters</span></span>  

 `threadID`  
 <span data-ttu-id="fac01-107">在目標進程中線程的作業系統識別碼。</span><span class="sxs-lookup"><span data-stu-id="fac01-107">[in] The operating system identifier of a thread in the target process.</span></span>  
  
 `index`  
 <span data-ttu-id="fac01-108">在位置的索引。</span><span class="sxs-lookup"><span data-stu-id="fac01-108">[in] The index of the location.</span></span> <span data-ttu-id="fac01-109">在指定之執行緒的本機存放區中，此值必須是有效的索引。</span><span class="sxs-lookup"><span data-stu-id="fac01-109">This value must be a valid index in the local store of the specified thread.</span></span>  
  
 `value`  
 <span data-ttu-id="fac01-110">擴展 `CLRDATA_ADDRESS` 值的指標，指定從指定的 TLS 位置傳回的值。</span><span class="sxs-lookup"><span data-stu-id="fac01-110">[out] A pointer to a `CLRDATA_ADDRESS` value that specifies the value returned from the given TLS location.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="fac01-111">備註</span><span class="sxs-lookup"><span data-stu-id="fac01-111">Remarks</span></span>  

 <span data-ttu-id="fac01-112">此方法是由偵錯應用程式的作者來實作。</span><span class="sxs-lookup"><span data-stu-id="fac01-112">This method is implemented by the writer of the debugging application.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="fac01-113">需求</span><span class="sxs-lookup"><span data-stu-id="fac01-113">Requirements</span></span>  

 <span data-ttu-id="fac01-114">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="fac01-114">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="fac01-115">**標頭：** ClrData .idl、ClrData。h</span><span class="sxs-lookup"><span data-stu-id="fac01-115">**Header:** ClrData.idl, ClrData.h</span></span>  
  
 <span data-ttu-id="fac01-116">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="fac01-116">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="fac01-117">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="fac01-117">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="fac01-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fac01-118">See also</span></span>

- [<span data-ttu-id="fac01-119">ICLRDataTarget 介面</span><span class="sxs-lookup"><span data-stu-id="fac01-119">ICLRDataTarget Interface</span></span>](iclrdatatarget-interface.md)
