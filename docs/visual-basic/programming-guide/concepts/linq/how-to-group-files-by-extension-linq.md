---
title: 作法：依副檔名分組檔案 (LINQ)
ms.date: 07/20/2015
ms.assetid: 904dc6d7-7162-4655-a7f4-5785d669bc5a
ms.openlocfilehash: 3b1b02283dc65148b8a44952ce39659cc92b483a
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91077302"
---
# <a name="how-to-group-files-by-extension-linq-visual-basic"></a><span data-ttu-id="b232b-102">如何：依副檔名將檔案分組 (LINQ)  (Visual Basic) </span><span class="sxs-lookup"><span data-stu-id="b232b-102">How to: Group Files by Extension (LINQ) (Visual Basic)</span></span>

<span data-ttu-id="b232b-103">此範例示範如何使用 LINQ，對檔案或資料庫清單執行進階群組和排序作業。</span><span class="sxs-lookup"><span data-stu-id="b232b-103">This example shows how LINQ can be used to perform advanced grouping and sorting operations on lists of files or folders.</span></span> <span data-ttu-id="b232b-104">它也示範如何使用 <xref:System.Linq.Enumerable.Skip%2A> 和 <xref:System.Linq.Enumerable.Take%2A> 方法在主控台視窗中分頁輸出。</span><span class="sxs-lookup"><span data-stu-id="b232b-104">It also shows how to page output in the console window by using the <xref:System.Linq.Enumerable.Skip%2A> and <xref:System.Linq.Enumerable.Take%2A> methods.</span></span>  
  
## <a name="example"></a><span data-ttu-id="b232b-105">範例</span><span class="sxs-lookup"><span data-stu-id="b232b-105">Example</span></span>  

 <span data-ttu-id="b232b-106">下列查詢示範如何依副檔名分組指定樹狀目錄的內容。</span><span class="sxs-lookup"><span data-stu-id="b232b-106">The following query shows how to group the contents of a specified directory tree by the file name extension.</span></span>  
  
```vb  
Module GroupByExtension  
    Public Sub Main()  
  
        ' Root folder to query, along with all subfolders.  
        Dim startFolder As String = "C:\program files\Microsoft Visual Studio 9.0\VB\"  
  
        ' Used in WriteLine() to skip over startfolder in output lines.  
        Dim rootLength As Integer = startFolder.Length  
  
        'Take a snapshot of the folder contents  
        Dim dir As New System.IO.DirectoryInfo(startFolder)  
        Dim fileList = dir.GetFiles("*.*", System.IO.SearchOption.AllDirectories)  
  
        ' Create the query.  
        Dim queryGroupByExt = From file In fileList _  
                          Group By file.Extension.ToLower() Into fileGroup = Group _  
                          Order By ToLower _  
                          Select fileGroup  
  
        ' Execute the query. By storing the result we can  
        ' page the display with good performance.  
        Dim groupByExtList = queryGroupByExt.ToList()  
  
        ' Display one group at a time. If the number of
        ' entries is greater than the number of lines  
        ' in the console window, then page the output.  
        Dim trimLength = startFolder.Length  
        PageOutput(groupByExtList, trimLength)  
  
    End Sub  
  
    ' Pages console display for large query results. No more than one group per page.  
    ' This sub specifically works with group queries of FileInfo objects  
    ' but can be modified for any type.  
    Sub PageOutput(ByVal groupQuery, ByVal charsToSkip)  
  
        ' "3" = 1 line for extension key + 1 for "Press any key" + 1 for input cursor.  
        Dim numLines As Integer = Console.WindowHeight - 3  
        ' Flag to indicate whether there are more results to display  
        Dim goAgain As Boolean = True  
  
        For Each fg As IEnumerable(Of System.IO.FileInfo) In groupQuery  
            ' Start a new extension at the top of a page.  
            Dim currentLine As Integer = 0  
  
            Do While (currentLine < fg.Count())  
                Console.Clear()  
                Console.WriteLine(fg(0).Extension)  
  
                ' Get the next page of results  
                ' No more than one filename per page  
                Dim resultPage = From file In fg _  
                                Skip currentLine Take numLines  
  
                ' Execute the query. Trim the display output.  
                For Each line In resultPage  
                    Console.WriteLine(vbTab & line.FullName.Substring(charsToSkip))  
                Next  
  
                ' Advance the current position  
                currentLine = numLines + currentLine  
  
                ' Give the user a chance to break out of the loop  
                Console.WriteLine("Press any key for next page or the 'End' key to exit.")  
                Dim key As ConsoleKey = Console.ReadKey().Key  
                If key = ConsoleKey.End Then  
                    goAgain = False  
                    Exit For  
                End If  
            Loop  
        Next  
    End Sub  
End Module  
```  
  
 <span data-ttu-id="b232b-107">根據本機檔案系統的詳細資料及 `startFolder` 的設定，此程式的輸出可能很長。</span><span class="sxs-lookup"><span data-stu-id="b232b-107">The output from this program can be long, depending on the details of the local file system and what the `startFolder` is set to.</span></span> <span data-ttu-id="b232b-108">為了能夠檢視所有結果，此範例示範如何將結果分頁。</span><span class="sxs-lookup"><span data-stu-id="b232b-108">To enable viewing of all results, this example shows how to page through results.</span></span> <span data-ttu-id="b232b-109">您可以將相同的技術應用到 Windows 和 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b232b-109">The same techniques can be applied to Windows and Web applications.</span></span> <span data-ttu-id="b232b-110">請注意，因為程式碼會將群組中的項目分頁，所以需要使用巢狀 `For Each` 迴圈。</span><span class="sxs-lookup"><span data-stu-id="b232b-110">Notice that because the code pages the items in a group, a nested `For Each` loop is required.</span></span> <span data-ttu-id="b232b-111">此外還需要一些額外的邏輯來計算清單中目前的位置，以及讓使用者停止分頁並結束程式。</span><span class="sxs-lookup"><span data-stu-id="b232b-111">There is also some additional logic to compute the current position in the list, and to enable the user to stop paging and exit the program.</span></span> <span data-ttu-id="b232b-112">在這種特殊情況下，會對原始查詢的快取結果執行分頁查詢。</span><span class="sxs-lookup"><span data-stu-id="b232b-112">In this particular case, the paging query is run against the cached results from the original query.</span></span> <span data-ttu-id="b232b-113">在其他內容中 (例如 LINQ to SQL)，則不需要這類快取。</span><span class="sxs-lookup"><span data-stu-id="b232b-113">In other contexts, such as LINQ to SQL, such caching is not required.</span></span>  
  
## <a name="compile-the-code"></a><span data-ttu-id="b232b-114">編譯程式碼</span><span class="sxs-lookup"><span data-stu-id="b232b-114">Compile the code</span></span>  

<span data-ttu-id="b232b-115">使用 `Imports` 適用于 system.string 命名空間的語句來建立 Visual Basic 主控台應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="b232b-115">Create a Visual Basic console application project, with an `Imports` statement for the System.Linq namespace.</span></span>
  
## <a name="see-also"></a><span data-ttu-id="b232b-116">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b232b-116">See also</span></span>

- [<span data-ttu-id="b232b-117">LINQ to Objects (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="b232b-117">LINQ to Objects (Visual Basic)</span></span>](linq-to-objects.md)
- [<span data-ttu-id="b232b-118">LINQ 與檔案目錄 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="b232b-118">LINQ and File Directories (Visual Basic)</span></span>](linq-and-file-directories.md)
