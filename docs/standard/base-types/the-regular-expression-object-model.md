---
title: 規則運算式物件模型
description: 請參閱 .NET 中的正則運算式物件模型。 使用正則運算式引擎，& 物件 & 與相符、群組、& 捕捉相關的集合。
ms.topic: conceptual
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- searching with regular expressions, backreferences
- Regex class
- Match class
- pattern-matching with regular expressions, backreferences
- .NET regular expressions, classes
- CaptureCollection class
- Group class
- characters [.NET], backreferences
- substrings
- .NET regular expressions, backreferences
- searching with regular expressions, classes
- backreferences
- Capture class
- repeating groups of characters
- MatchCollection class
- parsing text with regular expressions, backreferences
- regular expressions [.NET]
- characters [.NET], regular expressions
- classes [.NET], regular expression
- regular expressions [.NET], classes
- characters [.NET], metacharacters
- metacharacters, regular expression classes
- metacharacters, backreferences
- parsing text with regular expressions, classes
- regular expressions [.NET], backreferences
- strings [.NET], regular expressions
- pattern-matching with regular expressions, classes
- GroupCollection class
ms.assetid: 49a21470-64ca-4b5a-a889-8e24e3c0af7e
ms.openlocfilehash: 115955f48f0470adf584acf2c2e72680cef105cb
ms.sourcegitcommit: 4313614f57690f9a5119a37314f0a1fd738ebda2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/22/2021
ms.locfileid: "98692561"
---
# <a name="the-regular-expression-object-model"></a><span data-ttu-id="4d0eb-104">規則運算式物件模型</span><span class="sxs-lookup"><span data-stu-id="4d0eb-104">The Regular Expression Object Model</span></span>

<a name="introduction"></a> <span data-ttu-id="4d0eb-105">本主題說明用來處理 .NET 規則運算式的物件模型。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-105">This topic describes the object model used in working with .NET regular expressions.</span></span> <span data-ttu-id="4d0eb-106">它包含下列區段：</span><span class="sxs-lookup"><span data-stu-id="4d0eb-106">It contains the following sections:</span></span>  
  
