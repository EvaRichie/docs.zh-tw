---
title: 作法：聯結不同檔案中的內容 (LINQ)
ms.date: 06/27/2018
ms.assetid: e7530857-c467-41ea-9730-84e6b1065a4d
ms.openlocfilehash: 7dac73a16d0d3fbf409f58628bc5c69716dcee14
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84398366"
---
# <a name="how-to-join-content-from-dissimilar-files-linq-visual-basic"></a>如何：從不同的檔案聯結內容（LINQ）（Visual Basic）

此範例示範如何將兩個逗號分隔檔案中資料的共同值當做相符的索引鍵，聯結這兩個檔案中的資料。 如果您必須將兩個試算表中的資料，或一個試算表和一個不同格式之檔案中的資料合併為新的檔案，這個方法就很有用。 您可以修改範例，以搭配任何類型的結構化文字使用。

## <a name="to-create-the-data-files"></a>建立資料檔

1. 將下列各行複製到名為 scores.csv 的檔案中，然後將該檔案儲存至您的專案資料夾。 該檔案代表試算表資料。 第 1 欄是學生的學號，第 2 欄到第 5 欄則是測驗分數。

    ```csv
    111, 97, 92, 81, 60
    112, 75, 84, 91, 39
    113, 88, 94, 65, 91
    114, 97, 89, 85, 82
    115, 35, 72, 91, 70
    116, 99, 86, 90, 94
    117, 93, 92, 80, 87
    118, 92, 90, 83, 78
    119, 68, 79, 88, 92
    120, 99, 82, 81, 79
    121, 96, 85, 91, 60
    122, 94, 92, 91, 91
    ```

2. 將下列各行複製到名為 names.csv 的檔案中，然後將該檔案儲存至您的專案資料夾。 該檔案代表內含學生姓氏、名字和學號的試算表。

    ```csv
    Omelchenko,Svetlana,111
    O'Donnell,Claire,112
    Mortensen,Sven,113
    Garcia,Cesar,114
    Garcia,Debra,115
    Fakhouri,Fadi,116
    Feng,Hanying,117
    Garcia,Hugo,118
    Tucker,Lance,119
    Adams,Terry,120
    Zabokritski,Eugene,121
    Tucker,Michael,122
    ```

## <a name="example"></a>範例

```vb
Imports System.Collections.Generic
Imports System.Linq

Class JoinStrings

    Shared Sub Main()

        ' Join content from spreadsheet files that contain
        ' related information. names.csv contains the student name
        ' plus an ID number. scores.csv contains the ID and a
        ' set of four test scores. The following query joins
        ' the scores to the student names by using ID as a
        ' matching key.

        Dim names As String() = System.IO.File.ReadAllLines("../../../names.csv")
        Dim scores As String() = System.IO.File.ReadAllLines("../../../scores.csv")

        ' Name:    Last[0],       First[1],  ID[2],     Grade Level[3]
        '          Omelchenko,    Svetlana,  111,       2
        ' Score:   StudentID[0],  Exam1[1]   Exam2[2],  Exam3[3],  Exam4[4]
        '          111,           97,        92,        81,        60

        ' This query joins two dissimilar spreadsheets based on common ID value.
        ' Multiple from clauses are used instead of a join clause
        ' in order to store results of id.Split.
        Dim scoreQuery1 = From name In names
                         Let n = name.Split(New Char() {","})
                            From id In scores
                            Let n2 = id.Split(New Char() {","})
                            Where Convert.ToInt32(n(2)) = Convert.ToInt32(n2(0))
                            Select n(0) & "," & n2(1) & "," & n2(2) & "," & n2(3) & "," &  n2(4)

        ' Pass a query variable to a Sub and execute it there.
        ' The query itself is unchanged.
        OutputQueryResults(scoreQuery1, "Merge two spreadsheets:")

        ' Keep console window open in debug mode.
        Console.WriteLine("Press any key to exit.")
        Console.ReadKey()
    End Sub

    Shared Sub OutputQueryResults(ByVal query As IEnumerable(Of String), ByVal message As String)

        Console.WriteLine(System.Environment.NewLine & message)
        For Each item As String In query
            Console.WriteLine(item)
        Next
        Console.WriteLine(query.Count & " total names in list")

    End Sub
End Class
' Output:
' Merge two spreadsheets:
' Omelchenko, 97, 92, 81, 60
' O'Donnell, 75, 84, 91, 39
' Mortensen, 88, 94, 65, 91
' Garcia, 97, 89, 85, 82
' Garcia, 35, 72, 91, 70
' Fakhouri, 99, 86, 90, 94
' Feng, 93, 92, 80, 87
' Garcia, 92, 90, 83, 78
' Tucker, 68, 79, 88, 92
' Adams, 99, 82, 81, 79
' Zabokritski, 96, 85, 91, 60
' Tucker, 94, 92, 91, 91
' 12 total names in list
```

## <a name="see-also"></a>另請參閱

- [LINQ 與字串 (Visual Basic)](linq-and-strings.md)
- [LINQ 與檔案目錄 (Visual Basic)](linq-and-file-directories.md)
