---
title: 執行不區分文化特性的字串作業
ms.date: 08/22/2018
helpviewer_keywords:
- case mappings
- custom case mappings
- culture, custom sorting rules
- custom sorting rules
- culture-insensitive string operations, options for performing
- culture, custom case mappings
- culture-insensitive string operations, method overloads
ms.assetid: 579ef891-1f83-4c63-9ebd-2f40406b5b91
ms.openlocfilehash: a418432dfaba9ab070ddb6dc862dcbd798c16343
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95732212"
---
# <a name="performing-culture-insensitive-string-operations"></a><span data-ttu-id="9e05f-102">執行不區分文化特性的字串作業</span><span class="sxs-lookup"><span data-stu-id="9e05f-102">Performing culture-insensitive string operations</span></span>

<span data-ttu-id="9e05f-103">預設會執行區分文化特性的字串作業的大部分 .NET 方法都會提供方法多載，讓您可以藉由傳遞參數來明確指定要使用的文化特性 <xref:System.Globalization.CultureInfo> 。</span><span class="sxs-lookup"><span data-stu-id="9e05f-103">Most .NET methods that perform culture-sensitive string operations by default provide method overloads that allow you to explicitly specify the culture to use by passing a <xref:System.Globalization.CultureInfo> parameter.</span></span> <span data-ttu-id="9e05f-104">這些多載可讓您消除大小寫對應和排序規則中的文化特性變化，保證您可以得到不區分文化特性的結果。</span><span class="sxs-lookup"><span data-stu-id="9e05f-104">These overloads allow you to eliminate cultural variations in case mappings and sorting rules and guarantee culture-insensitive results.</span></span>  
  
 <span data-ttu-id="9e05f-105">本節提供下列文章，以示範如何使用預設為區分文化特性的 .NET 方法，執行不區分文化特性的字串作業。</span><span class="sxs-lookup"><span data-stu-id="9e05f-105">This section provides the following articles to demonstrate how to perform culture-insensitive string operations using .NET methods that are culture-sensitive by default.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="9e05f-106">本節內容</span><span class="sxs-lookup"><span data-stu-id="9e05f-106">In this section</span></span>  

 [<span data-ttu-id="9e05f-107">執行不區分文化特性的字串比較</span><span class="sxs-lookup"><span data-stu-id="9e05f-107">Performing Culture-Insensitive String Comparisons</span></span>](performing-culture-insensitive-string-comparisons.md)  
 <span data-ttu-id="9e05f-108">描述如何使用 <xref:System.String.Compare%2A?displayProperty=nameWithType> 和 <xref:System.String.CompareTo%2A?displayProperty=nameWithType> 方法執行不區分文化特性的字串比較。</span><span class="sxs-lookup"><span data-stu-id="9e05f-108">Describes how to use the <xref:System.String.Compare%2A?displayProperty=nameWithType> and <xref:System.String.CompareTo%2A?displayProperty=nameWithType> methods to perform culture-insensitive string comparisons.</span></span>  
  
 [<span data-ttu-id="9e05f-109">執行不區分文化特性的大小寫變更</span><span class="sxs-lookup"><span data-stu-id="9e05f-109">Performing Culture-Insensitive Case Changes</span></span>](performing-culture-insensitive-case-changes.md)  
 <span data-ttu-id="9e05f-110">描述如何使用 <xref:System.String.ToUpper%2A?displayProperty=nameWithType>、<xref:System.String.ToLower%2A?displayProperty=nameWithType>、<xref:System.Char.ToUpper%2A?displayProperty=nameWithType> 和 <xref:System.Char.ToLower%2A?displayProperty=nameWithType> 方法執行不區分文化特性的大小寫變更。</span><span class="sxs-lookup"><span data-stu-id="9e05f-110">Describes how to use the <xref:System.String.ToUpper%2A?displayProperty=nameWithType>, <xref:System.String.ToLower%2A?displayProperty=nameWithType>, <xref:System.Char.ToUpper%2A?displayProperty=nameWithType>, and <xref:System.Char.ToLower%2A?displayProperty=nameWithType> methods to perform culture-insensitive case changes.</span></span>  
  
 [<span data-ttu-id="9e05f-111">在集合中執行不區分文化特性的字串作業</span><span class="sxs-lookup"><span data-stu-id="9e05f-111">Performing Culture-Insensitive String Operations in Collections</span></span>](performing-culture-insensitive-string-operations-in-collections.md)  
 <span data-ttu-id="9e05f-112">描述如何使用 <xref:System.Collections.CaseInsensitiveComparer>、<xref:System.Collections.CaseInsensitiveHashCodeProvider> 類別、<xref:System.Collections.SortedList>、<xref:System.Collections.ArrayList.Sort%2A?displayProperty=nameWithType> 和 <xref:System.Collections.Specialized.CollectionsUtil.CreateCaseInsensitiveHashtable%2A?displayProperty=nameWithType>，在集合中執行不區分文化特性的作業。</span><span class="sxs-lookup"><span data-stu-id="9e05f-112">Describes how to use the <xref:System.Collections.CaseInsensitiveComparer>, <xref:System.Collections.CaseInsensitiveHashCodeProvider> class, <xref:System.Collections.SortedList>, <xref:System.Collections.ArrayList.Sort%2A?displayProperty=nameWithType> and <xref:System.Collections.Specialized.CollectionsUtil.CreateCaseInsensitiveHashtable%2A?displayProperty=nameWithType> to perform culture-insensitive operations in collections.</span></span>  
  
 [<span data-ttu-id="9e05f-113">在陣列中執行不區分文化特性的字串作業</span><span class="sxs-lookup"><span data-stu-id="9e05f-113">Performing Culture-Insensitive String Operations in Arrays</span></span>](performing-culture-insensitive-string-operations-in-arrays.md)  
 <span data-ttu-id="9e05f-114">描述如何使用 <xref:System.Array.Sort%2A?displayProperty=nameWithType> 和 <xref:System.Array.BinarySearch%2A?displayProperty=nameWithType> 方法，在陣列中執行不區分文化特性的作業。</span><span class="sxs-lookup"><span data-stu-id="9e05f-114">Describes how to use the <xref:System.Array.Sort%2A?displayProperty=nameWithType> and <xref:System.Array.BinarySearch%2A?displayProperty=nameWithType> methods to perform culture-insensitive operations in arrays.</span></span>  
  
