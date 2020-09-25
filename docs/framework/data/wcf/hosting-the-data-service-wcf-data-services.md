---
title: 裝載資料服務 (WCF 資料服務)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, configuring
- WCF Data Services, Windows Communication Foundation
ms.assetid: b48f42ce-22ce-4f8d-8f0d-f7ddac9125ee
ms.openlocfilehash: 5dfa1d9f02f660b55ecf6598ef5012174a1ba853
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91172589"
---
# <a name="hosting-the-data-service-wcf-data-services"></a><span data-ttu-id="66dea-102">裝載資料服務 (WCF 資料服務)</span><span class="sxs-lookup"><span data-stu-id="66dea-102">Hosting the Data Service (WCF Data Services)</span></span>

<span data-ttu-id="66dea-103">藉由使用 WCF Data Services，您可以建立將資料公開為開放式資料通訊協定 (OData) 摘要的服務。</span><span class="sxs-lookup"><span data-stu-id="66dea-103">By using WCF Data Services, you can create a service that exposes data as an Open Data Protocol (OData) feed.</span></span> <span data-ttu-id="66dea-104">這個資料服務會定義為繼承自 <xref:System.Data.Services.DataService%601> 的類別。</span><span class="sxs-lookup"><span data-stu-id="66dea-104">This data service is defined as a class that inherits from <xref:System.Data.Services.DataService%601>.</span></span> <span data-ttu-id="66dea-105">這個類別會提供處理要求訊息、針對資料來源執行更新，並依 OData 的要求產生回應訊息所需的功能。</span><span class="sxs-lookup"><span data-stu-id="66dea-105">This class provides the functionality required to process request messages, perform updates against the data source, and generate responses messages, as required by OData.</span></span> <span data-ttu-id="66dea-106">但是，資料服務無法繫結至及接聽內送 HTTP 要求所適用的網路通訊端。</span><span class="sxs-lookup"><span data-stu-id="66dea-106">However, a data service cannot bind to and listen on a network socket for incoming HTTP requests.</span></span> <span data-ttu-id="66dea-107">對於這個必要的功能而言，資料服務會依賴裝載的元件。</span><span class="sxs-lookup"><span data-stu-id="66dea-107">For this required functionality, the data service relies on a hosting component.</span></span>

 <span data-ttu-id="66dea-108">資料服務主機會代表資料服務執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="66dea-108">The data service host performs the following tasks on behalf of the data service:</span></span>

- <span data-ttu-id="66dea-109">接聽要求，並將這些要求路由傳送到資料服務。</span><span class="sxs-lookup"><span data-stu-id="66dea-109">Listens for requests and routes these requests to the data service.</span></span>

- <span data-ttu-id="66dea-110">為每一個要求建立資料服務的執行個體。</span><span class="sxs-lookup"><span data-stu-id="66dea-110">Creates an instance of the data service for each request.</span></span>

- <span data-ttu-id="66dea-111">要求資料服務處理傳入的要求。</span><span class="sxs-lookup"><span data-stu-id="66dea-111">Requests that the data service process the incoming request.</span></span>

- <span data-ttu-id="66dea-112">代表資料服務傳送回應。</span><span class="sxs-lookup"><span data-stu-id="66dea-112">Sends the response on behalf of the data service.</span></span>

 <span data-ttu-id="66dea-113">為了簡化資料服務的裝載，WCF Data Services 是設計來與 Windows Communication Foundation (WCF) 整合。</span><span class="sxs-lookup"><span data-stu-id="66dea-113">To simplify hosting a data service, WCF Data Services is designed to integrate with Windows Communication Foundation (WCF).</span></span> <span data-ttu-id="66dea-114">資料服務提供預設的 WCF 實作為 ASP.NET 應用程式中的資料服務主機。</span><span class="sxs-lookup"><span data-stu-id="66dea-114">The data service provides a default WCF implementation that serves as the data service host in an ASP.NET application.</span></span> <span data-ttu-id="66dea-115">因此，您可以透過下列其中一個方法來裝載資料服務：</span><span class="sxs-lookup"><span data-stu-id="66dea-115">Therefore, you can host a data service in one of the following ways:</span></span>

- <span data-ttu-id="66dea-116">在 ASP.NET 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="66dea-116">In an ASP.NET application.</span></span>

- <span data-ttu-id="66dea-117">在支援自我裝載之 WCF 服務的 Managed 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="66dea-117">In a managed application that supports self-hosted WCF services.</span></span>

- <span data-ttu-id="66dea-118">在某個其他自訂資料服務主機中。</span><span class="sxs-lookup"><span data-stu-id="66dea-118">In some other custom data service host.</span></span>

