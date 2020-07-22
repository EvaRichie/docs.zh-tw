---
title: 傳遞實值類型的參數 - C# 程式設計手冊
description: '當您以 c # 的值將實值型別變數傳遞至方法時，任何變更都不會影響原始資料。 若要變更值，請以傳址方式傳遞。'
ms.date: 07/20/2015
helpviewer_keywords:
- method parameters [C#], value types
- parameters [C#], value
ms.assetid: 193ab86f-5f9b-4359-ac29-7cdf8afad3a6
ms.openlocfilehash: 84829722cfb0b7ce71aff36f27a7c97cfa07ad5e
ms.sourcegitcommit: 3d84eac0818099c9949035feb96bbe0346358504
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/21/2020
ms.locfileid: "86864692"
---
# <a name="passing-value-type-parameters-c-programming-guide"></a>傳遞實值類型的參數 (C# 程式設計手冊)
相對於[參考型別](../../language-reference/keywords/reference-types.md)變數 (包含對其資料的參考)，[實值型別](../../language-reference/builtin-types/value-types.md)變數會直接包含資料。 以傳值方式將實值型別變數傳遞至方法，意味著將變數的複本傳遞至方法。 在方法內所進行之參數的任何變更，都不會影響儲存在引數變數中的原始資料。 如果您想要讓呼叫的方法變更參數值，就必須使用 [ref](../../language-reference/keywords/ref.md) 或 [out](../../language-reference/keywords/out-parameter-modifier.md) 關鍵字，以傳址方式來傳遞它。 您也可以使用 [in](../../language-reference/keywords/in-parameter-modifier.md) 關鍵字以傳址方式傳遞值，以避免發生複製的情況，同時確保該值不會變更。 為求簡化，下列範例使用 `ref`。  
  
## <a name="passing-value-types-by-value"></a>以傳值方式傳遞實值型別  
 下列範例示範以傳值方式傳遞實值型別參數。 `n` 變數會以傳值方式傳遞至 `SquareIt` 方法。 在方法內進行的任何變更都不會影響變數的原始值。  
  
 [!code-csharp[csProgGuideParameters#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideParameters/CS/Parameters.cs#3)]  
  
 `n` 變數是實值型別。 它包含值為 `5` 的資料。 叫用 `SquareIt` 時，會將 `n` 的內容複製到 `x` 參數，並在方法內部將其平方。 不過，在 `Main` 中，`n` 的值在呼叫`SquareIt` 方法前後是一樣的。 發生在方法內部的變更只會影響區域變數 `x`。  
  
## <a name="passing-value-types-by-reference"></a>以傳址方式傳遞實值型別  
 下列範例與上述範例相同，差別在於引數是以 `ref` 參數來傳遞。 當方法中的 `x` 變更時，基礎引數的值 (`n`) 也會變更。  
  
 [!code-csharp[csProgGuideParameters#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideParameters/CS/Parameters.cs#4)]  
  
 在此範例中，它不是所傳遞之 `n` 的值；而是傳遞對 `n` 的參考。 `x` 參數不是 [int](../../language-reference/builtin-types/integral-numeric-types.md)；它是對 `int` 的參考，在此案例中，為對 `n` 的參考。 因此，在方法內部將 `x` 平方時，實際平方的是 `x` 所參考的目標，即 `n`。  
  
## <a name="swapping-value-types"></a>交換實值型別  
 變更引數值的常見範例是 swap 方法，您會在其中將兩個變數傳遞至方法，而此方法會交換它們的內容。 您必須以傳址方式將引數傳遞至 swap 方法。 否則，您會交換方法內部參數的區域複本，而不會在呼叫方法中發生任何變更。 下例會交換整數值。  
  
 [!code-csharp[csProgGuideParameters#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideParameters/CS/Parameters.cs#5)]  
  
 當您呼叫 `SwapByRef` 方法時，請在呼叫中使用 `ref` 關鍵字，如下列範例所示。  
  
 [!code-csharp[csProgGuideParameters#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideParameters/CS/Parameters.cs#6)]  
  
## <a name="see-also"></a>另請參閱

- [C # 程式設計指南](../index.md)
- [傳遞參數](./passing-parameters.md)
- [傳遞參考型別參數](./passing-reference-type-parameters.md)
