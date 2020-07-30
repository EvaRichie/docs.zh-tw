---
title: 命名空間 - C# 程式設計手冊
description: '瞭解 c # 程式設計中的命名空間。 請參閱命名空間屬性的總覽並查看其他資源。'
ms.date: 08/21/2018
helpviewer_keywords:
- C# language, namespaces
- namespaces [C#]
ms.assetid: b1c4ab46-3fad-4ffa-9deb-dd50a2d8c65a
ms.openlocfilehash: fca2c641520bd9cd19a48bff2119a6f09c3713ea
ms.sourcegitcommit: 552b4b60c094559db9d8178fa74f5bafaece0caf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87382096"
---
# <a name="namespaces-c-programming-guide"></a><span data-ttu-id="34d2f-104">命名空間 (C# 程式設計手冊)</span><span class="sxs-lookup"><span data-stu-id="34d2f-104">Namespaces (C# Programming Guide)</span></span>

<span data-ttu-id="34d2f-105">C# 程式設計大量使用命名空間的原因有兩個。</span><span class="sxs-lookup"><span data-stu-id="34d2f-105">Namespaces are heavily used in C# programming in two ways.</span></span> <span data-ttu-id="34d2f-106">首先，.NET 會使用命名空間來組織其許多類別，如下所示：</span><span class="sxs-lookup"><span data-stu-id="34d2f-106">First, .NET uses namespaces to organize its many classes, as follows:</span></span>  

[!code-csharp[csProgGuide#22](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuide/CS/progGuide.cs#22)]

<span data-ttu-id="34d2f-107"><xref:System> 是命名空間，而 <xref:System.Console> 是該命名空間中的類別。</span><span class="sxs-lookup"><span data-stu-id="34d2f-107"><xref:System> is a namespace and <xref:System.Console> is a class in that namespace.</span></span> <span data-ttu-id="34d2f-108">您可以使用 `using` 關鍵字，如此就不需要完整名稱，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="34d2f-108">The `using` keyword can be used so that the complete name is not required, as in the following example:</span></span>

[!code-csharp[csProgGuide#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuide/CS/using.cs#1)]

[!code-csharp[csProgGuide#25](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuide/CS/progGuide.cs#25)]

<span data-ttu-id="34d2f-109">如需詳細資訊，請參閱 [using 指示詞](../../language-reference/keywords/using-directive.md)。</span><span class="sxs-lookup"><span data-stu-id="34d2f-109">For more information, see the [using Directive](../../language-reference/keywords/using-directive.md).</span></span>

<span data-ttu-id="34d2f-110">其次，宣告您自己的命名空間，將有助於在較大型的程式設計專案中控制類別和方法名稱的範圍。</span><span class="sxs-lookup"><span data-stu-id="34d2f-110">Second, declaring your own namespaces can help you control the scope of class and method names in larger programming projects.</span></span> <span data-ttu-id="34d2f-111">請使用 [namespace](../../language-reference/keywords/namespace.md) 關鍵字宣告命名空間，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="34d2f-111">Use the [namespace](../../language-reference/keywords/namespace.md) keyword to declare a namespace, as in the following example:</span></span>

[!code-csharp[csProgGuideNamespaces#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideNamespaces/CS/Namespaces.cs#6)]

<span data-ttu-id="34d2f-112">命名空間的名稱必須是有效的 C# [識別碼名稱](../inside-a-program/identifier-names.md)。</span><span class="sxs-lookup"><span data-stu-id="34d2f-112">The name of the namespace must be a valid C# [identifier name](../inside-a-program/identifier-names.md).</span></span>

## <a name="namespaces-overview"></a><span data-ttu-id="34d2f-113">命名空間總覽</span><span class="sxs-lookup"><span data-stu-id="34d2f-113">Namespaces overview</span></span>

<span data-ttu-id="34d2f-114">命名空間具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="34d2f-114">Namespaces have the following properties:</span></span>

- <span data-ttu-id="34d2f-115">命名空間可組織大型程式碼專案。</span><span class="sxs-lookup"><span data-stu-id="34d2f-115">They organize large code projects.</span></span>
- <span data-ttu-id="34d2f-116">命名空間會使用 `.` 運算子分隔。</span><span class="sxs-lookup"><span data-stu-id="34d2f-116">They are delimited by using the `.` operator.</span></span>
- <span data-ttu-id="34d2f-117">`using` 指示詞讓您不需要指定每個類別的命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="34d2f-117">The `using` directive obviates the requirement to specify the name of the namespace for every class.</span></span>
- <span data-ttu-id="34d2f-118">`global` 命名空間是「根」命名空間：`global::System` 一律會參考 .NET <xref:System> 命名空間。</span><span class="sxs-lookup"><span data-stu-id="34d2f-118">The `global` namespace is the "root" namespace: `global::System` will always refer to the .NET <xref:System> namespace.</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="34d2f-119">C# 語言規格</span><span class="sxs-lookup"><span data-stu-id="34d2f-119">C# language specification</span></span>

<span data-ttu-id="34d2f-120">如需詳細資訊，請參閱 [C# 語言規格](~/_csharplang/spec/introduction.md)的[命名空間](~/_csharplang/spec/namespaces.md)一節。</span><span class="sxs-lookup"><span data-stu-id="34d2f-120">For more information, see the [Namespaces](~/_csharplang/spec/namespaces.md) section of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="34d2f-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="34d2f-121">See also</span></span>

- [<span data-ttu-id="34d2f-122">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="34d2f-122">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="34d2f-123">使用命名空間</span><span class="sxs-lookup"><span data-stu-id="34d2f-123">Using Namespaces</span></span>](using-namespaces.md)
- [<span data-ttu-id="34d2f-124">如何使用 My 命名空間</span><span class="sxs-lookup"><span data-stu-id="34d2f-124">How to use the My namespace</span></span>](how-to-use-the-my-namespace.md)
- [<span data-ttu-id="34d2f-125">識別碼名稱</span><span class="sxs-lookup"><span data-stu-id="34d2f-125">Identifier names</span></span>](../inside-a-program/identifier-names.md)
- [<span data-ttu-id="34d2f-126">using 指示詞</span><span class="sxs-lookup"><span data-stu-id="34d2f-126">using Directive</span></span>](../../language-reference/keywords/using-directive.md)
- [<span data-ttu-id="34d2f-127">：：運算子</span><span class="sxs-lookup"><span data-stu-id="34d2f-127">:: Operator</span></span>](../../language-reference/operators/namespace-alias-qualifier.md)
