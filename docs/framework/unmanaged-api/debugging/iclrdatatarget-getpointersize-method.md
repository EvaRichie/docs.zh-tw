---
title: ICLRDataTarget::GetPointerSize 方法
ms.date: 03/30/2017
api_name:
- ICLRDataTarget.GetPointerSize
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDataTarget::GetPointerSize
helpviewer_keywords:
- GetPointerSize method [.NET Framework debugging]
- ICLRDataTarget::GetPointerSize method [.NET Framework debugging]
ms.assetid: 51d9f4a4-81a7-4527-8537-5212bdb05c70
topic_type:
- apiref
ms.openlocfilehash: 077aa50465d99c9098f26e67b3852feb0d399142
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95703521"
---
# <a name="iclrdatatargetgetpointersize-method"></a><span data-ttu-id="ba621-102">ICLRDataTarget::GetPointerSize 方法</span><span class="sxs-lookup"><span data-stu-id="ba621-102">ICLRDataTarget::GetPointerSize Method</span></span>

<span data-ttu-id="ba621-103">取得目標進程使用之指標類型的大小（以位元組為單位）。</span><span class="sxs-lookup"><span data-stu-id="ba621-103">Gets the size, in bytes, of the pointer type that the target process uses.</span></span> <span data-ttu-id="ba621-104">Common language runtime 資料存取服務會呼叫這個方法。</span><span class="sxs-lookup"><span data-stu-id="ba621-104">This method is called by the common language runtime data access services.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="ba621-105">語法</span><span class="sxs-lookup"><span data-stu-id="ba621-105">Syntax</span></span>  
  
```cpp  
HRESULT GetPointerSize (  
    [out] ULONG32     *pointerSize  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="ba621-106">參數</span><span class="sxs-lookup"><span data-stu-id="ba621-106">Parameters</span></span>  

 `pointerSize`  
 <span data-ttu-id="ba621-107">擴展整數值的指標，指定目標進程上指標的大小（以位元組為單位）。</span><span class="sxs-lookup"><span data-stu-id="ba621-107">[out] A pointer to an integer value that specifies the size, in bytes, of a pointer on the target process.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="ba621-108">備註</span><span class="sxs-lookup"><span data-stu-id="ba621-108">Remarks</span></span>  

 <span data-ttu-id="ba621-109">此方法是由偵錯應用程式的作者來實作。</span><span class="sxs-lookup"><span data-stu-id="ba621-109">This method is implemented by the writer of the debugging application.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="ba621-110">需求</span><span class="sxs-lookup"><span data-stu-id="ba621-110">Requirements</span></span>  

 <span data-ttu-id="ba621-111">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="ba621-111">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="ba621-112">**標頭：** ClrData .idl、ClrData。h</span><span class="sxs-lookup"><span data-stu-id="ba621-112">**Header:** ClrData.idl, ClrData.h</span></span>  
  
 <span data-ttu-id="ba621-113">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="ba621-113">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="ba621-114">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="ba621-114">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ba621-115">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ba621-115">See also</span></span>

- [<span data-ttu-id="ba621-116">ICLRDataTarget 介面</span><span class="sxs-lookup"><span data-stu-id="ba621-116">ICLRDataTarget Interface</span></span>](iclrdatatarget-interface.md)
