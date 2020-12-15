---
title: '如何定義抽象屬性-c # 程式設計手冊'
description: '瞭解如何在 c # 中定義抽象屬性。 宣告抽象屬性工作表示類別支援屬性。 衍生的類別會執行存取子。'
ms.date: 07/20/2015
helpviewer_keywords:
- properties [C#], abstract
- abstract properties [C#]
ms.topic: how-to
ms.custom: contperf-fy21q2
ms.assetid: 672a90eb-47b9-4ae0-9914-af53852fddcb
ms.openlocfilehash: e114e9349db9d6bcb18e15eb62532f48aa063339
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/15/2020
ms.locfileid: "97513025"
---
# <a name="how-to-define-abstract-properties-c-programming-guide"></a>如何定義抽象屬性 (c # 程式設計手冊) 

下例示範如何定義[抽象](../../language-reference/keywords/abstract.md)屬性。 抽象屬性宣告不提供屬性存取子實作 -- 它會宣告類別支援屬性，但保留衍生類別的存取子實作。 下例示範如何實作繼承自基底類別的抽象屬性。  
  
 這個範例包含三個檔案，每個檔案都是各自編譯，產生的組件是下次編譯參考的對象：  
  
- abstractshape.cs：包含抽象 `Area` 屬性的 `Shape` 類別。  
  
- shapes.cs：`Shape` 類別的子類別。  
  
- shapetest.cs：要顯示某些 `Shape` 衍生物件區域的測試程式。  
  
 若要編譯範例，請使用下列命令：  
  
 `csc abstractshape.cs shapes.cs shapetest.cs`  
  
 這會建立可執行檔 shapetest.exe。  
  
## <a name="example"></a>範例  

 這個檔案會宣告包含 `double` 類型 `Area` 屬性的 `Shape` 類別。  
  
 [!code-csharp[csProgGuideInheritance#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#1)]  
  
- 屬性的修飾詞是放在屬性宣告中。 例如︰  
  
    ```csharp  
    public abstract double Area  
    ```  
  
- 宣告抽象屬性時 (例如本例的 `Area`)，您只要指出有哪些屬性存取子可用即可，不用實作它們。 本例中只有 [get](../../language-reference/keywords/get.md) 存取子可用，所以此屬性是唯讀的。  
  
## <a name="example"></a>範例  

 下列程式碼會示範 `Shape` 的三個子類別，以及它們如何覆寫 `Area` 屬性以提供它們自己的實作。  
  
 [!code-csharp[csProgGuideInheritance#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#2)]  
  
## <a name="example"></a>範例  

 下列程式碼會示範測試程式，建立多個 `Shape` 衍生物件並列印其區域。  
  
 [!code-csharp[csProgGuideInheritance#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#3)]  
  
## <a name="see-also"></a>請參閱

- [C # 程式設計指南](../index.md)
- [類別和結構](./index.md)
- [抽象和密封類別以及類別成員](./abstract-and-sealed-classes-and-class-members.md)
- [屬性](./properties.md)
