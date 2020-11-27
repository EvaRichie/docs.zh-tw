---
title: AJAX 整合與 JSON 支援
ms.date: 03/30/2017
helpviewer_keywords:
- AJAX integration and JSON support [WCF]
ms.assetid: 3851a8fc-d861-4ac1-873c-96af0343d3a7
ms.openlocfilehash: c895a6dedc22a42adb7104927d39090ab6587f37
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96266021"
---
# <a name="ajax-integration-and-json-support"></a><span data-ttu-id="fee64-102">AJAX 整合與 JSON 支援</span><span class="sxs-lookup"><span data-stu-id="fee64-102">AJAX Integration and JSON Support</span></span>

<span data-ttu-id="fee64-103">Windows Communication Foundation (WCF) ASP.NET 非同步 JavaScript 和 XML (AJAX) 和 JavaScript 物件標記法 (JSON) 資料格式的支援，可讓 WCF 服務對 AJAX 用戶端公開作業。</span><span class="sxs-lookup"><span data-stu-id="fee64-103">The Windows Communication Foundation (WCF) support for ASP.NET Asynchronous JavaScript and XML (AJAX) and the JavaScript Object Notation (JSON) data format allow WCF services to expose operations to AJAX clients.</span></span> <span data-ttu-id="fee64-104">AJAX 用戶端是執行 JavaScript 程式碼的網頁，並使用 HTTP 要求來存取這些 WCF 服務。</span><span class="sxs-lookup"><span data-stu-id="fee64-104">AJAX clients are Web pages running JavaScript code and accessing these WCF services using HTTP requests.</span></span> <span data-ttu-id="fee64-105">本節中的主題會提供有關此支援以及如何實作的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="fee64-105">The topics in this section provide information about this support and about how to implement it.</span></span>  
  
 <span data-ttu-id="fee64-106">如需有關 ASP.NET AJAX 以及與 ASP.NET 2.0 整合的詳細資訊，請參閱 [ASP.NET Ajax 總覽](/previous-versions/aspnet/bb398874(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="fee64-106">For more information about ASP.NET AJAX and its integration with ASP.NET 2.0, see [ASP.NET AJAX Overview](/previous-versions/aspnet/bb398874(v=vs.100)).</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="fee64-107">本節內容</span><span class="sxs-lookup"><span data-stu-id="fee64-107">In This Section</span></span>  

 [<span data-ttu-id="fee64-108">建立 ASP.NET AJAX 的 WCF 服務</span><span class="sxs-lookup"><span data-stu-id="fee64-108">Creating WCF Services for ASP.NET AJAX</span></span>](creating-wcf-services-for-aspnet-ajax.md)  
 <span data-ttu-id="fee64-109">描述如何將 WCF 服務公開給 AJAX 用戶端，方法是透過設定新增適當的 AJAX 端點，或使用自訂的服務主機 factory 來產生自動設定 AJAX 端點的服務主機。</span><span class="sxs-lookup"><span data-stu-id="fee64-109">Describes how a WCF service can be exposed to AJAX clients by adding the appropriate AJAX endpoint either through configuration or by using a service host factory customized to generate a service host that configures the AJAX endpoint automatically.</span></span>  
  
 [<span data-ttu-id="fee64-110">建立不含 ASP.NET 的 WCF AJAX 服務</span><span class="sxs-lookup"><span data-stu-id="fee64-110">Creating WCF AJAX Services without ASP.NET</span></span>](creating-wcf-ajax-services-without-aspnet.md)  
 <span data-ttu-id="fee64-111">描述如何在不使用 ASP.NET 的情況下建立 WCF 服務。</span><span class="sxs-lookup"><span data-stu-id="fee64-111">Describes how to create a WCF service without using ASP.NET.</span></span>  
  
 [<span data-ttu-id="fee64-112">JSON 和其他資料傳輸格式的支援</span><span class="sxs-lookup"><span data-stu-id="fee64-112">Support for JSON and Other Data Transfer Formats</span></span>](support-for-json-and-other-data-transfer-formats.md)  
 <span data-ttu-id="fee64-113">針對使用 ASP.NET AJAX 服務的訊息，說明慣用的 JSON 格式 (而不是 XML) 支援。</span><span class="sxs-lookup"><span data-stu-id="fee64-113">Describes the support of the JSON format typically used (instead of XML) for messaging with ASP.NET AJAX services.</span></span>  
  
 [<span data-ttu-id="fee64-114">作法：將啟用 AJAX 的 ASP.NET Web 服務移轉至 WCF</span><span class="sxs-lookup"><span data-stu-id="fee64-114">How to: Migrate AJAX-Enabled ASP.NET Web Services to WCF</span></span>](how-to-migrate-ajax-enabled-aspnet-web-services-to-wcf.md)  
 <span data-ttu-id="fee64-115">說明如何將具備 AJAX 功能的 ASP.NET Web 服務遷移至 WCF Web 服務。</span><span class="sxs-lookup"><span data-stu-id="fee64-115">Describes how to migrate an AJAX-enabled ASP.NET Web service to a WCF Web service.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="fee64-116">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fee64-116">See also</span></span>

- <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory>
- [<span data-ttu-id="fee64-117">WCF Web HTTP 程式設計模型</span><span class="sxs-lookup"><span data-stu-id="fee64-117">WCF Web HTTP Programming Model</span></span>](wcf-web-http-programming-model.md)
