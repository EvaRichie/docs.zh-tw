---
title: CorPinvokeMap 列舉
ms.date: 03/30/2017
api_name:
- CorPinvokeMap
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorPinvokeMap
helpviewer_keywords:
- CorPinvokeMap enumeration [.NET Framework metadata]
ms.assetid: f14f986e-f6ce-42bc-aa23-18150c46d28c
topic_type:
- apiref
ms.openlocfilehash: da3ee54b1c3361149c11a9cfad8bdb07a5007ecf
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95706134"
---
# <a name="corpinvokemap-enumeration"></a><span data-ttu-id="340a9-102">CorPinvokeMap 列舉</span><span class="sxs-lookup"><span data-stu-id="340a9-102">CorPinvokeMap Enumeration</span></span>

<span data-ttu-id="340a9-103">指定 PInvoke 呼叫的選項。</span><span class="sxs-lookup"><span data-stu-id="340a9-103">Specifies options for a PInvoke call.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="340a9-104">語法</span><span class="sxs-lookup"><span data-stu-id="340a9-104">Syntax</span></span>  
  
```cpp  
typedef enum  CorPinvokeMap {  
  
    pmNoMangle          = 0x0001,  
  
    pmCharSetMask       = 0x0006,  
    pmCharSetNotSpec    = 0x0000,  
    pmCharSetAnsi       = 0x0002,  
    pmCharSetUnicode    = 0x0004,  
    pmCharSetAuto       = 0x0006,  
  
    pmBestFitUseAssem   = 0x0000,  
    pmBestFitEnabled    = 0x0010,  
    pmBestFitDisabled   = 0x0020,  
    pmBestFitMask       = 0x0030,  
  
    pmThrowOnUnmappableCharUseAssem   = 0x0000,  
    pmThrowOnUnmappableCharEnabled    = 0x1000,  
    pmThrowOnUnmappableCharDisabled   = 0x2000,  
    pmThrowOnUnmappableCharMask       = 0x3000,  
  
    pmSupportsLastError = 0x0040,
  
    pmCallConvMask      = 0x0700,  
    pmCallConvWinapi    = 0x0100,  
    pmCallConvCdecl     = 0x0200,  
    pmCallConvStdcall   = 0x0300,  
    pmCallConvThiscall  = 0x0400,  
    pmCallConvFastcall  = 0x0500,  
  
    pmMaxValue          = 0xFFFF  
  
} CorPinvokeMap;  
```  
  
## <a name="members"></a><span data-ttu-id="340a9-105">成員</span><span class="sxs-lookup"><span data-stu-id="340a9-105">Members</span></span>  
  
