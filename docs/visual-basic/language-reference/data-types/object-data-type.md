---
title: Object Data Type
ms.date: 07/20/2015
f1_keywords:
- vb.Object
- vb.Variant
helpviewer_keywords:
- object variables [Visual Basic], Object type
- data types [Visual Basic], assigning
- Object data type
- Object data type [Visual Basic], reference
ms.assetid: 61ea4a7c-3b3d-48d4-adc4-eacfa91779b2
ms.openlocfilehash: 14770e74a0169dba3a45a04845dd32323e6201e3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84415579"
---
# <a name="object-data-type"></a><span data-ttu-id="9535b-102">Object Data Type</span><span class="sxs-lookup"><span data-stu-id="9535b-102">Object Data Type</span></span>

<span data-ttu-id="9535b-103">保留參考物件的位址。</span><span class="sxs-lookup"><span data-stu-id="9535b-103">Holds addresses that refer to objects.</span></span> <span data-ttu-id="9535b-104">您可以將任何參考型別（字串、陣列、類別或介面）指派給 `Object` 變數。</span><span class="sxs-lookup"><span data-stu-id="9535b-104">You can assign any reference type (string, array, class, or interface) to an `Object` variable.</span></span> <span data-ttu-id="9535b-105">`Object`變數也可以參考任何實數值型別（數值、 `Boolean` 、 `Char` 、 `Date` 、結構或列舉）的資料。</span><span class="sxs-lookup"><span data-stu-id="9535b-105">An `Object` variable can also refer to data of any value type (numeric, `Boolean`, `Char`, `Date`, structure, or enumeration).</span></span>

## <a name="remarks"></a><span data-ttu-id="9535b-106">備註</span><span class="sxs-lookup"><span data-stu-id="9535b-106">Remarks</span></span>

<span data-ttu-id="9535b-107">`Object`資料類型可以指向任何資料類型的資料，包括您的應用程式可辨識的任何物件實例。</span><span class="sxs-lookup"><span data-stu-id="9535b-107">The `Object` data type can point to data of any data type, including any object instance your application recognizes.</span></span> <span data-ttu-id="9535b-108">`Object`當您在編譯時期不知道變數可能指向的資料類型時，請使用。</span><span class="sxs-lookup"><span data-stu-id="9535b-108">Use `Object` when you do not know at compile time what data type the variable might point to.</span></span>

<span data-ttu-id="9535b-109">的預設值 `Object` 為 `Nothing` （null 參考）。</span><span class="sxs-lookup"><span data-stu-id="9535b-109">The default value of `Object` is `Nothing` (a null reference).</span></span>

## <a name="data-types"></a><span data-ttu-id="9535b-110">資料類型</span><span class="sxs-lookup"><span data-stu-id="9535b-110">Data Types</span></span>

<span data-ttu-id="9535b-111">您可以將任何資料類型的變數、常數或運算式指派給 `Object` 變數。</span><span class="sxs-lookup"><span data-stu-id="9535b-111">You can assign a variable, constant, or expression of any data type to an `Object` variable.</span></span> <span data-ttu-id="9535b-112">若要判斷變數目前所參考的資料類型 `Object` ，您可以使用 <xref:System.Type.GetTypeCode%2A> 類別的方法 <xref:System.Type?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="9535b-112">To determine the data type an `Object` variable currently refers to, you can use the <xref:System.Type.GetTypeCode%2A> method of the <xref:System.Type?displayProperty=nameWithType> class.</span></span> <span data-ttu-id="9535b-113">下列範例將說明這點。</span><span class="sxs-lookup"><span data-stu-id="9535b-113">The following example illustrates this.</span></span>

```vb
Dim myObject As Object
' Suppose myObject has now had something assigned to it.
Dim datTyp As Integer
datTyp = Type.GetTypeCode(myObject.GetType())
```

<span data-ttu-id="9535b-114">`Object`資料類型是參考型別。</span><span class="sxs-lookup"><span data-stu-id="9535b-114">The `Object` data type is a reference type.</span></span> <span data-ttu-id="9535b-115">不過， `Object` 當參考實數值型別的資料時，Visual Basic 會將變數視為實數值型別。</span><span class="sxs-lookup"><span data-stu-id="9535b-115">However, Visual Basic treats an `Object` variable as a value type when it refers to data of a value type.</span></span>

