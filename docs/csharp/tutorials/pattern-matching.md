---
title: 教學課程：使用模式比對建立演算法
description: 此進階教學課程示範如何使用模式比對技術，以個別建立的資料和演算法來建立功能。
ms.date: 10/06/2020
ms.technology: csharp-whats-new
ms.custom: contperfq1
ms.openlocfilehash: ee8b3a90a06fabd4e9d73d7682efecda6cbfd23e
ms.sourcegitcommit: b59237ca4ec763969a0dd775a3f8f39f8c59fe24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/12/2020
ms.locfileid: "91955625"
---
# <a name="tutorial-use-pattern-matching-to-build-type-driven-and-data-driven-algorithms"></a><span data-ttu-id="9d5ee-103">教學課程：使用模式比對來建立型別驅動和資料驅動的演算法。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-103">Tutorial: Use pattern matching to build type-driven and data-driven algorithms.</span></span>

<span data-ttu-id="9d5ee-104">C# 7 引進基本的模式比對功能。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-104">C# 7 introduced basic pattern matching features.</span></span> <span data-ttu-id="9d5ee-105">這些功能是在 c # 8 和 c # 9 中使用新的運算式和模式來擴充。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-105">Those features are extended in C# 8 and C# 9 with new expressions and patterns.</span></span> <span data-ttu-id="9d5ee-106">您可以撰寫行為如同您擴充其他程式庫中之型別的功能。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-106">You can write functionality that behaves as though you extended types that may be in other libraries.</span></span> <span data-ttu-id="9d5ee-107">模式的另一個用途是建立應用程式需要的功能，但該功能不是要擴充之型別的基本功能。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-107">Another use for patterns is to create functionality your application requires that isn't a fundamental feature of the type being extended.</span></span>

<span data-ttu-id="9d5ee-108">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="9d5ee-108">In this tutorial, you'll learn how to:</span></span>

> [!div class="checklist"]
>
> - <span data-ttu-id="9d5ee-109">辨識應該使用模式比對的情況。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-109">Recognize situations where pattern matching should be used.</span></span>
> - <span data-ttu-id="9d5ee-110">使用模式比對運算式根據類型和屬性值實作行為。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-110">Use pattern matching expressions to implement behavior based on types and property values.</span></span>
> - <span data-ttu-id="9d5ee-111">結合模式比對與其他技術，建立完整的演算法。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-111">Combine pattern matching with other techniques to create complete algorithms.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d5ee-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="9d5ee-112">Prerequisites</span></span>

<span data-ttu-id="9d5ee-113">您將需要設定您的電腦以執行 .NET 5，其中包括 c # 9 編譯器。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-113">You'll need to set up your machine to run .NET 5, which includes the C# 9 compiler.</span></span> <span data-ttu-id="9d5ee-114">從 [Visual Studio 2019 16.9 版 preview 1](https://visualstudio.microsoft.com/vs/preview/) 或 [.net 5.0 SDK](https://dot.net/get-dotnet5)開始，可以使用 c # 9 編譯器。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-114">The C# 9 compiler is available starting with [Visual Studio 2019 version 16.9 preview 1](https://visualstudio.microsoft.com/vs/preview/) or [.NET 5.0 SDK](https://dot.net/get-dotnet5).</span></span>

<span data-ttu-id="9d5ee-115">本教學課程假設您已熟悉 C# 和 .NET，包括 Visual Studio 或 .NET Core CLI。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-115">This tutorial assumes you're familiar with C# and .NET, including either Visual Studio or the .NET Core CLI.</span></span>

## <a name="scenarios-for-pattern-matching"></a><span data-ttu-id="9d5ee-116">模式比對的案例</span><span class="sxs-lookup"><span data-stu-id="9d5ee-116">Scenarios for pattern matching</span></span>

<span data-ttu-id="9d5ee-117">新式開發通常包括整合來自多個來源的資料，並在單一且一致的應用程式內呈現來自該資料的資訊和見解。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-117">Modern development often includes integrating data from multiple sources and presenting information and insights from that data in a single cohesive application.</span></span> <span data-ttu-id="9d5ee-118">您和您的小組不會有代表傳入資料之所有型別的控制權和存取權。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-118">You and your team won't have control or access for all the types that represent the incoming data.</span></span>

<span data-ttu-id="9d5ee-119">傳統物件導向設計要求您在您的應用程式中建立型別，以代表來自多個資料來源的每個資料類型。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-119">The classic object-oriented design would call for creating types in your application that represent each data type from those multiple data sources.</span></span> <span data-ttu-id="9d5ee-120">然後，您的應用程式會使用這些新型別、建立繼承階層、建立虛擬方法，以及實作抽象概念。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-120">Then, your application would work with those new types, build inheritance hierarchies, create virtual methods, and implement abstractions.</span></span> <span data-ttu-id="9d5ee-121">那些技術可以運作，而且有時候它們是最好的工具。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-121">Those techniques work, and sometimes they are the best tools.</span></span> <span data-ttu-id="9d5ee-122">其他時候，您可以撰寫少一點程式碼。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-122">Other times you can write less code.</span></span> <span data-ttu-id="9d5ee-123">透過使用將資料與操作該資料之作業分離的技術，您可以撰寫更清楚的程式碼。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-123">You can write more clear code using techniques that separate the data from the operations that manipulate that data.</span></span>

<span data-ttu-id="9d5ee-124">在此教學課程中，您會建立並探索在單一情況下，接受來自數個外部來源之資料的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-124">In this tutorial, you'll create and explore an application that takes incoming data from several external sources for a single scenario.</span></span> <span data-ttu-id="9d5ee-125">您會了解**模式比對**如何提供有效率的方法，以不屬於原始系統的方式來取用及處理該資料。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-125">You'll see how **pattern matching** provides an efficient way to consume and process that data in ways that weren't part of the original system.</span></span>

<span data-ttu-id="9d5ee-126">請考慮使用通行費和尖峰時段計費來管理交通的主要都會區。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-126">Consider a major metropolitan area that is using tolls and peak time pricing to manage traffic.</span></span> <span data-ttu-id="9d5ee-127">您要撰寫根據車輛類型計算其通行費的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-127">You write an application that calculates tolls for a vehicle based on its type.</span></span> <span data-ttu-id="9d5ee-128">之後的改進會併入根據車輛中乘客數目的計費。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-128">Later enhancements incorporate pricing based on the number of occupants in the vehicle.</span></span> <span data-ttu-id="9d5ee-129">進一步的改進會新增根據時間和星期幾的計費。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-129">Further enhancements add pricing based on the time and the day of the week.</span></span>

