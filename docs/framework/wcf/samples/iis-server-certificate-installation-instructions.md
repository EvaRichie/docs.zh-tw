---
title: 網際網路資訊服務 (IIS) 伺服器憑證安裝指示
ms.date: 03/30/2017
ms.assetid: 11281490-d2ac-4324-8f33-e7714611a34b
ms.openlocfilehash: 301a10c615a13a42e1a6e1b89d2724476ca4fbae
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84594656"
---
# <a name="internet-information-services-iis-server-certificate-installation-instructions"></a>網際網路資訊服務 (IIS) 伺服器憑證安裝指示
若要執行能與網際網路資訊服務 (IIS) 安全通訊的範例，您必須建立並安裝伺服器憑證。  
  
## <a name="step-1-creating-certificates"></a>步驟 1： 建立憑證  
 若要為您的電腦建立憑證，請以系統管理員許可權開啟 Visual Studio 的開發人員命令提示字元，然後執行每個使用與 IIS 安全通訊的範例中所包含的安裝程式 .bat。 請先確定路徑有將 Makecert.exe 上一層的資料夾包含在內，再執行此批次 (Batch) 檔。 下列命令是用來建立 Setup.bat 中的憑證。  
  
```console  
makecert -sr LocalMachine -ss My -n CN=ServiceModelSamples-HTTPS-Server -sky exchange -sk ServiceModelSamples-HTTPS-Key  
```  
  
## <a name="step-2-installing-certificates"></a>步驟 2： 安裝憑證  
 安裝您剛才建立的憑證所需的步驟，視您使用的 IIS 版本而定。  
  
#### <a name="to-install-iis-on-iis-51-windows-xp-and-iis-60-windows-server-2003"></a>在 IIS 5.1 (Windows XP) 和 IIS 6.0 (Windows Server 2003) 上安裝 IIS  
  
1. 開啟網際網路資訊服務管理員 MMC 嵌入式管理單元。  
  
2. 以滑鼠右鍵按一下 [預設的網站]，然後選取 [**屬性**]。  
  
3. 選取 [**目錄安全性**] 索引標籤。  
  
4. 按一下 [**伺服器憑證**] 按鈕。 [Web 伺服器憑證精靈] 隨即啟動。  
  
5. 完成精靈。 選取選項以指派憑證。 從顯示的憑證清單中，選取 ServiceModelSamples-HTTPS-Server 憑證。  
  
     ![IIS 憑證精靈](media/iiscertificate-wizard.GIF "IISCertificate_Wizard")  
  
6. 使用 HTTPS 位址，在瀏覽器中測試服務的存取權 `https://localhost/servicemodelsamples/service.svc` 。  
  
#### <a name="if-ssl-was-previously-configured-by-using-httpcfgexe"></a>如果先前是使用 Httpcfg.exe 設定 SSL  
  
1. 請使用 Makecert.exe (或執行 Setup.bat) 來建立伺服器憑證。  
  
2. 執行 IIS 管理員，並根據先前的步驟安裝憑證。  
  
3. 在用戶端程式加入下面這行程式碼。  
  
> [!IMPORTANT]
> 只有測試憑證才需要這段程式碼，例如 Makecert.exe 建立的憑證。 在實際執行程式碼中不建議這樣做。  
  
```csharp  
PermissiveCertificatePolicy.Enact("CN=ServiceModelSamples-HTTPS-Server");  
```  
  
#### <a name="to-install-iis-on-iis-70-windows-vista-and-windows-server-2008"></a>在 IIS 7.0 (Windows Vista 和 Windows Server 2008) 上安裝 IIS  
  
1. 在 [**開始**] 功能表中，按一下 [**執行**]，然後輸入**inetmgr**以開啟 [Internet Information Services （IIS） mmc 嵌入式管理單元]。  
  
2. 以滑鼠右鍵按一下 [**預設的網站**]，然後選取 [編輯系結 **...** ]  
  
3. 按一下 [**網站**系結] 對話方塊的 [**新增**] 按鈕。  
  
4. 從 [**類型**] 下拉式清單中選取 [ **HTTPS** ]。  
  
5. 從 [ **SSL 憑證**] 下拉式清單中選取 [ **ServiceModelSamples-HTTPS-伺服器**]，然後按一下 **[確定]**。  
  
6. 使用 HTTPS 位址，在瀏覽器中測試服務的存取權 `https://localhost/servicemodelsamples/service.svc` 。  
  
> [!NOTE]
> 因為您剛剛安裝的測試憑證不是受信任的憑證，您在瀏覽使用這個憑證保護的本機網址時，可能會碰到其他 Internet Explorer 安全性警告。  
  
## <a name="removing-certificates"></a>移除憑證  
  
- 依照前述指示使用 Internet Information Services 管理員，但是改為移除憑證或繫結，而非新增。  
  
- 使用下列命令移除電腦憑證。  
  
    ```console  
    httpcfg delete ssl -i 0.0.0.0:443  
    ```
