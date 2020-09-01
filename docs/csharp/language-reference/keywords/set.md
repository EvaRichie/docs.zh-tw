---
description: set 關鍵字 - C# 參考
title: set 關鍵字 - C# 參考
ms.date: 03/10/2017
f1_keywords:
- set
- set_CSharpKeyword
helpviewer_keywords:
- set keyword [C#]
ms.assetid: 30d7e4e5-cc2e-4635-a597-14a724879619
ms.openlocfilehash: ff0c99e5d4d6271351783befd6650d9a77f39886
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89136911"
---
# <a name="set-c-reference"></a>set (C# 參考)

`set` 關鍵字會在屬性或索引子中定義「存取子」** 方法，以將值指派給屬性或索引子項目。 如需詳細資訊和範例，請參閱[屬性](../../programming-guide/classes-and-structs/properties.md)、[自動實作的屬性](../../programming-guide/classes-and-structs/auto-implemented-properties.md)和[索引子](../../programming-guide/indexers/index.md)。

下列範例會為名為 `Seconds` 的屬性定義 `get` 和 `set` 存取子。 它使用名為 `_seconds` 的私用欄位來支援屬性值。

[!code-csharp[set#1](~/samples/snippets/csharp/language-reference/keywords/get/get-1.cs)]

`set` 存取子通常是由指派值的單一陳述式所組成，如上述範例所示。 從 C# 7.0 開始，您可以將 `set` 存取子實作為運算式主體成員。 下列範例會將 `get` 和 `set` 存取子實作為運算式主體成員。

[!code-csharp[set#3](~/samples/snippets/csharp/language-reference/keywords/get/get-3.cs)]
  
如果屬性的 `get` 和 `set` 存取子只會設定或擷取私用支援欄位中的值，而不會執行其他作業，在此簡單的情況下，您可以利用 C# 編譯器的自動實作屬性支援。 下列程式碼範例將 `Hours` 實作為自動實作屬性。

[!code-csharp[set#2](~/samples/snippets/csharp/language-reference/keywords/get/get-2.cs)]
  
## <a name="c-language-specification"></a>C# 語言規格

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>另請參閱

- [C # 參考](../index.md)
- [C # 程式設計指南](../../programming-guide/index.md)
- [C # 關鍵字](index.md)
- [屬性](../../programming-guide/classes-and-structs/properties.md)
