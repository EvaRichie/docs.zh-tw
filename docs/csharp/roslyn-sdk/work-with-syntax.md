---
title: 使用 .NET Compiler Platform SDK 語法模型
description: 此概觀說明您使用的類型，以了解與管理語法節點。
ms.date: 10/15/2017
ms.custom: mvc
ms.openlocfilehash: fdb13095c2b91e54d58988a51a51b05652e57ea6
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83208391"
---
# <a name="work-with-syntax"></a>使用語法

*語法樹*是編譯器 API 公開的基本資料結構。 這些樹狀結構代表原始程式碼的語彙和語法結構。 它們有兩個重要用途：

- 若要允許像是 IDE、增益集、程式碼分析工具和重構等工具，在使用者的專案中查看和處理原始程式碼的語法結構。
- 若要啟用工具（例如重構和 IDE），以自然方式建立、修改和重新排列原始程式碼，而不需要使用直接文字編輯。 透過建立和管理樹狀結構，工具可以輕鬆建立及重新整理程式碼。

## <a name="syntax-trees"></a>語法樹

語法樹是用於編譯、程式碼分析、繫結、重構、IDE 功能與產生程式碼的主要結構。 若不先找到並分類成許多已知的結構化語言項目之一，原始程式碼的任何部分均無法解讀。

語法樹有三個索引鍵屬性。 第一個屬性是語法樹完整保存所有來源資訊不失真。 完整精確度表示語法樹狀結構包含在來源文字中找到的每個資訊片段、每個文法結構、每個詞彙 token，以及介於兩者之間的所有其他專案，包括空白字元、批註和預處理器指示詞。 例如，來源中提及的每個常值都和鍵入的一般無二。 當程式不完整或因表示已略過或遺漏的標記而不正確時，語法樹狀結構也會在原始程式碼中捕捉錯誤。

語法樹狀結構的第二個屬性是，它們可以產生其剖析來源的確切文字。 從任何語法節點，可以取得根節點之子樹的文字標記法。 這種功能表示語法樹狀結構可以用來建立和編輯來源文字。 藉由建立樹狀結構、隱含地建立對等的文字，並藉由編輯語法樹狀結構，讓現有樹狀結構的變更變成新的樹狀結構，您就能有效編輯文字。

語法樹的第三個屬性是它們為不可變且具備執行緒安全。 取得樹狀結構之後，它就是程式碼目前狀態的快照集，而且永遠不會變更。 這可讓多位使用者在不同的執行緒中同時與同一語法樹互動，不會鎖定或重複。 因為樹狀結構是不變的，而且不能直接對樹狀結構進行任何修改，所以 Factory 方法透過建立樹狀結構的其他快照集來協助建立和修改語法樹。 樹狀結構重複使用基礎節點很有效率，因此新版本重建迅速且只佔一點額外的記憶體。

語法樹實際上是樹狀資料結構，在此，其他項目的父代為非結尾結構化項目。 每一個語法樹都是由節點、權杖和邏輯所組成。

## <a name="syntax-nodes"></a>語法節點

語法節點是語法樹主要項目的其中之一。 這些節點代表語法建構，例如宣告、陳述式、子句和運算式。 每個語法節點類別都是由衍生自 <xref:Microsoft.CodeAnalysis.SyntaxNode?displayProperty=nameWithType> 的個別類別代表。 節點類別集不可擴充。

所有語法節點都是語法樹中的非結尾節點，這表示它們一律有其他子系節點和權杖。 身為另一個節點的子系，每個節點都有父節點，可透過 <xref:Microsoft.CodeAnalysis.SyntaxNode.Parent?displayProperty=nameWithType> 屬性存取。 因為節點和樹狀結構不可變，所以節點的父代永遠不會變更。 樹狀結構的根有 null 父代。

每個節點都有 <xref:Microsoft.CodeAnalysis.SyntaxNode.ChildNodes?displayProperty=nameWithType> 方法，根據子節點在原始程式文字中的位置，傳回它們的循序清單。 本清單不包含權杖。 每個節點也有可檢查子系的方法，例如 <xref:Microsoft.CodeAnalysis.SyntaxNode.DescendantNodes%2A> 、 <xref:Microsoft.CodeAnalysis.SyntaxNode.DescendantTokens%2A> 或 <xref:Microsoft.CodeAnalysis.SyntaxNode.DescendantTrivia%2A> -，代表存在於該節點根樹系中的所有節點、權杖或邏輯的清單。

