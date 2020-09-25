---
title: 委派 - C# 程式設計手冊
description: 'C # 中的委派是參考具有參數清單和傳回型別之方法的型別。 委派可以用來將方法當做引數傳遞給其他方法。'
ms.date: 07/20/2015
helpviewer_keywords:
- C# language, delegates
- delegates [C#]
ms.assetid: 97de039b-c76b-4b9c-a27d-8c1e1c8d93da
ms.openlocfilehash: 7365cb89ad617148fb26d5a01c07f13a7888bbf8
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91178693"
---
# <a name="delegates-c-programming-guide"></a>委派 (C# 程式設計手冊)

[委派](../../language-reference/builtin-types/reference-types.md)是一種類型，代表具有特定參數清單及傳回型別的方法參考。 當您具現化委派時，可以將其執行個體與任何具有相容簽章和傳回型別的方法產生關聯。 您可以透過委派執行個體叫用 (或呼叫) 方法。  
  
 委派可以用來將方法當做引數傳遞給其他方法。 事件處理常式就是透過委派叫用的方法。 建立自訂方法後，像是 Windows 控制項這樣的類別就會在特定事件發生時呼叫您的方法。 下列範例將示範委派宣告：  
  
 [!code-csharp[csProgGuideDelegates#20](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDelegates/CS/Delegates.cs#20)]  
  
 來自符合委派類型之任何可存取類別或結構的任何方法都可以指派給委派。 方法可以是靜態或執行個體方法。 如此即可用程式設計的方式變更方法呼叫，也可將新的程式碼插入現有的類別中。  
  
> [!NOTE]
> 在方法多載的內容中，方法的簽章並不包括傳回值。 不過在委派的內容中，簽章卻包含傳回值。 換句話說，方法必須與委派擁有相同的傳回類型。  
  
 由於委派能夠將方法當做參數來參考，因此很適合用來定義回呼方法。 例如，可以將比較兩個物件的方法參考當成引數傳遞至排序演算法。 因為比較程式碼是在獨立的程序中，因此排序演算法可以用較普通的方式撰寫。  
  
## <a name="delegates-overview"></a>委派概觀  

 委派包含下列屬性：  
  
- 委派與 C++ 函式指標相似，但委派完全為物件導向，而且不像 C++ 指標之於成員函式，會同時委派封裝物件執行個體與方法。
  
- 委派允許將方法當做參數傳遞。  
  
- 委派可用於定義回呼方法。  
  
- 您可將委派鏈結在一起，例如，可在單一事件上呼叫多個方法。  
  
- 方法不需要完全符合委派類型。 如需詳細資訊，請參閱[在委派中使用差異](../concepts/covariance-contravariance/using-variance-in-delegates.md)。  
  
- C # 2.0 版引進了 [匿名方法](../../language-reference/operators/delegate-operator.md)的概念，可讓程式碼區塊以參數的形式傳遞，以取代個別定義的方法。 C# 3.0 引進了 Lambda 運算式，做為更簡潔的內嵌 (Inline) 程式碼區塊撰寫方式。 匿名方法與 Lambda 運算式 (在特定內容中) 都會編譯為委派類型。 現在，這些功能合稱為「匿名函式」(Anonymous Function)。 如需 Lambda 運算式的詳細資訊，請參閱 [Lambda 運算式](../../language-reference/operators/lambda-expressions.md)。
  
## <a name="in-this-section"></a>本節內容  
  
- [使用委派](./using-delegates.md)  
  
- [何時應使用委派，而不使用介面 (C# 程式設計指南)](/previous-versions/visualstudio/visual-studio-2010/ms173173(v=vs.100))  
  
- [具名方法委派與匿名方法](./delegates-with-named-vs-anonymous-methods.md)  
  
- [在委派中使用變異數](../concepts/covariance-contravariance/using-variance-in-delegates.md)  
  
- [如何將委派合併 (多播委派) ](./how-to-combine-delegates-multicast-delegates.md)  
  
- [如何宣告、具現化和使用委派](./how-to-declare-instantiate-and-use-a-delegate.md)

## <a name="c-language-specification"></a>C# 語言規格  

如需詳細資訊，請參閱 [C# 語言規格](/dotnet/csharp/language-reference/language-specification/introduction)中的[委派](~/_csharplang/spec/delegates.md)。 語言規格是 C# 語法及用法的限定來源。
  
## <a name="featured-book-chapters"></a>精選書籍章節  

 [C# 3.0 Cookbook, Third Edition: More than 250 solutions for C# 3.0 programmers](/previous-versions/visualstudio/visual-studio-2008/ff518994(v=orm.10)) (C# 3.0 Cookbook 第三版：250 個以上 C# 3.0 程式設計人員適用的方案) 中的 [Delegates, Events, and Lambda Expressions](/previous-versions/visualstudio/visual-studio-2008/ff518995(v=orm.10))  
  
 [Delegates and Events](/previous-versions/visualstudio/visual-studio-2008/ff652490(v=orm.10)) in [Learning C# 3.0: Master the fundamentals of C# 3.0](/previous-versions/visualstudio/visual-studio-2008/ff652493(v=orm.10))  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Delegate>
- [C # 程式設計指南](../index.md)
- [事件](../events/index.md)
