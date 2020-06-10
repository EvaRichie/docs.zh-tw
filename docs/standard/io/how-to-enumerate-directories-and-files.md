---
title: 如何：列舉目錄和檔案
description: 瞭解如何使用可列舉集合來列舉目錄和檔案，以提供比 .NET 中的陣列更好的效能。
ms.date: 12/27/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- I/O [.NET Framework], enumerating directories and files
ms.assetid: 86b69a08-3bfa-4e5f-b4e1-3b7cb8478215
ms.openlocfilehash: 276668f4a3eee89610a81b1256820770d1f72dc3
ms.sourcegitcommit: 7137e12f54c4e83a94ae43ec320f8cf59c1772ea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/10/2020
ms.locfileid: "84662572"
---
# <a name="how-to-enumerate-directories-and-files"></a><span data-ttu-id="50d3d-103">如何：列舉目錄和檔案</span><span class="sxs-lookup"><span data-stu-id="50d3d-103">How to: Enumerate directories and files</span></span>
<span data-ttu-id="50d3d-104">當您使用目錄和檔案的大型集合時，相較於陣列，可列舉的集合會提供更佳的效能。</span><span class="sxs-lookup"><span data-stu-id="50d3d-104">Enumerable collections provide better performance than arrays when you work with large collections of directories and files.</span></span> <span data-ttu-id="50d3d-105">若要列舉目錄和檔案，請使用能夠傳回可列舉目錄或檔案名稱、或是其 <xref:System.IO.DirectoryInfo>、<xref:System.IO.FileInfo> 或 <xref:System.IO.FileSystemInfo> 物件集合的方法。</span><span class="sxs-lookup"><span data-stu-id="50d3d-105">To enumerate directories and files, use methods that return an enumerable collection of directory or file names, or their <xref:System.IO.DirectoryInfo>, <xref:System.IO.FileInfo>, or <xref:System.IO.FileSystemInfo> objects.</span></span>  
  
<span data-ttu-id="50d3d-106">如果您想要搜尋並只傳回目錄或檔案的名稱，請使用 <xref:System.IO.Directory> 類別的列舉方法。</span><span class="sxs-lookup"><span data-stu-id="50d3d-106">If you want to search and return only the names of directories or files, use the enumeration methods of the <xref:System.IO.Directory> class.</span></span> <span data-ttu-id="50d3d-107">如果您想要搜尋並傳回目錄或檔案的其他屬性，請使用 <xref:System.IO.DirectoryInfo> 和 <xref:System.IO.FileSystemInfo> 類別。</span><span class="sxs-lookup"><span data-stu-id="50d3d-107">If you want to search and return other properties of directories or files, use the <xref:System.IO.DirectoryInfo> and <xref:System.IO.FileSystemInfo> classes.</span></span>  
  
<span data-ttu-id="50d3d-108">您可以使用來自這些方法的可列舉集合，作為 <xref:System.Collections.Generic.List%601> 等集合類別建構函式的 <xref:System.Collections.Generic.IEnumerable%601> 參數。</span><span class="sxs-lookup"><span data-stu-id="50d3d-108">You can use enumerable collections from these methods as the <xref:System.Collections.Generic.IEnumerable%601> parameter for constructors of collection classes like <xref:System.Collections.Generic.List%601>.</span></span>  
  
<span data-ttu-id="50d3d-109">下表摘要說明能夠傳回可列舉檔案和目錄集合的方法：</span><span class="sxs-lookup"><span data-stu-id="50d3d-109">The following table summarizes the methods that return enumerable collections of files and directories:</span></span>  
  
