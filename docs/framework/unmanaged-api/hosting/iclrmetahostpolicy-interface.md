---
title: ICLRMetaHostPolicy 介面
ms.date: 03/30/2017
api_name:
- ICLRMetaHostPolicy
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRMetaHostPolicy
helpviewer_keywords:
- ICLRMetaHostPolicy interface [.NET Framework hosting]
ms.assetid: 1bdeccb6-0698-4c97-ad69-eae2b69e59f1
topic_type:
- apiref
ms.openlocfilehash: 79b62a5e2aad9cfcd14ba40c1abf0342bfe57a4b
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/20/2020
ms.locfileid: "83703525"
---
# <a name="iclrmetahostpolicy-interface"></a>ICLRMetaHostPolicy 介面
提供[GetRequestedRuntime](iclrmetahostpolicy-getrequestedruntime-method.md)方法，它會根據原則準則、managed 元件、版本和設定檔，傳回通用語言執行時間（CLR）介面的指標。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[GetRequestedRuntime 方法](iclrmetahostpolicy-getrequestedruntime-method.md)|根據原則準則、managed 元件、版本和設定檔，提供慣用的 CLR 介面。|  
  
## <a name="remarks"></a>備註  
 您可以呼叫[CLRCreateInstance](clrcreateinstance-function.md)函式來取得此介面的參考，如下列程式碼所示：  
  
```cpp  
ICLRMetaHostPolicy *pMetaHostPolicy = NULL;  
HRESULT hr = CLRCreateInstance(CLSID_CLRMetaHostPolicy,  
                   IID_ICLRMetaHostPolicy, (LPVOID*)&pMetaHostPolicy);  
```  
  
> [!NOTE]
> 這個介面實際上並不會載入或啟動 CLR，而只會根據已安裝或載入的可用版本傳回慣用的 CLR 版本。  
  
 .NET Framework 4 裝載 API 會合並原則，讓具有特定需求的主機可以使用基本功能，而不會產生非預期的負面影響。 例如，許多 Mscoree.dll 匯出都會系結至特定的 CLR，雖然方法在邏輯上可能不會要求它。 [METAHOST_POLICY_FLAGS](metahost-policy-flags-enumeration.md)列舉會提供大多數主機通用的系結原則。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** MetaHost。h  
  
 連結**庫：** 包含為 Mscoree.dll 中的資源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [.NET Framework 4 和 4.5 中新增的 CLR 裝載介面](clr-hosting-interfaces-added-in-the-net-framework-4-and-4-5.md)
- [裝載介面](hosting-interfaces.md)
- [裝載](index.md)
