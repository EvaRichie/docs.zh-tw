---
title: 作法：使用 LINQ 查詢 ArrayList
ms.date: 07/20/2015
ms.assetid: 176358a9-d765-4b57-9557-7feb4428138d
ms.openlocfilehash: b7b75e017fb314b5e5998b743dbf922f34fd9b7c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396463"
---
# <a name="how-to-query-an-arraylist-with-linq-visual-basic"></a>如何：使用 LINQ 查詢 ArrayList （Visual Basic）

使用 LINQ 查詢非泛型 <xref:System.Collections.IEnumerable> 集合時 (例如 <xref:System.Collections.ArrayList>)，您必須明確宣告範圍變數的類型，以反映集合中特定類型的物件。 例如，如果您有 <xref:System.Collections.ArrayList> `Student` 物件的，您的[from 子句](../../../language-reference/queries/from-clause.md)看起來應該像這樣：

```vb
Dim query = From student As Student In arrList
'...
```

藉由指定範圍變數的類型，您就可以將 <xref:System.Collections.ArrayList> 中的每個項目轉換為 `Student`。

在查詢運算式中使用具有明確類型的範圍變數，相當於呼叫 <xref:System.Linq.Enumerable.Cast%2A> 方法。 如果無法執行指定的轉換，則 <xref:System.Linq.Enumerable.Cast%2A> 會擲回例外狀況。 <xref:System.Linq.Enumerable.Cast%2A> 和 <xref:System.Linq.Enumerable.OfType%2A> 是對非泛型 <xref:System.Collections.IEnumerable> 類型執行的兩個標準查詢運算子方法。 在 Visual Basic 中，您必須在 <xref:System.Linq.Enumerable.Cast%2A> 資料來源上明確呼叫方法，以確保特定的範圍變數類型。 如需詳細資訊，請參閱[查詢作業中的類型關聯性（Visual Basic）](type-relationships-in-query-operations.md)。

## <a name="example"></a>範例

下列範例將顯示 <xref:System.Collections.ArrayList> 的簡單查詢。 請注意，此範例會在程式碼呼叫 <xref:System.Collections.ArrayList.Add%2A> 方法時使用物件初始設定式，但這不是必要的。

```vb
Imports System.Collections
Imports System.Linq

Module Module1

    Public Class Student
        Public Property FirstName As String
        Public Property LastName As String
        Public Property Scores As Integer()
    End Class

    Sub Main()

        Dim student1 As New Student With {.FirstName = "Svetlana",
                                     .LastName = "Omelchenko",
                                     .Scores = New Integer() {98, 92, 81, 60}}
        Dim student2 As New Student With {.FirstName = "Claire",
                                    .LastName = "O'Donnell",
                                    .Scores = New Integer() {75, 84, 91, 39}}
        Dim student3 As New Student With {.FirstName = "Cesar",
                                    .LastName = "Garcia",
                                    .Scores = New Integer() {97, 89, 85, 82}}
        Dim student4 As New Student With {.FirstName = "Sven",
                                    .LastName = "Mortensen",
                                    .Scores = New Integer() {88, 94, 65, 91}}

        Dim arrList As New ArrayList()
        arrList.Add(student1)
        arrList.Add(student2)
        arrList.Add(student3)
        arrList.Add(student4)

        ' Use an explicit type for non-generic collections
        Dim query = From student As Student In arrList
                    Where student.Scores(0) > 95
                    Select student

        For Each student As Student In query
            Console.WriteLine(student.LastName & ": " & student.Scores(0))
        Next
        ' Keep the console window open in debug mode.
        Console.WriteLine("Press any key to exit.")
        Console.ReadKey()
    End Sub

End Module
' Output:
'   Omelchenko: 98
'   Garcia: 97
```

## <a name="see-also"></a>另請參閱

- [LINQ to Objects (Visual Basic)](linq-to-objects.md)
