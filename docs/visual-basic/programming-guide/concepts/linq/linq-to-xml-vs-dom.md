---
title: LINQ to XML 比較DOM
ms.date: 07/20/2015
ms.assetid: 18c36130-d598-40b7-9007-828232252978
ms.openlocfilehash: 5813ca410e3e2b1ec284681451d0c0cec6f5e393
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84389328"
---
# <a name="linq-to-xml-vs-dom-visual-basic"></a><span data-ttu-id="787ab-102">LINQ to XML 與 DOM 的比較（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="787ab-102">LINQ to XML vs. DOM (Visual Basic)</span></span>
<span data-ttu-id="787ab-103">本節描述 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 和目前主流的 XML 程式設計 API (也就是 W3C 文件物件模型 (DOM)) 之間的一些主要差異。</span><span class="sxs-lookup"><span data-stu-id="787ab-103">This section describes some key differences between [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] and the current predominant XML programming API, the W3C Document Object Model (DOM).</span></span>  
  
## <a name="new-ways-to-construct-xml-trees"></a><span data-ttu-id="787ab-104">建構 XML 樹狀的新方式</span><span class="sxs-lookup"><span data-stu-id="787ab-104">New Ways to Construct XML Trees</span></span>  
 <span data-ttu-id="787ab-105">在 W3C DOM 中，您可以從下往上建置 XML 樹狀；也就是說，您可以建立文件、建立項目，然後將項目加入到文件中。</span><span class="sxs-lookup"><span data-stu-id="787ab-105">In the W3C DOM, you build an XML tree from the bottom up; that is, you create a document, you create elements, and then you add the elements to the document.</span></span>  
  
 <span data-ttu-id="787ab-106">例如，以下是使用 Microsoft 的 DOM 實作 <xref:System.Xml.XmlDocument> 建立 XML 樹狀的典型方式：</span><span class="sxs-lookup"><span data-stu-id="787ab-106">For example, the following would be a typical way to create an XML tree using the Microsoft implementation of DOM, <xref:System.Xml.XmlDocument>:</span></span>  
  
```vb  
Dim doc As XmlDocument = New XmlDocument()  
Dim name As XmlElement = doc.CreateElement("Name")  
name.InnerText = "Patrick Hines"  
Dim phone1 As XmlElement = doc.CreateElement("Phone")  
phone1.SetAttribute("Type", "Home")  
phone1.InnerText = "206-555-0144"  
Dim phone2 As XmlElement = doc.CreateElement("Phone")  
phone2.SetAttribute("Type", "Work")  
phone2.InnerText = "425-555-0145"  
Dim street1 As XmlElement = doc.CreateElement("Street1")  
street1.InnerText = "123 Main St"  
Dim city As XmlElement = doc.CreateElement("City")  
city.InnerText = "Mercer Island"  
Dim state As XmlElement = doc.CreateElement("State")  
state.InnerText = "WA"  
Dim postal As XmlElement = doc.CreateElement("Postal")  
postal.InnerText = "68042"  
Dim address As XmlElement = doc.CreateElement("Address")  
address.AppendChild(street1)  
address.AppendChild(city)  
address.AppendChild(state)  
address.AppendChild(postal)  
Dim contact As XmlElement = doc.CreateElement("Contact")  
contact.AppendChild(name)  
contact.AppendChild(phone1)  
contact.AppendChild(phone2)  
contact.AppendChild(address)  
Dim contacts As XmlElement = doc.CreateElement("Contacts")  
contacts.AppendChild(contact)  
doc.AppendChild(contacts)  
Console.WriteLine(doc.OuterXml)  
```  
  
 <span data-ttu-id="787ab-107">這個編碼樣式在視覺上不會提供太多 XML 樹狀的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="787ab-107">This style of coding does not visually provide much information about the structure of the XML tree.</span></span> [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] <span data-ttu-id="787ab-108">支援使用這個方法來建構 XML 樹狀結構，但是也支援採用「功能建構」\*\* 的替代方法。</span><span class="sxs-lookup"><span data-stu-id="787ab-108">supports this approach to constructing an XML tree, but also supports an alternative approach, *functional construction*.</span></span> <span data-ttu-id="787ab-109">在 Visual Basic 中，功能結構會使用 XML 常值來建立 XML 樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="787ab-109">In Visual Basic, functional construction uses XML literals to build an XML tree.</span></span>  
  
 <span data-ttu-id="787ab-110">此處說明您如何使用 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 功能建構，來建構相同的 XML 樹狀結構：</span><span class="sxs-lookup"><span data-stu-id="787ab-110">Here is how you would construct the same XML tree by using [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] functional construction:</span></span>  
  
