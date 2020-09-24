---
title: '如何在資料夾中查詢文字檔的內容 (LINQ)  (c # ) '
description: '瞭解如何使用 c # 中的 LINQ 來查詢目錄樹狀結構中的所有檔案、開啟每個檔案，以及檢查其內容。'
ms.date: 07/20/2015
ms.assetid: f5b4dce7-1a34-4eb4-9bf1-60d5bdda264c
ms.openlocfilehash: a1f3e29751cd91ac1fd8e6601aa078d967776f5a
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91159016"
---
# <a name="how-to-query-the-contents-of-text-files-in-a-folder-linq-c"></a>如何在資料夾中查詢文字檔的內容 (LINQ)  (c # ) 

此範例示範如何查詢所指定樹狀目錄中的所有檔案、開啟每個檔案，然後檢查檔案的內容。 這類技巧可以用來建立索引，或將樹狀目錄內容的索引反轉。 在此範例中，執行的是簡單字串搜尋。 不過，您可以使用規則運算式執行更複雜的模式比對類型。 如需詳細資訊，請參閱 [如何合併 LINQ 查詢與正則運算式 (c # ) ](./how-to-combine-linq-queries-with-regular-expressions.md)。  
  
## <a name="example"></a>範例  
  
```csharp  
class QueryContents  
{  
    public static void Main()  
    {  
        // Modify this path as necessary.  
        string startFolder = @"c:\program files\Microsoft Visual Studio 9.0\";  
  
        // Take a snapshot of the file system.  
        System.IO.DirectoryInfo dir = new System.IO.DirectoryInfo(startFolder);  
  
        // This method assumes that the application has discovery permissions  
        // for all folders under the specified path.  
        IEnumerable<System.IO.FileInfo> fileList = dir.GetFiles("*.*", System.IO.SearchOption.AllDirectories);  
  
        string searchTerm = @"Visual Studio";  
  
        // Search the contents of each file.  
        // A regular expression created with the RegEx class  
        // could be used instead of the Contains method.  
        // queryMatchingFiles is an IEnumerable<string>.  
        var queryMatchingFiles =  
            from file in fileList  
            where file.Extension == ".htm"  
            let fileText = GetFileText(file.FullName)  
            where fileText.Contains(searchTerm)  
            select file.FullName;  
  
        // Execute the query.  
        Console.WriteLine("The term \"{0}\" was found in:", searchTerm);  
        foreach (string filename in queryMatchingFiles)  
        {  
            Console.WriteLine(filename);  
        }  
  
        // Keep the console window open in debug mode.  
        Console.WriteLine("Press any key to exit");  
        Console.ReadKey();  
    }  
  
    // Read the contents of the file.  
    static string GetFileText(string name)  
    {  
        string fileContents = String.Empty;  
  
        // If the file has been deleted since we took
        // the snapshot, ignore it and return the empty string.  
        if (System.IO.File.Exists(name))  
        {  
            fileContents = System.IO.File.ReadAllText(name);  
        }  
        return fileContents;  
    }  
}  
```  
  
## <a name="compiling-the-code"></a>編譯程式碼  

建立 C# 主控台應用程式專案，以及具有 `using` 指示詞的 System.Linq 和 System.IO 命名空間。
  
## <a name="see-also"></a>另請參閱

- [LINQ 和檔案目錄 (C#)](./linq-and-file-directories.md)
- [LINQ to Objects (C#)](./linq-to-objects.md)
