---
title: CorBindToRuntime 函式
ms.date: 03/30/2017
api_name:
- CorBindToRuntime
api_location:
- mscoree.dll
- mscoreei.dll
api_type:
- DLLExport
f1_keywords:
- CorBindToRuntime
helpviewer_keywords:
- CorBindToRuntime function [.NET Framework hosting]
ms.assetid: 799740aa-46ec-4532-95da-6444565b4971
topic_type:
- apiref
ms.openlocfilehash: 0bcfe42a70d64c091851a1eec81d03e49dbde52b
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83616657"
---
# <a name="corbindtoruntime-function"></a>CorBindToRuntime 函式
讓非受控主機將 common language runtime （CLR）載入進程中。  
  
 此函式在 .NET Framework 4 中已被取代。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT CorBindToRuntime (  
    [in]  LPCWSTR     pwszVersion,
    [in]  LPCWSTR     pwszBuildFlavor,
    [in]  REFCLSID    rclsid,
    [in]  REFIID      riid,
    [out] LPVOID FAR  *ppv  
);  
```  
  
## <a name="parameters"></a>參數  
 `pwszVersion`  
 在描述您要載入之 CLR 版本的字串。  
  
 .NET Framework 中的版本號碼包含四個以句點分隔的部分： [主要]. [*次要. 組建. 修訂*]。 傳遞為的字串 `pwszVersion` 必須以字元 "v" 開頭，後面接著版本號碼的前三個部分（例如 "v 1.0.1529"）。  
  
 某些 CLR 版本會與原則語句一起安裝，以指定與舊版 CLR 的相容性。 根據預設，啟動填充碼 `pwszVersion` 會針對原則語句評估，並載入與所要求版本相容的最新執行階段版本。 主機可以強制填充碼略過原則評估，並藉由傳遞參數的值來載入中所指定的確切版本 `pwszVersion` `STARTUP_LOADER_SAFEMODE` `flags` ，如下所述。  
  
 如果呼叫端針對指定 null `pwszVersion` ，則會載入最新版本的執行時間。 傳遞 null 可讓主機無法控制載入的執行階段版本。 雖然這種方法可能適用于某些情況，但強烈建議主機提供要載入的特定版本。  
  
 `pwszBuildFlavor`  
 在字串，指定是否要載入伺服器或 CLR 的工作站組建。 有效值為 `svr` 和 `wks`。 伺服器組建已優化，可利用多個處理器進行垃圾收集，而且工作站組建已針對在單處理器機器上執行的用戶端應用程式優化。  
  
 如果 `pwszBuildFlavor` 設定為 null，則會載入工作站組建。 在單處理器機器上執行時，一律會載入工作站組建，即使 `pwszBuildFlavor` 設定為也一樣 `svr` 。 不過，如果 `pwszBuildFlavor` 設定為 `svr` ，且指定了並行垃圾收集（請參閱參數的描述 `flags` ），則會載入伺服器組建。  
  
 `rclsid`  
 在Coclass 的，其 `CLSID` 會執行[ICorRuntimeHost](../../../../docs/framework/unmanaged-api/hosting/icorruntimehost-interface.md)或[ICLRRuntimeHost](iclrruntimehost-interface.md)介面。 支援的值為 CLSID_CorRuntimeHost 或 CLSID_CLRRuntimeHost。  
  
 `riid`  
 在`IID`從所要求之介面的 `rclsid` 。 支援的值為 IID_ICorRuntimeHost 或 IID_ICLRRuntimeHost。  
  
 `ppv`  
 脫銷傳回的介面指標 `riid` 。  
  
## <a name="remarks"></a>備註  
 如果 `pwszVersion` 指定不存在的執行階段版本，則會傳回 `CorBindToRuntimeEx` CLR_E_SHIM_RUNTIMELOAD 的 HRESULT 值。  
  
## <a name="execution-context-and-flow-of-windows-identity"></a>執行內容和 Windows 身分識別流程  
 在 CLR 的第1版中， <xref:System.Security.Principal.WindowsIdentity> 物件不會流經非同步點，例如新執行緒、執行緒集區或計時器回呼。 在 CLR 的版本2.0 中， <xref:System.Threading.ExecutionContext> 物件會包裝目前執行中線程的一些相關資訊，並將其流經任何非同步點，但不會跨越應用程式域界限。 同樣地， <xref:System.Security.Principal.WindowsIdentity> 物件也會流經任何非同步點。 因此，執行緒上目前的模擬（如果有的話）也會流動。  
  
 您可以透過兩種方式來改變流程：  
  
1. 藉由修改 <xref:System.Threading.ExecutionContext> 設定來隱藏每個執行緒的流程（請參閱 <xref:System.Threading.ExecutionContext.SuppressFlow%2A> 、 <xref:System.Security.SecurityContext.SuppressFlow%2A> 和 <xref:System.Security.SecurityContext.SuppressFlowWindowsIdentity%2A> 方法）。  
  
2. 將進程預設模式變更為版本1相容性模式，其中物件不 <xref:System.Security.Principal.WindowsIdentity> 會流經任何非同步點，而不論 <xref:System.Threading.ExecutionContext> 目前線程上的設定為何。 您變更預設模式的方式，取決於您使用的是受控可執行檔或非受控裝載介面來載入 CLR：  
  
    1. 對於受控可執行檔，您必須將 `enabled` [ \< legacyImpersonationPolicy>](../../configure-apps/file-schema/runtime/legacyimpersonationpolicy-element.md)專案的屬性設定為 `true` 。  
  
    2. 若為非受控裝載介面，請在呼叫函式時，于 `STARTUP_LEGACY_IMPERSONATION` 參數中設定旗標 `flags` `CorBindToRuntimeEx` 。  
  
     版本1相容性模式適用于整個進程和進程中的所有應用程式域。  
  
## <a name="remarks"></a>備註  
 [CorBindToRuntimeEx](corbindtoruntimeex-function.md)並 `CorBindToRuntime` 執行相同的作業，但函式可 `CorBindToRuntimeEx` 讓您設定旗標來指定 CLR 的行為。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** Mscoree.dll. h  
  
 連結**庫：** Mscoree.dll .dll  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [CorBindToCurrentRuntime 函式](corbindtocurrentruntime-function.md)
- [CorBindToRuntimeByCfg 函式](corbindtoruntimebycfg-function.md)
- [CorBindToRuntimeEx 函式](corbindtoruntimeex-function.md)
- [CorBindToRuntimeHost 函式](corbindtoruntimehost-function.md)
- [ICorRuntimeHost 介面](icorruntimehost-interface.md)
- [已被取代的 CLR 裝載函式](deprecated-clr-hosting-functions.md)
