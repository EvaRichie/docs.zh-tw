---
title: 字串基本概念
ms.date: 07/20/2015
helpviewer_keywords:
- strings [Visual Basic], Like operator
- strings [Visual Basic], Visual Basic
- strings [Visual Basic], regular expressions
ms.assetid: 5674418d-f00d-4f72-9f98-d15897793350
ms.openlocfilehash: 935926b8b83afa47c20ea68aecd6bc8c40bd0234
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84363690"
---
# <a name="string-basics-in-visual-basic"></a><span data-ttu-id="6be2c-102">Visual Basic 中的字串基礎</span><span class="sxs-lookup"><span data-stu-id="6be2c-102">String Basics in Visual Basic</span></span>
<span data-ttu-id="6be2c-103">`String` 資料類型代表一系列字元 (每個依序代表 `Char` 資料類型的一個執行個體)。</span><span class="sxs-lookup"><span data-stu-id="6be2c-103">The `String` data type represents a series of characters (each representing in turn an instance of the `Char` data type).</span></span> <span data-ttu-id="6be2c-104">本主題介紹 Visual Basic 中字串的基本概念。</span><span class="sxs-lookup"><span data-stu-id="6be2c-104">This topic introduces the basic concepts of strings in Visual Basic.</span></span>  
  
## <a name="string-variables"></a><span data-ttu-id="6be2c-105">字串變數</span><span class="sxs-lookup"><span data-stu-id="6be2c-105">String Variables</span></span>  
 <span data-ttu-id="6be2c-106">可將代表字元數列的常值指派給字串的執行個體。</span><span class="sxs-lookup"><span data-stu-id="6be2c-106">An instance of a string can be assigned a literal value that represents a series of characters.</span></span> <span data-ttu-id="6be2c-107">例如：</span><span class="sxs-lookup"><span data-stu-id="6be2c-107">For example:</span></span>  
  
 [!code-vb[VbVbalrStrings#63](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#63)]  
  
 <span data-ttu-id="6be2c-108">`String` 變數也可以接受評估為字串的任何運算式。</span><span class="sxs-lookup"><span data-stu-id="6be2c-108">A `String` variable can also accept any expression that evaluates to a string.</span></span> <span data-ttu-id="6be2c-109">範例如下所示：</span><span class="sxs-lookup"><span data-stu-id="6be2c-109">Examples are shown below:</span></span>  
  
 [!code-vb[VbVbalrStrings#64](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#64)]  
  
 <span data-ttu-id="6be2c-110">指派給 `String` 變數的任何常值必須括在引號 ("") 內。</span><span class="sxs-lookup"><span data-stu-id="6be2c-110">Any literal that is assigned to a `String` variable must be enclosed in quotation marks ("").</span></span> <span data-ttu-id="6be2c-111">這表示無法以引號表示字串內的引號。</span><span class="sxs-lookup"><span data-stu-id="6be2c-111">This means that a quotation mark within a string cannot be represented by a quotation mark.</span></span> <span data-ttu-id="6be2c-112">例如，下列程式碼會導致編譯器錯誤：</span><span class="sxs-lookup"><span data-stu-id="6be2c-112">For example, the following code causes a compiler error:</span></span>  
  
 [!code-vb[VbVbalrStrings#65](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#65)]  
  
 <span data-ttu-id="6be2c-113">此程式碼會造成錯誤，因為編譯器會終止第二個引號後的字串，並將字串的其餘部分解譯為程式碼。</span><span class="sxs-lookup"><span data-stu-id="6be2c-113">This code causes an error because the compiler terminates the string after the second quotation mark, and the remainder of the string is interpreted as code.</span></span> <span data-ttu-id="6be2c-114">為了解決這個問題，Visual Basic 將字串常值中的兩個引號視為字串中的一個引號。</span><span class="sxs-lookup"><span data-stu-id="6be2c-114">To solve this problem, Visual Basic interprets two quotation marks in a string literal as one quotation mark in the string.</span></span> <span data-ttu-id="6be2c-115">下列範例示範在字串中包含引號的正確方式：</span><span class="sxs-lookup"><span data-stu-id="6be2c-115">The following example demonstrates the correct way to include a quotation mark in a string:</span></span>  
  
 [!code-vb[VbVbalrStrings#66](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#66)]  
  
 <span data-ttu-id="6be2c-116">在上述範例中，`Look` 文字前面的兩個引號會成為字串中的一個引號。</span><span class="sxs-lookup"><span data-stu-id="6be2c-116">In the preceding example, the two quotation marks preceding the word `Look` become one quotation mark in the string.</span></span> <span data-ttu-id="6be2c-117">一行結尾處的三個引號表示字串和字串結束字元的一個引號。</span><span class="sxs-lookup"><span data-stu-id="6be2c-117">The three quotation marks at the end of the line represent one quotation mark in the string and the string termination character.</span></span>  
  
 <span data-ttu-id="6be2c-118">字串常值可以包含多行：</span><span class="sxs-lookup"><span data-stu-id="6be2c-118">String literals can contain multiple lines:</span></span>  
  
```vb  
Dim x = "hello  
world"  
```  
  
 <span data-ttu-id="6be2c-119">產生的字串包含用於字串常值 (vbcr、vbcrlf 等) 的新行字元序列。</span><span class="sxs-lookup"><span data-stu-id="6be2c-119">The resulting string contains newline sequences that you used in your string literal (vbcr, vbcrlf, etc.).</span></span>  <span data-ttu-id="6be2c-120">您不再需要使用舊的因應措施：</span><span class="sxs-lookup"><span data-stu-id="6be2c-120">You no longer need to use the old workaround:</span></span>  
  
```vb  
Dim x = <xml><![CDATA[Hello  
World]]></xml>.Value  
```  
  
## <a name="characters-in-strings"></a><span data-ttu-id="6be2c-121">字串中的字元</span><span class="sxs-lookup"><span data-stu-id="6be2c-121">Characters in Strings</span></span>  
 <span data-ttu-id="6be2c-122">字串可以視為 `Char` 值序列，且 `String` 類型具有內建函式，可讓您在字串上執行許多操作 (類似於陣列所允許的操作)。</span><span class="sxs-lookup"><span data-stu-id="6be2c-122">A string can be thought of as a series of `Char` values, and the `String` type has built-in functions that allow you to perform many manipulations on a string that resemble the manipulations allowed by arrays.</span></span> <span data-ttu-id="6be2c-123">就像 .NET Framework 中的所有陣列一樣，這些都是以零為基底的陣列。</span><span class="sxs-lookup"><span data-stu-id="6be2c-123">Like all array in .NET Framework, these are zero-based arrays.</span></span> <span data-ttu-id="6be2c-124">您可以透過 `Chars` 屬性參考字串中的特殊字元 ，讓您能夠依字元在字串中的出現位置存取該字元。</span><span class="sxs-lookup"><span data-stu-id="6be2c-124">You may refer to a specific character in a string through the `Chars` property, which provides a way to access a character by the position in which it appears in the string.</span></span> <span data-ttu-id="6be2c-125">例如：</span><span class="sxs-lookup"><span data-stu-id="6be2c-125">For example:</span></span>  
  
 [!code-vb[VbVbalrStrings#67](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#67)]  
  
 <span data-ttu-id="6be2c-126">在上述範例中，字串的 `Chars` 屬性會傳回字串中的第四個字元，也就是 `D`，並將其指派給 `myChar`。</span><span class="sxs-lookup"><span data-stu-id="6be2c-126">In the above example, the `Chars` property of the string returns the fourth character in the string, which is `D`, and assigns it to `myChar`.</span></span> <span data-ttu-id="6be2c-127">您也可以透過 `Length` 屬性取得特定字串的長度。</span><span class="sxs-lookup"><span data-stu-id="6be2c-127">You can also get the length of a particular string through the `Length` property.</span></span> <span data-ttu-id="6be2c-128">如果您需要在字串上執行多個陣列類型操作，您可以使用字串的 `ToCharArray` 函式將它轉換為 `Char` 執行個體陣列。</span><span class="sxs-lookup"><span data-stu-id="6be2c-128">If you need to perform multiple array-type manipulations on a string, you can convert it to an array of `Char` instances using the `ToCharArray` function of the string.</span></span> <span data-ttu-id="6be2c-129">例如：</span><span class="sxs-lookup"><span data-stu-id="6be2c-129">For example:</span></span>  
  
 [!code-vb[VbVbalrStrings#68](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#68)]  
  
 <span data-ttu-id="6be2c-130">變數 `myArray` 現在包含 `Char` 值的陣列，每個都代表 `myString` 的一個字元。</span><span class="sxs-lookup"><span data-stu-id="6be2c-130">The variable `myArray` now contains an array of `Char` values, each representing a character from `myString`.</span></span>  
  
## <a name="the-immutability-of-strings"></a><span data-ttu-id="6be2c-131">字串的不變性</span><span class="sxs-lookup"><span data-stu-id="6be2c-131">The Immutability of Strings</span></span>  
 <span data-ttu-id="6be2c-132">字串是*不可變*的，這表示一旦建立之後，就無法變更其值。</span><span class="sxs-lookup"><span data-stu-id="6be2c-132">A string is *immutable*, which means its value cannot be changed once it has been created.</span></span> <span data-ttu-id="6be2c-133">不過，這不會讓您將多個值指派給一個字串變數。</span><span class="sxs-lookup"><span data-stu-id="6be2c-133">However, this does not prevent you from assigning more than one value to a string variable.</span></span> <span data-ttu-id="6be2c-134">請考慮下列範例：</span><span class="sxs-lookup"><span data-stu-id="6be2c-134">Consider the following example:</span></span>  
  
 [!code-vb[VbVbalrStrings#69](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#69)]  
  
 <span data-ttu-id="6be2c-135">在這裡會建立字串變數、指定值，然後變更其值。</span><span class="sxs-lookup"><span data-stu-id="6be2c-135">Here, a string variable is created, given a value, and then its value is changed.</span></span>  
  
 <span data-ttu-id="6be2c-136">更具體來說，在第一行中，會建立類型 `String` 的執行個體並提供值 `This string is immutable`。</span><span class="sxs-lookup"><span data-stu-id="6be2c-136">More specifically, in the first line, an instance of type `String` is created and given the value `This string is immutable`.</span></span> <span data-ttu-id="6be2c-137">在此範例的第二行，建立新執行個體並指定值 `Or is it?`，且字串變數會捨棄其對第一個執行個體的參考，並儲存新執行個體的參考。</span><span class="sxs-lookup"><span data-stu-id="6be2c-137">In the second line of the example, a new instance is created and given the value `Or is it?`, and the string variable discards its reference to the first instance and stores a reference to the new instance.</span></span>  
  
 <span data-ttu-id="6be2c-138">不同於其他內建資料類型，`String` 是參考類型。</span><span class="sxs-lookup"><span data-stu-id="6be2c-138">Unlike other intrinsic data types, `String` is a reference type.</span></span> <span data-ttu-id="6be2c-139">將參考類型的變數做為引數傳遞給函式或副程式時，會傳遞儲存資料的記憶體位址的參考，而不是字串的實際值。</span><span class="sxs-lookup"><span data-stu-id="6be2c-139">When a variable of reference type is passed as an argument to a function or subroutine, a reference to the memory address where the data is stored is passed instead of the actual value of the string.</span></span> <span data-ttu-id="6be2c-140">因此在前一個範例中，變數的名稱維持不變，但是它指向 `String` 類別的全新和不同的執行個體，其中包含新值。</span><span class="sxs-lookup"><span data-stu-id="6be2c-140">So in the previous example, the name of the variable remains the same, but it points to a new and different instance of the `String` class, which holds the new value.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="6be2c-141">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6be2c-141">See also</span></span>

- [<span data-ttu-id="6be2c-142">Visual Basic 中的字串簡介</span><span class="sxs-lookup"><span data-stu-id="6be2c-142">Introduction to Strings in Visual Basic</span></span>](introduction-to-strings.md)
- [<span data-ttu-id="6be2c-143">String 資料類型</span><span class="sxs-lookup"><span data-stu-id="6be2c-143">String Data Type</span></span>](../../../language-reference/data-types/string-data-type.md)
- [<span data-ttu-id="6be2c-144">Char 資料類型</span><span class="sxs-lookup"><span data-stu-id="6be2c-144">Char Data Type</span></span>](../../../language-reference/data-types/char-data-type.md)
- [<span data-ttu-id="6be2c-145">基底字元串作業</span><span class="sxs-lookup"><span data-stu-id="6be2c-145">Basic String Operations</span></span>](../../../../standard/base-types/basic-string-operations.md)