```vb  
Dim contacts = _  
    <Contacts>  
        <Contact>  
            <Name>Patrick Hines</Name>  
            <Phone Type="Home">206-555-0144</Phone>  
            <Phone Type="Work">425-555-0145</Phone>  
            <Address>  
                <Street1>123 Main St</Street1>  
                <City>Mercer Island</City>  
                <State>WA</State>  
                <Postal>68042</Postal>  
            </Address>  
        </Contact>  
    </Contacts>  
```  
  
 <span data-ttu-id="787ab-111">請注意，將要建構 XML 樹狀結構的程式碼縮排可顯示基礎 XML 的結構。</span><span class="sxs-lookup"><span data-stu-id="787ab-111">Notice that indenting the code to construct the XML tree shows the structure of the underlying XML.</span></span>  
  
 <span data-ttu-id="787ab-112">如需詳細資訊，請參閱[建立 XML 樹狀結構（Visual Basic）](creating-xml-trees.md)。</span><span class="sxs-lookup"><span data-stu-id="787ab-112">For more information, see [Creating XML Trees (Visual Basic)](creating-xml-trees.md).</span></span>  
  
## <a name="working-directly-with-xml-elements"></a><span data-ttu-id="787ab-113">直接使用 XML 項目</span><span class="sxs-lookup"><span data-stu-id="787ab-113">Working Directly with XML Elements</span></span>  
 <span data-ttu-id="787ab-114">當您使用 XML 進行程式設計時，您的主要焦點通常是 XML 項目，也可能是屬性。</span><span class="sxs-lookup"><span data-stu-id="787ab-114">When you program with XML, your primary focus is usually on XML elements and perhaps on attributes.</span></span> <span data-ttu-id="787ab-115">在 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 中，您可以直接使用 XML 項目和屬性。</span><span class="sxs-lookup"><span data-stu-id="787ab-115">In [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)], you can work directly with XML elements and attributes.</span></span> <span data-ttu-id="787ab-116">例如，您可以：</span><span class="sxs-lookup"><span data-stu-id="787ab-116">For example, you can do the following:</span></span>  
  
- <span data-ttu-id="787ab-117">完全不使用文件物件來建立 XML 項目。</span><span class="sxs-lookup"><span data-stu-id="787ab-117">Create XML elements without using a document object at all.</span></span> <span data-ttu-id="787ab-118">當您必須使用 XML 樹狀結構的片段時，這可以簡化程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="787ab-118">This simplifies programming when you have to work with fragments of XML trees.</span></span>  
  
- <span data-ttu-id="787ab-119">從 XML 檔案直接載入 `T:System.Xml.Linq.XElement` 物件。</span><span class="sxs-lookup"><span data-stu-id="787ab-119">Load `T:System.Xml.Linq.XElement` objects directly from an XML file.</span></span>  
  
