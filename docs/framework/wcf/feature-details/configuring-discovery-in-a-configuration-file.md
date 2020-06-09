---
title: 在組態檔中設定探索
ms.date: 03/30/2017
ms.assetid: b9884c11-8011-4763-bc2c-c526b80175d0
ms.openlocfilehash: 59eaecb7e34b9105bc694f444d98c13c036d552f
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84597549"
---
# <a name="configuring-discovery-in-a-configuration-file"></a><span data-ttu-id="05270-102">在組態檔中設定探索</span><span class="sxs-lookup"><span data-stu-id="05270-102">Configuring Discovery in a Configuration File</span></span>
<span data-ttu-id="05270-103">探索中使用四個主要的組態設定群組。</span><span class="sxs-lookup"><span data-stu-id="05270-103">There are four major groups of configuration settings used in discovery.</span></span> <span data-ttu-id="05270-104">本主題將簡要說明各群組，並且顯示如何設定這些群組的範例。</span><span class="sxs-lookup"><span data-stu-id="05270-104">This topic will briefly describe each and show examples of how to configure them.</span></span> <span data-ttu-id="05270-105">各節後面會有一個連結，可提供與各領域更為深入的文件。</span><span class="sxs-lookup"><span data-stu-id="05270-105">Following each section will be a link to more in-depth documentation about each area.</span></span>  
  
## <a name="behavior-configuration"></a><span data-ttu-id="05270-106">行為組態</span><span class="sxs-lookup"><span data-stu-id="05270-106">Behavior Configuration</span></span>  
 <span data-ttu-id="05270-107">探索會使用服務行為和端點行為。</span><span class="sxs-lookup"><span data-stu-id="05270-107">Discovery uses service behaviors and endpoint behaviors.</span></span> <span data-ttu-id="05270-108"><xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior> 行為會啟用服務所有端點的探索，並且讓您指定公告端點。</span><span class="sxs-lookup"><span data-stu-id="05270-108">The <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior> behavior enables discovery for all of a service’s endpoints and allows you to specify announcement endpoints.</span></span>  <span data-ttu-id="05270-109">下列範例示範如何加入 <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior> 並指定公告端點。</span><span class="sxs-lookup"><span data-stu-id="05270-109">The following example shows how to add the <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior> and specify an announcement endpoint.</span></span>  
  
```xml  
<behaviors>  
      <serviceBehaviors>  
        <behavior name="helloWorldServiceBehavior">  
          <serviceDiscovery>  
            <announcementEndpoints>  
              <endpoint kind="udpAnnouncementEndpoint"/>  
            </announcementEndpoints>  
          </serviceDiscovery>  
        </behavior>  
      </serviceBehaviors>  
</behaviors>  
```  
  
 <span data-ttu-id="05270-110">指定行為之後，請從 <的> 專案參考它， `service` 如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="05270-110">Once you specify the behavior, reference it from a <`service`> element as shown in the following sample.</span></span>  
  
```xml  
<system.serviceModel>  
   <services>  
      <service name="HelloWorldService" behaviorConfiguration="helloWorldServiceBehavior">  
         <!-- Application Endpoint -->  
         <endpoint address="endpoint0"  
                   binding="basicHttpBinding"  
                   contract="IHelloWorldService" />  
         <!-- Discovery Endpoints -->  
         <endpoint kind="udpDiscoveryEndpoint" />  
        </service>  
    </services>  
</system.serviceModel>  
```  
  
 <span data-ttu-id="05270-111">為了讓服務能夠探索，您還必須加入探索端點，上述範例即加入了 <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> 標準端點。</span><span class="sxs-lookup"><span data-stu-id="05270-111">In order for a service to be discoverable, you must also add a discovery endpoint, the example above adds a <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> standard endpoint.</span></span>  
  
 <span data-ttu-id="05270-112">當您加入公告端點時，也必須將公告接聽程式服務新增至 <`services`> 元素，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="05270-112">When you add announcement endpoints you must also add an announcement listener service to the <`services`> element as shown in the following example.</span></span>  
  
