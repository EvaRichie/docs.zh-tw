---
title: 安全性驗證
ms.date: 03/30/2017
ms.assetid: 48dcd496-0c4f-48ce-8b9b-0e25b77ffa58
ms.openlocfilehash: 1260aaa756e7be33ce2aa1bcce5fc79be553c990
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96262615"
---
# <a name="security-validation"></a><span data-ttu-id="b20d0-102">安全性驗證</span><span class="sxs-lookup"><span data-stu-id="b20d0-102">Security validation</span></span>

<span data-ttu-id="b20d0-103">這個範例示範如何使用自訂行為驗證電腦上的服務，以確定服務符合特定條件。</span><span class="sxs-lookup"><span data-stu-id="b20d0-103">This sample demonstrates how to use a custom behavior to validate services on a computer to ensure they meet specific criteria.</span></span> <span data-ttu-id="b20d0-104">在這個範例中，服務會經過驗證，其方式是自訂行為掃描服務上的每個端點，並檢查這些端點是否包含安全繫結項目。</span><span class="sxs-lookup"><span data-stu-id="b20d0-104">In this sample, services are validated by the custom behavior by scanning through each endpoint on the service and checking to see whether they contain secure binding elements.</span></span> <span data-ttu-id="b20d0-105">這個範例是以 [消費者入門](getting-started-sample.md)為基礎。</span><span class="sxs-lookup"><span data-stu-id="b20d0-105">This sample is based on the [Getting Started](getting-started-sample.md).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="b20d0-106">此範例的安裝程序與建置指示位於本主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="b20d0-106">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>  
  
## <a name="endpoint-validation-custom-behavior"></a><span data-ttu-id="b20d0-107">端點驗證自訂行為</span><span class="sxs-lookup"><span data-stu-id="b20d0-107">Endpoint Validation Custom Behavior</span></span>  

 <span data-ttu-id="b20d0-108">將使用者程式碼新增至包含在 `Validate` 介面中的 <xref:System.ServiceModel.Description.IServiceBehavior> 方法，可以提供自訂行為給服務或端點用來執行使用者定義的動作。</span><span class="sxs-lookup"><span data-stu-id="b20d0-108">By adding user code to the `Validate` method contained in the <xref:System.ServiceModel.Description.IServiceBehavior> interface, custom behavior can be given to a service or endpoint to perform user-defined actions.</span></span> <span data-ttu-id="b20d0-109">下列程式碼是用來對服務中包含的每個端點執行迴圈，以搜尋整個繫結集合中的安全繫結。</span><span class="sxs-lookup"><span data-stu-id="b20d0-109">The following code is used to loop through each endpoint contained in a service, which searches through their binding collections for secure bindings.</span></span>  
  
```csharp
public void Validate(ServiceDescription serviceDescription,
                                       ServiceHostBase serviceHostBase)  
{  
    // Loop through each endpoint individually, gathering their
    // binding elements.  
    foreach (ServiceEndpoint endpoint in serviceDescription.Endpoints)  
    {  
        secureElementFound = false;  
  
        // Retrieve the endpoint's binding element collection.  
        BindingElementCollection bindingElements =
            endpoint.Binding.CreateBindingElements();  
  
        // Look to see if the binding elements collection contains any
        // secure binding elements. Transport, Asymmetric, and Symmetric
        // binding elements are all derived from SecurityBindingElement.  
        if ((bindingElements.Find<SecurityBindingElement>() != null) || (bindingElements.Find<HttpsTransportBindingElement>() != null) || (bindingElements.Find<WindowsStreamSecurityBindingElement>() != null) || (bindingElements.Find<SslStreamSecurityBindingElement>() != null))  
        {  
            secureElementFound = true;  
        }  
  
    // Send a message to the system event viewer when an endpoint is deemed insecure.  
    if (!secureElementFound)  
        throw new Exception(System.DateTime.Now.ToString() + ": The endpoint \"" + endpoint.Name + "\" has no secure bindings.");  
    }  
}  
```  
  
 <span data-ttu-id="b20d0-110">將下列程式碼新增至 Web.config 檔案，就可以為所要辨認的服務新增 `serviceValidate` 行為延伸。</span><span class="sxs-lookup"><span data-stu-id="b20d0-110">Adding the following code to Web.config file adds the `serviceValidate` behavior extension for the service to recognize.</span></span>  
  
```xml  
<system.serviceModel>  
    <extensions>  
        <behaviorExtensions>  
            <add name="endpointValidate" type="Microsoft.ServiceModel.Samples.EndpointValidateElement, endpointValidate, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null" />  
        </behaviorExtensions>  
    </extensions>
    ...
</system.serviceModel>
```  
  
 <span data-ttu-id="b20d0-111">一旦將行為延伸新增至服務，就會立即將 `endpointValidate` 行為新增至 Web.config 檔案中的行為清單，從而新增至服務。</span><span class="sxs-lookup"><span data-stu-id="b20d0-111">Once the behavior extension is added to the service, it is now possible to add the `endpointValidate` behavior to the list of behaviors in the Web.config file and thus, to the service.</span></span>  
  
