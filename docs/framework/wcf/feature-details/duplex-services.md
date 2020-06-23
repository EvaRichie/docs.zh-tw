---
title: 雙工服務
description: 瞭解如何在 WCF 中建立雙工服務合約，讓這兩個端點可以透過用戶端建立的通道，將訊息傳送給彼此。
ms.date: 05/09/2018
dev_langs:
- csharp
- vb
ms.assetid: 396b875a-d203-4ebe-a3a1-6a330d962e95
ms.openlocfilehash: a43bb63a0ccf1a34b79dce755c19f7ed4cb6c16c
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85247347"
---
# <a name="duplex-services"></a><span data-ttu-id="c043b-103">雙工服務</span><span class="sxs-lookup"><span data-stu-id="c043b-103">Duplex Services</span></span>

<span data-ttu-id="c043b-104">雙工服務合約為訊息交換模式，其中的兩個端點可以彼此獨立地傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="c043b-104">A duplex service contract is a message exchange pattern in which both endpoints can send messages to the other independently.</span></span> <span data-ttu-id="c043b-105">因此，雙工服務可以將訊息傳送回用戶端端點，以提供類似事件的行為。</span><span class="sxs-lookup"><span data-stu-id="c043b-105">A duplex service, therefore, can send messages back to the client endpoint, providing event-like behavior.</span></span> <span data-ttu-id="c043b-106">用戶端建立與服務的連線，並提供服務所需的通道以供服務將訊息傳回用戶端，這個程序即是所謂的雙工通訊。</span><span class="sxs-lookup"><span data-stu-id="c043b-106">Duplex communication occurs when a client connects to a service and provides the service with a channel on which the service can send messages back to the client.</span></span> <span data-ttu-id="c043b-107">請注意，雙工服務的類似事件行為只會在工作階段內運作。</span><span class="sxs-lookup"><span data-stu-id="c043b-107">Note that the event-like behavior of duplex services only works within a session.</span></span>

<span data-ttu-id="c043b-108">若要建立雙工合約，您可建立一組介面。</span><span class="sxs-lookup"><span data-stu-id="c043b-108">To create a duplex contract you create a pair of interfaces.</span></span> <span data-ttu-id="c043b-109">第一個是服務合約介面，說明用戶端可叫用的作業。</span><span class="sxs-lookup"><span data-stu-id="c043b-109">The first is the service contract interface that describes the operations that a client can invoke.</span></span> <span data-ttu-id="c043b-110">該服務合約必須在屬性中指定*回呼合約* <xref:System.ServiceModel.ServiceContractAttribute.CallbackContract%2A?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="c043b-110">That service contract must specify a *callback contract* in the <xref:System.ServiceModel.ServiceContractAttribute.CallbackContract%2A?displayProperty=nameWithType> property.</span></span> <span data-ttu-id="c043b-111">回呼合約是一個介面，會定義服務可在用戶端端點上呼叫的作業。</span><span class="sxs-lookup"><span data-stu-id="c043b-111">The callback contract is the interface that defines the operations that the service can call on the client endpoint.</span></span> <span data-ttu-id="c043b-112">雙工合約不需要工作階段，不過系統提供的雙工繫結會利用工作階段。</span><span class="sxs-lookup"><span data-stu-id="c043b-112">A duplex contract does not require a session, although the system-provided duplex bindings make use of them.</span></span>

<span data-ttu-id="c043b-113">以下為雙工合約的範例。</span><span class="sxs-lookup"><span data-stu-id="c043b-113">The following is an example of a duplex contract.</span></span>

