---
title: 訊息安全性憑證
ms.date: 03/30/2017
helpviewer_keywords:
- WS Security
ms.assetid: 909333b3-35ec-48f0-baff-9a50161896f6
ms.openlocfilehash: 1dec66631368543eecd548ac1ec9bbcda466d746
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84584844"
---
# <a name="message-security-certificate"></a>訊息安全性憑證
這個範例會示範如何實作應用程式，該應用程式會對用戶端使用搭配 X.509 v3 憑證驗證的 WS-Security，並要求使用伺服器之 X.509 v3 憑證進行驗證的伺服器。 這個範例會使用預設的設定值，使所有在用戶端與伺服器之間的應用程式訊息進行簽署與加密。 這個範例是以[WSHttpBinding](wshttpbinding.md)為基礎，由用戶端主控台程式和由 INTERNET INFORMATION SERVICES （IIS）所裝載的服務程式庫所組成。 服務會實作定義要求-回覆通訊模式的合約。  
  
> [!NOTE]
> 此範例的安裝程序與建置指示位於本主題的結尾。  
  
 這個範例示範如何使用組態控制驗證以及如何從安全性內容取得呼叫者身分識別，如下列範例程式碼所示。  

```csharp
public class CalculatorService : ICalculator  
{  
    public string GetCallerIdentity()  
    {  
        // The client certificate is not mapped to a Windows identity by default.  
        // ServiceSecurityContext.PrimaryIdentity is populated based on the information  
        // in the certificate that the client used to authenticate itself to the service.  
        return ServiceSecurityContext.Current.PrimaryIdentity.Name;  
    }  
    ...  
}  
```  
  
 服務會公開一個與服務進行通訊的端點，以及一個使用組態檔 (Web.config) 定義並透過 WS-MetadataExchange 通訊協定公開服務之 WSDL 文件的端點。 端點是由位址、繫結及合約所組成。 系結是以標準元素設定 [\<wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md) ，預設為使用訊息安全性。 這個範例會將 `clientCredentialType` 屬性設定為 Certificate 以要求用戶端驗證。  
  
```xml  
<system.serviceModel>  
    <protocolMapping>  
      <add scheme="http" binding="wsHttpBinding"/>  
    </protocolMapping>  
    <bindings>  
      <wsHttpBinding>  
        <!--   
        This configuration defines the security mode as Message and   
        the clientCredentialType as Certificate.  
        -->  
        <binding>  
          <security mode ="Message">  
            <message clientCredentialType="Certificate" />  
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
    <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="True"/>  
          <serviceDebug includeExceptionDetailInFaults="False" />  
          <!--   
        The serviceCredentials behavior allows one to define a service certificate.  
        A service certificate is used by the service to authenticate itself to its clients and to provide message protection.  
        This configuration references the "localhost" certificate installed during the setup instructions.  
        -->  
          <serviceCredentials>  
            <serviceCertificate findValue="localhost" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectName" />  
            <clientCertificate>  
              <!--   
            Setting the certificateValidationMode to PeerOrChainTrust means that if the certificate   
            is in the user's Trusted People store, then it will be trusted without performing a  
            validation of the certificate's issuer chain. This setting is used here for convenience so that the   
            sample can be run without having to have certificates issued by a certification authority (CA).  
            This setting is less secure than the default, ChainTrust. The security implications of this   
            setting should be carefully considered before using PeerOrChainTrust in production code.   
            -->  
              <authentication certificateValidationMode="PeerOrChainTrust" />  
            </clientCertificate>  
          </serviceCredentials>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
```  
  
 此行為會指定當用戶端驗證服務時所使用的服務認證。 伺服器憑證主體名稱是在元素的屬性中指定的 `findValue` [\<serviceCredentials>](../../configure-apps/file-schema/wcf/servicecredentials.md) 。  
  
