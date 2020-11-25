---
title: .NET 規則運算式中的字元逸出
description: 了解 .NET 規則運算式中的特殊字元和逸出字元。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- unescaped characters
- replacement patterns
- characters, escapes
- regular expressions, character escapes
- escape characters
- .NET regular expressions, character escapes
- constructs, character escapes
ms.assetid: f49cc9cc-db7d-4058-8b8a-422bc08b29b0
ms.openlocfilehash: 820e6cd7fa4a60fa6adfcaf0f0ff4d25fdda0f21
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95734383"
---
# <a name="character-escapes-in-regular-expressions"></a><span data-ttu-id="16176-103">在規則運算式中執行字元逸出</span><span class="sxs-lookup"><span data-stu-id="16176-103">Character Escapes in Regular Expressions</span></span>

<span data-ttu-id="16176-104">規則運算式中的反斜線 (\\) 表示下列其中之一：</span><span class="sxs-lookup"><span data-stu-id="16176-104">The backslash (\\) in a regular expression indicates one of the following:</span></span>  
  
- <span data-ttu-id="16176-105">它後面所接的字元是特殊字元，如下節中的資料表所示。</span><span class="sxs-lookup"><span data-stu-id="16176-105">The character that follows it is a special character, as shown in the table in the following section.</span></span> <span data-ttu-id="16176-106">比方說，`\b` 是表示規則運算式比對應該在文字邊界上開始的一個錨點，`\t` 代表索引標籤，而 `\x020` 代表空間。</span><span class="sxs-lookup"><span data-stu-id="16176-106">For example, `\b` is an anchor that indicates that a regular expression match should begin on a word boundary, `\t` represents a tab, and `\x020` represents a space.</span></span>  
  
- <span data-ttu-id="16176-107">一個字元應該依其字面來解譯，否則會被解譯為未逸出的語言結構。</span><span class="sxs-lookup"><span data-stu-id="16176-107">A character that otherwise would be interpreted as an unescaped language construct should be interpreted literally.</span></span> <span data-ttu-id="16176-108">例如，括號 (`{`) 開始定義數量詞，但是反斜線後面接著一個括號 (`\{`) 則表示規則運算式引擎應該與括號相符。</span><span class="sxs-lookup"><span data-stu-id="16176-108">For example, a brace (`{`) begins the definition of a quantifier, but a backslash followed by a brace (`\{`) indicates that the regular expression engine should match the brace.</span></span> <span data-ttu-id="16176-109">同樣地，單一反斜線標記逸出的語言建構之開頭，但兩個反斜線 (`\\`) 表示規則運算式引擎應該符合反斜線。</span><span class="sxs-lookup"><span data-stu-id="16176-109">Similarly, a single backslash marks the beginning of an escaped language construct, but two backslashes (`\\`) indicate that the regular expression engine should match the backslash.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="16176-110">逸出字元會在規則運算式模式而不是在取代模式中被辨識。</span><span class="sxs-lookup"><span data-stu-id="16176-110">Character escapes are recognized in regular expression patterns but not in replacement patterns.</span></span>  
  
## <a name="character-escapes-in-net"></a><span data-ttu-id="16176-111">.NET 中的逸出字元</span><span class="sxs-lookup"><span data-stu-id="16176-111">Character Escapes in .NET</span></span>  

 <span data-ttu-id="16176-112">下表列出 .NET 中的規則運算式所支援的逸出字元。</span><span class="sxs-lookup"><span data-stu-id="16176-112">The following table lists the character escapes supported by regular expressions in .NET.</span></span>  
  
