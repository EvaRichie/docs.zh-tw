---
title: 訊息安全性匿名
ms.date: 03/30/2017
helpviewer_keywords:
- WS Security
ms.assetid: c321cbf9-8c05-4cce-b5a5-4bf7b230ee03
ms.openlocfilehash: 95101b8ec4f5a7fc60d0233ab6685b5c6851b44e
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84584972"
---
# <a name="message-security-anonymous"></a>訊息安全性匿名
訊息安全性匿名範例示範如何使用不具用戶端驗證的訊息層級安全性來執行 Windows Communication Foundation （WCF）應用程式，但這需要使用伺服器的 x.509 憑證來進行伺服器驗證。 用戶端與伺服器之間的所有應用程式訊息都會經過簽署及加密。 這個範例是以[WSHttpBinding](wshttpbinding.md)範例為基礎。 這個範例是由用戶端主控台程式 (.exe) 和網際網路資訊服務 (IIS) 所裝載的服務程式庫 (.dll) 所組成。 服務會實作定義要求-回覆通訊模式的合約。

> [!NOTE]
> 此範例的安裝程序與建置指示位於本主題的結尾。

 這個範例會將新作業新增至計算機介面，該介面會在用戶端未通過驗證時傳回 `True`。

```csharp
public class CalculatorService : ICalculator
{
    public bool IsCallerAnonymous()
    {
        // ServiceSecurityContext.IsAnonymous returns true if the caller is not authenticated.
        return ServiceSecurityContext.Current.IsAnonymous;
    }
    ...
}
```

 此服務會公開 (Expose) 單一的端點來與已使用組態檔 Web.config 定義之服務進行通訊。 端點是由位址、繫結及合約所組成。 此繫結是使用指定的 `wsHttpBinding` 繫結所設定的。 `wsHttpBinding` 繫結的預設安全性模式為 `Message`。 `clientCredentialType` 屬性會設定為 `None`。

```xml
<system.serviceModel>

  <protocolMapping>
    <add scheme="http" binding="wsHttpBinding" />
  </protocolMapping>

  <bindings>
    <wsHttpBinding>
     <!-- This configuration defines the security mode as Message and -->
     <!-- the clientCredentialType as None. This mode provides -->
     <!-- server authentication only using the service certificate. -->

     <binding>
       <security mode="Message">
         <message clientCredentialType="None" />
       </security>
     </binding>
    </wsHttpBinding>
  </bindings>
  ...
</system.serviceModel>
```

 要用於服務驗證的認證會在中指定 [\<behavior>](../../configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md) 。 伺服器憑證中包含的 `SubjectName` 值必須與 `findValue` 屬性的指定值相同，如下列範例程式碼所示。

```xml
<behaviors>
  <serviceBehaviors>
    <behavior>
      <!--
    The serviceCredentials behavior allows you to define a service certificate.
    A service certificate is used by a client to authenticate the service and provide message protection.
    This configuration references the "localhost" certificate installed during the setup instructions.
    -->
      <serviceCredentials>
        <serviceCertificate findValue="localhost" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectName" />
      </serviceCredentials>
      <serviceMetadata httpGetEnabled="True"/>
      <serviceDebug includeExceptionDetailInFaults="False" />
    </behavior>
  </serviceBehaviors>
</behaviors>
```

 用戶端端點組態是由服務端點的絕對位址、繫結及合約所組成。 `wsHttpBinding` 繫結的用戶端安全性模式為 `Message`。 `clientCredentialType` 屬性會設定為 `None`。

