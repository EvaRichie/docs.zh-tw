---
title: NetworkInformation
ms.date: 03/30/2017
helpviewer_keywords:
- Network
ms.assetid: 31b44dd3-b903-4a48-8419-40419a3e4038
ms.openlocfilehash: 550555be7cc95cafebabfd3ac230ced024a9202c
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96261614"
---
# <a name="networkinformation"></a><span data-ttu-id="a67bb-102">NetworkInformation</span><span class="sxs-lookup"><span data-stu-id="a67bb-102">NetworkInformation</span></span>

<span data-ttu-id="a67bb-103"><xref:System.Net.NetworkInformation> 命名空間可讓您收集網路事件、變更、統計資料和屬性的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a67bb-103">The <xref:System.Net.NetworkInformation> namespace enables you to gather information about network events, changes, statistics, and properties.</span></span> <span data-ttu-id="a67bb-104">您也可以使用 <xref:System.Net.NetworkInformation.Ping?displayProperty=nameWithType> 類別，來判斷是否可連線至遠端主機。</span><span class="sxs-lookup"><span data-stu-id="a67bb-104">You can also determine whether a remote host is reachable by using the <xref:System.Net.NetworkInformation.Ping?displayProperty=nameWithType> class.</span></span>  
  
## <a name="network-availability-and-events"></a><span data-ttu-id="a67bb-105">網路可用性和事件</span><span class="sxs-lookup"><span data-stu-id="a67bb-105">Network Availability and Events</span></span>  

 <span data-ttu-id="a67bb-106"><xref:System.Net.NetworkInformation.NetworkChange?displayProperty=nameWithType> 類別可讓您判斷網路位址或可用性是否已變更。</span><span class="sxs-lookup"><span data-stu-id="a67bb-106">The <xref:System.Net.NetworkInformation.NetworkChange?displayProperty=nameWithType> class enables you to determine whether the network address or availability has changed.</span></span> <span data-ttu-id="a67bb-107">若要使用此類別，請建立事件處理常式來處理變更，並將它與 <xref:System.Net.NetworkInformation.NetworkAddressChangedEventHandler> 或 <xref:System.Net.NetworkInformation.NetworkAvailabilityChangedEventHandler> 建立關聯。</span><span class="sxs-lookup"><span data-stu-id="a67bb-107">To use this class, create an event handler to process the change, and associate it with a <xref:System.Net.NetworkInformation.NetworkAddressChangedEventHandler> or a <xref:System.Net.NetworkInformation.NetworkAvailabilityChangedEventHandler>.</span></span> <span data-ttu-id="a67bb-108">如需詳細資訊，請參閱[如何：偵測網路可用性和位址變更](how-to-detect-network-availability-and-address-changes.md)。</span><span class="sxs-lookup"><span data-stu-id="a67bb-108">For more information, see [How to: Detect Network Availability and Address Changes](how-to-detect-network-availability-and-address-changes.md).</span></span>  
  
## <a name="network-statistics-and-properties"></a><span data-ttu-id="a67bb-109">網路統計資料和屬性</span><span class="sxs-lookup"><span data-stu-id="a67bb-109">Network Statistics and Properties</span></span>  

 <span data-ttu-id="a67bb-110">您可以根據介面或通訊協定來收集網路統計資料和屬性。</span><span class="sxs-lookup"><span data-stu-id="a67bb-110">You can gather network statistics and properties on an interface or protocol basis.</span></span> <span data-ttu-id="a67bb-111"><xref:System.Net.NetworkInformation.NetworkInterface>、<xref:System.Net.NetworkInformation.NetworkInterfaceType> 和 <xref:System.Net.NetworkInformation.PhysicalAddress> 類別提供特定網路介面的相關資訊，而 <xref:System.Net.NetworkInformation.IPInterfaceProperties>、<xref:System.Net.NetworkInformation.IPGlobalProperties>、<xref:System.Net.NetworkInformation.IPGlobalStatistics>、<xref:System.Net.NetworkInformation.TcpStatistics> 和 <xref:System.Net.NetworkInformation.UdpStatistics> 類別提供第 3 層和第 4 層封包的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a67bb-111">The <xref:System.Net.NetworkInformation.NetworkInterface>, <xref:System.Net.NetworkInformation.NetworkInterfaceType>, and <xref:System.Net.NetworkInformation.PhysicalAddress> classes give information about a particular network interface, while the <xref:System.Net.NetworkInformation.IPInterfaceProperties>, <xref:System.Net.NetworkInformation.IPGlobalProperties>, <xref:System.Net.NetworkInformation.IPGlobalStatistics>, <xref:System.Net.NetworkInformation.TcpStatistics>, and <xref:System.Net.NetworkInformation.UdpStatistics> classes give information about layer 3 and layer 4 packets.</span></span> <span data-ttu-id="a67bb-112">如需詳細資訊，請參閱[如何：取得介面和通訊協定資訊](how-to-get-interface-and-protocol-information.md)。</span><span class="sxs-lookup"><span data-stu-id="a67bb-112">For more information, see [How to: Get Interface and Protocol Information](how-to-get-interface-and-protocol-information.md).</span></span>  
  
## <a name="determine-if-a-remote-host-is-reachable"></a><span data-ttu-id="a67bb-113">判斷是否可以連線遠端主機</span><span class="sxs-lookup"><span data-stu-id="a67bb-113">Determine if a Remote Host is Reachable</span></span>  

 <span data-ttu-id="a67bb-114">您可以使用 <xref:System.Net.NetworkInformation.Ping> 類別，判斷網路上的遠端主機是否啟動且可連線。</span><span class="sxs-lookup"><span data-stu-id="a67bb-114">You can use the <xref:System.Net.NetworkInformation.Ping> class to determine whether a Remote Host is up, on the network, and reachable.</span></span> <span data-ttu-id="a67bb-115">如需詳細資訊，請參閱[如何：Ping 主機](how-to-ping-a-host.md)。</span><span class="sxs-lookup"><span data-stu-id="a67bb-115">For more information, see [How to: Ping a Host](how-to-ping-a-host.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a67bb-116">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a67bb-116">See also</span></span>

- [<span data-ttu-id="a67bb-117">網路程式設計範例</span><span class="sxs-lookup"><span data-stu-id="a67bb-117">Network Programming Samples</span></span>](network-programming-samples.md)

<!-- to-do: review sample links
- [Network Information Technology Sample](https://archive.msdn.microsoft.com/nclsamples/Wiki/View.aspx?title=Network%20Information)
- [NetStat Tool Technology Sample](https://archive.msdn.microsoft.com/nclsamples/Wiki/View.aspx?title=NetStat%20Tool)
- [Ping Client Technology Sample](https://archive.msdn.microsoft.com/nclsamples/Wiki/View.aspx?title=Ping%20Client)
-->
