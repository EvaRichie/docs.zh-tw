---
title: 建立 ASP.NET AJAX 的 WCF 服務
ms.date: 03/30/2017
ms.assetid: 04c0402c-e617-4ba5-aedf-d17692234776
ms.openlocfilehash: 8c82d4c61b32572fd1ad7d8f19e939273cc2280b
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84599304"
---
# <a name="creating-wcf-services-for-aspnet-ajax"></a>建立 ASP.NET AJAX 的 WCF 服務

Microsoft ASP.NET AJAX 可讓您使用反應靈敏和熟悉的使用者介面項目，快速建立包含豐富使用者經驗的 Web 網頁。 ASP.NET AJAX 提供用戶端指令碼的程式庫，其中加入跨平台的 ECMAScript (JavaScript) 和動態 HTML (DHTML) 技術，並將它們與 ASP.NET 2.0 伺服器基礎的開發平台整合。 您可以使用 ASP.NET AJAX 功能來改善使用者經驗和 Web 應用程式的效率。

ASP.NET AJAX 包含內建的用戶端指令碼程式庫與伺服器元件，以提供您穩固的開發架構。 若要從 ASP.NET 頁面存取服務：一旦服務 URL 新增至頁面上的 ASP.NET 指令碼管理員控制項，服務作業可能會透過看起來與正常 JavaScript 函式呼叫沒兩樣的 JavaScript 程式碼來叫用。

大部分的 Windows Communication Foundation （WCF）服務可能會藉由新增適當的 ASP.NET AJAX 端點，公開為與 ASP.NET AJAX 相容的服務。

如果您使用 Visual Studio，您可以針對啟用 AJAX 的 WCF 服務使用預先建立的範本，在使用 ASP.NET 網站或 Web 應用程式時，可以在 [**加入新專案**] 對話方塊中找到。

如果您不是使用 Visual Studio 範本，則您可以透過下列兩種方法來建立 ASP.NET AJAX 端點：

- 使用動態主機啟動 (而不是透過任何組態) 來建立端點。 如果您不熟悉 WCF 組態系統的話，這是最基本的操作方式。 如需詳細資訊，請參閱[如何：新增 ASP.NET AJAX 端點而不使用](how-to-add-an-aspnet-ajax-endpoint-without-using-configuration.md)設定。

- 使用設定，將啟用 AJAX 的端點新增至 WCF 服務。 如需詳細資訊，請參閱[如何：使用設定來新增 ASP.NET AJAX 端點](how-to-use-configuration-to-add-an-aspnet-ajax-endpoint.md)。

[WCF WEB HTTP 程式設計模型總覽](wcf-web-http-programming-model-overview.md)中所述的 Web 程式設計模型，可搭配 ASP.NET AJAX services 使用。 具體來說：

- 您可以使用 <xref:System.ServiceModel.Web.WebGetAttribute> 和 <xref:System.ServiceModel.Web.WebInvokeAttribute> 屬性，在 HTTP GET 和 HTTP POST 動詞之間進行選擇。 如果使用方式正確的話，可能會大幅改善應用程式的效能。 如需詳細資訊，請參閱 how [to：選擇 HTTP POST 和 HTTP GET 要求以 ASP.NET AJAX 端點](http-post-and-http-get-requests-for-aspnet-ajax-endpoints.md)。

- 您可以使用 <xref:System.ServiceModel.Web.WebGetAttribute.ResponseFormat%2A> 和 <xref:System.ServiceModel.Web.WebInvokeAttribute.ResponseFormat%2A> 屬性，讓您的服務傳回 XML 資料，而不是預設的 JavaScript Object Notation (JSON)。 使用 ASP.NET AJAX 架構來執行這項作業會導致 JavaScript 用戶端接收 XML DOM 物件。

  > [!WARNING]
  > 您的作業必須將內容類型設定為文字/xml，才能讓此作業運作。 否則，JavaScript 用戶端將收到包含 XML 物件 (而非 XML DOM 物件) 的字串。

    以下是內容類型設定正確時，傳回 XML 資料的範例：

  ```csharp
  [OperationContract, WebGet(ResponseFormat=WebMessageFormat.Xml)]
  public XElement GetData()
  {
      XElement x;
      //Get some data here...

      WebOperationContext.Current.OutgoingResponse.ContentType = "text/xml";
      return x;
  }
  ```

- 如需與 ASP.NET AJAX 相容，則 <xref:System.ServiceModel.Web.WebGetAttribute> 和 <xref:System.ServiceModel.Web.WebInvokeAttribute> 屬性 (Attribute) 上的其他屬性 (Property) 都將無法變更。 只要不違反 ASP.NET AJAX 呼叫慣例的話，就可以一直使用其他的 Web 程式設計模型方式。

 更先進的案例需要瞭解 WCF 中的其他 AJAX 支援詳細資料：

- 若要瞭解如何使用 JavaScript 在 AJAX 頁面用戶端與 WCF 服務之間傳輸資料，以及有關 .NET Framework 類型如何對應至 JavaScript 類型的詳細資訊，請參閱[JSON 和其他資料傳輸格式的支援](support-for-json-and-other-data-transfer-formats.md)。

- 為了善加利用各項 ASP.NET 功能，例如 URL 驗證與存取 ASP.NET 工作階段資訊，您可能會想要透過組態來啟用 ASP.NET 相容性模式。

WCF 中的 AJAX 端點甚至可能會在沒有 ASP.NET AJAX 架構的情況下使用。 這麼做需要瞭解 WCF 中 AJAX 支援的支援架構。 如需此架構的討論，請參閱[WCF WEB HTTP 程式設計物件模型](wcf-web-http-programming-object-model.md)。 如需示範此方法的程式碼範例，請參閱[使用 JSON 和 XML 的 AJAX 服務](../samples/ajax-service-with-json-and-xml-sample.md)。

## <a name="see-also"></a>請參閱

- [WCF Web HTTP 程式設計模型](wcf-web-http-programming-model.md)
- [如何：不使用組態新增 ASP.NET AJAX 端點](how-to-add-an-aspnet-ajax-endpoint-without-using-configuration.md)
- [如何：使用組態新增 ASP.NET AJAX 端點](how-to-use-configuration-to-add-an-aspnet-ajax-endpoint.md)
- [HOW TO：在 ASP.NET AJAX 端點的 HTTP POST 和 HTTP GET 要求之間進行選擇](http-post-and-http-get-requests-for-aspnet-ajax-endpoints.md)
