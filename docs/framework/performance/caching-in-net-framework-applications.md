---
title: .NET Framework 應用程式中的快取
description: 在 .NET 應用程式中使用快取。 瞭解如何快取資料、ASP.NET 應用程式中的快取或 WCF REST 服務，以及在 .NET 中擴充快取。
ms.date: 03/30/2017
helpviewer_keywords:
- ASP.NET caching
- caching [.NET Framework]
- caching [ASP.NET]
ms.assetid: c4b47ee0-4b82-4124-9bce-818088385e34
ms.openlocfilehash: 5518151c26c528095ec91116b53e82e22e23d25f
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96235204"
---
# <a name="caching-in-net-framework-applications"></a><span data-ttu-id="e4bd9-104">.NET Framework 應用程式中的快取</span><span class="sxs-lookup"><span data-stu-id="e4bd9-104">Caching in .NET Framework Applications</span></span>

<span data-ttu-id="e4bd9-105">快取可讓您將資料儲存在記憶體中，以進行快速存取。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-105">Caching enables you to store data in memory for rapid access.</span></span> <span data-ttu-id="e4bd9-106">重新存取資料時，應用程式可以從快取中取得資料，而不是從原始來源進行擷取。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-106">When the data is accessed again, applications can get the data from the cache instead of retrieving it from the original source.</span></span> <span data-ttu-id="e4bd9-107">這可以改善效能和延展性。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-107">This can improve performance and scalability.</span></span> <span data-ttu-id="e4bd9-108">此外，暫時無法使用資料來源時，快取可讓資料可用。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-108">In addition, caching makes data available when the data source is temporarily unavailable.</span></span>

 <span data-ttu-id="e4bd9-109">.NET Framework 所提供的快取功能可用來改善 Windows 用戶端和伺服器應用程式的效能和延展性，包含 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-109">The .NET Framework provides caching functionality that you can use to improve the performance and scalability of both Windows client and server applications, including ASP.NET.</span></span>

> [!NOTE]
> <span data-ttu-id="e4bd9-110">在 .NET Framework 3.5 及更早版本中，ASP.NET 會在命名空間中提供記憶體中的快取執行 <xref:System.Web.Caching> 。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-110">In the .NET Framework 3.5 and earlier versions, ASP.NET provided an in-memory cache implementation in the <xref:System.Web.Caching> namespace.</span></span> <span data-ttu-id="e4bd9-111">在舊版 .NET Framework 中，快取只能在命名空間中使用， <xref:System.Web> 因此需要 ASP.NET 類別的相依性。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-111">In previous versions of the .NET Framework, caching was available only in the <xref:System.Web> namespace and therefore required a dependency on ASP.NET classes.</span></span> <span data-ttu-id="e4bd9-112">在 .NET Framework 4 中，<xref:System.Runtime.Caching> 命名空間包含針對 Web 和非 Web 應用程式所設計的 API。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-112">In the .NET Framework 4, the <xref:System.Runtime.Caching> namespace contains APIs that are designed for both Web and non-Web applications.</span></span>

## <a name="caching-data"></a><span data-ttu-id="e4bd9-113">快取資料</span><span class="sxs-lookup"><span data-stu-id="e4bd9-113">Caching Data</span></span>

 <span data-ttu-id="e4bd9-114">您可以使用 <xref:System.Runtime.Caching> 命名空間中的類別來快取資訊。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-114">You can cache information by using classes in the <xref:System.Runtime.Caching> namespace.</span></span> <span data-ttu-id="e4bd9-115">這個命名空間中的快取類別提供下列功能：</span><span class="sxs-lookup"><span data-stu-id="e4bd9-115">The caching classes in this namespace provide the following features:</span></span>

- <span data-ttu-id="e4bd9-116">提供建立自訂快取實作之基礎的抽象類型。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-116">Abstract types that provide the foundation for creating custom cache implementations.</span></span>

- <span data-ttu-id="e4bd9-117">具體記憶體內部物件快取實作。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-117">A concrete in-memory object cache implementation.</span></span>

 <span data-ttu-id="e4bd9-118">抽象基底快取類別 (<xref:System.Runtime.Caching.ObjectCache>) 會定義下列快取工作：</span><span class="sxs-lookup"><span data-stu-id="e4bd9-118">The abstract base caching class (<xref:System.Runtime.Caching.ObjectCache>) defines the following caching tasks:</span></span>

- <span data-ttu-id="e4bd9-119">建立和管理快取項目。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-119">Creating and managing cache entries.</span></span>

- <span data-ttu-id="e4bd9-120">指定到期和收回資訊。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-120">Specifying expiration and eviction information.</span></span>

