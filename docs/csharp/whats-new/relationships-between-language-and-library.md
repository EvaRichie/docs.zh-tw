---
title: 語言功能和程式庫類型之間的關聯性 | Microsoft Docs
description: 語言功能經常會依賴程式庫類型進行實作。 了解該關聯性。
ms.date: 07/20/2017
ms.openlocfilehash: abf15385da3756c35db2df822cc2e11e9edf5758
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/09/2020
ms.locfileid: "86174097"
---
# <a name="relationships-between-language-features-and-library-types"></a><span data-ttu-id="ee5b3-104">語言功能和程式庫類型之間的關聯性</span><span class="sxs-lookup"><span data-stu-id="ee5b3-104">Relationships between language features and library types</span></span>

<span data-ttu-id="ee5b3-105">C# 語言定義要求標準程式庫具有特定類型和這些類型的特定可存取成員。</span><span class="sxs-lookup"><span data-stu-id="ee5b3-105">The C# language definition requires a standard library to have certain types and certain accessible members on those types.</span></span> <span data-ttu-id="ee5b3-106">編譯器產生的程式碼會將這些必要的類型和成員用在許多不同的語言功能。</span><span class="sxs-lookup"><span data-stu-id="ee5b3-106">The compiler generates code that uses these required types and members for many different language features.</span></span> <span data-ttu-id="ee5b3-107">必要時，為尚未部署這些類型或成員的環境撰寫程式碼時，會有包含較新語言版本所需類型的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="ee5b3-107">When necessary, there are NuGet packages that contain types needed for newer versions of the language when writing code for environments where those types or members have not been deployed yet.</span></span>

<span data-ttu-id="ee5b3-108">這種對標準程式庫功能的相依性，自其第一版本開始已成為 C# 語言的一部分。</span><span class="sxs-lookup"><span data-stu-id="ee5b3-108">This dependency on standard library functionality has been part of the C# language since its first version.</span></span> <span data-ttu-id="ee5b3-109">該版本包含的範例如下：</span><span class="sxs-lookup"><span data-stu-id="ee5b3-109">In that version, examples included:</span></span>

* <span data-ttu-id="ee5b3-110"><xref:System.Exception> - 用於所有編譯器產生的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="ee5b3-110"><xref:System.Exception> - used for all compiler generated exceptions.</span></span>
* <span data-ttu-id="ee5b3-111"><xref:System.String> - C# `string` 類型是 <xref:System.String> 的同義字。</span><span class="sxs-lookup"><span data-stu-id="ee5b3-111"><xref:System.String> - the C# `string` type is a synonym for <xref:System.String>.</span></span>
* <span data-ttu-id="ee5b3-112"><xref:System.Int32> - `int` 的同義字。</span><span class="sxs-lookup"><span data-stu-id="ee5b3-112"><xref:System.Int32> - synonym of `int`.</span></span>

<span data-ttu-id="ee5b3-113">第一個版本很簡單：編譯器和標準程式庫一起出貨，各只有一個版本。</span><span class="sxs-lookup"><span data-stu-id="ee5b3-113">That first version was simple: the compiler and the standard library shipped together, and there was only one version of each.</span></span>

<span data-ttu-id="ee5b3-114">後續的 C# 版本偶爾會在相依性中新增新的類型或成員。</span><span class="sxs-lookup"><span data-stu-id="ee5b3-114">Subsequent versions of C# have occasionally added new types or members to the dependencies.</span></span> <span data-ttu-id="ee5b3-115">範例包括 <xref:System.Runtime.CompilerServices.INotifyCompletion>、<xref:System.Runtime.CompilerServices.CallerFilePathAttribute> 和 <xref:System.Runtime.CompilerServices.CallerMemberNameAttribute>。</span><span class="sxs-lookup"><span data-stu-id="ee5b3-115">Examples include: <xref:System.Runtime.CompilerServices.INotifyCompletion>, <xref:System.Runtime.CompilerServices.CallerFilePathAttribute> and <xref:System.Runtime.CompilerServices.CallerMemberNameAttribute>.</span></span> <span data-ttu-id="ee5b3-116">C# 7.0 會繼續此行為，在 <xref:System.ValueTuple> 新增相依性實作 [Tuple](../language-reference/builtin-types/value-tuples.md) 語言功能。</span><span class="sxs-lookup"><span data-stu-id="ee5b3-116">C# 7.0 continues this by adding a dependency on <xref:System.ValueTuple> to implement the [tuples](../language-reference/builtin-types/value-tuples.md) language feature.</span></span>

