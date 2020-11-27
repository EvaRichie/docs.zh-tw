---
title: 網際網路通訊協定第 6 版
description: 瞭解 IPv6 通訊協定，以及它與 IPv4 有何不同。 .NET Framework 的應用程式支援 IPv6，但可能需要進行設定。
ms.date: 03/30/2017
helpviewer_keywords:
- IPv6, improvements
- IPv4
- IPv6
- Internet Protocol version 6, improvements
- Internet Protocol version 6
ms.assetid: e6fa8ebd-010a-4c48-a5ec-a5102c53c06f
ms.openlocfilehash: f5b74674ba4144f75d125267f2458394bb74fab1
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96283948"
---
# <a name="internet-protocol-version-6"></a><span data-ttu-id="7c11a-104">網際網路通訊協定第 6 版</span><span class="sxs-lookup"><span data-stu-id="7c11a-104">Internet Protocol Version 6</span></span>

<span data-ttu-id="7c11a-105">網際網路通訊協定第 6 版 (IPv6) 是網際網路網路層級的新標準通訊協定套件。</span><span class="sxs-lookup"><span data-stu-id="7c11a-105">The Internet Protocol version 6 (IPv6) is a new suite of standard protocols for the network layer of the Internet.</span></span> <span data-ttu-id="7c11a-106">IPv6 旨在解決網際網路通訊協定當前版本 (稱為 IPv4) 有關位址耗竭、安全性、自動組態和擴充性等等的許多問題。</span><span class="sxs-lookup"><span data-stu-id="7c11a-106">IPv6 is designed to solve many of the problems of the current version of the Internet Protocol suite (known as IPv4) with regard to address depletion, security, auto-configuration, extensibility, and so on.</span></span> <span data-ttu-id="7c11a-107">IPv6 展開網際網路的功能，以啟用新種類的應用程式，包括點對點與行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="7c11a-107">IPv6 expands the capabilities of the Internet to enable new kinds of applications, including peer-to-peer and mobile applications.</span></span> <span data-ttu-id="7c11a-108">以下是目前 IPv4 通訊協定的主要問題：</span><span class="sxs-lookup"><span data-stu-id="7c11a-108">The following are the main issues of the current IPv4 protocol:</span></span>  
  
- <span data-ttu-id="7c11a-109">快速消耗位址空間。</span><span class="sxs-lookup"><span data-stu-id="7c11a-109">Rapid depletion of the address space.</span></span>  
  
     <span data-ttu-id="7c11a-110">這導致使用網路位址轉譯器 (NAT) 將多個私人位址對應到單一公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7c11a-110">This has led to the use of Network Address Translators (NATs) that map multiple private addresses to a single public IP address.</span></span> <span data-ttu-id="7c11a-111">這項機制引起的主要問題是處理額外負荷以及缺乏端對端連線。</span><span class="sxs-lookup"><span data-stu-id="7c11a-111">The main problems created by this mechanism are processing overhead and lack of end-to-end connectivity.</span></span>  
  
- <span data-ttu-id="7c11a-112">缺少階層式支援。</span><span class="sxs-lookup"><span data-stu-id="7c11a-112">Lack of hierarchy support.</span></span>  
  
     <span data-ttu-id="7c11a-113">因為其固有的預先定義類別組織，IPv4 缺少真正的階層式支援。</span><span class="sxs-lookup"><span data-stu-id="7c11a-113">Because of its inherent predefined class organization, IPv4 lacks true hierarchical support.</span></span> <span data-ttu-id="7c11a-114">不可能以真正對應網路拓撲的方式來建立 IP 位址的結構。</span><span class="sxs-lookup"><span data-stu-id="7c11a-114">It is impossible to structure the IP addresses in a way that truly maps the network topology.</span></span> <span data-ttu-id="7c11a-115">此一重大的設計缺陷創造了對大型路由表的需求，以將 IPv4 封包傳遞至網際網路上的任何位置。</span><span class="sxs-lookup"><span data-stu-id="7c11a-115">This crucial design flaw creates the need for large routing tables to deliver IPv4 packets to any location on the Internet.</span></span>  
  
- <span data-ttu-id="7c11a-116">複雜的網路組態。</span><span class="sxs-lookup"><span data-stu-id="7c11a-116">Complex network configuration.</span></span>  
  
     <span data-ttu-id="7c11a-117">使用 IPv4，必須以靜態方式或使用 DHCP 等組態通訊協定指派位址。</span><span class="sxs-lookup"><span data-stu-id="7c11a-117">With IPv4, addresses must be assigned statically or using a configuration protocol such as DHCP.</span></span> <span data-ttu-id="7c11a-118">理想的情況下，主機可能不必依賴 DHCP 基礎結構的管理。</span><span class="sxs-lookup"><span data-stu-id="7c11a-118">In an ideal situation, hosts would not have to rely on the administration of a DHCP infrastructure.</span></span> <span data-ttu-id="7c11a-119">相反地，它們可以根據所在的網路區段自行設定。</span><span class="sxs-lookup"><span data-stu-id="7c11a-119">Instead, they would be able to configure themselves based on the network segment in which they are located.</span></span>  
  