## <a name="related-sections"></a><span data-ttu-id="9e05f-115">相關章節</span><span class="sxs-lookup"><span data-stu-id="9e05f-115">Related sections</span></span>  

 [<span data-ttu-id="9e05f-116">不區分文化特性的字串作業</span><span class="sxs-lookup"><span data-stu-id="9e05f-116">Culture-Insensitive String Operations</span></span>](culture-insensitive-string-operations.md)  
 <span data-ttu-id="9e05f-117">描述為何您應該注意對字串執行作業時的文化特性，並提供指導方針來指出何時該執行區分文化特性的作業，何時該執行不區分文化特性的作業。</span><span class="sxs-lookup"><span data-stu-id="9e05f-117">Describes why you should be aware of culture when performing operations on strings and provides guidelines for when to perform culture-sensitive operations and when to perform culture-insensitive operations.</span></span>

## <a name="see-also"></a><span data-ttu-id="9e05f-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9e05f-118">See also</span></span>

- [<span data-ttu-id="9e05f-119">排序權數資料表 (適用於 Windows 系統上的 .NET)</span><span class="sxs-lookup"><span data-stu-id="9e05f-119">Sorting Weight Tables (for .NET on Windows systems)</span></span>](https://www.microsoft.com/download/details.aspx?id=10921)
- [<span data-ttu-id="9e05f-120">預設 Unicode 定序元素資料表 (適用於 Linux 和 macOS 上的 .NET Core)</span><span class="sxs-lookup"><span data-stu-id="9e05f-120">Default Unicode Collation Element Table (for .NET Core on Linux and macOS)</span></span>](https://www.unicode.org/Public/UCA/latest/allkeys.txt)
