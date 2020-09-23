---
title: 序列化
ms.date: 07/20/2015
ms.assetid: 67379a76-5465-4af8-a781-0b0b25a62d9a
ms.openlocfilehash: 98400c9e7ed9e26a9dc6ca548988c3691bfecdc2
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91086500"
---
# <a name="serialization-visual-basic"></a><span data-ttu-id="f46c9-102">序列化 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="f46c9-102">Serialization (Visual Basic)</span></span>

<span data-ttu-id="f46c9-103">序列化程序會將物件轉換成位元組資料流，以將物件儲存或傳輸到記憶體、資料庫或檔案。</span><span class="sxs-lookup"><span data-stu-id="f46c9-103">Serialization is the process of converting an object into a stream of bytes in order to store the object or transmit it to memory, a database, or a file.</span></span> <span data-ttu-id="f46c9-104">其主要目的是儲存物件的狀態，這樣就能在需要時重新建立該物件。</span><span class="sxs-lookup"><span data-stu-id="f46c9-104">Its main purpose is to save the state of an object in order to be able to recreate it when needed.</span></span> <span data-ttu-id="f46c9-105">反向的程序則稱為還原序列化。</span><span class="sxs-lookup"><span data-stu-id="f46c9-105">The reverse process is called deserialization.</span></span>  
  
## <a name="how-serialization-works"></a><span data-ttu-id="f46c9-106">序列化的運作方式</span><span class="sxs-lookup"><span data-stu-id="f46c9-106">How Serialization Works</span></span>  

 <span data-ttu-id="f46c9-107">下圖顯示序列化的整體程序。</span><span class="sxs-lookup"><span data-stu-id="f46c9-107">This illustration shows the overall process of serialization.</span></span>  
  
![序列化圖形](./media/index/serialization-process.gif)
  
 <span data-ttu-id="f46c9-109">物件會序列化成資料流，且其中不只包含資料，還有物件型別 (版本、文化特性及組件名稱) 的資訊。</span><span class="sxs-lookup"><span data-stu-id="f46c9-109">The object is serialized to a stream, which carries not just the data, but information about the object's type, such as its version, culture, and assembly name.</span></span> <span data-ttu-id="f46c9-110">而該資料流可以儲存在資料庫、檔案或記憶體中。</span><span class="sxs-lookup"><span data-stu-id="f46c9-110">From that stream, it can be stored in a database, a file, or memory.</span></span>  
  
### <a name="uses-for-serialization"></a><span data-ttu-id="f46c9-111">序列化的用法</span><span class="sxs-lookup"><span data-stu-id="f46c9-111">Uses for Serialization</span></span>  

 <span data-ttu-id="f46c9-112">序列化讓開發人員能夠儲存物件的狀態，並在需要時重新建立它，因此提供儲存物件及交換資料的功能。</span><span class="sxs-lookup"><span data-stu-id="f46c9-112">Serialization allows the developer to save the state of an object and recreate it as needed, providing storage of objects as well as data exchange.</span></span> <span data-ttu-id="f46c9-113">藉由序列化，開發人員可以執行的動作如下：透過 Web 服務將物件傳送到遠端應用程式、將物件從一個網域傳遞到另一個網域、將物件以 XML 字串傳遞通過防火牆，或是跨應用程式維護安全性或使用者專屬資訊。</span><span class="sxs-lookup"><span data-stu-id="f46c9-113">Through serialization, a developer can perform actions like sending the object to a remote application by means of a Web Service, passing an object from one domain to another, passing an object through a firewall as an XML string, or maintaining security or user-specific information across applications.</span></span>  
  
