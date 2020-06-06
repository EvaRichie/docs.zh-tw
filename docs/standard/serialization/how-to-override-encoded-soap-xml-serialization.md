---
title: HOW TO：覆寫已編碼的 SOAP XML 序列化
description: 瞭解如何將物件的 XML 序列化覆寫為 SOAP 訊息，這與覆寫標準 XML 序列化的程式類似。
ms.date: 03/30/2017
helpviewer_keywords:
- overriding XML serialization
- SOAP, overriding encoded XML serialization
ms.assetid: d0791df8-04e3-46b4-a6be-fe0ed09267e8
ms.openlocfilehash: 50688cb25294f14a9dd4596258eb95adf93cdb41
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "84277982"
---
# <a name="how-to-override-encoded-soap-xml-serialization"></a><span data-ttu-id="a4c75-103">HOW TO：覆寫已編碼的 SOAP XML 序列化</span><span class="sxs-lookup"><span data-stu-id="a4c75-103">How to: Override Encoded SOAP XML Serialization</span></span>

<span data-ttu-id="a4c75-104">將物件的 XML 序列化覆寫為 SOAP 訊息的程序，與覆寫標準 XML 序列化的程序類似。</span><span class="sxs-lookup"><span data-stu-id="a4c75-104">The process for overriding XML serialization of objects as SOAP messages is similar to the process for overriding standard XML serialization.</span></span> <span data-ttu-id="a4c75-105">如需覆寫標準 XML 序列化的資訊，請參閱[如何：指定 XML 資料流的替代項目名稱](how-to-specify-an-alternate-element-name-for-an-xml-stream.md)。</span><span class="sxs-lookup"><span data-stu-id="a4c75-105">For information about overriding standard XML serialization, see [How to: Specify an Alternate Element Name for an XML Stream](how-to-specify-an-alternate-element-name-for-an-xml-stream.md).</span></span>

## <a name="to-override-serialization-of-objects-as-soap-messages"></a><span data-ttu-id="a4c75-106">將物件的序列化覆寫為 SOAP 訊息</span><span class="sxs-lookup"><span data-stu-id="a4c75-106">To override serialization of objects as SOAP messages</span></span>

1. <span data-ttu-id="a4c75-107">建立 <xref:System.Xml.Serialization.SoapAttributeOverrides> 類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="a4c75-107">Create an instance of the <xref:System.Xml.Serialization.SoapAttributeOverrides> class.</span></span>

2. <span data-ttu-id="a4c75-108">為每個序列化的類別成員建立 `SoapAttributes`。</span><span class="sxs-lookup"><span data-stu-id="a4c75-108">Create a `SoapAttributes` for each class member that is being serialized.</span></span>

3. <span data-ttu-id="a4c75-109">對序列化的成員適當地建立會影響 XML 序列化之一個或多個屬性的執行個體。</span><span class="sxs-lookup"><span data-stu-id="a4c75-109">Create an instance of one or more of the attributes that affect XML serialization, as appropriate, to the member being serialized.</span></span> <span data-ttu-id="a4c75-110">如需詳細資訊，請參閱＜控制編碼 SOAP 序列化的屬性＞。</span><span class="sxs-lookup"><span data-stu-id="a4c75-110">For more information, see "Attributes That Control Encoded SOAP Serialization".</span></span>

4. <span data-ttu-id="a4c75-111">將 `SoapAttributes` 的適當屬性 (property) 設定為在步驟 3 所建立的屬性 (attribute)。</span><span class="sxs-lookup"><span data-stu-id="a4c75-111">Set the appropriate property of `SoapAttributes` to the attribute created in step 3.</span></span>

5. <span data-ttu-id="a4c75-112">將 `SoapAttributes` 新增至 `SoapAttributeOverrides`。</span><span class="sxs-lookup"><span data-stu-id="a4c75-112">Add `SoapAttributes` to `SoapAttributeOverrides`.</span></span>

