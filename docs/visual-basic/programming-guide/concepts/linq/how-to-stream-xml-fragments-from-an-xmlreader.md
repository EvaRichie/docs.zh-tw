---
title: 作法：從 XmlReader 串流 XML 片段
ms.date: 07/20/2015
ms.assetid: f67ce598-4a12-4dcb-9a07-24deca02a111
ms.openlocfilehash: ff22625767c4e0752ca19d5a315395934b566230
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397696"
---
# <a name="how-to-stream-xml-fragments-from-an-xmlreader-visual-basic"></a><span data-ttu-id="d2892-102">如何：從 XmlReader 串流 XML 片段（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="d2892-102">How to: Stream XML Fragments from an XmlReader (Visual Basic)</span></span>
<span data-ttu-id="d2892-103">當您必須處理大型 XML 檔案時，可能無法將整個 XML 樹狀載入記憶體中。</span><span class="sxs-lookup"><span data-stu-id="d2892-103">When you have to process large XML files, it might not be feasible to load the whole XML tree into memory.</span></span> <span data-ttu-id="d2892-104">這個主題顯示如何使用 <xref:System.Xml.XmlReader> 串流片段。</span><span class="sxs-lookup"><span data-stu-id="d2892-104">This topic shows how to stream fragments using an <xref:System.Xml.XmlReader>.</span></span>  
  
 <span data-ttu-id="d2892-105">使用 <xref:System.Xml.XmlReader> 讀取 <xref:System.Xml.Linq.XElement> 物件的其中一個最有效方式為，撰寫您自己自訂的座標軸方法。</span><span class="sxs-lookup"><span data-stu-id="d2892-105">One of the most effective ways to use an <xref:System.Xml.XmlReader> to read <xref:System.Xml.Linq.XElement> objects is to write your own custom axis method.</span></span> <span data-ttu-id="d2892-106">座標軸方法通常會傳回集合，例如，<xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Xml.Linq.XElement>，如本主題的範例中所示。</span><span class="sxs-lookup"><span data-stu-id="d2892-106">An axis method typically returns a collection such as <xref:System.Collections.Generic.IEnumerable%601> of <xref:System.Xml.Linq.XElement>, as shown in the example in this topic.</span></span> <span data-ttu-id="d2892-107">在自訂座標軸方法中，呼叫 <xref:System.Xml.Linq.XNode.ReadFrom%2A> 方法來建立 XML 片段後，使用 `yield return` 傳回集合。</span><span class="sxs-lookup"><span data-stu-id="d2892-107">In the custom axis method, after you create the XML fragment by calling the <xref:System.Xml.Linq.XNode.ReadFrom%2A> method, return the collection using `yield return`.</span></span> <span data-ttu-id="d2892-108">這會將延後執行語意 (Semantics) 提供給您自訂的座標軸方法。</span><span class="sxs-lookup"><span data-stu-id="d2892-108">This provides deferred execution semantics to your custom axis method.</span></span>  
  
 <span data-ttu-id="d2892-109">當您從 <xref:System.Xml.XmlReader> 物件建立 XML 樹狀結構時，<xref:System.Xml.XmlReader> 必須定位在項目上。</span><span class="sxs-lookup"><span data-stu-id="d2892-109">When you create an XML tree from an <xref:System.Xml.XmlReader> object, the <xref:System.Xml.XmlReader> must be positioned on an element.</span></span> <span data-ttu-id="d2892-110"><xref:System.Xml.Linq.XNode.ReadFrom%2A> 方法在讀取項目的關閉標記前不會傳回。</span><span class="sxs-lookup"><span data-stu-id="d2892-110">The <xref:System.Xml.Linq.XNode.ReadFrom%2A> method does not return until it has read the close tag of the element.</span></span>  
  
 <span data-ttu-id="d2892-111">如果您要建立部分樹狀結構，您可以具現化 <xref:System.Xml.XmlReader>、將讀取器定位在您要轉換為 <xref:System.Xml.Linq.XElement> 樹狀結構的節點上，然後建立 <xref:System.Xml.Linq.XElement> 物件。</span><span class="sxs-lookup"><span data-stu-id="d2892-111">If you want to create a partial tree, you can instantiate an <xref:System.Xml.XmlReader>, position the reader on the node that you want to convert to an <xref:System.Xml.Linq.XElement> tree, and then create the <xref:System.Xml.Linq.XElement> object.</span></span>  
  
 <span data-ttu-id="d2892-112">[如何：串流 XML 片段並存取標頭資訊（Visual Basic）](how-to-stream-xml-fragments-with-access-to-header-information.md)主題包含如何串流更複雜檔的資訊和範例。</span><span class="sxs-lookup"><span data-stu-id="d2892-112">The topic [How to: Stream XML Fragments with Access to Header Information (Visual Basic)](how-to-stream-xml-fragments-with-access-to-header-information.md) contains information and an example on how to stream a more complex document.</span></span>  
  
 <span data-ttu-id="d2892-113">[如何：執行大型 XML 檔的資料流程轉換（Visual Basic）](how-to-perform-streaming-transform-of-large-xml-documents.md)主題包含使用 LINQ to XML 轉換非常大的 xml 檔，同時維持小型記憶體使用量的範例。</span><span class="sxs-lookup"><span data-stu-id="d2892-113">The topic [How to: Perform Streaming Transform of Large XML Documents (Visual Basic)](how-to-perform-streaming-transform-of-large-xml-documents.md) contains an example of using LINQ to XML to transform extremely large XML documents while maintaining a small memory footprint.</span></span>  
  
