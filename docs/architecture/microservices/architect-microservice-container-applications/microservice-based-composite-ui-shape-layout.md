---
title: 建立以微服務為基礎的複合 UI
description: 微服務架構不只可用於後端。 預覽以了解如何用於前端。
ms.date: 01/13/2021
ms.openlocfilehash: 3d866172cf7d15486dd2cc0d5dbb286c77693cea
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/14/2021
ms.locfileid: "98189406"
---
# <a name="creating-composite-ui-based-on-microservices"></a><span data-ttu-id="59731-104">建立以微服務為基礎的複合 UI</span><span class="sxs-lookup"><span data-stu-id="59731-104">Creating composite UI based on microservices</span></span>

<span data-ttu-id="59731-105">微服務架構通常是從伺服器端處理資料和邏輯開始，但在許多情況下，UI 仍會以單體的方式處理。</span><span class="sxs-lookup"><span data-stu-id="59731-105">Microservices architecture often starts with the server-side handling data and logic, but, in many cases, the UI is still handled as a monolith.</span></span> <span data-ttu-id="59731-106">不過，更先進的方法稱為 [微前端](https://martinfowler.com/articles/micro-frontends.html)，也就是根據微服務來設計您的應用程式 UI。</span><span class="sxs-lookup"><span data-stu-id="59731-106">However, a more advanced approach, called [micro frontends](https://martinfowler.com/articles/micro-frontends.html), is to design your application UI based on microservices as well.</span></span> <span data-ttu-id="59731-107">這表示具有微服務所產生的複合 UI，而不是在伺服器上擁有多個微服務，並只由一個整合型用戶端應用程式來取用這些微服務。</span><span class="sxs-lookup"><span data-stu-id="59731-107">That means having a composite UI produced by the microservices, instead of having microservices on the server and just a monolithic client app consuming the microservices.</span></span> <span data-ttu-id="59731-108">透過此方法，您建置的微服務就會同時具備邏輯和視覺表示。</span><span class="sxs-lookup"><span data-stu-id="59731-108">With this approach, the microservices you build can be complete with both logic and visual representation.</span></span>

<span data-ttu-id="59731-109">圖 4-20 顯示更簡單的方法，該方法只會從整合型用戶端應用程式取用微服務。</span><span class="sxs-lookup"><span data-stu-id="59731-109">Figure 4-20 shows the simpler approach of just consuming microservices from a monolithic client application.</span></span> <span data-ttu-id="59731-110">當然，您在產生 HTML 與 JavaScript 之間可能會有 ASP.NET MVC 服務。</span><span class="sxs-lookup"><span data-stu-id="59731-110">Of course, you could have an ASP.NET MVC service in between producing the HTML and JavaScript.</span></span> <span data-ttu-id="59731-111">下圖已經過簡化，顯示您有取用微服務的單一 (整合型) 用戶端 UI，只著重於邏輯和資料，而不是 UI 形狀 (HTML 和 JavaScript)。</span><span class="sxs-lookup"><span data-stu-id="59731-111">The figure is a simplification that highlights that you have a single (monolithic) client UI consuming the microservices, which just focus on logic and data and not on the UI shape (HTML and JavaScript).</span></span>

![連接至微服務的整合型 UI 應用程式圖表。](./media/microservice-based-composite-ui-shape-layout/monolith-ui-consume-microservices.png)

<span data-ttu-id="59731-113">**圖 4-20**：</span><span class="sxs-lookup"><span data-stu-id="59731-113">**Figure 4-20**.</span></span> <span data-ttu-id="59731-114">取用後端微服務的整合型 UI 應用程式</span><span class="sxs-lookup"><span data-stu-id="59731-114">A monolithic UI application consuming back-end microservices</span></span>

<span data-ttu-id="59731-115">相較之下，複合 UI 是由微服務本身精確地產生和撰寫而成。</span><span class="sxs-lookup"><span data-stu-id="59731-115">In contrast, a composite UI is precisely generated and composed by the microservices themselves.</span></span> <span data-ttu-id="59731-116">部分微服務會支援特定 UI 區域的視覺形狀。</span><span class="sxs-lookup"><span data-stu-id="59731-116">Some of the microservices drive the visual shape of specific areas of the UI.</span></span> <span data-ttu-id="59731-117">主要差異在於您有以範本為基礎的用戶端 UI 元件 (例如 TypeScript 類別)，而且這些範本的資料成形 UI ViewModel 來自每個微服務。</span><span class="sxs-lookup"><span data-stu-id="59731-117">The key difference is that you have client UI components (TypeScript classes, for example) based on templates, and the data-shaping-UI ViewModel for those templates comes from each microservice.</span></span>

<span data-ttu-id="59731-118">用戶端應用程式啟動時，每個用戶端 UI 元件 (例如 TypeScript 類別) 會向基礎結構微服務註冊其本身，以便能夠針對指定案例提供 ViewModel。</span><span class="sxs-lookup"><span data-stu-id="59731-118">At client application start-up time, each of the client UI components (TypeScript classes, for example) registers itself with an infrastructure microservice capable of providing ViewModels for a given scenario.</span></span> <span data-ttu-id="59731-119">如果微服務變更形狀，UI 也會變更。</span><span class="sxs-lookup"><span data-stu-id="59731-119">If the microservice changes the shape, the UI changes also.</span></span>

<span data-ttu-id="59731-120">圖 4-21 顯示此複合 UI 方法的版本。</span><span class="sxs-lookup"><span data-stu-id="59731-120">Figure 4-21 shows a version of this composite UI approach.</span></span> <span data-ttu-id="59731-121">這種方法已經過簡化，因為您可能會有其他微服務會匯總以不同技術為基礎的細微部分。</span><span class="sxs-lookup"><span data-stu-id="59731-121">This approach is simplified because you might have other microservices that are aggregating granular parts that are based on different techniques.</span></span> <span data-ttu-id="59731-122">這取決於您建置的是傳統 Web 方法 (ASP.NET MVC) 或 SPA (單頁應用程式)。</span><span class="sxs-lookup"><span data-stu-id="59731-122">It depends on whether you're building a traditional web approach (ASP.NET MVC) or an SPA (Single Page Application).</span></span>

![複合 UI 的圖表，由許多視圖模型組成。](./media/microservice-based-composite-ui-shape-layout/microservice-generate-composite-ui.png)

<span data-ttu-id="59731-124">**圖 4-21**：</span><span class="sxs-lookup"><span data-stu-id="59731-124">**Figure 4-21**.</span></span> <span data-ttu-id="59731-125">由後端微服務成形的複合 UI 應用程式範例</span><span class="sxs-lookup"><span data-stu-id="59731-125">Example of a composite UI application shaped by back-end microservices</span></span>

<span data-ttu-id="59731-126">每個 UI 組合微服務會類似於小型 API 閘道。</span><span class="sxs-lookup"><span data-stu-id="59731-126">Each of those UI composition microservices would be similar to a small API Gateway.</span></span> <span data-ttu-id="59731-127">但在這種情況下，每一個都有一個小的 UI 區域。</span><span class="sxs-lookup"><span data-stu-id="59731-127">But in this case, each one is responsible for a small UI area.</span></span>

<span data-ttu-id="59731-128">根據您所使用的 UI 技術，微服務導向的複合 UI 方法可能挑戰性很高，也可能很低。</span><span class="sxs-lookup"><span data-stu-id="59731-128">A composite UI approach that's driven by microservices can be more challenging or less so, depending on what UI technologies you're using.</span></span> <span data-ttu-id="59731-129">例如，您不會使用與用來建置 SPA 或原生行動應用程式相同的技術來建置傳統 Web 應用程式 (例如開發 Xamarin 應用程式時，此方法的挑戰性可能更高)。</span><span class="sxs-lookup"><span data-stu-id="59731-129">For instance, you won't use the same techniques for building a traditional web application that you use for building an SPA or for native mobile app (as when developing Xamarin apps, which can be more challenging for this approach).</span></span>

<span data-ttu-id="59731-130">[eShopOnContainers](https://aka.ms/MicroservicesArchitecture) 範例應用程式使用整合型 UI 方法的原因有很多。</span><span class="sxs-lookup"><span data-stu-id="59731-130">The [eShopOnContainers](https://aka.ms/MicroservicesArchitecture) sample application uses the monolithic UI approach for multiple reasons.</span></span> <span data-ttu-id="59731-131">首先，它是微服務和容器的前導。</span><span class="sxs-lookup"><span data-stu-id="59731-131">First, it's an introduction to microservices and containers.</span></span> <span data-ttu-id="59731-132">複合 UI 更進階，但在設計及開發 UI 時也需要更高的複雜度。</span><span class="sxs-lookup"><span data-stu-id="59731-132">A composite UI is more advanced but also requires further complexity when designing and developing the UI.</span></span> <span data-ttu-id="59731-133">其次，eShopOnContainers 也提供以 Xamarin 為基礎的原生行動應用程式，因此在用戶端 \# 側會更複雜。</span><span class="sxs-lookup"><span data-stu-id="59731-133">Second, eShopOnContainers also provides a native mobile app based on Xamarin, which would make it more complex on the client C\# side.</span></span>

<span data-ttu-id="59731-134">不過，建議您使用下列參考，深入了解以微服務為基礎的複合 UI。</span><span class="sxs-lookup"><span data-stu-id="59731-134">However, we encourage you to use the following references to learn more about composite UI based on microservices.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="59731-135">其他資源</span><span class="sxs-lookup"><span data-stu-id="59731-135">Additional resources</span></span>

- <span data-ttu-id="59731-136">**微前端 (聖馬丁 Fowler 的 blog)**</span><span class="sxs-lookup"><span data-stu-id="59731-136">**Micro Frontends (Martin Fowler's blog)**</span></span>  
  <https://martinfowler.com/articles/micro-frontends.html>
  
- <span data-ttu-id="59731-137">**微前端 (Michael Geers 網站)**</span><span class="sxs-lookup"><span data-stu-id="59731-137">**Micro Frontends (Michael Geers site)**</span></span>  
  <https://micro-frontends.org/>
  
- <span data-ttu-id="59731-138">**使用 ASP.NET 的複合 UI (特定研討)**</span><span class="sxs-lookup"><span data-stu-id="59731-138">**Composite UI using ASP.NET (Particular's Workshop)**</span></span>  
  <https://github.com/Particular/Workshop/tree/master/demos/asp-net-core>

- <span data-ttu-id="59731-139">**Ruben Oostinga。微服務架構中的整合前端**</span><span class="sxs-lookup"><span data-stu-id="59731-139">**Ruben Oostinga. The Monolithic Frontend in the Microservices Architecture**</span></span>  
  <https://xebia.com/blog/the-monolithic-frontend-in-the-microservices-architecture/>

- <span data-ttu-id="59731-140">**Mauro Servienti。更好的 UI 組合秘密**</span><span class="sxs-lookup"><span data-stu-id="59731-140">**Mauro Servienti. The secret of better UI composition**</span></span>  
  <https://particular.net/blog/secret-of-better-ui-composition>

- <span data-ttu-id="59731-141">**Viktor Farcic.將 Front-End Web 元件納入微服務**</span><span class="sxs-lookup"><span data-stu-id="59731-141">**Viktor Farcic. Including Front-End Web Components Into Microservices**</span></span>  
  <https://technologyconversations.com/2015/08/09/including-front-end-web-components-into-microservices/>

- <span data-ttu-id="59731-142">**Managing Frontend in the Microservices Architecture (管理微服務架構中的前端)**</span><span class="sxs-lookup"><span data-stu-id="59731-142">**Managing Frontend in the Microservices Architecture**</span></span>  
  <https://allegro.tech/2016/03/Managing-Frontend-in-the-microservices-architecture.html>

>[!div class="step-by-step"]
><span data-ttu-id="59731-143">[上一個](microservices-addressability-service-registry.md) 
>[下一步](resilient-high-availability-microservices.md)</span><span class="sxs-lookup"><span data-stu-id="59731-143">[Previous](microservices-addressability-service-registry.md)
[Next](resilient-high-availability-microservices.md)</span></span>