|<span data-ttu-id="50d3d-110">搜尋並傳回</span><span class="sxs-lookup"><span data-stu-id="50d3d-110">To search and return</span></span>|<span data-ttu-id="50d3d-111">使用方法</span><span class="sxs-lookup"><span data-stu-id="50d3d-111">Use method</span></span>|  
|------------------|-------------------------------------|-------------------|  
|<span data-ttu-id="50d3d-112">目錄名稱</span><span class="sxs-lookup"><span data-stu-id="50d3d-112">Directory names</span></span>|<xref:System.IO.Directory.EnumerateDirectories%2A?displayProperty=nameWithType>|  
|<span data-ttu-id="50d3d-113">虛擬資訊 (<xref:System.IO.DirectoryInfo>)</span><span class="sxs-lookup"><span data-stu-id="50d3d-113">Directory information (<xref:System.IO.DirectoryInfo>)</span></span>|<xref:System.IO.DirectoryInfo.EnumerateDirectories%2A?displayProperty=nameWithType>|  
|<span data-ttu-id="50d3d-114">檔案名稱</span><span class="sxs-lookup"><span data-stu-id="50d3d-114">File names</span></span>|<xref:System.IO.Directory.EnumerateFiles%2A?displayProperty=nameWithType>|  
|<span data-ttu-id="50d3d-115">檔案資訊 (<xref:System.IO.FileInfo>)</span><span class="sxs-lookup"><span data-stu-id="50d3d-115">File information (<xref:System.IO.FileInfo>)</span></span>|<xref:System.IO.DirectoryInfo.EnumerateFiles%2A?displayProperty=nameWithType>|  
|<span data-ttu-id="50d3d-116">檔案系統項目名稱</span><span class="sxs-lookup"><span data-stu-id="50d3d-116">File system entry names</span></span>|<xref:System.IO.Directory.EnumerateFileSystemEntries%2A?displayProperty=nameWithType>|  
|<span data-ttu-id="50d3d-117">檔案系統項目資訊 (<xref:System.IO.FileSystemInfo>)</span><span class="sxs-lookup"><span data-stu-id="50d3d-117">File system entry information (<xref:System.IO.FileSystemInfo>)</span></span>|<xref:System.IO.DirectoryInfo.EnumerateFileSystemInfos%2A?displayProperty=nameWithType>|  
|<span data-ttu-id="50d3d-118">目錄和檔案名稱</span><span class="sxs-lookup"><span data-stu-id="50d3d-118">Directory and file names</span></span> |<xref:System.IO.Directory.EnumerateFileSystemEntries%2A?displayProperty=nameWithType>|  

> [!NOTE]
> <span data-ttu-id="50d3d-119">雖然您可以使用選擇性 <xref:System.IO.SearchOption> 列舉的 <xref:System.IO.SearchOption.AllDirectories> 選項立即列舉父目錄中子目錄的所有檔案，但 <xref:System.UnauthorizedAccessException> 錯誤可能會使列舉不完整。</span><span class="sxs-lookup"><span data-stu-id="50d3d-119">Although you can immediately enumerate all the files in the subdirectories of a parent directory by using the <xref:System.IO.SearchOption.AllDirectories> option of the optional <xref:System.IO.SearchOption> enumeration, <xref:System.UnauthorizedAccessException> errors may make the enumeration incomplete.</span></span> <span data-ttu-id="50d3d-120">您可以先列舉目錄再列舉檔案來攔截這些例外狀況。</span><span class="sxs-lookup"><span data-stu-id="50d3d-120">You can catch these exceptions by first enumerating directories and then enumerating files.</span></span>  
  
## <a name="examples-use-the-directory-class"></a><span data-ttu-id="50d3d-121">範例：使用 Directory 類別</span><span class="sxs-lookup"><span data-stu-id="50d3d-121">Examples: Use the Directory class</span></span>  
  
<span data-ttu-id="50d3d-122">下列範例使用 <xref:System.IO.Directory.EnumerateDirectories%28System.String%29?displayProperty=nameWithType> 方法，在所指定路徑中取得最上層目錄名稱的清單。</span><span class="sxs-lookup"><span data-stu-id="50d3d-122">The following example uses the <xref:System.IO.Directory.EnumerateDirectories%28System.String%29?displayProperty=nameWithType> method to get a list of the top-level directory names in a specified path.</span></span>  

