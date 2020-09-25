---
title: '如何逐一查看目錄樹狀結構-c # 程式設計指南'
description: 瞭解如何逐一查看目錄樹狀結構。 存取指定根資料夾下每個嵌套子目錄中的每個檔案。
ms.date: 07/20/2015
helpviewer_keywords:
- iterating through folders [C#]
- file iteration [C#]
ms.assetid: c4be4a75-6b1b-46a7-9d38-bab353091ed7
ms.openlocfilehash: 9d927e8517ddbdb1c5a9a8aa8ca3c321bf7e8d9c
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91178537"
---
# <a name="how-to-iterate-through-a-directory-tree-c-programming-guide"></a><span data-ttu-id="671d4-104">如何逐一查看目錄樹狀結構 (c # 程式設計指南) </span><span class="sxs-lookup"><span data-stu-id="671d4-104">How to iterate through a directory tree (C# Programming Guide)</span></span>

<span data-ttu-id="671d4-105">「逐一查看樹狀目錄」一詞，代表存取指定根資料夾下每個巢狀子目錄中任意深度的每個檔案。</span><span class="sxs-lookup"><span data-stu-id="671d4-105">The phrase "iterate a directory tree" means to access each file in each nested subdirectory under a specified root folder, to any depth.</span></span> <span data-ttu-id="671d4-106">您不需要開啟每個檔案。</span><span class="sxs-lookup"><span data-stu-id="671d4-106">You do not necessarily have to open each file.</span></span> <span data-ttu-id="671d4-107">您可以只擷取的檔案名稱或子目錄當成 `string`，或者可以擷取格式為 <xref:System.IO.FileInfo?displayProperty=nameWithType> 或 <xref:System.IO.DirectoryInfo?displayProperty=nameWithType> 物件的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="671d4-107">You can just retrieve the name of the file or subdirectory as a `string`, or you can retrieve additional information in the form of a <xref:System.IO.FileInfo?displayProperty=nameWithType> or <xref:System.IO.DirectoryInfo?displayProperty=nameWithType> object.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="671d4-108">在 Windows 中，「目錄」和「資料夾」等詞可交替使用。</span><span class="sxs-lookup"><span data-stu-id="671d4-108">In Windows, the terms "directory" and "folder" are used interchangeably.</span></span> <span data-ttu-id="671d4-109">大部分檔和使用者介面文字都會使用「資料夾」一詞，但是 .NET 類別庫會使用「目錄」一詞。</span><span class="sxs-lookup"><span data-stu-id="671d4-109">Most documentation and user interface text uses the term "folder," but .NET class libraries use the term "directory."</span></span>  
  
 <span data-ttu-id="671d4-110">在最簡單的情況下，當您確定具有指定根資料夾下所有目錄的存取權限時，就可以使用 `System.IO.SearchOption.AllDirectories` 旗標。</span><span class="sxs-lookup"><span data-stu-id="671d4-110">In the simplest case, in which you know for certain that you have access permissions for all directories under a specified root, you can use the `System.IO.SearchOption.AllDirectories` flag.</span></span> <span data-ttu-id="671d4-111">此旗標會傳回符合指定模式的所有巢狀子目錄。</span><span class="sxs-lookup"><span data-stu-id="671d4-111">This flag returns all the nested subdirectories that match the specified pattern.</span></span> <span data-ttu-id="671d4-112">下列範例示範如何使用此旗標。</span><span class="sxs-lookup"><span data-stu-id="671d4-112">The following example shows how to use this flag.</span></span>  
  
```csharp  
root.GetDirectories("*.*", System.IO.SearchOption.AllDirectories);  
```  
  
 <span data-ttu-id="671d4-113">這樣做有一個缺點，那就是指定根資料夾下若有任何一個子目錄造成 <xref:System.IO.DirectoryNotFoundException> 或 <xref:System.UnauthorizedAccessException>，整個方法就會失敗，而且不會傳回任何目錄。</span><span class="sxs-lookup"><span data-stu-id="671d4-113">The weakness in this approach is that if any one of the subdirectories under the specified root causes a <xref:System.IO.DirectoryNotFoundException> or <xref:System.UnauthorizedAccessException>, the whole method fails and returns no directories.</span></span> <span data-ttu-id="671d4-114">當您使用 <xref:System.IO.DirectoryInfo.GetFiles%2A> 方法時，也同樣如此。</span><span class="sxs-lookup"><span data-stu-id="671d4-114">The same is true when you use the <xref:System.IO.DirectoryInfo.GetFiles%2A> method.</span></span> <span data-ttu-id="671d4-115">如果必須對特定子資料夾處理這些例外狀況，您必須手動查核樹狀目錄，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="671d4-115">If you have to handle these exceptions on specific subfolders, you must manually walk the directory tree, as shown in the following examples.</span></span>  
  
 <span data-ttu-id="671d4-116">當您手動查核樹狀目錄時，您可以先處理子目錄 (「前序走訪」**)，或是先處理檔案 (「後序走訪」**)。</span><span class="sxs-lookup"><span data-stu-id="671d4-116">When you manually walk a directory tree, you can handle the subdirectories first (*pre-order traversal*), or the files first (*post-order traversal*).</span></span> <span data-ttu-id="671d4-117">如果您執行前序走訪，您會先查核目前資料夾下的整個樹狀，再逐一查看直接位於該資料夾本身中的檔案。</span><span class="sxs-lookup"><span data-stu-id="671d4-117">If you perform a pre-order traversal, you walk the whole tree under the current folder before iterating through the files that are directly in that folder itself.</span></span> <span data-ttu-id="671d4-118">本文件稍後的範例會執行後序走訪，但您可以輕鬆地修改以執行前序走訪。</span><span class="sxs-lookup"><span data-stu-id="671d4-118">The examples later in this document perform post-order traversal, but you can easily modify them to perform pre-order traversal.</span></span>  
  
 <span data-ttu-id="671d4-119">另一個選項是要使用以遞迴或堆疊為基礎的走訪。</span><span class="sxs-lookup"><span data-stu-id="671d4-119">Another option is whether to use recursion or a stack-based traversal.</span></span> <span data-ttu-id="671d4-120">本文件稍後的範例會示範這兩種方法。</span><span class="sxs-lookup"><span data-stu-id="671d4-120">The examples later in this document show both approaches.</span></span>  
  
 <span data-ttu-id="671d4-121">如果您必須對檔案和資料夾執行各式各樣的作業，您可以藉由將作業重構到個別函式中以模組化這些範例，這樣就可以使用單一委派來叫用這些函式。</span><span class="sxs-lookup"><span data-stu-id="671d4-121">If you have to perform a variety of operations on files and folders, you can modularize these examples by refactoring the operation into separate functions that you can invoke by using a single delegate.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="671d4-122">NTFS 檔案系統可以包含「連接點」**、「符號連結」** 和「永久連結」\*\* 形式的「重新分析點」\*\*。</span><span class="sxs-lookup"><span data-stu-id="671d4-122">NTFS file systems can contain *reparse points* in the form of *junction points*, *symbolic links*, and *hard links*.</span></span> <span data-ttu-id="671d4-123">.NET 方法（例如 <xref:System.IO.DirectoryInfo.GetFiles%2A> 和） <xref:System.IO.DirectoryInfo.GetDirectories%2A> 不會傳回重新分析點下的任何子目錄。</span><span class="sxs-lookup"><span data-stu-id="671d4-123">.NET methods such as <xref:System.IO.DirectoryInfo.GetFiles%2A> and <xref:System.IO.DirectoryInfo.GetDirectories%2A> will not return any subdirectories under a reparse point.</span></span> <span data-ttu-id="671d4-124">此行為可防止兩個重新分析點彼此參考時進入無限迴圈的風險。</span><span class="sxs-lookup"><span data-stu-id="671d4-124">This behavior guards against the risk of entering into an infinite loop when two reparse points refer to each other.</span></span> <span data-ttu-id="671d4-125">一般而言，處理重新分析點要特別謹慎，以免不小心修改或刪除檔案。</span><span class="sxs-lookup"><span data-stu-id="671d4-125">In general, you should use extreme caution when you deal with reparse points to ensure that you do not unintentionally modify or delete files.</span></span> <span data-ttu-id="671d4-126">如果您需要精確控制重新分析點，請使用平台叫用或機器碼，直接呼叫適當的 Win32 檔案系統方法。</span><span class="sxs-lookup"><span data-stu-id="671d4-126">If you require precise control over reparse points, use platform invoke or native code to call the appropriate Win32 file system methods directly.</span></span>  
  
## <a name="example"></a><span data-ttu-id="671d4-127">範例</span><span class="sxs-lookup"><span data-stu-id="671d4-127">Example</span></span>  

 <span data-ttu-id="671d4-128">下列範例示範如何使用遞迴來查核樹狀目錄。</span><span class="sxs-lookup"><span data-stu-id="671d4-128">The following example shows how to walk a directory tree by using recursion.</span></span> <span data-ttu-id="671d4-129">遞迴是很簡潔的方法，但在樹狀目錄很大且巢狀結構很深時，可能會造成堆疊溢位例外狀況。</span><span class="sxs-lookup"><span data-stu-id="671d4-129">The recursive approach is elegant but has the potential to cause a stack overflow exception if the directory tree is large and deeply nested.</span></span>  
  
 <span data-ttu-id="671d4-130">這裡所處理的特定例外狀況，以及對每個檔案或資料夾所執行的特定動作，僅供示範之用。</span><span class="sxs-lookup"><span data-stu-id="671d4-130">The particular exceptions that are handled, and the particular actions that are performed on each file or folder, are provided as examples only.</span></span> <span data-ttu-id="671d4-131">您應該修改此程式碼，以符合特定需求。</span><span class="sxs-lookup"><span data-stu-id="671d4-131">You should modify this code to meet your specific requirements.</span></span> <span data-ttu-id="671d4-132">如需詳細資訊，請參閱程式碼中的註解。</span><span class="sxs-lookup"><span data-stu-id="671d4-132">See the comments in the code for more information.</span></span>  
  
 [!code-csharp[csFilesandFolders#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csFilesAndFolders/CS/FileIteration.cs#1)]  
  
## <a name="example"></a><span data-ttu-id="671d4-133">範例</span><span class="sxs-lookup"><span data-stu-id="671d4-133">Example</span></span>  

 <span data-ttu-id="671d4-134">下列範例示範如何在不使用遞迴的情況下，逐一查看樹狀目錄中的所有檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="671d4-134">The following example shows how to iterate through files and folders in a directory tree without using recursion.</span></span> <span data-ttu-id="671d4-135">這項技術使用泛型 <xref:System.Collections.Generic.Stack%601> 集合類型，也就是後進先出 (LIFO) 堆疊。</span><span class="sxs-lookup"><span data-stu-id="671d4-135">This technique uses the generic <xref:System.Collections.Generic.Stack%601> collection type, which is a last in first out (LIFO) stack.</span></span>  
  
 <span data-ttu-id="671d4-136">這裡所處理的特定例外狀況，以及對每個檔案或資料夾所執行的特定動作，僅供示範之用。</span><span class="sxs-lookup"><span data-stu-id="671d4-136">The particular exceptions that are handled, and the particular actions that are performed on each file or folder, are provided as examples only.</span></span> <span data-ttu-id="671d4-137">您應該修改此程式碼，以符合特定需求。</span><span class="sxs-lookup"><span data-stu-id="671d4-137">You should modify this code to meet your specific requirements.</span></span> <span data-ttu-id="671d4-138">如需詳細資訊，請參閱程式碼中的註解。</span><span class="sxs-lookup"><span data-stu-id="671d4-138">See the comments in the code for more information.</span></span>  
  
 [!code-csharp[csFilesandFolders#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csFilesAndFolders/CS/FileIteration.cs#2)]  
  
 <span data-ttu-id="671d4-139">測試每個資料夾來判斷應用程式是否有權開啟資料夾，通常非常耗時。</span><span class="sxs-lookup"><span data-stu-id="671d4-139">It is generally too time-consuming to test every folder to determine whether your application has permission to open it.</span></span> <span data-ttu-id="671d4-140">因此，程式碼範例只會將該部分的作業封入 `try/catch` 區塊中。</span><span class="sxs-lookup"><span data-stu-id="671d4-140">Therefore, the code example just encloses that part of the operation in a `try/catch` block.</span></span> <span data-ttu-id="671d4-141">您可以修改 `catch` 區塊，以便您在存取資料夾遭拒時，可以嘗試評估權限，然後重新進行存取。</span><span class="sxs-lookup"><span data-stu-id="671d4-141">You can modify the `catch` block so that when you are denied access to a folder, you try to elevate your permissions and then access it again.</span></span> <span data-ttu-id="671d4-142">一般而言，您只會攔截可處理的例外狀況，而不會讓應用程式處於未知狀態。</span><span class="sxs-lookup"><span data-stu-id="671d4-142">As a rule, only catch those exceptions that you can handle without leaving your application in an unknown state.</span></span>  
  
 <span data-ttu-id="671d4-143">如果您必須儲存樹狀目錄的內容，不論是儲存在記憶體或磁碟中，最好的做法就是只儲存每個檔案的 <xref:System.IO.FileSystemInfo.FullName%2A> 屬性 (類型為 `string`)。</span><span class="sxs-lookup"><span data-stu-id="671d4-143">If you must store the contents of a directory tree, either in memory or on disk, the best option is to store only the <xref:System.IO.FileSystemInfo.FullName%2A> property (of type `string`) for each file.</span></span> <span data-ttu-id="671d4-144">然後，您可以視需要使用此字串建立新的 <xref:System.IO.FileInfo> 或 <xref:System.IO.DirectoryInfo> 物件，或是開啟任何需要其他處理的檔案。</span><span class="sxs-lookup"><span data-stu-id="671d4-144">You can then use this string to create a new <xref:System.IO.FileInfo> or <xref:System.IO.DirectoryInfo> object as necessary, or open any file that requires additional processing.</span></span>  
  
## <a name="robust-programming"></a><span data-ttu-id="671d4-145">穩固程式設計</span><span class="sxs-lookup"><span data-stu-id="671d4-145">Robust Programming</span></span>  

 <span data-ttu-id="671d4-146">設計穩固的檔案逐一查看程式碼時，必須考慮檔案系統的許多複雜情況。</span><span class="sxs-lookup"><span data-stu-id="671d4-146">Robust file iteration code must take into account many complexities of the file system.</span></span> <span data-ttu-id="671d4-147">如需 Windows 檔案系統的詳細資訊，請參閱 [NTFS 概觀](/windows-server/storage/file-server/ntfs-overview)。</span><span class="sxs-lookup"><span data-stu-id="671d4-147">For more information on the Windows file system, see [NTFS overview](/windows-server/storage/file-server/ntfs-overview).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="671d4-148">另請參閱</span><span class="sxs-lookup"><span data-stu-id="671d4-148">See also</span></span>

- <xref:System.IO>
- [<span data-ttu-id="671d4-149">LINQ 和檔案目錄</span><span class="sxs-lookup"><span data-stu-id="671d4-149">LINQ and File Directories</span></span>](../concepts/linq/linq-and-file-directories.md)
- [<span data-ttu-id="671d4-150">檔案系統和登錄 (C# 程式設計手冊)</span><span class="sxs-lookup"><span data-stu-id="671d4-150">File System and the Registry (C# Programming Guide)</span></span>](./index.md)
