---
title: '具有命名與匿名方法的委派-c # 程式設計手冊'
description: 瞭解具有命名與匿名方法的委派。 請參閱程式碼範例，並查看其他可用的資源。
ms.date: 07/20/2015
helpviewer_keywords:
- delegates [C#], with named vs. anonymous methods
- methods [C#], in delegates
ms.assetid: 98fa8c61-66b6-4146-986c-3236c4045733
ms.openlocfilehash: 940363b87e17b34feeffaff38ed498d6fcf6850a
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87302746"
---
# <a name="delegates-with-named-vs-anonymous-methods-c-programming-guide"></a>使用具名和匿名方法委派的比較 (C# 程式設計手冊)
[delegate](../../language-reference/builtin-types/reference-types.md) 可以與具名方法產生關聯。 當您使用具名方法具現化委派時，方法會當做參數傳遞，例如：  
  
 [!code-csharp[csProgGuideDelegates#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDelegates/CS/Delegates.cs#1)]  
  
 這會使用具名方法呼叫。 使用具名方法建構的委派可封裝[靜態](../../language-reference/keywords/static.md)方法或執行個體方法。 在舊版 C# 中，要具現化委派只能使用具名方法。 不過，如果建立新方法會產生額外不必要的負荷，C# 可讓您具現化委派，並立即指定呼叫委派時會處理的程式碼區塊。 區塊可以包含 Lambda 運算式或匿名方法。 如需詳細資訊，請參閱[匿名函式](../statements-expressions-operators/anonymous-functions.md)。  
  
## <a name="remarks"></a>備註  
 當做委派參數傳遞的方法必須擁有與委派宣告相同的簽章。  
  
 委派執行個體可封裝靜態或執行個體方法。  
  
 即使委派可使用 [out](../../language-reference/keywords/out-parameter-modifier.md) 參數，但仍不建議您用於多點傳送事件委派，因為無從得知將呼叫哪一個委派。  
  
## <a name="example-1"></a>範例 1  
 以下是宣告和使用委派的簡單範例。 請注意，委派 `Del` 和相關聯的方法 `MultiplyNumbers` 必須擁有相同的簽章  
  
 [!code-csharp[csProgGuideDelegates#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDelegates/CS/Delegates.cs#2)]  
  
## <a name="example-2"></a>範例 2  
 在下列範例中，一個委派會同時對應到靜態和執行個體方法，並傳回每個方法的特定資訊。  
  
 [!code-csharp[csProgGuideDelegates#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDelegates/CS/Delegates.cs#3)]  
  
## <a name="see-also"></a>另請參閱

- [C # 程式設計指南](../index.md)
- [委派](./index.md)
- [如何合併委派（多播委派）](./how-to-combine-delegates-multicast-delegates.md)
- [事件](../events/index.md)
