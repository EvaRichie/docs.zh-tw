---
title: 用戶端組態
ms.date: 03/30/2017
ms.assetid: 5da5bd3b-65d9-43b7-91b9-cc9e989b1350
ms.openlocfilehash: 2d17438095e65ccf922061c03e406bab35b07c5d
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84593655"
---
# <a name="client-configuration"></a><span data-ttu-id="fc156-102">用戶端組態</span><span class="sxs-lookup"><span data-stu-id="fc156-102">Client Configuration</span></span>
<span data-ttu-id="fc156-103">您可以使用 Windows Communication Foundation （WCF）用戶端設定來指定位址、系結、行為和合約，也就是用戶端端點的 "ABC" 屬性，用戶端會用來連接到服務端點。</span><span class="sxs-lookup"><span data-stu-id="fc156-103">You can use the Windows Communication Foundation (WCF) client configuration to specify the address, binding, behavior, and contract, the "ABC" properties of the client endpoint, which clients use to connect to service endpoints.</span></span> <span data-ttu-id="fc156-104">[\<client>](../../configure-apps/file-schema/wcf/client.md)元素具有 [\<endpoint>](../../configure-apps/file-schema/wcf/endpoint-of-client.md) 元素，其屬性是用來設定端點 abc。</span><span class="sxs-lookup"><span data-stu-id="fc156-104">The [\<client>](../../configure-apps/file-schema/wcf/client.md) element has an [\<endpoint>](../../configure-apps/file-schema/wcf/endpoint-of-client.md) element whose attributes are used to configure the endpoint ABCs.</span></span> <span data-ttu-id="fc156-105">這些屬性會在設定[端點](#configuring-endpoints)一節中討論。</span><span class="sxs-lookup"><span data-stu-id="fc156-105">These attributes are discussed in the [Configuring Endpoints](#configuring-endpoints) section.</span></span>  
  
 <span data-ttu-id="fc156-106">[\<endpoint>](../../configure-apps/file-schema/wcf/endpoint-of-client.md)元素也包含元素， [\<metadata>](../../configure-apps/file-schema/wcf/metadata.md) 該專案用來指定匯入和匯出中繼資料的設定、 [\<headers>](../../configure-apps/file-schema/wcf/headers.md) 包含自訂位址標頭集合的專案，以及 [\<identity>](../../configure-apps/file-schema/wcf/identity.md) 可讓其他端點與訊息交換的端點進行驗證的元素。</span><span class="sxs-lookup"><span data-stu-id="fc156-106">The [\<endpoint>](../../configure-apps/file-schema/wcf/endpoint-of-client.md) element also contains a [\<metadata>](../../configure-apps/file-schema/wcf/metadata.md) element that is used to specify settings for importing and exporting metadata, a [\<headers>](../../configure-apps/file-schema/wcf/headers.md) element that contains a collection of custom address headers, and an [\<identity>](../../configure-apps/file-schema/wcf/identity.md) element that enables the authentication of an endpoint by other endpoints exchanging messages with it.</span></span> <span data-ttu-id="fc156-107">[\<headers>](../../configure-apps/file-schema/wcf/headers.md)和 [\<identity>](../../configure-apps/file-schema/wcf/identity.md) 專案是的一部分， <xref:System.ServiceModel.EndpointAddress> 並會在[位址](endpoint-addresses.md)一文中討論。</span><span class="sxs-lookup"><span data-stu-id="fc156-107">The [\<headers>](../../configure-apps/file-schema/wcf/headers.md) and [\<identity>](../../configure-apps/file-schema/wcf/identity.md) elements are part of the <xref:System.ServiceModel.EndpointAddress> and are discussed in the [Addresses](endpoint-addresses.md) article.</span></span> <span data-ttu-id="fc156-108">設定[中繼資料](#configuring-metadata)一節中會提供說明中繼資料延伸模組使用方式的主題連結。</span><span class="sxs-lookup"><span data-stu-id="fc156-108">Links to topics that explain the use of metadata extensions are provided in the [Configuring Metadata](#configuring-metadata) section.</span></span>  
  
## <a name="configuring-endpoints"></a><span data-ttu-id="fc156-109">設定端點</span><span class="sxs-lookup"><span data-stu-id="fc156-109">Configuring Endpoints</span></span>  
 <span data-ttu-id="fc156-110">用戶端設定的設計可讓用戶端指定一個或多個端點，每個端點都有自己的名稱、位址和合約，而每個端點 [\<bindings>](../../configure-apps/file-schema/wcf/bindings.md) [\<behaviors>](../../configure-apps/file-schema/wcf/behaviors.md) 都會參考用戶端設定中的和元素，以用來設定該端點。</span><span class="sxs-lookup"><span data-stu-id="fc156-110">The client configuration is designed to allow the client to specify one or more endpoints, each with its own name, address, and contract, with each referencing the [\<bindings>](../../configure-apps/file-schema/wcf/bindings.md) and [\<behaviors>](../../configure-apps/file-schema/wcf/behaviors.md) elements in the client configuration to be used to configure that endpoint.</span></span> <span data-ttu-id="fc156-111">用戶端設定檔案應命名為 "App.config"，因為這是 WCF 執行時間所預期的名稱。</span><span class="sxs-lookup"><span data-stu-id="fc156-111">The client configuration file should be named "App.config" because this is the name that the WCF runtime expects.</span></span> <span data-ttu-id="fc156-112">下列範例示範用戶端組態檔。</span><span class="sxs-lookup"><span data-stu-id="fc156-112">The following example shows a client configuration file.</span></span>  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
        <client>  
          <endpoint  
            name="endpoint1"  
            address="http://localhost/ServiceModelSamples/service.svc"  
            binding="wsHttpBinding"  
            bindingConfiguration="WSHttpBinding_IHello"  
            behaviorConfiguration="IHello_Behavior"  
            contract="IHello" >  
  
            <metadata>  
              <wsdlImporters>  
                <extension  
                  type="Microsoft.ServiceModel.Samples.WsdlDocumentationImporter, WsdlDocumentation"/>  
              </wsdlImporters>  
            </metadata>  
  
            <identity>  
              <servicePrincipalName value="host/localhost" />  
            </identity>  
          </endpoint>  
            <!-- Add another endpoint by adding another <endpoint> element. -->
          <endpoint  
            name="endpoint2">  
           //Configure another endpoint here.  
          </endpoint>  
        </client>  
  
//The bindings section references by the bindingConfiguration endpoint attribute.  
    <bindings>  
      <wsHttpBinding>  
        <binding name="WSHttpBinding_IHello"
                 bypassProxyOnLocal="false"
                 hostNameComparisonMode="StrongWildcard">  
          <readerQuotas maxDepth="32"/>  
          <reliableSession ordered="true"
                           enabled="false" />  
          <security mode="Message">  
           //Security settings go here.  
          </security>  
        </binding>  
        <binding name="Another Binding"  
          <!-- Configure this binding here. -->  
        </binding>  
          </wsHttpBinding>  
     </bindings>  
  
//The behavior section references by the behaviorConfiguration endpoint attribute.  
        <behaviors>  
            <endpointBehaviors>  
                <behavior name=" IHello_Behavior ">  
                    <clientVia />  
                </behavior>  
            </endpointBehaviors>  
        </behaviors>  
  
    </system.serviceModel>  
</configuration>  
```  
  
 <span data-ttu-id="fc156-113">選擇性的 `name` 屬性會針對指定的合約唯一識別端點。</span><span class="sxs-lookup"><span data-stu-id="fc156-113">The optional `name` attribute uniquely identifies an endpoint for a given contract.</span></span> <span data-ttu-id="fc156-114"><xref:System.ServiceModel.ChannelFactory%601.%23ctor%2A> 或 <xref:System.ServiceModel.ClientBase%601.%23ctor%2A> 會使用此端點來指定目前已指向用戶端組態中的哪個端點，並在建立提供服務的通道時，指定必須載入的端點。</span><span class="sxs-lookup"><span data-stu-id="fc156-114">It is used by the <xref:System.ServiceModel.ChannelFactory%601.%23ctor%2A> or by the <xref:System.ServiceModel.ClientBase%601.%23ctor%2A> to specify which endpoint in the client configuration is being targeted and must be loaded when a channel is created to service.</span></span> <span data-ttu-id="fc156-115">有萬用字元端點設定名稱 " \* " 可供使用，並向 <xref:System.ServiceModel.ChannelFactory.ApplyConfiguration%2A> 方法指出它應該在檔案中載入任何端點設定（前提是有一個可用的），否則會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="fc156-115">A wildcard endpoint configuration name "\*" is available and indicates to the <xref:System.ServiceModel.ChannelFactory.ApplyConfiguration%2A> method that it should load any endpoint configuration in the file, provided there is precisely one available, and otherwise throws an exception.</span></span> <span data-ttu-id="fc156-116">如果省略這個屬性，就會使用對應端點做為與所指定合約類型相關聯的預設端點。</span><span class="sxs-lookup"><span data-stu-id="fc156-116">If this attribute is omitted, the corresponding endpoint is used as the default endpoint associated with the specified contract type.</span></span> <span data-ttu-id="fc156-117">`name` 屬性的預設值是空字串 (與任何其他名稱相符)。</span><span class="sxs-lookup"><span data-stu-id="fc156-117">The default value for the `name` attribute is an empty string which is matched like any other name.</span></span>  
  
 <span data-ttu-id="fc156-118">每個端點都必須具有與其相關聯的位址，以便找出並識別端點。</span><span class="sxs-lookup"><span data-stu-id="fc156-118">Every endpoint must have an address associated with it to locate and identify the endpoint.</span></span> <span data-ttu-id="fc156-119">`address` 屬性可以用來指定 URL 以提供端點的位置。</span><span class="sxs-lookup"><span data-stu-id="fc156-119">The `address` attribute can be used to specify the URL that provides the location of the endpoint.</span></span> <span data-ttu-id="fc156-120">但是，您也可以使用其中一個 <xref:System.ServiceModel.ServiceHost> 方法，建立統一資源識別元 (URI) 並新增至 <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%2A>，以便在程式碼中指定服務端點的位址。</span><span class="sxs-lookup"><span data-stu-id="fc156-120">But the address for a service endpoint can also be specified in code by creating a Uniform Resource Identifier (URI) and is added to the <xref:System.ServiceModel.ServiceHost> using one of the <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%2A> methods.</span></span> <span data-ttu-id="fc156-121">如需詳細資訊，請參閱[位址](endpoint-addresses.md)。</span><span class="sxs-lookup"><span data-stu-id="fc156-121">For more information, see [Addresses](endpoint-addresses.md).</span></span> <span data-ttu-id="fc156-122">如簡介所示， [\<headers>](../../configure-apps/file-schema/wcf/headers.md) 和專案 [\<identity>](../../configure-apps/file-schema/wcf/identity.md) 都是的一部分，而且 <xref:System.ServiceModel.EndpointAddress> 也會在[位址](endpoint-addresses.md)主題中討論。</span><span class="sxs-lookup"><span data-stu-id="fc156-122">As the introduction indicates, the [\<headers>](../../configure-apps/file-schema/wcf/headers.md) and [\<identity>](../../configure-apps/file-schema/wcf/identity.md) elements are part of the <xref:System.ServiceModel.EndpointAddress> and are also discussed in the [Addresses](endpoint-addresses.md) topic.</span></span>  
  
 <span data-ttu-id="fc156-123">`binding` 屬性代表當端點連接至服務時，預期使用的繫結型別。</span><span class="sxs-lookup"><span data-stu-id="fc156-123">The `binding` attribute indicates the type of binding the endpoint expects to use when connecting to a service.</span></span> <span data-ttu-id="fc156-124">型別必須具有註冊的組態區段，才能加以參考。</span><span class="sxs-lookup"><span data-stu-id="fc156-124">The type must have a registered configuration section if it is to be referenced.</span></span> <span data-ttu-id="fc156-125">在上述範例中，這是 [\<wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md) 區段，表示端點使用 <xref:System.ServiceModel.WSHttpBinding> 。</span><span class="sxs-lookup"><span data-stu-id="fc156-125">In the previous example, this is the [\<wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md) section, which indicates that the endpoint uses a <xref:System.ServiceModel.WSHttpBinding>.</span></span> <span data-ttu-id="fc156-126">不過，端點可以使用的特定繫結型別可能不只一種。</span><span class="sxs-lookup"><span data-stu-id="fc156-126">But there may be more than one binding of a given type that the endpoint can use.</span></span> <span data-ttu-id="fc156-127">其中每一個都在 [\<binding>](../../configure-apps/file-schema/wcf/bindings.md) （binding） type 元素內有自己的元素。</span><span class="sxs-lookup"><span data-stu-id="fc156-127">Each of these has its own [\<binding>](../../configure-apps/file-schema/wcf/bindings.md) element within the (binding) type element.</span></span> <span data-ttu-id="fc156-128">`bindingconfiguration` 屬性可用來區分型別相同的繫結。</span><span class="sxs-lookup"><span data-stu-id="fc156-128">The `bindingconfiguration` attribute is used to distinguish between bindings of the same type.</span></span> <span data-ttu-id="fc156-129">其值與 `name` 元素的屬性相符 [\<binding>](../../configure-apps/file-schema/wcf/bindings.md) 。</span><span class="sxs-lookup"><span data-stu-id="fc156-129">Its value is matched with the `name` attribute of the [\<binding>](../../configure-apps/file-schema/wcf/bindings.md) element.</span></span> <span data-ttu-id="fc156-130">如需有關如何使用設定來設定用戶端系結的詳細資訊，請參閱 how [to：在 configuration 中指定用戶端](../how-to-specify-a-client-binding-in-configuration.md)系結。</span><span class="sxs-lookup"><span data-stu-id="fc156-130">For more information about how to configure a client binding using configuration, see [How to: Specify a Client Binding in Configuration](../how-to-specify-a-client-binding-in-configuration.md).</span></span>  
  
 <span data-ttu-id="fc156-131">`behaviorConfiguration`屬性是用來指定 [\<behavior>](../../configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md) [\<endpointBehaviors>](../../configure-apps/file-schema/wcf/endpointbehaviors.md) 端點應使用哪一個。</span><span class="sxs-lookup"><span data-stu-id="fc156-131">The `behaviorConfiguration` attribute is used to specify which [\<behavior>](../../configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md) of the [\<endpointBehaviors>](../../configure-apps/file-schema/wcf/endpointbehaviors.md) the endpoint should use.</span></span> <span data-ttu-id="fc156-132">其值與 `name` 元素的屬性相符 [\<behavior>](../../configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md) 。</span><span class="sxs-lookup"><span data-stu-id="fc156-132">Its value is matched with the `name` attribute of the [\<behavior>](../../configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md) element.</span></span> <span data-ttu-id="fc156-133">如需使用 configuration 來指定用戶端行為的範例，請參閱設定[用戶端行為](../configuring-client-behaviors.md)。</span><span class="sxs-lookup"><span data-stu-id="fc156-133">For an example of using configuration to specify client behaviors, see [Configuring Client Behaviors](../configuring-client-behaviors.md).</span></span>  
  
 <span data-ttu-id="fc156-134">`contract` 屬性會指定端點所公開的合約。</span><span class="sxs-lookup"><span data-stu-id="fc156-134">The `contract` attribute specifies which contract the endpoint is exposing.</span></span> <span data-ttu-id="fc156-135">這個值會對應至 <xref:System.ServiceModel.ServiceContractAttribute.ConfigurationName%2A> 的 <xref:System.ServiceModel.ServiceContractAttribute>。</span><span class="sxs-lookup"><span data-stu-id="fc156-135">This value maps to the <xref:System.ServiceModel.ServiceContractAttribute.ConfigurationName%2A> of the <xref:System.ServiceModel.ServiceContractAttribute>.</span></span> <span data-ttu-id="fc156-136">預設值是實作服務之類別的完整型別名稱。</span><span class="sxs-lookup"><span data-stu-id="fc156-136">The default value is the full type name of the class that implements the service.</span></span>  
  
### <a name="configuring-metadata"></a><span data-ttu-id="fc156-137">設定中繼資料</span><span class="sxs-lookup"><span data-stu-id="fc156-137">Configuring Metadata</span></span>  
 <span data-ttu-id="fc156-138">[\<metadata>](../../configure-apps/file-schema/wcf/metadata.md)元素可用來指定用來註冊中繼資料匯入延伸模組的設定。</span><span class="sxs-lookup"><span data-stu-id="fc156-138">The [\<metadata>](../../configure-apps/file-schema/wcf/metadata.md) element is used to specify settings used to register metadata import extensions.</span></span> <span data-ttu-id="fc156-139">如需擴充中繼資料系統的詳細資訊，請參閱[擴充中繼資料系統](../extending/extending-the-metadata-system.md)。</span><span class="sxs-lookup"><span data-stu-id="fc156-139">For more information about extending the metadata system, see [Extending the Metadata System](../extending/extending-the-metadata-system.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="fc156-140">請參閱</span><span class="sxs-lookup"><span data-stu-id="fc156-140">See also</span></span>

- [<span data-ttu-id="fc156-141">端點：位址、繫結和合約</span><span class="sxs-lookup"><span data-stu-id="fc156-141">Endpoints: Addresses, Bindings, and Contracts</span></span>](endpoints-addresses-bindings-and-contracts.md)
- [<span data-ttu-id="fc156-142">設定用戶端行為</span><span class="sxs-lookup"><span data-stu-id="fc156-142">Configuring Client Behaviors</span></span>](../configuring-client-behaviors.md)
