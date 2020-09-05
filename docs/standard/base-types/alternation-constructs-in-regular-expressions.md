---
title: .NET 規則運算式中的替代建構
description: 了解如何在規則運算式中使用條件式比對的替代建構。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- either/or matching
- alternative matching patterns
- regular expressions, alternation constructs
- alternation constructs
- optional matching patterns
- constructs, alternation
- .NET Framework regular expressions, alternation constructs
ms.assetid: 071e22e9-fbb0-4ecf-add1-8d2424f9f2d1
ms.openlocfilehash: 506c1cdeb577452628d67ab00df20dd30881f406
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/05/2020
ms.locfileid: "89495430"
---
# <a name="alternation-constructs-in-regular-expressions"></a>規則運算式中的替代建構

替代建構會修改規則運算式來啟用二選一或條件式比對。 .NET 支援下列三種替代建構：

- [以 &#124; 進行的模式比對](#Either_Or)
- [以 (?(expression)yes&#124;no) 進行的條件式比對](#Conditional_Expr)
- [根據有效的已捕獲群組進行條件式比對](#Conditional_Group)

<a name="Either_Or"></a>
## <a name="pattern-matching-with-124"></a>以 &#124; 進行的模式比對

您可以使用分隔號 (`|`) 字元來比對其中任一系列的模式，且 `|` 字元會分隔每一個模式。

`|` 字元和正字元類別一樣，可以用來比對一些單一字元當中的任一字元。 下列範例同時使用正字元類別和透過 `|` 字元的二選一模式比對，在字串中尋找與單字 "gray" 或 "grey" 相符的項目。 在此案例中，`|` 字元會產生更詳細的規則運算式。

[!code-csharp[RegularExpressions.Language.Alternation#1](~/samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.alternation/cs/alternation1.cs#1)]
[!code-vb[RegularExpressions.Language.Alternation#1](~/samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.alternation/vb/alternation1.vb#1)]

使用字元的正則運算式，如下 `|` `\bgr(a|e)y\b` 表所示：

|模式|描述|  
|-------------|-----------------|  
|`\b`|從字緣開始。|  
|`gr`|比對字元 "gr"。|  
|<code>(a&#124;e)</code>|比對 "a" 或 "e"。|  
|`y\b`|比對字邊界上的 "y"。|  

`|` 字元也可以用來與多個字元或子運算式執行兩選一的比對，這些字元或運算式可以包含字元常值和規則運算式語言項目的任何組合。  (字元類別未提供這項功能。 ) 下列範例會使用 `|` 字元，將美國社會安全號碼解壓縮 (SSN) ，也就是具有*ddd*dd dddd 格式的9位數數位 - *dd* - * *，或是美國雇主識別碼 (EIN) ，也就是具有*dd*ddddddd 格式的9位數數位 - * *。

[!code-csharp[RegularExpressions.Language.Alternation#2](~/samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.alternation/cs/alternation2.cs#2)]
[!code-vb[RegularExpressions.Language.Alternation#2](~/samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.alternation/vb/alternation2.vb#2)]  

正則運算式的 `\b(\d{2}-\d{7}|\d{3}-\d{2}-\d{4})\b` 解讀如下表所示：
  
|模式|描述|  
|-------------|-----------------|  
|`\b`|從字緣開始。|  
|<code>(\d{2}-\d{7}&#124;\d{3}-\d{2}-\d{4})</code>|比對下列其中一項：兩個十進位數字後接連字號再後接七個十進位數字，或是三個十進位數字、連字號、兩個十進位數字、另一個連字號及四個十進位數字。|  
|`\b`|結束字緣比對。|  
  
<a name="Conditional_Expr"></a>
## <a name="conditional-matching-with-an-expression"></a>使用運算式進行的條件式比對

這個語言項目會嘗試比對兩個模式的其中一個是否符合初始模式。 其語法如下：  

`(?(` *expression* `)` *yes* `|` *no* `)`

其中 *expression* 是要比對的初始模式， *yes* 是符合 *expression* 時要比對的模式，而 *no* 是不符合 *expression* 時要比對的選擇性模式。 規則運算式引擎會將 *expression* 視為零寬度的判斷提示，也就是說，規則運算式引擎不會在評估 *expression* 之後於輸入資料流中前進。 因此，此建構等同於下列：

`(?(?=` *expression* `)` *yes* `|` *no* `)`

其中 `(?=` *expression* `)` 是零寬度的判斷提示結構。  (如需詳細資訊，請參閱 [群組結構](grouping-constructs-in-regular-expressions.md)。 ) ，因為正則運算式引擎會將 *運算式* 視為錨點 (零寬度判斷提示) ，所以 *運算式* 必須是零寬度的判斷提示 (如需詳細資訊，請參閱 [錨點](anchors-in-regular-expressions.md)) 或也包含在 *[是]* 中的子運算式。 否則就無法比對 *yes* 模式。  
  
> [!NOTE]
> 如果 *expression* 是已命名或編號的捕獲群組，則替代結構會被視為捕捉測試;如需詳細資訊，請參閱下一節， [根據有效的捕獲群組進行條件](#Conditional_Group)式比對。 換句話說，規則運算式引擎不會嘗試比對擷取的子字串，而會測試群組是否存在。  
  
下列範例是[以 &#124; 進行的二選一模式比對](#Either_Or)一節中使用的範例變化。 它使用條件式比對，來判斷字邊界後的前三個字元是否為兩個位數後接連字號。 如果是，它會嘗試比對美國美國雇主識別碼 (EIN)。 如果不是，它會嘗試比對美國社會安全碼 (SSN)。

[!code-csharp[RegularExpressions.Language.Alternation#3](~/samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.alternation/cs/alternation3.cs#3)]
[!code-vb[RegularExpressions.Language.Alternation#3](~/samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.alternation/vb/alternation3.vb#3)]

正則運算式模式的 `\b(?(\d{2}-)\d{2}-\d{7}|\d{3}-\d{2}-\d{4})\b` 解讀如下表所示：

|模式|描述|  
|-------------|-----------------|  
|`\b`|從字緣開始。|  
|`(?(\d{2}-)`|判斷接下來三個字元是否為兩個數字後接連字號。|  
|`\d{2}-\d{7}`|如果上一個模式符合，便會比對兩個數字，後接連字號，再後接七個數字。|  
|`\d{3}-\d{2}-\d{4}`|如果上一個模式不符合，便會比對三個十進位數字、連字號、兩個十進位數字、另一個連字號，以及四個十進位數字。|  
|`\b`|比對字邊界。|  

<a name="Conditional_Group"></a>
## <a name="conditional-matching-based-on-a-valid-captured-group"></a>依據有效擷取群組進行的條件式比對

這個語言項目會嘗試根據它是否已經比對指定的擷取群組，比對兩種模式的其中一種。 其語法如下：

`(?(` *name* `)` *yes* `|` *no* `)`

或

`(?(` *數字* `)` *是* `|` *no* `)`

其中 *name* 是名稱，而 *number* 是捕捉群組的數目， *yes* 是 *name* 或 *number* 有相符項時要比對的運算式，而 *no* 則是不符合時要比對的選擇性運算式。

如果 *name* 並未對應到規則運算式模式中所使用的擷取群組名稱，則替代建構會解譯為運算式測試，如上一節中所說明。 一般而言，這表示 *運算式* 會評估為 `false` 。 如果 *number* 沒有對應到規則運算式模式中所使用的編號擷取群組，則規則運算式引擎會擲回 <xref:System.ArgumentException>。

下列範例是[以 &#124; 進行的二選一模式比對](#Either_Or)一節中使用的範例變化。 它會使用名為 `n2` 的擷取群組，其由兩個數字後接連字號所組成。 替代建構會測試是否已在輸入字串中比對這個擷取群組。 如果是，交替建構會嘗試比對九位數雇主識別碼 (EIN) 的末七碼。美國雇主識別碼 (EIN)。 如果不是，則會嘗試比對九位數美國社會安全碼 (SSN)。社會安全碼 (SSN)。

[!code-csharp[RegularExpressions.Language.Alternation#4](~/samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.alternation/cs/alternation4.cs#4)]
[!code-vb[RegularExpressions.Language.Alternation#4](~/samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.alternation/vb/alternation4.vb#4)]

正則運算式模式的 `\b(?<n2>\d{2}-)?(?(n2)\d{7}|\d{3}-\d{2}-\d{4})\b` 解讀如下表所示：

|模式|描述|  
|-------------|-----------------|  
|`\b`|從字緣開始。|  
|`(?<n2>\d{2}-)?`|比對出現零次或一次且後接連字號的兩個數字。 將此擷取群組命名為 `n2`。|  
|`(?(n2)`|測試 `n2` 在輸入字串中是否相符。|  
|`\d{7}`|如果 `n2` 相符，則會比對七個十進位數字。|  
|<code>&#124;\d{3}-\d{2}-\d{4}</code>|如果 `n2` 不相符，則會比對三個十進位數字、一個連字號、兩個十進位數字、另一個連字號，以及四個十進位數字。|  
|`\b`|比對字邊界。|  

此範例是使用編號的群組而不是具名群組的一種變化，如下所示。 它的規則運算式模式是 `\b(\d{2}-)?(?(1)\d{7}|\d{3}-\d{2}-\d{4})\b`。

[!code-csharp[RegularExpressions.Language.Alternation#5](~/samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.alternation/cs/alternation5.cs#5)]
[!code-vb[RegularExpressions.Language.Alternation#5](~/samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.alternation/vb/alternation5.vb#5)]

## <a name="see-also"></a>請參閱

- [規則運算式語言 - 快速參考](regular-expression-language-quick-reference.md)