- <span data-ttu-id="7c11a-120">缺少內建的驗證和機密性。</span><span class="sxs-lookup"><span data-stu-id="7c11a-120">Lack of built-in authentication and confidentiality.</span></span>  
  
     <span data-ttu-id="7c11a-121">IPv4 不需要任何提供交換資料驗證或加密之機制的支援。</span><span class="sxs-lookup"><span data-stu-id="7c11a-121">IPv4 does not require the support for any mechanism that provides authentication or encryption of the exchanged data.</span></span> <span data-ttu-id="7c11a-122">這會隨著 IPv6 變更。</span><span class="sxs-lookup"><span data-stu-id="7c11a-122">This changes with IPv6.</span></span> <span data-ttu-id="7c11a-123">網際網路通訊協定安全性 (IPSec) 是 IPv6 支援需求。</span><span class="sxs-lookup"><span data-stu-id="7c11a-123">Internet Protocol security (IPSec) is an IPv6 support requirement.</span></span>  
  
 <span data-ttu-id="7c11a-124">新的通訊協定套件必須滿足下列基本需求：</span><span class="sxs-lookup"><span data-stu-id="7c11a-124">A new protocol suite must satisfy the following basic requirements:</span></span>  
  
- <span data-ttu-id="7c11a-125">低額外負荷的大規模路由和定址。</span><span class="sxs-lookup"><span data-stu-id="7c11a-125">Large-scale routing and addressing with low overhead.</span></span>  
  
- <span data-ttu-id="7c11a-126">各種連線情況的自動組態。</span><span class="sxs-lookup"><span data-stu-id="7c11a-126">Auto-configuration for various connecting situations.</span></span>  
  
- <span data-ttu-id="7c11a-127">內建的驗證和機密性。</span><span class="sxs-lookup"><span data-stu-id="7c11a-127">Built-in authentication and confidentiality.</span></span>  
  
 <span data-ttu-id="7c11a-128">如需詳細資訊，請參閱 [IPv6 定址](ipv6-addressing.md)、[IPv6 路由](ipv6-routing.md)、[IPv6 自動組態](ipv6-auto-configuration.md)、[啟用和停用 IPv6](enabling-and-disabling-ipv6.md) 以及[如何：修改電腦組態檔以啟用 IPv6 支援](how-to-modify-the-computer-configuration-file-to-enable-ipv6-support.md)。</span><span class="sxs-lookup"><span data-stu-id="7c11a-128">For more information, see [IPv6 Addressing](ipv6-addressing.md), [IPv6 Routing](ipv6-routing.md), [IPv6 Auto-Configuration](ipv6-auto-configuration.md), [Enabling and Disabling IPv6](enabling-and-disabling-ipv6.md), and [How to: Modify the Computer Configuration File to Enable IPv6 Support](how-to-modify-the-computer-configuration-file-to-enable-ipv6-support.md).</span></span>  
  
## <a name="references"></a><span data-ttu-id="7c11a-129">參考資料</span><span class="sxs-lookup"><span data-stu-id="7c11a-129">References</span></span>  

 <span data-ttu-id="7c11a-130">以下是您可在[網際網路工程任務推動小組 (IETF)](https://www.ietf.org/) 網站中找到的精選 RFC 文件：</span><span class="sxs-lookup"><span data-stu-id="7c11a-130">The following are selected RFC documents that you can find at the [Internet Engineering Task Force (IETF)](https://www.ietf.org/) website:</span></span>  
  
- <span data-ttu-id="7c11a-131">RFC 1287，前進未來網際網路架構。</span><span class="sxs-lookup"><span data-stu-id="7c11a-131">RFC 1287, Towards the Future Internet Architecture.</span></span>  
  
- <span data-ttu-id="7c11a-132">RFC 1454，下一版 IP 的建議比較。</span><span class="sxs-lookup"><span data-stu-id="7c11a-132">RFC 1454, Comparison of Proposals for Next Version of IP.</span></span>  
  
- <span data-ttu-id="7c11a-133">RFC 2373，IP 第 6 版定址架構。</span><span class="sxs-lookup"><span data-stu-id="7c11a-133">RFC 2373, IP Version 6 Addressing Architecture.</span></span>  
  
- <span data-ttu-id="7c11a-134">RFC 2374，IPv6 彙總全域單點傳播位址格式。</span><span class="sxs-lookup"><span data-stu-id="7c11a-134">RFC 2374, An IPv6 Aggregatable Global Unicast Address Format.</span></span>  
  
 <span data-ttu-id="7c11a-135">您也可以在 [IP 版本 6 (IPv6)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd379498(v=ws.10)) 找到 IPv6 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7c11a-135">You can also find IPv6-related information on the [IP Version 6 (IPv6)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd379498(v=ws.10)).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="7c11a-136">另請參閱</span><span class="sxs-lookup"><span data-stu-id="7c11a-136">See also</span></span>

- <span data-ttu-id="7c11a-137">[IPv6 通訊端範例](/previous-versions/dotnet/netframework-3.0/ms180981(v=vs.85))</span><span class="sxs-lookup"><span data-stu-id="7c11a-137">[IPv6 Sockets Sample](/previous-versions/dotnet/netframework-3.0/ms180981(v=vs.85))</span></span>
- [<span data-ttu-id="7c11a-138">網路程式設計範例</span><span class="sxs-lookup"><span data-stu-id="7c11a-138">Network Programming Samples</span></span>](network-programming-samples.md)
- [<span data-ttu-id="7c11a-139">通訊端</span><span class="sxs-lookup"><span data-stu-id="7c11a-139">Sockets</span></span>](sockets.md)
