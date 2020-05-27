---
title: METAHOST_POLICY_FLAGS 列舉
ms.date: 03/30/2017
api_name:
- METAHOST_POLICY_FLAGS
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- METAHOST_POLICY_FLAGS
helpviewer_keywords:
- METAHOST_POLICY_FLAGS enumeration [.NET Framework hosting]
ms.assetid: 3bb4b526-0118-42e2-ba59-c95648528ce9
topic_type:
- apiref
ms.openlocfilehash: bb40ed65a2e34f1bf293e4c4c842d7db63d2eaa5
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "84008439"
---
# <a name="metahost_policy_flags-enumeration"></a>METAHOST_POLICY_FLAGS 列舉
提供大部分執行時間主機通用的系結原則。 [ICLRMetaHostPolicy：： GetRequestedRuntime](iclrmetahostpolicy-getrequestedruntime-method.md)方法會使用這個列舉。  
  
## <a name="syntax"></a>語法  
  
```cpp  
typedef enum {  
    METAHOST_POLICY_HIGHCOMPAT              = 0x00,  
    METAHOST_POLICY_APPLY_UPGRADE_POLICY    = 0x08,  
    METAHOST_POLICY_EMULATE_EXE_LAUNCH      = 0x10,  
    METAHOST_POLICY_SHOW_ERROR_DIALOG       = 0x20,  
    METAHOST_POLICY_USE_PROCESS_IMAGE_PATH  = 0x40,  
    METAHOST_POLICY_ENSURE_SKU_SUPPORTED    = 0x80,  
    METAHOST_POLICY_IGNORE_ERROR_MODE       = 0x1000  
  
} METAHOST_POLICY_FLAGS;  
```  
  
## <a name="members"></a>成員  
  
|成員|描述|  
|------------|-----------------|  
|`METAHOST_POLICY_HIGHCOMPAT`|定義高相容性原則，這不會考慮任何載入目前進程中的 common language runtime （CLR）。 相反地，它只會考慮已安裝的 CLRs 和元件的喜好設定，衍生自元件檔本身、宣告的內建版本或設定檔。|  
|`METAHOST_POLICY_APPLY_UPGRADE_POLICY`|根據 HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft 的內容，在找不到完全相符的情況下，將升級原則套用至版本系結結果 \\ 。NETFramework\Policy\Upgrades. 這與[RUNTIME_INFO_UPGRADE_VERSION](runtime-info-flags-enumeration.md)的效果相同。|  
|`METAHOST_POLICY_EMULATE_EXE_LAUNCH`|會傳回系結結果，就像提供給呼叫的影像是在新進程中啟動一樣。 目前，會 `GetRequestedRuntime` 忽略一組可載入的執行時間，並針對一組已安裝的執行時間進行系結。 此旗標可讓主機判斷 EXE 在啟動時將系結至哪個執行時間。|  
|`METAHOST_POLICY_SHOW_ERROR_DIALOG`|如果找不 `GetRequestedRuntime` 到與輸入參數相容的執行時間，就會顯示錯誤對話方塊。 從 .NET Framework 4.5 開始，這個錯誤對話方塊可能會採用 Windows 功能對話方塊的形式，詢問使用者是否要啟用適當的功能。|  
|`METAHOST_POLICY_USE_PROCESS_IMAGE_PATH`|`GetRequestedRuntime`會使用處理程式映射（以及任何對應的設定檔）做為系結程式的額外輸入。 根據預設， `GetRequestedRuntime` 在決定要系結的執行時間時，不會切換回進程影像路徑（通常是用來啟動進程的 EXE）。|  
|`METAHOST_POLICY_ENSURE_SKU_SUPPORTED`|`GetRequestedRuntime`當設定檔中沒有可用的資訊時，必須檢查是否已安裝適當的 SKU。 這可讓沒有設定檔的應用程式在較小的 Sku 上正常地失敗，而不是 .NET Framework 的預設安裝。 根據預設， `GetRequestedRuntime` 除非在設定檔元素中指定了 sku 屬性，否則不會檢查是否已安裝適當的 sku `<supportedRuntime />` 。|  
|`METAHOST_POLICY_IGNORE_ERROR_MODE`|`GetRequestedRuntime`應該忽略 SEM_FAILCRITICALERRORS （藉由呼叫[SetErrorMode](/windows/win32/api/errhandlingapi/nf-errhandlingapi-seterrormode)函數來設定），並顯示 [錯誤] 對話方塊。 根據預設，SEM_FAILCRITICALERRORS 會隱藏 [錯誤] 對話方塊。 它可能已繼承自另一個進程，而在您的案例中可能不需要無訊息錯誤。|  
  
## <a name="remarks"></a>備註  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** Metahost。h  
  
 連結**庫：** 包含為 Mscoree.dll 中的資源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [裝載列舉](hosting-enumerations.md)
- [GetRequestedRuntime 方法](iclrmetahostpolicy-getrequestedruntime-method.md)
