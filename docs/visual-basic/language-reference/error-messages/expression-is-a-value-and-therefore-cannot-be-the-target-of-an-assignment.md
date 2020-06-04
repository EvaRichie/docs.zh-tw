---
title: 運算式是一個數值，不可以是指派的目標
ms.date: 07/20/2015
f1_keywords:
- bc30068
- vbc30068
helpviewer_keywords:
- BC30068
ms.assetid: d65141e1-f31e-4ac5-a3b8-0b2e02a71ebf
ms.openlocfilehash: 9e4dbaf2f2800454c673cd58ddec4cf0f6e5c6b9
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84409503"
---
# <a name="expression-is-a-value-and-therefore-cannot-be-the-target-of-an-assignment"></a><span data-ttu-id="2b8b0-102">運算式是一個數值，不可以是指派的目標</span><span class="sxs-lookup"><span data-stu-id="2b8b0-102">Expression is a value and therefore cannot be the target of an assignment</span></span>

<span data-ttu-id="2b8b0-103">語句會嘗試將值指派給運算式。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-103">A statement attempts to assign a value to an expression.</span></span> <span data-ttu-id="2b8b0-104">您只能在執行時間，將值指派給可寫入的變數、屬性或陣列元素。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-104">You can assign a value only to a writable variable, property, or array element at run time.</span></span> <span data-ttu-id="2b8b0-105">下列範例說明此錯誤的發生方式。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-105">The following example illustrates how this error can occur.</span></span>

```vb
Dim yesterday As Integer
ReadOnly maximum As Integer = 45
yesterday + 1 = DatePart(DateInterval.Day, Now)
' The preceding line is an ERROR because of an expression on the left.
maximum = 50
' The preceding line is an ERROR because maximum is declared ReadOnly.
```

<span data-ttu-id="2b8b0-106">類似的範例可能適用于屬性和陣列元素。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-106">Similar examples could apply to properties and array elements.</span></span>

<span data-ttu-id="2b8b0-107">**間接存取。**</span><span class="sxs-lookup"><span data-stu-id="2b8b0-107">**Indirect Access.**</span></span> <span data-ttu-id="2b8b0-108">透過實值型別的間接存取也會產生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-108">Indirect access through a value type can also generate this error.</span></span> <span data-ttu-id="2b8b0-109">請考慮下列程式碼範例，它會嘗試透過間接存取來設定的值 <xref:System.Drawing.Point> <xref:System.Windows.Forms.Control.Location%2A> 。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-109">Consider the following code example, which attempts to set the value of <xref:System.Drawing.Point> by accessing it indirectly through <xref:System.Windows.Forms.Control.Location%2A>.</span></span>

```vb
' Assume this code runs inside Form1.
Dim exitButton As New System.Windows.Forms.Button()
exitButton.Text = "Exit this form"
exitButton.Location.X = 140
' The preceding line is an ERROR because of no storage for Location.
```

<span data-ttu-id="2b8b0-110">前述範例的最後一個語句會失敗，因為它只會針對屬性所傳回的結構建立暫存配置 <xref:System.Drawing.Point> <xref:System.Windows.Forms.Control.Location%2A> 。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-110">The last statement of the preceding example fails because it creates only a temporary allocation for the <xref:System.Drawing.Point> structure returned by the <xref:System.Windows.Forms.Control.Location%2A> property.</span></span> <span data-ttu-id="2b8b0-111">結構是實值型別，而且在執行語句之後，不會保留暫存結構。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-111">A structure is a value type, and the temporary structure is not retained after the statement runs.</span></span> <span data-ttu-id="2b8b0-112">此問題的解決方式是宣告和使用的變數 <xref:System.Windows.Forms.Control.Location%2A> ，這會為結構建立更永久的配置 <xref:System.Drawing.Point> 。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-112">The problem is resolved by declaring and using a variable for <xref:System.Windows.Forms.Control.Location%2A>, which creates a more permanent allocation for the <xref:System.Drawing.Point> structure.</span></span> <span data-ttu-id="2b8b0-113">下列範例顯示的程式碼可以取代先前範例中的最後一個語句。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-113">The following example shows code that can replace the last statement of the preceding example.</span></span>

```vb
Dim exitLocation as New System.Drawing.Point(140, exitButton.Location.Y)
exitButton.Location = exitLocation
```

<span data-ttu-id="2b8b0-114">**錯誤識別碼：** BC30068</span><span class="sxs-lookup"><span data-stu-id="2b8b0-114">**Error ID:** BC30068</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="2b8b0-115">更正這個錯誤</span><span class="sxs-lookup"><span data-stu-id="2b8b0-115">To correct this error</span></span>

- <span data-ttu-id="2b8b0-116">如果語句將值指派給運算式，請將運算式取代為單一可寫入的變數、屬性或陣列元素。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-116">If the statement assigns a value to an expression, replace the expression with a single writable variable, property, or array element.</span></span>

- <span data-ttu-id="2b8b0-117">如果語句透過實值型別（通常是結構）進行間接存取，請建立變數來保存實值型別。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-117">If the statement makes indirect access through a value type (usually a structure), create a variable to hold the value type.</span></span>

- <span data-ttu-id="2b8b0-118">將適當的結構（或其他實數值型別）指派給變數。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-118">Assign the appropriate structure (or other value type) to the variable.</span></span>

- <span data-ttu-id="2b8b0-119">使用變數來存取屬性，以將值指派給它。</span><span class="sxs-lookup"><span data-stu-id="2b8b0-119">Use the variable to access the property to assign it a value.</span></span>

## <a name="see-also"></a><span data-ttu-id="2b8b0-120">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2b8b0-120">See also</span></span>

- [<span data-ttu-id="2b8b0-121">運算子和運算式</span><span class="sxs-lookup"><span data-stu-id="2b8b0-121">Operators and Expressions</span></span>](../../programming-guide/language-features/operators-and-expressions/index.md)
- [<span data-ttu-id="2b8b0-122">陳述式</span><span class="sxs-lookup"><span data-stu-id="2b8b0-122">Statements</span></span>](../../programming-guide/language-features/statements.md)
- [<span data-ttu-id="2b8b0-123">程序的疑難排解</span><span class="sxs-lookup"><span data-stu-id="2b8b0-123">Troubleshooting Procedures</span></span>](../../programming-guide/language-features/procedures/troubleshooting-procedures.md)