- <span data-ttu-id="787ab-120">將 `T:System.Xml.Linq.XElement` 物件序列化為檔案或資料流。</span><span class="sxs-lookup"><span data-stu-id="787ab-120">Serialize `T:System.Xml.Linq.XElement` objects to a file or a stream.</span></span>  
  
 <span data-ttu-id="787ab-121">將這個 XML 項目或屬性與 W3C DOM 相比較，後者中的 XML 文件會當做 XML 樹狀結構的邏輯容器使用。</span><span class="sxs-lookup"><span data-stu-id="787ab-121">Compare this to the W3C DOM, in which the XML document is used as a logical container for the XML tree.</span></span> <span data-ttu-id="787ab-122">在 DOM 中，XML 節點 (包括項目和屬性) 必須在 XML 文件的內容中建立。</span><span class="sxs-lookup"><span data-stu-id="787ab-122">In DOM, XML nodes, including elements and attributes, must be created in the context of an XML document.</span></span> <span data-ttu-id="787ab-123">此處為要在 DOM 中建立名稱項目之節點的片段：</span><span class="sxs-lookup"><span data-stu-id="787ab-123">Here is a fragment of the code to create a name element in DOM:</span></span>  
  
```vb  
Dim doc As XmlDocument = New XmlDocument()  
Dim name As XmlElement = doc.CreateElement("Name")  
name.InnerText = "Patrick Hines"  
doc.AppendChild(name)  
```  
  
 <span data-ttu-id="787ab-124">如果您要跨多個文件使用同一個項目，您必須匯入跨這些文件的節點。</span><span class="sxs-lookup"><span data-stu-id="787ab-124">If you want to use an element across multiple documents, you must import the nodes across documents.</span></span> [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]<span data-ttu-id="787ab-125">可避免這層複雜度。</span><span class="sxs-lookup"><span data-stu-id="787ab-125">avoids this layer of complexity.</span></span>  
  
 <span data-ttu-id="787ab-126">使用 LINQ to XML 時，您僅能在想要於文件根層級上加入註解或處理指示時，才能使用 <xref:System.Xml.Linq.XDocument> 類別。</span><span class="sxs-lookup"><span data-stu-id="787ab-126">When using LINQ to XML, you use the <xref:System.Xml.Linq.XDocument> class only if you want to add a comment or processing instruction at the root level of the document.</span></span>  
  
