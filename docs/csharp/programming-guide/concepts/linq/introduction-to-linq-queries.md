---
title: LINQ 查詢簡介 (C#)
description: LINQ 提供一致的模型來查詢各種資料來源和格式的資料。 在 LINQ 查詢中，您一律會使用物件。
ms.date: 07/20/2015
helpviewer_keywords:
- deferred execution [LINQ]
- LINQ, queries
- LINQ, deferred execution
- queries [LINQ], about LINQ queries
ms.assetid: 37895c02-268c-41d5-be39-f7d936fa88a8
ms.openlocfilehash: ce878dc255d2502f0594626b294393c399c932e5
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87165837"
---
# <a name="introduction-to-linq-queries-c"></a>LINQ 查詢簡介 (C#)
「查詢」** 是指從資料來源中擷取資料的運算式。 查詢通常以特定的查詢語言來表示。 針對各種資料來源類型開發不同的語言已有一段時間，例如用於關聯式資料庫的 SQL，以及用於 XML 的 XQuery。 因此，開發人員在過去必須針對所需支援的每種資料來源類型或資料格式，學習新的查詢語言。 LINQ 藉由提供一致的模型來處理各種資料來源和格式的資料，來簡化這種情況。 在 LINQ 查詢中，您一律會使用物件。 您可以使用相同的基本編碼模式來查詢和轉換 XML 檔、SQL 資料庫、ADO.NET 資料集、.NET 集合，以及可使用 LINQ 提供者的任何其他格式的資料。  
  
## <a name="three-parts-of-a-query-operation"></a>查詢作業的三個部分  
 所有的 LINQ 查詢作業都包含三個不同的動作：  
  
1. 取得資料來源。  
  
2. 建立查詢。  
  
3. 執行查詢。  
  
 下列範例示範查詢作業的三個部分在原始程式碼中的表示方式。 為了方便起見，此範例使用整數陣列作為資料來源；不過，相同的概念也適用於其他資料來源。 本主題的其他部分都會參考此範例。  
  
 [!code-csharp[CsLINQGettingStarted#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#1)]  
  
 下圖顯示完整的查詢作業。 在 LINQ 中，查詢的執行與查詢本身不同。 換句話說，您只要建立查詢變數，就不會取出任何資料。  
  
 ![完整 LINQ 查詢作業的圖表。](./media/introduction-to-linq-queries/linq-query-complete-operation.png)  
  
## <a name="the-data-source"></a>資料來源  
 在上述範例中，因為資料來源來自陣列，意味著其也支援泛型 <xref:System.Collections.Generic.IEnumerable%601> 介面。 這表示它可以使用 LINQ 進行查詢。 查詢會在 `foreach` 陳述式中執行，而 `foreach` 則需要<xref:System.Collections.IEnumerable> 或 <xref:System.Collections.Generic.IEnumerable%601>。 支援 <xref:System.Collections.Generic.IEnumerable%601> 或衍生介面的類型，例如泛型 <xref:System.Linq.IQueryable%601> 稱為*可查詢的類型*。  
  
 可查詢的類型不需要修改或特殊處理，就能做為 LINQ 資料來源。 如果來源資料還不是記憶體中的可查詢型別，LINQ 提供者就必須將其表示為。 例如 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 會將 XML 文件載入可查詢的 <xref:System.Xml.Linq.XElement> 類型：  
  
 [!code-csharp[CsLINQGettingStarted#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#2)]  
  
 在 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] 中，您會先以手動方式或使用[Visual Studio 中的 LINQ to SQL 工具](/visualstudio/data-tools/linq-to-sql-tools-in-visual-studio2)，在設計階段建立物件關聯式對應。 您可以針對物件撰寫查詢，而 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] 則會在執行階段處理與資料庫之間的通訊。 在下列範例中，`Customers` 代表資料庫中特定的資料表，而查詢結果 <xref:System.Linq.IQueryable%601> 的類型則衍生自 <xref:System.Collections.Generic.IEnumerable%601>。  
  
```csharp  
Northwnd db = new Northwnd(@"c:\northwnd.mdf");  
  
// Query for customers in London.  
IQueryable<Customer> custQuery =  
    from cust in db.Customers  
    where cust.City == "London"  
    select cust;  
```  
  
 如需有關如何建立特定資料來源類型的詳細資訊，請參閱各種 LINQ 提供者的檔。 不過，基本規則非常簡單： LINQ 資料來源是支援泛型介面的任何物件 <xref:System.Collections.Generic.IEnumerable%601> ，或繼承自它的介面。  
  
> [!NOTE]
> <xref:System.Collections.ArrayList>支援非泛型介面的類型（例如） <xref:System.Collections.IEnumerable> 也可以當做 LINQ 資料來源使用。 如需詳細資訊，請參閱[如何使用 LINQ 查詢 ArrayList （c #）](./how-to-query-an-arraylist-with-linq.md)。  
  
## <a name="the-query"></a><a name="query"></a>查詢  
 查詢可指定要從一或多個資料來源擷取的資訊。 查詢也可選擇性地指定該項資訊傳回之前應該如何排序、分組和成形。 查詢是儲存在查詢變數中，並以查詢運算式初始化。 為了簡化撰寫查詢的作業，C# 已引進新的查詢語法。  
  
 上述範例中的查詢會傳回整數陣列中的所有偶數。 此查詢運算式包含三個子句︰`from`、`where` 和 `select` （如果您熟悉 SQL，您會注意到，子句的順序會從 SQL 中的順序反轉）。`from`子句會指定資料來源、子句會 `where` 套用篩選準則，而子句會 `select` 指定傳回之元素的類型。 [語言整合式查詢（LINQ）](../../../linq/index.md)一節中會詳細討論這些和其他查詢子句。 現在，重點在於，在 LINQ 中，查詢變數本身不會採取任何動作，也不會傳回任何資料。 它只會儲存稍後執行查詢以產生結果時所需要的資訊。 如需如何在幕後建構查詢的詳細資訊，請參閱[標準查詢運算子概觀 (C#)](./standard-query-operators-overview.md)。  
  
> [!NOTE]
> 查詢也可以使用方法語法來表示。 如需詳細資訊，請參閱 [LINQ 中的查詢語法及方法語法](./query-syntax-and-method-syntax-in-linq.md)。  
  
## <a name="query-execution"></a>查詢執行  
  
### <a name="deferred-execution"></a>延後執行  
 如前所述，查詢變數本身只會儲存查詢命令。 查詢的實際執行必須等到您逐一查看 `foreach` 陳述式中的查詢變數之後才會進行。 此概念稱為「延後執行」**，如下列範例所示：  
  
 [!code-csharp[csLinqGettingStarted#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#4)]  
  
 `foreach` 陳述式也是擷取查詢結果的位置。 例如，在上述查詢中，反覆運算變數 `num` 會保留傳回序列中的每個值 (一次一個)。  
  
 因為查詢變數本身絕不會保留查詢結果，所以您可以視需要多次執行。 例如，您可以擁有會由個別應用程式持續更新的資料庫。 您可以在應用程式中建立一個擷取最新資料的查詢，然後依特定時間間隔反覆執行，每次擷取不同的結果。  
  
### <a name="forcing-immediate-execution"></a>強制立即執行  
 針對某個來源項目範圍執行彙總函式的查詢必須先逐一查看這些項目。 這類查詢的範例包括 `Count`、`Max`、`Average` 和 `First`。 這些查詢執行時並未使用明確的 `foreach` 陳述式，因為查詢本身必須使用 `foreach` 才能傳回結果。 另外也請注意，這些查詢類型傳回的是單一的值，而不是 `IEnumerable` 集合。 下列查詢會傳回來源陣列中的偶數計數：  
  
 [!code-csharp[csLinqGettingStarted#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#5)]  
  
 若要立即強制執行任何查詢，並快取其結果，可以呼叫 <xref:System.Linq.Enumerable.ToList%2A> 或 <xref:System.Linq.Enumerable.ToArray%2A>方法。  
  
 [!code-csharp[csLinqGettingStarted#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#6)]  
  
 您也可以將 `foreach` 迴圈放在緊接著查詢運算式後方的位置，以強制執行查詢。 不過，藉由呼叫 `ToList` 或 `ToArray`，您也可以快取單一集合物件中的所有資料。  
  
## <a name="see-also"></a>另請參閱

- [開始使用 C# 中的 LINQ](index.md)
- [逐步解說：在 C# 中撰寫查詢](./walkthrough-writing-queries-linq.md)
- [語言整合式查詢（LINQ）](../../../linq/index.md)
- [foreach、in](../../../language-reference/keywords/foreach-in.md)
- [查詢關鍵字（LINQ）](../../../language-reference/keywords/query-keywords.md)
