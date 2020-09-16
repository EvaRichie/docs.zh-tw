---
title: 作法：重新排列分隔檔的欄位 (LINQ)
ms.date: 07/20/2015
ms.assetid: c451c7db-663b-4daf-b8ba-a2093095d672
ms.openlocfilehash: 62c21dfb67ef35591a8ffe214bc132e63a2433bd
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90535380"
---
# <a name="how-to-reorder-the-fields-of-a-delimited-file-linq-visual-basic"></a><span data-ttu-id="be43b-102">如何：將分隔檔的欄位重新排列 (LINQ)  (Visual Basic) </span><span class="sxs-lookup"><span data-stu-id="be43b-102">How to: Reorder the Fields of a Delimited File (LINQ) (Visual Basic)</span></span>

<span data-ttu-id="be43b-103">逗號分隔值 (CSV) 檔案是一種文字檔，常用來儲存試算表資料或其他以資料列和資料行呈現的表格式資料。</span><span class="sxs-lookup"><span data-stu-id="be43b-103">A comma-separated value (CSV) file is a text file that is often used to store spreadsheet data or other tabular data that is represented by rows and columns.</span></span> <span data-ttu-id="be43b-104">使用 <xref:System.String.Split%2A> 方法隔開欄位後，就可以利用 LINQ 輕鬆地查詢和管理 CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="be43b-104">By using the <xref:System.String.Split%2A> method to separate the fields, it is very easy to query and manipulate CSV files by using LINQ.</span></span> <span data-ttu-id="be43b-105">事實上，您可以使用此相同的方法來重新排列任何結構化文字行中的其中幾部分，而不限於 CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="be43b-105">In fact, the same technique can be used to reorder the parts of any structured line of text; it is not limited to CSV files.</span></span>

<span data-ttu-id="be43b-106">在下列範例中，假設有三個資料行分別表示學生的「姓氏」、「名字」和「學號」。</span><span class="sxs-lookup"><span data-stu-id="be43b-106">In the following example, assume that the three columns represent students' "last name," "first name", and "ID."</span></span> <span data-ttu-id="be43b-107">這些欄位會依照學生的姓氏字母排序。</span><span class="sxs-lookup"><span data-stu-id="be43b-107">The fields are in alphabetical order based on the students' last names.</span></span> <span data-ttu-id="be43b-108">此查詢會產生新的順序，其中會先出現學號資料行，後面接著結合學生姓氏和名字的第二個資料行。</span><span class="sxs-lookup"><span data-stu-id="be43b-108">The query produces a new sequence in which the ID column appears first, followed by a second column that combines the student's first name and last name.</span></span> <span data-ttu-id="be43b-109">這些行會根據學號欄位重新排列。</span><span class="sxs-lookup"><span data-stu-id="be43b-109">The lines are reordered according to the ID field.</span></span> <span data-ttu-id="be43b-110">結果會儲存至新的檔案，而且不會修改原始資料。</span><span class="sxs-lookup"><span data-stu-id="be43b-110">The results are saved into a new file and the original data is not modified.</span></span>

### <a name="to-create-the-data-file"></a><span data-ttu-id="be43b-111">建立資料檔</span><span class="sxs-lookup"><span data-stu-id="be43b-111">To create the data file</span></span>

1. <span data-ttu-id="be43b-112">將下列幾行複製到名為 spreadsheet1.csv 的純文字檔。</span><span class="sxs-lookup"><span data-stu-id="be43b-112">Copy the following lines into a plain text file that is named spreadsheet1.csv.</span></span> <span data-ttu-id="be43b-113">將此檔案儲存在您的專案資料夾中。</span><span class="sxs-lookup"><span data-stu-id="be43b-113">Save the file in your project folder.</span></span>

    ```csv
    Adams,Terry,120
    Fakhouri,Fadi,116
    Feng,Hanying,117
    Garcia,Cesar,114
    Garcia,Debra,115
    Garcia,Hugo,118
    Mortensen,Sven,113
    O'Donnell,Claire,112
    Omelchenko,Svetlana,111
    Tucker,Lance,119
    Tucker,Michael,122
    Zabokritski,Eugene,121
    ```

## <a name="example"></a><span data-ttu-id="be43b-114">範例</span><span class="sxs-lookup"><span data-stu-id="be43b-114">Example</span></span>

```vb
Class CSVFiles

    Shared Sub Main()

        ' Create the IEnumerable data source.
        Dim lines As String() = System.IO.File.ReadAllLines("../../../spreadsheet1.csv")

        ' Execute the query. Put field 2 first, then
        ' reverse and combine fields 0 and 1 from the old field
        Dim lineQuery = From line In lines
                        Let x = line.Split(New Char() {","})
                        Order By x(2)
                        Select x(2) & ", " & (x(1) & " " & x(0))

        ' Execute the query and write out the new file. Note that WriteAllLines
        ' takes a string array, so ToArray is called on the query.
        System.IO.File.WriteAllLines("../../../spreadsheet2.csv", lineQuery.ToArray())

        ' Keep console window open in debug mode.
        Console.WriteLine("Spreadsheet2.csv written to disk. Press any key to exit")
        Console.ReadKey()
    End Sub
End Class
' Output to spreadsheet2.csv:
' 111, Svetlana Omelchenko
' 112, Claire O'Donnell
' 113, Sven Mortensen
' 114, Cesar Garcia
' 115, Debra Garcia
' 116, Fadi Fakhouri
' 117, Hanying Feng
' 118, Hugo Garcia
' 119, Lance Tucker
' 120, Terry Adams
' 121, Eugene Zabokritski
' 122, Michael Tucker
```

## <a name="see-also"></a><span data-ttu-id="be43b-115">另請參閱</span><span class="sxs-lookup"><span data-stu-id="be43b-115">See also</span></span>

- [<span data-ttu-id="be43b-116">LINQ 與字串 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="be43b-116">LINQ and Strings (Visual Basic)</span></span>](linq-and-strings.md)
- [<span data-ttu-id="be43b-117">LINQ 與檔案目錄 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="be43b-117">LINQ and File Directories (Visual Basic)</span></span>](linq-and-file-directories.md)
- [<span data-ttu-id="be43b-118">如何：從 CSV 檔案產生 XML</span><span class="sxs-lookup"><span data-stu-id="be43b-118">How to: Generate XML from CSV Files</span></span>](../../../../standard/linq/generate-xml-csv-files.md)
