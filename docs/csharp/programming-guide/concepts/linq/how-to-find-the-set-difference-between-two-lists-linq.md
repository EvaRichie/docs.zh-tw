---
title: '如何尋找兩個清單之間的集合差異 (LINQ)  (c # ) '
description: '瞭解如何使用 c # 中的 LINQ 來比較兩個字串清單，並輸出位於一個清單但不在另一個清單中的行。'
ms.date: 07/20/2015
ms.assetid: 8e8945f0-4aba-439d-8d5d-c8d1eeef4e71
ms.openlocfilehash: 01aba16b3489e4bf21a76bc715b6d4d2c9d250dd
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91159055"
---
# <a name="how-to-find-the-set-difference-between-two-lists-linq-c"></a>如何尋找兩個清單之間的集合差異 (LINQ)  (c # ) 

此範例示範如何使用 LINQ 比較兩份字串清單，然後輸出在 names1.txt 但不在 names2.txt 中的字串行。  
  
### <a name="to-create-the-data-files"></a>建立資料檔  
  
1. 將 names1.txt 和 names2.txt 複製到您的方案資料夾，如 [如何合併和比較字串集合 (LINQ)  (c # ) ](./how-to-combine-and-compare-string-collections-linq.md)所示。  
  
## <a name="example"></a>範例  
  
```csharp  
class CompareLists  
{
    static void Main()  
    {  
        // Create the IEnumerable data sources.  
        string[] names1 = System.IO.File.ReadAllLines(@"../../../names1.txt");  
        string[] names2 = System.IO.File.ReadAllLines(@"../../../names2.txt");  
  
        // Create the query. Note that method syntax must be used here.  
        IEnumerable<string> differenceQuery =  
          names1.Except(names2);  
  
        // Execute the query.  
        Console.WriteLine("The following lines are in names1.txt but not names2.txt");  
        foreach (string s in differenceQuery)  
            Console.WriteLine(s);  
  
        // Keep the console window open in debug mode.  
        Console.WriteLine("Press any key to exit");  
        Console.ReadKey();  
    }  
}  
/* Output:  
     The following lines are in names1.txt but not names2.txt  
    Potra, Cristina  
    Noriega, Fabricio  
    Aw, Kam Foo  
    Toyoshima, Tim  
    Guy, Wey Yuan  
    Garcia, Debra  
     */  
```  
  
 C# 中某些查詢作業類型，如 <xref:System.Linq.Enumerable.Except%2A>、<xref:System.Linq.Enumerable.Distinct%2A>、<xref:System.Linq.Enumerable.Union%2A> 和 <xref:System.Linq.Enumerable.Concat%2A>，只能使用以方法為基礎的語法表示。  
  
## <a name="compiling-the-code"></a>編譯程式碼  

 建立 C# 主控台應用程式專案，以及具有 `using` 指示詞的 System.Linq 和 System.IO 命名空間。  
  
## <a name="see-also"></a>另請參閱

- [LINQ 和字串 (C#)](./linq-and-strings.md)
