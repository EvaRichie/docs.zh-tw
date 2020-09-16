---
title: 訊息安全性範例
ms.date: 03/30/2017
ms.assetid: 82444166-6288-493a-85d4-85f43f134d19
ms.openlocfilehash: 02e758633f810d785c914152cbd4fbe687bea4f9
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90558624"
---
# <a name="message-security-sample"></a>訊息安全性範例
這個範例會示範如何實作一個使用 `basicHttpBinding` 和訊息安全性的應用程式。 這個範例是以實作為計算機服務的 [消費者入門](getting-started-sample.md) 為基礎。  
  
> [!NOTE]
> 此範例的安裝程序與建置指示位於本主題的結尾。  
  
 `basicHttpBinding` 的安全性模式可以設定為下列值：`Message`、`Transport`、`TransportWithMessageCredential`、`TransportCredentialOnly` 和 `None`。 在下列範例服務 App.config 檔中，端點定義會指定 `basicHttpBinding`，並參考名為 `Binding1` 的繫結組態，如下列範例組態所示：  
  
```xml  
<system.serviceModel>  
  <services>  
    <service name="Microsoft.ServiceModel.Samples.CalculatorService"  
             behaviorConfiguration="CalculatorServiceBehavior">  
     <!-- This endpoint is exposed at the base address provided by -->  
     <!-- host: http://localhost:8000/ServiceModelSamples/service.-->  
     <endpoint address=""  
               binding="basicHttpBinding"  
               bindingConfiguration="Binding1"
               contract="Microsoft.ServiceModel.Samples.ICalculator" />  
    </service>  
  </services>  
  ...  
</system.serviceModel>  
```  
  
 系結設定會將的 `mode` 屬性設定 [\<security>](../../configure-apps/file-schema/wcf/security-of-basichttpbinding.md) 為， `Message` 並將的 `clientCredentialType` 屬性設定 [\<message>](../../configure-apps/file-schema/wcf/message-of-basichttpbinding.md) 為， `Certificate` 如下列範例設定所示：  
  
```xml  
<bindings>  
  <basicHttpBinding>  
    <!--   
        This configuration defines the SecurityMode as Message and   
        the clientCredentialType as Certificate.  
        -->  
    <binding name="Binding1" >  
      <security mode = "Message">  
        <message clientCredentialType="Certificate"/>  
      </security>  
    </binding>  
  </basicHttpBinding>  
</bindings>  
```  
  
 服務對用戶端驗證它自己時所使用的憑證是在組態檔案行為區段中的 `serviceCredentials` 項目下設定。 用戶端用來對服務驗證本身之憑證所套用的驗證模式也是在 `clientCertificate` 項目下的行為區段中設定。  
  
