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
# <a name="how-to-populate-object-collections-from-multiple-sources-linq-c"></a><span data-ttu-id="03c5c-104">如何從多個來源填入物件集合（LINQ）（c #）</span><span class="sxs-lookup"><span data-stu-id="03c5c-104">How to populate object collections from multiple sources (LINQ) (C#)</span></span>

<span data-ttu-id="03c5c-105">此範例示範如何將不同來源的資料合併成新的類型。</span><span class="sxs-lookup"><span data-stu-id="03c5c-105">This example shows how to merge data from different sources into a sequence of new types.</span></span>

> [!NOTE]
> <span data-ttu-id="03c5c-106">請勿嘗試將記憶體內部資料或檔案系統中的資料，與仍在資料庫中的資料聯結。</span><span class="sxs-lookup"><span data-stu-id="03c5c-106">Don't try to join in-memory data or data in the file system with data that is still in a database.</span></span> <span data-ttu-id="03c5c-107">這類跨定義域的聯結會產生未定義的結果，因為針對資料庫查詢和其他類型的來源定義聯結作業的方式可能不同。</span><span class="sxs-lookup"><span data-stu-id="03c5c-107">Such cross-domain joins can yield undefined results because of different ways in which join operations might be defined for database queries and other types of sources.</span></span> <span data-ttu-id="03c5c-108">此外，如果資料庫中的資料量太大，這類作業也可能會導致記憶體不足的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="03c5c-108">Additionally, there is a risk that such an operation could cause an out-of-memory exception if the amount of data in the database is large enough.</span></span> <span data-ttu-id="03c5c-109">若要將資料庫中的資料聯結至記憶體內部資料，請先在資料庫查詢中呼叫 `ToList` 或 `ToArray`，然後對傳回的集合執行聯結。</span><span class="sxs-lookup"><span data-stu-id="03c5c-109">To join data from a database to in-memory data, first call `ToList` or `ToArray` on the database query, and then perform the join on the returned collection.</span></span>

## <a name="to-create-the-data-file"></a><span data-ttu-id="03c5c-110">建立資料檔</span><span class="sxs-lookup"><span data-stu-id="03c5c-110">To create the data file</span></span>

<span data-ttu-id="03c5c-111">將 names.csv 和 scores.csv 檔案複製到您的專案資料夾中，如[如何從不同的檔案聯結內容（LINQ）（c #）](./how-to-join-content-from-dissimilar-files-linq.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="03c5c-111">Copy the names.csv and scores.csv files into your project folder, as described in [How to join content from dissimilar files (LINQ) (C#)](./how-to-join-content-from-dissimilar-files-linq.md).</span></span>

## <a name="example"></a><span data-ttu-id="03c5c-112">範例</span><span class="sxs-lookup"><span data-stu-id="03c5c-112">Example</span></span>

<span data-ttu-id="03c5c-113">下列範例示範如何使用具名類型 `Student`，來儲存將兩個記憶體內部字串集合合併得來的資料，這些字串模擬 .csv 格式的試算表資料。</span><span class="sxs-lookup"><span data-stu-id="03c5c-113">The following example shows how to use a named type `Student` to store merged data from two in-memory collections of strings that simulate spreadsheet data in .csv format.</span></span> <span data-ttu-id="03c5c-114">第一個字串集合代表學生姓名和學號，第二個集合代表學生學號 (第一欄) 和四個測驗分數。</span><span class="sxs-lookup"><span data-stu-id="03c5c-114">The first collection of strings represents the student names and IDs, and the second collection represents the student ID (in the first column) and four exam scores.</span></span> <span data-ttu-id="03c5c-115">學號會作為外部索引鍵使用。</span><span class="sxs-lookup"><span data-stu-id="03c5c-115">The ID is used as the foreign key.</span></span>

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

<span data-ttu-id="03c5c-116">在 [select](../../../language-reference/keywords/select-clause.md) 子句中，會使用物件初始設定式，透過兩個來源的資料具現化每個新的 `Student` 物件。</span><span class="sxs-lookup"><span data-stu-id="03c5c-116">In the [select](../../../language-reference/keywords/select-clause.md) clause, an object initializer is used to instantiate each new `Student` object by using the data from the two sources.</span></span>

<span data-ttu-id="03c5c-117">如果您不需要儲存查詢的結果，則匿名型別會比具名類型更方便使用。</span><span class="sxs-lookup"><span data-stu-id="03c5c-117">If you don't have to store the results of a query, anonymous types can be more convenient than named types.</span></span> <span data-ttu-id="03c5c-118">如果要在執行查詢的方法外傳遞查詢結果，則必須使用具名類型。</span><span class="sxs-lookup"><span data-stu-id="03c5c-118">Named types are required if you pass the query results outside the method in which the query is executed.</span></span> <span data-ttu-id="03c5c-119">下列範例會執行與上述範例相同的工作，但使用匿名型別而不是具名類型：</span><span class="sxs-lookup"><span data-stu-id="03c5c-119">The following example executes the same task as the previous example, but uses anonymous types instead of named types:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="03c5c-120">請參閱</span><span class="sxs-lookup"><span data-stu-id="03c5c-120">See also</span></span>

- [<span data-ttu-id="03c5c-121">LINQ 和字串 (C#)</span><span class="sxs-lookup"><span data-stu-id="03c5c-121">LINQ and Strings (C#)</span></span>](./linq-and-strings.md)
- [<span data-ttu-id="03c5c-122">物件和集合初始設定式</span><span class="sxs-lookup"><span data-stu-id="03c5c-122">Object and Collection Initializers</span></span>](../../classes-and-structs/object-and-collection-initializers.md)
- [<span data-ttu-id="03c5c-123">匿名類型</span><span class="sxs-lookup"><span data-stu-id="03c5c-123">Anonymous Types</span></span>](../../classes-and-structs/anonymous-types.md)