[!code-csharp[c_DuplexServices#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_duplexservices/cs/service.cs#0)]
[!code-vb[c_DuplexServices#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_duplexservices/vb/service.vb#0)]

<span data-ttu-id="c043b-114">`CalculatorService` 類別會實作主要的 `ICalculatorDuplex` 介面。</span><span class="sxs-lookup"><span data-stu-id="c043b-114">The `CalculatorService` class implements the primary `ICalculatorDuplex` interface.</span></span> <span data-ttu-id="c043b-115">服務會使用 <xref:System.ServiceModel.InstanceContextMode.PerSession> 執行個體模式維持各工作階段的結果。</span><span class="sxs-lookup"><span data-stu-id="c043b-115">The service uses the <xref:System.ServiceModel.InstanceContextMode.PerSession> instance mode to maintain the result for each session.</span></span> <span data-ttu-id="c043b-116">而名為 `Callback` 的私用屬性會存取用戶端的回呼通道。</span><span class="sxs-lookup"><span data-stu-id="c043b-116">A private property named `Callback` accesses the callback channel to the client.</span></span> <span data-ttu-id="c043b-117">服務會使用回呼，以透過回呼介面將訊息傳回用戶端，如以下範例程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="c043b-117">The service uses the callback for sending messages back to the client through the callback interface, as shown in the following sample code.</span></span>

[!code-csharp[c_DuplexServices#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_duplexservices/cs/service.cs#1)]
[!code-vb[c_DuplexServices#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_duplexservices/vb/service.vb#1)]

<span data-ttu-id="c043b-118">用戶端必須提供實作雙工合約回呼介面的類別，用於接收來自服務的訊息。</span><span class="sxs-lookup"><span data-stu-id="c043b-118">The client must provide a class that implements the callback interface of the duplex contract, for receiving messages from the service.</span></span> <span data-ttu-id="c043b-119">以下範例程式碼將示範實作 `CallbackHandler` 介面的 `ICalculatorDuplexCallback` 類別。</span><span class="sxs-lookup"><span data-stu-id="c043b-119">The following sample code shows a `CallbackHandler` class that implements the `ICalculatorDuplexCallback` interface.</span></span>

[!code-csharp[c_DuplexServices#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_duplexservices/cs/client.cs#2)]
[!code-vb[c_DuplexServices#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_duplexservices/vb/client.vb#2)]

<span data-ttu-id="c043b-120">針對雙工合約所產生的 WCF 用戶端，需要在 <xref:System.ServiceModel.InstanceContext> 結構上提供類別。</span><span class="sxs-lookup"><span data-stu-id="c043b-120">The WCF client that is generated for a duplex contract requires a <xref:System.ServiceModel.InstanceContext> class to be provided upon construction.</span></span> <span data-ttu-id="c043b-121">這個 <xref:System.ServiceModel.InstanceContext> 類別會用來做為站台，讓物件實作回呼介面並處理服務傳回的訊息。</span><span class="sxs-lookup"><span data-stu-id="c043b-121">This <xref:System.ServiceModel.InstanceContext> class is used as the site for an object that implements the callback interface and handles messages that are sent back from the service.</span></span> <span data-ttu-id="c043b-122"><xref:System.ServiceModel.InstanceContext> 類別是以 `CallbackHandler` 類別的執行個體所建構。</span><span class="sxs-lookup"><span data-stu-id="c043b-122">An <xref:System.ServiceModel.InstanceContext> class is constructed with an instance of the `CallbackHandler` class.</span></span> <span data-ttu-id="c043b-123">這個物件會處理回呼介面上，從服務傳回至用戶端的訊息。</span><span class="sxs-lookup"><span data-stu-id="c043b-123">This object handles messages sent from the service to the client on the callback interface.</span></span>

[!code-csharp[c_DuplexServices#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_duplexservices/cs/client.cs#3)]
[!code-vb[c_DuplexServices#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_duplexservices/vb/client.vb#3)]

<span data-ttu-id="c043b-124">服務的組態必須進行設定，以提供同時支援工作階段通訊和雙工通訊的繫結。</span><span class="sxs-lookup"><span data-stu-id="c043b-124">The configuration for the service must be set up to provide a binding that supports both session communication and duplex communication.</span></span> <span data-ttu-id="c043b-125">`wsDualHttpBinding` 項目支援工作階段通訊，並且藉由提供雙重 HTTP 連接 (一個方向一個連接) 允許雙工通訊。</span><span class="sxs-lookup"><span data-stu-id="c043b-125">The `wsDualHttpBinding` element supports session communication and allows duplex communication by providing dual HTTP connections, one for each direction.</span></span>

<span data-ttu-id="c043b-126">在用戶端上，您必須設定伺服器可用來連接用戶端的位址，如下面的範例組態中所示。</span><span class="sxs-lookup"><span data-stu-id="c043b-126">On the client, you must configure an address that the server can use to connect to the client, as shown in the following sample configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="c043b-127">無法使用安全對話來進行驗證的非雙工用戶端通常會擲回 <xref:System.ServiceModel.Security.MessageSecurityException>。</span><span class="sxs-lookup"><span data-stu-id="c043b-127">Non-duplex clients that fail to authenticate using a secure conversation typically throw a <xref:System.ServiceModel.Security.MessageSecurityException>.</span></span> <span data-ttu-id="c043b-128">不過，如果使用安全對話的雙工用戶端驗證失敗，則用戶端會收到 <xref:System.TimeoutException>。</span><span class="sxs-lookup"><span data-stu-id="c043b-128">However, if a duplex client that uses a secure conversation fails to authenticate, the client receives a <xref:System.TimeoutException> instead.</span></span>

<span data-ttu-id="c043b-129">如果您使用 `WSHttpBinding` 項目建立用戶端/服務，但是未包含用戶端回呼端點，則會收到以下錯誤。</span><span class="sxs-lookup"><span data-stu-id="c043b-129">If you create a client/service using the `WSHttpBinding` element and you do not include the client callback endpoint, you will receive the following error.</span></span>

```console
HTTP could not register URL
htp://+:80/Temporary_Listen_Addresses/<guid> because TCP port 80 is being used by another application.
```

<span data-ttu-id="c043b-130">下列範例程式碼說明如何以程式設計方式指定用戶端端點位址。</span><span class="sxs-lookup"><span data-stu-id="c043b-130">The following sample code shows how to specify the client endpoint address programmatically.</span></span>

```csharp
WSDualHttpBinding binding = new WSDualHttpBinding();
EndpointAddress endptadr = new EndpointAddress("http://localhost:12000/DuplexTestUsingCode/Server");
binding.ClientBaseAddress = new Uri("http://localhost:8000/DuplexTestUsingCode/Client/");
```

```vb
Dim binding As New WSDualHttpBinding()
Dim endptadr As New EndpointAddress("http://localhost:12000/DuplexTestUsingCode/Server")
binding.ClientBaseAddress = New Uri("http://localhost:8000/DuplexTestUsingCode/Client/")
```

<span data-ttu-id="c043b-131">以下範例程式碼將示範如何在組態中指定用戶端端點位址。</span><span class="sxs-lookup"><span data-stu-id="c043b-131">The following sample code shows how to specify the client endpoint address in configuration.</span></span>

```xml
<client>
    <endpoint name ="ServerEndpoint"
          address="http://localhost:12000/DuplexTestUsingConfig/Server"
          bindingConfiguration="WSDualHttpBinding_IDuplexTest"
            binding="wsDualHttpBinding"
           contract="IDuplexTest" />
</client>
<bindings>
    <wsDualHttpBinding>
        <binding name="WSDualHttpBinding_IDuplexTest"
          clientBaseAddress="http://localhost:8000/myClient/" >
            <security mode="None"/>
         </binding>
    </wsDualHttpBinding>
</bindings>
```

> [!WARNING]
> <span data-ttu-id="c043b-132">當服務或用戶端關閉其通道時，雙工模型不會自動偵測。</span><span class="sxs-lookup"><span data-stu-id="c043b-132">The duplex model doesn't automatically detect when a service or client closes its channel.</span></span> <span data-ttu-id="c043b-133">因此，如果用戶端意外終止，則預設不會通知服務，或服務意外終止時，用戶端將不會收到通知。</span><span class="sxs-lookup"><span data-stu-id="c043b-133">So if a client unexpectedly terminates, by default the service will not be notified, or if a service unexpectedly terminates, the client will not be notified.</span></span> <span data-ttu-id="c043b-134">如果您使用已中斷連線的服務，則 <xref:System.ServiceModel.CommunicationException> 會引發例外狀況。</span><span class="sxs-lookup"><span data-stu-id="c043b-134">If you use a service that is disconnected, the <xref:System.ServiceModel.CommunicationException> exception is raised.</span></span> <span data-ttu-id="c043b-135">用戶端和服務可以實作自己的通訊協定來通知彼此 (如果選擇這樣做的話)。</span><span class="sxs-lookup"><span data-stu-id="c043b-135">Clients and services can implement their own protocol to notify each other if they so choose.</span></span> <span data-ttu-id="c043b-136">如需有關錯誤處理的詳細資訊，請參閱[WCF 錯誤處理](../wcf-error-handling.md)。</span><span class="sxs-lookup"><span data-stu-id="c043b-136">For more information on error handling, see [WCF Error Handling](../wcf-error-handling.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="c043b-137">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c043b-137">See also</span></span>

- [<span data-ttu-id="c043b-138">雙工</span><span class="sxs-lookup"><span data-stu-id="c043b-138">Duplex</span></span>](../samples/duplex.md)
- [<span data-ttu-id="c043b-139">指定用端執行階段行為</span><span class="sxs-lookup"><span data-stu-id="c043b-139">Specifying Client Run-Time Behavior</span></span>](../specifying-client-run-time-behavior.md)
- [<span data-ttu-id="c043b-140">如何：建立通道處理站並使用它來建立與管理通道</span><span class="sxs-lookup"><span data-stu-id="c043b-140">How to: Create a Channel Factory and Use it to Create and Manage Channels</span></span>](how-to-create-a-channel-factory-and-use-it-to-create-and-manage-channels.md)
