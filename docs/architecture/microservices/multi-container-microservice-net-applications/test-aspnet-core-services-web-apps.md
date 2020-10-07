---
title: 測試 ASP.NET Core 服務和 Web 應用程式
description: .NET 微服務：容器化 .NET 應用程式的架構 | 探索在容器中用於測試 ASP.NET Core 服務和 Web 應用程式的架構。
ms.date: 08/07/2020
ms.openlocfilehash: af1187fb1e2afbb9fa953db5a280c9cc317ab6a8
ms.sourcegitcommit: 636af37170ae75a11c4f7d1ecd770820e7dfe7bd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91804766"
---
# <a name="testing-aspnet-core-services-and-web-apps"></a><span data-ttu-id="eee15-103">測試 ASP.NET Core 服務和 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="eee15-103">Testing ASP.NET Core services and web apps</span></span>

<span data-ttu-id="eee15-104">控制器是任何 ASP.NET Core API 和 ASP.NET MVC Web 應用程式的核心部分。</span><span class="sxs-lookup"><span data-stu-id="eee15-104">Controllers are a central part of any ASP.NET Core API service and ASP.NET MVC Web application.</span></span> <span data-ttu-id="eee15-105">因此，您應該確信其行為符合應用程式的預期。</span><span class="sxs-lookup"><span data-stu-id="eee15-105">As such, you should have confidence they behave as intended for your application.</span></span> <span data-ttu-id="eee15-106">自動化的測試可建立您這方面的信心，並可在錯誤到達生產環境之前就偵測到錯誤。</span><span class="sxs-lookup"><span data-stu-id="eee15-106">Automated tests can provide you with this confidence and can detect errors before they reach production.</span></span>

<span data-ttu-id="eee15-107">您需要測試控制器根據有效或無效輸入的運作方式，以及測試根據所執行商務作業結果的控制器回應。</span><span class="sxs-lookup"><span data-stu-id="eee15-107">You need to test how the controller behaves based on valid or invalid inputs, and test controller responses based on the result of the business operation it performs.</span></span> <span data-ttu-id="eee15-108">不過，您的微服務應該有這些類型的測試：</span><span class="sxs-lookup"><span data-stu-id="eee15-108">However, you should have these types of tests for your microservices:</span></span>

- <span data-ttu-id="eee15-109">單元測試。</span><span class="sxs-lookup"><span data-stu-id="eee15-109">Unit tests.</span></span> <span data-ttu-id="eee15-110">這些可確保應用程式的個別元件會如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="eee15-110">These ensure that individual components of the application work as expected.</span></span> <span data-ttu-id="eee15-111">判斷提示測試元件 API。</span><span class="sxs-lookup"><span data-stu-id="eee15-111">Assertions test the component API.</span></span>

- <span data-ttu-id="eee15-112">整合測試。</span><span class="sxs-lookup"><span data-stu-id="eee15-112">Integration tests.</span></span> <span data-ttu-id="eee15-113">這些可確保針對外部成品 (如資料庫) 的元件互動會如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="eee15-113">These ensure that component interactions work as expected against external artifacts like databases.</span></span> <span data-ttu-id="eee15-114">判斷提示可以測試元件 API、UI 或資料庫 I/O、記錄之類的動作副作用。</span><span class="sxs-lookup"><span data-stu-id="eee15-114">Assertions can test component API, UI, or the side effects of actions like database I/O, logging, etc.</span></span>

- <span data-ttu-id="eee15-115">每個微服務的功能測試。</span><span class="sxs-lookup"><span data-stu-id="eee15-115">Functional tests for each microservice.</span></span> <span data-ttu-id="eee15-116">這些可確保應用程式從使用者的觀點來看如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="eee15-116">These ensure that the application works as expected from the user's perspective.</span></span>

