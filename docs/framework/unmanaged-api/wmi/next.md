---
title: 'Next function (非受控 API 參考) '
description: 下一個函數會捕獲列舉中的下一個屬性。
ms.date: 11/06/2017
api_name:
- Next
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- Next
helpviewer_keywords:
- Next function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: c2a7fae32e82caae40a95bfdad10fa78082988ef
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95726778"
---
# <a name="next-function"></a><span data-ttu-id="50dfa-103">Next 函式</span><span class="sxs-lookup"><span data-stu-id="50dfa-103">Next function</span></span>

<span data-ttu-id="50dfa-104">抓取列舉中的下一個屬性，其開頭為 [BeginEnumeration](beginenumeration.md)的呼叫。</span><span class="sxs-lookup"><span data-stu-id="50dfa-104">Retrieves the next property in an enumeration that begins with a call to [BeginEnumeration](beginenumeration.md).</span></span>

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a><span data-ttu-id="50dfa-105">語法</span><span class="sxs-lookup"><span data-stu-id="50dfa-105">Syntax</span></span>

```cpp
HRESULT Next (
   [in] int               vFunc,
   [in] IWbemClassObject* ptr,
   [in] LONG              lFlags,
   [out] BSTR*            pstrName,
   [out] VARIANT*         pVal,
   [out] CIMTYPE*         pvtType,
   [out] LONG*            plFlavor
);
```

## <a name="parameters"></a><span data-ttu-id="50dfa-106">參數</span><span class="sxs-lookup"><span data-stu-id="50dfa-106">Parameters</span></span>

`vFunc`\
<span data-ttu-id="50dfa-107">在此參數未使用。</span><span class="sxs-lookup"><span data-stu-id="50dfa-107">[in] This parameter is unused.</span></span>

`ptr`\
<span data-ttu-id="50dfa-108">在 [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) 實例的指標。</span><span class="sxs-lookup"><span data-stu-id="50dfa-108">[in] A pointer to an [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) instance.</span></span>

`lFlags`\
<span data-ttu-id="50dfa-109">[in] 保留。</span><span class="sxs-lookup"><span data-stu-id="50dfa-109">[in] Reserved.</span></span> <span data-ttu-id="50dfa-110">此參數必須為0。</span><span class="sxs-lookup"><span data-stu-id="50dfa-110">This parameter must be 0.</span></span>

`pstrName`\
<span data-ttu-id="50dfa-111">擴展 `BSTR` 包含屬性名稱的新。</span><span class="sxs-lookup"><span data-stu-id="50dfa-111">[out] A new `BSTR` that contains the property name.</span></span> <span data-ttu-id="50dfa-112">`null`如果名稱不是必要的，您可以將此參數設定為。</span><span class="sxs-lookup"><span data-stu-id="50dfa-112">You can set this parameter to `null` if the name is not required.</span></span>

`pVal`\
<span data-ttu-id="50dfa-113">擴展 `VARIANT` 填滿屬性值的。</span><span class="sxs-lookup"><span data-stu-id="50dfa-113">[out] A `VARIANT` filled with the value of the property.</span></span> <span data-ttu-id="50dfa-114">如果不需要此值，您可以將此參數設定為 `null` 。</span><span class="sxs-lookup"><span data-stu-id="50dfa-114">You can set this parameter to `null` if the value is not required.</span></span> <span data-ttu-id="50dfa-115">如果函式傳回錯誤碼，則 `VARIANT` 傳遞至的 `pVal` 會保持未修改狀態。</span><span class="sxs-lookup"><span data-stu-id="50dfa-115">If the function returns an error code, the `VARIANT` passed to `pVal` is left unmodified.</span></span>

`pvtType`\
<span data-ttu-id="50dfa-116">擴展變數的指標， `CIMTYPE` (將 `LONG` 屬性的型別放置) 。</span><span class="sxs-lookup"><span data-stu-id="50dfa-116">[out] A pointer to a `CIMTYPE` variable (a `LONG` into which the type of the property is placed).</span></span> <span data-ttu-id="50dfa-117">這個屬性的值可以是 `VT_NULL_VARIANT` ，在這種情況下，必須判斷屬性的實際類型。</span><span class="sxs-lookup"><span data-stu-id="50dfa-117">The value of this property can be a `VT_NULL_VARIANT`, in which case it is necessary to determine the actual type of the property.</span></span> <span data-ttu-id="50dfa-118">此參數也可以是 `null` 。</span><span class="sxs-lookup"><span data-stu-id="50dfa-118">This parameter can also be `null`.</span></span>

