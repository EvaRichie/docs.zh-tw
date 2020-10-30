---
title: 泛型中的共變數和反變數
description: 瞭解共變數（可讓您使用更多衍生型別）和反變數（可讓您在 .NET 泛型中使用較不衍生的型別）。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- generics, covariance and contravariance
- generics, variance
- covariance and contravariance in generics
- generic type parameters
ms.assetid: 2678dc63-c7f9-4590-9ddc-0a4df684d42e
ms.openlocfilehash: 1606238b22bd355b997b54cf94e0c28d16ec5cac
ms.sourcegitcommit: b1442669f1982d3a1cb18ea35b5acfb0fc7d93e4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/30/2020
ms.locfileid: "93063172"
---
# <a name="covariance-and-contravariance-in-generics"></a>泛型中的共變數和反變數

共變數 *和反**變數* 是指使用更多衍生型別的能力 (更明確的) 或較少衍生的類型 (比原先指定更少的特定) 。 泛型類型參數支援共變數和反變數，可在指派和使用泛型類型時提供更大的彈性。

當您指的是類型系統、共變數、反變數和 invariance 時，會有下列定義。 範例中會假設名為 `Base` 的基底類別，以及名為 `Derived`的衍生類別。  
  
- `Covariance`  
  
     可讓您使用比原本指定更多衍生的類型。  
  
     您可以將的實例指派 `IEnumerable<Derived>` 給類型的變數 `IEnumerable<Base>` 。  
  
- `Contravariance`  
  
     可讓您使用比原本所指定更泛型 (較少衍生) 的類型。  
  
     您可以將的實例指派 `Action<Base>` 給類型的變數 `Action<Derived>` 。  
  
