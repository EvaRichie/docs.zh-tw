---
title: 自訂訊息攔截器
ms.date: 03/30/2017
ms.assetid: 73f20972-53f8-475a-8bfe-c133bfa225b0
ms.openlocfilehash: a3362ee33e6d3813d6715646ecb7d066f1930c76
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96240910"
---
# <a name="custom-message-interceptor"></a><span data-ttu-id="c3d76-102">自訂訊息攔截器</span><span class="sxs-lookup"><span data-stu-id="c3d76-102">Custom Message Interceptor</span></span>

<span data-ttu-id="c3d76-103">這個範例示範通道擴充性模型的使用方式。</span><span class="sxs-lookup"><span data-stu-id="c3d76-103">This sample demonstrates the use of the channel extensibility model.</span></span> <span data-ttu-id="c3d76-104">尤其，這個範例會示範如何實作建立通道處理站和通道接聽程式的自訂繫結項目，以攔截執行階段堆疊中特定點的所有傳入與傳出訊息。</span><span class="sxs-lookup"><span data-stu-id="c3d76-104">In particular, it shows how to implement a custom binding element that creates channel factories and channel listeners to intercept all incoming and outgoing messages at a particular point in the run-time stack.</span></span> <span data-ttu-id="c3d76-105">範例也包含用戶端和伺服器，以示範這些自訂處理站的使用方式。</span><span class="sxs-lookup"><span data-stu-id="c3d76-105">The sample also includes a client and server that demonstrate the use of these custom factories.</span></span>  
  
 <span data-ttu-id="c3d76-106">在這個範例中，用戶端和服務都是主控台程式 (.exe)。</span><span class="sxs-lookup"><span data-stu-id="c3d76-106">In this sample, both the client and the service are console programs (.exe).</span></span> <span data-ttu-id="c3d76-107">用戶端和服務都會使用含有自訂繫結項目及其相關執行階段物件的通用程式庫 (.dll)。</span><span class="sxs-lookup"><span data-stu-id="c3d76-107">The client and service both make use of a common library (.dll) that contains the custom binding element and its associated run-time objects.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="c3d76-108">此範例的安裝程序與建置指示位於本主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="c3d76-108">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="c3d76-109">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="c3d76-109">The samples may already be installed on your machine.</span></span> <span data-ttu-id="c3d76-110">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="c3d76-110">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="c3d76-111">如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="c3d76-111">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="c3d76-112">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="c3d76-112">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Channels\MessageInterceptor`  
  
 <span data-ttu-id="c3d76-113">此範例說明使用通道架構並遵循 WCF 最佳作法，在 Windows Communication Foundation (WCF) 中建立自訂分層通道的建議程式。</span><span class="sxs-lookup"><span data-stu-id="c3d76-113">The sample describes the recommended procedure for creating a custom layered channel in Windows Communication Foundation (WCF), by using the channel framework and following WCF best practices.</span></span> <span data-ttu-id="c3d76-114">建立自訂層次通道的步驟如下：</span><span class="sxs-lookup"><span data-stu-id="c3d76-114">The steps to create a custom layered channel are as follows:</span></span>  
  
1. <span data-ttu-id="c3d76-115">決定通道處理站和通道接聽項所要支援的通道類型。</span><span class="sxs-lookup"><span data-stu-id="c3d76-115">Decide which of the channel shapes your channel factory and channel listener will support.</span></span>  
  
2. <span data-ttu-id="c3d76-116">建立支援您通道類型的通道處理站和通道接聽項。</span><span class="sxs-lookup"><span data-stu-id="c3d76-116">Create a channel factory and a channel listener that support your channel shapes.</span></span>  
  
3. <span data-ttu-id="c3d76-117">新增繫結項目，而此繫結項目會將自訂層次通道新增至通道堆疊。</span><span class="sxs-lookup"><span data-stu-id="c3d76-117">Add a binding element that adds the custom layered channel to a channel stack.</span></span>  
  
4. <span data-ttu-id="c3d76-118">新增繫結元素延伸區段，即可將新的繫結元素公開至組態系統。</span><span class="sxs-lookup"><span data-stu-id="c3d76-118">Add a binding element extension section to expose the new binding element to the configuration system.</span></span>  
  
## <a name="channel-shapes"></a><span data-ttu-id="c3d76-119">通道形狀</span><span class="sxs-lookup"><span data-stu-id="c3d76-119">Channel Shapes</span></span>  

 <span data-ttu-id="c3d76-120">撰寫自訂層次通道時的第一個步驟是，決定通道所需要的類型。</span><span class="sxs-lookup"><span data-stu-id="c3d76-120">The first step in writing a custom layered channel is to decide which shapes are required for the channel.</span></span> <span data-ttu-id="c3d76-121">對於訊息偵測器，我們支援下面層次所支援的任何類型 (例如，如果下面的層次可以建置 <xref:System.ServiceModel.Channels.IOutputChannel> 和 <xref:System.ServiceModel.Channels.IDuplexSessionChannel>，則也會公開 <xref:System.ServiceModel.Channels.IOutputChannel> 和 <xref:System.ServiceModel.Channels.IDuplexSessionChannel>)。</span><span class="sxs-lookup"><span data-stu-id="c3d76-121">For our message inspector, we support any shape that the layer below us supports (for example, if the layer below us can build <xref:System.ServiceModel.Channels.IOutputChannel> and <xref:System.ServiceModel.Channels.IDuplexSessionChannel>, then we also expose <xref:System.ServiceModel.Channels.IOutputChannel> and <xref:System.ServiceModel.Channels.IDuplexSessionChannel>).</span></span>  
  
## <a name="channel-factory-and-listener-factory"></a><span data-ttu-id="c3d76-122">通道處理站和接聽項處理站</span><span class="sxs-lookup"><span data-stu-id="c3d76-122">Channel Factory and Listener Factory</span></span>  

 <span data-ttu-id="c3d76-123">撰寫自訂層次通道的下一個步驟是，建立用戶端通道的 <xref:System.ServiceModel.Channels.IChannelFactory> 實作以及服務通道的 <xref:System.ServiceModel.Channels.IChannelListener> 實作。</span><span class="sxs-lookup"><span data-stu-id="c3d76-123">The next step in writing a custom layered channel is to create an implementation of <xref:System.ServiceModel.Channels.IChannelFactory> for client channels and of <xref:System.ServiceModel.Channels.IChannelListener> for service channels.</span></span>  
  
 <span data-ttu-id="c3d76-124">這些類別會接受內部處理站和接聽項，並且將除了 `OnCreateChannel` 和 `OnAcceptChannel` 以外的所有呼叫委派至內部處理站和接聽項。</span><span class="sxs-lookup"><span data-stu-id="c3d76-124">These classes take an inner factory and listener, and delegate all but the `OnCreateChannel` and `OnAcceptChannel` calls to the inner factory and listener.</span></span>  
  
```csharp
class InterceptingChannelFactory<TChannel> : ChannelFactoryBase<TChannel>  
{
    //...
}

