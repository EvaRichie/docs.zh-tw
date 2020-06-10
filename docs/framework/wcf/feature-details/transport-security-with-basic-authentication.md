---
title: 基本驗證的傳輸安全性
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: b54f491d-196b-4279-876c-76b83ec0442c
ms.openlocfilehash: 7c83de70e404fe8304bc2e35c1bb5df9e42f95b7
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84576092"
---
# <a name="transport-security-with-basic-authentication"></a>基本驗證的傳輸安全性
下圖顯示 Windows Communication Foundation （WCF）服務和用戶端。 伺服器需要可用於 Secure Sockets Layer (SSL) 的有效 X.509 憑證，而用戶端必須信任伺服器的憑證。 此外，Web 服務已經有可以使用的 SSL 實作。 如需在 Internet Information Services （IIS）上啟用基本驗證的詳細資訊，請參閱 <https://docs.microsoft.com/iis/configuration/system.webserver/security/authentication/basicauthentication> 。  
  
 ![顯示使用基本驗證之傳輸安全性的螢幕擷取畫面。](./media/transport-security-with-basic-authentication/transport-security-basic-authentication.gif)  
  
|特性|描述|  
|--------------------|-----------------|  
|安全性模式|傳輸|  
|互通性|使用現有的 Web 服務用戶端和服務|  
|驗證 (伺服器)<br /><br /> 驗證 (用戶端)|是 (使用 HTTPS)<br /><br /> 是 (透過使用者名稱/密碼)|  
|完整性|是|  
|保密|是|  
|傳輸|HTTPS|  
|繫結|<xref:System.ServiceModel.WSHttpBinding>|  
  
## <a name="service"></a>服務  
 下列程式碼和組態要獨立執行。 執行下列其中一個動作：  
  
- 使用不含組態的程式碼建立獨立服務。  
  
- 使用提供的組態建立服務，但不要定義任何端點。  
  
### <a name="code"></a>程式碼  
 下列程式碼顯示如何為傳輸安全性建立使用 Windows 網域使用者名稱和密碼的服務端點。 請注意，服務需要 X.509 憑證來驗證用戶端。 如需詳細資訊，請參閱使用[憑證](working-with-certificates.md)和[如何：使用 SSL 憑證設定埠](how-to-configure-a-port-with-an-ssl-certificate.md)。  
  
 [!code-csharp[C_SecurityScenarios#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#1)]
 [!code-vb[C_SecurityScenarios#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#1)]  
  
## <a name="configuration"></a>組態  
 下列會設定服務以使用具有傳輸層級安全性的基本驗證：  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
    <system.serviceModel>  
        <bindings>  
            <wsHttpBinding>  
                <binding name="UsernameWithTransport">  
                    <security mode="Transport">  
                        <transport clientCredentialType="Basic" />  
                    </security>  
                </binding>  
            </wsHttpBinding>  
        </bindings>  
        <services>  
            <service name="BasicAuthentication.Calculator">  
                <endpoint address="https://localhost/Calculator"  
                          binding="wsHttpBinding"
                          bindingConfiguration="UsernameWithTransport"  
                          name="BasicEndpoint"
                          contract="BasicAuthentication.ICalculator" />  
            </service>  
        </services>  
    </system.serviceModel>  
</configuration>  
```  
  
## <a name="client"></a>用戶端  
  
### <a name="code"></a>程式碼  
 下列程式碼顯示包含使用者名稱和密碼的用戶端程式碼。 請注意，使用者必須提供有效的 Windows 使用者名稱和密碼。 此處未顯示傳回使用者名稱和密碼的程式碼。 請使用對話方塊或其他介面向使用者查詢資訊。  
  
> [!NOTE]
> 使用者名稱和密碼只能使用程式碼來設定。  
  
 [!code-csharp[C_SecurityScenarios#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#2)]
 [!code-vb[C_SecurityScenarios#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#2)]  
  
### <a name="configuration"></a>組態  
 下列程式碼顯示用戶端組態。  
  
> [!NOTE]
> 您不能使用組態來設定使用者名稱和密碼。 此處所示的組態必須使用程式碼來增強，以設定使用者名稱和密碼。  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <bindings>  
      <wsHttpBinding>  
        <binding name="WSHttpBinding_ICalculator" >  
          <security mode="Transport">  
            <transport clientCredentialType="Basic" />  
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
    <client>  
      <endpoint address="https://machineName/Calculator"
                binding="wsHttpBinding"  
                bindingConfiguration="WSHttpBinding_ICalculator"
                contract="ICalculator"  
                name="WSHttpBinding_ICalculator" />  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a>請參閱

- <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A>
- <xref:System.ServiceModel.Security.UserNamePasswordClientCredential>
- [Working with Certificates](working-with-certificates.md)
- [如何：使用 SSL 憑證設定連接埠](how-to-configure-a-port-with-an-ssl-certificate.md)
- [安全性總覽](security-overview.md)
- [\<clientCredentials>](../../configure-apps/file-schema/wcf/clientcredentials.md)
- [Windows Server AppFabric 的資訊安全模型](https://docs.microsoft.com/previous-versions/appfabric/ee677202(v=azure.10))