- `Invariance`  
  
     表示您只能使用原本指定的型別。 非變異的泛型型別參數不是協變數也不是逆變的。  
  
     您無法將的實例指派 `List<Base>` 給類型的變數，反之亦然 `List<Derived>` 。  
  
 Covariant 型別參數可讓您進行看起來很像一般[多型](../../csharp/programming-guide/classes-and-structs/polymorphism.md)的指派，如下列程式碼所示。  
  
 [!code-csharp[CoContraSimpleIEnum#1](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontrasimpleienum/cs/example.cs#1)]
 [!code-vb[CoContraSimpleIEnum#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontrasimpleienum/vb/example.vb#1)]  
  
 <xref:System.Collections.Generic.List%601> 類別會實作 <xref:System.Collections.Generic.IEnumerable%601> 介面，因此 `List<Derived>` (在 Visual Basic 中則為`List(Of Derived)` ) 會實作 `IEnumerable<Derived>`。 Covariant 型別參數會完成其餘工作。  
  
 而 Contravariance 看起來則違反直覺。 下列範例會建立 `Action<Base>` (在 Visual Basic 中則為`Action(Of Base)` ) 類型的委派，然後將該委派指派給 `Action<Derived>`類型的變數。  
  
 [!code-csharp[CoContraSimpleAction#1](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontrasimpleaction/cs/example.cs#1)]
 [!code-vb[CoContraSimpleAction#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontrasimpleaction/vb/example.vb#1)]  
  
 這看起來是反向的，但是在編譯和執行時是類型安全的程式碼。 Lambda 運算式符合指派給它的委派，因此它會定義一個方法，此方法會接受一個類型的參數， `Base` 而且沒有傳回值。 結果產生的委派可以指派給 `Action<Derived>` 類型的變數，因為 `T` 委派的 <xref:System.Action%601> 類型參數是 Contravariant。 程式碼是類型安全的，因為 `T` 指定參數類型。 當 `Action<Base>` 類型的委派當成 `Action<Derived>`類型的委派被叫用時，引數必須是 `Derived`類型。 此引數永遠可以安全地傳遞至基礎方法，因為方法的參數是 `Base`類型。  
  
 一般來說，Covariant 類型參數可以用來做為委派的傳回類型，而 Contravariant 類型參數可以用來做為參數類型。 例如，Covariant 類型參數可以用來做為介面方法的傳回類型，而 Contravariant 類型參數可以用來做為介面方法的參數類型。  
  
 共變數和反變數合稱為「變異數」  。 未標示 Covariant 或 Contravariant 的泛型類型參數，稱為 *Invariant* 參數。 通用語言執行平台中變異數事實的簡短摘要。  
  
- Variant 型別參數限制為泛型介面和泛型委派類型。  
  
- 泛型介面或泛型委派類型可以同時具有 Covariant 和 Contravariant 類型參數。  
  
- 變異數只適用於參考類型，因此如果將 Variant 類型參數指定為實值類型，該類型參數最後建構的類型會是 Invariant。  
  
- 變異數不適用於委派組合。 也就是說，如果有分別適用於 `Action<Derived>` 和 `Action<Base>` (在 Visual Basic 中則為`Action(Of Derived)` 和 `Action(Of Base)` ) 類型的兩個委派，您無法將第二個委派與第一個委派組合 (雖然結果會是類型安全的)。 變異數允許將第二個委派指派給 `Action<Derived>`類型的變數，但是委派只有在類型完全相符時才能組合。

- 從 c # 9 開始，支援協變數傳回類型。 覆寫方法可以宣告它所覆寫的方法更衍生的傳回型別，而覆寫的唯讀屬性可以宣告更多衍生的型別。

<a name="InterfaceCovariantTypeParameters"></a>
## <a name="generic-interfaces-with-covariant-type-parameters"></a>具有協變數型別參數的泛型介面

數個泛型介面具有協變數型別參數，例如，、、 <xref:System.Collections.Generic.IEnumerable%601> <xref:System.Collections.Generic.IEnumerator%601> <xref:System.Linq.IQueryable%601> 和 <xref:System.Linq.IGrouping%602> 。 這些介面的所有類型參數都是共變數，因此類型參數只能用於成員的傳回類型。  
  
 下列範例會說明 Covariant 類型參數。 這個範例定義兩個類型： `Base` 具有名為 `PrintBases` 的靜態方法，此方法會接受 `IEnumerable<Base>` (在 Visual Basic 中則為`IEnumerable(Of Base)` ) 並列印項目。 `Derived` 繼承自 `Base`。 範例會建立空的 `List<Derived>` (在 Visual Basic 中則為 `List(Of Derived)`)，並示範可將此類型傳遞至 `PrintBases`，再指派給類型為 `IEnumerable<Base>` 的變數而不用轉型。 <xref:System.Collections.Generic.List%601> 會實作 <xref:System.Collections.Generic.IEnumerable%601>，後者具有單一 Covariant 類型參數。 Covariant 類型參數是可以使用 `IEnumerable<Derived>` 的執行個體而不能使用 `IEnumerable<Base>`的執行個體的原因。  
  
 [!code-csharp[CoContravarianceInClrGenericI#1](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontravarianceinclrgenerici/cs/example.cs#1)]
 [!code-vb[CoContravarianceInClrGenericI#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontravarianceinclrgenerici/vb/example.vb#1)]  
  
## <a name="generic-interfaces-with-contravariant-type-parameters"></a>具有逆變型別參數的泛型介面

數個泛型介面具有逆變型別參數;例如： <xref:System.Collections.Generic.IComparer%601> 、 <xref:System.IComparable%601> 和 <xref:System.Collections.Generic.IEqualityComparer%601> 。 這些介面只有 Contravariant 型別參數，因此型別參數只用來做為介面成員中的參數類型。  
  
 下列範例會說明 Contravariant 類型參數。 範例定義了包含`MustInherit` 屬性的抽象 (在 Visual Basic 中為 `Shape` ) `Area` 類別。 範例還定義了實作 `ShapeAreaComparer` (在 Visual Basic 中則為 `IComparer<Shape>` ) 的`IComparer(Of Shape)` 類別。 <xref:System.Collections.Generic.IComparer%601.Compare%2A?displayProperty=nameWithType> 方法的實作是以 `Area` 屬性值為基礎，因此可以使用 `ShapeAreaComparer` 依區域排序 `Shape` 物件。  
  
 `Circle` 類別會繼承 `Shape` 並覆寫 `Area`。 此範例會使用採用 <xref:System.Collections.Generic.SortedSet%601> (在 Visual Basic 中為 `Circle` ) 的建構函式建立 `IComparer<Circle>` 物件的`IComparer(Of Circle)` 。 不過，此範例不會傳遞 `IComparer<Circle>`，而是傳遞實作 `ShapeAreaComparer` 的 `IComparer<Shape>` 物件。 當程式碼呼叫衍生程度較大類型 (`Shape`) 的比較子時，範例可以傳遞衍生程度較小類型 (`Circle`) 的比較子，因為 <xref:System.Collections.Generic.IComparer%601> 泛型介面的類型參數為 Contravariant。  
  
 將新的 `Circle` 物件加入至 `SortedSet<Circle>`時， `IComparer<Shape>.Compare` 物件的`IComparer(Of Shape).Compare` 方法 (在 Visual Basic 中為 `ShapeAreaComparer` 方法) 會在每次新項目與現有項目比較時呼叫。 這個方法的類型參數 (`Shape`) 相較於傳遞的類型 (`Circle`)，其衍生程度較小，因此該呼叫具備類型安全。 反變數 (Contravariance) 可讓 `ShapeAreaComparer` 排序衍生自 `Shape`的任何單一類型集合，以及混合類型集合。  
  
 [!code-csharp[CoContravarianceInClrGenericI2#1](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontravarianceinclrgenerici2/cs/example.cs#1)]
 [!code-vb[CoContravarianceInClrGenericI2#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontravarianceinclrgenerici2/vb/example.vb#1)]  

## <a name="generic-delegates-with-variant-type-parameters"></a>具有 variant 類型參數的泛型委派

`Func`泛型委派（例如 <xref:System.Func%602> ）具有協變數傳回類型和逆變參數類型。 `Action` 泛型委派 (例如 <xref:System.Action%602>) 則具有 Contravariant 類型參數。 這表示可以將委派指派給具有衍生程度較大參數類型及 (如果是 `Func` 泛型委派) 衍生程度較小的傳回類型的變數。  
  
> [!NOTE]
> `Func` 泛型委派的最後一個泛型類型參數會指定委派簽章中的傳回值類型。 這個參數是 Covariant (`out` 關鍵字)，而其他泛型類型參數則是 Contravariant (`in` 關鍵字)。  
  
 下列程式碼會說明這一點。 程式碼的第一段會定義名為 `Base`的類別、繼承 `Derived` 的 `Base`類別，和另一個具有 `static` 方法 (在 Visual Basic 中則為`Shared` 方法) 的 `MyMethod`類別。 這個方法會接受 `Base` 的執行個體，然後傳回 `Derived`的執行個體  (如果引數為的實例 `Derived` ，就會傳回 `MyMethod` 它; 如果引數是的實例，就會傳回的 `Base` `MyMethod` 新實例 `Derived` 。 ) 在中 `Main()` ，此範例會在 `Func<Base, Derived>` 代表的 Visual Basic) 中建立 (的實例，並將 `Func(Of Base, Derived)` `MyMethod` 它儲存在變數中 `f1` 。  
  
 [!code-csharp[CoContravarianceDelegates#2](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontravariancedelegates/cs/example.cs#2)]
 [!code-vb[CoContravarianceDelegates#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontravariancedelegates/vb/example.vb#2)]  
  
 程式碼的第二段顯示可以將委派指派給類型為 `Func<Base, Base>` (在 Visual Basic 中則為`Func(Of Base, Base)` ) 的變數，因為傳回類型是 Covariant。  
  
 [!code-csharp[CoContravarianceDelegates#3](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontravariancedelegates/cs/example.cs#3)]
 [!code-vb[CoContravarianceDelegates#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontravariancedelegates/vb/example.vb#3)]  
  
 程式碼的第三段顯示可以將委派指派給類型為 `Func<Derived, Derived>` (在 Visual Basic 中則為`Func(Of Derived, Derived)` ) 的變數，因為參數類型是 Contravariant。  
  
 [!code-csharp[CoContravarianceDelegates#4](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontravariancedelegates/cs/example.cs#4)]
 [!code-vb[CoContravarianceDelegates#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontravariancedelegates/vb/example.vb#4)]  
  
 程式碼的最後一段顯示結合 Contravariant 參數類型與 Covariant 傳回類型的效果，即可將委派指派給類型為 `Func<Derived, Base>` (在 Visual Basic 中則為`Func(Of Derived, Base)` ) 的變數。  
  
 [!code-csharp[CoContravarianceDelegates#5](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontravariancedelegates/cs/example.cs#5)]
 [!code-vb[CoContravarianceDelegates#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontravariancedelegates/vb/example.vb#5)]  
  
### <a name="variance-in-non-generic-delegates"></a>非泛型委派中的變異數

 在上述的程式碼中，`MyMethod` 的簽章與建構的泛型委派 `Func<Base, Derived>` (在 Visual Basic 中則為 `Func(Of Base, Derived)`) 之簽章完全相符。 這個範例顯示，只要所有委派類型都是從泛型委派類型 <xref:System.Func%602>建構的，即可將這個泛型委派儲存在具有衍生程度較大參數類型及衍生程度較小傳回類型的變數或方法參數中。  
  
 這一點很重要。 泛型委派參數類型中的共變數和反變數效果類似於一般委派繫結中的共變數和反變數效果 (請參閱[委派中的變異數 (C# )](../../csharp/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md) 和[委派中的變異數 (Visual Basic)](../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md))。 不過，委派繫結中的變異數可以使用所有的委派類型，而不只是具有 Variant 型別參數的泛型委派類型。 此外，委派繫結中的變異數可讓方法繫結至任何具有較嚴格參數類型及較不嚴格傳回類型的委派，而泛型委派的指派只適用於這兩種委派類型都是從相同泛型類型定義建構的情況。  
  
 在下列範例中，會說明委派繫結中的變異數與泛型類型參數中的變異數合併之效果。 範例中定義包含三個類型的類型階層，其中衍生程度最小的是`Type1`，而最大的是`Type3`。 在一般委派繫結中，會使用變異數以將參數類型為 `Type1` 且傳回類型為 `Type3` 的方法繫結至參數類型為 `Type2` 且傳回類型為 `Type2`的泛型委派。 然後，範例會使用泛型類型參數的共變數和反變數，將產生的泛型委派指派給另一個參數類型為 `Type3` 且傳回類型為 `Type1` 的泛型委派類型變數。 在第二項指派中，變數類型和委派類型都必須是從相同的泛型類型定義 (在本範例中為 <xref:System.Func%602>) 建構的。  
  
 [!code-csharp[CoContravarianceDelegatesGenRelaxed#1](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontravariancedelegatesgenrelaxed/cs/example.cs#1)]
 [!code-vb[CoContravarianceDelegatesGenRelaxed#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontravariancedelegatesgenrelaxed/vb/example.vb#1)]  

## <a name="define-variant-generic-interfaces-and-delegates"></a>定義 variant 泛型介面和委派

Visual Basic 和 c # 都有關鍵詞，可讓您將介面和委派的泛型型別參數標示為協變數或逆變。
  
 `out`在 Visual Basic) 中，以關鍵字 (關鍵字標記的協變數型別參數 `Out` 。 您可以使用 Covariant 類型參數當做屬於介面之方法的傳回值，或當做委派的傳回類型。 但是，您不能將 Covariant 類型參數當做介面方法的泛型類型條件約束使用。  
  
> [!NOTE]
> 如果介面的方法具有泛型委派類型的參數，就可以使用介面類型的 Covariant 類型參數指定委派類型的 Contravariant 類型參數。  
  
 `in`在 Visual Basic) 中，以關鍵字 (關鍵字標記的逆變型別參數 `In` 。 您可以使用 Contravariant 類型參數當做屬於介面之方法的參數類型，或當做委派的參數類型。 此外，您也可以將 Contravariant 類型參數當做介面方法的泛型類型條件約束使用。  
  
 只有介面類型和委派類型可以有 Variant 類型參數。 介面或委派類型可以同時具有 Covariant 和 Contravariant 類型參數。  
  
 Visual Basic 和 C# 不允許您違反使用 Covariant 和 Contravariant 類型參數的規則，也不允許您將 Covariant 和 Contravariant 附註加入至介面及委派以外類型的類型參數。
  
 如需詳細資訊與範例程式碼，請參閱[泛型介面中的變異數 (C#)](../../csharp/programming-guide/concepts/covariance-contravariance/variance-in-generic-interfaces.md) 和[泛型介面中的變異數 (Visual Basic)](../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-generic-interfaces.md)。  

## <a name="list-of-types"></a>類型清單

下列介面和委派類型具有協變數和/或逆變型別參數。  
  
|類型|Covariant 類型參數|Contravariant 類型參數|  
|----------|-------------------------------|-----------------------------------|  
|<xref:System.Action%601> 到 <xref:System.Action%6016>||是|  
|<xref:System.Comparison%601>||是|  
|<xref:System.Converter%602>|是|是|  
|<xref:System.Func%601>|是||  
|<xref:System.Func%602> 到 <xref:System.Func%6017>|是|是|  
|<xref:System.IComparable%601>||是|  
|<xref:System.Predicate%601>||是|  
|<xref:System.Collections.Generic.IComparer%601>||是|  
|<xref:System.Collections.Generic.IEnumerable%601>|是||  
|<xref:System.Collections.Generic.IEnumerator%601>|是||  
|<xref:System.Collections.Generic.IEqualityComparer%601>||是|  
|<xref:System.Linq.IGrouping%602>|是||  
|<xref:System.Linq.IOrderedEnumerable%601>|是||  
|<xref:System.Linq.IOrderedQueryable%601>|是||  
|<xref:System.Linq.IQueryable%601>|是||  
  
## <a name="see-also"></a>另請參閱

- [共變數和反變數 (C#)](../../csharp/programming-guide/concepts/covariance-contravariance/index.md)
- [共變數和反變數 (Visual Basic)](../../visual-basic/programming-guide/concepts/covariance-contravariance/index.md)
- [委派中的差異 (C#)](../../csharp/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md)
- [委派中的變異數 (Visual Basic)](../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md)
