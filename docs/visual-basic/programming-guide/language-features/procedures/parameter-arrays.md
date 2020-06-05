---
title: 參數陣列
ms.date: 07/20/2015
helpviewer_keywords:
- parameter arrays [Visual Basic], about parameter arrays
- ParamArray keyword [Visual Basic], parameter arrays
- Visual Basic code, procedures
- parameters [Visual Basic], parameter arrays
- arguments [Visual Basic], parameter arrays
- procedures [Visual Basic], indefinite number of argument values
- arrays [Visual Basic], parameter arrays
ms.assetid: c43edfae-9114-4096-9ebc-8c5c957a1067
ms.openlocfilehash: dac0575d73ffd4159e89bff344915a33b9d0e5d3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84364275"
---
# <a name="parameter-arrays-visual-basic"></a><span data-ttu-id="6a9d1-102">參數陣列 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="6a9d1-102">Parameter Arrays (Visual Basic)</span></span>
<span data-ttu-id="6a9d1-103">通常，您不能使用比程式宣告指定的多個引數來呼叫程式。</span><span class="sxs-lookup"><span data-stu-id="6a9d1-103">Usually, you cannot call a procedure with more arguments than the procedure declaration specifies.</span></span> <span data-ttu-id="6a9d1-104">當您需要不限數目的引數時，您可以宣告*參數陣列*，讓程式接受參數值陣列。</span><span class="sxs-lookup"><span data-stu-id="6a9d1-104">When you need an indefinite number of arguments, you can declare a *parameter array*, which allows a procedure to accept an array of values for a parameter.</span></span> <span data-ttu-id="6a9d1-105">當您定義程式時，不需要知道參數陣列中的元素數目。</span><span class="sxs-lookup"><span data-stu-id="6a9d1-105">You do not have to know the number of elements in the parameter array when you define the procedure.</span></span> <span data-ttu-id="6a9d1-106">陣列大小是由程式的每個呼叫個別決定。</span><span class="sxs-lookup"><span data-stu-id="6a9d1-106">The array size is determined individually by each call to the procedure.</span></span>  
  
## <a name="declaring-a-paramarray"></a><span data-ttu-id="6a9d1-107">宣告 ParamArray</span><span class="sxs-lookup"><span data-stu-id="6a9d1-107">Declaring a ParamArray</span></span>  
 <span data-ttu-id="6a9d1-108">您可以使用[ParamArray](../../../language-reference/modifiers/paramarray.md)關鍵字來表示參數清單中的參數陣列。</span><span class="sxs-lookup"><span data-stu-id="6a9d1-108">You use the [ParamArray](../../../language-reference/modifiers/paramarray.md) keyword to denote a parameter array in the parameter list.</span></span> <span data-ttu-id="6a9d1-109">適用的規則如下：</span><span class="sxs-lookup"><span data-stu-id="6a9d1-109">The following rules apply:</span></span>  
  
- <span data-ttu-id="6a9d1-110">程式只能定義一個參數陣列，而且它必須是程序定義中的最後一個參數。</span><span class="sxs-lookup"><span data-stu-id="6a9d1-110">A procedure can define only one parameter array, and it must be the last parameter in the procedure definition.</span></span>  
  
- <span data-ttu-id="6a9d1-111">參數陣列必須以傳值方式傳遞。</span><span class="sxs-lookup"><span data-stu-id="6a9d1-111">The parameter array must be passed by value.</span></span> <span data-ttu-id="6a9d1-112">在程序定義中明確包含[ByVal](../../../language-reference/modifiers/byval.md)關鍵字是良好的程式設計作法。</span><span class="sxs-lookup"><span data-stu-id="6a9d1-112">It is good programming practice to explicitly include the [ByVal](../../../language-reference/modifiers/byval.md) keyword in the procedure definition.</span></span>  
  
