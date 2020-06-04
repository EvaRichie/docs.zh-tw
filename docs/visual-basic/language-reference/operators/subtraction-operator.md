---
title: '- 運算子'
ms.date: 07/20/2015
f1_keywords:
- vb.Negate
- vb.-
helpviewer_keywords:
- operator [Visual Basic]
- operators [Visual Basic], subtraction
- operators [Visual Basic], difference
- negation operator [Visual Basic]
- operators [Visual Basic], arithmetic
- subtraction operator [Visual Basic], syntax
- arithmetic operators [Visual Basic], subtraction
- difference operator [Visual Basic]
- math operators [Visual Basic]
- operators [Visual Basic], negation
- minus operator [Visual Basic]
ms.assetid: bff2c368-662d-4c92-ac87-1d9bdfd3426a
ms.openlocfilehash: 6539beb5cf8078281357445e2391fac189208087
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84406349"
---
# <a name="--operator-visual-basic"></a>- 運算子 (Visual Basic)
傳回兩個數值運算式之間的差異，或數值運算式的負數值。  
  
## <a name="syntax"></a>語法  
  
```vb  
expression1 – expression2
```
  
或

```vb  
–expression1  
```  
  
## <a name="parts"></a>組件  
 `expression1`  
 必要。 任何數值運算式。  
  
 `expression2`  
 除非 `–` 運算子正在計算負數值，否則為必要。 任何數值運算式。  
  
## <a name="result"></a>結果  
 結果是和之間的差異 `expression1` `expression2` ，或的負值 `expression1` 。  
  
 結果資料類型是適用于和之資料類型的數數值型別 `expression1` `expression2` 。 請參閱[運算子結果的資料類型](data-types-of-operator-results.md)中的「整數算術」資料表。  
  
## <a name="supported-types"></a>支援的型別  
 所有數值類型。 這包括不帶正負號的和浮點類型，以及 `Decimal` 。  
  
## <a name="remarks"></a>備註  
 在先前所示的語法中，第一次使用 `–` 時，運算子是*二元*算術減法運算子，用於兩個數值運算式之間的差異。  
  
 在先前顯示的語法中，第二個使用方式中， `–` 運算子是運算式之負值的*一元*負運算子。 就這一點而言，否定是由反轉的正負號所組成， `expression1` 因此如果為負數，則結果為正數 `expression1` 。  
  
 如果任一運算式評估為不是[任何](../nothing.md)值，則 `–` 運算子會將它視為零。  
  
> [!NOTE]
> `–`運算子可以多載*overloaded*，這表示當運算元具有該類別或結構的類型時，類別或結構可以重新定義其行為。 如果您的程式碼在這類類別或結構上使用這個運算子，請確定您瞭解其已重新定義的行為。 如需詳細資訊，請參閱 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)。  
  
## <a name="example"></a>範例  
 下列範例會使用 `–` 運算子來計算並傳回兩個數字之間的差異，然後再將數位否定。  
  
 [!code-vb[VbVbalrOperators#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#10)]  
  
 執行這些語句之後，會 `binaryResult` 包含124.45 和 `unaryResult` contains –334.90。  
  
## <a name="see-also"></a>另請參閱

- [-= 運算子 (Visual Basic)](subtraction-assignment-operator.md)
- [算術運算子](arithmetic-operators.md)
- [Visual Basic 中的運算子優先順序](operator-precedence.md)
- [依功能列出運算子](operators-listed-by-functionality.md)
- [Visual Basic 的算術運算子](../../programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
