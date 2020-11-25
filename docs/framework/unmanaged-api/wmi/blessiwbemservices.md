---
title: 'BlessIWbemServices 函式 (非受控 API 參考) '
description: BlessIWbemServices 函式會指出使用者認證是否允許存取 IWbemServices 類別。
ms.date: 11/06/2017
api_name:
- BlessIWbemServices
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- BlessIWbemServices
helpviewer_keywords:
- BlessIWbemServices function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 43ef617ee754c9dcd661b31abba6b17434563c22
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95708149"
---
# <a name="blessiwbemservices-function"></a><span data-ttu-id="f521b-103">BlessIWbemServices 函式</span><span class="sxs-lookup"><span data-stu-id="f521b-103">BlessIWbemServices function</span></span>

<span data-ttu-id="f521b-104">指出使用者認證是否允許存取指定的 [IWbemServices](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemservices) 類別。</span><span class="sxs-lookup"><span data-stu-id="f521b-104">Indicates whether the user credentials permit access to the specified [IWbemServices](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemservices) class.</span></span>
  
[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a><span data-ttu-id="f521b-105">語法</span><span class="sxs-lookup"><span data-stu-id="f521b-105">Syntax</span></span>  
  
```cpp
HRESULT BlessIWbemServices (
   [in] IWbemServices* pIWbemServices,
   [in] BSTR strUser,
   [in] BSTR strPassword,
   [in] BSTR strAuthority,
   [in] DWORD impLevel,
   [in] DWORD authnLevel
);
```  

## <a name="parameters"></a><span data-ttu-id="f521b-106">參數</span><span class="sxs-lookup"><span data-stu-id="f521b-106">Parameters</span></span>

`pIWbemServices`\
<span data-ttu-id="f521b-107">在需要許可權的 [IWbemServices](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemservices) 物件指標。</span><span class="sxs-lookup"><span data-stu-id="f521b-107">[in] A pointer to the [IWbemServices](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemservices) object for which permissions are required.</span></span>

`strUser`\
<span data-ttu-id="f521b-108">在使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="f521b-108">[in] The user name.</span></span>

`strPassword`\
<span data-ttu-id="f521b-109">在與相關聯的密碼 `strUser` 。</span><span class="sxs-lookup"><span data-stu-id="f521b-109">[in] The password associated with `strUser`.</span></span>

`strAuthority`\
<span data-ttu-id="f521b-110">在使用者的功能變數名稱。</span><span class="sxs-lookup"><span data-stu-id="f521b-110">[in] The domain name of the user.</span></span> <span data-ttu-id="f521b-111">如需詳細資訊，請參閱 [ConnectServerWmi](connectserverwmi.md) 函數。</span><span class="sxs-lookup"><span data-stu-id="f521b-111">See the [ConnectServerWmi](connectserverwmi.md) function for more information.</span></span>

`impLevel`\
<span data-ttu-id="f521b-112">在模擬等級。</span><span class="sxs-lookup"><span data-stu-id="f521b-112">[in] The impersonation level.</span></span>

`authnLevel`\
<span data-ttu-id="f521b-113">在授權層級。</span><span class="sxs-lookup"><span data-stu-id="f521b-113">[in] The authorization level.</span></span>

## <a name="return-value"></a><span data-ttu-id="f521b-114">傳回值</span><span class="sxs-lookup"><span data-stu-id="f521b-114">Return value</span></span>

<span data-ttu-id="f521b-115">這個函式所傳回的下列值是在 *winerror.h .h* 標頭檔中定義，您也可以在程式碼中將它們定義為常數：</span><span class="sxs-lookup"><span data-stu-id="f521b-115">The following values returned by this function are defined in the *WinError.h* header file, or you can define them as constants in your code:</span></span>

|<span data-ttu-id="f521b-116">常數</span><span class="sxs-lookup"><span data-stu-id="f521b-116">Constant</span></span>  |<span data-ttu-id="f521b-117">值</span><span class="sxs-lookup"><span data-stu-id="f521b-117">Value</span></span>  |<span data-ttu-id="f521b-118">描述</span><span class="sxs-lookup"><span data-stu-id="f521b-118">Description</span></span>  |
|---------|---------|---------|
| `E_INVALIDARG` | <span data-ttu-id="f521b-119">0x80070057</span><span class="sxs-lookup"><span data-stu-id="f521b-119">0x80070057</span></span> | <span data-ttu-id="f521b-120">一或多個引數無效。</span><span class="sxs-lookup"><span data-stu-id="f521b-120">One or more arguments are invalid.</span></span> |
| `E_POINTER` | <span data-ttu-id="f521b-121">且顯示0x80004003</span><span class="sxs-lookup"><span data-stu-id="f521b-121">0x80004003</span></span> | <span data-ttu-id="f521b-122">`pIWbemServices` 為 `null`。</span><span class="sxs-lookup"><span data-stu-id="f521b-122">`pIWbemServices` is `null`.</span></span> |
| `E_FAIL` | <span data-ttu-id="f521b-123">0x80000008</span><span class="sxs-lookup"><span data-stu-id="f521b-123">0x80000008</span></span> | <span data-ttu-id="f521b-124">發生未指定的錯誤。</span><span class="sxs-lookup"><span data-stu-id="f521b-124">An unspecified error has occurred.</span></span> |
| `E_OUTOFMEMORY` | <span data-ttu-id="f521b-125">0x80000002</span><span class="sxs-lookup"><span data-stu-id="f521b-125">0x80000002</span></span> | <span data-ttu-id="f521b-126">記憶體不足，無法執行此作業。</span><span class="sxs-lookup"><span data-stu-id="f521b-126">Insufficient memory is available to perform the operation.</span></span> |
| `S_OK` | <span data-ttu-id="f521b-127">0</span><span class="sxs-lookup"><span data-stu-id="f521b-127">0</span></span> | <span data-ttu-id="f521b-128">函式呼叫成功。</span><span class="sxs-lookup"><span data-stu-id="f521b-128">The function call was successful.</span></span> |

## <a name="requirements"></a><span data-ttu-id="f521b-129">需求</span><span class="sxs-lookup"><span data-stu-id="f521b-129">Requirements</span></span>  

 <span data-ttu-id="f521b-130">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="f521b-130">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="f521b-131">**標頭：** WMINet_Utils .idl</span><span class="sxs-lookup"><span data-stu-id="f521b-131">**Header:** WMINet_Utils.idl</span></span>  
  
 <span data-ttu-id="f521b-132">**.NET Framework 版本：**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]</span><span class="sxs-lookup"><span data-stu-id="f521b-132">**.NET Framework Versions:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f521b-133">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f521b-133">See also</span></span>

- [<span data-ttu-id="f521b-134">WMI 與效能計數器 (非受控 API 參考)</span><span class="sxs-lookup"><span data-stu-id="f521b-134">WMI and Performance Counters (Unmanaged API Reference)</span></span>](index.md)