## <a name="hosting-a-data-service-in-an-aspnet-application"></a><span data-ttu-id="66dea-119">在 ASP.NET 應用程式中裝載資料服務</span><span class="sxs-lookup"><span data-stu-id="66dea-119">Hosting a Data Service in an ASP.NET Application</span></span>

<span data-ttu-id="66dea-120">當您使用 Visual Studio 2015 中的 [ **加入新專案** ] 對話方塊來定義 ASP.NET 應用程式中的資料服務時，此工具會在專案中產生兩個新檔案。</span><span class="sxs-lookup"><span data-stu-id="66dea-120">When you use the **Add New Item** dialog in Visual Studio 2015 to define a data service in an ASP.NET application, the tool generates two new files in the project.</span></span> <span data-ttu-id="66dea-121">第一個檔案的副檔名為 `.svc`，而且它會指示 WCF 執行階段如何具現化資料服務。</span><span class="sxs-lookup"><span data-stu-id="66dea-121">The first file has a `.svc` extension and instructs the WCF runtime how to instantiate the data service.</span></span> <span data-ttu-id="66dea-122">以下是您完成 [快速入門](quickstart-wcf-data-services.md)時所建立的 Northwind 範例資料服務的範例：</span><span class="sxs-lookup"><span data-stu-id="66dea-122">The following is an example of this file for the Northwind sample data service created when you complete the [quickstart](quickstart-wcf-data-services.md):</span></span>

