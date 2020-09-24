---
title: 傳遞參考類型的參數 - C# 程式設計手冊
description: '當您在 c # 中以傳值方式傳遞參考型別參數時，參考物件中的資料可能會變更，但不能變更參考本身的值。'
ms.date: 07/20/2015
helpviewer_keywords:
- method parameters [C#], reference types
- parameters [C#], reference
ms.assetid: 9e6eb65c-942e-48ab-920a-b7ba9df4ea20
ms.openlocfilehash: 315c1193de12a8fb5c066e023bb98bc228ce85bb
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91154115"
---
# <a name="passing-reference-type-parameters-c-programming-guide"></a>傳遞參考類型的參數 (C# 程式設計手冊)

[參考型別](../../language-reference/keywords/reference-types.md)的變數不會直接包含其資料；它會包含其資料的參考。 以值的方式傳遞參考型別參數時，可以變更屬於參考資料的資料，例如類別成員的值。 但您無法變更參考本身的值；例如，您無法使用相同的參考，為新的物件配置記憶體，並讓其保存在方法之外。 若要這樣做，請使用 [ref](../../language-reference/keywords/ref.md) 或 [out](../../language-reference/keywords/out-parameter-modifier.md) 關鍵字來傳遞參數。 為求簡化，下列範例使用 `ref`。  
  
## <a name="passing-reference-types-by-value"></a>以傳值方式傳遞參考型別  

 下列範例示範以傳值方式將 `arr` 參考型別參數傳遞至 `Change` 方法。 因為參數是對 `arr` 的參考，所以可以變更陣列元素的值。 不過，嘗試將參數重新指派至不同的記憶體位置只能在方法內運作，而且不會影響原始的 `arr` 變數。  
  
 [!code-csharp[csProgGuideParameters#7](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideParameters/CS/Parameters.cs#7)]  
  
 在上述範例中，作為參考型別的 `arr` 陣列傳遞至方法時，不會使用 `ref` 參數。 在這種情況下，指向 `arr` 的參考複本會傳遞至方法。 輸出顯示方法可以變更陣列元素的內容，在此情況下為 `1` 到 `888`。 不過，在 `Change` 方法內部使用 [new](../../language-reference/operators/new-operator.md) 運算子來配置新的記憶體部分，會讓 `pArray` 參數參考新的陣列。 因此，之後的任何變更將不會影響在 `Main` 內部建立的 `arr` 原始陣列。 事實上，在此範例中會建立兩個陣列，一個在 `Main` 內部，另一個在 `Change` 方法內部。  
  
## <a name="passing-reference-types-by-reference"></a>以傳址式傳遞參考型別  

 下列範例與上述範例相同，差別在於 `ref` 關鍵字會新增方法標題和呼叫。 任何在方法中進行的變更會影響呼叫端程式中的原始變數。  
  
 [!code-csharp[csProgGuideParameters#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideParameters/CS/Parameters.cs#8)]  
  
 方法內部進行的所有變更都會影響 `Main` 中的原始陣列。 事實上，原始陣列會使用 `new` 運算子重新配置。 因此，在呼叫 `Change` 方法之後，所有對 `arr` 的參考都會指向在 `Change` 方法中建立的五個項目陣列。  
  
## <a name="swapping-two-strings"></a>交換兩個字串  

 以傳址方式傳遞參考型別參數的絶佳範例就是交換字串。 在此範例中，`str1` 和 `str2` 兩個字串會在 `Main` 中初始化，並作為 `ref` 關鍵字修改的參數傳遞給 `SwapStrings` 方法。 兩個字串也會在方法和 `Main` 內部交換。  
  
 [!code-csharp[csProgGuideParameters#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideParameters/CS/Parameters.cs#9)]  
  
 在此範例中，參數需要以傳址方式傳遞以影響呼叫端程式中的變數。 如果您移除了方法標頭和方法呼叫中的 `ref` 關鍵字，就不會在呼叫端程式中進行任何變更。  
  
 如需字串的詳細資訊，請參閱 [string](../../language-reference/builtin-types/reference-types.md)。  
  
## <a name="see-also"></a>另請參閱

- [C # 程式設計指南](../index.md)
- [傳遞參數](./passing-parameters.md)
- [ref](../../language-reference/keywords/ref.md)
- [in](../../language-reference/keywords/in-parameter-modifier.md)
- [out](../../language-reference/keywords/out.md)
- [參考型別](../../language-reference/keywords/reference-types.md)
