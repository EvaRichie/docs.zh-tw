---
title: WCF svcutil 工具概觀
description: Microsoft WCF dotnet-svcutil 工具的概觀，此工具可新增 .NET Core 和 ASP.NET Core 專案功能，與 .NET Framework 專案的 WCF svcutil 工具類似。
author: mlacouture
ms.date: 02/22/2019
ms.openlocfilehash: fde42f7d040fba91f51ce6faa58282ed0206a853
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/14/2020
ms.locfileid: "83396211"
---
# <a name="wcf-dotnet-svcutil-tool-for-net-core"></a><span data-ttu-id="36172-103">適用於 .NET Core 的 WCF dotnet-svcutil 工具</span><span class="sxs-lookup"><span data-stu-id="36172-103">WCF dotnet-svcutil tool for .NET Core</span></span>

<span data-ttu-id="36172-104">Windows Communication Foundation （WCF） **dotnet-svcutil**工具是一種 .net 工具，可從網路位置上的 web 服務或從 WSDL 檔案抓取中繼資料，並產生包含用戶端 proxy 方法的 WCF 類別來存取 web 服務作業。</span><span class="sxs-lookup"><span data-stu-id="36172-104">The Windows Communication Foundation (WCF) **dotnet-svcutil** tool is a .NET tool that retrieves metadata from a web service on a network location or from a WSDL file, and generates a WCF class containing client proxy methods that access the web service operations.</span></span>

