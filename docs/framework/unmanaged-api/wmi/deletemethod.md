---
title: 'DeleteMethod 函式 (非受控 API 參考) '
description: DeleteMethod 函式會從 CIM 類別定義中刪除指定的方法。
ms.date: 11/06/2017
api_name:
- DeleteMethod
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- DeleteMethod
helpviewer_keywords:
- DeleteMethod function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 8ca58ed3510360b20577890055e4284869d1bf94
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95708097"
---
# <a name="deletemethod-function"></a><span data-ttu-id="ea80d-103">DeleteMethod 函式</span><span class="sxs-lookup"><span data-stu-id="ea80d-103">DeleteMethod function</span></span>

<span data-ttu-id="ea80d-104">從 CIM 類別定義中刪除指定的方法。</span><span class="sxs-lookup"><span data-stu-id="ea80d-104">Deletes the specified method from a CIM class definition.</span></span>

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a><span data-ttu-id="ea80d-105">語法</span><span class="sxs-lookup"><span data-stu-id="ea80d-105">Syntax</span></span>  
  
```cpp  
HRESULT Delete (
   [in] int               vFunc,
   [in] IWbemClassObject* ptr,
   [in] LPCWSTR           wszName
);
```  

## <a name="parameters"></a><span data-ttu-id="ea80d-106">參數</span><span class="sxs-lookup"><span data-stu-id="ea80d-106">Parameters</span></span>

`vFunc`  
<span data-ttu-id="ea80d-107">在此參數未使用。</span><span class="sxs-lookup"><span data-stu-id="ea80d-107">[in] This parameter is unused.</span></span>

`ptr`  
<span data-ttu-id="ea80d-108">在 [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) 實例的指標。</span><span class="sxs-lookup"><span data-stu-id="ea80d-108">[in] A pointer to an [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) instance.</span></span>

`wszName`  
<span data-ttu-id="ea80d-109">在要從類別資料表中移除之方法的名稱。</span><span class="sxs-lookup"><span data-stu-id="ea80d-109">[in] The name of the method to remove from the class table.</span></span> <span data-ttu-id="ea80d-110">`wszName` 必須是有效的指標 `LPCWSTR` 。</span><span class="sxs-lookup"><span data-stu-id="ea80d-110">`wszName` must be a pointer to a valid `LPCWSTR`.</span></span>

## <a name="return-value"></a><span data-ttu-id="ea80d-111">傳回值</span><span class="sxs-lookup"><span data-stu-id="ea80d-111">Return value</span></span>

<span data-ttu-id="ea80d-112">這個函式所傳回的下列值是在 *WbemCli .h* 標頭檔中定義，您也可以在程式碼中將它們定義為常數：</span><span class="sxs-lookup"><span data-stu-id="ea80d-112">The following values returned by this function are defined in the *WbemCli.h* header file, or you can define them as constants in your code:</span></span>

|<span data-ttu-id="ea80d-113">常數</span><span class="sxs-lookup"><span data-stu-id="ea80d-113">Constant</span></span>  |<span data-ttu-id="ea80d-114">值</span><span class="sxs-lookup"><span data-stu-id="ea80d-114">Value</span></span>  |<span data-ttu-id="ea80d-115">描述</span><span class="sxs-lookup"><span data-stu-id="ea80d-115">Description</span></span>  |
|---------|---------|---------|
| `WBEM_E_NOT_FOUND` | <span data-ttu-id="ea80d-116">0x80041002</span><span class="sxs-lookup"><span data-stu-id="ea80d-116">0x80041002</span></span> | <span data-ttu-id="ea80d-117">指定的方法不存在。</span><span class="sxs-lookup"><span data-stu-id="ea80d-117">The specified method does not exist.</span></span> |
| `WBEM_E_OUT_OF_MEMORY` | <span data-ttu-id="ea80d-118">0x80041006</span><span class="sxs-lookup"><span data-stu-id="ea80d-118">0x80041006</span></span> | <span data-ttu-id="ea80d-119">記憶體不足，無法完成此作業。</span><span class="sxs-lookup"><span data-stu-id="ea80d-119">There is not enough memory to complete the operation.</span></span> |
| `WBEM_S_NO_ERROR` | <span data-ttu-id="ea80d-120">0</span><span class="sxs-lookup"><span data-stu-id="ea80d-120">0</span></span> | <span data-ttu-id="ea80d-121">函式呼叫成功。</span><span class="sxs-lookup"><span data-stu-id="ea80d-121">The function call was successful.</span></span>  |

## <a name="remarks"></a><span data-ttu-id="ea80d-122">備註</span><span class="sxs-lookup"><span data-stu-id="ea80d-122">Remarks</span></span>

<span data-ttu-id="ea80d-123">此函數會包裝對 [IWbemClassObject：:D eletemethod](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-deletemethod) 方法的呼叫。</span><span class="sxs-lookup"><span data-stu-id="ea80d-123">This function wraps a call to the [IWbemClassObject::DeleteMethod](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-deletemethod) method.</span></span>

<span data-ttu-id="ea80d-124">指向 CIM 實例的 [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) 指標不支援方法刪除。</span><span class="sxs-lookup"><span data-stu-id="ea80d-124">Method deletion is not supported for [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) pointers that point to CIM instances.</span></span>

## <a name="requirements"></a><span data-ttu-id="ea80d-125">需求</span><span class="sxs-lookup"><span data-stu-id="ea80d-125">Requirements</span></span>  

 <span data-ttu-id="ea80d-126">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="ea80d-126">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="ea80d-127">**標頭：** WMINet_Utils .idl</span><span class="sxs-lookup"><span data-stu-id="ea80d-127">**Header:** WMINet_Utils.idl</span></span>  
  
 <span data-ttu-id="ea80d-128">**.NET Framework 版本：**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]</span><span class="sxs-lookup"><span data-stu-id="ea80d-128">**.NET Framework Versions:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ea80d-129">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ea80d-129">See also</span></span>

- [<span data-ttu-id="ea80d-130">WMI 與效能計數器 (非受控 API 參考)</span><span class="sxs-lookup"><span data-stu-id="ea80d-130">WMI and Performance Counters (Unmanaged API Reference)</span></span>](index.md)
