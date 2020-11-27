---
title: 對等網狀結構
ms.date: 03/30/2017
ms.assetid: d93e312e-ac04-40f8-baea-5da1cacb546e
ms.openlocfilehash: 62feb237dd4a8a471175e32363887376f7d86212
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96272094"
---
# <a name="peer-meshes"></a><span data-ttu-id="a3e94-102">對等網狀結構</span><span class="sxs-lookup"><span data-stu-id="a3e94-102">Peer Meshes</span></span>

<span data-ttu-id="a3e94-103">*網格* 是一個命名集合， (互連的圖形) 對等節點，這些節點可彼此通訊，並由唯一的網格識別碼識別。</span><span class="sxs-lookup"><span data-stu-id="a3e94-103">A *mesh* is a named collection (an interconnected graph) of peer nodes that can communicate among themselves and that are identified by a unique mesh ID.</span></span> <span data-ttu-id="a3e94-104">每一個節點都會連接到多個不同節點。</span><span class="sxs-lookup"><span data-stu-id="a3e94-104">Each node is connected to multiple other nodes.</span></span> <span data-ttu-id="a3e94-105">在連線正確的網狀架構中，有兩個節點之間有相對較少的躍點，網格之間的節點之間會有相對較少的躍點，而且即使某些節點或連接中斷，網格仍會保持連線。網格中的使用中節點會發行其端點資訊與對應的網格識別碼，讓其他對等可以找到它們。</span><span class="sxs-lookup"><span data-stu-id="a3e94-105">In a well-connected mesh, there is a path between any two nodes, with relatively few hops between the nodes on the furthest edges of the mesh, and the mesh will remain connected even if some nodes or connections drop out. Active nodes in the mesh publish their endpoint information with a corresponding mesh ID so that other peers can find them.</span></span>  
  
## <a name="characteristics-of-a-mesh-created-using-peer-channel"></a><span data-ttu-id="a3e94-106">使用對等通道建立之網狀結構的特性</span><span class="sxs-lookup"><span data-stu-id="a3e94-106">Characteristics of a Mesh Created Using Peer Channel</span></span>  
  
#### <a name="uniquely-identified"></a><span data-ttu-id="a3e94-107">唯一識別</span><span class="sxs-lookup"><span data-stu-id="a3e94-107">Uniquely Identified</span></span>  
  
- <span data-ttu-id="a3e94-108">可識別每一個網狀結構的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="a3e94-108">A unique ID identifies each mesh.</span></span> <span data-ttu-id="a3e94-109">網狀結構的名稱 (或網狀結構識別碼) 格式和網域名稱系統 (DNS) 主機名稱相同。</span><span class="sxs-lookup"><span data-stu-id="a3e94-109">The name of the mesh (or mesh ID) is in the same format as a Domain Name System (DNS) host name.</span></span> <span data-ttu-id="a3e94-110">因此，對於在解析程式範圍內使用的預期應用程式用戶端而言，這個網狀結構識別碼必須是獨一無二的。</span><span class="sxs-lookup"><span data-stu-id="a3e94-110">As such, this mesh ID must be unique for the intended client of the application within the scope of the resolver being used.</span></span> <span data-ttu-id="a3e94-111">"MyFamilysPeers" 或 "KevinsPokerTable" 這種常見名稱，很容易與其他使用者名稱混淆，也可能傳回不想要的對等端點資訊，進而導致隱私權問題或增加連線延遲時間。</span><span class="sxs-lookup"><span data-stu-id="a3e94-111">A common name such as "MyFamilysPeers" or "KevinsPokerTable," may easily collide with other user names and may return unintended peer endpoint information, which could result in privacy issues or increase connection latency.</span></span> <span data-ttu-id="a3e94-112">避免發生這些問題的一種方法，是將唯一識別碼加入成網狀結構暱稱的後置 (例如，"KevinsPokerTable90210")。</span><span class="sxs-lookup"><span data-stu-id="a3e94-112">One way to avoid these issues may be to add a unique ID as a postfix to the nickname for the mesh (for example, "KevinsPokerTable90210").</span></span>  
  