### <a name="making-an-object-serializable"></a><span data-ttu-id="f46c9-114">讓物件可序列化</span><span class="sxs-lookup"><span data-stu-id="f46c9-114">Making an Object Serializable</span></span>  

 <span data-ttu-id="f46c9-115">若要將物件序列化，您需要將要序列化的物件、將包含序列化物件的資料流，以及 <xref:System.Runtime.Serialization.Formatter>。</span><span class="sxs-lookup"><span data-stu-id="f46c9-115">To serialize an object, you need the object to be serialized, a stream to contain the serialized object, and a <xref:System.Runtime.Serialization.Formatter>.</span></span> <span data-ttu-id="f46c9-116"><xref:System.Runtime.Serialization> 包含序列化及還原序列化物件所需的類別。</span><span class="sxs-lookup"><span data-stu-id="f46c9-116"><xref:System.Runtime.Serialization> contains the classes necessary for serializing and deserializing objects.</span></span>  
  
 <span data-ttu-id="f46c9-117">將 <xref:System.SerializableAttribute> 屬性套用至某個類型，以表示此類型的執行個體為可序列化。</span><span class="sxs-lookup"><span data-stu-id="f46c9-117">Apply the <xref:System.SerializableAttribute> attribute to a type to indicate that instances of this type can be serialized.</span></span> <span data-ttu-id="f46c9-118">如果您嘗試序列化但該類型沒有 <xref:System.SerializableAttribute> 屬性，則會擲回 <xref:System.Runtime.Serialization.SerializationException> 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f46c9-118">A <xref:System.Runtime.Serialization.SerializationException> exception is thrown if you attempt to serialize but the type does not have the <xref:System.SerializableAttribute> attribute.</span></span>  
  
 <span data-ttu-id="f46c9-119">如果您不要將類別中的某個欄位序列化，請套用 <xref:System.NonSerializedAttribute> 屬性。</span><span class="sxs-lookup"><span data-stu-id="f46c9-119">If you do not want a field within your class to be serializable, apply the <xref:System.NonSerializedAttribute> attribute.</span></span> <span data-ttu-id="f46c9-120">如果可序列化型別的欄位包含指標、控制代碼，或一些其他特定環境專屬的資料結構，且無法以有意義的方式在不同環境中重新建構該欄位，則您可能想要讓它成為不可序列化的。</span><span class="sxs-lookup"><span data-stu-id="f46c9-120">If a field of a serializable type contains a pointer, a handle, or some other data structure that is specific to a particular environment, and the field cannot be meaningfully reconstituted in a different environment, then you may want to make it nonserializable.</span></span>  
  
 <span data-ttu-id="f46c9-121">如果序列化類別包含對其他類別之物件的參考，且該類別標記為 <xref:System.SerializableAttribute>，則系統也會將那些物件序列化。</span><span class="sxs-lookup"><span data-stu-id="f46c9-121">If a serialized class contains references to objects of other classes that are marked <xref:System.SerializableAttribute>, those objects will also be serialized.</span></span>  
  
## <a name="binary-and-xml-serialization"></a><span data-ttu-id="f46c9-122">二進位與 XML 序列化</span><span class="sxs-lookup"><span data-stu-id="f46c9-122">Binary and XML Serialization</span></span>  

 <span data-ttu-id="f46c9-123">二進位或 XML 序列化都能使用。</span><span class="sxs-lookup"><span data-stu-id="f46c9-123">Either binary or XML serialization can be used.</span></span> <span data-ttu-id="f46c9-124">在二進位序列化中，系統會序列化所有成員 (即使是唯讀的成員)，且效能會增強。</span><span class="sxs-lookup"><span data-stu-id="f46c9-124">In binary serialization, all members, even those that are read-only, are serialized, and performance is enhanced.</span></span> <span data-ttu-id="f46c9-125">XML 序列化提供可讀性較高的程式碼，也會基於互通性目的為物件共用和使用方式提供更大的彈性。</span><span class="sxs-lookup"><span data-stu-id="f46c9-125">XML serialization provides more readable code, as well as greater flexibility of object sharing and usage for interoperability purposes.</span></span>  
  
### <a name="binary-serialization"></a><span data-ttu-id="f46c9-126">二進位序列化</span><span class="sxs-lookup"><span data-stu-id="f46c9-126">Binary Serialization</span></span>  

 <span data-ttu-id="f46c9-127">二進位序列化使用二進位編碼來產生精簡的序列化，適用於儲存或通訊端型網路資料流。</span><span class="sxs-lookup"><span data-stu-id="f46c9-127">Binary serialization uses binary encoding to produce compact serialization for uses such as storage or socket-based network streams.</span></span>  
  
