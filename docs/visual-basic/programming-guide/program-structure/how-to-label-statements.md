---
title: 作法：Label 陳述式
ms.date: 07/20/2015
helpviewer_keywords:
- colons (:)
- statements [Visual Basic], labels
- ': separator character'
- Visual Basic code, labeling statements
ms.assetid: 38f1ff43-2054-42cb-963b-1998e60c6ed4
ms.openlocfilehash: 8f04d592c51b6a0630bfe623fd3574555aef9ff8
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403209"
---
# <a name="how-to-label-statements-visual-basic"></a><span data-ttu-id="0a923-102">如何：標記陳述式 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="0a923-102">How to: Label Statements (Visual Basic)</span></span>

<span data-ttu-id="0a923-103">語句區塊是由以冒號分隔的程式程式碼所組成。</span><span class="sxs-lookup"><span data-stu-id="0a923-103">Statement blocks are made up of lines of code delimited by colons.</span></span> <span data-ttu-id="0a923-104">前面加上識別字串或整數的程式程式碼，稱為*標記*。</span><span class="sxs-lookup"><span data-stu-id="0a923-104">Lines of code preceded by an identifying string or integer are said to be *labeled*.</span></span> <span data-ttu-id="0a923-105">語句標籤是用來標記程式程式碼，以識別它與語句搭配使用，例如 `On Error Goto` 。</span><span class="sxs-lookup"><span data-stu-id="0a923-105">Statement labels are used to mark a line of code to identify it for use with statements such as `On Error Goto`.</span></span>

<span data-ttu-id="0a923-106">標籤可能是有效的 Visual Basic 識別碼，例如可識別程式設計項目的識別碼，或整數常值。</span><span class="sxs-lookup"><span data-stu-id="0a923-106">Labels may be either valid Visual Basic identifiers—such as those that identify programming elements—or integer literals.</span></span> <span data-ttu-id="0a923-107">標籤必須出現在源程式碼首，而且後面必須加上冒號，而不論後面是否緊接著同一行的語句。</span><span class="sxs-lookup"><span data-stu-id="0a923-107">A label must appear at the beginning of a line of source code and must be followed by a colon, regardless of whether it is followed by a statement on the same line.</span></span>

<span data-ttu-id="0a923-108">編譯器會藉由檢查行的開頭是否符合任何已定義的識別碼來識別標籤。</span><span class="sxs-lookup"><span data-stu-id="0a923-108">The compiler identifies labels by checking whether the beginning of the line matches any already-defined identifier.</span></span> <span data-ttu-id="0a923-109">如果不是，則編譯器會假設它是標籤。</span><span class="sxs-lookup"><span data-stu-id="0a923-109">If it does not, the compiler assumes it is a label.</span></span>

<span data-ttu-id="0a923-110">標籤有自己的宣告空間，而且不會干擾其他識別碼。</span><span class="sxs-lookup"><span data-stu-id="0a923-110">Labels have their own declaration space and do not interfere with other identifiers.</span></span> <span data-ttu-id="0a923-111">標籤的範圍是方法的主體。</span><span class="sxs-lookup"><span data-stu-id="0a923-111">A label's scope is the body of the method.</span></span> <span data-ttu-id="0a923-112">標籤宣告的優先順序會在任何不明確的情況下。</span><span class="sxs-lookup"><span data-stu-id="0a923-112">Label declaration takes precedence in any ambiguous situation.</span></span>

> [!NOTE]
> <span data-ttu-id="0a923-113">標籤只能用於方法內的可執行語句。</span><span class="sxs-lookup"><span data-stu-id="0a923-113">Labels can be used only on executable statements inside methods.</span></span>

## <a name="to-label-a-line-of-code"></a><span data-ttu-id="0a923-114">為程式程式碼加上標籤</span><span class="sxs-lookup"><span data-stu-id="0a923-114">To label a line of code</span></span>

<span data-ttu-id="0a923-115">將識別碼（後面接著冒號）放在源程式碼的開頭。</span><span class="sxs-lookup"><span data-stu-id="0a923-115">Place an identifier, followed by a colon, at the beginning of the line of source code.</span></span>

<span data-ttu-id="0a923-116">例如，下列幾行程式碼分別標示了 `Jump` 和 `120` ：</span><span class="sxs-lookup"><span data-stu-id="0a923-116">For example, the following lines of code are labeled with `Jump` and `120`, respectively:</span></span>

[!code-vb[VbVbalrStatements#708](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#708)]

## <a name="see-also"></a><span data-ttu-id="0a923-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0a923-117">See also</span></span>

- [<span data-ttu-id="0a923-118">陳述式</span><span class="sxs-lookup"><span data-stu-id="0a923-118">Statements</span></span>](../language-features/statements.md)
- [<span data-ttu-id="0a923-119">Declared Element Names</span><span class="sxs-lookup"><span data-stu-id="0a923-119">Declared Element Names</span></span>](../language-features/declared-elements/declared-element-names.md)
- [<span data-ttu-id="0a923-120">程式結構和程式碼慣例</span><span class="sxs-lookup"><span data-stu-id="0a923-120">Program Structure and Code Conventions</span></span>](program-structure-and-code-conventions.md)