```xml  
<behaviors>  
    <serviceBehaviors>  
        <behavior name="CalcServiceSEB1">  
            <serviceMetadata httpGetEnabled="true" />  
            <endpointValidate />  
        </behavior>  
    </serviceBehaviors>  
</behaviors>  
```  
  
 <span data-ttu-id="b20d0-112">新增至 Web.config 檔案的行為及其延伸會將行為套用至個別服務；然而，當新增至 Machine.config 檔案時，則會將行為套用至電腦上所有在作用中的服務。</span><span class="sxs-lookup"><span data-stu-id="b20d0-112">Behaviors and their extensions that are added to the Web.config file apply behavior to individual services, while when added to the Machine.config file apply behavior to every service active on the computer.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="b20d0-113">將行為新增至所有服務時，建議您最好在進行任何變更前先備份 Machine.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="b20d0-113">When adding behavior to all services, it is suggested to backup the Machine.config file before making any change.</span></span>  
  
 <span data-ttu-id="b20d0-114">現在，請執行本範例 client\bin 目錄中提供的用戶端。</span><span class="sxs-lookup"><span data-stu-id="b20d0-114">Now run the client provided in the client\bin directory of this sample.</span></span> <span data-ttu-id="b20d0-115">擲回例外狀況，並出現下列訊息：「無法啟動要求的服務 ' http://localhost/servicemodelsamples/service.svc '。」</span><span class="sxs-lookup"><span data-stu-id="b20d0-115">An exception is thrown with the following message: "The requested service, 'http://localhost/servicemodelsamples/service.svc' could not be activated."</span></span> <span data-ttu-id="b20d0-116">這是預料中的事，因為端點驗證行為認為該端點不安全，所以不讓服務啟動。</span><span class="sxs-lookup"><span data-stu-id="b20d0-116">This is expected because an endpoint is considered insecure by the endpoint validating behavior and prevents the service from being started.</span></span> <span data-ttu-id="b20d0-117">這個行為還會擲回內部例外狀況，以描述哪個端點不安全，並且在系統「事件檢視器」中的 [System.ServiceModel 4.0.0.0] 來源與 [WebHost] 類別下方寫入訊息。</span><span class="sxs-lookup"><span data-stu-id="b20d0-117">The behavior also throws an internal exception that describes which endpoint is insecure and writes a message to the system Event Viewer under the "System.ServiceModel 4.0.0.0" source and the "WebHost" category.</span></span> <span data-ttu-id="b20d0-118">此外，您也可以在這個範例中的服務上開啟追蹤功能。</span><span class="sxs-lookup"><span data-stu-id="b20d0-118">It is also possible to turn on tracing on the service in this sample.</span></span> <span data-ttu-id="b20d0-119">這將允許使用者使用「服務追蹤檢視器」工具開啟產生的服務追蹤，以檢視端點驗證行為擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b20d0-119">This allows the user to view the exceptions thrown by endpoint validating behavior by opening the resulting service traces using the Service Trace Viewer tool.</span></span>  
  
### <a name="view-failed-endpoint-validation-exception-messages-in-the-event-viewer"></a><span data-ttu-id="b20d0-120">在事件檢視器中查看失敗的端點驗證例外狀況訊息</span><span class="sxs-lookup"><span data-stu-id="b20d0-120">View failed endpoint validation exception messages in the Event Viewer</span></span>  
  
1. <span data-ttu-id="b20d0-121">按一下 [ **開始** ] 功能表，然後選取 [ **執行 ...**]。</span><span class="sxs-lookup"><span data-stu-id="b20d0-121">Click the **Start** menu and select **Run…**.</span></span>  
  
2. <span data-ttu-id="b20d0-122">輸入 `eventvwr` ，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="b20d0-122">Type `eventvwr` and click **OK**.</span></span>  
  
3. <span data-ttu-id="b20d0-123">在 [事件檢視器] 視窗中，按一下 [ **應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="b20d0-123">In the Event Viewer window, click **Application**.</span></span>  
  
4. <span data-ttu-id="b20d0-124">在 [ **應用程式** ] 視窗中，按兩下 [WebHost] 類別下最近新增的 [system.servicemodel 4.0.0.0] 事件，以查看不安全的端點訊息。</span><span class="sxs-lookup"><span data-stu-id="b20d0-124">Double-click the recently added "System.ServiceModel 4.0.0.0" event under the "WebHost" category in the **Application** window to view insecure endpoint messages.</span></span>  
  
## <a name="set-up-build-and-run-the-sample"></a><span data-ttu-id="b20d0-125">設定、建立及執行範例</span><span class="sxs-lookup"><span data-stu-id="b20d0-125">Set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="b20d0-126">確定您已 [針對 Windows Communication Foundation 範例執行一次性安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="b20d0-126">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2. <span data-ttu-id="b20d0-127">若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="b20d0-127">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
3. <span data-ttu-id="b20d0-128">若要在單一或跨電腦的設定中執行範例，請遵循執行 [Windows Communication Foundation 範例](running-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="b20d0-128">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="b20d0-129">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="b20d0-129">The samples may already be installed on your computer.</span></span> <span data-ttu-id="b20d0-130">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="b20d0-130">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="b20d0-131">如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="b20d0-131">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="b20d0-132">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="b20d0-132">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Management\ServiceValidation`  
  
## <a name="see-also"></a><span data-ttu-id="b20d0-133">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b20d0-133">See also</span></span>

- <span data-ttu-id="b20d0-134">[AppFabric 監控範例](/previous-versions/appfabric/ff383407(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="b20d0-134">[AppFabric Monitoring Samples](/previous-versions/appfabric/ff383407(v=azure.10))</span></span>