## <a name="simplified-handling-of-names-and-namespaces"></a><span data-ttu-id="787ab-127">簡化的名稱和命名空間處理方式</span><span class="sxs-lookup"><span data-stu-id="787ab-127">Simplified Handling of Names and Namespaces</span></span>  
 <span data-ttu-id="787ab-128">名稱、命名空間和命名空間前置詞的處理通常是 XML 程式設計的複雜部分。</span><span class="sxs-lookup"><span data-stu-id="787ab-128">Handling names, namespaces, and namespace prefixes is generally a complex part of XML programming.</span></span> [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] <span data-ttu-id="787ab-129">不必處理命名空間前置詞，可簡化名稱和命名空間。</span><span class="sxs-lookup"><span data-stu-id="787ab-129">simplifies names and namespaces by eliminating the requirement to deal with namespace prefixes.</span></span> <span data-ttu-id="787ab-130">您也可以控制命名空間前置詞。</span><span class="sxs-lookup"><span data-stu-id="787ab-130">If you want to control namespace prefixes, you can.</span></span> <span data-ttu-id="787ab-131">但是，如果您決定不明確控制命名空間前置詞，則在序列化期間，[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 會指派命名空間前置詞 (如有必要)，或使用預設的命名空間進行序列化 (如果非必要的話)。</span><span class="sxs-lookup"><span data-stu-id="787ab-131">But if you decide to not explicitly control namespace prefixes, [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] will assign namespace prefixes during serialization if they are required, or will serialize using default namespaces if they are not.</span></span> <span data-ttu-id="787ab-132">如果使用預設的命名空間，在產生的文件中將不會有任何命名空間前置詞。</span><span class="sxs-lookup"><span data-stu-id="787ab-132">If default namespaces are used, there will be no namespace prefixes in the resulting document.</span></span> <span data-ttu-id="787ab-133">如需詳細資訊，請參閱[命名空間總覽（LINQ to XML）（Visual Basic）](namespaces-overview-linq-to-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="787ab-133">For more information, see [Namespaces Overview (LINQ to XML) (Visual Basic)](namespaces-overview-linq-to-xml.md).</span></span>  
  
 <span data-ttu-id="787ab-134">另一個 DOM 問題是，DOM 不會讓您變更節點的名稱，</span><span class="sxs-lookup"><span data-stu-id="787ab-134">Another problem with the DOM is that it does not let you change the name of a node.</span></span> <span data-ttu-id="787ab-135">而是必須建立新的節點，並將所有子節點複製到該節點中，因此會失去原始的節點識別。</span><span class="sxs-lookup"><span data-stu-id="787ab-135">Instead, you have to create a new node and copy all the child nodes to it, losing the original node identity.</span></span> [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] <span data-ttu-id="787ab-136">會讓您在節點上設定 <xref:System.Xml.Linq.XName> 屬性，藉以避免這個問題。</span><span class="sxs-lookup"><span data-stu-id="787ab-136">avoids this problem by enabling you to set the <xref:System.Xml.Linq.XName> property on a node.</span></span>  
  
## <a name="static-method-support-for-loading-xml"></a><span data-ttu-id="787ab-137">載入 XML 的靜態方法支援</span><span class="sxs-lookup"><span data-stu-id="787ab-137">Static Method Support for Loading XML</span></span>  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] <span data-ttu-id="787ab-138">可讓您使用靜態方法 (而非執行個體方法) 來載入 XML。</span><span class="sxs-lookup"><span data-stu-id="787ab-138">lets you load XML by using static methods, instead of instance methods.</span></span> <span data-ttu-id="787ab-139">這會簡化載入和剖析的程序。</span><span class="sxs-lookup"><span data-stu-id="787ab-139">This simplifies loading and parsing.</span></span> <span data-ttu-id="787ab-140">如需詳細資訊，請參閱[如何：從檔案載入 XML （Visual Basic）](how-to-load-xml-from-a-file.md)。</span><span class="sxs-lookup"><span data-stu-id="787ab-140">For more information, see [How to: Load XML from a File (Visual Basic)](how-to-load-xml-from-a-file.md).</span></span>  
  
## <a name="removal-of-support-for-dtd-constructs"></a><span data-ttu-id="787ab-141">移除 DTD 建構函式的支援</span><span class="sxs-lookup"><span data-stu-id="787ab-141">Removal of Support for DTD Constructs</span></span>  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] <span data-ttu-id="787ab-142">會移除實體和實體參考的支援，進一步簡化 XML 程式設計。</span><span class="sxs-lookup"><span data-stu-id="787ab-142">further simplifies XML programming by removing support for entities and entity references.</span></span> <span data-ttu-id="787ab-143">實體的管理很複雜，而且不常使用。</span><span class="sxs-lookup"><span data-stu-id="787ab-143">The management of entities is complex, and is rarely used.</span></span> <span data-ttu-id="787ab-144">移除這些支援會增進效能並簡化程式設計介面。</span><span class="sxs-lookup"><span data-stu-id="787ab-144">Removing their support increases performance and simplifies the programming interface.</span></span> <span data-ttu-id="787ab-145">填入 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 樹狀結構時，系統會展開所有 DTD 實體。</span><span class="sxs-lookup"><span data-stu-id="787ab-145">When a [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] tree is populated, all DTD entities are expanded.</span></span>  
  
## <a name="support-for-fragments"></a><span data-ttu-id="787ab-146">支援片段</span><span class="sxs-lookup"><span data-stu-id="787ab-146">Support for Fragments</span></span>  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] <span data-ttu-id="787ab-147">不提供 `XmlDocumentFragment` 類別的對等類別。</span><span class="sxs-lookup"><span data-stu-id="787ab-147">does not provide an equivalent for the `XmlDocumentFragment` class.</span></span> <span data-ttu-id="787ab-148">在許多情況下，`XmlDocumentFragment` 概念可藉由查詢結果來處理，該查詢的類型為 <xref:System.Xml.Linq.XNode> 的 <xref:System.Collections.Generic.IEnumerable%601> 或 <xref:System.Xml.Linq.XElement> 的 <xref:System.Collections.Generic.IEnumerable%601>。</span><span class="sxs-lookup"><span data-stu-id="787ab-148">In many cases, however, the `XmlDocumentFragment` concept can be handled by the result of a query that is typed as <xref:System.Collections.Generic.IEnumerable%601> of <xref:System.Xml.Linq.XNode>, or <xref:System.Collections.Generic.IEnumerable%601> of <xref:System.Xml.Linq.XElement>.</span></span>  
  
## <a name="support-for-xpathnavigator"></a><span data-ttu-id="787ab-149">支援 XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="787ab-149">Support for XPathNavigator</span></span>  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] <span data-ttu-id="787ab-150">透過 <xref:System.Xml.XPath?displayProperty=nameWithType> 命名空間中的擴充方法，提供 <xref:System.Xml.XPath.XPathNavigator> 的支援。</span><span class="sxs-lookup"><span data-stu-id="787ab-150">provides support for <xref:System.Xml.XPath.XPathNavigator> through extension methods in the <xref:System.Xml.XPath?displayProperty=nameWithType> namespace.</span></span> <span data-ttu-id="787ab-151">如需詳細資訊，請參閱 <xref:System.Xml.XPath.Extensions?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="787ab-151">For more information, see <xref:System.Xml.XPath.Extensions?displayProperty=nameWithType>.</span></span>  
  
## <a name="support-for-white-space-and-indentation"></a><span data-ttu-id="787ab-152">支援空白字元與縮排</span><span class="sxs-lookup"><span data-stu-id="787ab-152">Support for White Space and Indentation</span></span>  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] <span data-ttu-id="787ab-153">處理空白字元時，比處理 DOM 更為容易。</span><span class="sxs-lookup"><span data-stu-id="787ab-153">handles white space more simply than the DOM.</span></span>  
  
 <span data-ttu-id="787ab-154">常見的案例為讀取縮排的 XML、建立沒有任何空白字元文字節點 (也就是不保留空白字元) 的記憶體中 XML 樹狀結構、在 XML 上執行某些作業，然後儲存包含縮排的 XML。</span><span class="sxs-lookup"><span data-stu-id="787ab-154">A common scenario is to read indented XML, create an in-memory XML tree without any white space text nodes (that is, not preserving white space), perform some operations on the XML, and then save the XML with indentation.</span></span> <span data-ttu-id="787ab-155">當您序列化具有格式的 XML 時，只會保留 XML 樹狀結構中的有效空白字元。</span><span class="sxs-lookup"><span data-stu-id="787ab-155">When you serialize the XML with formatting, only significant white space in the XML tree is preserved.</span></span> <span data-ttu-id="787ab-156">這是 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 的預設行為。</span><span class="sxs-lookup"><span data-stu-id="787ab-156">This is the default behavior for [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)].</span></span>  
  
 <span data-ttu-id="787ab-157">其他常見案例為讀取與修改已經過刻意縮排的 XML。</span><span class="sxs-lookup"><span data-stu-id="787ab-157">Another common scenario is to read and modify XML that has already been intentionally indented.</span></span> <span data-ttu-id="787ab-158">您可能不想用任何方式變更這個縮排。</span><span class="sxs-lookup"><span data-stu-id="787ab-158">You might not want to change this indentation in any way.</span></span> <span data-ttu-id="787ab-159">在 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 中，如果您在載入或剖析 XML 時保留空白字元，並在序列化 XML 時停用格式化，您就可以達到這個效果。</span><span class="sxs-lookup"><span data-stu-id="787ab-159">In [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)], you can do this by preserving white space when you load or parse the XML and disabling formatting when you serialize the XML.</span></span>  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] <span data-ttu-id="787ab-160">會將空白字元儲存為 <xref:System.Xml.Linq.XText> 節點，而不是像 DOM 儲存為序列化的 <xref:System.Xml.XmlNodeType.Whitespace> 節點類型。</span><span class="sxs-lookup"><span data-stu-id="787ab-160">stores white space as an <xref:System.Xml.Linq.XText> node, instead of having a specialized <xref:System.Xml.XmlNodeType.Whitespace> node type, as the DOM does.</span></span>  
  
