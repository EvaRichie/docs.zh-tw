---
title: AddressOf 運算子
ms.date: 07/20/2015
f1_keywords:
- AddressOf
- vb.AddressOf
helpviewer_keywords:
- AddressOf operator [Visual Basic]
- addresses, passing to API procedures
ms.assetid: 8105a59d-60d8-4ab5-b221-5899cdfacbf4
ms.openlocfilehash: 3e7db8e7329ce8d21b6e07863e6f1673a6389608
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84372060"
---
# <a name="addressof-operator-visual-basic"></a><span data-ttu-id="2345f-102">AddressOf 運算子 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="2345f-102">AddressOf Operator (Visual Basic)</span></span>
<span data-ttu-id="2345f-103">建立參考特定程式的委派實例。</span><span class="sxs-lookup"><span data-stu-id="2345f-103">Creates a delegate instance that references the specific procedure.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="2345f-104">語法</span><span class="sxs-lookup"><span data-stu-id="2345f-104">Syntax</span></span>  
  
```vb  
AddressOf procedurename  
```  
  
## <a name="parts"></a><span data-ttu-id="2345f-105">組件</span><span class="sxs-lookup"><span data-stu-id="2345f-105">Parts</span></span>  
 `procedurename`  
 <span data-ttu-id="2345f-106">必要。</span><span class="sxs-lookup"><span data-stu-id="2345f-106">Required.</span></span> <span data-ttu-id="2345f-107">指定新建立的委派所要參考的程式。</span><span class="sxs-lookup"><span data-stu-id="2345f-107">Specifies the procedure to be referenced by the newly created delegate.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="2345f-108">備註</span><span class="sxs-lookup"><span data-stu-id="2345f-108">Remarks</span></span>  
 <span data-ttu-id="2345f-109">`AddressOf`運算子會建立指向指定之子函數或函式的委派 `procedurename` 。</span><span class="sxs-lookup"><span data-stu-id="2345f-109">The `AddressOf` operator creates a delegate that points to the sub or function specified by `procedurename`.</span></span> <span data-ttu-id="2345f-110">當指定的程式是實例方法時，委派會同時參考實例和方法。</span><span class="sxs-lookup"><span data-stu-id="2345f-110">When the specified procedure is an instance method then the delegate refers to both the instance and the method.</span></span> <span data-ttu-id="2345f-111">然後，當叫用委派時，會呼叫指定實例的指定方法。</span><span class="sxs-lookup"><span data-stu-id="2345f-111">Then, when the  delegate is invoked the specified method of the specified instance is called.</span></span>  
  
 <span data-ttu-id="2345f-112">`AddressOf`運算子可以做為委派函式的運算元使用，也可以用於可以由編譯器決定委派類型的內容中。</span><span class="sxs-lookup"><span data-stu-id="2345f-112">The `AddressOf` operator can be used as the operand of a delegate constructor or it can be used in a context in which the type of the delegate can be determined by the compiler.</span></span>  
  
## <a name="example"></a><span data-ttu-id="2345f-113">範例</span><span class="sxs-lookup"><span data-stu-id="2345f-113">Example</span></span>  
 <span data-ttu-id="2345f-114">這個範例會使用 `AddressOf` 運算子來指定委派，以處理 `Click` 按鈕的事件。</span><span class="sxs-lookup"><span data-stu-id="2345f-114">This example uses the `AddressOf` operator to designate a delegate to handle the `Click` event of a button.</span></span>  
  
 [!code-vb[VbVbalrDelegates#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDelegates/VB/Class1.vb#8)]  
  
## <a name="example"></a><span data-ttu-id="2345f-115">範例</span><span class="sxs-lookup"><span data-stu-id="2345f-115">Example</span></span>  
 <span data-ttu-id="2345f-116">下列範例會使用 `AddressOf` 運算子來指定執行緒的啟動函數。</span><span class="sxs-lookup"><span data-stu-id="2345f-116">The following example uses the `AddressOf` operator to designate the startup function for a thread.</span></span>  
  
 [!code-vb[VbVbalrDelegates#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDelegates/VB/Class1.vb#9)]  
  
## <a name="see-also"></a><span data-ttu-id="2345f-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2345f-117">See also</span></span>

- [<span data-ttu-id="2345f-118">Declare Statement</span><span class="sxs-lookup"><span data-stu-id="2345f-118">Declare Statement</span></span>](../statements/declare-statement.md)
- [<span data-ttu-id="2345f-119">Function 陳述式</span><span class="sxs-lookup"><span data-stu-id="2345f-119">Function Statement</span></span>](../statements/function-statement.md)
- [<span data-ttu-id="2345f-120">Sub 陳述式</span><span class="sxs-lookup"><span data-stu-id="2345f-120">Sub Statement</span></span>](../statements/sub-statement.md)
- [<span data-ttu-id="2345f-121">委派</span><span class="sxs-lookup"><span data-stu-id="2345f-121">Delegates</span></span>](../../programming-guide/language-features/delegates/index.md)
