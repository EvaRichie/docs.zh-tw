---
title: 物件和集合初始設定式 - C# 程式設計手冊
description: 'C # 中的物件初始化運算式會在叫用函式之後，將值指派給建立物件的可存取欄位或屬性。'
ms.date: 12/19/2018
helpviewer_keywords:
- object initializers [C#]
- collection initializers [C#]
ms.assetid: c58f3db5-d7d4-4651-bd2d-5a3a97357f61
ms.openlocfilehash: 81deed8a21bff10364524c3e0784c562d4e727e6
ms.sourcegitcommit: 3d84eac0818099c9949035feb96bbe0346358504
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/21/2020
ms.locfileid: "86864770"
---
# <a name="object-and-collection-initializers-c-programming-guide"></a><span data-ttu-id="b1be7-103">物件和集合初始設定式 (C# 程式設計手冊)</span><span class="sxs-lookup"><span data-stu-id="b1be7-103">Object and Collection Initializers (C# Programming Guide)</span></span>

<span data-ttu-id="b1be7-104">C# 可讓您具現化物件或集合，並以單一陳述式執行成員指派。</span><span class="sxs-lookup"><span data-stu-id="b1be7-104">C# lets you instantiate an object or collection and perform member assignments in a single statement.</span></span>

## <a name="object-initializers"></a><span data-ttu-id="b1be7-105">物件初始設定式</span><span class="sxs-lookup"><span data-stu-id="b1be7-105">Object initializers</span></span>

<span data-ttu-id="b1be7-106">物件初始設定式可讓您在建立期間將值指派給物件的任何可存取欄位或屬性，而不用叫用後面接著幾行指派陳述式的建構函式。</span><span class="sxs-lookup"><span data-stu-id="b1be7-106">Object initializers let you assign values to any accessible fields or properties of an object at creation time without having to invoke a constructor followed by lines of assignment statements.</span></span> <span data-ttu-id="b1be7-107">物件初始設定式語法可讓您為建構函式指定引數或省略引數 (以及括號語法)。</span><span class="sxs-lookup"><span data-stu-id="b1be7-107">The object initializer syntax enables you to specify arguments for a constructor or omit the arguments (and parentheses syntax).</span></span>  <span data-ttu-id="b1be7-108">下列範例將示範如何使用有具名型別 `Cat` 的物件初始設定式，以及如何叫用無參數建構函式。</span><span class="sxs-lookup"><span data-stu-id="b1be7-108">The following example shows how to use an object initializer with a named type, `Cat` and how to invoke the parameterless constructor.</span></span> <span data-ttu-id="b1be7-109">請注意 `Cat` 類別中自動實作屬性的用法。</span><span class="sxs-lookup"><span data-stu-id="b1be7-109">Note the use of auto-implemented properties in the `Cat` class.</span></span> <span data-ttu-id="b1be7-110">如需詳細資訊，請參閱[自動實作的屬性](auto-implemented-properties.md)。</span><span class="sxs-lookup"><span data-stu-id="b1be7-110">For more information, see [Auto-Implemented Properties](auto-implemented-properties.md).</span></span>  
  
[!code-csharp[ObjectInitializer1](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/BasicObjectInitializers.cs#CatDeclaration)]  
[!code-csharp[ObjectInitializer1a](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/BasicObjectInitializers.cs#ObjectPropertyInitialization)]  

<span data-ttu-id="b1be7-111">物件初始設定式語法可讓您建立執行個體，然後將新建立的物件及其指派的屬性指派給指派作業中的變數。</span><span class="sxs-lookup"><span data-stu-id="b1be7-111">The object initializers syntax allows you to create an instance, and after that it assigns the newly created object, with its assigned properties, to the variable in the assignment.</span></span>

<span data-ttu-id="b1be7-112">從 C# 6 開始，物件初始設定式除了指派欄位和屬性，還可以設定索引子。</span><span class="sxs-lookup"><span data-stu-id="b1be7-112">Starting with C# 6, object initializers can set indexers, in addition to assigning fields and properties.</span></span> <span data-ttu-id="b1be7-113">請考慮此基本 `Matrix` 類別：</span><span class="sxs-lookup"><span data-stu-id="b1be7-113">Consider this basic `Matrix` class:</span></span>

[!code-csharp[ObjectInitializer2](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/BasicObjectInitializers.cs#MatrixDeclaration)]  

<span data-ttu-id="b1be7-114">您可以使用下列程式碼來初始化單位矩陣：</span><span class="sxs-lookup"><span data-stu-id="b1be7-114">You could initialize the identity matrix with the following code:</span></span>

[!code-csharp[ObjectInitializer2a](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/BasicObjectInitializers.cs#MatrixInitialization)]  

<span data-ttu-id="b1be7-115">任何包含可存取 setter 的可存取索引子都可作為物件初始設定式中的其中一個運算式，不論引數的數目或類型為何。</span><span class="sxs-lookup"><span data-stu-id="b1be7-115">Any accessible indexer that contains an accessible setter can be used as one of the expressions in an object initializer, regardless of the number or types of arguments.</span></span> <span data-ttu-id="b1be7-116">指派左側是由索引引數組成，運算式右側是其值。</span><span class="sxs-lookup"><span data-stu-id="b1be7-116">The index arguments form the left side of the assignment, and the value is the right side of the expression.</span></span>  <span data-ttu-id="b1be7-117">例如，如果 `IndexersExample` 具有適當的索引子，下列內容全部有效：</span><span class="sxs-lookup"><span data-stu-id="b1be7-117">For example, these are all valid if `IndexersExample` has the appropriate indexers:</span></span>

```csharp
var thing = new IndexersExample {
    name = "object one",
    [1] = '1',
    [2] = '4',
    [3] = '9',
    Size = Math.PI,
    ['C',4] = "Middle C"
}
```

<span data-ttu-id="b1be7-118">若要編譯上述程式碼，`IndexersExample` 類型必須具有下列成員：</span><span class="sxs-lookup"><span data-stu-id="b1be7-118">For the preceding code to compile, the `IndexersExample` type must have the following members:</span></span>

```csharp
public string name;
public double Size { set { ... }; }
public char this[int i] { set { ... }; }
public string this[char c, int i] {  set { ... }; }
```

## <a name="object-initializers-with-anonymous-types"></a><span data-ttu-id="b1be7-119">具有匿名類型的物件初始設定式</span><span class="sxs-lookup"><span data-stu-id="b1be7-119">Object Initializers with anonymous types</span></span>

<span data-ttu-id="b1be7-120">雖然物件初始化運算式可以用於任何內容中，但它們在 LINQ 查詢運算式中特別有用。</span><span class="sxs-lookup"><span data-stu-id="b1be7-120">Although object initializers can be used in any context, they are especially useful in LINQ query expressions.</span></span> <span data-ttu-id="b1be7-121">查詢運算式經常使用[匿名型別](./anonymous-types.md)，此型別只能使用物件初始設定式初始化，如下列宣告所示。</span><span class="sxs-lookup"><span data-stu-id="b1be7-121">Query expressions make frequent use of [anonymous types](./anonymous-types.md), which can only be initialized by using an object initializer, as shown in the following declaration.</span></span>  

```csharp
var pet = new { Age = 10, Name = "Fluffy" };  
```

<span data-ttu-id="b1be7-122">匿名型別 `select` 可讓 LINQ 查詢運算式中的子句將原始序列的物件轉換成物件，其值和圖形可能與原始的不同。</span><span class="sxs-lookup"><span data-stu-id="b1be7-122">Anonymous types enable the `select` clause in a LINQ query expression to transform objects of the original sequence into objects whose value and shape may differ from the original.</span></span> <span data-ttu-id="b1be7-123">如果您只要儲存序列中每個物件的部分資訊，這就會很實用。</span><span class="sxs-lookup"><span data-stu-id="b1be7-123">This is useful if you want to store only a part of the information from each object in a sequence.</span></span> <span data-ttu-id="b1be7-124">在下列範例中，假設產品物件 (`p`) 包含許多欄位和方法，而您只想要建立包含產品名稱和單價的物件序列。</span><span class="sxs-lookup"><span data-stu-id="b1be7-124">In the following example, assume that a product object (`p`) contains many fields and methods, and that you are only interested in creating a sequence of objects that contain the product name and the unit price.</span></span>  
  
[!code-csharp[ObjectInitializer3](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/BasicObjectInitializers.cs#AnonymousUse)]  

<span data-ttu-id="b1be7-125">執行此查詢時，`productInfos` 變數將會包含可以在 `foreach` 陳述式中存取的物件序列，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="b1be7-125">When this query is executed, the `productInfos` variable will contain a sequence of objects that can be accessed in a `foreach` statement as shown in this example:</span></span>  

```csharp
foreach(var p in productInfos){...}  
```

<span data-ttu-id="b1be7-126">新的匿名型別中的每個物件都有兩個公用屬性，這兩個屬性會接收與原始物件中的屬性或欄位相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="b1be7-126">Each object in the new anonymous type has two public properties that receive the same names as the properties or fields in the original object.</span></span> <span data-ttu-id="b1be7-127">您也可以在建立匿名類型時重新命名欄位，下列範例會將 `UnitPrice` 欄位重新命名為 `Price`。</span><span class="sxs-lookup"><span data-stu-id="b1be7-127">You can also rename a field when you are creating an anonymous type; the following example renames the `UnitPrice` field to `Price`.</span></span>  

```csharp
select new {p.ProductName, Price = p.UnitPrice};  
```

## <a name="collection-initializers"></a><span data-ttu-id="b1be7-128">集合初始設定式</span><span class="sxs-lookup"><span data-stu-id="b1be7-128">Collection initializers</span></span>

<span data-ttu-id="b1be7-129">如果集合類別是實作 <xref:System.Collections.IEnumerable>，且具有 `Add` 與適當簽章以作為執行個體方法或擴充方法，集合初始設定式可讓您在初始化這類集合類別時，指定一或多個項目初始設定式。</span><span class="sxs-lookup"><span data-stu-id="b1be7-129">Collection initializers let you specify one or more element initializers when you initialize a collection type that implements <xref:System.Collections.IEnumerable> and has `Add` with the appropriate signature as an instance method or an extension method.</span></span> <span data-ttu-id="b1be7-130">項目初始設定式可以是簡單的值、運算式或物件初始設定式。</span><span class="sxs-lookup"><span data-stu-id="b1be7-130">The element initializers can be a simple value, an expression, or an object initializer.</span></span> <span data-ttu-id="b1be7-131">藉由使用集合初始設定式，您就不需要指定多個呼叫，編譯器會自動新增呼叫。</span><span class="sxs-lookup"><span data-stu-id="b1be7-131">By using a collection initializer, you do not have to specify multiple calls; the compiler adds the calls automatically.</span></span>  
  
<span data-ttu-id="b1be7-132">下列範例將示範兩個簡單的集合初始設定式：</span><span class="sxs-lookup"><span data-stu-id="b1be7-132">The following example shows two simple collection initializers:</span></span>  

```csharp
List<int> digits = new List<int> { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };  
List<int> digits2 = new List<int> { 0 + 1, 12 % 3, MakeInt() };  
```

<span data-ttu-id="b1be7-133">下列集合初始設定式會使用物件初始設定式來初始化先前範例中所定義 `Cat` 類別的物件。</span><span class="sxs-lookup"><span data-stu-id="b1be7-133">The following collection initializer uses object initializers to initialize objects of the `Cat` class defined in a previous example.</span></span> <span data-ttu-id="b1be7-134">請注意，每個物件初始設定式會以括號括住並以逗號分隔。</span><span class="sxs-lookup"><span data-stu-id="b1be7-134">Note that the individual object initializers are enclosed in braces and separated by commas.</span></span>  
  
[!code-csharp[ListInitializer](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/BasicObjectInitializers.cs#ListInitializer)]  
  
<span data-ttu-id="b1be7-135">如果集合的 `Add` 方法允許，您可以將 [null](../../language-reference/keywords/null.md) 指定為集合初始設定式中的項目。</span><span class="sxs-lookup"><span data-stu-id="b1be7-135">You can specify [null](../../language-reference/keywords/null.md) as an element in a collection initializer if the collection's `Add` method allows it.</span></span>  
  
[!code-csharp[ListInitializerNull](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/BasicObjectInitializers.cs#ListInitialerWithNull)]  
  
 <span data-ttu-id="b1be7-136">如果集合支援讀取/寫入索引，您可以指定索引的項目。</span><span class="sxs-lookup"><span data-stu-id="b1be7-136">You can specify indexed elements if the collection supports read / write indexing.</span></span>
  
[!code-csharp[DictionaryInitializer](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/BasicObjectInitializers.cs#DictionaryIndexerInitializer)]  

<span data-ttu-id="b1be7-137">上述範例會產生呼叫 <xref:System.Collections.Generic.Dictionary%602.Item(%600)> 以設定值的程式碼。</span><span class="sxs-lookup"><span data-stu-id="b1be7-137">The preceding sample generates code that calls the <xref:System.Collections.Generic.Dictionary%602.Item(%600)> to set the values.</span></span> <span data-ttu-id="b1be7-138">在 c # 6 之前，您可以使用下列語法來初始化字典和其他關聯的容器。</span><span class="sxs-lookup"><span data-stu-id="b1be7-138">Before C# 6, you could initialize dictionaries and other associative containers using the following syntax.</span></span> <span data-ttu-id="b1be7-139">請注意，它會使用具有多個值的物件，而不是使用括弧和指派的索引子語法：</span><span class="sxs-lookup"><span data-stu-id="b1be7-139">Notice that instead of indexer syntax, with parentheses and an assignment, it uses an object with multiple values:</span></span>

[!code-csharp[DictionaryAddInitializer](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/BasicObjectInitializers.cs#DictionaryAddInitializer)]  

<span data-ttu-id="b1be7-140">初始設定式範例會呼叫 <xref:System.Collections.Generic.Dictionary%602.Add(%600,%601)> 來將三個項目新增至字典。</span><span class="sxs-lookup"><span data-stu-id="b1be7-140">This initializer example calls <xref:System.Collections.Generic.Dictionary%602.Add(%600,%601)> to add the three items into the dictionary.</span></span> <span data-ttu-id="b1be7-141">由於編譯器所產生的方法呼叫，這兩種初始化關聯集合的方式會有稍微不同的行為。</span><span class="sxs-lookup"><span data-stu-id="b1be7-141">These two different ways to initialize associative collections have slightly different behavior because of the method calls the compiler generates.</span></span> <span data-ttu-id="b1be7-142">這兩種方式都可以搭配 `Dictionary` 類別運作。</span><span class="sxs-lookup"><span data-stu-id="b1be7-142">Both variants work with the `Dictionary` class.</span></span> <span data-ttu-id="b1be7-143">其他類型視其公用 API 而定，可能只支援其中一種。</span><span class="sxs-lookup"><span data-stu-id="b1be7-143">Other types may only support one or the other based on their public API.</span></span>

## <a name="examples"></a><span data-ttu-id="b1be7-144">範例</span><span class="sxs-lookup"><span data-stu-id="b1be7-144">Examples</span></span>

<span data-ttu-id="b1be7-145">下列範例結合了物件和集合初始設定式的概念。</span><span class="sxs-lookup"><span data-stu-id="b1be7-145">The following example combines the concepts of object and collection initializers.</span></span>

[!code-csharp[InitializerExample](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/BasicObjectInitializers.cs#FullExample)]  

<span data-ttu-id="b1be7-146">下列範例顯示實作 <xref:System.Collections.IEnumerable> 並包含具有多個參數之 `Add` 方法的物件，它使用集合初始設定式來處理對應至 `Add` 方法簽章之清單中每個項目的多個元素。</span><span class="sxs-lookup"><span data-stu-id="b1be7-146">The following example shows an object that implements <xref:System.Collections.IEnumerable> and contains an `Add` method with multiple parameters, It uses a collection initializer with multiple elements per item in the list that correspond to the signature of the `Add` method.</span></span>

[!code-csharp[InitializerListExample](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/BasicObjectInitializers.cs#FullListExample)]  

<span data-ttu-id="b1be7-147">`Add` 方法可以使用 `params` 關鍵字來接受各種數目的引數，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="b1be7-147">`Add` methods can use the `params` keyword to take a variable number of arguments, as shown in the following example.</span></span> <span data-ttu-id="b1be7-148">此範例也示範索引子的自訂實作，以使用索引來初始化集合。</span><span class="sxs-lookup"><span data-stu-id="b1be7-148">This example also demonstrates the custom implementation of an indexer to initialize a collection using indexes.</span></span>

[!code-csharp[InitializerListExample](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/BasicObjectInitializers.cs#FullDictionaryInitializer)]  

## <a name="see-also"></a><span data-ttu-id="b1be7-149">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b1be7-149">See also</span></span>

- [<span data-ttu-id="b1be7-150">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="b1be7-150">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="b1be7-151">C# 中的 LINQ</span><span class="sxs-lookup"><span data-stu-id="b1be7-151">LINQ in C#</span></span>](../../linq/index.md)
- [<span data-ttu-id="b1be7-152">匿名類型</span><span class="sxs-lookup"><span data-stu-id="b1be7-152">Anonymous Types</span></span>](anonymous-types.md)
