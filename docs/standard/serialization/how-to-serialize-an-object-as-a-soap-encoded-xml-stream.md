---
title: HOW TO：將物件序列化為 SOAP 編碼的 XML 資料流
description: 瞭解如何將物件序列化為 SOAP 編碼的 XML 資料流程。 XmlSerializer 類別可以用來序列化類別並產生編碼的 SOAP 訊息。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- SOAP, XML serialization
- XML serialization, SOAP
- serialization, SOAP
ms.assetid: af406e0a-fa3a-46dd-a7ba-c80731eba3a0
ms.openlocfilehash: 1d38c4e334439ef41b4d4429e52cff04c6463573
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84291561"
---
# <a name="how-to-serialize-an-object-as-a-soap-encoded-xml-stream"></a><span data-ttu-id="61f1c-104">HOW TO：將物件序列化為 SOAP 編碼的 XML 資料流</span><span class="sxs-lookup"><span data-stu-id="61f1c-104">How to: Serialize an Object as a SOAP-Encoded XML Stream</span></span>
  
 <span data-ttu-id="61f1c-105">因為 SOAP 訊息是使用 XML 建置的，所以 <xref:System.Xml.Serialization.XmlSerializer> 類別可用來序列化類別並產生編碼的 SOAP 訊息。</span><span class="sxs-lookup"><span data-stu-id="61f1c-105">Because a SOAP message is built using XML, the <xref:System.Xml.Serialization.XmlSerializer> class can be used to serialize classes and generate encoded SOAP messages.</span></span> <span data-ttu-id="61f1c-106">產生的 XML 會與[全球資訊網協會之＜Simple Object Access Protocol (SOAP) 1.1＞文件中的第 5 節](https://www.w3.org/TR/2000/NOTE-SOAP-20000508/#_Toc478383512)相符。</span><span class="sxs-lookup"><span data-stu-id="61f1c-106">The resulting XML conforms to [section 5 of the World Wide Web Consortium document "Simple Object Access Protocol (SOAP) 1.1"](https://www.w3.org/TR/2000/NOTE-SOAP-20000508/#_Toc478383512).</span></span> <span data-ttu-id="61f1c-107">當您建立透過 SOAP 訊息溝通的 XML Web 服務時，您可以將特殊 SOAP 屬性集套用至類別與類別成員以自訂 XML 資料流。</span><span class="sxs-lookup"><span data-stu-id="61f1c-107">When you are creating an XML Web service that communicates through SOAP messages, you can customize the XML stream by applying a set of special SOAP attributes to classes and members of classes.</span></span> <span data-ttu-id="61f1c-108">如需屬性的清單，請參閱[控制編碼 SOAP 序列化的屬性](attributes-that-control-encoded-soap-serialization.md)。</span><span class="sxs-lookup"><span data-stu-id="61f1c-108">For a list of attributes, see [Attributes That Control Encoded SOAP Serialization](attributes-that-control-encoded-soap-serialization.md).</span></span>  
  
### <a name="to-serialize-an-object-as-a-soap-encoded-xml-stream"></a><span data-ttu-id="61f1c-109">將物件序列化為 SOAP 編碼的 XML 資料流</span><span class="sxs-lookup"><span data-stu-id="61f1c-109">To serialize an object as a SOAP-encoded XML stream</span></span>  
  
1. <span data-ttu-id="61f1c-110">使用 [XML 結構描述定義工具 (Xsd.exe)](xml-schema-definition-tool-xsd-exe.md)建立類別。</span><span class="sxs-lookup"><span data-stu-id="61f1c-110">Create the class using the [XML Schema Definition Tool (Xsd.exe)](xml-schema-definition-tool-xsd-exe.md).</span></span>  
  
2. <span data-ttu-id="61f1c-111">套用在 中發現的一個或多個特殊屬性。</span><span class="sxs-lookup"><span data-stu-id="61f1c-111">Apply one or more of the special attributes found in `System.Xml.Serialization`.</span></span> <span data-ttu-id="61f1c-112">請參閱＜控制編碼 SOAP 序列化的屬性＞中的清單。</span><span class="sxs-lookup"><span data-stu-id="61f1c-112">See the list in "Attributes That Control Encoded SOAP Serialization."</span></span>  
  
3. <span data-ttu-id="61f1c-113">藉由建立新的 `XmlTypeMapping` 及使用已序列化類別的型別叫用 `SoapReflectionImporter` 方法，來建立 `ImportTypeMapping`。</span><span class="sxs-lookup"><span data-stu-id="61f1c-113">Create an `XmlTypeMapping` by creating a new `SoapReflectionImporter`, and invoking the `ImportTypeMapping` method with the type of the serialized class.</span></span>  
  
     <span data-ttu-id="61f1c-114">下列程式碼範例會呼叫 `SoapReflectionImporter` 類別的 `ImportTypeMapping` 方法，以建立 `XmlTypeMapping`。</span><span class="sxs-lookup"><span data-stu-id="61f1c-114">The following code example calls the `ImportTypeMapping` method of the `SoapReflectionImporter` class to create an `XmlTypeMapping`.</span></span>  
  
    ```vb  
    ' Serializes a class named Group as a SOAP message.  
    Dim myTypeMapping As XmlTypeMapping =
        New SoapReflectionImporter().ImportTypeMapping(GetType(Group))  
    ```  
  
    ```csharp  
    // Serializes a class named Group as a SOAP message.  
    XmlTypeMapping myTypeMapping =
        new SoapReflectionImporter().ImportTypeMapping(typeof(Group));
    ```  
  
4. <span data-ttu-id="61f1c-115">利用傳遞 `XmlSerializer` 給 `XmlTypeMapping` 建構函式的方式，來建立 <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Xml.Serialization.XmlTypeMapping%29> 類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="61f1c-115">Create an instance of the `XmlSerializer` class by passing the `XmlTypeMapping` to the <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Xml.Serialization.XmlTypeMapping%29> constructor.</span></span>  
  
    ```vb  
    Dim mySerializer As XmlSerializer = New XmlSerializer(myTypeMapping)  
    ```  
  
    ```csharp  
    XmlSerializer mySerializer = new XmlSerializer(myTypeMapping);  
    ```  
  
5. <span data-ttu-id="61f1c-116">呼叫 `Serialize` 或 `Deserialize` 方法。</span><span class="sxs-lookup"><span data-stu-id="61f1c-116">Call the `Serialize` or `Deserialize` method.</span></span>  
  
## <a name="example"></a><span data-ttu-id="61f1c-117">範例</span><span class="sxs-lookup"><span data-stu-id="61f1c-117">Example</span></span>  
  
```vb  
' Serializes a class named Group as a SOAP message.  
Dim myTypeMapping As XmlTypeMapping =
    New SoapReflectionImporter().ImportTypeMapping(GetType(Group))
Dim mySerializer As XmlSerializer = New XmlSerializer(myTypeMapping)  
```  
  
```csharp  
// Serializes a class named Group as a SOAP message.  
XmlTypeMapping myTypeMapping =
    new SoapReflectionImporter().ImportTypeMapping(typeof(Group));
XmlSerializer mySerializer = new XmlSerializer(myTypeMapping);  
```  
  
## <a name="see-also"></a><span data-ttu-id="61f1c-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="61f1c-118">See also</span></span>

- [<span data-ttu-id="61f1c-119">XML 和 SOAP 序列化</span><span class="sxs-lookup"><span data-stu-id="61f1c-119">XML and SOAP Serialization</span></span>](xml-and-soap-serialization.md)
- [<span data-ttu-id="61f1c-120">控制編碼 SOAP 序列化的屬性</span><span class="sxs-lookup"><span data-stu-id="61f1c-120">Attributes That Control Encoded SOAP Serialization</span></span>](attributes-that-control-encoded-soap-serialization.md)
- [<span data-ttu-id="61f1c-121">使用 XML Web Service 進行 XML 序列化</span><span class="sxs-lookup"><span data-stu-id="61f1c-121">XML Serialization with XML Web Services</span></span>](xml-serialization-with-xml-web-services.md)
- [<span data-ttu-id="61f1c-122">HOW TO：序列化物件</span><span class="sxs-lookup"><span data-stu-id="61f1c-122">How to: Serialize an Object</span></span>](how-to-serialize-an-object.md)
- [<span data-ttu-id="61f1c-123">如何：還原序列化物件</span><span class="sxs-lookup"><span data-stu-id="61f1c-123">How to: Deserialize an Object</span></span>](how-to-deserialize-an-object.md)
- [<span data-ttu-id="61f1c-124">如何：覆寫已編碼的 SOAP XML 序列化</span><span class="sxs-lookup"><span data-stu-id="61f1c-124">How to: Override Encoded SOAP XML Serialization</span></span>](how-to-override-encoded-soap-xml-serialization.md)
