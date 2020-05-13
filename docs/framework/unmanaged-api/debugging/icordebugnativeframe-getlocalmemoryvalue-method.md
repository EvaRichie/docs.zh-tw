---
title: ICorDebugNativeFrame::GetLocalMemoryValue 方法
ms.date: 03/30/2017
api_name:
- ICorDebugNativeFrame.GetLocalMemoryValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugNativeFrame::GetLocalMemoryValue
helpviewer_keywords:
- GetLocalMemoryValue method [.NET Framework debugging]
- ICorDebugNativeFrame::GetLocalMemoryValue method [.NET Framework debugging]
ms.assetid: b600b3a2-9908-42d8-8093-ab6f39e9a2c9
topic_type:
- apiref
ms.openlocfilehash: 4c4bfe6a797fc1476ff53a8f2db4f80debc41f6b
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212434"
---
# <a name="icordebugnativeframegetlocalmemoryvalue-method"></a><span data-ttu-id="b83d7-102">ICorDebugNativeFrame::GetLocalMemoryValue 方法</span><span class="sxs-lookup"><span data-stu-id="b83d7-102">ICorDebugNativeFrame::GetLocalMemoryValue Method</span></span>
<span data-ttu-id="b83d7-103">取得在這個原生框架的指定記憶體位置中儲存之引數或區域變數的值。</span><span class="sxs-lookup"><span data-stu-id="b83d7-103">Gets the value of an argument or local variable that is stored in the specified memory location for this native frame.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="b83d7-104">語法</span><span class="sxs-lookup"><span data-stu-id="b83d7-104">Syntax</span></span>  
  
```cpp  
HRESULT GetLocalMemoryValue (  
    [in]  CORDB_ADDRESS      address,  
    [in]  ULONG              cbSigBlob,  
    [in]  PCCOR_SIGNATURE    pvSigBlob,  
    [out] ICorDebugValue     **ppValue  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="b83d7-105">參數</span><span class="sxs-lookup"><span data-stu-id="b83d7-105">Parameters</span></span>  
 `address`  
 <span data-ttu-id="b83d7-106">在`CORDB_ADDRESS`值，指定包含值的記憶體位置。</span><span class="sxs-lookup"><span data-stu-id="b83d7-106">[in] A `CORDB_ADDRESS` value that specifies the memory location containing the value.</span></span>  
  
 `cbSigBlob`  
 <span data-ttu-id="b83d7-107">在整數，指定參數所參考的二進位中繼資料簽章大小 `pvSigBlob` 。</span><span class="sxs-lookup"><span data-stu-id="b83d7-107">[in] An integer that specifies the size of the binary metadata signature which is referenced by the `pvSigBlob` parameter.</span></span>  
  
 `pvSigBlob`  
 <span data-ttu-id="b83d7-108">在`PCCOR_SIGNATURE`值，指向數值型別的二進位中繼資料簽章。</span><span class="sxs-lookup"><span data-stu-id="b83d7-108">[in] A `PCCOR_SIGNATURE` value that points to the binary metadata signature of the value's type.</span></span>  
  
 `ppValue`  
 <span data-ttu-id="b83d7-109">脫銷"ICorDebugValue" 物件位址的指標，代表儲存在指定記憶體位置的已抓取值。</span><span class="sxs-lookup"><span data-stu-id="b83d7-109">[out] A pointer to the address of an "ICorDebugValue" object representing the retrieved value that is stored in the specified memory location.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="b83d7-110">需求</span><span class="sxs-lookup"><span data-stu-id="b83d7-110">Requirements</span></span>  
 <span data-ttu-id="b83d7-111">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="b83d7-111">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="b83d7-112">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="b83d7-112">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="b83d7-113">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="b83d7-113">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="b83d7-114">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="b83d7-114">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b83d7-115">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b83d7-115">See also</span></span>
