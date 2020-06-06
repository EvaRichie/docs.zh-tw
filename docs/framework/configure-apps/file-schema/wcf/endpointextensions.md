---
title: <endpointExtensions>
ms.date: 03/30/2017
ms.assetid: 33396e0a-1fae-4616-b822-923584eebfd1
ms.openlocfilehash: fe57cb84cfa70b1f6b92abf1dbac89ddad9d4dc8
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "69925703"
---
# \<endpointExtensions>
這個區段會在電腦或應用程式的組態檔的擴充區段中註冊新的標準端點。 您可以透過使用 `add` 關鍵字，並將項目的 `type` 屬性設定為端點型別，同時將 `name` 屬性設定為標準端點的名稱，將標準端點加入至這個集合。  
  
 下列範例使用 `add` 項目及 `name` 屬性，將標準端點加入至組態檔的 `<endpointExtensions>` 區段。  
  
```xml  
<system.serviceModel>
  <extensions>
    <endpointExtensions>
      <add name="udpDiscoveryEndpoint"
           type="System.Discovery.UdpEndpointCollectionElement, System.Discovery.dll, Version=1.0.0.0, Culture=neutral, PublicKeyToken=ffffffffffffffff"/>
    </endpointExtensions>
  </extensions>
</system.serviceModel>
```  
  
 註冊標準端點後，您可以如下列範例所示使用該端點。 在 [\<endpoint>](endpoint-element.md) 元素中， `kind` 屬性會指定已在區段中註冊的標準端點類型 `<endpointExtensions>` 。 `endpointConfiguration`屬性會與 `name` 一節中標準端點之 configuration 元素的屬性相同 `<standardEndpoints>` 。  
  
```xml  
<system.serviceModel>
  <services>
    <service name="Service1">
      <endpoint kind="udpDiscoveryEndpoint"
                endpointConfiguration="udpConfig" />
    </service>
  </services>
  <standardEndpoints>
    <udpDiscoveryEndpoint>
      <standardEndpoint name="udpConfig"
                        multicastAddress="soap.udp://239.255.255.250:3703"
                        ... />
    </udpDiscoveryEndpoint>
  </standardEndpoints>
</system.serviceModel>
```  