[!code-csharp[System.IO.EnumDirs1#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.enumdirs1/cs/program.cs#1)]
[!code-vb[System.IO.EnumDirs1#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.enumdirs1/vb/program.vb#1)]  

<span data-ttu-id="50d3d-123">下列範例使用 <xref:System.IO.Directory.EnumerateFiles%28System.String%2CSystem.String%2CSystem.IO.SearchOption%29?displayProperty=nameWithType> 方法，以遞迴方式列舉目錄和子目錄中符合特定模式的所有檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="50d3d-123">The following example uses the <xref:System.IO.Directory.EnumerateFiles%28System.String%2CSystem.String%2CSystem.IO.SearchOption%29?displayProperty=nameWithType> method to recursively enumerate all file names in a directory and subdirectories that match a certain pattern.</span></span> <span data-ttu-id="50d3d-124">然後，它會讀取每個檔案的每一行，並顯示包含指定字串的行，以及其檔名和路徑。</span><span class="sxs-lookup"><span data-stu-id="50d3d-124">It then reads each line of each file and displays the lines that contain a specified string, with their filenames and paths.</span></span>

[!code-csharp[System.IO.Directory.EnumerateFiles#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.directory.enumeratefiles/cs/program.cs#1)]
[!code-vb[System.IO.Directory.EnumerateFiles#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.directory.enumeratefiles/vb/program.vb#1)]  
  
## <a name="examples-use-the-directoryinfo-class"></a><span data-ttu-id="50d3d-125">範例：使用 DirectoryInfo 類別</span><span class="sxs-lookup"><span data-stu-id="50d3d-125">Examples: Use the DirectoryInfo class</span></span>  
  
<span data-ttu-id="50d3d-126">下列範例使用 <xref:System.IO.DirectoryInfo.EnumerateDirectories%2A?displayProperty=nameWithType> 方法，列出其 <xref:System.IO.FileSystemInfo.CreationTimeUtc> 早於特定 <xref:System.DateTime> 值的最上層目錄集合。</span><span class="sxs-lookup"><span data-stu-id="50d3d-126">The following example uses the <xref:System.IO.DirectoryInfo.EnumerateDirectories%2A?displayProperty=nameWithType> method to list a collection of top-level directories whose <xref:System.IO.FileSystemInfo.CreationTimeUtc> is earlier than a certain <xref:System.DateTime> value.</span></span>  

[!code-csharp[System.IO.DirectoryInfo.EnumDirs#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.directoryinfo.enumdirs/cs/program.cs)]
[!code-vb[System.IO.DirectoryInfo.EnumDirs#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.directoryinfo.enumdirs/vb/module1.vb)]  
  
<span data-ttu-id="50d3d-127">下列範例使用 <xref:System.IO.DirectoryInfo.EnumerateFiles%2A?displayProperty=nameWithType> 方法，列出其 <xref:System.IO.FileInfo.Length> 超過 10 MB 的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="50d3d-127">The following example uses the <xref:System.IO.DirectoryInfo.EnumerateFiles%2A?displayProperty=nameWithType> method to list all files whose <xref:System.IO.FileInfo.Length> exceeds 10MB.</span></span> <span data-ttu-id="50d3d-128">此範例會先列舉最上層目錄來攔截可能未經授權的存取例外狀況，再列舉檔案。</span><span class="sxs-lookup"><span data-stu-id="50d3d-128">This example first enumerates the top-level directories, to catch possible unauthorized access exceptions, and then enumerates the files.</span></span>  

[!code-csharp[System.IO.DirectoryInfo.EnumerateDirectories#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.directoryinfo.enumeratedirectories/cs/program.cs#1)]
[!code-vb[System.IO.DirectoryInfo.EnumerateDirectories#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.directoryinfo.enumeratedirectories/vb/program.vb#1)]  
  
## <a name="see-also"></a><span data-ttu-id="50d3d-129">另請參閱</span><span class="sxs-lookup"><span data-stu-id="50d3d-129">See also</span></span>

- [<span data-ttu-id="50d3d-130">檔案和資料流 I/O</span><span class="sxs-lookup"><span data-stu-id="50d3d-130">File and stream I/O</span></span>](index.md)
