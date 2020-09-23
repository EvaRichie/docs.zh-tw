---
title: 指定給事件記錄檔的名稱無效
ms.date: 07/20/2015
ms.assetid: b1b158bd-f13f-4371-a8af-31c0e86ae6be
ms.openlocfilehash: 36e2bc91a671a22e808d0e30e292471729b1e50b
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91083874"
---
# <a name="an-invalid-name-was-specified-for-the-event-log"></a><span data-ttu-id="49522-102">指定給事件記錄檔的名稱無效</span><span class="sxs-lookup"><span data-stu-id="49522-102">An invalid name was specified for the event log</span></span>

<span data-ttu-id="49522-103">指定給事件記錄檔的名稱無效。</span><span class="sxs-lookup"><span data-stu-id="49522-103">An invalid name was specified for the event log.</span></span> <span data-ttu-id="49522-104">這通常是名稱中有無效的字元、檔案名稱空白或檔案名稱太長的結果。</span><span class="sxs-lookup"><span data-stu-id="49522-104">Usually this is a result of invalid characters in the name, a blank file name, or a file name that is too long.</span></span>  
  
## <a name="to-correct-this-error"></a><span data-ttu-id="49522-105">更正這個錯誤</span><span class="sxs-lookup"><span data-stu-id="49522-105">To correct this error</span></span>  
  
- <span data-ttu-id="49522-106">如果指定的名稱超過八個字元，請確定該名稱未與其他事件記錄檔的名稱相衝突。</span><span class="sxs-lookup"><span data-stu-id="49522-106">If the specified name is more than eight characters, make sure there is no conflict with the names of other event logs.</span></span> <span data-ttu-id="49522-107">判斷此名稱是否唯一時，只會評估前八個字元。</span><span class="sxs-lookup"><span data-stu-id="49522-107">Only the first eight characters are evaluated when determining if the name is unique.</span></span>  
  
- <span data-ttu-id="49522-108">如果提供路徑，請確定已正確地剖析該路徑。</span><span class="sxs-lookup"><span data-stu-id="49522-108">If supplying a path, make sure it is parsed correctly.</span></span>  
  
- <span data-ttu-id="49522-109">檢查名稱中沒有無效的字元。</span><span class="sxs-lookup"><span data-stu-id="49522-109">Check that there are no invalid characters in the name.</span></span> <span data-ttu-id="49522-110">不能在檔案名稱中使用的字元包括 `<`、 `>`、 `:`、 `"`、 `/`、 `\`和 `|`。</span><span class="sxs-lookup"><span data-stu-id="49522-110">Characters that cannot be used in a file name include `<`, `>`, `:`, `"`, `/`, `\`, and `|`.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="49522-111">另請參閱</span><span class="sxs-lookup"><span data-stu-id="49522-111">See also</span></span>

- [<span data-ttu-id="49522-112">作法：剖析檔案路徑</span><span class="sxs-lookup"><span data-stu-id="49522-112">How to: Parse File Paths</span></span>](../developing-apps/programming/drives-directories-files/how-to-parse-file-paths.md)
- [<span data-ttu-id="49522-113">作法：重新命名檔案</span><span class="sxs-lookup"><span data-stu-id="49522-113">How to: Rename a File</span></span>](../developing-apps/programming/drives-directories-files/how-to-rename-a-file.md)
