---
title: 實作探索 Proxy
ms.date: 03/30/2017
ms.assetid: dda20e79-8df3-438e-a281-69d779d978ec
ms.openlocfilehash: ae003c89bb0f14623c5d31a1596533d821380336
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96268296"
---
# <a name="implementing-a-discovery-proxy"></a><span data-ttu-id="07b1b-102">實作探索 Proxy</span><span class="sxs-lookup"><span data-stu-id="07b1b-102">Implementing a Discovery Proxy</span></span>

<span data-ttu-id="07b1b-103">本節說明實作探索 Proxy 的必要步驟。</span><span class="sxs-lookup"><span data-stu-id="07b1b-103">This section describes the steps required to implement a discovery proxy.</span></span> <span data-ttu-id="07b1b-104">探索 Proxy 是一項獨立的服務，包含服務的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="07b1b-104">A discovery proxy is a standalone service that contains a repository of services.</span></span> <span data-ttu-id="07b1b-105">用戶端可以查詢探索 Proxy 來尋找 Proxy 感知的可探索服務。</span><span class="sxs-lookup"><span data-stu-id="07b1b-105">Clients can query a discovery proxy to find discoverable services that the proxy is aware of.</span></span> <span data-ttu-id="07b1b-106">Proxy 中如何填入服務的方式完全取決於實作器。</span><span class="sxs-lookup"><span data-stu-id="07b1b-106">How a proxy is populated with services is up to the implementer.</span></span> <span data-ttu-id="07b1b-107">例如，探索 Proxy 可以連接至現有服務儲存機制，並且使資訊成為可探索，系統管理員可以使用管理 API 將可探索的服務加入至 Proxy，或是探索 Proxy 可以使用公告功能更新其內部快取。</span><span class="sxs-lookup"><span data-stu-id="07b1b-107">For example, a discovery proxy can connect to an existing service repository and make that information discoverable, an administrator can use a management API to add discoverable services to a proxy, or a discovery proxy can use the announcement functionality to update its internal cache.</span></span>  
  
 <span data-ttu-id="07b1b-108">WCF 實作提供的基底類別可讓您輕鬆建置 Proxy。</span><span class="sxs-lookup"><span data-stu-id="07b1b-108">The WCF implementation provides base classes that allow you to easily build a proxy.</span></span> <span data-ttu-id="07b1b-109">您可以利用這些 API 在現有儲存機制之上建置探索 Proxy。</span><span class="sxs-lookup"><span data-stu-id="07b1b-109">You can utilize these APIs to build a Discovery Proxy on top of your existing repository.</span></span>  
  
 <span data-ttu-id="07b1b-110">此處實作的探索 Proxy 就像其他 WCF 服務一般，也就是說，您也可以讓探索 Proxy 成為可探索，並且讓用戶端尋找其端點。</span><span class="sxs-lookup"><span data-stu-id="07b1b-110">The discovery proxy implemented here is like any other WCF services, in that you can also make the discovery proxy discoverable and have the clients locate its endpoints.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="07b1b-111">本節內容</span><span class="sxs-lookup"><span data-stu-id="07b1b-111">In This Section</span></span>  

 [<span data-ttu-id="07b1b-112">作法：實作探索 Proxy</span><span class="sxs-lookup"><span data-stu-id="07b1b-112">How to: Implement a Discovery Proxy</span></span>](how-to-implement-a-discovery-proxy.md)  
 <span data-ttu-id="07b1b-113">說明如何實作探索 Proxy。</span><span class="sxs-lookup"><span data-stu-id="07b1b-113">Describes how to implement a discovery proxy.</span></span>  
  
 [<span data-ttu-id="07b1b-114">作法：實作以探索 Proxy 註冊的可探索服務</span><span class="sxs-lookup"><span data-stu-id="07b1b-114">How to: Implement a Discoverable Service that Registers with the Discovery Proxy</span></span>](discoverable-service-that-registers-with-the-discovery-proxy.md)  
 <span data-ttu-id="07b1b-115">說明如何執行可探索的 WCF 服務，該服務會向探索 proxy 註冊。</span><span class="sxs-lookup"><span data-stu-id="07b1b-115">Describes how to implement a discoverable WCF service that registers with the discovery proxy.</span></span>  
  
 [<span data-ttu-id="07b1b-116">作法：實作使用探索 Proxy 的用戶端應用程式來尋找服務</span><span class="sxs-lookup"><span data-stu-id="07b1b-116">How to: Implement a Client Application that Uses the Discovery Proxy to Find a Service</span></span>](client-app-discovery-proxy-to-find-a-service.md)  
 <span data-ttu-id="07b1b-117">說明如何執行使用探索 proxy 來搜尋服務的 WCF 用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="07b1b-117">Describes how to implement a WCF client application that uses the discovery proxy to search for a service.</span></span>  
  
 [<span data-ttu-id="07b1b-118">作法：測試探索 Proxy</span><span class="sxs-lookup"><span data-stu-id="07b1b-118">How to: Test the Discovery Proxy</span></span>](how-to-test-the-discovery-proxy.md)  
 <span data-ttu-id="07b1b-119">說明如何測試前三個主題中撰寫的程式碼。</span><span class="sxs-lookup"><span data-stu-id="07b1b-119">Describes how to test the code written in the previous three topics.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="07b1b-120">另請參閱</span><span class="sxs-lookup"><span data-stu-id="07b1b-120">See also</span></span>

- [<span data-ttu-id="07b1b-121">WCF 探索</span><span class="sxs-lookup"><span data-stu-id="07b1b-121">WCF Discovery</span></span>](wcf-discovery.md)
- [<span data-ttu-id="07b1b-122">作法：以程式設計方式將探索能力新增至 WCF 服務與用戶端</span><span class="sxs-lookup"><span data-stu-id="07b1b-122">How to: Programmatically Add Discoverability to a WCF Service and Client</span></span>](how-to-programmatically-add-discoverability-to-a-wcf-service-and-client.md)