此外，每個語法節點的子類別會透過強型別屬性公開所有相同的子系。 例如，<xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax> 節點類別有三個針對二元運算子的額外屬性：<xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.Left>、<xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.OperatorToken> 和 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.Right>。 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.Left> 和 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.Right> 的類型是 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.ExpressionSyntax>，<xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.OperatorToken> 的類型是 <xref:Microsoft.CodeAnalysis.SyntaxToken>。

某些語法節點有選擇性的子系。 例如，<xref:Microsoft.CodeAnalysis.CSharp.Syntax.IfStatementSyntax> 有選擇性的 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.ElseClauseSyntax>。 如果子系不存在，則屬性會傳回 null。

## <a name="syntax-tokens"></a>語法權杖

語法權杖是語言文法的結尾，代表最小的程式碼語法片段。 它們永遠不是其他節點或權杖的父代。 語法權杖是由關鍵字、識別碼、常值和標點符號所組成。

基於效率考量，<xref:Microsoft.CodeAnalysis.SyntaxToken> 類型是 CLR 值類型。 因此，不像語法節點，所有種類的混合屬性權杖只有一種結構，這些屬性具有依賴要代表之權杖種類的意義。

例如，整數常值權杖代表數值。 除了權杖跨越的未經處理原始程式文字，常值權杖有 <xref:Microsoft.CodeAnalysis.SyntaxToken.Value> 屬性會告訴您精確的已解碼整數值。 此屬性歸類為 <xref:System.Object>，因為它可能是眾多基本類型之一。

<xref:Microsoft.CodeAnalysis.SyntaxToken.ValueText> 屬性告訴您的資訊和 <xref:Microsoft.CodeAnalysis.SyntaxToken.Value> 屬性一樣，但這個屬性一律歸類為 <xref:System.String>。 C# 原始程式文字中的識別碼可能包含 Unicode 逸出字元，但逸出序列本身的語法不視為識別碼名稱的一部分。 所以，雖然權杖跨越的原始文字確實包含逸出序列，但 <xref:Microsoft.CodeAnalysis.SyntaxToken.ValueText> 屬性則否。 它反而會包含逸出所識別的 Unicode 字元。 例如，如果原始程式文字包含寫為 `\u03C0` 的識別碼，則此權杖的 <xref:Microsoft.CodeAnalysis.SyntaxToken.ValueText> 屬性會傳回 `π`。

## <a name="syntax-trivia"></a>語法邏輯

語法邏輯代表的原始程式文字部分，主要是一般的程式碼，例如空白字元、註解和前置處理器指示詞。 像語法權杖一樣，邏輯為實值型別。 單一 <xref:Microsoft.CodeAnalysis.SyntaxTrivia?displayProperty=nameWithType> 類型用以描述所有種類的邏輯。

因為邏輯不屬於一般的語言語法，而且會出現在任兩個權杖之間的任何位置，所以它們未被納入語法樹成為子節點。 但因為它們在實作重構等功能以維護完整的原始程式文字不失真時很重要，所以它們又是語法樹的一部分。

您可以藉由檢查權杖的或集合來存取邏輯 <xref:Microsoft.CodeAnalysis.SyntaxToken.LeadingTrivia?displayProperty=nameWithType> <xref:Microsoft.CodeAnalysis.SyntaxToken.TrailingTrivia?displayProperty=nameWithType> 。 剖析原始程式文字後，邏輯的順序就與權杖產生關聯。 一般情況下，權杖擁有自同一行到下一個權杖的任何邏輯。 該行之後的所有邏輯都與接續的權杖建立關聯。 原始程式檔中的第一個權杖取得所有初始邏輯，檔案中邏輯的最後一個序列會跟到檔案結尾的權杖，這本來會是零寬度。

不同於語法節點和權杖，語法邏輯沒有父代。 但因為它們屬於樹狀結構，而且每一個都與單一權杖建立關聯，所以您可以存取它使用 <xref:Microsoft.CodeAnalysis.SyntaxTrivia.Token?displayProperty=nameWithType> 屬性來建立關聯的權杖。

## <a name="spans"></a>跨越

