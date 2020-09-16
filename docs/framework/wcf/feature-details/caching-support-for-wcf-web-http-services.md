---
title: WCF Web HTTP 服務的快取支援
ms.date: 03/30/2017
ms.assetid: 7f8078e0-00d9-415c-b8ba-c1b6d5c31799
ms.openlocfilehash: 0445f0214f90873dad4241789db270c9b6f4a2f6
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90559411"
---
# <a name="caching-support-for-wcf-web-http-services"></a>WCF Web HTTP 服務的快取支援

[!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] 可讓您使用 WCF Web HTTP 服務的 ASP.NET 中已提供的宣告式快取機制。 這可讓您快取來自 WCF Web HTTP 服務作業的回應。 當使用者傳送 HTTP GET 至您設為快取的服務時，ASP.NET 會傳回快取的回應，且不會呼叫服務方法。 當快取逾期後，下次使用者傳送 HTTP GET 時，會呼叫您的服務方法且再次快取回應。 如需 ASP.NET 快取的詳細資訊，請參閱 ASP.NET 快取 [總覽](/previous-versions/aspnet/ms178597(v=vs.100))。  
  
## <a name="basic-web-http-service-caching"></a>基本 Web HTTP 服務快取  

  若要啟用 WEB HTTP 服務快取，您必須先將套用 <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsAttribute> 至服務設定至或，以啟用 ASP.NET 相容性 <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsAttribute.RequirementsMode%2A> <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode.Allowed> <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode.Required> 。  
  
 .NET Framework 4 導入了名為 <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute> 的新屬性，可讓您指定快取設定檔名稱。 此屬性便會套用至服務作業。 下列範例套用 <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsAttribute> 至服務來啟用 ASP.NET 相容性並設定 `GetCustomer` 快取作業。 <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute> 屬性會指定包含要使用之快取設定的快取設定檔。  
  
```csharp
[ServiceContract]
[AspNetCompatibilityRequirements(RequirementsMode=AspNetCompatibilityRequirementsMode.Allowed)]
public class Service
{
    [WebGet(UriTemplate = "{id}")]
    [AspNetCacheProfile("CacheFor60Seconds")]
    public Customer GetCustomer(string id)
    {
        // ...
    }
}
```  
  
此外，請在 Web.config 檔案中開啟 ASP.NET 相容性模式，如下列範例所示。  
  
```xml
<system.serviceModel>
  <serviceHostingEnvironment aspNetCompatibilityEnabled="true" />
</system.serviceModel>
```
  
> [!WARNING]
> 如果未開啟 ASP.NET 相容性模式且使用 <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute>，就會擲回例外狀況。  
  
 由 <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute> 指定的快取設定檔名稱會識別加入至 Web.config 組態檔的快取設定檔。 快取設定檔會在 <的> 元素中定義， `outputCacheSetting` 如下列設定範例所示。  
  
```xml
<!-- ...  -->
<system.web>  
   <caching>  
      <outputCacheSettings>  
         <outputCacheProfiles>  
            <add name="CacheFor60Seconds" duration="60" varyByParam="none" sqlDependency="MyTestDatabase:MyTable"/>  
         </outputCacheProfiles>  
      </outputCacheSettings>  
   </caching>  
   <!-- ... -->  
</system.web>  
```  
  
 此組態項目與 ASP.NET 應用程式所使用的項目相同。 如需 ASP.NET 快取設定檔的詳細資訊，請參閱 <xref:System.Web.Configuration.OutputCacheProfile> 。 若是 Web HTTP 服務，快取設定檔中最重要的屬性是：`cacheDuration` 和 `varyByParam`。 這兩個屬性都是必要項。 `cacheDuration` 可設定應快取回應的時間 (以秒為單位)。 `varyByParam` 可讓您指定用來快取回應的查詢字串參數。 使用不同查詢字串參數值所執行的所有請求會分別快取。 例如，在初始要求提出之後 `http://MyServer/MyHttpService/MyOperation?param=10` ，所有使用相同 URI 提出的後續要求都會傳回快取的回應 (只要快取持續時間尚未經過) 。 請求相似但對參數查詢字串參數有不同值的回應會分別快取。 如果您不想要此分別快取行為，請將 `varyByParam` 設為 "none"。  
  
## <a name="sql-cache-dependency"></a>SQL 快取相依性  

  Web HTTP 服務回應也可使用 SQL 快取相依性來加以快取。 如果您的 WCF Web HTTP 服務依賴儲存在 SQL 資料庫中的資料，您可能需要快取服務的回應，並在 SQL 資料庫資料表中的資料變更時，使快取的回應失效。 此行為會完全在 Web.config 檔案中設定完成。 首先，在 <> 元素中定義連接字串 `connectionStrings` 。  
  
```xml
<connectionStrings>
  <add name="connectString"
       connectionString="Data Source=MyService;Initial Catalog=MyTestDatabase;Integrated Security=True"
       providerName="System.Data.SqlClient" />
</connectionStrings>
```  
  
 然後，您必須在 <> 元素內的 <> 元素內啟用 SQL 快取相依性， `caching` `system.web` 如下列設定範例所示。  
  
```xml  
<system.web>
  <caching>
    <sqlCacheDependency enabled="true" pollTime="1000">
      <databases>
        <add name="MyTestDatabase" connectionStringName="connectString" />
      </databases>
    </sqlCacheDependency>
    <!-- ... -->
  </caching>
  <!-- ... -->
</system.web>
```  
  
 SQL 快取相依性會在此處啟用，且輪詢時間設為 1000 毫秒。 每次輪詢時間結束時，就會檢查資料庫資料表是否已更新。 如果偵測到變更就會移除快取的內容，並於下次叫用服務作業時快取新的回應。 在 <的 `sqlCacheDependency`> 專案中，加入資料庫，並參考 <> 元素內的連接字串， `databases` 如下列範例所示。  
  
