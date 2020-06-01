---
title: 泛型 - C# 程式設計手冊
ms.date: 07/20/2015
helpviewer_keywords:
- C# language, generics
- generics [C#]
ms.assetid: 75ea8509-a4ea-4e7a-a2b3-cf72482e9282
ms.openlocfilehash: a3ed3aa412c7d9c9d6b705dba80b527057c647fa
ms.sourcegitcommit: a241301495a84cc8c64fe972330d16edd619868b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/01/2020
ms.locfileid: "84241665"
---
# <a name="generics-c-programming-guide"></a>泛型 (C# 程式設計手冊)

泛型引進 .NET 類型參數的概念，讓您可以設計類別和方法，以延遲一或多個類型的規格，直到用戶端程式代碼宣告並具現化類別或方法為止。 例如，藉由使用泛型型別參數 `T` ，您可以撰寫其他用戶端程式代碼可以使用的單一類別，而不會產生執行時間轉換或裝箱作業的成本或風險，如下所示：

[!code-csharp[csProgGuideGenerics#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#1)]

泛型類別和方法結合重複使用性、型別安全和效率，使其非泛型對應項無法使用。 泛型最常搭配在其上操作的集合和方法使用。 <xref:System.Collections.Generic>命名空間包含數個以泛型為基礎的集合類別。 不建議使用非泛型集合，例如，基於 <xref:System.Collections.ArrayList> 相容性目的而維護。 如需詳細資訊，請參閱 [.NET 的泛型](../../../standard/generics/index.md)。

當然，您也可以建立自訂的泛型型別和方法，自行處理泛型化的問題，並設計型別安全且有效率的模式。 下列程式碼範例顯示一個簡單的泛型連結清單類別，以供示範之用 （在大部分的情況下，您應該使用 <xref:System.Collections.Generic.List%601> .net 所提供的類別，而不是自行建立）。類型參數 `T` 用於數個位置，而具體類型通常會用來表示清單中儲存的專案類型。 這個參數可以用於下列方面：

- 作為 `AddHead` 方法中的方法參數類型。
- 作為巢狀 `Node` 類別中 `Data` 屬性的傳回型別。
- 作為巢狀類別中私用成員 `data` 的類型。

 請注意， `T` 可供 nested `Node` 類別使用。 當 `GenericList<T>` 以具象類型具現化時 (例如具現化為 `GenericList<int>`)，所出現的每個 `T` 都會以 `int` 取代。

[!code-csharp[csProgGuideGenerics#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#2)]

下列程式碼範例示範用戶端程式碼如何使用泛型 `GenericList<T>` 類別建立整數清單。 您只要變更型別引數，就能輕鬆修改下列的程式碼來建立字串清單或任何其他自訂類型的清單：

[!code-csharp[csProgGuideGenerics#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#3)]

## <a name="generics-overview"></a>泛型總覽

- 使用泛型型別以最佳化程式碼重複使用、型別安全和效能。
- 泛型的最常見用法是建立集合類別。
- .NET 類別庫包含命名空間中的數個泛型集合類別 <xref:System.Collections.Generic> 。 您應該盡可能使用這些類別，而不是使用類似在 <xref:System.Collections> 命名空間中的 <xref:System.Collections.ArrayList> 類別。
- 您可以建立自己的泛型介面、類別、方法、事件和委派。
- 泛型類別可限制為允許存取特定資料類型上的方法。
- 泛型資料類型中所使用的類型相關資訊，可在執行階段透過反映取得。

## <a name="related-sections"></a>相關章節

- [泛型類型參數](generic-type-parameters.md)
- [型別參數的條件約束](constraints-on-type-parameters.md)
- [泛型類別](generic-classes.md)
- [泛型介面](generic-interfaces.md)
- [泛型方法](generic-methods.md)
- [泛型委派](generic-delegates.md)
- [C++ 範本和 C# 泛型之間的差異](differences-between-cpp-templates-and-csharp-generics.md)
- [泛型和反映](generics-and-reflection.md)
- [執行階段中的泛型](generics-in-the-run-time.md)

## <a name="c-language-specification"></a>C# 語言規格

如需詳細資訊，請參閱[c # 語言規格](~/_csharplang/spec/types.md#constructed-types)。

## <a name="see-also"></a>另請參閱

- <xref:System.Collections.Generic>
- [C # 程式設計指南](../index.md)
- [類型](../types/index.md)
- [\<typeparam>](../xmldoc/typeparam.md)
- [\<typeparamref>](../xmldoc/typeparamref.md)
- [.NET 的泛型](../../../standard/generics/index.md)
