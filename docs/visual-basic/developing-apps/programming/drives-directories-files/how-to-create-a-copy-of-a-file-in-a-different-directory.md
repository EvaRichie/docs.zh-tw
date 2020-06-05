---
title: 作法：在不同目錄中建立檔案複本
ms.date: 07/20/2015
helpviewer_keywords:
- My.Computer.FileSystem.CopyFile method, copying files [Visual Basic]
- files [Visual Basic], copying
- CopyFile method [Visual Basic], copying files in Visual Basic
- I/O [Visual Basic], copying files
ms.assetid: 88e2145c-d414-45a5-ad03-6f5d58ecca26
ms.openlocfilehash: 3b4b41e105d6bb6a17fbb688aa4718b33c23b9d6
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401689"
---
# <a name="how-to-create-a-copy-of-a-file-in-a-different-directory-in-visual-basic"></a><span data-ttu-id="acf78-102">如何：在 Visual Basic 中於不同資料夾內建立檔案複本</span><span class="sxs-lookup"><span data-stu-id="acf78-102">How to: Create a Copy of a File in a Different Directory in Visual Basic</span></span>

<span data-ttu-id="acf78-103">`My.Computer.FileSystem.CopyFile` 方法可讓您複製檔案。</span><span class="sxs-lookup"><span data-stu-id="acf78-103">The `My.Computer.FileSystem.CopyFile` method allows you to copy files.</span></span> <span data-ttu-id="acf78-104">它的參數可以覆寫現有檔案、重新命名檔案、顯示作業進度，並讓使用者取消作業。</span><span class="sxs-lookup"><span data-stu-id="acf78-104">Its parameters provide the ability to overwrite existing files, rename the file, show the progress of the operation, and allow the user to cancel the operation.</span></span>  
  
### <a name="to-copy-a-text-file-to-another-folder"></a><span data-ttu-id="acf78-105">將文字檔複製到另一個資料夾</span><span class="sxs-lookup"><span data-stu-id="acf78-105">To copy a text file to another folder</span></span>  
  
