---
ms.openlocfilehash: c0c1c9c9d8e3aeb6f689f754d09b50b208b54112
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/20/2020
ms.locfileid: "83702277"
---
### <a name="stringinfo-and-textelementenumerator-are-now-uax29-compliant"></a><span data-ttu-id="8f89a-101">System.globalization.stringinfo> 和 TextElementEnumerator 現在符合 UAX29 標準</span><span class="sxs-lookup"><span data-stu-id="8f89a-101">StringInfo and TextElementEnumerator are now UAX29-compliant</span></span>

<span data-ttu-id="8f89a-102">在此變更之前， <xref:System.Globalization.StringInfo?displayProperty=fullName> 和 <xref:System.Globalization.TextElementEnumerator?displayProperty=fullName> 未正確處理所有語素簇叢集。</span><span class="sxs-lookup"><span data-stu-id="8f89a-102">Prior to this change, <xref:System.Globalization.StringInfo?displayProperty=fullName> and <xref:System.Globalization.TextElementEnumerator?displayProperty=fullName> didn't properly handle all grapheme clusters.</span></span> <span data-ttu-id="8f89a-103">有些 graphemes 已分割成其組成元件，而不是保持在一起。</span><span class="sxs-lookup"><span data-stu-id="8f89a-103">Some graphemes were split into their constituent components instead of being kept together.</span></span> <span data-ttu-id="8f89a-104">現在， <xref:System.Globalization.StringInfo> 和會 <xref:System.Globalization.TextElementEnumerator> 根據 Unicode 標準的最新版本來處理語素簇叢集。</span><span class="sxs-lookup"><span data-stu-id="8f89a-104">Now, <xref:System.Globalization.StringInfo> and <xref:System.Globalization.TextElementEnumerator> process grapheme clusters according to the latest version of the Unicode Standard.</span></span>

<span data-ttu-id="8f89a-105">此外，方法會 <xref:Microsoft.VisualBasic.Strings.StrReverse%2A?displayProperty=fullName> 反轉 Visual Basic 字串中的字元，現在也會遵循語素簇叢集的 Unicode 標準。</span><span class="sxs-lookup"><span data-stu-id="8f89a-105">In addition, the <xref:Microsoft.VisualBasic.Strings.StrReverse%2A?displayProperty=fullName> method, which reverses the characters in a string in Visual Basic, now also follows the Unicode standard for grapheme clusters.</span></span>

#### <a name="change-description"></a><span data-ttu-id="8f89a-106">變更描述</span><span class="sxs-lookup"><span data-stu-id="8f89a-106">Change description</span></span>