```xml  
<services>  
   <service name="HelloWorldService" behaviorConfiguration="helloWorldServiceBehavior">  
      <!-- Application Endpoint -->  
      <endpoint address="endpoint0"  
                binding="basicHttpBinding"  
                contract="IHelloWorldService" />  
      <!-- Discovery Endpoints -->  
      <endpoint kind="udpDiscoveryEndpoint" />  
   </service>  
   <!-- Announcement Listener Configuration -->  
   <service name="AnnouncementListener">  
      <endpoint kind="udpAnnouncementEndpoint" />  
   </service>  
</services>
```  
  
 <span data-ttu-id="05270-113"><xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior> 行為可用來啟用或停用特定端點的探索。</span><span class="sxs-lookup"><span data-stu-id="05270-113">The <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior> behavior is used to enable or disable discovery of a specific endpoint.</span></span>  <span data-ttu-id="05270-114">下列範例設定服務的兩個應用程式端點，其中一個會啟用探索，另一個則停用探索。</span><span class="sxs-lookup"><span data-stu-id="05270-114">The following example configures a service with two application endpoints, one with discovery enabled and one with discovery disabled.</span></span> <span data-ttu-id="05270-115">請為各端點加入 <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior> 行為。</span><span class="sxs-lookup"><span data-stu-id="05270-115">For each endpoint an <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior> behavior is added.</span></span>  
  
```xml  
<system.serviceModel>  
   <services>  
      <service name="HelloWorldService"  
               behaviorConfiguration="helloWorldServiceBehavior">  
  
        <!-- Application Endpoints -->  
        <endpoint address="endpoint0"  
                 binding="basicHttpBinding"  
                 contract="IHelloWorldService"
                 behaviorConfiguration="ep0Behavior" />  
  
        <endpoint address="endpoint1"  
                  binding="basicHttpBinding"  
                  contract="IHelloWorldService"  
                  behaviorConfiguration="ep1Behavior" />  
  
        <!-- Discovery Endpoints -->  
        <endpoint kind="udpDiscoveryEndpoint" />  
      </service>  
   </services>  
   <behaviors>  
      <serviceBehaviors>  
        <behavior name="helloWorldServiceBehavior">  
          <serviceDiscovery />  
        </behavior>  
      </serviceBehaviors>  
      <endpointBehaviors>  
        <behavior name="ep0Behavior">  
          <endpointDiscovery enabled="true"/>  
        </behavior>  
        <behavior name="ep1Behavior">  
          <endpointDiscovery enabled="false"/>  
        </behavior>  
     </endpointBehaviors>  
   </behaviors>  
</system.serviceModel>  
```  
  
 <span data-ttu-id="05270-116"><xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior> 行為也可以用來將自訂中繼資料加入至服務傳回的端點中繼資料。</span><span class="sxs-lookup"><span data-stu-id="05270-116">The <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior> behavior can also be used to add custom metadata to the endpoint metadata returned by the service.</span></span> <span data-ttu-id="05270-117">下列範例示範如何執行。</span><span class="sxs-lookup"><span data-stu-id="05270-117">The following example shows how to do this.</span></span>  
  
```xml  
<behavior name="ep4Behavior">  
   <endpointDiscovery enabled="true">  
      <extensions>  
         <CustomMetadata>This is custom metadata.</CustomMetadata>  
         <d:Types xmlns:d="http://schemas.xmlsoap.org/ws/2005/04/discovery" xmlns:i="http://printer.example.org/2003/imaging">i:PrintBasic</d:Types>  
         <CustomMetadata netsted="true">  
            <NestedMetadata>This is a nested custom metadata.</NestedMetadata>  
         </CustomMetadata>  
      </extensions>  
   </endpointDiscovery>  
</behavior>  
```  
  
 <span data-ttu-id="05270-118"><xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior> 行為也可以用來加入用戶端用來搜尋服務的範圍和類型。</span><span class="sxs-lookup"><span data-stu-id="05270-118">The <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior> behavior can also be used to add scopes and types that clients use to search for services.</span></span> <span data-ttu-id="05270-119">下列範例示範如何在用戶端組態檔中執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="05270-119">The following example shows how to do this in a client side configuration file.</span></span>  
  