## <a name="example"></a><span data-ttu-id="d2892-114">範例</span><span class="sxs-lookup"><span data-stu-id="d2892-114">Example</span></span>  
 <span data-ttu-id="d2892-115">這個範例會建立自訂座標軸方法。</span><span class="sxs-lookup"><span data-stu-id="d2892-115">This example creates a custom axis method.</span></span> <span data-ttu-id="d2892-116">您可以使用 LINQ 查詢來查詢它。</span><span class="sxs-lookup"><span data-stu-id="d2892-116">You can query it by using a LINQ query.</span></span> <span data-ttu-id="d2892-117">自訂座標軸方法  `StreamRootChildDoc` 是一種方法，特別針對讀取具有重複 `Child` 項目的文件而設計。</span><span class="sxs-lookup"><span data-stu-id="d2892-117">The custom axis method, `StreamRootChildDoc`, is a method that is designed specifically to read a document that has a repeating `Child` element.</span></span>  
  
```vb  
Module Module1  
    Sub Main()  
        Dim markup = "<Root>" &  
                     "  <Child Key=""01"">" &  
                     "    <GrandChild>aaa</GrandChild>" &  
                     "  </Child>" &  
                     "  <Child Key=""02"">" &  
                     "    <GrandChild>bbb</GrandChild>" &  
                     "  </Child>" &  
                     "  <Child Key=""03"">" &  
                     "    <GrandChild>ccc</GrandChild>" &  
                     "  </Child>" &  
                     "</Root>"  
  
        Dim grandChildData =  
             From el In New StreamRootChildDoc(New IO.StringReader(markup))  
             Where CInt(el.@Key) > 1  
             Select el.<GrandChild>.Value  
  
        For Each s In grandChildData  
            Console.WriteLine(s)  
        Next  
    End Sub  
End Module  
  
Public Class StreamRootChildDoc  
    Implements IEnumerable(Of XElement)  
  
    Private _stringReader As IO.StringReader  
  
    Public Sub New(ByVal stringReader As IO.StringReader)  
        _stringReader = stringReader  
    End Sub  
  
    Public Function GetEnumerator() As IEnumerator(Of XElement) Implements IEnumerable(Of XElement).GetEnumerator  
        Return New StreamChildEnumerator(_stringReader)  
    End Function  
  
    Public Function GetEnumerator1() As IEnumerator Implements IEnumerable.GetEnumerator  
        Return Me.GetEnumerator()  
    End Function  
End Class  
  
Public Class StreamChildEnumerator  
    Implements IEnumerator(Of XElement)  
  
    Private _current As XElement  
    Private _reader As Xml.XmlReader  
    Private _stringReader As IO.StringReader  
  
    Public Sub New(ByVal stringReader As IO.StringReader)  
        _stringReader = stringReader  
        _reader = Xml.XmlReader.Create(_stringReader)  
        _reader.MoveToContent()  
    End Sub  
  
    Public ReadOnly Property Current As XElement Implements IEnumerator(Of XElement).Current  
        Get  
            Return _current  
        End Get  
    End Property  
  
    Public ReadOnly Property Current1 As Object Implements IEnumerator.Current  
        Get  
            Return Me.Current  
        End Get  
    End Property  
  
    Public Function MoveNext() As Boolean Implements IEnumerator.MoveNext  
        While _reader.Read()  
            Select Case _reader.NodeType  
                Case Xml.XmlNodeType.Element  
                    Dim el = TryCast(XElement.ReadFrom(_reader), XElement)  
                    If el IsNot Nothing Then  
                        _current = el  
                        Return True  
                    End If  
            End Select  
        End While  
  
        Return False  
    End Function  
  
    Public Sub Reset() Implements IEnumerator.Reset  
        _reader = Xml.XmlReader.Create(_stringReader)  
        _reader.MoveToContent()  
    End Sub  
  
#Region "IDisposable Support"  
    Private disposedValue As Boolean ' To detect redundant calls  
  
    ' IDisposable  
    Protected Overridable Sub Dispose(ByVal disposing As Boolean)  
        If Not Me.disposedValue Then  
            If disposing Then  
                _reader.Close()  
            End If  
        End If  
        Me.disposedValue = True  
    End Sub  
  
    Public Sub Dispose() Implements IDisposable.Dispose  
        Dispose(True)  
        GC.SuppressFinalize(Me)  
    End Sub  
#End Region  
  
End Class  
```  
  
 <span data-ttu-id="d2892-118">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="d2892-118">This example produces the following output:</span></span>  
  
```console  
bbb  
ccc  
```  
  
 <span data-ttu-id="d2892-119">在此範例中，來源文件很小。</span><span class="sxs-lookup"><span data-stu-id="d2892-119">In this example, the source document is very small.</span></span> <span data-ttu-id="d2892-120">但是，即使有數百萬的 `Child` 元素，此範例的記憶體使用量還是很小。</span><span class="sxs-lookup"><span data-stu-id="d2892-120">However, even if there were millions of `Child` elements, this example would still have a small memory footprint.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d2892-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d2892-121">See also</span></span>

- [<span data-ttu-id="d2892-122">逐步解說：在 Visual Basic 中實作 IEnumerable(Of T)</span><span class="sxs-lookup"><span data-stu-id="d2892-122">Walkthrough: Implementing IEnumerable(Of T) in Visual Basic</span></span>](../../language-features/control-flow/walkthrough-implementing-ienumerable-of-t.md)
- [<span data-ttu-id="d2892-123">剖析 XML （Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="d2892-123">Parsing XML (Visual Basic)</span></span>](parsing-xml.md)
