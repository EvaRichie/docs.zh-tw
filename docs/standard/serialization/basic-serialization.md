---
title: 基本序列化
description: 本文說明如何使用 SerializableAttribute 讓類別可序列化，並包含序列化和還原序列化的範例。
ms.date: 03/30/2017
helpviewer_keywords:
- binary serialization, basic serialization
- serialization, basic serialization
ms.assetid: d899d43c-335a-433e-a589-cd187192984f
dev_langs:
- CSharp
ms.openlocfilehash: 98ea6f23467b85dc270aa323e72a8a9b0934994a
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/13/2020
ms.locfileid: "83378420"
---
# <a name="basic-serialization"></a><span data-ttu-id="53e51-103">基本序列化</span><span class="sxs-lookup"><span data-stu-id="53e51-103">Basic serialization</span></span>

[!INCLUDE [binary-serialization-warning](../../../includes/binary-serialization-warning.md)]

<span data-ttu-id="53e51-104">要讓類別可序列化的最簡單方式就是以 <xref:System.SerializableAttribute> 加以標示，如下所示。</span><span class="sxs-lookup"><span data-stu-id="53e51-104">The easiest way to make a class serializable is to mark it with the <xref:System.SerializableAttribute> as follows.</span></span>  
  
```csharp  
[Serializable]  
public class MyObject {  
  public int n1 = 0;  
  public int n2 = 0;  
  public String str = null;  
}  
```  
  
<span data-ttu-id="53e51-105">下列程式碼範例示範如何將此類別的執行個體序列化成檔案。</span><span class="sxs-lookup"><span data-stu-id="53e51-105">The following code example shows how an instance of this class can be serialized to a file.</span></span>  
  
```csharp  
MyObject obj = new MyObject();  
obj.n1 = 1;  
obj.n2 = 24;  
obj.str = "Some String";  
IFormatter formatter = new BinaryFormatter();  
Stream stream = new FileStream("MyFile.bin", FileMode.Create, FileAccess.Write, FileShare.None);  
formatter.Serialize(stream, obj);  
stream.Close();  
```  
  
<span data-ttu-id="53e51-106">此範例使用二進位格式子進行序列化。</span><span class="sxs-lookup"><span data-stu-id="53e51-106">This example uses a binary formatter to do the serialization.</span></span> <span data-ttu-id="53e51-107">您只需要建立資料流執行個體以及想要使用的格式子，然後在格式子上呼叫 **Serialize** 方法。</span><span class="sxs-lookup"><span data-stu-id="53e51-107">All you need to do is create an instance of the stream and the formatter you intend to use, and then call the **Serialize** method on the formatter.</span></span> <span data-ttu-id="53e51-108">將要序列化的資料流及物件，當做參數提供給此呼叫。</span><span class="sxs-lookup"><span data-stu-id="53e51-108">The stream and the object to serialize are provided as parameters to this call.</span></span> <span data-ttu-id="53e51-109">雖然在此範例中未明確示範，不過類別的所有成員變數都將序列化，即使是標示為私用的變數亦然。</span><span class="sxs-lookup"><span data-stu-id="53e51-109">Although it is not explicitly demonstrated in this example, all member variables of a class will be serialized—even variables marked as private.</span></span> <span data-ttu-id="53e51-110">在這方面，二進位序列化與 <xref:System.Xml.Serialization.XmlSerializer> 類別不同，後者只會序列化公用欄位。</span><span class="sxs-lookup"><span data-stu-id="53e51-110">In this aspect, binary serialization differs from the <xref:System.Xml.Serialization.XmlSerializer> class, which only serializes public fields.</span></span> <span data-ttu-id="53e51-111">如需從二進位序列化排除成員變數的資訊，請參閱[選擇式序列化](selective-serialization.md)。</span><span class="sxs-lookup"><span data-stu-id="53e51-111">For information on excluding member variables from binary serialization, see [Selective Serialization](selective-serialization.md).</span></span>  
  
<span data-ttu-id="53e51-112">將物件還原成其先前的狀態也一樣容易。</span><span class="sxs-lookup"><span data-stu-id="53e51-112">Restoring the object back to its former state is just as easy.</span></span> <span data-ttu-id="53e51-113">首先，建立供讀取的資料流和 <xref:System.Runtime.Serialization.Formatter>，然後指示格式子對物件還原序列化。</span><span class="sxs-lookup"><span data-stu-id="53e51-113">First, create a stream for reading and a <xref:System.Runtime.Serialization.Formatter>, and then instruct the formatter to deserialize the object.</span></span> <span data-ttu-id="53e51-114">下列程式碼範例會示範其做法。</span><span class="sxs-lookup"><span data-stu-id="53e51-114">The code example below shows how this is done.</span></span>  
  
```csharp  
IFormatter formatter = new BinaryFormatter();  
Stream stream = new FileStream("MyFile.bin", FileMode.Open, FileAccess.Read, FileShare.Read);  
MyObject obj = (MyObject) formatter.Deserialize(stream);  
stream.Close();  
  
// Here's the proof.  
Console.WriteLine("n1: {0}", obj.n1);  
Console.WriteLine("n2: {0}", obj.n2);  
Console.WriteLine("str: {0}", obj.str);  
```  
  
