---
title: 設定 Windows Communication Foundation 服務的繫結
description: 瞭解如何藉由編輯系統下的專案，在部署階段為 WCF 應用程式設定系結。System.servicemodel 元素。
ms.date: 03/30/2017
helpviewer_keywords:
- binding configuration [WCF]
ms.assetid: 99a85fd8-f7eb-4a84-a93e-7721b37d415c
ms.openlocfilehash: 60ab04764851ef82a43d5c2050d3bac7b56ce551
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96266723"
---
# <a name="configuring-bindings-for-windows-communication-foundation-services"></a>設定 Windows Communication Foundation 服務的繫結

建立應用程式時，您經常會需要在應用程式部署後，延後系統管理員的決定。 例如，我們很多時都無法預知服務位址，或統一資源識別元 (URI)。 這時候，為位址進行硬式編碼並不是理想的作法，較好的作法是讓系統管理員在建立服務後再處理。 這樣的靈活性是透過組態達成。  
  
> [!NOTE]
> 使用「配置 [中繼資料公用程式工具」 ( # A0) ](servicemodel-metadata-utility-tool-svcutil-exe.md) 搭配 `/config` 參數來快速建立設定檔。  
  
## <a name="major-sections"></a>主要區段  

 Windows Communication Foundation (WCF) 設定配置包含下列三個主要區段 (`serviceModel` 、 `bindings` 和 `services`) ：  
  
```xml  
<configuration>  
    <system.serviceModel>  
        <bindings>  
        </bindings>  
        <services>  
        </services>  
        <behaviors>  
        </behaviors>  
    </system.serviceModel>  
</configuration>  
```  
  
### <a name="servicemodel-elements"></a>ServiceModel 項目  

 您可以使用專案所系結的區段 `system.ServiceModel` ，以一或多個端點來設定服務類型，以及服務的設定。 然後可以使用位址、合約與繫結來設定每個端點。 如需端點的詳細資訊，請參閱 [端點建立總覽](endpoint-creation-overview.md)。 如果沒有指定任何端點，則執行階段會加入預設端點。 如需預設端點、繫結和行為的詳細資訊，請參閱[簡化的組態](simplified-configuration.md)和 [WCF 服務的簡化組態](./samples/simplified-configuration-for-wcf-services.md)。  
  
 繫結程序指定傳輸 (HTTP、TCP、管道、訊息佇列) 與通訊協定 (安全性、可靠性、異動流) 並且包含繫結程序項目，每個皆指定端點如何與外界通訊。  
  
 例如，指定 [\<basicHttpBinding>](../configure-apps/file-schema/wcf/basichttpbinding.md) 元素表示使用 HTTP 做為端點的傳輸。 這是在執行階段，當使用此端點的服務開啟時，用來連接端點。  
  
 有兩類的繫結：預先定義和自訂。 預先定義的繫結包含有用的項目組合，在一般狀況下使用。 如需 WCF 提供之預先定義系結類型的清單，請參閱 [系統提供](system-provided-bindings.md)的系結。 若無預先定義的繫結程序集合擁有服務應用程式所需的正確功能組合，您可以建構自訂繫結程序來滿足應用程式的要求。 如需自訂系結的詳細資訊，請參閱 [\<customBinding>](../configure-apps/file-schema/wcf/custombinding.md) 。  
  
 下列四個範例說明用來設定 WCF 服務的最常見系結設定。  
  
#### <a name="specifying-an-endpoint-to-use-a-binding-type"></a>指定使用繫結型別的端點  

 第一個範例說明如何指定以位址、合約及繫結組態的端點。  
  
```xml  
<service name="HelloWorld, IndigoConfig, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null">  
  <!-- This section is optional with the default configuration introduced  
       in .NET Framework 4. -->  
  <endpoint
      address="/HelloWorld2/"  
      contract="HelloWorld, IndigoConfig, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null"  
      binding="basicHttpBinding" />
</service>  
```  
  
 在此範例中，`name` 屬性表示組態是針對哪種服務類型。 當您在編碼中以 `HelloWorld` 合約建立服務，它將以範例組態定義的所有端點進行初始化。 如果元件只實作為一個服務合約， `name` 就可以省略屬性，因為服務會使用唯一可用的型別。 該屬性取用一個字串，格式必須為 `Namespace.Class, AssemblyName, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null`  
  
 `address` 屬性指定其他端點用來和服務通訊的 URI。 URI 可能是絕對或相對路徑。 如果提供相對位址，主機必須為繫結中使用的傳輸配置提供適當的基底位址。 如果沒有設定位址，會將基底位址假設為該端點的位址。  
  
 `contract` 屬性指定此端點所公開的合約。 服務實作型別必須實作合約類型。 如果服務實作實作單一合約類型，便可省略這個屬性。  
  
 `binding` 屬性選擇此特定端點使用之預先定義或自訂繫結。 未明確選擇繫結的端點會使用預設的繫結選擇，也就是 `BasicHttpBinding`。  
  
#### <a name="modifying-a-predefined-binding"></a>修改預先定義繫結  

 下列範例會修改預先定義的繫結， 然後可用作設定服務中的所有端點。 設定 <xref:System.ServiceModel.Configuration.IBindingConfigurationElement.ReceiveTimeout%2A> 值為 1 秒以修改繫結。 請注意，屬性傳回 <xref:System.TimeSpan> 物件。  
  
 更動後的繫結會在繫結區段內。 如今當您設定 `binding` 項目的 `endpoint` 屬性建立任何端點時，都可以使用此已更動的繫結。  
  
> [!NOTE]
> 如果您賦予此繫結一個特定名稱，則服務端點所指定的 `bindingConfiguration` 必須與其相一致。  
  
```xml  
<service name="HelloWorld, IndigoConfig, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null">  
  <endpoint
      address="/HelloWorld2/"  
      contract="HelloWorld, IndigoConfig, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null"  
      binding="basicHttpBinding" />
</service>  
<bindings>  
    <basicHttpBinding
        receiveTimeout="00:00:01"  
    />  
</bindings>  
```  
  
## <a name="configuring-a-behavior-to-apply-to-a-service"></a>設定行為以套用至服務  

 下列範例會針對服務類型來設定特定行為。 `ServiceMetadataBehavior`元素可用來啟用 [ [System.servicemodel 中繼資料公用程式] 工具 ( # A0) ](servicemodel-metadata-utility-tool-svcutil-exe.md)來查詢服務，並從中繼資料產生 Web 服務描述語言 (WSDL) 檔。  
  
> [!NOTE]
> 如果您賦予此行為一個特定名稱，則服務或端點區段內所指定的 `behaviorConfiguration` 必須與其相一致。  
  
```xml  
<behaviors>  
    <behavior>  
        <ServiceMetadata httpGetEnabled="true" />
    </behavior>  
</behaviors>  
<services>  
    <service
       name="HelloWorld, IndigoConfig, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null">
       <endpoint
          address="http://computer:8080/Hello"  
          contract="HelloWorld, IndigoConfig, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null"  
          binding="basicHttpBinding" />
    </service>  
</services>  
```  
  
 前述組態讓用戶端得以呼叫 "HelloWorld" 類型的服務並取得中繼資料。  
  
 `svcutil /config:Client.exe.config http://computer:8080/Hello?wsdl`  
  
## <a name="specifying-a-service-with-two-endpoints-using-different-binding-values"></a>指定具有使用不同繫結值之兩端點的服務  

 在此最後的範例，兩個端點設定為 `HelloWorld` 服務類型。 每個端點都會使用相同系結類型的不同自訂  `bindingConfiguration` 屬性 (每個端點都會修改 `basicHttpBinding`) 。  
  
```xml  
<service name="HelloWorld, IndigoConfig, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null">  
    <endpoint  
        address="http://computer:8080/Hello1"  
        contract="HelloWorld, IndigoConfig, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null"  
        binding="basicHttpBinding"  
        bindingConfiguration="shortTimeout" />
    <endpoint  
        address="http://computer:8080/Hello2"  
        contract="HelloWorld, IndigoConfig, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null"  
        binding="basicHttpBinding"  
        bindingConfiguration="Secure" />
</service>  
<bindings>  
    <basicHttpBinding
        name="shortTimeout"  
        timeout="00:00:00:01"
     />  
     <basicHttpBinding
        name="Secure">  
        <Security mode="Transport" />  
     </basicHttpBinding>
</bindings>  
```  
  
 您可以使用預設組態再加入 `protocolMapping` 區段並設定繫結，而得到同樣的行為，如下列範例所示。  
  
```xml  
<protocolMapping>  
    <add scheme="http" binding="basicHttpBinding" bindingConfiguration="shortTimeout" />  
    <add scheme="https" binding="basicHttpBinding" bindingConfiguration="Secure" />  
</protocolMapping>  
<bindings>  
    <basicHttpBinding
        name="shortTimeout"  
        timeout="00:00:00:01"
     />  
     <basicHttpBinding
        name="Secure" />  
        <Security mode="Transport" />  
</bindings>  
```  
  
## <a name="see-also"></a>另請參閱

- [簡化的組態](simplified-configuration.md)
- [系統提供的繫結](system-provided-bindings.md)
- [端點建立概觀](endpoint-creation-overview.md)
- [使用繫結來設定服務和用戶端](using-bindings-to-configure-services-and-clients.md)
