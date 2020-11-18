---
title: 規則運算式中的群組建構
description: 瞭解如何在 .NET 中使用群組結構。 群組結構會描繪正則運算式的子運算式，並捕捉輸入字串的子字串。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- lookbehinds
- regular expressions, grouping constructs
- lookaheads
- .NET regular expressions, grouping constructs
- constructs, grouping
- grouping constructs
ms.assetid: 0fc18634-f590-4062-8d5c-f0b71abe405b
ms.openlocfilehash: 52f7efdf5591901602811cba8f2b6c1a4f42f96c
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94823000"
---
# <a name="grouping-constructs-in-regular-expressions"></a>規則運算式中的群組建構
群組建構會描寫規則運算式的子運算式，以及擷取輸入字串的子字串。 您可以使用分組建構來執行下列作業：  
  
- 比對輸入字串中重複的子運算式。  
  
- 將數量詞套用至具有多個規則運算式語言項目的子運算式。 如需數量詞的詳細資訊，請參閱 [Quantifiers](quantifiers-in-regular-expressions.md)。  
  
- 在 <xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=nameWithType> 和 <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=nameWithType> 方法傳回的字串中包含子運算式。  
  
- 從 <xref:System.Text.RegularExpressions.Match.Groups%2A?displayProperty=nameWithType> 屬性擷取個別子運算式，再全部一起與相符文字分開處理。  
  
 下表列出 .NET 規則運算式引擎支援的群組建構，並指出其為擷取或非擷取。  
  
