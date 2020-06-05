---
title: 在 .NET 中修剪和移除字串中的字元
description: 瞭解如何從字串的開頭或結尾修剪空白空格，或從 .NET 的字串中的指定位置移除任何數目的空格或字元。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- strings [.NET Framework], removing characters
- Remove method
- TrimEnd method
- Trim method
- trimming characters
- TrimStart method
- removing characters
ms.assetid: ab248dab-70d4-4413-81c6-542d153fd195
ms.openlocfilehash: 630fe6b51d151d1f1384f2e3cde62750c303d883
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2020
ms.locfileid: "84446889"
---
# <a name="trimming-and-removing-characters-from-strings-in-net"></a><span data-ttu-id="96ccd-103">在 .NET 中修剪和移除字串中的字元</span><span class="sxs-lookup"><span data-stu-id="96ccd-103">Trimming and Removing Characters from Strings in .NET</span></span>
<span data-ttu-id="96ccd-104">如果您將句子剖析成個別文字，最後可能會得到許多文字，但文字任一端有空格 (也稱為空白字元)。</span><span class="sxs-lookup"><span data-stu-id="96ccd-104">If you are parsing a sentence into individual words, you might end up with words that have blank spaces (also called white spaces) on either end of the word.</span></span> <span data-ttu-id="96ccd-105">在這種情況下，您可以使用 **System.String** 類別中的其中一個 Trim 方法，從字串中的指定位置移除任意數目的空格或其他字元。</span><span class="sxs-lookup"><span data-stu-id="96ccd-105">In this situation, you can use one of the trim methods in the **System.String** class to remove any number of spaces or other characters from a specified position in the string.</span></span> <span data-ttu-id="96ccd-106">下表描述可用的 Trim 方法。</span><span class="sxs-lookup"><span data-stu-id="96ccd-106">The following table describes the available trim methods.</span></span>  
  
|<span data-ttu-id="96ccd-107">方法名稱</span><span class="sxs-lookup"><span data-stu-id="96ccd-107">Method name</span></span>|<span data-ttu-id="96ccd-108">使用</span><span class="sxs-lookup"><span data-stu-id="96ccd-108">Use</span></span>|  
|-----------------|---------|  
|<xref:System.String.Trim%2A?displayProperty=nameWithType>|<span data-ttu-id="96ccd-109">將字元陣列中字串開頭和結尾指定的空格或空白字元移除。</span><span class="sxs-lookup"><span data-stu-id="96ccd-109">Removes white spaces or characters specified in an array of characters from the beginning and end of a string.</span></span>|  
|<xref:System.String.TrimEnd%2A?displayProperty=nameWithType>|<span data-ttu-id="96ccd-110">從字串尾端移除字元陣列中指定的字元。</span><span class="sxs-lookup"><span data-stu-id="96ccd-110">Removes characters specified in an array of characters from the end of a string.</span></span>|  
|<xref:System.String.TrimStart%2A?displayProperty=nameWithType>|<span data-ttu-id="96ccd-111">從字串開頭移除字元陣列中指定的字元。</span><span class="sxs-lookup"><span data-stu-id="96ccd-111">Removes characters specified in an array of characters from the beginning of a string.</span></span>|  
|<xref:System.String.Remove%2A?displayProperty=nameWithType>|<span data-ttu-id="96ccd-112">從字串中指定的索引位置移除指定的字元數。</span><span class="sxs-lookup"><span data-stu-id="96ccd-112">Removes a specified number of characters from a specified index position in a string.</span></span>|  
  
