---
title: 只能從不含引數的簡單或限定名稱來推斷範圍變數名稱
ms.date: 07/20/2015
f1_keywords:
- vbc36599
- bc36599
helpviewer_keywords:
- BC36599
ms.assetid: 17763dbe-f74f-4ccb-8086-cb7e45ec4d12
ms.openlocfilehash: 63990b7d37388057ff2cdb430d29878a1c7b39ba
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/17/2020
ms.locfileid: "92162358"
---
# <a name="bc36599-range-variable-name-can-be-inferred-only-from-a-simple-or-qualified-name-with-no-arguments"></a><span data-ttu-id="ce3cb-102">BC36599：只能從簡單或限定名稱（沒有引數）推斷範圍變數名稱</span><span class="sxs-lookup"><span data-stu-id="ce3cb-102">BC36599: Range variable name can be inferred only from a simple or qualified name with no arguments</span></span>

<span data-ttu-id="ce3cb-103">LINQ 查詢中包含接受一或多個引數的程式設計項目。</span><span class="sxs-lookup"><span data-stu-id="ce3cb-103">A programming element that takes one or more arguments is included in a LINQ query.</span></span> <span data-ttu-id="ce3cb-104">編譯器無法從該程式設計項目推斷範圍變數。</span><span class="sxs-lookup"><span data-stu-id="ce3cb-104">The compiler is unable to infer a range variable from that programming element.</span></span>

<span data-ttu-id="ce3cb-105">**錯誤識別碼：** BC36599</span><span class="sxs-lookup"><span data-stu-id="ce3cb-105">**Error ID:** BC36599</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="ce3cb-106">更正這個錯誤</span><span class="sxs-lookup"><span data-stu-id="ce3cb-106">To correct this error</span></span>

<span data-ttu-id="ce3cb-107">提供程式設計項目的明確變數名稱，如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="ce3cb-107">Supply an explicit variable name for the programming element, as shown in the following code:</span></span>

```vb
Dim query = From var1 In collection1
            Select VariableAlias= SampleFunction(var1), var1
```

## <a name="see-also"></a><span data-ttu-id="ce3cb-108">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ce3cb-108">See also</span></span>

- [<span data-ttu-id="ce3cb-109">Visual Basic 中的 LINQ 簡介</span><span class="sxs-lookup"><span data-stu-id="ce3cb-109">Introduction to LINQ in Visual Basic</span></span>](../../programming-guide/language-features/linq/introduction-to-linq.md)
- [<span data-ttu-id="ce3cb-110">Select 子句</span><span class="sxs-lookup"><span data-stu-id="ce3cb-110">Select Clause</span></span>](../queries/select-clause.md)
