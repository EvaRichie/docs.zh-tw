---
title: 靜態類別和靜態類別成員 - C# 程式設計手冊
ms.date: 07/20/2015
helpviewer_keywords:
- C# language, static members
- static members [C#]
- static classes [C#]
- C# language, static classes
- static class members [C#]
ms.assetid: 235614b5-1371-4dbd-9abd-b406a8b0298b
ms.openlocfilehash: f5e355d66d9b022a037d53e1241e76282852888e
ms.sourcegitcommit: a241301495a84cc8c64fe972330d16edd619868b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/01/2020
ms.locfileid: "84241457"
---
# <a name="static-classes-and-static-class-members-c-programming-guide"></a><span data-ttu-id="0603b-102">靜態類別和靜態類別成員 (C# 程式設計手冊)</span><span class="sxs-lookup"><span data-stu-id="0603b-102">Static Classes and Static Class Members (C# Programming Guide)</span></span>

<span data-ttu-id="0603b-103">[static](../../language-reference/keywords/static.md) 類別基本上與非靜態類別相同，但有一項差異︰無法具現化靜態類別。</span><span class="sxs-lookup"><span data-stu-id="0603b-103">A [static](../../language-reference/keywords/static.md) class is basically the same as a non-static class, but there is one difference: a static class cannot be instantiated.</span></span> <span data-ttu-id="0603b-104">換句話說，您不能使用 [new](../../language-reference/operators/new-operator.md) 運算子來建立類別型別的變數。</span><span class="sxs-lookup"><span data-stu-id="0603b-104">In other words, you cannot use the [new](../../language-reference/operators/new-operator.md) operator to create a variable of the class type.</span></span> <span data-ttu-id="0603b-105">因為沒有任何執行個體變數，所以您可以使用類別名稱本身來存取靜態類別的成員。</span><span class="sxs-lookup"><span data-stu-id="0603b-105">Because there is no instance variable, you access the members of a static class by using the class name itself.</span></span> <span data-ttu-id="0603b-106">例如，如果您的 `UtilityClass` 靜態類別包含 `MethodA` 公用靜態方法，則會呼叫方法，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="0603b-106">For example, if you have a static class that is named `UtilityClass` that has a public static method named `MethodA`, you call the method as shown in the following example:</span></span>  
  
```csharp  
UtilityClass.MethodA();  
```  
  
 <span data-ttu-id="0603b-107">如果方法集只作業於輸入參數，並且不需要取得或設定任何內部執行個體欄位，則靜態類別可以用作其方便使用的容器。</span><span class="sxs-lookup"><span data-stu-id="0603b-107">A static class can be used as a convenient container for sets of methods that just operate on input parameters and do not have to get or set any internal instance fields.</span></span> <span data-ttu-id="0603b-108">例如，在 .NET 類別庫中，靜態 <xref:System.Math?displayProperty=nameWithType> 類別包含執行數學運算的方法，不需要儲存或抓取特定類別實例特有的資料 <xref:System.Math> 。</span><span class="sxs-lookup"><span data-stu-id="0603b-108">For example, in the .NET Class Library, the static <xref:System.Math?displayProperty=nameWithType> class contains methods that perform mathematical operations, without any requirement to store or retrieve data that is unique to a particular instance of the <xref:System.Math> class.</span></span> <span data-ttu-id="0603b-109">亦即，您可以指定類別名稱和方法名稱來套用類別的成員，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="0603b-109">That is, you apply the members of the class by specifying the class name and the method name, as shown in the following example.</span></span>  
  
```csharp  
double dub = -3.14;  
Console.WriteLine(Math.Abs(dub));  
Console.WriteLine(Math.Floor(dub));  
Console.WriteLine(Math.Round(Math.Abs(dub)));  
  
// Output:  
// 3.14  
// -4  
// 3  
```  
  
 <span data-ttu-id="0603b-110">如同所有類別類型的情況，當載入參考類別的程式時，.NET 執行時間會載入靜態類別的型別資訊。</span><span class="sxs-lookup"><span data-stu-id="0603b-110">As is the case with all class types, the type information for a static class is loaded by the .NET runtime when the program that references the class is loaded.</span></span> <span data-ttu-id="0603b-111">程式無法指定確實載入類別的時間。</span><span class="sxs-lookup"><span data-stu-id="0603b-111">The program cannot specify exactly when the class is loaded.</span></span> <span data-ttu-id="0603b-112">不過，一定會載入類別、初始化其欄位，並在第一次於程式中參考類別之前呼叫其靜態建構函式。</span><span class="sxs-lookup"><span data-stu-id="0603b-112">However, it is guaranteed to be loaded and to have its fields initialized and its static constructor called before the class is referenced for the first time in your program.</span></span> <span data-ttu-id="0603b-113">只會呼叫靜態建構函式一次，而且靜態類別在程式所在應用程式定義域的存留期間保留在記憶體中。</span><span class="sxs-lookup"><span data-stu-id="0603b-113">A static constructor is only called one time, and a static class remains in memory for the lifetime of the application domain in which your program resides.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="0603b-114">若要建立只允許建立它本身之一個執行個體的非靜態類別，請參閱 [Implementing Singleton in C#](https://docs.microsoft.com/previous-versions/msp-n-p/ff650316%28v=pandp.10%29) (在 C# 中實作單一)。</span><span class="sxs-lookup"><span data-stu-id="0603b-114">To create a non-static class that allows only one instance of itself to be created, see [Implementing Singleton in C#](https://docs.microsoft.com/previous-versions/msp-n-p/ff650316%28v=pandp.10%29).</span></span>  
  
 <span data-ttu-id="0603b-115">下列清單提供靜態類別的主要功能︰</span><span class="sxs-lookup"><span data-stu-id="0603b-115">The following list provides the main features of a static class:</span></span>  
  
- <span data-ttu-id="0603b-116">僅包含靜態成員。</span><span class="sxs-lookup"><span data-stu-id="0603b-116">Contains only static members.</span></span>  
  
- <span data-ttu-id="0603b-117">無法具現化。</span><span class="sxs-lookup"><span data-stu-id="0603b-117">Cannot be instantiated.</span></span>  
  
- <span data-ttu-id="0603b-118">已密封。</span><span class="sxs-lookup"><span data-stu-id="0603b-118">Is sealed.</span></span>  
  
- <span data-ttu-id="0603b-119">不能包含[執行個體建構函式](./instance-constructors.md)。</span><span class="sxs-lookup"><span data-stu-id="0603b-119">Cannot contain [Instance Constructors](./instance-constructors.md).</span></span>  
  
 <span data-ttu-id="0603b-120">因此，建立靜態類別，基本上與建立只包含靜態成員和私用建構函式的類別相同。</span><span class="sxs-lookup"><span data-stu-id="0603b-120">Creating a static class is therefore basically the same as creating a class that contains only static members and a private constructor.</span></span> <span data-ttu-id="0603b-121">私用建構函式可防止具現化類別。</span><span class="sxs-lookup"><span data-stu-id="0603b-121">A private constructor prevents the class from being instantiated.</span></span> <span data-ttu-id="0603b-122">使用靜態類別的優點在於編譯器可以確認不會意外新增任何執行個體成員。</span><span class="sxs-lookup"><span data-stu-id="0603b-122">The advantage of using a static class is that the compiler can check to make sure that no instance members are accidentally added.</span></span> <span data-ttu-id="0603b-123">編譯器將保證無法建立此類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="0603b-123">The compiler will guarantee that instances of this class cannot be created.</span></span>  
  
 <span data-ttu-id="0603b-124">靜態類別已密封，因此無法進行繼承。</span><span class="sxs-lookup"><span data-stu-id="0603b-124">Static classes are sealed and therefore cannot be inherited.</span></span> <span data-ttu-id="0603b-125">它們無法繼承自 <xref:System.Object> 以外的任何類別。</span><span class="sxs-lookup"><span data-stu-id="0603b-125">They cannot inherit from any class except <xref:System.Object>.</span></span> <span data-ttu-id="0603b-126">靜態類別不能包含執行個體建構函式，但可以包含靜態建構函式。</span><span class="sxs-lookup"><span data-stu-id="0603b-126">Static classes cannot contain an instance constructor; however, they can contain a static constructor.</span></span> <span data-ttu-id="0603b-127">如果類別包含需要重要初始化的靜態成員，則非靜態類別也應該定義靜態建構函式。</span><span class="sxs-lookup"><span data-stu-id="0603b-127">Non-static classes should also define a static constructor if the class contains static members that require non-trivial initialization.</span></span> <span data-ttu-id="0603b-128">如需詳細資訊，請參閱[靜態建構函式](./static-constructors.md)。</span><span class="sxs-lookup"><span data-stu-id="0603b-128">For more information, see [Static Constructors](./static-constructors.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="0603b-129">範例</span><span class="sxs-lookup"><span data-stu-id="0603b-129">Example</span></span>  
 <span data-ttu-id="0603b-130">以下是包含兩種方法可將溫度從攝氏轉換為華氏以及從華氏轉換為攝氏的靜態類別範例︰</span><span class="sxs-lookup"><span data-stu-id="0603b-130">Here is an example of a static class that contains two methods that convert temperature from Celsius to Fahrenheit and from Fahrenheit to Celsius:</span></span>  
  
 [!code-csharp[csProgGuideObjects#31](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#31)]  
  
## <a name="static-members"></a><span data-ttu-id="0603b-131">靜態成員</span><span class="sxs-lookup"><span data-stu-id="0603b-131">Static Members</span></span>  
 <span data-ttu-id="0603b-132">非靜態類別可以包含靜態方法、欄位、屬性或事件。</span><span class="sxs-lookup"><span data-stu-id="0603b-132">A non-static class can contain static methods, fields, properties, or events.</span></span> <span data-ttu-id="0603b-133">即使尚未建立類別的執行個體，還是可以在類別上呼叫靜態成員。</span><span class="sxs-lookup"><span data-stu-id="0603b-133">The static member is callable on a class even when no instance of the class has been created.</span></span> <span data-ttu-id="0603b-134">靜態成員一律是透過類別名稱進行存取，而不是執行個體名稱。</span><span class="sxs-lookup"><span data-stu-id="0603b-134">The static member is always accessed by the class name, not the instance name.</span></span> <span data-ttu-id="0603b-135">不論建立多少個類別執行個體，都只會有一個靜態成員複本。</span><span class="sxs-lookup"><span data-stu-id="0603b-135">Only one copy of a static member exists, regardless of how many instances of the class are created.</span></span> <span data-ttu-id="0603b-136">靜態方法和屬性無法存取其包含類型中的非靜態欄位和事件，也無法存取任何物件的執行個體變數，除非它明確地傳入方法參數。</span><span class="sxs-lookup"><span data-stu-id="0603b-136">Static methods and properties cannot access non-static fields and events in their containing type, and they cannot access an instance variable of any object unless it is explicitly passed in a method parameter.</span></span>  
  
 <span data-ttu-id="0603b-137">使用一些靜態成員宣告非靜態類別，會比將整個類別宣告為靜態更為常見。</span><span class="sxs-lookup"><span data-stu-id="0603b-137">It is more typical to declare a non-static class with some static members, than to declare an entire class as static.</span></span> <span data-ttu-id="0603b-138">靜態欄位的兩個常用用法是持續計算已具現化的物件數目，或是儲存必須在所有執行個體之間共用的值。</span><span class="sxs-lookup"><span data-stu-id="0603b-138">Two common uses of static fields are to keep a count of the number of objects that have been instantiated, or to store a value that must be shared among all instances.</span></span>  
  
 <span data-ttu-id="0603b-139">可以多載但無法覆寫靜態方法，因為它們屬於類別，而不是類別的任何執行個體。</span><span class="sxs-lookup"><span data-stu-id="0603b-139">Static methods can be overloaded but not overridden, because they belong to the class, and not to any instance of the class.</span></span>  
  
 <span data-ttu-id="0603b-140">雖然欄位不可以宣告為 `static const`，但是 [const](../../language-reference/keywords/const.md) 欄位在其行為中基本上是靜態的。</span><span class="sxs-lookup"><span data-stu-id="0603b-140">Although a field cannot be declared as `static const`, a [const](../../language-reference/keywords/const.md) field is essentially static in its behavior.</span></span> <span data-ttu-id="0603b-141">它屬於類型，而不是類型的執行個體。</span><span class="sxs-lookup"><span data-stu-id="0603b-141">It belongs to the type, not to instances of the type.</span></span> <span data-ttu-id="0603b-142">因此，使用用於靜態欄位的相同 `ClassName.MemberName` 標記法可以存取 const 欄位。</span><span class="sxs-lookup"><span data-stu-id="0603b-142">Therefore, const fields can be accessed by using the same `ClassName.MemberName` notation that is used for static fields.</span></span> <span data-ttu-id="0603b-143">不需要物件執行個體。</span><span class="sxs-lookup"><span data-stu-id="0603b-143">No object instance is required.</span></span>  
  
 <span data-ttu-id="0603b-144">C# 不支援靜態區域變數 (方法範圍中所宣告的變數)。</span><span class="sxs-lookup"><span data-stu-id="0603b-144">C# does not support static local variables (variables that are declared in method scope).</span></span>  
  
 <span data-ttu-id="0603b-145">在成員的傳回型別前面使用 `static` 關鍵字，即可宣告靜態類別成員，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="0603b-145">You declare static class members by using the `static` keyword before the return type of the member, as shown in the following example:</span></span>  
  
 [!code-csharp[csProgGuideObjects#29](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#29)]  
  
 <span data-ttu-id="0603b-146">第一次存取靜態成員之前，以及呼叫靜態建構函式 (如果有的話) 之前，都會初始化靜態成員。</span><span class="sxs-lookup"><span data-stu-id="0603b-146">Static members are initialized before the static member is accessed for the first time and before the static constructor, if there is one, is called.</span></span> <span data-ttu-id="0603b-147">若要存取靜態類別成員，請使用類別的名稱來指定成員的位置，而不是變數名稱，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="0603b-147">To access a static class member, use the name of the class instead of a variable name to specify the location of the member, as shown in the following example:</span></span>  
  
 [!code-csharp[csProgGuideObjects#30](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#30)]  
  
 <span data-ttu-id="0603b-148">如果您的類別包含靜態欄位，請提供在載入類別時初始化它們的靜態建構函式。</span><span class="sxs-lookup"><span data-stu-id="0603b-148">If your class contains static fields, provide a static constructor that initializes them when the class is loaded.</span></span>  
  
 <span data-ttu-id="0603b-149">靜態方法的呼叫會使用 Microsoft Intermediate Language (MSIL) 產生呼叫指令，而執行個體方法的呼叫會產生 `callvirt` 指令，這也會檢查是否有 Null 物件參考。</span><span class="sxs-lookup"><span data-stu-id="0603b-149">A call to a static method generates a call instruction in Microsoft intermediate language (MSIL), whereas a call to an instance method generates a `callvirt` instruction, which also checks for a null object references.</span></span> <span data-ttu-id="0603b-150">不過，大部分的時間，兩者之間的效能差異並不明顯。</span><span class="sxs-lookup"><span data-stu-id="0603b-150">However, most of the time the performance difference between the two is not significant.</span></span>  
  
## <a name="c-language-specification"></a><span data-ttu-id="0603b-151">C# 語言規格</span><span class="sxs-lookup"><span data-stu-id="0603b-151">C# Language Specification</span></span>  

<span data-ttu-id="0603b-152">如需詳細資訊，請參閱 [C# 語言規格](/dotnet/csharp/language-reference/language-specification/introduction)中的[靜態類別](~/_csharplang/spec/classes.md#static-classes)與[靜態和執行個體的成員](~/_csharplang/spec/classes.md#static-and-instance-members)。</span><span class="sxs-lookup"><span data-stu-id="0603b-152">For more information, see [Static classes](~/_csharplang/spec/classes.md#static-classes) and [Static and instance members](~/_csharplang/spec/classes.md#static-and-instance-members) in the [C# Language Specification](/dotnet/csharp/language-reference/language-specification/introduction).</span></span> <span data-ttu-id="0603b-153">語言規格是 C# 語法及用法的限定來源。</span><span class="sxs-lookup"><span data-stu-id="0603b-153">The language specification is the definitive source for C# syntax and usage.</span></span>
  
## <a name="see-also"></a><span data-ttu-id="0603b-154">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0603b-154">See also</span></span>

- [<span data-ttu-id="0603b-155">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="0603b-155">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="0603b-156">static</span><span class="sxs-lookup"><span data-stu-id="0603b-156">static</span></span>](../../language-reference/keywords/static.md)
- [<span data-ttu-id="0603b-157">類別</span><span class="sxs-lookup"><span data-stu-id="0603b-157">Classes</span></span>](./classes.md)
- [<span data-ttu-id="0603b-158">class</span><span class="sxs-lookup"><span data-stu-id="0603b-158">class</span></span>](../../language-reference/keywords/class.md)
- [<span data-ttu-id="0603b-159">靜態建構函式</span><span class="sxs-lookup"><span data-stu-id="0603b-159">Static Constructors</span></span>](./static-constructors.md)
- [<span data-ttu-id="0603b-160">執行個體建構函式</span><span class="sxs-lookup"><span data-stu-id="0603b-160">Instance Constructors</span></span>](./instance-constructors.md)
