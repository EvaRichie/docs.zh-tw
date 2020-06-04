---
title: 作法：移動檔案
ms.date: 07/20/2015
helpviewer_keywords:
- files [Visual Basic], moving
ms.assetid: 53a7457b-5815-41ad-b37d-28537c1fb77a
ms.openlocfilehash: 2dafeb3b5f8b8c3a8976b25c1a57f405aebb32b9
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401598"
---
# <a name="how-to-move-a-file-in-visual-basic"></a><span data-ttu-id="1d230-102">如何：在 Visual Basic 中移動檔案</span><span class="sxs-lookup"><span data-stu-id="1d230-102">How to: Move a File in Visual Basic</span></span>

<span data-ttu-id="1d230-103">`My.Computer.FileSystem.MoveFile` 方法可以用來將檔案移至另一個資料夾。</span><span class="sxs-lookup"><span data-stu-id="1d230-103">The `My.Computer.FileSystem.MoveFile` method can be used to move a file to another folder.</span></span> <span data-ttu-id="1d230-104">如果目標結構不存在，則會予以建立。</span><span class="sxs-lookup"><span data-stu-id="1d230-104">If the target structure does not exist, it will be created.</span></span>  
  
### <a name="to-move-a-file"></a><span data-ttu-id="1d230-105">移動檔案</span><span class="sxs-lookup"><span data-stu-id="1d230-105">To move a file</span></span>  
  
