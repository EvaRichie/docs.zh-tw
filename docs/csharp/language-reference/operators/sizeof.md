---
title: sizeof 運算子 - C# 參考
ms.date: 07/25/2019
f1_keywords:
- sizeof_CSharpKeyword
- sizeof
helpviewer_keywords:
- sizeof keyword [C#]
ms.assetid: c548592c-677c-4f40-a4ce-e613f7529141
ms.openlocfilehash: 327183ccdf79cb8e15cd15aa3cffb044120808f8
ms.sourcegitcommit: ef50c99928183a0bba75e07b9f22895cd4c480f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87916693"
---
# <a name="sizeof-operator-c-reference"></a>sizeof 運算子 (C# 參考)

`sizeof` 運算子會返回指定型別變數所佔用的位元組總數。 `sizeof` 運算子的引數必須是[非受控型別](../builtin-types/unmanaged-types.md)的名稱，或是[限制](../../programming-guide/generics/constraints-on-type-parameters.md#unmanaged-constraint)為非受控型別的型別參數。

`sizeof` 運算子需要 [unsafe](../keywords/unsafe.md) 內容。 但是，下表顯示的運算式會在編譯時評估至對應的常數值，因此不需要 unsafe 內容：

|運算是|常數值|
|---------|---------------|
|`sizeof(sbyte)`|1|
|`sizeof(byte)`|1|
|`sizeof(short)`|2|
|`sizeof(ushort)`|2|
|`sizeof(int)`|4|
|`sizeof(uint)`|4|
|`sizeof(long)`|8|
|`sizeof(ulong)`|8|
|`sizeof(char)`|2|
|`sizeof(float)`|4|
|`sizeof(double)`|8|
|`sizeof(decimal)`|16|
|`sizeof(bool)`|1|

您也不需要在 `sizeof` 運算子的運算元是 [enum](../builtin-types/enum.md) 型別時使用 unsafe 內容。

下列範例示範 `sizeof` 運算子的用法：

[!code-csharp[sizeof examples](snippets/shared/SizeOfOperator.cs)]

`sizeof` 運算子會傳回通用語言執行平台在受控記憶體中原先將配置的位元組數。 針對 [struct](../builtin-types/struct.md)型別，該值包含任何填補，如先前範例所示範。 `sizeof` 運算子的結果可能會與 <xref:System.Runtime.InteropServices.Marshal.SizeOf%2A?displayProperty=nameWithType> 方法的結果不同，因為後者會傳回型別在 *unmanaged* 記憶體中的大小。

## <a name="c-language-specification"></a>C# 語言規格

如需詳細資訊，請參閱 [C# 語言規格](~/_csharplang/spec/introduction.md)中的 [sizeof 運算子](~/_csharplang/spec/unsafe-code.md#the-sizeof-operator)區段。

## <a name="see-also"></a>另請參閱

- [C# 參考資料](../index.md)
- [C# 運算子與運算式](index.md)
- [指標相關運算子](pointer-related-operators.md)
- [指標類型](../../programming-guide/unsafe-code-pointers/pointer-types.md)
- [記憶體與延伸相關類型](../../../standard/memory-and-spans/index.md)
- [.NET 的泛型](../../../standard/generics/index.md)
