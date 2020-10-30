---
title: .NET 中的泛型集合
ms.date: 02/15/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- generics [.NET], collections
- generic collections [.NET]
- generic types [.NET]
ms.assetid: 5b646751-6ab7-465c-916c-b1a76aefa9f5
ms.openlocfilehash: 956db9ace4ae00062accdd6e80c7911aaac7523f
ms.sourcegitcommit: b1442669f1982d3a1cb18ea35b5acfb0fc7d93e4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/30/2020
ms.locfileid: "93064245"
---
# <a name="generic-collections-in-net"></a>.NET 中的泛型集合

 .NET 類別庫提供 <xref:System.Collections.Generic> 和 <xref:System.Collections.ObjectModel> 命名空間中的數種泛型集合類別。 如需這些類別的詳細資訊，請參閱[常用的集合類型](../collections/commonly-used-collection-types.md)。  
  
## <a name="systemcollectionsgeneric"></a>System.Collections.Generic

 許多泛型集合類型是非泛型類型的直接模擬。 <xref:System.Collections.Generic.Dictionary%602> 是 <xref:System.Collections.Hashtable> 的泛型版本，使用泛型結構 <xref:System.Collections.Generic.KeyValuePair%602> (而不是 <xref:System.Collections.DictionaryEntry>) 來進行列舉。  
  
 <xref:System.Collections.Generic.List%601> 是 <xref:System.Collections.ArrayList> 的泛型版本。 泛型 <xref:System.Collections.Generic.Queue%601> 和 <xref:System.Collections.Generic.Stack%601> 類別有對應的非泛型版本。  
  
 <xref:System.Collections.Generic.SortedList%602> 有泛型和非泛型版本。 這兩種版本是字典和清單的混合。 <xref:System.Collections.Generic.SortedDictionary%602> 泛型類別是純字典，沒有對應的非泛型版本。  
  
 <xref:System.Collections.Generic.LinkedList%601> 泛型類別是純連結清單， 沒有對應的非泛型版本。  
  
## <a name="systemcollectionsobjectmodel"></a>System.Collections.ObjectModel

 <xref:System.Collections.ObjectModel.Collection%601> 泛型類別提供基底類別，可用於衍生您自己的泛型集合類型。 <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> 類別提供一個簡單的方法，從任何實作 <xref:System.Collections.Generic.IList%601> 泛型介面的類型中產生唯讀集合。 <xref:System.Collections.ObjectModel.KeyedCollection%602> 泛型類別提供一個方法來儲存物件 (其中包含物件的索引鍵)。  
  
## <a name="other-generic-types"></a>其他泛型型別

 <xref:System.Nullable%601> 泛型結構可讓您使用可指派 `null` 的實值類型。 這在使用資料庫查詢時會很有用，因為包含實值類型的欄位可能遺漏。 泛型類型參數可以是任何實值類型。  
  
> [!NOTE]
> 在 C# 和 Visual Basic 中，不需要明確使用 <xref:System.Nullable%601>，因為語言已具有可為 Null 型別的語法。 請參閱[可為 null 的實值型別 (c # 參考) ](../../csharp/language-reference/builtin-types/nullable-value-types.md)和[可為 null 的實數值型別 () Visual Basic](../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)
  
 <xref:System.ArraySegment%601> 泛型結構提供一個方法，將項目範圍限定在任何類型之以零為起始的一維陣列中。 泛型型別參數是陣列的項目類型。  
  
 <xref:System.EventHandler%601>如果您的事件遵循 .net 所使用的事件處理模式，泛型委派就不需要宣告委派類型來處理事件。 例如，假設您已建立衍生自 <xref:System.EventArgs> 的 `MyEventArgs` 類別來保存事件的資料。 您可以接著依照下列方式來宣告事件：  
  
 [!code-cpp[Conceptual.Generics.Overview#7](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.generics.overview/cpp/source2.cpp#7)]
 [!code-csharp[Conceptual.Generics.Overview#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.generics.overview/cs/source2.cs#7)]
 [!code-vb[Conceptual.Generics.Overview#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.generics.overview/vb/source2.vb#7)]  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Collections.Generic?displayProperty=nameWithType>
- <xref:System.Collections.ObjectModel?displayProperty=nameWithType>
- [泛型](index.md)
- [用於運算元組和清單的泛型委派](delegates-for-manipulating-arrays-and-lists.md)
- [泛型介面](interfaces.md)