|<span data-ttu-id="340a9-106">member</span><span class="sxs-lookup"><span data-stu-id="340a9-106">Member</span></span>|<span data-ttu-id="340a9-107">描述</span><span class="sxs-lookup"><span data-stu-id="340a9-107">Description</span></span>|  
|------------|-----------------|  
|`pmNoMangle`|<span data-ttu-id="340a9-108">使用指定的每個成員名稱。</span><span class="sxs-lookup"><span data-stu-id="340a9-108">Use each member name as specified.</span></span>|  
|`pmCharSetMask`|<span data-ttu-id="340a9-109">保留的。</span><span class="sxs-lookup"><span data-stu-id="340a9-109">Reserved.</span></span>|  
|`pmCharSetNotSpec`|<span data-ttu-id="340a9-110">保留的。</span><span class="sxs-lookup"><span data-stu-id="340a9-110">Reserved.</span></span>|  
|`pmCharSetAnsi`|<span data-ttu-id="340a9-111">將字串當做多位元組字元字串來封送處理。</span><span class="sxs-lookup"><span data-stu-id="340a9-111">Marshal strings as multiple-byte character strings.</span></span>|  
|`pmCharSetUnicode`|<span data-ttu-id="340a9-112">封送處理字串為 Unicode 2 個位元組字元。</span><span class="sxs-lookup"><span data-stu-id="340a9-112">Marshal strings as Unicode 2-byte characters.</span></span>|  
|`pmCharSetAuto`|<span data-ttu-id="340a9-113">自動為目標作業系統妥善地封送處理字串。</span><span class="sxs-lookup"><span data-stu-id="340a9-113">Automatically marshal strings appropriately for the target operating system.</span></span> <span data-ttu-id="340a9-114">預設值是 Windows NT、Windows 2000、Windows XP 及 Windows Server 2003 系列上的 Unicode;預設值是 Windows 98 和 Windows Me 上的 ANSI。</span><span class="sxs-lookup"><span data-stu-id="340a9-114">The default is Unicode on Windows NT, Windows 2000, Windows XP, and the Windows Server 2003 family; the default is ANSI on Windows 98 and Windows Me.</span></span>|  
|`pmBestFitUseAssem`|<span data-ttu-id="340a9-115">保留的。</span><span class="sxs-lookup"><span data-stu-id="340a9-115">Reserved.</span></span>|  
|`pmBestFitEnabled`|<span data-ttu-id="340a9-116">對 ANSI 字元集中缺少完全相符的 Unicode 字元執行最符合的對應。</span><span class="sxs-lookup"><span data-stu-id="340a9-116">Perform best-fit mapping of Unicode characters that lack an exact match in the ANSI character set.</span></span>|  
|`pmBestFitDisabled`|<span data-ttu-id="340a9-117">請勿對 Unicode 字元執行最符合的對應。</span><span class="sxs-lookup"><span data-stu-id="340a9-117">Do not perform best-fit mapping of Unicode characters.</span></span> <span data-ttu-id="340a9-118">在此情況下，所有無法映射的字元都會被 '？ ' 取代。</span><span class="sxs-lookup"><span data-stu-id="340a9-118">In this case, all unmappable characters will be replaced by a ‘?’.</span></span>|  
|`pmBestFitMask`|<span data-ttu-id="340a9-119">保留的。</span><span class="sxs-lookup"><span data-stu-id="340a9-119">Reserved.</span></span>|  
|`pmThrowOnUnmappableCharUseAssem`|<span data-ttu-id="340a9-120">保留的。</span><span class="sxs-lookup"><span data-stu-id="340a9-120">Reserved.</span></span>|  
|`pmThrowOnUnmappableCharEnabled`|<span data-ttu-id="340a9-121">當 interop 封送處理器遇到無法映射的字元時，會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="340a9-121">Throw an exception when the interop marshaler encounters an unmappable character.</span></span>|  
|`pmThrowOnUnmappableCharDisabled`|<span data-ttu-id="340a9-122">當 interop 封送處理器遇到無法映射的字元時，請勿擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="340a9-122">Do not throw an exception when the interop marshaler encounters an unmappable character.</span></span>|  
|`pmThrowOnUnmappableCharMask`|<span data-ttu-id="340a9-123">保留</span><span class="sxs-lookup"><span data-stu-id="340a9-123">Reserved</span></span>|  
|`pmSupportsLastError`|<span data-ttu-id="340a9-124">允許被呼叫者呼叫 Win32 函式， `SetLastError` 再從屬性化方法傳回。</span><span class="sxs-lookup"><span data-stu-id="340a9-124">Allow the callee to call the Win32 `SetLastError` function before returning from the attributed method.</span></span>|  
|`pmCallConvMask`|<span data-ttu-id="340a9-125">保留</span><span class="sxs-lookup"><span data-stu-id="340a9-125">Reserved</span></span>|  
|`pmCallConvWinapi`|<span data-ttu-id="340a9-126">使用預設的平臺呼叫慣例。</span><span class="sxs-lookup"><span data-stu-id="340a9-126">Use the default platform calling convention.</span></span> <span data-ttu-id="340a9-127">例如，在 Windows 上，預設值為 `StdCall` ，而在 Windows CE .net 則為 `Cdecl` 。</span><span class="sxs-lookup"><span data-stu-id="340a9-127">For example, on Windows the default is `StdCall` and on Windows CE .NET it is `Cdecl`.</span></span>|  
|`pmCallConvCdecl`|<span data-ttu-id="340a9-128">使用 `Cdecl` 呼叫慣例。</span><span class="sxs-lookup"><span data-stu-id="340a9-128">Use the `Cdecl` calling convention.</span></span> <span data-ttu-id="340a9-129">在此情況下，呼叫端會清除堆疊。</span><span class="sxs-lookup"><span data-stu-id="340a9-129">In this case, the caller cleans the stack.</span></span> <span data-ttu-id="340a9-130">這樣就可以使用 (來呼叫函式 `varargs` ，也就是接受) 參數數目的函式。</span><span class="sxs-lookup"><span data-stu-id="340a9-130">This enables calling functions with `varargs` (that is, functions that accept a variable number of parameters).</span></span>|  
|`pmCallConvStdcall`|<span data-ttu-id="340a9-131">使用 `StdCall` 呼叫慣例。</span><span class="sxs-lookup"><span data-stu-id="340a9-131">Use the `StdCall` calling convention.</span></span> <span data-ttu-id="340a9-132">在此情況下，被呼叫端會清除堆疊。</span><span class="sxs-lookup"><span data-stu-id="340a9-132">In this case, the callee cleans the stack.</span></span> <span data-ttu-id="340a9-133">這是針對用平台叫用呼叫 Unmanaged 函式的預設慣例。</span><span class="sxs-lookup"><span data-stu-id="340a9-133">This is the default convention for calling unmanaged functions with platform invoke.</span></span>|  
|`pmCallConvThiscall`|<span data-ttu-id="340a9-134">使用 `ThisCall` 呼叫慣例。</span><span class="sxs-lookup"><span data-stu-id="340a9-134">Use the `ThisCall` calling convention.</span></span> <span data-ttu-id="340a9-135">在此情況下，第一個參數是 `this` 指標，並儲存在 REGISTER ECX 中。</span><span class="sxs-lookup"><span data-stu-id="340a9-135">In this case, the first parameter is the `this` pointer and is stored in register ECX.</span></span> <span data-ttu-id="340a9-136">其他參數會被推入至堆疊。</span><span class="sxs-lookup"><span data-stu-id="340a9-136">Other parameters are pushed on the stack.</span></span> <span data-ttu-id="340a9-137">`ThisCall`呼叫慣例可用來呼叫從非受控 DLL 匯出之類別的方法。</span><span class="sxs-lookup"><span data-stu-id="340a9-137">The `ThisCall` calling convention is used to call methods on classes exported from an unmanaged DLL.</span></span>|  
|`pmCallConvFastcall`|<span data-ttu-id="340a9-138">保留的。</span><span class="sxs-lookup"><span data-stu-id="340a9-138">Reserved.</span></span>|  
|`pmMaxValue`|<span data-ttu-id="340a9-139">保留的。</span><span class="sxs-lookup"><span data-stu-id="340a9-139">Reserved.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="340a9-140">需求</span><span class="sxs-lookup"><span data-stu-id="340a9-140">Requirements</span></span>  

 <span data-ttu-id="340a9-141">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="340a9-141">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="340a9-142">**標頭：** Corhdr.h。h</span><span class="sxs-lookup"><span data-stu-id="340a9-142">**Header:** CorHdr.h</span></span>  
  
 <span data-ttu-id="340a9-143">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="340a9-143">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="340a9-144">另請參閱</span><span class="sxs-lookup"><span data-stu-id="340a9-144">See also</span></span>

- [<span data-ttu-id="340a9-145">中繼資料列舉</span><span class="sxs-lookup"><span data-stu-id="340a9-145">Metadata Enumerations</span></span>](metadata-enumerations.md)
