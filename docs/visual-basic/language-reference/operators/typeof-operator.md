---
title: TypeOf 運算子
ms.date: 07/20/2015
f1_keywords:
- TypeOf
- vb.TypeOf
helpviewer_keywords:
- types [Visual Basic], compatible
- comparison operators [Visual Basic]
- TypeOf...Is expression
- data types [Visual Basic], compatible
- TypeOf operator [Visual Basic]
- compatible data types [Visual Basic]
ms.assetid: 33f65296-659a-4b9a-9a29-c2a91cff68b2
ms.openlocfilehash: 0a01b49cf1e0bf9ad7b2ce541cee39cba83025ca
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90875305"
---
# <a name="typeof-operator-visual-basic"></a>TypeOf 運算子 (Visual Basic)

檢查運算式結果的執行時間型別是否與指定的類型相容。
  
## <a name="syntax"></a>Syntax  
  
```vb  
result = TypeOf objectexpression Is typename  
```  
  
```vb  
result = TypeOf objectexpression IsNot typename  
```  
  
## <a name="parts"></a>組件  

 `result`  
 更有效率。 `Boolean` 值。  
  
 `objectexpression`  
 必要。 評估為參考類型的任何運算式。  
  
 `typename`  
 必要。 任何資料類型名稱。  
  
## <a name="remarks"></a>備註  

 `TypeOf` 運算子會判定 `objectexpression` 的執行階段類型是否相容 `typename`。 相容性取決 `typename` 的類型分類。 下表顯示如何判斷相容性。  
  
|`typename` 的類型分類|相容性準則|  
|---------------------------------|-----------------------------|  
|類別|`objectexpression` 屬於類型 `typename` 或繼承自 `typename`|  
|結構|`objectexpression` 屬於類型 `typename`|  
|介面|`objectexpression` 實作 `typename` 或繼承自實作 `typename` 的類別|  
  
 如果 `objectexpression` 的執行階段類別滿足相容性準則，則 `result` 是 `True`。 否則，`result` 為 `False`。  如果 `objectexpression` 為 null，則 `TypeOf`...`Is` 傳回 `False`，`IsNot` 則傳回 `True`。  
  
 `TypeOf` 一律會使用 `Is` 關鍵字來建構 `TypeOf`...`Is` 運算式，或使用 `IsNot` 關鍵字來建構 `TypeOf`...`IsNot` 運算式。  
  
## <a name="example"></a>範例  

 下列範例會使用 `TypeOf`...`Is` 運算式，測試兩個包含各種資料類型的物件參考變數的類型相容性。  
  
 [!code-vb[VbVbalrOperators#39](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#39)]  
  
 變數 `refInteger` 具有執行階段類型 `Integer`。 它相容 `Integer`，但不相容 `Double`。 變數 `refForm` 具有執行階段類型 <xref:System.Windows.Forms.Form>。 它相容 <xref:System.Windows.Forms.Form> (因為那是其類型)、相容 <xref:System.Windows.Forms.Control> (因為 <xref:System.Windows.Forms.Form> 繼承自 <xref:System.Windows.Forms.Control>)，且具有 <xref:System.ComponentModel.IComponent> (因為 <xref:System.Windows.Forms.Form> 繼承自 <xref:System.ComponentModel.Component>，它會實作 <xref:System.ComponentModel.IComponent>)。 不過，`refForm` 不相容 <xref:System.Windows.Forms.Label>。  
  
## <a name="see-also"></a>另請參閱

- [Is 運算子](is-operator.md)
- [IsNot 運算子](isnot-operator.md)
- [Comparison Operators in Visual Basic](../../programming-guide/language-features/operators-and-expressions/comparison-operators.md)
- [Visual Basic 中的運算子優先順序](operator-precedence.md)
- [依功能列出運算子](operators-listed-by-functionality.md)
- [運算子和運算式](../../programming-guide/language-features/operators-and-expressions/index.md)