## <a name="storage"></a><span data-ttu-id="9535b-116">儲存體</span><span class="sxs-lookup"><span data-stu-id="9535b-116">Storage</span></span>

<span data-ttu-id="9535b-117">無論它參考的資料類型為何， `Object` 變數不會包含資料值本身，而是值的指標。</span><span class="sxs-lookup"><span data-stu-id="9535b-117">Whatever data type it refers to, an `Object` variable does not contain the data value itself, but rather a pointer to the value.</span></span> <span data-ttu-id="9535b-118">它一律會在電腦記憶體中使用四個位元組，但這不會包含代表變數值之資料的儲存體。</span><span class="sxs-lookup"><span data-stu-id="9535b-118">It always uses four bytes in computer memory, but this does not include the storage for the data representing the value of the variable.</span></span> <span data-ttu-id="9535b-119">由於使用指標來尋找資料的程式碼，因此， `Object` 存取數值型別的變數會比明確類型的變數稍微慢一點。</span><span class="sxs-lookup"><span data-stu-id="9535b-119">Because of the code that uses the pointer to locate the data, `Object` variables holding value types are slightly slower to access than explicitly typed variables.</span></span>

## <a name="programming-tips"></a><span data-ttu-id="9535b-120">程式設計提示</span><span class="sxs-lookup"><span data-stu-id="9535b-120">Programming Tips</span></span>

- <span data-ttu-id="9535b-121">**Interop 考量：**</span><span class="sxs-lookup"><span data-stu-id="9535b-121">**Interop Considerations.**</span></span> <span data-ttu-id="9535b-122">如果您要使用的元件不是針對 .NET Framework 所撰寫（例如 Automation 或 COM 物件），請記住，其他環境中的指標類型與 Visual Basic 類型不相容 `Object` 。</span><span class="sxs-lookup"><span data-stu-id="9535b-122">If you are interfacing with components not written for the .NET Framework, for example Automation or COM objects, keep in mind that pointer types in other environments are not compatible with the Visual Basic `Object` type.</span></span>

