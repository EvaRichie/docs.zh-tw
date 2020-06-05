---
title: Sub 或 Function 未定義
ms.date: 07/20/2015
f1_keywords:
- vbrID35
ms.assetid: 661fdb90-ee7d-40ce-b30b-5e7267bd957a
ms.openlocfilehash: 9eb13d943f9f1cffc984847f7339111e06f5aa6b
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84373923"
---
# <a name="sub-or-function-not-defined-visual-basic"></a><span data-ttu-id="6b4d2-102">Sub 或 Function 未定義 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="6b4d2-102">Sub or Function not defined (Visual Basic)</span></span>
<span data-ttu-id="6b4d2-103">`Sub` `Function` 必須定義或，才能呼叫。</span><span class="sxs-lookup"><span data-stu-id="6b4d2-103">A `Sub` or `Function` must be defined in order to be called.</span></span> <span data-ttu-id="6b4d2-104">可能導致本錯誤的原因包括：</span><span class="sxs-lookup"><span data-stu-id="6b4d2-104">Possible causes of this error include:</span></span>  
  
- <span data-ttu-id="6b4d2-105">程式名稱拼錯。</span><span class="sxs-lookup"><span data-stu-id="6b4d2-105">Misspelling the procedure name.</span></span>  
  
- <span data-ttu-id="6b4d2-106">嘗試從另一個專案呼叫程式，但未在 [**參考**] 對話方塊中明確加入該專案的參考。</span><span class="sxs-lookup"><span data-stu-id="6b4d2-106">Trying to call a procedure from another project without explicitly adding a reference to that project in the **References** dialog box.</span></span>  
  
- <span data-ttu-id="6b4d2-107">指定呼叫程式看不到的程式。</span><span class="sxs-lookup"><span data-stu-id="6b4d2-107">Specifying a procedure that is not visible to the calling procedure.</span></span>  
  
- <span data-ttu-id="6b4d2-108">宣告不在指定之程式庫或程式碼資源中的 Windows 動態連結程式庫（DLL）常式或 Macintosh 程式碼資源常式。</span><span class="sxs-lookup"><span data-stu-id="6b4d2-108">Declaring a Windows dynamic-link library (DLL) routine or Macintosh code-resource routine that is not in the specified library or code resource.</span></span>  
  
## <a name="to-correct-this-error"></a><span data-ttu-id="6b4d2-109">更正這個錯誤</span><span class="sxs-lookup"><span data-stu-id="6b4d2-109">To correct this error</span></span>  
  
1. <span data-ttu-id="6b4d2-110">請確定程式名稱的拼寫正確。</span><span class="sxs-lookup"><span data-stu-id="6b4d2-110">Make sure that the procedure name is spelled correctly.</span></span>  
  
2. <span data-ttu-id="6b4d2-111">在 [**參考**] 對話方塊中，尋找包含您要呼叫之程式的專案名稱。</span><span class="sxs-lookup"><span data-stu-id="6b4d2-111">Find the name of the project containing the procedure you want to call in the **References** dialog box.</span></span> <span data-ttu-id="6b4d2-112">如果沒有出現，請按一下 [**流覽]** 按鈕來搜尋它。</span><span class="sxs-lookup"><span data-stu-id="6b4d2-112">If it does not appear, click the **Browse** button to search for it.</span></span> <span data-ttu-id="6b4d2-113">選取專案名稱左邊的核取方塊，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="6b4d2-113">Select the check box to the left of the project name, and then click **OK**.</span></span>  
  
3. <span data-ttu-id="6b4d2-114">檢查常式的名稱。</span><span class="sxs-lookup"><span data-stu-id="6b4d2-114">Check the name of the routine.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="6b4d2-115">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6b4d2-115">See also</span></span>

- [<span data-ttu-id="6b4d2-116">錯誤類型</span><span class="sxs-lookup"><span data-stu-id="6b4d2-116">Error Types</span></span>](../../programming-guide/language-features/error-types.md)
- [<span data-ttu-id="6b4d2-117">管理專案中的參考</span><span class="sxs-lookup"><span data-stu-id="6b4d2-117">Managing references in a project</span></span>](/visualstudio/ide/managing-references-in-a-project)
- [<span data-ttu-id="6b4d2-118">Sub 陳述式</span><span class="sxs-lookup"><span data-stu-id="6b4d2-118">Sub Statement</span></span>](../statements/sub-statement.md)
- [<span data-ttu-id="6b4d2-119">Function 陳述式</span><span class="sxs-lookup"><span data-stu-id="6b4d2-119">Function Statement</span></span>](../statements/function-statement.md)
