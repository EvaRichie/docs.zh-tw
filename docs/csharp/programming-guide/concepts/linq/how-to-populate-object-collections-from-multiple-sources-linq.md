---
title: '如何從多個來源填入物件集合（LINQ）（c #）'
description: '瞭解如何在 c # 中使用 LINQ，將不同來源的資料合併成一系列的新類型。 這些範例會同時使用匿名和命名的類型。'
ms.date: 06/12/2018
ms.assetid: 8ad7d480-b46c-4ccc-8c57-76f2d04ccc6d
ms.openlocfilehash: 9dc9f98ae09e0fe3437b5d2ccab32b3dbcd93714
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87104715"
---
# <a name="how-to-populate-object-collections-from-multiple-sources-linq-c"></a>如何從多個來源填入物件集合（LINQ）（c #）

此範例示範如何將不同來源的資料合併成新的類型。

> [!NOTE]
> 請勿嘗試將記憶體內部資料或檔案系統中的資料，與仍在資料庫中的資料聯結。 這類跨定義域的聯結會產生未定義的結果，因為針對資料庫查詢和其他類型的來源定義聯結作業的方式可能不同。 此外，如果資料庫中的資料量太大，這類作業也可能會導致記憶體不足的例外狀況。 若要將資料庫中的資料聯結至記憶體內部資料，請先在資料庫查詢中呼叫 `ToList` 或 `ToArray`，然後對傳回的集合執行聯結。

## <a name="to-create-the-data-file"></a>建立資料檔

將 names.csv 和 scores.csv 檔案複製到您的專案資料夾中，如[如何從不同的檔案聯結內容（LINQ）（c #）](./how-to-join-content-from-dissimilar-files-linq.md)中所述。

## <a name="example"></a>範例

下列範例示範如何使用具名類型 `Student`，來儲存將兩個記憶體內部字串集合合併得來的資料，這些字串模擬 .csv 格式的試算表資料。 第一個字串集合代表學生姓名和學號，第二個集合代表學生學號 (第一欄) 和四個測驗分數。 學號會作為外部索引鍵使用。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Student
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public int ID { get; set; }
    public List<int> ExamScores { get; set; }
}

class PopulateCollection
{
    static void Main()
    {
        // These data files are defined in How to join content from
        // dissimilar files (LINQ).

        // Each line of names.csv consists of a last name, a first name, and an
        // ID number, separated by commas. For example, Omelchenko,Svetlana,111
        string[] names = System.IO.File.ReadAllLines(@"../../../names.csv");

        // Each line of scores.csv consists of an ID number and four test
        // scores, separated by commas. For example, 111, 97, 92, 81, 60
        string[] scores = System.IO.File.ReadAllLines(@"../../../scores.csv");

        // Merge the data sources using a named type.
        // var could be used instead of an explicit type. Note the dynamic
        // creation of a list of ints for the ExamScores member. The first item
        // is skipped in the split string because it is the student ID,
        // not an exam score.
        IEnumerable<Student> queryNamesScores =
            from nameLine in names
            let splitName = nameLine.Split(',')
            from scoreLine in scores
            let splitScoreLine = scoreLine.Split(',')
            where Convert.ToInt32(splitName[2]) == Convert.ToInt32(splitScoreLine[0])
            select new Student()
            {
                FirstName = splitName[0],
                LastName = splitName[1],
                ID = Convert.ToInt32(splitName[2]),
                ExamScores = (from scoreAsText in splitScoreLine.Skip(1)
                              select Convert.ToInt32(scoreAsText)).
                              ToList()
            };

        // Optional. Store the newly created student objects in memory
        // for faster access in future queries. This could be useful with
        // very large data files.
        List<Student> students = queryNamesScores.ToList();

        // Display each student's name and exam score average.
        foreach (var student in students)
        {
            Console.WriteLine("The average score of {0} {1} is {2}.",
                student.FirstName, student.LastName,
                student.ExamScores.Average());
        }

        //Keep console window open in debug mode
        Console.WriteLine("Press any key to exit.");
        Console.ReadKey();
    }
}
/* Output:
    The average score of Omelchenko Svetlana is 82.5.
    The average score of O'Donnell Claire is 72.25.
    The average score of Mortensen Sven is 84.5.
    The average score of Garcia Cesar is 88.25.
    The average score of Garcia Debra is 67.
    The average score of Fakhouri Fadi is 92.25.
    The average score of Feng Hanying is 88.
    The average score of Garcia Hugo is 85.75.
    The average score of Tucker Lance is 81.75.
    The average score of Adams Terry is 85.25.
    The average score of Zabokritski Eugene is 83.
    The average score of Tucker Michael is 92.
 */
```

在 [select](../../../language-reference/keywords/select-clause.md) 子句中，會使用物件初始設定式，透過兩個來源的資料具現化每個新的 `Student` 物件。

如果您不需要儲存查詢的結果，則匿名型別會比具名類型更方便使用。 如果要在執行查詢的方法外傳遞查詢結果，則必須使用具名類型。 下列範例會執行與上述範例相同的工作，但使用匿名型別而不是具名類型：

```csharp
// Merge the data sources by using an anonymous type.
// Note the dynamic creation of a list of ints for the
// ExamScores member. We skip 1 because the first string
// in the array is the student ID, not an exam score.
var queryNamesScores2 =
    from nameLine in names
    let splitName = nameLine.Split(',')
    from scoreLine in scores
    let splitScoreLine = scoreLine.Split(',')
    where Convert.ToInt32(splitName[2]) == Convert.ToInt32(splitScoreLine[0])
    select new
    {
        First = splitName[0],
        Last = splitName[1],
        ExamScores = (from scoreAsText in splitScoreLine.Skip(1)
                      select Convert.ToInt32(scoreAsText))
                      .ToList()
    };

// Display each student's name and exam score average.
foreach (var student in queryNamesScores2)
{
    Console.WriteLine("The average score of {0} {1} is {2}.",
        student.First, student.Last, student.ExamScores.Average());
}
```

## <a name="see-also"></a>請參閱

- [LINQ 和字串 (C#)](./linq-and-strings.md)
- [物件和集合初始設定式](../../classes-and-structs/object-and-collection-initializers.md)
- [匿名類型](../../classes-and-structs/anonymous-types.md)
