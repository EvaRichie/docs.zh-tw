---
title: .NET Framework 應用程式中的快取
description: 在 .NET 應用程式中使用快取。 閱讀有關快取資料、ASP.NET 應用程式中的快取或 WCF REST 服務，以及在 .NET 中擴充快取的資訊。
ms.date: 03/30/2017
helpviewer_keywords:
- ASP.NET caching
- caching [.NET Framework]
- caching [ASP.NET]
ms.assetid: c4b47ee0-4b82-4124-9bce-818088385e34
ms.openlocfilehash: 9b08a07e9b446c2998150a327dccdc8d0481722a
ms.sourcegitcommit: 0fa2b7b658bf137e813a7f4d09589d64c148ebf5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/14/2020
ms.locfileid: "86309764"
---
# <a name="caching-in-net-framework-applications"></a>.NET Framework 應用程式中的快取
快取可讓您將資料儲存在記憶體中，以進行快速存取。 重新存取資料時，應用程式可以從快取中取得資料，而不是從原始來源進行擷取。 這可以改善效能和延展性。 此外，暫時無法使用資料來源時，快取可讓資料可用。  
  
 .NET Framework 所提供的快取功能可用來改善 Windows 用戶端和伺服器應用程式的效能和延展性，包含 ASP.NET。  
  
> [!NOTE]
> 在 .NET Framework 3.5 和更早版本中，ASP.NET 提供了命名空間中的記憶體內部快取實作為功能 <xref:System.Web.Caching> 。 在舊版的 .NET Framework 中，快取僅適用于 <xref:System.Web> 命名空間，因此需要 ASP.NET 類別的相依性。 在 .NET Framework 4 中，<xref:System.Runtime.Caching> 命名空間包含針對 Web 和非 Web 應用程式所設計的 API。  
  
## <a name="caching-data"></a>快取資料  
 您可以使用 <xref:System.Runtime.Caching> 命名空間中的類別來快取資訊。 這個命名空間中的快取類別提供下列功能：  
  
- 提供建立自訂快取實作之基礎的抽象類型。  
  
- 具體記憶體內部物件快取實作。  
  
 抽象基底快取類別 (<xref:System.Runtime.Caching.ObjectCache>) 會定義下列快取工作：  
  
- 建立和管理快取項目。  
  
- 指定到期和收回資訊。  
  
- 觸發回應快取項目變更所引發的事件。  
  
 <xref:System.Runtime.Caching.MemoryCache> 類別是 <xref:System.Runtime.Caching.ObjectCache> 類別的記憶體內部物件快取實作。 您可以使用大部分快取工作的 <xref:System.Runtime.Caching.MemoryCache> 類別。  
  
> [!NOTE]
> 在 <xref:System.Web.Caching> 命名空間中所定義的 ASP.NET 快取物件上，建立 <xref:System.Runtime.Caching.MemoryCache> 類別的模型。 因此，內部快取邏輯類似於舊版 ASP.NET 中所提供的邏輯。  
  
 如需如何在 WPF 應用程式中使用快取的範例，請參閱[逐步解說：在 WPF 應用程式中快取應用程式資料](../wpf/advanced/walkthrough-caching-application-data-in-a-wpf-application.md)。  
  
## <a name="caching-in-aspnet-applications"></a>ASP.NET 應用程式中的快取  
 <xref:System.Runtime.Caching> 命名空間中的快取類別提供在 ASP.NET 中快取資料的功能。  
  