- <span data-ttu-id="6a9d1-113">參數陣列是自動選擇的。</span><span class="sxs-lookup"><span data-stu-id="6a9d1-113">The parameter array is automatically optional.</span></span> <span data-ttu-id="6a9d1-114">其預設值為參數陣列的元素類型的一維空陣列。</span><span class="sxs-lookup"><span data-stu-id="6a9d1-114">Its default value is an empty one-dimensional array of the parameter array's element type.</span></span>  
  
- <span data-ttu-id="6a9d1-115">參數陣列前面的所有參數都必須是必要的。</span><span class="sxs-lookup"><span data-stu-id="6a9d1-115">All parameters preceding the parameter array must be required.</span></span> <span data-ttu-id="6a9d1-116">參數陣列必須是唯一的選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="6a9d1-116">The parameter array must be the only optional parameter.</span></span>  
  
## <a name="calling-a-paramarray"></a><span data-ttu-id="6a9d1-117">呼叫 ParamArray</span><span class="sxs-lookup"><span data-stu-id="6a9d1-117">Calling a ParamArray</span></span>  
 <span data-ttu-id="6a9d1-118">當您呼叫定義參數陣列的程式時，您可以使用下列任何一種方式提供引數：</span><span class="sxs-lookup"><span data-stu-id="6a9d1-118">When you call a procedure that defines a parameter array, you can supply the argument in any one of the following ways:</span></span>  
  
- <span data-ttu-id="6a9d1-119">沒有，也就是說，您可以省略[ParamArray](../../../language-reference/modifiers/paramarray.md)引數。</span><span class="sxs-lookup"><span data-stu-id="6a9d1-119">Nothing — that is, you can omit the [ParamArray](../../../language-reference/modifiers/paramarray.md) argument.</span></span> <span data-ttu-id="6a9d1-120">在此情況下，會將空的陣列傳遞給程式。</span><span class="sxs-lookup"><span data-stu-id="6a9d1-120">In this case, an empty array is passed to the procedure.</span></span> <span data-ttu-id="6a9d1-121">如果您明確地傳遞[not 關鍵字，](../../../language-reference/nothing.md)則會將 null 陣列傳遞給程式，如果被呼叫的程式未檢查這個條件，可能會產生 NullReferenceException。</span><span class="sxs-lookup"><span data-stu-id="6a9d1-121">If you explicitly pass the [Nothing](../../../language-reference/nothing.md) keyword, a null array is passed to the procedure and may result in a NullReferenceException if the called procedure does not check for this condition.</span></span>
  
- <span data-ttu-id="6a9d1-122">任意數目的引數清單（以逗號分隔）。</span><span class="sxs-lookup"><span data-stu-id="6a9d1-122">A list of an arbitrary number of arguments, separated by commas.</span></span> <span data-ttu-id="6a9d1-123">每個引數的資料類型必須可以隱含地轉換成 `ParamArray` 元素類型。</span><span class="sxs-lookup"><span data-stu-id="6a9d1-123">The data type of each argument must be implicitly convertible to the `ParamArray` element type.</span></span>  
  