- <span data-ttu-id="9535b-123">**效能。**</span><span class="sxs-lookup"><span data-stu-id="9535b-123">**Performance.**</span></span> <span data-ttu-id="9535b-124">您使用類型宣告的變數具有 `Object` 足夠的彈性，可包含任何物件的參考。</span><span class="sxs-lookup"><span data-stu-id="9535b-124">A variable you declare with the `Object` type is flexible enough to contain a reference to any object.</span></span> <span data-ttu-id="9535b-125">不過，當您在這類變數上叫用方法或屬性時，一律會產生*晚期繫結*（在執行時間）。</span><span class="sxs-lookup"><span data-stu-id="9535b-125">However, when you invoke a method or property on such a variable, you always incur *late binding* (at run time).</span></span> <span data-ttu-id="9535b-126">若要強制*早期繫結*（在編譯時期）和更好的效能，請使用特定類別名稱宣告變數，或將它轉換成特定的資料類型。</span><span class="sxs-lookup"><span data-stu-id="9535b-126">To force *early binding* (at compile time) and better performance, declare the variable with a specific class name, or cast it to the specific data type.</span></span>

  <span data-ttu-id="9535b-127">當您宣告物件變數時，請嘗試使用特定的類別類型，例如 <xref:System.OperatingSystem> ，而不是一般化 `Object` 類型。</span><span class="sxs-lookup"><span data-stu-id="9535b-127">When you declare an object variable, try to use a specific class type, for example <xref:System.OperatingSystem>, instead of the generalized `Object` type.</span></span> <span data-ttu-id="9535b-128">您也應該使用可用的最特定類別（例如 <xref:System.Windows.Forms.TextBox> ，而不是 <xref:System.Windows.Forms.Control> ），以便存取其屬性和方法。</span><span class="sxs-lookup"><span data-stu-id="9535b-128">You should also use the most specific class available, such as <xref:System.Windows.Forms.TextBox> instead of <xref:System.Windows.Forms.Control>, so that you can access its properties and methods.</span></span> <span data-ttu-id="9535b-129">您通常可以使用 [**物件瀏覽器**中的 [**類別**] 清單來尋找可用的類別名稱。</span><span class="sxs-lookup"><span data-stu-id="9535b-129">You can usually use the **Classes** list in the **Object Browser** to find available class names.</span></span>

- <span data-ttu-id="9535b-130">**加寬.**</span><span class="sxs-lookup"><span data-stu-id="9535b-130">**Widening.**</span></span> <span data-ttu-id="9535b-131">所有的資料類型和所有參考類型都會擴大至 `Object` 資料類型。</span><span class="sxs-lookup"><span data-stu-id="9535b-131">All data types and all reference types widen to the `Object` data type.</span></span> <span data-ttu-id="9535b-132">這表示您可以將任何類型轉換成， `Object` 而不會遇到 <xref:System.OverflowException?displayProperty=nameWithType> 錯誤。</span><span class="sxs-lookup"><span data-stu-id="9535b-132">This means you can convert any type to `Object` without encountering a <xref:System.OverflowException?displayProperty=nameWithType> error.</span></span>

  <span data-ttu-id="9535b-133">不過，如果您在實數值型別和之間進行轉換， `Object` Visual Basic 會執行稱為「*裝箱*和*取消裝箱*」的作業，使執行速度變慢。</span><span class="sxs-lookup"><span data-stu-id="9535b-133">However, if you convert between value types and `Object`, Visual Basic performs operations called *boxing* and *unboxing*, which make execution slower.</span></span>

- <span data-ttu-id="9535b-134">**輸入字元。**</span><span class="sxs-lookup"><span data-stu-id="9535b-134">**Type Characters.**</span></span> <span data-ttu-id="9535b-135">`Object`沒有常數值型別字元或識別項型別字元。</span><span class="sxs-lookup"><span data-stu-id="9535b-135">`Object` has no literal type character or identifier type character.</span></span>

- <span data-ttu-id="9535b-136">**架構類型：**</span><span class="sxs-lookup"><span data-stu-id="9535b-136">**Framework Type.**</span></span> <span data-ttu-id="9535b-137">.NET Framework 中的對應類型是 <xref:System.Object?displayProperty=nameWithType> 類別。</span><span class="sxs-lookup"><span data-stu-id="9535b-137">The corresponding type in the .NET Framework is the <xref:System.Object?displayProperty=nameWithType> class.</span></span>

## <a name="example"></a><span data-ttu-id="9535b-138">範例</span><span class="sxs-lookup"><span data-stu-id="9535b-138">Example</span></span>

<span data-ttu-id="9535b-139">下列範例說明 `Object` 指向物件實例的變數。</span><span class="sxs-lookup"><span data-stu-id="9535b-139">The following example illustrates an `Object` variable pointing to an object instance.</span></span>

```vb
Dim objDb As Object
Dim myCollection As New Collection()
' Suppose myCollection has now been populated.
objDb = myCollection.Item(1)
```

## <a name="see-also"></a><span data-ttu-id="9535b-140">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9535b-140">See also</span></span>

- <xref:System.Object>
- [<span data-ttu-id="9535b-141">資料類型</span><span class="sxs-lookup"><span data-stu-id="9535b-141">Data Types</span></span>](index.md)
- [<span data-ttu-id="9535b-142">Type Conversion Functions</span><span class="sxs-lookup"><span data-stu-id="9535b-142">Type Conversion Functions</span></span>](../functions/type-conversion-functions.md)
- [<span data-ttu-id="9535b-143">轉換摘要</span><span class="sxs-lookup"><span data-stu-id="9535b-143">Conversion Summary</span></span>](../keywords/conversion-summary.md)
- [<span data-ttu-id="9535b-144">有效率地使用資料類型</span><span class="sxs-lookup"><span data-stu-id="9535b-144">Efficient Use of Data Types</span></span>](../../programming-guide/language-features/data-types/efficient-use-of-data-types.md)
- [<span data-ttu-id="9535b-145">如何：判斷兩個物件是否關聯</span><span class="sxs-lookup"><span data-stu-id="9535b-145">How to: Determine Whether Two Objects Are Related</span></span>](../../programming-guide/language-features/variables/how-to-determine-whether-two-objects-are-related.md)
- [<span data-ttu-id="9535b-146">如何：判斷兩個物件是否相同</span><span class="sxs-lookup"><span data-stu-id="9535b-146">How to: Determine Whether Two Objects Are Identical</span></span>](../../programming-guide/language-features/variables/how-to-determine-whether-two-objects-are-identical.md)