```xml  
<behavior name="ep2Behavior">  
   <endpointDiscovery enabled="true">  
      <scopes>  
         <add scope="http://www.microsoft.com/building42/floor1"/>  
         <add scope="ldap:///ou=engineeringo=examplecomc=us"/>  
      </scopes>  
      <types>  
         <add name="test" namespace="http://example.microsoft.com/" />  
         <add name="additionalContract" namespace="http://example.microsoft.com/" />  
      </types>  
   </endpointDiscovery>  
</behavior>  
```  
  
 <span data-ttu-id="05270-120">如需的詳細資訊 <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior> ， <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior> 請參閱[WCF 探索總覽](wcf-discovery-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="05270-120">For more information about <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior> and <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior> see [WCF Discovery Overview](wcf-discovery-overview.md).</span></span>  
  
## <a name="binding-element-configuration"></a><span data-ttu-id="05270-121">繫結項目組態</span><span class="sxs-lookup"><span data-stu-id="05270-121">Binding Element Configuration</span></span>  
 <span data-ttu-id="05270-122">繫結項目組態是用戶端上最有趣的一部分。</span><span class="sxs-lookup"><span data-stu-id="05270-122">Binding element configuration is most interesting on the client side.</span></span> <span data-ttu-id="05270-123">您可以使用組態指定尋找準則，用來從 WCF 用戶端應用程式探索服務。</span><span class="sxs-lookup"><span data-stu-id="05270-123">You can use configuration to specify the find criteria used to discover services from a WCF client application.</span></span>  <span data-ttu-id="05270-124">下列範例會建立使用 <xref:System.ServiceModel.Discovery.DiscoveryClient> 通道的自訂繫結，並指定包含型別和範圍的尋找準則。</span><span class="sxs-lookup"><span data-stu-id="05270-124">The following example creates a custom binding with the <xref:System.ServiceModel.Discovery.DiscoveryClient> channel and specifies find criteria that includes a type and scope.</span></span> <span data-ttu-id="05270-125">此外，還會指定 <xref:System.ServiceModel.Discovery.FindCriteria.Duration%2A> 和 <xref:System.ServiceModel.Discovery.FindCriteria.MaxResults%2A> 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="05270-125">In addition it specifies values for the <xref:System.ServiceModel.Discovery.FindCriteria.Duration%2A> and <xref:System.ServiceModel.Discovery.FindCriteria.MaxResults%2A> properties.</span></span>  
  
```xml  
<bindings>  
   <customBinding>  
      <!-- Binding Configuration for the Application Endpoint -->  
      <binding name="discoBindingConfiguration">  
         <discoveryClient>  
            <endpoint kind="discoveryEndpoint"  
                      address="http://localhost:8000/ConfigTest/Discovery"  
                      binding="customBinding"  
                      bindingConfiguration="httpSoap12WSAddressing10"/>  
            <findCriteria duration="00:00:10" maxResults="2">  
              <types>  
                <add name="IHelloWorldService"/>  
              </types>  
              <scopes>  
                <add scope="http://www.microsoft.com/building42/floor1"/>  
              </scopes>
            </findCriteria>  
          </discoveryClient>  
          <textMessageEncoding messageVersion="Soap11"/>  
          <httpTransport />  
      </binding>
   </customBinding>
</bindings>  
```  
  
 <span data-ttu-id="05270-126">用戶端端點必須參考此自訂繫結組態：</span><span class="sxs-lookup"><span data-stu-id="05270-126">This custom binding configuration must be referenced by a client endpoint:</span></span>  
  
```xml  
<client>  
      <endpoint address="http://schemas.microsoft.com/discovery/dynamic"  
                binding="customBinding"  
                bindingConfiguration="discoBindingConfiguration"  
                contract="IHelloWorldService" />  
</client>  
```  
  
 <span data-ttu-id="05270-127">如需尋找準則的詳細資訊[，請參閱探索尋找和尋找準則](discovery-find-and-findcriteria.md)。</span><span class="sxs-lookup"><span data-stu-id="05270-127">For more information about find criteria see [Discovery Find and FindCriteria](discovery-find-and-findcriteria.md).</span></span> <span data-ttu-id="05270-128">如需探索和繫結項目的詳細資訊，請參閱[WCF 探索總覽](wcf-discovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="05270-128">For more information about discovery and binding elements see, [WCF Discovery Overview](wcf-discovery-overview.md)</span></span>  
  
## <a name="standard-endpoint-configuration"></a><span data-ttu-id="05270-129">標準端點組態</span><span class="sxs-lookup"><span data-stu-id="05270-129">Standard Endpoint Configuration</span></span>  
 <span data-ttu-id="05270-130">標準端點是預先定義的端點，其中包含一個或多個屬性 (位址、繫結或合約) 的預設值，或是不可變更的一個或多個屬性值。</span><span class="sxs-lookup"><span data-stu-id="05270-130">Standard endpoints are predefined endpoints that have default values for one or more properties (address, binding, or contract) or one or more property values that cannot change.</span></span> <span data-ttu-id="05270-131">.NET 4 隨附 3 個探索相關的標準端點：<xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>、<xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint> 和 <xref:System.ServiceModel.Discovery.DynamicEndpoint>。</span><span class="sxs-lookup"><span data-stu-id="05270-131">.NET 4 ships with 3 discovery related standard endpoints: <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>, <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint>, and <xref:System.ServiceModel.Discovery.DynamicEndpoint>.</span></span>  <span data-ttu-id="05270-132"><xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> 是為透過 UDP 多點傳送繫結的探索作業而預先設定的標準端點。</span><span class="sxs-lookup"><span data-stu-id="05270-132">The <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> is a standard endpoint that is pre-configured for discovery operations over a UDP multicast binding.</span></span> <span data-ttu-id="05270-133"><xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint> 是為透過 UDP 繫結傳送公告訊息而預先設定的標準端點。</span><span class="sxs-lookup"><span data-stu-id="05270-133">The <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint> is a standard endpoint that is pre-configured to send announcement messages over a UDP binding.</span></span> <span data-ttu-id="05270-134"><xref:System.ServiceModel.Discovery.DynamicEndpoint> 是在執行階段使用探索動態尋找已探索服務之端點位址的標準端點。</span><span class="sxs-lookup"><span data-stu-id="05270-134">The <xref:System.ServiceModel.Discovery.DynamicEndpoint> is a standard endpoint that uses discovery to find the endpoint address of a discovered service dynamically at runtime.</span></span>  <span data-ttu-id="05270-135">標準系結是使用 <`endpoint`> 元素所指定，其中包含指定要加入之標準端點類型的 kind 屬性。</span><span class="sxs-lookup"><span data-stu-id="05270-135">Standard bindings are specified with an <`endpoint`> element that contains kind attribute that specified the type of standard endpoint to add.</span></span> <span data-ttu-id="05270-136">下列範例示範如何加入 <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> 和 <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint>。</span><span class="sxs-lookup"><span data-stu-id="05270-136">The following example shows how to add a <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> and a <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint>.</span></span>  
  
```xml  
<services>  
   <service name="HelloWorldService">  
      <!-- ...  -->
      <endpoint kind="udpDiscoveryEndpoint" />  
   </service>  
   <service name="AnnouncementListener">  
      <endpoint kind="udpAnnouncementEndpoint" />  
   </service>  
</services>  
```  
  
 <span data-ttu-id="05270-137">標準端點會在 <`standardEndpoints`> 元素中設定。</span><span class="sxs-lookup"><span data-stu-id="05270-137">Standard endpoints are configured in a <`standardEndpoints`> element.</span></span> <span data-ttu-id="05270-138">下列範例示範如何設定 <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> 和 <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint>。</span><span class="sxs-lookup"><span data-stu-id="05270-138">The following example shows how to configure the <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> and the <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint>.</span></span>  
  
```xml  
<standardEndpoints>  
      <udpAnnouncementEndpoint>  
        <standardEndpoint
            name="udpAnnouncementEndpointSettings"
            multicastAddress="soap.udp://239.255.255.250:3703"
            maxAnnouncementDelay="00:00:00.800">  
          <transportSettings  
            duplicateMessageHistoryLength="1028"  
            maxPendingMessageCount="10"  
            maxMulticastRetransmitCount="3"  
            maxUnicastRetransmitCount="2"  
            socketReceiveBufferSize="131072"  
            timeToLive="2" />  
        </standardEndpoint>  
      </udpAnnouncementEndpoint>  
      <udpDiscoveryEndpoint>  
        <standardEndpoint  
            name="udpDiscoveryEndpointSettings"  
            multicastAddress="soap.udp://239.255.255.252:3704"  
            maxResponseDelay="00:00:00.800">  
          <transportSettings  
            duplicateMessageHistoryLength="2048"  
            maxPendingMessageCount="5"  
            maxReceivedMessageSize="8192"  
            maxBufferPoolSize="262144"/>  
        </standardEndpoint>  
      </udpDiscoveryEndpoint>
</standardEndpoints>
```  
  
 <span data-ttu-id="05270-139">新增標準端點設定後，請參考每個端點之 <> 元素中的設定， `endpoint` 如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="05270-139">Once you’ve added the standard endpoint configuration, reference the configuration in the <`endpoint`> element for each endpoint as shown in the following sample.</span></span>  
  
```xml  
<services>  
   <service name="HelloWorldService">  
      <!-- ...  -->
      <endpoint kind="udpDiscoveryEndpoint" endpointConfiguration="udpDiscoveryEndpointSettings"/>  
   </service>  
   <service name="AnnouncementListener">  
      <endpoint kind="udpAnnouncementEndpoint" endpointConfiguration="udpAnnouncementEndpointSettings" >  
   </service>  
</services>  
```  
  
 <span data-ttu-id="05270-140">與探索中使用的其他標準端點不同的是，您會指定 <xref:System.ServiceModel.Discovery.DynamicEndpoint> 的繫結和合約。</span><span class="sxs-lookup"><span data-stu-id="05270-140">Unlike the other standard endpoints used in discovery, you specify a binding and contract for <xref:System.ServiceModel.Discovery.DynamicEndpoint>.</span></span> <span data-ttu-id="05270-141">下列範例示範如何加入和設定 <xref:System.ServiceModel.Discovery.DynamicEndpoint>。</span><span class="sxs-lookup"><span data-stu-id="05270-141">The following example shows how to add and configure a <xref:System.ServiceModel.Discovery.DynamicEndpoint>.</span></span>  
  
```xml  
<system.serviceModel>  
    <client>  
      <endpoint kind="dynamicEndpoint" binding="basicHttpBinding" contract="IHelloWorldService" endpointConfiguration="dynamicEndpointConfiguration" />  
    </client>
   <standardEndpoints>  
      <dynamicEndpoint>  
         <standardEndpoint name="dynamicEndpointConfiguration">  
             <discoveryClientSettings>  
              <findCriteria scopeMatchBy="http://schemas.microsoft.com/ws/2008/06/discovery/rfc" duration="00:00:10" maxResults="2">  
                 <types>  
                   <add name="IHelloWorldService"/>  
                 </types>  
                 <scopes>  
                   <add scope="http://www.microsoft.com/building42/floor1"/>  
                 </scopes>  
                 <extensions>  
                   <CustomMetadata>This is custom metadata.</CustomMetadata>
                 </extensions>  
               </findCriteria>  
             </discoveryClientSettings>  
           </standardEndpoint>  
         </dynamicEndpoint>  
   </standardEndpoints>  
</system.ServiceModel>  
```  
  
 <span data-ttu-id="05270-142">如需標準端點的詳細資訊，請參閱[標準端點](standard-endpoints.md)。</span><span class="sxs-lookup"><span data-stu-id="05270-142">For more information about standard endpoints see [Standard Endpoints](standard-endpoints.md).</span></span>