- <span data-ttu-id="6a9d1-124">陣列，其元素類型與參數陣列的元素類型相同。</span><span class="sxs-lookup"><span data-stu-id="6a9d1-124">An array with the same element type as the parameter array's element type.</span></span>  
  
 <span data-ttu-id="6a9d1-125">在所有情況下，程式內的程式碼會將參數陣列視為一維陣列，其中包含與資料類型相同之資料類型的元素 `ParamArray` 。</span><span class="sxs-lookup"><span data-stu-id="6a9d1-125">In all cases, the code within the procedure treats the parameter array as a one-dimensional array with elements of the same data type as the `ParamArray` data type.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="6a9d1-126">當您處理可能會無限大的陣列時，會有 overrunning 應用程式的一些內部容量的風險。</span><span class="sxs-lookup"><span data-stu-id="6a9d1-126">Whenever you deal with an array which can be indefinitely large, there is a risk of overrunning some internal capacity of your application.</span></span> <span data-ttu-id="6a9d1-127">如果您接受參數陣列，您應該測試呼叫程式碼傳遞給它的陣列大小。</span><span class="sxs-lookup"><span data-stu-id="6a9d1-127">If you accept a parameter array, you should test for the size of the array that the calling code passed to it.</span></span> <span data-ttu-id="6a9d1-128">如果您的應用程式太大，請採取適當的步驟。</span><span class="sxs-lookup"><span data-stu-id="6a9d1-128">Take appropriate steps if it is too large for your application.</span></span> <span data-ttu-id="6a9d1-129">如需詳細資訊，請參閱[陣列](../arrays/index.md)。</span><span class="sxs-lookup"><span data-stu-id="6a9d1-129">For more information, see [Arrays](../arrays/index.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="6a9d1-130">範例</span><span class="sxs-lookup"><span data-stu-id="6a9d1-130">Example</span></span>  
 <span data-ttu-id="6a9d1-131">下列範例會定義和呼叫函式 `calcSum` 。</span><span class="sxs-lookup"><span data-stu-id="6a9d1-131">The following example defines and calls the function `calcSum`.</span></span> <span data-ttu-id="6a9d1-132">`ParamArray`參數的修飾詞可讓函式 `args` 接受可變數目的引數。</span><span class="sxs-lookup"><span data-stu-id="6a9d1-132">The `ParamArray` modifier for the parameter `args` enables the function to accept a variable number of arguments.</span></span>  
  
 [!code-vb[VbVbalrStatements#26](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#26)]  
  
 <span data-ttu-id="6a9d1-133">下列範例會定義具有參數陣列的程式，並輸出傳遞至參數陣列之所有陣列元素的值。</span><span class="sxs-lookup"><span data-stu-id="6a9d1-133">The following example defines a procedure with a parameter array, and outputs the values of all the array elements passed to the parameter array.</span></span>  
  
 [!code-vb[VbVbcnProcedures#48](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#48)]  
  
 [!code-vb[VbVbcnProcedures#49](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#49)]  
  
## <a name="see-also"></a><span data-ttu-id="6a9d1-134">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6a9d1-134">See also</span></span>

- <xref:Microsoft.VisualBasic.Information.UBound%2A>
- [<span data-ttu-id="6a9d1-135">程序</span><span class="sxs-lookup"><span data-stu-id="6a9d1-135">Procedures</span></span>](./index.md)
- [<span data-ttu-id="6a9d1-136">程序參數和引數</span><span class="sxs-lookup"><span data-stu-id="6a9d1-136">Procedure Parameters and Arguments</span></span>](./procedure-parameters-and-arguments.md)
- [<span data-ttu-id="6a9d1-137">以傳值和傳址方式傳遞引數</span><span class="sxs-lookup"><span data-stu-id="6a9d1-137">Passing Arguments by Value and by Reference</span></span>](./passing-arguments-by-value-and-by-reference.md)
- [<span data-ttu-id="6a9d1-138">依位置和名稱傳遞引數</span><span class="sxs-lookup"><span data-stu-id="6a9d1-138">Passing Arguments by Position and by Name</span></span>](./passing-arguments-by-position-and-by-name.md)
- [<span data-ttu-id="6a9d1-139">選擇性參數</span><span class="sxs-lookup"><span data-stu-id="6a9d1-139">Optional Parameters</span></span>](./optional-parameters.md)
- [<span data-ttu-id="6a9d1-140">程序多載化</span><span class="sxs-lookup"><span data-stu-id="6a9d1-140">Procedure Overloading</span></span>](./procedure-overloading.md)
- [<span data-ttu-id="6a9d1-141">陣列</span><span class="sxs-lookup"><span data-stu-id="6a9d1-141">Arrays</span></span>](../arrays/index.md)
- [<span data-ttu-id="6a9d1-142">選擇性</span><span class="sxs-lookup"><span data-stu-id="6a9d1-142">Optional</span></span>](../../../language-reference/modifiers/optional.md)
