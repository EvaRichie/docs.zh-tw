---
title: 如何：使用物件初始設定式宣告物件
ms.date: 07/20/2015
helpviewer_keywords:
- declaring objects using object initializer
- object initializers [Visual Basic]
- initializers [Visual Basic]
- Video How tos, Visual Basic
ms.assetid: 0f53a553-efd6-466d-80bf-6b679e5cd174
ms.openlocfilehash: cf4954059a4b0bf015bed82a74357ecfd5f5987e
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404871"
---
# <a name="how-to-declare-an-object-by-using-an-object-initializer-visual-basic"></a>如何：使用物件初始設定式宣告物件 (Visual Basic)
物件初始化運算式可讓您在單一語句中宣告及具現化類別的實例。 此外，您可以同時初始化實例的一個或多個成員，而不叫用參數化的函式。  
  
 當您使用物件初始化運算式建立命名類型的實例時，會呼叫類別的無參數的函式，然後依照您指定的順序初始化指定的成員。  
  
 下列程式說明如何使用 `Student` 三種不同的方式來建立類別的實例。 類別具有 [名字]、[姓氏] 和 [class year] 屬性等等。 這三個宣告中的每一個都會建立新的實例 `Student` ，並將屬性 `First` 設定為 "Michael"、 `Last` 將屬性設定為 "Tucker"，並將所有其他成員設定為其預設值。 程式中每個宣告的結果相當於下列範例，這不會使用物件初始化運算式。  
  
 [!code-vb[VbVbalrObjectInit#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class2.vb#20)]  
  
 如需類別的執行 `Student` 方式，請參閱[如何：建立專案清單](../../concepts/linq/how-to-create-a-list-of-items.md)。 您可以從該主題複製程式碼來設定類別，並建立 `Student` 要使用的物件清單。  
  
### <a name="to-create-an-object-of-a-named-class-by-using-an-object-initializer"></a>若要使用物件初始化運算式建立已命名類別的物件  
  
1. 開始宣告，就像您計畫使用的是一個函數。  
  
     `Dim student1 As New Student`  
  
2. 輸入關鍵字 `With` ，後面接著以大括弧括住的初始化清單。  
  
     `Dim student1 As New Student With { <initialization list> }`  
  
3. 在初始化清單中，包含您要初始化的每個屬性，並為其指派初始值。 屬性的名稱前面會加上句點。  
  
     [!code-vb[VbVbalrObjectInit#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class2.vb#21)]  
  
     您可以初始化類別的一個或多個成員。  
  
4. 或者，您可以宣告類別的新實例，然後為它指派值。 首先，宣告的實例 `Student` ：  
  
     `Dim student2 As Student`  
  
5. 以一般方式開始建立的實例 `Student` 。  
  
     `Dim student2 As Student = New Student`  
  
6. 輸入 `With` ，然後按物件初始化運算式，將新實例的一個或多個成員初始化。  
  
     [!code-vb[VbVbalrObjectInit#22](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class2.vb#22)]  
  
7. 您可以藉由省略來簡化上一個步驟中的定義 `As Student` 。 如果您這樣做，編譯器 `student3` 會 `Student` 使用區欄位型別推斷來判斷是的實例。  
  
     [!code-vb[VbVbalrObjectInit#23](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class2.vb#23)]  
  
     如需詳細資訊，請參閱[區欄位型別推斷](../variables/local-type-inference.md)。  
  
## <a name="see-also"></a>另請參閱

- [區域型別推斷](../variables/local-type-inference.md)
- [作法：建立項目清單](../../concepts/linq/how-to-create-a-list-of-items.md)
- [物件初始設定式：具名和匿名型別](object-initializers-named-and-anonymous-types.md)
- [匿名類型](anonymous-types.md)
