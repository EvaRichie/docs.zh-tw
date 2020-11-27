---
title: System.Web.Routing 整合
ms.date: 03/30/2017
ms.assetid: 31fe2a4f-5c47-4e5d-8ee1-84c524609d41
ms.openlocfilehash: bb820f535a69a24e05b7374bcf97539ae2b87aef
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96266424"
---
# <a name="systemwebrouting-integration"></a><span data-ttu-id="3e569-102">System.Web.Routing 整合</span><span class="sxs-lookup"><span data-stu-id="3e569-102">System.Web.Routing Integration</span></span>

<span data-ttu-id="3e569-103">在 Internet Information Service 中裝載 Windows Communication Foundation (WCF) 服務 (IIS) 您在虛擬目錄中放置 .svc 檔案。</span><span class="sxs-lookup"><span data-stu-id="3e569-103">When hosting a Windows Communication Foundation (WCF) service in Internet Information Service (IIS) you place a .svc file in the virtual directory.</span></span> <span data-ttu-id="3e569-104">此 .svc 檔案會指定要使用的服務主機處理站，以及實作服務的類別。</span><span class="sxs-lookup"><span data-stu-id="3e569-104">This .svc file specifies the service host factory to use as well as the class that implements the service.</span></span> <span data-ttu-id="3e569-105">對服務提出要求時，您會在 URI 中指定 .svc 檔案，例如： `http://contoso.com/EmployeeServce.svc` 。</span><span class="sxs-lookup"><span data-stu-id="3e569-105">When making requests to the service you specify the .svc file in the URI, for example: `http://contoso.com/EmployeeServce.svc`.</span></span> <span data-ttu-id="3e569-106">對於撰寫 REST 服務的程式設計人員而言，此類型的 URI 不是最佳的方法。</span><span class="sxs-lookup"><span data-stu-id="3e569-106">For programmers writing REST services, this type of URI is not optimal.</span></span> <span data-ttu-id="3e569-107">REST 服務的 URI 會指定特定資源，且一般來說沒有任何擴充。</span><span class="sxs-lookup"><span data-stu-id="3e569-107">URIs for REST services specify a specific resource and normally do not have any extensions.</span></span> <span data-ttu-id="3e569-108"><xref:System.Web.Routing>整合功能可讓您裝載 WCF REST 服務，以回應沒有副檔名的 uri。</span><span class="sxs-lookup"><span data-stu-id="3e569-108">The <xref:System.Web.Routing> integration feature allows you to host a WCF REST service that responds to URIs without an extension.</span></span> <span data-ttu-id="3e569-109">如需路由的詳細資訊，請參閱 [ASP.NET 路由](/previous-versions/aspnet/cc668201(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="3e569-109">For more information about routing see [ASP.NET Routing](/previous-versions/aspnet/cc668201(v=vs.100)).</span></span>  
  
## <a name="using-systemwebrouting-integration"></a><span data-ttu-id="3e569-110">使用 System.Web.Routing 整合</span><span class="sxs-lookup"><span data-stu-id="3e569-110">Using System.Web.Routing Integration</span></span>  

 <span data-ttu-id="3e569-111">若要使用 <xref:System.Web.Routing> 整合功能，請使用 <xref:System.ServiceModel.Activation.ServiceRoute> 類別建立一個或多個路由，並且將路由加入至 Global.asax 檔案中的 <xref:System.Web.Routing.RouteTable>。</span><span class="sxs-lookup"><span data-stu-id="3e569-111">To use the <xref:System.Web.Routing> integration feature, you use the <xref:System.ServiceModel.Activation.ServiceRoute> class to create one or more routes and add them to the <xref:System.Web.Routing.RouteTable> in a Global.asax file.</span></span> <span data-ttu-id="3e569-112">這些路由會指定服務回應的相對 URI。</span><span class="sxs-lookup"><span data-stu-id="3e569-112">These routes specify the relative URIs that the service responds to.</span></span> <span data-ttu-id="3e569-113">下列範例示範如何執行。</span><span class="sxs-lookup"><span data-stu-id="3e569-113">The following example shows how to do this.</span></span>  
  
```aspx-csharp  
<%@ Application Language="C#" %>  
<%@ Import Namespace="System.Web.Routing" %>  
<%@ Import Namespace="System.ServiceModel.Activation" %>  
<%@ Import Namespace="System.ServiceModel.Web " %>  
  
<script RunAt="server">  
    void Application_Start(object sender, EventArgs e)  
    {  
        RegisterRoutes(RouteTable.Routes);  
    }  
  
    private void RegisterRoutes(RouteCollection routes)  
    {  
        routes.Add(new ServiceRoute("Customers", new WebServiceHostFactory(), typeof(Service)));
   }  
</script>  
```  
  
 <span data-ttu-id="3e569-114">這會將含有相對 URI 以 Customers 開頭的所有要求路由至 `Service` 服務。</span><span class="sxs-lookup"><span data-stu-id="3e569-114">This routes all requests with a relative URI that begins with Customers to the `Service` service.</span></span>  
  
 <span data-ttu-id="3e569-115">在 Web.config 檔案中，您必須加入 `System.Web.Routing.UrlRoutingModule` 模組、將 `runAllManagedModulesForAllRequests`屬性設定為 `true`，並且將 `UrlRoutingHandler` 處理常式加入至 `<system.webServer>` 項目，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="3e569-115">In your Web.config file you must add the `System.Web.Routing.UrlRoutingModule` module, set the `runAllManagedModulesForAllRequests` attribute to `true`, and add the `UrlRoutingHandler` handler to the `<system.webServer>` element as shown in the following example.</span></span>  
  
```xml  
<system.webServer>  
      <modules runAllManagedModulesForAllRequests="true">  
        <add name="UrlRoutingModule" type="System.Web.Routing.UrlRoutingModule, System.Web, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a" />  
      </modules>  
      <handlers>  
        <add name="UrlRoutingHandler" preCondition="integratedMode" verb="*" path="UrlRouting.axd"/>  
      </handlers>  
    </system.webServer>  
```  
  
 <span data-ttu-id="3e569-116">這會載入路由需要的模組與處理常式。</span><span class="sxs-lookup"><span data-stu-id="3e569-116">This loads a module and handler required for routing.</span></span> <span data-ttu-id="3e569-117">如需詳細資訊，請參閱[路由](routing.md)。</span><span class="sxs-lookup"><span data-stu-id="3e569-117">For more information, see [Routing](routing.md).</span></span> <span data-ttu-id="3e569-118">您也必須在 `aspNetCompatibilityEnabled` 項目中，將 `true` 屬性設定為 `<serviceHostingEnvironment>`，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="3e569-118">You must also set the `aspNetCompatibilityEnabled` attribute to `true` in the `<serviceHostingEnvironment>` element as shown in the following example.</span></span>  
  
```xml  
<system.serviceModel>  
    <serviceHostingEnvironment aspNetCompatibilityEnabled="true"/>  
        <!-- ... -->  
    </system.serviceModel>  
```  
  
 <span data-ttu-id="3e569-119">實作服務的類別必須啟用 ASP.NET 相容性需求，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="3e569-119">The class that implements the service must enable ASP.NET compatibility requirements as shown in the following example.</span></span>  
  
```csharp
[ServiceContract]  
[AspNetCompatibilityRequirements(RequirementsMode=AspNetCompatibilityRequirementsMode.Allowed)]  
    public class Service  
    {  
        // ...  
    }  
```  
  
## <a name="see-also"></a><span data-ttu-id="3e569-120">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3e569-120">See also</span></span>

- [<span data-ttu-id="3e569-121">WCF Web HTTP 程式設計模型</span><span class="sxs-lookup"><span data-stu-id="3e569-121">WCF Web HTTP Programming Model</span></span>](wcf-web-http-programming-model.md)
- <span data-ttu-id="3e569-122">[ASP.NET 路由](/previous-versions/aspnet/cc668201(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="3e569-122">[ASP.NET Routing](/previous-versions/aspnet/cc668201(v=vs.100))</span></span>