<span data-ttu-id="ee5b3-117">語言設計小組努力將相容標準程式庫中所需類型和成員的介面區縮減至最小。</span><span class="sxs-lookup"><span data-stu-id="ee5b3-117">The language design team works to minimize the surface area of the types and members required in a compliant standard library.</span></span> <span data-ttu-id="ee5b3-118">該目標與新程式庫功能順利併入到語言的全新設計平衡。</span><span class="sxs-lookup"><span data-stu-id="ee5b3-118">That goal is balanced against a clean design where new library features are incorporated seamlessly into the language.</span></span> <span data-ttu-id="ee5b3-119">未來的 C# 版本中會有在標準程式庫中需要新類型和成員的新功能。</span><span class="sxs-lookup"><span data-stu-id="ee5b3-119">There will be new features in future versions of C# that require new types and members in a standard library.</span></span> <span data-ttu-id="ee5b3-120">請務必了解如何管理工作中的這些相依性。</span><span class="sxs-lookup"><span data-stu-id="ee5b3-120">It's important to understand how to manage those dependencies in your work.</span></span>

## <a name="managing-your-dependencies"></a><span data-ttu-id="ee5b3-121">管理相依性</span><span class="sxs-lookup"><span data-stu-id="ee5b3-121">Managing your dependencies</span></span>

<span data-ttu-id="ee5b3-122">C# 編譯器工具現在已從受支援平台上的 .NET 程式庫發行週期中分離出來。</span><span class="sxs-lookup"><span data-stu-id="ee5b3-122">C# compiler tools are now decoupled from the release cycle of the .NET libraries on supported platforms.</span></span> <span data-ttu-id="ee5b3-123">事實上，不同的 .NET 程式庫有不同的發行週期：Windows 上的 .NET Framework 發行為 Windows Update，.NET Core 隨附於個別的排程，而 Xamarin 版的程式庫更新則隨每個目標平台的 Xamarin 工具出貨。</span><span class="sxs-lookup"><span data-stu-id="ee5b3-123">In fact, different .NET libraries have different release cycles: the .NET Framework on Windows is released as a Windows Update, .NET Core ships on a separate schedule, and the Xamarin versions of library updates ship with the Xamarin tools for each target platform.</span></span>

<span data-ttu-id="ee5b3-124">大多時候您都不會注意到這些變更。</span><span class="sxs-lookup"><span data-stu-id="ee5b3-124">The majority of time, you won't notice these changes.</span></span> <span data-ttu-id="ee5b3-125">不過，當您使用較新的語言版本，需要該平台 .NET 程式庫尚未提供的功能時，要參考 NuGet 套件以提供這些新的類型。</span><span class="sxs-lookup"><span data-stu-id="ee5b3-125">However, when you are working with a newer version of the language that requires features not yet in the .NET libraries on that platform, you'll reference the NuGet packages to provide those new types.</span></span>
<span data-ttu-id="ee5b3-126">使用新的 Framework 安裝更新您的應用程式支援平台時，您可以移除額外的參考。</span><span class="sxs-lookup"><span data-stu-id="ee5b3-126">As the platforms your app supports are updated with new framework installations, you can remove the extra reference.</span></span>

<span data-ttu-id="ee5b3-127">這項分隔表示，即使您的目標機器可能沒有對應的架構，您仍可以使用新的語言功能。</span><span class="sxs-lookup"><span data-stu-id="ee5b3-127">This separation means you can use new language features even when you are targeting machines that may not have the corresponding framework.</span></span>