<span data-ttu-id="53e51-115">上述使用的 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> 非常有效率，可產生精簡的位元組資料流。</span><span class="sxs-lookup"><span data-stu-id="53e51-115">The <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> used above is very efficient and produces a compact byte stream.</span></span> <span data-ttu-id="53e51-116">利用此格式子序列化的所有物件也可以用它來還原序列化，所以此格式子是理想的工具，可以在 .NET Framework 上對將要還原序列化的物件進行序列化。</span><span class="sxs-lookup"><span data-stu-id="53e51-116">All objects serialized with this formatter can also be deserialized with it, which makes it an ideal tool for serializing objects that will be deserialized on the .NET Framework.</span></span> <span data-ttu-id="53e51-117">務必注意，物件還原序列化時，不會呼叫建構函式。</span><span class="sxs-lookup"><span data-stu-id="53e51-117">It is important to note that constructors are not called when an object is deserialized.</span></span> <span data-ttu-id="53e51-118">還原序列化有此限制是基於效能的考量。</span><span class="sxs-lookup"><span data-stu-id="53e51-118">This constraint is placed on deserialization for performance reasons.</span></span> <span data-ttu-id="53e51-119">然而，這樣違反了執行階段與物件寫入器之間建立的某些一般合約，開發人員應確定他們了解將物件標示為可序列化時，可能出現的後果。</span><span class="sxs-lookup"><span data-stu-id="53e51-119">However, this violates some of the usual contracts the runtime makes with the object writer, and developers should ensure that they understand the ramifications when marking an object as serializable.</span></span>  
  
<span data-ttu-id="53e51-120">如果要求可攜性，請改為使用 <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>。</span><span class="sxs-lookup"><span data-stu-id="53e51-120">If portability is a requirement, use the <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter> instead.</span></span> <span data-ttu-id="53e51-121">只要將上述程式碼中的 **BinaryFormatter** 取代為 **SoapFormatter**，並如之前一樣呼叫 **Serialize** 和 **Deserialize** 即可。</span><span class="sxs-lookup"><span data-stu-id="53e51-121">Simply replace the **BinaryFormatter** in the code above with **SoapFormatter,** and call **Serialize** and **Deserialize** as before.</span></span> <span data-ttu-id="53e51-122">在上述範例中使用的此格式子會產生下列輸出。</span><span class="sxs-lookup"><span data-stu-id="53e51-122">This formatter produces the following output for the example used above.</span></span>  
  
```xml  
<SOAP-ENV:Envelope  
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
  xmlns:xsd="http://www.w3.org/2001/XMLSchema"
  xmlns:SOAP-ENC="http://schemas.xmlsoap.org/soap/encoding/"  
  xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/"  
  SOAP-ENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/"  
  xmlns:a1="http://schemas.microsoft.com/clr/assem/ToFile">  
  
  <SOAP-ENV:Body>  
    <a1:MyObject id="ref-1">  
      <n1>1</n1>  
      <n2>24</n2>  
      <str id="ref-3">Some String</str>  
    </a1:MyObject>  
  </SOAP-ENV:Body>  
</SOAP-ENV:Envelope>  
```  
  
<span data-ttu-id="53e51-123">請注意，無法繼承 [Serializable](xref:System.SerializableAttribute) 屬性。</span><span class="sxs-lookup"><span data-stu-id="53e51-123">It's important to note that the [Serializable](xref:System.SerializableAttribute) attribute cannot be inherited.</span></span> <span data-ttu-id="53e51-124">若您從 `MyObject` 衍生新類別，新類別必須也用該屬性標示，否則無法將其序列化。</span><span class="sxs-lookup"><span data-stu-id="53e51-124">If you derive a new class from `MyObject`, the new class must be marked with the attribute as well, or it cannot be serialized.</span></span> <span data-ttu-id="53e51-125">例如，當您嘗試序列化下列類別的執行個體時，會出現 <xref:System.Runtime.Serialization.SerializationException> 通知您 `MyStuff` 類型未標示為可序列化。</span><span class="sxs-lookup"><span data-stu-id="53e51-125">For example, when you attempt to serialize an instance of the class below, you'll get a <xref:System.Runtime.Serialization.SerializationException> informing you that the `MyStuff` type is not marked as serializable.</span></span>  
  
```csharp  
public class MyStuff : MyObject
{  
  public int n3;  
}  
```  
  
 <span data-ttu-id="53e51-126">使用 [Serializable](xref:System.SerializableAttribute) 屬性十分方便，但有上述限制。</span><span class="sxs-lookup"><span data-stu-id="53e51-126">Using the [Serializable](xref:System.SerializableAttribute) attribute is convenient, but it has limitations as previously demonstrated.</span></span> <span data-ttu-id="53e51-127">如需何時應將類別標示為序列化的資訊，請參閱[序列化方針](serialization-guidelines.md)。</span><span class="sxs-lookup"><span data-stu-id="53e51-127">Refer to the [Serialization Guidelines](serialization-guidelines.md) for information about when you should mark a class for serialization.</span></span> <span data-ttu-id="53e51-128">類別在編譯後即無法在其中新增序列化。</span><span class="sxs-lookup"><span data-stu-id="53e51-128">Serialization cannot be added to a class after it has been compiled.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="53e51-129">請參閱</span><span class="sxs-lookup"><span data-stu-id="53e51-129">See also</span></span>

- [<span data-ttu-id="53e51-130">二進位序列化</span><span class="sxs-lookup"><span data-stu-id="53e51-130">Binary Serialization</span></span>](binary-serialization.md)
- [<span data-ttu-id="53e51-131">XML 和 SOAP 序列化</span><span class="sxs-lookup"><span data-stu-id="53e51-131">XML and SOAP Serialization</span></span>](xml-and-soap-serialization.md)