#### <a name="message-flooding"></a><span data-ttu-id="a3e94-113">訊息湧入</span><span class="sxs-lookup"><span data-stu-id="a3e94-113">Message Flooding</span></span>  
  
- <span data-ttu-id="a3e94-114">網狀結構可讓訊息從一或多個寄件者傳播至相同網狀結構中的所有其他對等節點。</span><span class="sxs-lookup"><span data-stu-id="a3e94-114">The mesh allows messages to be propagated from one or more senders to all other peer nodes in the same mesh.</span></span> <span data-ttu-id="a3e94-115">對等節點湧入的訊息會使用命名空間中指定的標頭，其網址為 `http://schemas.microsoft.com/net/2006/05/peer`。</span><span class="sxs-lookup"><span data-stu-id="a3e94-115">Messages flooded by peer nodes use headers specified in the namespace at `http://schemas.microsoft.com/net/2006/05/peer`.</span></span>  
  
#### <a name="optimized-connections"></a><span data-ttu-id="a3e94-116">最佳化連線</span><span class="sxs-lookup"><span data-stu-id="a3e94-116">Optimized Connections</span></span>  
  
- <span data-ttu-id="a3e94-117">當節點結合與離開時，對等通道網狀結構會自動調整，以確保所有節點皆有良好的連接能力，而不至於太常產生分割的狀況 (彼此分離的節點群組)。</span><span class="sxs-lookup"><span data-stu-id="a3e94-117">A Peer Channel mesh automatically adjusts when nodes join and leave, ensuring that all nodes have good connectivity with little chance of creating partitions (groups of nodes isolated from each other).</span></span> <span data-ttu-id="a3e94-118">網狀結構中的連線也會依據目前的傳輸模式而動態最佳化，盡可能讓寄件者到接收者之間的訊息連線延遲降至最低。</span><span class="sxs-lookup"><span data-stu-id="a3e94-118">Connections in the mesh are also dynamically optimized based on current traffic patterns so that message latency from sender to receiver is as small as possible.</span></span>  
  
#### <a name="popular-network-features-that-peer-channel-does-not-provide"></a><span data-ttu-id="a3e94-119">對等通道未提供的常用網路功能</span><span class="sxs-lookup"><span data-stu-id="a3e94-119">Popular Network Features That Peer Channel Does Not Provide</span></span>  

 <span data-ttu-id="a3e94-120">了解對等通道不提供的常見網路功能可說是相當重要。</span><span class="sxs-lookup"><span data-stu-id="a3e94-120">It is important to be aware of popular network features that Peer Channel does not provide.</span></span> <span data-ttu-id="a3e94-121">這些功能 (可能都是建立在對等通道之上) 包括下列各項：</span><span class="sxs-lookup"><span data-stu-id="a3e94-121">These features, which may all be built on top of Peer Channel, include the following:</span></span>  
  
- <span data-ttu-id="a3e94-122">**訊息順序：** 源自單一來源的訊息可能不會以相同順序或依照來源傳送的順序抵達其他所有物件。</span><span class="sxs-lookup"><span data-stu-id="a3e94-122">**Message ordering:** Messages originating from a single source may not arrive at all other parties in the same order or in the order that the source sent.</span></span> <span data-ttu-id="a3e94-123">需要以特定順序傳遞訊息的應用程式，必須將此順序建置於應用程式中 (例如，在所有訊息中加入依序遞增的識別碼)。</span><span class="sxs-lookup"><span data-stu-id="a3e94-123">Applications that require messages be delivered in a certain order must build it into their applications (for example, by including a monotonically increasing ID with all messages).</span></span>  
  
- <span data-ttu-id="a3e94-124">**可靠的訊息：** 對等通道不包含可確保所有對等的訊息接收的機制。</span><span class="sxs-lookup"><span data-stu-id="a3e94-124">**Reliable messaging:** Peer Channel does not include a mechanism to ensure message reception by all peers.</span></span> <span data-ttu-id="a3e94-125">若要保證訊息傳遞，您必須在對等通道最上方寫入可靠性層。</span><span class="sxs-lookup"><span data-stu-id="a3e94-125">To guarantee message delivery, you must write a reliability layer on top of Peer Channel.</span></span>
