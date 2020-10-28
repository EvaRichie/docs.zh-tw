---
title: 在 .NET 中比較字串
description: 深入瞭解在 .NET 中比較字串的方法。 瞭解 Compare、CompareOrdinal、CompareTo、StartsWith、EndsWith、Equals、IndexOf & LastIndexOf 方法。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- value comparisons of strings
- LastIndexOf method
- CompareTo method
- IndexOf method
- Compare method
- strings [.NET], comparing
- CompareOrdinal method
- EndsWith method
- Equals method
- StartsWith method
ms.assetid: 977dc094-fe19-4955-98ec-d2294d04a4ba
ms.openlocfilehash: 658f8b2cf7d7b2431654df1caebdac8118b3674b
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/28/2020
ms.locfileid: "92889487"
---
# <a name="comparing-strings-in-net"></a><span data-ttu-id="fe7fa-104">在 .NET 中比較字串</span><span class="sxs-lookup"><span data-stu-id="fe7fa-104">Comparing Strings in .NET</span></span>
<span data-ttu-id="fe7fa-105">.NET 會提供數種方法來比較字串值。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-105">.NET provides several methods to compare the values of strings.</span></span> <span data-ttu-id="fe7fa-106">下表列出並描述數值比較的方法。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-106">The following table lists and describes the value-comparison methods.</span></span>  
  
|<span data-ttu-id="fe7fa-107">方法名稱</span><span class="sxs-lookup"><span data-stu-id="fe7fa-107">Method name</span></span>|<span data-ttu-id="fe7fa-108">用途</span><span class="sxs-lookup"><span data-stu-id="fe7fa-108">Use</span></span>|  
|-----------------|---------|  
|<xref:System.String.Compare%2A?displayProperty=nameWithType>|<span data-ttu-id="fe7fa-109">比較兩個字串的值。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-109">Compares the values of two strings.</span></span> <span data-ttu-id="fe7fa-110">傳回整數值。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-110">Returns an integer value.</span></span>|  
|<xref:System.String.CompareOrdinal%2A?displayProperty=nameWithType>|<span data-ttu-id="fe7fa-111">比較兩個字串，而不考慮當地文化特性。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-111">Compares two strings without regard to local culture.</span></span> <span data-ttu-id="fe7fa-112">傳回整數值。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-112">Returns an integer value.</span></span>|  
|<xref:System.String.CompareTo%2A?displayProperty=nameWithType>|<span data-ttu-id="fe7fa-113">比較目前字串物件與另一個字串。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-113">Compares the current string object to another string.</span></span> <span data-ttu-id="fe7fa-114">傳回整數值。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-114">Returns an integer value.</span></span>|  
|<xref:System.String.StartsWith%2A?displayProperty=nameWithType>|<span data-ttu-id="fe7fa-115">判斷字串是否以傳遞的字串開頭。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-115">Determines whether a string begins with the string passed.</span></span> <span data-ttu-id="fe7fa-116">傳回布林值。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-116">Returns a Boolean value.</span></span>|  
|<xref:System.String.EndsWith%2A?displayProperty=nameWithType>|<span data-ttu-id="fe7fa-117">判斷字串是否以傳遞的字串結束。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-117">Determines whether a string ends with the string passed.</span></span> <span data-ttu-id="fe7fa-118">傳回布林值。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-118">Returns a Boolean value.</span></span>|  
|<xref:System.String.Equals%2A?displayProperty=nameWithType>|<span data-ttu-id="fe7fa-119">判斷兩個字串是否相同。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-119">Determines whether two strings are the same.</span></span> <span data-ttu-id="fe7fa-120">傳回布林值。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-120">Returns a Boolean value.</span></span>|  
|<xref:System.String.IndexOf%2A?displayProperty=nameWithType>|<span data-ttu-id="fe7fa-121">從您正在檢查之字串的開頭開始，傳回字元或字串的索引位置。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-121">Returns the index position of a character or string, starting from the beginning of the string you are examining.</span></span> <span data-ttu-id="fe7fa-122">傳回整數值。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-122">Returns an integer value.</span></span>|  
|<xref:System.String.LastIndexOf%2A?displayProperty=nameWithType>|<span data-ttu-id="fe7fa-123">從您正在檢查之字串的結尾開始，傳回字元或字串的索引位置。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-123">Returns the index position of a character or string, starting from the end of the string you are examining.</span></span> <span data-ttu-id="fe7fa-124">傳回整數值。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-124">Returns an integer value.</span></span>|  
  