|<span data-ttu-id="16176-113">字元或序列</span><span class="sxs-lookup"><span data-stu-id="16176-113">Character or sequence</span></span>|<span data-ttu-id="16176-114">描述</span><span class="sxs-lookup"><span data-stu-id="16176-114">Description</span></span>|  
|---------------------------|-----------------|  
|<span data-ttu-id="16176-115">下列字元以外的所有字元：</span><span class="sxs-lookup"><span data-stu-id="16176-115">All characters except for the following:</span></span><br /><br /> <span data-ttu-id="16176-116">.</span><span class="sxs-lookup"><span data-stu-id="16176-116">.</span></span> <span data-ttu-id="16176-117">$ ^ { [ ( &#124; ) \* + ?</span><span class="sxs-lookup"><span data-stu-id="16176-117">$ ^ { [ ( &#124; ) \* + ?</span></span> \ |<span data-ttu-id="16176-118">不同於列在 [字元或序列] 資料行中的其他字元在規則運算式中沒有任何特殊的意義；它們符合其本身。</span><span class="sxs-lookup"><span data-stu-id="16176-118">Characters other than those listed in the **Character or sequence** column have no special meaning in regular expressions; they match themselves.</span></span><br /><br /> <span data-ttu-id="16176-119">[字元或序列] 資料行中所包含的字元是規則運算式的特殊語言項目。</span><span class="sxs-lookup"><span data-stu-id="16176-119">The characters included in the **Character or sequence** column are special regular expression language elements.</span></span> <span data-ttu-id="16176-120">若要在正則運算式中比對它們，必須將它們轉義或包含在 [正字元群組](character-classes-in-regular-expressions.md)中。</span><span class="sxs-lookup"><span data-stu-id="16176-120">To match them in a regular expression, they must be escaped or included in a [positive character group](character-classes-in-regular-expressions.md).</span></span> <span data-ttu-id="16176-121">例如，規則運算式 `\$\d+` 或 `[$]\d+` 符合「$1200」。</span><span class="sxs-lookup"><span data-stu-id="16176-121">For example, the regular expression `\$\d+` or `[$]\d+` matches "$1200".</span></span>|  
|`\a`|<span data-ttu-id="16176-122">符合警鈴 (警示) 字元 `\u0007`。</span><span class="sxs-lookup"><span data-stu-id="16176-122">Matches a bell (alarm) character, `\u0007`.</span></span>|  
|`\b`|<span data-ttu-id="16176-123">在 `[` *character_group* `]` 字元類別中，符合倒退鍵 `\u0008` 。</span><span class="sxs-lookup"><span data-stu-id="16176-123">In a `[`*character_group*`]` character class, matches a backspace, `\u0008`.</span></span>  <span data-ttu-id="16176-124"> (請參閱 [字元類別](character-classes-in-regular-expressions.md)。 ) 字元類別之外， `\b` 是符合單字界限的錨點。</span><span class="sxs-lookup"><span data-stu-id="16176-124">(See [Character Classes](character-classes-in-regular-expressions.md).) Outside a character class, `\b` is an anchor that matches a word boundary.</span></span> <span data-ttu-id="16176-125">(請參閱[錨點](anchors-in-regular-expressions.md)。)</span><span class="sxs-lookup"><span data-stu-id="16176-125">(See [Anchors](anchors-in-regular-expressions.md).)</span></span>|  
|`\t`|<span data-ttu-id="16176-126">符合索引標籤， `\u0009`。</span><span class="sxs-lookup"><span data-stu-id="16176-126">Matches a tab, `\u0009`.</span></span>|  
|`\r`|<span data-ttu-id="16176-127">符合歸位字元， `\u000D`。</span><span class="sxs-lookup"><span data-stu-id="16176-127">Matches a carriage return, `\u000D`.</span></span> <span data-ttu-id="16176-128">請注意，`\r` 不等於新行字元 `\n`。</span><span class="sxs-lookup"><span data-stu-id="16176-128">Note that `\r` is not equivalent to the newline character, `\n`.</span></span>|  
|`\v`|<span data-ttu-id="16176-129">符合垂直定位， `\u000B`。</span><span class="sxs-lookup"><span data-stu-id="16176-129">Matches a vertical tab, `\u000B`.</span></span>|  
|`\f`|<span data-ttu-id="16176-130">符合換頁字元， `\u000C`。</span><span class="sxs-lookup"><span data-stu-id="16176-130">Matches a form feed, `\u000C`.</span></span>|  
|`\n`|<span data-ttu-id="16176-131">符合新行字元， `\u000A`。</span><span class="sxs-lookup"><span data-stu-id="16176-131">Matches a new line, `\u000A`.</span></span>|  
|`\e`|<span data-ttu-id="16176-132">符合逸出字元， `\u001B`。</span><span class="sxs-lookup"><span data-stu-id="16176-132">Matches an escape, `\u001B`.</span></span>|  
|<span data-ttu-id="16176-133">`\`*nnn*</span><span class="sxs-lookup"><span data-stu-id="16176-133">`\` *nnn*</span></span>|<span data-ttu-id="16176-134">符合 ASCII 字元，其中 *nnn* 由代表八進位字元碼的兩個或三個數字所組成。</span><span class="sxs-lookup"><span data-stu-id="16176-134">Matches an ASCII character, where *nnn* consists of two or three digits that represent the octal character code.</span></span> <span data-ttu-id="16176-135">例如，`\040` 代表空格字元。</span><span class="sxs-lookup"><span data-stu-id="16176-135">For example, `\040` represents a space character.</span></span> <span data-ttu-id="16176-136">其若只有一個數字 (例如 `\2`)，或其對應至擷取群組的編號，會將此建構解譯為反向參考 </span><span class="sxs-lookup"><span data-stu-id="16176-136">This construct is interpreted as a backreference if it has only one digit (for example, `\2`) or if it corresponds to the number of a capturing group.</span></span> <span data-ttu-id="16176-137">(請參閱[反向參考建構](backreference-constructs-in-regular-expressions.md)。)</span><span class="sxs-lookup"><span data-stu-id="16176-137">(See [Backreference Constructs](backreference-constructs-in-regular-expressions.md).)</span></span>|  
|<span data-ttu-id="16176-138">`\x` *nn*</span><span class="sxs-lookup"><span data-stu-id="16176-138">`\x` *nn*</span></span>|<span data-ttu-id="16176-139">符合 ASCII 字元，其中 *nn* 是兩位數的十六進位字元碼。</span><span class="sxs-lookup"><span data-stu-id="16176-139">Matches an ASCII character, where *nn* is a two-digit hexadecimal character code.</span></span>|  
|<span data-ttu-id="16176-140">`\c`*X*</span><span class="sxs-lookup"><span data-stu-id="16176-140">`\c` *X*</span></span>|<span data-ttu-id="16176-141">符合 ASCII 控制字元，其中 X 是控制字元的字母。</span><span class="sxs-lookup"><span data-stu-id="16176-141">Matches an ASCII control character, where X is the letter of the control character.</span></span> <span data-ttu-id="16176-142">例如，`\cC` 是 CTRL + C。</span><span class="sxs-lookup"><span data-stu-id="16176-142">For example, `\cC` is CTRL-C.</span></span>|  
|<span data-ttu-id="16176-143">`\u` *nnnn*</span><span class="sxs-lookup"><span data-stu-id="16176-143">`\u` *nnnn*</span></span>|<span data-ttu-id="16176-144">符合 UTF-16 字碼單位，其值為十六進位的 *nnnn*。</span><span class="sxs-lookup"><span data-stu-id="16176-144">Matches a UTF-16 code unit whose value is *nnnn* hexadecimal.</span></span> <span data-ttu-id="16176-145">**注意：**.NET 不支援用來指定 Unicode 的 Perl 5 逸出字元。</span><span class="sxs-lookup"><span data-stu-id="16176-145">**Note:**  The Perl 5 character escape that is used to specify Unicode is not supported by .NET.</span></span> <span data-ttu-id="16176-146">Perl 5 字元 escape 的格式為 `\x{` *####* `…}` ，其中 *####* `…` 是一系列的十六進位數位。</span><span class="sxs-lookup"><span data-stu-id="16176-146">The Perl 5 character escape has the form `\x{`*####*`…}`, where *####*`…` is a series of hexadecimal digits.</span></span> <span data-ttu-id="16176-147">請改用 `\u`*nnnn*。</span><span class="sxs-lookup"><span data-stu-id="16176-147">Instead, use `\u`*nnnn*.</span></span>|  
|`\`|<span data-ttu-id="16176-148">當後面加上一個不被認為是逸出的字元時，符合該字元。</span><span class="sxs-lookup"><span data-stu-id="16176-148">When followed by a character that is not recognized as an escaped character, matches that character.</span></span> <span data-ttu-id="16176-149">例如，`\*` 符合使用星號 (\*)，而且與 `\x2A` 相同。</span><span class="sxs-lookup"><span data-stu-id="16176-149">For example, `\*` matches an asterisk (\*) and is the same as `\x2A`.</span></span>|  
  
## <a name="an-example"></a><span data-ttu-id="16176-150">範例</span><span class="sxs-lookup"><span data-stu-id="16176-150">An Example</span></span>  

 <span data-ttu-id="16176-151">下列範例說明如何在規則運算式中使用逸出字元。</span><span class="sxs-lookup"><span data-stu-id="16176-151">The following example illustrates the use of character escapes in a regular expression.</span></span> <span data-ttu-id="16176-152">它會剖析字串，包含在 2009 年世界上最大城市的名稱以及人口。</span><span class="sxs-lookup"><span data-stu-id="16176-152">It parses a string that contains the names of the world's largest cities and their populations in 2009.</span></span> <span data-ttu-id="16176-153">每個城市名稱及其人口數目被 Tab (`\t`) 或分隔號 (&#124; 或 `\u007c`) 分開。</span><span class="sxs-lookup"><span data-stu-id="16176-153">Each city name is separated from its population by a tab (`\t`) or a vertical bar (&#124; or `\u007c`).</span></span> <span data-ttu-id="16176-154">個別的城市及其人口是被歸位字元和換行字元分隔開的。</span><span class="sxs-lookup"><span data-stu-id="16176-154">Individual cities and their populations are separated from each other by a carriage return and line feed.</span></span>  
  
 [!code-csharp[RegularExpressions.Language.Escapes#1](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.escapes/cs/escape1.cs#1)]
 [!code-vb[RegularExpressions.Language.Escapes#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.escapes/vb/escape1.vb#1)]  
  
 <span data-ttu-id="16176-155">規則運算式 `\G(.+)[\t\u007c](.+)\r?\n` 的解譯方式如下表所示。</span><span class="sxs-lookup"><span data-stu-id="16176-155">The regular expression `\G(.+)[\t\u007c](.+)\r?\n` is interpreted as shown in the following table.</span></span>  
  
|<span data-ttu-id="16176-156">模式</span><span class="sxs-lookup"><span data-stu-id="16176-156">Pattern</span></span>|<span data-ttu-id="16176-157">描述</span><span class="sxs-lookup"><span data-stu-id="16176-157">Description</span></span>|  
|-------------|-----------------|  
|`\G`|<span data-ttu-id="16176-158">從最後比對結束之處開始比對。</span><span class="sxs-lookup"><span data-stu-id="16176-158">Begin the match where the last match ended.</span></span>|  
|`(.+)`|<span data-ttu-id="16176-159">一或多次比對任何字元。</span><span class="sxs-lookup"><span data-stu-id="16176-159">Match any character one or more times.</span></span> <span data-ttu-id="16176-160">這是第一個擷取群組。</span><span class="sxs-lookup"><span data-stu-id="16176-160">This is the first capturing group.</span></span>|  
|`[\t\u007c]`|<span data-ttu-id="16176-161">比對 Tab (`\t`) 或分隔號 (&#124;)。</span><span class="sxs-lookup"><span data-stu-id="16176-161">Match a tab (`\t`) or a vertical bar (&#124;).</span></span>|  
|`(.+)`|<span data-ttu-id="16176-162">一或多次比對任何字元。</span><span class="sxs-lookup"><span data-stu-id="16176-162">Match any character one or more times.</span></span> <span data-ttu-id="16176-163">這是第二個擷取群組。</span><span class="sxs-lookup"><span data-stu-id="16176-163">This is the second capturing group.</span></span>|  
|`\r?\n`|<span data-ttu-id="16176-164">比對後面接著新行的歸位字元其中的零或指定項目。</span><span class="sxs-lookup"><span data-stu-id="16176-164">Match zero or one occurrence of a carriage return followed by a new line.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="16176-165">另請參閱</span><span class="sxs-lookup"><span data-stu-id="16176-165">See also</span></span>

- [<span data-ttu-id="16176-166">規則運算式語言 - 快速參考</span><span class="sxs-lookup"><span data-stu-id="16176-166">Regular Expression Language - Quick Reference</span></span>](regular-expression-language-quick-reference.md)