6. <span data-ttu-id="a4c75-113">使用 `XmlTypeMapping` 建立 `SoapAttributeOverrides`。</span><span class="sxs-lookup"><span data-stu-id="a4c75-113">Create an `XmlTypeMapping` using the `SoapAttributeOverrides`.</span></span> <span data-ttu-id="a4c75-114">請使用 `SoapReflectionImporter.ImportTypeMapping` 方法。</span><span class="sxs-lookup"><span data-stu-id="a4c75-114">Use the `SoapReflectionImporter.ImportTypeMapping` method.</span></span>

7. <span data-ttu-id="a4c75-115">使用 `XmlSerializer` 建立 `XmlTypeMapping`。</span><span class="sxs-lookup"><span data-stu-id="a4c75-115">Create an `XmlSerializer` using `XmlTypeMapping`.</span></span>

8. <span data-ttu-id="a4c75-116">序列化或還原序列化物件。</span><span class="sxs-lookup"><span data-stu-id="a4c75-116">Serialize or deserialize the object.</span></span>

## <a name="example"></a><span data-ttu-id="a4c75-117">範例</span><span class="sxs-lookup"><span data-stu-id="a4c75-117">Example</span></span>

<span data-ttu-id="a4c75-118">下列程式碼範例以兩種方法序列化檔案：第一種是不覆寫 `XmlSerializer` 類別的行為，第二種則是覆寫此行為。</span><span class="sxs-lookup"><span data-stu-id="a4c75-118">The following code example serializes a file in two ways: first, without overriding the `XmlSerializer` class's behavior, and second, by overriding the behavior.</span></span> <span data-ttu-id="a4c75-119">本範例包含具有數個成員的 `Group` 類別。</span><span class="sxs-lookup"><span data-stu-id="a4c75-119">The example contains a class named `Group` with several members.</span></span> <span data-ttu-id="a4c75-120">已將不同屬性 (例如 `SoapElementAttribute`) 套用至類別成員。</span><span class="sxs-lookup"><span data-stu-id="a4c75-120">Various attributes, such as the `SoapElementAttribute`, have been applied to class members.</span></span> <span data-ttu-id="a4c75-121">當類別以 `SerializeOriginal` 方法序列化後，屬性會控制 SOAP 訊息內容。</span><span class="sxs-lookup"><span data-stu-id="a4c75-121">When the class is serialized with the `SerializeOriginal` method, the attributes control the SOAP message content.</span></span> <span data-ttu-id="a4c75-122">呼叫 `SerializeOverride` 方法時，會建立不同屬性 (Attribute) 並將 `XmlSerializer` 的屬性 (Property) 設定為那些屬性 (Attribute) 來覆寫 `SoapAttributes` 的行為 (如果適合的話)。</span><span class="sxs-lookup"><span data-stu-id="a4c75-122">When the `SerializeOverride` method is called, the behavior of the `XmlSerializer` is overridden by creating various attributes and setting the properties of a `SoapAttributes` to those attributes (as appropriate).</span></span>

