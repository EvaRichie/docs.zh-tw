---
title: ICLRAppDomainResourceMonitor::GetCurrentSurvived 方法
ms.date: 03/30/2017
api_name:
- ICLRAppDomainResourceMonitor.GetCurrentSurvived
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRAppDomainResourceMonitor::GetCurrentSurvived
helpviewer_keywords:
- ICLRAppDomainResourceMonitor::GetCurrentSurvived method [.NET Framework hosting]
- GetCurrentSurvived method [.NET Framework hosting]
ms.assetid: 392e9009-40ef-40e3-ad4d-7ce93a989e78
topic_type:
- apiref
ms.openlocfilehash: a73c0731c79dea3a0c411fe27a864ec9ac4e20b2
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83616017"
---
# <a name="iclrappdomainresourcemonitorgetcurrentsurvived-method"></a>ICLRAppDomainResourceMonitor::GetCurrentSurvived 方法
取得最後一次完整、封鎖垃圾收集以及目前應用程式域所參考的位元組數目。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT STDMETHODCALLTYPE GetCurrentSurvived(  
             [in]  DWORD dwAppDomainId,  
             [out] ULONGLONG *pAppDomainBytesSurvived,  
             [out] ULONGLONG *pTotalBytesSurvived);  
```  
  
## <a name="parameters"></a>參數  
 `dwAppDomainId`  
 在要求之應用程式域的識別碼。  
  
 `pAppDomainBytesSurvived`  
 脫銷這個應用程式域所持有的最後一次垃圾收集之後，被回收的位元組數目指標。 在完整集合之後，此數位會正確且完整。 在暫時集合之後，此數位可能不完整。 這個參數可以是 `null`。  
  
 `pRuntimeBytesSurvived`  
 脫銷從上一次垃圾收集中未被回收之位元組總數的指標。 在完整集合之後，此數位代表保留在受控堆積中的位元組數目。 在暫時集合之後，此數位代表暫時層代中存留的位元組數目。 這個參數可以是 `null`。  
  
## <a name="return-value"></a>傳回值  
 這個方法會傳回下列特定的 HRESULT，以及表示方法失敗的 HRESULT 錯誤。  
  
|HRESULT|說明|  
|-------------|-----------------|  
|S_OK|已成功完成命令。|  
|COR_E_APPDOMAINUNLOADED|應用程式域已卸載或不存在。|  
  
## <a name="remarks"></a>備註  
 只有在完整的封鎖垃圾收集之後，才會更新統計資料。也就是包含所有層代的集合，而且會在收集時停止應用程式。 例如，方法多載會 <xref:System.GC.Collect?displayProperty=nameWithType> 執行完整的封鎖集合。 並行垃圾收集會在背景進行，而且不會封鎖應用程式。  
  
 `GetCurrentSurvived`方法是 managed 屬性的不受管理對等 <xref:System.AppDomain.MonitoringSurvivedMemorySize%2A?displayProperty=nameWithType> 。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** MetaHost。h  
  
 連結**庫：** 包含為 Mscoree.dll 中的資源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICLRAppDomainResourceMonitor 介面](iclrappdomainresourcemonitor-interface.md)
- [應用程式域資源監視](../../../standard/garbage-collection/app-domain-resource-monitoring.md)
- [裝載介面](hosting-interfaces.md)
- [裝載](index.md)