```xml  
<!--For debugging purposes, set the includeExceptionDetailInFaults attribute to true.-->  
<behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="True"/>  
          <serviceDebug includeExceptionDetailInFaults="False" />  
          <!--   
        The serviceCredentials behavior allows one to define a service certificate.  
        A service certificate is used by the service to authenticate itself to its clients and to provide message protection.  
        This configuration references the "localhost" certificate installed during the setup instructions.  
        -->  
          <serviceCredentials>  
            <serviceCertificate findValue="localhost" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectName" />  
            <clientCertificate>  
              <!--   
            Setting the certificateValidationMode to PeerOrChainTrust means that if the certificate   
            is in the user's Trusted People store, then it will be trusted without performing a  
            validation of the certificate's issuer chain. This setting is used here for convenience so that the   
            sample can be run without having to have certificates issued by a certification authority (CA).  
            This setting is less secure than the default, ChainTrust. The security implications of this   
            setting should be carefully considered before using PeerOrChainTrust in production code.   
            -->  
              <authentication certificateValidationMode="PeerOrChainTrust" />  
            </clientCertificate>  
          </serviceCredentials>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
```  
  
 用戶端端點組態是由服務端點的絕對位址、繫結及合約所組成。 用戶端繫結會設定成適當的安全性模式與驗證模式。 在跨電腦案例中執行時，請確定服務端點位址已隨同變更。  
  
```xml  
<system.serviceModel>  
    <client>  
      <!-- Use a behavior to configure the client certificate to present to the service. -->  
      <endpoint address="http://localhost/servicemodelsamples/service.svc" binding="wsHttpBinding" bindingConfiguration="Binding1" behaviorConfiguration="ClientCertificateBehavior" contract="Microsoft.Samples.Certificate.ICalculator"/>  
    </client>  
  
    <bindings>  
      <wsHttpBinding>  
        <!--   
        This configuration defines the security mode as Message and   
        the clientCredentialType as Certificate.  
        -->  
        <binding name="Binding1">  
          <security mode="Message">  
            <message clientCredentialType="Certificate"/>  
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
...  
</system.serviceModel>  
```  
  
 用戶端實作可以透過組態檔或程式碼設定要使用的憑證。 下列範例會示範如何在組態檔中設定要使用的憑證。  
  
```xml  
<system.serviceModel>  
  ...  
  
<behaviors>  
      <endpointBehaviors>  
        <behavior name="ClientCertificateBehavior">  
          <!--   
        The clientCredentials behavior allows one to define a certificate to present to a service.  
        A certificate is used by a client to authenticate itself to the service and provide message integrity.  
        This configuration references the "client.com" certificate installed during the setup instructions.  
        -->  
          <clientCredentials>  
            <clientCertificate findValue="client.com" storeLocation="CurrentUser" storeName="My" x509FindType="FindBySubjectName"/>  
            <serviceCertificate>  
              <!--   
            Setting the certificateValidationMode to PeerOrChainTrust means that if the certificate   
            is in the user's Trusted People store, then it will be trusted without performing a  
            validation of the certificate's issuer chain. This setting is used here for convenience so that the   
            sample can be run without having to have certificates issued by a certificate authority (CA).  
            This setting is less secure than the default, ChainTrust. The security implications of this   
            setting should be carefully considered before using PeerOrChainTrust in production code.   
            -->  
              <authentication certificateValidationMode="PeerOrChainTrust"/>  
            </serviceCertificate>  
          </clientCredentials>  
        </behavior>  
      </endpointBehaviors>  
    </behaviors>  
  
</system.serviceModel>  
```  
  
 下列範例會示範如何在程式中呼叫服務。  

```csharp
// Create a client.  
CalculatorClient client = new CalculatorClient();  
  
// Call the GetCallerIdentity service operation.  
Console.WriteLine(client.GetCallerIdentity());  
...  
//Closing the client gracefully closes the connection and cleans up resources.  
client.Close();  
```
  
 當您執行範例時，作業要求和回應會顯示在用戶端主控台視窗中。 在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。  
  
```console  
CN=client.com  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
Press <ENTER> to terminate client.  
```  
  
 「訊息安全性」範例中所包含的 Setup.bat 批次檔可讓您使用相關的憑證設定用戶端與伺服器，以執行需要憑證安全性的裝載應用程式。 此批次檔可以執行於三種模式。 若要在單一電腦模式中執行，請在 Visual Studio 的開發人員命令提示字元中輸入**setup .bat** ;針對服務模式，請輸入**安裝程式 .bat 服務**;若是用戶端模式，請輸入**setup. .bat client**。 當跨電腦執行範例時，會使用用戶端與伺服器模式。 如需詳細資訊，請參閱本主題結尾的安裝程序。 下面提供批次檔的各區段簡要概觀，讓批次檔得以修改為在適當的組態下執行：  
  