<span data-ttu-id="9d5ee-130">從這個簡短描述，您可能已經快速地勾勒出建構此系統模型的階層。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-130">From that brief description, you may have quickly sketched out an object hierarchy to model this system.</span></span> <span data-ttu-id="9d5ee-131">不過，您的資料來自多個來源，如其他車輛註冊管理系統。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-131">However, your data is coming from multiple sources like other vehicle registration management systems.</span></span> <span data-ttu-id="9d5ee-132">這些系統提供建構資料模型的不同類別，而且您沒有任何可用的單一物件模型。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-132">These systems provide different classes to model that data and you don't have a single object model you can use.</span></span> <span data-ttu-id="9d5ee-133">在此教學課程中，您將使用這些簡化的類別，從來自外部系統的這些車輛資料建構模型，如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="9d5ee-133">In this tutorial, you'll use these simplified classes to model for the vehicle data from these external systems, as shown in the following code:</span></span>

[!code-csharp[ExternalSystems](~/samples/snippets/csharp/tutorials/patterns/start/toll-calculator/ExternalSystems.cs)]

<span data-ttu-id="9d5ee-134">您可以從 [dotnet/samples](https://github.com/dotnet/samples/tree/master/csharp/tutorials/patterns/start) GitHub 存放庫下載起始程式碼。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-134">You can download the starter code from the [dotnet/samples](https://github.com/dotnet/samples/tree/master/csharp/tutorials/patterns/start) GitHub repository.</span></span> <span data-ttu-id="9d5ee-135">您可以看到車輛類別是來自不同的系統，且位於不同的命名空間中。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-135">You can see that the vehicle classes are from different systems, and are in different namespaces.</span></span> <span data-ttu-id="9d5ee-136">除了可用的 `System.Object` 之外，沒有通用的基底類別。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-136">No common base class, other than `System.Object` can be leveraged.</span></span>

## <a name="pattern-matching-designs"></a><span data-ttu-id="9d5ee-137">模式比對設計</span><span class="sxs-lookup"><span data-stu-id="9d5ee-137">Pattern matching designs</span></span>

<span data-ttu-id="9d5ee-138">本教學課程中使用的案例強調模式比對適用的問題類型：</span><span class="sxs-lookup"><span data-stu-id="9d5ee-138">The scenario used in this tutorial highlights the kinds of problems that pattern matching is well suited to solve:</span></span>

- <span data-ttu-id="9d5ee-139">您要處理的物件不在符合您目標的物件階層中。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-139">The objects you need to work with aren't in an object hierarchy that matches your goals.</span></span> <span data-ttu-id="9d5ee-140">您可能會使用屬於不相關之系統的類別。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-140">You may be working with classes that are part of unrelated systems.</span></span>
- <span data-ttu-id="9d5ee-141">您要新增的功能不屬於這些類別的核心抽象概念。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-141">The functionality you're adding isn't part of the core abstraction for these classes.</span></span> <span data-ttu-id="9d5ee-142">車輛付的通行費隨不同類型的車輛而「變更」\*\*，但通行費不是車輛的核心函式。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-142">The toll paid by a vehicle *changes* for different types of vehicles, but the toll isn't a core function of the vehicle.</span></span>

<span data-ttu-id="9d5ee-143">當資料的「圖形」\*\* 與資料上的「作業」\*\* 不是一起描述時，C# 中的模式比對功能可讓它變得更容易使用。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-143">When the *shape* of the data and the *operations* on that data are not described together, the pattern matching features in C# make it easier to work with.</span></span>

## <a name="implement-the-basic-toll-calculations"></a><span data-ttu-id="9d5ee-144">實作基本通行費計算</span><span class="sxs-lookup"><span data-stu-id="9d5ee-144">Implement the basic toll calculations</span></span>

<span data-ttu-id="9d5ee-145">最基本的通行費計算僅依賴車輛類型：</span><span class="sxs-lookup"><span data-stu-id="9d5ee-145">The most basic toll calculation relies only on the vehicle type:</span></span>

- <span data-ttu-id="9d5ee-146">`Car` 是 $2.00。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-146">A `Car` is $2.00.</span></span>
- <span data-ttu-id="9d5ee-147">`Taxi` 是 $3.50。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-147">A `Taxi` is $3.50.</span></span>
- <span data-ttu-id="9d5ee-148">`Bus` 是 $5.00。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-148">A `Bus` is $5.00.</span></span>
- <span data-ttu-id="9d5ee-149">`DeliveryTruck` 是 $10.00</span><span class="sxs-lookup"><span data-stu-id="9d5ee-149">A `DeliveryTruck` is $10.00</span></span>

<span data-ttu-id="9d5ee-150">建立新的 `TollCalculator` 類別，並在車輛類型上實作模式比對來取得通行費金額。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-150">Create a new `TollCalculator` class, and implement pattern matching on the vehicle type to get the toll amount.</span></span> <span data-ttu-id="9d5ee-151">下列程式碼示範 `TollCalculator` 的初始實作。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-151">The following code shows the initial implementation of the `TollCalculator`.</span></span>

```csharp
using System;
using CommercialRegistration;
using ConsumerVehicleRegistration;
using LiveryRegistration;

namespace toll_calculator
{
    public class TollCalculator
    {
        public decimal CalculateToll(object vehicle) =>
            vehicle switch
        {
            Car c           => 2.00m,
            Taxi t          => 3.50m,
            Bus b           => 5.00m,
            DeliveryTruck t => 10.00m,
            { }             => throw new ArgumentException(message: "Not a known vehicle type", paramName: nameof(vehicle)),
            null            => throw new ArgumentNullException(nameof(vehicle))
        };
    }
}
```

<span data-ttu-id="9d5ee-152">上述程式碼使用可測試**型別模式**的 **switch 運算式** (與 [`switch`](../language-reference/keywords/switch.md) 陳述式不同)。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-152">The preceding code uses a **switch expression** (not the same as a [`switch`](../language-reference/keywords/switch.md) statement) that tests the **type pattern**.</span></span> <span data-ttu-id="9d5ee-153">**switch 運算式**的開始是變數 (上述程式碼中的 `vehicle`)，接著是 `switch` 關鍵字。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-153">A **switch expression** begins with the variable, `vehicle` in the preceding code, followed by the `switch` keyword.</span></span> <span data-ttu-id="9d5ee-154">然後所有的 **switch 臂**都在大括號內。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-154">Next comes all the **switch arms** inside curly braces.</span></span> <span data-ttu-id="9d5ee-155">`switch` 運算式會對括住 `switch` 陳述式的語法進行其他細分。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-155">The `switch` expression makes other refinements to the syntax that surrounds the `switch` statement.</span></span> <span data-ttu-id="9d5ee-156">已省略 `case` 關鍵字，且每個臂的結果都是運算式。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-156">The `case` keyword is omitted, and the result of each arm is an expression.</span></span> <span data-ttu-id="9d5ee-157">最後兩個臂顯示新的語言功能。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-157">The last two arms show a new language feature.</span></span> <span data-ttu-id="9d5ee-158">`{ }` 案例比對不符合先前臂的任何非 Null 物件。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-158">The `{ }` case matches any non-null object that didn't match an earlier arm.</span></span> <span data-ttu-id="9d5ee-159">此臂會攔截傳遞到此方法的任何不正確型別。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-159">This arm catches any incorrect types passed to this method.</span></span>  <span data-ttu-id="9d5ee-160">`{ }` 案例必須遵循每種車輛類型的案例。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-160">The `{ }` case must follow the cases for each vehicle type.</span></span> <span data-ttu-id="9d5ee-161">順序如已顛倒，則 `{ }` 案例會優先。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-161">If the order were reversed, the `{ }` case would take precedence.</span></span> <span data-ttu-id="9d5ee-162">最後，`null` 模式會偵測 `null` 於何時傳遞至這個方法。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-162">Finally, the `null` pattern detects when a `null` is passed to this method.</span></span> <span data-ttu-id="9d5ee-163">因為其他型別模式只比對正確型別的非 Null 物件，所以 `null` 可以在最後。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-163">The `null` pattern can be last because the other type patterns match only a non-null object of the correct type.</span></span>

<span data-ttu-id="9d5ee-164">您可以使用 `Program.cs` 中的下列程式碼來測試此程式碼：</span><span class="sxs-lookup"><span data-stu-id="9d5ee-164">You can test this code using the following code in `Program.cs`:</span></span>

```csharp
using System;
using CommercialRegistration;
using ConsumerVehicleRegistration;
using LiveryRegistration;

namespace toll_calculator
{
    class Program
    {
        static void Main(string[] args)
        {
            var tollCalc = new TollCalculator();

            var car = new Car();
            var taxi = new Taxi();
            var bus = new Bus();
            var truck = new DeliveryTruck();

            Console.WriteLine($"The toll for a car is {tollCalc.CalculateToll(car)}");
            Console.WriteLine($"The toll for a taxi is {tollCalc.CalculateToll(taxi)}");
            Console.WriteLine($"The toll for a bus is {tollCalc.CalculateToll(bus)}");
            Console.WriteLine($"The toll for a truck is {tollCalc.CalculateToll(truck)}");

            try
            {
                tollCalc.CalculateToll("this will fail");
            }
            catch (ArgumentException e)
            {
                Console.WriteLine("Caught an argument exception when using the wrong type");
            }
            try
            {
                tollCalc.CalculateToll(null!);
            }
            catch (ArgumentNullException e)
            {
                Console.WriteLine("Caught an argument exception when using null");
            }
        }
    }
}
```

<span data-ttu-id="9d5ee-165">該程式碼包含在入門專案中，但已批註化。移除批註，您可以測試您所撰寫的內容。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-165">That code is included in the starter project, but is commented out. Remove the comments, and you can test what you've written.</span></span>

<span data-ttu-id="9d5ee-166">您已經開始了解模式能如何協助您在程式碼和資料分離的情況下建立演算法。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-166">You're starting to see how patterns can help you create algorithms where the code and the data are separate.</span></span> <span data-ttu-id="9d5ee-167">`switch` 運算式會測試型別，並根據結果產生不同的值。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-167">The `switch` expression tests the type and produces different values based on the results.</span></span> <span data-ttu-id="9d5ee-168">這只是個開頭。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-168">That's only the beginning.</span></span>

## <a name="add-occupancy-pricing"></a><span data-ttu-id="9d5ee-169">新增承載率計費</span><span class="sxs-lookup"><span data-stu-id="9d5ee-169">Add occupancy pricing</span></span>

<span data-ttu-id="9d5ee-170">通行費主管機關想要鼓勵車輛在行駛時達到最大承載。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-170">The toll authority wants to encourage vehicles to travel at maximum capacity.</span></span> <span data-ttu-id="9d5ee-171">他們決定要對乘客較少的車輛收更多費用，並透過提供較低的費用來鼓勵車輛載滿乘客：</span><span class="sxs-lookup"><span data-stu-id="9d5ee-171">They've decided to charge more when vehicles have fewer passengers, and encourage full vehicles by offering lower pricing:</span></span>

- <span data-ttu-id="9d5ee-172">沒有乘客的汽車和計程車要付額外的 $0.50。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-172">Cars and taxis with no passengers pay an extra $0.50.</span></span>
- <span data-ttu-id="9d5ee-173">有兩名乘客的汽車和計程車可折價美金 $0.50 元。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-173">Cars and taxis with two passengers get a $0.50 discount.</span></span>
- <span data-ttu-id="9d5ee-174">有三個或更多乘客的汽車和計程車可折價 $1.00。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-174">Cars and taxis with three or more passengers get a $1.00 discount.</span></span>
- <span data-ttu-id="9d5ee-175">小於 50% 載滿的巴士要付額外的 $2.00。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-175">Buses that are less than 50% full pay an extra $2.00.</span></span>
- <span data-ttu-id="9d5ee-176">大於 90% 載滿的巴士可折價 $1.00。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-176">Buses that are more than 90% full get a $1.00 discount.</span></span>

<span data-ttu-id="9d5ee-177">這些規則可以在相同的 switch 運算式中使用**屬性模式**來實作。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-177">These rules can be implemented using the **property pattern** in the same switch expression.</span></span> <span data-ttu-id="9d5ee-178">一旦判斷出型別，屬性模式就會檢查物件的屬性。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-178">The property pattern examines properties of the object once the type has been determined.</span></span> <span data-ttu-id="9d5ee-179">單一的 `Car` 案例展開為四個不同案例：</span><span class="sxs-lookup"><span data-stu-id="9d5ee-179">The single case for a `Car` expands to four different cases:</span></span>

```csharp
vehicle switch
{
    Car {Passengers: 0}        => 2.00m + 0.50m,
    Car {Passengers: 1}        => 2.0m,
    Car {Passengers: 2}        => 2.0m - 0.50m,
    Car c                      => 2.00m - 1.0m,

    // ...
};
```

<span data-ttu-id="9d5ee-180">前三個案例測試型別是否為 `Car`，然後檢查 `Passengers` 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-180">The first three cases test the type as a `Car`, then check the value of the `Passengers` property.</span></span> <span data-ttu-id="9d5ee-181">如果兩個都符合，系統就會評估該運算式並傳回。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-181">If both match, that expression is evaluated and returned.</span></span>

<span data-ttu-id="9d5ee-182">您也可以用類似的方式來展開計程車的案例：</span><span class="sxs-lookup"><span data-stu-id="9d5ee-182">You would also expand the cases for taxis in a similar manner:</span></span>

```csharp
vehicle switch
{
    // ...

    Taxi {Fares: 0}  => 3.50m + 1.00m,
    Taxi {Fares: 1}  => 3.50m,
    Taxi {Fares: 2}  => 3.50m - 0.50m,
    Taxi t           => 3.50m - 1.00m,

    // ...
};
```

<span data-ttu-id="9d5ee-183">在上述範例中，最後一個案例省略了 `when` 子句。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-183">In the preceding example, the `when` clause was omitted on the final case.</span></span>

<span data-ttu-id="9d5ee-184">接下來，藉由展開巴士的案例來實作承載率規則，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="9d5ee-184">Next, implement the occupancy rules by expanding the cases for buses, as shown in the following example:</span></span>

```csharp
vehicle switch
{
    // ...

    Bus b when ((double)b.Riders / (double)b.Capacity) < 0.50 => 5.00m + 2.00m,
    Bus b when ((double)b.Riders / (double)b.Capacity) > 0.90 => 5.00m - 1.00m,
    Bus b => 5.00m,

    // ...
};
```

<span data-ttu-id="9d5ee-185">通行費主管機關不在意貨車中的乘客數目。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-185">The toll authority isn't concerned with the number of passengers in the delivery trucks.</span></span> <span data-ttu-id="9d5ee-186">它們會根據卡車的重量類別調整通行費，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9d5ee-186">Instead, they adjust the toll amount based on the weight class of the trucks as follows:</span></span>

- <span data-ttu-id="9d5ee-187">超過 5000 磅的卡車要付額外的 $5.00。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-187">Trucks over 5000 lbs are charged an extra $5.00.</span></span>
- <span data-ttu-id="9d5ee-188">未滿 3000 磅的輕型卡車有美金 $2.00 元折扣。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-188">Light trucks under 3000 lbs are given a $2.00 discount.</span></span>

<span data-ttu-id="9d5ee-189">該規則使用下列程式碼來實作：</span><span class="sxs-lookup"><span data-stu-id="9d5ee-189">That rule is implemented with the following code:</span></span>

```csharp
vehicle switch
{
    // ...

    DeliveryTruck t when (t.GrossWeightClass > 5000) => 10.00m + 5.00m,
    DeliveryTruck t when (t.GrossWeightClass < 3000) => 10.00m - 2.00m,
    DeliveryTruck t => 10.00m,
};
```

<span data-ttu-id="9d5ee-190">前一個程式碼顯示 switch 臂的 `when` 子句。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-190">The preceding code shows the `when` clause of a switch arm.</span></span> <span data-ttu-id="9d5ee-191">您使用 `when` 子句是測試條件，而不是屬性是否相等。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-191">You use the `when` clause to test conditions other than equality on a property.</span></span> <span data-ttu-id="9d5ee-192">當您完成時，您將會有類似下列程式碼的方法：</span><span class="sxs-lookup"><span data-stu-id="9d5ee-192">When you've finished, you'll have a method that looks much like the following code:</span></span>

```csharp
vehicle switch
{
    Car {Passengers: 0}        => 2.00m + 0.50m,
    Car {Passengers: 1}        => 2.0m,
    Car {Passengers: 2}        => 2.0m - 0.50m,
    Car c                      => 2.00m - 1.0m,

    Taxi {Fares: 0}  => 3.50m + 1.00m,
    Taxi {Fares: 1}  => 3.50m,
    Taxi {Fares: 2}  => 3.50m - 0.50m,
    Taxi t           => 3.50m - 1.00m,

    Bus b when ((double)b.Riders / (double)b.Capacity) < 0.50 => 5.00m + 2.00m,
    Bus b when ((double)b.Riders / (double)b.Capacity) > 0.90 => 5.00m - 1.00m,
    Bus b => 5.00m,

    DeliveryTruck t when (t.GrossWeightClass > 5000) => 10.00m + 5.00m,
    DeliveryTruck t when (t.GrossWeightClass < 3000) => 10.00m - 2.00m,
    DeliveryTruck t => 10.00m,

    { }     => throw new ArgumentException(message: "Not a known vehicle type", paramName: nameof(vehicle)),
    null    => throw new ArgumentNullException(nameof(vehicle))
};
```

<span data-ttu-id="9d5ee-193">這些 switch 臂許多都是**遞迴模式**的範例。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-193">Many of these switch arms are examples of **recursive patterns**.</span></span> <span data-ttu-id="9d5ee-194">例如，`Car { Passengers: 1}` 顯示屬性模式內的常數模式。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-194">For example, `Car { Passengers: 1}` shows a constant pattern inside a property pattern.</span></span>

<span data-ttu-id="9d5ee-195">您可以使用巢狀 switch 讓此程式碼較不重複。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-195">You can make this code less repetitive by using nested switches.</span></span> <span data-ttu-id="9d5ee-196">在上述範例中，`Car` 和 `Taxi` 都有四個不同的臂。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-196">The `Car` and `Taxi` both have four different arms in the preceding examples.</span></span> <span data-ttu-id="9d5ee-197">在這兩種情況下，您可以建立饋入屬性模式的型別模式。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-197">In both cases, you can create a type pattern that feeds into a property pattern.</span></span> <span data-ttu-id="9d5ee-198">下列程式碼中顯示此技術：</span><span class="sxs-lookup"><span data-stu-id="9d5ee-198">This technique is shown in the following code:</span></span>

```csharp
public decimal CalculateToll(object vehicle) =>
    vehicle switch
    {
        Car c => c.Passengers switch
        {
            0 => 2.00m + 0.5m,
            1 => 2.0m,
            2 => 2.0m - 0.5m,
            _ => 2.00m - 1.0m
        },

        Taxi t => t.Fares switch
        {
            0 => 3.50m + 1.00m,
            1 => 3.50m,
            2 => 3.50m - 0.50m,
            _ => 3.50m - 1.00m
        },

        Bus b when ((double)b.Riders / (double)b.Capacity) < 0.50 => 5.00m + 2.00m,
        Bus b when ((double)b.Riders / (double)b.Capacity) > 0.90 => 5.00m - 1.00m,
        Bus b => 5.00m,

        DeliveryTruck t when (t.GrossWeightClass > 5000) => 10.00m + 5.00m,
        DeliveryTruck t when (t.GrossWeightClass < 3000) => 10.00m - 2.00m,
        DeliveryTruck t => 10.00m,

        { }  => throw new ArgumentException(message: "Not a known vehicle type", paramName: nameof(vehicle)),
        null => throw new ArgumentNullException(nameof(vehicle))
    };
```

<span data-ttu-id="9d5ee-199">在上述範例中，使用遞迴運算式表示您不重複包含子臂 (測試屬性值) 的 `Car` 和 `Taxi` 臂。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-199">In the preceding sample, using a recursive expression means you don't repeat the `Car` and `Taxi` arms containing child arms that test the property value.</span></span> <span data-ttu-id="9d5ee-200">此技術未用於 `Bus` 和 `DeliveryTruck` 臂，因為這些臂是測試屬性的範圍 (不是離散值)。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-200">This technique isn't used for the `Bus` and `DeliveryTruck` arms because those arms are testing ranges for the property, not discrete values.</span></span>

## <a name="add-peak-pricing"></a><span data-ttu-id="9d5ee-201">新增尖峰時段計費</span><span class="sxs-lookup"><span data-stu-id="9d5ee-201">Add peak pricing</span></span>

<span data-ttu-id="9d5ee-202">針對最後一個功能，通行費主管機關想要新增有時間性的尖峰時段計費。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-202">For the final feature, the toll authority wants to add time sensitive peak pricing.</span></span> <span data-ttu-id="9d5ee-203">在早上和晚上尖峰時段，通行費會加倍。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-203">During the morning and evening rush hours, the tolls are doubled.</span></span> <span data-ttu-id="9d5ee-204">該規則只影響單向的交通：早上尖峰時段進入城市，以及晚上尖峰時段離開城市。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-204">That rule only affects traffic in one direction: inbound to the city in the morning, and outbound in the evening rush hour.</span></span> <span data-ttu-id="9d5ee-205">在工作日的其他時間，通行費增加 50%。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-205">During other times during the workday, tolls increase by 50%.</span></span> <span data-ttu-id="9d5ee-206">在半夜和清晨，通行費減少 25%。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-206">Late night and early morning, tolls are reduced by 25%.</span></span> <span data-ttu-id="9d5ee-207">在週末，無論時間皆為一般費率。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-207">During the weekend, it's the normal rate, regardless of the time.</span></span> <span data-ttu-id="9d5ee-208">您可以使用序列 if `if` 和 `else` 語句，以使用下列程式碼來表示：</span><span class="sxs-lookup"><span data-stu-id="9d5ee-208">You could use a series if `if` and `else` statements to express this using the following code:</span></span>

[!code-csharp[FullTuplePattern](~/samples/snippets/csharp/tutorials/patterns/finished/toll-calculator/TollCalculator.cs#SnippetPremiumWithoutPattern)]

<span data-ttu-id="9d5ee-209">上述程式碼可正常運作，但無法讀取。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-209">The preceding code does work correctly, but isn't readable.</span></span> <span data-ttu-id="9d5ee-210">您必須將所有的輸入案例和嵌套 `if` 語句連結到程式碼的原因。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-210">You have to chain through all the input cases and the nested `if` statements to reason about the code.</span></span> <span data-ttu-id="9d5ee-211">相反地，您將使用這項功能的模式比對，但您會將它與其他技術整合。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-211">Instead, you'll use pattern matching for this feature, but you'll integrate it with other techniques.</span></span> <span data-ttu-id="9d5ee-212">您可以建置單一模式比對運算式，納入所有方向、星期幾和時間的組合。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-212">You could build a single pattern match expression that would account for all the combinations of direction, day of the week, and time.</span></span> <span data-ttu-id="9d5ee-213">結果會是一個複雜的運算式，</span><span class="sxs-lookup"><span data-stu-id="9d5ee-213">The result would be a complicated expression.</span></span> <span data-ttu-id="9d5ee-214">而它會難以閱讀及理解。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-214">It would be hard to read and difficult to understand.</span></span> <span data-ttu-id="9d5ee-215">這樣會讓確認其正確性變得困難。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-215">That makes it hard to ensure correctness.</span></span> <span data-ttu-id="9d5ee-216">反之，結合那些方法來建立值的元組，一致地描述所有那些狀態。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-216">Instead, combine those methods to build a tuple of values that concisely describes all those states.</span></span> <span data-ttu-id="9d5ee-217">然後使用模式比對來計算通行費的乘數。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-217">Then use pattern matching to calculate a multiplier for the toll.</span></span> <span data-ttu-id="9d5ee-218">元組包含三個不連續的條件：</span><span class="sxs-lookup"><span data-stu-id="9d5ee-218">The tuple contains three discrete conditions:</span></span>

- <span data-ttu-id="9d5ee-219">星期是工作日或週末。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-219">The day is either a weekday or a weekend.</span></span>
- <span data-ttu-id="9d5ee-220">收取通行費時的時段。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-220">The band of time when the toll is collected.</span></span>
- <span data-ttu-id="9d5ee-221">方向是進入城市或離開城市</span><span class="sxs-lookup"><span data-stu-id="9d5ee-221">The direction is into the city or out of the city</span></span>

<span data-ttu-id="9d5ee-222">下表顯示輸入值和尖峰時段計費乘數的組合：</span><span class="sxs-lookup"><span data-stu-id="9d5ee-222">The following table shows the combinations of input values and the peak pricing multiplier:</span></span>

| <span data-ttu-id="9d5ee-223">天</span><span class="sxs-lookup"><span data-stu-id="9d5ee-223">Day</span></span>        | <span data-ttu-id="9d5ee-224">時間</span><span class="sxs-lookup"><span data-stu-id="9d5ee-224">Time</span></span>         | <span data-ttu-id="9d5ee-225">Direction</span><span class="sxs-lookup"><span data-stu-id="9d5ee-225">Direction</span></span> | <span data-ttu-id="9d5ee-226">Premium</span><span class="sxs-lookup"><span data-stu-id="9d5ee-226">Premium</span></span> |
| ---------- | ------------ | --------- |--------:|
| <span data-ttu-id="9d5ee-227">Weekday</span><span class="sxs-lookup"><span data-stu-id="9d5ee-227">Weekday</span></span>    | <span data-ttu-id="9d5ee-228">早上尖峰時段</span><span class="sxs-lookup"><span data-stu-id="9d5ee-228">morning rush</span></span> | <span data-ttu-id="9d5ee-229">進入</span><span class="sxs-lookup"><span data-stu-id="9d5ee-229">inbound</span></span>   | <span data-ttu-id="9d5ee-230">x 2.00</span><span class="sxs-lookup"><span data-stu-id="9d5ee-230">x 2.00</span></span>  |
| <span data-ttu-id="9d5ee-231">Weekday</span><span class="sxs-lookup"><span data-stu-id="9d5ee-231">Weekday</span></span>    | <span data-ttu-id="9d5ee-232">早上尖峰時段</span><span class="sxs-lookup"><span data-stu-id="9d5ee-232">morning rush</span></span> | <span data-ttu-id="9d5ee-233">離開</span><span class="sxs-lookup"><span data-stu-id="9d5ee-233">outbound</span></span>  | <span data-ttu-id="9d5ee-234">x 1.00</span><span class="sxs-lookup"><span data-stu-id="9d5ee-234">x 1.00</span></span>  |
| <span data-ttu-id="9d5ee-235">Weekday</span><span class="sxs-lookup"><span data-stu-id="9d5ee-235">Weekday</span></span>    | <span data-ttu-id="9d5ee-236">日間</span><span class="sxs-lookup"><span data-stu-id="9d5ee-236">daytime</span></span>      | <span data-ttu-id="9d5ee-237">進入</span><span class="sxs-lookup"><span data-stu-id="9d5ee-237">inbound</span></span>   | <span data-ttu-id="9d5ee-238">x 1.50</span><span class="sxs-lookup"><span data-stu-id="9d5ee-238">x 1.50</span></span>  |
| <span data-ttu-id="9d5ee-239">Weekday</span><span class="sxs-lookup"><span data-stu-id="9d5ee-239">Weekday</span></span>    | <span data-ttu-id="9d5ee-240">日間</span><span class="sxs-lookup"><span data-stu-id="9d5ee-240">daytime</span></span>      | <span data-ttu-id="9d5ee-241">離開</span><span class="sxs-lookup"><span data-stu-id="9d5ee-241">outbound</span></span>  | <span data-ttu-id="9d5ee-242">x 1.50</span><span class="sxs-lookup"><span data-stu-id="9d5ee-242">x 1.50</span></span>  |
| <span data-ttu-id="9d5ee-243">Weekday</span><span class="sxs-lookup"><span data-stu-id="9d5ee-243">Weekday</span></span>    | <span data-ttu-id="9d5ee-244">晚上尖峰時段</span><span class="sxs-lookup"><span data-stu-id="9d5ee-244">evening rush</span></span> | <span data-ttu-id="9d5ee-245">進入</span><span class="sxs-lookup"><span data-stu-id="9d5ee-245">inbound</span></span>   | <span data-ttu-id="9d5ee-246">x 1.00</span><span class="sxs-lookup"><span data-stu-id="9d5ee-246">x 1.00</span></span>  |
| <span data-ttu-id="9d5ee-247">Weekday</span><span class="sxs-lookup"><span data-stu-id="9d5ee-247">Weekday</span></span>    | <span data-ttu-id="9d5ee-248">晚上尖峰時段</span><span class="sxs-lookup"><span data-stu-id="9d5ee-248">evening rush</span></span> | <span data-ttu-id="9d5ee-249">離開</span><span class="sxs-lookup"><span data-stu-id="9d5ee-249">outbound</span></span>  | <span data-ttu-id="9d5ee-250">x 2.00</span><span class="sxs-lookup"><span data-stu-id="9d5ee-250">x 2.00</span></span>  |
| <span data-ttu-id="9d5ee-251">Weekday</span><span class="sxs-lookup"><span data-stu-id="9d5ee-251">Weekday</span></span>    | <span data-ttu-id="9d5ee-252">夜間</span><span class="sxs-lookup"><span data-stu-id="9d5ee-252">overnight</span></span>    | <span data-ttu-id="9d5ee-253">進入</span><span class="sxs-lookup"><span data-stu-id="9d5ee-253">inbound</span></span>   | <span data-ttu-id="9d5ee-254">x 0.75</span><span class="sxs-lookup"><span data-stu-id="9d5ee-254">x 0.75</span></span>  |
| <span data-ttu-id="9d5ee-255">Weekday</span><span class="sxs-lookup"><span data-stu-id="9d5ee-255">Weekday</span></span>    | <span data-ttu-id="9d5ee-256">夜間</span><span class="sxs-lookup"><span data-stu-id="9d5ee-256">overnight</span></span>    | <span data-ttu-id="9d5ee-257">離開</span><span class="sxs-lookup"><span data-stu-id="9d5ee-257">outbound</span></span>  | <span data-ttu-id="9d5ee-258">x 0.75</span><span class="sxs-lookup"><span data-stu-id="9d5ee-258">x 0.75</span></span>  |
| <span data-ttu-id="9d5ee-259">週末</span><span class="sxs-lookup"><span data-stu-id="9d5ee-259">Weekend</span></span>    | <span data-ttu-id="9d5ee-260">早上尖峰時段</span><span class="sxs-lookup"><span data-stu-id="9d5ee-260">morning rush</span></span> | <span data-ttu-id="9d5ee-261">進入</span><span class="sxs-lookup"><span data-stu-id="9d5ee-261">inbound</span></span>   | <span data-ttu-id="9d5ee-262">x 1.00</span><span class="sxs-lookup"><span data-stu-id="9d5ee-262">x 1.00</span></span>  |
| <span data-ttu-id="9d5ee-263">週末</span><span class="sxs-lookup"><span data-stu-id="9d5ee-263">Weekend</span></span>    | <span data-ttu-id="9d5ee-264">早上尖峰時段</span><span class="sxs-lookup"><span data-stu-id="9d5ee-264">morning rush</span></span> | <span data-ttu-id="9d5ee-265">離開</span><span class="sxs-lookup"><span data-stu-id="9d5ee-265">outbound</span></span>  | <span data-ttu-id="9d5ee-266">x 1.00</span><span class="sxs-lookup"><span data-stu-id="9d5ee-266">x 1.00</span></span>  |
| <span data-ttu-id="9d5ee-267">週末</span><span class="sxs-lookup"><span data-stu-id="9d5ee-267">Weekend</span></span>    | <span data-ttu-id="9d5ee-268">日間</span><span class="sxs-lookup"><span data-stu-id="9d5ee-268">daytime</span></span>      | <span data-ttu-id="9d5ee-269">進入</span><span class="sxs-lookup"><span data-stu-id="9d5ee-269">inbound</span></span>   | <span data-ttu-id="9d5ee-270">x 1.00</span><span class="sxs-lookup"><span data-stu-id="9d5ee-270">x 1.00</span></span>  |
| <span data-ttu-id="9d5ee-271">週末</span><span class="sxs-lookup"><span data-stu-id="9d5ee-271">Weekend</span></span>    | <span data-ttu-id="9d5ee-272">日間</span><span class="sxs-lookup"><span data-stu-id="9d5ee-272">daytime</span></span>      | <span data-ttu-id="9d5ee-273">離開</span><span class="sxs-lookup"><span data-stu-id="9d5ee-273">outbound</span></span>  | <span data-ttu-id="9d5ee-274">x 1.00</span><span class="sxs-lookup"><span data-stu-id="9d5ee-274">x 1.00</span></span>  |
| <span data-ttu-id="9d5ee-275">週末</span><span class="sxs-lookup"><span data-stu-id="9d5ee-275">Weekend</span></span>    | <span data-ttu-id="9d5ee-276">晚上尖峰時段</span><span class="sxs-lookup"><span data-stu-id="9d5ee-276">evening rush</span></span> | <span data-ttu-id="9d5ee-277">進入</span><span class="sxs-lookup"><span data-stu-id="9d5ee-277">inbound</span></span>   | <span data-ttu-id="9d5ee-278">x 1.00</span><span class="sxs-lookup"><span data-stu-id="9d5ee-278">x 1.00</span></span>  |
| <span data-ttu-id="9d5ee-279">週末</span><span class="sxs-lookup"><span data-stu-id="9d5ee-279">Weekend</span></span>    | <span data-ttu-id="9d5ee-280">晚上尖峰時段</span><span class="sxs-lookup"><span data-stu-id="9d5ee-280">evening rush</span></span> | <span data-ttu-id="9d5ee-281">離開</span><span class="sxs-lookup"><span data-stu-id="9d5ee-281">outbound</span></span>  | <span data-ttu-id="9d5ee-282">x 1.00</span><span class="sxs-lookup"><span data-stu-id="9d5ee-282">x 1.00</span></span>  |
| <span data-ttu-id="9d5ee-283">週末</span><span class="sxs-lookup"><span data-stu-id="9d5ee-283">Weekend</span></span>    | <span data-ttu-id="9d5ee-284">夜間</span><span class="sxs-lookup"><span data-stu-id="9d5ee-284">overnight</span></span>    | <span data-ttu-id="9d5ee-285">進入</span><span class="sxs-lookup"><span data-stu-id="9d5ee-285">inbound</span></span>   | <span data-ttu-id="9d5ee-286">x 1.00</span><span class="sxs-lookup"><span data-stu-id="9d5ee-286">x 1.00</span></span>  |
| <span data-ttu-id="9d5ee-287">週末</span><span class="sxs-lookup"><span data-stu-id="9d5ee-287">Weekend</span></span>    | <span data-ttu-id="9d5ee-288">夜間</span><span class="sxs-lookup"><span data-stu-id="9d5ee-288">overnight</span></span>    | <span data-ttu-id="9d5ee-289">離開</span><span class="sxs-lookup"><span data-stu-id="9d5ee-289">outbound</span></span>  | <span data-ttu-id="9d5ee-290">x 1.00</span><span class="sxs-lookup"><span data-stu-id="9d5ee-290">x 1.00</span></span>  |

<span data-ttu-id="9d5ee-291">三個變數的 16 個不同組合。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-291">There are 16 different combinations of the three variables.</span></span> <span data-ttu-id="9d5ee-292">透過結合一些條件，您將會簡化最終的 switch 運算式。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-292">By combining some of the conditions, you'll simplify the final switch expression.</span></span>

<span data-ttu-id="9d5ee-293">針對何時收取通行費，收取通行費的系統會使用 <xref:System.DateTime> 結構。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-293">The system that collects the tolls uses a <xref:System.DateTime> structure for the time when the toll was collected.</span></span> <span data-ttu-id="9d5ee-294">建置從上述表格建立變數的成員方法。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-294">Build member methods that create the variables from the preceding table.</span></span> <span data-ttu-id="9d5ee-295">下列函式會使用模式比對 switch 運算式，表達 <xref:System.DateTime> 代表週末或工作日：</span><span class="sxs-lookup"><span data-stu-id="9d5ee-295">The following function uses a pattern matching switch expression to express whether a <xref:System.DateTime> represents a weekend or a weekday:</span></span>

```csharp
private static bool IsWeekDay(DateTime timeOfToll) =>
    timeOfToll.DayOfWeek switch
    {
        DayOfWeek.Monday    => true,
        DayOfWeek.Tuesday   => true,
        DayOfWeek.Wednesday => true,
        DayOfWeek.Thursday  => true,
        DayOfWeek.Friday    => true,
        DayOfWeek.Saturday  => false,
        DayOfWeek.Sunday    => false
    };
```

<span data-ttu-id="9d5ee-296">這種方法是正確的，但它是重複性的。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-296">That method is correct, but it's repetitious.</span></span> <span data-ttu-id="9d5ee-297">您可以簡化它，如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="9d5ee-297">You can simplify it, as shown in the following code:</span></span>

[!code-csharp[IsWeekDay](~/samples/snippets/csharp/tutorials/patterns/finished/toll-calculator/TollCalculator.cs#IsWeekDay)]

<span data-ttu-id="9d5ee-298">接下來，新增類似的函式來將時間分類為區塊：</span><span class="sxs-lookup"><span data-stu-id="9d5ee-298">Next, add a similar function to categorize the time into the blocks:</span></span>

[!code-csharp[GetTimeBand](~/samples/snippets/csharp/tutorials/patterns/finished/toll-calculator/TollCalculator.cs#GetTimeBand)]

<span data-ttu-id="9d5ee-299">您可以新增私用 `enum` ，將每個時間範圍轉換成離散值。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-299">You add a private `enum` to convert each range of time to a discrete value.</span></span> <span data-ttu-id="9d5ee-300">然後， `GetTimeBand` 方法會使用 *關聯式模式*和 *組成或模式*，這兩個都是在 c # 9.0 中新增。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-300">Then, the `GetTimeBand` method uses *relational patterns*, and *conjunctive or patterns*, both added in C# 9.0.</span></span> <span data-ttu-id="9d5ee-301">關聯式模式可讓您使用 `<` 、、或來測試 `>` 數值 `<=` `>=` 。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-301">The relational pattern lets you test a numeric value using `<`, `>`, `<=`, or `>=`.</span></span> <span data-ttu-id="9d5ee-302">此 `or` 模式會測試運算式是否符合一或多個模式。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-302">The `or` pattern tests if an expression matches one or more patterns.</span></span> <span data-ttu-id="9d5ee-303">您也可以使用 `and` 模式來確定運算式符合兩個不同的模式，以及一個 `not` 模式來測試運算式是否不符合模式。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-303">You can also use an `and` pattern to ensure that an expression matches two distinct patterns, and a `not` pattern to test that an expression doesn't match a pattern.</span></span>

<span data-ttu-id="9d5ee-304">建立這些方法之後，您可以搭配使用另一個 `switch` 運算式和**元組模式**來計算計費溢價。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-304">After you create those methods, you can use another `switch` expression with the **tuple pattern** to calculate the pricing premium.</span></span> <span data-ttu-id="9d5ee-305">您可以建置有 16 個臂的 `switch` 運算式：</span><span class="sxs-lookup"><span data-stu-id="9d5ee-305">You could build a `switch` expression with all 16 arms:</span></span>

[!code-csharp[FullTuplePattern](~/samples/snippets/csharp/tutorials/patterns/finished/toll-calculator/TollCalculator.cs#TuplePatternOne)]

<span data-ttu-id="9d5ee-306">上面的程式碼可以運作，但它可以簡化。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-306">The above code works, but it can be simplified.</span></span> <span data-ttu-id="9d5ee-307">週末的八個組合通行費都相同。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-307">All eight combinations for the weekend have the same toll.</span></span> <span data-ttu-id="9d5ee-308">您可以用下列一行取代所有八個：</span><span class="sxs-lookup"><span data-stu-id="9d5ee-308">You can replace all eight with the following line:</span></span>

```csharp
(false, _, _) => 1.0m,
```

<span data-ttu-id="9d5ee-309">進入和離開的流量在工作日日間和夜間，都有相同的乘數。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-309">Both inbound and outbound traffic have the same multiplier during the weekday daytime and overnight hours.</span></span> <span data-ttu-id="9d5ee-310">這四個 switch 臂都可以替換成下列兩行：</span><span class="sxs-lookup"><span data-stu-id="9d5ee-310">Those four switch arms can be replaced with the following two lines:</span></span>

```csharp
(true, TimeBand.Overnight, _) => 0.75m,
(true, TimeBand.Daytime, _)   => 1.5m,
```

<span data-ttu-id="9d5ee-311">經過這兩個變更之後，程式碼應該看起來像下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="9d5ee-311">The code should look like the following code after those two changes:</span></span>

```csharp
public decimal PeakTimePremium(DateTime timeOfToll, bool inbound) =>
    (IsWeekDay(timeOfToll), GetTimeBand(timeOfToll), inbound) switch
    {
        (true, TimeBand.MorningRush, true)  => 2.00m,
        (true, TimeBand.MorningRush, false) => 1.00m,
        (true, TimeBand.Daytime,     _)     => 1.50m,
        (true, TimeBand.EveningRush, true)  => 1.00m,
        (true, TimeBand.EveningRush, false) => 2.00m,
        (true, TimeBand.Overnight,   _)     => 0.75m,
        (false, _,                   _)     => 1.00m,
    };
```

<span data-ttu-id="9d5ee-312">最後，您可以移除收取一般價格的兩個尖峰時段。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-312">Finally, you can remove the two rush hour times that pay the regular price.</span></span> <span data-ttu-id="9d5ee-313">移除那些臂之後，您可以將最後一個 switch 臂中的 `false` 取代為捨棄 (`_`)。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-313">Once you remove those arms, you can replace the `false` with a discard (`_`) in the final switch arm.</span></span> <span data-ttu-id="9d5ee-314">您會有下列已完成的方法：</span><span class="sxs-lookup"><span data-stu-id="9d5ee-314">You'll have the following finished method:</span></span>

[!code-csharp[SimplifiedTuplePattern](../../../samples/snippets/csharp/tutorials/patterns/finished/toll-calculator/TollCalculator.cs#FinalTuplePattern)]

<span data-ttu-id="9d5ee-315">此範例會醒目提示模式比對的優點之一：依序評估模式分支。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-315">This example highlights one of the advantages of pattern matching: the pattern branches are evaluated in order.</span></span> <span data-ttu-id="9d5ee-316">如果您重新排列它們，讓前面分支處理其中一個最近的案例，則編譯器會提出有關無法連線程式碼的警告。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-316">If you rearrange them so that an earlier branch handles one of your later cases, the compiler warns you about the unreachable code.</span></span> <span data-ttu-id="9d5ee-317">那些語言規則讓您可以放心地進行上述簡化，而不需擔心程式碼會變更。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-317">Those language rules made it easier to do the preceding simplifications with confidence that the code didn't change.</span></span>

<span data-ttu-id="9d5ee-318">模式比對讓某些類型的程式碼更容易讀取，並在您無法將程式碼新增至類別時，提供物件導向技術的替代方式。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-318">Pattern matching makes some types of code more readable and offers an alternative to object-oriented techniques when you can't add code to your classes.</span></span> <span data-ttu-id="9d5ee-319">雲端是造成資料和功能分開的原因。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-319">The cloud is causing data and functionality to live apart.</span></span> <span data-ttu-id="9d5ee-320">資料的「圖形」\*\* 與資料上的「作業」\*\* 不需要一起描述。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-320">The *shape* of the data and the *operations* on it aren't necessarily described together.</span></span> <span data-ttu-id="9d5ee-321">在此教學課程中，您以和現有資料原始功能完全不同的方式取用它們。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-321">In this tutorial, you consumed existing data in entirely different ways from its original function.</span></span> <span data-ttu-id="9d5ee-322">模式比對讓您能夠撰寫覆寫這些類型的功能，即使您無法擴充它們。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-322">Pattern matching gave you the ability to write functionality that overrode those types, even though you couldn't extend them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d5ee-323">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9d5ee-323">Next steps</span></span>

<span data-ttu-id="9d5ee-324">您可以從 [dotnet/samples](https://github.com/dotnet/samples/tree/master/csharp/tutorials/patterns/finished) GitHub 存放庫下載已完成的程式碼。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-324">You can download the finished code from the [dotnet/samples](https://github.com/dotnet/samples/tree/master/csharp/tutorials/patterns/finished) GitHub repository.</span></span> <span data-ttu-id="9d5ee-325">自行探索模式，並將此技術新增到您平常撰寫程式碼的活動中。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-325">Explore patterns on your own and add this technique into your regular coding activities.</span></span> <span data-ttu-id="9d5ee-326">學習這些技巧提供您處理問題並建立新功能的另一種方式。</span><span class="sxs-lookup"><span data-stu-id="9d5ee-326">Learning these techniques gives you another way to approach problems and create new functionality.</span></span>
