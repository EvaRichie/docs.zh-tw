---
title: 泛型委派 - C# 程式設計指南
description: '瞭解如何在 c # 中使用泛型委派。 請參閱程式碼範例，並檢視其他可用的資源。'
ms.date: 07/20/2015
helpviewer_keywords:
- generics [C#], delegates
- delegates [C#], generic
ms.assetid: bdea509c-44c1-4309-aaa9-15c7aee009df
ms.openlocfilehash: df417701feb77dc47cff1cdd68eb4c7405d15beb
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91157404"
---
# <a name="generic-delegates-c-programming-guide"></a><span data-ttu-id="d8282-104">泛型委派 (C# 程式設計手冊)</span><span class="sxs-lookup"><span data-stu-id="d8282-104">Generic Delegates (C# Programming Guide)</span></span>

<span data-ttu-id="d8282-105">[委派](../../language-reference/builtin-types/reference-types.md)可以定義自己的型別參數。</span><span class="sxs-lookup"><span data-stu-id="d8282-105">A [delegate](../../language-reference/builtin-types/reference-types.md) can define its own type parameters.</span></span> <span data-ttu-id="d8282-106">參考泛型委派的程式碼，可以指定型別引數建立封閉式建構類型，就像在具現化泛型類別或呼叫泛型方法時一樣，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="d8282-106">Code that references the generic delegate can specify the type argument to create a closed constructed type, just like when instantiating a generic class or calling a generic method, as shown in the following example:</span></span>  
  
 [!code-csharp[csProgGuideGenerics#36](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#36)]  
  
 <span data-ttu-id="d8282-107">C# 2.0 版具有方法群組轉換新功能，適用於實體及泛型委派類型，並可讓您使用這個簡化的語法撰寫上一行：</span><span class="sxs-lookup"><span data-stu-id="d8282-107">C# version 2.0 has a new feature called method group conversion, which applies to concrete as well as generic delegate types, and enables you to write the previous line with this simplified syntax:</span></span>  
  
 [!code-csharp[csProgGuideGenerics#37](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#37)]  
  
 <span data-ttu-id="d8282-108">在泛型類別中定義的委派，可以使用和類別方法相同的方式，使用泛型類別類型參數。</span><span class="sxs-lookup"><span data-stu-id="d8282-108">Delegates defined within a generic class can use the generic class type parameters in the same way that class methods do.</span></span>  
  
 [!code-csharp[csProgGuideGenerics#38](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#38)]  
  
 <span data-ttu-id="d8282-109">參考委派的程式碼必須指定包含類別的型別引數，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d8282-109">Code that references the delegate must specify the type argument of the containing class, as follows:</span></span>  
  
 [!code-csharp[csProgGuideGenerics#39](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#39)]  
  
 <span data-ttu-id="d8282-110">泛型委派在根據一般設計模式定義事件方面特別有幫助，因為傳送者引數可以是強型別，不必再在 <xref:System.Object> 間來回轉換。</span><span class="sxs-lookup"><span data-stu-id="d8282-110">Generic delegates are especially useful in defining events based on the typical design pattern because the sender argument can be strongly typed and no longer has to be cast to and from <xref:System.Object>.</span></span>  
  
 [!code-csharp[csProgGuideGenerics#40](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#40)]  
  
## <a name="see-also"></a><span data-ttu-id="d8282-111">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d8282-111">See also</span></span>

- <xref:System.Collections.Generic>
- [<span data-ttu-id="d8282-112">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="d8282-112">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="d8282-113">泛型簡介</span><span class="sxs-lookup"><span data-stu-id="d8282-113">Introduction to Generics</span></span>](./index.md)
- [<span data-ttu-id="d8282-114">泛型方法</span><span class="sxs-lookup"><span data-stu-id="d8282-114">Generic Methods</span></span>](./generic-methods.md)
- [<span data-ttu-id="d8282-115">泛型類別</span><span class="sxs-lookup"><span data-stu-id="d8282-115">Generic Classes</span></span>](./generic-classes.md)
- [<span data-ttu-id="d8282-116">泛型介面</span><span class="sxs-lookup"><span data-stu-id="d8282-116">Generic Interfaces</span></span>](./generic-interfaces.md)
- [<span data-ttu-id="d8282-117">委派</span><span class="sxs-lookup"><span data-stu-id="d8282-117">Delegates</span></span>](../delegates/index.md)
- [<span data-ttu-id="d8282-118">泛型</span><span class="sxs-lookup"><span data-stu-id="d8282-118">Generics</span></span>](../../../standard/generics/index.md)