```xml
<system.serviceModel>
  <client>
    <endpoint name=""
             address="http://localhost/servicemodelsamples/service.svc"
             binding="wsHttpBinding"
             behaviorConfiguration="ClientCredentialsBehavior"
             bindingConfiguration="Binding1"
             contract="Microsoft.ServiceModel.Samples.ICalculator" />
  </client>

  <bindings>
    <wsHttpBinding>
      <!--This configuration defines the security mode as -->
      <!--Message and the clientCredentialType as None. -->
      <binding name="Binding1">
        <security mode = "Message">
          <message clientCredentialType="None"/>
        </security>
      </binding>
    </wsHttpBinding>
  </bindings>
  ...
</system.serviceModel>
```

 此範例會將 <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication.CertificateValidationMode%2A> 設定為 <xref:System.ServiceModel.Security.X509CertificateValidationMode.PeerOrChainTrust> 以驗證服務的憑證。 此項作業會在用戶端 App.config 檔的 `behaviors` 區段中完成。 這表示如果憑證位在使用者之受信任人的存放區，則此憑證就受到信任，而不會執行驗證憑證的簽發者鏈結。 範例中是基於方便而使用這項設定，這樣便能夠在不需要憑證授權單位 (CA) 發出之憑證的情況下執行此範例。 這個設定的安全性比預設值 (ChainTrust) 低。 在實際執行程式碼 (Production Code) 中使用 `PeerOrChainTrust` 之前，應該要謹慎考量這項設定。

 用戶端執行會將呼叫新增至 `IsCallerAnonymous` 方法，否則不會與[WSHttpBinding](wshttpbinding.md)範例不同。

```csharp
// Create a client with a client endpoint configuration.
CalculatorClient client = new CalculatorClient();

// Call the GetCallerIdentity operation.
Console.WriteLine("IsCallerAnonymous returned: {0}", client.IsCallerAnonymous());

// Call the Add service operation.
double value1 = 100.00D;
double value2 = 15.99D;
double result = client.Add(value1, value2);
Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);

...

//Closing the client gracefully closes the connection and cleans up resources.
client.Close();

Console.WriteLine();
Console.WriteLine("Press <ENTER> to terminate client.");
Console.ReadLine();
```

 當您執行範例時，作業要求和回應會顯示在用戶端主控台視窗中。 在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。

```console
IsCallerAnonymous returned: True
Add(100,15.99) = 115.99
Subtract(145,76.54) = 68.46
Multiply(9,81.25) = 731.25
Divide(22,7) = 3.14285714285714
Press <ENTER> to terminate client.
```

 訊息安全性匿名範例所包含的 Setup.bat 批次檔可讓您使用相關的憑證設定伺服器，以執行需要憑證安全性的裝載應用程式。 此批次檔可以在兩種模式中執行。 若要在單一電腦模式中執行此批次檔，請在命令列中輸入 `setup.bat`。 若要在服務模式中執行此批次檔，請輸入 `setup.bat service`。 請在跨電腦執行範例時使用這個模式。 如需詳細資訊，請參閱本主題結尾的安裝程序。

 下面會提供批次檔之不同區段的簡短概觀。

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

     %SERVER_NAME% 變數會指定伺服器名稱。 憑證是儲存在 LocalMachine 存放區中。 如果使用 service 引數執行安裝批次檔 (例如 `setup.bat service`)，%SERVER_NAME% 就會包含電腦的完整網域名稱。 否則，預設為 localhost。

- 將伺服器憑證安裝至用戶端的受信任憑證存放區中。

     下列程式行會將伺服器憑證複製到用戶端受信任人的存放區中。 這是必要步驟，因為用戶端系統並未隱含信任 Makecert.exe 產生的憑證。 如果您已經有一個以用戶端信任的根憑證 (例如 Microsoft 所發行的憑證) 為基礎的憑證，就不需要這個將伺服器憑證填入用戶端憑證的步驟。

    ```console
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople
    ```

- 授與憑證私密金鑰的權限。

     安裝程式 .bat 批次檔中的下列幾行，可讓 ASP.NET worker 進程帳戶存取儲存在 LocalMachine 存放區的伺服器憑證。

    ```bat
    echo ************
    echo setting privileges on server certificates
    echo ************
    for /F "delims=" %%i in ('"%MSSDK%\bin\FindPrivateKey.exe" My LocalMachine -n CN^=%SERVER_NAME% -a') do set PRIVATE_KEY_FILE=%%i set WP_ACCOUNT=NT AUTHORITY\NETWORK SERVICE
    (ver | findstr "5.1") && set WP_ACCOUNT=%COMPUTERNAME%\ASPNET
    echo Y|cacls.exe "%PRIVATE_KEY_FILE%" /E /G "%WP_ACCOUNT%":R
    iisreset
    ```

