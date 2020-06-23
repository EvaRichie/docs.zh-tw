---
title: HOW TO：在組態中建立服務端點
description: 瞭解如何使用同時包含相對和絕對位址的設定檔來新增 WCF 服務的端點。
ms.date: 06/16/2016
ms.assetid: f474e25d-2a27-4f31-84c5-395c442b8e70
ms.openlocfilehash: 184bcb5f7f3e83f12608757b55bbb4d57be58f7d
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85247061"
---
# <a name="how-to-create-a-service-endpoint-in-configuration"></a>HOW TO：在組態中建立服務端點
端點可讓用戶端存取 Windows Communication Foundation （WCF）服務所提供的功能。 您可以使用相對與絕對端點位址的組合，定義一個或多個端點，如果您沒有定義任何服務端點，執行階段預設會提供一些服務端點。 本主題說明如何使用包含相對與絕對位址的組態檔來加入端點。  
  
## <a name="example"></a>範例  
 下列服務組態會指定一個基底位址與五個端點。  
  
```xml  
<configuration>  
  
  <appSettings>  
    <!-- use appSetting to configure base address provided by host -->  
    <add key="baseAddress" value="http://localhost:8000/servicemodelsamples/service" />  
  </appSettings>  
  
  <system.serviceModel>  
    <services>  
    <!-- This section is optional with the default configuration introduced in .NET Framework 4. -->  
      <service name="Microsoft.ServiceModel.Samples.CalculatorService">  
        <host>  
          <baseAddresses>  
            <add baseAddress="http://localhost:8000/ServiceModelSamples/service"/>  
          </baseAddresses>  
        </host>  
        <endpoint address=""  
                  binding="wsHttpBinding"  
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />  
        <endpoint address="/test"  
                  binding="wsHttpBinding"  
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />  
        <endpoint address="http://localhost:8001/hello/servicemodelsamples"  
                  binding="wsHttpBinding"  
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />  
        <endpoint address="net.tcp://localhost:9000/servicemodelsamples/service"  
                  binding="netTcpBinding"  
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />  
        <!-- the mex endpoint is another relative address exposed at   
             http://localhost:8000/ServiceModelSamples/service/mex -->  
        <endpoint address="mex"  
                  binding="mexHttpBinding"  
                  contract="IMetadataExchange" />  
      </service>  
    </services>  
  
    <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="True"/>  
          <serviceDebug includeExceptionDetailInFaults="False" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  
  </system.serviceModel>  
  
</configuration>  
```  
  
## <a name="example"></a>範例  
 基底位址會透過 `add` 項目來指定，而此項目位於 service/host/baseAddresses 底下，如下列範例所示。  
  
```xml  
<service
    name="Microsoft.ServiceModel.Samples.CalculatorService">  
  <host>  
    <baseAddresses>  
      <add baseAddress="http://localhost:8000/ServiceModelSamples/service"/>  
    </baseAddresses>  
  </host>  
```  
  
## <a name="example"></a>範例  
 下列範例中的第一個端點定義會指定相對位址，表示端點位址是符合統一資源識別元 (URI) 撰寫規則的基底位址與相對位址組合。 相對位址為空白位址 ("")，因此端點位址與基底位址是同一個。 實際的端點位址是 `http://localhost:8000/servicemodelsamples/service` 。  
  
```xml  
<endpoint address=""
    binding="wsHttpBinding"  
    contract="Microsoft.ServiceModel.Samples.ICalculator" />  
```  
  
## <a name="example"></a>範例  
 第二個端點定義也是指定相對位址，如下列範例組態所示。 此相對位址 "test" 會附加在基底位址。 實際的端點位址是 `http://localhost:8000/servicemodelsamples/service/test` 。  
  
```xml  
<endpoint address="/test"  
    binding="wsHttpBinding"  
    contract="Microsoft.ServiceModel.Samples.ICalculator" />  
```  
  
## <a name="example"></a>範例  
 第三個端點定義是指定絕對位址，如下列範例組態所示。 位址中不需要基底位址。 實際的端點位址是 `http://localhost:8001/hello/servicemodelsamples` 。  
  
```xml  
<endpoint address="http://localhost:8001/hello/servicemodelsamples"  
    binding="wsHttpBinding"  
    contract="Microsoft.ServiceModel.Samples.ICalculator" />  
```  
  
## <a name="example"></a>範例  
 第四個端點位址是指定絕對位址以及不同的傳輸 (TCP)。 位址中不需要基底位址。 實際的端點位址是 net.tcp://localhost:9000/servicemodelsamples/service。  
  
```xml  
<endpoint address="net.tcp://localhost:9000/servicemodelsamples/service"  
    binding="netTcpBinding"  
    contract="Microsoft.ServiceModel.Samples.ICalculator" />  
```  
  
## <a name="example"></a>範例  
 若要使用執行階段提供的預設端點，請不要在程式碼或組態檔中指定任何服務端點。 在這個範例中，執行階段會在服務開啟時建立預設端點。 如需預設端點、繫結和行為的詳細資訊，請參閱[簡化的組態](../simplified-configuration.md)和 [WCF 服務的簡化組態](../samples/simplified-configuration-for-wcf-services.md)。  
  
```xml  
<configuration>  
  
  <appSettings>  
    <!-- use appSetting to configure base address provided by host -->  
    <add key="baseAddress" value="http://localhost:8000/servicemodelsamples/service" />  
  </appSettings>  
  
  <system.serviceModel>  
    <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="True"/>  
          <serviceDebug includeExceptionDetailInFaults="False" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  
  </system.serviceModel>  
  
</configuration>  
```
