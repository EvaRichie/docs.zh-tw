---
title: 常數概觀
ms.date: 07/20/2015
helpviewer_keywords:
- constants [Visual Basic]
ms.assetid: 29016fe8-78b3-4dc8-90b8-1cfec2fa8ac9
ms.openlocfilehash: f45cb12c6ef0f90b9c90190f30ce8600fec80947
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84414514"
---
# <a name="constants-overview-visual-basic"></a><span data-ttu-id="8556f-102">常數的概觀 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="8556f-102">Constants Overview (Visual Basic)</span></span>
<span data-ttu-id="8556f-103">常數是有意義的名稱，用來取代不會變更的數位或字串。</span><span class="sxs-lookup"><span data-stu-id="8556f-103">A constant is a meaningful name that takes the place of a number or string that does not change.</span></span> <span data-ttu-id="8556f-104">如同名稱所示，常數會儲存應用程式執行時保持不變的值。</span><span class="sxs-lookup"><span data-stu-id="8556f-104">Constants store values that, as the name implies, remain the same throughout the execution of an application.</span></span> <span data-ttu-id="8556f-105">您可以大幅改善程式碼的可讀性，並讓您更輕鬆地使用常數進行維護。</span><span class="sxs-lookup"><span data-stu-id="8556f-105">You can greatly improve the readability of your code and make it easier to maintain by using constants.</span></span> <span data-ttu-id="8556f-106">在程式碼中使用它們，其中包含重新出現的值，或取決於不容易記住或沒有明顯意義的特定數位。</span><span class="sxs-lookup"><span data-stu-id="8556f-106">Use them in code that contains values that reappear or that depends on certain numbers that are difficult to remember or have no obvious meaning.</span></span>  
  
## <a name="how-to-create-and-use-constants"></a><span data-ttu-id="8556f-107">如何建立和使用常數</span><span class="sxs-lookup"><span data-stu-id="8556f-107">How to Create and Use Constants</span></span>  
 <span data-ttu-id="8556f-108">Visual Basic 包含許多預先定義的常數，主要是用來列印和顯示。</span><span class="sxs-lookup"><span data-stu-id="8556f-108">Visual Basic contains a number of predefined constants, mainly using for printing and displaying.</span></span> <span data-ttu-id="8556f-109">您也可以使用語句來建立自己的常數 `Const` ，如同建立變數名稱所用的相同方針。</span><span class="sxs-lookup"><span data-stu-id="8556f-109">You can also create your own constants with the `Const` statement, using the same guidelines you would for creating a variable name.</span></span> <span data-ttu-id="8556f-110">如果 `Option Strict` 為 `On` ，則您必須明確宣告常數類型。</span><span class="sxs-lookup"><span data-stu-id="8556f-110">If `Option Strict` is `On`, you must explicitly declare the constant type.</span></span>  
  
 <span data-ttu-id="8556f-111">常數的範圍，這是一組可以參考它而不限定其名稱的程式碼，與相同位置中宣告的變數相同。</span><span class="sxs-lookup"><span data-stu-id="8556f-111">A constant's scope, which is the set of all code that can refer to it without qualifying its name, is the same as that of a variable declared in the same location.</span></span> <span data-ttu-id="8556f-112">若要建立存在於特定程式範圍內的常數，請在該程式內宣告。</span><span class="sxs-lookup"><span data-stu-id="8556f-112">To create a constant that exists within the scope of a particular procedure, declare it inside that procedure.</span></span> <span data-ttu-id="8556f-113">若要建立可在整個應用程式中使用的常數，請 `Public` 在類別的宣告區段中使用關鍵字進行宣告。</span><span class="sxs-lookup"><span data-stu-id="8556f-113">To create a constant that is available throughout an application, declare it using the `Public` keyword in the declarations section of the class.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="8556f-114">雖然常數有點類似變數，但是您無法修改它們，或將新值指派給它們，就像您可以變數一樣。</span><span class="sxs-lookup"><span data-stu-id="8556f-114">Although constants somewhat resemble variables, you cannot modify them or assign new values to them as you can to variables.</span></span>  
  
 <span data-ttu-id="8556f-115">您在程式碼中使用的常數可以由您所使用之控制項或元件的物件模型來定義，也可以是使用者定義的（也就是您自行建立的）。</span><span class="sxs-lookup"><span data-stu-id="8556f-115">The constants you use in your code can be defined by the object model for controls or components you work with, or they can be user-defined (that is, those you create yourself).</span></span>  
  
## <a name="compile-time-and-run-time-constants"></a><span data-ttu-id="8556f-116">編譯時間和執行時間常數</span><span class="sxs-lookup"><span data-stu-id="8556f-116">Compile-time and Run-time Constants</span></span>  
 <span data-ttu-id="8556f-117">編譯時間常數會在程式碼編譯時計算，而執行時間常數則只能在應用程式執行時計算。</span><span class="sxs-lookup"><span data-stu-id="8556f-117">A compile-time constant is computed at the time the code is compiled, while a run-time constant can only be computed while the application is running.</span></span> <span data-ttu-id="8556f-118">每次執行應用程式時，編譯時間常數將會有相同的值，而執行時間常數可能會每次都變更。</span><span class="sxs-lookup"><span data-stu-id="8556f-118">A compile-time constant will have the same value each time an application runs, while a run-time constant may change each time.</span></span> <span data-ttu-id="8556f-119">如陣列界限、case 運算式或列舉值初始化運算式等案例，則需要編譯時間常數。</span><span class="sxs-lookup"><span data-stu-id="8556f-119">Compile-time constants are required for cases such as array bounds, case expressions, or enumerator initializers.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="8556f-120">本節內容</span><span class="sxs-lookup"><span data-stu-id="8556f-120">In This Section</span></span>  
  