### <a name="xml-serialization"></a><span data-ttu-id="f46c9-128">XML 序列化</span><span class="sxs-lookup"><span data-stu-id="f46c9-128">XML Serialization</span></span>  

 <span data-ttu-id="f46c9-129">XML 序列化會將物件的公用欄位和屬性，或是方法的參數和傳回值，序列化為與特定 XML 結構描述定義語言 (XSD) 文件相符的 XML 資料流。</span><span class="sxs-lookup"><span data-stu-id="f46c9-129">XML serialization serializes the public fields and properties of an object, or the parameters and return values of methods, into an XML stream that conforms to a specific XML Schema definition language (XSD) document.</span></span> <span data-ttu-id="f46c9-130">XML 序列化會產生強型別的類別，其中包含的公用屬性和欄位都會轉換成 XML。</span><span class="sxs-lookup"><span data-stu-id="f46c9-130">XML serialization results in strongly typed classes with public properties and fields that are converted to XML.</span></span> <span data-ttu-id="f46c9-131"><xref:System.Xml.Serialization> 包含序列化及還原序列化 XML 所需的類別。</span><span class="sxs-lookup"><span data-stu-id="f46c9-131"><xref:System.Xml.Serialization> contains the classes necessary for serializing and deserializing XML.</span></span>  
  
 <span data-ttu-id="f46c9-132">您可以將屬性套用至類別和類別成員，以便控制 <xref:System.Xml.Serialization.XmlSerializer> 序列化或還原序列化類別執行個體的方式。</span><span class="sxs-lookup"><span data-stu-id="f46c9-132">You can apply attributes to classes and class members in order to control the way the <xref:System.Xml.Serialization.XmlSerializer> serializes or deserializes an instance of the class.</span></span>  
  
## <a name="basic-and-custom-serialization"></a><span data-ttu-id="f46c9-133">基本和自訂序列化</span><span class="sxs-lookup"><span data-stu-id="f46c9-133">Basic and Custom Serialization</span></span>  

 <span data-ttu-id="f46c9-134">有兩種方式可以執行序列化：基本和自訂。</span><span class="sxs-lookup"><span data-stu-id="f46c9-134">Serialization can be performed in two ways, basic and custom.</span></span> <span data-ttu-id="f46c9-135">基本序列化使用 .NET Framework 來自動序列化物件。</span><span class="sxs-lookup"><span data-stu-id="f46c9-135">Basic serialization uses the .NET Framework to automatically serialize the object.</span></span>  
  
### <a name="basic-serialization"></a><span data-ttu-id="f46c9-136">基本序列化</span><span class="sxs-lookup"><span data-stu-id="f46c9-136">Basic Serialization</span></span>  

 <span data-ttu-id="f46c9-137">基本序列化的唯一需求是物件已套用 <xref:System.SerializableAttribute> 屬性。</span><span class="sxs-lookup"><span data-stu-id="f46c9-137">The only requirement in basic serialization is that the object has the <xref:System.SerializableAttribute> attribute applied.</span></span> <span data-ttu-id="f46c9-138">可以使用 <xref:System.NonSerializedAttribute> 來防止特定欄位被序列化。</span><span class="sxs-lookup"><span data-stu-id="f46c9-138">The <xref:System.NonSerializedAttribute> can be used to keep specific fields from being serialized.</span></span>  
  
 <span data-ttu-id="f46c9-139">如果使用基本序列化，物件的版本控制可能會產生問題，這種情況則較適合使用自訂序列化。</span><span class="sxs-lookup"><span data-stu-id="f46c9-139">When you use basic serialization, the versioning of objects may create problems, in which case custom serialization may be preferable.</span></span> <span data-ttu-id="f46c9-140">基本序列化是執行序列化最簡單的方式，但它對該程序提供的控制機制並不多。</span><span class="sxs-lookup"><span data-stu-id="f46c9-140">Basic serialization is the easiest way to perform serialization, but it does not provide much control over the process.</span></span>  
  
