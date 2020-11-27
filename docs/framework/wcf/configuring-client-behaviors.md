---
title: 設定用戶端行為
description: 深入瞭解 WCF 設定行為的兩種方式：在應用程式佈建檔中，或從呼叫應用程式以程式設計方式進行。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: df5b32fa-e73b-4e8e-b66f-357c748e0173
ms.openlocfilehash: 34cbb9e31933debb5120eb30956c3a5f0be065ed
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96266710"
---
# <a name="configuring-client-behaviors"></a><span data-ttu-id="7999a-103">設定用戶端行為</span><span class="sxs-lookup"><span data-stu-id="7999a-103">Configuring Client Behaviors</span></span>

<span data-ttu-id="7999a-104">Windows Communication Foundation (WCF) 以兩種方式設定行為：藉由參考行為設定（定義于 `<behavior>` 用戶端應用程式設定檔的區段中），或在呼叫應用程式中以程式設計方式進行。</span><span class="sxs-lookup"><span data-stu-id="7999a-104">Windows Communication Foundation (WCF) configures behaviors in two ways: either by referring to behavior configurations -- which are defined in the `<behavior>` section of a client application configuration file – or programmatically in the calling application.</span></span> <span data-ttu-id="7999a-105">這個主題將描述這兩種方法。</span><span class="sxs-lookup"><span data-stu-id="7999a-105">This topic describes both approaches.</span></span>  
  
 <span data-ttu-id="7999a-106">使用組態檔時，行為組態都是具名的組態設定集合。</span><span class="sxs-lookup"><span data-stu-id="7999a-106">When using a configuration file, behavior configuration is a named collection of configuration settings.</span></span> <span data-ttu-id="7999a-107">每個行為組態的名稱必須是獨一無二的。</span><span class="sxs-lookup"><span data-stu-id="7999a-107">The name of each behavior configuration must be unique.</span></span> <span data-ttu-id="7999a-108">會在端點組態的 `behaviorConfiguration` 屬性中使用這個字串，以便將端點連結至行為。</span><span class="sxs-lookup"><span data-stu-id="7999a-108">This string is used in the `behaviorConfiguration` attribute of an endpoint configuration to link the endpoint to the behavior.</span></span>  
  
## <a name="example"></a><span data-ttu-id="7999a-109">範例</span><span class="sxs-lookup"><span data-stu-id="7999a-109">Example</span></span>  

 <span data-ttu-id="7999a-110">下列組態程式碼會定義名稱為 `myBehavior` 的行為。</span><span class="sxs-lookup"><span data-stu-id="7999a-110">The following configuration code defines a behavior called `myBehavior`.</span></span> <span data-ttu-id="7999a-111">用戶端端點會參考 `behaviorConfiguration` 屬性中的這個行為。</span><span class="sxs-lookup"><span data-stu-id="7999a-111">The client endpoint references this behavior in the `behaviorConfiguration` attribute.</span></span>  
  
```xml  
<configuration>  
    <system.serviceModel>  
        <behaviors>  
            <endpointBehaviors>  
                <behavior name="myBehavior">  
                    <clientVia />  
                </behavior>  
            </endpointBehaviors>  
        </behaviors>  
        <bindings>  
            <basicHttpBinding>  
                <binding name="myBinding" maxReceivedMessageSize="10000" />  
            </basicHttpBinding>  
        </bindings>  
        <client>  
            <endpoint address="myAddress" binding="basicHttpBinding" bindingConfiguration="myBinding" behaviorConfiguration="myBehavior" contract="myContract" />  
        </client>  
    </system.serviceModel>  
</configuration>  
```  
  
## <a name="using-behaviors-programmatically"></a><span data-ttu-id="7999a-112">以程式設計方式使用行為</span><span class="sxs-lookup"><span data-stu-id="7999a-112">Using Behaviors Programmatically</span></span>  

 <span data-ttu-id="7999a-113">您也可以在 `Behaviors` 開啟用戶端之前，在 Windows Communication Foundation (WCF) 用戶端物件或用戶端通道處理站物件上找到適當的屬性，以程式設計方式設定或插入行為。</span><span class="sxs-lookup"><span data-stu-id="7999a-113">You can also configure or insert behaviors programmatically by locating the appropriate `Behaviors` property on the Windows Communication Foundation (WCF) client object or on the client channel factory object prior to opening the client.</span></span>  
  
## <a name="example"></a><span data-ttu-id="7999a-114">範例</span><span class="sxs-lookup"><span data-stu-id="7999a-114">Example</span></span>  

 <span data-ttu-id="7999a-115">下列程式碼範例會示範如何以程式設計的方式插入行為，其方法是先存取傳回自 <xref:System.ServiceModel.Description.ServiceEndpoint.Behaviors%2A> 屬性之 <xref:System.ServiceModel.Description.ServiceEndpoint> 上的 <xref:System.ServiceModel.ChannelFactory.Endpoint%2A> 屬性，再建立通道物件。</span><span class="sxs-lookup"><span data-stu-id="7999a-115">The following code example shows how to programmatically insert a behavior by accessing the <xref:System.ServiceModel.Description.ServiceEndpoint.Behaviors%2A> property on the <xref:System.ServiceModel.Description.ServiceEndpoint> returned from the <xref:System.ServiceModel.ChannelFactory.Endpoint%2A> property prior to the creation of the channel object.</span></span>  
  
 [!code-csharp[ChannelFactoryBehaviors#10](../../../samples/snippets/csharp/VS_Snippets_CFX/channelfactorybehaviors/cs/client.cs#10)]
 [!code-vb[ChannelFactoryBehaviors#10](../../../samples/snippets/visualbasic/VS_Snippets_CFX/channelfactorybehaviors/vb/client.vb#10)]  
  
## <a name="see-also"></a><span data-ttu-id="7999a-116">另請參閱</span><span class="sxs-lookup"><span data-stu-id="7999a-116">See also</span></span>

- [\<behaviors>](../configure-apps/file-schema/wcf/behaviors.md)