- <span data-ttu-id="e4bd9-121">觸發回應快取項目變更所引發的事件。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-121">Triggering events that are raised in response to changes in cache entries.</span></span>

 <span data-ttu-id="e4bd9-122"><xref:System.Runtime.Caching.MemoryCache> 類別是 <xref:System.Runtime.Caching.ObjectCache> 類別的記憶體內部物件快取實作。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-122">The <xref:System.Runtime.Caching.MemoryCache> class is an in-memory object cache implementation of the <xref:System.Runtime.Caching.ObjectCache> class.</span></span> <span data-ttu-id="e4bd9-123">您可以使用大部分快取工作的 <xref:System.Runtime.Caching.MemoryCache> 類別。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-123">You can use the <xref:System.Runtime.Caching.MemoryCache> class for most caching tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="e4bd9-124">在 <xref:System.Web.Caching> 命名空間中所定義的 ASP.NET 快取物件上，建立 <xref:System.Runtime.Caching.MemoryCache> 類別的模型。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-124">The <xref:System.Runtime.Caching.MemoryCache> class is modeled on the ASP.NET cache object that is defined in the <xref:System.Web.Caching> namespace.</span></span> <span data-ttu-id="e4bd9-125">因此，內部快取邏輯類似於舊版 ASP.NET 中所提供的邏輯。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-125">Therefore, the internal caching logic similar to the logic that was provided in earlier versions of ASP.NET.</span></span>

 <span data-ttu-id="e4bd9-126">如需如何在 WPF 應用程式中使用快取的範例，請參閱[逐步解說：在 WPF 應用程式中快取應用程式資料](/dotnet/desktop/wpf/advanced/walkthrough-caching-application-data-in-a-wpf-application)。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-126">For an example of how to use to caching in a WPF application, see [Walkthrough: Caching Application Data in a WPF Application](/dotnet/desktop/wpf/advanced/walkthrough-caching-application-data-in-a-wpf-application).</span></span>

## <a name="caching-in-aspnet-applications"></a><span data-ttu-id="e4bd9-127">ASP.NET 應用程式中的快取</span><span class="sxs-lookup"><span data-stu-id="e4bd9-127">Caching in ASP.NET Applications</span></span>

 <span data-ttu-id="e4bd9-128"><xref:System.Runtime.Caching> 命名空間中的快取類別提供在 ASP.NET 中快取資料的功能。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-128">The caching classes in the <xref:System.Runtime.Caching> namespace provide functionality for caching data in ASP.NET.</span></span>

> [!NOTE]
> <span data-ttu-id="e4bd9-129">如果您的應用程式以 .NET Framework 3.5 或更早版本為目標，您必須使用命名空間中定義的快取類別 <xref:System.Web.Caching> 。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-129">If your application targets the .NET Framework 3.5 or earlier, you must use the caching classes that are defined in the <xref:System.Web.Caching> namespace.</span></span> <span data-ttu-id="e4bd9-130">如需詳細資訊，請參閱 [ASP.NET 快取概觀](/previous-versions/aspnet/ms178597(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-130">For more information, see [ASP.NET Caching Overview](/previous-versions/aspnet/ms178597(v=vs.100)).</span></span>

> [!NOTE]
> <span data-ttu-id="e4bd9-131">當您開發新的應用程式時，建議您使用 <xref:System.Runtime.Caching.MemoryCache> 類別。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-131">When you develop new applications, we recommend that you use the <xref:System.Runtime.Caching.MemoryCache> class.</span></span> <span data-ttu-id="e4bd9-132"><xref:System.Runtime.Caching> 命名空間中所提供的 API 就像 <xref:System.Web.Caching.Cache> 命名空間中提供的 API。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-132">The API that is provided in the <xref:System.Runtime.Caching> namespace is like the API that is provided in the <xref:System.Web.Caching.Cache> namespace.</span></span> <span data-ttu-id="e4bd9-133">因此，如果您已在舊版 ASP.NET 中使用快取，則會熟悉 API。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-133">Therefore, the API will be familiar if you used caching in earlier versions of ASP.NET.</span></span> <span data-ttu-id="e4bd9-134">如需如何在 ASP.NET 應用程式中使用快取的範例，請參閱[逐步解說：在 ASP.NET 中快取應用程式資料](/previous-versions/ff477235(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-134">For an example of how to use caching in ASP.NET applications, see [Walkthrough: Caching Application Data in ASP.NET](/previous-versions/ff477235(v=vs.100)).</span></span>