`plFlavor`\
<span data-ttu-id="50dfa-119">[out] `null` ，或在屬性的原點接收資訊的值。</span><span class="sxs-lookup"><span data-stu-id="50dfa-119">[out] `null`, or a value that receives information on the origin of the property.</span></span> <span data-ttu-id="50dfa-120">如需可能的值，請參閱 [備註] 區段。</span><span class="sxs-lookup"><span data-stu-id="50dfa-120">See the [Remarks] section for possible values.</span></span>

## <a name="return-value"></a><span data-ttu-id="50dfa-121">傳回值</span><span class="sxs-lookup"><span data-stu-id="50dfa-121">Return value</span></span>

<span data-ttu-id="50dfa-122">這個函式所傳回的下列值是在 *WbemCli .h* 標頭檔中定義，您也可以在程式碼中將它們定義為常數：</span><span class="sxs-lookup"><span data-stu-id="50dfa-122">The following values returned by this function are defined in the *WbemCli.h* header file, or you can define them as constants in your code:</span></span>

|<span data-ttu-id="50dfa-123">常數</span><span class="sxs-lookup"><span data-stu-id="50dfa-123">Constant</span></span>  |<span data-ttu-id="50dfa-124">值</span><span class="sxs-lookup"><span data-stu-id="50dfa-124">Value</span></span>  |<span data-ttu-id="50dfa-125">描述</span><span class="sxs-lookup"><span data-stu-id="50dfa-125">Description</span></span>  |
|---------|---------|---------|
| `WBEM_E_FAILED` | <span data-ttu-id="50dfa-126">0x80041001</span><span class="sxs-lookup"><span data-stu-id="50dfa-126">0x80041001</span></span> | <span data-ttu-id="50dfa-127">一般失敗。</span><span class="sxs-lookup"><span data-stu-id="50dfa-127">There has been a general failure.</span></span> |
| `WBEM_E_INVALID_PARAMETER` | <span data-ttu-id="50dfa-128">0x80041008</span><span class="sxs-lookup"><span data-stu-id="50dfa-128">0x80041008</span></span> | <span data-ttu-id="50dfa-129">參數無效。</span><span class="sxs-lookup"><span data-stu-id="50dfa-129">A parameter is invalid.</span></span> |
| `WBEM_E_UNEXPECTED` | <span data-ttu-id="50dfa-130">0x8004101d</span><span class="sxs-lookup"><span data-stu-id="50dfa-130">0x8004101d</span></span> | <span data-ttu-id="50dfa-131">沒有函數的呼叫 [`BeginEnumeration`](beginenumeration.md) 。</span><span class="sxs-lookup"><span data-stu-id="50dfa-131">There was no call to the [`BeginEnumeration`](beginenumeration.md) function.</span></span> |
| `WBEM_E_OUT_OF_MEMORY` | <span data-ttu-id="50dfa-132">0x80041006</span><span class="sxs-lookup"><span data-stu-id="50dfa-132">0x80041006</span></span> | <span data-ttu-id="50dfa-133">沒有足夠的記憶體可用來開始新的列舉。</span><span class="sxs-lookup"><span data-stu-id="50dfa-133">Not enough memory is available to begin a new enumeration.</span></span> |
| `WBEM_E_TRANSPORT_FAILURE` | <span data-ttu-id="50dfa-134">0x80041015</span><span class="sxs-lookup"><span data-stu-id="50dfa-134">0x80041015</span></span> | <span data-ttu-id="50dfa-135">目前進程與 Windows 管理之間的遠端程序呼叫失敗。</span><span class="sxs-lookup"><span data-stu-id="50dfa-135">The remote procedure call between the current process and Windows Management failed.</span></span> |
| `WBEM_S_NO_ERROR` | <span data-ttu-id="50dfa-136">0</span><span class="sxs-lookup"><span data-stu-id="50dfa-136">0</span></span> | <span data-ttu-id="50dfa-137">函式呼叫成功。</span><span class="sxs-lookup"><span data-stu-id="50dfa-137">The function call was successful.</span></span>  |
| `WBEM_S_NO_MORE_DATA` | <span data-ttu-id="50dfa-138">0x40005</span><span class="sxs-lookup"><span data-stu-id="50dfa-138">0x40005</span></span> | <span data-ttu-id="50dfa-139">列舉中沒有其他屬性。</span><span class="sxs-lookup"><span data-stu-id="50dfa-139">There are no more properties in the enumeration.</span></span> |

## <a name="remarks"></a><span data-ttu-id="50dfa-140">備註</span><span class="sxs-lookup"><span data-stu-id="50dfa-140">Remarks</span></span>

<span data-ttu-id="50dfa-141">此函數會包裝對 [IWbemClassObject：： Next](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-next) 方法的呼叫。</span><span class="sxs-lookup"><span data-stu-id="50dfa-141">This function wraps a call to the [IWbemClassObject::Next](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-next) method.</span></span>