- <span data-ttu-id="acf78-106">使用 `CopyFile` 方法來複製檔案，並指定來源檔案和目標目錄。</span><span class="sxs-lookup"><span data-stu-id="acf78-106">Use the `CopyFile` method to copy a file, specifying a source file and the target directory.</span></span> <span data-ttu-id="acf78-107">`overwrite` 參數可讓您指定是否要覆寫現有檔案。</span><span class="sxs-lookup"><span data-stu-id="acf78-107">The `overwrite` parameter allows you to specify whether or not to overwrite existing files.</span></span> <span data-ttu-id="acf78-108">下列程式碼範例示範如何使用 `CopyFile`。</span><span class="sxs-lookup"><span data-stu-id="acf78-108">The following code examples demonstrate how to use `CopyFile`.</span></span>  
  
     [!code-vb[VbFileIOMisc#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIOMisc/VB/Class1.vb#24)]  
  
## <a name="robust-programming"></a><span data-ttu-id="acf78-109">穩固程式設計</span><span class="sxs-lookup"><span data-stu-id="acf78-109">Robust Programming</span></span>  

 <span data-ttu-id="acf78-110">下列條件可能會造成擲回例外狀況：</span><span class="sxs-lookup"><span data-stu-id="acf78-110">The following conditions may cause an exception to be thrown:</span></span>  
  
- <span data-ttu-id="acf78-111">因下列其中一項原因而導致路徑無效：它是長度為零的字串、它只包含空白字元、它包含無效的字元，或者它是裝置路徑 (開頭為 \\\\.\\) (<xref:System.ArgumentException>)。</span><span class="sxs-lookup"><span data-stu-id="acf78-111">The path is not valid for one of the following reasons: it is a zero-length string, it contains only white space, it contains invalid characters, or it is a device path (starts with \\\\.\\) (<xref:System.ArgumentException>).</span></span>  
  
- <span data-ttu-id="acf78-112">系統無法擷取絕對路徑 (<xref:System.ArgumentException>)。</span><span class="sxs-lookup"><span data-stu-id="acf78-112">The system could not retrieve the absolute path (<xref:System.ArgumentException>).</span></span>  
  
- <span data-ttu-id="acf78-113">路徑無效，因為它是 `Nothing` (<xref:System.ArgumentNullException>)。</span><span class="sxs-lookup"><span data-stu-id="acf78-113">The path is not valid because it is `Nothing` (<xref:System.ArgumentNullException>).</span></span>  
  
- <span data-ttu-id="acf78-114">來源檔案無效或不存在 (<xref:System.IO.FileNotFoundException>)。</span><span class="sxs-lookup"><span data-stu-id="acf78-114">The source file is not valid or does not exist (<xref:System.IO.FileNotFoundException>).</span></span>  
  
- <span data-ttu-id="acf78-115">合併的路徑指向現有目錄 (<xref:System.IO.IOException>)。</span><span class="sxs-lookup"><span data-stu-id="acf78-115">The combined path points to an existing directory (<xref:System.IO.IOException>).</span></span>  
  
- <span data-ttu-id="acf78-116">目的地檔案存在且 `overwrite` 設定為 `False` (<xref:System.IO.IOException>)。</span><span class="sxs-lookup"><span data-stu-id="acf78-116">The destination file exists and `overwrite` is set to `False` (<xref:System.IO.IOException>).</span></span>  
  
- <span data-ttu-id="acf78-117">使用者沒有足夠權限以存取檔案 (<xref:System.IO.IOException>)。</span><span class="sxs-lookup"><span data-stu-id="acf78-117">The user does not have sufficient permissions to access the file (<xref:System.IO.IOException>).</span></span>  
  
- <span data-ttu-id="acf78-118">正在使用目標資枓夾中同名的檔案 (<xref:System.IO.IOException>)。</span><span class="sxs-lookup"><span data-stu-id="acf78-118">A file in the target folder with the same name is in use (<xref:System.IO.IOException>).</span></span>  
  
- <span data-ttu-id="acf78-119">路徑中的檔案或資料夾名稱包含冒號 (:)，或者是無效的格式 (<xref:System.NotSupportedException>)。</span><span class="sxs-lookup"><span data-stu-id="acf78-119">A file or folder name in the path contains a colon (:) or is in an invalid format (<xref:System.NotSupportedException>).</span></span>  
  
- <span data-ttu-id="acf78-120">`ShowUI` 設定為 `True`、`onUserCancel` 設定為 `ThrowException`，而且使用者已取消作業 (<xref:System.OperationCanceledException>)。</span><span class="sxs-lookup"><span data-stu-id="acf78-120">`ShowUI` is set to `True`, `onUserCancel` is set to `ThrowException`, and the user has cancelled the operation (<xref:System.OperationCanceledException>).</span></span>  
  
- <span data-ttu-id="acf78-121">`ShowUI` 設定為 `True`、`onUserCancel` 設定為 `ThrowException`，而且發生未指定的 I/O 錯誤 (<xref:System.OperationCanceledException>)。</span><span class="sxs-lookup"><span data-stu-id="acf78-121">`ShowUI` is set to `True`, `onUserCancel` is set to `ThrowException`, and an unspecified I/O error occurs (<xref:System.OperationCanceledException>).</span></span>  
  
- <span data-ttu-id="acf78-122">路徑超過系統定義的最大長度 (<xref:System.IO.PathTooLongException>)。</span><span class="sxs-lookup"><span data-stu-id="acf78-122">The path exceeds the system-defined maximum length (<xref:System.IO.PathTooLongException>).</span></span>  
  
- <span data-ttu-id="acf78-123">使用者沒有必要的權限 (<xref:System.UnauthorizedAccessException>)。</span><span class="sxs-lookup"><span data-stu-id="acf78-123">The user does not have required permission (<xref:System.UnauthorizedAccessException>).</span></span>  
  
- <span data-ttu-id="acf78-124">使用者缺乏必要的使用權限來檢視路徑 (<xref:System.Security.SecurityException>)。</span><span class="sxs-lookup"><span data-stu-id="acf78-124">The user lacks necessary permissions to view the path (<xref:System.Security.SecurityException>).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="acf78-125">另請參閱</span><span class="sxs-lookup"><span data-stu-id="acf78-125">See also</span></span>

- <xref:Microsoft.VisualBasic.FileIO.FileSystem>
- <xref:Microsoft.VisualBasic.FileIO.FileSystem.CopyFile%2A>
- <xref:Microsoft.VisualBasic.FileIO.UICancelOption>
- [<span data-ttu-id="acf78-126">作法：將具有特定模式的檔案複製到目錄</span><span class="sxs-lookup"><span data-stu-id="acf78-126">How to: Copy Files with a Specific Pattern to a Directory</span></span>](how-to-copy-files-with-a-specific-pattern-to-a-directory.md)
- [<span data-ttu-id="acf78-127">作法：在相同目錄中建立檔案複本</span><span class="sxs-lookup"><span data-stu-id="acf78-127">How to: Create a Copy of a File in the Same Directory</span></span>](how-to-create-a-copy-of-a-file-in-the-same-directory.md)
- [<span data-ttu-id="acf78-128">作法：將目錄複製到另一個目錄</span><span class="sxs-lookup"><span data-stu-id="acf78-128">How to: Copy a Directory to Another Directory</span></span>](how-to-copy-a-directory-to-another-directory.md)
- [<span data-ttu-id="acf78-129">作法：重新命名檔案</span><span class="sxs-lookup"><span data-stu-id="acf78-129">How to: Rename a File</span></span>](how-to-rename-a-file.md)
