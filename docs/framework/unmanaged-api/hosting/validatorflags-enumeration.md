---
title: ValidatorFlags 列舉
ms.date: 03/30/2017
api_name:
- ValidatorFlags
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ValidatorFlags
helpviewer_keywords:
- ValidatorFlags enumeration [.NET Framework hosting]
ms.assetid: a3f5c266-3fcc-4ad1-aaf5-4cdbe26304ad
topic_type:
- apiref
ms.openlocfilehash: 92c430cdb8b46cf75dde9a8395ce713116dc05a5
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95732849"
---
# <a name="validatorflags-enumeration"></a>ValidatorFlags 列舉

包含值，這些值表示應該在 [ICLRValidator：： Validate](iclrvalidator-validate-method.md) 方法的呼叫中執行的驗證類型。  
  
## <a name="syntax"></a>語法  
  
```cpp  
enum ValidatorFlags {  
    VALIDATOR_EXTRA_VERBOSE =       0x00000001,  
    VALIDATOR_SHOW_SOURCE_LINES =   0x00000002,  
    VALIDATOR_CHECK_ILONLY =        0x00000004,  
    VALIDATOR_CHECK_PEFORMAT_ONLY = 0x00000008,  
    VALIDATOR_NOCHECK_PEFORMAT =    0x00000010,  
};  
```  
  
## <a name="members"></a>成員  
  
|member|描述|  
|------------|-----------------|  
|`VALIDATOR_CHECK_ILONLY`|指定只能驗證可執行檔中的 Microsoft 中繼語言 (MSIL) 。|  
|`VALIDATOR_CHECK_PEFORMAT_ONLY`|指定只能驗證可執行檔的格式。|  
|`VALIDATOR_EXTRA_VERBOSE`|指定應該執行和報告所有類型的驗證。|  
|`VALIDATOR_NOCHECK_PEFORMAT`|指定不應該驗證可執行檔的格式。|  
|`VALIDATOR_SHOW_SOURCE_LINES`|指定驗證錯誤訊息應該包含引發驗證錯誤的源程式碼。 在 .NET Framework 版本2.0 中，此域值無效。|  
  
## <a name="requirements"></a>需求  

 **平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** IValidator .idl、IValidator。h  
  
 連結 **庫：** MSCorEE.dll  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICLRErrorReportingManager 介面](iclrerrorreportingmanager-interface.md)
- [裝載列舉](hosting-enumerations.md)
