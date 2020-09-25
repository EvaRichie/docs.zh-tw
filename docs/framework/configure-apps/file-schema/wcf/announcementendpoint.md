---
title: <announcementEndpoint>
ms.date: 03/30/2017
ms.assetid: 034b7c69-a770-4502-8cef-38007bbcd025
ms.openlocfilehash: f68972cdf0e55f92fd4856aff912f00db7c62be4
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91201612"
---
# \<announcementEndpoint>

<span data-ttu-id="4c4e7-101">這個組態項目會定義具有固定公告合約的標準端點。</span><span class="sxs-lookup"><span data-stu-id="4c4e7-101">This configuration element defines a standard endpoint with a fixed announcement contract.</span></span> <span data-ttu-id="4c4e7-102">服務可以選擇性地公告其可用性，方法是分別在開啟與關閉該服務時傳送線上及離線公告訊息。</span><span class="sxs-lookup"><span data-stu-id="4c4e7-102">A service can optionally announce its availability by sending an online and offline announcement message when it is opened or closed respectively.</span></span> <span data-ttu-id="4c4e7-103">Windows Communication Foundation (WCF) 服務會在元素中指定公告端點 [\<serviceDiscovery>](servicediscovery.md) ，並使用 AnnouncementClient 來執行宣告。</span><span class="sxs-lookup"><span data-stu-id="4c4e7-103">A Windows Communication Foundation (WCF) service specifies the announcement endpoints in the [\<serviceDiscovery>](servicediscovery.md) element and uses the AnnouncementClient to perform the announcements.</span></span> <span data-ttu-id="4c4e7-104">希望接聽來自其他服務之公告的用戶端實際上是作為 WCF 服務;因此，您必須在區段中設定該用戶端的公告端點 [\<services>](services.md) 。</span><span class="sxs-lookup"><span data-stu-id="4c4e7-104">A client wishing to listen for the announcement from other service is actually acting as a WCF service; thus you have to configure the announcement endpoints for that client in the [\<services>](services.md) section.</span></span>  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<standardEndpoints>**](standardendpoints.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<announcementEndpoint>**  
  
## <a name="syntax"></a><span data-ttu-id="4c4e7-105">Syntax</span><span class="sxs-lookup"><span data-stu-id="4c4e7-105">Syntax</span></span>  
  
```xml  
<system.serviceModel>
  <standardEndpoints>
    <announcementEndpoint>
      <standardEndpoint discoveryVersion="WSDiscovery11/WSDiscoveryApril2005"
                        maxAnnouncementDelay="Timespan"
                        name="String" />
    </announcementEndpoint>
  </standardEndpoints>
</system.serviceModel>
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="4c4e7-106">屬性和項目</span><span class="sxs-lookup"><span data-stu-id="4c4e7-106">Attributes and Elements</span></span>  

 <span data-ttu-id="4c4e7-107">下列章節說明屬性、子元素和父元素。</span><span class="sxs-lookup"><span data-stu-id="4c4e7-107">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="4c4e7-108">屬性</span><span class="sxs-lookup"><span data-stu-id="4c4e7-108">Attributes</span></span>  
  
|<span data-ttu-id="4c4e7-109">屬性</span><span class="sxs-lookup"><span data-stu-id="4c4e7-109">Attribute</span></span>|<span data-ttu-id="4c4e7-110">描述</span><span class="sxs-lookup"><span data-stu-id="4c4e7-110">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="4c4e7-111">discoveryVersion</span><span class="sxs-lookup"><span data-stu-id="4c4e7-111">discoveryVersion</span></span>|<span data-ttu-id="4c4e7-112">字串，此字串會指定兩個 WS-Discovery 通訊協定版本的其中之一。</span><span class="sxs-lookup"><span data-stu-id="4c4e7-112">A string that specifies one of the two versions of WS-Discovery protocol.</span></span> <span data-ttu-id="4c4e7-113">有效的值為 WSDiscovery11 和 WSDiscoveryApril2005。</span><span class="sxs-lookup"><span data-stu-id="4c4e7-113">Valid values are WSDiscovery11 and WSDiscoveryApril2005.</span></span> <span data-ttu-id="4c4e7-114">這個值的型別為 <xref:System.ServiceModel.Discovery.Configuration.AnnouncementEndpointElement.DiscoveryVersion>。</span><span class="sxs-lookup"><span data-stu-id="4c4e7-114">This value is of type <xref:System.ServiceModel.Discovery.Configuration.AnnouncementEndpointElement.DiscoveryVersion>.</span></span>|  
|<span data-ttu-id="4c4e7-115">maxAnnouncementDelay</span><span class="sxs-lookup"><span data-stu-id="4c4e7-115">maxAnnouncementDelay</span></span>|<span data-ttu-id="4c4e7-116">Timespan 值，這個值指定 Discovery 通訊協定傳送 Hello 訊息之前會等候的延遲值上限。</span><span class="sxs-lookup"><span data-stu-id="4c4e7-116">A Timespan value that specifies the maximum value for the delay the Discovery protocol will wait before sending a Hello message.</span></span> <span data-ttu-id="4c4e7-117">系統會等候一段隨機時間值 (介於 0 和此屬性的值之間)，之後才傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="4c4e7-117">The messages will wait for a random time value between 0 and the value of this attribute before being sent.</span></span> <span data-ttu-id="4c4e7-118">這個屬性用於設定一小段隨機的延遲，避免網路關閉而所有服務同時再次上線時網路負荷過大。</span><span class="sxs-lookup"><span data-stu-id="4c4e7-118">This attribute is used to set a small, random delay to prevent network storms when a network goes out and all services come back online at the same time.</span></span>|  
|<span data-ttu-id="4c4e7-119">NAME</span><span class="sxs-lookup"><span data-stu-id="4c4e7-119">name</span></span>|<span data-ttu-id="4c4e7-120">字串，這個字串會指定標準端點之組態的名稱。</span><span class="sxs-lookup"><span data-stu-id="4c4e7-120">A String that specifies the name of the configuration of the standard endpoint.</span></span> <span data-ttu-id="4c4e7-121">這個名稱用於服務端點的 `endpointConfiguration` 屬性中，可將標準端點連結至其組態。</span><span class="sxs-lookup"><span data-stu-id="4c4e7-121">The name is used in the `endpointConfiguration` attribute of the service endpoint to link a standard endpoint to its configuration.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="4c4e7-122">子元素</span><span class="sxs-lookup"><span data-stu-id="4c4e7-122">Child Elements</span></span>  

 <span data-ttu-id="4c4e7-123">無。</span><span class="sxs-lookup"><span data-stu-id="4c4e7-123">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="4c4e7-124">父項目</span><span class="sxs-lookup"><span data-stu-id="4c4e7-124">Parent Elements</span></span>  
  
|<span data-ttu-id="4c4e7-125">項目</span><span class="sxs-lookup"><span data-stu-id="4c4e7-125">Element</span></span>|<span data-ttu-id="4c4e7-126">描述</span><span class="sxs-lookup"><span data-stu-id="4c4e7-126">Description</span></span>|  
|-------------|-----------------|  
|[\<standardEndpoints>](standardendpoints.md)|<span data-ttu-id="4c4e7-127">標準端點的集合，這些端點是預先定義的端點，其中包含一個或多個固定的屬性 (位址、繫結、合約)。</span><span class="sxs-lookup"><span data-stu-id="4c4e7-127">A collection of standard endpoints that are pre-defined endpoints with one or more of their properties (address, binding, contract) fixed.</span></span>|  
  
## <a name="example"></a><span data-ttu-id="4c4e7-128">範例</span><span class="sxs-lookup"><span data-stu-id="4c4e7-128">Example</span></span>  

 <span data-ttu-id="4c4e7-129">下列範例示範透過 http 及 peernet 接聽公告訊息的用戶端。</span><span class="sxs-lookup"><span data-stu-id="4c4e7-129">The following example demonstrates a client listening for announcements messages over http and peernet.</span></span>  
  
```xml  
<services>
  <service name="ServiceAnnouncementListener">
    <endpoint name="httpAnnouncementEndpoint"
              kind="announcementEndpoint"
              binding="basicHttpBinding"
              address="announcements" />
    <endpoint name="peerNetAnnouncementEndpoint"
              kind="announcementEndpoint"
              binding="peerTcpBinding"
              address="net.p2p://discoveryMesh/multicast"
              bindingConfiguration="discoveryPeerTcpBindingConfig" />
  ...
  </service>
</services>

<standardEndpoints>
  <announcementEndpoint>
    <standardEndpoint name="httpAnnouncementEndpoint"
                      version="WSDiscoveryApril2005" />
    <standardEndpoint name="peerNetAnnouncementEndpoint"
                      version="WSDiscoveryApril2005" />
  </announcementEndpoint>
</standardEndpoints>
```  
  
## <a name="see-also"></a><span data-ttu-id="4c4e7-130">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4c4e7-130">See also</span></span>

- <xref:System.ServiceModel.Discovery.AnnouncementEndpoint>
