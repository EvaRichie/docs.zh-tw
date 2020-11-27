---
title: WorkFlow 服務登錄工具 (WFServicesReg.exe)
ms.date: 03/30/2017
ms.assetid: 9e92c87b-99c5-4e8d-9d53-7944cc2b47d3
ms.openlocfilehash: 763b617a99c98383b5b873e4fb8646884f9b5253
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96261874"
---
# <a name="workflow-service-registration-tool-wfservicesregexe"></a>WorkFlow 服務登錄工具 (WFServicesReg.exe)

Workflow 服務登錄工具 (WFServicesReg.exe) 是一個獨立工具，可用於新增、移除或修復 Windows Workflow Foundation (WF) 服務的組態項目。  
  
## <a name="syntax"></a>語法  
  
```console  
WFServicesReg.exe [-c | -r | -v | -m | -i]  
```  
  
## <a name="remarks"></a>備註  

 您可以在 .NET Framework 3.5 安裝位置（尤其是%windir%\Microsoft.NET\Framework\v3.5）或64位電腦的%windir%\Microsoft.NET\Framework64\v3.5 中找到此工具。  
  
 下表描述可與 Workflow 服務登錄工具 (WFServicesReg.exe) 搭配使用的選項。  
  
|選項|描述|  
|------------|-----------------|  
|`/c`|設定 Windows 工作流程服務。 用於安裝和修復案例中。|  
|`/r`|移除 Windows 工作流程服務組態。|  
|`/v`|列印詳細資訊 (適用於設定或移除)。|  
|`/m`|啟用 MSI 記錄格式。|  
|`/i`|應用程式執行時，最小化視窗。|  
  
## <a name="registration"></a>註冊  

 工具會檢查 Web.config 檔案並註冊下列項目：  
  
- .NET Framework 3.5 參考元件。  
  
- .xoml 檔案的組建提供者。  
  
- .xoml 和 .rules 檔案的 HTTP 處理常式。  
  
 工具會檢查 Machine.config 檔案並註冊下列延伸項目：  
  
- behaviorExtensions  
  
- bindingElementExtensions  
  
- bindingExtensions  
  
 工具也會註冊下列用戶端中繼資料匯入工具：  
  
- policyImporters  
  
- wsdlImporters  
  
 工具也會在 IIS Metabase 中註冊 .xoml 和 .rules Scriptmap 與處理常式。  
  
 在 Windows Server 2003 和 Windows XP 電腦上 (IIS 5.1 和 IIS 6.0) ，會註冊一組 xoml 和。  
  
 在 64 位元電腦上，如果已啟用 `Enable32BitAppOnWin64` 參數，此工具就會註冊 WOW 模式 Scriptmap，如果已停用 `Enable32BitAppOnWin64` 參數，則會註冊原生 64 位元 Scriptmap。  
  
 在 Windows Vista 和 Windows Server 2008 (IIS 7.0 和更新版本) 電腦上，會註冊兩組 xoml 和. 規則處理常式：一組用於整合模式，另一組用於傳統模式。  
  
 在 64 位元電腦上，會註冊三組處理常式 (無論 `Enable32BitAppOnWin64` 參數的狀態為何)：一組用於整合模式，一組用於 WOW 傳統模式，一組用於原生 64 位元傳統模式。  
  
> [!NOTE]
> 與 ServiceModelreg.exe 不同的是，WFServicesReg.exe 不允許新增、移除或修復用於特定網站的 Scriptmap 或處理常式。 如需這個問題的解決方法，請參閱「修復 Scriptmap」一節。  
  
## <a name="usage-scenarios"></a>使用案例  
  
### <a name="installing-iis-after-net-framework-35-is-installed"></a>在安裝 .NET Framework 3.5 之後安裝 IIS  

 在 Windows Server 2003 電腦上，.NET Framework 3.5 會在安裝 IIS 之前安裝。 由於 IIS 的元資料庫無法使用，因此 .NET Framework 3.5 的安裝會成功，而不需要安裝 xoml 和. 規則腳本。  
  
 安裝 IIS 之後，您可以使用 WFServicesReg.exe 工具搭配 `/c` 參數來安裝這些特定 Scriptmap。  
  
### <a name="repairing-the-scriptmaps"></a>修復 Scriptmap  
  
#### <a name="scriptmap-deleted-under-web-sites-node"></a>在網站節點下刪除的 Scriptmap  

 在 Windows Server 2003 電腦上，xoml 或。不小心刪除 [網站] 節點中的規則。 您可以使用 `/c` 參數執行 WFServicesReg.exe 工具修復這種情況。  
  
#### <a name="scriptmap-deleted-under-a-particular-web-site"></a>在特定網站下刪除的 Scriptmap  

 在 Windows Server 2003 電腦上，xoml 或。不小心刪除特定網站 (例如，預設的網站) ，而不是從 [網站] 節點。  
  
 若要修復特定網站的已刪除處理常式，您應該執行 "WFServicesReg.exe/r" 來移除所有網站的處理常式，然後執行 "WFServicesReg.exe/c" 來為所有網站建立適當的處理常式。  
  
### <a name="configuring-handlers-after-switching-iis-mode"></a>在切換 IIS 模式之後設定處理常式  

 當 IIS 處於共用設定模式，且安裝了 .NET Framework 3.5 時，就會在共用位置下設定 IIS 元資料庫。 如果將 IIS 切換為非共用組態模式，本機 Metabase 將不會包含所需的處理常式。 若要正確設定本機的元資料庫，您可以將共用的元資料庫匯入至本機，或執行 "WFServicesReg.exe/c"，以設定本機的元資料庫。