## <a name="trim"></a><span data-ttu-id="96ccd-113">Trim</span><span class="sxs-lookup"><span data-stu-id="96ccd-113">Trim</span></span>

 <span data-ttu-id="96ccd-114">您可以使用 <xref:System.String.Trim%2A?displayProperty=nameWithType> 方法，輕鬆地移除字串頭尾的空格，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="96ccd-114">You can easily remove white spaces from both ends of a string by using the <xref:System.String.Trim%2A?displayProperty=nameWithType> method, as shown in the following example.</span></span>  
  
 [!code-cpp[Conceptual.String.BasicOps#17](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/trimming.cpp#17)]
 [!code-csharp[Conceptual.String.BasicOps#17](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/trimming.cs#17)]
 [!code-vb[Conceptual.String.BasicOps#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/trimming.vb#17)]  
  
 <span data-ttu-id="96ccd-115">您也可以將字元陣列中字串開頭和結尾指定的字元移除。</span><span class="sxs-lookup"><span data-stu-id="96ccd-115">You can also remove characters that you specify in a character array from the beginning and end of a string.</span></span> <span data-ttu-id="96ccd-116">下列範例將會移除空白字元、句號和星號。</span><span class="sxs-lookup"><span data-stu-id="96ccd-116">The following example removes white-space characters, periods, and asterisks.</span></span>  
  
 [!code-csharp[Conceptual.String.BasicOps#22](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/trim2.cs#22)]
 [!code-vb[Conceptual.String.BasicOps#22](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/trim2.vb#22)]  
  
## <a name="trimend"></a><span data-ttu-id="96ccd-117">TrimEnd</span><span class="sxs-lookup"><span data-stu-id="96ccd-117">TrimEnd</span></span>

 <span data-ttu-id="96ccd-118">**String.TrimEnd** 方法會從字串結尾移除字元，並建立新的字串物件。</span><span class="sxs-lookup"><span data-stu-id="96ccd-118">The **String.TrimEnd** method removes characters from the end of a string, creating a new string object.</span></span> <span data-ttu-id="96ccd-119">系統會將字元陣列傳遞給這個方法，以指定要移除的字元。</span><span class="sxs-lookup"><span data-stu-id="96ccd-119">An array of characters is passed to this method to specify the characters to be removed.</span></span> <span data-ttu-id="96ccd-120">字元陣列中的項目順序不會影響修剪作業。</span><span class="sxs-lookup"><span data-stu-id="96ccd-120">The order of the elements in the character array does not affect the trim operation.</span></span> <span data-ttu-id="96ccd-121">一旦找到陣列中未指定的字元時，修剪作業就會停止。</span><span class="sxs-lookup"><span data-stu-id="96ccd-121">The trim stops when a character not specified in the array is found.</span></span>  
  
 <span data-ttu-id="96ccd-122">下列範例會使用 **TrimEnd** 方法，移除字串的最後一個字母。</span><span class="sxs-lookup"><span data-stu-id="96ccd-122">The following example removes the last letters of a string using the **TrimEnd** method.</span></span> <span data-ttu-id="96ccd-123">在此範例中，`'r'` 字元和 `'W'` 字元的位置顛倒，用以說明字元陣列中的順序並不重要。</span><span class="sxs-lookup"><span data-stu-id="96ccd-123">In this example, the position of the `'r'` character and the `'W'` character are reversed to illustrate that the order of characters in the array does not matter.</span></span> <span data-ttu-id="96ccd-124">請注意，此程式碼會移除 `MyString` 的最後一個字以及第一個字的一部分。</span><span class="sxs-lookup"><span data-stu-id="96ccd-124">Notice that this code removes the last word of `MyString` plus part of the first.</span></span>  
  
 [!code-cpp[Conceptual.String.BasicOps#18](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/trimming.cpp#18)]
 [!code-csharp[Conceptual.String.BasicOps#18](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/trimming.cs#18)]
 [!code-vb[Conceptual.String.BasicOps#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/trimming.vb#18)]  
  
 <span data-ttu-id="96ccd-125">此程式碼會讓主控台顯示 `He`。</span><span class="sxs-lookup"><span data-stu-id="96ccd-125">This code displays `He` to the console.</span></span>  
  
 <span data-ttu-id="96ccd-126">下列範例會使用 **TrimEnd** 方法，移除字串的最後一個文字。</span><span class="sxs-lookup"><span data-stu-id="96ccd-126">The following example removes the last word of a string using the **TrimEnd** method.</span></span> <span data-ttu-id="96ccd-127">在這個程式碼中，`Hello` 文字後接一個逗號，不過由於要修剪的字元陣列中未指定逗號，因此修剪作業會在逗號處停止。</span><span class="sxs-lookup"><span data-stu-id="96ccd-127">In this code, a comma follows the word `Hello` and, because the comma is not specified in the array of characters to trim, the trim ends at the comma.</span></span>  
  
 [!code-cpp[Conceptual.String.BasicOps#19](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/trimming.cpp#19)]
 [!code-csharp[Conceptual.String.BasicOps#19](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/trimming.cs#19)]
 [!code-vb[Conceptual.String.BasicOps#19](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/trimming.vb#19)]  
  
 <span data-ttu-id="96ccd-128">此程式碼會讓主控台顯示 `Hello,`。</span><span class="sxs-lookup"><span data-stu-id="96ccd-128">This code displays `Hello,` to the console.</span></span>  
  
## <a name="trimstart"></a><span data-ttu-id="96ccd-129">TrimStart</span><span class="sxs-lookup"><span data-stu-id="96ccd-129">TrimStart</span></span>

 <span data-ttu-id="96ccd-130">**String.TrimStart** 方法與 **String.TrimEnd** 方法類似，只是它會移除現有字串物件開頭的字元以建立新字串。</span><span class="sxs-lookup"><span data-stu-id="96ccd-130">The **String.TrimStart** method is similar to the **String.TrimEnd** method except that it creates a new string by removing characters from the beginning of an existing string object.</span></span> <span data-ttu-id="96ccd-131">系統會將字元陣列傳遞給 **TrimStart** 方法，以指定要移除的字元。</span><span class="sxs-lookup"><span data-stu-id="96ccd-131">An array of characters is passed to the **TrimStart** method to specify the characters to be removed.</span></span> <span data-ttu-id="96ccd-132">使用 **TrimEnd** 時，字元陣列中的項目順序不會影響修剪作業。</span><span class="sxs-lookup"><span data-stu-id="96ccd-132">As with the **TrimEnd** method, the order of the elements in the character array does not affect the trim operation.</span></span> <span data-ttu-id="96ccd-133">一旦找到陣列中未指定的字元時，修剪作業就會停止。</span><span class="sxs-lookup"><span data-stu-id="96ccd-133">The trim stops when a character not specified in the array is found.</span></span>  
  
 <span data-ttu-id="96ccd-134">下列範例會移除字串的第一個文字。</span><span class="sxs-lookup"><span data-stu-id="96ccd-134">The following example removes the first word of a string.</span></span> <span data-ttu-id="96ccd-135">在此範例中，`'l'` 字元和 `'H'` 字元的位置顛倒，用以說明字元陣列中的順序並不重要。</span><span class="sxs-lookup"><span data-stu-id="96ccd-135">In this example, the position of the `'l'` character and the `'H'` character are reversed to illustrate that the order of characters in the array does not matter.</span></span>  
  
 [!code-cpp[Conceptual.String.BasicOps#20](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/trimming.cpp#20)]
 [!code-csharp[Conceptual.String.BasicOps#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/trimming.cs#20)]
 [!code-vb[Conceptual.String.BasicOps#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/trimming.vb#20)]  
  
 <span data-ttu-id="96ccd-136">此程式碼會讓主控台顯示 `World!`。</span><span class="sxs-lookup"><span data-stu-id="96ccd-136">This code displays `World!` to the console.</span></span>  
  
## <a name="remove"></a><span data-ttu-id="96ccd-137">移除</span><span class="sxs-lookup"><span data-stu-id="96ccd-137">Remove</span></span>

 <span data-ttu-id="96ccd-138"><xref:System.String.Remove%2A?displayProperty=nameWithType> 方法會從現有字串中的指定位置開始，移除指定的字元數。</span><span class="sxs-lookup"><span data-stu-id="96ccd-138">The <xref:System.String.Remove%2A?displayProperty=nameWithType> method removes a specified number of characters that begin at a specified position in an existing string.</span></span> <span data-ttu-id="96ccd-139">這個方法會假設以零為起始的索引。</span><span class="sxs-lookup"><span data-stu-id="96ccd-139">This method assumes a zero-based index.</span></span>  
  
 <span data-ttu-id="96ccd-140">下列範例會於字串中以零為起始之索引的位置五開始，從字串中移除 10 個字元。</span><span class="sxs-lookup"><span data-stu-id="96ccd-140">The following example removes ten characters from a string beginning at position five of a zero-based index of the string.</span></span>  
  
 [!code-cpp[Conceptual.String.BasicOps#21](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/trimming.cpp#21)]
 [!code-csharp[Conceptual.String.BasicOps#21](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/trimming.cs#21)]
 [!code-vb[Conceptual.String.BasicOps#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/trimming.vb#21)]  
  
## <a name="replace"></a><span data-ttu-id="96ccd-141">Replace</span><span class="sxs-lookup"><span data-stu-id="96ccd-141">Replace</span></span>

 <span data-ttu-id="96ccd-142">您也可以從字串中移除指定的字元或子字串，方法是呼叫 <xref:System.String.Replace%28System.String%2CSystem.String%29?displayProperty=nameWithType> 方法並指定空字串 (<xref:System.String.Empty?displayProperty=nameWithType>) 做為取代。</span><span class="sxs-lookup"><span data-stu-id="96ccd-142">You can also remove a specified character or substring from a string by calling the <xref:System.String.Replace%28System.String%2CSystem.String%29?displayProperty=nameWithType> method and specifying an empty string (<xref:System.String.Empty?displayProperty=nameWithType>) as the replacement.</span></span> <span data-ttu-id="96ccd-143">下列範例將會從字串中移除所有逗號。</span><span class="sxs-lookup"><span data-stu-id="96ccd-143">The following example removes all commas from a string.</span></span>  
  
 [!code-csharp[Conceptual.String.BasicOps#23](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/replace1.cs#23)]
 [!code-vb[Conceptual.String.BasicOps#23](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/replace1.vb#23)]  
  
## <a name="see-also"></a><span data-ttu-id="96ccd-144">請參閱</span><span class="sxs-lookup"><span data-stu-id="96ccd-144">See also</span></span>

- [<span data-ttu-id="96ccd-145">基底字元串作業</span><span class="sxs-lookup"><span data-stu-id="96ccd-145">Basic String Operations</span></span>](basic-string-operations.md)
