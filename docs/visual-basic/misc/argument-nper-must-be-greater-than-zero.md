---
title: 引數 'NPer' 必須大於零
ms.date: 07/20/2015
f1_keywords:
- vbrRate_NPerMustBeGTZero
ms.assetid: d49242df-dbd1-4b26-bd8c-ed56d24fdfcd
ms.openlocfilehash: f0185e30cb711472105955f5febf8d7702b29c72
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91087137"
---
# <a name="argument-nper-must-be-greater-than-zero"></a><span data-ttu-id="1480f-102">引數 'NPer' 必須大於零</span><span class="sxs-lookup"><span data-stu-id="1480f-102">Argument 'NPer' must be greater than zero</span></span>

<span data-ttu-id="1480f-103">`NPer` 函式會傳回 `Double` 指定根據定期支付和固定利率的年金期數，它需要大於零的引數。</span><span class="sxs-lookup"><span data-stu-id="1480f-103">The `NPer` function, which returns a `Double` specifying the number of periods for an annuity based on periodic fixed payments and a fixed interest rate, requires an argument greater than zero.</span></span>  
  
## <a name="to-correct-this-error"></a><span data-ttu-id="1480f-104">更正這個錯誤</span><span class="sxs-lookup"><span data-stu-id="1480f-104">To correct this error</span></span>  
  
- <span data-ttu-id="1480f-105">請檢查運算式中的引數拼法。</span><span class="sxs-lookup"><span data-stu-id="1480f-105">Check the spelling of arguments in the expression.</span></span> <span data-ttu-id="1480f-106">拼錯的變數名稱可能會隱含地建立初始化為零的數值變數。</span><span class="sxs-lookup"><span data-stu-id="1480f-106">A misspelled variable name can implicitly create a numeric variable that is initialized to zero.</span></span>  
  
- <span data-ttu-id="1480f-107">請檢查運算式中先前的變數作業，特別是那些作為引數從其他程序傳遞至程序的變數。</span><span class="sxs-lookup"><span data-stu-id="1480f-107">Check previous operations on variables in the expression, especially those passed into the procedure as arguments from other procedures.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="1480f-108">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1480f-108">See also</span></span>

- [<span data-ttu-id="1480f-109">以傳值和傳址方式傳遞引數</span><span class="sxs-lookup"><span data-stu-id="1480f-109">Passing Arguments by Value and by Reference</span></span>](../programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)
