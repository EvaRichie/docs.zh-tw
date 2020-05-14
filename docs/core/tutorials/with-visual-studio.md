---
title: 在 Visual Studio 中使用 .NET Core 建立 Hello World 應用程式
description: '瞭解如何使用 Visual Studio，以 c # 或 Visual Basic 建立您的第一個 .NET Core 主控台應用程式。'
author: BillWagner
ms.author: wiwagn
ms.date: 12/09/2019
ms.custom: vs-dotnet
ms.openlocfilehash: 738fc49a820c3c5d94fb35c1bf7a8b718ed75cb3
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/14/2020
ms.locfileid: "83394832"
---
# <a name="tutorial-create-your-first-net-core-console-application-in-visual-studio-2019"></a><span data-ttu-id="e8f2e-103">教學課程：在 Visual Studio 2019 中建立您的第一個 .NET Core 主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="e8f2e-103">Tutorial: Create your first .NET Core console application in Visual Studio 2019</span></span>

<span data-ttu-id="e8f2e-104">本文提供在 Visual Studio 2019 中建立和執行 Hello World .NET Core 主控台應用程式的逐步介紹。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-104">This article provides a step-by-step introduction to create and run a Hello World .NET Core console application in Visual Studio 2019.</span></span> <span data-ttu-id="e8f2e-105">Hello World 的應用程式傳統上是用來向初學者介紹新的程式設計語言。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-105">A Hello World application is traditionally used to introduce beginners to a new programming language.</span></span> <span data-ttu-id="e8f2e-106">此程式只會顯示 "Hello World！" 這個片語</span><span class="sxs-lookup"><span data-stu-id="e8f2e-106">This program simply displays the phrase "Hello World!"</span></span> <span data-ttu-id="e8f2e-107">。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-107">on the screen.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8f2e-108">先決條件</span><span class="sxs-lookup"><span data-stu-id="e8f2e-108">Prerequisites</span></span>

- <span data-ttu-id="e8f2e-109">已安裝 **.Net Core 跨平臺開發**工作負載的[Visual Studio 2019 16.4 版或更新版本](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019)。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-109">[Visual Studio 2019 version 16.4 or a later version](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) with the **.NET Core cross-platform development** workload installed.</span></span> <span data-ttu-id="e8f2e-110">當您選取此工作負載時，會自動安裝 .NET Core 3.1 SDK。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-110">.NET Core 3.1 SDK is automatically installed when you select this workload.</span></span>

