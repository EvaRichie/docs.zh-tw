---
title: XML 序列化的範例
description: 這些程式碼範例會顯示 advanced 案例，包括如何使用 XML 序列化來產生符合 XML 架構檔的 XML 資料流程。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- XML serialization, examples
- arrays, serializing
- ICollection interface, serializing
- XmlSerializer class, serializing
- serialization, examples
- DataSet class, serializing
- XML Schema, serializing
ms.assetid: eec46337-9696-435b-a375-dc5effae6992
ms.openlocfilehash: 98cc4a983c9703e6c5ab132f6110a327c6081b6c
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84289625"
---
# <a name="examples-of-xml-serialization"></a><span data-ttu-id="8b9bf-103">XML 序列化的範例</span><span class="sxs-lookup"><span data-stu-id="8b9bf-103">Examples of XML Serialization</span></span>

<span data-ttu-id="8b9bf-104">XML 序列化的形式不只一種，從簡單到複雜都有。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-104">XML serialization can take more than one form, from simple to complex.</span></span> <span data-ttu-id="8b9bf-105">例如，您可序列化僅包含公用欄位及屬性的類別，如 [XML 序列化簡介](introducing-xml-serialization.md)中所示。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-105">For example, you can serialize a class that simply consists of public fields and properties, as shown in [Introducing XML Serialization](introducing-xml-serialization.md).</span></span> <span data-ttu-id="8b9bf-106">下列程式碼範例說明各種不同的進階案例，包括如何使用 XML 序列化以產生符合特定 XML 結構描述 (XSD) 文件的 XML 資料流。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-106">The following code examples address various advanced scenarios, including how to use XML serialization to generate an XML stream that conforms to a specific XML Schema (XSD) document.</span></span>

## <a name="serializing-a-dataset"></a><span data-ttu-id="8b9bf-107">序列化資料集</span><span class="sxs-lookup"><span data-stu-id="8b9bf-107">Serializing a DataSet</span></span>

<span data-ttu-id="8b9bf-108">除了序列化公用類別的執行個體之外，<xref:System.Data.DataSet> 的執行個體也能序列化，如下列程式碼範例所示。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-108">Besides serializing an instance of a public class, an instance of a <xref:System.Data.DataSet> can also be serialized, as shown in the following code example.</span></span>

```vb
Private Sub SerializeDataSet(filename As String)
    Dim ser As XmlSerializer = new XmlSerializer(GetType(DataSet))
    ' Creates a DataSet; adds a table, column, and ten rows.
    Dim ds As DataSet = new DataSet("myDataSet")
    Dim t As DataTable = new DataTable("table1")
    Dim c As DataColumn = new DataColumn("thing")
    t.Columns.Add(c)
    ds.Tables.Add(t)
    Dim r As DataRow
    Dim i As Integer
    for i = 0 to 10
        r = t.NewRow()
        r(0) = "Thing " &  i
        t.Rows.Add(r)
    Next
    Dim writer As TextWriter = new StreamWriter(filename)
    ser.Serialize(writer, ds)
    writer.Close()
End Sub
```

```csharp
private void SerializeDataSet(string filename){
    XmlSerializer ser = new XmlSerializer(typeof(DataSet));

    // Creates a DataSet; adds a table, column, and ten rows.
    DataSet ds = new DataSet("myDataSet");
    DataTable t = new DataTable("table1");
    DataColumn c = new DataColumn("thing");
    t.Columns.Add(c);
    ds.Tables.Add(t);
    DataRow r;
    for(int i = 0; i<10;i++){
        r = t.NewRow();
        r[0] = "Thing " + i;
        t.Rows.Add(r);
    }
    TextWriter writer = new StreamWriter(filename);
    ser.Serialize(writer, ds);
    writer.Close();
}
```

## <a name="serializing-an-xmlelement-and-xmlnode"></a><span data-ttu-id="8b9bf-109">序列化 XmlElement 與 XmlNode</span><span class="sxs-lookup"><span data-stu-id="8b9bf-109">Serializing an XmlElement and XmlNode</span></span>

<span data-ttu-id="8b9bf-110">您也可以序列化 <xref:System.Xml.XmlElement> 或類別的實例 <xref:System.Xml.XmlNode> ，如下列程式碼範例所示。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-110">You can also serialize instances of an <xref:System.Xml.XmlElement> or <xref:System.Xml.XmlNode> class, as shown in the following code example.</span></span>

