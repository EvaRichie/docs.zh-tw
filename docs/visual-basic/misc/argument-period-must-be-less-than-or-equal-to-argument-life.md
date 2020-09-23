---
title: 引數 'Period' 必須小於或等於引數 'Life'
ms.date: 07/20/2015
f1_keywords:
- vbrFinancial_PeriodLELife
ms.assetid: dc575d41-b376-4b05-bbbe-6de1e98385f1
ms.openlocfilehash: 844192f1168e6fef7906ffc133dcc3b5ba40b42c
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91087033"
---
# <a name="argument-period-must-be-less-than-or-equal-to-argument-life"></a><span data-ttu-id="66c7f-102">引數 'Period' 必須小於或等於引數 'Life'</span><span class="sxs-lookup"><span data-stu-id="66c7f-102">Argument 'Period' must be less than or equal to argument 'Life'</span></span>

<span data-ttu-id="66c7f-103">`Period` 引數 (指定計算資產折舊期間) 的值大於 `Life` 引數的值。</span><span class="sxs-lookup"><span data-stu-id="66c7f-103">The value of the `Period` argument, which specifies the period for which asset depreciation is calculated, is greater than the value of the `Life` argument.</span></span>  
  
## <a name="to-correct-this-error"></a><span data-ttu-id="66c7f-104">更正這個錯誤</span><span class="sxs-lookup"><span data-stu-id="66c7f-104">To correct this error</span></span>  
  
- <span data-ttu-id="66c7f-105">確定 `Life` 和 `Period` 引數以相同的單位表示。</span><span class="sxs-lookup"><span data-stu-id="66c7f-105">Ensure that the `Life` and `Period` arguments are expressed in the same units.</span></span> <span data-ttu-id="66c7f-106">例如，如果 `Life` 是以月份為測量單位，則 `Period` 應該也是。</span><span class="sxs-lookup"><span data-stu-id="66c7f-106">For example, if `Life` is measured in months, `Period` should be as well.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="66c7f-107">另請參閱</span><span class="sxs-lookup"><span data-stu-id="66c7f-107">See also</span></span>

- [<span data-ttu-id="66c7f-108">以傳值和傳址方式傳遞引數</span><span class="sxs-lookup"><span data-stu-id="66c7f-108">Passing Arguments by Value and by Reference</span></span>](../programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)
