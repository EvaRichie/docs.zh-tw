---
title: 類型 'typename' 的 'IsNot' 運算元只能與 'Nothing' 比較，因為 'typename' 是可為 Null 的類型
ms.date: 07/20/2015
f1_keywords:
- bc32128
- vbc32128
helpviewer_keywords:
- BC32128
ms.assetid: 1155b23a-ad75-4bab-b9da-73f35c767a36
ms.openlocfilehash: 084978c1e047eebd60149af63c0ec9a1135225be
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/17/2020
ms.locfileid: "92163333"
---
# <a name="bc32128-isnot-operand-of-type-typename-can-only-be-compared-to-nothing-because-typename-is-a-nullable-type"></a>BC32128：類型 ' typename ' 的 ' IsNot ' 運算元只能與 ' Nothing ' 進行比較，因為 ' typename ' 是可為 null 的類型

宣告為可為 null 實值型別的變數已經與使用運算子以外的運算式進行比較 `Nothing` `IsNot` 。

**錯誤識別碼：** BC32128

## <a name="to-correct-this-error"></a>更正這個錯誤

若要使用 `Nothing` 運算子，將可為 Null 的類型與 `IsNot` 以外的運算式進行比較，請在可為 Null 的類型上呼叫 `GetType` 方法，並將結果與運算式進行比較，如下列範例所示。

```vb
Dim number? As Integer = 5

If number IsNot Nothing Then
  If number.GetType() IsNot Type.GetType("System.Int32") Then

  End If
End If
```

## <a name="see-also"></a>另請參閱

- [可為 null 的實數值型別](../../programming-guide/language-features/data-types/nullable-value-types.md)
- [IsNot 運算子](../operators/isnot-operator.md)
