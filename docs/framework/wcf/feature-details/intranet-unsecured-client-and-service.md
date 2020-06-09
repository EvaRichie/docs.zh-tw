---
title: 沒有安全保障的內部網路用戶端與服務
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: f450f5d4-3547-47ec-9320-2809e6a12634
ms.openlocfilehash: 591f7db0f6b4e928a991961d3bc7c404f41028bf
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84579276"
---
# <a name="intranet-unsecured-client-and-service"></a><span data-ttu-id="a394e-102">沒有安全保障的內部網路用戶端與服務</span><span class="sxs-lookup"><span data-stu-id="a394e-102">Intranet Unsecured Client and Service</span></span>
<span data-ttu-id="a394e-103">下圖說明一個簡單的 Windows Communication Foundation （WCF）服務，其開發目的是要將安全的私人網路資訊提供給 WCF 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a394e-103">The following illustration depicts a simple Windows Communication Foundation (WCF) service developed to provide information on a secure private network to a WCF application.</span></span> <span data-ttu-id="a394e-104">安全性不是必要的，因為資料的重要性較低、網路應原本就安全，或由 WCF 基礎結構底下的一層提供安全性。</span><span class="sxs-lookup"><span data-stu-id="a394e-104">Security is not required because the data is of low importance, the network is expected to be inherently secure, or security is provided by a layer below the WCF infrastructure.</span></span>  
  
 ![內部網路不安全的用戶端和服務案例。](./media/intranet-unsecured-client-and-service/unsecured-web-client-service.gif)  
  
|<span data-ttu-id="a394e-106">特性</span><span class="sxs-lookup"><span data-stu-id="a394e-106">Characteristic</span></span>|<span data-ttu-id="a394e-107">描述</span><span class="sxs-lookup"><span data-stu-id="a394e-107">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="a394e-108">安全性模式</span><span class="sxs-lookup"><span data-stu-id="a394e-108">Security Mode</span></span>|<span data-ttu-id="a394e-109">無</span><span class="sxs-lookup"><span data-stu-id="a394e-109">None</span></span>|  
|<span data-ttu-id="a394e-110">傳輸</span><span class="sxs-lookup"><span data-stu-id="a394e-110">Transport</span></span>|<span data-ttu-id="a394e-111">TCP</span><span class="sxs-lookup"><span data-stu-id="a394e-111">TCP</span></span>|  
|<span data-ttu-id="a394e-112">繫結</span><span class="sxs-lookup"><span data-stu-id="a394e-112">Binding</span></span>|<xref:System.ServiceModel.NetTcpBinding>|  
|<span data-ttu-id="a394e-113">互通性</span><span class="sxs-lookup"><span data-stu-id="a394e-113">Interoperability</span></span>|<span data-ttu-id="a394e-114">僅限 WCF</span><span class="sxs-lookup"><span data-stu-id="a394e-114">WCF only</span></span>|  
|<span data-ttu-id="a394e-115">驗證</span><span class="sxs-lookup"><span data-stu-id="a394e-115">Authentication</span></span>|<span data-ttu-id="a394e-116">無</span><span class="sxs-lookup"><span data-stu-id="a394e-116">None</span></span>|  
|<span data-ttu-id="a394e-117">完整性</span><span class="sxs-lookup"><span data-stu-id="a394e-117">Integrity</span></span>|<span data-ttu-id="a394e-118">無</span><span class="sxs-lookup"><span data-stu-id="a394e-118">None</span></span>|  
|<span data-ttu-id="a394e-119">保密</span><span class="sxs-lookup"><span data-stu-id="a394e-119">Confidentiality</span></span>|<span data-ttu-id="a394e-120">無</span><span class="sxs-lookup"><span data-stu-id="a394e-120">None</span></span>|  
  
## <a name="service"></a><span data-ttu-id="a394e-121">服務</span><span class="sxs-lookup"><span data-stu-id="a394e-121">Service</span></span>  
 <span data-ttu-id="a394e-122">下列程式碼和組態要獨立執行。</span><span class="sxs-lookup"><span data-stu-id="a394e-122">The following code and configuration are meant to run independently.</span></span> <span data-ttu-id="a394e-123">執行下列其中一個動作：</span><span class="sxs-lookup"><span data-stu-id="a394e-123">Do one of the following:</span></span>  
  
- <span data-ttu-id="a394e-124">使用不含組態的程式碼建立獨立服務。</span><span class="sxs-lookup"><span data-stu-id="a394e-124">Create a stand-alone service using the code with no configuration.</span></span>  
  
- <span data-ttu-id="a394e-125">使用提供的組態建立服務，但不要定義任何端點。</span><span class="sxs-lookup"><span data-stu-id="a394e-125">Create a service using the supplied configuration, but do not define any endpoints.</span></span>  
  