|分組建構|擷取或非擷取|  
|------------------------|-------------------------------|  
|[相符子運算式](#matched_subexpression)|擷取|  
|[具名的相符子運算式](#named_matched_subexpression)|擷取|  
|[平衡群組定義](#balancing_group_definition)|擷取|  
|[非擷取群組](#noncapturing_group)|非擷取|  
|[群組選項](#group_options)|非擷取|  
|[零寬度右合樣 (Positive Lookahead) 判斷提示](#zerowidth_positive_lookahead_assertion)|非擷取|  
|[零寬度右不合樣 (Negative Lookahead) 判斷提示](#zerowidth_negative_lookahead_assertion)|非擷取|  
|[零寬度左合樣 (Positive Lookbehind) 判斷提示](#zerowidth_positive_lookbehind_assertion)|非擷取|  
|[零寬度左不合樣 (Negative Lookbehind) 判斷提示](#zerowidth_negative_lookbehind_assertion)|非擷取|  
|[不可部分完成的群組](#atomic_groups)|非擷取|  
  
 如需群組和正則運算式物件模型的詳細資訊，請參閱 [群組結構和正則運算式物件](#Objects)。  
  
<a name="matched_subexpression"></a>
## <a name="matched-subexpressions"></a>相符子運算式  
 下列分組建構會擷取相符子運算式：  
  
  subexpression`(`  `)`  
  
 其中 *subexpression* 是任何有效的規則運算式模式。 使用括號的擷取會依據規則運算式中的左括號順序，從一開始，由左至右自動編號。 編號零的擷取是整個規則運算式模式比對的文字。  
  
> [!NOTE]
> 依預設， `(` *子運算式* `)` 語言專案會捕捉相符的子運算式。 但是如果規則運算式模式比對方法的 <xref:System.Text.RegularExpressions.RegexOptions> 參數包含 <xref:System.Text.RegularExpressions.RegexOptions.ExplicitCapture?displayProperty=nameWithType> 旗標，或這個子運算式套用了 `n` 選項 (請參閱本主題稍後的[群組選項](#group_options))，則不會擷取相符的子運算式。  
  
 您可以用四種方式來存取擷取群組：  
  
- 在規則運算式中使用反向參考建構。 使用語法編號，在相同的正則運算式中參考相符的子運算式 `\` **，其中 *number* 是所捕獲之子運算式的序號。  
  
- 在規則運算式中使用具名的反向參考建構。 在相同的正則運算式中，使用語法名稱來參考相符的子運算式， `\k<` *name* `>` 其中 *name* 是捕捉群組的名稱或 `\k<` *數位* `>` ，其中 *number* 是捕捉群組的序數。 擷取群組的預設名稱與其序號相同。 如需詳細資訊，請參閱本主題稍後的 [具名的相符子運算式](#named_matched_subexpression) 。  
  
- 在 <xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=nameWithType> 或 <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=nameWithType> 方法呼叫中使用 `$`*number* 取代序列，其中 *number* 是所擷取子運算式的序號。  
  
- 以程式設計方式，使用 <xref:System.Text.RegularExpressions.GroupCollection> 屬性傳回的 <xref:System.Text.RegularExpressions.Match.Groups%2A?displayProperty=nameWithType> 物件。 集合中位置為零的成員代表整個規則運算式相符。 每個後續成員各代表一個相符子運算式。 如需詳細資訊，請參閱 [Grouping Constructs and Regular Expression Objects](#Objects) 一節。  
  
 下列範例說明可識別文字中重複文字的規則運算式。 規則運算式模式的兩個擷取群組代表重複文字的兩個執行個體。 擷取第二個執行個體是為了報告其於輸入字串中的開始位置。  
  
 [!code-csharp[RegularExpressions.Language.Grouping#1](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.grouping/cs/grouping1.cs#1)]
 [!code-vb[RegularExpressions.Language.Grouping#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.grouping/vb/grouping1.vb#1)]  
  
 規則運算式模式如下：  
  
`(\w+)\s(\1)\W`  
  
 下表顯示規則運算式模式的解譯方式。  
  
|模式|描述|  
|-------------|-----------------|  
|`(\w+)`|比對一個或多個文字字元。 這是第一個擷取群組。|  
|`\s`|比對空白字元。|  
|`(\1)`|比對第一個擷取群組中的字串。 這是第二個擷取群組。 此範例將其指派給擷取的群組，以便從 `Match.Index` 物件。|  
|`\W`|比對非文字字元，包括空格和標點符號。 如此可防止規則運算式模式比對以第一個擷取群組中的文字為開頭的文字。|  
  
<a name="named_matched_subexpression"></a>
## <a name="named-matched-subexpressions"></a>具名的相符子運算式  
 下列分組建構會擷取相符子運算式，並可讓您依名稱或依號碼加以存取。  
  
`(?<name>subexpression)`  
  
 或者：  
  
`(?'name'subexpression)`  
  
 其中 *name* 是有效的群組名稱，而 *subexpression* 是任何有效的規則運算式模式。 *name* 絕不能包含任何標點符號字元，而且不能以數字開頭。  
  
> [!NOTE]
> 如果規則運算式模式比對方法的 <xref:System.Text.RegularExpressions.RegexOptions> 參數包含 <xref:System.Text.RegularExpressions.RegexOptions.ExplicitCapture?displayProperty=nameWithType> 旗標，或這個子運算式套用了 `n` 選項 (請參閱本主題稍後的[群組選項](#group_options))，則擷取子運算式的唯一方式就是明確地為擷取群組命名。  
  
 您可以用下列方式來存取具名的擷取群組：  
  
- 在規則運算式中使用具名的反向參考建構。 使用語法名稱，在相同的正則運算式中參考相符的子運算式 `\k<` *name* `>` ，其中 *name* 是所捕獲之子運算式的名稱。  
  
- 在規則運算式中使用反向參考建構。 使用語法編號，在相同的正則運算式中參考相符的子運算式 `\` **，其中 *number* 是所捕獲之子運算式的序號。 具名的相符子運算式會在相符子運算式之後，由左至右連續編號。  
  
- `${` *name* `}` 在或方法呼叫中使用名稱取代 <xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=nameWithType> 順序 <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=nameWithType> ，其中 *name* 是所捕獲之子運算式的名稱。  
  
- 在 <xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=nameWithType> 或 <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=nameWithType> 方法呼叫中使用 `$`*number* 取代序列，其中 *number* 是所擷取子運算式的序號。  
  
- 以程式設計方式，使用 <xref:System.Text.RegularExpressions.GroupCollection> 屬性傳回的 <xref:System.Text.RegularExpressions.Match.Groups%2A?displayProperty=nameWithType> 物件。 集合中位置為零的成員代表整個規則運算式相符。 每個後續成員各代表一個相符子運算式。 具名的擷取群組儲存在集合中，編號的擷取群組之後。  
  
- 以程式設計方式，提供子運算式名稱給 <xref:System.Text.RegularExpressions.GroupCollection> 物件的索引子 (在 C# 中) 或其 <xref:System.Text.RegularExpressions.GroupCollection.Item%2A> 屬性 (在 Visual Basic 中)。  
  
 有一個簡單的規則運算式模式，說明如何以程式設計方式，或是使用規則運算式語言語法，來參考編號 (未具名) 和具名群組。 規則運算式 `((?<One>abc)\d+)?(?<Two>xyz)(.*)` 會依號碼或依名稱產生下列擷取群組。 第一個擷取群組 (編號 0) 一律參考整個模式。  
  
|數字|名稱|模式|  
|------------|----------|-------------|  
|0|0 (預設名稱)|`((?<One>abc)\d+)?(?<Two>xyz)(.*)`|  
|1|1 (預設名稱)|`((?<One>abc)\d+)`|  
|2|2 (預設名稱)|`(.*)`|  
|3|一個|`(?<One>abc)`|  
|4|兩個|`(?<Two>xyz)`|  
  
 下列範例說明的規則運算式可識別重複文字，以及緊接在每個重複文字後面的文字。 規則運算式模式會定義兩個具名子運算式： `duplicateWord`代表重複文字，而 `nextWord`代表接在重複文字後面的文字。  
  
 [!code-csharp[RegularExpressions.Language.Grouping#2](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.grouping/cs/grouping2.cs#2)]
 [!code-vb[RegularExpressions.Language.Grouping#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.grouping/vb/grouping2.vb#2)]  
  
 規則運算式模式如下：  
  
`(?<duplicateWord>\w+)\s\k<duplicateWord>\W(?<nextWord>\w+)`  
  
 下表顯示規則運算式的解譯方式。  
  
|模式|描述|  
|-------------|-----------------|  
|`(?<duplicateWord>\w+)`|比對一個或多個文字字元。 將此擷取群組命名為 `duplicateWord`。|  
|`\s`|比對空白字元。|  
|`\k<duplicateWord>`|從名為 `duplicateWord`的擷取群組比對字串。|  
|`\W`|比對非文字字元，包括空格和標點符號。 如此可防止規則運算式模式比對以第一個擷取群組中的文字為開頭的文字。|  
|`(?<nextWord>\w+)`|比對一個或多個文字字元。 將此擷取群組命名為 `nextWord`。|  
  
 請注意可以在規則運算式中重複群組名稱。 例如，可能會有多於一個群組命名為 `digit`，如下列範例所示。 對於重複名稱的案例， <xref:System.Text.RegularExpressions.Group> 物件的值取決於輸入字串中的最後一個成功擷取。 此外，將每個擷取的相關資訊填入 <xref:System.Text.RegularExpressions.CaptureCollection> ，就如同群組名稱不重複的情況。  
  
 在下列範例中，規則運算式 `\D+(?<digit>\d+)\D+(?<digit>\d+)?` 包含兩次出現名為 `digit` 的群組。 第一個 `digit` 具名群組擷取一或多個數字字元。 第二個 `digit` 具名群組擷取一或多個數字字元的零次或一次發生。 如範例的輸出所示，如果第二個擷取群組成功地與文字相符，該文字的值會定義 <xref:System.Text.RegularExpressions.Group> 物件的值。 如果第二個擷取群組不符合輸入的字串，則上一次成功比對的值會定義 <xref:System.Text.RegularExpressions.Group> 物件的數值。  
  
 [!code-csharp[RegularExpressions.Language.Grouping#12](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.grouping/cs/duplicate1.cs#12)]
 [!code-vb[RegularExpressions.Language.Grouping#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.grouping/vb/duplicate1.vb#12)]  
  
 下表顯示規則運算式的解譯方式。  
  
|模式|描述|  
|-------------|-----------------|  
|`\D+`|比對一個或更多非十進位數字字元。|  
|`(?<digit>\d+)`|比對一個或更多十進位數字字元。 指派 `digit` 具名群組的比對。|  
|`\D+`|比對一個或更多非十進位數字字元。|  
|`(?<digit>\d+)?`|比對一或多個十進位數字字元的零次或一次發生。 指派 `digit` 具名群組的比對。|  
  
<a name="balancing_group_definition"></a>
## <a name="balancing-group-definitions"></a>平衡群組定義  
 平衡群組定義會刪除先前定義之群組的定義，並且在目前群組中儲存先前定義的群組與目前群組之間的間隔。 此分組建構的格式如下：  
  
`(?<name1-name2>subexpression)`  
  
 或者：  
  
`(?'name1-name2' subexpression)`
  
 其中 *name1* 是目前群組 (選用)， *name2* 是先前定義的群組，而 *subexpression* 是任何有效的規則運算式模式。 平衡群組定義會刪除 *name2* 的定義，並且將 *name2* 與 *name1* 之間的間隔儲存在 *name1* 中。 如果沒有定義 *name2* 群組，比對結果會回溯。 因為刪除 *name2* 的最後一個定義會顯示 *name2* 的上一個定義，所以此建構可讓您將擷取堆疊用於群組 *name2*，以作為追蹤巢狀建構 (例如圓括弧或左右方括弧) 的計數器。  
  
 平衡群組定義將 *name2* 當作堆疊使用。 每個巢狀建構的開頭字元都會放在群組及其 <xref:System.Text.RegularExpressions.Group.Captures%2A?displayProperty=nameWithType> 集合中。 找到配對的結尾字元時，就會從群組中移除其對應的開頭字元，而 <xref:System.Text.RegularExpressions.Group.Captures%2A> 集合中就會減少一個。 所有巢狀建構的開頭和結尾字元都配成對之後，*name2* 就空了。  
  
> [!NOTE]
> 在您修改下列範例中的規則運算式來使用巢狀建構的適當開頭和結尾字元之後，即可用它來處理大部分的巢狀建構，例如包含多個巢狀方法呼叫的數學運算式或程式碼字行。  
  
 下列範例使用平衡群組定義來比對輸入字串中的左右角括號 (<>)。 此範例定義兩個具名群組 `Open` 和 `Close`，像堆疊一樣可用來追蹤成對的角括號。 所擷取的每個左角括號都會被推送至 `Open` 群組的擷取集合中，而所擷取的每個右角括號都會被推送至 `Close` 群組的擷取集合中。 平衡群組定義可確保每個左角括號都有成對的右角括號。 如果沒有，唯有當 `(?(Open)(?!))`群組不是空的 (而因此如果所有巢狀建構都未關閉)，才會評估最後的子模式 `Open` 。 如果評估最後的子模式，比對會失敗，因為 `(?!)` 子模式是一律會失敗的零寬度右不合樣 (Negative Lookahead) 判斷提示。  
  
 [!code-csharp[RegularExpressions.Language.Grouping#3](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.grouping/cs/grouping3.cs#3)]
 [!code-vb[RegularExpressions.Language.Grouping#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.grouping/vb/grouping3.vb#3)]  
  
 規則運算式模式為：  
  
`^[^<>]*(((?'Open'<)[^<>]*)+((?'Close-Open'>)[^<>]*)+)*(?(Open)(?!))$`  
  
 規則運算式解譯如下：  
  
|模式|描述|  
|-------------|-----------------|  
|`^`|從字串開頭開始。|  
|`[^<>]*`|比對非左右角括號的零或多個字元。|  
|`(?'Open'<)`|比對左角括號，並將其指派給名為 `Open`的群組。|  
|`[^<>]*`|比對非左右角括號的零或多個字元。|  
|`((?'Open'<)[^<>]*)+`|比對出現一或數次、後面接零或多個非左右角括號字元的左角括號。 這是第二個擷取群組。|  
|`(?'Close-Open'>)`|比對右角括號，將 `Open` 群組與目前群組之間的子字串指派給 `Close` 群組，並刪除 `Open` 群組的定義。|  
|`[^<>]*`|比對出現零或數次、非左右角括號的任何字元。|  
|`((?'Close-Open'>)[^<>]*)+`|比對出現一或數次、後接零或多個非左右角括號字元的右角括號。 比對右角括號時，將 `Open` 群組與目前群組之間的子字串指派給 `Close` 群組，並刪除 `Open` 群組的定義。 這是第三個擷取群組。|  
|`(((?'Open'<)[^<>]*)+((?'Close-Open'>)[^<>]*)+)*`|比對出現零或數次的下列模式：出現一或數次的左角括號，後接零或多個非角括號字元，後接出現一或數次的右角括號，後接出現零或數次的非角括號。 比對右角括號時，刪除 `Open` 群組的定義，並將 `Open` 群組與目前群組之間的子字串指派給 `Close` 群組。 這是第一個擷取群組。|  
|`(?(Open)(?!))`|如果 `Open` 群組存在，若可以比對空字串，則放棄比對，但不要將字串中的規則運算式引擎的位置向前移動。 這是零寬度右不合樣 (Negative Lookahead) 判斷提示。 因為空字串一律以隱含方式存在於輸入字串中，所以此比對一定會失敗。 此比對失敗表示角括號不平衡。|  
|`$`|比對輸入字串的結尾。|  
  
 最後的子運算式 `(?(Open)(?!))` 指出輸入字串中的巢狀建構是否正確平衡 (例如，是否每個左角括號都有配對的右角括號)。 其依據有效的擷取群組進行條件式比對；如需詳細資訊，請參閱 [Alternation Constructs](alternation-constructs-in-regular-expressions.md)。 如果已定義 `Open` 群組，規則運算式引擎會嘗試比對輸入字串中的子運算式 `(?!)` 。 唯有當巢狀建構不平衡時，才應定義 `Open` 群組。 因此，要在輸入字串中比對的模式，應該是一律導致比對失敗的模式。 在這個情況下，`(?!)` 是一律失敗的零寬度右不合樣 (Negative Lookahead) 判斷提示，因為空字串一律以隱含方式存在於輸入字串中。  
  
 在這個範例中，規則運算式引擎會評估輸入字串 "\<abc><mno\<xyz>>"，如下表所示。  
  
|步驟|模式|結果|  
|----------|-------------|------------|  
|1|`^`|從輸入字串的開頭開始比對。|  
|2|`[^<>]*`|在左角括號之前尋找非角括號字元；沒有找到配對。|  
|3|`(((?'Open'<)`|比對 "\<abc>" 中的左角括弧，並將其指派給 `Open` 群組。|  
|4|`[^<>]*`|比對 "abc"。|  
|5|`)+`|"<abc" 是第二個擷取群組的值。<br /><br /> 輸入字串中的下一個字元不是左角括號，所以規則運算式引擎未回送至 `(?'Open'<)[^<>]*)` 子模式。|  
|6|`((?'Close-Open'>)`|比對 "\<abc>" 中的右角括弧，將 "abc" (`Open` 群組與右角括弧之間的子字串) 指派給 `Close` 群組，並刪除 `Open` 群組的目前值 ("<")，使其空白。|  
|7|`[^<>]*`|在右角括號之後尋找非角括號字元；沒有找到配對。|  
|8|`)+`|第三個擷取群組的值是 ">"。<br /><br /> 輸入字串中的下一個字元不是右角括號，所以規則運算式引擎未回送至 `((?'Close-Open'>)[^<>]*)` 子模式。|  
|9|`)*`|第一個擷取群組的值是 "\<abc>"。<br /><br /> 輸入字串中的下一個字元是左角括號，所以規則運算式引擎會回送至 `(((?'Open'<)` 子模式。|  
|10|`(((?'Open'<)`|符合「集合中的左角括弧 \<mno" and assigns it to the `Open` group. Its <xref:System.Text.RegularExpressions.Group.Captures%2A?displayProperty=nameWithType> 現在具有單一值」，「<」。|  
|11|`[^<>]*`|比對 "mno"。|  
|12|`)+`|"<mno" 是第二個擷取群組的值。<br /><br /> 輸入字串中的下一個字元是左角括號，所以規則運算式引擎會回送至 `(?'Open'<)[^<>]*)` 子模式。|  
|13|`(((?'Open'<)`|比對 "\<xyz>" 中的左角括弧，並將其指派給 `Open` 群組。 <xref:System.Text.RegularExpressions.Group.Captures%2A?displayProperty=nameWithType>群組的集合 `Open` 現在包含兩個捕獲： "" 中的左角括弧 \<mno", and the left angle bracket from "\<xyz> 。|  
|14|`[^<>]*`|比對 "xyz"。|  
|15|`)+`|"<xyz" 是第二個擷取群組的值。<br /><br /> 輸入字串中的下一個字元不是左角括號，所以規則運算式引擎未回送至 `(?'Open'<)[^<>]*)` 子模式。|  
|16|`((?'Close-Open'>)`|比對 "\<xyz>" 中的右角括弧。 "xyz"，將 `Open` 群組與右角括弧之間的子字串指派給 `Close` 群組，並刪除 `Open` 群組目前的值。 先前的 capture (值：「群組的集合中的左角括弧 \<mno") becomes the current value of the `Open` group. The <xref:System.Text.RegularExpressions.Group.Captures%2A> `Open` 現在包含單一捕獲，也就是 "" 的左角括弧 \<xyz> 。|  
|17|`[^<>]*`|尋找非角括號字元；沒有找到配對。|  
|18|`)+`|第三個擷取群組的值是 ">"。<br /><br /> 輸入字串中的下一個字元是右角括號，所以規則運算式引擎會回送至 `((?'Close-Open'>)[^<>]*)` 子模式。|  
|19|`((?'Close-Open'>)`|比對 "xyz>>" 中的最後一個右角括弧，將 "mno\<xyz>" (`Open` 群組與右角括弧之間的子字串) 指派給 `Close` 群組，並刪除 `Open` 群組的目前值。 `Open` 群組現在是空的。|  
|20|`[^<>]*`|尋找非角括號字元；沒有找到配對。|  
|21|`)+`|第三個擷取群組的值是 ">"。<br /><br /> 輸入字串中的下一個字元不是右角括號，所以規則運算式引擎未回送至 `((?'Close-Open'>)[^<>]*)` 子模式。|  
|22|`)*`|第一個擷取群組的值是 "<mno\<xyz>>"。<br /><br /> 輸入字串中的下一個字元不是左角括號，所以規則運算式引擎未回送至 `(((?'Open'<)` 子模式。|  
|23|`(?(Open)(?!))`|`Open` 群組未定義，所以未嘗試任何比對。|  
|24|`$`|比對輸入字串的結尾。|  
  
<a name="noncapturing_group"></a>
## <a name="noncapturing-groups"></a>非擷取群組  
 下列分組建構不會擷取由下列子運算式比對的子字串：  
  
`(?:subexpression)`
  
 其中 *subexpression* 是任何有效的規則運算式模式。 將數量詞套用至群組時，通常會使用非擷取分組建構，但是群組擷取的子字串沒有用。  
  
> [!NOTE]
> 如果規則運算式包含巢狀分組建構，則外部非擷取分組建構不會套用至內部巢狀分組建構。  
  
 下列範例說明包含非擷取群組的規則運算式。 請注意，輸出沒有包含任何擷取群組。  
  
 [!code-csharp[RegularExpressions.Language.Grouping#5](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.grouping/cs/noncapture1.cs#5)]
 [!code-vb[RegularExpressions.Language.Grouping#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.grouping/vb/noncapture1.vb#5)]  
  
 規則運算式 `(?:\b(?:\w+)\W*)+\.` 符合以句點終止的句子。 因為規則運算式著重在句子，而不是個別文字，所以分組建構只會用做數量詞。 規則運算式模式的解譯方式如下表所示。  
  
|模式|描述|  
|-------------|-----------------|  
|`\b`|開始字緣比對。|  
|`(?:\w+)`|比對一個或多個文字字元。 請勿將相符的文字指派給擷取群組。|  
|`\W*`|比對零或多個非文字字元。|  
|`(?:\b(?:\w+)\W*)+`|比對下列模式一次或多次：以字邊界開頭的一或多個文字字元，後面接零或多個非文字字元。 請勿將相符的文字指派給擷取群組。|  
|`\.`|比對句點。|  
  
<a name="group_options"></a>
## <a name="group-options"></a>群組選項  
 下列群組建構會在子運算式中套用或停用指定的選項：  
  
  subexpression`(?imnsx-imnsx:`  `)`  
  
 其中 *subexpression* 是任何有效的規則運算式模式。 例如，`(?i-s:)` 會開啟不區分大小寫，並停用單行模式。 如需您可以指定之內嵌選項的詳細資訊，請參閱 [正則運算式選項](regular-expression-options.md)。  
  
> [!NOTE]
> 若要將指定的選項套用至整個規則運算式，而不是單一子運算式，您可以使用 <xref:System.Text.RegularExpressions.Regex?displayProperty=nameWithType> 類別建構函式或靜態方法。 您也可以使用 `(?imnsx-imnsx)` 語言建構，以指定在規則運算式的特定點之後，套用內嵌選項。  
  
 群組選項建構不是擷取群組。 也就是說，雖然 *subexpression* 擷取之字串的任何部分都會包含在比對中，但不會包含在擷取群組中，也不會用來填入 <xref:System.Text.RegularExpressions.GroupCollection> 物件。  
  
 例如，下列範例中的規則運算式 `\b(?ix: d \w+)\s` 在分組建構中使用內嵌選項，來啟用不區分大小寫的比對，並會在識別以字母 "d" 開頭的所有字組時，忽略模式空白字元。 規則運算式的定義如下表所示。  
  
|模式|描述|  
|-------------|-----------------|  
|`\b`|開始字緣比對。|  
|`(?ix: d \w+)`|使用不區分大小寫比對，並忽略此模式中的空格，比對後面接一或多個文字字元的 "d"。|  
|`\s`|比對空白字元。|  
  
 [!code-csharp[Conceptual.Regex.Language.Options#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.options/cs/example1.cs#8)]
 [!code-vb[Conceptual.Regex.Language.Options#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.options/vb/example1.vb#8)]  
  
<a name="zerowidth_positive_lookahead_assertion"></a>
## <a name="zero-width-positive-lookahead-assertions"></a>零寬度右合樣 (Positive Lookahead) 判斷提示  
 下列群組建構可定義零寬度右合樣 (Positive Lookahead) 判斷提示：  
  
  subexpression`(?=`  `)`  
  
 其中 *subexpression* 是任何規則運算式模式。 若要讓比對成功，輸入字串必須符合 *subexpression* 中的規則運算式模式，但是相符的子字串不會包含在比對結果中。 零寬度右合樣 (Positive Lookahead) 判斷提示不會回溯。  
  
 通常會在規則運算式模式結尾找到零寬度右合樣 (Positive Lookahead) 判斷提示。 它會定義必須在字串結尾找到，以讓相符項出現的子字串，但不應包含在比對中。 防止過度回溯也很有用。 您可以使用零寬度右合樣 (Positive Lookahead) 判斷提示，以確保特定擷取群組的開頭文字，符合針對該擷取群組所定義的模式子集。 例如，如果擷取群組符合連續的文字字元，您就可以使用零寬度右合樣 (Positive Lookahead) 判斷提示，要求第一個字元為英文字母大寫字元。  
  
 下列範例使用以零寬度右合樣判斷提示，比對輸入字串中在動詞 "is" 之前的字組。  
  
 [!code-csharp[RegularExpressions.Language.Grouping#6](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.grouping/cs/lookahead1.cs#6)]
 [!code-vb[RegularExpressions.Language.Grouping#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.grouping/vb/lookahead1.vb#6)]  
  
 規則運算式 `\b\w+(?=\sis\b)` 的解譯方式如下表所示。  
  
|模式|描述|  
|-------------|-----------------|  
|`\b`|開始字緣比對。|  
|`\w+`|比對一個或多個文字字元。|  
|`(?=\sis\b)`|判定文字字元後面是否接著空格字元和字串 "is"，在字邊界結束。 若是如此，比對將會成功。|  
  
<a name="zerowidth_negative_lookahead_assertion"></a>
## <a name="zero-width-negative-lookahead-assertions"></a>零寬度右不合樣 (Negative Lookahead) 判斷提示  
 下列群組建構可定義零寬度右不合樣 (Negative Lookahead) 判斷提示：  
  
  subexpression`(?!`  `)`  
  
 其中 *subexpression* 是任何規則運算式模式。 為了若要讓比對成功，輸入字串絕不能符合 *subexpression* 中的規則運算式模式，但是相符的字串不會包含在比對結果中。  
  
 零寬度右不合樣 (Negative Lookahead) 判斷提示通常會用在規則運算式開頭或結尾。 若是在規則運算式開頭，當規則運算式開頭定義類似但較為廣泛的模式以供比對時，此判斷提示可定義不應相符的模式。 在此情況下，通常是用來限制回溯。 若是在規則運算式結尾，則可定義不能出現在相符項結尾的子運算式。  
  
 下列範例定義的規則運算式在規則運算式開頭使用零寬度右合樣判斷提示，以比對不是以 "un" 開頭的文字。  
  
 [!code-csharp[RegularExpressions.Language.Grouping#7](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.grouping/cs/negativelookahead1.cs#7)]
 [!code-vb[RegularExpressions.Language.Grouping#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.grouping/vb/negativelookahead1.vb#7)]  
  
 規則運算式 `\b(?!un)\w+\b` 的解譯方式如下表所示。  
  
|模式|描述|  
|-------------|-----------------|  
|`\b`|開始字緣比對。|  
|`(?!un)`|判斷下兩個字元是否為 "un"。 如果不是，才可能比對。|  
|`\w+`|比對一個或多個文字字元。|  
|`\b`|結束字緣比對。|  
  
 下列範例定義的規則運算式在規則運算式結尾使用零寬度右合樣判斷提示，以比對不是以標點符號字元結尾的文字。  
  
 [!code-csharp[RegularExpressions.Language.Grouping#8](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.grouping/cs/negativelookahead2.cs#8)]
 [!code-vb[RegularExpressions.Language.Grouping#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.grouping/vb/negativelookahead2.vb#8)]  
  
 規則運算式 `\b\w+\b(?!\p{P})` 的解譯方式如下表所示。  
  
|模式|描述|  
|-------------|-----------------|  
|`\b`|開始字緣比對。|  
|`\w+`|比對一個或多個文字字元。|  
|`\b`|結束字緣比對。|  
|`\p{P})`|如果下一個字元不是標點符號 (例如句點或逗號)，則比對成功。|  
  
<a name="zerowidth_positive_lookbehind_assertion"></a>
## <a name="zero-width-positive-lookbehind-assertions"></a>零寬度左合樣 (Positive Lookbehind) 判斷提示  
 下列群組建構可定義零寬度左合樣 (Positive Lookbehind) 判斷提示：  
  
  subexpression`(?<=`  `)`  
  
 其中 *subexpression* 是任何規則運算式模式。 若要讓比對成功， *subexpression* 必須出現在目前位置左邊的輸入字串中，但是 `subexpression` 不會包含在比對結果中。 零寬度左合樣 (Positive Lookbehind) 判斷提示不會回溯。  
  
 零寬度左合樣 (Positive Lookbehind) 判斷提示通常會用在規則運算式開頭。 其定義的模式是比對的前置條件，但不包含在比對結果中。  
  
 例如，下列範例會比對 21 世紀年份的後兩位數 (也就是說，比對的字串前面需要有數字 "20")。  
  
 [!code-csharp[RegularExpressions.Language.Grouping#9](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.grouping/cs/lookbehind1.cs#9)]
 [!code-vb[RegularExpressions.Language.Grouping#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.grouping/vb/lookbehind1.vb#9)]  
  
 規則運算式模式 `(?<=\b20)\d{2}\b` 的解譯方式如下表所示。  
  
|模式|描述|  
|-------------|-----------------|  
|`\d{2}`|比對兩個十進位數字。|  
|`(?<=\b20)`|如果字邊界上的兩個十進位數字前置十進位數字 "20"，則繼續比對。|  
|`\b`|結束字緣比對。|  
  
 當擷取群組中的最後一或多個字元，必須是符合該群組規則運算式模式的字元子集時，零寬度左合樣 (Positive Lookbehind) 判斷提示也可以用來限制回溯。 例如，如果群組擷取所有連續的文字字元，您就可以使用零寬度左合樣 (Positive Lookbehind) 判斷提示，要求最後一個字元為英文字母。  
  
<a name="zerowidth_negative_lookbehind_assertion"></a>
## <a name="zero-width-negative-lookbehind-assertions"></a>零寬度左不合樣 (Negative Lookbehind) 判斷提示  
 下列分組建構可定義零寬度左不合樣 (Negative Lookbehind) 判斷提示：  
  
  subexpression`(?<!`  `)`  
  
 其中 *subexpression* 是任何規則運算式模式。 若要讓比對成功，*subexpression* 絕不能出現在目前位置左邊的輸入字串中。 不過，不符合 `subexpression` 的任何子字串都不會包含在比對結果中。  
  
 零寬度左不合樣 (Negative Lookbehind) 判斷提示通常會用在規則運算式開頭。 其定義的模式排除了後面字串中的比對。 當擷取群組中的最後一或多個字元，絕不能是符合該群組規則運算式模式的一或多個字元時，此判斷提示也可以用來限制回溯。 例如，如果群組擷取所有連續的文字字元，您就可以使用零寬度左合樣 (Positive Lookbehind) 判斷提示，要求最後一個字元不能是底線 (\_)。  
  
 下列範例會比對週間非週末 (不是星期六也不是星期日) 任何一天的日期。  
  
 [!code-csharp[RegularExpressions.Language.Grouping#10](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.grouping/cs/negativelookbehind1.cs#10)]
 [!code-vb[RegularExpressions.Language.Grouping#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.grouping/vb/negativelookbehind1.vb#10)]  
  
 規則運算式模式 `(?<!(Saturday|Sunday) )\b\w+ \d{1,2}, \d{4}\b` 的解譯方式如下表所示。  
  
|模式|描述|  
|-------------|-----------------|  
|`\b`|開始字緣比對。|  
|`\w+`|比對後接空格字元的一或多個文字字元。|  
|`\d{1,2},`|比對後接空格字元和逗號的一或兩個十進位數。|  
|`\d{4}\b`|比對四個十進位數，並且在字邊界上結束比對。|  
|<code>(?<!(Saturday&#124;Sunday) )</code>|如果比對項目前置文字不是後接空格的字串 "Saturday" 或 "Sunday"，則比對成功。|  
  
<a name="atomic_groups"></a>
## <a name="atomic-groups"></a>不可部分完成的群組  
 下列群組結構表示不可部分完成的群組 (在某些其他正則運算式引擎中已知為非回溯子運算式、不可部分完成子運算式或僅限一次的子運算式) ：
  
  subexpression`(?>`  `)`  
  
 其中 *subexpression* 是任何規則運算式模式。  
  
 一般而言，如果規則運算式包含選用性或替代性比對模式，而比對未成功，規則運算式引擎可以分支在多個方向，將輸入字串與模式比對。 如果採用第一個分支時，沒有找到比對項目，規則運算式引擎可以備份或回溯至採用第一個比對項目的點，並嘗試使用第二個分支來比對。 此程序可以一直持續到所有分支都試過為止。  
  
 `(?>`*子運算式* `)` 語言結構會停用回溯。 規則運算式引擎會盡可能比對輸入字串中的所有字元。 如果已無法進一步比對，將不會回溯嘗試替代模式比對。 (也就是說，子運算式只會比對該子運算式單獨比對的字串，而不會嘗試依據子運算式和其後的任何子運算式來比對字串。)  
  
 如果您知道回溯會成功，則建議使用此選項。 防止規則運算式引擎執行不必要的搜尋，以提升效能。  
  
 下列範例說明不可部分完成的群組如何修改模式比對的結果。 回溯規則運算式成功比對一連串重複的字元，其後面接著字邊界上出現一或多次的相同字元，而非回溯規則運算式則不成功。  
  
 [!code-csharp[RegularExpressions.Language.Grouping#11](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.grouping/cs/nonbacktracking1.cs#11)]
 [!code-vb[RegularExpressions.Language.Grouping#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.grouping/vb/nonbacktracking1.vb#11)]  
  
 非回溯規則運算式 `(?>(\w)\1+).\b` 的定義如下表所示。  
  
|模式|描述|  
|-------------|-----------------|  
|`(\w)`|比對單一文字字元，並將其指派給第一個擷取群組。|  
|`\1+`|比對第一個擷取子字串的值一或數次。|  
|`.`|比對任何字元。|  
|`\b`|結束字邊界比對。|  
|`(?>(\w)\1+)`|比對出現一或數次的重複文字字元，但不要回溯比對字邊界上的最後一個字元。|  
  
<a name="Objects"></a>
## <a name="grouping-constructs-and-regular-expression-objects"></a>群組建構和規則運算式物件  
 規則運算式擷取群組所比對的子字串會以 <xref:System.Text.RegularExpressions.Group?displayProperty=nameWithType> 物件來代表，此物件可從 <xref:System.Text.RegularExpressions.GroupCollection?displayProperty=nameWithType> 屬性傳回的 <xref:System.Text.RegularExpressions.Match.Groups%2A?displayProperty=nameWithType> 物件來擷取。 <xref:System.Text.RegularExpressions.GroupCollection> 物件的填入方式如下：  
  
- 集合中的第一個 <xref:System.Text.RegularExpressions.Group> 物件 (索引位置為零的物件) 代表整個比對。  
  
- 下一個 <xref:System.Text.RegularExpressions.Group> 物件組合代表未具名 (編號的) 擷取群組。 其出現順序會依照規則運算式中定義的順序，由左至右。 這些群組的索引值範圍是從 1 到集合中未具名擷取群組的編號。 (特定群組的索引同等於其編號的反向參考。 如需反向參考的詳細資訊，請參閱 [Backreference Constructs](backreference-constructs-in-regular-expressions.md)。)  
  
- 最後一個 <xref:System.Text.RegularExpressions.Group> 物件組合代表具名擷取群組。 其出現順序會依照規則運算式中定義的順序，由左至右。 第一個具名擷取群組的索引值比最後一個未具名擷取群組的索引值大一。 如果規則運算式中沒有未具名擷取群組，則第一個具名擷取群組的索引值為一。  
  
 如果您將數量詞套用至擷取群組，對應之 <xref:System.Text.RegularExpressions.Group> 物件的 <xref:System.Text.RegularExpressions.Capture.Value%2A?displayProperty=nameWithType>、 <xref:System.Text.RegularExpressions.Capture.Index%2A?displayProperty=nameWithType>和 <xref:System.Text.RegularExpressions.Capture.Length%2A?displayProperty=nameWithType> 屬性會反映擷取群組所擷取的最後一個子字串。 您可以擷取由群組所擷取的一組完整子字串，那些群組具有 <xref:System.Text.RegularExpressions.CaptureCollection> 屬性傳回之 <xref:System.Text.RegularExpressions.Group.Captures%2A?displayProperty=nameWithType> 物件中的數量詞。  
  
 下列範例說明 <xref:System.Text.RegularExpressions.Group> 與 <xref:System.Text.RegularExpressions.Capture> 物件之間的關聯性。  
  
 [!code-csharp[RegularExpressions.Language.Grouping#4](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.grouping/cs/objectmodel1.cs#4)]
 [!code-vb[RegularExpressions.Language.Grouping#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.grouping/vb/objectmodel1.vb#4)]  
  
 規則運算式模式 `(\b(\w+)\W+)+` 會從字串擷取個別文字。 其定義方式如下表所示。  
  
|模式|描述|  
|-------------|-----------------|  
|`\b`|開始字緣比對。|  
|`(\w+)`|比對一個或多個文字字元。 這些字元共同構成一個單字。 這是第二個擷取群組。|  
|`\W+`|比對一或多個非文字字元。|  
|`(\b(\w+)\W+)`|一或多次比對一或多個文字字元後面接著一或多個非文字字元的模式。 這是第一個擷取群組。|  
  
 第二個擷取群組會比對句子中的每個字。 第一個擷取群組會比對每個字以及接在該字後面的標點符號和空白字元。 索引為 2 的 <xref:System.Text.RegularExpressions.Group> 物件會提供第二個擷取群組所比對之文字的相關資訊。 您可以從 <xref:System.Text.RegularExpressions.CaptureCollection> 屬性傳回的 <xref:System.Text.RegularExpressions.Group.Captures%2A?displayProperty=nameWithType> 物件取得擷取群組所擷取的一整組文字。  
  
## <a name="see-also"></a>請參閱

- [規則運算式語言 - 快速參考](regular-expression-language-quick-reference.md)
- [回溯](backtracking-in-regular-expressions.md)
