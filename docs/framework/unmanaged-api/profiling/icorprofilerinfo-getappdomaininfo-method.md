---
title: ICorProfilerInfo::GetAppDomainInfo 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.GetAppDomainInfo
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::GetAppDomainInfo
helpviewer_keywords:
- ICorProfilerInfo::GetAppDomainInfo method [.NET Framework profiling]
- GetAppDomainInfo method [.NET Framework profiling]
ms.assetid: a6bf5a04-e03e-44f0-917a-96f6a6d3cc96
topic_type:
- apiref
ms.openlocfilehash: 5e5510ec098b2c1aa3b768830b812328287fd31a
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503025"
---
# <a name="icorprofilerinfogetappdomaininfo-method"></a>ICorProfilerInfo::GetAppDomainInfo 方法
接受應用程式定義域 ID。 傳回應用程式定義域名稱和包含該處理序的 ID。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT GetAppDomainInfo(  
    [in]  AppDomainID appDomainId,  
    [in]  ULONG       cchName,  
    [out] ULONG       *pcchName,  
    [out, size_is(cchName), length_is(*pcchName)]  
          WCHAR       szName[] ,  
    [out] ProcessID   *pProcessId);  
```  
  
## <a name="parameters"></a>參數  
 `appDomainId`  
 [in] 應用程式定義域的 ID。  
  
 `cchName`  
 [in] `szName` 傳回緩衝區的長度 (以字元為單位)。  
  
 `pcchName`  
 [out] 應用程式定義域名稱之總字元長度的指標。  
  
 `szName`  
 [out] 呼叫端提供的寬字元緩衝區。 當此方法傳回時，`szName` 將包含完整或部分的應用程式定義域名稱。  
  
 `pProcessId`  
 [out] 包含應用程式定義域之處理序 ID 的指標。  
  
## <a name="remarks"></a>備註  
 在此方法傳回之後，您必須確認 `szName` 緩衝區的大小足以包含應用程式定義域的完整檔案名稱。 若要這樣做，請比對 `pcchName` 指向的值和 `cchName` 參數。 如果 `pcchName` 指向大於 `cchName` 的值，請配置較大的 `szName` 緩衝區，並以較大的大小來更新 `cchName`，然後再次呼叫 `GetAppDomainInfo`。  
  
 或者，您也可以先使用長度為零的 `szName` 緩衝區來呼叫 `GetAppDomainInfo`，以取得正確的緩衝區大小。 接著您就可以將緩衝區大小設定為 `pcchName` 中傳回的值，並再次呼叫 `GetAppDomainInfo`。  
  
## <a name="requirements"></a>規格需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorProf.idl、CorProf.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICorProfilerInfo 介面](icorprofilerinfo-interface.md)
- [分析介面](profiling-interfaces.md)
- [程式碼剖析](index.md)
