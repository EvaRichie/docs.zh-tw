---
title: 匿名類型
ms.date: 07/20/2015
f1_keywords:
- vb.AnonymousType
helpviewer_keywords:
- anonymous types [Visual Basic], about anonymous types
- anonymous types [Visual Basic]
- types [Visual Basic], anonymous
ms.assetid: 7b87532c-4b3e-4398-8503-6ea9d67574a4
ms.openlocfilehash: bbe84ce8a62705027c00bc26db74a3c21fa34fd9
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84411791"
---
# <a name="anonymous-types-visual-basic"></a><span data-ttu-id="86e37-102">匿名類型 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="86e37-102">Anonymous Types (Visual Basic)</span></span>
<span data-ttu-id="86e37-103">Visual Basic 支援匿名型別，這可讓您建立物件，而不需要撰寫資料類型的類別定義。</span><span class="sxs-lookup"><span data-stu-id="86e37-103">Visual Basic supports anonymous types, which enable you to create objects without writing a class definition for the data type.</span></span> <span data-ttu-id="86e37-104">編譯器 (Compiler) 會自動幫您建立類別 (Class)。</span><span class="sxs-lookup"><span data-stu-id="86e37-104">Instead, the compiler generates a class for you.</span></span> <span data-ttu-id="86e37-105">類別沒有可用的名稱、直接繼承自 <xref:System.Object> ，且包含您在宣告物件中指定的屬性。</span><span class="sxs-lookup"><span data-stu-id="86e37-105">The class has no usable name, inherits directly from <xref:System.Object>, and contains the properties you specify in declaring the object.</span></span> <span data-ttu-id="86e37-106">由於未指定資料類型的名稱，因此稱為*匿名型別*。</span><span class="sxs-lookup"><span data-stu-id="86e37-106">Because the name of the data type is not specified, it is referred to as an *anonymous type*.</span></span>  
  
 <span data-ttu-id="86e37-107">下列範例會宣告並建立變數 `product` ，做為具有兩個屬性（和）的匿名型別實例 `Name` `Price` 。</span><span class="sxs-lookup"><span data-stu-id="86e37-107">The following example declares and creates variable `product` as an instance of an anonymous type that has two properties, `Name` and `Price`.</span></span>  
  
 [!code-vb[VbVbalrAnonymousTypes#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#1)]  
  
 <span data-ttu-id="86e37-108">*查詢運算式*會使用匿名型別來結合查詢所選取的資料行。</span><span class="sxs-lookup"><span data-stu-id="86e37-108">A *query expression* uses anonymous types to combine columns of data selected by a query.</span></span> <span data-ttu-id="86e37-109">您無法事先定義結果的類型，因為您無法預測特定查詢可能會選取的資料行。</span><span class="sxs-lookup"><span data-stu-id="86e37-109">You cannot define the type of the result in advance, because you cannot predict the columns a particular query might select.</span></span> <span data-ttu-id="86e37-110">匿名型別可讓您撰寫查詢，依任何順序選取任意數目的資料行。</span><span class="sxs-lookup"><span data-stu-id="86e37-110">Anonymous types enable you to write a query that selects any number of columns, in any order.</span></span> <span data-ttu-id="86e37-111">編譯器會建立符合指定屬性和指定順序的資料類型。</span><span class="sxs-lookup"><span data-stu-id="86e37-111">The compiler creates a data type that matches the specified properties and the specified order.</span></span>  
  
 <span data-ttu-id="86e37-112">在下列範例中， `products` 是產品物件的清單，每個都有許多屬性。</span><span class="sxs-lookup"><span data-stu-id="86e37-112">In the following examples, `products` is a list of product objects, each of which has many properties.</span></span> <span data-ttu-id="86e37-113">變數 `namePriceQuery` 會保留查詢的定義，當它執行時，會傳回具有兩個屬性（和）之匿名型別實例的集合 `Name` `Price` 。</span><span class="sxs-lookup"><span data-stu-id="86e37-113">Variable `namePriceQuery` holds the definition of a query that, when it is executed, returns a collection of instances of an anonymous type that has two properties, `Name` and `Price`.</span></span>  
  
 [!code-vb[VbVbalrAnonymousTypes#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#2)]  
  
 <span data-ttu-id="86e37-114">變數 `nameQuantityQuery` 會保留查詢的定義，當它執行時，會傳回具有兩個屬性（和）之匿名型別實例的集合 `Name` `OnHand` 。</span><span class="sxs-lookup"><span data-stu-id="86e37-114">Variable `nameQuantityQuery` holds the definition of a query that, when it is executed, returns a collection of instances of an anonymous type that has two properties, `Name` and `OnHand`.</span></span>  
  
 [!code-vb[VbVbalrAnonymousTypes#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#3)]  
  
 <span data-ttu-id="86e37-115">如需編譯器針對匿名型別所建立之程式碼的詳細資訊，請參閱[匿名型別定義](anonymous-type-definition.md)。</span><span class="sxs-lookup"><span data-stu-id="86e37-115">For more information about the code created by the compiler for an anonymous type, see [Anonymous Type Definition](anonymous-type-definition.md).</span></span>  
  
> [!CAUTION]
> <span data-ttu-id="86e37-116">匿名型別的名稱是編譯器產生的，而且可能會因編譯而異。</span><span class="sxs-lookup"><span data-stu-id="86e37-116">The name of the anonymous type is compiler generated and may vary from compilation to compilation.</span></span> <span data-ttu-id="86e37-117">您的程式碼不應該使用或依賴匿名型別的名稱，因為重新編譯專案時，名稱可能會變更。</span><span class="sxs-lookup"><span data-stu-id="86e37-117">Your code should not use or rely on the name of an anonymous type because the name might change when a project is recompiled.</span></span>  
  
## <a name="declaring-an-anonymous-type"></a><span data-ttu-id="86e37-118">宣告匿名型別</span><span class="sxs-lookup"><span data-stu-id="86e37-118">Declaring an Anonymous Type</span></span>  
 <span data-ttu-id="86e37-119">匿名型別的實例宣告會使用初始化運算式清單來指定型別的屬性（property）。</span><span class="sxs-lookup"><span data-stu-id="86e37-119">The declaration of an instance of an anonymous type uses an initializer list to specify the properties of the type.</span></span> <span data-ttu-id="86e37-120">當您宣告匿名型別，而不是其他類別專案（例如方法或事件）時，您可以只指定屬性。</span><span class="sxs-lookup"><span data-stu-id="86e37-120">You can specify only properties when you declare an anonymous type, not other class elements such as methods or events.</span></span> <span data-ttu-id="86e37-121">在下列範例中， `product1` 是匿名型別的實例，其中包含兩個屬性： `Name` 和 `Price` 。</span><span class="sxs-lookup"><span data-stu-id="86e37-121">In the following example, `product1` is an instance of an anonymous type that has two properties: `Name` and `Price`.</span></span>  
  
 [!code-vb[VbVbalrAnonymousTypes#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#4)]  
  
 <span data-ttu-id="86e37-122">如果您指定屬性做為索引鍵屬性，您可以使用它們來比較兩個匿名型別實例是否相等。</span><span class="sxs-lookup"><span data-stu-id="86e37-122">If you designate properties as key properties, you can use them to compare two anonymous type instances for equality.</span></span> <span data-ttu-id="86e37-123">不過，無法變更索引鍵屬性的值。</span><span class="sxs-lookup"><span data-stu-id="86e37-123">However, the values of key properties cannot be changed.</span></span> <span data-ttu-id="86e37-124">如需詳細資訊，請參閱本主題稍後的金鑰屬性一節。</span><span class="sxs-lookup"><span data-stu-id="86e37-124">See the Key Properties section later in this topic for more information.</span></span>  
  
 <span data-ttu-id="86e37-125">請注意，宣告匿名型別的實例，就像使用物件初始化運算式宣告已命名類型的實例一樣：</span><span class="sxs-lookup"><span data-stu-id="86e37-125">Notice that declaring an instance of an anonymous type is like declaring an instance of a named type by using an object initializer:</span></span>  
  
 [!code-vb[VbVbalrAnonymousTypes#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#5)]  
  
 <span data-ttu-id="86e37-126">如需有關其他指定匿名型別屬性之方式的詳細資訊，請參閱[如何：推斷匿名型別宣告中的屬性名稱和類型](how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)。</span><span class="sxs-lookup"><span data-stu-id="86e37-126">For more information about other ways to specify anonymous type properties, see [How to: Infer Property Names and Types in Anonymous Type Declarations](how-to-infer-property-names-and-types-in-anonymous-type-declarations.md).</span></span>  
  
## <a name="key-properties"></a><span data-ttu-id="86e37-127">索引鍵內容</span><span class="sxs-lookup"><span data-stu-id="86e37-127">Key Properties</span></span>  
 <span data-ttu-id="86e37-128">索引鍵屬性與非索引鍵屬性有幾個基本的差異：</span><span class="sxs-lookup"><span data-stu-id="86e37-128">Key properties differ from non-key properties in several fundamental ways:</span></span>  
  
- <span data-ttu-id="86e37-129">只有索引鍵屬性的值會進行比較，以便判斷兩個實例是否相等。</span><span class="sxs-lookup"><span data-stu-id="86e37-129">Only the values of key properties are compared in order to determine whether two instances are equal.</span></span>  
  
- <span data-ttu-id="86e37-130">索引鍵屬性的值是唯讀的，而且無法變更。</span><span class="sxs-lookup"><span data-stu-id="86e37-130">The values of key properties are read-only and cannot be changed.</span></span>  
  
- <span data-ttu-id="86e37-131">只有索引鍵屬性值會包含在編譯器為匿名型別所產生的雜湊程式碼演算法中。</span><span class="sxs-lookup"><span data-stu-id="86e37-131">Only key property values are included in the compiler-generated hash code algorithm for an anonymous type.</span></span>  
  
### <a name="equality"></a><span data-ttu-id="86e37-132">等式</span><span class="sxs-lookup"><span data-stu-id="86e37-132">Equality</span></span>  
 <span data-ttu-id="86e37-133">匿名型別的實例只有在是相同匿名型別的實例時，才可以相等。</span><span class="sxs-lookup"><span data-stu-id="86e37-133">Instances of anonymous types can be equal only if they are instances of the same anonymous type.</span></span> <span data-ttu-id="86e37-134">如果符合下列條件，編譯器會將兩個實例視為相同類型的實例：</span><span class="sxs-lookup"><span data-stu-id="86e37-134">The compiler treats two instances as instances of the same type if they meet the following conditions:</span></span>  
  
- <span data-ttu-id="86e37-135">它們會在同一個元件中宣告。</span><span class="sxs-lookup"><span data-stu-id="86e37-135">They are declared in the same assembly.</span></span>  
  
- <span data-ttu-id="86e37-136">其屬性具有相同的名稱、相同的推斷型別，而且會以相同的順序宣告。</span><span class="sxs-lookup"><span data-stu-id="86e37-136">Their properties have the same names, the same inferred types, and are declared in the same order.</span></span> <span data-ttu-id="86e37-137">名稱比較不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="86e37-137">Name comparisons are not case-sensitive.</span></span>  
  
- <span data-ttu-id="86e37-138">每個中的相同屬性都會標示為索引鍵屬性。</span><span class="sxs-lookup"><span data-stu-id="86e37-138">The same properties in each are marked as key properties.</span></span>  
  
- <span data-ttu-id="86e37-139">每個宣告中至少有一個屬性是索引鍵屬性。</span><span class="sxs-lookup"><span data-stu-id="86e37-139">At least one property in each declaration is a key property.</span></span>  
  
 <span data-ttu-id="86e37-140">沒有索引鍵屬性的匿名型別實例，只等於本身。</span><span class="sxs-lookup"><span data-stu-id="86e37-140">An instance of an anonymous types that has no key properties is equal only to itself.</span></span>  
  
 [!code-vb[VbVbalrAnonymousTypes#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#6)]  
  
 <span data-ttu-id="86e37-141">如果索引鍵屬性的值相等，則相同匿名型別的兩個實例相等。</span><span class="sxs-lookup"><span data-stu-id="86e37-141">Two instances of the same anonymous type are equal if the values of their key properties are equal.</span></span> <span data-ttu-id="86e37-142">下列範例說明如何測試等號比較。</span><span class="sxs-lookup"><span data-stu-id="86e37-142">The following examples illustrate how equality is tested.</span></span>  
  
 [!code-vb[VbVbalrAnonymousTypes#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#7)]  
  
### <a name="read-only-values"></a><span data-ttu-id="86e37-143">唯讀值</span><span class="sxs-lookup"><span data-stu-id="86e37-143">Read-Only Values</span></span>  
 <span data-ttu-id="86e37-144">無法變更索引鍵屬性的值。</span><span class="sxs-lookup"><span data-stu-id="86e37-144">The values of key properties cannot be changed.</span></span> <span data-ttu-id="86e37-145">例如，在 `prod8` 上一個範例中， `Name` 和 `Price` 欄位是 `read-only` ，但 `OnHand` 可以變更。</span><span class="sxs-lookup"><span data-stu-id="86e37-145">For example, in `prod8` in the previous example, the `Name` and `Price` fields are `read-only`, but `OnHand` can be changed.</span></span>  
  
 [!code-vb[VbVbalrAnonymousTypes#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#8)]  
  
## <a name="anonymous-types-from-query-expressions"></a><span data-ttu-id="86e37-146">查詢運算式中的匿名型別</span><span class="sxs-lookup"><span data-stu-id="86e37-146">Anonymous Types from Query Expressions</span></span>  
 <span data-ttu-id="86e37-147">查詢運算式不一定需要建立匿名型別。</span><span class="sxs-lookup"><span data-stu-id="86e37-147">Query expressions do not always require the creation of anonymous types.</span></span> <span data-ttu-id="86e37-148">可能的話，它們會使用現有的類型來保存資料行資料。</span><span class="sxs-lookup"><span data-stu-id="86e37-148">When possible, they use an existing type to hold the column data.</span></span> <span data-ttu-id="86e37-149">當查詢從資料來源傳回完整記錄，或從每一筆記錄中只有一個欄位時，就會發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="86e37-149">This occurs when the query returns either whole records from the data source, or only one field from each record.</span></span> <span data-ttu-id="86e37-150">在下列程式碼範例中， `customers` 是類別物件的集合 `Customer` 。</span><span class="sxs-lookup"><span data-stu-id="86e37-150">In the following code examples, `customers` is a collection of objects of a `Customer` class.</span></span> <span data-ttu-id="86e37-151">類別有許多屬性，而且您可以依任何順序在查詢結果中包含一或多個屬性。</span><span class="sxs-lookup"><span data-stu-id="86e37-151">The class has many properties, and you can include one or more of them in the query result, in any order.</span></span> <span data-ttu-id="86e37-152">在前兩個範例中，不需要匿名型別，因為查詢會選取命名類型的元素：</span><span class="sxs-lookup"><span data-stu-id="86e37-152">In the first two examples, no anonymous types are required because the queries select elements of named types:</span></span>  
  
- <span data-ttu-id="86e37-153">`custs1`包含字串的集合，因為 `cust.Name` 是字串。</span><span class="sxs-lookup"><span data-stu-id="86e37-153">`custs1` contains a collection of strings, because `cust.Name` is a string.</span></span>  
  
     [!code-vb[VbVbalrAnonymousTypes#30](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class2.vb#30)]  
  
- <span data-ttu-id="86e37-154">`custs2`包含物件的集合 `Customer` ，因為的每個專案 `customers` 都是 `Customer` 物件，而且查詢會選取整個元素。</span><span class="sxs-lookup"><span data-stu-id="86e37-154">`custs2` contains a collection of `Customer` objects, because each element of `customers` is a `Customer` object, and the whole element is selected by the query.</span></span>  
  
     [!code-vb[VbVbalrAnonymousTypes#31](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class2.vb#31)]  
  
 <span data-ttu-id="86e37-155">不過，適當的命名類型不一定是可用的。</span><span class="sxs-lookup"><span data-stu-id="86e37-155">However, appropriate named types are not always available.</span></span> <span data-ttu-id="86e37-156">您可能想要選取客戶名稱和位址的一個用途、客戶識別碼和位置，以及第三個的客戶名稱、位址和訂單歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="86e37-156">You might want to select customer names and addresses for one purpose, customer ID numbers and locations for another, and customer names, addresses, and order histories for a third.</span></span> <span data-ttu-id="86e37-157">匿名型別可讓您依任何順序選取任何屬性組合，而不需要先宣告新的命名類型來保存結果。</span><span class="sxs-lookup"><span data-stu-id="86e37-157">Anonymous types enable you to select any combination of properties, in any order, without first declaring a new named type to hold the result.</span></span> <span data-ttu-id="86e37-158">相反地，編譯器會針對每個屬性編譯建立匿名型別。</span><span class="sxs-lookup"><span data-stu-id="86e37-158">Instead, the compiler creates an anonymous type for each compilation of properties.</span></span> <span data-ttu-id="86e37-159">下列查詢只會從中的每個物件選取客戶的名稱和 ID 編號 `Customer` `customers` 。</span><span class="sxs-lookup"><span data-stu-id="86e37-159">The following query selects only the customer's name and ID number from each `Customer` object in `customers`.</span></span> <span data-ttu-id="86e37-160">因此，編譯器會建立只包含這兩個屬性的匿名型別。</span><span class="sxs-lookup"><span data-stu-id="86e37-160">Therefore, the compiler creates an anonymous type that contains only those two properties.</span></span>  
  
 [!code-vb[VbVbalrAnonymousTYpes#32](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class2.vb#32)]  
  
 <span data-ttu-id="86e37-161">匿名型別中屬性的名稱和資料類型都是從的引數取得 `Select` 、 `cust.Name` 和 `cust.ID` 。</span><span class="sxs-lookup"><span data-stu-id="86e37-161">Both the names and the data types of the properties in the anonymous type are taken from the arguments to `Select`, `cust.Name` and `cust.ID`.</span></span> <span data-ttu-id="86e37-162">查詢所建立之匿名型別中的屬性一律是索引鍵屬性。</span><span class="sxs-lookup"><span data-stu-id="86e37-162">The properties in an anonymous type that is created by a query are always key properties.</span></span> <span data-ttu-id="86e37-163">`custs3`在下列迴圈中執行時 `For Each` ，結果會是匿名型別的實例集合，其中包含兩個索引鍵屬性： `Name` 和 `ID` 。</span><span class="sxs-lookup"><span data-stu-id="86e37-163">When `custs3` is executed in the following `For Each` loop, the result is a collection of instances of an anonymous type with two key properties, `Name` and `ID`.</span></span>  
  
 [!code-vb[VbVbalrAnonymousTypes#33](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class2.vb#33)]  
  
 <span data-ttu-id="86e37-164">所表示之集合中的元素 `custs3` 是強型別，您可以使用 IntelliSense 來流覽可用的屬性，並驗證其型別。</span><span class="sxs-lookup"><span data-stu-id="86e37-164">The elements in the collection represented by `custs3` are strongly typed, and you can use IntelliSense to navigate through the available properties and to verify their types.</span></span>  
  
 <span data-ttu-id="86e37-165">如需詳細資訊，請參閱[Visual Basic 中的 LINQ 簡介](../linq/introduction-to-linq.md)。</span><span class="sxs-lookup"><span data-stu-id="86e37-165">For more information, see [Introduction to LINQ in Visual Basic](../linq/introduction-to-linq.md).</span></span>  
  
## <a name="deciding-whether-to-use-anonymous-types"></a><span data-ttu-id="86e37-166">決定是否要使用匿名型別</span><span class="sxs-lookup"><span data-stu-id="86e37-166">Deciding Whether to Use Anonymous Types</span></span>  
 <span data-ttu-id="86e37-167">將物件建立為匿名類別的實例之前，請考慮這是否為最佳選項。</span><span class="sxs-lookup"><span data-stu-id="86e37-167">Before you create an object as an instance of an anonymous class, consider whether that is the best option.</span></span> <span data-ttu-id="86e37-168">例如，如果您想要建立暫存物件以包含相關資料，而不需要完整類別可能包含的其他欄位和方法，則匿名型別是不錯的解決方案。</span><span class="sxs-lookup"><span data-stu-id="86e37-168">For example, if you want to create a temporary object to contain related data, and you have no need for other fields and methods that a complete class might contain, an anonymous type is a good solution.</span></span> <span data-ttu-id="86e37-169">如果您想要針對每個宣告選擇不同的屬性，或者您想要變更屬性的順序，則匿名型別也很方便。</span><span class="sxs-lookup"><span data-stu-id="86e37-169">Anonymous types are also convenient if you want a different selection of properties for each declaration, or if you want to change the order of the properties.</span></span> <span data-ttu-id="86e37-170">不過，如果您的專案包含多個具有相同屬性的物件（以固定順序），您可以使用具有類別的方法的命名類型來更輕鬆地宣告它們。</span><span class="sxs-lookup"><span data-stu-id="86e37-170">However, if your project includes several objects that have the same properties, in a fixed order, you can declare them more easily by using a named type with a class constructor.</span></span> <span data-ttu-id="86e37-171">例如，使用適當的函式，可以更輕鬆地宣告類別的數個實例， `Product` 而不是宣告多個匿名型別的實例。</span><span class="sxs-lookup"><span data-stu-id="86e37-171">For example, with an appropriate constructor, it is easier to declare several instances of a `Product` class than it is to declare several instances of an anonymous type.</span></span>  
  
 [!code-vb[VbVbalrAnonymousTypes#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#9)]  
  
 <span data-ttu-id="86e37-172">命名類型的另一個優點是，編譯器可以攔截不小心的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="86e37-172">Another advantage of named types is that the compiler can catch an accidental mistyping of a property name.</span></span> <span data-ttu-id="86e37-173">在先前的範例中，、 `firstProd2` `secondProd2` 和 `thirdProd2` 是要作為相同匿名型別的實例。</span><span class="sxs-lookup"><span data-stu-id="86e37-173">In the previous examples, `firstProd2`, `secondProd2`, and `thirdProd2` are intended to be instances of the same anonymous type.</span></span> <span data-ttu-id="86e37-174">不過，如果您不小心以 `thirdProd2` 下列其中一種方式宣告，其型別會與和的類型不同 `firstProd2` `secondProd2` 。</span><span class="sxs-lookup"><span data-stu-id="86e37-174">However, if you were to accidentally declare `thirdProd2` in one of the following ways, its type would be different from that of `firstProd2` and `secondProd2`.</span></span>  
  
 [!code-vb[VbVbalrAnonymousTypes#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#10)]  
  
 <span data-ttu-id="86e37-175">更重要的是，使用不會套用至命名類型實例的匿名型別會有一些限制。</span><span class="sxs-lookup"><span data-stu-id="86e37-175">More importantly, there are limitations on the use of anonymous types that do not apply to instances of named types.</span></span> <span data-ttu-id="86e37-176">`firstProd2`、 `secondProd2` 和 `thirdProd2` 是相同匿名型別的實例。</span><span class="sxs-lookup"><span data-stu-id="86e37-176">`firstProd2`, `secondProd2`, and `thirdProd2` are instances of the same anonymous type.</span></span> <span data-ttu-id="86e37-177">不過，共用匿名型別的名稱無法使用，而且不能出現在您的程式碼中需要類型名稱的位置。</span><span class="sxs-lookup"><span data-stu-id="86e37-177">However, the name for the shared anonymous type is not available and cannot appear where a type name is expected in your code.</span></span> <span data-ttu-id="86e37-178">例如，匿名型別不能用來定義方法簽章、宣告另一個變數或欄位，或是在任何型別宣告中。</span><span class="sxs-lookup"><span data-stu-id="86e37-178">For example, an anonymous type cannot be used to define a method signature, to declare another variable or field, or in any type declaration.</span></span> <span data-ttu-id="86e37-179">因此，當您必須跨方法共用資訊時，匿名型別就不適用。</span><span class="sxs-lookup"><span data-stu-id="86e37-179">As a result, anonymous types are not appropriate when you have to share information across methods.</span></span>  
  
## <a name="an-anonymous-type-definition"></a><span data-ttu-id="86e37-180">匿名型別定義</span><span class="sxs-lookup"><span data-stu-id="86e37-180">An Anonymous Type Definition</span></span>  
 <span data-ttu-id="86e37-181">為了回應匿名型別的實例宣告，編譯器會建立新的類別定義，其中包含指定的屬性。</span><span class="sxs-lookup"><span data-stu-id="86e37-181">In response to the declaration of an instance of an anonymous type, the compiler creates a new class definition that contains the specified properties.</span></span>  
  
 <span data-ttu-id="86e37-182">如果匿名型別至少包含一個索引鍵屬性，則定義會覆寫繼承自的三個成員 <xref:System.Object> ： <xref:System.Object.Equals%2A> 、 <xref:System.Object.GetHashCode%2A> 和 <xref:System.Object.ToString%2A> 。</span><span class="sxs-lookup"><span data-stu-id="86e37-182">If the anonymous type contains at least one key property, the definition overrides three members inherited from <xref:System.Object>: <xref:System.Object.Equals%2A>, <xref:System.Object.GetHashCode%2A>, and <xref:System.Object.ToString%2A>.</span></span> <span data-ttu-id="86e37-183">針對測試相等和判斷雜湊碼值所產生的程式碼只會考慮索引鍵屬性。</span><span class="sxs-lookup"><span data-stu-id="86e37-183">The code produced for testing equality and determining the hash code value considers only the key properties.</span></span> <span data-ttu-id="86e37-184">如果匿名型別不包含索引鍵屬性， <xref:System.Object.ToString%2A> 則只會覆寫。</span><span class="sxs-lookup"><span data-stu-id="86e37-184">If the anonymous type contains no key properties, only <xref:System.Object.ToString%2A> is overridden.</span></span> <span data-ttu-id="86e37-185">匿名型別的明確命名屬性不能與這些產生的方法衝突。</span><span class="sxs-lookup"><span data-stu-id="86e37-185">Explicitly named properties of an anonymous type cannot conflict with these generated methods.</span></span> <span data-ttu-id="86e37-186">也就是說，您不能使用 `.Equals` 、 `.GetHashCode` 或 `.ToString` 來命名屬性。</span><span class="sxs-lookup"><span data-stu-id="86e37-186">That is, you cannot use `.Equals`, `.GetHashCode`, or `.ToString` to name a property.</span></span>  
  
 <span data-ttu-id="86e37-187">具有至少一個索引鍵屬性的匿名型別定義也 <xref:System.IEquatable%601?displayProperty=nameWithType> 會執行介面，其中 `T` 是匿名型別的型別。</span><span class="sxs-lookup"><span data-stu-id="86e37-187">Anonymous type definitions that have at least one key property also implement the <xref:System.IEquatable%601?displayProperty=nameWithType> interface, where `T` is the type of the anonymous type.</span></span>  
  
 <span data-ttu-id="86e37-188">如需編譯器所建立之程式碼和覆寫方法之功能的詳細資訊，請參閱[匿名型別定義](anonymous-type-definition.md)。</span><span class="sxs-lookup"><span data-stu-id="86e37-188">For more information about the code created by the compiler and the functionality of the overridden methods, see [Anonymous Type Definition](anonymous-type-definition.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="86e37-189">另請參閱</span><span class="sxs-lookup"><span data-stu-id="86e37-189">See also</span></span>

- [<span data-ttu-id="86e37-190">物件初始設定式：具名和匿名型別</span><span class="sxs-lookup"><span data-stu-id="86e37-190">Object Initializers: Named and Anonymous Types</span></span>](object-initializers-named-and-anonymous-types.md)
- [<span data-ttu-id="86e37-191">區域型別推斷</span><span class="sxs-lookup"><span data-stu-id="86e37-191">Local Type Inference</span></span>](../variables/local-type-inference.md)
- [<span data-ttu-id="86e37-192">Visual Basic 中的 LINQ 簡介</span><span class="sxs-lookup"><span data-stu-id="86e37-192">Introduction to LINQ in Visual Basic</span></span>](../linq/introduction-to-linq.md)
- [<span data-ttu-id="86e37-193">如何：在匿名類型宣告中推斷屬性名稱和類型</span><span class="sxs-lookup"><span data-stu-id="86e37-193">How to: Infer Property Names and Types in Anonymous Type Declarations</span></span>](how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)
- [<span data-ttu-id="86e37-194">匿名型別定義</span><span class="sxs-lookup"><span data-stu-id="86e37-194">Anonymous Type Definition</span></span>](anonymous-type-definition.md)
- [<span data-ttu-id="86e37-195">關鍵</span><span class="sxs-lookup"><span data-stu-id="86e37-195">Key</span></span>](../../../language-reference/modifiers/key.md)
