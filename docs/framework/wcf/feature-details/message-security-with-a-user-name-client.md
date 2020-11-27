---
title: 使用者名稱用戶端的訊息安全性
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 36335cb9-76b8-4443-92c7-44f081eabb21
ms.openlocfilehash: 7168b393bde626c8c413cda3c7422e0eee4ce267
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96292866"
---
# <a name="message-security-with-a-user-name-client"></a><span data-ttu-id="2e2a4-102">使用者名稱用戶端的訊息安全性</span><span class="sxs-lookup"><span data-stu-id="2e2a4-102">Message Security with a User Name Client</span></span>

<span data-ttu-id="2e2a4-103">下圖顯示 Windows Communication Foundation 使用訊息層級安全性來保護 WCF) 服務和用戶端 (。</span><span class="sxs-lookup"><span data-stu-id="2e2a4-103">The following illustration shows an Windows Communication Foundation (WCF) service and client secured using message-level security.</span></span> <span data-ttu-id="2e2a4-104">服務會使用 X.509 憑證來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="2e2a4-104">The service is authenticated with an X.509 certificate.</span></span> <span data-ttu-id="2e2a4-105">用戶端會使用使用者名稱與密碼來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="2e2a4-105">The client authenticates using a user name and password.</span></span>  
  
 <span data-ttu-id="2e2a4-106">如需範例應用程式，請參閱 [訊息安全性使用者名稱](../samples/message-security-user-name.md)。</span><span class="sxs-lookup"><span data-stu-id="2e2a4-106">For a sample application, see [Message Security User Name](../samples/message-security-user-name.md).</span></span>  
  
 <span data-ttu-id="2e2a4-107">![使用使用者名稱驗證的訊息安全性](media/1fb10a61-7e1d-42f5-b1af-195bfee5b3c6.gif "1fb10a61-7e1d-42f5-b1af-195bfee5b3c6")</span><span class="sxs-lookup"><span data-stu-id="2e2a4-107">![Message security using username authentication](media/1fb10a61-7e1d-42f5-b1af-195bfee5b3c6.gif "1fb10a61-7e1d-42f5-b1af-195bfee5b3c6")</span></span>  
  
|<span data-ttu-id="2e2a4-108">特性</span><span class="sxs-lookup"><span data-stu-id="2e2a4-108">Characteristic</span></span>|<span data-ttu-id="2e2a4-109">描述</span><span class="sxs-lookup"><span data-stu-id="2e2a4-109">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="2e2a4-110">安全性模式</span><span class="sxs-lookup"><span data-stu-id="2e2a4-110">Security Mode</span></span>|<span data-ttu-id="2e2a4-111">訊息</span><span class="sxs-lookup"><span data-stu-id="2e2a4-111">Message</span></span>|  
|<span data-ttu-id="2e2a4-112">互通性</span><span class="sxs-lookup"><span data-stu-id="2e2a4-112">Interoperability</span></span>|<span data-ttu-id="2e2a4-113">Windows Communication Foundation 只 (WCF) </span><span class="sxs-lookup"><span data-stu-id="2e2a4-113">Windows Communication Foundation (WCF) only</span></span>|  
|<span data-ttu-id="2e2a4-114">驗證 (伺服器)</span><span class="sxs-lookup"><span data-stu-id="2e2a4-114">Authentication (Server)</span></span>|<span data-ttu-id="2e2a4-115">初始交涉需要伺服器驗證</span><span class="sxs-lookup"><span data-stu-id="2e2a4-115">Initial negotiation requires server authentication</span></span>|  
|<span data-ttu-id="2e2a4-116">驗證 (用戶端)</span><span class="sxs-lookup"><span data-stu-id="2e2a4-116">Authentication (Client)</span></span>|<span data-ttu-id="2e2a4-117">使用者名稱/密碼</span><span class="sxs-lookup"><span data-stu-id="2e2a4-117">User name/password</span></span>|  
|<span data-ttu-id="2e2a4-118">完整性</span><span class="sxs-lookup"><span data-stu-id="2e2a4-118">Integrity</span></span>|<span data-ttu-id="2e2a4-119">是，使用共用安全性內容</span><span class="sxs-lookup"><span data-stu-id="2e2a4-119">Yes, using shared security context</span></span>|  
|<span data-ttu-id="2e2a4-120">機密性</span><span class="sxs-lookup"><span data-stu-id="2e2a4-120">Confidentiality</span></span>|<span data-ttu-id="2e2a4-121">是，使用共用安全性內容</span><span class="sxs-lookup"><span data-stu-id="2e2a4-121">Yes, using shared security context</span></span>|  
|<span data-ttu-id="2e2a4-122">傳輸</span><span class="sxs-lookup"><span data-stu-id="2e2a4-122">Transport</span></span>|<span data-ttu-id="2e2a4-123">HTTP</span><span class="sxs-lookup"><span data-stu-id="2e2a4-123">HTTP</span></span>|  
|<span data-ttu-id="2e2a4-124">繫結</span><span class="sxs-lookup"><span data-stu-id="2e2a4-124">Binding</span></span>|<xref:System.ServiceModel.WSHttpBinding>|  
  
## <a name="service"></a><span data-ttu-id="2e2a4-125">服務</span><span class="sxs-lookup"><span data-stu-id="2e2a4-125">Service</span></span>  

 <span data-ttu-id="2e2a4-126">下列程式碼和組態要獨立執行。</span><span class="sxs-lookup"><span data-stu-id="2e2a4-126">The following code and configuration are meant to run independently.</span></span> <span data-ttu-id="2e2a4-127">請執行下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="2e2a4-127">Do one of the following:</span></span>  
  
- <span data-ttu-id="2e2a4-128">使用不含組態的程式碼建立獨立服務。</span><span class="sxs-lookup"><span data-stu-id="2e2a4-128">Create a stand-alone service using the code with no configuration.</span></span>  
  
- <span data-ttu-id="2e2a4-129">使用提供的組態建立服務，但不要定義任何端點。</span><span class="sxs-lookup"><span data-stu-id="2e2a4-129">Create a service using the supplied configuration, but do not define any endpoints.</span></span>  
  
### <a name="code"></a><span data-ttu-id="2e2a4-130">程式碼</span><span class="sxs-lookup"><span data-stu-id="2e2a4-130">Code</span></span>  

 <span data-ttu-id="2e2a4-131">下列程式碼會顯示如何建立會使用訊息安全性的服務端點。</span><span class="sxs-lookup"><span data-stu-id="2e2a4-131">The following code shows how to create a service endpoint that uses message security.</span></span>  
  
 [!code-csharp[C_SecurityScenarios#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#9)]
 [!code-vb[C_SecurityScenarios#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#9)]  
  
### <a name="configuration"></a><span data-ttu-id="2e2a4-132">設定</span><span class="sxs-lookup"><span data-stu-id="2e2a4-132">Configuration</span></span>  

 <span data-ttu-id="2e2a4-133">可使用下列組態來取代程式碼：</span><span class="sxs-lookup"><span data-stu-id="2e2a4-133">The following configuration can be used instead of the code:</span></span>  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="ServiceCredentialsBehavior">  
          <serviceCredentials>  
            <serviceCertificate findValue="Contoso.com"
                                storeLocation="LocalMachine"  
                                storeName="My"
                                x509FindType="FindBySubjectName" />  
          </serviceCredentials>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    <services>  
      <service behaviorConfiguration="ServiceCredentialsBehavior"  
               name="ServiceModel.Calculator">  
        <endpoint address="http://localhost/Calculator"  
                  binding="wsHttpBinding"  
                  bindingConfiguration="MessageAndUserName"  
                  name="SecuredByTransportEndpoint"  
                  contract="ServiceModel.ICalculator" />  
      </service>  
    </services>  
    <bindings>  
      <wsHttpBinding>  
        <binding name="MessageAndUserName">  
          <security mode="Message">
            <message clientCredentialType="UserName" />  
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
    <client />  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="client"></a><span data-ttu-id="2e2a4-134">用戶端</span><span class="sxs-lookup"><span data-stu-id="2e2a4-134">Client</span></span>  
  
### <a name="code"></a><span data-ttu-id="2e2a4-135">程式碼</span><span class="sxs-lookup"><span data-stu-id="2e2a4-135">Code</span></span>  

 <span data-ttu-id="2e2a4-136">下列程式碼會建立用戶端。</span><span class="sxs-lookup"><span data-stu-id="2e2a4-136">The following code creates the client.</span></span> <span data-ttu-id="2e2a4-137">繫結會使用訊息模式安全性，而且用戶端認證類型設為 `UserName`。</span><span class="sxs-lookup"><span data-stu-id="2e2a4-137">The binding is to message mode security, and the client credential type is set to `UserName`.</span></span> <span data-ttu-id="2e2a4-138">使用者名稱和密碼只能使用程式碼 (它是不可設定的) 來指定。</span><span class="sxs-lookup"><span data-stu-id="2e2a4-138">The user name and password can only be specified using code (it is not configurable).</span></span> <span data-ttu-id="2e2a4-139">在此不示範傳回使用者名稱與密碼的程式碼，因為必須在應用程式層級才能完成這個動作。</span><span class="sxs-lookup"><span data-stu-id="2e2a4-139">The code to return the user name and password is not shown here because it must be done at the application level.</span></span> <span data-ttu-id="2e2a4-140">例如，使用 [Windows 表單] 對話方塊查詢使用者的資料。</span><span class="sxs-lookup"><span data-stu-id="2e2a4-140">For example, use a Windows Forms dialog box to query the user for the data.</span></span>  
  
 [!code-csharp[C_SecurityScenarios#16](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#16)]
 [!code-vb[C_SecurityScenarios#16](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#16)]  
  
### <a name="configuration"></a><span data-ttu-id="2e2a4-141">設定</span><span class="sxs-lookup"><span data-stu-id="2e2a4-141">Configuration</span></span>  

 <span data-ttu-id="2e2a4-142">下列程式碼會設定用戶端。</span><span class="sxs-lookup"><span data-stu-id="2e2a4-142">The following code configures the client.</span></span> <span data-ttu-id="2e2a4-143">繫結會使用訊息模式安全性，而且用戶端認證類型設為 `UserName`。</span><span class="sxs-lookup"><span data-stu-id="2e2a4-143">The binding is to message mode security, and the client credential type is set to `UserName`.</span></span> <span data-ttu-id="2e2a4-144">使用者名稱和密碼只能使用程式碼 (它是不可設定的) 來指定。</span><span class="sxs-lookup"><span data-stu-id="2e2a4-144">The user name and password can only be specified using code (it is not configurable).</span></span>  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <bindings>  
      <wsHttpBinding>  
        <binding name="WSHttpBinding_ICalculator" >  
          <security mode="Message">  
            <message clientCredentialType="UserName" />  
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
    <client>  
      <endpoint address="http://machineName/Calculator"
                binding="wsHttpBinding"  
                bindingConfiguration="WSHttpBinding_ICalculator"
                contract="ICalculator"  
                name="WSHttpBinding_ICalculator">  
        <identity>  
          <dns value ="Contoso.com" />  
        </identity>  
      </endpoint>  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a><span data-ttu-id="2e2a4-145">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2e2a4-145">See also</span></span>

- [<span data-ttu-id="2e2a4-146">安全性概觀</span><span class="sxs-lookup"><span data-stu-id="2e2a4-146">Security Overview</span></span>](security-overview.md)
- [<span data-ttu-id="2e2a4-147">訊息安全性使用者名稱</span><span class="sxs-lookup"><span data-stu-id="2e2a4-147">Message Security User Name</span></span>](../samples/message-security-user-name.md)
- [<span data-ttu-id="2e2a4-148">服務身分識別和驗證</span><span class="sxs-lookup"><span data-stu-id="2e2a4-148">Service Identity and Authentication</span></span>](service-identity-and-authentication.md)
- [\<identity>](../../configure-apps/file-schema/wcf/identity.md)
- <span data-ttu-id="2e2a4-149">[Windows Server AppFabric 的資訊安全模型](/previous-versions/appfabric/ee677202(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="2e2a4-149">[Security Model for Windows Server App Fabric](/previous-versions/appfabric/ee677202(v=azure.10))</span></span>