- <span data-ttu-id="1d230-106">使用 `MoveFile` 方法移動檔案，並指定來源檔案和目標檔案的檔案名稱和位置。</span><span class="sxs-lookup"><span data-stu-id="1d230-106">Use the `MoveFile` method to move the file, specifying the file name and location for both the source file and the target file.</span></span> <span data-ttu-id="1d230-107">這個範例會將名稱為 `test.txt` 的檔案從 `TestDir1` 移至 `TestDir2`。</span><span class="sxs-lookup"><span data-stu-id="1d230-107">This example moves the file named `test.txt` from `TestDir1` to `TestDir2`.</span></span> <span data-ttu-id="1d230-108">請注意，即使目標檔案名稱與來源檔案名稱相同，還是要指定目標檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="1d230-108">Note that the target file name is specified even though it is the same as the source file name.</span></span>  
  
     [!code-vb[VbVbcnMyFileSystem#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#24)]  
  
### <a name="to-move-a-file-and-rename-it"></a><span data-ttu-id="1d230-109">移動檔案並將它重新命名</span><span class="sxs-lookup"><span data-stu-id="1d230-109">To move a file and rename it</span></span>  
  
- <span data-ttu-id="1d230-110">使用 `MoveFile` 方法移動檔案，並指定來源檔案名稱和位置、目標位置以及目標位置上的新名稱。</span><span class="sxs-lookup"><span data-stu-id="1d230-110">Use the `MoveFile` method to move the file, specifying the source file name and location, the target location, and the new name at the target location.</span></span> <span data-ttu-id="1d230-111">這個範例會將名稱為 `test.txt` 的檔案從 `TestDir1` 移至 `TestDir2` ，並將它重新命名為 `nexttest.txt`。</span><span class="sxs-lookup"><span data-stu-id="1d230-111">This example moves the file named `test.txt` from `TestDir1` to `TestDir2` and renames it `nexttest.txt`.</span></span>  
  
     [!code-vb[VbVbcnMyFileSystem#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#25)]  
  
## <a name="robust-programming"></a><span data-ttu-id="1d230-112">穩固程式設計</span><span class="sxs-lookup"><span data-stu-id="1d230-112">Robust Programming</span></span>  

 <span data-ttu-id="1d230-113">以下條件可能會造成例外狀況：</span><span class="sxs-lookup"><span data-stu-id="1d230-113">The following conditions may cause an exception:</span></span>  
  
- <span data-ttu-id="1d230-114">因下列其中一項原因而導致路徑無效：它是長度為零的字串、它只包含空白字元、它包含無效的字元，或者它是裝置路徑 (開頭為 \\\\.\\) (<xref:System.ArgumentException>)。</span><span class="sxs-lookup"><span data-stu-id="1d230-114">The path is not valid for one of the following reasons: it is a zero-length string, it contains only white space, it contains invalid characters, or it is a device path (starts with \\\\.\\) (<xref:System.ArgumentException>).</span></span>  
  
- <span data-ttu-id="1d230-115">路徑無效，因為它是 `Nothing` (<xref:System.ArgumentNullException>)。</span><span class="sxs-lookup"><span data-stu-id="1d230-115">The path is not valid because it is `Nothing` (<xref:System.ArgumentNullException>).</span></span>  
  
- <span data-ttu-id="1d230-116">`destinationFileName` 為 `Nothing` 或空字串 (<xref:System.ArgumentNullException>)。</span><span class="sxs-lookup"><span data-stu-id="1d230-116">`destinationFileName` is `Nothing` or an empty string (<xref:System.ArgumentNullException>).</span></span>  
  
- <span data-ttu-id="1d230-117">來源檔案無效或不存在 (<xref:System.IO.FileNotFoundException>)。</span><span class="sxs-lookup"><span data-stu-id="1d230-117">The source file is not valid or does not exist (<xref:System.IO.FileNotFoundException>).</span></span>  
  
- <span data-ttu-id="1d230-118">合併的路徑指向現有目錄、目的地檔案已存在，以及 `overwrite` 設為 `False`、正在使用目標目錄中同名的檔案，或使用者的權限不足無法存取檔案 (<xref:System.IO.IOException>)。</span><span class="sxs-lookup"><span data-stu-id="1d230-118">The combined path points to an existing directory, the destination file exists and `overwrite` is set to `False`, a file in the target directory with the same name is in use, or the user does not have sufficient permissions to access the file (<xref:System.IO.IOException>).</span></span>  
  
- <span data-ttu-id="1d230-119">路徑中的檔案或目錄名稱含有冒號 (:)，或者是無效的格式 (<xref:System.NotSupportedException>)。</span><span class="sxs-lookup"><span data-stu-id="1d230-119">A file or directory name in the path contains a colon (:) or is in an invalid format (<xref:System.NotSupportedException>).</span></span>  
  
- <span data-ttu-id="1d230-120">`showUI` 設為 `True`、 `onUserCancel` 設為 `ThrowException`，以及使用者已取消作業，或發生未指定的 I/O 錯誤 (<xref:System.OperationCanceledException>)。</span><span class="sxs-lookup"><span data-stu-id="1d230-120">`showUI` is set to `True`, `onUserCancel` is set to `ThrowException`, and either the user has cancelled the operation or an unspecified I/O error occurs (<xref:System.OperationCanceledException>).</span></span>  
  
- <span data-ttu-id="1d230-121">路徑超過系統定義的最大長度 (<xref:System.IO.PathTooLongException>)。</span><span class="sxs-lookup"><span data-stu-id="1d230-121">The path exceeds the system-defined maximum length (<xref:System.IO.PathTooLongException>).</span></span>  
  
- <span data-ttu-id="1d230-122">使用者缺乏必要的使用權限來檢視路徑 (<xref:System.Security.SecurityException>)。</span><span class="sxs-lookup"><span data-stu-id="1d230-122">The user lacks necessary permissions to view the path (<xref:System.Security.SecurityException>).</span></span>  
  
- <span data-ttu-id="1d230-123">使用者沒有必要的權限 (<xref:System.UnauthorizedAccessException>)。</span><span class="sxs-lookup"><span data-stu-id="1d230-123">The user does not have required permission (<xref:System.UnauthorizedAccessException>).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="1d230-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1d230-124">See also</span></span>

- <xref:Microsoft.VisualBasic.FileIO.FileSystem.MoveFile%2A>
- [<span data-ttu-id="1d230-125">作法：重新命名檔案</span><span class="sxs-lookup"><span data-stu-id="1d230-125">How to: Rename a File</span></span>](how-to-rename-a-file.md)
- [<span data-ttu-id="1d230-126">作法：在不同目錄中建立檔案複本</span><span class="sxs-lookup"><span data-stu-id="1d230-126">How to: Create a Copy of a File in a Different Directory</span></span>](how-to-create-a-copy-of-a-file-in-a-different-directory.md)
- [<span data-ttu-id="1d230-127">作法：剖析檔案路徑</span><span class="sxs-lookup"><span data-stu-id="1d230-127">How to: Parse File Paths</span></span>](how-to-parse-file-paths.md)