- <span data-ttu-id="eee15-117">服務測試。</span><span class="sxs-lookup"><span data-stu-id="eee15-117">Service tests.</span></span> <span data-ttu-id="eee15-118">這些可確保會測試端對端的服務使用案例，包括在相同的時間測試多個服務。</span><span class="sxs-lookup"><span data-stu-id="eee15-118">These ensure that end-to-end service use cases, including testing multiple services at the same time, are tested.</span></span> <span data-ttu-id="eee15-119">針對這種測試，您需要先準備環境。</span><span class="sxs-lookup"><span data-stu-id="eee15-119">For this type of testing, you need to prepare the environment first.</span></span> <span data-ttu-id="eee15-120">在此情況下，這表示啟動服務 (例如，使用 docker-compose up)。</span><span class="sxs-lookup"><span data-stu-id="eee15-120">In this case, it means starting the services (for example, by using docker-compose up).</span></span>

### <a name="implementing-unit-tests-for-aspnet-core-web-apis"></a><span data-ttu-id="eee15-121">實作 ASP.NET Core Web API 的單元測試</span><span class="sxs-lookup"><span data-stu-id="eee15-121">Implementing unit tests for ASP.NET Core Web APIs</span></span>

<span data-ttu-id="eee15-122">單元測試包括將應用程式的一部分與其基礎結構和相依性隔離測試。</span><span class="sxs-lookup"><span data-stu-id="eee15-122">Unit testing involves testing a part of an application in isolation from its infrastructure and dependencies.</span></span> <span data-ttu-id="eee15-123">對控制器邏輯進行單元測試時，只會測試單一動作或方法的內容，而不會測試其相依性或架構本身的行為。</span><span class="sxs-lookup"><span data-stu-id="eee15-123">When you unit test controller logic, only the content of a single action or method is tested, not the behavior of its dependencies or of the framework itself.</span></span> <span data-ttu-id="eee15-124">單元測試不會偵測元件之間的互動問題，這需要使用整合測試。</span><span class="sxs-lookup"><span data-stu-id="eee15-124">Unit tests do not detect issues in the interaction between components—that is the purpose of integration testing.</span></span>

<span data-ttu-id="eee15-125">當您對控制器動作進行單元測試時，請務必只著重於其行為。</span><span class="sxs-lookup"><span data-stu-id="eee15-125">As you unit test your controller actions, make sure you focus only on their behavior.</span></span> <span data-ttu-id="eee15-126">控制器單元測試會避免像是篩選器、路由，或模型繫結 (將要求資料對應到 ViewModel 或 DTO) 等項目。</span><span class="sxs-lookup"><span data-stu-id="eee15-126">A controller unit test avoids things like filters, routing, or model binding (the mapping of request data to a ViewModel or DTO).</span></span> <span data-ttu-id="eee15-127">由於測試的焦點只有一個，因此單元測試通常很容易撰寫，而且執行速度很快。</span><span class="sxs-lookup"><span data-stu-id="eee15-127">Because they focus on testing just one thing, unit tests are generally simple to write and quick to run.</span></span> <span data-ttu-id="eee15-128">一組編寫完善的單元測試可以經常執行，而不會造成太多額外負荷。</span><span class="sxs-lookup"><span data-stu-id="eee15-128">A well-written set of unit tests can be run frequently without much overhead.</span></span>

<span data-ttu-id="eee15-129">單元測試是根據測試架構而實作，例如 xUnit.net、MSTest、Moq 或使用 NUnit。</span><span class="sxs-lookup"><span data-stu-id="eee15-129">Unit tests are implemented based on test frameworks like xUnit.net, MSTest, Moq, or NUnit.</span></span> <span data-ttu-id="eee15-130">針對 eShopOnContainers 範例應用程式，我們使用 xUnit。</span><span class="sxs-lookup"><span data-stu-id="eee15-130">For the eShopOnContainers sample application, we are using xUnit.</span></span>