- [<span data-ttu-id="4d0eb-107">正則運算式引擎</span><span class="sxs-lookup"><span data-stu-id="4d0eb-107">The Regular Expression Engine</span></span>](#Engine)  
  
- [<span data-ttu-id="4d0eb-108">>matchcollection 和 Match 物件</span><span class="sxs-lookup"><span data-stu-id="4d0eb-108">The MatchCollection and Match Objects</span></span>](#Match_and_MCollection)  
  
- [<span data-ttu-id="4d0eb-109">群組集合</span><span class="sxs-lookup"><span data-stu-id="4d0eb-109">The Group Collection</span></span>](#GroupCollection)  
  
- [<span data-ttu-id="4d0eb-110">已捕獲的群組</span><span class="sxs-lookup"><span data-stu-id="4d0eb-110">The Captured Group</span></span>](#the_captured_group)  
  
- [<span data-ttu-id="4d0eb-111">Capture 集合</span><span class="sxs-lookup"><span data-stu-id="4d0eb-111">The Capture Collection</span></span>](#CaptureCollection)  
  
- [<span data-ttu-id="4d0eb-112">個別的捕獲</span><span class="sxs-lookup"><span data-stu-id="4d0eb-112">The Individual Capture</span></span>](#the_individual_capture)  
  
<a name="Engine"></a>

## <a name="the-regular-expression-engine"></a><span data-ttu-id="4d0eb-113">規則運算式引擎</span><span class="sxs-lookup"><span data-stu-id="4d0eb-113">The Regular Expression Engine</span></span>  

 <span data-ttu-id="4d0eb-114">.NET 的規則運算式引擎會以 <xref:System.Text.RegularExpressions.Regex> 類別表示。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-114">The regular expression engine in .NET is represented by the <xref:System.Text.RegularExpressions.Regex> class.</span></span> <span data-ttu-id="4d0eb-115">規則運算式引擎負責剖析和編譯規則運算式，以及執行規則運算式模式與輸入字串的比對作業。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-115">The regular expression engine is responsible for parsing and compiling a regular expression, and for performing operations that match the regular expression pattern with an input string.</span></span> <span data-ttu-id="4d0eb-116">引擎是 .NET 規則運算式物件模型的中心元件。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-116">The engine is the central component in the .NET regular expression object model.</span></span>  
  
 <span data-ttu-id="4d0eb-117">規則運算式引擎有兩種使用方式：</span><span class="sxs-lookup"><span data-stu-id="4d0eb-117">You can use the regular expression engine in either of two ways:</span></span>  
  
- <span data-ttu-id="4d0eb-118">呼叫 <xref:System.Text.RegularExpressions.Regex> 類別的靜態方法。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-118">By calling the static methods of the <xref:System.Text.RegularExpressions.Regex> class.</span></span> <span data-ttu-id="4d0eb-119">方法參數包括輸入字串和規則運算式模式。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-119">The method parameters include the input string and the regular expression pattern.</span></span> <span data-ttu-id="4d0eb-120">規則運算式引擎會快取靜態方法呼叫中所使用的規則運算式，因此重複呼叫使用相同規則運算式的靜態規則運算式方法，可提供相對較佳的效能。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-120">The regular expression engine caches regular expressions that are used in static method calls, so repeated calls to static regular expression methods that use the same regular expression offer relatively good performance.</span></span>  
  
- <span data-ttu-id="4d0eb-121">傳遞規則運算式到類別建構函式，以具現化 <xref:System.Text.RegularExpressions.Regex> 物件。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-121">By instantiating a <xref:System.Text.RegularExpressions.Regex> object, by passing a regular expression to the class constructor.</span></span> <span data-ttu-id="4d0eb-122">在此案例中，<xref:System.Text.RegularExpressions.Regex> 物件不可變 (唯讀)，並代表與單一規則運算式緊密結合的規則運算式引擎。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-122">In this case, the <xref:System.Text.RegularExpressions.Regex> object is immutable (read-only) and represents a regular expression engine that is tightly coupled with a single regular expression.</span></span> <span data-ttu-id="4d0eb-123">由於未快取 <xref:System.Text.RegularExpressions.Regex> 執行個體所使用的規則運算式，因此您不應該以相同的規則運算式將 <xref:System.Text.RegularExpressions.Regex> 物件具現化多次。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-123">Because regular expressions used by <xref:System.Text.RegularExpressions.Regex> instances are not cached, you should not instantiate a <xref:System.Text.RegularExpressions.Regex> object multiple times with the same regular expression.</span></span>  
  
 <span data-ttu-id="4d0eb-124">您可以呼叫 <xref:System.Text.RegularExpressions.Regex> 類別的方法來執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="4d0eb-124">You can call the methods of the <xref:System.Text.RegularExpressions.Regex> class to perform the following operations:</span></span>  
  
- <span data-ttu-id="4d0eb-125">判定字串是否符合規則運算式模式。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-125">Determine whether a string matches a regular expression pattern.</span></span>  
  
- <span data-ttu-id="4d0eb-126">擷取單一相符項目或第一個相符項目。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-126">Extract a single match or the first match.</span></span>  
  
- <span data-ttu-id="4d0eb-127">擷取所有相符項目。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-127">Extract all matches.</span></span>  
  
- <span data-ttu-id="4d0eb-128">取代相符的子字串。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-128">Replace a matched substring.</span></span>  
  
- <span data-ttu-id="4d0eb-129">將單一字串分割成字串陣列。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-129">Split a single string into an array of strings.</span></span>  
  
 <span data-ttu-id="4d0eb-130">下面各節將會說明這些作業。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-130">These operations are described in the following sections.</span></span>  
  
### <a name="matching-a-regular-expression-pattern"></a><span data-ttu-id="4d0eb-131">比對規則運算式模式</span><span class="sxs-lookup"><span data-stu-id="4d0eb-131">Matching a Regular Expression Pattern</span></span>  

 <span data-ttu-id="4d0eb-132">如果字串符合模式，<xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=nameWithType> 方法會傳回 `true`，如果不符合，則傳回 `false`。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-132">The <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=nameWithType> method returns `true` if the string matches the pattern, or `false` if it does not.</span></span> <span data-ttu-id="4d0eb-133"><xref:System.Text.RegularExpressions.Regex.IsMatch%2A> 方法常用來驗證字串輸入。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-133">The <xref:System.Text.RegularExpressions.Regex.IsMatch%2A> method is often used to validate string input.</span></span> <span data-ttu-id="4d0eb-134">例如，下列程式碼可確保字串符合美國境內有效的社會安全號碼。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-134">For example, the following code ensures that a string matches a valid social security number in the United States.</span></span>  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/validate1.cs#1)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/validate1.vb#1)]  
  
 <span data-ttu-id="4d0eb-135">規則運算式模式 `^\d{3}-\d{2}-\d{4}$` 的解譯方式如下表所示。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-135">The regular expression pattern `^\d{3}-\d{2}-\d{4}$` is interpreted as shown in the following table.</span></span>  
  
|<span data-ttu-id="4d0eb-136">模式</span><span class="sxs-lookup"><span data-stu-id="4d0eb-136">Pattern</span></span>|<span data-ttu-id="4d0eb-137">描述</span><span class="sxs-lookup"><span data-stu-id="4d0eb-137">Description</span></span>|  
|-------------|-----------------|  
|`^`|<span data-ttu-id="4d0eb-138">比對輸入字串的開頭。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-138">Match the beginning of the input string.</span></span>|  
|`\d{3}`|<span data-ttu-id="4d0eb-139">比對三個十進位數字。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-139">Match three decimal digits.</span></span>|  
|`-`|<span data-ttu-id="4d0eb-140">比對連字號。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-140">Match a hyphen.</span></span>|  
|`\d{2}`|<span data-ttu-id="4d0eb-141">比對兩個十進位數字。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-141">Match two decimal digits.</span></span>|  
|`-`|<span data-ttu-id="4d0eb-142">比對連字號。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-142">Match a hyphen.</span></span>|  
|`\d{4}`|<span data-ttu-id="4d0eb-143">比對四個十進位數字。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-143">Match four decimal digits.</span></span>|  
|`$`|<span data-ttu-id="4d0eb-144">比對輸入字串的結尾。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-144">Match the end of the input string.</span></span>|  
  
### <a name="extracting-a-single-match-or-the-first-match"></a><span data-ttu-id="4d0eb-145">擷取單一相符項目或第一個相符項目</span><span class="sxs-lookup"><span data-stu-id="4d0eb-145">Extracting a Single Match or the First Match</span></span>  

 <span data-ttu-id="4d0eb-146"><xref:System.Text.RegularExpressions.Regex.Match%2A?displayProperty=nameWithType> 方法會傳回 <xref:System.Text.RegularExpressions.Match> 物件，其中包含符合規則運算式模式之第一個子字串的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-146">The <xref:System.Text.RegularExpressions.Regex.Match%2A?displayProperty=nameWithType> method returns a <xref:System.Text.RegularExpressions.Match> object that contains information about the first substring that matches a regular expression pattern.</span></span> <span data-ttu-id="4d0eb-147">如果 `Match.Success` 屬性傳回 `true`，指出已找到相符項目，您就可以呼叫 <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=nameWithType> 方法來擷取後續相符項目的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-147">If the `Match.Success` property returns `true`, indicating that a match was found, you can retrieve information about subsequent matches by calling the <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="4d0eb-148">這些方法呼叫可以一直持續到 `Match.Success` 屬性傳回 `false`。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-148">These method calls can continue until the `Match.Success` property returns `false`.</span></span> <span data-ttu-id="4d0eb-149">例如，下列程式碼會使用 <xref:System.Text.RegularExpressions.Regex.Match%28System.String%2CSystem.String%29?displayProperty=nameWithType> 方法來尋找字串中第一次出現的重複文字。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-149">For example, the following code uses the <xref:System.Text.RegularExpressions.Regex.Match%28System.String%2CSystem.String%29?displayProperty=nameWithType> method to find the first occurrence of a duplicated word in a string.</span></span> <span data-ttu-id="4d0eb-150">然後會呼叫 <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=nameWithType> 方法來尋找所出現的任何其他重複文字。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-150">It then calls the <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=nameWithType> method to find any additional occurrences.</span></span> <span data-ttu-id="4d0eb-151">此範例會在每次方法呼叫之後檢查 `Match.Success` 屬性，以判定目前比對是否成功，以及後面是否應該接著呼叫 <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-151">The example examines the `Match.Success` property after each method call to determine whether the current match was successful and whether a call to the <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=nameWithType> method should follow.</span></span>  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/match1.cs#2)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/match1.vb#2)]  
  
 <span data-ttu-id="4d0eb-152">規則運算式模式 `\b(\w+)\W+(\1)\b` 的解譯方式如下表所示。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-152">The regular expression pattern `\b(\w+)\W+(\1)\b` is interpreted as shown in the following table.</span></span>  
  
|<span data-ttu-id="4d0eb-153">模式</span><span class="sxs-lookup"><span data-stu-id="4d0eb-153">Pattern</span></span>|<span data-ttu-id="4d0eb-154">描述</span><span class="sxs-lookup"><span data-stu-id="4d0eb-154">Description</span></span>|  
|-------------|-----------------|  
|`\b`|<span data-ttu-id="4d0eb-155">開始字邊界比對。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-155">Begin the match on a word boundary.</span></span>|  
|`(\w+)`|<span data-ttu-id="4d0eb-156">比對一個或多個文字字元。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-156">Match one or more word characters.</span></span> <span data-ttu-id="4d0eb-157">這是第一個擷取群組。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-157">This is the first capturing group.</span></span>|  
|`\W+`|<span data-ttu-id="4d0eb-158">比對一或多個非文字字元。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-158">Match one or more non-word characters.</span></span>|  
|`(\1)`|<span data-ttu-id="4d0eb-159">比對第一個擷取的字串。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-159">Match the first captured string.</span></span> <span data-ttu-id="4d0eb-160">這是第二個擷取群組。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-160">This is the second capturing group.</span></span>|  
|`\b`|<span data-ttu-id="4d0eb-161">結束字邊界比對。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-161">End the match on a word boundary.</span></span>|  
  
### <a name="extracting-all-matches"></a><span data-ttu-id="4d0eb-162">擷取所有相符項目</span><span class="sxs-lookup"><span data-stu-id="4d0eb-162">Extracting All Matches</span></span>  

 <span data-ttu-id="4d0eb-163"><xref:System.Text.RegularExpressions.Regex.Matches%2A?displayProperty=nameWithType> 方法會傳回 <xref:System.Text.RegularExpressions.MatchCollection> 物件，其中包含規則運算式引擎在輸入字串中找到之所有相符項目的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-163">The <xref:System.Text.RegularExpressions.Regex.Matches%2A?displayProperty=nameWithType> method returns a <xref:System.Text.RegularExpressions.MatchCollection> object that contains information about all matches that the regular expression engine found in the input string.</span></span> <span data-ttu-id="4d0eb-164">例如，您可以將上一個範例重寫為呼叫 <xref:System.Text.RegularExpressions.Regex.Matches%2A> 方法，而不是 <xref:System.Text.RegularExpressions.Regex.Match%2A> 和 <xref:System.Text.RegularExpressions.Match.NextMatch%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-164">For example, the previous example could be rewritten to call the <xref:System.Text.RegularExpressions.Regex.Matches%2A> method instead of the <xref:System.Text.RegularExpressions.Regex.Match%2A> and <xref:System.Text.RegularExpressions.Match.NextMatch%2A> methods.</span></span>  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/matches1.cs#3)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/matches1.vb#3)]  
  
### <a name="replacing-a-matched-substring"></a><span data-ttu-id="4d0eb-165">取代相符的子字串</span><span class="sxs-lookup"><span data-stu-id="4d0eb-165">Replacing a Matched Substring</span></span>  

 <span data-ttu-id="4d0eb-166"><xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=nameWithType> 方法會將符合規則運算式模式的每個子字串，取代為指定的字串或規則運算式模式，並傳回含有取代項目的整個輸入字串。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-166">The <xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=nameWithType> method replaces each substring that matches the regular expression pattern with a specified string or regular expression pattern, and returns the entire input string with replacements.</span></span> <span data-ttu-id="4d0eb-167">例如，下列程式碼會在字串中的十進位數字前面加上美國貨幣符號。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-167">For example, the following code adds a U.S. currency symbol before a decimal number in a string.</span></span>  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/replace1.cs#4)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/replace1.vb#4)]  
  
 <span data-ttu-id="4d0eb-168">規則運算式模式 `\b\d+\.\d{2}\b` 的解譯方式如下表所示。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-168">The regular expression pattern `\b\d+\.\d{2}\b` is interpreted as shown in the following table.</span></span>  
  
|<span data-ttu-id="4d0eb-169">模式</span><span class="sxs-lookup"><span data-stu-id="4d0eb-169">Pattern</span></span>|<span data-ttu-id="4d0eb-170">描述</span><span class="sxs-lookup"><span data-stu-id="4d0eb-170">Description</span></span>|  
|-------------|-----------------|  
|`\b`|<span data-ttu-id="4d0eb-171">開始字緣比對。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-171">Begin the match at a word boundary.</span></span>|  
|`\d+`|<span data-ttu-id="4d0eb-172">比對一個或多個十進位數字。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-172">Match one or more decimal digits.</span></span>|  
|`\.`|<span data-ttu-id="4d0eb-173">比對句點。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-173">Match a period.</span></span>|  
|`\d{2}`|<span data-ttu-id="4d0eb-174">比對兩個十進位數字。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-174">Match two decimal digits.</span></span>|  
|`\b`|<span data-ttu-id="4d0eb-175">結束字緣比對。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-175">End the match at a word boundary.</span></span>|  
  
 <span data-ttu-id="4d0eb-176">取代模式 `$$$&` 的解譯方式如下表所示。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-176">The replacement pattern `$$$&` is interpreted as shown in the following table.</span></span>  
  
|<span data-ttu-id="4d0eb-177">模式</span><span class="sxs-lookup"><span data-stu-id="4d0eb-177">Pattern</span></span>|<span data-ttu-id="4d0eb-178">取代字串</span><span class="sxs-lookup"><span data-stu-id="4d0eb-178">Replacement string</span></span>|  
|-------------|------------------------|  
|`$$`|<span data-ttu-id="4d0eb-179">貨幣符號 ($) 字元。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-179">The dollar sign ($) character.</span></span>|  
|`$&`|<span data-ttu-id="4d0eb-180">整個相符子字串。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-180">The entire matched substring.</span></span>|  
  
### <a name="splitting-a-single-string-into-an-array-of-strings"></a><span data-ttu-id="4d0eb-181">將單一字串分割成字串陣列</span><span class="sxs-lookup"><span data-stu-id="4d0eb-181">Splitting a Single String into an Array of Strings</span></span>  

 <span data-ttu-id="4d0eb-182"><xref:System.Text.RegularExpressions.Regex.Split%2A?displayProperty=nameWithType> 方法會在規則運算式比對所定義的位置分割輸入字串。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-182">The <xref:System.Text.RegularExpressions.Regex.Split%2A?displayProperty=nameWithType> method splits the input string at the positions defined by a regular expression match.</span></span> <span data-ttu-id="4d0eb-183">例如，下列程式碼會將編號清單中的項目放在字串陣列中。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-183">For example, the following code places the items in a numbered list into a string array.</span></span>  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/split1.cs#5)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/split1.vb#5)]  
  
 <span data-ttu-id="4d0eb-184">規則運算式模式 `\b\d{1,2}\.\s` 的解譯方式如下表所示。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-184">The regular expression pattern `\b\d{1,2}\.\s` is interpreted as shown in the following table.</span></span>  
  
|<span data-ttu-id="4d0eb-185">模式</span><span class="sxs-lookup"><span data-stu-id="4d0eb-185">Pattern</span></span>|<span data-ttu-id="4d0eb-186">描述</span><span class="sxs-lookup"><span data-stu-id="4d0eb-186">Description</span></span>|  
|-------------|-----------------|  
|`\b`|<span data-ttu-id="4d0eb-187">開始字緣比對。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-187">Begin the match at a word boundary.</span></span>|  
|`\d{1,2}`|<span data-ttu-id="4d0eb-188">比對一個或兩個十進位數字。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-188">Match one or two decimal digits.</span></span>|  
|`\.`|<span data-ttu-id="4d0eb-189">比對句點。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-189">Match a period.</span></span>|  
|`\s`|<span data-ttu-id="4d0eb-190">比對空白字元。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-190">Match a white-space character.</span></span>|  
  
<a name="Match_and_MCollection"></a>

## <a name="the-matchcollection-and-match-objects"></a><span data-ttu-id="4d0eb-191">MatchCollection 和 Match 物件</span><span class="sxs-lookup"><span data-stu-id="4d0eb-191">The MatchCollection and Match Objects</span></span>  

 <span data-ttu-id="4d0eb-192">Regex 方法會傳回兩個屬於規則運算式物件模型的物件：<xref:System.Text.RegularExpressions.MatchCollection> 物件和 <xref:System.Text.RegularExpressions.Match> 物件。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-192">Regex methods return two objects that are part of the regular expression object model: the <xref:System.Text.RegularExpressions.MatchCollection> object, and the <xref:System.Text.RegularExpressions.Match> object.</span></span>  
  
<a name="the_match_collection"></a>

### <a name="the-match-collection"></a><span data-ttu-id="4d0eb-193">比對集合</span><span class="sxs-lookup"><span data-stu-id="4d0eb-193">The Match Collection</span></span>  

 <span data-ttu-id="4d0eb-194"><xref:System.Text.RegularExpressions.Regex.Matches%2A?displayProperty=nameWithType> 方法會傳回 <xref:System.Text.RegularExpressions.MatchCollection> 物件，其中包含 <xref:System.Text.RegularExpressions.Match> 物件，這些物件代表規則運算式引擎找到的所有相符項目，並按照其於輸入字串中出現的順序排列。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-194">The <xref:System.Text.RegularExpressions.Regex.Matches%2A?displayProperty=nameWithType> method returns a <xref:System.Text.RegularExpressions.MatchCollection> object that contains <xref:System.Text.RegularExpressions.Match> objects that represent all the matches that the regular expression engine found, in the order in which they occur in the input string.</span></span> <span data-ttu-id="4d0eb-195">如果沒有相符項目，該方法會傳回 <xref:System.Text.RegularExpressions.MatchCollection> 物件，但不含成員。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-195">If there are no matches, the method returns a <xref:System.Text.RegularExpressions.MatchCollection> object with no members.</span></span> <span data-ttu-id="4d0eb-196"><xref:System.Text.RegularExpressions.MatchCollection.Item%2A?displayProperty=nameWithType> 屬性可讓您依索引存取集合的個別成員，從零到 <xref:System.Text.RegularExpressions.MatchCollection.Count%2A?displayProperty=nameWithType> 屬性的值減一。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-196">The <xref:System.Text.RegularExpressions.MatchCollection.Item%2A?displayProperty=nameWithType> property lets you access individual members of the collection by index, from zero to one less than the value of the <xref:System.Text.RegularExpressions.MatchCollection.Count%2A?displayProperty=nameWithType> property.</span></span> <span data-ttu-id="4d0eb-197"><xref:System.Text.RegularExpressions.MatchCollection.Item%2A> 是集合的索引子 (在 C# 中) 和預設屬性 (在 Visual Basic 中)。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-197"><xref:System.Text.RegularExpressions.MatchCollection.Item%2A> is the collection's indexer (in C#) and default property (in Visual Basic).</span></span>  
  
 <span data-ttu-id="4d0eb-198">依預設，呼叫 <xref:System.Text.RegularExpressions.Regex.Matches%2A?displayProperty=nameWithType> 方法時會使用延遲評估來填入 <xref:System.Text.RegularExpressions.MatchCollection> 物件。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-198">By default, the call to the <xref:System.Text.RegularExpressions.Regex.Matches%2A?displayProperty=nameWithType> method uses lazy evaluation to populate the <xref:System.Text.RegularExpressions.MatchCollection> object.</span></span> <span data-ttu-id="4d0eb-199">若要存取需要完整填入集合的屬性，例如 <xref:System.Text.RegularExpressions.MatchCollection.Count%2A?displayProperty=nameWithType> 和 <xref:System.Text.RegularExpressions.MatchCollection.Item%2A?displayProperty=nameWithType> 屬性，可能會導致效能傷害。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-199">Access to properties that require a fully populated collection, such as the <xref:System.Text.RegularExpressions.MatchCollection.Count%2A?displayProperty=nameWithType> and <xref:System.Text.RegularExpressions.MatchCollection.Item%2A?displayProperty=nameWithType> properties, may involve a performance penalty.</span></span> <span data-ttu-id="4d0eb-200">因此，建議您使用 <xref:System.Collections.IEnumerator> 方法傳回的 <xref:System.Text.RegularExpressions.MatchCollection.GetEnumerator%2A?displayProperty=nameWithType> 物件來存取集合。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-200">As a result, we recommend that you access the collection by using the <xref:System.Collections.IEnumerator> object that is returned by the <xref:System.Text.RegularExpressions.MatchCollection.GetEnumerator%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="4d0eb-201">個別語言會提供包裝集合之 <xref:System.Collections.IEnumerator> 介面的建構 (例如 Visual Basic 中的 `For Each`，以及 C# 中的 `foreach`)。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-201">Individual languages provide constructs, such as `For Each` in Visual Basic and `foreach` in C#, that wrap the collection's <xref:System.Collections.IEnumerator> interface.</span></span>  
  
 <span data-ttu-id="4d0eb-202">下列範例使用 <xref:System.Text.RegularExpressions.Regex.Matches%28System.String%29?displayProperty=nameWithType> 方法，以在輸入字串中找到的所有相符項目來填入 <xref:System.Text.RegularExpressions.MatchCollection> 物件。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-202">The following example uses the <xref:System.Text.RegularExpressions.Regex.Matches%28System.String%29?displayProperty=nameWithType> method to populate a <xref:System.Text.RegularExpressions.MatchCollection> object with all the matches found in an input string.</span></span> <span data-ttu-id="4d0eb-203">此範例會列舉集合、將相符項目複製到字串陣列，並記錄整數陣列中的字元位置。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-203">The example enumerates the collection, copies the matches to a string array, and records the character positions in an integer array.</span></span>  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/matchcollection1.cs#6)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/matchcollection1.vb#6)]  
  
<a name="the_match"></a>

### <a name="the-match"></a><span data-ttu-id="4d0eb-204">比對</span><span class="sxs-lookup"><span data-stu-id="4d0eb-204">The Match</span></span>  

 <span data-ttu-id="4d0eb-205"><xref:System.Text.RegularExpressions.Match> 類別代表單一規則運算式比對的結果。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-205">The <xref:System.Text.RegularExpressions.Match> class represents the result of a single regular expression match.</span></span> <span data-ttu-id="4d0eb-206">您可以用兩個方式來存取 <xref:System.Text.RegularExpressions.Match> 物件：</span><span class="sxs-lookup"><span data-stu-id="4d0eb-206">You can access <xref:System.Text.RegularExpressions.Match> objects in two ways:</span></span>  
  
- <span data-ttu-id="4d0eb-207">從 <xref:System.Text.RegularExpressions.MatchCollection> 方法傳回的 <xref:System.Text.RegularExpressions.Regex.Matches%2A?displayProperty=nameWithType> 物件中擷取。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-207">By retrieving them from the <xref:System.Text.RegularExpressions.MatchCollection> object that is returned by the <xref:System.Text.RegularExpressions.Regex.Matches%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="4d0eb-208">若要擷取個別 <xref:System.Text.RegularExpressions.Match> 物件，請使用 `foreach` (在 C# 中) 或 `For Each`...`Next` (在 Visual Basic 中) 的建構來逐一查看集合，或是使用 <xref:System.Text.RegularExpressions.MatchCollection.Item%2A?displayProperty=nameWithType> 屬性來依據索引或名稱擷取特定的 <xref:System.Text.RegularExpressions.Match> 物件。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-208">To retrieve individual <xref:System.Text.RegularExpressions.Match> objects, iterate the collection by using a `foreach` (in C#) or `For Each`...`Next` (in Visual Basic) construct, or use the <xref:System.Text.RegularExpressions.MatchCollection.Item%2A?displayProperty=nameWithType> property to retrieve a specific <xref:System.Text.RegularExpressions.Match> object either by index or by name.</span></span> <span data-ttu-id="4d0eb-209">您也可以依索引 (從零到集合中的物件數減一) 從集合擷取個別 <xref:System.Text.RegularExpressions.Match> 物件。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-209">You can also retrieve individual <xref:System.Text.RegularExpressions.Match> objects from the collection by iterating the collection by index, from zero to one less that the number of objects in the collection.</span></span> <span data-ttu-id="4d0eb-210">不過，此方法不會利用延遲評估，因為它會存取 <xref:System.Text.RegularExpressions.MatchCollection.Count%2A?displayProperty=nameWithType> 屬性。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-210">However, this method does not take advantage of lazy evaluation, because it accesses the <xref:System.Text.RegularExpressions.MatchCollection.Count%2A?displayProperty=nameWithType> property.</span></span>  
  
     <span data-ttu-id="4d0eb-211">下列範例會使用 <xref:System.Text.RegularExpressions.Match> 或 <xref:System.Text.RegularExpressions.MatchCollection>...`foreach` 建構逐一查看集合，以從 `For Each` 物件擷取個別 `Next` 物件。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-211">The following example retrieves individual <xref:System.Text.RegularExpressions.Match> objects from a <xref:System.Text.RegularExpressions.MatchCollection> object by iterating the collection using the `foreach` or `For Each`...`Next` construct.</span></span> <span data-ttu-id="4d0eb-212">規則運算式會單純比對輸入字串中的字串 "abc"。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-212">The regular expression simply matches the string "abc" in the input string.</span></span>  
  
     [!code-csharp[Conceptual.RegularExpressions.ObjectModel#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/match2.cs#7)]
     [!code-vb[Conceptual.RegularExpressions.ObjectModel#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/match2.vb#7)]  
  
- <span data-ttu-id="4d0eb-213">呼叫 <xref:System.Text.RegularExpressions.Regex.Match%2A?displayProperty=nameWithType> 方法，它會傳回代表字串中第一個相符項目或字串一部分的 <xref:System.Text.RegularExpressions.Match> 物件。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-213">By calling the <xref:System.Text.RegularExpressions.Regex.Match%2A?displayProperty=nameWithType> method, which returns a <xref:System.Text.RegularExpressions.Match> object that represents the first match in a string or a portion of a string.</span></span> <span data-ttu-id="4d0eb-214">您可以擷取 `Match.Success` 屬性的值，以判斷是否找到相符項目。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-214">You can determine whether the match has been found by retrieving the value of the `Match.Success` property.</span></span> <span data-ttu-id="4d0eb-215">若要擷取代表後續相符項目的 <xref:System.Text.RegularExpressions.Match> 物件，請重複呼叫 <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=nameWithType> 方法，直到傳回之 `Success` 物件的 <xref:System.Text.RegularExpressions.Match> 屬性為 `false`。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-215">To retrieve <xref:System.Text.RegularExpressions.Match> objects that represent subsequent matches, call the <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=nameWithType> method repeatedly, until the `Success` property of the returned <xref:System.Text.RegularExpressions.Match> object is `false`.</span></span>  
  
     <span data-ttu-id="4d0eb-216">下列範例使用 <xref:System.Text.RegularExpressions.Regex.Match%28System.String%2CSystem.String%29?displayProperty=nameWithType> 和 <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=nameWithType> 方法來比對輸入字串中的字串 "abc"。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-216">The following example uses the <xref:System.Text.RegularExpressions.Regex.Match%28System.String%2CSystem.String%29?displayProperty=nameWithType> and <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=nameWithType> methods to match the string "abc" in the input string.</span></span>  
  
     [!code-csharp[Conceptual.RegularExpressions.ObjectModel#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/match3.cs#8)]
     [!code-vb[Conceptual.RegularExpressions.ObjectModel#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/match3.vb#8)]  
  
 <span data-ttu-id="4d0eb-217"><xref:System.Text.RegularExpressions.Match> 類別的兩個屬性會傳回集合物件：</span><span class="sxs-lookup"><span data-stu-id="4d0eb-217">Two properties of the <xref:System.Text.RegularExpressions.Match> class return collection objects:</span></span>  
  
- <span data-ttu-id="4d0eb-218"><xref:System.Text.RegularExpressions.Match.Groups%2A?displayProperty=nameWithType> 屬性會傳回 <xref:System.Text.RegularExpressions.GroupCollection> 物件，其中包含符合規則運算式模式中之擷取群組的子字串相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-218">The <xref:System.Text.RegularExpressions.Match.Groups%2A?displayProperty=nameWithType> property returns a <xref:System.Text.RegularExpressions.GroupCollection> object that contains information about the substrings that match capturing groups in the regular expression pattern.</span></span>  
  
- <span data-ttu-id="4d0eb-219">`Match.Captures` 屬性會傳回用法受限的 <xref:System.Text.RegularExpressions.CaptureCollection> 物件。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-219">The `Match.Captures` property returns a <xref:System.Text.RegularExpressions.CaptureCollection> object that is of limited use.</span></span> <span data-ttu-id="4d0eb-220">針對 <xref:System.Text.RegularExpressions.Match> 屬性為 `Success` 的 `false` 物件，不會填入集合。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-220">The collection is not populated for a <xref:System.Text.RegularExpressions.Match> object whose `Success` property is `false`.</span></span> <span data-ttu-id="4d0eb-221">否則，就會包含具有與 <xref:System.Text.RegularExpressions.Capture> 物件相同資訊的單一 <xref:System.Text.RegularExpressions.Match> 物件。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-221">Otherwise, it contains a single <xref:System.Text.RegularExpressions.Capture> object that has the same information as the <xref:System.Text.RegularExpressions.Match> object.</span></span>  
  
 <span data-ttu-id="4d0eb-222">如需這些物件的詳細資訊，請參閱本主題稍後的[群組集合](#GroupCollection)及[擷取集合](#CaptureCollection)兩節。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-222">For more information about these objects, see [The Group Collection](#GroupCollection) and [The Capture Collection](#CaptureCollection) sections later in this topic.</span></span>  
  
 <span data-ttu-id="4d0eb-223"><xref:System.Text.RegularExpressions.Match> 類別的兩個其他屬性會提供比對的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-223">Two additional properties of the <xref:System.Text.RegularExpressions.Match> class provide information about the match.</span></span> <span data-ttu-id="4d0eb-224">`Match.Value` 屬性會傳回輸入字串中，符合規則運算式模式的子字串。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-224">The `Match.Value` property returns the substring in the input string that matches the regular expression pattern.</span></span> <span data-ttu-id="4d0eb-225">`Match.Index` 屬性會傳回輸入字串中相符字串以零起始的開始位置。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-225">The `Match.Index` property returns the zero-based starting position of the matched string in the input string.</span></span>  
  
 <span data-ttu-id="4d0eb-226"><xref:System.Text.RegularExpressions.Match> 類別也有兩個模式比對方法：</span><span class="sxs-lookup"><span data-stu-id="4d0eb-226">The <xref:System.Text.RegularExpressions.Match> class also has two pattern-matching methods:</span></span>  
  
- <span data-ttu-id="4d0eb-227"><xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=nameWithType> 方法會尋找目前 <xref:System.Text.RegularExpressions.Match> 物件代表之相符項目後面的相符項目，並傳回代表該相符項目的 <xref:System.Text.RegularExpressions.Match> 物件。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-227">The <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=nameWithType> method finds the match after the match represented by the current <xref:System.Text.RegularExpressions.Match> object, and returns a <xref:System.Text.RegularExpressions.Match> object that represents that match.</span></span>  
  
- <span data-ttu-id="4d0eb-228"><xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=nameWithType> 方法會在相符字串上執行指定的取代作業，並傳回結果。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-228">The <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=nameWithType> method performs a specified replacement operation on the matched string and returns the result.</span></span>  
  
 <span data-ttu-id="4d0eb-229">下列範例會使用 <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=nameWithType> 方法，在包含兩個小數位數的每個數字前面，加上 $ 符號和空格。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-229">The following example uses the <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=nameWithType> method to prepend a $ symbol and a space before every number that includes two fractional digits.</span></span>  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/result1.cs#9)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/result1.vb#9)]  
  
 <span data-ttu-id="4d0eb-230">規則運算式模式 `\b\d+(,\d{3})*\.\d{2}\b` 的定義如下表所示。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-230">The regular expression pattern `\b\d+(,\d{3})*\.\d{2}\b` is defined as shown in the following table.</span></span>  
  
|<span data-ttu-id="4d0eb-231">模式</span><span class="sxs-lookup"><span data-stu-id="4d0eb-231">Pattern</span></span>|<span data-ttu-id="4d0eb-232">描述</span><span class="sxs-lookup"><span data-stu-id="4d0eb-232">Description</span></span>|  
|-------------|-----------------|  
|`\b`|<span data-ttu-id="4d0eb-233">開始字緣比對。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-233">Begin the match at a word boundary.</span></span>|  
|`\d+`|<span data-ttu-id="4d0eb-234">比對一個或多個十進位數字。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-234">Match one or more decimal digits.</span></span>|  
|`(,\d{3})*`|<span data-ttu-id="4d0eb-235">比對後面接三個十進位數字的零或多個逗號。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-235">Match zero or more occurrences of a comma followed by three decimal digits.</span></span>|  
|`\.`|<span data-ttu-id="4d0eb-236">比對小數點字元。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-236">Match the decimal point character.</span></span>|  
|`\d{2}`|<span data-ttu-id="4d0eb-237">比對兩個十進位數字。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-237">Match two decimal digits.</span></span>|  
|`\b`|<span data-ttu-id="4d0eb-238">結束字緣比對。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-238">End the match at a word boundary.</span></span>|  
  
 <span data-ttu-id="4d0eb-239">取代模式 `$$ $&` 指出相符的子字串應取代為貨幣符號 ($) (`$$` 模式)、空格和相符項的值 (`$&` 模式)。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-239">The replacement pattern `$$ $&` indicates that the matched substring should be replaced by a dollar sign ($) symbol (the `$$` pattern), a space, and the value of the match (the `$&` pattern).</span></span>  
  
 [<span data-ttu-id="4d0eb-240">回到頁首</span><span class="sxs-lookup"><span data-stu-id="4d0eb-240">Back to top</span></span>](#introduction)  
  
<a name="GroupCollection"></a>

## <a name="the-group-collection"></a><span data-ttu-id="4d0eb-241">群組集合</span><span class="sxs-lookup"><span data-stu-id="4d0eb-241">The Group Collection</span></span>  

 <span data-ttu-id="4d0eb-242"><xref:System.Text.RegularExpressions.Match.Groups%2A?displayProperty=nameWithType> 屬性會傳回 <xref:System.Text.RegularExpressions.GroupCollection> 物件，其中包含單一比對中代表擷取群組的 <xref:System.Text.RegularExpressions.Group> 物件。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-242">The <xref:System.Text.RegularExpressions.Match.Groups%2A?displayProperty=nameWithType> property returns a <xref:System.Text.RegularExpressions.GroupCollection> object that contains <xref:System.Text.RegularExpressions.Group> objects that represent captured groups in a single match.</span></span> <span data-ttu-id="4d0eb-243">集合中的第一個 <xref:System.Text.RegularExpressions.Group> 物件 (索引位置為 0) 代表整個比對。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-243">The first <xref:System.Text.RegularExpressions.Group> object in the collection (at index 0) represents the entire match.</span></span> <span data-ttu-id="4d0eb-244">後面接續的每個物件各代表單一擷取群組的結果。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-244">Each object that follows represents the results of a single capturing group.</span></span>  
  
 <span data-ttu-id="4d0eb-245">您可以使用 <xref:System.Text.RegularExpressions.Group> 屬性，擷取集合中的個別 <xref:System.Text.RegularExpressions.GroupCollection.Item%2A?displayProperty=nameWithType> 物件。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-245">You can retrieve individual <xref:System.Text.RegularExpressions.Group> objects in the collection by using the <xref:System.Text.RegularExpressions.GroupCollection.Item%2A?displayProperty=nameWithType> property.</span></span> <span data-ttu-id="4d0eb-246">您可以依集合中的序數位置來擷取未具名群組，以及依名稱或依序數位置來擷取具名群組。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-246">You can retrieve unnamed groups by their ordinal position in the collection, and retrieve named groups either by name or by ordinal position.</span></span> <span data-ttu-id="4d0eb-247">未具名擷取會先出現在集合中，並依其出現在規則運算式模式中的順序，由左至右編排索引。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-247">Unnamed captures appear first in the collection, and are indexed from left to right in the order in which they appear in the regular expression pattern.</span></span> <span data-ttu-id="4d0eb-248">具名擷取的索引會依其出現在規則運算式模式中的順序，由左至右編排在未具名擷取之後。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-248">Named captures are indexed after unnamed captures, from left to right in the order in which they appear in the regular expression pattern.</span></span> <span data-ttu-id="4d0eb-249">若要判定特定規則運算式比對方法傳回的集合中，有哪些編號群組可用，您可以呼叫執行個體 <xref:System.Text.RegularExpressions.Regex.GetGroupNumbers%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-249">To determine what numbered groups are available in the collection returned for a particular regular expression matching method, you can call the instance <xref:System.Text.RegularExpressions.Regex.GetGroupNumbers%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="4d0eb-250">若要判定集合中有哪些具名群組可用，您可以呼叫執行個體 <xref:System.Text.RegularExpressions.Regex.GetGroupNames%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-250">To determine what named groups are available in the collection, you can call the instance <xref:System.Text.RegularExpressions.Regex.GetGroupNames%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="4d0eb-251">在用來分析任何規則運算式找到之相符項目的一般用途常式中，這兩種方法都特別好用。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-251">Both methods are particularly useful in general-purpose routines that analyze the matches found by any regular expression.</span></span>  
  
 <span data-ttu-id="4d0eb-252"><xref:System.Text.RegularExpressions.GroupCollection.Item%2A?displayProperty=nameWithType> 屬性在 C# 是集合的索引子，在 Visual Basic 中是集合物件的預設屬性。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-252">The <xref:System.Text.RegularExpressions.GroupCollection.Item%2A?displayProperty=nameWithType> property is the indexer of the collection in C# and the collection object's default property in Visual Basic.</span></span> <span data-ttu-id="4d0eb-253">這表示，可以依索引 (若為具名群組，可依名稱) 來存取個別 <xref:System.Text.RegularExpressions.Group> 物件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4d0eb-253">This means that individual <xref:System.Text.RegularExpressions.Group> objects can be accessed by index (or by name, in the case of named groups) as follows:</span></span>  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#13](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/groupsyntax1.cs#13)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/groupsyntax1.vb#13)]  
  
 <span data-ttu-id="4d0eb-254">下列範例定義的規則運算式會使用群組建構來擷取日期的月、日和年。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-254">The following example defines a regular expression that uses grouping constructs to capture the month, day, and year of a date.</span></span>  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/groupcollection1.cs#10)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/groupcollection1.vb#10)]  
  
 <span data-ttu-id="4d0eb-255">規則運算式模式 `\b(\w+)\s(\d{1,2}),\s(\d{4})\b` 的定義如下表所示。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-255">The regular expression pattern `\b(\w+)\s(\d{1,2}),\s(\d{4})\b` is defined as shown in the following table.</span></span>  
  
|<span data-ttu-id="4d0eb-256">模式</span><span class="sxs-lookup"><span data-stu-id="4d0eb-256">Pattern</span></span>|<span data-ttu-id="4d0eb-257">描述</span><span class="sxs-lookup"><span data-stu-id="4d0eb-257">Description</span></span>|  
|-------------|-----------------|  
|`\b`|<span data-ttu-id="4d0eb-258">開始字緣比對。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-258">Begin the match at a word boundary.</span></span>|  
|`(\w+)`|<span data-ttu-id="4d0eb-259">比對一個或多個文字字元。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-259">Match one or more word characters.</span></span> <span data-ttu-id="4d0eb-260">這是第一個擷取群組。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-260">This is the first capturing group.</span></span>|  
|`\s`|<span data-ttu-id="4d0eb-261">比對空白字元。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-261">Match a white-space character.</span></span>|  
|`(\d{1,2})`|<span data-ttu-id="4d0eb-262">比對一個或兩個十進位數字。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-262">Match one or two decimal digits.</span></span> <span data-ttu-id="4d0eb-263">這是第二個擷取群組。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-263">This is the second capturing group.</span></span>|  
|`,`|<span data-ttu-id="4d0eb-264">比對逗號。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-264">Match a comma.</span></span>|  
|`\s`|<span data-ttu-id="4d0eb-265">比對空白字元。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-265">Match a white-space character.</span></span>|  
|`(\d{4})`|<span data-ttu-id="4d0eb-266">比對四個十進位數字。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-266">Match four decimal digits.</span></span> <span data-ttu-id="4d0eb-267">這是第三個擷取群組。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-267">This is the third capturing group.</span></span>|  
|`\b`|<span data-ttu-id="4d0eb-268">結束字邊界比對。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-268">End the match on a word boundary.</span></span>|  
  
 [<span data-ttu-id="4d0eb-269">回到頁首</span><span class="sxs-lookup"><span data-stu-id="4d0eb-269">Back to top</span></span>](#introduction)  
  
<a name="the_captured_group"></a>

## <a name="the-captured-group"></a><span data-ttu-id="4d0eb-270">擷取群組</span><span class="sxs-lookup"><span data-stu-id="4d0eb-270">The Captured Group</span></span>  

 <span data-ttu-id="4d0eb-271"><xref:System.Text.RegularExpressions.Group> 類別代表單一擷取群組的結果。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-271">The <xref:System.Text.RegularExpressions.Group> class represents the result from a single capturing group.</span></span> <span data-ttu-id="4d0eb-272"><xref:System.Text.RegularExpressions.GroupCollection.Item%2A> 屬性傳回之 <xref:System.Text.RegularExpressions.GroupCollection> 物件的 <xref:System.Text.RegularExpressions.Match.Groups%2A?displayProperty=nameWithType> 屬性，會傳回代表規則運算式中定義之擷取群組的群組物件。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-272">Group objects that represent the capturing groups defined in a regular expression are returned by the <xref:System.Text.RegularExpressions.GroupCollection.Item%2A> property of the <xref:System.Text.RegularExpressions.GroupCollection> object returned by the <xref:System.Text.RegularExpressions.Match.Groups%2A?displayProperty=nameWithType> property.</span></span> <span data-ttu-id="4d0eb-273"><xref:System.Text.RegularExpressions.GroupCollection.Item%2A> 屬性是 <xref:System.Text.RegularExpressions.Group> 類別的索引子 (在 C# 中) 及預設屬性 (在 Visual Basic 中)。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-273">The <xref:System.Text.RegularExpressions.GroupCollection.Item%2A> property is the indexer (in C#) and the default property (in Visual Basic) of the <xref:System.Text.RegularExpressions.Group> class.</span></span> <span data-ttu-id="4d0eb-274">您也可以使用 `foreach` 或 `For Each` 建構，逐一查看集合來擷取個別成員。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-274">You can also retrieve individual members by iterating the collection using the `foreach` or `For Each` construct.</span></span> <span data-ttu-id="4d0eb-275">如需範例，請參閱上一節。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-275">For an example, see the previous section.</span></span>  
  
 <span data-ttu-id="4d0eb-276">下列範例會使用巢狀群組建構，將子字串擷取至群組中。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-276">The following example uses nested grouping constructs to capture substrings into groups.</span></span> <span data-ttu-id="4d0eb-277">規則運算式模式 `(a(b))c` 會相符字串 "abc"。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-277">The regular expression pattern `(a(b))c` matches the string "abc".</span></span> <span data-ttu-id="4d0eb-278">它會將子字串 "ab" 指派給第一個擷取群組，並將子字串 "b" 指派給第二個擷取群組。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-278">It assigns the substring "ab" to the first capturing group, and the substring "b" to the second capturing group.</span></span>  
  
 [!code-csharp[RegularExpressions.Classes#6](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Classes/cs/Example.cs#6)]
 [!code-vb[RegularExpressions.Classes#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Classes/vb/Example.vb#6)]  
  
 <span data-ttu-id="4d0eb-279">下列範例會使用具名群組建構，從包含 "DATANAME:VALUE" 格式 (規則運算式會在冒號 (:) 處分割) 資料的字串擷取子字串。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-279">The following example uses named grouping constructs to capture substrings from a string that contains data in the format "DATANAME:VALUE", which the regular expression splits at the colon (:).</span></span>  
  
 [!code-csharp[RegularExpressions.Classes#8](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Classes/cs/Example.cs#8)]
 [!code-vb[RegularExpressions.Classes#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Classes/vb/Example.vb#8)]  
  
 <span data-ttu-id="4d0eb-280">規則運算式模式 `^(?<name>\w+):(?<value>\w+)` 的定義如下表所示。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-280">The regular expression pattern `^(?<name>\w+):(?<value>\w+)` is defined as shown in the following table.</span></span>  
  
|<span data-ttu-id="4d0eb-281">模式</span><span class="sxs-lookup"><span data-stu-id="4d0eb-281">Pattern</span></span>|<span data-ttu-id="4d0eb-282">描述</span><span class="sxs-lookup"><span data-stu-id="4d0eb-282">Description</span></span>|  
|-------------|-----------------|  
|`^`|<span data-ttu-id="4d0eb-283">在輸入字串的開頭開始比對。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-283">Begin the match at the beginning of the input string.</span></span>|  
|`(?<name>\w+)`|<span data-ttu-id="4d0eb-284">比對一個或多個文字字元。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-284">Match one or more word characters.</span></span> <span data-ttu-id="4d0eb-285">此擷取群組的名稱為 `name`。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-285">The name of this capturing group is `name`.</span></span>|  
|`:`|<span data-ttu-id="4d0eb-286">比對冒號。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-286">Match a colon.</span></span>|  
|`(?<value>\w+)`|<span data-ttu-id="4d0eb-287">比對一個或多個文字字元。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-287">Match one or more word characters.</span></span> <span data-ttu-id="4d0eb-288">此擷取群組的名稱為 `value`。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-288">The name of this capturing group is `value`.</span></span>|  
  
 <span data-ttu-id="4d0eb-289"><xref:System.Text.RegularExpressions.Group> 類別的屬性會提供擷取群組的相關資訊：`Group.Value` 屬性包含擷取的子字串，`Group.Index` 屬性會指出擷取群組在輸入文字中的開始位置，`Group.Length` 屬性包含擷取文字的長度，而 `Group.Success` 屬性會指出子字串是否符合擷取群組所定義的模式。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-289">The properties of the <xref:System.Text.RegularExpressions.Group> class provide information about the captured group: The `Group.Value` property contains the captured substring, the `Group.Index` property indicates the starting position of the captured group in the input text, the `Group.Length` property contains the length of the captured text, and the `Group.Success` property indicates whether a substring matched the pattern defined by the capturing group.</span></span>  
  
 <span data-ttu-id="4d0eb-290">將數量詞套用至群組 (如需詳細資訊，請參閱[數量詞](quantifiers-in-regular-expressions.md)) 會以兩種方式來修改每個擷取群組各一個擷取的關聯性：</span><span class="sxs-lookup"><span data-stu-id="4d0eb-290">Applying quantifiers to a group (for more information, see [Quantifiers](quantifiers-in-regular-expressions.md)) modifies the relationship of one capture per capturing group in two ways:</span></span>  
  
- <span data-ttu-id="4d0eb-291">如果將 `*` 或 `*?` 數量詞 (可指定零或多個相符項目) 套用至群組，擷取群組在輸入字串中可會沒有相符項目。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-291">If the `*` or `*?` quantifier (which specifies zero or more matches) is applied to a group, a capturing group may not have a match in the input string.</span></span> <span data-ttu-id="4d0eb-292">沒有擷取文字時，<xref:System.Text.RegularExpressions.Group> 物件的屬性會設定如下表所示。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-292">When there is no captured text, the properties of the <xref:System.Text.RegularExpressions.Group> object are set as shown in the following table.</span></span>  
  
    |<span data-ttu-id="4d0eb-293">群組屬性</span><span class="sxs-lookup"><span data-stu-id="4d0eb-293">Group property</span></span>|<span data-ttu-id="4d0eb-294">值</span><span class="sxs-lookup"><span data-stu-id="4d0eb-294">Value</span></span>|  
    |--------------------|-----------|  
    |`Success`|`false`|  
    |`Value`|<xref:System.String.Empty?displayProperty=nameWithType>|  
    |`Length`|<span data-ttu-id="4d0eb-295">0</span><span class="sxs-lookup"><span data-stu-id="4d0eb-295">0</span></span>|  
  
     <span data-ttu-id="4d0eb-296">下列範例提供說明。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-296">The following example provides an illustration.</span></span> <span data-ttu-id="4d0eb-297">在規則運算式模式 `aaa(bbb)*ccc` 中，第一個擷取群組 (子字串 "bbb") 可比對零或多次。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-297">In the regular expression pattern `aaa(bbb)*ccc`, the first capturing group (the substring "bbb") can be matched zero or more times.</span></span> <span data-ttu-id="4d0eb-298">因為輸入字串 "aaaccc" 符合模式，所以擷取群組沒有相符項目。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-298">Because the input string "aaaccc" matches the pattern, the capturing group does not have a match.</span></span>  
  
     [!code-csharp[Conceptual.RegularExpressions.ObjectModel#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/nocapture1.cs#11)]
     [!code-vb[Conceptual.RegularExpressions.ObjectModel#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/nocapture1.vb#11)]  
  
- <span data-ttu-id="4d0eb-299">數量詞可以比對多次出現的擷取群組定義的模式。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-299">Quantifiers can match multiple occurrences of a pattern that is defined by a capturing group.</span></span> <span data-ttu-id="4d0eb-300">在此情況下，`Value` 物件的 `Length` 和 <xref:System.Text.RegularExpressions.Group> 屬性只包含最後擷取之子字串的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-300">In this case, the `Value` and `Length` properties of a <xref:System.Text.RegularExpressions.Group> object contain information only about the last captured substring.</span></span> <span data-ttu-id="4d0eb-301">例如，下列規則運算式會比對以句點結尾的單一句子。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-301">For example, the following regular expression matches a single sentence that ends in a period.</span></span> <span data-ttu-id="4d0eb-302">其使用兩個群組建構：第一個群組建構會擷取個別文字和空格字元，第二個群組建構會擷取個別文字。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-302">It uses two grouping constructs: The first captures individual words along with a white-space character; the second captures individual words.</span></span> <span data-ttu-id="4d0eb-303">如範例輸出所示，雖然規則運算式成功擷取了整個句子，但是第二個擷取群組只擷取了最後一個字。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-303">As the output from the example shows, although the regular expression succeeds in capturing an entire sentence, the second capturing group captures only the last word.</span></span>  
  
     [!code-csharp[Conceptual.RegularExpressions.ObjectModel#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/lastcapture1.cs#12)]
     [!code-vb[Conceptual.RegularExpressions.ObjectModel#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/lastcapture1.vb#12)]  
  
 [<span data-ttu-id="4d0eb-304">回到頁首</span><span class="sxs-lookup"><span data-stu-id="4d0eb-304">Back to top</span></span>](#introduction)  
  
<a name="CaptureCollection"></a>

## <a name="the-capture-collection"></a><span data-ttu-id="4d0eb-305">擷取集合</span><span class="sxs-lookup"><span data-stu-id="4d0eb-305">The Capture Collection</span></span>  

 <span data-ttu-id="4d0eb-306"><xref:System.Text.RegularExpressions.Group> 物件只包含最後一個擷取的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-306">The <xref:System.Text.RegularExpressions.Group> object contains information only about the last capture.</span></span> <span data-ttu-id="4d0eb-307">不過，您仍可從 <xref:System.Text.RegularExpressions.CaptureCollection> 屬性傳回的 <xref:System.Text.RegularExpressions.Group.Captures%2A?displayProperty=nameWithType> 物件，取得擷取群組所建立的一整組擷取。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-307">However, the entire set of captures made by a capturing group is still available from the <xref:System.Text.RegularExpressions.CaptureCollection> object that is returned by the <xref:System.Text.RegularExpressions.Group.Captures%2A?displayProperty=nameWithType> property.</span></span> <span data-ttu-id="4d0eb-308">集合的每個成員都是 <xref:System.Text.RegularExpressions.Capture> 物件，代表擷取群組所建立的擷取，並依照擷取的順序排列 (因此，順序為在輸入字串中比對擷取群組的順序，由左至右排列)。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-308">Each member of the collection is a <xref:System.Text.RegularExpressions.Capture> object that represents a capture made by that capturing group, in the order in which they were captured (and, therefore, in the order in which the captured strings were matched from left to right in the input string).</span></span> <span data-ttu-id="4d0eb-309">您可以從集合擷取個別 <xref:System.Text.RegularExpressions.Capture> 物件，有兩種方式：</span><span class="sxs-lookup"><span data-stu-id="4d0eb-309">You can retrieve individual <xref:System.Text.RegularExpressions.Capture> objects from the collection in either of two ways:</span></span>  
  
- <span data-ttu-id="4d0eb-310">使用 `foreach` (在 C# 中) 或 `For Each` (在 Visual Basic 中) 之類的建構逐一查看集合。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-310">By iterating through the collection using a construct such as `foreach` (in C#) or `For Each` (in Visual Basic).</span></span>  
  
- <span data-ttu-id="4d0eb-311">使用 <xref:System.Text.RegularExpressions.CaptureCollection.Item%2A?displayProperty=nameWithType> 屬性，依索引擷取特定物件。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-311">By using the <xref:System.Text.RegularExpressions.CaptureCollection.Item%2A?displayProperty=nameWithType> property to retrieve a specific object by index.</span></span> <span data-ttu-id="4d0eb-312"><xref:System.Text.RegularExpressions.CaptureCollection.Item%2A> 屬性是 <xref:System.Text.RegularExpressions.CaptureCollection> 物件的預設屬性 (在 Visual Basic 中) 或索引子 (在 C# 中)。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-312">The <xref:System.Text.RegularExpressions.CaptureCollection.Item%2A> property is the <xref:System.Text.RegularExpressions.CaptureCollection> object's default property (in Visual Basic) or indexer (in C#).</span></span>  
  
 <span data-ttu-id="4d0eb-313">如果沒有將數量詞套用至擷取群組，則 <xref:System.Text.RegularExpressions.CaptureCollection> 物件會包含單一較無用處的 <xref:System.Text.RegularExpressions.Capture> 物件，因為其提供與其 <xref:System.Text.RegularExpressions.Group> 物件相同之相符項目的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-313">If a quantifier is not applied to a capturing group, the <xref:System.Text.RegularExpressions.CaptureCollection> object contains a single <xref:System.Text.RegularExpressions.Capture> object that is of little interest, because it provides information about the same match as its <xref:System.Text.RegularExpressions.Group> object.</span></span> <span data-ttu-id="4d0eb-314">如果將數量詞套用至擷取群組，則 <xref:System.Text.RegularExpressions.CaptureCollection> 物件包含擷取群組建立的所有擷取，而集合的最後一個成員代表與 <xref:System.Text.RegularExpressions.Group> 物件相同的擷取。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-314">If a quantifier is applied to a capturing group, the <xref:System.Text.RegularExpressions.CaptureCollection> object contains all captures made by the capturing group, and the last member of the collection represents the same capture as the <xref:System.Text.RegularExpressions.Group> object.</span></span>  
  
 <span data-ttu-id="4d0eb-315">例如，如果您使用規則運算式模式 `((a(b))c)+` (其中 + 數量詞指定一或多個比對)，以從字串 "abcabcabc" 擷取相符項目，則每個 <xref:System.Text.RegularExpressions.CaptureCollection> 物件的 <xref:System.Text.RegularExpressions.Group> 物件各包含三個成員。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-315">For example, if you use the regular expression pattern `((a(b))c)+` (where the + quantifier specifies one or more matches) to capture matches from the string "abcabcabc", the <xref:System.Text.RegularExpressions.CaptureCollection> object for each <xref:System.Text.RegularExpressions.Group> object contains three members.</span></span>  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#14](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/capturecollection1.cs#14)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/capturecollection1.vb#14)]  
  
 <span data-ttu-id="4d0eb-316">下列範例使用規則運算式 `(Abc)+`，在字串 "XYZAbcAbcAbcXYZAbcAb" 中尋找一或多次連續執行的字串 "Abc"。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-316">The following example uses the regular expression `(Abc)+` to find one or more consecutive runs of the string "Abc" in the string "XYZAbcAbcAbcXYZAbcAb".</span></span> <span data-ttu-id="4d0eb-317">此範例說明如何使用 <xref:System.Text.RegularExpressions.Group.Captures%2A?displayProperty=nameWithType> 屬性來傳回多個擷取子字串群組。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-317">The example illustrates the use of the <xref:System.Text.RegularExpressions.Group.Captures%2A?displayProperty=nameWithType> property to return multiple groups of captured substrings.</span></span>  
  
 [!code-csharp[RegularExpressions.Classes#5](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Classes/cs/Example.cs#5)]
 [!code-vb[RegularExpressions.Classes#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Classes/vb/Example.vb#5)]  
  
 [<span data-ttu-id="4d0eb-318">回到頁首</span><span class="sxs-lookup"><span data-stu-id="4d0eb-318">Back to top</span></span>](#introduction)  
  
<a name="the_individual_capture"></a>

## <a name="the-individual-capture"></a><span data-ttu-id="4d0eb-319">個別擷取</span><span class="sxs-lookup"><span data-stu-id="4d0eb-319">The Individual Capture</span></span>  

 <span data-ttu-id="4d0eb-320"><xref:System.Text.RegularExpressions.Capture> 類別包含單一子運算式擷取的結果。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-320">The <xref:System.Text.RegularExpressions.Capture> class contains the results from a single subexpression capture.</span></span> <span data-ttu-id="4d0eb-321"><xref:System.Text.RegularExpressions.Capture.Value%2A?displayProperty=nameWithType> 屬性包含相符的文字，而 <xref:System.Text.RegularExpressions.Capture.Index%2A?displayProperty=nameWithType> 屬性指出輸入字串中以零起始的位置，也就是相符的子字串開始的位置。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-321">The <xref:System.Text.RegularExpressions.Capture.Value%2A?displayProperty=nameWithType> property contains the matched text, and the <xref:System.Text.RegularExpressions.Capture.Index%2A?displayProperty=nameWithType> property indicates the zero-based position in the input string at which the matched substring begins.</span></span>  
  
 <span data-ttu-id="4d0eb-322">下列範例會針對所選城市的氣溫剖析輸入字串。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-322">The following example parses an input string for the temperature of selected cities.</span></span> <span data-ttu-id="4d0eb-323">逗號 (",") 用來分隔城市及其氣溫，而分號 (";") 用來分隔每個城市的資料。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-323">A comma (",") is used to separate a city and its temperature, and a semicolon (";") is used to separate each city's data.</span></span> <span data-ttu-id="4d0eb-324">整個輸入字串代表單一比對。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-324">The entire input string represents a single match.</span></span> <span data-ttu-id="4d0eb-325">在規則運算式模式 `((\w+(\s\w+)*),(\d+);)+` (用來剖析字串) 中，城市名稱指派給第二個擷取群組，而氣溫指派給第四個擷取群組。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-325">In the regular expression pattern `((\w+(\s\w+)*),(\d+);)+`, which is used to parse the string, the city name is assigned to the second capturing group, and the temperature is assigned to the fourth capturing group.</span></span>  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#16](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/capture1.cs#16)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/capture1.vb#16)]  
  
 <span data-ttu-id="4d0eb-326">規則運算式的定義如下表所示。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-326">The regular expression is defined as shown in the following table.</span></span>  
  
|<span data-ttu-id="4d0eb-327">模式</span><span class="sxs-lookup"><span data-stu-id="4d0eb-327">Pattern</span></span>|<span data-ttu-id="4d0eb-328">描述</span><span class="sxs-lookup"><span data-stu-id="4d0eb-328">Description</span></span>|  
|-------------|-----------------|  
|`\w+`|<span data-ttu-id="4d0eb-329">比對一個或多個文字字元。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-329">Match one or more word characters.</span></span>|  
|`(\s\w+)*`|<span data-ttu-id="4d0eb-330">比對出現零或多次、後接一或多個文字字元的空格字元。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-330">Match zero or more occurrences of a white-space character followed by one or more word characters.</span></span> <span data-ttu-id="4d0eb-331">此模式會比對多字的城市名稱。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-331">This pattern matches multi-word city names.</span></span> <span data-ttu-id="4d0eb-332">這是第三個擷取群組。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-332">This is the third capturing group.</span></span>|  
|`(\w+(\s\w+)*)`|<span data-ttu-id="4d0eb-333">比對一或多個文字字元，其後面接出現零或多次的空格字元，以及一或多個文字字元。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-333">Match one or more word characters followed by zero or more occurrences of a white-space character and one or more word characters.</span></span> <span data-ttu-id="4d0eb-334">這是第二個擷取群組。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-334">This is the second capturing group.</span></span>|  
|`,`|<span data-ttu-id="4d0eb-335">比對逗號。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-335">Match a comma.</span></span>|  
|`(\d+)`|<span data-ttu-id="4d0eb-336">比對一或多個數字。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-336">Match one or more digits.</span></span> <span data-ttu-id="4d0eb-337">這是第四個擷取群組。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-337">This is the fourth capturing group.</span></span>|  
|`;`|<span data-ttu-id="4d0eb-338">比對分號。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-338">Match a semicolon.</span></span>|  
|`((\w+(\s\w+)*),(\d+);)+`|<span data-ttu-id="4d0eb-339">一或多次比對文字的模式，該文字後面接任何其他文字，後面再接逗號、一或多個數字和分號。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-339">Match the pattern of a word followed by any additional words followed by a comma, one or more digits, and a semicolon, one or more times.</span></span> <span data-ttu-id="4d0eb-340">這是第一個擷取群組。</span><span class="sxs-lookup"><span data-stu-id="4d0eb-340">This is the first capturing group.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="4d0eb-341">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4d0eb-341">See also</span></span>

- <xref:System.Text.RegularExpressions>
- [<span data-ttu-id="4d0eb-342">.NET 規則運算式</span><span class="sxs-lookup"><span data-stu-id="4d0eb-342">.NET Regular Expressions</span></span>](regular-expressions.md)
- [<span data-ttu-id="4d0eb-343">規則運算式語言 - 快速參考</span><span class="sxs-lookup"><span data-stu-id="4d0eb-343">Regular Expression Language - Quick Reference</span></span>](regular-expression-language-quick-reference.md)
