---
title: '如何使用正則運算式合併 LINQ 查詢 (c # ) '
description: '這個範例會在 c # 中使用 Regex 類別，建立要在文字字串中比對的正則運算式。'
ms.date: 07/20/2015
ms.assetid: 6b003b65-20a4-4ca2-929e-2ee3f215aecc
ms.openlocfilehash: e423261961c25c6aae62483d332ce053d7b6f963
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91157495"
---
# <a name="how-to-combine-linq-queries-with-regular-expressions-c"></a><span data-ttu-id="9b8c7-103">如何使用正則運算式合併 LINQ 查詢 (c # ) </span><span class="sxs-lookup"><span data-stu-id="9b8c7-103">How to combine LINQ queries with regular expressions (C#)</span></span>

<span data-ttu-id="9b8c7-104">此範例會示範如何使用 <xref:System.Text.RegularExpressions.Regex> 類別來建立規則運算式，以在文字字串中進行更複雜的比對。</span><span class="sxs-lookup"><span data-stu-id="9b8c7-104">This example shows how to use the <xref:System.Text.RegularExpressions.Regex> class to create a regular expression for more complex matching in text strings.</span></span> <span data-ttu-id="9b8c7-105">LINQ 查詢讓您輕鬆地準確篩選出您想要用規則運算式搜尋的檔案，並調整結果。</span><span class="sxs-lookup"><span data-stu-id="9b8c7-105">The LINQ query makes it easy to filter on exactly the files that you want to search with the regular expression, and to shape the results.</span></span>  
  
## <a name="example"></a><span data-ttu-id="9b8c7-106">範例</span><span class="sxs-lookup"><span data-stu-id="9b8c7-106">Example</span></span>  
  
```csharp  
class QueryWithRegEx  
{  
    public static void Main()  
    {  
        // Modify this path as necessary so that it accesses your version of Visual Studio.  
        string startFolder = @"C:\Program Files (x86)\Microsoft Visual Studio 14.0\";  
        // One of the following paths may be more appropriate on your computer.  
        //string startFolder = @"C:\Program Files (x86)\Microsoft Visual Studio\2017\";  
  
        // Take a snapshot of the file system.  
        IEnumerable<System.IO.FileInfo> fileList = GetFiles(startFolder);  
  
        // Create the regular expression to find all things "Visual".  
        System.Text.RegularExpressions.Regex searchTerm =  
            new System.Text.RegularExpressions.Regex(@"Visual (Basic|C#|C\+\+|Studio)");  
  
        // Search the contents of each .htm file.  
        // Remove the where clause to find even more matchedValues!  
        // This query produces a list of files where a match  
        // was found, and a list of the matchedValues in that file.  
        // Note: Explicit typing of "Match" in select clause.  
        // This is required because MatchCollection is not a
        // generic IEnumerable collection.  
        var queryMatchingFiles =  
            from file in fileList  
            where file.Extension == ".htm"  
            let fileText = System.IO.File.ReadAllText(file.FullName)  
            let matches = searchTerm.Matches(fileText)  
            where matches.Count > 0  
            select new  
            {  
                name = file.FullName,  
                matchedValues = from System.Text.RegularExpressions.Match match in matches  
                                select match.Value  
            };  
  
        // Execute the query.  
        Console.WriteLine("The term \"{0}\" was found in:", searchTerm.ToString());  
  
        foreach (var v in queryMatchingFiles)  
        {  
            // Trim the path a bit, then write
            // the file name in which a match was found.  
            string s = v.name.Substring(startFolder.Length - 1);  
            Console.WriteLine(s);  
  
            // For this file, write out all the matching strings  
            foreach (var v2 in v.matchedValues)  
            {  
                Console.WriteLine("  " + v2);  
            }  
        }  
  
        // Keep the console window open in debug mode  
        Console.WriteLine("Press any key to exit");  
        Console.ReadKey();  
    }  
  
    // This method assumes that the application has discovery
    // permissions for all folders under the specified path.  
    static IEnumerable<System.IO.FileInfo> GetFiles(string path)  
    {  
        if (!System.IO.Directory.Exists(path))  
            throw new System.IO.DirectoryNotFoundException();  
  
        string[] fileNames = null;  
        List<System.IO.FileInfo> files = new List<System.IO.FileInfo>();  
  
        fileNames = System.IO.Directory.GetFiles(path, "*.*", System.IO.SearchOption.AllDirectories);  
        foreach (string name in fileNames)  
        {  
            files.Add(new System.IO.FileInfo(name));  
        }  
        return files;  
    }  
}  
```  
  
 <span data-ttu-id="9b8c7-107">請注意，您也可以對由 `RegEx` 搜尋所傳回的 <xref:System.Text.RegularExpressions.MatchCollection> 物件進行查詢。</span><span class="sxs-lookup"><span data-stu-id="9b8c7-107">Note that you can also query the <xref:System.Text.RegularExpressions.MatchCollection> object that is returned by a `RegEx` search.</span></span> <span data-ttu-id="9b8c7-108">在本例中，結果只會產生每個相符項目的值。</span><span class="sxs-lookup"><span data-stu-id="9b8c7-108">In this example only the value of each match is produced in the results.</span></span> <span data-ttu-id="9b8c7-109">不過，它也可以使用 LINQ 對該集合執行所有種類的篩選、排序及群組。</span><span class="sxs-lookup"><span data-stu-id="9b8c7-109">However, it is also possible to use LINQ to perform all kinds of filtering, sorting, and grouping on that collection.</span></span> <span data-ttu-id="9b8c7-110">因為 <xref:System.Text.RegularExpressions.MatchCollection> 為非泛型 <xref:System.Collections.IEnumerable> 集合，所以您必須在查詢中明確地陳述範圍變數的類型。</span><span class="sxs-lookup"><span data-stu-id="9b8c7-110">Because <xref:System.Text.RegularExpressions.MatchCollection> is a non-generic <xref:System.Collections.IEnumerable> collection, you have to explicitly state the type of the range variable in the query.</span></span>  
  
## <a name="compiling-the-code"></a><span data-ttu-id="9b8c7-111">編譯程式碼</span><span class="sxs-lookup"><span data-stu-id="9b8c7-111">Compiling the Code</span></span>  

 <span data-ttu-id="9b8c7-112">建立 C# 主控台應用程式專案，以及具有 `using` 指示詞的 System.Linq 和 System.IO 命名空間。</span><span class="sxs-lookup"><span data-stu-id="9b8c7-112">Create a C# console application project with `using` directives for the System.Linq and System.IO namespaces.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="9b8c7-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9b8c7-113">See also</span></span>

- [<span data-ttu-id="9b8c7-114">LINQ 和字串 (C#)</span><span class="sxs-lookup"><span data-stu-id="9b8c7-114">LINQ and Strings (C#)</span></span>](./linq-and-strings.md)
- [<span data-ttu-id="9b8c7-115">LINQ 和檔案目錄 (C#)</span><span class="sxs-lookup"><span data-stu-id="9b8c7-115">LINQ and File Directories (C#)</span></span>](./linq-and-file-directories.md)
