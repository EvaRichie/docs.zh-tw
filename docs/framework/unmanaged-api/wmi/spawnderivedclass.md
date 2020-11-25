---
title: 'SpawnDerivedClass 函式 (非受控 API 參考) '
description: SpawnDerivedClass 函式會建立衍生自物件的新物件。
ms.date: 11/06/2017
api_name:
- SpawnDerivedClass
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- SpawnDerivedClass
helpviewer_keywords:
- SpawnDerivedClass function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 8020dd851b6773e6c76c53892c4b2bc21e4261bb
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95716508"
---
# <a name="spawnderivedclass-function"></a>SpawnDerivedClass 函式

從指定的物件建立新的衍生類別物件。
  
[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT SpawnDerivedClass (
   [in] int                  vFunc,
   [in] IWbemClassObject*    ptr,
   [in] LONG                 lFlags,
   [out] IWbemClassObject**  ppNewClass);
```  

## <a name="parameters"></a>參數

`vFunc`  
在此參數未使用。

`ptr`  
在 [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) 實例的指標。

`lFlags`  
[in] 保留。 此參數必須為0。

`ppNewClass`  
擴展接收新類別定義物件的指標。 如果發生錯誤，則不會傳回新的物件，而且 `ppNewClass` 會保持未修改狀態。 其值不能是 `null` 。

## <a name="return-value"></a>傳回值

這個函式所傳回的下列值是在 *WbemCli .h* 標頭檔中定義，您也可以在程式碼中將它們定義為常數：

|常數  |值  |描述  |
|---------|---------|---------|
| `WBEM_E_FAILED` | 0x80041001 | 一般失敗。 |
| `WBEM_E_INVALID_OPERATION` | 0x80041016 | 要求的作業無效，例如從實例產生類別。 |
| `WBEM_E_INCOMPLETE_CLASS` | 來源類別未完整定義或向 Windows 管理註冊，因此不允許新的衍生類別。 |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 可用的記憶體不足，無法完成作業。 |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | `ppNewClass` 為 `null`。 |
| `WBEM_S_NO_ERROR` | 0 | 函式呼叫成功。  |
  
## <a name="remarks"></a>備註

此函數會包裝對 [IWbemClassObject：： SpawnDerivedClass](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-clone) 方法的呼叫。

`ptr` 必須是類別定義，才能成為衍生物件的父類別。 傳回的物件會成為目前物件的子類別。

中傳回的新物件 `ppNewClass` 會自動成為目前物件的子類別。 無法覆寫此行為。 無法建立子類別 (衍生類別) 的其他方法。

## <a name="requirements"></a>需求  

 **平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** WMINet_Utils .idl  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>另請參閱

- [WMI 與效能計數器 (非受控 API 參考)](index.md)