```xml  
<system.web>
  <caching>
    <sqlCacheDependency enabled="true" pollTime="1000">
      <databases>
        <add name="MyTestDatabase" connectionStringName="connectString" />
      </databases>  
    </sqlCacheDependency>  
    <!-- ... -->  
  </caching>  
  <!-- ... -->  
</system.web>  
```  
  
 接下來，您必須在 <> 元素內設定輸出快取設定， `caching` 如下列範例所示。  
  
```xml
<system.web>
  <caching>  
    <!-- ...  -->
    <outputCacheSettings>
      <outputCacheProfiles>
        <add name="CacheFor60Seconds" duration="60" varyByParam="none" sqlDependency="MyTestDatabase:MyTable" />
      </outputCacheProfiles>
    </outputCacheSettings>
  </caching>
  <!-- ... -->
</system.web>
```  
  
 快取持續時間設為60秒、 `varyByParam` 設定為 [無]，並 `sqlDependency` 設定為以分號分隔的資料庫名稱/資料表配對清單（以冒號分隔）。 當 `MyTable` 中的資料變更就會移除服務作業的已快取回應，而當叫用作業時，就會產生 (以呼叫服務作業的方式) 及快取新的回應並傳回至用戶端。  
  
> [!IMPORTANT]
> 若要讓 ASP.NET 存取 SQL database，您必須使用 [ASP.NET SQL Server 註冊工具](/previous-versions/dotnet/netframework-3.5/ms229862(v=vs.90))。 除此之外，您必須允許適當的使用者帳戶存取資料庫和資料表。 如需詳細資訊，請參閱 [從 Web 應用程式存取 SQL Server](/previous-versions/aspnet/ht43wsex(v=vs.100))。  
  
## <a name="conditional-http-get-based-caching"></a>條件式 HTTP GET 型快取  

  在 Web HTTP 案例中，條件式 HTTP GET 通常會由服務用來依照 [HTTP 規格](https://www.w3.org/Protocols/rfc2616/rfc2616.html)中所述的方式來執行智慧型 HTTP 快取。 若要這樣做，服務必須設定 HTTP 回應中的 ETag 標頭值。 服務也必須檢查 HTTP 請求中的 If-None-Match 標頭，確認是否有任何指定的 ETag 符合目前的 ETag。  
  
 若是 GET 和 HEAD 請求，<xref:System.ServiceModel.Web.IncomingWebRequestContext.CheckConditionalRetrieve%2A> 會使用 ETag 值並將它和請求的 If-None-Match 標頭比對。 如果標頭存在，而且有相符的，則會擲回 <xref:System.ServiceModel.Web.WebFaultException> 具有 HTTP 狀態碼 304 (未修改) ，並將 etag 標頭新增至具有相符 ETag 的回應。  
  
 <xref:System.ServiceModel.Web.IncomingWebRequestContext.CheckConditionalRetrieve%2A> 方法的一個多載會使用上次修改的日期並將它和請求的 If-Modified-Since 標頭比對。 如果有標頭且尚未修改資源，就會擲回含有 HTTP 狀態碼 304 (未修改) 的<xref:System.ServiceModel.Web.WebFaultException>。  
  
 針對 PUT、POST 和 DELETE 請求，<xref:System.ServiceModel.Web.IncomingWebRequestContext.CheckConditionalUpdate%2A> 會使用資源目前的 ETag 值。 如果目前的 ETag 值為 null，則此方法會檢查 If-match 標頭的值是否為 "*"。  如果目前的 ETag 值不是預設值，那麼方法就會將目前的 ETag 值和請求的 If- Match 標頭比對。 不論那一種情況，如果預期的標頭不在請求中，或其值無法滿足條件式檢查時，方法都會擲回含有 HTTP 狀態碼 412 (前置條件失敗) 的<xref:System.ServiceModel.Web.WebFaultException>，並將回應的 ETag 標頭設為目前的 ETag 值。  
  
 這兩個 `CheckConditional` 方法和 <xref:System.ServiceModel.Web.OutgoingWebResponseContext.SetETag%2A> 方法可確保在回應標頭上設定的 ETag 值，根據 HTTP 規格，為有效的 ETag 值。 如果雙引號不是已存在且未正確逸出任何內部雙引號字元時，就會將 ETag 值以雙引號括住。 不支援弱式 ETag 比較。  
  
 下列範例示範如何使用這些方法。  
  
```csharp
[WebGet(UriTemplate = "{id}"), Description("Returns the specified customer from customers collection. Returns NotFound if there is no such customer. Supports conditional GET.")]
public Customer GetCustomer(string id)
{
    lock (writeLock)
    {
        // return NotFound if there is no item with the specified id.
        object itemEtag = customerEtags[id];
        if (itemEtag == null)
        {
            throw new WebFaultException(HttpStatusCode.NotFound);
        }
  
        // return NotModified if the client did a conditional GET and the customer item has not changed
        // since when the client last retrieved it
        WebOperationContext.Current.IncomingRequest.CheckConditionalRetrieve((long)itemEtag);
        Customer result = this.customers[id] as Customer;

        // set the customer etag before returning the result
        WebOperationContext.Current.OutgoingResponse.SetETag((long)itemEtag);
        return result;
    }
}
```  
  
## <a name="security-considerations"></a>安全性考量  
 需要權限的要求不得快取其回應，因為從快取提供回應時，不會執行授權。  快取此類回應會導致嚴重的安全性弱點。  需要授權的要求通常會提供使用者專屬的資料，因此伺服器端快取甚至沒有任何好處。  在此類情況下，用戶端快取或完全不快取將更為適當。
