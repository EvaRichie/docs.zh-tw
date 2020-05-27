---
title: 使用 CLI 開始使用 .NET Core
description: 逐步教學課程示範如何使用 .NET Core CLI 在 Windows、Linux 或 macOS 上開始使用 .NET Core。
author: thraka
ms.author: adegeo
ms.date: 12/05/2019
ms.technology: dotnet-cli
ms.custom: updateeachrelease
ms.openlocfilehash: 7658f2498b87a90b3925d83628f6ea9247a2fc15
ms.sourcegitcommit: e5772b3ddcc114c80b4c9767ffdb3f6c7fad8f05
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/26/2020
ms.locfileid: "83840867"
---
# <a name="get-started-with-net-core-using-the-net-core-cli"></a><span data-ttu-id="f0ee3-103">使用 .NET Core CLI 開始使用 .NET Core</span><span class="sxs-lookup"><span data-stu-id="f0ee3-103">Get started with .NET Core using the .NET Core CLI</span></span>

<span data-ttu-id="f0ee3-104">本文將說明如何開始開發使用 .NET Core CLI 在 Windows、Linux 和 macOS 上工作的 .NET Core 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-104">This article will show you how to start developing .NET Core apps that work on Windows, Linux, and macOS using the .NET Core CLI.</span></span>

<span data-ttu-id="f0ee3-105">如果您不熟悉 .NET Core CLI，請參閱[.NET Core CLI 總覽](../tools/index.md)。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-105">If you're unfamiliar with the .NET Core CLI, see the [.NET Core CLI overview](../tools/index.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0ee3-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="f0ee3-106">Prerequisites</span></span>