## <a name="compare"></a><span data-ttu-id="fe7fa-125">比較</span><span class="sxs-lookup"><span data-stu-id="fe7fa-125">Compare</span></span>  
 <span data-ttu-id="fe7fa-126">靜態 <xref:System.String.Compare%2A?displayProperty=nameWithType> 方法提供全面的方式來比較兩個字串。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-126">The static <xref:System.String.Compare%2A?displayProperty=nameWithType> method provides a thorough way of comparing two strings.</span></span> <span data-ttu-id="fe7fa-127">該方法會感知文化特性。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-127">This method is culturally aware.</span></span> <span data-ttu-id="fe7fa-128">您可以使用這個函式來比較兩個字串或兩個字串的子字串。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-128">You can use this function to compare two strings or substrings of two strings.</span></span> <span data-ttu-id="fe7fa-129">此外，會假定多載為考慮或是忽略大小寫和文化特性變異數。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-129">Additionally, overloads are provided that regard or disregard case and cultural variance.</span></span> <span data-ttu-id="fe7fa-130">下表顯示這個方法可能會傳回的三個整數值。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-130">The following table shows the three integer values that this method might return.</span></span>  
  
|<span data-ttu-id="fe7fa-131">傳回值</span><span class="sxs-lookup"><span data-stu-id="fe7fa-131">Return value</span></span>|<span data-ttu-id="fe7fa-132">條件</span><span class="sxs-lookup"><span data-stu-id="fe7fa-132">Condition</span></span>|  
|------------------|---------------|  
|<span data-ttu-id="fe7fa-133">負整數</span><span class="sxs-lookup"><span data-stu-id="fe7fa-133">A negative integer</span></span>|<span data-ttu-id="fe7fa-134">在此排序次序中，第一個字串優先於第二個字串。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-134">The first string precedes the second string in the sort order.</span></span><br /><br /> <span data-ttu-id="fe7fa-135">-或-</span><span class="sxs-lookup"><span data-stu-id="fe7fa-135">-or-</span></span><br /><br /> <span data-ttu-id="fe7fa-136">第一個字串是 `null`。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-136">The first string is `null`.</span></span>|  
|<span data-ttu-id="fe7fa-137">0</span><span class="sxs-lookup"><span data-stu-id="fe7fa-137">0</span></span>|<span data-ttu-id="fe7fa-138">第一個字串和第二個字串相等。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-138">The first string and the second string are equal.</span></span><br /><br /> <span data-ttu-id="fe7fa-139">-或-</span><span class="sxs-lookup"><span data-stu-id="fe7fa-139">-or-</span></span><br /><br /> <span data-ttu-id="fe7fa-140">這兩個字串都是 `null`。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-140">Both strings are `null`.</span></span>|  
|<span data-ttu-id="fe7fa-141">正整數</span><span class="sxs-lookup"><span data-stu-id="fe7fa-141">A positive integer</span></span><br /><br /> <span data-ttu-id="fe7fa-142">-或-</span><span class="sxs-lookup"><span data-stu-id="fe7fa-142">-or-</span></span><br /><br /> <span data-ttu-id="fe7fa-143">1</span><span class="sxs-lookup"><span data-stu-id="fe7fa-143">1</span></span>|<span data-ttu-id="fe7fa-144">在此排序次序中，第一個字串在第二個字串的後面。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-144">The first string follows the second string in the sort order.</span></span><br /><br /> <span data-ttu-id="fe7fa-145">-或-</span><span class="sxs-lookup"><span data-stu-id="fe7fa-145">-or-</span></span><br /><br /> <span data-ttu-id="fe7fa-146">第二個字串是 `null`。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-146">The second string is `null`.</span></span>|  
  
