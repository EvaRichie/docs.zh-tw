---
title: IHostThreadPoolManager 介面
ms.date: 03/30/2017
api_name:
- IHostThreadPoolManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostThreadPoolManager
helpviewer_keywords:
- IHostThreadPoolManager interface [.NET Framework hosting]
ms.assetid: c3a2cd90-7c4e-4374-bb87-b41befb8344f
topic_type:
- apiref
ms.openlocfilehash: b6625b0ef4dc3de4067514a0b39849c7a958d5c4
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95730756"
---
# <a name="ihostthreadpoolmanager-interface"></a>IHostThreadPoolManager 介面

提供的方法，可讓 common language runtime (CLR) 設定執行緒集區，以及將工作專案加入執行緒集區。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[GetAvailableThreads 方法](ihostthreadpoolmanager-getavailablethreads-method.md)|取得執行緒集區中目前未處理工作專案的執行緒數目。|  
|[GetMaxThreads 方法](ihostthreadpoolmanager-getmaxthreads-method.md)|取得主機線上程集區中同時維護的執行緒數目上限。|  
|[GetMinThreads 方法](ihostthreadpoolmanager-getminthreads-method.md)|取得主機在預期的要求中維持的最小閒置執行緒數目。|  
|[QueueUserWorkItem 方法](ihostthreadpoolmanager-queueuserworkitem-method.md)|將函式排入佇列以便執行，並提供包含函式所要使用之資料的物件。|  
|[SetMaxThreads 方法](ihostthreadpoolmanager-setmaxthreads-method.md)|設定主機可以線上程集區中維護的執行緒數目上限。|  
|[SetMinThreads 方法](ihostthreadpoolmanager-setminthreads-method.md)|設定主機必須在預期的要求中維持的最小閒置執行緒數目。|  
  
## <a name="remarks"></a>備註  

 使用和方法的呼叫中指定的值，不需要主控制項來設定執行緒集區 `SetMaxThreads` `SetMinThreads` 。 在此情況下，主機應該會從這些方法傳回 E_NOTIMPL 的 HRESULT 值。  
  
## <a name="requirements"></a>需求  

 **平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** Mscoree.dll  
  
 連結 **庫：** 以資源的形式包含在 MSCorEE.dll 中  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Threading>
- <xref:System.Threading.ThreadPool>
- [裝載介面](hosting-interfaces.md)
