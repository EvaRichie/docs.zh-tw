---
title: <<= 運算子
ms.date: 07/20/2015
f1_keywords:
- vb.<<=
helpviewer_keywords:
- operator <<=
- assignment statements [Visual Basic], compound
- <<= operator [Visual Basic]
- statements [Visual Basic], compound assignment
- operator<<=
- compound assignment statements [Visual Basic]
ms.assetid: 8ad26613-faff-4e2f-89ee-63feee33bfda
ms.openlocfilehash: 72fc842002586a4d5e48bc39b5c785fc6a9e9451
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90866905"
---
# <a name="-operator-visual-basic"></a><span data-ttu-id="789b8-102">\<\<= 運算子 (Visual Basic) </span><span class="sxs-lookup"><span data-stu-id="789b8-102">\<\<= Operator (Visual Basic)</span></span>

<span data-ttu-id="789b8-103">在變數或屬性的值上執行算術左移位，並將結果指派回變數或屬性。</span><span class="sxs-lookup"><span data-stu-id="789b8-103">Performs an arithmetic left shift on the value of a variable or property and assigns the result back to the variable or property.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="789b8-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="789b8-104">Syntax</span></span>  
  
```vb  
variableorproperty <<= amount  
```  
  
## <a name="parts"></a><span data-ttu-id="789b8-105">組件</span><span class="sxs-lookup"><span data-stu-id="789b8-105">Parts</span></span>  

 `variableorproperty`  
 <span data-ttu-id="789b8-106">必要。</span><span class="sxs-lookup"><span data-stu-id="789b8-106">Required.</span></span> <span data-ttu-id="789b8-107">整數類資料類型的變數或屬性 (、、、、、、 `SByte` `Byte` `Short` `UShort` `Integer` `UInteger` `Long` 或 `ULong`) 。</span><span class="sxs-lookup"><span data-stu-id="789b8-107">Variable or property of an integral type (`SByte`, `Byte`, `Short`, `UShort`, `Integer`, `UInteger`, `Long`, or `ULong`).</span></span>  
  
 `amount`  
 <span data-ttu-id="789b8-108">必要。</span><span class="sxs-lookup"><span data-stu-id="789b8-108">Required.</span></span> <span data-ttu-id="789b8-109">擴大至之資料類型的數值運算式 `Integer` 。</span><span class="sxs-lookup"><span data-stu-id="789b8-109">Numeric expression of a data type that widens to `Integer`.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="789b8-110">備註</span><span class="sxs-lookup"><span data-stu-id="789b8-110">Remarks</span></span>  

 <span data-ttu-id="789b8-111">運算子左邊的元素 `<<=` 可以是簡單的純量變數、屬性或陣列的元素。</span><span class="sxs-lookup"><span data-stu-id="789b8-111">The element on the left side of the `<<=` operator can be a simple scalar variable, a property, or an element of an array.</span></span> <span data-ttu-id="789b8-112">變數或屬性不可以是 [ReadOnly](../modifiers/readonly.md)。</span><span class="sxs-lookup"><span data-stu-id="789b8-112">The variable or property cannot be [ReadOnly](../modifiers/readonly.md).</span></span>  
  
 <span data-ttu-id="789b8-113">`<<=`運算子會先在變數或屬性的值上執行算術左移位。</span><span class="sxs-lookup"><span data-stu-id="789b8-113">The `<<=` operator first performs an arithmetic left shift on the value of the variable or property.</span></span> <span data-ttu-id="789b8-114">然後，運算子會將該操作的結果指派回該變數或屬性。</span><span class="sxs-lookup"><span data-stu-id="789b8-114">The operator then assigns the result of that operation back to that variable or property.</span></span>  
  
 <span data-ttu-id="789b8-115">算術移位不是迴圈的，這表示不會在另一端重新出現從結果的一端移出的位。</span><span class="sxs-lookup"><span data-stu-id="789b8-115">Arithmetic shifts are not circular, which means the bits shifted off one end of the result are not reintroduced at the other end.</span></span> <span data-ttu-id="789b8-116">在算術左移位中，會捨棄超出結果資料類型範圍的位，而且右邊的位位置會設定為零。</span><span class="sxs-lookup"><span data-stu-id="789b8-116">In an arithmetic left shift, the bits shifted beyond the range of the result data type are discarded, and the bit positions vacated on the right are set to zero.</span></span>  
  
## <a name="overloading"></a><span data-ttu-id="789b8-117">多載化</span><span class="sxs-lookup"><span data-stu-id="789b8-117">Overloading</span></span>  

 <span data-ttu-id="789b8-118">您可以多載 [<< 運算子](left-shift-operator.md) ，這表示當運算元的類型為該類別或結構 *時，類別*或結構可以重新定義其行為。</span><span class="sxs-lookup"><span data-stu-id="789b8-118">The [<< Operator](left-shift-operator.md) can be *overloaded*, which means that a class or structure can redefine its behavior when an operand has the type of that class or structure.</span></span> <span data-ttu-id="789b8-119">多載 `<<` 運算子會影響運算子的行為 `<<=` 。</span><span class="sxs-lookup"><span data-stu-id="789b8-119">Overloading the `<<` operator affects the behavior of the `<<=` operator.</span></span> <span data-ttu-id="789b8-120">如果您的程式碼在多載的 `<<=` 類別或結構上使用 `<<` ，請務必瞭解其重新定義的行為。</span><span class="sxs-lookup"><span data-stu-id="789b8-120">If your code uses `<<=` on a class or structure that overloads `<<`, be sure you understand its redefined behavior.</span></span> <span data-ttu-id="789b8-121">如需詳細資訊，請參閱 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)。</span><span class="sxs-lookup"><span data-stu-id="789b8-121">For more information, see [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="789b8-122">範例</span><span class="sxs-lookup"><span data-stu-id="789b8-122">Example</span></span>  

 <span data-ttu-id="789b8-123">下列範例會使用運算子，將 `<<=` 變數的位模式向 `Integer` 左移位指定的數量，並將結果指派給變數。</span><span class="sxs-lookup"><span data-stu-id="789b8-123">The following example uses the `<<=` operator to shift the bit pattern of an `Integer` variable left by the specified amount and assign the result to the variable.</span></span>  
  
 [!code-vb[VbVbalrOperators#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#13)]  
  
## <a name="see-also"></a><span data-ttu-id="789b8-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="789b8-124">See also</span></span>

- [<span data-ttu-id="789b8-125"><< 運算子</span><span class="sxs-lookup"><span data-stu-id="789b8-125"><< Operator</span></span>](left-shift-operator.md)
- [<span data-ttu-id="789b8-126">指派運算子</span><span class="sxs-lookup"><span data-stu-id="789b8-126">Assignment Operators</span></span>](assignment-operators.md)
- [<span data-ttu-id="789b8-127">位元移位運算子</span><span class="sxs-lookup"><span data-stu-id="789b8-127">Bit Shift Operators</span></span>](bit-shift-operators.md)
- [<span data-ttu-id="789b8-128">Visual Basic 中的運算子優先順序</span><span class="sxs-lookup"><span data-stu-id="789b8-128">Operator Precedence in Visual Basic</span></span>](operator-precedence.md)
- [<span data-ttu-id="789b8-129">依功能列出運算子</span><span class="sxs-lookup"><span data-stu-id="789b8-129">Operators Listed by Functionality</span></span>](operators-listed-by-functionality.md)
- [<span data-ttu-id="789b8-130">陳述式</span><span class="sxs-lookup"><span data-stu-id="789b8-130">Statements</span></span>](../../programming-guide/language-features/statements.md)