<span data-ttu-id="eee15-131">當您為 Web API 控制器撰寫單元測試時，您會直接使用 C\# 中的新關鍵字具現化控制器類別，以便盡快執行測試。</span><span class="sxs-lookup"><span data-stu-id="eee15-131">When you write a unit test for a Web API controller, you instantiate the controller class directly using the new keyword in C\#, so that the test will run as fast as possible.</span></span> <span data-ttu-id="eee15-132">下列範例示範在使用 [xUnit](https://xunit.github.io/) 作為測試架構時如何執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="eee15-132">The following example shows how to do this when using [xUnit](https://xunit.github.io/) as the Test framework.</span></span>

```csharp
[Fact]
public async Task Get_order_detail_success()
{
    //Arrange
    var fakeOrderId = "12";
    var fakeOrder = GetFakeOrder();

    //...

    //Act
    var orderController = new OrderController(
        _orderServiceMock.Object,
        _basketServiceMock.Object,
        _identityParserMock.Object);

    orderController.ControllerContext.HttpContext = _contextMock.Object;
    var actionResult = await orderController.Detail(fakeOrderId);

    //Assert
    var viewResult = Assert.IsType<ViewResult>(actionResult);
    Assert.IsAssignableFrom<Order>(viewResult.ViewData.Model);
}
```

### <a name="implementing-integration-and-functional-tests-for-each-microservice"></a><span data-ttu-id="eee15-133">為每個微服務實作整合和功能測試</span><span class="sxs-lookup"><span data-stu-id="eee15-133">Implementing integration and functional tests for each microservice</span></span>

<span data-ttu-id="eee15-134">如前所述，整合測試和功能測試有不同用途和目標。</span><span class="sxs-lookup"><span data-stu-id="eee15-134">As noted, integration tests and functional tests have different purposes and goals.</span></span> <span data-ttu-id="eee15-135">不過，測試 ASP.NET Core 控制器時兩者的實作方式很類似，因此在這一節讓我們專注於整合測試。</span><span class="sxs-lookup"><span data-stu-id="eee15-135">However, the way you implement both when testing ASP.NET Core controllers is similar, so in this section we concentrate on integration tests.</span></span>

<span data-ttu-id="eee15-136">整合測試可確保應用程式的元件在組合時可正確運作。</span><span class="sxs-lookup"><span data-stu-id="eee15-136">Integration testing ensures that an application's components function correctly when assembled.</span></span> <span data-ttu-id="eee15-137">ASP.NET Core 支援使用單元測試架構和內建測試 Web 主機來進行整合測試，此 Web 主機可以用來處理要求而不會有網路額外負荷。</span><span class="sxs-lookup"><span data-stu-id="eee15-137">ASP.NET Core supports integration testing using unit test frameworks and a built-in test web host that can be used to handle requests without network overhead.</span></span>

<span data-ttu-id="eee15-138">不像單元測試，整合測試經常牽涉到應用程式基礎結構考量，例如資料庫、檔案系統、網路資源或 Web 要求和回應。</span><span class="sxs-lookup"><span data-stu-id="eee15-138">Unlike unit testing, integration tests frequently involve application infrastructure concerns, such as a database, file system, network resources, or web requests and responses.</span></span> <span data-ttu-id="eee15-139">單元測試使用虛假或模擬物件來取代這些考量。</span><span class="sxs-lookup"><span data-stu-id="eee15-139">Unit tests use fakes or mock objects in place of these concerns.</span></span> <span data-ttu-id="eee15-140">但是，整合測試的目的是要確認系統搭配這些系統時如預期般運作，因此進行整合測試時，請勿使用虛假或模擬物件。</span><span class="sxs-lookup"><span data-stu-id="eee15-140">But the purpose of integration tests is to confirm that the system works as expected with these systems, so for integration testing you do not use fakes or mock objects.</span></span> <span data-ttu-id="eee15-141">相反地，您要包含基礎結構，例如資料庫存取或從其他服務進行的服務引動過程。</span><span class="sxs-lookup"><span data-stu-id="eee15-141">Instead, you include the infrastructure, like database access or service invocation from other services.</span></span>