- <span data-ttu-id="f0ee3-107">[.NET Core SDK 3.1](https://dotnet.microsoft.com/download)或更新版本。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-107">[.NET Core SDK 3.1](https://dotnet.microsoft.com/download) or later versions.</span></span>
- <span data-ttu-id="f0ee3-108">您偏好的文字編輯器或程式碼編輯器。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-108">A text editor or code editor of your choice.</span></span>

## <a name="hello-console-app"></a><span data-ttu-id="f0ee3-109">嗨，主控台應用程式！</span><span class="sxs-lookup"><span data-stu-id="f0ee3-109">Hello, Console App!</span></span>

<span data-ttu-id="f0ee3-110">您可以從 dotnet/samples GitHub 存放庫[檢視或下載範例程式碼](https://github.com/dotnet/samples/tree/master/core/console-apps/HelloMsBuild)。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-110">You can [view or download the sample code](https://github.com/dotnet/samples/tree/master/core/console-apps/HelloMsBuild) from the dotnet/samples GitHub repository.</span></span> <span data-ttu-id="f0ee3-111">如需下載指示，請參閱[範例和教學課程](../../samples-and-tutorials/index.md#viewing-and-downloading-samples)。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-111">For download instructions, see [Samples and Tutorials](../../samples-and-tutorials/index.md#viewing-and-downloading-samples).</span></span>

<span data-ttu-id="f0ee3-112">開啟命令提示字元，並建立名為 *Hello* 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-112">Open a command prompt and create a folder named *Hello*.</span></span> <span data-ttu-id="f0ee3-113">流覽至您所建立的資料夾，然後輸入下列文字。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-113">Navigate to the folder you created and type the following.</span></span>

```dotnetcli
dotnet new console
dotnet run
```

<span data-ttu-id="f0ee3-114">讓我們快速逐步解說︰</span><span class="sxs-lookup"><span data-stu-id="f0ee3-114">Let's do a quick walkthrough:</span></span>

01. `dotnet new console`

    <span data-ttu-id="f0ee3-115">[dotnet new](../tools/dotnet-new.md)會以建立主控台應用程式所需的相依性，建立最新的*Hello .csproj*專案檔案。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-115">[dotnet new](../tools/dotnet-new.md) creates an up-to-date *Hello.csproj* project file with the dependencies necessary to build a console app.</span></span> <span data-ttu-id="f0ee3-116">它也會建立一個*Program.cs*，這是一個基本檔案，其中包含應用程式的進入點。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-116">It also creates a *Program.cs*, a basic file containing the entry point for the application.</span></span>

    <span data-ttu-id="f0ee3-117">您*好，.csproj*：</span><span class="sxs-lookup"><span data-stu-id="f0ee3-117">*Hello.csproj*:</span></span>

    [!code-xml[Hello.csproj](~/samples/snippets/core/tutorials/cli-create-console-app/HelloMsBuild/csharp/Hello.csproj)]

    <span data-ttu-id="f0ee3-118">專案檔會指定還原相依性和建置程式所需的所有內容。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-118">The project file specifies everything that's needed to restore dependencies and build the program.</span></span>

    - <span data-ttu-id="f0ee3-119">`<OutputType>`元素會指定我們要建立可執行檔，亦即主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-119">The `<OutputType>` element specifies that we're building an executable, in other words a console application.</span></span>
    - <span data-ttu-id="f0ee3-120">`<TargetFramework>`元素會指定我們以何種 .net 實作為目標。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-120">The `<TargetFramework>` element specifies what .NET implementation we're targeting.</span></span> <span data-ttu-id="f0ee3-121">在進階案例中，您可以指定多個目標架構，並在單一作業中建置這全部的架構。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-121">In an advanced scenario, you can specify multiple target frameworks and build to all those in a single operation.</span></span> <span data-ttu-id="f0ee3-122">在本教學課程中，我們將只針對 .NET Core 3.1 進行建立。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-122">In this tutorial, we'll stick to building only for .NET Core 3.1.</span></span>

    <span data-ttu-id="f0ee3-123">*Program.cs*：</span><span class="sxs-lookup"><span data-stu-id="f0ee3-123">*Program.cs*:</span></span>

    [!code-csharp[Program.cs](~/samples/snippets/core/tutorials/cli-create-console-app/HelloMsBuild/csharp/Program.cs)]

    <span data-ttu-id="f0ee3-124">程式是透過 `using System` 來啟動，這表示「將 `System` 命名空間中的所有內容帶入這個檔案的範圍內」。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-124">The program starts by `using System`, which means "bring everything in the `System` namespace into scope for this file".</span></span> <span data-ttu-id="f0ee3-125">`System`命名空間包含 `Console` 類別。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-125">The `System` namespace includes the `Console` class.</span></span>

    <span data-ttu-id="f0ee3-126">然後，我們會定義稱為 `Hello` 的命名空間。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-126">We then define a namespace called `Hello`.</span></span> <span data-ttu-id="f0ee3-127">您可以將其變更為任何所需的位置。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-127">You can change this to anything you want.</span></span> <span data-ttu-id="f0ee3-128">名為 `Program` 的類別是在該命名空間內定義，其中包含的 `Main` 方法會接受名為的字串陣列 `args` 。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-128">A class named `Program` is defined within that namespace, with a `Main` method that takes an array of strings named `args`.</span></span> <span data-ttu-id="f0ee3-129">此陣列包含執行程式時傳入的引數清單。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-129">This array contains the list of arguments passed in when the program is run.</span></span> <span data-ttu-id="f0ee3-130">就像這樣，此陣列不會使用，而且程式只會寫入文字 "Hello World！"</span><span class="sxs-lookup"><span data-stu-id="f0ee3-130">As it is, this array is not used and the program simply writes the text "Hello World!"</span></span> <span data-ttu-id="f0ee3-131">到主控台。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-131">to the console.</span></span> <span data-ttu-id="f0ee3-132">稍後，我們將變更程式碼以便使用此引數。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-132">Later, we'll make changes to the code that will make use of this argument.</span></span>

    <span data-ttu-id="f0ee3-133">`dotnet new`會以隱含方式呼叫[dotnet restore](../tools/dotnet-restore.md) 。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-133">`dotnet new` calls [dotnet restore](../tools/dotnet-restore.md) implicitly.</span></span> <span data-ttu-id="f0ee3-134">`dotnet restore` 呼叫 [NuGet](https://www.nuget.org/) (.NET 套件管理員)，以還原相依性的樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-134">`dotnet restore` calls into [NuGet](https://www.nuget.org/) (.NET package manager) to restore the tree of dependencies.</span></span> <span data-ttu-id="f0ee3-135">NuGet 會分析 Hello.csproj\*\* 檔案、下載檔案中所述的相依性 (或從您電腦上的快取抓取)，並寫入 obj/project.assets.json\*\* 檔案，該檔案是編譯及執行範例的必要項目。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-135">NuGet analyzes the *Hello.csproj* file, downloads the dependencies defined in the file (or grabs them from a cache on your machine), and writes the *obj/project.assets.json* file, which is necessary to compile and run the sample.</span></span>

02. `dotnet run`

    <span data-ttu-id="f0ee3-136">[dotnet run](../tools/dotnet-run.md)會呼叫[dotnet 組建](../tools/dotnet-build.md)，以確保組建目標已建立，然後呼叫 `dotnet <assembly.dll>` 以執行目標應用程式。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-136">[dotnet run](../tools/dotnet-run.md) calls [dotnet build](../tools/dotnet-build.md) to ensure that the build targets have been built, and then calls `dotnet <assembly.dll>` to run the target application.</span></span>

    ```dotnetcli
    dotnet run
    ```

    <span data-ttu-id="f0ee3-137">您會取得下列輸出。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-137">You get the following output.</span></span>

    ```console
    Hello World!
    ```

    <span data-ttu-id="f0ee3-138">或者，您也可以執行 `dotnet build` 來編譯器代碼，而不需執行組建主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-138">Alternatively, you can also run `dotnet build` to compile the code without running the build console applications.</span></span> <span data-ttu-id="f0ee3-139">這會根據專案的名稱，以 DLL 檔案的形式產生已編譯的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-139">This results in a compiled application, as a DLL file, based on the name of the project.</span></span> <span data-ttu-id="f0ee3-140">在此情況下，所建立的檔案會命名為*Hello .dll*。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-140">In this case, the file created is named *Hello.dll*.</span></span> <span data-ttu-id="f0ee3-141">此應用程式可以 `dotnet bin\Debug\netcoreapp3.1\Hello.dll` 在 Windows 上搭配執行（用於 `/` 非 windows 系統）。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-141">This app can be run with `dotnet bin\Debug\netcoreapp3.1\Hello.dll` on Windows (use `/` for non-Windows systems).</span></span>

    ```dotnetcli
    dotnet bin\Debug\netcoreapp3.1\Hello.dll
    ```

    <span data-ttu-id="f0ee3-142">您會取得下列輸出。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-142">You get the following output.</span></span>

    ```console
    Hello World!
    ```

    <span data-ttu-id="f0ee3-143">在編譯應用程式時，會連同建立作業系統特定的可執行檔 `Hello.dll` 。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-143">When the app is compiled, an operating system-specific executable was created along with the `Hello.dll`.</span></span> <span data-ttu-id="f0ee3-144">在 Windows 上，這會是 `Hello.exe` ; 在 Linux 或 macOS 上，這會是 `hello` 。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-144">On Windows, this would be `Hello.exe`; on Linux or macOS, this would be `hello`.</span></span> <span data-ttu-id="f0ee3-145">在上述範例中，檔案會以或命名 `Hello.exe` `Hello` 。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-145">With the example above, the file is named with `Hello.exe` or `Hello`.</span></span> <span data-ttu-id="f0ee3-146">您可以直接執行該可執行檔。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-146">You can run that executable directly.</span></span>

    ```console
    .\bin\Debug\netcoreapp3.1\Hello.exe

    Hello World!
    ```

## <a name="modify-the-program"></a><span data-ttu-id="f0ee3-147">修改程式</span><span class="sxs-lookup"><span data-stu-id="f0ee3-147">Modify the program</span></span>

<span data-ttu-id="f0ee3-148">讓我們稍微變更程式。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-148">Let's change the program a bit.</span></span> <span data-ttu-id="f0ee3-149">斐波里的數位很有趣，因此讓我們新增它，並使用引數來歡迎執行應用程式的人員。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-149">Fibonacci numbers are fun, so let's add that and also to use the argument to greet the person running the app.</span></span>

01. <span data-ttu-id="f0ee3-150">以下列程式碼取代 *Program.cs* 檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="f0ee3-150">Replace the contents of your *Program.cs*  file with the following code:</span></span>

    [!code-csharp[Fibonacci](~/samples/snippets/core/tutorials/cli-create-console-app/fibonacci-msbuild/csharp/Program.cs)]

02. <span data-ttu-id="f0ee3-151">執行[dotnet build](../tools/dotnet-build.md)以編譯變更。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-151">Run [dotnet build](../tools/dotnet-build.md) to compile the changes.</span></span>

03. <span data-ttu-id="f0ee3-152">執行程式，將參數傳遞至應用程式。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-152">Run the program passing a parameter to the app.</span></span> <span data-ttu-id="f0ee3-153">當您使用 `dotnet` 命令來執行應用程式時，請將新增 `--` 至結尾。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-153">When you use the `dotnet` command to run an app, add `--` to the end.</span></span> <span data-ttu-id="f0ee3-154">右邊的任何專案 `--` 都會當做參數傳遞至應用程式。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-154">Anything to the right of `--` will be passed as a parameter to the app.</span></span> <span data-ttu-id="f0ee3-155">在下列範例中，會將值 `John` 傳遞給應用程式。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-155">In the following example, the value `John` is passed to the app.</span></span>

    ```dotnetcli
    dotnet run -- John
    ```

    <span data-ttu-id="f0ee3-156">您會取得下列輸出。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-156">You get the following output.</span></span>

    ```console
    Hello John!
    Fibonacci Numbers 1-15:
    1: 0
    2: 1
    3: 1
    4: 2
    5: 3
    6: 5
    7: 8
    8: 13
    9: 21
    10: 34
    11: 55
    12: 89
    13: 144
    14: 233
    15: 377
    ```

<span data-ttu-id="f0ee3-157">這樣就大功告成了！</span><span class="sxs-lookup"><span data-stu-id="f0ee3-157">And that's it!</span></span> <span data-ttu-id="f0ee3-158">您可以用您喜歡的任何方式修改*Program.cs* 。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-158">You can modify *Program.cs* any way you like.</span></span>

## <a name="working-with-multiple-files"></a><span data-ttu-id="f0ee3-159">使用多個檔案</span><span class="sxs-lookup"><span data-stu-id="f0ee3-159">Working with multiple files</span></span>

<span data-ttu-id="f0ee3-160">單一檔案適用于簡單的一次性程式，但如果您要建立更複雜的應用程式，您的專案可能會有多個程式碼檔案。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-160">Single files are fine for simple one-off programs, but if you're building a more complex app, you're probably going to have multiple code files on your project.</span></span> <span data-ttu-id="f0ee3-161">請藉由快取某些 Fibonacci 值，再新增一些遞迴功能，從先前的 Fibonacci 範例開始建置。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-161">Let's build off of the previous Fibonacci example by caching some Fibonacci values and add some recursive features.</span></span>

01. <span data-ttu-id="f0ee3-162">使用下列程式碼在 *Hello* 目錄中新增名為 *FibonacciGenerator.cs* 的檔案：</span><span class="sxs-lookup"><span data-stu-id="f0ee3-162">Add a new file inside the *Hello* directory named *FibonacciGenerator.cs* with the following code:</span></span>

    [!code-csharp[Fibonacci Generator](~/samples/snippets/core/tutorials/cli-create-console-app/FibonacciBetterMsBuild/csharp/FibonacciGenerator.cs)]

02. <span data-ttu-id="f0ee3-163">變更 *Program.cs* 檔案中的 `Main` 方法，以具現化新的類別並呼叫其方法，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="f0ee3-163">Change the `Main` method in your *Program.cs* file to instantiate the new class and call its method as in the following example:</span></span>

    [!code-csharp[New Program.cs](~/samples/snippets/core/tutorials/cli-create-console-app/FibonacciBetterMsBuild/csharp/Program.cs)]

03. <span data-ttu-id="f0ee3-164">執行[dotnet build](../tools/dotnet-build.md)以編譯變更。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-164">Run [dotnet build](../tools/dotnet-build.md) to compile the changes.</span></span>

04. <span data-ttu-id="f0ee3-165">執行[dotnet run](../tools/dotnet-run.md)來執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-165">Run your app by executing [dotnet run](../tools/dotnet-run.md).</span></span>

    ```dotnetcli
    dotnet run
    ```

    <span data-ttu-id="f0ee3-166">您會取得下列輸出。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-166">You get the following output.</span></span>

    ```console
    0
    1
    1
    2
    3
    5
    8
    13
    21
    34
    55
    89
    144
    233
    377
    ```

## <a name="publish-your-app"></a><span data-ttu-id="f0ee3-167">發佈您的應用程式</span><span class="sxs-lookup"><span data-stu-id="f0ee3-167">Publish your app</span></span>

<span data-ttu-id="f0ee3-168">準備好散發應用程式之後，請使用[dotnet publish](../tools/dotnet-publish.md)命令來產生_bin \\ debug \\ netcoreapp 3.1 \\ publish \\ _ （用於_publish_ `/` 非 Windows 系統）的 publish 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-168">Once you're ready to distribute your app, use the [dotnet publish](../tools/dotnet-publish.md) command to generate the _publish_ folder at _bin\\debug\\netcoreapp3.1\\publish\\_ (use `/` for non-Windows systems).</span></span> <span data-ttu-id="f0ee3-169">您可以將 _publish_  資料夾的內容散發到其他平台，只要那些平台已安裝 dotnet 執行階段。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-169">You can distribute the contents of the _publish_ folder to other platforms as long as they've already installed the dotnet runtime.</span></span>

```dotnetcli
dotnet publish
```

<span data-ttu-id="f0ee3-170">您會取得如下所示的輸出。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-170">You get output similar to the following.</span></span>

```console
Microsoft (R) Build Engine version 16.4.0+e901037fe for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 20 ms for C:\Code\Temp\Hello\Hello.csproj.
  Hello -> C:\Code\Temp\Hello\bin\Debug\netcoreapp3.1\Hello.dll
  Hello -> C:\Code\Temp\Hello\bin\Debug\netcoreapp3.1\publish\
```

<span data-ttu-id="f0ee3-171">上述輸出可能會根據您目前的資料夾和作業系統而有所不同，但輸出應該類似。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-171">The output above may differ based on your current folder and operating system, but the output should be similar.</span></span>

<span data-ttu-id="f0ee3-172">您可以使用 [dotnet](../tools/dotnet.md) 命令來執行已發佈的應用程式：</span><span class="sxs-lookup"><span data-stu-id="f0ee3-172">You can run your published app with the [dotnet](../tools/dotnet.md) command:</span></span>

```dotnetcli
dotnet bin\Debug\netcoreapp3.1\publish\Hello.dll
```

<span data-ttu-id="f0ee3-173">您會取得下列輸出。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-173">You get the following output.</span></span>

```console
0
1
1
2
3
5
8
13
21
34
55
89
144
233
377
```

<span data-ttu-id="f0ee3-174">如同本文開頭所述，作業系統特定的可執行檔是連同一併建立的 `Hello.dll` 。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-174">As mentioned at the start of this article, an operating system-specific executable was created along with the `Hello.dll`.</span></span> <span data-ttu-id="f0ee3-175">在 Windows 上，這會是 `Hello.exe` ; 在 Linux 或 macOS 上，這會是 `hello` 。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-175">On Windows, this would be `Hello.exe`; on Linux or macOS, this would be `hello`.</span></span> <span data-ttu-id="f0ee3-176">在上述範例中，檔案會以或命名 `Hello.exe` `Hello` 。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-176">With the example above, the file is named with `Hello.exe` or `Hello`.</span></span> <span data-ttu-id="f0ee3-177">您可以直接執行這個已發行的可執行檔。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-177">You can run this published executable directly.</span></span>

```console
.\bin\Debug\netcoreapp3.1\publish\Hello.exe

0
1
1
2
3
5
8
13
21
34
55
89
144
233
377
```

## <a name="conclusion"></a><span data-ttu-id="f0ee3-178">結論</span><span class="sxs-lookup"><span data-stu-id="f0ee3-178">Conclusion</span></span>

<span data-ttu-id="f0ee3-179">這樣就大功告成了！</span><span class="sxs-lookup"><span data-stu-id="f0ee3-179">And that's it!</span></span> <span data-ttu-id="f0ee3-180">現在，您可以開始使用這裡學到的基本概念，建立您自己的程式。</span><span class="sxs-lookup"><span data-stu-id="f0ee3-180">Now, you can start using the basic concepts learned here to create your own programs.</span></span>

## <a name="see-also"></a><span data-ttu-id="f0ee3-181">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f0ee3-181">See also</span></span>

- [<span data-ttu-id="f0ee3-182">使用 .NET Core CLI 組織和測試專案</span><span class="sxs-lookup"><span data-stu-id="f0ee3-182">Organizing and testing projects with the .NET Core CLI</span></span>](testing-with-cli.md)
- [<span data-ttu-id="f0ee3-183">使用 .NET Core CLI 發佈 .NET Core 應用程式</span><span class="sxs-lookup"><span data-stu-id="f0ee3-183">Publish .NET Core apps with the .NET Core CLI</span></span>](../deploying/deploy-with-cli.md)
- [<span data-ttu-id="f0ee3-184">.NET Core 應用程式部署</span><span class="sxs-lookup"><span data-stu-id="f0ee3-184">.NET Core application deployment</span></span>](../deploying/index.md)
