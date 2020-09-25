---
title: '具有命名與匿名方法的委派-c # 程式設計手冊'
description: 深入瞭解具有命名和匿名方法的委派。 請參閱程式碼範例，並檢視其他可用的資源。
ms.date: 07/20/2015
helpviewer_keywords:
- delegates [C#], with named vs. anonymous methods
- methods [C#], in delegates
ms.assetid: 98fa8c61-66b6-4146-986c-3236c4045733
ms.openlocfilehash: d8d2c6d8c7792b81f2fc2e25d0836e3780e58e52
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91202496"
---
# <a name="delegates-with-named-vs-anonymous-methods-c-programming-guide"></a><span data-ttu-id="9454b-104">使用具名和匿名方法委派的比較 (C# 程式設計手冊)</span><span class="sxs-lookup"><span data-stu-id="9454b-104">Delegates with Named vs. Anonymous Methods (C# Programming Guide)</span></span>

<span data-ttu-id="9454b-105">[delegate](../../language-reference/builtin-types/reference-types.md) 可以與具名方法產生關聯。</span><span class="sxs-lookup"><span data-stu-id="9454b-105">A [delegate](../../language-reference/builtin-types/reference-types.md) can be associated with a named method.</span></span> <span data-ttu-id="9454b-106">當您使用具名方法具現化委派時，方法會當做參數傳遞，例如：</span><span class="sxs-lookup"><span data-stu-id="9454b-106">When you instantiate a delegate by using a named method, the method is passed as a parameter, for example:</span></span>  
  
 [!code-csharp[csProgGuideDelegates#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDelegates/CS/Delegates.cs#1)]  
  
 <span data-ttu-id="9454b-107">這會使用具名方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="9454b-107">This is called using a named method.</span></span> <span data-ttu-id="9454b-108">使用具名方法建構的委派可封裝[靜態](../../language-reference/keywords/static.md)方法或執行個體方法。</span><span class="sxs-lookup"><span data-stu-id="9454b-108">Delegates constructed with a named method can encapsulate either a [static](../../language-reference/keywords/static.md) method or an instance method.</span></span> <span data-ttu-id="9454b-109">在舊版 C# 中，要具現化委派只能使用具名方法。</span><span class="sxs-lookup"><span data-stu-id="9454b-109">Named methods are the only way to instantiate a delegate in earlier versions of C#.</span></span> <span data-ttu-id="9454b-110">不過，如果建立新方法會產生額外不必要的負荷，C# 可讓您具現化委派，並立即指定呼叫委派時會處理的程式碼區塊。</span><span class="sxs-lookup"><span data-stu-id="9454b-110">However, in a situation where creating a new method is unwanted overhead, C# enables you to instantiate a delegate and immediately specify a code block that the delegate will process when it is called.</span></span> <span data-ttu-id="9454b-111">區塊可以包含 Lambda 運算式或匿名方法。</span><span class="sxs-lookup"><span data-stu-id="9454b-111">The block can contain either a lambda expression or an anonymous method.</span></span> <span data-ttu-id="9454b-112">如需詳細資訊，請參閱[匿名函式](../statements-expressions-operators/anonymous-functions.md)。</span><span class="sxs-lookup"><span data-stu-id="9454b-112">For more information, see [Anonymous Functions](../statements-expressions-operators/anonymous-functions.md).</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="9454b-113">備註</span><span class="sxs-lookup"><span data-stu-id="9454b-113">Remarks</span></span>  

 <span data-ttu-id="9454b-114">當做委派參數傳遞的方法必須擁有與委派宣告相同的簽章。</span><span class="sxs-lookup"><span data-stu-id="9454b-114">The method that you pass as a delegate parameter must have the same signature as the delegate declaration.</span></span>  
  
 <span data-ttu-id="9454b-115">委派執行個體可封裝靜態或執行個體方法。</span><span class="sxs-lookup"><span data-stu-id="9454b-115">A delegate instance may encapsulate either static or instance method.</span></span>  
  
 <span data-ttu-id="9454b-116">即使委派可使用 [out](../../language-reference/keywords/out-parameter-modifier.md) 參數，但仍不建議您用於多點傳送事件委派，因為無從得知將呼叫哪一個委派。</span><span class="sxs-lookup"><span data-stu-id="9454b-116">Although the delegate can use an [out](../../language-reference/keywords/out-parameter-modifier.md) parameter, we do not recommend its use with multicast event delegates because you cannot know which delegate will be called.</span></span>  
  
## <a name="example-1"></a><span data-ttu-id="9454b-117">範例 1</span><span class="sxs-lookup"><span data-stu-id="9454b-117">Example 1</span></span>  

 <span data-ttu-id="9454b-118">以下是宣告和使用委派的簡單範例。</span><span class="sxs-lookup"><span data-stu-id="9454b-118">The following is a simple example of declaring and using a delegate.</span></span> <span data-ttu-id="9454b-119">請注意，委派 `Del` 和相關聯的方法 `MultiplyNumbers` 必須擁有相同的簽章</span><span class="sxs-lookup"><span data-stu-id="9454b-119">Notice that both the delegate, `Del`, and the associated method, `MultiplyNumbers`, have the same signature</span></span>  
  
 [!code-csharp[csProgGuideDelegates#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDelegates/CS/Delegates.cs#2)]  
  
## <a name="example-2"></a><span data-ttu-id="9454b-120">範例 2</span><span class="sxs-lookup"><span data-stu-id="9454b-120">Example 2</span></span>  

 <span data-ttu-id="9454b-121">在下列範例中，一個委派會同時對應到靜態和執行個體方法，並傳回每個方法的特定資訊。</span><span class="sxs-lookup"><span data-stu-id="9454b-121">In the following example, one delegate is mapped to both static and instance methods and returns specific information from each.</span></span>  
  
 [!code-csharp[csProgGuideDelegates#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDelegates/CS/Delegates.cs#3)]  
  
## <a name="see-also"></a><span data-ttu-id="9454b-122">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9454b-122">See also</span></span>

- [<span data-ttu-id="9454b-123">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="9454b-123">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="9454b-124">委派</span><span class="sxs-lookup"><span data-stu-id="9454b-124">Delegates</span></span>](./index.md)
- [<span data-ttu-id="9454b-125">如何將委派合併 (多播委派) </span><span class="sxs-lookup"><span data-stu-id="9454b-125">How to combine delegates (Multicast Delegates)</span></span>](./how-to-combine-delegates-multicast-delegates.md)
- [<span data-ttu-id="9454b-126">事件</span><span class="sxs-lookup"><span data-stu-id="9454b-126">Events</span></span>](../events/index.md)
