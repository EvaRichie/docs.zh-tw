---
title: System.Net 類別的最佳作法
description: 請遵循這些建議，使用 System.Net 中所含的類別，以充分利用 .NET Framework 程式設計。
ms.date: 03/30/2017
helpviewer_keywords:
- sending data, best practices
- requesting data from Internet, best practices
- WebRequest class, best practices
- data requests, best practices
- WebResponse class, best practices
- best practices, data requests
- receiving data, best practices
ms.assetid: 716decc6-5952-47b7-9c5a-ba6fc5698684
ms.openlocfilehash: 583fa5e57c7c4d60252dddfd425596e7acad7c0d
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502674"
---
# <a name="best-practices-for-systemnet-classes"></a><span data-ttu-id="1dbf4-103">System.Net 類別的最佳作法</span><span class="sxs-lookup"><span data-stu-id="1dbf4-103">Best Practices for System.Net Classes</span></span>
<span data-ttu-id="1dbf4-104">下列建議將協助您善加利用 <xref:System.Net> 中所含的類別：</span><span class="sxs-lookup"><span data-stu-id="1dbf4-104">The following recommendations will help you use the classes contained in <xref:System.Net> to their best advantage:</span></span>  
  
- <span data-ttu-id="1dbf4-105">如需傳輸層安全性 (TLS) 的最佳做法，請參閱 [.NET Framework 的傳輸層安全性 (TLS) 最佳做法](tls.md)。</span><span class="sxs-lookup"><span data-stu-id="1dbf4-105">For Transport Layer Security (TLS) best practices, see [Transport Layer Security (TLS) best practices with .NET Framework](tls.md).</span></span>

- <span data-ttu-id="1dbf4-106">可能的話，請使用 <xref:System.Net.WebRequest> 和 <xref:System.Net.WebResponse>，而不是對子系類別進行類型轉換。</span><span class="sxs-lookup"><span data-stu-id="1dbf4-106">Use <xref:System.Net.WebRequest> and <xref:System.Net.WebResponse> whenever possible instead of type casting to descendant classes.</span></span> <span data-ttu-id="1dbf4-107">使用 **WebRequest** 和 **WebResponse** 的應用程式可以利用新的網際網路通訊協定，而不需要大量的程式碼變更。</span><span class="sxs-lookup"><span data-stu-id="1dbf4-107">Applications that use **WebRequest** and **WebResponse** can take advantage of new Internet protocols without needing extensive code changes.</span></span>  
  
- <span data-ttu-id="1dbf4-108">使用 **System.Net** 類別撰寫在伺服器上執行的 ASP.NET 應用程式時，其效能通常會比使用 <xref:System.Net.WebRequest.GetResponse%2A> 和 <xref:System.Net.WebResponse.GetResponseStream%2A> 的非同步方法還要好。</span><span class="sxs-lookup"><span data-stu-id="1dbf4-108">When writing ASP.NET applications that run on a server using the **System.Net** classes, it is often better, from a performance standpoint, to use the asynchronous methods for <xref:System.Net.WebRequest.GetResponse%2A> and <xref:System.Net.WebResponse.GetResponseStream%2A>.</span></span>  
  
- <span data-ttu-id="1dbf4-109">開啟至網際網路資源的連線數目，會對網路效能和輸送量造成明顯影響。</span><span class="sxs-lookup"><span data-stu-id="1dbf4-109">The number of connections opened to an Internet resource can have a significant impact on network performance and throughput.</span></span> <span data-ttu-id="1dbf4-110">**System.Net** 預設會為每個主機的每個應用程式使用兩個連線。</span><span class="sxs-lookup"><span data-stu-id="1dbf4-110">**System.Net** uses two connections per application per host by default.</span></span> <span data-ttu-id="1dbf4-111">在應用程式的 <xref:System.Net.ServicePoint> 中設定 <xref:System.Net.ServicePoint.ConnectionLimit%2A> 屬性，可能會針對特定主機增加這個數目。</span><span class="sxs-lookup"><span data-stu-id="1dbf4-111">Setting the <xref:System.Net.ServicePoint.ConnectionLimit%2A> property in the <xref:System.Net.ServicePoint> for your application can increase this number for a particular host.</span></span> <span data-ttu-id="1dbf4-112">設定 <xref:System.Net.ServicePointManager.DefaultPersistentConnectionLimit?displayProperty=nameWithType> 屬性可以為所有主機增加這個預設值。</span><span class="sxs-lookup"><span data-stu-id="1dbf4-112">Setting the <xref:System.Net.ServicePointManager.DefaultPersistentConnectionLimit?displayProperty=nameWithType> property can increase this default for all hosts.</span></span>  
  
- <span data-ttu-id="1dbf4-113">撰寫通訊端層級通訊協定時，請盡可能嘗試使用 <xref:System.Net.Sockets.TcpClient> 或 <xref:System.Net.Sockets.UdpClient>，而不是直接寫入至 <xref:System.Net.Sockets.Socket>。</span><span class="sxs-lookup"><span data-stu-id="1dbf4-113">When writing socket-level protocols, try to use <xref:System.Net.Sockets.TcpClient> or <xref:System.Net.Sockets.UdpClient> whenever possible instead of writing directly to a <xref:System.Net.Sockets.Socket>.</span></span> <span data-ttu-id="1dbf4-114">這兩個用戶端類別會封裝 TCP 和 UDP 通訊端的建立，而不需要您處理連線的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="1dbf4-114">These two client classes encapsulate the creation of TCP and UDP sockets without requiring you to handle the details of the connection.</span></span>  
  
- <span data-ttu-id="1dbf4-115">存取需要認證的網站時，請使用 <xref:System.Net.CredentialCache> 類別建立認證的快取，而不是每個要求都提供它們。</span><span class="sxs-lookup"><span data-stu-id="1dbf4-115">When accessing sites that require credentials, use the <xref:System.Net.CredentialCache> class to create a cache of credentials rather than supplying them with every request.</span></span> <span data-ttu-id="1dbf4-116">**CredentialCache** 類別會搜尋快取，以透過要求找到要呈現的適當認證，讓您不需要負責根據 URL 來建立和呈現認證。</span><span class="sxs-lookup"><span data-stu-id="1dbf4-116">The **CredentialCache** class searches the cache to find the appropriate credential to present with a request, relieving you of the responsibility of creating and presenting credentials based on the URL.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="1dbf4-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1dbf4-117">See also</span></span>

- [<span data-ttu-id="1dbf4-118">.NET Framework 中的網路程式設計</span><span class="sxs-lookup"><span data-stu-id="1dbf4-118">Network Programming in the .NET Framework</span></span>](index.md)
