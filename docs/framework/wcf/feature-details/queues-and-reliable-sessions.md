---
title: 佇列和可靠的工作階段
ms.date: 03/30/2017
ms.assetid: 7e794d03-141c-45ed-b6b1-6c0e104c1464
ms.openlocfilehash: db47838db1608dac4e0fe22252795b6dd33a0b6e
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96244687"
---
# <a name="queues-and-reliable-sessions"></a><span data-ttu-id="9f4d8-102">佇列和可靠的工作階段</span><span class="sxs-lookup"><span data-stu-id="9f4d8-102">Queues and Reliable Sessions</span></span>

<span data-ttu-id="9f4d8-103">佇列和可靠會話是執行可靠訊息的 WCF) 功能 Windows Communication Foundation (。</span><span class="sxs-lookup"><span data-stu-id="9f4d8-103">Queues and reliable sessions are the Windows Communication Foundation (WCF) features that implement reliable messaging.</span></span> <span data-ttu-id="9f4d8-104">本章節包含的主題會討論 WCF 可靠訊息功能。</span><span class="sxs-lookup"><span data-stu-id="9f4d8-104">The topics contained in this section discuss the WCF reliable messaging features.</span></span>  
  
 <span data-ttu-id="9f4d8-105">「可信賴傳訊」為可信賴傳訊來源 (稱為來源) 將訊息可靠地傳輸到可信賴傳訊目的地 (稱為目的地) 的方式。</span><span class="sxs-lookup"><span data-stu-id="9f4d8-105">Reliable messaging is how a reliable messaging source (called the source) transfers messages reliably to a reliable messaging destination (called the destination).</span></span>  
  
 <span data-ttu-id="9f4d8-106">可信賴傳訊具有下列重要功能：</span><span class="sxs-lookup"><span data-stu-id="9f4d8-106">Reliable messaging has the following key aspects:</span></span>  
  
- <span data-ttu-id="9f4d8-107">傳輸保證，保證無論是訊息傳輸 (Transfer) 失敗或傳輸 (Transport) 失敗，訊息都會從來源傳送到目的地。</span><span class="sxs-lookup"><span data-stu-id="9f4d8-107">Transfer assurances for messages sent from a source to a destination regardless of message transfer failure or transport failures.</span></span>  
  
- <span data-ttu-id="9f4d8-108">將來源和目的地彼此分開，如此可對來源與目的地提供獨立的失敗與復原作業，以及可靠訊息傳輸與傳遞，就算來源或目的地無法使用也是一樣。</span><span class="sxs-lookup"><span data-stu-id="9f4d8-108">Separation of the source and the destination from each other, which provides independent failure and recovery of the source and the destination as well as reliable transfer and delivery of messages even though the source or destination is unavailable.</span></span>  
  
 <span data-ttu-id="9f4d8-109">可信賴傳訊通常會伴隨長延遲時間的發生。</span><span class="sxs-lookup"><span data-stu-id="9f4d8-109">Reliable messaging frequently comes at the cost of high latency.</span></span> <span data-ttu-id="9f4d8-110">「延遲時間」為訊息從來源到達目的地所需要的時間。</span><span class="sxs-lookup"><span data-stu-id="9f4d8-110">Latency is the time it takes for the message to reach the destination from the source.</span></span> <span data-ttu-id="9f4d8-111">因此，WCF 提供下列類型的可靠訊息：</span><span class="sxs-lookup"><span data-stu-id="9f4d8-111">WCF, therefore, provides the following types of reliable messaging:</span></span>  
  
- <span data-ttu-id="9f4d8-112">[可靠的會話](reliable-sessions.md)，提供可靠的傳輸而不需要高延遲的成本</span><span class="sxs-lookup"><span data-stu-id="9f4d8-112">[Reliable Sessions](reliable-sessions.md), which offer reliable transfer without the cost of high latency</span></span>  
  
- <span data-ttu-id="9f4d8-113">[WCF 中的佇列](queues-in-wcf.md)，可在來源與目的地之間提供可靠的傳輸和分隔。</span><span class="sxs-lookup"><span data-stu-id="9f4d8-113">[Queues in WCF](queues-in-wcf.md), which offer both reliable transfers and separation between the source and the destination.</span></span>  
  
## <a name="reliable-sessions"></a><span data-ttu-id="9f4d8-114">可靠工作階段</span><span class="sxs-lookup"><span data-stu-id="9f4d8-114">Reliable Sessions</span></span>  

 <span data-ttu-id="9f4d8-115">可靠工作階段使用 WS-ReliableMessaging 通訊協定提供來源和目的地之間的端對端可靠訊息傳輸，而不論傳訊端點 (來源和目的地) 之間媒介的類型或數目為何。</span><span class="sxs-lookup"><span data-stu-id="9f4d8-115">Reliable sessions provide end-to-end reliable transfer of messages between a source and a destination using the WS-ReliableMessaging protocol regardless of the number or type of intermediaries that separate the messaging (source and destination) endpoints.</span></span> <span data-ttu-id="9f4d8-116">這包括不是使用 SOAP 的任何傳輸媒介 (例如，HTTP Proxy) 或使用 SOAP 的媒介 (例如，SOAP 架構的路由器或橋接器)，而訊息在端點之間流動時需要這些媒介。</span><span class="sxs-lookup"><span data-stu-id="9f4d8-116">This includes any transport intermediaries that do not use SOAP (for example, HTTP proxies) or intermediaries that use SOAP (for example, SOAP-based routers or bridges) that are required for messages to flow between the endpoints.</span></span> <span data-ttu-id="9f4d8-117">可靠工作階段會使用記憶體中傳輸視窗來遮罩 SOAP 訊息層級的失敗，並在發生傳輸失敗時重新建立連線。</span><span class="sxs-lookup"><span data-stu-id="9f4d8-117">Reliable sessions use an in-memory transfer window to mask SOAP message-level failures and re-establish connections in the case of transport failures.</span></span>  
  
 <span data-ttu-id="9f4d8-118">可靠工作階段會提供短延遲時間的可信賴訊息傳輸。</span><span class="sxs-lookup"><span data-stu-id="9f4d8-118">Reliable sessions provide low-latency reliable message transfers.</span></span> <span data-ttu-id="9f4d8-119">它們可透過任何的 Proxy 或媒介提供 SOAP 訊息，而這相當於 TCP 透過 IP 橋接器為封包提供的內容。</span><span class="sxs-lookup"><span data-stu-id="9f4d8-119">They provide for SOAP messages over any proxies or intermediaries, equivalent to what TCP provides for packets over IP bridges.</span></span> <span data-ttu-id="9f4d8-120">如需可靠會話的詳細資訊，請參閱 [可靠會話](reliable-sessions.md)。</span><span class="sxs-lookup"><span data-stu-id="9f4d8-120">For more information about reliable sessions, see [Reliable Sessions](reliable-sessions.md).</span></span>  
  
## <a name="queues"></a><span data-ttu-id="9f4d8-121">佇列</span><span class="sxs-lookup"><span data-stu-id="9f4d8-121">Queues</span></span>  

 <span data-ttu-id="9f4d8-122">WCF 中的佇列提供可靠的訊息傳輸，並以高延遲的成本在來源與目的地之間分開。</span><span class="sxs-lookup"><span data-stu-id="9f4d8-122">Queues in WCF provide both reliable transfers of messages and separation between sources and destinations at the cost of high latency.</span></span> <span data-ttu-id="9f4d8-123">WCF 佇列的通訊是以訊息佇列 (（也稱為 MSMQ) ）為基礎。</span><span class="sxs-lookup"><span data-stu-id="9f4d8-123">WCF queued communication is built on top of Message Queuing (also known as MSMQ).</span></span>  
  
 <span data-ttu-id="9f4d8-124">MSMQ 是 Windows 隨附的選用元件，而且會以 NT 服務的身分執行。</span><span class="sxs-lookup"><span data-stu-id="9f4d8-124">MSMQ is shipped as an option with Windows that runs as an NT service.</span></span> <span data-ttu-id="9f4d8-125">它會代表來源擷取傳輸佇列中要進行傳輸的訊息，並將該訊息傳遞至目標佇列。</span><span class="sxs-lookup"><span data-stu-id="9f4d8-125">It captures messages for transmission in a transmission queue on behalf of the source and delivers it to a target queue.</span></span> <span data-ttu-id="9f4d8-126">目標佇列會代表目的地接受訊息，以便隨時因應目的地要求訊息而進行傳遞。</span><span class="sxs-lookup"><span data-stu-id="9f4d8-126">The target queue accepts messages on behalf of the destination for later delivery whenever the destination requests for messages.</span></span> <span data-ttu-id="9f4d8-127">MSMQ 佇列管理員會實作可靠訊息傳輸通訊協定，使訊息不會在傳輸期間遺失。</span><span class="sxs-lookup"><span data-stu-id="9f4d8-127">The MSMQ queue managers implement a reliable message-transfer protocol so that messages are not lost in transmission.</span></span> <span data-ttu-id="9f4d8-128">此通訊協定可以是原生或以 SOAP 為基礎的 SOAP Reliable Messaging Protocol (SRMP)。</span><span class="sxs-lookup"><span data-stu-id="9f4d8-128">The protocol can be native or SOAP-based, such as Soap Reliable Messaging Protocol (SRMP).</span></span>  
  
 <span data-ttu-id="9f4d8-129">佇列之間的區隔性以及可信賴傳訊，可讓鬆散耦合的應用程式進行可靠的通訊。</span><span class="sxs-lookup"><span data-stu-id="9f4d8-129">The separation, coupled with reliable message transfers between queues, enables applications that are loosely coupled to communicate reliably.</span></span> <span data-ttu-id="9f4d8-130">與可靠工作階段不同的是，來源和目的地不需要同時執行。</span><span class="sxs-lookup"><span data-stu-id="9f4d8-130">Unlike reliable sessions, the source and destination do not have to be running at the same time.</span></span> <span data-ttu-id="9f4d8-131">這個特點促使當來源的訊息生產率與目的地的訊息消耗率不相同時，作用中的佇列會被用來當做負載平衡機制。</span><span class="sxs-lookup"><span data-stu-id="9f4d8-131">This implicitly enables scenarios where queues are, in effect, used as a load-leveling mechanism when there is a mismatch between the rate of message production by the source and the rate of the message consumption by the destination.</span></span> <span data-ttu-id="9f4d8-132">如需佇列的詳細資訊，請參閱 [WCF 中的佇列](queues-in-wcf.md)。</span><span class="sxs-lookup"><span data-stu-id="9f4d8-132">For more information about queues, see [Queues in WCF](queues-in-wcf.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="9f4d8-133">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9f4d8-133">See also</span></span>

- [<span data-ttu-id="9f4d8-134">WCF 中的佇列</span><span class="sxs-lookup"><span data-stu-id="9f4d8-134">Queues in WCF</span></span>](queues-in-wcf.md)
- [<span data-ttu-id="9f4d8-135">WCF 中的佇列</span><span class="sxs-lookup"><span data-stu-id="9f4d8-135">Queuing in WCF</span></span>](queuing-in-wcf.md)
- [<span data-ttu-id="9f4d8-136">可靠工作階段</span><span class="sxs-lookup"><span data-stu-id="9f4d8-136">Reliable Sessions</span></span>](reliable-sessions.md)
- [<span data-ttu-id="9f4d8-137">可靠的工作階段概觀</span><span class="sxs-lookup"><span data-stu-id="9f4d8-137">Reliable Sessions Overview</span></span>](reliable-sessions-overview.md)