<span data-ttu-id="8f89a-107">[語素簇](https://www.unicode.org/glossary/#grapheme)或[extended 語素簇](https://www.unicode.org/glossary/#extended_grapheme_cluster)叢集是單一使用者察覺的字元，可能由多個 Unicode 程式碼點組成。</span><span class="sxs-lookup"><span data-stu-id="8f89a-107">A [grapheme](https://www.unicode.org/glossary/#grapheme) or [extended grapheme cluster](https://www.unicode.org/glossary/#extended_grapheme_cluster) is a single user-perceived character that may be made up of multiple Unicode code points.</span></span> <span data-ttu-id="8f89a-108">例如，包含泰文字元 "kam" （）的字串 :::no-loc text="กำ"::: 包含下列兩個字元：</span><span class="sxs-lookup"><span data-stu-id="8f89a-108">For example, the string containing the Thai character "kam" (:::no-loc text="กำ":::) consists of the following two characters:</span></span>

- <span data-ttu-id="8f89a-109">:::no-loc text="ก":::（= ' \u0e01 '）泰文字元 KO KAI</span><span class="sxs-lookup"><span data-stu-id="8f89a-109">:::no-loc text="ก"::: (= '\u0e01') THAI CHARACTER KO KAI</span></span>
- <span data-ttu-id="8f89a-110">:::no-loc text=" ำ":::（= ' \u0e33 '）泰文字元 SARA AM</span><span class="sxs-lookup"><span data-stu-id="8f89a-110">:::no-loc text=" ำ"::: (= '\u0e33') THAI CHARACTER SARA AM</span></span>

<span data-ttu-id="8f89a-111">向使用者顯示時，作業系統會結合兩個字元來形成單一顯示字元（或語素簇） "kam" 或 :::no-loc text="กำ"::: 。</span><span class="sxs-lookup"><span data-stu-id="8f89a-111">When displayed to the user, the operating system combines the two characters to form the single display character (or grapheme) "kam" or :::no-loc text="กำ":::.</span></span> <span data-ttu-id="8f89a-112">表情也可以包含多個合併成以類似方式顯示的字元。</span><span class="sxs-lookup"><span data-stu-id="8f89a-112">Emoji can also consist of multiple characters that are combined for display in a similar way.</span></span>

> [!TIP]
> <span data-ttu-id="8f89a-113">.NET 檔在參考語素簇時，有時會使用「文字元素」一詞。</span><span class="sxs-lookup"><span data-stu-id="8f89a-113">The .NET documentation sometimes uses the term "text element" when referring to a grapheme.</span></span>

<span data-ttu-id="8f89a-114"><xref:System.Globalization.StringInfo>和 <xref:System.Globalization.TextElementEnumerator> 類別會檢查字串，並傳回其所包含之 graphemes 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="8f89a-114">The <xref:System.Globalization.StringInfo> and <xref:System.Globalization.TextElementEnumerator> classes inspect strings and return information about the graphemes they contain.</span></span> <span data-ttu-id="8f89a-115">在 .NET Framework （所有版本）和 .NET Core 3.x 和更早版本中，這兩個類別會使用自訂邏輯來處理一些結合類別，但不完全符合[Unicode 標準](https://www.unicode.org/reports/tr29/tr29-35.html#Grapheme_Cluster_Boundaries)。</span><span class="sxs-lookup"><span data-stu-id="8f89a-115">In .NET Framework (all versions) and .NET Core 3.x and earlier, these two classes use custom logic that handles some combining classes but doesn't fully comply with the [Unicode Standard](https://www.unicode.org/reports/tr29/tr29-35.html#Grapheme_Cluster_Boundaries).</span></span> <span data-ttu-id="8f89a-116">例如， <xref:System.Globalization.StringInfo> 和 <xref:System.Globalization.TextElementEnumerator> 類別不正確地將單一泰文字元 "kam" 分割回其組成的元件，而不是將它們保持在一起。</span><span class="sxs-lookup"><span data-stu-id="8f89a-116">For example, the <xref:System.Globalization.StringInfo> and <xref:System.Globalization.TextElementEnumerator> classes incorrectly split the single Thai character "kam" back into its constituent components instead of keeping them together.</span></span> <span data-ttu-id="8f89a-117">這些類別也會不正確地將表情字元「🤷🏽♀️」分割成四個叢集（person shrugging、膚色音調修飾詞、性別修飾詞和不可見的結合器），而不是將它們一起保持為單一語素簇叢集。</span><span class="sxs-lookup"><span data-stu-id="8f89a-117">These classes also incorrectly split the emoji character "🤷🏽‍♀️" into four clusters (person shrugging, skin tone modifier, gender modifier, and an invisible combiner) instead of keeping them together as a single grapheme cluster.</span></span>

<span data-ttu-id="8f89a-118">從 .NET 5 開始， <xref:System.Globalization.StringInfo> 和類別會依照 <xref:System.Globalization.TextElementEnumerator> [unicode 標準附錄 \# 29、rev 35、sec. 3](https://www.unicode.org/reports/tr29/tr29-35.html)所定義的方式來執行 unicode 標準。</span><span class="sxs-lookup"><span data-stu-id="8f89a-118">Starting with .NET 5, the <xref:System.Globalization.StringInfo> and <xref:System.Globalization.TextElementEnumerator> classes implement the Unicode standard as defined by [Unicode Standard Annex \#29, rev. 35, sec. 3](https://www.unicode.org/reports/tr29/tr29-35.html).</span></span> <span data-ttu-id="8f89a-119">特別是，他們現在會針對所有結合類別傳回[擴充的語素簇](https://www.unicode.org/glossary/#extended_grapheme_cluster)叢集。</span><span class="sxs-lookup"><span data-stu-id="8f89a-119">In particular, they now return [extended grapheme clusters](https://www.unicode.org/glossary/#extended_grapheme_cluster) for all combining classes.</span></span>

<span data-ttu-id="8f89a-120">請考慮下列 c # 程式碼：</span><span class="sxs-lookup"><span data-stu-id="8f89a-120">Consider the following C# code:</span></span>

```cs
using System.Globalization;

static void Main(string[] args)
{
    PrintGraphemes("กำ");
    PrintGraphemes("🤷🏽‍♀️");
}

static void PrintGraphemes(string str)
{
    Console.WriteLine($"Printing graphemes of \"{str}\"...");
    int i = 0;

    TextElementEnumerator enumerator = StringInfo.GetTextElementEnumerator(str);
    while (enumerator.MoveNext())
    {
        Console.WriteLine($"Grapheme {++i}: \"{enumerator.Current}\"");
    }

    Console.WriteLine($"({i} grapheme(s) total.)");
    Console.WriteLine();
}
```

<span data-ttu-id="8f89a-121">在 .NET Framework 和 .NET Core 3.x 和更早版本中，graphemes 會進行分割，而主控台輸出如下所示：</span><span class="sxs-lookup"><span data-stu-id="8f89a-121">In .NET Framework and .NET Core 3.x and earlier versions, the graphemes are split up, and the console output is as follows:</span></span>

```txt
Printing graphemes of "กำ"...
Grapheme 1: "ก"
Grapheme 2: "ำ"
(2 grapheme(s) total.)

Printing graphemes of "🤷🏽‍♀️"...
Grapheme 1: "🤷"
Grapheme 2: "🏽"
Grapheme 3: "‍"
Grapheme 4: "♀️"
(4 grapheme(s) total.)
```

<span data-ttu-id="8f89a-122">在 .NET 5 和更新版本中，graphemes 會保持在一起，而主控台輸出如下所示：</span><span class="sxs-lookup"><span data-stu-id="8f89a-122">In .NET 5 and later versions, the graphemes are kept together, and the console output is as follows:</span></span>

```txt
Printing graphemes of "กำ"...
Grapheme 1: "กำ"
(1 grapheme(s) total.)

Printing graphemes of "🤷🏽‍♀️"...
Grapheme 1: "🤷🏽‍♀️"
(1 grapheme(s) total.)
```

<span data-ttu-id="8f89a-123">此外，從 .NET 5 開始，在 Visual Basic 中將字串中的 <xref:Microsoft.VisualBasic.Strings.StrReverse%2A?displayProperty=fullName> 字元反轉的方法，現在也會遵循語素簇叢集的 Unicode 標準。</span><span class="sxs-lookup"><span data-stu-id="8f89a-123">In addition, starting in .NET 5, the <xref:Microsoft.VisualBasic.Strings.StrReverse%2A?displayProperty=fullName> method, which reverses the characters in a string in Visual Basic, now also follows the Unicode standard for grapheme clusters.</span></span>

<span data-ttu-id="8f89a-124">這些變更是 .NET 中更廣泛 Unicode 和 UTF-8 改良功能的一部分，包括擴充的語素簇叢集列舉 API，以補充 <xref:System.Text.Rune?displayProperty=fullName> .Net Core 3.0 中的類型所引進的 unicode 純量值列舉 api。</span><span class="sxs-lookup"><span data-stu-id="8f89a-124">These changes are part of a wider set of Unicode and UTF-8 improvements in .NET, including an extended grapheme cluster enumeration API to complement the Unicode scalar-value enumeration APIs that were introduced with the <xref:System.Text.Rune?displayProperty=fullName> type in .NET Core 3.0.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="8f89a-125">引進的版本</span><span class="sxs-lookup"><span data-stu-id="8f89a-125">Version introduced</span></span>

<span data-ttu-id="8f89a-126">.NET 5.0 Preview 1</span><span class="sxs-lookup"><span data-stu-id="8f89a-126">.NET 5.0 Preview 1</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="8f89a-127">建議的動作</span><span class="sxs-lookup"><span data-stu-id="8f89a-127">Recommended action</span></span>

<span data-ttu-id="8f89a-128">您不需要採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="8f89a-128">You don't need to take any action.</span></span> <span data-ttu-id="8f89a-129">在各種全球化的相關案例中，您的應用程式將會以更符合標準的方式自動行為。</span><span class="sxs-lookup"><span data-stu-id="8f89a-129">Your apps will automatically behave in a more standards-compliant manner in a variety of globalization-related scenarios.</span></span>

#### <a name="category"></a><span data-ttu-id="8f89a-130">類別</span><span class="sxs-lookup"><span data-stu-id="8f89a-130">Category</span></span>

<span data-ttu-id="8f89a-131">全球化</span><span class="sxs-lookup"><span data-stu-id="8f89a-131">Globalization</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="8f89a-132">受影響的 API</span><span class="sxs-lookup"><span data-stu-id="8f89a-132">Affected APIs</span></span>

- <xref:System.Globalization.StringInfo?displayProperty=fullName>
- <xref:System.Globalization.TextElementEnumerator?displayProperty=fullName>
- <xref:Microsoft.VisualBasic.Strings.StrReverse%2A?displayProperty=fullName>

<!--

#### Affected APIs

- `T:System.Globalization.StringInfo`
- `T:System.Globalization.TextElementEnumerator`
- `Overload:Microsoft.VisualBasic.Strings.StrReverse`

-->
