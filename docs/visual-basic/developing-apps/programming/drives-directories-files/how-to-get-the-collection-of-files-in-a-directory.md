---
title: 作法：取得目錄中的檔案集合
ms.date: 07/20/2015
helpviewer_keywords:
- folders, working with
- files [Visual Basic], accessing
ms.assetid: 6c8ba7e8-dd37-4853-92bf-762b67c98160
ms.openlocfilehash: 055151d4b3e3aba6be9b9b03ac9abffc6eb7b734
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401611"
---
# <a name="how-to-get-the-collection-of-files-in-a-directory-in-visual-basic"></a><span data-ttu-id="52a79-102">如何：在 Visual Basic 中取得目錄的檔案集合</span><span class="sxs-lookup"><span data-stu-id="52a79-102">How to: Get the Collection of Files in a Directory in Visual Basic</span></span>

<span data-ttu-id="52a79-103"><xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFiles%2A?displayProperty=nameWithType> 方法的多載會傳回唯讀的字串集合，代表了目錄內的檔案名稱：</span><span class="sxs-lookup"><span data-stu-id="52a79-103">The overloads of the <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFiles%2A?displayProperty=nameWithType> method return a read-only collection of strings representing the names of the files within a directory:</span></span>  
  
- <span data-ttu-id="52a79-104">使用 <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFiles%28System.String%29> 多載在指定目錄中進行簡單的檔案搜尋，而不搜尋子目錄。</span><span class="sxs-lookup"><span data-stu-id="52a79-104">Use the <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFiles%28System.String%29> overload for a simple file search in a specified directory, without searching subdirectories.</span></span>  
  
- <span data-ttu-id="52a79-105">使用 <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFiles(System.String,Microsoft.VisualBasic.FileIO.SearchOption,System.String[])> 多載指定搜尋的其他選項。</span><span class="sxs-lookup"><span data-stu-id="52a79-105">Use the <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFiles(System.String,Microsoft.VisualBasic.FileIO.SearchOption,System.String[])> overload to specify additional options for your search.</span></span> <span data-ttu-id="52a79-106">您可以使用 `wildCards` 參數，指定搜尋模式。</span><span class="sxs-lookup"><span data-stu-id="52a79-106">You can use the `wildCards` parameter to specify a search pattern.</span></span> <span data-ttu-id="52a79-107">若要在搜尋中包含子目錄，請將 `searchType` 參數設成 <xref:Microsoft.VisualBasic.FileIO.SearchOption.SearchAllSubDirectories?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="52a79-107">To include subdirectories in the search, set the `searchType` parameter to <xref:Microsoft.VisualBasic.FileIO.SearchOption.SearchAllSubDirectories?displayProperty=nameWithType>.</span></span>  
  
 <span data-ttu-id="52a79-108">如果找不到符合指定模式的檔案，會傳回空的集合。</span><span class="sxs-lookup"><span data-stu-id="52a79-108">An empty collection is returned if no files matching the specified pattern are found.</span></span>  
  
### <a name="to-list-files-in-a-directory"></a><span data-ttu-id="52a79-109">列出目錄中的檔案</span><span class="sxs-lookup"><span data-stu-id="52a79-109">To list files in a directory</span></span>  
  
