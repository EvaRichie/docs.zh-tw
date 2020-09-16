---
title: 資料流處理提供者 (WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, providers
- WCF Data Services, binary data
- streaming data provider [WCF Data Services]
- WCF Data Services, streams
ms.assetid: f0978fe4-5f9f-42aa-a5c2-df395d7c9495
ms.openlocfilehash: 9ed728fa8d1d56c835aa27645a28921aa4f641e9
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90544449"
---
# <a name="streaming-provider-wcf-data-services"></a>資料流處理提供者 (WCF Data Services)

資料服務可以公開大型物件二進位資料。 這項二進位資料可能代表視訊和音訊資料流、影像、文件檔案，或其他類型的二進位媒體。 當資料模型中的實體包含一個或多個二進位屬性時，資料服務會在回應摘要的項目內，傳回這個 base-64 編碼形式的二進位資料。 因為以這種方式載入及序列化大型二進位資料會影響效能，所以開放式資料通訊協定 (OData) 會定義一種機制，以抓取與它所屬實體無關的二進位資料。 只要將實體中的二進位資料分成一個或多個資料流就可以完成這項處理。

- 媒體資源-屬於實體的二進位資料，例如影片、音訊、影像或其他類型的媒體資源資料流程。

- 媒體連結項目 - 具有相關媒體資源資料流之參考的實體。

使用 WCF Data Services，您可以藉由執行串流資料提供者來定義二進位資源資料流。 串流提供者實作為物件，提供資料服務與特定實體相關聯的媒體資源資料流程 <xref:System.IO.Stream> 。 這個實作可讓資料服務透過 HTTP 接受並傳回媒體資源當做指定之 MIME 類型的二進位資料流。

設定資料服務來支援二進位資料的資料流處理需要進行以下步驟：

1. 將資料模型中的一個或多個實體歸類為媒體連結項目。 這些實體不應該包含要進行資料流處理的二進位資料。 實體的任何二進位屬性一定會在此項目中以 base-64 二進位編碼形式傳回。

2. 實作 T:System.Data.Services.Providers.IDataServiceStreamProvider 介面。

3. 定義資料服務來實作 <xref:System.IServiceProvider> 介面。 此資料服務會使用 <xref:System.IServiceProvider.GetService%2A> 實作來存取資料流處理資料提供者實作。 這個方法會傳回適當的資料流處理提供者實作。

4. 在 Web 應用程式組態中啟用大型訊息資料流。

5. 啟用伺服器上或資料來源中之二進位資源的存取權。

本主題中的範例是以串流相片服務範例為基礎，在 [資料服務串流處理提供者系列中的深入探討：執行串流提供者 (第1部) ](/archive/blogs/astoriateam/data-services-streaming-provider-series-implementing-a-streaming-provider-part-1)。 您可以在 [GitHub](https://github.com/microsoftarchive/msdn-code-gallery-community-s-z/tree/master/Streaming%20Photo%20OData%20Service%20Sample)上取得串流相片資料服務範例的原始程式碼。

## <a name="defining-a-media-link-entry-in-the-data-model"></a>在資料模型中定義媒體連結項目

資料來源提供者會判斷實體定義為資料模型中媒體連結項目的方式。

**Entity Framework 提供者**

若要指出某個實體為媒體連結項目，請在概念模型中的實體類型定義內加上 `HasStream` 屬性，如下列範例所示：

[!code-xml[Astoria Photo Streaming Service#HasStream](../../../../samples/snippets/xml/VS_Snippets_Misc/astoria_photo_streaming_service/xml/photodata.edmx#hasstream)]

您也必須將命名空間 `xmlns:m=http://schemas.microsoft.com/ado/2007/08/dataservices/metadata` 加入至實體或定義資料模型之 .edmx 或 .csdl 檔案的根。

如需使用 Entity Framework 提供者並公開媒體資源的資料服務範例，請參閱 post [資料服務串流提供者系列：執行串流提供者 (第1部分) ](/archive/blogs/astoriateam/data-services-streaming-provider-series-implementing-a-streaming-provider-part-1)。

**反映提供者**

若要指出某個實體為媒體連結項目，請將 <xref:System.Data.Services.Common.HasStreamAttribute> 加入至在反映提供者內定義實體類型的類別。

**自訂資料服務提供者**

使用自訂服務提供者時，您必須實作 <xref:System.Data.Services.Providers.IDataServiceMetadataProvider> 介面來定義資料服務的中繼資料。 如需詳細資訊，請參閱 [自訂資料服務提供者](custom-data-service-providers-wcf-data-services.md)。 您可以在代表實體類型 (媒體連結項目) 的 <xref:System.Data.Services.Providers.ResourceType> 上，將 <xref:System.Data.Services.Providers.ResourceType.IsMediaLinkEntry%2A> 屬性設定為 `true`，藉以指出二進位資源資料流屬於 <xref:System.Data.Services.Providers.ResourceType>。

## <a name="implementing-the-idataservicestreamprovider-interface"></a>實作 IDataServiceStreamProvider 介面

若要建立支援二進位資料流的資料服務，您必須實作 <xref:System.Data.Services.Providers.IDataServiceStreamProvider> 介面。 這個實作可讓資料服務將二進位資料當做資料流傳回給用戶端，並將二進位資料當做從用戶端傳送的資料流來取用。 每當資料服務需要存取二進位資料當做資料流時，它就會建立此介面的執行個體。 <xref:System.Data.Services.Providers.IDataServiceStreamProvider> 介面會指定下列成員：

|成員名稱|描述|
|-----------------|-----------------|
|<xref:System.Data.Services.Providers.IDataServiceStreamProvider.DeleteStream%2A>|這個方法是由資料服務所叫用，在對應媒體資源的媒體連結項目遭到刪除時，一併刪除該媒體資源。 當您實作 <xref:System.Data.Services.Providers.IDataServiceStreamProvider> 時，這個方法所包含的程式碼會刪除與提供之媒體連結項目相關聯的媒體資源。|
|<xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetReadStream%2A>|這個方法是由資料服務所叫用，以便將媒體資源當做資料流傳回。 當您實作 <xref:System.Data.Services.Providers.IDataServiceStreamProvider> 時，這個方法所包含的程式碼會提供資料服務所使用的資料流，以便傳回與提供之媒體連結項目相關聯的媒體資源。|
|<xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetReadStreamUri%2A>|這個方法是由資料服務所叫用，以便傳回用來要求媒體連結項目之媒體資源的 URI。 這個值是用來在媒體連結項目的內容項目中建立 `src` 屬性，也可用來要求資料流。 當此方法傳回 `null` 時，資料服務就會自動決定 URI。 當您必須為用戶端提供二進位資料的直接存取權，而不使用資料流提供者時，請使用此方法。|
|<xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetStreamContentType%2A>|這個方法是由資料服務所叫用，以便傳回與指定之媒體連結項目相關聯之媒體資源的 Content-Type 值。|
|<xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetStreamETag%2A>|這個方法是由資料服務所叫用，以便傳回與指定之實體相關聯之資料流的 eTag。 當您管理二進位資料的並行時，將會使用這個方法。 當這個方法傳回 null 時，資料服務不會追蹤並行。|
|<xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetWriteStream%2A>|這個方法是由資料服務所叫用，可取得當接收從用戶端傳送的資料流時所使用的資料流。 當您實作 <xref:System.Data.Services.Providers.IDataServiceStreamProvider> 時，您必須傳回可寫入的資料流，資料服務會將接收的資料流資料寫入其中。|
|<xref:System.Data.Services.Providers.IDataServiceStreamProvider.ResolveType%2A>|傳回命名空間限定的型別名稱，代表資料服務執行階段必須為媒體連結項目建立的類型，該連結項目與正在插入之媒體資源的資料流相關聯。|

## <a name="creating-the-streaming-data-service"></a>建立資料流處理資料服務

若要提供可存取執行的 WCF Data Services 執行時間 <xref:System.Data.Services.Providers.IDataServiceStreamProvider> ，您所建立的資料服務也必須執行 <xref:System.IServiceProvider> 介面。 下列範例將示範如何實作 <xref:System.IServiceProvider.GetService%2A> 方法來傳回實作 `PhotoServiceStreamProvider` 之 <xref:System.Data.Services.Providers.IDataServiceStreamProvider> 類別的執行個體。

[!code-csharp[Astoria Photo Streaming Service#PhotoServiceStreamingProvider](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_photo_streaming_service/cs/photodata.svc.cs#photoservicestreamingprovider)]
[!code-vb[Astoria Photo Streaming Service#PhotoServiceStreamingProvider](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_photo_streaming_service/vb/photodata.svc.vb#photoservicestreamingprovider)]

如需有關如何建立資料服務的一般資訊，請參閱設定 [資料服務](configuring-the-data-service-wcf-data-services.md)。

## <a name="enabling-large-binary-streams-in-the-hosting-environment"></a>在裝載環境中啟用大型二進位資料流

當您在 ASP.NET Web 應用程式中建立資料服務時，會使用 Windows Communication Foundation (WCF) 來提供 HTTP 通訊協定的執行。 根據預設，WCF 會將 HTTP 訊息的大小限制為只有 65 KB。 為了要能夠與資料服務之間來回進行大型二進位資料的資料流處理，您也必須設定 Web 應用程式啟用大型二進位檔案及使用資料流進行傳輸。 若要這樣做，請在應用程式 Web.config 檔案的 `<configuration />` 項目中加入下列程式碼：

> [!NOTE]
> 您必須使用 <xref:System.ServiceModel.TransferMode.Streamed?displayProperty=nameWithType> 傳輸模式，以確保要求和回應訊息中的二進位資料會經過資料流程處理，而不會由 WCF 進行緩衝處理。

如需詳細資訊，請參閱 [串流訊息傳輸](../../wcf/feature-details/streaming-message-transfer.md) 和 [傳輸配額](../../wcf/feature-details/transport-quotas.md)。

根據預設，Internet Information Services (IIS) 也會將要求的大小限制為 4 MB。 若要讓您的資料服務在 IIS 上執行時接收大於 4 MB 的資料流程，您也必須 `maxRequestLength` 在設定區段中設定 [HTTPRuntime 元素 (ASP.NET 設定架構) ](/previous-versions/dotnet/netframework-4.0/e1f13641(v=vs.100)) 的屬性 `<system.web />` ，如下列範例所示：

## <a name="using-data-streams-in-a-client-application"></a>在用戶端應用程式中使用資料流

WCF Data Services 用戶端程式庫可讓您在用戶端上將這些公開的資源當作二進位資料流程來取得和更新。 如需詳細資訊，請參閱 [使用二進位資料](working-with-binary-data-wcf-data-services.md)。

## <a name="considerations-for-working-with-a-streaming-provider"></a>使用資料流處理提供者的考量

下列是當您實作資料流處理提供者以及從資料服務存取媒體資源時，所要考量的事項。

- 媒體資源不支援 MERGE 要求。 使用 PUT 要求可變更現有實體的媒體資源。

- POST 要求不能用來建立新的媒體連結項目。 您必須改為發出 POST 要求來建立新的媒體資源，而資料服務會使用預設值建立新的媒體連結項目。 後續的 MERGE 或 PUT 要求可以更新這個新的實體。 您也可以考慮快取實體，並在處置工具中進行更新，例如將屬性值設定為 POST 要求中 Slug 標頭的值。

- 當收到 POST 要求時，資料服務會呼叫 <xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetWriteStream%2A> 來建立媒體資源，然後再呼叫 <xref:System.Data.Services.IUpdatable.SaveChanges%2A> 建立媒體連結項目。

- <xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetWriteStream%2A> 的實作不應該傳回 <xref:System.IO.MemoryStream> 物件。 當您使用這種資料流時，服務收到非常大型的資料流時將會發生記憶體資源問題。

- 以下是將媒體資源儲存在資料庫時所要考量的事項：

  - 屬於媒體資源的二進位屬性不應該包含在資料模型中。 資料模型中公開的所有屬性都會在回應摘要的項目中傳回。

  - 為了改良大型二進位資料流的效能，我們建議您最好建立自訂資料流類別，將二進位資料儲存在資料庫中。 這個類別是由 <xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetWriteStream%2A> 實作所傳回，而且會以區塊傳送二進位資料給資料庫。 若為 SQL Server 資料庫，我們建議您在二進位資料超過 1 MB 時，使用 FILESTREAM 將資料串流至資料庫。

  - 請確定資料庫設計為可儲存二進位大型資料流，而且您的資料服務將會收到這些資料流。

  - 當用戶端傳送 POST 要求，將包含媒體資源的媒體連結項目插入單一要求時，將會呼叫 <xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetWriteStream%2A> 來取得資料流，然後資料服務才會將新的實體插入資料庫中。 資料流處理提供者實作必須能夠處理這個資料服務行為。 請考慮使用個別的資料表來儲存二進位資料或是將資料流儲存在檔案中，直到實體已經插入資料庫為止。

- 當您實作 <xref:System.Data.Services.Providers.IDataServiceStreamProvider.DeleteStream%2A>、<xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetReadStream%2A> 或 <xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetWriteStream%2A> 方法時，您必須使用當做方法參數提供的 eTag 和 Content-Type 值。 請勿在 <xref:System.Data.Services.Providers.IDataServiceStreamProvider> 提供者實作中設定 eTag 或 Content-Type 標頭。

- 根據預設，用戶端會使用區塊式 HTTP Transfer-Encoding 來傳送大型二進位資料流。 因為 ASP.NET 程式開發伺服器不支援這種編碼方式，所以您無法使用此 Web 服務器來裝載必須接受大型二進位資料流程的資料流程處理資料服務。 如需 ASP.NET 程式開發伺服器的詳細資訊，請參閱 [Visual Studio 中的網頁伺服器以 ASP.NET Web 專案](/previous-versions/aspnet/58wxa9w5(v=vs.120))。

<a name="versioning"></a>

## <a name="versioning-requirements"></a>版本控制需求

串流提供者具有下列 OData 通訊協定版本控制需求：

- 串流提供者要求資料服務支援2.0 版的 OData 通訊協定和更新版本。

如需詳細資訊，請參閱 [資料服務版本控制](data-service-versioning-wcf-data-services.md)。

## <a name="see-also"></a>另請參閱

- [資料服務提供者](data-services-providers-wcf-data-services.md)
- [自訂資料服務提供者](custom-data-service-providers-wcf-data-services.md)
- [使用二進位資料](working-with-binary-data-wcf-data-services.md)