class InterceptingChannelListener<TChannel> : ListenerFactoryBase<TChannel>  
{
    //...
}  
```  
  
## <a name="adding-a-binding-element"></a><span data-ttu-id="c3d76-125">新增繫結項目</span><span class="sxs-lookup"><span data-stu-id="c3d76-125">Adding a Binding Element</span></span>  

 <span data-ttu-id="c3d76-126">範例會定義自訂繫結項目：`InterceptingBindingElement`。</span><span class="sxs-lookup"><span data-stu-id="c3d76-126">The sample defines a custom binding element: `InterceptingBindingElement`.</span></span> <span data-ttu-id="c3d76-127">`InterceptingBindingElement` 採用 `ChannelMessageInterceptor` 做為輸入，並使用它 `ChannelMessageInterceptor` 來管理通過它的訊息。</span><span class="sxs-lookup"><span data-stu-id="c3d76-127">`InterceptingBindingElement` takes a `ChannelMessageInterceptor` as an input, and uses this `ChannelMessageInterceptor` to manipulate messages that pass through it.</span></span> <span data-ttu-id="c3d76-128">這是唯一必須為公用的類別。</span><span class="sxs-lookup"><span data-stu-id="c3d76-128">This is the only class that must be public.</span></span> <span data-ttu-id="c3d76-129">處理站、接聽項和通道全部都可以是公用執行階段介面的內部實作。</span><span class="sxs-lookup"><span data-stu-id="c3d76-129">The factory, listener, and channels can all be internal implementations of the public run-time interfaces.</span></span>  
  
```csharp
public class InterceptingBindingElement : BindingElement
{
}
```  
  
## <a name="adding-configuration-support"></a><span data-ttu-id="c3d76-130">新增組態支援</span><span class="sxs-lookup"><span data-stu-id="c3d76-130">Adding Configuration Support</span></span>  

 <span data-ttu-id="c3d76-131">為了與繫結組態整合，程式庫會將組態區段處理常式定義為繫結項目延伸區段。</span><span class="sxs-lookup"><span data-stu-id="c3d76-131">To integrate with binding configuration, the library defines a configuration section handler as a binding element extension section.</span></span> <span data-ttu-id="c3d76-132">用戶端和伺服器組態檔必須向組態系統註冊繫結項目延伸。</span><span class="sxs-lookup"><span data-stu-id="c3d76-132">The client and server configuration files must register the binding element extension with the configuration system.</span></span> <span data-ttu-id="c3d76-133">想要將其繫結項目公開給組態系統的實作器都可以衍生自這個類別。</span><span class="sxs-lookup"><span data-stu-id="c3d76-133">Implementers that want to expose their binding element to the configuration system can derive from this class.</span></span>  
  
```csharp
public abstract class InterceptingElement : BindingElementExtensionElement
{
    //...
}
```  
  
## <a name="adding-policy"></a><span data-ttu-id="c3d76-134">新增原則</span><span class="sxs-lookup"><span data-stu-id="c3d76-134">Adding Policy</span></span>  

 <span data-ttu-id="c3d76-135">為了與原則系統整合，`InterceptingBindingElement` 會實作 IPolicyExportExtension 以表示必須參與產生原則。</span><span class="sxs-lookup"><span data-stu-id="c3d76-135">To integrate with our policy system, `InterceptingBindingElement` implements IPolicyExportExtension to signal that we should participate in generating policy.</span></span> <span data-ttu-id="c3d76-136">若要在產生的用戶端上支援匯入原則，使用者可以註冊 `InterceptingBindingElementImporter` 的衍生類別，並覆寫 `CreateMessageInterceptor`() 來產生啟用原則的 `ChannelMessageInterceptor` 類別。</span><span class="sxs-lookup"><span data-stu-id="c3d76-136">To support importing policy on a generated client, the user can register a derived class of `InterceptingBindingElementImporter` and override `CreateMessageInterceptor`() to generate their policy-enabled `ChannelMessageInterceptor` class.</span></span>  
  
## <a name="example-droppable-message-inspector"></a><span data-ttu-id="c3d76-137">範例：可卸除的訊息偵測器</span><span class="sxs-lookup"><span data-stu-id="c3d76-137">Example: Droppable Message Inspector</span></span>  

 <span data-ttu-id="c3d76-138">範例中包含了會卸除訊息的 `ChannelMessageInspector` 的範例實作。</span><span class="sxs-lookup"><span data-stu-id="c3d76-138">Included in the sample is an example implementation of `ChannelMessageInspector` which drops messages.</span></span>  
  
```csharp
class DroppingServerElement : InterceptingElement  
{  
    protected override ChannelMessageInterceptor CreateMessageInterceptor()  
    {  
        return new DroppingServerInterceptor();  
    }  
}  
```  
  
 <span data-ttu-id="c3d76-139">您可以從組態中存取，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c3d76-139">You can access it from configuration as follows:</span></span>  
  
```xml  
<configuration>  
    ...  
    <system.serviceModel>  
        ...  
        <extensions>  
            <bindingElementExtensions>  
                <add name="droppingInterceptor"
                   type=  
          "Microsoft.ServiceModel.Samples.DroppingServerElement, library"/>  
            </bindingElementExtensions>  
        </extensions>  
    </system.serviceModel>  
