---
title: 路由服務
ms.date: 03/30/2017
ms.assetid: ca7c216a-5141-4132-8193-102c181d2eba
ms.openlocfilehash: 833c824e17d70a982a2f7bb13fe388b9b2b0dec1
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84590445"
---
# <a name="routing-service"></a><span data-ttu-id="d6964-102">路由服務</span><span class="sxs-lookup"><span data-stu-id="d6964-102">Routing Service</span></span>

<span data-ttu-id="d6964-103">「路由服務」是一種泛型 SOAP 媒介，可做為訊息路由器。</span><span class="sxs-lookup"><span data-stu-id="d6964-103">The Routing Service is a generic SOAP intermediary that acts as a message router.</span></span> <span data-ttu-id="d6964-104">路由服務的核心功能是可根據訊息內容傳送訊息的能力，這可讓訊息根據訊息 (不論是標頭或訊息本文) 內部本身的值轉送至用戶端端點。</span><span class="sxs-lookup"><span data-stu-id="d6964-104">The core functionality of the Routing Service is the ability to route messages based on message content, which allows a message to be forwarded to a client endpoint based on a value within the message itself, in either the header or the message body.</span></span>

<span data-ttu-id="d6964-105"><xref:System.ServiceModel.Routing.RoutingService>會實作為命名空間中的 Windows Communication Foundation （WCF）服務 <xref:System.ServiceModel.Routing> 。</span><span class="sxs-lookup"><span data-stu-id="d6964-105">The <xref:System.ServiceModel.Routing.RoutingService> is implemented as a Windows Communication Foundation (WCF) service in the <xref:System.ServiceModel.Routing> namespace.</span></span> <span data-ttu-id="d6964-106">路由服務會公開一個或多個接收訊息的服務端點，然後將每則訊息根據訊息內容傳送至一個或多個用戶端端點。</span><span class="sxs-lookup"><span data-stu-id="d6964-106">The Routing Service exposes one or more service endpoints that receive messages and then routes each message to one or more client endpoints based on the message content.</span></span> <span data-ttu-id="d6964-107">服務提供下列功能：</span><span class="sxs-lookup"><span data-stu-id="d6964-107">The service provides the following features:</span></span>

- <span data-ttu-id="d6964-108">以內容為基礎的路由</span><span class="sxs-lookup"><span data-stu-id="d6964-108">Content-based routing</span></span>

  - <span data-ttu-id="d6964-109">服務彙總</span><span class="sxs-lookup"><span data-stu-id="d6964-109">Service aggregation</span></span>

  - <span data-ttu-id="d6964-110">服務版本控制</span><span class="sxs-lookup"><span data-stu-id="d6964-110">Service versioning</span></span>

  - <span data-ttu-id="d6964-111">優先權路由</span><span class="sxs-lookup"><span data-stu-id="d6964-111">Priority routing</span></span>

  - <span data-ttu-id="d6964-112">動態組態</span><span class="sxs-lookup"><span data-stu-id="d6964-112">Dynamic configuration</span></span>

- <span data-ttu-id="d6964-113">通訊協定橋接</span><span class="sxs-lookup"><span data-stu-id="d6964-113">Protocol bridging</span></span>

- <span data-ttu-id="d6964-114">SOAP 處理</span><span class="sxs-lookup"><span data-stu-id="d6964-114">SOAP processing</span></span>

- <span data-ttu-id="d6964-115">進階的錯誤處理</span><span class="sxs-lookup"><span data-stu-id="d6964-115">Advanced error handling</span></span>

- <span data-ttu-id="d6964-116">備份端點</span><span class="sxs-lookup"><span data-stu-id="d6964-116">Backup endpoints</span></span>

<span data-ttu-id="d6964-117">雖然您可以建立媒介服務來完成一或多項上述目標，但是這類實作經常與特定案例或方案關係密切，而且無法輕易套用至新應用程式。</span><span class="sxs-lookup"><span data-stu-id="d6964-117">While it is possible to create an intermediary service that accomplishes one or more of these goals, often such an implementation is tied to a specific scenario or solution and cannot be readily applied to new applications.</span></span>