<span data-ttu-id="e8f2e-111">如需詳細資訊，請參閱[安裝 .NET Core SDK](../install/sdk.md?pivots=os-windows)一文中的[install with Visual Studio](../install/sdk.md?pivots=os-windows#install-with-visual-studio)一節。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-111">For more information, see the [Install with Visual Studio](../install/sdk.md?pivots=os-windows#install-with-visual-studio) section on the [Install the .NET Core SDK](../install/sdk.md?pivots=os-windows) article.</span></span>

## <a name="create-the-app"></a><span data-ttu-id="e8f2e-112">建立應用程式</span><span class="sxs-lookup"><span data-stu-id="e8f2e-112">Create the app</span></span>

<span data-ttu-id="e8f2e-113">下列指示會建立簡單的 Hello World 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="e8f2e-113">The following instructions create a simple Hello World console application:</span></span>

<!-- markdownlint-disable MD025 -->

# <a name="c"></a>[<span data-ttu-id="e8f2e-114">C#</span><span class="sxs-lookup"><span data-stu-id="e8f2e-114">C#</span></span>](#tab/csharp)

1. <span data-ttu-id="e8f2e-115">開啟 Visual Studio 2019。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-115">Open Visual Studio 2019.</span></span>

1. <span data-ttu-id="e8f2e-116">建立名為 "HelloWorld" 的新 c # .NET Core 主控台應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-116">Create a new C# .NET Core console app project named "HelloWorld".</span></span>

   1. <span data-ttu-id="e8f2e-117">在 [開始] 視窗中，選擇 [**建立新專案**]。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-117">On the start window, choose **Create a new project**.</span></span>

      ![在 [Visual Studio 開始] 視窗上選取 [建立新專案] 按鈕](./media/with-visual-studio/start-window.png)

   1. <span data-ttu-id="e8f2e-119">在 [**建立新專案**] 頁面的 [搜尋] 方塊中，輸入**主控台**。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-119">On the **Create a new project** page, enter **console** in the search box.</span></span> <span data-ttu-id="e8f2e-120">接下來，從 [語言] 清單中選擇 [ **c #** ]，然後從 [平臺] 清單中選擇 [**所有平臺**]。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-120">Next, choose **C#** from the Language list, and then choose **All platforms** from the Platform list.</span></span> <span data-ttu-id="e8f2e-121">選擇 [**主控台應用程式（.Net Core）** ] 範本，然後選擇 [**下一步]**。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-121">Choose the **Console App (.NET Core)** template, and then choose **Next**.</span></span>

      ![建立已選取篩選的新專案視窗](./media/with-visual-studio/create-new-project.png)

      > [!TIP]
      > <span data-ttu-id="e8f2e-123">如果您看不到 .NET Core 範本，可能是您已安裝必要的工作負載。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-123">If you don't see the .NET Core templates, you're probably missing the required workload installed.</span></span> <span data-ttu-id="e8f2e-124">在 [**找不到您要尋找的內容嗎？** ] 訊息底下，選擇 [**安裝更多工具和功能**] 連結。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-124">Under the **Not finding what you're looking for?** message, choose the **Install more tools and features** link.</span></span> <span data-ttu-id="e8f2e-125">Visual Studio 安裝程式隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-125">The Visual Studio Installer opens.</span></span> <span data-ttu-id="e8f2e-126">請確定您已安裝 **.Net Core 跨平臺開發**工作負載。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-126">Make sure you have the **.NET Core cross-platform development** workload installed.</span></span>

   1. <span data-ttu-id="e8f2e-127">在 [**設定您的新專案**] 頁面的 [**專案名稱**] 方塊中，輸入**HelloWorld** 。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-127">On the **Configure your new project** page,  enter **HelloWorld** in the **Project name** box.</span></span> <span data-ttu-id="e8f2e-128">然後選擇 [**建立**]。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-128">Then, choose **Create**.</span></span>

      ![以 [專案名稱]、[位置] 和 [方案名稱] 欄位設定新的專案視窗](./media/with-visual-studio/configure-new-project.png)

   <span data-ttu-id="e8f2e-130">.NET Core 的 C# 主控台應用程式範本會自動定義一個 `Program` 類別，該類別具有採用 <xref:System.String> 陣列為引數的單一 `Main` 方法。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-130">The C# Console Application template for .NET Core automatically defines a class, `Program`, with a single method, `Main`, that takes a <xref:System.String> array as an argument.</span></span> <span data-ttu-id="e8f2e-131">`Main` 是應用程式進入點，是執行階段在啟動應用程式時會自動呼叫的方法。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-131">`Main` is the application entry point, the method that's called automatically by the runtime when it launches the application.</span></span> <span data-ttu-id="e8f2e-132">在應用程式啟動時所提供的所有命令列引數，都會在 *args* 陣列中提供。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-132">Any command-line arguments supplied when the application is launched are available in the *args* array.</span></span>

   ![Visual Studio 和新的 HelloWorld 專案](./media/with-visual-studio/visual-studio-main-window.png)

# <a name="visual-basic"></a>[<span data-ttu-id="e8f2e-134">Visual Basic</span><span class="sxs-lookup"><span data-stu-id="e8f2e-134">Visual Basic</span></span>](#tab/vb)

1. <span data-ttu-id="e8f2e-135">開啟 Visual Studio 2019。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-135">Open Visual Studio 2019.</span></span>

1. <span data-ttu-id="e8f2e-136">建立名為 "HelloWorld" 的新 Visual Basic .NET Core 主控台應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-136">Create a new Visual Basic .NET Core console app project named "HelloWorld".</span></span>

   1. <span data-ttu-id="e8f2e-137">在 [開始] 視窗中，選擇 [**建立新專案**]。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-137">On the start window, choose **Create a new project**.</span></span>

      ![在 [Visual Studio 開始] 視窗上選取 [建立新專案] 按鈕](./media/with-visual-studio/start-window.png)

   1. <span data-ttu-id="e8f2e-139">在 [**建立新專案**] 頁面的 [搜尋] 方塊中，輸入**主控台**。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-139">On the **Create a new project** page, enter **console** in the search box.</span></span> <span data-ttu-id="e8f2e-140">接下來，從 [語言] 清單中選擇 [ **Visual Basic** ]，然後從 [平臺] 清單中選擇 [**所有平臺**]。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-140">Next, choose **Visual Basic** from the Language list, and then choose **All platforms** from the Platform list.</span></span> <span data-ttu-id="e8f2e-141">選擇 [**主控台應用程式（.Net Core）** ] 範本，然後選擇 [**下一步]**。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-141">Choose the **Console App (.NET Core)** template, and then choose **Next**.</span></span>

      ![選擇主控台應用程式 (.NET Framework) 的 Visual Basic 專案範本](./media/with-visual-studio/vb/create-new-project.png)

      > [!TIP]
      > <span data-ttu-id="e8f2e-143">如果您看不到 .NET Core 範本，可能是您已安裝必要的工作負載。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-143">If you don't see the .NET Core templates, you're probably missing the required workload installed.</span></span> <span data-ttu-id="e8f2e-144">在 [**找不到您要尋找的內容嗎？** ] 訊息底下，選擇 [**安裝更多工具和功能**] 連結。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-144">Under the **Not finding what you're looking for?** message, choose the **Install more tools and features** link.</span></span> <span data-ttu-id="e8f2e-145">Visual Studio 安裝程式隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-145">The Visual Studio Installer opens.</span></span> <span data-ttu-id="e8f2e-146">請確定您已安裝 **.Net Core 跨平臺開發**工作負載。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-146">Make sure you have the **.NET Core cross-platform development** workload installed.</span></span>

   1. <span data-ttu-id="e8f2e-147">在 [**設定您的新專案**] 頁面的 [**專案名稱**] 方塊中，輸入**HelloWorld** 。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-147">On the **Configure your new project** page,  enter **HelloWorld** in the **Project name** box.</span></span> <span data-ttu-id="e8f2e-148">然後選擇 [**建立**]。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-148">Then, choose **Create**.</span></span>

   <span data-ttu-id="e8f2e-149">適用于 .NET Core 的主控台應用程式範本會自動定義一個類別， `Program` 其中包含使用 `Main` <xref:System.String> 陣列做為引數的單一方法。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-149">The console app template for .NET Core automatically defines a class, `Program`, with a single method, `Main`, that takes a <xref:System.String> array as an argument.</span></span> <span data-ttu-id="e8f2e-150">`Main` 是應用程式進入點，是執行階段在啟動應用程式時會自動呼叫的方法。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-150">`Main` is the application entry point, the method that's called automatically by the runtime when it launches the application.</span></span> <span data-ttu-id="e8f2e-151">當應用程式啟動時所提供的任何命令列引數都可以在參數中使用 `args` 。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-151">Any command-line arguments supplied when the application is launched are available in the `args` parameter.</span></span>

   ![Visual Studio 和新的 HelloWorld 專案](./media/with-visual-studio/vb/visual-studio-main-window.png)

---

   <span data-ttu-id="e8f2e-153">此範本會建立簡單的 "Hello World" 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-153">The template creates a simple "Hello World" application.</span></span> <span data-ttu-id="e8f2e-154">它會呼叫 <xref:System.Console.WriteLine(System.String)?displayProperty=nameWithType> 方法，以在主控台視窗中顯示常值字串 "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="e8f2e-154">It calls the <xref:System.Console.WriteLine(System.String)?displayProperty=nameWithType> method to display the literal string "Hello World!"</span></span> <span data-ttu-id="e8f2e-155">。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-155">in the console window.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="e8f2e-156">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="e8f2e-156">Run the app</span></span>

1. <span data-ttu-id="e8f2e-157">若要執行程式，請選擇工具列上的 [ **HelloWorld** ]，或按**F5**。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-157">To run the program, choose **HelloWorld** on the toolbar, or press **F5**.</span></span>

   ![已選取 [HelloWorld 執行] 按鈕的 Visual Studio 工具列](./media/with-visual-studio/run-program.png)

   <span data-ttu-id="e8f2e-159">主控台視窗隨即開啟，並出現 "Hello World！" 文字</span><span class="sxs-lookup"><span data-stu-id="e8f2e-159">A console window opens with the text "Hello World!"</span></span> <span data-ttu-id="e8f2e-160">列印在畫面上，而部分 Visual Studio 的調試資訊。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-160">printed on the screen and some Visual Studio debug information.</span></span>

   ![主控台視窗顯示 Hello World，請按任意鍵以繼續](./media/with-visual-studio/hello-world-console.png)

1. <span data-ttu-id="e8f2e-162">按任意鍵關閉主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-162">Press any key to close the console window.</span></span>

## <a name="enhance-the-app"></a><span data-ttu-id="e8f2e-163">增強應用程式</span><span class="sxs-lookup"><span data-stu-id="e8f2e-163">Enhance the app</span></span>

<span data-ttu-id="e8f2e-164">增強您的應用程式以提示使用者輸入其名稱，並將其與日期和時間一起顯示。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-164">Enhance your application to prompt the user for their name and display it along with the date and time.</span></span> <span data-ttu-id="e8f2e-165">下列指示會再次修改並執行應用程式：</span><span class="sxs-lookup"><span data-stu-id="e8f2e-165">The following instructions modify and run the app again:</span></span>

# <a name="c"></a>[<span data-ttu-id="e8f2e-166">C#</span><span class="sxs-lookup"><span data-stu-id="e8f2e-166">C#</span></span>](#tab/csharp)

1. <span data-ttu-id="e8f2e-167">`Main`以下列程式碼取代方法的內容，這目前只是呼叫的那一行 `Console.WriteLine` ：</span><span class="sxs-lookup"><span data-stu-id="e8f2e-167">Replace the contents of the `Main` method, which is currently just the line that calls `Console.WriteLine`, with the following code:</span></span>

   [!code-csharp[GettingStarted#1](~/samples/snippets/csharp/getting_started/with_visual_studio/HelloWorld.cs#1)]

   <span data-ttu-id="e8f2e-168">此程式碼會在主控台中顯示「What is your name?」，</span><span class="sxs-lookup"><span data-stu-id="e8f2e-168">This code displays "What is your name?"</span></span> <span data-ttu-id="e8f2e-169">然後等待使用者輸入字串並按 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-169">in the console window and waits until the user enters a string followed by the Enter key.</span></span> <span data-ttu-id="e8f2e-170">它會將此字串儲存至名為 `name` 的變數。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-170">It stores this string into a variable named `name`.</span></span> <span data-ttu-id="e8f2e-171">此程式碼也會擷取 <xref:System.DateTime.Now?displayProperty=nameWithType> 屬性的值，其中包含目前的當地時間，並將它指派至名稱為 `date` 的變數。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-171">It also retrieves the value of the <xref:System.DateTime.Now?displayProperty=nameWithType> property, which contains the current local time, and assigns it to a variable named `date`.</span></span> <span data-ttu-id="e8f2e-172">最後，使用[字串插值](../../csharp/language-reference/tokens/interpolated.md)在主控台視窗中顯示這些值。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-172">Finally, it uses an [interpolated string](../../csharp/language-reference/tokens/interpolated.md) to display these values in the console window.</span></span>

1. <span data-ttu-id="e8f2e-173">選擇 [組建] [ **Build**  >  **組建方案**]，以編譯器。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-173">Compile the program by choosing **Build** > **Build Solution**.</span></span>

1. <span data-ttu-id="e8f2e-174">若要執行程式，請選擇工具列上的 [ **HelloWorld** ]，或按**F5**。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-174">To run the program, choose **HelloWorld** on the toolbar, or press **F5**.</span></span>

1. <span data-ttu-id="e8f2e-175">輸入名稱並按**enter**鍵，以回應提示。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-175">Respond to the prompt by entering a name and pressing the **Enter** key.</span></span>

   ![含有已修改程式輸出的主控台視窗](./media/with-visual-studio/hello-world-update.png)

1. <span data-ttu-id="e8f2e-177">按任意鍵關閉主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-177">Press any key to close the console window.</span></span>

# <a name="visual-basic"></a>[<span data-ttu-id="e8f2e-178">Visual Basic</span><span class="sxs-lookup"><span data-stu-id="e8f2e-178">Visual Basic</span></span>](#tab/vb)

1. <span data-ttu-id="e8f2e-179">`Main`以下列程式碼取代方法的內容，這目前只是呼叫的那一行 `Console.WriteLine` ：</span><span class="sxs-lookup"><span data-stu-id="e8f2e-179">Replace the contents of the `Main` method, which is currently just the line that calls `Console.WriteLine`, with the following code:</span></span>

   [!code-vb[GettingStarted#1](~/samples/snippets/core/tutorials/vb-with-visual-studio/Program.vb#1)]

   <span data-ttu-id="e8f2e-180">此程式碼會在主控台中顯示「What is your name?」，</span><span class="sxs-lookup"><span data-stu-id="e8f2e-180">This code displays "What is your name?"</span></span> <span data-ttu-id="e8f2e-181">然後等待使用者輸入字串並按 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-181">in the console window and waits until the user enters a string followed by the Enter key.</span></span> <span data-ttu-id="e8f2e-182">它會將此字串儲存至名為 `name` 的變數。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-182">It stores this string into a variable named `name`.</span></span> <span data-ttu-id="e8f2e-183">此程式碼也會擷取 <xref:System.DateTime.Now?displayProperty=nameWithType> 屬性的值，其中包含目前的當地時間，並將它指派至名稱為 `date` 的變數。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-183">It also retrieves the value of the <xref:System.DateTime.Now?displayProperty=nameWithType> property, which contains the current local time, and assigns it to a variable named `date`.</span></span> <span data-ttu-id="e8f2e-184">最後，使用[字串插值](../../visual-basic/programming-guide/language-features/strings/interpolated-strings.md)在主控台視窗中顯示這些值。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-184">Finally, it uses an [interpolated string](../../visual-basic/programming-guide/language-features/strings/interpolated-strings.md) to display these values in the console window.</span></span>

1. <span data-ttu-id="e8f2e-185">選擇 [組建] [ **Build**  >  **組建方案**]，以編譯器。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-185">Compile the program by choosing **Build** > **Build Solution**.</span></span>

1. <span data-ttu-id="e8f2e-186">若要執行程式，請選擇工具列上的 [ **HelloWorld** ]，或按**F5**。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-186">To run the program, choose **HelloWorld** on the toolbar, or press **F5**.</span></span>

1. <span data-ttu-id="e8f2e-187">輸入名稱並按**enter**鍵，以回應提示。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-187">Respond to the prompt by entering a name and pressing the **Enter** key.</span></span>

   ![含有已修改程式輸出的主控台視窗](./media/with-visual-studio/hello-world-update.png)

1. <span data-ttu-id="e8f2e-189">按任意鍵關閉主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-189">Press any key to close the console window.</span></span>

---

## <a name="next-steps"></a><span data-ttu-id="e8f2e-190">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e8f2e-190">Next steps</span></span>

<span data-ttu-id="e8f2e-191">在本文中，您已建立並執行您的第一個 .NET Core 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-191">In this article, you've created and run your first .NET Core application.</span></span> <span data-ttu-id="e8f2e-192">在下一個步驟中，您會對應用程式進行 debug。</span><span class="sxs-lookup"><span data-stu-id="e8f2e-192">In the next step, you debug your app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e8f2e-193">在 Visual Studio 中，對 .NET Core Hello World 應用程式進行 Debug</span><span class="sxs-lookup"><span data-stu-id="e8f2e-193">Debug a .NET Core Hello World application in Visual Studio</span></span>](debugging-with-visual-studio.md)
