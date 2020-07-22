---
title: 使用 Override 和 New 關鍵字進行版本控制 - C# 程式設計手冊
description: '瞭解 c # 中基底和衍生類別的版本控制，以及如何指定方法是否要覆寫或隱藏繼承的方法。'
ms.date: 07/20/2015
helpviewer_keywords:
- C# language, versioning
- C# language, override and new
ms.assetid: 88247d07-bd0d-49e9-a619-45ccbbfdf0c5
ms.openlocfilehash: c2630741e1055a14dd5b9e4445d660cfd68891b0
ms.sourcegitcommit: 3d84eac0818099c9949035feb96bbe0346358504
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/21/2020
ms.locfileid: "86863860"
---
# <a name="versioning-with-the-override-and-new-keywords-c-programming-guide"></a><span data-ttu-id="14b9b-103">使用 Override 和 New 關鍵字進行版本控制 (C# 程式設計手冊)</span><span class="sxs-lookup"><span data-stu-id="14b9b-103">Versioning with the Override and New Keywords (C# Programming Guide)</span></span>
<span data-ttu-id="14b9b-104">C# 語言的設計，就是讓不同文件庫的[基底](../../language-reference/keywords/base.md)和衍生類別的版本控制能夠發展兼具回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="14b9b-104">The C# language is designed so that versioning between [base](../../language-reference/keywords/base.md) and derived classes in different libraries can evolve and maintain backward compatibility.</span></span> <span data-ttu-id="14b9b-105">例如，這表示 C# 完全支援在基底[類別](../../language-reference/keywords/class.md)中引入與衍生類別成員同名的新成員，不會導致非預期的行為。</span><span class="sxs-lookup"><span data-stu-id="14b9b-105">This means, for example, that the introduction of a new member in a base [class](../../language-reference/keywords/class.md) with the same name as a member in a derived class is completely supported by C# and does not lead to unexpected behavior.</span></span> <span data-ttu-id="14b9b-106">這也表示，類別必須明確指出方法是打算覆寫繼承的方法，還是方法是一種新方法，會隱藏名稱相似的繼承方法。</span><span class="sxs-lookup"><span data-stu-id="14b9b-106">It also means that a class must explicitly state whether a method is intended to override an inherited method, or whether a method is a new method that hides a similarly named inherited method.</span></span>  
  
 <span data-ttu-id="14b9b-107">在 C# 中，衍生類別可以包含與基底類別方法同名的方法。</span><span class="sxs-lookup"><span data-stu-id="14b9b-107">In C#, derived classes can contain methods with the same name as base class methods.</span></span>  

- <span data-ttu-id="14b9b-108">如果衍生類別中的方法前未加上 [new](../../language-reference/keywords/new-modifier.md) 或 [override](../../language-reference/keywords/override.md) 關鍵字，編譯器就會發出警告，方法會表現為如同有 `new` 關鍵字。</span><span class="sxs-lookup"><span data-stu-id="14b9b-108">If the method in the derived class is not preceded by [new](../../language-reference/keywords/new-modifier.md) or [override](../../language-reference/keywords/override.md) keywords, the compiler will issue a warning and the method will behave as if the `new` keyword were present.</span></span>  
  
- <span data-ttu-id="14b9b-109">如果衍生類別中的方法前面加上 `new` 關鍵字，方法會定義為不受基底類別中的方法影響。</span><span class="sxs-lookup"><span data-stu-id="14b9b-109">If the method in the derived class is preceded with the `new` keyword, the method is defined as being independent of the method in the base class.</span></span>  
  
- <span data-ttu-id="14b9b-110">如果衍生類別中的方法前面加上 `override` 關鍵字，衍生類別的物件會呼叫該方法，不會呼叫基底類別方法。</span><span class="sxs-lookup"><span data-stu-id="14b9b-110">If the method in the derived class is preceded with the `override` keyword, objects of the derived class will call that method instead of the base class method.</span></span>  

- <span data-ttu-id="14b9b-111">為了將 `override` 關鍵字套用至衍生類別中的方法，基類方法必須定義為[virtual](../../language-reference/keywords/virtual.md)。</span><span class="sxs-lookup"><span data-stu-id="14b9b-111">In order to apply the `override` keyword to the method in the derived class, the base class method must be defined [virtual](../../language-reference/keywords/virtual.md).</span></span>
  
- <span data-ttu-id="14b9b-112">您可以使用 `base` 關鍵字從衍生類別中呼叫基底類別方法。</span><span class="sxs-lookup"><span data-stu-id="14b9b-112">The base class method can be called from within the derived class using the `base` keyword.</span></span>  
  
