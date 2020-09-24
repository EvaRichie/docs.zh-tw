---
description: internal - C# 參考
title: internal - C# 參考
ms.date: 07/20/2015
f1_keywords:
- internal_CSharpKeyword
- internal
helpviewer_keywords:
- internal keyword [C#]
ms.assetid: 6ee0785c-d7c8-49b8-bb72-0a4dfbcb6461
ms.openlocfilehash: c66f4ff578e9864ebaf2b89ec03ce95f3cb2ba91
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91168734"
---
# <a name="internal-c-reference"></a><span data-ttu-id="04853-103">internal (C# 參考)</span><span class="sxs-lookup"><span data-stu-id="04853-103">internal (C# Reference)</span></span>

<span data-ttu-id="04853-104">`internal` 關鍵字是類型和類型成員的[存取修飾詞](./access-modifiers.md)。</span><span class="sxs-lookup"><span data-stu-id="04853-104">The `internal` keyword is an [access modifier](./access-modifiers.md) for types and type members.</span></span>
  
 > <span data-ttu-id="04853-105">此頁面涵蓋 `internal` 存取。</span><span class="sxs-lookup"><span data-stu-id="04853-105">This page covers `internal` access.</span></span> <span data-ttu-id="04853-106">`internal`關鍵字也是存取修飾詞的一部分 [`protected internal`](./protected-internal.md) 。</span><span class="sxs-lookup"><span data-stu-id="04853-106">The `internal` keyword is also part of the [`protected internal`](./protected-internal.md) access modifier.</span></span>
  
<span data-ttu-id="04853-107">內部類型或成員只能在相同組件的檔案內存取，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="04853-107">Internal types or members are accessible only within files in the same assembly, as in this example:</span></span>  
  
```csharp  
public class BaseClass
{  
    // Only accessible within the same assembly.
    internal static int x = 0;
}  
```  

 <span data-ttu-id="04853-108">如需 `internal` 和其他存取修飾詞的比較，請參閱[存取範圍層級](./accessibility-levels.md)和[存取修飾詞](../../programming-guide/classes-and-structs/access-modifiers.md)。</span><span class="sxs-lookup"><span data-stu-id="04853-108">For a comparison of `internal` with the other access modifiers, see [Accessibility Levels](./accessibility-levels.md) and [Access Modifiers](../../programming-guide/classes-and-structs/access-modifiers.md).</span></span>  
  
 <span data-ttu-id="04853-109">如需組件的詳細資訊，請參閱 [.NET 中的組件](../../../standard/assembly/index.md)。</span><span class="sxs-lookup"><span data-stu-id="04853-109">For more information about assemblies, see [Assemblies in .NET](../../../standard/assembly/index.md).</span></span>  
  
 <span data-ttu-id="04853-110">內部存取常用於以元件為基礎的開發作業，因為它可讓一組元件私下相互合作，而不會公開給應用程式的其餘程式碼。</span><span class="sxs-lookup"><span data-stu-id="04853-110">A common use of internal access is in component-based development because it enables a group of components to cooperate in a private manner without being exposed to the rest of the application code.</span></span> <span data-ttu-id="04853-111">例如，建立圖形化使用者介面的架構可提供 `Control` 和 `Form` 類別，這兩個類別會以內部存取方式透過成員來相互合作。</span><span class="sxs-lookup"><span data-stu-id="04853-111">For example, a framework for building graphical user interfaces could provide `Control` and `Form` classes that cooperate by using members with internal access.</span></span> <span data-ttu-id="04853-112">由於這些是內部成員，因此不會公開給使用此架構的程式碼。</span><span class="sxs-lookup"><span data-stu-id="04853-112">Since these members are internal, they are not exposed to code that is using the framework.</span></span>  
  
 <span data-ttu-id="04853-113">在定義類型或成員的組件外部，以內部存取方式來參考此類型或成員是錯誤的做法。</span><span class="sxs-lookup"><span data-stu-id="04853-113">It is an error to reference a type or a member with internal access outside the assembly within which it was defined.</span></span>  
  
## <a name="example"></a><span data-ttu-id="04853-114">範例</span><span class="sxs-lookup"><span data-stu-id="04853-114">Example</span></span>  

 <span data-ttu-id="04853-115">此範例包含兩個檔案：`Assembly1.cs` 和 `Assembly1_a.cs`。</span><span class="sxs-lookup"><span data-stu-id="04853-115">This example contains two files, `Assembly1.cs` and `Assembly1_a.cs`.</span></span> <span data-ttu-id="04853-116">第一個檔案包含內部基底類別 `BaseClass`。</span><span class="sxs-lookup"><span data-stu-id="04853-116">The first file contains an internal base class, `BaseClass`.</span></span> <span data-ttu-id="04853-117">在第二個檔案中，嘗試具現化 `BaseClass` 會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="04853-117">In the second file, an attempt to instantiate `BaseClass` will produce an error.</span></span>  
  
```csharp  
// Assembly1.cs  
// Compile with: /target:library  
internal class BaseClass
{  
   public static int intM = 0;  
}  
```  
  
```csharp  
// Assembly1_a.cs  
// Compile with: /reference:Assembly1.dll  
class TestAccess
{  
   static void Main()
   {  
      var myBase = new BaseClass();   // CS0122  
   }  
}  
```  
  
## <a name="example"></a><span data-ttu-id="04853-118">範例</span><span class="sxs-lookup"><span data-stu-id="04853-118">Example</span></span>  

 <span data-ttu-id="04853-119">在此範例中，請使用您在範例 1 中所用的相同檔案，並將 `BaseClass` 的存取範圍層級變更為 `public`。</span><span class="sxs-lookup"><span data-stu-id="04853-119">In this example, use the same files you used in example 1, and change the accessibility level of `BaseClass` to `public`.</span></span> <span data-ttu-id="04853-120">同時將成員 `intM` 的存取範圍層級變更為 `internal`。</span><span class="sxs-lookup"><span data-stu-id="04853-120">Also change the accessibility level of the member `intM` to `internal`.</span></span> <span data-ttu-id="04853-121">在此情況下，您可以具現化類別，但無法存取內部成員。</span><span class="sxs-lookup"><span data-stu-id="04853-121">In this case, you can instantiate the class, but you cannot access the internal member.</span></span>  
  
```csharp  
// Assembly2.cs  
// Compile with: /target:library  
public class BaseClass
{  
   internal static int intM = 0;  
}  
```  
  
```csharp  
// Assembly2_a.cs  
// Compile with: /reference:Assembly2.dll  
public class TestAccess
{  
   static void Main()
   {  
      var myBase = new BaseClass();   // Ok.  
      BaseClass.intM = 444;    // CS0117  
   }  
}  
```  
  
## <a name="c-language-specification"></a><span data-ttu-id="04853-122">C# 語言規格</span><span class="sxs-lookup"><span data-stu-id="04853-122">C# Language Specification</span></span>  

<span data-ttu-id="04853-123">如需詳細資訊，請參閱 [C# 語言規格](/dotnet/csharp/language-reference/language-specification/introduction)的[已宣告存取範圍](~/_csharplang/spec/basic-concepts.md#declared-accessibility)。</span><span class="sxs-lookup"><span data-stu-id="04853-123">For more information, see [Declared accessibility](~/_csharplang/spec/basic-concepts.md#declared-accessibility) in the [C# Language Specification](/dotnet/csharp/language-reference/language-specification/introduction).</span></span> <span data-ttu-id="04853-124">語言規格是 C# 語法及用法的限定來源。</span><span class="sxs-lookup"><span data-stu-id="04853-124">The language specification is the definitive source for C# syntax and usage.</span></span>
  
## <a name="see-also"></a><span data-ttu-id="04853-125">另請參閱</span><span class="sxs-lookup"><span data-stu-id="04853-125">See also</span></span>

- [<span data-ttu-id="04853-126">C # 參考</span><span class="sxs-lookup"><span data-stu-id="04853-126">C# Reference</span></span>](../index.md)
- [<span data-ttu-id="04853-127">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="04853-127">C# Programming Guide</span></span>](../../programming-guide/index.md)
- [<span data-ttu-id="04853-128">C # 關鍵字</span><span class="sxs-lookup"><span data-stu-id="04853-128">C# Keywords</span></span>](./index.md)
- [<span data-ttu-id="04853-129">存取修飾詞</span><span class="sxs-lookup"><span data-stu-id="04853-129">Access Modifiers</span></span>](./access-modifiers.md)
- [<span data-ttu-id="04853-130">協助工具層級</span><span class="sxs-lookup"><span data-stu-id="04853-130">Accessibility Levels</span></span>](./accessibility-levels.md)
- [<span data-ttu-id="04853-131">修飾詞</span><span class="sxs-lookup"><span data-stu-id="04853-131">Modifiers</span></span>](index.md)
- [<span data-ttu-id="04853-132">public</span><span class="sxs-lookup"><span data-stu-id="04853-132">public</span></span>](./public.md)
- [<span data-ttu-id="04853-133">private</span><span class="sxs-lookup"><span data-stu-id="04853-133">private</span></span>](./private.md)
- [<span data-ttu-id="04853-134">protected</span><span class="sxs-lookup"><span data-stu-id="04853-134">protected</span></span>](./protected.md)