<span data-ttu-id="50dfa-142">這個方法也會傳回系統屬性。</span><span class="sxs-lookup"><span data-stu-id="50dfa-142">This method also returns system properties.</span></span>

<span data-ttu-id="50dfa-143">如果屬性的基礎類型是物件路徑、日期或時間或其他特殊類型，則傳回的型別不會包含足夠的資訊。</span><span class="sxs-lookup"><span data-stu-id="50dfa-143">If the underlying type of the property is an object path, a date or time, or another special type, then the returned type does not contain enough information.</span></span> <span data-ttu-id="50dfa-144">呼叫端必須檢查 `CIMTYPE` 是否有指定的屬性，以判斷屬性是否為物件參考、日期或時間，或另一種特殊類型。</span><span class="sxs-lookup"><span data-stu-id="50dfa-144">The caller must examine the `CIMTYPE` for the specified property to determine if the property is an object reference, a date or time, or another special type.</span></span>

<span data-ttu-id="50dfa-145">如果 `plFlavor` 不是 `null` ，此 `LONG` 值會接收有關屬性來源的資訊，如下所示：</span><span class="sxs-lookup"><span data-stu-id="50dfa-145">If `plFlavor` is not `null`, the `LONG` value receives information about the origin of the property, as follows:</span></span>

|<span data-ttu-id="50dfa-146">常數</span><span class="sxs-lookup"><span data-stu-id="50dfa-146">Constant</span></span>  |<span data-ttu-id="50dfa-147">值</span><span class="sxs-lookup"><span data-stu-id="50dfa-147">Value</span></span>  |<span data-ttu-id="50dfa-148">描述</span><span class="sxs-lookup"><span data-stu-id="50dfa-148">Description</span></span>  |
|---------|---------|---------|
| `WBEM_FLAVOR_ORIGIN_SYSTEM` | <span data-ttu-id="50dfa-149">0x40</span><span class="sxs-lookup"><span data-stu-id="50dfa-149">0x40</span></span> | <span data-ttu-id="50dfa-150">屬性是標準的系統屬性。</span><span class="sxs-lookup"><span data-stu-id="50dfa-150">The property is a standard system property.</span></span> |
| `WBEM_FLAVOR_ORIGIN_PROPAGATED` | <span data-ttu-id="50dfa-151">0x20</span><span class="sxs-lookup"><span data-stu-id="50dfa-151">0x20</span></span> | <span data-ttu-id="50dfa-152">針對類別：屬性繼承自父類別。</span><span class="sxs-lookup"><span data-stu-id="50dfa-152">For a class: The property is inherited from the parent class.</span></span> <br> <span data-ttu-id="50dfa-153">針對實例：實例尚未修改屬性（繼承自父類別）。</span><span class="sxs-lookup"><span data-stu-id="50dfa-153">For an instance: The property, while inherited from the parent class, has not been modified by the instance.</span></span>  |
| `WBEM_FLAVOR_ORIGIN_LOCAL` | <span data-ttu-id="50dfa-154">0</span><span class="sxs-lookup"><span data-stu-id="50dfa-154">0</span></span> | <span data-ttu-id="50dfa-155">若為類別：屬性屬於衍生類別。</span><span class="sxs-lookup"><span data-stu-id="50dfa-155">For a class: The property belongs to the derived class.</span></span> <br> <span data-ttu-id="50dfa-156">針對實例：此屬性是由實例修改;亦即，已提供值，或新增或修改了限定詞。</span><span class="sxs-lookup"><span data-stu-id="50dfa-156">For an instance: The property is modified by the instance; that is, a value was supplied, or a qualifier was added or modified.</span></span> |

## <a name="requirements"></a><span data-ttu-id="50dfa-157">需求</span><span class="sxs-lookup"><span data-stu-id="50dfa-157">Requirements</span></span>

<span data-ttu-id="50dfa-158">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="50dfa-158">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>

<span data-ttu-id="50dfa-159">**標頭：** WMINet_Utils .idl</span><span class="sxs-lookup"><span data-stu-id="50dfa-159">**Header:** WMINet_Utils.idl</span></span>

<span data-ttu-id="50dfa-160">**.NET Framework 版本：**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]</span><span class="sxs-lookup"><span data-stu-id="50dfa-160">**.NET Framework Versions:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]</span></span>

## <a name="see-also"></a><span data-ttu-id="50dfa-161">另請參閱</span><span class="sxs-lookup"><span data-stu-id="50dfa-161">See also</span></span>

- [<span data-ttu-id="50dfa-162">WMI 與效能計數器 (非受控 API 參考)</span><span class="sxs-lookup"><span data-stu-id="50dfa-162">WMI and Performance Counters (Unmanaged API Reference)</span></span>](index.md)