> [!NOTE]
> 如果您的應用程式以 .NET Framework 3.5 或更早版本為目標，則必須使用在命名空間中定義的快取類別 <xref:System.Web.Caching> 。 如需詳細資訊，請參閱 [ASP.NET 快取概觀](https://docs.microsoft.com/previous-versions/aspnet/ms178597(v=vs.100))。  
  
> [!NOTE]
> 當您開發新的應用程式時，建議您使用 <xref:System.Runtime.Caching.MemoryCache> 類別。 <xref:System.Runtime.Caching> 命名空間中所提供的 API 就像 <xref:System.Web.Caching.Cache> 命名空間中提供的 API。 因此，如果您已在舊版 ASP.NET 中使用快取，則會熟悉 API。 如需如何在 ASP.NET 應用程式中使用快取的範例，請參閱[逐步解說：在 ASP.NET 中快取應用程式資料](https://docs.microsoft.com/previous-versions/ff477235(v=vs.100))。  
  
### <a name="output-caching"></a>輸出快取  
 若要手動快取應用程式資料，您可以在 ASP.NET 中使用 <xref:System.Runtime.Caching.MemoryCache> 類別。 ASP.NET 也支援輸出快取，以將所產生的頁面、控制項和 HTTP 回應輸出儲存至記憶體中。 您可以在 ASP.NET 網頁中透過宣告方式設定輸出快取，或使用 Web.config 檔案中的設定來設定輸出快取。 如需詳細資訊，請參閱[快取的 outputCache 項目 (ASP.NET 設定結構描述)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms228124(v=vs.100))。  
  
 ASP.NET 可讓您建立自訂輸出快取提供者來擴充輸出快取。 使用自訂提供者，即可使用其他存放裝置 (例如磁碟、雲端存放裝置和分散式快取引擎) 來儲存快取的內容。 為了建立自訂輸出快取提供者，您可以建立衍生自 <xref:System.Web.Caching.OutputCacheProvider> 類別的類別，並設定應用程式使用自訂輸出快取提供者。  
  
## <a name="caching-in-wcf-rest-services"></a>WCF REST 服務中的快取  
 針對 WCF REST 服務，.NET Framework 可讓您充分利用 ASP.NET 中可用的宣告式輸出快取。 這可讓您快取來自 WCF REST 服務作業的回應。 使用者將 HTTP GET 要求傳送至設定進行快取的服務時，ASP.NET 會傳回快取的回應，且不會呼叫服務方法。 快取到期之後，下次使用者傳送 HTTP GET 要求時，會呼叫您的服務方法，並重新快取回應。  
  
 .NET Framework 也可讓您實作條件式 HTTP GET 快取。 在 REST 案例中，通常服務會使用條件式 HTTP GET 要求實作智慧型 HTTP 快取，如 [HTTP 規格](https://www.w3.org/Protocols/rfc2616/rfc2616.html)中所述。 如需詳細資訊，請參閱 [WCF Web HTTP 服務的快取支援](../wcf/feature-details/caching-support-for-wcf-web-http-services.md)。  
  
## <a name="extending-caching-in-the-net-framework"></a>擴充 .NET Framework 中的快取  
 .NET Framework 中的快取是設計成可擴充。 <xref:System.Runtime.Caching.ObjectCache> 類別可讓您建立自訂快取實作。 這個類別提供可用於所有 Managed 應用程式的成員，包含 Windows Form、Windows Presentation Foundation (WPF) 和 Windows Communications Foundation (WCF)。 若要建立使用不同儲存機制的快取類別，或您想要更精確地控制快取作業，則可能要執行這項作業。  
  
 若要擴充快取，您可執行下列動作：  
  
- 建立衍生自 <xref:System.Runtime.Caching.ObjectCache> 類別的自訂類別，然後在衍生類別中提供自訂快取實作。  
  
- 建立衍生自 <xref:System.Runtime.Caching.MemoryCache> 類別的類別，以及自訂或擴充衍生類別。 如需如何執行這項作業的範例，請參閱[在 ASP.NET 應用程式使用多個快取物件來快取應用程式資料](https://docs.microsoft.com/archive/blogs/aspnetue/caching-application-data-by-using-multiple-cache-objects-in-an-asp-net-application)。  
  
- 建立衍生自 <xref:System.Web.Caching.OutputCacheProvider> 類別的類別，並設定應用程式使用自訂輸出快取提供者。  
  
 如需詳細資訊，請參閱 Scott Guthrie 部落格上的 [Extensible Output Caching with ASP.NET 4 (VS 2010 and .NET 4.0 Series)](https://weblogs.asp.net/scottgu/extensible-output-caching-with-asp-net-4-vs-2010-and-net-4-0-series)(ASP.NET 4 (VS 2010 和 .NET 4.0 系列) 中的可擴充輸出快取) 一文。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Runtime.Caching.ObjectCache>
- <xref:System.Runtime.Caching.MemoryCache>
- [逐步解說：在 WPF 應用程式中快取應用程式資料](../wpf/advanced/walkthrough-caching-application-data-in-a-wpf-application.md)
- [逐步解說：在 ASP.NET 中快取應用程式資料](https://docs.microsoft.com/previous-versions/ff477235(v=vs.100))
