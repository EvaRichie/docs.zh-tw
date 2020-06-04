---
title: 作法：查詢包含指定詞組的句子 (LINQ)
ms.date: 07/20/2015
ms.assetid: a5ae8ced-61fe-4c10-bb8a-95630e50f603
ms.openlocfilehash: ce88bf001346f90eb9b08ca1ff14afc7dcb04fa0
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397956"
---
# <a name="how-to-query-for-sentences-that-contain-a-specified-set-of-words-linq-visual-basic"></a><span data-ttu-id="0e65f-102">如何：查詢包含指定字組的句子 (LINQ) (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="0e65f-102">How to: Query for Sentences that Contain a Specified Set of Words (LINQ) (Visual Basic)</span></span>

<span data-ttu-id="0e65f-103">此範例示範如何在文字檔中尋找含有每個指定字組之相符項目的句子。</span><span class="sxs-lookup"><span data-stu-id="0e65f-103">This example shows how to find sentences in a text file that contain matches for each of a specified set of words.</span></span> <span data-ttu-id="0e65f-104">雖然此範例硬式編碼了搜尋字詞的陣列，但也可以在執行階段將它動態填入。</span><span class="sxs-lookup"><span data-stu-id="0e65f-104">Although the array of search terms is hard-coded in this example, it could also be populated dynamically at runtime.</span></span> <span data-ttu-id="0e65f-105">在此範例中，查詢會傳回包含 "Historically"、"data" 和 "integrated" 等字的句子。</span><span class="sxs-lookup"><span data-stu-id="0e65f-105">In this example, the query returns the sentences that contain the words "Historically," "data," and "integrated."</span></span>

## <a name="example"></a><span data-ttu-id="0e65f-106">範例</span><span class="sxs-lookup"><span data-stu-id="0e65f-106">Example</span></span>

```vb
Class FindSentences

    Shared Sub Main()
        Dim text As String = "Historically, the world of data and the world of objects " &
        "have not been well integrated. Programmers work in C# or Visual Basic " &
        "and also in SQL or XQuery. On the one side are concepts such as classes, " &
        "objects, fields, inheritance, and .NET Framework APIs. On the other side " &
        "are tables, columns, rows, nodes, and separate languages for dealing with " &
        "them. Data types often require translation between the two worlds; there are " &
        "different standard functions. Because the object world has no notion of query, a " &
        "query can only be represented as a string without compile-time type checking or " &
        "IntelliSense support in the IDE. Transferring data from SQL tables or XML trees to " &
        "objects in memory is often tedious and error-prone."

        ' Split the text block into an array of sentences.
        Dim sentences As String() = text.Split(New Char() {".", "?", "!"})

        ' Define the search terms. This list could also be dynamically populated at runtime
        Dim wordsToMatch As String() = {"Historically", "data", "integrated"}

        ' Find sentences that contain all the terms in the wordsToMatch array
        ' Note that the number of terms to match is not specified at compile time
        Dim sentenceQuery = From sentence In sentences
                            Let w = sentence.Split(New Char() {" ", ",", ".", ";", ":"},
                                                   StringSplitOptions.RemoveEmptyEntries)
                            Where w.Distinct().Intersect(wordsToMatch).Count = wordsToMatch.Count()
                            Select sentence

        ' Execute the query
        For Each str As String In sentenceQuery
            Console.WriteLine(str)
        Next

        ' Keep console window open in debug mode.
        Console.WriteLine("Press any key to exit.")
        Console.ReadKey()
    End Sub

End Class
' Output:
' Historically, the world of data and the world of objects have not been well integrated
```

<span data-ttu-id="0e65f-107">查詢的運作方式是先將文字分割成句子，然後將句子分割成包含每個字的字串陣列。</span><span class="sxs-lookup"><span data-stu-id="0e65f-107">The query works by first splitting the text into sentences, and then splitting the sentences into an array of strings that hold each word.</span></span> <span data-ttu-id="0e65f-108">對於每個陣列，<xref:System.Linq.Enumerable.Distinct%2A> 方法會移除所有重複的字組，接著查詢會對字組陣列和 `wordsToMatch` 陣列執行 <xref:System.Linq.Enumerable.Intersect%2A> 作業。</span><span class="sxs-lookup"><span data-stu-id="0e65f-108">For each of these arrays, the <xref:System.Linq.Enumerable.Distinct%2A> method removes all duplicate words, and then the query performs an <xref:System.Linq.Enumerable.Intersect%2A> operation on the word array and the `wordsToMatch` array.</span></span> <span data-ttu-id="0e65f-109">如果交集的計數與 `wordsToMatch` 陣列的計數相同，則所有字都可以在字組中找到，因而傳回原始句子。</span><span class="sxs-lookup"><span data-stu-id="0e65f-109">If the count of the intersection is the same as the count of the `wordsToMatch` array, all words were found in the words and the original sentence is returned.</span></span>

<span data-ttu-id="0e65f-110">在 <xref:System.String.Split%2A> 呼叫中，標點符號會當成分隔符號，以便從字串中移除。</span><span class="sxs-lookup"><span data-stu-id="0e65f-110">In the call to <xref:System.String.Split%2A>, the punctuation marks are used as separators in order to remove them from the string.</span></span> <span data-ttu-id="0e65f-111">如果您不這麼做，則您的字串 "Historically," 與 `wordsToMatch` 陣列中的 "Historically" 不符。</span><span class="sxs-lookup"><span data-stu-id="0e65f-111">If you did not do this, for example you could have a string "Historically," that would not match "Historically" in the `wordsToMatch` array.</span></span> <span data-ttu-id="0e65f-112">根據來源文字中找到的標點符號類型，您可能必須使用其他分隔符號。</span><span class="sxs-lookup"><span data-stu-id="0e65f-112">You may have to use additional separators, depending on the types of punctuation found in the source text.</span></span>

## <a name="compile-the-code"></a><span data-ttu-id="0e65f-113">編譯程式碼</span><span class="sxs-lookup"><span data-stu-id="0e65f-113">Compile the code</span></span>

<span data-ttu-id="0e65f-114">建立 Visual Basic 的主控台應用程式專案，其中包含 `Imports` System. Linq 命名空間的語句。</span><span class="sxs-lookup"><span data-stu-id="0e65f-114">Create a Visual Basic console application project, with an `Imports` statement for the System.Linq namespace.</span></span>

## <a name="see-also"></a><span data-ttu-id="0e65f-115">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0e65f-115">See also</span></span>

- [<span data-ttu-id="0e65f-116">LINQ 與字串 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="0e65f-116">LINQ and Strings (Visual Basic)</span></span>](linq-and-strings.md)
