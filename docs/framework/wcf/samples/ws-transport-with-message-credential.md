---
title: 使用訊息認證的 WS 傳輸
ms.date: 03/30/2017
ms.assetid: 0d092f3a-b309-439b-920b-66d8f46a0e3c
ms.openlocfilehash: 0082a9df5c112b66315236aad91bc891b80d27c7
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84596380"
---
# <a name="ws-transport-with-message-credential"></a>使用訊息認證的 WS 傳輸
這個範例會示範結合訊息中傳遞的用戶端認證來使用 SSL 傳輸安全性。 這個範例會使用 `wsHttpBinding` 繫結。  
  
 根據預設，`wsHttpBinding` 繫結會提供 HTTP 通訊。 當針對傳輸安全性設定時，此繫結會支援 HTTPS 通訊。 HTTPS 會保護在網路上傳輸之訊息的機密性與完整性。 但是，可以用來驗證服務之用戶端的驗證機制集合會受限於 HTTPS 傳輸所支援的機制。 Windows Communication Foundation （WCF）提供了一種 `TransportWithMessageCredential` 安全性模式，其設計目的是為了克服這項限制。 如果是設定這種安全性模式，傳輸安全性就會用來提供所傳輸訊息的機密性與完整性，以及用來執行服務驗證。 不過，用戶端驗證的執行方式是將用戶端認證直接放在訊息中。 這可讓您使用訊息安全性模式支援的任何認證類型進行用戶端驗證，同時保持傳輸安全性模式的效能優勢。  
  
 在這個範例中，`UserName` 認證類型會用來驗證服務的用戶端。  
  
 這個範例是以執行計算機服務的[消費者入門](getting-started-sample.md)為基礎。 `wsHttpBinding` 繫結會指定並設定在用戶端和服務的應用程式組態檔中。  
  
> [!NOTE]
> 此範例的安裝程序與建置指示位於本主題的結尾。  
  
 範例中的程式碼幾乎與[消費者入門](getting-started-sample.md)服務相同。 服務合約則另外提供一項作業 - `GetCallerIdentity`。 這個作業會將呼叫者身分識別名稱傳回呼叫者。  

```csharp
public string GetCallerIdentity()  
{  
    // Use ServiceSecurityContext.WindowsIdentity to get the name of the caller.  
    return ServiceSecurityContext.Current.WindowsIdentity.Name;  
}  
```

 您必須建立一個憑證並使用 [Web 伺服器憑證精靈] 指派憑證，再建置及執行範例。 組態檔設定中的端點定義與繫結定義會啟用 `TransportWithMessageCredential` 安全性模式，如同下列用戶端的範例組態所示。  
  
```xml  
<system.serviceModel>  
  <client>  
    <endpoint name=""  
              address="https://localhost/servicemodelsamples/service.svc"
              binding="wsHttpBinding"
              bindingConfiguration="Binding1"
              contract="Microsoft.ServiceModel.Samples.ICalculator" />  
  </client>  
  
  <bindings>  
    <wsHttpBinding>  
      <!--   
        This configuration defines the security mode as TransportWithMessageCredential.  
        and the clientCredentialType as UserName.  
        -->  
      <binding name="Binding1">  
        <security mode ="TransportWithMessageCredential">  
          <message clientCredentialType="UserName" />  
        </security>  
      </binding>  
    </wsHttpBinding>  
  </bindings>  
</system.serviceModel>  
```  
  
 指定的位址會使用 `https://` 配置。 繫結組態會將安全性模式設定為 `TransportWithMessageCredential`。 相同的安全性模式必須指定在服務的 Web.config 檔中。  
  
 因為此範例中使用的憑證是使用 Makecert 建立的測試憑證，所以當您嘗試從瀏覽器存取 HTTPs：位址（例如）時，就會出現安全性警示 `https://localhost/servicemodelsamples/service.svc` 。 為了讓 WCF 用戶端能夠使用測試憑證，已將一些額外的程式碼新增至用戶端，以隱藏安全性警示。 使用實際執行憑證時，不需要這個程式碼及伴隨的類別。  

```csharp
// WARNING: This code is only needed for test certificates such as those created by makecert. It is
// not recommended for production code.  
PermissiveCertificatePolicy.Enact("CN=ServiceModelSamples-HTTPS-Server");  
```
  
 當您執行範例時，作業要求和回應會顯示在用戶端主控台視窗中。 在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。  
  
```console  
Username authentication required.  
Provide a valid machine or domain account. [domain\\user]  
   Enter username:
YourDomainName\YourAccountName  
   Enter password:
********  
YourDomainName\YourAccountName  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
```  
  
### <a name="to-set-up-build-and-run-the-sample"></a>若要安裝、建置及執行範例  
  
1. 請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2. 請確定您已執行[Internet Information Services （IIS）伺服器憑證安裝指示](iis-server-certificate-installation-instructions.md)。  
  
3. 若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。  
  
4. 若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。  
