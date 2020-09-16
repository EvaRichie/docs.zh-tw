---
title: 使用 LINQ 轉換資料 (C#)
description: '瞭解如何在 c # 中使用 LINQ 查詢來轉換資料。 您可以使用 select 子句來排序和分組，並建立新的類型，以修改序列。'
ms.date: 07/20/2015
helpviewer_keywords:
- LINQ [C#], data transformations
- source elements [LINQ in C#]
- joining multiple inputs [LINQ in C#]
- multiple outputs for one output sequence [LINQ in C#]
- subset of source elements [LINQ in C#]
- data sources [LINQ in C#], data transformations
- data transformations [LINQ in C#]
ms.assetid: 674eae9e-bc72-4a88-aed3-802b45b25811
ms.openlocfilehash: af08938b6b8f169ded2180529c2b4aadebefef55
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90558806"
---
# <a name="data-transformations-with-linq-c"></a>使用 LINQ 轉換資料 (C#)
 (LINQ) 的語言整合式查詢，不只是要抓取資料。 它也是功能強大的資料轉換工具。 藉由使用 LINQ 查詢，您可以使用來源序列作為輸入，並以許多方式修改它，以建立新的輸出序列。 藉由排序及群組，您可以修改序列本身，而不修改項目本身。 但 LINQ 查詢最強大的功能是能夠建立新的類型。 這是在 [select](../../../language-reference/keywords/select-clause.md) 子句中完成。 例如，您可以進行下列工作：  
  
- 將多個輸入序列合併為具有新類型的單一輸出序列。  
  
- 建立輸出序列，使其項目只包含來源序列中每個項目的一或多個屬性。  
  
- 建立輸出序列，使其項目包含對來源資料執行的作業結果。  
  
- 以不同格式建立輸出序列。 比方說，您可以將資料從 SQL 資料列或文字檔轉換成 XML。  
  
 這些只是一些範例。 當然，這些轉換可以用各種方式結合在相同的查詢中。 此外，一個查詢的輸出序列也可用作新查詢的輸入序列。  
  
## <a name="joining-multiple-inputs-into-one-output-sequence"></a>將多個輸入聯結成一個輸出序列  
 您可以使用 LINQ 查詢來建立包含來自多個輸入序列之元素的輸出序列。 下列範例示範如何結合兩個記憶體中的資料結構，但相同的原則可以套用以合併 XML 或 SQL 或資料集來源的資料。 假設下列兩個類別類型︰  
  
 [!code-csharp[CsLINQGettingStarted#7](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#7)]  
  
 下列範例顯示查詢：  
  
 [!code-csharp[CSLinqGettingStarted#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#8)]  
  
 如需詳細資訊，請參閱 [join 子句](../../../language-reference/keywords/join-clause.md)和 [select 子句](../../../language-reference/keywords/select-clause.md)。  
  
## <a name="selecting-a-subset-of-each-source-element"></a>選取每個來源項目的子集  
 有兩種主要方式，可選取來源序列中每個項目的子集︰  
  
1. 若只要選取來源項目的一個成員，請使用點運算。 在下列範例中，假設 `Customer` 物件包含數個公用屬性，包括名為 `City` 的字串。 在執行時，此查詢會產生字串的輸出序列。  
  
    ```csharp
    var query = from cust in Customers  
                select cust.City;  
    ```  
  
2. 若要建立包含來自來源項目之多個屬性的項目，您可以使用物件初始設定式與具名物件或匿名型別。 下列範例示範如何使用匿名型別封裝來自每個 `Customer` 項目的兩個屬性︰  
  
    ```csharp
    var query = from cust in Customer  
                select new {Name = cust.Name, City = cust.City};  
    ```  
  
 如需詳細資訊，請參閱[物件和集合初始設定式](../../classes-and-structs/object-and-collection-initializers.md)和[匿名型別](../../classes-and-structs/anonymous-types.md)。  
  
## <a name="transforming-in-memory-objects-into-xml"></a>將記憶體中的物件轉換成 XML  
 LINQ 查詢可讓您輕鬆地在記憶體中的資料結構、SQL 資料庫、ADO.NET 資料集和 XML 資料流程或檔之間轉換資料。 下列範例會將記憶體中資料結構的物件轉換成 XML 項目。  
  
 [!code-csharp[CsLINQGettingStarted#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#9)]  
  
 該程式碼會產生下列 XML 輸出：  
  
```xml  
<Root>  
  <student>  
    <First>Svetlana</First>  
    <Last>Omelchenko</Last>  
    <Scores>97,92,81,60</Scores>  
  </student>  
  <student>  
    <First>Claire</First>  
    <Last>O'Donnell</Last>  
    <Scores>75,84,91,39</Scores>  
  </student>  
  <student>  
    <First>Sven</First>  
    <Last>Mortensen</Last>  
    <Scores>88,94,65,91</Scores>  
  </student>  
</Root>  
```  
  
 如需詳細資訊，請參閱[在 C# 中建立 XML 樹狀結構 (LINQ to XML)](../../../../standard/linq/create-xml-trees.md)。  
  
## <a name="performing-operations-on-source-elements"></a>對來源項目執行作業  
 輸出序列可能不會包含來自來源序列的任何項目或項目屬性。 輸出可能會是使用來源項目作為輸入引數而計算的值序列。

 下列查詢會採用一連串的數位來表示圓形的半徑、計算每個半徑的區域，並傳回包含以計算區域格式化之字串的輸出序列。

 輸出序列的每個字串都會使用 [字串插補](../../../language-reference/tokens/interpolated.md)來格式化。 內插字串的 `$` 左引號前面會有一個，而且可以在插入字串內的大括弧內執行作業。 一旦執行這些作業，就會串連結果。
  
> [!NOTE]
> 如果查詢會轉譯成某個其他領域，則不支援在查詢運算式中呼叫方法。 例如，您無法在 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] 呼叫一般 C# 方法，因為 SQL Server 沒有它的內容。 不過，您可以將預存程序對應至方法，並呼叫它們。 如需詳細資訊，請參閱[預存程序](../../../../framework/data/adonet/sql/linq/stored-procedures.md)。  
  
 [!code-csharp[CsLINQGettingStarted#10](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#10)]  
  
## <a name="see-also"></a>另請參閱

- [Language-Integrated Query (LINQ) (C#)](./index.md)
- [LINQ to SQL](../../../../framework/data/adonet/sql/linq/index.md)
- [LINQ to DataSet](../../../../framework/data/adonet/linq-to-dataset.md)
- [LINQ to XML (C#)](../../../../standard/linq/linq-xml-overview.md)
- [LINQ 查詢運算式](../../../linq/index.md)
- [select 子句](../../../language-reference/keywords/select-clause.md)