<span data-ttu-id="36172-105">類似適用於 .NET Framework 專案的 [**Service Model Metadata - svcutil**](../../framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 工具，**dotnet-svcutil** 是一種命令列工具，可用來產生與 .NET Core 和 .NET Standard 專案相容的 Web 服務參考。</span><span class="sxs-lookup"><span data-stu-id="36172-105">Similar to the [**Service Model Metadata - svcutil**](../../framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) tool for .NET Framework projects, the **dotnet-svcutil** is a command-line tool for generating a web service reference compatible with .NET Core and .NET Standard projects.</span></span>

<span data-ttu-id="36172-106">**Dotnet-svcutil**工具是[**WCF Web 服務參考**](wcf-web-service-reference-guide.md)Visual Studio 連線服務提供者的替代選項，第一次隨附于 Visual Studio 2017 15.5 版。</span><span class="sxs-lookup"><span data-stu-id="36172-106">The **dotnet-svcutil** tool is an alternative option to the [**WCF Web Service Reference**](wcf-web-service-reference-guide.md) Visual Studio connected service provider that first shipped with Visual Studio 2017 version 15.5.</span></span> <span data-ttu-id="36172-107">**Dotnet-svcutil** tool as a .net tool 提供跨平臺的 Linux、MacOS 和 Windows。</span><span class="sxs-lookup"><span data-stu-id="36172-107">The **dotnet-svcutil** tool as a .NET tool, is available cross-platform on Linux, macOS, and Windows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="36172-108">您只應該參考來自信任來源的服務。</span><span class="sxs-lookup"><span data-stu-id="36172-108">You should only reference services from a trusted source.</span></span> <span data-ttu-id="36172-109">新增不信任來源的參考可能會危及安全性。</span><span class="sxs-lookup"><span data-stu-id="36172-109">Adding references from an untrusted source may compromise security.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36172-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="36172-110">Prerequisites</span></span>

<!-- markdownlint-disable MD025 -->

# <a name="dotnet-svcutil-2x"></a>[<span data-ttu-id="36172-111">dotnet-svcutil 2.x</span><span class="sxs-lookup"><span data-stu-id="36172-111">dotnet-svcutil 2.x</span></span>](#tab/dotnetsvcutil2x)

- <span data-ttu-id="36172-112">[.Net Core 2.1 SDK](https://dotnet.microsoft.com/download)或更新版本</span><span class="sxs-lookup"><span data-stu-id="36172-112">[.NET Core 2.1 SDK](https://dotnet.microsoft.com/download) or later versions</span></span>
- <span data-ttu-id="36172-113">您慣用的程式碼編輯器</span><span class="sxs-lookup"><span data-stu-id="36172-113">Your favorite code editor</span></span>

# <a name="dotnet-svcutil-1x"></a>[<span data-ttu-id="36172-114">dotnet-svcutil 1.x</span><span class="sxs-lookup"><span data-stu-id="36172-114">dotnet-svcutil 1.x</span></span>](#tab/dotnetsvcutil1x)

- <span data-ttu-id="36172-115">[.NET Core 1.0.4 SDK](https://dotnet.microsoft.com/download) 或更新版本</span><span class="sxs-lookup"><span data-stu-id="36172-115">[.NET Core 1.0.4 SDK](https://dotnet.microsoft.com/download) or later versions</span></span>
- <span data-ttu-id="36172-116">您慣用的程式碼編輯器</span><span class="sxs-lookup"><span data-stu-id="36172-116">Your favorite code editor</span></span>

---

## <a name="getting-started"></a><span data-ttu-id="36172-117">開始使用</span><span class="sxs-lookup"><span data-stu-id="36172-117">Getting started</span></span>

<span data-ttu-id="36172-118">下列範例會引導您完成將 Web 服務參考新增到 .NET Core Web 專案並叫用服務的必要步驟。</span><span class="sxs-lookup"><span data-stu-id="36172-118">The following example walks you through the steps required to add a web service reference to a .NET Core web project and invoke the service.</span></span> <span data-ttu-id="36172-119">您建立名為 *HelloSvcutil* 的 .NET Core Web 應用程式，並對實作下列合約的 Web 服務新增參考：</span><span class="sxs-lookup"><span data-stu-id="36172-119">You'll create a .NET Core web application named *HelloSvcutil* and add a reference to a web service that implements the following contract:</span></span>

```csharp
[ServiceContract]
public interface ISayHello
{
    [OperationContract]
    string Hello(string name);
}
```

<span data-ttu-id="36172-120">對於此範例，我們假設 Web 服務裝載於下列位址：`http://contoso.com/SayHello.svc`</span><span class="sxs-lookup"><span data-stu-id="36172-120">For this example, let's assume the web service will be hosted at the following address: `http://contoso.com/SayHello.svc`</span></span>

<span data-ttu-id="36172-121">從 Windows、macOS 或 Linux 命令視窗執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="36172-121">From a Windows, macOS, or Linux command window perform the following steps:</span></span>

1. <span data-ttu-id="36172-122">為您的專案建立一個名為 _HelloSvcutil_ 的目錄，然後讓它成為您目前所在的目錄，如下列範例中所示：</span><span class="sxs-lookup"><span data-stu-id="36172-122">Create a directory named _HelloSvcutil_ for your project and make it your current directory, as in the following example:</span></span>

    ```console
    mkdir HelloSvcutil
    cd HelloSvcutil
    ```

2. <span data-ttu-id="36172-123">使用命令在該目錄中建立新的 c # Web 專案，如下所示 [`dotnet new`](../tools/dotnet-new.md) ：</span><span class="sxs-lookup"><span data-stu-id="36172-123">Create a new C# web project in that directory using the [`dotnet new`](../tools/dotnet-new.md) command as follows:</span></span>

    ```dotnetcli
    dotnet new web
    ```

3. <span data-ttu-id="36172-124">將[ `dotnet-svcutil` NuGet 套件](https://nuget.org/packages/dotnet-svcutil)安裝為 CLI 工具： </span><span class="sxs-lookup"><span data-stu-id="36172-124">Install the [`dotnet-svcutil` NuGet package](https://nuget.org/packages/dotnet-svcutil) as a CLI tool:  </span></span><!-- markdownlint-disable MD023 -->
    # <a name="dotnet-svcutil-2x"></a>[<span data-ttu-id="36172-125">dotnet-svcutil 2.x</span><span class="sxs-lookup"><span data-stu-id="36172-125">dotnet-svcutil 2.x</span></span>](#tab/dotnetsvcutil2x)

    ```dotnetcli
    dotnet tool install --global dotnet-svcutil
    ```

    # <a name="dotnet-svcutil-1x"></a>[<span data-ttu-id="36172-126">dotnet-svcutil 1.x</span><span class="sxs-lookup"><span data-stu-id="36172-126">dotnet-svcutil 1.x</span></span>](#tab/dotnetsvcutil1x)
    <span data-ttu-id="36172-127">`HelloSvcutil.csproj`在您的編輯器中開啟專案檔，編輯 `Project` 元素，然後使用下列程式碼，將[ `dotnet-svcutil` NUGET 套件](https://nuget.org/packages/dotnet-svcutil)新增為 CLI 工具參考：</span><span class="sxs-lookup"><span data-stu-id="36172-127">Open the `HelloSvcutil.csproj` project file in your editor, edit the `Project` element, and add the [`dotnet-svcutil` NuGet package](https://nuget.org/packages/dotnet-svcutil) as a CLI tool reference, using the following code:</span></span>

    ```xml
    <ItemGroup>
      <DotNetCliToolReference Include="dotnet-svcutil" Version="1.0.*" />
    </ItemGroup>
    ```

    <span data-ttu-id="36172-128">接著使用 [`dotnet restore`](../tools/dotnet-restore.md) 命令還原 _dotnet-svcutil_ 套件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="36172-128">Then restore the _dotnet-svcutil_ package using the [`dotnet restore`](../tools/dotnet-restore.md) command as follows:</span></span>

    ```dotnetcli
    dotnet restore
    ```

    ---

4. <span data-ttu-id="36172-129">執行 _dotnet-svcutil_ 命令以產生 Web 服務參考檔案，如下所示：</span><span class="sxs-lookup"><span data-stu-id="36172-129">Run the _dotnet-svcutil_ command to generate the web service reference file as follows:</span></span>

    # <a name="dotnet-svcutil-2x"></a>[<span data-ttu-id="36172-130">dotnet-svcutil 2.x</span><span class="sxs-lookup"><span data-stu-id="36172-130">dotnet-svcutil 2.x</span></span>](#tab/dotnetsvcutil2x)

    ```dotnetcli
    dotnet-svcutil http://contoso.com/SayHello.svc
    ```

    # <a name="dotnet-svcutil-1x"></a>[<span data-ttu-id="36172-131">dotnet-svcutil 1.x</span><span class="sxs-lookup"><span data-stu-id="36172-131">dotnet-svcutil 1.x</span></span>](#tab/dotnetsvcutil1x)

    ```dotnetcli
    dotnet svcutil http://contoso.com/SayHello.svc
    ```

    ---

<span data-ttu-id="36172-132">產生的檔案會儲存為 _HelloSvcutil/ServiceReference/Reference.cs_。</span><span class="sxs-lookup"><span data-stu-id="36172-132">The generated file is saved as _HelloSvcutil/ServiceReference/Reference.cs_.</span></span> <span data-ttu-id="36172-133">_Dotnet-svcutil_工具也會將 proxy 程式碼所需的適當 WCF 封裝當做封裝參考新增至專案。</span><span class="sxs-lookup"><span data-stu-id="36172-133">The _dotnet-svcutil_ tool also adds to the project the appropriate WCF packages required by the proxy code as package references.</span></span>

## <a name="using-the-service-reference"></a><span data-ttu-id="36172-134">使用服務參考</span><span class="sxs-lookup"><span data-stu-id="36172-134">Using the Service Reference</span></span>

1. <span data-ttu-id="36172-135">使用命令還原 WCF 封裝 [`dotnet restore`](../tools/dotnet-restore.md) ，如下所示：</span><span class="sxs-lookup"><span data-stu-id="36172-135">Restore the WCF packages using the [`dotnet restore`](../tools/dotnet-restore.md) command as follows:</span></span>

    ```dotnetcli
    dotnet restore
    ```

2. <span data-ttu-id="36172-136">尋找您要使用的用戶端類別與作業名稱。</span><span class="sxs-lookup"><span data-stu-id="36172-136">Find the name of the client class and operation you want to use.</span></span> <span data-ttu-id="36172-137">`Reference.cs` 會包含繼承自 `System.ServiceModel.ClientBase`的類別，並有可用來在服務上呼叫作業的方法。</span><span class="sxs-lookup"><span data-stu-id="36172-137">`Reference.cs` will contain a class that inherits from `System.ServiceModel.ClientBase`, with methods that can be used to call operations on the service.</span></span> <span data-ttu-id="36172-138">在此例中，您想要呼叫 _SayHello_ 服務的 _Hello_ 作業。</span><span class="sxs-lookup"><span data-stu-id="36172-138">In this example, you want to call the _SayHello_ service's _Hello_ operation.</span></span> <span data-ttu-id="36172-139">`ServiceReference.SayHelloClient` 是用戶端類別的名稱，並有稱為 `HelloAsync` 的方法，可用來呼叫作業。</span><span class="sxs-lookup"><span data-stu-id="36172-139">`ServiceReference.SayHelloClient` is the name of the client class, and has a method called `HelloAsync` that can be used to call the operation.</span></span>

3. <span data-ttu-id="36172-140">`Startup.cs`在您的編輯器中開啟檔案，並在 `using` 頂端加入服務參考命名空間的指示詞：</span><span class="sxs-lookup"><span data-stu-id="36172-140">Open the `Startup.cs` file in your editor, and add a `using` directive for the service reference namespace at the top:</span></span>

    ```csharp
    using ServiceReference;
    ```

4. <span data-ttu-id="36172-141">編輯 `Configure` 方法以叫用 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="36172-141">Edit the `Configure` method to invoke the web service.</span></span> <span data-ttu-id="36172-142">若要這樣做，請建立繼承自 `ClientBase` 的類別執行個體，然後在用戶端物件呼叫方法：</span><span class="sxs-lookup"><span data-stu-id="36172-142">You do this by creating an instance of the class that inherits from `ClientBase` and calling the method on the client object:</span></span>

    ```csharp
    public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
    {
        if (env.IsDevelopment())
        {
            app.UseDeveloperExceptionPage();
        }

        app.Run(async (context) =>
        {
            var client = new SayHelloClient();
            var response = await client.HelloAsync();
            await context.Response.WriteAsync(response);
        });
    }

    ```

5. <span data-ttu-id="36172-143">使用命令執行應用程式，如下所示 [`dotnet run`](../tools/dotnet-run.md) ：</span><span class="sxs-lookup"><span data-stu-id="36172-143">Run the application using the [`dotnet run`](../tools/dotnet-run.md) command as follows:</span></span>

    ```dotnetcli
    dotnet run
    ```

6. <span data-ttu-id="36172-144">在您的網頁瀏覽器中，瀏覽到主控台列出的 URL (例如 `http://localhost:5000`)。</span><span class="sxs-lookup"><span data-stu-id="36172-144">Navigate to the URL listed in the console (for example, `http://localhost:5000`) in your web browser.</span></span>

<span data-ttu-id="36172-145">您應該會看見下列輸出："Hello dotnet-svcutil!"</span><span class="sxs-lookup"><span data-stu-id="36172-145">You should see the following output: "Hello dotnet-svcutil!"</span></span>

<span data-ttu-id="36172-146">如需 `dotnet-svcutil` 工具參數的詳細說明，請依下列所示叫用工具並傳遞 help 參數：</span><span class="sxs-lookup"><span data-stu-id="36172-146">For a detailed description of the `dotnet-svcutil` tool parameters, invoke the tool passing the help parameter as follows:</span></span>
# <a name="dotnet-svcutil-2x"></a>[<span data-ttu-id="36172-147">dotnet-svcutil 2.x</span><span class="sxs-lookup"><span data-stu-id="36172-147">dotnet-svcutil 2.x</span></span>](#tab/dotnetsvcutil2x)

```dotnetcli
dotnet-svcutil --help
```

# <a name="dotnet-svcutil-1x"></a>[<span data-ttu-id="36172-148">dotnet-svcutil 1.x</span><span class="sxs-lookup"><span data-stu-id="36172-148">dotnet-svcutil 1.x</span></span>](#tab/dotnetsvcutil1x)

```dotnetcli
dotnet svcutil --help
```

---

## <a name="feedback--questions"></a><span data-ttu-id="36172-149">意見反應和問題</span><span class="sxs-lookup"><span data-stu-id="36172-149">Feedback & questions</span></span>

<span data-ttu-id="36172-150">如果您有任何問題或意見反應，請[在 GitHub 上開啟問題](https://github.com/dotnet/wcf/issues/new)。</span><span class="sxs-lookup"><span data-stu-id="36172-150">If you have any questions or feedback, [open an issue on GitHub](https://github.com/dotnet/wcf/issues/new).</span></span> <span data-ttu-id="36172-151">您也可以[在 GitHub 的 WCF 存放庫](https://github.com/dotnet/wcf/issues?utf8=%E2%9C%93&q=is:issue%20label:tooling)檢閱任何現有問題或議題。</span><span class="sxs-lookup"><span data-stu-id="36172-151">You can also review any existing questions or issues [at the WCF repo on GitHub](https://github.com/dotnet/wcf/issues?utf8=%E2%9C%93&q=is:issue%20label:tooling).</span></span>

## <a name="release-notes"></a><span data-ttu-id="36172-152">版本資訊</span><span class="sxs-lookup"><span data-stu-id="36172-152">Release notes</span></span>

- <span data-ttu-id="36172-153">如需已更新的版本資訊，請參閱[版本資訊](https://github.com/dotnet/wcf/blob/master/release-notes/dotnet-svcutil-notes.md) (包含已知問題)。</span><span class="sxs-lookup"><span data-stu-id="36172-153">Refer to the [Release notes](https://github.com/dotnet/wcf/blob/master/release-notes/dotnet-svcutil-notes.md) for updated release information, including known issues.</span></span>

## <a name="information"></a><span data-ttu-id="36172-154">資訊</span><span class="sxs-lookup"><span data-stu-id="36172-154">Information</span></span>

- <span data-ttu-id="36172-155">[dotnet-svcutil NuGet 套件](https://nuget.org/packages/dotnet-svcutil) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="36172-155">[dotnet-svcutil NuGet Package](https://nuget.org/packages/dotnet-svcutil)</span></span>
