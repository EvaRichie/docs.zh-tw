---
description: protected 關鍵字 - C# 參考
title: protected 關鍵字 - C# 參考
ms.date: 07/20/2015
f1_keywords:
- protected
- protected_CSharpKeyword
helpviewer_keywords:
- protected keyword [C#]
ms.assetid: 05ce3794-6675-4025-bddb-eaaa0ec22892
ms.openlocfilehash: 4c18d1f2f45a0a154dccd42736a01874dd1af853
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89122377"
---
# <a name="protected-c-reference"></a>protected (C# 參考)

`protected` 關鍵字是成員存取修飾詞。

 > 此頁面涵蓋 `protected` 存取。 `protected`關鍵字也是和存取修飾詞的一部分 [`protected internal`](protected-internal.md) [`private protected`](private-protected.md) 。

受保護的成員可在其類別內由衍生類別執行個體存取。

如需 `protected` 和其他存取修飾詞的比較，請參閱[存取範圍層級](accessibility-levels.md)。

## <a name="example"></a>範例

只有在存取是透過衍生類別類型進行時，才可以存取衍生類別中屬於基底類別的受保護成員。 例如，請考慮下列程式碼區段：

[!code-csharp[csrefKeywordsModifiers#11](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#11)]

陳述式 `a.x = 10` 會產生錯誤，因為它是在靜態方法 Main 中發出，而不是在類別 B 的執行個體中發出。

結構成員不可以是受保護的成員，因為無法繼承結構。

## <a name="example"></a>範例

在此範例中，`DerivedPoint` 類別衍生自 `Point`。 因此，您可以直接從衍生類別存取基底類別的受保護成員。

[!code-csharp[csrefKeywordsModifiers#12](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#12)]  

如果您將 `x` 和 `y` 的存取層級變更為 [private](private.md)，編譯器會發出錯誤訊息：

`'Point.y' is inaccessible due to its protection level.`

`'Point.x' is inaccessible due to its protection level.`

## <a name="c-language-specification"></a>C# 語言規格  

如需詳細資訊，請參閱 [C# 語言規格](/dotnet/csharp/language-reference/language-specification/introduction)的[已宣告存取範圍](~/_csharplang/spec/basic-concepts.md#declared-accessibility)。 語言規格是 C# 語法及用法的限定來源。

## <a name="see-also"></a>另請參閱

- [C # 參考](../index.md)
- [C # 程式設計指南](../../programming-guide/index.md)
- [C # 關鍵字](index.md)
- [存取修飾詞](access-modifiers.md)
- [協助工具層級](accessibility-levels.md)
- [修飾詞](index.md)
- [public](public.md)
- [私人](private.md)
- [internal](internal.md)
- [internal virtual 關鍵字的安全性考量](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/heyd8kky(v=vs.100))