> [!IMPORTANT]
> <span data-ttu-id="fe7fa-147"><xref:System.String.Compare%2A?displayProperty=nameWithType> 方法主要是用於排序或字串排序時。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-147">The <xref:System.String.Compare%2A?displayProperty=nameWithType> method is primarily intended for use when ordering or sorting strings.</span></span> <span data-ttu-id="fe7fa-148">您不應該使用 <xref:System.String.Compare%2A?displayProperty=nameWithType> 方法來測試是否相等 (也就是明確地尋找為 0 的傳回值，而不考慮字串是否小於或大於另一個字串)。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-148">You should not use the <xref:System.String.Compare%2A?displayProperty=nameWithType> method to test for equality (that is, to explicitly look for a return value of 0 with no regard for whether one string is less than or greater than the other).</span></span> <span data-ttu-id="fe7fa-149">相反地，若要判斷兩個字串是否相等，請使用 <xref:System.String.Equals%28System.String%2CSystem.String%2CSystem.StringComparison%29?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-149">Instead, to determine whether two strings are equal, use the <xref:System.String.Equals%28System.String%2CSystem.String%2CSystem.StringComparison%29?displayProperty=nameWithType> method.</span></span>  
  
 <span data-ttu-id="fe7fa-150">下列範例會使用 <xref:System.String.Compare%2A?displayProperty=nameWithType> 方法，以判斷兩個字串的相對值。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-150">The following example uses the <xref:System.String.Compare%2A?displayProperty=nameWithType> method to determine the relative values of two strings.</span></span>  
  
 [!code-cpp[Conceptual.String.BasicOps#6](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/compare.cpp#6)]
 [!code-csharp[Conceptual.String.BasicOps#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/compare.cs#6)]
 [!code-vb[Conceptual.String.BasicOps#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/compare.vb#6)]  
  
 <span data-ttu-id="fe7fa-151">此範例會顯示 `-1` 至主控台。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-151">This example displays `-1` to the console.</span></span>  
  
 <span data-ttu-id="fe7fa-152">上述範例根據預設會區分文化特性。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-152">The preceding example is culture-sensitive by default.</span></span> <span data-ttu-id="fe7fa-153">若要執行不區分文化特性的字串比較，使用 <xref:System.String.Compare%2A?displayProperty=nameWithType> 方法的多載，可讓您藉由提供「文化特性」  參數來指定要使用的文化特性。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-153">To perform a culture-insensitive string comparison, use an overload of the <xref:System.String.Compare%2A?displayProperty=nameWithType> method that allows you to specify the culture to use by supplying a *culture* parameter.</span></span> <span data-ttu-id="fe7fa-154">如需示範如何使用 <xref:System.String.Compare%2A?displayProperty=nameWithType> 方法以執行不區分文化特性比較的範例，請參閱[執行不區分文化特性的字串比較](../globalization-localization/performing-culture-insensitive-string-comparisons.md)。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-154">For an example that demonstrates how to use the <xref:System.String.Compare%2A?displayProperty=nameWithType> method to perform a culture-insensitive comparison, see [Performing Culture-Insensitive String Comparisons](../globalization-localization/performing-culture-insensitive-string-comparisons.md).</span></span>  
  
## <a name="compareordinal"></a><span data-ttu-id="fe7fa-155">CompareOrdinal</span><span class="sxs-lookup"><span data-stu-id="fe7fa-155">CompareOrdinal</span></span>  
 <span data-ttu-id="fe7fa-156"><xref:System.String.CompareOrdinal%2A?displayProperty=nameWithType> 方法會比較兩個字串物件，而不考慮當地文化特性。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-156">The <xref:System.String.CompareOrdinal%2A?displayProperty=nameWithType> method compares two string objects without considering the local culture.</span></span> <span data-ttu-id="fe7fa-157">這個方法的傳回值與上表中 **比較** 方法所傳回的值相同。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-157">The return values of this method are identical to the values returned by the **Compare** method in the previous table.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="fe7fa-158"><xref:System.String.CompareOrdinal%2A?displayProperty=nameWithType> 方法主要是用於排序或字串排序時。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-158">The <xref:System.String.CompareOrdinal%2A?displayProperty=nameWithType> method is primarily intended for use when ordering or sorting strings.</span></span> <span data-ttu-id="fe7fa-159">您不應該使用 <xref:System.String.CompareOrdinal%2A?displayProperty=nameWithType> 方法來測試是否相等 (也就是明確地尋找為 0 的傳回值，而不考慮字串是否小於或大於另一個字串)。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-159">You should not use the <xref:System.String.CompareOrdinal%2A?displayProperty=nameWithType> method to test for equality (that is, to explicitly look for a return value of 0 with no regard for whether one string is less than or greater than the other).</span></span> <span data-ttu-id="fe7fa-160">相反地，若要判斷兩個字串是否相等，請使用 <xref:System.String.Equals%28System.String%2CSystem.String%2CSystem.StringComparison%29?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-160">Instead, to determine whether two strings are equal, use the <xref:System.String.Equals%28System.String%2CSystem.String%2CSystem.StringComparison%29?displayProperty=nameWithType> method.</span></span>  
  
 <span data-ttu-id="fe7fa-161">下列範例會使用 **CompareOrdinal** 方法，以判斷兩個字串的值。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-161">The following example uses the **CompareOrdinal** method to compare the values of two strings.</span></span>  
  
 [!code-cpp[Conceptual.String.BasicOps#7](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/compare.cpp#7)]
 [!code-csharp[Conceptual.String.BasicOps#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/compare.cs#7)]
 [!code-vb[Conceptual.String.BasicOps#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/compare.vb#7)]  
  
 <span data-ttu-id="fe7fa-162">此範例會顯示 `-32` 至主控台。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-162">This example displays `-32` to the console.</span></span>  
  
## <a name="compareto"></a><span data-ttu-id="fe7fa-163">CompareTo</span><span class="sxs-lookup"><span data-stu-id="fe7fa-163">CompareTo</span></span>  
 <span data-ttu-id="fe7fa-164"><xref:System.String.CompareTo%2A?displayProperty=nameWithType> 方法會比較目前字串物件封裝到另一個字串或物件中的字串。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-164">The <xref:System.String.CompareTo%2A?displayProperty=nameWithType> method compares the string that the current string object encapsulates to another string or object.</span></span> <span data-ttu-id="fe7fa-165">這個方法的傳回值與上表中 <xref:System.String.Compare%2A?displayProperty=nameWithType> 方法所傳回的值相同。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-165">The return values of this method are identical to the values returned by the <xref:System.String.Compare%2A?displayProperty=nameWithType> method in the previous table.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="fe7fa-166"><xref:System.String.CompareTo%2A?displayProperty=nameWithType> 方法主要是用於排序或字串排序時。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-166">The <xref:System.String.CompareTo%2A?displayProperty=nameWithType> method is primarily intended for use when ordering or sorting strings.</span></span> <span data-ttu-id="fe7fa-167">您不應該使用 <xref:System.String.CompareTo%2A?displayProperty=nameWithType> 方法來測試是否相等 (也就是明確地尋找為 0 的傳回值，而不考慮字串是否小於或大於另一個字串)。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-167">You should not use the <xref:System.String.CompareTo%2A?displayProperty=nameWithType> method to test for equality (that is, to explicitly look for a return value of 0 with no regard for whether one string is less than or greater than the other).</span></span> <span data-ttu-id="fe7fa-168">相反地，若要判斷兩個字串是否相等，請使用 <xref:System.String.Equals%28System.String%2CSystem.String%2CSystem.StringComparison%29?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-168">Instead, to determine whether two strings are equal, use the <xref:System.String.Equals%28System.String%2CSystem.String%2CSystem.StringComparison%29?displayProperty=nameWithType> method.</span></span>  
  
 <span data-ttu-id="fe7fa-169">下列範例會使用 <xref:System.String.CompareTo%2A?displayProperty=nameWithType> 方法來比較 `string1` 物件和 `string2` 物件。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-169">The following example uses the <xref:System.String.CompareTo%2A?displayProperty=nameWithType> method to compare the `string1` object to the `string2` object.</span></span>  
  
 [!code-cpp[Conceptual.String.BasicOps#8](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/compare.cpp#8)]
 [!code-csharp[Conceptual.String.BasicOps#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/compare.cs#8)]
 [!code-vb[Conceptual.String.BasicOps#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/compare.vb#8)]  
  
 <span data-ttu-id="fe7fa-170">此範例會顯示 `-1` 至主控台。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-170">This example displays `-1` to the console.</span></span>  
  
 <span data-ttu-id="fe7fa-171">根據預設，<xref:System.String.CompareTo%2A?displayProperty=nameWithType> 方法的所有多載都會執行區分文化特性和區分大小寫的比較。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-171">All overloads of the <xref:System.String.CompareTo%2A?displayProperty=nameWithType> method perform culture-sensitive and case-sensitive comparisons by default.</span></span> <span data-ttu-id="fe7fa-172">此方法不提供可讓您執行不區分文化特性比較的多載。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-172">No overloads of this method are provided that allow you to perform a culture-insensitive comparison.</span></span> <span data-ttu-id="fe7fa-173">為了讓程式碼更清楚，建議您改用 **String.Compare** 方法，對於區分文化特性的作業指定 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType>，或對於不區分文化特性的作業指定 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-173">For code clarity, we recommend that you use the **String.Compare** method instead, specifying <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType> for culture-sensitive operations or <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> for culture-insensitive operations.</span></span> <span data-ttu-id="fe7fa-174">如需範例示範如何使用 **String.Compare** 方法以執行區分文化特性和不區分文化特性的比較，請參閱 [執行不區分文化特性的字串比較](../globalization-localization/performing-culture-insensitive-string-comparisons.md)。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-174">For examples that demonstrate how to use the **String.Compare** method to perform both culture-sensitive and culture-insensitive comparisons, see [Performing Culture-Insensitive String Comparisons](../globalization-localization/performing-culture-insensitive-string-comparisons.md).</span></span>  
  
## <a name="equals"></a><span data-ttu-id="fe7fa-175">等於</span><span class="sxs-lookup"><span data-stu-id="fe7fa-175">Equals</span></span>  
 <span data-ttu-id="fe7fa-176">**String.Equals** 方法可以輕易地判斷兩個字串是否相同。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-176">The **String.Equals** method can easily determine if two strings are the same.</span></span> <span data-ttu-id="fe7fa-177">這個區分大小寫的方法會傳回 **true** 或 **false** 布林值。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-177">This case-sensitive method returns a **true** or **false** Boolean value.</span></span> <span data-ttu-id="fe7fa-178">它可從現有的類別下使用，如下一個範例中所示。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-178">It can be used from an existing class, as illustrated in the next example.</span></span> <span data-ttu-id="fe7fa-179">下列範例會使用 **等於** 方法來判斷字串物件是否包含片語 "Hello World"。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-179">The following example uses the **Equals** method to determine whether a string object contains the phrase "Hello World".</span></span>  
  
 [!code-cpp[Conceptual.String.BasicOps#9](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/compare.cpp#9)]
 [!code-csharp[Conceptual.String.BasicOps#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/compare.cs#9)]
 [!code-vb[Conceptual.String.BasicOps#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/compare.vb#9)]  
  
 <span data-ttu-id="fe7fa-180">此範例會顯示 `True` 至主控台。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-180">This example displays `True` to the console.</span></span>  
  
 <span data-ttu-id="fe7fa-181">這個方法也可用做為靜態方法。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-181">This method can also be used as a static method.</span></span> <span data-ttu-id="fe7fa-182">下列範例會使用靜態方法來比較兩個字串物件。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-182">The following example compares two string objects using a static method.</span></span>  
  
 [!code-cpp[Conceptual.String.BasicOps#10](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/compare.cpp#10)]
 [!code-csharp[Conceptual.String.BasicOps#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/compare.cs#10)]
 [!code-vb[Conceptual.String.BasicOps#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/compare.vb#10)]  
  
 <span data-ttu-id="fe7fa-183">此範例會顯示 `True` 至主控台。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-183">This example displays `True` to the console.</span></span>  
  
## <a name="startswith-and-endswith"></a><span data-ttu-id="fe7fa-184">StartsWith 和 EndsWith</span><span class="sxs-lookup"><span data-stu-id="fe7fa-184">StartsWith and EndsWith</span></span>  
 <span data-ttu-id="fe7fa-185">您可以使用 **String.StartsWith** 方法來判斷字串物件開頭是否為包含另一個字串的相同字元。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-185">You can use the **String.StartsWith** method to determine whether a string object begins with the same characters that encompass another string.</span></span> <span data-ttu-id="fe7fa-186">如果目前字串物件的開頭為傳遞的字串，則這個區分大小寫的方法會傳回 **true** ，否則為 **false** 。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-186">This case-sensitive method returns **true** if the current string object begins with the passed string and **false** if it does not.</span></span> <span data-ttu-id="fe7fa-187">下列範例會使用這個方法，以判斷字串物件開頭是否為 "Hello"。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-187">The following example uses this method to determine if a string object begins with "Hello".</span></span>  
  
 [!code-cpp[Conceptual.String.BasicOps#11](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/compare.cpp#11)]
 [!code-csharp[Conceptual.String.BasicOps#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/compare.cs#11)]
 [!code-vb[Conceptual.String.BasicOps#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/compare.vb#11)]  
  
 <span data-ttu-id="fe7fa-188">此範例會顯示 `True` 至主控台。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-188">This example displays `True` to the console.</span></span>  
  
 <span data-ttu-id="fe7fa-189">**String.EndsWith** 方法會比較傳遞的字串和目前字串物件結尾上存在的字元。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-189">The **String.EndsWith** method compares a passed string to the characters that exist at the end of the current string object.</span></span> <span data-ttu-id="fe7fa-190">它也會傳回布林值。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-190">It also returns a Boolean value.</span></span> <span data-ttu-id="fe7fa-191">下列範例會使用 **EndsWith** 方法檢查字串結尾。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-191">The following example checks the end of a string using the **EndsWith** method.</span></span>  
  
 [!code-cpp[Conceptual.String.BasicOps#12](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/compare.cpp#12)]
 [!code-csharp[Conceptual.String.BasicOps#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/compare.cs#12)]
 [!code-vb[Conceptual.String.BasicOps#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/compare.vb#12)]  
  
 <span data-ttu-id="fe7fa-192">此範例會顯示 `False` 至主控台。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-192">This example displays `False` to the console.</span></span>  
  
## <a name="indexof-and-lastindexof"></a><span data-ttu-id="fe7fa-193">IndexOf 和 LastIndexOf</span><span class="sxs-lookup"><span data-stu-id="fe7fa-193">IndexOf and LastIndexOf</span></span>  
 <span data-ttu-id="fe7fa-194">您可以使用 **String.IndexOf** 方法，以判斷字串中第一次出現特定字元的位置。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-194">You can use the **String.IndexOf** method to determine the position of the first occurrence of a particular character within a string.</span></span> <span data-ttu-id="fe7fa-195">這個區分大小寫的方法從字串開頭開始算起，並使用以零為起始的索引傳回傳遞字元的位置。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-195">This case-sensitive method starts counting from the beginning of a string and returns the position of a passed character using a zero-based index.</span></span> <span data-ttu-id="fe7fa-196">如果找不到該字元，則會傳回 –1 的值。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-196">If the character cannot be found, a value of –1 is returned.</span></span>  
  
 <span data-ttu-id="fe7fa-197">下列範例會使用 **IndexOf** 方法在字串中搜尋 '`l`' 字元的第一次出現。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-197">The following example uses the **IndexOf** method to search for the first occurrence of the '`l`' character in a string.</span></span>  
  
 [!code-cpp[Conceptual.String.BasicOps#13](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/compare.cpp#13)]
 [!code-csharp[Conceptual.String.BasicOps#13](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/compare.cs#13)]
 [!code-vb[Conceptual.String.BasicOps#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/compare.vb#13)]  
  
 <span data-ttu-id="fe7fa-198">此範例會顯示 `2` 至主控台。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-198">This example displays `2` to the console.</span></span>  
  
 <span data-ttu-id="fe7fa-199">**String.LastIndexOf** 方法類似 **String.IndexOf** 方法，只是它會傳回字串內特定字元最後一次出現的位置。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-199">The **String.LastIndexOf** method is similar to the **String.IndexOf** method except that it returns the position of the last occurrence of a particular character within a string.</span></span> <span data-ttu-id="fe7fa-200">它會區分大小寫，並使用以零為起始的索引。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-200">It is case-sensitive and uses a zero-based index.</span></span>  
  
 <span data-ttu-id="fe7fa-201">下列範例會使用 **LastIndexOf** 方法在字串中搜尋 '`l`' 字元的最後一次出現。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-201">The following example uses the **LastIndexOf** method to search for the last occurrence of the '`l`' character in a string.</span></span>  
  
 [!code-cpp[Conceptual.String.BasicOps#14](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/compare.cpp#14)]
 [!code-csharp[Conceptual.String.BasicOps#14](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/compare.cs#14)]
 [!code-vb[Conceptual.String.BasicOps#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/compare.vb#14)]  
  
 <span data-ttu-id="fe7fa-202">此範例會顯示 `9` 至主控台。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-202">This example displays `9` to the console.</span></span>  
  
 <span data-ttu-id="fe7fa-203">當搭配 **String.Remove** 方法使用時，這兩種方法都很實用。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-203">Both methods are useful when used in conjunction with the **String.Remove** method.</span></span> <span data-ttu-id="fe7fa-204">您可以使用 **IndexOf** 或 **LastIndexOf** 方法來擷取字元的位置，然後提供該位置給 **移除** 方法，以移除字元或以該字元開頭的單字。</span><span class="sxs-lookup"><span data-stu-id="fe7fa-204">You can use either the **IndexOf** or **LastIndexOf** methods to retrieve the position of a character, and then supply that position to the **Remove** method in order to remove a character or a word that begins with that character.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="fe7fa-205">請參閱</span><span class="sxs-lookup"><span data-stu-id="fe7fa-205">See also</span></span>

- [<span data-ttu-id="fe7fa-206">基底字元串作業</span><span class="sxs-lookup"><span data-stu-id="fe7fa-206">Basic String Operations</span></span>](basic-string-operations.md)
- [<span data-ttu-id="fe7fa-207">執行不區分文化特性的字串作業</span><span class="sxs-lookup"><span data-stu-id="fe7fa-207">Performing Culture-Insensitive String Operations</span></span>](../globalization-localization/performing-culture-insensitive-string-operations.md)
- [<span data-ttu-id="fe7fa-208">排序權數資料表 (適用於 Windows 上的 .NET)</span><span class="sxs-lookup"><span data-stu-id="fe7fa-208">Sorting Weight Tables (for .NET on Windows)</span></span>](https://www.microsoft.com/download/details.aspx?id=10921)
- [<span data-ttu-id="fe7fa-209">預設 Unicode 定序元素資料表 (適用於 Linux 和 macOS 上的 .NET Core)</span><span class="sxs-lookup"><span data-stu-id="fe7fa-209">Default Unicode Collation Element Table (for .NET Core on Linux and macOS)</span></span>](https://www.unicode.org/Public/UCA/latest/allkeys.txt)
