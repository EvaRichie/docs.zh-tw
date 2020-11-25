---
title: ICorDebugILCode2::GetLocalVarSigToken 方法
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICorDebugILCode2.GetLocalVarSigToken
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 17665b77-1342-4115-94fd-9f45b0ecfb0f
topic_type:
- apiref
ms.openlocfilehash: 33533c9e3bfbe78abeddb5ed591f741219826127
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95728628"
---
# <a name="icordebugilcode2getlocalvarsigtoken-method"></a><span data-ttu-id="a53f2-102">ICorDebugILCode2::GetLocalVarSigToken 方法</span><span class="sxs-lookup"><span data-stu-id="a53f2-102">ICorDebugILCode2::GetLocalVarSigToken Method</span></span>

<span data-ttu-id="a53f2-103">[.NET Framework 4.5.2 與更新版本提供支援]</span><span class="sxs-lookup"><span data-stu-id="a53f2-103">[Supported in the .NET Framework 4.5.2 and later versions]</span></span>  
  
 <span data-ttu-id="a53f2-104">針對此執行個體表示的函式，取得區域變數簽章的中繼資料語彙基元。</span><span class="sxs-lookup"><span data-stu-id="a53f2-104">Gets the metadata token for the local variable signature for the function that is represented by this instance.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="a53f2-105">語法</span><span class="sxs-lookup"><span data-stu-id="a53f2-105">Syntax</span></span>  
  
```cpp
HRESULT GetLocalVarSigToken(  
   [out] mdSignature *pmdSig  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="a53f2-106">參數</span><span class="sxs-lookup"><span data-stu-id="a53f2-106">Parameters</span></span>  

 `pmdSig`  
 <span data-ttu-id="a53f2-107">[out] 針對此函式的區域變數簽章，指向 `mdSignature` 語彙基元的指標，如果沒有簽章 (意即，如果函式沒有任何區域變數)，則指向 `mdSignatureNil`。</span><span class="sxs-lookup"><span data-stu-id="a53f2-107">[out] A pointer to the `mdSignature` token for the local variable signature for this function, or `mdSignatureNil` if there is no signature (that is, if the function doesn't have any local variables).</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="a53f2-108">備註</span><span class="sxs-lookup"><span data-stu-id="a53f2-108">Remarks</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="a53f2-109">需求</span><span class="sxs-lookup"><span data-stu-id="a53f2-109">Requirements</span></span>  

 <span data-ttu-id="a53f2-110">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="a53f2-110">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="a53f2-111">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="a53f2-111">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="a53f2-112">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="a53f2-112">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="a53f2-113">**.NET Framework 版本：**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="a53f2-113">**.NET Framework Versions:** [!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a53f2-114">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a53f2-114">See also</span></span>

- [<span data-ttu-id="a53f2-115">ICorDebugILCode2 介面</span><span class="sxs-lookup"><span data-stu-id="a53f2-115">ICorDebugILCode2 Interface</span></span>](icordebugilcode2-interface.md)
- [<span data-ttu-id="a53f2-116">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="a53f2-116">Debugging Interfaces</span></span>](debugging-interfaces.md)