<span data-ttu-id="d6964-118">路由服務提供泛型、可動態設定、插入的 SOAP 媒介，與 WCF 服務和通道模型相容，並可讓您執行以內容為基礎的 SOAP 訊息路由。</span><span class="sxs-lookup"><span data-stu-id="d6964-118">The Routing Service provides a generic, dynamically configurable, pluggable SOAP intermediary that is compatible with the WCF Service and Channel models and allows you to perform content-based routing of SOAP-based messages.</span></span>

> [!NOTE]
> <span data-ttu-id="d6964-119">路由服務目前不支援 WCF REST 服務的路由。</span><span class="sxs-lookup"><span data-stu-id="d6964-119">The Routing Service does not currently support routing of WCF REST services.</span></span>  <span data-ttu-id="d6964-120">若要路由傳送 REST 呼叫，請考慮使用 <xref:System.Web.Routing> 或[應用程式要求路由](https://go.microsoft.com/fwlink/?LinkId=164589)。</span><span class="sxs-lookup"><span data-stu-id="d6964-120">To route REST calls, consider using <xref:System.Web.Routing> or [Application Request Routing](https://go.microsoft.com/fwlink/?LinkId=164589).</span></span>

## <a name="content-based-routing"></a><span data-ttu-id="d6964-121">內容架構路由</span><span class="sxs-lookup"><span data-stu-id="d6964-121">Content-Based Routing</span></span>

<span data-ttu-id="d6964-122">內容架構路由是根據訊息內包含的一個或多個值路由傳送訊息的能力。</span><span class="sxs-lookup"><span data-stu-id="d6964-122">Content-based routing is the ability to route a message based on one or more values contained within the message.</span></span> <span data-ttu-id="d6964-123">路由服務會檢查每一個訊息，並且根據訊息內容和您建立的路由邏輯，將訊息路由傳送至目的端點。</span><span class="sxs-lookup"><span data-stu-id="d6964-123">The Routing Service inspects each message and routes it to the destination endpoint based on the message contents and the routing logic you create.</span></span> <span data-ttu-id="d6964-124">以內容為基礎的路由會提供服務彙總、服務版本控制和優先權路由的基礎。</span><span class="sxs-lookup"><span data-stu-id="d6964-124">Content-based routing provides the basis for service aggregation, service versioning, and priority routing.</span></span>

<span data-ttu-id="d6964-125">為了實作以內容為基礎的路由，路由服務需依靠 <xref:System.ServiceModel.Dispatcher.MessageFilter> 實作，該實作是用來比對要傳送之訊息內的特定值。</span><span class="sxs-lookup"><span data-stu-id="d6964-125">To implement content-based routing, the Routing Service relies on <xref:System.ServiceModel.Dispatcher.MessageFilter> implementations that are used to match specific values within the messages to be routed.</span></span> <span data-ttu-id="d6964-126">如果**MessageFilter**符合訊息，則訊息會路由傳送至與**MessageFilter**相關聯的目的地端點。</span><span class="sxs-lookup"><span data-stu-id="d6964-126">If a **MessageFilter** matches a message, the message is routed to the destination endpoint associated with the **MessageFilter**.</span></span>  <span data-ttu-id="d6964-127">訊息篩選會群組至篩選資料表中 (<xref:System.ServiceModel.Routing.Configuration.FilterTableCollection>) 以建構複雜路由邏輯。</span><span class="sxs-lookup"><span data-stu-id="d6964-127">Message filters are grouped together into filter tables (<xref:System.ServiceModel.Routing.Configuration.FilterTableCollection>) to construct complex routing logic.</span></span> <span data-ttu-id="d6964-128">例如，篩選資料表可能包含五個相互為獨佔的訊息篩選條件，這些篩選條件會導致訊息僅傳送至五個目的地端點的其中之一。</span><span class="sxs-lookup"><span data-stu-id="d6964-128">For example, a filter table might contain five mutually exclusive message filters that cause messages to be routed to only one of the five destination endpoints.</span></span>

<span data-ttu-id="d6964-129">路由服務可讓您設定用來執行以內容為基礎之路由的邏輯，以及在執行階段動態更新路由邏輯。</span><span class="sxs-lookup"><span data-stu-id="d6964-129">The Routing Service allows you to configure the logic that is used to perform content-based routing, as well as dynamically update the routing logic at run time.</span></span>

<span data-ttu-id="d6964-130">將訊息篩選條件群組為篩選資料表，可建構路由邏輯，讓您處理多個路由案例，例如：</span><span class="sxs-lookup"><span data-stu-id="d6964-130">Through the grouping of message filters into filter tables, routing logic can be constructed that allows you to handle multiple routing scenarios such as:</span></span>

- <span data-ttu-id="d6964-131">服務彙總</span><span class="sxs-lookup"><span data-stu-id="d6964-131">Service aggregation</span></span>

- <span data-ttu-id="d6964-132">服務版本控制</span><span class="sxs-lookup"><span data-stu-id="d6964-132">Service versioning</span></span>

- <span data-ttu-id="d6964-133">優先權路由</span><span class="sxs-lookup"><span data-stu-id="d6964-133">Priority routing</span></span>

- <span data-ttu-id="d6964-134">動態組態</span><span class="sxs-lookup"><span data-stu-id="d6964-134">Dynamic configuration</span></span>

<span data-ttu-id="d6964-135">如需訊息篩選和篩選資料表的詳細資訊，請參閱[路由簡介](routing-introduction.md)和[訊息篩選](message-filters.md)。</span><span class="sxs-lookup"><span data-stu-id="d6964-135">For more information about message filters and filter tables, see [Routing Introduction](routing-introduction.md) and [Message Filters](message-filters.md).</span></span>

### <a name="service-aggregation"></a><span data-ttu-id="d6964-136">服務彙總</span><span class="sxs-lookup"><span data-stu-id="d6964-136">Service Aggregation</span></span>

<span data-ttu-id="d6964-137">透過使用以內容為基礎的路由，您就可以公開從外部用戶端應用程式接收訊息的端點，然後根據訊息內的值，將每個訊息路由傳送至適當的內容端點。</span><span class="sxs-lookup"><span data-stu-id="d6964-137">By using content-based routing, you can expose one endpoint that receives messages from external client applications and then routes each message to the appropriate internal endpoint based on a value within the message.</span></span> <span data-ttu-id="d6964-138">這項益處相當實用，可提供一個特定端點給各種不同的後端應用程式，以及對客戶呈現一個應用程式端點，同時將應用程式重構至各種不同服務。</span><span class="sxs-lookup"><span data-stu-id="d6964-138">This is useful to offer one specific endpoint for a variety of back-end applications, and also to present one application endpoint to customers while factoring your application into a variety of services.</span></span>

### <a name="service-versioning"></a><span data-ttu-id="d6964-139">服務版本控制</span><span class="sxs-lookup"><span data-stu-id="d6964-139">Service Versioning</span></span>

<span data-ttu-id="d6964-140">當您轉換新版方案時，可能需要保留舊版，以便同時對現有客戶提供服務。</span><span class="sxs-lookup"><span data-stu-id="d6964-140">When migrating to a new version of your solution, you may have to maintain the old version in parallel to serve existing customers.</span></span> <span data-ttu-id="d6964-141">在這種情況下，經常會要求連接至較新版本的用戶端與方案進行通訊時，必須使用不同的位址。</span><span class="sxs-lookup"><span data-stu-id="d6964-141">Often this requires that clients connecting to the newer version must use a different address when communicating with the solution.</span></span> <span data-ttu-id="d6964-142">路由服務可讓您根據訊息中包含的版本專屬資訊，將訊息路由傳送至適當的方案，藉此公開一個同時對兩個方案版本提供服務的服務端點。</span><span class="sxs-lookup"><span data-stu-id="d6964-142">The Routing Service allows you to expose one service endpoint that serves both versions of your solution by routing messages to the appropriate solution based on version-specific information contained in the message.</span></span> <span data-ttu-id="d6964-143">如需這類實現的範例，請參閱[如何：服務版本](how-to-service-versioning.md)設定。</span><span class="sxs-lookup"><span data-stu-id="d6964-143">For an example of such an implementation see [How To: Service Versioning](how-to-service-versioning.md).</span></span>

### <a name="priority-routing"></a><span data-ttu-id="d6964-144">優先權路由</span><span class="sxs-lookup"><span data-stu-id="d6964-144">Priority Routing</span></span>

<span data-ttu-id="d6964-145">為多個用戶端提供服務時，您可能與某些夥伴有服務等級協定 (SLA)，該協定會要求來自這些夥伴的所有資料與其他用戶端的資料分開處理。</span><span class="sxs-lookup"><span data-stu-id="d6964-145">When providing a service for multiple clients, you may have a service level agreement (SLA) with some partners that requires all data from these partners to be processed separately from that of other clients.</span></span> <span data-ttu-id="d6964-146">透過使用尋找訊息內所包含客戶專屬資訊的篩選，您就可以輕鬆將特定夥伴的訊息路由傳送至專為符合其 SLA 需求所建立的端點。</span><span class="sxs-lookup"><span data-stu-id="d6964-146">By using a filter that looks for customer-specific information contained in the message, you can easily route messages from specific partners to an endpoint that has been created to meet their SLA requirements.</span></span>

## <a name="dynamic-configuration"></a><span data-ttu-id="d6964-147">動態組態</span><span class="sxs-lookup"><span data-stu-id="d6964-147">Dynamic Configuration</span></span>

<span data-ttu-id="d6964-148">為了支援重要的運作系統，訊息的處理過程不能有任何服務中斷，因此您必須能在執行階段於系統內修改元件組態。</span><span class="sxs-lookup"><span data-stu-id="d6964-148">To support mission-critical systems, where messages must be processed without any service interruptions, it is vital that you be able to modify the configuration of components within the system at run time.</span></span> <span data-ttu-id="d6964-149">為了支援這項需求，路由服務提供 <xref:System.ServiceModel.IExtension%601> 實作，也就是 <xref:System.ServiceModel.Routing.RoutingExtension>，可讓路由服務組態在執行階段進行動態更新。</span><span class="sxs-lookup"><span data-stu-id="d6964-149">To support this need, the Routing Service provides an <xref:System.ServiceModel.IExtension%601> implementation, the <xref:System.ServiceModel.Routing.RoutingExtension>, which allows dynamic updating of the Routing Service configuration at run time.</span></span>

<span data-ttu-id="d6964-150">如需有關路由服務動態設定的詳細資訊，請參閱[路由簡介](routing-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="d6964-150">For more information about dynamic configuration of the Routing Service, see [Routing Introduction](routing-introduction.md).</span></span>

## <a name="protocol-bridging"></a><span data-ttu-id="d6964-151">通訊協定橋接</span><span class="sxs-lookup"><span data-stu-id="d6964-151">Protocol Bridging</span></span>

<span data-ttu-id="d6964-152">媒介案例的其中一項挑戰，就是內部端點的傳輸或 SOAP 版本需求可能與接收訊息所在的端點不同。</span><span class="sxs-lookup"><span data-stu-id="d6964-152">One of the challenges in intermediary scenarios is that the internal endpoints may have different transport or SOAP version requirements than the endpoint that messages are received on.</span></span> <span data-ttu-id="d6964-153">為了支援此案例，路由服務可以橋接通訊協定，包括將 SOAP 訊息處理至目的端點所需的 <xref:System.ServiceModel.Channels.MessageVersion>。</span><span class="sxs-lookup"><span data-stu-id="d6964-153">To support this scenario, the Routing Service can bridge protocols, including processing the SOAP message to the <xref:System.ServiceModel.Channels.MessageVersion> required by the destination endpoint(s).</span></span> <span data-ttu-id="d6964-154">透過這種方式，就可以將一個通訊協定用於內部通訊，同時將另一個通訊協定用於外部通訊。</span><span class="sxs-lookup"><span data-stu-id="d6964-154">In this way, one protocol can be used for internal communication, while another can be used for external communication.</span></span>

<span data-ttu-id="d6964-155">為了支援端點間使用不同傳輸的訊息傳送，路由服務會使用系統提供的繫結，讓服務能夠橋接不同的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="d6964-155">To support the routing of messages between endpoints with different transports, the Routing Service uses system-provided bindings that enable the service to bridge dissimilar protocols.</span></span> <span data-ttu-id="d6964-156">當路由服務所公開的服務端點，使用與用戶端端點 (訊息傳送的位置) 不同的通訊協定時，此情形便會自動發生。</span><span class="sxs-lookup"><span data-stu-id="d6964-156">This occurs automatically when the service endpoint exposed by the Routing Service uses a different protocol than the client endpoints that messages are routed to.</span></span>

## <a name="soap-processing"></a><span data-ttu-id="d6964-157">SOAP 處理</span><span class="sxs-lookup"><span data-stu-id="d6964-157">SOAP Processing</span></span>

<span data-ttu-id="d6964-158">使用不同 SOAP 需求在端點間路由訊息是一項常見的傳送需求。</span><span class="sxs-lookup"><span data-stu-id="d6964-158">A common routing requirement is the ability to route messages between endpoints with differing SOAP requirements.</span></span> <span data-ttu-id="d6964-159">為了支援這項需求，路由服務會提供 <xref:System.ServiceModel.Routing.SoapProcessingBehavior> ，它會自動建立新的**MessageVersion** ，以符合目的地端點的需求，然後才將訊息路由傳送給它。</span><span class="sxs-lookup"><span data-stu-id="d6964-159">To support this requirement, the Routing Service provides a <xref:System.ServiceModel.Routing.SoapProcessingBehavior> that automatically creates a new **MessageVersion** that meets the requirements of the destination endpoint before the message is routed to it.</span></span> <span data-ttu-id="d6964-160">此行為也會在將回應訊息傳回給要求的用戶端應用程式之前，為該訊息建立新的**MessageVersion** ，以確保回應的 MessageVersion 符合原始要求的**MessageVersion** 。</span><span class="sxs-lookup"><span data-stu-id="d6964-160">This behavior also creates a new **MessageVersion** for any response message before returning it to the requesting client application, to ensure that the **MessageVersion** of the response matches that of the original request.</span></span>

<span data-ttu-id="d6964-161">如需 SOAP 處理的詳細資訊，請參閱[路由簡介](routing-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="d6964-161">For more information about SOAP processing, see [Routing Introduction](routing-introduction.md).</span></span>

## <a name="error-handling"></a><span data-ttu-id="d6964-162">錯誤處理</span><span class="sxs-lookup"><span data-stu-id="d6964-162">Error Handling</span></span>

<span data-ttu-id="d6964-163">在由依賴網路通訊之分散式服務所組成的系統中，確定系統內部通訊不會發生暫時性網路故障是相當重要的。</span><span class="sxs-lookup"><span data-stu-id="d6964-163">In a system composed of distributed services that rely on network communications, it is important to ensure that communications within your system are resistant to transient network failures.</span></span>  <span data-ttu-id="d6964-164">路由服務會實作錯誤處理，讓您能夠處理許多可能會導致服務中斷的通訊故障案例。</span><span class="sxs-lookup"><span data-stu-id="d6964-164">The Routing Service implements error handling that allows you to handle many communication failure scenarios that might otherwise result in a service outage.</span></span>

<span data-ttu-id="d6964-165">如果路由服務在嘗試傳送訊息時發生 <xref:System.ServiceModel.CommunicationException> 情況，錯誤處理便會開始。</span><span class="sxs-lookup"><span data-stu-id="d6964-165">If the Routing Service encounters a <xref:System.ServiceModel.CommunicationException> while attempting to send a message, error handling will take place.</span></span>  <span data-ttu-id="d6964-166">這些例外狀況通常表示，嘗試與定義的用戶端端點 (如 <xref:System.ServiceModel.EndpointNotFoundException>、<xref:System.ServiceModel.ServerTooBusyException> 或 <xref:System.ServiceModel.CommunicationObjectFaultedException>) 進行通訊時發生問題。</span><span class="sxs-lookup"><span data-stu-id="d6964-166">These exceptions typically indicate that a problem was encountered while attempting to communicate with the defined client endpoint, such as an <xref:System.ServiceModel.EndpointNotFoundException>, <xref:System.ServiceModel.ServerTooBusyException>, or <xref:System.ServiceModel.CommunicationObjectFaultedException>.</span></span>  <span data-ttu-id="d6964-167">錯誤處理常式代碼也會在**TimeoutException**發生時攔截並嘗試重試傳送，這是另一個不是衍生自**CommunicationException**的常見例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d6964-167">The error-handling code will also catch and attempt to retry sending when a **TimeoutException** occurs, which is another common exception that is not derived from **CommunicationException**.</span></span>

<span data-ttu-id="d6964-168">如需有關錯誤處理的詳細資訊，請參閱[路由簡介](routing-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="d6964-168">For more information about error handling, see [Routing Introduction](routing-introduction.md).</span></span>

## <a name="backup-endpoints"></a><span data-ttu-id="d6964-169">備份端點</span><span class="sxs-lookup"><span data-stu-id="d6964-169">Backup Endpoints</span></span>

<span data-ttu-id="d6964-170">除了篩選資料表中與每個篩選定義關聯的目的地用戶端端點之外，您也可以建立備份端點清單，在傳輸失敗時傳送訊息至該端點。</span><span class="sxs-lookup"><span data-stu-id="d6964-170">In addition to the destination client endpoints associated with each filter definition in the filter table, you can also create a list of backup endpoints that the message will be routed to in the event of a transmission failure.</span></span> <span data-ttu-id="d6964-171">如果錯誤發生且備份清單是用於篩選項目，路由服務便會嘗試將訊息傳送至已在清單中定義的第一個端點。</span><span class="sxs-lookup"><span data-stu-id="d6964-171">If an error occurs and a backup list is defined for the filter entry, the Routing Service will attempt to send the message to the first endpoint defined in the list.</span></span> <span data-ttu-id="d6964-172">如果此次傳輸失敗，服務會嘗試下一個端點並繼續此程序，直到傳輸成功、傳回非傳輸相關的錯誤，或備份清單中的所有端點已傳回傳輸錯誤。</span><span class="sxs-lookup"><span data-stu-id="d6964-172">If this transmission attempt fails, the service will try the next endpoint, and continue this process until the transmission attempt succeeds, returns a non-transmission related error, or all endpoints in the backup list have returned a transmission error.</span></span>

<span data-ttu-id="d6964-173">如需備份端點的詳細資訊，請參閱[路由簡介](routing-introduction.md)和[訊息篩選](message-filters.md)。</span><span class="sxs-lookup"><span data-stu-id="d6964-173">For more information about backup endpoints, see [Routing Introduction](routing-introduction.md) and [Message Filters](message-filters.md).</span></span>

## <a name="streaming"></a><span data-ttu-id="d6964-174">串流</span><span class="sxs-lookup"><span data-stu-id="d6964-174">Streaming</span></span>

<span data-ttu-id="d6964-175">如果您將繫結設定為支援資料流，路由服務就可以成功地串流處理訊息。</span><span class="sxs-lookup"><span data-stu-id="d6964-175">The routing service can successfully stream messages if you set the binding to support streaming.</span></span>  <span data-ttu-id="d6964-176">不過，在某些情況下，您可能必須緩衝處理訊息：</span><span class="sxs-lookup"><span data-stu-id="d6964-176">However, there are some conditions under which messages may need to buffered:</span></span>

- <span data-ttu-id="d6964-177">多點傳送 (緩衝處理以建立其他訊息複本)</span><span class="sxs-lookup"><span data-stu-id="d6964-177">Multicast (buffer to create additional message copies)</span></span>

- <span data-ttu-id="d6964-178">容錯移轉 (如果訊息必須傳送至備份，則緩衝處理)</span><span class="sxs-lookup"><span data-stu-id="d6964-178">Failover (buffer in case the message needs to be sent to a backup)</span></span>

- <span data-ttu-id="d6964-179">System.ServiceModel.Routing.RoutingConfiguration.RouteOnHeadersOnly 為 false (緩衝處理以呈現含有 MessageBuffer 的 MessageFilterTable，讓篩選能夠檢查本文)</span><span class="sxs-lookup"><span data-stu-id="d6964-179">System.ServiceModel.Routing.RoutingConfiguration.RouteOnHeadersOnly is false (buffer to present the MessageFilterTable with a MessageBuffer so that filters can inspect the body)</span></span>

- <span data-ttu-id="d6964-180">動態組態</span><span class="sxs-lookup"><span data-stu-id="d6964-180">Dynamic configuration</span></span>

## <a name="see-also"></a><span data-ttu-id="d6964-181">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d6964-181">See also</span></span>

- [<span data-ttu-id="d6964-182">路由簡介</span><span class="sxs-lookup"><span data-stu-id="d6964-182">Routing Introduction</span></span>](routing-introduction.md)
- [<span data-ttu-id="d6964-183">路由合約</span><span class="sxs-lookup"><span data-stu-id="d6964-183">Routing Contracts</span></span>](routing-contracts.md)
- [<span data-ttu-id="d6964-184">訊息篩選</span><span class="sxs-lookup"><span data-stu-id="d6964-184">Message Filters</span></span>](message-filters.md)