<span data-ttu-id="eee15-142">因為整合測試會執行比單元測試大的程式碼區段，且整合測試會依賴基礎結構項目，所以它們的速度通常和單元測試相比，會呈數量級地變慢。</span><span class="sxs-lookup"><span data-stu-id="eee15-142">Because integration tests exercise larger segments of code than unit tests, and because integration tests rely on infrastructure elements, they tend to be orders of magnitude slower than unit tests.</span></span> <span data-ttu-id="eee15-143">因此，最好限制您撰寫和執行多少整合測試。</span><span class="sxs-lookup"><span data-stu-id="eee15-143">Thus, it is a good idea to limit how many integration tests you write and run.</span></span>

<span data-ttu-id="eee15-144">ASP.NET Core 包含內建的測試 web 主機，可用來處理 HTTP 要求，而不會有網路額外負荷，這表示您可以比使用真正的 web 主機更快執行這些測試。</span><span class="sxs-lookup"><span data-stu-id="eee15-144">ASP.NET Core includes a built-in test web host that can be used to handle HTTP requests without network overhead, meaning that you can run those tests faster than when using a real web host.</span></span> <span data-ttu-id="eee15-145">測試 Web 主機 (TestServer) 可透過 Microsoft.AspNetCore.TestHost NuGet 元件取得。</span><span class="sxs-lookup"><span data-stu-id="eee15-145">The test web host (TestServer) is available in a NuGet component as Microsoft.AspNetCore.TestHost.</span></span> <span data-ttu-id="eee15-146">它可以新增至整合測試專案，並用於裝載 ASP.NET Core 應用程式。</span><span class="sxs-lookup"><span data-stu-id="eee15-146">It can be added to integration test projects and used to host ASP.NET Core applications.</span></span>

<span data-ttu-id="eee15-147">您可以在下列程式碼中看到，當您建立 ASP.NET Core 控制器的整合測試時，您會透過測試主機將控制器具現化。</span><span class="sxs-lookup"><span data-stu-id="eee15-147">As you can see in the following code, when you create integration tests for ASP.NET Core controllers, you instantiate the controllers through the test host.</span></span> <span data-ttu-id="eee15-148">這相當於 HTTP 要求，但執行速度較快。</span><span class="sxs-lookup"><span data-stu-id="eee15-148">This is comparable to an HTTP request, but it runs faster.</span></span>

```csharp
public class PrimeWebDefaultRequestShould
{
    private readonly TestServer _server;
    private readonly HttpClient _client;

    public PrimeWebDefaultRequestShould()
    {
        // Arrange
        _server = new TestServer(new WebHostBuilder()
           .UseStartup<Startup>());
           _client = _server.CreateClient();
    }

    [Fact]
    public async Task ReturnHelloWorld()
    {
        // Act
        var response = await _client.GetAsync("/");
        response.EnsureSuccessStatusCode();
        var responseString = await response.Content.ReadAsStringAsync();
        // Assert
        Assert.Equal("Hello World!", responseString);
    }
}
```

#### <a name="additional-resources"></a><span data-ttu-id="eee15-149">其他資源</span><span class="sxs-lookup"><span data-stu-id="eee15-149">Additional resources</span></span>