- <span data-ttu-id="52a79-110">使用其中一個 <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFiles%2A?displayProperty=nameWithType> 方法多載，並在 `directory` 參數中提供要搜尋的目錄名稱和路徑。</span><span class="sxs-lookup"><span data-stu-id="52a79-110">Use one of the <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFiles%2A?displayProperty=nameWithType> method overloads, supplying the name and path of the directory to search in the `directory` parameter.</span></span> <span data-ttu-id="52a79-111">下列範例會傳回目錄中的所有檔案，並將它們新增到 `ListBox1`。</span><span class="sxs-lookup"><span data-stu-id="52a79-111">The following example returns all files in the directory and adds them to `ListBox1`.</span></span>  
  
     [!code-vb[VbVbcnMyFileSystem#32](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#32)]  
  
## <a name="robust-programming"></a><span data-ttu-id="52a79-112">穩固程式設計</span><span class="sxs-lookup"><span data-stu-id="52a79-112">Robust Programming</span></span>  

 <span data-ttu-id="52a79-113">以下條件可能會造成例外狀況：</span><span class="sxs-lookup"><span data-stu-id="52a79-113">The following conditions may cause an exception:</span></span>  
  
- <span data-ttu-id="52a79-114">因下列其中一項原因而導致路徑無效：它是長度為零的字串、它只包含空白字元、它包含無效的字元，或者它是裝置路徑 (開頭為 \\\\.\\) (<xref:System.ArgumentException>)。</span><span class="sxs-lookup"><span data-stu-id="52a79-114">The path is not valid for one of the following reasons: it is a zero-length string, it contains only white space, it contains invalid characters, or it is a device path (starts with \\\\.\\) (<xref:System.ArgumentException>).</span></span>  
  
- <span data-ttu-id="52a79-115">路徑無效，因為它是 `Nothing` (<xref:System.ArgumentNullException>)。</span><span class="sxs-lookup"><span data-stu-id="52a79-115">The path is not valid because it is `Nothing` (<xref:System.ArgumentNullException>).</span></span>  
  
- <span data-ttu-id="52a79-116">`directory` 不存在 (<xref:System.IO.DirectoryNotFoundException>)。</span><span class="sxs-lookup"><span data-stu-id="52a79-116">`directory` does not exist (<xref:System.IO.DirectoryNotFoundException>).</span></span>  
  
- <span data-ttu-id="52a79-117">`directory` 指向現有檔案 (<xref:System.IO.IOException>)。</span><span class="sxs-lookup"><span data-stu-id="52a79-117">`directory` points to an existing file (<xref:System.IO.IOException>).</span></span>  
  
- <span data-ttu-id="52a79-118">路徑超過系統定義的最大長度 (<xref:System.IO.PathTooLongException>)。</span><span class="sxs-lookup"><span data-stu-id="52a79-118">The path exceeds the system-defined maximum length (<xref:System.IO.PathTooLongException>).</span></span>  
  
- <span data-ttu-id="52a79-119">路徑中的檔案或目錄名稱含有冒號 (:)，或者是無效的格式 (<xref:System.NotSupportedException>)。</span><span class="sxs-lookup"><span data-stu-id="52a79-119">A file or directory name in the path contains a colon (:) or is in an invalid format (<xref:System.NotSupportedException>).</span></span>  
  
- <span data-ttu-id="52a79-120">使用者缺乏必要的使用權限來檢視路徑 (<xref:System.Security.SecurityException>)。</span><span class="sxs-lookup"><span data-stu-id="52a79-120">The user lacks necessary permissions to view the path (<xref:System.Security.SecurityException>).</span></span>  
  
- <span data-ttu-id="52a79-121">使用者缺乏必要的權限 (<xref:System.UnauthorizedAccessException>)。</span><span class="sxs-lookup"><span data-stu-id="52a79-121">The user lacks necessary permissions (<xref:System.UnauthorizedAccessException>).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="52a79-122">另請參閱</span><span class="sxs-lookup"><span data-stu-id="52a79-122">See also</span></span>

- <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFiles%2A>
- [<span data-ttu-id="52a79-123">作法：尋找具有特定模式的檔案</span><span class="sxs-lookup"><span data-stu-id="52a79-123">How to: Find Files with a Specific Pattern</span></span>](how-to-find-files-with-a-specific-pattern.md)
- [<span data-ttu-id="52a79-124">作法：尋找具有特定模式的子目錄</span><span class="sxs-lookup"><span data-stu-id="52a79-124">How to: Find Subdirectories with a Specific Pattern</span></span>](how-to-find-subdirectories-with-a-specific-pattern.md)