```vb
private Sub SerializeElement(filename As String)
    Dim ser As XmlSerializer = new XmlSerializer(GetType(XmlElement))
    Dim myElement As XmlElement = _
    new XmlDocument().CreateElement("MyElement", "ns")
    myElement.InnerText = "Hello World"
    Dim writer As TextWriter = new StreamWriter(filename)
    ser.Serialize(writer, myElement)
    writer.Close()
End Sub

Private Sub SerializeNode(filename As String)
    Dim ser As XmlSerializer = _
    new XmlSerializer(GetType(XmlNode))
    Dim myNode As XmlNode = new XmlDocument(). _
    CreateNode(XmlNodeType.Element, "MyNode", "ns")
    myNode.InnerText = "Hello Node"
    Dim writer As TextWriter = new StreamWriter(filename)
    ser.Serialize(writer, myNode)
    writer.Close()
End Sub
```

```csharp
private void SerializeElement(string filename){
    XmlSerializer ser = new XmlSerializer(typeof(XmlElement));
    XmlElement myElement=
    new XmlDocument().CreateElement("MyElement", "ns");
    myElement.InnerText = "Hello World";
    TextWriter writer = new StreamWriter(filename);
    ser.Serialize(writer, myElement);
    writer.Close();
}

private void SerializeNode(string filename){
    XmlSerializer ser = new XmlSerializer(typeof(XmlNode));
    XmlNode myNode= new XmlDocument().
    CreateNode(XmlNodeType.Element, "MyNode", "ns");
    myNode.InnerText = "Hello Node";
    TextWriter writer = new StreamWriter(filename);
    ser.Serialize(writer, myNode);
    writer.Close();
}
```

## <a name="serializing-a-class-that-contains-a-field-returning-a-complex-object"></a><span data-ttu-id="8b9bf-111">序列化包含傳回複雜物件之欄位的類別</span><span class="sxs-lookup"><span data-stu-id="8b9bf-111">Serializing a Class that Contains a Field Returning a Complex Object</span></span>

<span data-ttu-id="8b9bf-112">如果屬性或欄位傳回複雜物件 (例如陣列或類別執行個體)，<xref:System.Xml.Serialization.XmlSerializer> 會將它轉換為主要 XML 文件中的巢狀項目。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-112">If a property or field returns a complex object (such as an array or a class instance), the <xref:System.Xml.Serialization.XmlSerializer> converts it to an element nested within the main XML document.</span></span> <span data-ttu-id="8b9bf-113">例如，下列程式碼範例中的第一個類別，會傳回第二個類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-113">For example, the first class in the following code example returns an instance of the second class.</span></span>

```vb
Public Class PurchaseOrder
    Public MyAddress As Address
End Class

Public Class Address
    Public FirstName As String
End Class
```

```csharp
public class PurchaseOrder
{
    public Address MyAddress;
}
public class Address
{
    public string FirstName;
}
```

<span data-ttu-id="8b9bf-114">序列化 XML 輸出可能類似於下列項目。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-114">The serialized XML output might resemble the following.</span></span>

```xml
<PurchaseOrder>
    <MyAddress>
        <FirstName>George</FirstName>
    </MyAddress>
</PurchaseOrder>
```

## <a name="serializing-an-array-of-objects"></a><span data-ttu-id="8b9bf-115">序列化物件陣列</span><span class="sxs-lookup"><span data-stu-id="8b9bf-115">Serializing an Array of Objects</span></span>

<span data-ttu-id="8b9bf-116">您也可序列化傳回物件陣列的欄位，如下列程式碼範例所示。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-116">You can also serialize a field that returns an array of objects, as shown in the following code example.</span></span>

```vb
Public Class PurchaseOrder
    public ItemsOrders () As Item
End Class

Public Class Item
    Public ItemID As String
    Public ItemPrice As decimal
End Class
```

```csharp
public class PurchaseOrder
{
    public Item [] ItemsOrders;
}

public class Item
{
    public string ItemID;
    public decimal ItemPrice;
}
```

<span data-ttu-id="8b9bf-117">如果兩個項目已設定順序，則已序列化的類別執行個體可能類似於下列項目。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-117">The serialized class instance might resemble the following, if two items are ordered.</span></span>

```xml
<PurchaseOrder xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  xmlns:xsd="http://www.w3.org/2001/XMLSchema">
    <ItemsOrders>
        <Item>
            <ItemID>aaa111</ItemID>
            <ItemPrice>34.22</ItemPrice>
        </Item>
        <Item>
            <ItemID>bbb222</ItemID>
            <ItemPrice>2.89</ItemPrice>
        </Item>
    </ItemsOrders>
</PurchaseOrder>
```

