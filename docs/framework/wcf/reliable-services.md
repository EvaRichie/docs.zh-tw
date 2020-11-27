---
title: 可靠的服務
ms.date: 03/30/2017
helpviewer_keywords:
- WCF [WCF], reliable messaging
- Windows Communication Foundation [WCF], reliable messaging
- WCF [WCF], reliable sessions
- Windows Communication Foundation [WCF], reliable sessions
- service contracts [WCF], reliable services
ms.assetid: 07814ed0-0775-47f2-987b-d8134fdd5099
ms.openlocfilehash: d028af80a30fd18b6aa6e9678e7fd8788e7b7b95
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96249744"
---
# <a name="reliable-services"></a><span data-ttu-id="eded2-102">可靠的服務</span><span class="sxs-lookup"><span data-stu-id="eded2-102">Reliable Services</span></span>

<span data-ttu-id="eded2-103">佇列和可靠會話是執行可靠訊息的 WCF) 功能 Windows Communication Foundation (。</span><span class="sxs-lookup"><span data-stu-id="eded2-103">Queues and reliable sessions are the Windows Communication Foundation (WCF) features that implement reliable messaging.</span></span> <span data-ttu-id="eded2-104">本主題說明 WCF 的可靠訊息功能。</span><span class="sxs-lookup"><span data-stu-id="eded2-104">This topic explains the reliable messaging features of WCF.</span></span>  
  
 <span data-ttu-id="eded2-105">*可靠的訊息處理* 是可靠的訊息來源 (呼叫 *來源*) 如何可靠地將訊息傳送到可靠的訊息目的地， (稱為 *目的地*) 。</span><span class="sxs-lookup"><span data-stu-id="eded2-105">*Reliable messaging* is how a reliable messaging source (called the *source*) transfers messages reliably to a reliable messaging destination (called the *destination*).</span></span>  
  
 <span data-ttu-id="eded2-106">可信賴傳訊可執行下列功能：</span><span class="sxs-lookup"><span data-stu-id="eded2-106">Reliable messaging performs the following functions:</span></span>  
  
- <span data-ttu-id="eded2-107">傳輸保證，保證無論是訊息傳輸或傳輸失敗，訊息都會從來源傳輸到目的地。</span><span class="sxs-lookup"><span data-stu-id="eded2-107">Transfers assurances for messages sent from a source to a destination regardless of message transfer or transport failures.</span></span>  
  
- <span data-ttu-id="eded2-108">區隔來源和目的地。</span><span class="sxs-lookup"><span data-stu-id="eded2-108">Separates the source and the destination from each other.</span></span> <span data-ttu-id="eded2-109">這樣可以讓來源和目的地所發生的失敗與復原不具相關性，並且提供可靠的訊息傳輸和傳遞，即使在來源或目的地無法使用的情況下也是如此。</span><span class="sxs-lookup"><span data-stu-id="eded2-109">This provides independent failure and recovery of the source and the destination, as well as reliable transfer and delivery of messages, even when the source or destination is unavailable.</span></span>  
  
 <span data-ttu-id="eded2-110">可信賴傳訊通常會伴隨長延遲時間的發生。</span><span class="sxs-lookup"><span data-stu-id="eded2-110">Reliable messaging frequently comes at the cost of high latency.</span></span> <span data-ttu-id="eded2-111">*延遲* 是指訊息到達來源的目的地所需的時間。</span><span class="sxs-lookup"><span data-stu-id="eded2-111">*Latency* is the time it takes for the message to reach the destination from the source.</span></span> <span data-ttu-id="eded2-112">因此，WCF 提供下列類型的可靠訊息：</span><span class="sxs-lookup"><span data-stu-id="eded2-112">WCF, therefore, provides the following types of reliable messaging:</span></span>  
  
- <span data-ttu-id="eded2-113">[可靠的會話](./feature-details/reliable-sessions.md)，可提供可靠的傳輸，而不會產生高延遲的成本。</span><span class="sxs-lookup"><span data-stu-id="eded2-113">[Reliable Sessions](./feature-details/reliable-sessions.md), which offers reliable transfer without the cost of high latency.</span></span>  
  
- <span data-ttu-id="eded2-114">[WCF 中的佇列](./feature-details/queues-in-wcf.md)，可在來源與目的地之間提供可靠的傳輸和分隔。</span><span class="sxs-lookup"><span data-stu-id="eded2-114">[Queues in WCF](./feature-details/queues-in-wcf.md), which offers both reliable transfers and separation between the source and the destination.</span></span>  
  
## <a name="reliable-sessions"></a><span data-ttu-id="eded2-115">可靠工作階段</span><span class="sxs-lookup"><span data-stu-id="eded2-115">Reliable Sessions</span></span>  

 <span data-ttu-id="eded2-116">可靠工作階段使用 WS-Reliable Messaging 通訊協定提供來源和目的地之間的端對端可靠訊息傳輸，而不論個別傳訊端點 (來源和目的地) 之間媒介的類型或數目為何。</span><span class="sxs-lookup"><span data-stu-id="eded2-116">Reliable sessions provide end-to-end reliable transfer of messages between a source and a destination using the WS-Reliable Messaging protocol, regardless of the number or type of intermediaries that separate the messaging (source and destination) endpoints.</span></span> <span data-ttu-id="eded2-117">這包括不是使用 SOAP 的任何傳輸媒介 (例如，HTTP Proxy) 或使用 SOAP 的媒介 (例如，SOAP 架構的路由器或橋接器)，而訊息在端點之間流動時需要這些媒介。</span><span class="sxs-lookup"><span data-stu-id="eded2-117">This includes any transport intermediaries that do not use SOAP (for example, HTTP proxies) or intermediaries that use SOAP (for example, SOAP-based routers or bridges) that are required for messages to flow between the endpoints.</span></span> <span data-ttu-id="eded2-118">可靠工作階段會使用記憶體中傳輸視窗來遮罩 SOAP 訊息層級的失敗，並在發生傳輸失敗時重新建立連線。</span><span class="sxs-lookup"><span data-stu-id="eded2-118">Reliable sessions use an in-memory transfer window to mask SOAP message-level failures and re-establish connections in the case of transport failures.</span></span>  
  
 <span data-ttu-id="eded2-119">可靠工作階段會提供短延遲時間的可信賴訊息傳輸。</span><span class="sxs-lookup"><span data-stu-id="eded2-119">Reliable sessions provide low-latency reliable message transfers.</span></span> <span data-ttu-id="eded2-120">它們可透過任何的 Proxy 或媒介提供 SOAP 訊息，而這相當於 TCP 透過 IP 橋接器為封包提供的內容。</span><span class="sxs-lookup"><span data-stu-id="eded2-120">They provide for SOAP messages over any proxies or intermediaries, equivalent to what TCP provides for packets over IP bridges.</span></span> <span data-ttu-id="eded2-121">如需可靠會話的詳細資訊，請參閱 [可靠會話](./feature-details/reliable-sessions.md)。</span><span class="sxs-lookup"><span data-stu-id="eded2-121">For more information about reliable sessions, see [Reliable Sessions](./feature-details/reliable-sessions.md).</span></span>  
  
### <a name="queues"></a><span data-ttu-id="eded2-122">佇列</span><span class="sxs-lookup"><span data-stu-id="eded2-122">Queues</span></span>  

 <span data-ttu-id="eded2-123">WCF 中的佇列提供可靠的訊息傳輸，並以高延遲的成本在來源與目的地之間分開。</span><span class="sxs-lookup"><span data-stu-id="eded2-123">Queues in WCF provide both reliable transfers of messages and separation between sources and destinations at the cost of high latency.</span></span> <span data-ttu-id="eded2-124">WCF 佇列通訊是以訊息佇列 (MSMQ) 為基礎。</span><span class="sxs-lookup"><span data-stu-id="eded2-124">WCF queued communication is built on top of Message Queuing (MSMQ).</span></span>  
  
 <span data-ttu-id="eded2-125">MSMQ 是 Windows 所附的選用元件。</span><span class="sxs-lookup"><span data-stu-id="eded2-125">MSMQ ships as an optional component with Windows.</span></span> <span data-ttu-id="eded2-126">MSMQ 服務會執行為 Windows 服務。</span><span class="sxs-lookup"><span data-stu-id="eded2-126">The MSMQ service runs as a Windows Service.</span></span> <span data-ttu-id="eded2-127">它會代表來源擷取傳輸佇列中要進行傳輸的訊息，並將該訊息傳遞至目標佇列。</span><span class="sxs-lookup"><span data-stu-id="eded2-127">It captures messages for transmission in a transmission queue on behalf of the source and delivers it to a target queue.</span></span> <span data-ttu-id="eded2-128">目標佇列會代表目的地接受訊息，以便隨時因應目的地要求訊息而進行傳遞。</span><span class="sxs-lookup"><span data-stu-id="eded2-128">The target queue accepts messages on behalf of the destination for later delivery whenever the destination requests messages.</span></span> <span data-ttu-id="eded2-129">MSMQ 管理員會實作可信賴傳訊通訊協定，這樣訊息就不會在傳輸期間遺失。</span><span class="sxs-lookup"><span data-stu-id="eded2-129">The MSMQ managers implement a reliable message-transfer protocol so that messages are not lost in transmission.</span></span> <span data-ttu-id="eded2-130">此通訊協定可以是原生 (Native)，或是稱為 SOAP Reliable Messaging Protocol (SRMP) 的 SOAP 架構通訊協定。</span><span class="sxs-lookup"><span data-stu-id="eded2-130">The protocol can be native or a SOAP-based protocol called SOAP Reliable Messaging Protocol (SRMP).</span></span>  
  
 <span data-ttu-id="eded2-131">佇列之間的區隔性以及可信賴傳訊，可讓鬆散耦合的應用程式進行可靠的通訊。</span><span class="sxs-lookup"><span data-stu-id="eded2-131">The separation, coupled with reliable message transfers between queues, enables applications that are loosely coupled to communicate reliably.</span></span> <span data-ttu-id="eded2-132">與可靠工作階段不同的是，來源和目的地不需要同時執行。</span><span class="sxs-lookup"><span data-stu-id="eded2-132">Unlike reliable sessions, the source and destination do not have to be running at the same time.</span></span> <span data-ttu-id="eded2-133">這個特點促使當來源的訊息生產率與目的地的訊息消耗率不相同時，作用中的佇列會被用來當做負載撫平機制。</span><span class="sxs-lookup"><span data-stu-id="eded2-133">This implicitly enables scenarios where queues are, in effect, used as a load-leveling mechanism when the source's rate of message production and the destination's rate of the message consumption do not match.</span></span> <span data-ttu-id="eded2-134">如需佇列的詳細資訊，請參閱 [WCF 中的佇列](./feature-details/queues-in-wcf.md)。</span><span class="sxs-lookup"><span data-stu-id="eded2-134">For more information about queues, see [Queues in WCF](./feature-details/queues-in-wcf.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="eded2-135">另請參閱</span><span class="sxs-lookup"><span data-stu-id="eded2-135">See also</span></span>

- [<span data-ttu-id="eded2-136">可靠的工作階段概觀</span><span class="sxs-lookup"><span data-stu-id="eded2-136">Reliable Sessions Overview</span></span>](./feature-details/reliable-sessions-overview.md)
- [<span data-ttu-id="eded2-137">WCF 中的佇列</span><span class="sxs-lookup"><span data-stu-id="eded2-137">Queuing in WCF</span></span>](./feature-details/queuing-in-wcf.md)