- 建立用戶端憑證。  
  
     批次檔中的下列程式行會建立用戶端憑證。 在所建立之憑證主體的名稱中，會使用指定的用戶端名稱。 憑證會儲存在位於 `My` 存放區的 `CurrentUser` 存放區中。  
  
    ```bat
    echo ************  
    echo making client cert  
    echo ************  
    makecert.exe -sr CurrentUser -ss MY -a sha1 -n CN=%CLIENT_NAME% -sky exchange -pe  
    ```  
  
- 將用戶端憑證安裝至伺服器的受信任憑證存放區中。  
  
     批次檔中的下列程式行會將用戶端憑證複製到伺服器的 TrustedPeople 存放區，讓伺服器可以做出相關的信任或不信任決定。 為了讓安裝在 TrustedPeople 存放區中的憑證受 Windows Communication Foundation （WCF）服務信任，用戶端憑證驗證模式必須設定為 `PeerOrChainTrust` 或 `PeerTrust` 。 請參閱先前的服務組態範例，以了解如何使用組態檔完成這個工作。  
  
    ```bat
    echo ************  
    echo copying client cert to server's LocalMachine store  
    echo ************  
    certmgr.exe -add -r CurrentUser -s My -c -n %CLIENT_NAME% -r LocalMachine -s TrustedPeople
    ```  
  
- 建立伺服器憑證。  
  
     下列 Setup.bat 批次檔中的程式行會建立要使用的伺服器憑證。  
  
    ```bat
    echo ************  
    echo Server cert setup starting  
    echo %SERVER_NAME%  
    echo ************  
    echo making server cert  
    echo ************  
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe  
    ```  
  
     %SERVER_NAME% 變數會指定伺服器名稱。 憑證是儲存在 LocalMachine 存放區中。 如果安裝 .bat 批次檔是以服務的引數（例如，**安裝程式 .bat 服務**）執行，% SERVER_NAME% 就會包含電腦的完整功能變數名稱。 否則，預設為 localhost。  
  
- 將伺服器憑證安裝至用戶端的受信任憑證存放區中。  
  
     下列程式行會將伺服器憑證複製到用戶端受信任人的存放區中。 這是必要步驟，因為用戶端系統並未隱含信任 Makecert.exe 產生的憑證。 如果您已經有一個以用戶端信任的根憑證 (例如 Microsoft 所發行的憑證) 為基礎的憑證，就不需要這個將伺服器憑證填入用戶端憑證的步驟。  
  
    ```console  
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople  
    ```  
  
- 授與憑證私密金鑰的權限。  
  
     在安裝程式 .bat 檔案中的下列幾行，可讓 ASP.NET worker 進程帳戶存取儲存在 LocalMachine 存放區的伺服器憑證。  
  
    ```bat
    echo ************  
    echo setting privileges on server certificates  
    echo ************  
    for /F "delims=" %%i in ('"%ProgramFiles%\ServiceModelSampleTools\FindPrivateKey.exe" My LocalMachine -n CN^=%SERVER_NAME% -a') do set PRIVATE_KEY_FILE=%%i  
    set WP_ACCOUNT=NT AUTHORITY\NETWORK SERVICE  
    (ver | findstr /C:"5.1") && set WP_ACCOUNT=%COMPUTERNAME%\ASPNET  
    echo Y|cacls.exe "%PRIVATE_KEY_FILE%" /E /G "%WP_ACCOUNT%":R  
    iisreset  
    ```  
  
    > [!NOTE]
    > 如果您使用非英文版的 Windows，則必須編輯 .bat 檔案，並將 "NT AUTHORITY\NETWORK SERVICE" 帳戶名稱取代為您的對等區域。  
  
> [!NOTE]
> 在這個批次檔中使用的工具位於 C:\Program Files\Microsoft Visual Studio 8\Common7\tools 或 C:\Program Files\Microsoft SDKs\Windows\v6.0\bin。 上述其中一種目錄一定會出現在您的系統路徑中。 如果您已安裝 Visual Studio，在您的路徑中取得此目錄最簡單的方式是開啟 Visual Studio 的開發人員命令提示字元。 按一下 [**開始**]，然後選取 [**所有程式**]， **Visual Studio 2012**，[**工具**]。 這個命令提示字元包含已設定的適當路徑。 否則，您必須手動將適當目錄新增至您的路徑。  
  
> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續：  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> 如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄：  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\WS\MessageSecurity`  
  
### <a name="to-set-up-build-and-run-the-sample"></a>若要安裝、建置及執行範例  
  
1. 請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2. 若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。  
  
### <a name="to-run-the-sample-on-the-same-computer"></a>若要在同一部電腦上執行範例  
  
1. 以系統管理員許可權開啟 Visual Studio 的開發人員命令提示字元，然後從範例安裝資料夾中執行安裝程式 .bat。 這會安裝執行範例所需的所有憑證。  
  
    > [!NOTE]
    > 安裝 .bat 批次檔是設計用來從 Visual Studio 的開發人員命令提示字元執行。 它要求 path 環境變數指向安裝 SDK 的目錄。 此環境變數會在 Visual Studio 的開發人員命令提示字元中自動設定（2010）。  
  
2. 輸入位址以驗證使用瀏覽器存取服務 `http://localhost/servicemodelsamples/service.svc` 。  
  
3. 從 \client\bin 啟動 Client.exe。 用戶端活動會顯示在用戶端主控台應用程式上。  
  
4. 如果用戶端和服務無法通訊，請參閱[WCF 範例的疑難排解秘訣](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))。  
  
### <a name="to-run-the-sample-across-computers"></a>若要跨電腦執行範例  
  
1. 在服務電腦上建立目錄。 使用 Internet Information Services (IIS) 管理工具，為這個目錄建立名為 servicemodelsamples 的虛擬應用程式。  
  
2. 將 \inetpub\wwwroot\servicemodelsamples 中的服務程式檔複製至服務電腦上的虛擬目錄中。 確定複製 \bin 子目錄中的檔案。 同時將 Setup.bat、Cleanup.bat 和 ImportClientCert.bat 檔案複製到服務電腦。  
  
3. 在用戶端電腦上為用戶端二進位碼檔案建立一個目錄。  
  
4. 將用戶端程式檔複製到用戶端電腦上的用戶端目錄。 同時，將 Setup.bat、Cleanup.bat 和 ImportServiceCert.bat 檔案複製到用戶端。  
  
5. 在伺服器上，以系統管理員許可權 Visual Studio 的開發人員命令提示字元中執行**安裝程式 .bat 服務**。 使用**服務**引數執行**安裝程式 .bat** ，會使用電腦的完整功能變數名稱建立服務憑證，並將服務憑證匯出至名為 .cer 的檔案。  
  
6. 編輯 Web.config 以反映新的憑證名稱（在 `findValue` 的屬性中 [\<serviceCertificate>](../../configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md) ），這與電腦的完整功能變數名稱相同。  
  
7. 從服務目錄中將 Service.cer 檔案複製至用戶端電腦上的用戶端目錄。  
  
8. 在用戶端上，以系統管理員許可權在 Visual Studio 的開發人員命令提示字元中執行**安裝程式 .bat 用戶端**。 使用**client**引數執行**安裝程式 .bat**會建立名為 client.com 的用戶端憑證，並將用戶端憑證匯出至名為 client .cer 的檔案。  
  
9. 在用戶端電腦上的 Client.exe.config 檔案中，變更端點的位址值以符合服務的新位址。 若要這麼做，請使用伺服器的完整網域名稱取代 localhost。  
  
10. 從用戶端目錄將 Client.cer 檔案複製到伺服器上的服務目錄中。  
  
11. 在用戶端上，以系統管理許可權在 Visual Studio 的開發人員命令提示字元中執行 Importservicecert.bat。 這樣會將服務憑證從 Service.cer 檔案匯入至 CurrentUser - TrustedPeople 存放區中。  
  
12. 在伺服器上，以系統管理許可權在 Visual Studio 的開發人員命令提示字元中執行 Importclientcert.bat。 這樣便會從 Client.cer 檔將用戶端憑證匯入至 LocalMachine - TrustedPeople 存放區中。  
  
13. 在用戶端電腦上，從命令提示字元視窗啟動 Client.exe。 如果用戶端和服務無法通訊，請參閱[WCF 範例的疑難排解秘訣](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))。  
  
### <a name="to-clean-up-after-the-sample"></a>若要在使用範例之後進行清除  
  
- 當您完成執行範例後，請執行範例資料夾中的 Cleanup.bat。  
  
    > [!NOTE]
    > 跨電腦執行此範例時，這個指令碼不會移除用戶端上的服務憑證。 如果您已在電腦上執行使用憑證的 Windows Communication Foundation （WCF）範例，請務必清除已安裝在 CurrentUser-TrustedPeople 存放區中的服務憑證。 若要這麼做，請使用下列命令：`certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>`，例如：`certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`。  