```csharp
using System;
using System.IO;
using System.Xml;
using System.Xml.Serialization;
using System.Xml.Schema;

public class Group
{
    [SoapAttribute (Namespace = "http://www.cpandl.com")]
    public string GroupName;

    [SoapAttribute(DataType = "base64Binary")]
    public Byte [] GroupNumber;

    [SoapAttribute(DataType = "date", AttributeName = "CreationDate")]
    public DateTime Today;
    [SoapElement(DataType = "nonNegativeInteger", ElementName = "PosInt")]
    public string PositiveInt;
    // This is ignored when serialized unless it is overridden.
    [SoapIgnore]
    public bool IgnoreThis;

    public GroupType Grouptype;

    [SoapInclude(typeof(Car))]
    public Vehicle myCar(string licNumber)
    {
        Vehicle v;
        if(licNumber == "")
            {
                v = new Car();
            v.licenseNumber = "!!!!!!";
        }
        else
        {
            v = new Car();
            v.licenseNumber = licNumber;
        }
        return v;
    }
}

public abstract class Vehicle
{
    public string licenseNumber;
    public DateTime makeDate;
}

public class Car: Vehicle
{
}

public enum GroupType
{
    // These enums can be overridden.
    small,
    large
}

public class Run
{
    public static void Main()
    {
        Run test = new Run();
        test.SerializeOriginal("SoapOriginal.xml");
        test.SerializeOverride("SoapOverrides.xml");
        test.DeserializeOriginal("SoapOriginal.xml");
        test.DeserializeOverride("SoapOverrides.xml");

    }
    public void SerializeOriginal(string filename)
    {
        // Creates an instance of the XmlSerializer class.
        XmlTypeMapping myMapping =
        (new SoapReflectionImporter().ImportTypeMapping(
        typeof(Group)));
        XmlSerializer mySerializer =
        new XmlSerializer(myMapping);

        // Writing the file requires a TextWriter.
        TextWriter writer = new StreamWriter(filename);

        // Creates an instance of the class that will be serialized.
        Group myGroup = new Group();

        // Sets the object properties.
        myGroup.GroupName = ".NET";

        Byte [] hexByte = new Byte[2]{Convert.ToByte(100),
        Convert.ToByte(50)};
        myGroup.GroupNumber = hexByte;

        DateTime myDate = new DateTime(2002,5,2);
        myGroup.Today = myDate;

        myGroup.PositiveInt= "10000";
        myGroup.IgnoreThis=true;
        myGroup.Grouptype= GroupType.small;
        Car thisCar =(Car)  myGroup.myCar("1234566");

        // Prints the license number just to prove the car was created.
        Console.WriteLine("License#: " + thisCar.licenseNumber + "\n");

        // Serializes the class and closes the TextWriter.
        mySerializer.Serialize(writer, myGroup);
        writer.Close();
    }

    public void SerializeOverride(string filename)
    {
        // Creates an instance of the XmlSerializer class
        // that overrides the serialization.
        XmlSerializer overRideSerializer = CreateOverrideSerializer();

        // Writing the file requires a TextWriter.
        TextWriter writer = new StreamWriter(filename);

        // Creates an instance of the class that will be serialized.
        Group myGroup = new Group();

        // Sets the object properties.
        myGroup.GroupName = ".NET";

        Byte [] hexByte = new Byte[2]{Convert.ToByte(100),
        Convert.ToByte(50)};
        myGroup.GroupNumber = hexByte;

        DateTime myDate = new DateTime(2002,5,2);
        myGroup.Today = myDate;

        myGroup.PositiveInt= "10000";
        myGroup.IgnoreThis=true;
        myGroup.Grouptype= GroupType.small;
        Car thisCar =(Car)  myGroup.myCar("1234566");

        // Serializes the class and closes the TextWriter.
        overRideSerializer.Serialize(writer, myGroup);
         writer.Close();
    }

    public void DeserializeOriginal(string filename)
    {
        // Creates an instance of the XmlSerializer class.
        XmlTypeMapping myMapping =
        (new SoapReflectionImporter().ImportTypeMapping(
        typeof(Group)));
        XmlSerializer mySerializer =
        new XmlSerializer(myMapping);

        TextReader reader = new StreamReader(filename);

        // Deserializes and casts the object.
        Group myGroup;
        myGroup = (Group) mySerializer.Deserialize(reader);

        Console.WriteLine(myGroup.GroupName);
        Console.WriteLine(myGroup.GroupNumber[0]);
        Console.WriteLine(myGroup.GroupNumber[1]);
        Console.WriteLine(myGroup.Today);
        Console.WriteLine(myGroup.PositiveInt);
        Console.WriteLine(myGroup.IgnoreThis);
        Console.WriteLine();
    }

    public void DeserializeOverride(string filename)
    {
        // Creates an instance of the XmlSerializer class.
        XmlSerializer overRideSerializer = CreateOverrideSerializer();
        // Reading the file requires a TextReader.
        TextReader reader = new StreamReader(filename);

        // Deserializes and casts the object.
        Group myGroup;
        myGroup = (Group) overRideSerializer.Deserialize(reader);

        Console.WriteLine(myGroup.GroupName);
        Console.WriteLine(myGroup.GroupNumber[0]);
        Console.WriteLine(myGroup.GroupNumber[1]);
        Console.WriteLine(myGroup.Today);
        Console.WriteLine(myGroup.PositiveInt);
        Console.WriteLine(myGroup.IgnoreThis);
    }

    private XmlSerializer CreateOverrideSerializer()
    {
        SoapAttributeOverrides mySoapAttributeOverrides =
        new SoapAttributeOverrides();
        SoapAttributes soapAtts = new SoapAttributes();

        SoapElementAttribute mySoapElement = new SoapElementAttribute();
        mySoapElement.ElementName = "xxxx";
        soapAtts.SoapElement = mySoapElement;
        mySoapAttributeOverrides.Add(typeof(Group), "PositiveInt",
        soapAtts);

        // Overrides the IgnoreThis property.
        SoapIgnoreAttribute myIgnore = new SoapIgnoreAttribute();
        soapAtts = new SoapAttributes();
        soapAtts.SoapIgnore = false;
        mySoapAttributeOverrides.Add(typeof(Group), "IgnoreThis",
        soapAtts);

        // Overrides the GroupType enumeration.
        soapAtts = new SoapAttributes();
        SoapEnumAttribute xSoapEnum = new SoapEnumAttribute();
        xSoapEnum.Name = "Over1000";
        soapAtts.SoapEnum = xSoapEnum;

        // Adds the SoapAttributes to the
        // mySoapAttributeOverrides.
        mySoapAttributeOverrides.Add(typeof(GroupType), "large",
        soapAtts);

        // Creates a second enumeration and adds it.
        soapAtts = new SoapAttributes();
        xSoapEnum = new SoapEnumAttribute();
        xSoapEnum.Name = "ZeroTo1000";
        soapAtts.SoapEnum = xSoapEnum;
        mySoapAttributeOverrides.Add(typeof(GroupType), "small",
        soapAtts);

        // Overrides the Group type.
        soapAtts = new SoapAttributes();
        SoapTypeAttribute soapType = new SoapTypeAttribute();
        soapType.TypeName = "Team";
        soapAtts.SoapType = soapType;
        mySoapAttributeOverrides.Add(typeof(Group),soapAtts);

        // Creates an XmlTypeMapping that is used to create an instance
        // of the XmlSerializer class. Then returns the XmlSerializer.
        XmlTypeMapping myMapping = (new SoapReflectionImporter(
        mySoapAttributeOverrides)).ImportTypeMapping(typeof(Group));

        XmlSerializer ser = new XmlSerializer(myMapping);
        return ser;
    }
}
```

