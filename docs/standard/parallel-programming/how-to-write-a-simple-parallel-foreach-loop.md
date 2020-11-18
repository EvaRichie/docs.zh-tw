---
title: 使用 Parallel.ForEach 寫入一個簡單的平行程式
description: 在本文中，您將瞭解如何在 .NET 中啟用資料平行處理原則。 對任何 IEnumerable 或 IEnumerable 資料來源撰寫 Parallel. ForEach 迴圈。 <T>
ms.date: 02/14/2019
dev_langs:
- csharp
- vb
helpviewer_keywords:
- foreach, parallel version
- parallel programming, foreach
ms.assetid: cb5fab92-1c19-499e-ae91-8b7525dd875f
ms.openlocfilehash: e4f67f6fbe5a79e925ecd6aaec3f833704cda38c
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94825412"
---
# <a name="how-to-write-a-simple-parallelforeach-loop"></a><span data-ttu-id="bc233-104">如何：撰寫簡單的 Parallel. ForEach 迴圈</span><span class="sxs-lookup"><span data-stu-id="bc233-104">How to: Write a simple Parallel.ForEach loop</span></span>

<span data-ttu-id="bc233-105">此範例示範如何使用 <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> 迴圈來透過 <xref:System.Collections.IEnumerable?displayProperty=nameWithType> 或 <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType> 資料來源啟用資料平行處理原則。</span><span class="sxs-lookup"><span data-stu-id="bc233-105">This example shows how to use a <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> loop to enable data parallelism over any <xref:System.Collections.IEnumerable?displayProperty=nameWithType> or <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType> data source.</span></span>

> [!NOTE]
> <span data-ttu-id="bc233-106">本文件使用 Lambda 運算式來定義 PLINQ 中的委派。</span><span class="sxs-lookup"><span data-stu-id="bc233-106">This documentation uses lambda expressions to define delegates in PLINQ.</span></span> <span data-ttu-id="bc233-107">如果您不熟悉 c # 或 Visual Basic 中的 lambda 運算式，請參閱 [PLINQ 和 TPL 中的 lambda 運算式](lambda-expressions-in-plinq-and-tpl.md)。</span><span class="sxs-lookup"><span data-stu-id="bc233-107">If you are not familiar with lambda expressions in C# or Visual Basic, see [Lambda expressions in PLINQ and TPL](lambda-expressions-in-plinq-and-tpl.md).</span></span>

## <a name="example"></a><span data-ttu-id="bc233-108">範例</span><span class="sxs-lookup"><span data-stu-id="bc233-108">Example</span></span>

<span data-ttu-id="bc233-109">此範例會假設您在 C:\Users\Public\Pictures\Sample Pictures 資料夾中擁有數個 .jpg 檔案，且建立名為 *Modified* 的新子資料夾。</span><span class="sxs-lookup"><span data-stu-id="bc233-109">This example assumes you have several .jpg files in a *C:\Users\Public\Pictures\Sample Pictures* folder and creates a new sub-folder named *Modified*.</span></span> <span data-ttu-id="bc233-110">當您執行範例時，其會旋轉在 *Sample Pictures* 中的各 .jpg 影像，並將其儲存至 *Modified*。</span><span class="sxs-lookup"><span data-stu-id="bc233-110">When you run the example, it rotates each .jpg image in *Sample Pictures* and saves it to *Modified*.</span></span> <span data-ttu-id="bc233-111">如有必要，您可以修改這兩個路徑。</span><span class="sxs-lookup"><span data-stu-id="bc233-111">You can modify the two paths as necessary.</span></span>

