---
title: LINQ to Objects (C#)
ms.date: 07/20/2015
ms.assetid: c5c2c178-3529-4f6c-b3df-2d5267af7f22
ms.openlocfilehash: c488e49283f3e30ea729adf111fd9ca297039838
ms.sourcegitcommit: a241301495a84cc8c64fe972330d16edd619868b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/01/2020
ms.locfileid: "84241561"
---
# <a name="linq-to-objects-c"></a><span data-ttu-id="650b4-102">LINQ to Objects (C#)</span><span class="sxs-lookup"><span data-stu-id="650b4-102">LINQ to Objects (C#)</span></span>
<span data-ttu-id="650b4-103">詞彙 "LINQ to Objects" 是指直接搭配使用 LINQ 查詢與任何 <xref:System.Collections.IEnumerable> 或 <xref:System.Collections.Generic.IEnumerable%601> 集合，而不要使用中繼 LINQ 提供者或 API (例如 [LINQ to SQL](../../../../framework/data/adonet/sql/linq/index.md) 或 [LINQ to XML](./linq-to-xml-overview.md))。</span><span class="sxs-lookup"><span data-stu-id="650b4-103">The term "LINQ to Objects" refers to the use of LINQ queries with any <xref:System.Collections.IEnumerable> or <xref:System.Collections.Generic.IEnumerable%601> collection directly, without the use of an intermediate LINQ provider or API such as [LINQ to SQL](../../../../framework/data/adonet/sql/linq/index.md) or [LINQ to XML](./linq-to-xml-overview.md).</span></span> <span data-ttu-id="650b4-104">您可以使用 LINQ 查詢任何可列舉的集合，例如 <xref:System.Collections.Generic.List%601>、<xref:System.Array> 或 <xref:System.Collections.Generic.Dictionary%602>。</span><span class="sxs-lookup"><span data-stu-id="650b4-104">You can use LINQ to query any enumerable collections such as <xref:System.Collections.Generic.List%601>, <xref:System.Array>, or <xref:System.Collections.Generic.Dictionary%602>.</span></span> <span data-ttu-id="650b4-105">集合可能是使用者定義的，或可能由 .NET API 傳回。</span><span class="sxs-lookup"><span data-stu-id="650b4-105">The collection may be user-defined or may be returned by a .NET API.</span></span>  
  
 <span data-ttu-id="650b4-106">基本上，LINQ to Objects 代表使用集合的新方法。</span><span class="sxs-lookup"><span data-stu-id="650b4-106">In a basic sense, LINQ to Objects represents a new approach to collections.</span></span> <span data-ttu-id="650b4-107">在舊的方法中，您必須撰寫複雜的 `foreach` 迴圈，以指定如何從集合擷取資料。</span><span class="sxs-lookup"><span data-stu-id="650b4-107">In the old way, you had to write complex `foreach` loops that specified how to retrieve data from a collection.</span></span> <span data-ttu-id="650b4-108">在 LINQ 方法中，您會撰寫描述所要擷取內容的宣告式程式碼。</span><span class="sxs-lookup"><span data-stu-id="650b4-108">In the LINQ approach, you write declarative code that describes what you want to retrieve.</span></span>  
  
 <span data-ttu-id="650b4-109">此外，LINQ 查詢還提供三種超越傳統 `foreach` 迴圈的主要優點：</span><span class="sxs-lookup"><span data-stu-id="650b4-109">In addition, LINQ queries offer three main advantages over traditional `foreach` loops:</span></span>  
  
1. <span data-ttu-id="650b4-110">它們更加簡潔易懂 (尤其是在篩選多個條件時)。</span><span class="sxs-lookup"><span data-stu-id="650b4-110">They are more concise and readable, especially when filtering multiple conditions.</span></span>  
  
2. <span data-ttu-id="650b4-111">它們只要使用最少的應用程式程式碼，即可提供強大的篩選、排序及群組功能。</span><span class="sxs-lookup"><span data-stu-id="650b4-111">They provide powerful filtering, ordering, and grouping capabilities with a minimum of application code.</span></span>  
  
3. <span data-ttu-id="650b4-112">它們只需要一點修改，甚至不用修改，便可以移植到其他資料來源。</span><span class="sxs-lookup"><span data-stu-id="650b4-112">They can be ported to other data sources with little or no modification.</span></span>  
  
 <span data-ttu-id="650b4-113">一般來說，您要對資料執行的作業越複雜，就越能體會使用 LINQ 取代傳統反覆項目技術的好處。</span><span class="sxs-lookup"><span data-stu-id="650b4-113">In general, the more complex the operation you want to perform on the data, the more benefit you will realize by using LINQ instead of traditional iteration techniques.</span></span>  
  
 <span data-ttu-id="650b4-114">本節的目的是要透過一些精選的範例，示範 LINQ 方法，</span><span class="sxs-lookup"><span data-stu-id="650b4-114">The purpose of this section is to demonstrate the LINQ approach with some select examples.</span></span> <span data-ttu-id="650b4-115">而不是要提供詳細的說明。</span><span class="sxs-lookup"><span data-stu-id="650b4-115">It is not intended to be exhaustive.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="650b4-116">本節內容</span><span class="sxs-lookup"><span data-stu-id="650b4-116">In This Section</span></span>  
 [<span data-ttu-id="650b4-117">LINQ 和字串 (C#)</span><span class="sxs-lookup"><span data-stu-id="650b4-117">LINQ and Strings (C#)</span></span>](./linq-and-strings.md)  
 <span data-ttu-id="650b4-118">說明如何使用 LINQ 查詢及轉換字串與字串集合。</span><span class="sxs-lookup"><span data-stu-id="650b4-118">Explains how LINQ can be used to query and transform strings and collections of strings.</span></span> <span data-ttu-id="650b4-119">此外也包含示範這些原理的主題連結。</span><span class="sxs-lookup"><span data-stu-id="650b4-119">Also includes links to topics that demonstrate these principles.</span></span>  
  
 [<span data-ttu-id="650b4-120">LINQ 和反映 (C#)</span><span class="sxs-lookup"><span data-stu-id="650b4-120">LINQ and Reflection (C#)</span></span>](how-to-query-an-assembly-s-metadata-with-reflection-linq.md)  
 <span data-ttu-id="650b4-121">示範 LINQ 如何使用反映的範例連結。</span><span class="sxs-lookup"><span data-stu-id="650b4-121">Links to a sample that demonstrates how LINQ uses reflection.</span></span>  
  
 [<span data-ttu-id="650b4-122">LINQ 和檔案目錄 (C#)</span><span class="sxs-lookup"><span data-stu-id="650b4-122">LINQ and File Directories (C#)</span></span>](./linq-and-file-directories.md)  
 <span data-ttu-id="650b4-123">說明如何使用 LINQ 與檔案系統互動。</span><span class="sxs-lookup"><span data-stu-id="650b4-123">Explains how LINQ can be used to interact with file systems.</span></span> <span data-ttu-id="650b4-124">此外也包含示範這些概念的主題連結。</span><span class="sxs-lookup"><span data-stu-id="650b4-124">Also includes links to topics that demonstrate these concepts.</span></span>  
  
 [<span data-ttu-id="650b4-125">如何使用 LINQ 查詢 ArrayList （c #）</span><span class="sxs-lookup"><span data-stu-id="650b4-125">How to query an ArrayList with LINQ (C#)</span></span>](./how-to-query-an-arraylist-with-linq.md)  
 <span data-ttu-id="650b4-126">示範如何以 C# 查詢 ArrayList。</span><span class="sxs-lookup"><span data-stu-id="650b4-126">Demonstrates how to query an ArrayList in C#.</span></span>  
  
 [<span data-ttu-id="650b4-127">如何新增 LINQ 查詢的自訂方法（c #）</span><span class="sxs-lookup"><span data-stu-id="650b4-127">How to add custom methods for LINQ queries (C#)</span></span>](./how-to-add-custom-methods-for-linq-queries.md)  
 <span data-ttu-id="650b4-128">說明如何透過將擴充方法加入至 <xref:System.Collections.Generic.IEnumerable%601> 介面，來延伸您可以用於 LINQ 查詢的方法組。</span><span class="sxs-lookup"><span data-stu-id="650b4-128">Explains how to extend the set of methods that you can use for LINQ queries by adding extension methods to the <xref:System.Collections.Generic.IEnumerable%601> interface.</span></span>  
  
 [<span data-ttu-id="650b4-129">Language-Integrated Query (LINQ) (C#)</span><span class="sxs-lookup"><span data-stu-id="650b4-129">Language-Integrated Query (LINQ) (C#)</span></span>](./index.md)  
 <span data-ttu-id="650b4-130">提供 LINQ 的主題說明連結，以及執行查詢的程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="650b4-130">Provides links to topics that explain LINQ and provide examples of code that perform queries.</span></span>