|<span data-ttu-id="8556f-121">定義</span><span class="sxs-lookup"><span data-stu-id="8556f-121">Definition</span></span>|<span data-ttu-id="8556f-122">詞彙</span><span class="sxs-lookup"><span data-stu-id="8556f-122">Term</span></span>|  
|---|---|  
|[<span data-ttu-id="8556f-123">如何：宣告常數</span><span class="sxs-lookup"><span data-stu-id="8556f-123">How to: Declare A Constant</span></span>](how-to-declare-a-constant.md)|<span data-ttu-id="8556f-124">說明如何使用 `Const` 語句來宣告常數並設定其值; 藉由宣告常數，您可以將有意義的名稱指派給值。</span><span class="sxs-lookup"><span data-stu-id="8556f-124">Explains how to use the `Const` statement to declare a constant and set its value; by declaring a constant, you assign a meaningful name to the value.</span></span>|  
|[<span data-ttu-id="8556f-125">使用者定義的常數</span><span class="sxs-lookup"><span data-stu-id="8556f-125">User-Defined Constants</span></span>](user-defined-constants.md)|<span data-ttu-id="8556f-126">描述如何建立您自己的常數，包括範圍的資訊，以及如何避免迴圈參考。</span><span class="sxs-lookup"><span data-stu-id="8556f-126">Describes how to create your own constants, including information on scoping and how to avoid circular references.</span></span>|  
|[<span data-ttu-id="8556f-127">常數和常值資料類型</span><span class="sxs-lookup"><span data-stu-id="8556f-127">Constant and Literal Data Types</span></span>](constant-and-literal-data-types.md)|<span data-ttu-id="8556f-128">提供當關閉時，Visual Basic 編譯器如何初始化常數的相關資訊 `Option Explicit` 。</span><span class="sxs-lookup"><span data-stu-id="8556f-128">Provides information on how the Visual Basic compiler initializes constants when `Option Explicit` is turned off.</span></span>|  
|[<span data-ttu-id="8556f-129">如何：將關聯的常數值群組在一起</span><span class="sxs-lookup"><span data-stu-id="8556f-129">How to: Group Related Constant Values Together</span></span>](how-to-group-related-constant-values-together.md)|<span data-ttu-id="8556f-130">示範如何將相關的常數值群組在一起。</span><span class="sxs-lookup"><span data-stu-id="8556f-130">Demonstrates how to group constant values that are related.</span></span>|  
  
## <a name="reference"></a><span data-ttu-id="8556f-131">參考</span><span class="sxs-lookup"><span data-stu-id="8556f-131">Reference</span></span>  
  
|<span data-ttu-id="8556f-132">定義</span><span class="sxs-lookup"><span data-stu-id="8556f-132">Definition</span></span>|<span data-ttu-id="8556f-133">詞彙</span><span class="sxs-lookup"><span data-stu-id="8556f-133">Term</span></span>|  
|---|---|  
|[<span data-ttu-id="8556f-134">常數和列舉</span><span class="sxs-lookup"><span data-stu-id="8556f-134">Constants and Enumerations</span></span>](../../../language-reference/constants-and-enumerations.md)|<span data-ttu-id="8556f-135">列出 Visual Basic 預先定義的常數。</span><span class="sxs-lookup"><span data-stu-id="8556f-135">Lists the constants predefined by Visual Basic.</span></span>|  
|[<span data-ttu-id="8556f-136">Const 陳述式</span><span class="sxs-lookup"><span data-stu-id="8556f-136">Const Statement</span></span>](../../../language-reference/statements/const-statement.md)|<span data-ttu-id="8556f-137">描述 `Const` 語句及其用法。</span><span class="sxs-lookup"><span data-stu-id="8556f-137">Describes the `Const` statement and its use.</span></span>|  
|[<span data-ttu-id="8556f-138">Long</span><span class="sxs-lookup"><span data-stu-id="8556f-138">Option Strict Statement</span></span>](../../../language-reference/statements/option-strict-statement.md)|<span data-ttu-id="8556f-139">描述 `Option Strict` 語句及其用法。</span><span class="sxs-lookup"><span data-stu-id="8556f-139">Describes the `Option Strict` statement and its use.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="8556f-140">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8556f-140">See also</span></span>

- [<span data-ttu-id="8556f-141">列舉的概觀</span><span class="sxs-lookup"><span data-stu-id="8556f-141">Enumerations Overview</span></span>](enumerations-overview.md)
- [<span data-ttu-id="8556f-142">如何：在 Visual Basic 中初始化陣列變數</span><span class="sxs-lookup"><span data-stu-id="8556f-142">How to: Initialize an Array Variable in Visual Basic</span></span>](../arrays/how-to-initialize-an-array-variable.md)