</configuration>  
```  
  
 <span data-ttu-id="c3d76-140">用戶端和伺服器都會使用這個新建立的組態區段，將自訂處理站插入至執行階段通道堆疊的最下一層 (在傳輸層級之上)。</span><span class="sxs-lookup"><span data-stu-id="c3d76-140">The client and server both use this newly created configuration section to insert the custom factories into the lowest-level of their run-time channel stacks (above the transport level).</span></span>  
  
```xml  
<customBinding>  
  <binding name="sampleBinding">  
    <droppingInterceptor/>  
    <httpTransport/>  
  </binding>  
</customBinding>  
```  
  
 <span data-ttu-id="c3d76-141">用戶端會使用 `MessageInterceptor` 程式庫，將自訂標頭新增至偶數編號的訊息。</span><span class="sxs-lookup"><span data-stu-id="c3d76-141">The client uses the `MessageInterceptor` library to add a custom header to even numbered messages.</span></span> <span data-ttu-id="c3d76-142">另一方面，服務則會使用 `MessageInterceptor` 程式庫來卸除任何沒有這個特殊標頭的訊息。</span><span class="sxs-lookup"><span data-stu-id="c3d76-142">The service on the other hand uses `MessageInterceptor` library to drop any messages that do not have this special header.</span></span>  
  
 <span data-ttu-id="c3d76-143">在依序執行服務和用戶端之後，您應該看見下列用戶端輸出。</span><span class="sxs-lookup"><span data-stu-id="c3d76-143">You should see the following client output after running the service and then the client.</span></span>  
  
```console  
Reporting the next 10 wind speed  
100 kph  
Server dropped a message.  
90 kph  
80 kph  
Server dropped a message.  
70 kph  
60 kph  
Server dropped a message.  
50 kph  
40 kph  
Server dropped a message.  
30 kph  
20 kph  
Server dropped a message.  
10 kph  
Press ENTER to shut down client  
```  
  
 <span data-ttu-id="c3d76-144">用戶端會向服務報告 10 種不同的風速，但是只將其中半數標記以特殊標頭。</span><span class="sxs-lookup"><span data-stu-id="c3d76-144">The client reports 10 different wind speeds to the service, but only tags half of them with the special header.</span></span>  
  
 <span data-ttu-id="c3d76-145">您應該會在服務上看見下列輸出：</span><span class="sxs-lookup"><span data-stu-id="c3d76-145">On the service, you should see the following output:</span></span>  
  
```console  
Press ENTER to exit.  
Dangerous wind detected! Reported speed (90) is greater than 64 kph.  
Dangerous wind detected! Reported speed (70) is greater than 64 kph.  
5 wind speed reports have been received.  
```  
  
### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="c3d76-146">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="c3d76-146">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="c3d76-147">使用下列命令安裝 ASP.NET 4.0。</span><span class="sxs-lookup"><span data-stu-id="c3d76-147">Install ASP.NET 4.0 using the following command.</span></span>  
  
    ```console  
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable  
    ```  
  
2. <span data-ttu-id="c3d76-148">確定您已 [針對 Windows Communication Foundation 範例執行一次性安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="c3d76-148">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
3. <span data-ttu-id="c3d76-149">若要建立方案，請依照 [建立 Windows Communication Foundation 範例](building-the-samples.md)中的指示進行。</span><span class="sxs-lookup"><span data-stu-id="c3d76-149">To build the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
4. <span data-ttu-id="c3d76-150">若要在單一或跨電腦的設定中執行範例，請遵循執行 [Windows Communication Foundation 範例](running-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="c3d76-150">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>  
  
5. <span data-ttu-id="c3d76-151">先執行 Service.exe，然後執行 Client.exe，再查看兩個主控台視窗上的輸出。</span><span class="sxs-lookup"><span data-stu-id="c3d76-151">Run Service.exe first then run Client.exe and watch both console windows for output.</span></span>  