## <a name="see-also"></a><span data-ttu-id="a4c75-123">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a4c75-123">See also</span></span>

- [<span data-ttu-id="a4c75-124">XML 和 SOAP 序列化</span><span class="sxs-lookup"><span data-stu-id="a4c75-124">XML and SOAP Serialization</span></span>](xml-and-soap-serialization.md)
- [<span data-ttu-id="a4c75-125">控制編碼 SOAP 序列化的屬性</span><span class="sxs-lookup"><span data-stu-id="a4c75-125">Attributes That Control Encoded SOAP Serialization</span></span>](attributes-that-control-encoded-soap-serialization.md)
- [<span data-ttu-id="a4c75-126">使用 XML Web Service 進行 XML 序列化</span><span class="sxs-lookup"><span data-stu-id="a4c75-126">XML Serialization with XML Web Services</span></span>](xml-serialization-with-xml-web-services.md)
- [<span data-ttu-id="a4c75-127">HOW TO：序列化物件</span><span class="sxs-lookup"><span data-stu-id="a4c75-127">How to: Serialize an Object</span></span>](how-to-serialize-an-object.md)
- [<span data-ttu-id="a4c75-128">如何：還原序列化物件</span><span class="sxs-lookup"><span data-stu-id="a4c75-128">How to: Deserialize an Object</span></span>](how-to-deserialize-an-object.md)
- [<span data-ttu-id="a4c75-129">如何：將物件序列化為 SOAP 編碼的 XML 資料流</span><span class="sxs-lookup"><span data-stu-id="a4c75-129">How to: Serialize an Object as a SOAP-Encoded XML Stream</span></span>](how-to-serialize-an-object-as-a-soap-encoded-xml-stream.md)