- <span data-ttu-id="14b9b-113">`override`、`virtual` 和 `new` 關鍵字也可以套用至屬性、索引子和事件。</span><span class="sxs-lookup"><span data-stu-id="14b9b-113">The `override`, `virtual`, and `new` keywords can also be applied to properties, indexers, and events.</span></span>  
  
 <span data-ttu-id="14b9b-114">C# 方法預設不是虛擬的。</span><span class="sxs-lookup"><span data-stu-id="14b9b-114">By default, C# methods are not virtual.</span></span> <span data-ttu-id="14b9b-115">如果方法宣告為虛擬，則繼承該方法的任何類別都可以實作自己的版本。</span><span class="sxs-lookup"><span data-stu-id="14b9b-115">If a method is declared as virtual, any class inheriting the method can implement its own version.</span></span> <span data-ttu-id="14b9b-116">若要使方法成為虛擬的，基底類別的方法宣告中會使用 `virtual` 修飾詞。</span><span class="sxs-lookup"><span data-stu-id="14b9b-116">To make a method virtual, the `virtual` modifier is used in the method declaration of the base class.</span></span> <span data-ttu-id="14b9b-117">然後，衍生類別可以使用 `override` 關鍵字覆寫基底虛擬方法，或使用 `new` 關鍵字隱藏基底類別中的虛擬方法。</span><span class="sxs-lookup"><span data-stu-id="14b9b-117">The derived class can then override the base virtual method by using the `override` keyword or hide the virtual method in the base class by using the `new` keyword.</span></span> <span data-ttu-id="14b9b-118">如果不指定 `override` 關鍵字，也不指定 `new` 關鍵字，則編譯器會發出警告，且衍生類別中的方法會隱藏基底類別中的方法。</span><span class="sxs-lookup"><span data-stu-id="14b9b-118">If neither the `override` keyword nor the `new` keyword is specified, the compiler will issue a warning and the method in the derived class will hide the method in the base class.</span></span>  
  
 <span data-ttu-id="14b9b-119">為在練習中示範此技巧，假設公司 A 建立了類別 `GraphicsClass`，為您的程式所用。</span><span class="sxs-lookup"><span data-stu-id="14b9b-119">To demonstrate this in practice, assume for a moment that Company A has created a class named `GraphicsClass`, which your program uses.</span></span> <span data-ttu-id="14b9b-120">以下即為 `GraphicsClass`：</span><span class="sxs-lookup"><span data-stu-id="14b9b-120">The following is `GraphicsClass`:</span></span>  
  
 [!code-csharp[csProgGuideInheritance#27](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#27)]  
  
 <span data-ttu-id="14b9b-121">您的公司使用這個類別，而您用它衍生自己的類別，新增了新的方法︰</span><span class="sxs-lookup"><span data-stu-id="14b9b-121">Your company uses this class, and you use it to derive your own class, adding a new method:</span></span>  
  
 [!code-csharp[csProgGuideInheritance#28](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#28)]  
  
 <span data-ttu-id="14b9b-122">您的應用程式一直使用正常，直到公司 A 發行新版的 `GraphicsClass`，類似下列程式碼︰</span><span class="sxs-lookup"><span data-stu-id="14b9b-122">Your application is used without problems, until Company A releases a new version of `GraphicsClass`, which resembles the following code:</span></span>  
  
 [!code-csharp[csProgGuideInheritance#29](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#29)]  
  
 <span data-ttu-id="14b9b-123">新版的 `GraphicsClass` 現在包含一個名為 `DrawRectangle` 的方法。</span><span class="sxs-lookup"><span data-stu-id="14b9b-123">The new version of `GraphicsClass` now contains a method named `DrawRectangle`.</span></span> <span data-ttu-id="14b9b-124">一開始，一切如常。</span><span class="sxs-lookup"><span data-stu-id="14b9b-124">Initially, nothing occurs.</span></span> <span data-ttu-id="14b9b-125">新版本與舊版仍為二進位相容。</span><span class="sxs-lookup"><span data-stu-id="14b9b-125">The new version is still binary compatible with the old version.</span></span> <span data-ttu-id="14b9b-126">您部署的所有軟體仍繼續運作，即使這些電腦系統上安裝了新類別。</span><span class="sxs-lookup"><span data-stu-id="14b9b-126">Any software that you have deployed will continue to work, even if the new class is installed on those computer systems.</span></span> <span data-ttu-id="14b9b-127">目前對方法 `DrawRectangle` 的任何呼叫仍繼續參考您衍生類別中的版本。</span><span class="sxs-lookup"><span data-stu-id="14b9b-127">Any existing calls to the method `DrawRectangle` will continue to reference your version, in your derived class.</span></span>  
  
 <span data-ttu-id="14b9b-128">不過，一旦使用新版的 `GraphicsClass` 重新編譯應用程式，就會立刻收到編譯器警告 CS0108。</span><span class="sxs-lookup"><span data-stu-id="14b9b-128">However, as soon as you recompile your application by using the new version of `GraphicsClass`, you will receive a warning from the compiler, CS0108.</span></span> <span data-ttu-id="14b9b-129">這個警告會通知您，您必須考慮希望 `DrawRectangle` 方法在應用程式中如何表現。</span><span class="sxs-lookup"><span data-stu-id="14b9b-129">This warning informs you that you have to consider how you want your `DrawRectangle` method to behave in your application.</span></span>  
  
 <span data-ttu-id="14b9b-130">如果您希望自己的方法覆寫新的基底類別方法，請使用 `override` 關鍵字︰</span><span class="sxs-lookup"><span data-stu-id="14b9b-130">If you want your method to override the new base class method, use the `override` keyword:</span></span>  
  
 [!code-csharp[csProgGuideInheritance#30](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#30)]  
  
 <span data-ttu-id="14b9b-131">`override` 關鍵字可以確保衍生自 `YourDerivedGraphicsClass` 的所有物件都會使用 `DrawRectangle` 的衍生類別版本。</span><span class="sxs-lookup"><span data-stu-id="14b9b-131">The `override` keyword makes sure that any objects derived from `YourDerivedGraphicsClass` will use the derived class version of `DrawRectangle`.</span></span> <span data-ttu-id="14b9b-132">衍生自 `YourDerivedGraphicsClass` 的物件仍然可以使用 base 關鍵字存取 `DrawRectangle` 的基底類別版本︰</span><span class="sxs-lookup"><span data-stu-id="14b9b-132">Objects derived from `YourDerivedGraphicsClass` can still access the base class version of `DrawRectangle` by using the base keyword:</span></span>  
  
 [!code-csharp[csProgGuideInheritance#44](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#44)]  
  
 <span data-ttu-id="14b9b-133">如果您不希望自己的方法覆寫新的基底類別方法，請採納下列考量。</span><span class="sxs-lookup"><span data-stu-id="14b9b-133">If you do not want your method to override the new base class method, the following considerations apply.</span></span> <span data-ttu-id="14b9b-134">為避免混淆兩個方法，您可以重新命名您的方法。</span><span class="sxs-lookup"><span data-stu-id="14b9b-134">To avoid confusion between the two methods, you can rename your method.</span></span> <span data-ttu-id="14b9b-135">這很耗時間又容易發生錯誤，並且在某些情況下不實際。</span><span class="sxs-lookup"><span data-stu-id="14b9b-135">This can be time-consuming and error-prone, and just not practical in some cases.</span></span> <span data-ttu-id="14b9b-136">不過，如果您的專案相對較小，您可以使用 Visual Studio 的重構選項來重新命名方法。</span><span class="sxs-lookup"><span data-stu-id="14b9b-136">However, if your project is relatively small, you can use Visual Studio's Refactoring options to rename the method.</span></span> <span data-ttu-id="14b9b-137">如需詳細資訊，請參閱[重構類別和型別 (類別設計工具)](/visualstudio/ide/class-designer/refactoring-classes-and-types)。</span><span class="sxs-lookup"><span data-stu-id="14b9b-137">For more information, see [Refactoring Classes and Types (Class Designer)](/visualstudio/ide/class-designer/refactoring-classes-and-types).</span></span>  
  
 <span data-ttu-id="14b9b-138">或者，您也可以在衍生類別定義中使用關鍵字 `new`，避免出現警告：</span><span class="sxs-lookup"><span data-stu-id="14b9b-138">Alternatively, you can prevent the warning by using the keyword `new` in your derived class definition:</span></span>  
  
 [!code-csharp[csProgGuideInheritance#31](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#31)]  
  
 <span data-ttu-id="14b9b-139">使用 `new` 關鍵字會通知編譯器，您的定義要隱藏基底類別中包含的定義。</span><span class="sxs-lookup"><span data-stu-id="14b9b-139">Using the `new` keyword tells the compiler that your definition hides the definition that is contained in the base class.</span></span> <span data-ttu-id="14b9b-140">此為預設行為。</span><span class="sxs-lookup"><span data-stu-id="14b9b-140">This is the default behavior.</span></span>  
  
## <a name="override-and-method-selection"></a><span data-ttu-id="14b9b-141">覆寫和方法選擇</span><span class="sxs-lookup"><span data-stu-id="14b9b-141">Override and Method Selection</span></span>  
 <span data-ttu-id="14b9b-142">在類別上命名方法時，如果有多個方法與呼叫相容，C# 編譯器會選取最好的方法呼叫，例如當有兩種方法同名時，並傳遞與參數相容的參數。</span><span class="sxs-lookup"><span data-stu-id="14b9b-142">When a method is named on a class, the C# compiler selects the best method to call if more than one method is compatible with the call, such as when there are two methods with the same name, and parameters that are compatible with the parameter passed.</span></span> <span data-ttu-id="14b9b-143">下列方法相容︰</span><span class="sxs-lookup"><span data-stu-id="14b9b-143">The following methods would be compatible:</span></span>  
  
 [!code-csharp[csProgGuideInheritance#32](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#32)]  
  
 <span data-ttu-id="14b9b-144">在 `Derived` 的執行個體上呼叫 `DoWork` 時，C# 編譯器會先嘗試進行與 `DoWork` 版本相容的呼叫，此版本原是在 `Derived` 上宣告。</span><span class="sxs-lookup"><span data-stu-id="14b9b-144">When `DoWork` is called on an instance of `Derived`, the C# compiler will first try to make the call compatible with the versions of `DoWork` declared originally on `Derived`.</span></span> <span data-ttu-id="14b9b-145">覆寫方法不視為在類別中宣告，它們是基底類別中所宣告方法的新實作。</span><span class="sxs-lookup"><span data-stu-id="14b9b-145">Override methods are not considered as declared on a class, they are new implementations of a method declared on a base class.</span></span> <span data-ttu-id="14b9b-146">只有當 C# 編譯器無法比對方法呼叫和 `Derived` 中的原始方法時，才會嘗試比對具有相同名稱和相容參數的覆寫方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="14b9b-146">Only if the C# compiler cannot match the method call to an original method on `Derived` will it try to match the call to an overridden method with the same name and compatible parameters.</span></span> <span data-ttu-id="14b9b-147">例如：</span><span class="sxs-lookup"><span data-stu-id="14b9b-147">For example:</span></span>  
  
 [!code-csharp[csProgGuideInheritance#33](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#33)]  
  
 <span data-ttu-id="14b9b-148">因為變數 `val` 可以隱含方式轉換為 double，所以 C# 編譯器會呼叫 `DoWork(double)`，不是呼叫 `DoWork(int)`。</span><span class="sxs-lookup"><span data-stu-id="14b9b-148">Because the variable `val` can be converted to a double implicitly, the C# compiler calls `DoWork(double)` instead of `DoWork(int)`.</span></span> <span data-ttu-id="14b9b-149">有兩種方式可避免這種情況。</span><span class="sxs-lookup"><span data-stu-id="14b9b-149">There are two ways to avoid this.</span></span> <span data-ttu-id="14b9b-150">首先，避免使用和虛擬方法相同的名稱宣告新方法。</span><span class="sxs-lookup"><span data-stu-id="14b9b-150">First, avoid declaring new methods with the same name as virtual methods.</span></span> <span data-ttu-id="14b9b-151">第二，您可以將 `Derived` 執行個體轉換成 `Base`，讓 C# 編譯器搜尋基底類別方法清單，指示它呼叫虛擬方法。</span><span class="sxs-lookup"><span data-stu-id="14b9b-151">Second, you can instruct the C# compiler to call the virtual method by making it search the base class method list by casting the instance of `Derived` to `Base`.</span></span> <span data-ttu-id="14b9b-152">因為方法是虛擬的，所以會在 `Derived` 呼叫 `DoWork(int)` 實作。</span><span class="sxs-lookup"><span data-stu-id="14b9b-152">Because the method is virtual, the implementation of `DoWork(int)` on `Derived` will be called.</span></span> <span data-ttu-id="14b9b-153">例如：</span><span class="sxs-lookup"><span data-stu-id="14b9b-153">For example:</span></span>  
  
 [!code-csharp[csProgGuideInheritance#34](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#34)]  
  
 <span data-ttu-id="14b9b-154">如需更多的 `new` 和 `override` 範例，請參閱[了解使用 Override 和 New 關鍵字的時機](./knowing-when-to-use-override-and-new-keywords.md)。</span><span class="sxs-lookup"><span data-stu-id="14b9b-154">For more examples of `new` and `override`, see [Knowing When to Use Override and New Keywords](./knowing-when-to-use-override-and-new-keywords.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="14b9b-155">另請參閱</span><span class="sxs-lookup"><span data-stu-id="14b9b-155">See also</span></span>

- [<span data-ttu-id="14b9b-156">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="14b9b-156">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="14b9b-157">類別和結構</span><span class="sxs-lookup"><span data-stu-id="14b9b-157">Classes and Structs</span></span>](./index.md)
- [<span data-ttu-id="14b9b-158">方法</span><span class="sxs-lookup"><span data-stu-id="14b9b-158">Methods</span></span>](./methods.md)
- [<span data-ttu-id="14b9b-159">繼承</span><span class="sxs-lookup"><span data-stu-id="14b9b-159">Inheritance</span></span>](./inheritance.md)