```aspx-csharp
<%@ ServiceHost Language="C#"
    Factory="System.Data.Services.DataServiceHostFactory,
            System.Data.Services, Version=4.0.0.0,
            Culture=neutral, PublicKeyToken=b77a5c561934e089"
    Service="NorthwindService.Northwind" %>
```

 <span data-ttu-id="66dea-123">這個指示詞會告訴應用程式針對指名的資料服務類別建立服務主機，其方式是使用 <xref:System.Data.Services.DataServiceHostFactory> 類別。</span><span class="sxs-lookup"><span data-stu-id="66dea-123">This directive tells the application to create the service host for the named data service class by using the <xref:System.Data.Services.DataServiceHostFactory> class.</span></span>

 <span data-ttu-id="66dea-124">`.svc` 檔案的程式碼後置頁面包含資料服務本身之實作的類別，如下列 Northwind 範例資料服務所定義：</span><span class="sxs-lookup"><span data-stu-id="66dea-124">The code-behind page for the `.svc` file contains the class that is the implementation of the data service itself, which is defined as follows for the Northwind sample data service:</span></span>

 [!code-csharp[Astoria Quickstart Service#ServiceDefinition](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_quickstart_service/cs/northwind.svc.cs#servicedefinition)]
 [!code-vb[Astoria Quickstart Service#ServiceDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_quickstart_service/vb/northwind.svc.vb#servicedefinition)]

 <span data-ttu-id="66dea-125">因為資料服務的行為就像 WCF 服務，所以資料服務會與 ASP.NET 整合，並遵循 WCF Web 程式設計模型。</span><span class="sxs-lookup"><span data-stu-id="66dea-125">Because a data service behaves like a WCF service, the data service integrates with ASP.NET and follows the WCF Web programming model.</span></span> <span data-ttu-id="66dea-126">如需詳細資訊，請參閱 [Wcf 服務和 ASP.NET](../../wcf/feature-details/wcf-services-and-aspnet.md) 和 [wcf Web HTTP 程式設計模型](../../wcf/feature-details/wcf-web-http-programming-model.md)。</span><span class="sxs-lookup"><span data-stu-id="66dea-126">For more information, see [WCF Services and ASP.NET](../../wcf/feature-details/wcf-services-and-aspnet.md) and [WCF Web HTTP Programming Model](../../wcf/feature-details/wcf-web-http-programming-model.md).</span></span>

## <a name="self-hosted-wcf-services"></a><span data-ttu-id="66dea-127">自我裝載的 WCF 服務</span><span class="sxs-lookup"><span data-stu-id="66dea-127">Self-Hosted WCF Services</span></span>

 <span data-ttu-id="66dea-128">因為它包含 WCF 的執行，WCF Data Services 支援將資料服務自我裝載為 WCF 服務。</span><span class="sxs-lookup"><span data-stu-id="66dea-128">Because it incorporates a WCF implementation, WCF Data Services support self-hosting a data service as a WCF service.</span></span> <span data-ttu-id="66dea-129">服務可以在任何 .NET Framework 應用程式中自我裝載，例如主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="66dea-129">A service can be self-hosted in any .NET Framework application, such as a console application.</span></span> <span data-ttu-id="66dea-130">繼承自 <xref:System.Data.Services.DataServiceHost> 的 <xref:System.ServiceModel.Web.WebServiceHost> 類別是用來具現化特定位址上的資料服務。</span><span class="sxs-lookup"><span data-stu-id="66dea-130">The <xref:System.Data.Services.DataServiceHost> class, which inherits from <xref:System.ServiceModel.Web.WebServiceHost>, is used to instantiate the data service at a specific address.</span></span>

 <span data-ttu-id="66dea-131">自我裝載可用於開發及測試，因為它可更輕鬆地部署服務以及針對服務進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="66dea-131">Self-hosting can be used for development and testing because it can make it easier to deploy and troubleshoot the service.</span></span> <span data-ttu-id="66dea-132">不過，這種裝載不會提供 ASP.NET 所提供的 advanced 裝載和管理功能，也不會提供 (IIS) 的 Internet Information Services。</span><span class="sxs-lookup"><span data-stu-id="66dea-132">However, this kind of hosting does not provide the advanced hosting and management features provided by ASP.NET or by Internet Information Services (IIS).</span></span> <span data-ttu-id="66dea-133">如需詳細資訊，請參閱 [在 Managed 應用程式中裝載](../../wcf/feature-details/hosting-in-a-managed-application.md)。</span><span class="sxs-lookup"><span data-stu-id="66dea-133">For more information, see [Hosting in a Managed Application](../../wcf/feature-details/hosting-in-a-managed-application.md).</span></span>

## <a name="defining-a-custom-data-service-host"></a><span data-ttu-id="66dea-134">定義自訂資料服務主機</span><span class="sxs-lookup"><span data-stu-id="66dea-134">Defining a Custom Data Service Host</span></span>

 <span data-ttu-id="66dea-135">如果是 WCF 主機實作太具限制性的情況，您也可以為資料服務定義自訂主機。</span><span class="sxs-lookup"><span data-stu-id="66dea-135">For cases where the WCF host implementation is too restrictive, you can also define a custom host for a data service.</span></span> <span data-ttu-id="66dea-136">實作 <xref:System.Data.Services.IDataServiceHost> 介面的任何類別都可以當做資料服務的網路主機使用。</span><span class="sxs-lookup"><span data-stu-id="66dea-136">Any class that implements <xref:System.Data.Services.IDataServiceHost> interface can be used as the network host for a data service.</span></span> <span data-ttu-id="66dea-137">自訂主機必須實作 <xref:System.Data.Services.IDataServiceHost> 介面，而且必須能夠處理資料服務主機的下列基本責任：</span><span class="sxs-lookup"><span data-stu-id="66dea-137">A custom host must implement the <xref:System.Data.Services.IDataServiceHost> interface and be able to handle the following basic responsibilities of the data service host:</span></span>

- <span data-ttu-id="66dea-138">為資料服務提供服務根路徑。</span><span class="sxs-lookup"><span data-stu-id="66dea-138">Provide the data service with the service root path.</span></span>

- <span data-ttu-id="66dea-139">針對適當的 <xref:System.Data.Services.IDataServiceHost> 成員實作處理要求和回應標頭資訊。</span><span class="sxs-lookup"><span data-stu-id="66dea-139">Process request and response headers information to the appropriate <xref:System.Data.Services.IDataServiceHost> member implementation.</span></span>

- <span data-ttu-id="66dea-140">處理資料服務所引發的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="66dea-140">Handle exceptions raised by the data service.</span></span>

- <span data-ttu-id="66dea-141">驗證查詢字串中的參數。</span><span class="sxs-lookup"><span data-stu-id="66dea-141">Validate parameters in the query string.</span></span>

## <a name="see-also"></a><span data-ttu-id="66dea-142">另請參閱</span><span class="sxs-lookup"><span data-stu-id="66dea-142">See also</span></span>

- [<span data-ttu-id="66dea-143">定義 WCF 資料服務</span><span class="sxs-lookup"><span data-stu-id="66dea-143">Defining WCF Data Services</span></span>](defining-wcf-data-services.md)
- [<span data-ttu-id="66dea-144">將資料公開為服務</span><span class="sxs-lookup"><span data-stu-id="66dea-144">Exposing Your Data as a Service</span></span>](exposing-your-data-as-a-service-wcf-data-services.md)
- [<span data-ttu-id="66dea-145">設定資料服務</span><span class="sxs-lookup"><span data-stu-id="66dea-145">Configuring the Data Service</span></span>](configuring-the-data-service-wcf-data-services.md)
