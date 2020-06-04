---
title: 作法：建立目錄
ms.date: 07/20/2015
helpviewer_keywords:
- directories [Visual Basic], creating
- folders [Visual Basic], creating
ms.assetid: 0351a2ca-24d8-43b5-bb39-9b99e6401cff
ms.openlocfilehash: 0da915054a2e38c778f15bc0b472fe9b02521189
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401663"
---
# <a name="how-to-create-a-directory-in-visual-basic"></a><span data-ttu-id="9d31c-102">如何：在 Visual Basic 中建立目錄</span><span class="sxs-lookup"><span data-stu-id="9d31c-102">How to: Create a Directory in Visual Basic</span></span>

<span data-ttu-id="9d31c-103">使用 `My.Computer.FileSystem` 物件的 `CreateDirectory` 方法來建立目錄。</span><span class="sxs-lookup"><span data-stu-id="9d31c-103">Use the `CreateDirectory` method of the `My.Computer.FileSystem` object to create directories.</span></span>  
  
 <span data-ttu-id="9d31c-104">如果目錄已經存在，則不會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="9d31c-104">If the directory already exists, no exception is thrown.</span></span>  
  
### <a name="to-create-a-directory"></a><span data-ttu-id="9d31c-105">建立目錄</span><span class="sxs-lookup"><span data-stu-id="9d31c-105">To create a directory</span></span>  
  
- <span data-ttu-id="9d31c-106">指定應該建立目錄之位置的完整路徑，以使用 `CreateDirectory` 方法。</span><span class="sxs-lookup"><span data-stu-id="9d31c-106">Use the `CreateDirectory` method by specifying the full path of the location where the directory should be created.</span></span> <span data-ttu-id="9d31c-107">這個範例會在 `C:\Documents and Settings\All Users\Documents` 中建立 `NewDirectory` 目錄。</span><span class="sxs-lookup"><span data-stu-id="9d31c-107">This example creates the directory `NewDirectory` in `C:\Documents and Settings\All Users\Documents`.</span></span>  
  
     [!code-vb[VbVbcnMyFileSystem#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#2)]  
  
## <a name="robust-programming"></a><span data-ttu-id="9d31c-108">穩固程式設計</span><span class="sxs-lookup"><span data-stu-id="9d31c-108">Robust Programming</span></span>  

 <span data-ttu-id="9d31c-109">以下條件可能會造成例外狀況：</span><span class="sxs-lookup"><span data-stu-id="9d31c-109">The following conditions may cause an exception:</span></span>  
  
- <span data-ttu-id="9d31c-110">目錄名稱的格式不正確。</span><span class="sxs-lookup"><span data-stu-id="9d31c-110">The directory name is malformed.</span></span> <span data-ttu-id="9d31c-111">例如，它包含不合法的字元，或只有空白字元 (<xref:System.ArgumentException>)。</span><span class="sxs-lookup"><span data-stu-id="9d31c-111">For example, it contains illegal characters or is only white space (<xref:System.ArgumentException>).</span></span>  
  
- <span data-ttu-id="9d31c-112">要建立之目錄的父目錄為唯讀 (<xref:System.IO.IOException>)。</span><span class="sxs-lookup"><span data-stu-id="9d31c-112">The parent directory of the directory to be created is read-only (<xref:System.IO.IOException>).</span></span>  
  
- <span data-ttu-id="9d31c-113">目錄名稱為 `Nothing` (<xref:System.ArgumentNullException>)。</span><span class="sxs-lookup"><span data-stu-id="9d31c-113">The directory name is `Nothing` (<xref:System.ArgumentNullException>).</span></span>  
  
- <span data-ttu-id="9d31c-114">目錄名稱太長 (<xref:System.IO.PathTooLongException>)。</span><span class="sxs-lookup"><span data-stu-id="9d31c-114">The directory name is too long (<xref:System.IO.PathTooLongException>).</span></span>  
  
- <span data-ttu-id="9d31c-115">目錄名稱為冒號 ":" (<xref:System.NotSupportedException>)。</span><span class="sxs-lookup"><span data-stu-id="9d31c-115">The directory name is a colon ":" (<xref:System.NotSupportedException>).</span></span>  
  
- <span data-ttu-id="9d31c-116">使用者沒有權限，無法建立目錄 (<xref:System.UnauthorizedAccessException>)。</span><span class="sxs-lookup"><span data-stu-id="9d31c-116">The user does not have permission to create the directory (<xref:System.UnauthorizedAccessException>).</span></span>  
  
- <span data-ttu-id="9d31c-117">使用者在部分信任狀況下的權限不足 (<xref:System.Security.SecurityException>)。</span><span class="sxs-lookup"><span data-stu-id="9d31c-117">The user lacks permissions in a partial-trust situation (<xref:System.Security.SecurityException>).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="9d31c-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9d31c-118">See also</span></span>

- <xref:Microsoft.VisualBasic.FileIO.FileSystem.CreateDirectory%2A>
- [<span data-ttu-id="9d31c-119">建立、刪除和移動檔案和目錄</span><span class="sxs-lookup"><span data-stu-id="9d31c-119">Creating, Deleting, and Moving Files and Directories</span></span>](creating-deleting-and-moving-files-and-directories.md)