### <a name="code"></a><span data-ttu-id="a394e-126">程式碼</span><span class="sxs-lookup"><span data-stu-id="a394e-126">Code</span></span>  
 <span data-ttu-id="a394e-127">下列程式碼會示範如何建立無安全性的端點：</span><span class="sxs-lookup"><span data-stu-id="a394e-127">The following code shows how to create an endpoint with no security:</span></span>  
  
 [!code-csharp[C_UnsecuredService#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_unsecuredservice/cs/source.cs#2)]
 [!code-vb[C_UnsecuredService#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_unsecuredservice/vb/source.vb#2)]  
  
### <a name="configuration"></a><span data-ttu-id="a394e-128">組態</span><span class="sxs-lookup"><span data-stu-id="a394e-128">Configuration</span></span>  
 <span data-ttu-id="a394e-129">下列程式碼會設定使用組態的相同端點：</span><span class="sxs-lookup"><span data-stu-id="a394e-129">The following code sets up the same endpoint using configuration:</span></span>  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <behaviors />  
    <services>  
      <service behaviorConfiguration=""
               name="ServiceModel.Calculator">  
        <endpoint address="net.tcp://localhost:8008/Calculator"
                  binding="netTcpBinding"  
                  bindingConfiguration="tcp_Unsecured"
                  name="netTcp_ICalculator"  
                  contract="ServiceModel.ICalculator" />  
      </service>  
    </services>  
    <bindings>  
      <netTcpBinding>  
        <binding name="tcp_Unsecured">  
          <security mode="None" />  
        </binding>  
      </netTcpBinding>  
    </bindings>  
    <client />  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="client"></a><span data-ttu-id="a394e-130">用戶端</span><span class="sxs-lookup"><span data-stu-id="a394e-130">Client</span></span>  
 <span data-ttu-id="a394e-131">下列程式碼和組態要獨立執行。</span><span class="sxs-lookup"><span data-stu-id="a394e-131">The following code and configuration are meant to run independently.</span></span> <span data-ttu-id="a394e-132">執行下列其中一個動作：</span><span class="sxs-lookup"><span data-stu-id="a394e-132">Do one of the following:</span></span>  
  
- <span data-ttu-id="a394e-133">使用此程式碼 (和用戶端程式碼) 建立獨立用戶端。</span><span class="sxs-lookup"><span data-stu-id="a394e-133">Create a stand-alone client using the code (and client code).</span></span>  
  
- <span data-ttu-id="a394e-134">建立未定義任何端點位址的用戶端，</span><span class="sxs-lookup"><span data-stu-id="a394e-134">Create a client that does not define any endpoint addresses.</span></span> <span data-ttu-id="a394e-135">然後改用可接受組態名稱當做引數的用戶端建構函式。</span><span class="sxs-lookup"><span data-stu-id="a394e-135">Instead, use the client constructor that takes the configuration name as an argument.</span></span> <span data-ttu-id="a394e-136">例如：</span><span class="sxs-lookup"><span data-stu-id="a394e-136">For example:</span></span>  
  
     [!code-csharp[C_SecurityScenarios#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#0)]
     [!code-vb[C_SecurityScenarios#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#0)]  
  
### <a name="code"></a><span data-ttu-id="a394e-137">程式碼</span><span class="sxs-lookup"><span data-stu-id="a394e-137">Code</span></span>  
 <span data-ttu-id="a394e-138">下列程式碼顯示使用 TCP 通訊協定來存取不安全端點的基本 WCF 用戶端。</span><span class="sxs-lookup"><span data-stu-id="a394e-138">The following code shows a basic WCF client that accesses an unsecured endpoint using the TCP protocol.</span></span>  
  
 [!code-csharp[C_UnsecuredClient#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_unsecuredclient/cs/source.cs#2)]
 [!code-vb[C_UnsecuredClient#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_unsecuredclient/vb/source.vb#2)]  
  
### <a name="configuration"></a><span data-ttu-id="a394e-139">組態</span><span class="sxs-lookup"><span data-stu-id="a394e-139">Configuration</span></span>  
 <span data-ttu-id="a394e-140">下列組態程式碼會套用至用戶端：</span><span class="sxs-lookup"><span data-stu-id="a394e-140">The following configuration code applies to the client:</span></span>  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <bindings>  
      <netTcpBinding>  
        <binding name="NetTcpBinding_ICalculator" >  
          <security mode="None">  
          </security>  
        </binding>  
      </netTcpBinding>  
    </bindings>  
    <client>  
      <endpoint address="net.tcp://machineName:8008/Calculator "  
                binding="netTcpBinding"
                bindingConfiguration="NetTcpBinding_ICalculator"  
                contract="ICalculator"
                name="NetTcpBinding_ICalculator" />  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a><span data-ttu-id="a394e-141">請參閱</span><span class="sxs-lookup"><span data-stu-id="a394e-141">See also</span></span>

- <xref:System.ServiceModel.NetTcpBinding>
- [<span data-ttu-id="a394e-142">安全性總覽</span><span class="sxs-lookup"><span data-stu-id="a394e-142">Security Overview</span></span>](security-overview.md)
- <span data-ttu-id="a394e-143">[Windows Server AppFabric 的資訊安全模型](https://docs.microsoft.com/previous-versions/appfabric/ee677202(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="a394e-143">[Security Model for Windows Server App Fabric](https://docs.microsoft.com/previous-versions/appfabric/ee677202(v=azure.10))</span></span>