### <a name="custom-serialization"></a><span data-ttu-id="f46c9-141">自訂序列化</span><span class="sxs-lookup"><span data-stu-id="f46c9-141">Custom Serialization</span></span>  

 <span data-ttu-id="f46c9-142">在自訂序列化中，您可以明確指定要序列化的物件，以及序列化的方式。</span><span class="sxs-lookup"><span data-stu-id="f46c9-142">In custom serialization, you can specify exactly which objects will be serialized and how it will be done.</span></span> <span data-ttu-id="f46c9-143">類別必須標記為 <xref:System.SerializableAttribute> 並實作 <xref:System.Runtime.Serialization.ISerializable> 介面。</span><span class="sxs-lookup"><span data-stu-id="f46c9-143">The class must be marked <xref:System.SerializableAttribute> and implement the <xref:System.Runtime.Serialization.ISerializable> interface.</span></span>  
  
 <span data-ttu-id="f46c9-144">如果您也想讓物件以自訂方式還原序列化，就必須使用自訂建構函式。</span><span class="sxs-lookup"><span data-stu-id="f46c9-144">If you want your object to be deserialized in a custom manner as well, you must use a custom constructor.</span></span>  
  
## <a name="designer-serialization"></a><span data-ttu-id="f46c9-145">設計工具序列化</span><span class="sxs-lookup"><span data-stu-id="f46c9-145">Designer Serialization</span></span>  

 <span data-ttu-id="f46c9-146">設計工具序列化是特殊格式的序列化，其中包含一種通常與開發工具相關聯的物件持續性。</span><span class="sxs-lookup"><span data-stu-id="f46c9-146">Designer serialization is a special form of serialization that involves the kind of object persistence usually associated with development tools.</span></span> <span data-ttu-id="f46c9-147">設計工具序列化程序的作用是將物件圖形轉換成來源檔案，而該檔案稍後可用於復原物件圖形。</span><span class="sxs-lookup"><span data-stu-id="f46c9-147">Designer serialization is the process of converting an object graph into a source file that can later be used to recover the object graph.</span></span> <span data-ttu-id="f46c9-148">來源檔案可以包含程式碼、標記，或甚至 SQL 資料表資訊。</span><span class="sxs-lookup"><span data-stu-id="f46c9-148">A source file can contain code, markup, or even SQL table information.</span></span>  
  
## <a name="related-topics-and-examples"></a><a name="BKMK_RelatedTopics"></a> <span data-ttu-id="f46c9-149">相關主題和範例</span><span class="sxs-lookup"><span data-stu-id="f46c9-149">Related Topics and Examples</span></span>  

 [<span data-ttu-id="f46c9-150">逐步解說：在 Visual Studio 中保存物件 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="f46c9-150">Walkthrough: Persisting an Object in Visual Studio (Visual Basic)</span></span>](walkthrough-persisting-an-object-in-visual-studio.md)  
 <span data-ttu-id="f46c9-151">示範序列化能如何用來保存物件在執行個體之間的資料，可讓您儲存值，並且在下次物件具現化時擷取它們。</span><span class="sxs-lookup"><span data-stu-id="f46c9-151">Demonstrates how serialization can be used to persist an object's data between instances, allowing you to store values and retrieve them the next time the object is instantiated.</span></span>  
  
 [<span data-ttu-id="f46c9-152">如何：從 XML 檔案讀取物件資料 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="f46c9-152">How to: Read Object Data from an XML File (Visual Basic)</span></span>](how-to-read-object-data-from-an-xml-file.md)  
 <span data-ttu-id="f46c9-153">示範如何讀取先前使用 <xref:System.Xml.Serialization.XmlSerializer> 類別來寫入 XML 檔案的物件資料。</span><span class="sxs-lookup"><span data-stu-id="f46c9-153">Shows how to read object data that was previously written to an XML file using the <xref:System.Xml.Serialization.XmlSerializer> class.</span></span>  
  
 [<span data-ttu-id="f46c9-154">如何：將物件資料寫入 XML 檔案 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="f46c9-154">How to: Write Object Data to an XML File (Visual Basic)</span></span>](how-to-write-object-data-to-an-xml-file.md)  
 <span data-ttu-id="f46c9-155">示範如何使用 <xref:System.Xml.Serialization.XmlSerializer> 類別，將來自某個類別的物件寫入 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="f46c9-155">Shows how to write the object from a class to an XML file using the <xref:System.Xml.Serialization.XmlSerializer> class.</span></span>