[!code-csharp[TPL_Parallel#03](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/simpleforeach.cs#03)]
[!code-vb[TPL_Parallel#03](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/simpleforeach.vb#03)]

<span data-ttu-id="bc233-112"><xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> 迴圈的運作方式類似 <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> 迴圈。</span><span class="sxs-lookup"><span data-stu-id="bc233-112">A <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> loop works like a <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> loop.</span></span> <span data-ttu-id="bc233-113">迴圈會根據系統環境分割來源集合，及對多個執行緒上的作業進行排程。</span><span class="sxs-lookup"><span data-stu-id="bc233-113">The loop partitions the source collection and schedules the work on multiple threads based on the system environment.</span></span> <span data-ttu-id="bc233-114">系統上的處理器愈多，平行方法的執行速度愈快。</span><span class="sxs-lookup"><span data-stu-id="bc233-114">The more processors on the system, the faster the parallel method runs.</span></span> <span data-ttu-id="bc233-115">對於某些來源集合，循序迴圈的執行速度可能更快，這取決於來源的大小和迴圈執行的作業種類。</span><span class="sxs-lookup"><span data-stu-id="bc233-115">For some source collections, a sequential loop may be faster, depending on the size of the source and the kind of work the loop performs.</span></span> <span data-ttu-id="bc233-116">如需效能的詳細資訊，請參閱 [資料和工作平行處理原則中的潛在陷阱](potential-pitfalls-in-data-and-task-parallelism.md)。</span><span class="sxs-lookup"><span data-stu-id="bc233-116">For more information about performance, see [Potential pitfalls in data and task parallelism](potential-pitfalls-in-data-and-task-parallelism.md).</span></span>

<span data-ttu-id="bc233-117">如需平行迴圈的詳細資訊，請參閱 [如何：撰寫簡單的 parallel. for 迴圈](how-to-write-a-simple-parallel-for-loop.md)。</span><span class="sxs-lookup"><span data-stu-id="bc233-117">For more information about parallel loops, see [How to: Write a simple Parallel.For loop](how-to-write-a-simple-parallel-for-loop.md).</span></span>

<span data-ttu-id="bc233-118">若要將 <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType>使用於非泛型集合 ，可使用 <xref:System.Linq.Enumerable.Cast%2A?displayProperty=nameWithType> 擴充方法將集合轉換成泛型集合，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="bc233-118">To use <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> with a non-generic collection, you can use the <xref:System.Linq.Enumerable.Cast%2A?displayProperty=nameWithType> extension method to convert the collection to a generic collection, as shown in the following example:</span></span>

[!code-csharp[TPL_Parallel#07](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/nongeneric.cs#07)]
[!code-vb[TPL_Parallel#07](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/nongeneric.vb#07)]

<span data-ttu-id="bc233-119">您也可以使用平行 LINQ (PLINQ) 來平行處理 <xref:System.Collections.Generic.IEnumerable%601> 資料來源。</span><span class="sxs-lookup"><span data-stu-id="bc233-119">You can also use Parallel LINQ (PLINQ) to parallelize processing of <xref:System.Collections.Generic.IEnumerable%601> data sources.</span></span> <span data-ttu-id="bc233-120">PLINQ 可讓您使用宣告式查詢語法來表示迴圈行為。</span><span class="sxs-lookup"><span data-stu-id="bc233-120">PLINQ enables you to use declarative query syntax to express the loop behavior.</span></span> <span data-ttu-id="bc233-121">如需詳細資訊，請參閱 [Parallel LINQ (PLINQ)](introduction-to-plinq.md)。</span><span class="sxs-lookup"><span data-stu-id="bc233-121">For more information, see [Parallel LINQ (PLINQ)](introduction-to-plinq.md).</span></span>

## <a name="compile-and-run-the-code"></a><span data-ttu-id="bc233-122">編譯並執行程式碼</span><span class="sxs-lookup"><span data-stu-id="bc233-122">Compile and run the code</span></span>

<span data-ttu-id="bc233-123">您可將程式碼編譯為 .NET Framework 的主控台應用程式，或 .NET Core 的主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="bc233-123">You can compile the code as a console application for .NET Framework or as a console application for .NET Core.</span></span>

<span data-ttu-id="bc233-124">在 Visual Studio 中，有 Windows Desktop 及 .NET Core 的 Visual Basic 及 C# 主控台應用程式範本。</span><span class="sxs-lookup"><span data-stu-id="bc233-124">In Visual Studio, there are Visual Basic and C# console application templates for Windows Desktop and .NET Core.</span></span>

<span data-ttu-id="bc233-125">從命令列中，您可以使用 .NET Core CLI 命令 (例如 `dotnet new console` 或 `dotnet new console -lang vb`) ，也可以建立檔案並針對 .NET Framework 應用程式使用命令列編譯器。</span><span class="sxs-lookup"><span data-stu-id="bc233-125">From the command line, you can use either the .NET Core CLI commands (for example, `dotnet new console` or `dotnet new console -lang vb`), or you can create the file and use the command-line compiler for a .NET Framework application.</span></span>

<span data-ttu-id="bc233-126">對於 .NET Core 專案，您必須參考 **System.Drawing.Common** NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="bc233-126">For a .NET Core project, you must reference the **System.Drawing.Common** NuGet package.</span></span> <span data-ttu-id="bc233-127">在 Visual Studio 中，使用 NuGet 套件管理員來安裝套件。</span><span class="sxs-lookup"><span data-stu-id="bc233-127">In Visual Studio, use the NuGet Package Manager to install the package.</span></span> <span data-ttu-id="bc233-128">或者，您可將參考新增至 \*.csproj 或 \*.vbproj 檔案中的套件：</span><span class="sxs-lookup"><span data-stu-id="bc233-128">Alternatively, you can add a reference to the package in your \*.csproj or \*.vbproj file:</span></span>

```xml
<ItemGroup>
     <PackageReference Include="System.Drawing.Common" Version="4.5.1" />
</ItemGroup>
```

<span data-ttu-id="bc233-129">若要從命令列執行 .NET Core 主控台應用程式，請從包含您應用程式的資料夾中使用 `dotnet run`。</span><span class="sxs-lookup"><span data-stu-id="bc233-129">To run a .NET Core console application from the command line, use `dotnet run` from the folder that contains your application.</span></span>

<span data-ttu-id="bc233-130">若要從 Visual Studio 執行您的主控台應用程式，請按 **F5**。</span><span class="sxs-lookup"><span data-stu-id="bc233-130">To run your console application from Visual Studio, press **F5**.</span></span>

## <a name="see-also"></a><span data-ttu-id="bc233-131">請參閱</span><span class="sxs-lookup"><span data-stu-id="bc233-131">See also</span></span>

- [<span data-ttu-id="bc233-132">資料平行處理原則</span><span class="sxs-lookup"><span data-stu-id="bc233-132">Data parallelism</span></span>](data-parallelism-task-parallel-library.md)
- [<span data-ttu-id="bc233-133">平行程式設計</span><span class="sxs-lookup"><span data-stu-id="bc233-133">Parallel programming</span></span>](index.md)
- [<span data-ttu-id="bc233-134">平行 LINQ (PLINQ)</span><span class="sxs-lookup"><span data-stu-id="bc233-134">Parallel LINQ (PLINQ)</span></span>](introduction-to-plinq.md)