- <span data-ttu-id="eee15-150">**Steve Smith。測試控制器** (ASP.NET Core) </span><span class="sxs-lookup"><span data-stu-id="eee15-150">**Steve Smith. Testing controllers** (ASP.NET Core) </span></span>\
    [https://docs.microsoft.com/aspnet/core/mvc/controllers/testing](/aspnet/core/mvc/controllers/testing)

- <span data-ttu-id="eee15-151">**Steve Smith。整合測試** (ASP.NET Core) </span><span class="sxs-lookup"><span data-stu-id="eee15-151">**Steve Smith. Integration testing** (ASP.NET Core) </span></span>\
    [https://docs.microsoft.com/aspnet/core/test/integration-tests](/aspnet/core/test/integration-tests)

- <span data-ttu-id="eee15-152">**使用 dotnet test 的 .NET Core 單元測試** </span><span class="sxs-lookup"><span data-stu-id="eee15-152">**Unit testing in .NET Core using dotnet test** </span></span>\
    [https://docs.microsoft.com/dotnet/core/testing/unit-testing-with-dotnet-test](../../../core/testing/unit-testing-with-dotnet-test.md)

- <span data-ttu-id="eee15-153">**xUnit.net**.</span><span class="sxs-lookup"><span data-stu-id="eee15-153">**xUnit.net**.</span></span> <span data-ttu-id="eee15-154">官方網站。</span><span class="sxs-lookup"><span data-stu-id="eee15-154">Official site.</span></span> \
    <https://xunit.github.io/>

- <span data-ttu-id="eee15-155">**單元測試基本概念。**</span><span class="sxs-lookup"><span data-stu-id="eee15-155">**Unit Test Basics.**</span></span> \
    [https://docs.microsoft.com/visualstudio/test/unit-test-basics](/visualstudio/test/unit-test-basics)

- <span data-ttu-id="eee15-156">**Moq**.</span><span class="sxs-lookup"><span data-stu-id="eee15-156">**Moq**.</span></span> <span data-ttu-id="eee15-157">GitHub 存放庫。</span><span class="sxs-lookup"><span data-stu-id="eee15-157">GitHub repo.</span></span> \
    <https://github.com/moq/moq>

- <span data-ttu-id="eee15-158">**NUnit**。</span><span class="sxs-lookup"><span data-stu-id="eee15-158">**NUnit**.</span></span> <span data-ttu-id="eee15-159">官方網站。</span><span class="sxs-lookup"><span data-stu-id="eee15-159">Official site.</span></span> \
    <https://nunit.org/>

### <a name="implementing-service-tests-on-a-multi-container-application"></a><span data-ttu-id="eee15-160">實作多重容器應用程式上的服務測試</span><span class="sxs-lookup"><span data-stu-id="eee15-160">Implementing service tests on a multi-container application</span></span>

<span data-ttu-id="eee15-161">如前文所述，當您測試多重容器應用程式時，所有微服務都需要在 Docker 主機或容器叢集內執行。</span><span class="sxs-lookup"><span data-stu-id="eee15-161">As noted earlier, when you test multi-container applications, all the microservices need to be running within the Docker host or container cluster.</span></span> <span data-ttu-id="eee15-162">端對端服務測試包含牽涉到數個微服務的多個作業，需要您在 Docker 主機中執行 docker-compose up (如果您使用協調器則是類似的機制) 部署和啟動整個應用程式。</span><span class="sxs-lookup"><span data-stu-id="eee15-162">End-to-end service tests that include multiple operations involving several microservices require you to deploy and start the whole application in the Docker host by running docker-compose up (or a comparable mechanism if you are using an orchestrator).</span></span> <span data-ttu-id="eee15-163">一旦整個應用程式及其所有服務執行之後，您便可以執行端對端整合和功能測試。</span><span class="sxs-lookup"><span data-stu-id="eee15-163">Once the whole application and all its services is running, you can execute end-to-end integration and functional tests.</span></span>

<span data-ttu-id="eee15-164">有一些方法可供您使用。</span><span class="sxs-lookup"><span data-stu-id="eee15-164">There are a few approaches you can use.</span></span> <span data-ttu-id="eee15-165">在您用來部署應用程式的 docker-compose.yml 檔案中，您可以在解決方案層級展開進入點，以使用 [dotnet test](../../../core/tools/dotnet-test.md)。</span><span class="sxs-lookup"><span data-stu-id="eee15-165">In the docker-compose.yml file that you use to deploy the application at the solution level you can expand the entry point to use [dotnet test](../../../core/tools/dotnet-test.md).</span></span> <span data-ttu-id="eee15-166">您也可以使用另一個 compose 檔案，在您目標的映像中執行測試。</span><span class="sxs-lookup"><span data-stu-id="eee15-166">You can also use another compose file that would run your tests in the image you are targeting.</span></span> <span data-ttu-id="eee15-167">藉由針對包含您容器上之微服務和資料庫的整合測試使用另一個 compose 檔案，您可以確保相關的資料永遠重設為其原始狀態，然後才執行測試。</span><span class="sxs-lookup"><span data-stu-id="eee15-167">By using another compose file for integration tests that includes your microservices and databases on containers, you can make sure that the related data is always reset to its original state before running the tests.</span></span>

<span data-ttu-id="eee15-168">compose 應用程式啟動且執行之後，如果您正在執行 Visual Studio，則可以利用中斷點和例外狀況。</span><span class="sxs-lookup"><span data-stu-id="eee15-168">Once the compose application is up and running, you can take advantage of breakpoints and exceptions if you are running Visual Studio.</span></span> <span data-ttu-id="eee15-169">或者，您可以在 Azure DevOps Services 中的 CI 管線，或其他支援 Docker 容器的任何 CI/CD 系統中，自動執行整合測試。</span><span class="sxs-lookup"><span data-stu-id="eee15-169">Or you can run the integration tests automatically in your CI pipeline in Azure DevOps Services or any other CI/CD system that supports Docker containers.</span></span>

## <a name="testing-in-eshoponcontainers"></a><span data-ttu-id="eee15-170">在 eShopOnContainers 中進行測試</span><span class="sxs-lookup"><span data-stu-id="eee15-170">Testing in eShopOnContainers</span></span>

<span data-ttu-id="eee15-171">最近已重組參考應用程式 (eShopOnContainers) 測試，現在有四個類別：</span><span class="sxs-lookup"><span data-stu-id="eee15-171">The reference application (eShopOnContainers) tests were recently restructured and now there are four categories:</span></span>

1. <span data-ttu-id="eee15-172">**單元**測試，只是單純的舊版一般單元測試，包含在 **{MicroserviceName}.UnitTests** 專案中</span><span class="sxs-lookup"><span data-stu-id="eee15-172">**Unit** tests, just plain old regular unit tests, contained in the **{MicroserviceName}.UnitTests** projects</span></span>

2. <span data-ttu-id="eee15-173">**微服務功能/整合測試**，其中測試案例涉及每個微服務的基礎結構，但會與其他項目隔離，且包含在 **{MicroserviceName}.FunctionalTests** 專案中。</span><span class="sxs-lookup"><span data-stu-id="eee15-173">**Microservice functional/integration tests**, with test cases involving the infrastructure for each microservice but isolated from the others and are contained in the **{MicroserviceName}.FunctionalTests** projects.</span></span>

3. <span data-ttu-id="eee15-174">**應用程式功能/整合測試**，著重于微服務整合，以及進行數個微服務的測試案例。</span><span class="sxs-lookup"><span data-stu-id="eee15-174">**Application functional/integration tests**, which focus on microservices integration, with test cases that exert several microservices.</span></span> <span data-ttu-id="eee15-175">這些測試位於 **Application.FunctionalTests** 專案中。</span><span class="sxs-lookup"><span data-stu-id="eee15-175">These tests are located in project **Application.FunctionalTests**.</span></span>

<span data-ttu-id="eee15-176">雖然單元和整合測試是組織在微服務專案內的測試檔案夾中，但應用程式和負載測試會在根資料夾下分開管理，如圖6-25 所示。</span><span class="sxs-lookup"><span data-stu-id="eee15-176">While unit and integration tests are organized in a test folder within the microservice project, application and load tests are managed separately under the root folder, as shown in Figure 6-25.</span></span>

![VS 指出方案中某些測試專案的 VS 螢幕擷取畫面。](./media/test-aspnet-core-services-web-apps/eshoponcontainers-test-folder-structure.png)

<span data-ttu-id="eee15-178">**圖 6-25**。</span><span class="sxs-lookup"><span data-stu-id="eee15-178">**Figure 6-25**.</span></span> <span data-ttu-id="eee15-179">eShopOnContainers 中的測試資料夾結構</span><span class="sxs-lookup"><span data-stu-id="eee15-179">Test folder structure in eShopOnContainers</span></span>

<span data-ttu-id="eee15-180">微服務和應用程式功能/整合測試會使用一般測試執行器從 Visual Studio 執行，但您必須先透過一組包含在解決方案測試資料夾中的 docker-compose 檔案，來啟動必要的基礎結構服務：</span><span class="sxs-lookup"><span data-stu-id="eee15-180">Microservice and Application functional/integration tests are run from Visual Studio, using the regular tests runner, but first you need to start the required infrastructure services, by means of a set of docker-compose files contained in the solution test folder:</span></span>

<span data-ttu-id="eee15-181">**docker-compose-test.yml**</span><span class="sxs-lookup"><span data-stu-id="eee15-181">**docker-compose-test.yml**</span></span>

```yml
version: '3.4'

services:
  redis.data:
    image: redis:alpine
  rabbitmq:
    image: rabbitmq:3-management-alpine
  sqldata:
    image: mcr.microsoft.com/mssql/server:2017-latest
  nosqldata:
    image: mongo
```

<span data-ttu-id="eee15-182">**docker-compose-test.override.yml**</span><span class="sxs-lookup"><span data-stu-id="eee15-182">**docker-compose-test.override.yml**</span></span>

```yml
version: '3.4'

services:
  redis.data:
    ports:
      - "6379:6379"
  rabbitmq:
    ports:
      - "15672:15672"
      - "5672:5672"
  sqldata:
    environment:
      - SA_PASSWORD=Pass@word
      - ACCEPT_EULA=Y
    ports:
      - "5433:1433"
  nosqldata:
    ports:
      - "27017:27017"
```

<span data-ttu-id="eee15-183">因此，若要執行功能/整合測試，您必須先從解決方案測試資料夾執行此命令：</span><span class="sxs-lookup"><span data-stu-id="eee15-183">So, to run the functional/integration tests you must first run this command, from the solution test folder:</span></span>

```console
docker-compose -f docker-compose-test.yml -f docker-compose-test.override.yml up
```

<span data-ttu-id="eee15-184">如您所見，這些 docker-compose 檔案只啟動 Redis、RabbitMQ、SQL Server 和 MongoDB 微服務。</span><span class="sxs-lookup"><span data-stu-id="eee15-184">As you can see, these docker-compose files only start the Redis, RabbitMQ, SQL Server and MongoDB microservices.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="eee15-185">其他資源</span><span class="sxs-lookup"><span data-stu-id="eee15-185">Additional resources</span></span>

- <span data-ttu-id="eee15-186">EShopOnContainers 上的**單元 & 整合測試**</span><span class="sxs-lookup"><span data-stu-id="eee15-186">**Unit & Integration testing** on the eShopOnContainers </span></span>\
    <https://github.com/dotnet-architecture/eShopOnContainers/wiki/Unit-and-integration-testing>

- <span data-ttu-id="eee15-187">EShopOnContainers 上的**負載測試**</span><span class="sxs-lookup"><span data-stu-id="eee15-187">**Load testing** on the eShopOnContainers </span></span>\
    <https://github.com/dotnet-architecture/eShopOnContainers/wiki/Load-testing>

> [!div class="step-by-step"]
> <span data-ttu-id="eee15-188">[上一個](subscribe-events.md) 
> [下一步](background-tasks-with-ihostedservice.md)</span><span class="sxs-lookup"><span data-stu-id="eee15-188">[Previous](subscribe-events.md)
[Next](background-tasks-with-ihostedservice.md)</span></span>
