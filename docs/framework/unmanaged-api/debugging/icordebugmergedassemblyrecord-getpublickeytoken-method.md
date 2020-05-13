---
title: ICorDebugMergedAssemblyRecord::GetPublicKey 方法
ms.date: 03/30/2017
ms.assetid: 72020b72-9611-4bc3-b1e7-5a16b023bfa3
ms.openlocfilehash: 4cd0ff788401a7b5d70e215209194c0eb6cad1f8
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212109"
---
# <a name="icordebugmergedassemblyrecordgetpublickeytoken-method"></a><span data-ttu-id="b5d6a-102">ICorDebugMergedAssemblyRecord::GetPublicKey 方法</span><span class="sxs-lookup"><span data-stu-id="b5d6a-102">ICorDebugMergedAssemblyRecord::GetPublicKeyToken Method</span></span>
<span data-ttu-id="b5d6a-103">取得組件的公開金鑰語彙基元。</span><span class="sxs-lookup"><span data-stu-id="b5d6a-103">Gets the assembly's public key token.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="b5d6a-104">語法</span><span class="sxs-lookup"><span data-stu-id="b5d6a-104">Syntax</span></span>  
  
```cpp  
HRESULT GetPublicKeyToken(  
   [in] ULONG32 cbPublicKeyToken,
   [out] ULONG32 *pcbPublicKeyToken,
   [out, size_is(cbPublicKeyToken), length_is(*pcbPublicKeyToken)] BYTE pbPublicKeyToken[]  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="b5d6a-105">參數</span><span class="sxs-lookup"><span data-stu-id="b5d6a-105">Parameters</span></span>  
 `cbPublicKeyToken`  
 <span data-ttu-id="b5d6a-106">[in] `pbPublicKeyToken` 陣列中的最大位元組數。</span><span class="sxs-lookup"><span data-stu-id="b5d6a-106">[in] The maximum number of bytes in the `pbPublicKeyToken` array.</span></span>  
  
 `pcbPublicKeyToken`  
 <span data-ttu-id="b5d6a-107">[out] 寫入 `pbPublicKeyToken` 陣列之實際位元組數的指標。</span><span class="sxs-lookup"><span data-stu-id="b5d6a-107">[out] A pointer to the actual number of bytes written to the `pbPublicKeyToken` array.</span></span>  
  
 `pbPublicKeyToken`  
 <span data-ttu-id="b5d6a-108">[out] 包含組件公開金鑰語彙基元之位元組陣列的指標。</span><span class="sxs-lookup"><span data-stu-id="b5d6a-108">[out] A pointer to a byte array that contains the assembly's public key token.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="b5d6a-109">備註</span><span class="sxs-lookup"><span data-stu-id="b5d6a-109">Remarks</span></span>  
 <span data-ttu-id="b5d6a-110">組件的公開金鑰語彙基元是其公開金鑰之 SHA1 雜湊的最後 8 個位元組。</span><span class="sxs-lookup"><span data-stu-id="b5d6a-110">An assembly's public key token is the last eight bytes of a SHA1 hash of its public key.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="b5d6a-111">這個方法僅適用於 .NET Native。</span><span class="sxs-lookup"><span data-stu-id="b5d6a-111">This method is available with .NET Native only.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="b5d6a-112">需求</span><span class="sxs-lookup"><span data-stu-id="b5d6a-112">Requirements</span></span>  
 <span data-ttu-id="b5d6a-113">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="b5d6a-113">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="b5d6a-114">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="b5d6a-114">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="b5d6a-115">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="b5d6a-115">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="b5d6a-116">**.NET Framework 版本：**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span><span class="sxs-lookup"><span data-stu-id="b5d6a-116">**.NET Framework Versions:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b5d6a-117">請參閱</span><span class="sxs-lookup"><span data-stu-id="b5d6a-117">See also</span></span>

- [<span data-ttu-id="b5d6a-118">ICorDebugMergedAssemblyRecord 介面</span><span class="sxs-lookup"><span data-stu-id="b5d6a-118">ICorDebugMergedAssemblyRecord Interface</span></span>](icordebugmergedassemblyrecord-interface.md)
- [<span data-ttu-id="b5d6a-119">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="b5d6a-119">Debugging Interfaces</span></span>](debugging-interfaces.md)
