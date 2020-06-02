---
title: 在陣列中執行不區分文化特性的字串作業
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- culture-insensitive string operations, in arrays
- arrays [.NET Framework], culture-insensitive string operations
- comparer parameter
ms.assetid: f12922e1-6234-4165-8896-63f0653ab478
ms.openlocfilehash: 02690f78184ca4f216df7346a84f0266c2dcec99
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288598"
---
# <a name="performing-culture-insensitive-string-operations-in-arrays"></a><span data-ttu-id="e9f5b-102">在陣列中執行不區分文化特性的字串作業</span><span class="sxs-lookup"><span data-stu-id="e9f5b-102">Performing Culture-Insensitive String Operations in Arrays</span></span>

<span data-ttu-id="e9f5b-103"><xref:System.Array.Sort%2A?displayProperty=nameWithType> 和 <xref:System.Array.BinarySearch%2A?displayProperty=nameWithType> 方法的多載預設會使用 <xref:System.Threading.Thread.CurrentCulture%2A?displayProperty=nameWithType> 屬性執行區分文化特性的排序。</span><span class="sxs-lookup"><span data-stu-id="e9f5b-103">Overloads of the <xref:System.Array.Sort%2A?displayProperty=nameWithType> and <xref:System.Array.BinarySearch%2A?displayProperty=nameWithType> methods perform culture-sensitive sorts by default using the <xref:System.Threading.Thread.CurrentCulture%2A?displayProperty=nameWithType> property.</span></span> <span data-ttu-id="e9f5b-104">這些方法所傳回的區分文化特性的結果可能會因為文化特性排序順序上的差異而有所不同。</span><span class="sxs-lookup"><span data-stu-id="e9f5b-104">Culture-sensitive results returned by these methods can vary by culture due to differences in sort orders.</span></span> <span data-ttu-id="e9f5b-105">若要消除區分文化特性的行為，請使用此方法中可接受 `comparer` 參數的其中一個多載。</span><span class="sxs-lookup"><span data-stu-id="e9f5b-105">To eliminate culture-sensitive behavior, use one of the overloads of this method that accepts a `comparer` parameter.</span></span> <span data-ttu-id="e9f5b-106">`comparer` 參數會指定要在比較陣列中元素時使用的 <xref:System.Collections.IComparer> 實作。</span><span class="sxs-lookup"><span data-stu-id="e9f5b-106">The `comparer` parameter specifies the <xref:System.Collections.IComparer> implementation to use when comparing elements in the array.</span></span> <span data-ttu-id="e9f5b-107">為參數指定一個使用 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> 的自訂非變異值比較子類別。</span><span class="sxs-lookup"><span data-stu-id="e9f5b-107">For the parameter, specify a custom invariant comparer class that uses <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType>.</span></span> <span data-ttu-id="e9f5b-108">如需自訂非變異值比較子類別的範例，請參閱[在集合中執行不區分文化特性的字串作業](performing-culture-insensitive-string-operations-in-collections.md)主題中的「使用 SortedList 類別」子主題。</span><span class="sxs-lookup"><span data-stu-id="e9f5b-108">An example of a custom invariant comparer class is provided in the "Using the SortedList Class" subtopic of the [Performing Culture-Insensitive String Operations in Collections](performing-culture-insensitive-string-operations-in-collections.md) topic.</span></span>

> [!NOTE]
> <span data-ttu-id="e9f5b-109">將**InvariantCulture**傳遞至比較方法，會執行不區分文化特性的比較。</span><span class="sxs-lookup"><span data-stu-id="e9f5b-109">Passing **CultureInfo.InvariantCulture** to a comparison method does perform a culture-insensitive comparison.</span></span> <span data-ttu-id="e9f5b-110">不過，它不會讓某些項目進行非語言比較，例如檔案路徑、登錄機碼和環境變數。</span><span class="sxs-lookup"><span data-stu-id="e9f5b-110">However, it does not cause a non-linguistic comparison, for example, for file paths, registry keys, and environment variables.</span></span> <span data-ttu-id="e9f5b-111">它也不支援根據比較結果所做出的安全性決策。</span><span class="sxs-lookup"><span data-stu-id="e9f5b-111">Neither does it support security decisions based on the comparison result.</span></span> <span data-ttu-id="e9f5b-112">若要進行非語言比較或需要支援根據結果的安全性決策，應用程式應該使用可接受 <xref:System.StringComparison> 值的比較方法。</span><span class="sxs-lookup"><span data-stu-id="e9f5b-112">For a non-linguistic comparison or support for result-based security decisions, the application should use a comparison method that accepts a <xref:System.StringComparison> value.</span></span> <span data-ttu-id="e9f5b-113">接著，應用程式應該會傳遞 <xref:System.StringComparison.Ordinal>。</span><span class="sxs-lookup"><span data-stu-id="e9f5b-113">The application should then pass <xref:System.StringComparison.Ordinal>.</span></span>

## <a name="see-also"></a><span data-ttu-id="e9f5b-114">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e9f5b-114">See also</span></span>

- <xref:System.Array.Sort%2A?displayProperty=nameWithType>
- <xref:System.Array.BinarySearch%2A?displayProperty=nameWithType>
- <xref:System.Collections.IComparer>
- [<span data-ttu-id="e9f5b-115">執行不區分文化特性的字串作業</span><span class="sxs-lookup"><span data-stu-id="e9f5b-115">Performing Culture-Insensitive String Operations</span></span>](performing-culture-insensitive-string-operations.md)