## <a name="support-for-annotations"></a><span data-ttu-id="787ab-161">支援附註</span><span class="sxs-lookup"><span data-stu-id="787ab-161">Support for Annotations</span></span>  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] <span data-ttu-id="787ab-162">項目支援一組可延伸的附註。</span><span class="sxs-lookup"><span data-stu-id="787ab-162">elements support an extensible set of annotations.</span></span> <span data-ttu-id="787ab-163">這在追蹤項目的其他資訊 (例如，結構描述資訊)、項目是否繫結至 UI 的相關資訊，或任何種類的應用程式專屬資訊時，相當實用。</span><span class="sxs-lookup"><span data-stu-id="787ab-163">This is useful for tracking miscellaneous information about an element, such as schema information, information about whether the element is bound to a UI, or any other kind of application-specific information.</span></span> <span data-ttu-id="787ab-164">如需詳細資訊，請參閱 [LINQ to XML 註釋](linq-to-xml-annotations.md)。</span><span class="sxs-lookup"><span data-stu-id="787ab-164">For more information, see [LINQ to XML Annotations](linq-to-xml-annotations.md).</span></span>  
  
## <a name="support-for-schema-information"></a><span data-ttu-id="787ab-165">支援結構描述資訊</span><span class="sxs-lookup"><span data-stu-id="787ab-165">Support for Schema Information</span></span>  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] <span data-ttu-id="787ab-166">透過 <xref:System.Xml.Schema?displayProperty=nameWithType> 命名空間中的擴充方法，提供 XSD 驗證支援。</span><span class="sxs-lookup"><span data-stu-id="787ab-166">provides support for XSD validation through extension methods in the <xref:System.Xml.Schema?displayProperty=nameWithType> namespace.</span></span> <span data-ttu-id="787ab-167">您可以驗證 XML 樹狀是以 XSD 編譯。</span><span class="sxs-lookup"><span data-stu-id="787ab-167">You can validate that an XML tree complies with an XSD.</span></span> <span data-ttu-id="787ab-168">您可以利用 Post-Schema-Validation Infoset (PSVI) 填入 XML 樹狀。</span><span class="sxs-lookup"><span data-stu-id="787ab-168">You can populate the XML tree with the post-schema-validation infoset (PSVI).</span></span> <span data-ttu-id="787ab-169">如需詳細資訊，請參閱[如何：使用 XSD 進行驗證](how-to-validate-using-xsd-linq-to-xml.md)和<xref:System.Xml.Schema.Extensions>。</span><span class="sxs-lookup"><span data-stu-id="787ab-169">For more information, see [How to: Validate Using XSD](how-to-validate-using-xsd-linq-to-xml.md) and <xref:System.Xml.Schema.Extensions>.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="787ab-170">另請參閱</span><span class="sxs-lookup"><span data-stu-id="787ab-170">See also</span></span>

- [<span data-ttu-id="787ab-171">使用者入門 (LINQ to XML)</span><span class="sxs-lookup"><span data-stu-id="787ab-171">Getting Started (LINQ to XML)</span></span>](getting-started-linq-to-xml.md)