```xml  
<!--For debugging purposes, set the includeExceptionDetailInFaults attribute to true.-->  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="CalculatorServiceBehavior">  
      <serviceMetadata httpGetEnabled="True"/>  
      <serviceDebug includeExceptionDetailInFaults="False" />  
      <!--The serviceCredentials behavior allows one to define a -->  
      <!--service certificate. A service certificate is used by a -->  
      <!--client to authenticate the service and provide message -->  
      <!-- protection. This configuration references the "localhost"-->  
      <!--certificate installed during the setup instructions. -->  
      <serviceCredentials>  
        <serviceCertificate findValue="localhost"  
               storeLocation="LocalMachine"
               storeName="My" x509FindType="FindBySubjectName" />  
        <clientCertificate>  
          <!-- Setting the certificateValidationMode to -->  
          <!-- PeerOrChainTrust means that if the certificate -->  
          <!--is in the user's Trusted People store, then it is -->  
          <!-- trusted without performing a validation of the -->  
          <!-- certificate's issuer chain. This setting is used -->  
          <!-- here for convenience so that the sample can be run -->  
          <!-- without having to have certificates issued by a -->  
          <!-- certification authority (CA). -->  
          <!-- This setting is less secure than the default, -->  
          <!-- ChainTrust. The security implications of this -->  
          <!-- setting should be carefully considered before using -->  
          <!-- PeerOrChainTrust in production code. -->  
          <authentication
                       certificateValidationMode="PeerOrChainTrust" />  
        </clientCertificate>  
      </serviceCredentials>  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
 相同的繫結和安全性詳細資訊是在用戶端組態檔中設定。  
  
 呼叫者的身分識別會透過下列程式碼顯示在服務主控台視窗中：  

```csharp
Console.WriteLine("Called by {0}", ServiceSecurityContext.Current.PrimaryIdentity.Name);  
```

 當您執行範例時，作業要求和回應會顯示在用戶端主控台視窗中。 在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。  
  
```console
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
Press <ENTER> to terminate client.  
```  
  
### <a name="to-set-up-and-build-the-sample"></a>若要設定和建置範例  
  
1. 確定您已 [針對 Windows Communication Foundation 範例執行一次性安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2. 若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。  
  
### <a name="to-run-the-sample-on-the-same-machine"></a>若要在同一部機器上執行範例  
  
1. 從範例安裝資料夾執行 Setup.bat。 這會安裝執行範例所需的所有憑證。  
  
    > [!NOTE]
    > Setup.bat 批次檔是設計用來從 Windows SDK 命令提示字元執行。 它要求 MSSDK 環境變數指向安裝 SDK 的目錄。 這個環境變數是自動在 Windows SDK 命令提示字元中設定。  
  
2. 從 \service\bin 執行服務應用程式。  
  
3. 從 \client\bin 執行用戶端應用程式。 用戶端活動會顯示在用戶端主控台應用程式上。  
  
4. 如果用戶端和服務無法通訊，請參閱 [WCF 範例的疑難排解提示](/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))。  
  
5. 當您完成範例時，請執行 Cleanup.bat 以移除憑證。 其他安全性範例使用相同的憑證。  
  
### <a name="to-run-the-sample-across-machines"></a>若要跨機器執行範例  
  
1. 在服務機器上為服務二進位碼檔案建立一個目錄。  
  
2. 將服務程式檔複製到伺服器的服務目錄上。 同時，將 Setup.bat、Cleanup.bat 和 ImportClientCert.bat 檔案複製到伺服器。  
  
3. 在用戶端機器上為用戶端二進位碼檔案建立一個目錄。  
  
4. 將用戶端程式檔複製到用戶端機器上的用戶端目錄。 同時，將 Setup.bat、Cleanup.bat 和 ImportServiceCert.bat 檔案複製到用戶端。  
  
5. 在伺服器上執行 `setup.bat service`。 `setup.bat`使用 `service` 引數執行時，會建立具有電腦完整功能變數名稱的服務憑證，並將服務憑證匯出至名為 service .cer 的檔案。  
  
6. 編輯 Service.exe.config，以反映元素) 中的新憑證名稱 (， `findValue` [\<serviceCertificate>](../../configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md) 其與電腦的完整功能變數名稱相同。 同時將基底位址的值變更成指定完整機器名稱，而不要指定 localhost`.`。  
  
7. 從服務目錄中將 Service.cer 檔案複製至用戶端機器上的用戶端目錄。  
  
8. 在用戶端上執行 `setup.bat client`。 使用 `setup.bat` 引數來執行 `client`，就會建立名稱為 client.com 的用戶端憑證，並且會將用戶端憑證匯出為名為 Client.cer 的檔案。  
  
9. 在用戶端機器上的 Client.exe.config 檔案中，變更端點的位址值以符合服務的新位址。 您可以藉由使用伺服器的完整網域名稱取代 localhost，完成這個動作。 也將的 `findValue` 屬性變更 [\<defaultCertificate>](../../configure-apps/file-schema/wcf/defaultcertificate-element.md) 為新的服務憑證名稱，此名稱是伺服器的完整功能變數名稱。  
  
10. 從用戶端目錄將 Client.cer 檔案複製到伺服器上的服務目錄中。  
  
11. 在用戶端上執行 ImportServiceCert.bat。 這樣會將服務憑證從 Service.cer 檔案匯入至 CurrentUser - TrustedPeople 存放區中。  
  
12. 在伺服器上執行 ImportClientCert.bat，這樣會從 Client.cer 檔案中將用戶端憑證匯入至 LocalMachine - TrustedPeople 存放區中。  
  
13. 在服務機器上，從命令提示字元執行 Service.exe。  
  
14. 在用戶端機器上，從命令提示字元視窗啟動 Client.exe。  
  
    1. 如果用戶端和服務無法通訊，請參閱 [WCF 範例的疑難排解提示](/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))。  
  
### <a name="to-clean-up-after-the-sample"></a>若要在使用範例之後進行清除  
  
- 當您完成執行範例後，請執行範例資料夾中的 Cleanup.bat。  
  
    > [!NOTE]
    > 跨機器執行此範例時，這個指令碼不會移除用戶端上的服務憑證。 如果您已執行 Windows Communication Foundation (使用跨電腦憑證的 WCF) 範例，請務必清除 TrustedPeople 存放區中已安裝的服務憑證。 若要這麼做，請使用下列命令：`certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>`，例如：`certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`。  
  
> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> 如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\Basic\MessageSecurity`
