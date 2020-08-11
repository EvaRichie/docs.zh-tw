---
title: delegate 運算子 - C# 參考
ms.date: 07/18/2019
helpviewer_keywords:
- delegate [C#]
- anonymous method [C#]
ms.openlocfilehash: 33c438b88f1e993f4648786da9b20b91961b7ee1
ms.sourcegitcommit: 7476c20d2f911a834a00b8a7f5e8926bae6804d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/11/2020
ms.locfileid: "88062986"
---
# <a name="delegate-operator-c-reference"></a>delegate 運算子 (C# 參考)

`delegate` 運算子會建立可轉換成委派型別的匿名方法：

[!code-csharp-interactive[anonymous method](snippets/shared/DelegateOperator.cs#AnonymousMethod)]

> [!NOTE]
> 從 C# 3 開始，Lambda 運算式提供更精簡且更具表達性的方式來建立匿名函式。 使用 [=> 運算子](lambda-operator.md)來建構 Lambda 運算式：
>
> [!code-csharp-interactive[lambda expression](snippets/shared/DelegateOperator.cs#Lambda)]
>
> 如需 Lambda 運算式功能的詳細資訊 (例如，捕捉外部變數)，請參閱 [Lambda 運算式](lambda-expressions.md)。

當您使用 `delegate` 運算子時，您可以省略參數清單。 如果您這樣做，則可以將建立的匿名方法轉換成含任何參數清單的委派型別，如下列範例所示：

[!code-csharp-interactive[no parameter list](snippets/shared/DelegateOperator.cs#WithoutParameterList)]

那是 Lambda 運算式不支援的唯一匿名方法功能。 在所有其他情況下，建議您以 Lambda 運算式的方式來撰寫內嵌程式碼。

您也可以使用 `delegate` 關鍵字來宣告[委派型別](../builtin-types/reference-types.md#the-delegate-type)。

## <a name="c-language-specification"></a>C# 語言規格

如需詳細資訊，請參閱 [C# 語言規格](~/_csharplang/spec/introduction.md)的[匿名函式運算式](~/_csharplang/spec/expressions.md#anonymous-function-expressions)一節。

## <a name="see-also"></a>另請參閱

- [C# 參考資料](../index.md)
- [C# 運算子與運算式](index.md)
- [=> 運算子](lambda-operator.md)