每個節點、權杖或邏輯都知道其在原始程式文字內的位置及其組成字元數。 文字位置是以 32 位元的整數表示，也就是以零起始的 `char` 索引。 <xref:Microsoft.CodeAnalysis.Text.TextSpan> 物件是起始位置和字元計數，兩個都以整數表示。 如果 <xref:Microsoft.CodeAnalysis.Text.TextSpan> 長度為零，即指兩個字元之間的位置。

每個節點均有兩個 <xref:Microsoft.CodeAnalysis.Text.TextSpan> 屬性：<xref:Microsoft.CodeAnalysis.SyntaxNode.Span%2A> 與 <xref:Microsoft.CodeAnalysis.SyntaxNode.FullSpan%2A>。

<xref:Microsoft.CodeAnalysis.SyntaxNode.Span%2A>屬性是從節點之子樹的第一個 token 開頭到最後一個 token 結尾的文字範圍。 此範圍不包含任何開頭或尾端邏輯。

<xref:Microsoft.CodeAnalysis.SyntaxNode.FullSpan%2A>屬性是包含節點正常範圍的文字範圍，加上任何前置或尾端邏輯的範圍。

例如：

``` csharp
      if (x > 3)
      {
||        // this is bad
          |throw new Exception("Not right.");|  // better exception?||
      }
```

區塊內的陳述式節點有單一分隔號 (|) 所指示的範圍。 它包括字元 `throw new Exception("Not right.");`。 完整範圍以雙分隔號 (|) 表示。 當範圍和字元與開頭和尾端邏輯建立關聯時，它會包含相同字元。

## <a name="kinds"></a>種類

每個節點、權杖或邏輯都有 <xref:System.Int32?displayProperty=nameWithType> 類型的 <xref:Microsoft.CodeAnalysis.SyntaxNode.RawKind?displayProperty=nameWithType> 屬性，可識別所代表的確切語法項目。 這個值可以轉換成語言特定的列舉型別。 每個語言（c # 或 Visual Basic）都具有單一 `SyntaxKind` 列舉（ <xref:Microsoft.CodeAnalysis.CSharp.SyntaxKind?displayProperty=nameWithType> 分別為和 <xref:Microsoft.CodeAnalysis.VisualBasic.SyntaxKind?displayProperty=nameWithType> ），其中會列出文法中所有可能的節點、權杖和邏輯元素。 可透過存取 <xref:Microsoft.CodeAnalysis.CSharp.CSharpExtensions.Kind%2A?displayProperty=nameWithType> 或 <xref:Microsoft.CodeAnalysis.VisualBasic.VisualBasicExtensions.Kind%2A?displayProperty=nameWithType> 擴充方法來自動完成這項轉換。

<xref:Microsoft.CodeAnalysis.SyntaxToken.RawKind> 屬性允許共用相同節點類別的語法節點類型簡單去除混淆。 對權杖和邏輯而言，這個屬性是區別某項目類型的唯一方式。

例如，單一 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax> 類別有 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.Left>、<xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.OperatorToken> 和 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.Right> 子系。 <xref:Microsoft.CodeAnalysis.CSharp.CSharpExtensions.Kind%2A> 屬性可區別其為 <xref:Microsoft.CodeAnalysis.CSharp.SyntaxKind.AddExpression>、<xref:Microsoft.CodeAnalysis.CSharp.SyntaxKind.SubtractExpression> 或 <xref:Microsoft.CodeAnalysis.CSharp.SyntaxKind.MultiplyExpression> 種類的語法節點。

## <a name="errors"></a>Errors

即使原始程式文字包含語法錯誤，仍會公開可往返來源的完整語法樹。 當剖析器遇到不符合所定義語言語法的程式碼時，它會使用兩種技術的其中一種來建立語法樹狀結構：

- 如果剖析器需要特定種類的 token，但找不到，則可能會將遺漏的 token 插入至語法樹狀結構中所需的標記位置。 遺漏的權杖代表預期的實際權杖，但具有空的範圍，且其 <xref:Microsoft.CodeAnalysis.SyntaxNode.IsMissing?displayProperty=nameWithType> 屬性會傳回 `true`。

- 剖析器可能會略過權杖，直到找到可以繼續剖析的 token 為止。 在此情況下，略過的權杖會附加為種類為 <xref:Microsoft.CodeAnalysis.CSharp.SyntaxKind.SkippedTokensTrivia> 的邏輯節點。