> [!NOTE]
> 如果您使用非英文版的 Windows，則必須編輯安裝 .bat 檔案，並將 `NT AUTHORITY\NETWORK SERVICE` 帳戶名稱取代為您的對等區域。

### <a name="to-set-up-build-and-run-the-sample"></a>若要安裝、建置及執行範例

1. 請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。

2. 若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。

### <a name="to-run-the-sample-on-the-same-computer"></a>若要在同一部電腦上執行範例

1. 確認路徑中包含 Makecert.exe 和 FindPrivateKey.exe 所在的資料夾。

2. 從開發人員命令提示字元中的範例安裝資料夾執行安裝程式 .bat，Visual Studio 以系統管理員許可權執行。 這會安裝執行範例所需的所有憑證。

    > [!NOTE]
    > 安裝批次檔是設計用來從 Visual Studio 的開發人員命令提示字元執行。 它要求 path 環境變數指向安裝 SDK 的目錄。 此環境變數會在 Visual Studio 的開發人員命令提示字元中自動設定。  
  
3. 輸入位址以驗證使用瀏覽器存取服務 `http://localhost/servicemodelsamples/service.svc` 。  
  
4. 從 \client\bin 啟動 Client.exe。 用戶端活動會顯示在用戶端主控台應用程式上。  
  
5. 如果用戶端和服務無法通訊，請參閱[WCF 範例的疑難排解秘訣](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))。  
  
### <a name="to-run-the-sample-across-computers"></a>若要跨電腦執行範例  
  
1. 在服務電腦上建立目錄。 使用 Internet Information Services (IIS) 管理工具，為這個目錄建立名為 servicemodelsamples 的虛擬應用程式。  
  
2. 將 \inetpub\wwwroot\servicemodelsamples 中的服務程式檔複製至服務電腦上的虛擬目錄中。 確定複製 \bin 子目錄中的檔案。 同時，將 Setup.bat 和 Cleanup.bat 檔案複製到服務電腦中。  
  
3. 在用戶端電腦上為用戶端二進位碼檔案建立一個目錄。  
  
4. 將用戶端程式檔複製到用戶端電腦上的用戶端目錄。 同時，將 Setup.bat、Cleanup.bat 和 ImportServiceCert.bat 檔案複製到用戶端。  
  
5. 在伺服器上，于 `setup.bat service` 使用系統管理員許可權開啟 Visual Studio 的開發人員命令提示字元中執行。 `setup.bat`使用引數執行時，會 `service` 建立具有電腦完整功能變數名稱的服務憑證，並將服務憑證匯出至名為 .cer 的檔案。  
  
6. 編輯 Web.config 以反映新的憑證名稱（在 `findValue` 的屬性中 [\<serviceCertificate>](../../configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md) ），這與電腦的完整功能變數名稱相同。  
  
7. 從服務目錄中將 Service.cer 檔案複製至用戶端電腦上的用戶端目錄。  
  
8. 在用戶端電腦上的 Client.exe.config 檔案中，變更端點的位址值以符合服務的新位址。  
  
9. 在用戶端上，于 Visual Studio 以系統管理員許可權開啟的開發人員命令提示字元中執行 Importservicecert.bat。 這樣會將服務憑證從 Service.cer 檔案匯入至 CurrentUser - TrustedPeople 存放區中。  
  
10. 在用戶端電腦上，從命令提示字元啟動 Client.exe。 如果用戶端和服務無法通訊，請參閱[WCF 範例的疑難排解秘訣](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))。  
  
### <a name="to-clean-up-after-the-sample"></a>若要在使用範例之後進行清除  
  
- 當您完成執行範例後，請執行範例資料夾中的 Cleanup.bat。  
  
> [!NOTE]
> 跨電腦執行此範例時，這個指令碼不會移除用戶端上的服務憑證。 如果您已在電腦上執行使用憑證的 Windows Communication Foundation （WCF）範例，請務必清除已安裝在 CurrentUser-TrustedPeople 存放區中的服務憑證。 若要這麼做，請使用下列命令：`certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>`，例如：`certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com.`。
