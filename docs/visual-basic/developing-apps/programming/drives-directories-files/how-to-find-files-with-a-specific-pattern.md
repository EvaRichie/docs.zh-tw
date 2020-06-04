---
title: 作法：尋找具有特定模式的檔案
ms.date: 07/20/2015
helpviewer_keywords:
- files [Visual Basic], finding
- pattern matching
- patterns, matching
ms.assetid: 25e3b71d-b844-4293-9e4e-f06c5836b5cc
ms.openlocfilehash: 71073672ed14cb2d5df5b5365266b718c59cb18f
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401637"
---
# <a name="how-to-find-files-with-a-specific-pattern-in-visual-basic"></a><span data-ttu-id="a0f24-102">如何：在 Visual Basic 中尋找具有特定模式的檔案</span><span class="sxs-lookup"><span data-stu-id="a0f24-102">How to: Find Files with a Specific Pattern in Visual Basic</span></span>

<span data-ttu-id="a0f24-103"><xref:Microsoft.VisualBasic.MyServices.FileSystemProxy.GetFiles%2A> 方法會傳回代表檔案路徑名稱的唯讀字串集合。</span><span class="sxs-lookup"><span data-stu-id="a0f24-103">The <xref:Microsoft.VisualBasic.MyServices.FileSystemProxy.GetFiles%2A> method returns a read-only collection of strings representing the path names for the files.</span></span> <span data-ttu-id="a0f24-104">您可以使用 `wildCards` 參數指定特定模式。</span><span class="sxs-lookup"><span data-stu-id="a0f24-104">You can use the `wildCards` parameter to specify a specific pattern.</span></span> <span data-ttu-id="a0f24-105">如果您想要在搜尋中包含子目錄，請將 `searchType` 參數設定為 `SearchOption.SearchAllSubDirectories`。</span><span class="sxs-lookup"><span data-stu-id="a0f24-105">If you would like to include subdirectories in the search, set the `searchType` parameter to `SearchOption.SearchAllSubDirectories`.</span></span>  
  
 <span data-ttu-id="a0f24-106">如果找不到符合指定模式的檔案，會傳回空的集合。</span><span class="sxs-lookup"><span data-stu-id="a0f24-106">An empty collection is returned if no files matching the specified pattern are found.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="a0f24-107">如需使用 `System.IO` 命名空間的 `DirectoryInfo` 類別來傳回檔案清單的資訊，請參閱 <xref:System.IO.DirectoryInfo.GetFiles%2A>。</span><span class="sxs-lookup"><span data-stu-id="a0f24-107">For information about returning a file list by using the `DirectoryInfo` class of the `System.IO` namespace, see <xref:System.IO.DirectoryInfo.GetFiles%2A>.</span></span>  
  
### <a name="to-find-files-with-a-specified-pattern"></a><span data-ttu-id="a0f24-108">尋找具有所指定模式的檔案</span><span class="sxs-lookup"><span data-stu-id="a0f24-108">To find files with a specified pattern</span></span>  
  
