---
title: System.Web.Routing 整合
ms.date: 03/30/2017
ms.assetid: 31fe2a4f-5c47-4e5d-8ee1-84c524609d41
ms.openlocfilehash: 6e67aa4a790edeb367b099d4a94f465f1e7b9bcc
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90554771"
---
# <a name="systemwebrouting-integration"></a>System.Web.Routing 整合
在 Internet Information Service 中裝載 Windows Communication Foundation (WCF) 服務 (IIS) 您在虛擬目錄中放置 .svc 檔案。 此 .svc 檔案會指定要使用的服務主機處理站，以及實作服務的類別。 對服務提出要求時，您會在 URI 中指定 .svc 檔案，例如： `http://contoso.com/EmployeeServce.svc` 。 對於撰寫 REST 服務的程式設計人員而言，此類型的 URI 不是最佳的方法。 REST 服務的 URI 會指定特定資源，且一般來說沒有任何擴充。 <xref:System.Web.Routing>整合功能可讓您裝載 WCF REST 服務，以回應沒有副檔名的 uri。 如需路由的詳細資訊，請參閱 [ASP.NET 路由](/previous-versions/aspnet/cc668201(v=vs.100))。  
  
## <a name="using-systemwebrouting-integration"></a>使用 System.Web.Routing 整合  
 若要使用 <xref:System.Web.Routing> 整合功能，請使用 <xref:System.ServiceModel.Activation.ServiceRoute> 類別建立一個或多個路由，並且將路由加入至 Global.asax 檔案中的 <xref:System.Web.Routing.RouteTable>。 這些路由會指定服務回應的相對 URI。 下列範例示範如何執行。  
  
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
  
 這會將含有相對 URI 以 Customers 開頭的所有要求路由至 `Service` 服務。  
  
 在 Web.config 檔案中，您必須加入 `System.Web.Routing.UrlRoutingModule` 模組、將 `runAllManagedModulesForAllRequests`屬性設定為 `true`，並且將 `UrlRoutingHandler` 處理常式加入至 `<system.webServer>` 項目，如下列範例所示。  
  
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
  
 這會載入路由需要的模組與處理常式。 如需詳細資訊，請參閱[路由](routing.md)。 您也必須在 `aspNetCompatibilityEnabled` 項目中，將 `true` 屬性設定為 `<serviceHostingEnvironment>`，如下列範例所示。  
  
```xml  
<system.serviceModel>  
    <serviceHostingEnvironment aspNetCompatibilityEnabled="true"/>  
        <!-- ... -->  
    </system.serviceModel>  
```  
  
 實作服務的類別必須啟用 ASP.NET 相容性需求，如下列範例所示。  
  
```csharp
[ServiceContract]  
[AspNetCompatibilityRequirements(RequirementsMode=AspNetCompatibilityRequirementsMode.Allowed)]  
    public class Service  
    {  
        // ...  
    }  
```  
  
## <a name="see-also"></a>另請參閱

- [WCF Web HTTP 程式設計模型](wcf-web-http-programming-model.md)
- [ASP.NET 路由](/previous-versions/aspnet/cc668201(v=vs.100))
