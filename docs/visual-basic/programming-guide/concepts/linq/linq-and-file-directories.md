---
title: LINQ 和檔案目錄
ms.date: 07/20/2015
ms.assetid: 159fd5c3-3926-4071-ae78-d8e423287eb7
ms.openlocfilehash: 9738dc2b07b33b2d96f8134e8418c54aae53e6a1
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397515"
---
# <a name="linq-and-file-directories-visual-basic"></a><span data-ttu-id="e28ca-102">LINQ 與檔案目錄 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="e28ca-102">LINQ and File Directories (Visual Basic)</span></span>
<span data-ttu-id="e28ca-103">許多檔案系統作業基本上就是查詢，因此很適合使用 LINQ 方法。</span><span class="sxs-lookup"><span data-stu-id="e28ca-103">Many file system operations are essentially queries and are therefore well-suited to the LINQ approach.</span></span>  
  
 <span data-ttu-id="e28ca-104">請注意，本節中的查詢不具破壞性。</span><span class="sxs-lookup"><span data-stu-id="e28ca-104">Note that the queries in this section are non-destructive.</span></span> <span data-ttu-id="e28ca-105">這些查詢不會用來變更原始檔案或資料夾的內容。</span><span class="sxs-lookup"><span data-stu-id="e28ca-105">They are not used to change the contents of the original files or folders.</span></span> <span data-ttu-id="e28ca-106">這是依照查詢不應該造成任何副作用的規則。</span><span class="sxs-lookup"><span data-stu-id="e28ca-106">This follows the rule that queries should not cause any side-effects.</span></span> <span data-ttu-id="e28ca-107">一般而言，任何修改來源資料的程式碼 (包括執行 create/update/delete 運算子的查詢)，都應該與單純查詢資料的程式碼分開。</span><span class="sxs-lookup"><span data-stu-id="e28ca-107">In general, any code (including queries that perform create / update / delete operators) that modifies source data should be kept separate from the code that just queries the data.</span></span>  
  
 <span data-ttu-id="e28ca-108">本節包含下列主題：</span><span class="sxs-lookup"><span data-stu-id="e28ca-108">This section contains the following topics:</span></span>  
  
 [<span data-ttu-id="e28ca-109">如何：查詢具有指定之屬性或名稱的檔案（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="e28ca-109">How to: Query for Files with a Specified Attribute or Name (Visual Basic)</span></span>](how-to-query-for-files-with-a-specified-attribute-or-name.md)  
 <span data-ttu-id="e28ca-110">示範如何檢查檔案之 <xref:System.IO.FileInfo> 物件的一或多個屬性來搜尋檔案。</span><span class="sxs-lookup"><span data-stu-id="e28ca-110">Shows how to search for files by examining one or more properties of its <xref:System.IO.FileInfo> object.</span></span>  
  
 [<span data-ttu-id="e28ca-111">如何：依副檔名分組檔案（LINQ）（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="e28ca-111">How to: Group Files by Extension (LINQ) (Visual Basic)</span></span>](how-to-group-files-by-extension-linq.md)  
 <span data-ttu-id="e28ca-112">示範如何依據檔案的副檔名來傳回 <xref:System.IO.FileInfo> 物件的群組。</span><span class="sxs-lookup"><span data-stu-id="e28ca-112">Shows how to return groups of <xref:System.IO.FileInfo> object based on their file name extension.</span></span>  
  
 [<span data-ttu-id="e28ca-113">如何：查詢一組資料夾中的總位元組數（LINQ）（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="e28ca-113">How to: Query for the Total Number of Bytes in a Set of Folders (LINQ) (Visual Basic)</span></span>](how-to-query-for-the-total-number-of-bytes-in-a-set-of-folders.md)  
 <span data-ttu-id="e28ca-114">示範如何傳回指定之樹狀目錄中所有檔案的位元組總數。</span><span class="sxs-lookup"><span data-stu-id="e28ca-114">Shows how to return the total number of bytes in all the files in a specified directory tree.</span></span>  
  
 <span data-ttu-id="e28ca-115">[如何：比較兩個資料夾的內容（LINQ）（Visual Basic）](how-to-compare-the-contents-of-two-folders-linq.md)s</span><span class="sxs-lookup"><span data-stu-id="e28ca-115">[How to: Compare the Contents of Two Folders (LINQ) (Visual Basic)](how-to-compare-the-contents-of-two-folders-linq.md)s</span></span>  
 <span data-ttu-id="e28ca-116">示範如何傳回同時出現在兩個指定資料夾中的所有檔案，以及只出現在其中一個資料夾中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="e28ca-116">Shows how to return all the files that are present in two specified folders, and also all the files that are present in one folder but not the other.</span></span>  
  
 [<span data-ttu-id="e28ca-117">如何：查詢目錄樹狀中的最大檔案 (LINQ) (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="e28ca-117">How to: Query for the Largest File or Files in a Directory Tree (LINQ) (Visual Basic)</span></span>](how-to-query-for-the-largest-file-or-files-in-a-directory-tree.md)  
 <span data-ttu-id="e28ca-118">示範如何傳回樹狀目錄中的最大檔案或最小檔案，或是指定數目的檔案。</span><span class="sxs-lookup"><span data-stu-id="e28ca-118">Shows how to return the largest or smallest file, or a specified number of files, in a directory tree.</span></span>  
  
 [<span data-ttu-id="e28ca-119">如何：查詢目錄樹狀結構中的重複檔案（LINQ）（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="e28ca-119">How to: Query for Duplicate Files in a Directory Tree (LINQ) (Visual Basic)</span></span>](how-to-query-for-duplicate-files-in-a-directory-tree-linq.md)  
 <span data-ttu-id="e28ca-120">示範如何將出現在指定樹狀目錄中多個位置的所有檔案名稱群組在一起。</span><span class="sxs-lookup"><span data-stu-id="e28ca-120">Shows how to group for all file names that occur in more than one location in a specified directory tree.</span></span> <span data-ttu-id="e28ca-121">同時示範如何根據自訂比較子，來執行更複雜的比較。</span><span class="sxs-lookup"><span data-stu-id="e28ca-121">Also shows how to perform more complex comparisons based on a custom comparer.</span></span>  
  
 [<span data-ttu-id="e28ca-122">如何查詢資料夾中的檔案內容（LINQ）（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="e28ca-122">How to query the contents of files in a folder (LINQ) (Visual Basic)</span></span>](how-to-query-the-contents-of-files-in-a-folder-linq.md)  
 <span data-ttu-id="e28ca-123">示範如何逐一查看樹狀目錄中的資料夾、開啟每個檔案，並查詢檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="e28ca-123">Shows how to iterate through folders in a tree, open each file, and query the file's contents.</span></span>  
  
## <a name="comments"></a><span data-ttu-id="e28ca-124">註解</span><span class="sxs-lookup"><span data-stu-id="e28ca-124">Comments</span></span>  
 <span data-ttu-id="e28ca-125">要建立能夠精確代表檔案系統內容，同時又能順利處理例外狀況的資料來源，其實是件複雜的工作。</span><span class="sxs-lookup"><span data-stu-id="e28ca-125">There is some complexity involved in creating a data source that accurately represents the contents of the file system and handles exceptions gracefully.</span></span> <span data-ttu-id="e28ca-126">本節中的範例會建立 <xref:System.IO.FileInfo> 物件的快照集合，以代表所指定根資料夾和其所有子資料夾下的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="e28ca-126">The examples in this section create a snapshot collection of <xref:System.IO.FileInfo> objects that represents all the files under a specified root folder and all its subfolders.</span></span> <span data-ttu-id="e28ca-127">從您開始到結束執行查詢的這段期間，每個 <xref:System.IO.FileInfo> 的實際狀態都可能會變更。</span><span class="sxs-lookup"><span data-stu-id="e28ca-127">The actual state of each <xref:System.IO.FileInfo> may change in the time between when you begin and end executing a query.</span></span> <span data-ttu-id="e28ca-128">例如，您可以建立 <xref:System.IO.FileInfo> 物件的清單來用作資料來源。</span><span class="sxs-lookup"><span data-stu-id="e28ca-128">For example, you can create a list of <xref:System.IO.FileInfo> objects to use as a data source.</span></span> <span data-ttu-id="e28ca-129">如果您嘗試在查詢中存取 `Length` 屬性，<xref:System.IO.FileInfo> 物件會嘗試存取檔案系統以更新 `Length` 的值。</span><span class="sxs-lookup"><span data-stu-id="e28ca-129">If you try to access the `Length` property in a query, the <xref:System.IO.FileInfo> object will try to access the file system to update the value of `Length`.</span></span> <span data-ttu-id="e28ca-130">如果檔案不再存在，即使您未直接查詢檔案系統，也會在查詢中收到 <xref:System.IO.FileNotFoundException>。</span><span class="sxs-lookup"><span data-stu-id="e28ca-130">If the file no longer exists, you will get a <xref:System.IO.FileNotFoundException> in your query, even though you are not querying the file system directly.</span></span> <span data-ttu-id="e28ca-131">本節中的某些查詢會另外使用一個方法，來解決某些情況下的特定例外狀況。</span><span class="sxs-lookup"><span data-stu-id="e28ca-131">Some queries in this section use a separate method that consumes these particular exceptions in certain cases.</span></span> <span data-ttu-id="e28ca-132">另一個選項是使用 <xref:System.IO.FileSystemWatcher> 持續動態更新資料來源。</span><span class="sxs-lookup"><span data-stu-id="e28ca-132">Another option is to keep your data source updated dynamically by using the <xref:System.IO.FileSystemWatcher>.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e28ca-133">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e28ca-133">See also</span></span>

- [<span data-ttu-id="e28ca-134">LINQ to Objects (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="e28ca-134">LINQ to Objects (Visual Basic)</span></span>](linq-to-objects.md)
