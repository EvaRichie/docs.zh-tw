---
title: 在 Serializing2 時保留空白字元
ms.date: 07/20/2015
ms.assetid: 2d7abbd4-37f4-422b-89dd-0a694b5edc17
ms.openlocfilehash: e9b73089830bf7e6cb0ea9e469bf667f12c571d8
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396398"
---
# <a name="preserving-white-space-while-serializing"></a><span data-ttu-id="a04c1-102">序列化時保留空白字元</span><span class="sxs-lookup"><span data-stu-id="a04c1-102">Preserving White Space While Serializing</span></span>
<span data-ttu-id="a04c1-103">本主題描述如何在序列化 XML 樹狀結構時控制空白字元。</span><span class="sxs-lookup"><span data-stu-id="a04c1-103">This topic describes how to control white space when serializing an XML tree.</span></span>  
  
 <span data-ttu-id="a04c1-104">常見的案例為讀取縮排的 XML、建立沒有任何空白字元文字節點 (也就是不保留空白字元) 的記憶體中 XML 樹狀結構、在 XML 上執行某些作業，然後儲存包含縮排的 XML。</span><span class="sxs-lookup"><span data-stu-id="a04c1-104">A common scenario is to read indented XML, create an in-memory XML tree without any white space text nodes (that is, not preserving white space), perform some operations on the XML, and then save the XML with indentation.</span></span> <span data-ttu-id="a04c1-105">當您序列化具有格式的 XML 時，只會保留 XML 樹狀結構中的有效空白字元。</span><span class="sxs-lookup"><span data-stu-id="a04c1-105">When you serialize the XML with formatting, only significant white space in the XML tree is preserved.</span></span> <span data-ttu-id="a04c1-106">這是 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 的預設行為。</span><span class="sxs-lookup"><span data-stu-id="a04c1-106">This is the default behavior for [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)].</span></span>  
  
 <span data-ttu-id="a04c1-107">其他常見案例為讀取與修改已經過刻意縮排的 XML。</span><span class="sxs-lookup"><span data-stu-id="a04c1-107">Another common scenario is to read and modify XML that has already been intentionally indented.</span></span> <span data-ttu-id="a04c1-108">您可能不想用任何方式變更這個縮排。</span><span class="sxs-lookup"><span data-stu-id="a04c1-108">You might not want to change this indentation in any way.</span></span> <span data-ttu-id="a04c1-109">在 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 中，如果您在載入或剖析 XML 時保留空白字元，並在序列化 XML 時停用格式化，就可以達到這個效果。</span><span class="sxs-lookup"><span data-stu-id="a04c1-109">To do this in [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)], you preserve white space when you load or parse the XML and disable formatting when you serialize the XML.</span></span>  
  
## <a name="white-space-behavior-of-methods-that-serialize-xml-trees"></a><span data-ttu-id="a04c1-110">序列化 XML 樹狀結構之方法的空白字元行為</span><span class="sxs-lookup"><span data-stu-id="a04c1-110">White Space Behavior of Methods that Serialize XML Trees</span></span>  
 <span data-ttu-id="a04c1-111">下列 <xref:System.Xml.Linq.XElement> 和 <xref:System.Xml.Linq.XDocument> 類別中的方法會序列化 XML 樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="a04c1-111">The following methods in the <xref:System.Xml.Linq.XElement> and <xref:System.Xml.Linq.XDocument> classes serialize an XML tree.</span></span> <span data-ttu-id="a04c1-112">您可以將 XML 樹狀結構序列化至檔案、<xref:System.IO.TextReader> 或 <xref:System.Xml.XmlReader>。</span><span class="sxs-lookup"><span data-stu-id="a04c1-112">You can serialize an XML tree to a file, a <xref:System.IO.TextReader>, or an <xref:System.Xml.XmlReader>.</span></span> <span data-ttu-id="a04c1-113">`ToString` 方法會序列化至字串。</span><span class="sxs-lookup"><span data-stu-id="a04c1-113">The `ToString` method serializes to a string.</span></span>  
  
- <xref:System.Xml.Linq.XElement.Save%2A?displayProperty=nameWithType>  
  
- <xref:System.Xml.Linq.XDocument.Save%2A?displayProperty=nameWithType>  
  
- [<span data-ttu-id="a04c1-114">XElement.ToString()</span><span class="sxs-lookup"><span data-stu-id="a04c1-114">XElement.ToString()</span></span>](xref:System.Xml.Linq.XNode.ToString%2A?displayProperty=nameWithType)
  
- [<span data-ttu-id="a04c1-115">XDocument.ToString()</span><span class="sxs-lookup"><span data-stu-id="a04c1-115">XDocument.ToString()</span></span>](xref:System.Xml.Linq.XNode.ToString%2A?displayProperty=nameWithType)
  
 <span data-ttu-id="a04c1-116">如果此方法不採用 <xref:System.Xml.Linq.SaveOptions> 當做引數，該方法將會格式化 (縮排) 序列化的 XML。</span><span class="sxs-lookup"><span data-stu-id="a04c1-116">If the method does not take <xref:System.Xml.Linq.SaveOptions> as an argument, then the method will format (indent) the serialized XML.</span></span> <span data-ttu-id="a04c1-117">在此情況下，會宣告 XML 樹狀結構中的所有有效空白字元。</span><span class="sxs-lookup"><span data-stu-id="a04c1-117">In this case, all insignificant white space in the XML tree is discarded.</span></span>  
  
 <span data-ttu-id="a04c1-118">如果此方法採用 <xref:System.Xml.Linq.SaveOptions> 當做引數，您就可以指定該方法不格式化 (縮排) 序列化的 XML。</span><span class="sxs-lookup"><span data-stu-id="a04c1-118">If the method does take <xref:System.Xml.Linq.SaveOptions> as an argument, then you can specify that the method not format (indent) the serialized XML.</span></span> <span data-ttu-id="a04c1-119">在此情況下，會保留 XML 樹狀中的所有空白字元。</span><span class="sxs-lookup"><span data-stu-id="a04c1-119">In this case, all white space in the XML tree is preserved.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a04c1-120">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a04c1-120">See also</span></span>

- [<span data-ttu-id="a04c1-121">序列化 XML 樹狀結構（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="a04c1-121">Serializing XML Trees (Visual Basic)</span></span>](serializing-xml-trees.md)