### <a name="output-caching"></a><span data-ttu-id="e4bd9-135">輸出快取</span><span class="sxs-lookup"><span data-stu-id="e4bd9-135">Output Caching</span></span>

 <span data-ttu-id="e4bd9-136">若要手動快取應用程式資料，您可以在 ASP.NET 中使用 <xref:System.Runtime.Caching.MemoryCache> 類別。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-136">To manually cache application data, you can use the <xref:System.Runtime.Caching.MemoryCache> class in ASP.NET.</span></span> <span data-ttu-id="e4bd9-137">ASP.NET 也支援輸出快取，以將所產生的頁面、控制項和 HTTP 回應輸出儲存至記憶體中。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-137">ASP.NET also supports output caching, which stores the generated output of pages, controls, and HTTP responses in memory.</span></span> <span data-ttu-id="e4bd9-138">您可以在 ASP.NET 網頁中透過宣告方式設定輸出快取，或使用 Web.config 檔案中的設定來設定輸出快取。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-138">You can configure output caching declaratively in an ASP.NET Web page or by using settings in the Web.config file.</span></span> <span data-ttu-id="e4bd9-139">如需詳細資訊，請參閱[快取的 outputCache 項目 (ASP.NET 設定結構描述)](/previous-versions/dotnet/netframework-4.0/ms228124(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-139">For more information, see [outputCache Element for caching (ASP.NET Settings Schema)](/previous-versions/dotnet/netframework-4.0/ms228124(v=vs.100)).</span></span>

 <span data-ttu-id="e4bd9-140">ASP.NET 可讓您建立自訂輸出快取提供者來擴充輸出快取。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-140">ASP.NET lets you extend output caching by creating custom output-cache providers.</span></span> <span data-ttu-id="e4bd9-141">使用自訂提供者，即可使用其他存放裝置 (例如磁碟、雲端存放裝置和分散式快取引擎) 來儲存快取的內容。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-141">By using custom providers, you can store cached content using other storage devices such as disks, cloud storage, and distributed cache engines.</span></span> <span data-ttu-id="e4bd9-142">為了建立自訂輸出快取提供者，您可以建立衍生自 <xref:System.Web.Caching.OutputCacheProvider> 類別的類別，並設定應用程式使用自訂輸出快取提供者。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-142">To create a custom output cache provider, you create a class that derives from the <xref:System.Web.Caching.OutputCacheProvider> class and configure the application to use the custom output cache provider.</span></span>

