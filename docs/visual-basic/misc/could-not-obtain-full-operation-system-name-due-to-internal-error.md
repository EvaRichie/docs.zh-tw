---
title: 由於內部錯誤，無法取得完整作業系統名稱
ms.date: 07/20/2015
f1_keywords:
- vbrDiagnosticInfo_FullOSName
ms.assetid: f69da02b-eb9a-4284-bb9e-3025517ae6c1
ms.openlocfilehash: 67e8fb5e906800d28bf15714463b7ff6ae585693
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84402274"
---
# <a name="could-not-obtain-full-operation-system-name-due-to-internal-error"></a><span data-ttu-id="35afb-102">由於內部錯誤，無法取得完整作業系統名稱</span><span class="sxs-lookup"><span data-stu-id="35afb-102">Could not obtain full operation system name due to internal error</span></span>
<span data-ttu-id="35afb-103">由於內部錯誤，無法取得完整作業系統名稱。</span><span class="sxs-lookup"><span data-stu-id="35afb-103">Could not obtain full operation system name due to internal error.</span></span> <span data-ttu-id="35afb-104">這可能是因為目前電腦上沒有 WMI 存在所造成。</span><span class="sxs-lookup"><span data-stu-id="35afb-104">This might be caused by WMI not existing on the current machine.</span></span>  
  
 <span data-ttu-id="35afb-105">呼叫 `My.Computer.Info.OSFullName` 屬性失敗。</span><span class="sxs-lookup"><span data-stu-id="35afb-105">A call to the `My.Computer.Info.OSFullName` property failed.</span></span> <span data-ttu-id="35afb-106">如果目前電腦上未安裝 Windows Management Instrumentation (WMI)，就可能會發生這項失敗。</span><span class="sxs-lookup"><span data-stu-id="35afb-106">A possible cause for this failure is if Windows Management Instrumentation (WMI) is not installed on the current computer.</span></span>  
  
## <a name="to-correct-this-error"></a><span data-ttu-id="35afb-107">更正這個錯誤</span><span class="sxs-lookup"><span data-stu-id="35afb-107">To correct this error</span></span>  
  
1. <span data-ttu-id="35afb-108">將包圍呼叫的 `Try...Catch` 區塊加入 `My.Computer.Info.OSFullName` 屬性中。</span><span class="sxs-lookup"><span data-stu-id="35afb-108">Add a `Try...Catch` block around the call to the `My.Computer.Info.OSFullName` property.</span></span>  
  
2. <span data-ttu-id="35afb-109">如需 WMI 及其安裝方式的詳細資訊，請移至並搜尋「Windows Management Instrumentation 核心」。</span><span class="sxs-lookup"><span data-stu-id="35afb-109">For more information about WMI and how to install it, go to  and search for "Windows Management Instrumentation Core".</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="35afb-110">另請參閱</span><span class="sxs-lookup"><span data-stu-id="35afb-110">See also</span></span>

- [<span data-ttu-id="35afb-111">我的 OSFullName</span><span class="sxs-lookup"><span data-stu-id="35afb-111">My.Computer.Info.OSFullName</span></span>](xref:Microsoft.VisualBasic.Devices.ComputerInfo.OSFullName)
- [<span data-ttu-id="35afb-112">在 .NET 中處理和擲回例外狀況</span><span class="sxs-lookup"><span data-stu-id="35afb-112">Handling and throwing exceptions in .NET</span></span>](../../standard/exceptions/index.md)
- [<span data-ttu-id="35afb-113">Try...Catch...Finally 陳述式</span><span class="sxs-lookup"><span data-stu-id="35afb-113">Try...Catch...Finally Statement</span></span>](../language-reference/statements/try-catch-finally-statement.md)