## <a name="serializing-a-class-that-implements-the-icollection-interface"></a><span data-ttu-id="8b9bf-118">序列化實作 ICollection 介面的類別</span><span class="sxs-lookup"><span data-stu-id="8b9bf-118">Serializing a Class that Implements the ICollection Interface</span></span>

<span data-ttu-id="8b9bf-119">您可以實作 <xref:System.Collections.ICollection> 介面來建立自己的集合類別，並且使用 <xref:System.Xml.Serialization.XmlSerializer> 對這些類別的執行個體序列化。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-119">You can create your own collection classes by implementing the <xref:System.Collections.ICollection> interface, and use the <xref:System.Xml.Serialization.XmlSerializer> to serialize instances of these classes.</span></span> <span data-ttu-id="8b9bf-120">請注意，當類別實作 <xref:System.Collections.ICollection> 介面時，只會序列化該類別包含的集合。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-120">Note that when a class implements the <xref:System.Collections.ICollection> interface, only the collection contained by the class is serialized.</span></span> <span data-ttu-id="8b9bf-121">加入至該類別的任何公共屬性或欄位都不會序列化。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-121">Any public properties or fields added to the class will not be serialized.</span></span> <span data-ttu-id="8b9bf-122">該類別必須包含要序列化的 **Add** 方法以及 **Item** 屬性 (C# 索引子)。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-122">The class must include an **Add** method and an **Item** property (C# indexer) to be serialized.</span></span>

```vb
Imports System.Collections
Imports System.IO
Imports System.Xml.Serialization

Public Class Test
    Shared Sub Main()
        Dim t As Test= new Test()
        t.SerializeCollection("coll.xml")
    End Sub

    Private Sub SerializeCollection(filename As String)
        Dim Emps As Employees  = new Employees()
        ' Note that only the collection is serialized -- not the
        ' CollectionName or any other public property of the class.
        Emps.CollectionName = "Employees"
        Dim John100 As Employee = new Employee("John", "100xxx")
        Emps.Add(John100)
        Dim x As XmlSerializer = new XmlSerializer(GetType(Employees))
        Dim writer As TextWriter = new StreamWriter(filename)
        x.Serialize(writer, Emps)
        writer.Close()
    End Sub
End Class

Public Class Employees
    Implements ICollection
    Public CollectionName As String
    Private empArray As ArrayList = new ArrayList()

    Public ReadOnly Default Overloads _
    Property Item(index As Integer) As Employee
        get
        return CType (empArray(index), Employee)
        End Get
    End Property

    Public Sub CopyTo(a As Array, index As Integer) _
    Implements ICollection.CopyTo
        empArray.CopyTo(a, index)
    End Sub

    Public ReadOnly Property Count () As integer Implements _
    ICollection.Count
        get
            Count = empArray.Count
        End Get

    End Property

    Public ReadOnly Property SyncRoot ()As Object _
    Implements ICollection.SyncRoot
        get
        return me
        End Get
    End Property

    Public ReadOnly Property IsSynchronized () As Boolean _
    Implements ICollection.IsSynchronized
        get
        return false
        End Get
    End Property

    Public Function GetEnumerator() As IEnumerator _
    Implements IEnumerable.GetEnumerator

        return empArray.GetEnumerator()
    End Function

    Public Function Add(newEmployee As Employee) As Integer
        empArray.Add(newEmployee)
        return empArray.Count
    End Function
End Class

Public Class Employee
    Public EmpName As String
    Public EmpID As String

    Public Sub New ()
    End Sub

    Public Sub New (newName As String , newID As String )
        EmpName = newName
        EmpID = newID
    End Sub
End Class
```

```csharp
using System;
using System.Collections;
using System.IO;
using System.Xml.Serialization;

public class Test {
    static void Main(){
        Test t = new Test();
        t.SerializeCollection("coll.xml");
    }

    private void SerializeCollection(string filename){
        Employees Emps = new Employees();
        // Note that only the collection is serialized -- not the
        // CollectionName or any other public property of the class.
        Emps.CollectionName = "Employees";
        Employee John100 = new Employee("John", "100xxx");
        Emps.Add(John100);
        XmlSerializer x = new XmlSerializer(typeof(Employees));
        TextWriter writer = new StreamWriter(filename);
        x.Serialize(writer, Emps);
    }
}
public class Employees:ICollection {
    public string CollectionName;
    private ArrayList empArray = new ArrayList();

    public Employee this[int index]{
        get{return (Employee) empArray[index];}
    }

    public void CopyTo(Array a, int index){
        empArray.CopyTo(a, index);
    }
    public int Count{
        get{return empArray.Count;}
    }
    public object SyncRoot{
        get{return this;}
    }
    public bool IsSynchronized{
        get{return false;}
    }
    public IEnumerator GetEnumerator(){
        return empArray.GetEnumerator();
    }

    public void Add(Employee newEmployee){
        empArray.Add(newEmployee);
    }
}

public class Employee {
    public string EmpName;
    public string EmpID;
    public Employee(){}
    public Employee(string empName, string empID){
        EmpName = empName;
        EmpID = empID;
    }
}
```

## <a name="purchase-order-example"></a><span data-ttu-id="8b9bf-123">採購單範例</span><span class="sxs-lookup"><span data-stu-id="8b9bf-123">Purchase Order Example</span></span>

<span data-ttu-id="8b9bf-124">您可以將下列範例程式碼剪下並貼至重新命名為 .cs 或 .vb 副檔名的文字檔。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-124">You can cut and paste the following example code into a text file renamed with a .cs or .vb file name extension.</span></span> <span data-ttu-id="8b9bf-125">使用 C# 或 Visual Basic 編譯器編譯檔案。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-125">Use the C# or Visual Basic compiler to compile the file.</span></span> <span data-ttu-id="8b9bf-126">然後使用可執行檔的名稱執行它。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-126">Then run it using the name of the executable.</span></span>

<span data-ttu-id="8b9bf-127">此範例使用簡單的案例，顯示如何使用 <xref:System.Xml.Serialization.XmlSerializer.Serialize%2A> 方法將物件的執行個體建立及序列化為檔案資料流。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-127">This example uses a simple scenario to demonstrate how an instance of an object is created and serialized into a file stream using the <xref:System.Xml.Serialization.XmlSerializer.Serialize%2A> method.</span></span> <span data-ttu-id="8b9bf-128">XML 資料流已儲存成檔案，然後使用 <xref:System.Xml.Serialization.XmlSerializer.Deserialize%2A> 方法將相同檔案讀回並重新建構成為原始物件的複本。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-128">The XML stream is saved to a file, and the same file is then read back and reconstructed into a copy of the original object using the <xref:System.Xml.Serialization.XmlSerializer.Deserialize%2A> method.</span></span>

<span data-ttu-id="8b9bf-129">在此範例中，會序列化名為 `PurchaseOrder` 的類別，然後再將其還原序列化。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-129">In this example, a class named `PurchaseOrder` is serialized and then deserialized.</span></span> <span data-ttu-id="8b9bf-130">也包含名為 `Address` 的第二類別，因為名為 `ShipTo` 的公用欄位必須設定為 `Address`。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-130">A second class named `Address` is also included because the public field named `ShipTo` must be set to an `Address`.</span></span> <span data-ttu-id="8b9bf-131">同樣地，會包含 `OrderedItem` 類別，因為 `OrderedItem` 物件的陣列必須設定為 `OrderedItems` 欄位。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-131">Similarly, an `OrderedItem` class is included because an array of `OrderedItem` objects must be set to the `OrderedItems` field.</span></span> <span data-ttu-id="8b9bf-132">最後，名為 `Test` 的類別包含序列化與還原序列化類別的程式碼。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-132">Finally, a class named `Test` contains the code that serializes and deserializes the classes.</span></span>

<span data-ttu-id="8b9bf-133">`CreatePO` 方法會建立 `PurchaseOrder`、`Address` 和 `OrderedItem` 類別物件，並且設定公用欄位的值。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-133">The `CreatePO` method creates the `PurchaseOrder`, `Address`, and `OrderedItem` class objects, and sets the public field values.</span></span> <span data-ttu-id="8b9bf-134">該方法也建構用來序列化及還原序列化 之  類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-134">The method also constructs an instance of the <xref:System.Xml.Serialization.XmlSerializer> class that is used to serialize and deserialize the `PurchaseOrder`.</span></span> <span data-ttu-id="8b9bf-135">請注意，程式碼把要序列化之類別的型別傳遞給建構函式。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-135">Note that the code passes the type of the class that will be serialized to the constructor.</span></span> <span data-ttu-id="8b9bf-136">程式碼也建立用來將 XML 資料流寫入 XML 文件的 `FileStream`。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-136">The code also creates a `FileStream` that is used to write the XML stream to an XML document.</span></span>

<span data-ttu-id="8b9bf-137">`ReadPo` 方法比較簡單。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-137">The `ReadPo` method is a little simpler.</span></span> <span data-ttu-id="8b9bf-138">它只會建立要還原序列化的物件，並讀出它們的值。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-138">It just creates objects to deserialize and reads out their values.</span></span> <span data-ttu-id="8b9bf-139">如同 `CreatePo` 方法，您必須先建立 <xref:System.Xml.Serialization.XmlSerializer> ，傳遞要還原序列化之類別的型別，以還原序列化為函式。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-139">As with the `CreatePo` method, you must first construct an <xref:System.Xml.Serialization.XmlSerializer>, passing the type of the class to be deserialized to the constructor.</span></span> <span data-ttu-id="8b9bf-140">同時，需要有 <xref:System.IO.FileStream> 讀取 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-140">Also, a <xref:System.IO.FileStream> is required to read the XML document.</span></span> <span data-ttu-id="8b9bf-141">若要還原序列化物件，以 <xref:System.Xml.Serialization.XmlSerializer.Deserialize%2A> 做為引數呼叫 <xref:System.IO.FileStream> 方法。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-141">To deserialize the objects, call the <xref:System.Xml.Serialization.XmlSerializer.Deserialize%2A> method with the <xref:System.IO.FileStream> as an argument.</span></span> <span data-ttu-id="8b9bf-142">還原序列化物件必須轉型為型別 的物件變數。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-142">The deserialized object must be cast to an object variable of type `PurchaseOrder`.</span></span> <span data-ttu-id="8b9bf-143">然後程式碼會讀取已還原序列化的 值。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-143">The code then reads the values of the deserialized `PurchaseOrder`.</span></span> <span data-ttu-id="8b9bf-144">請注意，您也可以讀取已建立的 PO.xml 檔案，檢視實際的 XML 輸出。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-144">Note that you can also read the PO.xml file that is created to see the actual XML output.</span></span>

```vb
Imports System.IO
Imports System.Xml
Imports System.Xml.Serialization
Imports Microsoft.VisualBasic

' The XmlRoot attribute allows you to set an alternate name
' (PurchaseOrder) for the XML element and its namespace. By
' default, the XmlSerializer uses the class name. The attribute
' also allows you to set the XML namespace for the element. Lastly,
' the attribute sets the IsNullable property, which specifies whether
' the xsi:null attribute appears if the class instance is set to
' a null reference.
<XmlRoot("PurchaseOrder", _
 Namespace := "http://www.cpandl.com", IsNullable := False)> _
Public Class PurchaseOrder
    Public ShipTo As Address
    Public OrderDate As String
    ' The XmlArrayAttribute changes the XML element name
    ' from the default of "OrderedItems" to "Items".
    <XmlArray("Items")> _
    Public OrderedItems() As OrderedItem
    Public SubTotal As Decimal
    Public ShipCost As Decimal
    Public TotalCost As Decimal
End Class

Public Class Address
    ' The XmlAttribute attribute instructs the XmlSerializer to serialize the
    ' Name field as an XML attribute instead of an XML element (XML element is
    ' the default behavior).
    <XmlAttribute()> _
    Public Name As String
    Public Line1 As String

    ' Setting the IsNullable property to false instructs the
    ' XmlSerializer that the XML attribute will not appear if
    ' the City field is set to a null reference.
    <XmlElement(IsNullable := False)> _
    Public City As String
    Public State As String
    Public Zip As String
End Class

Public Class OrderedItem
    Public ItemName As String
    Public Description As String
    Public UnitPrice As Decimal
    Public Quantity As Integer
    Public LineTotal As Decimal

    ' Calculate is a custom method that calculates the price per item
    ' and stores the value in a field.
    Public Sub Calculate()
    LineTotal = UnitPrice * Quantity
    End Sub
End Class

Public Class Test
        Public Shared Sub Main()
    ' Read and write purchase orders.
    Dim t As New Test()
    t.CreatePO("po.xml")
    t.ReadPO("po.xml")
    End Sub

    Private Sub CreatePO(filename As String)
        ' Creates an instance of the XmlSerializer class;
        ' specifies the type of object to serialize.
        Dim serializer As New XmlSerializer(GetType(PurchaseOrder))
        Dim writer As New StreamWriter(filename)
        Dim po As New PurchaseOrder()

        ' Creates an address to ship and bill to.
        Dim billAddress As New Address()
        billAddress.Name = "Teresa Atkinson"
        billAddress.Line1 = "1 Main St."
        billAddress.City = "AnyTown"
        billAddress.State = "WA"
        billAddress.Zip = "00000"
        ' Set ShipTo and BillTo to the same addressee.
        po.ShipTo = billAddress
        po.OrderDate = System.DateTime.Now.ToLongDateString()

        ' Creates an OrderedItem.
        Dim i1 As New OrderedItem()
        i1.ItemName = "Widget S"
        i1.Description = "Small widget"
        i1.UnitPrice = CDec(5.23)
        i1.Quantity = 3
        i1.Calculate()

        ' Inserts the item into the array.
        Dim items(0) As OrderedItem
        items(0) = i1
        po.OrderedItems = items
        ' Calculates the total cost.
        Dim subTotal As New Decimal()
        Dim oi As OrderedItem
        For Each oi In  items
            subTotal += oi.LineTotal
        Next oi
        po.SubTotal = subTotal
        po.ShipCost = CDec(12.51)
        po.TotalCost = po.SubTotal + po.ShipCost
        ' Serializes the purchase order, and close the TextWriter.
        serializer.Serialize(writer, po)
        writer.Close()
    End Sub

    Protected Sub ReadPO(filename As String)
        ' Creates an instance of the XmlSerializer class;
        ' specifies the type of object to be deserialized.
        Dim serializer As New XmlSerializer(GetType(PurchaseOrder))
        ' If the XML document has been altered with unknown
        ' nodes or attributes, handles them with the
        ' UnknownNode and UnknownAttribute events.
        AddHandler serializer.UnknownNode, AddressOf serializer_UnknownNode
        AddHandler serializer.UnknownAttribute, AddressOf _
        serializer_UnknownAttribute

        ' A FileStream is needed to read the XML document.
        Dim fs As New FileStream(filename, FileMode.Open)
        ' Declare an object variable of the type to be deserialized.
        Dim po As PurchaseOrder
        ' Uses the Deserialize method to restore the object's state
        ' with data from the XML document.
        po = CType(serializer.Deserialize(fs), PurchaseOrder)
        ' Reads the order date.
        Console.WriteLine(("OrderDate: " & po.OrderDate))

        ' Reads the shipping address.
        Dim shipTo As Address = po.ShipTo
        ReadAddress(shipTo, "Ship To:")
        ' Reads the list of ordered items.
        Dim items As OrderedItem() = po.OrderedItems
        Console.WriteLine("Items to be shipped:")
        Dim oi As OrderedItem
        For Each oi In items
            Console.WriteLine((ControlChars.Tab & oi.ItemName & _
            ControlChars.Tab & _
                oi.Description & ControlChars.Tab & oi.UnitPrice & _
                ControlChars.Tab & _
                oi.Quantity & ControlChars.Tab & oi.LineTotal))
        Next oi
        ' Reads the subtotal, shipping cost, and total cost.
        Console.WriteLine((ControlChars.Cr & New String _
        (ControlChars.Tab, 5) & _
        " Subtotal" & ControlChars.Tab & po.SubTotal & ControlChars.Cr & _
        New String(ControlChars.Tab, 5) & " Shipping" & ControlChars.Tab & _
        po.ShipCost & ControlChars.Cr &  New String(ControlChars.Tab, 5) & _
        " Total" & New String(ControlChars.Tab, 2) & po.TotalCost))
    End Sub

    Protected Sub ReadAddress(a As Address, label As String)
        ' Reads the fields of the Address.
        Console.WriteLine(label)
        Console.Write((ControlChars.Tab & a.Name & ControlChars.Cr & _
        ControlChars.Tab & a.Line1 & ControlChars.Cr & ControlChars.Tab & _
        a.City & ControlChars.Tab & a.State & ControlChars.Cr & _
        ControlChars.Tab & a.Zip & ControlChars.Cr))
    End Sub

    Protected Sub serializer_UnknownNode(sender As Object, e As _
    XmlNodeEventArgs)
        Console.WriteLine(("Unknown Node:" & e.Name & _
        ControlChars.Tab & e.Text))
    End Sub

    Protected Sub serializer_UnknownAttribute(sender As Object, _
    e As XmlAttributeEventArgs)
        Dim attr As System.Xml.XmlAttribute = e.Attr
        Console.WriteLine(("Unknown attribute " & attr.Name & "='" & _
        attr.Value & "'"))
    End Sub 'serializer_UnknownAttribute
End Class 'Test
```

```csharp
using System;
using System.IO;
using System.Xml;
using System.Xml.Serialization;

// The XmlRoot attribute allows you to set an alternate name
// (PurchaseOrder) for the XML element and its namespace. By
// default, the XmlSerializer uses the class name. The attribute
// also allows you to set the XML namespace for the element. Lastly,
// the attribute sets the IsNullable property, which specifies whether
// the xsi:null attribute appears if the class instance is set to
// a null reference.
[XmlRoot("PurchaseOrder", Namespace="http://www.cpandl.com",
IsNullable = false)]
public class PurchaseOrder
{
    public Address ShipTo;
    public string OrderDate;
    // The XmlArray attribute changes the XML element name
    // from the default of "OrderedItems" to "Items".
    [XmlArray("Items")]
    public OrderedItem[] OrderedItems;
    public decimal SubTotal;
    public decimal ShipCost;
    public decimal TotalCost;
}

public class Address
{
    // The XmlAttribute attribute instructs the XmlSerializer to serialize the
    // Name field as an XML attribute instead of an XML element (XML element is
    // the default behavior).
    [XmlAttribute]
    public string Name;
    public string Line1;

    // Setting the IsNullable property to false instructs the
    // XmlSerializer that the XML attribute will not appear if
    // the City field is set to a null reference.
    [XmlElement(IsNullable = false)]
    public string City;
    public string State;
    public string Zip;
}

public class OrderedItem
{
    public string ItemName;
    public string Description;
    public decimal UnitPrice;
    public int Quantity;
    public decimal LineTotal;

    // Calculate is a custom method that calculates the price per item
    // and stores the value in a field.
    public void Calculate()
    {
        LineTotal = UnitPrice * Quantity;
    }
}

public class Test
{
    public static void Main()
    {
        // Read and write purchase orders.
        Test t = new Test();
        t.CreatePO("po.xml");
        t.ReadPO("po.xml");
    }

    private void CreatePO(string filename)
    {
        // Creates an instance of the XmlSerializer class;
        // specifies the type of object to serialize.
        XmlSerializer serializer =
        new XmlSerializer(typeof(PurchaseOrder));
        TextWriter writer = new StreamWriter(filename);
        PurchaseOrder po=new PurchaseOrder();

        // Creates an address to ship and bill to.
        Address billAddress = new Address();
        billAddress.Name = "Teresa Atkinson";
        billAddress.Line1 = "1 Main St.";
        billAddress.City = "AnyTown";
        billAddress.State = "WA";
        billAddress.Zip = "00000";
        // Sets ShipTo and BillTo to the same addressee.
        po.ShipTo = billAddress;
        po.OrderDate = System.DateTime.Now.ToLongDateString();

        // Creates an OrderedItem.
        OrderedItem i1 = new OrderedItem();
        i1.ItemName = "Widget S";
        i1.Description = "Small widget";
        i1.UnitPrice = (decimal) 5.23;
        i1.Quantity = 3;
        i1.Calculate();

        // Inserts the item into the array.
        OrderedItem [] items = {i1};
        po.OrderedItems = items;
        // Calculate the total cost.
        decimal subTotal = new decimal();
        foreach(OrderedItem oi in items)
        {
            subTotal += oi.LineTotal;
        }
        po.SubTotal = subTotal;
        po.ShipCost = (decimal) 12.51;
        po.TotalCost = po.SubTotal + po.ShipCost;
        // Serializes the purchase order, and closes the TextWriter.
        serializer.Serialize(writer, po);
        writer.Close();
    }

    protected void ReadPO(string filename)
    {
        // Creates an instance of the XmlSerializer class;
        // specifies the type of object to be deserialized.
        XmlSerializer serializer = new XmlSerializer(typeof(PurchaseOrder));
        // If the XML document has been altered with unknown
        // nodes or attributes, handles them with the
        // UnknownNode and UnknownAttribute events.
        serializer.UnknownNode+= new
        XmlNodeEventHandler(serializer_UnknownNode);
        serializer.UnknownAttribute+= new
        XmlAttributeEventHandler(serializer_UnknownAttribute);

        // A FileStream is needed to read the XML document.
        FileStream fs = new FileStream(filename, FileMode.Open);
        // Declares an object variable of the type to be deserialized.
        PurchaseOrder po;
        // Uses the Deserialize method to restore the object's state
        // with data from the XML document. */
        po = (PurchaseOrder) serializer.Deserialize(fs);
        // Reads the order date.
        Console.WriteLine ("OrderDate: " + po.OrderDate);

        // Reads the shipping address.
        Address shipTo = po.ShipTo;
        ReadAddress(shipTo, "Ship To:");
        // Reads the list of ordered items.
        OrderedItem [] items = po.OrderedItems;
        Console.WriteLine("Items to be shipped:");
        foreach(OrderedItem oi in items)
        {
            Console.WriteLine("\t"+
            oi.ItemName + "\t" +
            oi.Description + "\t" +
            oi.UnitPrice + "\t" +
            oi.Quantity + "\t" +
            oi.LineTotal);
        }
        // Reads the subtotal, shipping cost, and total cost.
        Console.WriteLine(
        "\n\t\t\t\t\t Subtotal\t" + po.SubTotal +
        "\n\t\t\t\t\t Shipping\t" + po.ShipCost +
        "\n\t\t\t\t\t Total\t\t" + po.TotalCost
        );
    }

    protected void ReadAddress(Address a, string label)
    {
        // Reads the fields of the Address.
        Console.WriteLine(label);
        Console.Write("\t"+
        a.Name +"\n\t" +
        a.Line1 +"\n\t" +
        a.City +"\t" +
        a.State +"\n\t" +
        a.Zip +"\n");
    }

    protected void serializer_UnknownNode
    (object sender, XmlNodeEventArgs e)
    {
        Console.WriteLine("Unknown Node:" +   e.Name + "\t" + e.Text);
    }

    protected void serializer_UnknownAttribute
    (object sender, XmlAttributeEventArgs e)
    {
        System.Xml.XmlAttribute attr = e.Attr;
        Console.WriteLine("Unknown attribute " +
        attr.Name + "='" + attr.Value + "'");
    }
}
```

<span data-ttu-id="8b9bf-145">XML 輸出可能類似下列所示。</span><span class="sxs-lookup"><span data-stu-id="8b9bf-145">The XML output might resemble the following.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<PurchaseOrder xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://www.cpandl.com">
    <ShipTo Name="Teresa Atkinson">
        <Line1>1 Main St.</Line1>
        <City>AnyTown</City>
        <State>WA</State>
        <Zip>00000</Zip>
    </ShipTo>
    <OrderDate>Wednesday, June 27, 2001</OrderDate>
    <Items>
        <OrderedItem>
            <ItemName>Widget S</ItemName>
            <Description>Small widget</Description>
            <UnitPrice>5.23</UnitPrice>
            <Quantity>3</Quantity>
            <LineTotal>15.69</LineTotal>
        </OrderedItem>
    </Items>
    <SubTotal>15.69</SubTotal>
    <ShipCost>12.51</ShipCost>
    <TotalCost>28.2</TotalCost>
</PurchaseOrder>
```

## <a name="see-also"></a><span data-ttu-id="8b9bf-146">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8b9bf-146">See also</span></span>

- [<span data-ttu-id="8b9bf-147">XML 序列化簡介</span><span class="sxs-lookup"><span data-stu-id="8b9bf-147">Introducing XML Serialization</span></span>](introducing-xml-serialization.md)
- [<span data-ttu-id="8b9bf-148">使用屬性控制 XML 序列化</span><span class="sxs-lookup"><span data-stu-id="8b9bf-148">Controlling XML Serialization Using Attributes</span></span>](controlling-xml-serialization-using-attributes.md)
- [<span data-ttu-id="8b9bf-149">控制 XML 序列化的屬性</span><span class="sxs-lookup"><span data-stu-id="8b9bf-149">Attributes That Control XML Serialization</span></span>](attributes-that-control-xml-serialization.md)
- [<span data-ttu-id="8b9bf-150">XmlSerializer 類別</span><span class="sxs-lookup"><span data-stu-id="8b9bf-150">XmlSerializer Class</span></span>](xref:System.Xml.Serialization.XmlSerializer)
- [<span data-ttu-id="8b9bf-151">HOW TO：序列化物件</span><span class="sxs-lookup"><span data-stu-id="8b9bf-151">How to: Serialize an Object</span></span>](how-to-serialize-an-object.md)
- [<span data-ttu-id="8b9bf-152">如何：還原序列化物件</span><span class="sxs-lookup"><span data-stu-id="8b9bf-152">How to: Deserialize an Object</span></span>](how-to-deserialize-an-object.md)
