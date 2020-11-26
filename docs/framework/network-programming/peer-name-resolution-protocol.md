---
title: 對等名稱解析通訊協定
description: 深入瞭解對等名稱解析通訊協定 (PNRP) ，這是安全、可調整的動態名稱註冊和名稱解析通訊協定。
ms.date: 03/30/2017
ms.assetid: 11940511-c124-4d91-ae31-d4ed6e81ee58
ms.openlocfilehash: d50514569d066d04391ce65522df789ed421dbed
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96239389"
---
# <a name="peer-name-resolution-protocol"></a><span data-ttu-id="dd28a-103">對等名稱解析通訊協定</span><span class="sxs-lookup"><span data-stu-id="dd28a-103">Peer Name Resolution Protocol</span></span>

<span data-ttu-id="dd28a-104">在對等環境中，對等使用特定名稱解析系統，才能從名稱或其他類型的識別碼解析彼此的網路位置 (位址、通訊協定和連接埠)。</span><span class="sxs-lookup"><span data-stu-id="dd28a-104">In peer-to-peer environments, peers use specific name resolution systems to resolve each other's network locations (addresses, protocols, and ports) from names or other types of identifiers.</span></span> <span data-ttu-id="dd28a-105">過去，網域名稱系統 (DNS) 內本來就是暫時性連線以及其他缺點，而讓對等名稱解析變得複雜。</span><span class="sxs-lookup"><span data-stu-id="dd28a-105">In the past, peer name resolution has been complicated by the inherently transient connectivity as well as other shortcomings within the Domain Name System (DNS).</span></span>  
  
 <span data-ttu-id="dd28a-106">Microsoft® Windows® 對等網路平台會利用對等名稱解析通訊協定 (PNRP) 解決此問題，此通訊協定最先是針對 Windows XP 所開發，之後於 Windows Vista™ 中升級，是一項安全、可調整的動態名稱登錄與名稱解析通訊協定。</span><span class="sxs-lookup"><span data-stu-id="dd28a-106">The Microsoft® Windows® Peer-to-Peer Networking platform solves this problem with the Peer Name Resolution Protocol (PNRP), a secure, scalable, and dynamic name registration and name resolution protocol first developed for Windows XP and then upgraded in Windows Vista™.</span></span> <span data-ttu-id="dd28a-107">PNRP 的運作方式與傳統的名稱解析系統十分不同，為應用程式開發人員開拓令人雀躍的嶄新視野。</span><span class="sxs-lookup"><span data-stu-id="dd28a-107">PNRP works very differently from traditional name resolution systems, opening up exciting new possibilities for application developers.</span></span>  
  
 <span data-ttu-id="dd28a-108">使用 PNRP，可以將對等名稱套用至電腦，或是電腦上的個別應用程式或服務。</span><span class="sxs-lookup"><span data-stu-id="dd28a-108">With PNRP, peer names can be applied to the machine, or individual applications or services on the machine.</span></span> <span data-ttu-id="dd28a-109">對等名稱解析包含位址、連接埠，以及可能的延伸承載。</span><span class="sxs-lookup"><span data-stu-id="dd28a-109">A peer name resolution includes an address, port, and possibly an extended payload.</span></span> <span data-ttu-id="dd28a-110">此系統的優點包含容錯、無瓶頸，以及絕不會傳回過時位址的名稱解析；這樣讓通訊協定成為尋找行動使用者的最佳解決方案。</span><span class="sxs-lookup"><span data-stu-id="dd28a-110">Benefits of this system include fault tolerance, no bottlenecks, and name resolutions that will never return stale addresses; making the protocol an excellent solution for locating mobile users.</span></span>  
  
 <span data-ttu-id="dd28a-111">就安全性而言，可以將對等名稱發行為安全的 (受保護) 或不安全的 (未受保護)。</span><span class="sxs-lookup"><span data-stu-id="dd28a-111">In terms of security, peer names can be published as secured (protected) or unsecured (unprotected).</span></span> <span data-ttu-id="dd28a-112">PNRP 使用公開金鑰加密來保護安全對等名稱防止詐騙；您可以使用 PNRP 來命名電腦和服務。</span><span class="sxs-lookup"><span data-stu-id="dd28a-112">PNRP uses public key cryptography to protect secure peer names against spoofing; both computers and services can be named with PNRP.</span></span>  
  
<span data-ttu-id="dd28a-113">對等名稱解析通訊協定會示範下列屬性：</span><span class="sxs-lookup"><span data-stu-id="dd28a-113">The Peer Name Resolution Protocol demonstrates the following properties:</span></span>  
  
- <span data-ttu-id="dd28a-114">分散式且幾乎完全無伺服器。</span><span class="sxs-lookup"><span data-stu-id="dd28a-114">Distributed and almost entirely serverless.</span></span> <span data-ttu-id="dd28a-115">只有啟動程序處理序才需要伺服器。</span><span class="sxs-lookup"><span data-stu-id="dd28a-115">Servers are only required for the bootstrapping process.</span></span>  
  
- <span data-ttu-id="dd28a-116">沒有第三方的安全名稱發行。</span><span class="sxs-lookup"><span data-stu-id="dd28a-116">Secure name publication without the involvement of third parties.</span></span> <span data-ttu-id="dd28a-117">與 DNS 名稱發行不同，PNRP 名稱發行是瞬間發生的，沒有財務成本。</span><span class="sxs-lookup"><span data-stu-id="dd28a-117">Unlike DNS name publication, PNRP name publication is instantaneous and without financial cost.</span></span>  
  