## <a name="caching-in-wcf-rest-services"></a><span data-ttu-id="e4bd9-143">WCF REST 服務中的快取</span><span class="sxs-lookup"><span data-stu-id="e4bd9-143">Caching in WCF REST Services</span></span>

 <span data-ttu-id="e4bd9-144">針對 WCF REST 服務，.NET Framework 可讓您充分利用 ASP.NET 中可用的宣告式輸出快取。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-144">For WCF REST services, the .NET Framework enables you to take advantage of the declarative output caching that is available in ASP.NET.</span></span> <span data-ttu-id="e4bd9-145">這可讓您快取來自 WCF REST 服務作業的回應。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-145">This enables you to cache responses from your WCF REST service operations.</span></span> <span data-ttu-id="e4bd9-146">使用者將 HTTP GET 要求傳送至設定進行快取的服務時，ASP.NET 會傳回快取的回應，且不會呼叫服務方法。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-146">When a user sends an HTTP GET request to a service that is configured for caching, ASP.NET sends back the cached response, and the service method is not called.</span></span> <span data-ttu-id="e4bd9-147">快取到期之後，下次使用者傳送 HTTP GET 要求時，會呼叫您的服務方法，並重新快取回應。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-147">After the cache expires, the next time that a user sends an HTTP GET request, your service method is called and the response is again cached.</span></span>

 <span data-ttu-id="e4bd9-148">.NET Framework 也可讓您實作條件式 HTTP GET 快取。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-148">The .NET Framework also enables you to implement conditional HTTP GET caching.</span></span> <span data-ttu-id="e4bd9-149">在 REST 案例中，通常服務會使用條件式 HTTP GET 要求實作智慧型 HTTP 快取，如 [HTTP 規格](https://www.w3.org/Protocols/rfc2616/rfc2616.html)中所述。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-149">In REST scenarios, a conditional HTTP GET request is often used by services to implement intelligent HTTP caching as described in the [HTTP Specification](https://www.w3.org/Protocols/rfc2616/rfc2616.html).</span></span> <span data-ttu-id="e4bd9-150">如需詳細資訊，請參閱 [WCF Web HTTP 服務的快取支援](../wcf/feature-details/caching-support-for-wcf-web-http-services.md)。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-150">For more information, see [Caching Support for WCF Web HTTP Services](../wcf/feature-details/caching-support-for-wcf-web-http-services.md).</span></span>

## <a name="extending-caching-in-the-net-framework"></a><span data-ttu-id="e4bd9-151">擴充 .NET Framework 中的快取</span><span class="sxs-lookup"><span data-stu-id="e4bd9-151">Extending Caching in the .NET Framework</span></span>

 <span data-ttu-id="e4bd9-152">.NET Framework 中的快取是設計成可擴充。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-152">Caching in the .NET Framework is designed to be extensible.</span></span> <span data-ttu-id="e4bd9-153"><xref:System.Runtime.Caching.ObjectCache> 類別可讓您建立自訂快取實作。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-153">The <xref:System.Runtime.Caching.ObjectCache> class enables you to create a custom cache implementation.</span></span> <span data-ttu-id="e4bd9-154">這個類別提供可用於所有 Managed 應用程式的成員，包含 Windows Form、Windows Presentation Foundation (WPF) 和 Windows Communications Foundation (WCF)。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-154">This class provides members that are available to all managed applications, including Windows Forms, Windows Presentation Foundation (WPF), and Windows Communications Foundation (WCF).</span></span> <span data-ttu-id="e4bd9-155">若要建立使用不同儲存機制的快取類別，或您想要更精確地控制快取作業，則可能要執行這項作業。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-155">You might do this in order to create a cache class that uses a different storage mechanism, or if you want granular control over cache operations.</span></span>

 <span data-ttu-id="e4bd9-156">若要擴充快取，您可執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="e4bd9-156">To extend caching you can do the following:</span></span>

- <span data-ttu-id="e4bd9-157">建立衍生自 <xref:System.Runtime.Caching.ObjectCache> 類別的自訂類別，然後在衍生類別中提供自訂快取實作。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-157">Create a custom class that derives from the <xref:System.Runtime.Caching.ObjectCache> class and then provide a custom cache implementation in the derived class.</span></span>

- <span data-ttu-id="e4bd9-158">建立衍生自 <xref:System.Runtime.Caching.MemoryCache> 類別的類別，以及自訂或擴充衍生類別。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-158">Create a class that derives from <xref:System.Runtime.Caching.MemoryCache> class and customize or extend the derived class.</span></span> <span data-ttu-id="e4bd9-159">如需如何執行這項作業的範例，請參閱[在 ASP.NET 應用程式使用多個快取物件來快取應用程式資料](/archive/blogs/aspnetue/caching-application-data-by-using-multiple-cache-objects-in-an-asp-net-application)。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-159">For an example of how to do this, see [Caching Application Data by Using Multiple Cache Objects in an ASP.NET Application](/archive/blogs/aspnetue/caching-application-data-by-using-multiple-cache-objects-in-an-asp-net-application).</span></span>

- <span data-ttu-id="e4bd9-160">建立衍生自 <xref:System.Web.Caching.OutputCacheProvider> 類別的類別，並設定應用程式使用自訂輸出快取提供者。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-160">Create a class that derives from the <xref:System.Web.Caching.OutputCacheProvider> class and configure the application to use the custom output cache provider.</span></span>

 <span data-ttu-id="e4bd9-161">如需詳細資訊，請參閱 Scott Guthrie 的 blog 上的進入可延伸 [的輸出快取與 ASP.NET 4 (VS 2010 和 .NET Framework 4.0 系列) ](https://weblogs.asp.net/scottgu/extensible-output-caching-with-asp-net-4-vs-2010-and-net-4-0-series) 。</span><span class="sxs-lookup"><span data-stu-id="e4bd9-161">For more information, see the entry [Extensible Output Caching with ASP.NET 4 (VS 2010 and .NET Framework 4.0 Series)](https://weblogs.asp.net/scottgu/extensible-output-caching-with-asp-net-4-vs-2010-and-net-4-0-series) on Scott Guthrie's blog.</span></span>

## <a name="see-also"></a><span data-ttu-id="e4bd9-162">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e4bd9-162">See also</span></span>

- <xref:System.Runtime.Caching.ObjectCache>
- <xref:System.Runtime.Caching.MemoryCache>
- [<span data-ttu-id="e4bd9-163">逐步解說：在 WPF 應用程式中快取應用程式資料</span><span class="sxs-lookup"><span data-stu-id="e4bd9-163">Walkthrough: Caching Application Data in a WPF Application</span></span>](/dotnet/desktop/wpf/advanced/walkthrough-caching-application-data-in-a-wpf-application)
- <span data-ttu-id="e4bd9-164">[逐步解說：在 ASP.NET 中快取應用程式資料](/previous-versions/ff477235(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="e4bd9-164">[Walkthrough: Caching Application Data in ASP.NET](/previous-versions/ff477235(v=vs.100))</span></span>