- <span data-ttu-id="a0f24-109">使用 `GetFiles` 方法，並提供您想要搜尋之目錄的名稱和路徑，並指定模式。</span><span class="sxs-lookup"><span data-stu-id="a0f24-109">Use the `GetFiles` method, supplying the name and path of the directory you want to search and specifying the pattern.</span></span> <span data-ttu-id="a0f24-110">下列範例會傳回目錄中副檔名為 `.dll` 的所有檔案，並將它們新增到 `ListBox1`。</span><span class="sxs-lookup"><span data-stu-id="a0f24-110">The following example returns all files with the extension `.dll` in the directory and adds them to `ListBox1`.</span></span>  
  
     [!code-vb[VbFileIOMisc#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIOMisc/VB/Class1.vb#4)]  
  
## <a name="net-framework-security"></a><span data-ttu-id="a0f24-111">.NET Framework 安全性</span><span class="sxs-lookup"><span data-stu-id="a0f24-111">.NET Framework Security</span></span>  

 <span data-ttu-id="a0f24-112">以下條件可能會造成例外狀況：</span><span class="sxs-lookup"><span data-stu-id="a0f24-112">The following conditions may cause an exception:</span></span>  
  
- <span data-ttu-id="a0f24-113">因下列其中一項原因而導致路徑無效：它是長度為零的字串、它只包含空白字元、它包含無效的字元，或者它是裝置路徑 (開頭為 \\\\.\\) (<xref:System.ArgumentException>)。</span><span class="sxs-lookup"><span data-stu-id="a0f24-113">The path is not valid for one of the following reasons: it is a zero-length string, it contains only white space, it contains invalid characters, or it is a device path (starts with \\\\.\\) (<xref:System.ArgumentException>).</span></span>  
  
- <span data-ttu-id="a0f24-114">路徑無效，因為它是 `Nothing` (<xref:System.ArgumentNullException>)。</span><span class="sxs-lookup"><span data-stu-id="a0f24-114">The path is not valid because it is `Nothing` (<xref:System.ArgumentNullException>).</span></span>  
  
- <span data-ttu-id="a0f24-115">`directory` 不存在 (<xref:System.IO.DirectoryNotFoundException>)。</span><span class="sxs-lookup"><span data-stu-id="a0f24-115">`directory` does not exist (<xref:System.IO.DirectoryNotFoundException>).</span></span>  
  
- <span data-ttu-id="a0f24-116">`directory` 指向現有檔案 (<xref:System.IO.IOException>)。</span><span class="sxs-lookup"><span data-stu-id="a0f24-116">`directory` points to an existing file (<xref:System.IO.IOException>).</span></span>  
  
- <span data-ttu-id="a0f24-117">路徑超過系統定義的最大長度 (<xref:System.IO.PathTooLongException>)。</span><span class="sxs-lookup"><span data-stu-id="a0f24-117">The path exceeds the system-defined maximum length (<xref:System.IO.PathTooLongException>).</span></span>  
  
- <span data-ttu-id="a0f24-118">路徑中的檔案或資料夾名稱包含冒號 (:)，或者是無效的格式 (<xref:System.NotSupportedException>)。</span><span class="sxs-lookup"><span data-stu-id="a0f24-118">A file or folder name in the path contains a colon (:) or is in an invalid format (<xref:System.NotSupportedException>).</span></span>  
  
- <span data-ttu-id="a0f24-119">使用者缺乏必要的使用權限來檢視路徑 (<xref:System.Security.SecurityException>)。</span><span class="sxs-lookup"><span data-stu-id="a0f24-119">The user lacks necessary permissions to view the path (<xref:System.Security.SecurityException>).</span></span>  
  
- <span data-ttu-id="a0f24-120">使用者缺乏必要的權限 (<xref:System.UnauthorizedAccessException>)。</span><span class="sxs-lookup"><span data-stu-id="a0f24-120">The user lacks necessary permissions (<xref:System.UnauthorizedAccessException>).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a0f24-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a0f24-121">See also</span></span>

- <xref:Microsoft.VisualBasic.MyServices.FileSystemProxy.GetFiles%2A>
- [<span data-ttu-id="a0f24-122">作法：尋找具有特定模式的子目錄</span><span class="sxs-lookup"><span data-stu-id="a0f24-122">How to: Find Subdirectories with a Specific Pattern</span></span>](how-to-find-subdirectories-with-a-specific-pattern.md)
- [<span data-ttu-id="a0f24-123">疑難排解：讀取和寫入文字檔</span><span class="sxs-lookup"><span data-stu-id="a0f24-123">Troubleshooting: Reading from and Writing to Text Files</span></span>](troubleshooting-reading-from-and-writing-to-text-files.md)
- [<span data-ttu-id="a0f24-124">作法：取得目錄中的檔案集合</span><span class="sxs-lookup"><span data-stu-id="a0f24-124">How to: Get the Collection of Files in a Directory</span></span>](how-to-get-the-collection-of-files-in-a-directory.md)
