---
title: 無法完成作業，因為目標目錄在來源目錄底下
ms.date: 07/20/2015
f1_keywords:
- vbrIO_CyclicOperation
ms.assetid: 850d3a24-5d51-4ac8-a912-630efcd75278
ms.openlocfilehash: d159b9bb3a765a2fefe99fa15dff42e979fda9e3
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91079135"
---
# <a name="could-not-complete-operation-since-target-directory-is-under-source-directory"></a><span data-ttu-id="ea39c-102">無法完成作業，因為目標目錄在來源目錄底下</span><span class="sxs-lookup"><span data-stu-id="ea39c-102">Could not complete operation since target directory is under source directory</span></span>

<span data-ttu-id="ea39c-103">循環作業失敗。</span><span class="sxs-lookup"><span data-stu-id="ea39c-103">A cyclic operation has failed.</span></span> <span data-ttu-id="ea39c-104">循環作業會循環，因此無法完成。</span><span class="sxs-lookup"><span data-stu-id="ea39c-104">Cyclic operations cycle and therefore cannot complete.</span></span> <span data-ttu-id="ea39c-105">例如，物件 A 可能會嘗試繼承自物件 B，而物件 B 又接著繼承自物件 A。</span><span class="sxs-lookup"><span data-stu-id="ea39c-105">For example, Object A may attempt to inherit from Object B, which in turn inherits from Object A.</span></span>  
  
## <a name="to-correct-this-error"></a><span data-ttu-id="ea39c-106">更正這個錯誤</span><span class="sxs-lookup"><span data-stu-id="ea39c-106">To correct this error</span></span>  
  
- <span data-ttu-id="ea39c-107">繼承時，請確定沒有循環參考。</span><span class="sxs-lookup"><span data-stu-id="ea39c-107">When inheriting, make sure that there are no cyclic references.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ea39c-108">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ea39c-108">See also</span></span>

- [<span data-ttu-id="ea39c-109">錯誤類型</span><span class="sxs-lookup"><span data-stu-id="ea39c-109">Error Types</span></span>](../programming-guide/language-features/error-types.md)
- [<span data-ttu-id="ea39c-110">在 Visual Studio 偵錯工具中使用中斷點</span><span class="sxs-lookup"><span data-stu-id="ea39c-110">Use breakpoints in the Visual Studio debugger</span></span>](/visualstudio/debugger/using-breakpoints)
