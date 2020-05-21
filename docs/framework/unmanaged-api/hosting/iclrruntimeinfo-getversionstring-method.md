---
title: ICLRRuntimeInfo::GetVersionString 方法
ms.date: 03/30/2017
api_name:
- ICLRRuntimeInfo.GetVersionString
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeInfo::GetVersionString
helpviewer_keywords:
- ICLRRuntimeInfo::GetVersionString method [.NET Framework hosting]
- GetVersionString method, ICLRRuntimeInfo interface [.NET Framework hosting]
ms.assetid: 98b097ef-2276-4dd9-8551-b03c972e8179
topic_type:
- apiref
ms.openlocfilehash: ccf48b6aea25bd602b55727c2e5958811702f6bf
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/21/2020
ms.locfileid: "83762574"
---
# <a name="iclrruntimeinfogetversionstring-method"></a>ICLRRuntimeInfo::GetVersionString 方法
取得與指定的[ICLRRuntimeInfo](iclrruntimeinfo-interface.md)介面相關聯的 common language RUNTIME （CLR）版本資訊。  
  
 這個方法會取代下列函數：  
  
- [GetRequestedRuntimeInfo](getrequestedruntimeinfo-function.md)  
  
- [GetRequestedRuntimeVersion](getrequestedruntimeversion-function.md)  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT GetVersionString(  
    [out, size_is(*pcchBuffer)] LPWSTR pwzBuffer,  
    [in, out]  DWORD *pcchBuffer);  
```  
  
## <a name="parameters"></a>參數  
 `pwzBuffer`  
 脫銷.NET Framework 的編譯版本，格式為 "v*A*。*B*[。*X*] "。 *A*、 *B*和*X*是對應至主要版本、次要版本和組建編號的十進位數。 *X*是選擇性的。 如果*X*不存在，則沒有尾端句點。  
  
> [!NOTE]
> 這個參數必須符合 .NET Framework 版本的目錄名稱，因為它出現在 C:\Windows\Microsoft.NET\Framework。  
  
 範例值為 "v v1.0.3705"、"v 1.1.4322"、"v 2.0.50727" 和 "v4.0"。*x*"，其中*x*取決於安裝的組建編號。 請注意，"v" 前置詞是強制的。  
  
 `pchBuffer`  
 [in、out]指定的大小 `pwzBuffer` ，以避免緩衝區溢位。 如果 `pwzBuffer` 為，則會傳回 `null` `pchBuffer` 所需的大小 `pwzBuffer` 以允許預先配置。  
  
## <a name="return-value"></a>傳回值  
 這個方法會傳回下列特定的 HRESULT，以及表示方法失敗的 HRESULT 錯誤。  
  
|HRESULT|Description|  
|-------------|-----------------|  
|S_OK|已成功完成命令。|  
|E_POINTER|`pwzBuffer` 或 `pchBuffer` 為 null。|  
  
## <a name="requirements"></a>規格需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** MetaHost。h  
  
 連結**庫：** 包含為 Mscoree.dll 中的資源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICLRRuntimeInfo 介面](iclrruntimeinfo-interface.md)
- [裝載介面](hosting-interfaces.md)
- [.NET Framework 4 和 4.5 中新增的 CLR 裝載介面](clr-hosting-interfaces-added-in-the-net-framework-4-and-4-5.md)
- [裝載](index.md)
