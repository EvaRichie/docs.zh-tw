---
title: Windows 驗證的傳輸安全性
description: 請參閱此案例，其中顯示由 Windows 安全性保護的 WCF 用戶端/服務。 在此範例中，內部網路服務會顯示人力資源資訊。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 96dd26e2-46e7-4de0-9a29-4fcb05bf187b
ms.openlocfilehash: b6134d4cbdff0c1adea704a7f3aaff7e40fd75ec
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85244760"
---
# <a name="transport-security-with-windows-authentication"></a>Windows 驗證的傳輸安全性
下列案例顯示由 Windows 安全性保護的 Windows Communication Foundation （WCF）用戶端和服務。 如需程式設計的詳細資訊，請參閱[如何：使用 Windows 認證保護服務](../how-to-secure-a-service-with-windows-credentials.md)。  
  
 內部網路 Web 服務顯示人力資源資訊。 用戶端為 Windows Form 應用程式。 應用程式部署於由 Kerberos 控制站負責網域安全的網域內。  
  
 ![使用 Windows 驗證的傳輸安全性](./media/transport-security-with-windows-authentication/secured-windows-authentication.gif)  
  
|特性|描述|  
|--------------------|-----------------|  
|安全性模式|傳輸|  
|互通性|僅限 WCF|  
|驗證 (伺服器)<br /><br /> 驗證 (用戶端)|是 (使用 Windows 整合式驗證)<br /><br /> 是 (使用 Windows 整合式驗證)|  
|完整性|Yes|  
|保密|Yes|  
|傳輸|NET.TCP|  
|繫結|<xref:System.ServiceModel.NetTcpBinding>|  
  
## <a name="service"></a>服務  
 下列程式碼和組態要獨立執行。 執行下列其中一個動作：  
  
- 使用不含組態的程式碼建立獨立服務。  
  
- 使用提供的組態建立服務，但不要定義任何端點。  
  
### <a name="code"></a>程式碼  
 下列程式碼顯示如何建立使用 Windows 安全性的服務端點。  
  
 [!code-csharp[C_SecurityScenarios#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#3)]
 [!code-vb[C_SecurityScenarios#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#3)]  
  
### <a name="configuration"></a>設定  
 可使用以下組態來取代程式碼設定服務端點。  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <behaviors />  
    <services>  
      <service behaviorConfiguration="" name="ServiceModel.Calculator">  
        <endpoint address="net.tcp://localhost:8008/Calculator"
                  binding="netTcpBinding"  
          bindingConfiguration="WindowsClientOverTcp"
                  name="WindowsClientOverTcp"  
                  contract="ServiceModel.ICalculator" />  
      </service>  
    </services>  
    <bindings>  
      <netTcpBinding>  
        <binding name="WindowsClientOverTcp">  
          <security mode="Transport">  
            <transport clientCredentialType="Windows" />  
          </security>  
        </binding>  
      </netTcpBinding>  
    </bindings>  
    <client />  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="client"></a>Client  
 下列程式碼和組態要獨立執行。 執行下列其中一個動作：  
  
- 使用此程式碼 (和用戶端程式碼) 建立獨立用戶端。  
  
- 建立未定義任何端點位址的用戶端， 然後改用可接受組態名稱當做引數的用戶端建構函式。 例如：  
  
     [!code-csharp[C_SecurityScenarios#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#0)]
     [!code-vb[C_SecurityScenarios#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#0)]  
  
### <a name="code"></a>程式碼  
 下列程式碼會建立用戶端。 繫結會設定為使用傳輸模式安全性，採用 TCP 傳輸，並將用戶端認證類型設為 Windows。  
  
 [!code-csharp[C_SecurityScenarios#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#4)]
 [!code-vb[C_SecurityScenarios#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#4)]  
  
### <a name="configuration"></a>設定  
 可使用以下組態來取代程式碼建立用戶端。  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <bindings>  
      <netTcpBinding>  
        <binding name="NetTcpBinding_ICalculator" >  
          <security mode="Transport">  
            <transport clientCredentialType="Windows" />  
          </security>  
        </binding>  
      </netTcpBinding>  
    </bindings>  
    <client>  
      <endpoint address="net.tcp://localhost:8008/Calculator"
                binding="netTcpBinding"
                bindingConfiguration="NetTcpBinding_ICalculator"
                contract="ICalculator"  
                name="NetTcpBinding_ICalculator">  
      </endpoint>  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a>另請參閱

- [安全性總覽](security-overview.md)
- [如何：利用 Windows 認證保護服務的安全](../how-to-secure-a-service-with-windows-credentials.md)
- [Windows Server AppFabric 的資訊安全模型](https://docs.microsoft.com/previous-versions/appfabric/ee677202(v=azure.10))