- <span data-ttu-id="dd28a-118">PNRP 會即時更新，以防止解析過時位址。</span><span class="sxs-lookup"><span data-stu-id="dd28a-118">PNRP updates in real-time, which prevents the resolution of stale addresses.</span></span>  
  
- <span data-ttu-id="dd28a-119">透過 PNRP 的名稱解析同時允許服務的名稱解析，以擴充到不只限於電腦。</span><span class="sxs-lookup"><span data-stu-id="dd28a-119">The resolution of names via PNRP extends beyond computers by also allowing name resolution for services.</span></span>  
  
## <a name="the-systemnetpeertopeer-namespace"></a><span data-ttu-id="dd28a-120">System.Net.PeerToPeer 命名空間</span><span class="sxs-lookup"><span data-stu-id="dd28a-120">The System.Net.PeerToPeer namespace</span></span>  
  
- <span data-ttu-id="dd28a-121">PNRP 功能是由 .NET Framework 3.5 版內的 <xref:System.Net.PeerToPeer> 命名空間所定義。</span><span class="sxs-lookup"><span data-stu-id="dd28a-121">PNRP functionality is defined by the <xref:System.Net.PeerToPeer> namespace within the .NET Framework version 3.5.</span></span> <span data-ttu-id="dd28a-122">它提供的一組類型可用來向可用的 PNRP 服務註冊和解析對等名稱。</span><span class="sxs-lookup"><span data-stu-id="dd28a-122">It provides a set of types that can be used to register and resolve peer names with an available PNRP service.</span></span>  
  
- <span data-ttu-id="dd28a-123">(PNRP 和自訂對等解析程式可以使用 <xref:System.ServiceModel.PeerResolvers> 命名空間中所提供的類型進行建立和具現化)。</span><span class="sxs-lookup"><span data-stu-id="dd28a-123">(PNRP and custom peer resolvers can be created and instantiated using the types provided in the <xref:System.ServiceModel.PeerResolvers> namespace.)</span></span>  
  
- <span data-ttu-id="dd28a-124">用來向可用 PNRP 服務註冊和解析名稱的基本類型如下：</span><span class="sxs-lookup"><span data-stu-id="dd28a-124">The basic types used to register and resolve names with an available PNRP service are as follows:</span></span>  
  
- <span data-ttu-id="dd28a-125"><xref:System.Net.PeerToPeer.Cloud>：定義描述可用 PNRP 雲端的資訊，包含其範圍。</span><span class="sxs-lookup"><span data-stu-id="dd28a-125"><xref:System.Net.PeerToPeer.Cloud>: Defines the information describing an available PNRP cloud, including its scope.</span></span>  
  
- <span data-ttu-id="dd28a-126"><xref:System.Net.PeerToPeer.PeerName>：定義可用來註冊並後續解析雲端內對等的對等名稱。</span><span class="sxs-lookup"><span data-stu-id="dd28a-126"><xref:System.Net.PeerToPeer.PeerName>: Defines a peer name that can be used to register and subsequently resolve a peer within a cloud.</span></span>  
  
- <span data-ttu-id="dd28a-127"><xref:System.Net.PeerToPeer.PeerNameRecord>：定義 PNRP 雲端中包含對等註冊資訊的記錄，而對等包含可連絡對等的網路端點。</span><span class="sxs-lookup"><span data-stu-id="dd28a-127"><xref:System.Net.PeerToPeer.PeerNameRecord>: Defines the record in PNRP cloud that contains the registration information for a peer, which includes the network endpoints at which the peer can be contacted.</span></span>  
  
- <span data-ttu-id="dd28a-128"><xref:System.Net.PeerToPeer.PeerNameRegistration>：定義對等名稱的註冊處理序，包含啟動和停止對等名稱註冊的方法。</span><span class="sxs-lookup"><span data-stu-id="dd28a-128"><xref:System.Net.PeerToPeer.PeerNameRegistration>: Defines the registration process for a peer name, including methods to start and stop peer name registration.</span></span>  
  
- <span data-ttu-id="dd28a-129"><xref:System.Net.PeerToPeer.PeerNameResolver>：定義將對等名稱解析成其網路端點的處理序，同時包含解析的同步和非同步方法。</span><span class="sxs-lookup"><span data-stu-id="dd28a-129"><xref:System.Net.PeerToPeer.PeerNameResolver>: Defines the process for resolving a peer name to its network endpoint(s), including both synchronous and asynchronous methods for resolution.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="dd28a-130">另請參閱</span><span class="sxs-lookup"><span data-stu-id="dd28a-130">See also</span></span>

- <xref:System.ServiceModel.PeerResolvers>
- <xref:System.Net.PeerToPeer>
- [<span data-ttu-id="dd28a-131">網路程式設計範例</span><span class="sxs-lookup"><span data-stu-id="dd28a-131">Network Programming Samples</span></span>](network-programming-samples.md)

<!-- to-do: review sample links
- [PeerToPeer Technology Sample](https://go.microsoft.com/fwlink/?LinkID=179571)
-->
