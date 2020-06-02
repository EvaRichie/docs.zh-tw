---
title: 從 XML 載入資料集
description: 瞭解如何從 XML 將內容新增至 ADO.NET 資料集。 .NET Framework 提供要載入的專案和資料集結構的彈性。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 49c083b7-a5ed-41cf-aabc-5aaba96f00e6
ms.openlocfilehash: 8c81e6e29678fe2e30af7c15d8d6e90f23dd0762
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286879"
---
# <a name="loading-a-dataset-from-xml"></a><span data-ttu-id="4fcff-104">從 XML 載入資料集</span><span class="sxs-lookup"><span data-stu-id="4fcff-104">Loading a DataSet from XML</span></span>
<span data-ttu-id="4fcff-105">可以從 XML 資料流或文件建立 ADO.NET <xref:System.Data.DataSet> 的內容。</span><span class="sxs-lookup"><span data-stu-id="4fcff-105">The contents of an ADO.NET <xref:System.Data.DataSet> can be created from an XML stream or document.</span></span> <span data-ttu-id="4fcff-106">此外，使用 .NET Framework 可讓您在決定從 XML 載入何種資訊，以及如何建立 <xref:System.Data.DataSet> 的結構描述或關聯式結構時，擁有相當大的彈性。</span><span class="sxs-lookup"><span data-stu-id="4fcff-106">In addition, with the .NET Framework you have great flexibility over what information is loaded from XML, and how the schema or relational structure of the <xref:System.Data.DataSet> is created.</span></span>  
  
 <span data-ttu-id="4fcff-107">若要使用 <xref:System.Data.DataSet> XML 中的資料填入，請使用物件的**ReadXml**方法 <xref:System.Data.DataSet> 。</span><span class="sxs-lookup"><span data-stu-id="4fcff-107">To fill a <xref:System.Data.DataSet> with data from XML, use the **ReadXml** method of the <xref:System.Data.DataSet> object.</span></span> <span data-ttu-id="4fcff-108">**ReadXml**方法會從檔案、資料流程或**XmlReader**讀取，並以 XML 的來源加上選擇性的**XmlReadMode**引數作為引數。</span><span class="sxs-lookup"><span data-stu-id="4fcff-108">The **ReadXml** method reads from a file, a stream, or an **XmlReader**, and takes as arguments the source of the XML plus an optional **XmlReadMode** argument.</span></span> <span data-ttu-id="4fcff-109">如需**XmlReader**的詳細資訊，請參閱[使用 XmlTextReader 讀取 XML 資料](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/tfz3cz6w(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="4fcff-109">For more information about the **XmlReader**, see [Reading XML Data with XmlTextReader](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/tfz3cz6w(v=vs.100)).</span></span> <span data-ttu-id="4fcff-110">**ReadXml**方法會讀取 XML 資料流程或檔的內容，並載入 <xref:System.Data.DataSet> 具有資料的。</span><span class="sxs-lookup"><span data-stu-id="4fcff-110">The **ReadXml** method reads the contents of the XML stream or document and loads the <xref:System.Data.DataSet> with data.</span></span> <span data-ttu-id="4fcff-111">它也會 <xref:System.Data.DataSet> 根據指定的**XmlReadMode**以及是否已有關系結構描述，建立的關聯式結構描述。</span><span class="sxs-lookup"><span data-stu-id="4fcff-111">It will also create the relational schema of the <xref:System.Data.DataSet> depending on the **XmlReadMode** specified and whether or not a relational schema already exists.</span></span>  
  
 <span data-ttu-id="4fcff-112">下表描述**XmlReadMode**引數的選項。</span><span class="sxs-lookup"><span data-stu-id="4fcff-112">The following table describes the options for the **XmlReadMode** argument.</span></span>  
  
|<span data-ttu-id="4fcff-113">選項</span><span class="sxs-lookup"><span data-stu-id="4fcff-113">Option</span></span>|<span data-ttu-id="4fcff-114">描述</span><span class="sxs-lookup"><span data-stu-id="4fcff-114">Description</span></span>|  
|------------|-----------------|  
|<span data-ttu-id="4fcff-115">**Auto**</span><span class="sxs-lookup"><span data-stu-id="4fcff-115">**Auto**</span></span>|<span data-ttu-id="4fcff-116">此為預設值。</span><span class="sxs-lookup"><span data-stu-id="4fcff-116">This is the default.</span></span> <span data-ttu-id="4fcff-117">檢查 XML 並依下列順序選擇最適當的選項：</span><span class="sxs-lookup"><span data-stu-id="4fcff-117">Examines the XML and chooses the most appropriate option in the following order:</span></span><br /><br /> <span data-ttu-id="4fcff-118">-如果 XML 為 DiffGram，則使用**diffgram** 。</span><span class="sxs-lookup"><span data-stu-id="4fcff-118">-   If the XML is a DiffGram, **DiffGram** is used.</span></span><br /><span data-ttu-id="4fcff-119">-如果 <xref:System.Data.DataSet> 包含架構，或 XML 包含內嵌架構，則會使用**ReadSchema** 。</span><span class="sxs-lookup"><span data-stu-id="4fcff-119">-   If the <xref:System.Data.DataSet> contains a schema or the XML contains an inline schema, **ReadSchema** is used.</span></span><br /><span data-ttu-id="4fcff-120">-如果 <xref:System.Data.DataSet> 不包含架構，而且 XML 不包含內嵌架構，則會使用**InferSchema** 。</span><span class="sxs-lookup"><span data-stu-id="4fcff-120">-   If the <xref:System.Data.DataSet> does not contain a schema and the XML does not contain an inline schema, **InferSchema** is used.</span></span><br /><br /> <span data-ttu-id="4fcff-121">如果您知道要讀取的 XML 格式，建議您設定明確的**XmlReadMode**，而不是接受**自動**預設值，以達到最佳效能。</span><span class="sxs-lookup"><span data-stu-id="4fcff-121">If you know the format of the XML being read, for best performance it is recommended that you set an explicit **XmlReadMode**, rather than accept the **Auto** default.</span></span>|  
|<span data-ttu-id="4fcff-122">**ReadSchema**</span><span class="sxs-lookup"><span data-stu-id="4fcff-122">**ReadSchema**</span></span>|<span data-ttu-id="4fcff-123">讀取任何內嵌結構描述，並載入資料和結構描述。</span><span class="sxs-lookup"><span data-stu-id="4fcff-123">Reads any inline schema and loads the data and schema.</span></span><br /><br /> <span data-ttu-id="4fcff-124">如果 <xref:System.Data.DataSet> 已經包含結構描述，則會將新資料表從內嵌結構描述加入 <xref:System.Data.DataSet> 的現有結構描述中。</span><span class="sxs-lookup"><span data-stu-id="4fcff-124">If the <xref:System.Data.DataSet> already contains a schema, new tables are added from the inline schema to the existing schema in the <xref:System.Data.DataSet>.</span></span> <span data-ttu-id="4fcff-125">如果內嵌結構描述中的任何資料表已經存在於 <xref:System.Data.DataSet> 中，則會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="4fcff-125">If any tables in the inline schema already exist in the <xref:System.Data.DataSet>, an exception is thrown.</span></span> <span data-ttu-id="4fcff-126">您將無法使用 XmlReadMode 修改現有資料表的架構。 **ReadSchema**。</span><span class="sxs-lookup"><span data-stu-id="4fcff-126">You will not be able to modify the schema of an existing table using **XmlReadMode.ReadSchema**.</span></span><br /><br /> <span data-ttu-id="4fcff-127">如果 <xref:System.Data.DataSet> 不包含結構描述，且沒有內嵌結構描述，則不會讀取任何資料。</span><span class="sxs-lookup"><span data-stu-id="4fcff-127">If the <xref:System.Data.DataSet> does not contain a schema, and there is no inline schema, no data is read.</span></span><br /><br /> <span data-ttu-id="4fcff-128">內嵌結構描述可使用 XML 結構描述定義語言 (XSD) 的結構描述來定義。</span><span class="sxs-lookup"><span data-stu-id="4fcff-128">Inline schema can be defined using XML Schema definition language (XSD) schema.</span></span> <span data-ttu-id="4fcff-129">如需將內嵌架構撰寫為 XML 架構的詳細資訊，請參閱[從 XML 架構（XSD）衍生資料集關聯式結構](deriving-dataset-relational-structure-from-xml-schema-xsd.md)。</span><span class="sxs-lookup"><span data-stu-id="4fcff-129">For details about writing inline schema as XML Schema, see [Deriving DataSet Relational Structure from XML Schema (XSD)](deriving-dataset-relational-structure-from-xml-schema-xsd.md).</span></span>|  
|<span data-ttu-id="4fcff-130">**IgnoreSchema**</span><span class="sxs-lookup"><span data-stu-id="4fcff-130">**IgnoreSchema**</span></span>|<span data-ttu-id="4fcff-131">忽略任何內嵌結構描述，並將資料載入現有的 <xref:System.Data.DataSet> 結構描述中。</span><span class="sxs-lookup"><span data-stu-id="4fcff-131">Ignores any inline schema and loads the data into the existing <xref:System.Data.DataSet> schema.</span></span> <span data-ttu-id="4fcff-132">任何與現有結構描述不相符的資料會被捨棄。</span><span class="sxs-lookup"><span data-stu-id="4fcff-132">Any data that does not match the existing schema is discarded.</span></span> <span data-ttu-id="4fcff-133">如果 <xref:System.Data.DataSet> 中沒有結構描述，則不會載入任何資料。</span><span class="sxs-lookup"><span data-stu-id="4fcff-133">If no schema exists in the <xref:System.Data.DataSet>, no data is loaded.</span></span><br /><br /> <span data-ttu-id="4fcff-134">如果資料為 DiffGram，則**IgnoreSchema**具有與 diffgram 相同的功能**DiffGram** *。*</span><span class="sxs-lookup"><span data-stu-id="4fcff-134">If the data is a DiffGram, **IgnoreSchema** has the same functionality as **DiffGram** *.*</span></span>|  
|<span data-ttu-id="4fcff-135">**InferSchema**</span><span class="sxs-lookup"><span data-stu-id="4fcff-135">**InferSchema**</span></span>|<span data-ttu-id="4fcff-136">忽略任何內嵌結構描述，並推斷每個 XML 資料結構的結構描述，然後載入資料。</span><span class="sxs-lookup"><span data-stu-id="4fcff-136">Ignores any inline schema and infers the schema per the structure of the XML data, then loads the data.</span></span><br /><br /> <span data-ttu-id="4fcff-137">如果 <xref:System.Data.DataSet> 已經包含結構描述，則會將資料行加入現有的資料表來擴充目前的結構描述。</span><span class="sxs-lookup"><span data-stu-id="4fcff-137">If the <xref:System.Data.DataSet> already contains a schema, the current schema is extended by adding columns to existing tables.</span></span> <span data-ttu-id="4fcff-138">如果沒有現有的資料表，則不會加入額外的資料表。</span><span class="sxs-lookup"><span data-stu-id="4fcff-138">Extra tables will not be added if there are not existing tables.</span></span> <span data-ttu-id="4fcff-139">如果推斷資料表已經存在但使用不同的命名空間，或者任何推斷的資料行與現有資料行衝突，便會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="4fcff-139">An exception is thrown if an inferred table already exists with a different namespace, or if any inferred columns conflict with existing columns.</span></span><br /><br /> <span data-ttu-id="4fcff-140">如需**ReadXmlSchema**如何從 xml 檔推斷架構的詳細資訊，請參閱[從 Xml 推斷資料集關聯式結構](inferring-dataset-relational-structure-from-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="4fcff-140">For details about how **ReadXmlSchema** infers a schema from an XML document, see [Inferring DataSet Relational Structure from XML](inferring-dataset-relational-structure-from-xml.md).</span></span>|  
|<span data-ttu-id="4fcff-141">**DiffGram**</span><span class="sxs-lookup"><span data-stu-id="4fcff-141">**DiffGram**</span></span>|<span data-ttu-id="4fcff-142">讀取 DiffGram 並將資料加入目前的結構描述。</span><span class="sxs-lookup"><span data-stu-id="4fcff-142">Reads a DiffGram and adds the data to the current schema.</span></span> <span data-ttu-id="4fcff-143">**DiffGram**會將新資料列與唯一識別碼值相符的現有資料列合併。</span><span class="sxs-lookup"><span data-stu-id="4fcff-143">**DiffGram** merges new rows with existing rows where the unique identifier values match.</span></span> <span data-ttu-id="4fcff-144">請參閱這個主題結尾處＜從 XML 合併資料＞。</span><span class="sxs-lookup"><span data-stu-id="4fcff-144">See "Merging Data from XML" at the end of this topic.</span></span> <span data-ttu-id="4fcff-145">如需 Diffgram 的詳細資訊，請參閱[diffgram](diffgrams.md)。</span><span class="sxs-lookup"><span data-stu-id="4fcff-145">For more information about DiffGrams, see [DiffGrams](diffgrams.md).</span></span>|  
|<span data-ttu-id="4fcff-146">**碎片**</span><span class="sxs-lookup"><span data-stu-id="4fcff-146">**Fragment**</span></span>|<span data-ttu-id="4fcff-147">繼續讀取多個 XML 片段，直到到達資料流末。</span><span class="sxs-lookup"><span data-stu-id="4fcff-147">Continues reading multiple XML fragments until the end of the stream is reached.</span></span> <span data-ttu-id="4fcff-148">與 <xref:System.Data.DataSet> 結構描述相符的片段會附加至適當的資料表。</span><span class="sxs-lookup"><span data-stu-id="4fcff-148">Fragments that match the <xref:System.Data.DataSet> schema are appended to the appropriate tables.</span></span> <span data-ttu-id="4fcff-149">與 <xref:System.Data.DataSet> 結構描述不相符的片段則會捨棄。</span><span class="sxs-lookup"><span data-stu-id="4fcff-149">Fragments that do not match the <xref:System.Data.DataSet> schema are discarded.</span></span>|  
  
> [!NOTE]
> <span data-ttu-id="4fcff-150">如果您將**XmlReader**傳遞至**ReadXml** ，並將其置於 XML 檔中，則**ReadXml**會讀取至下一個專案節點，並將其視為根項目，並讀取直到元素節點結尾為止。</span><span class="sxs-lookup"><span data-stu-id="4fcff-150">If you pass an **XmlReader** to **ReadXml** that is positioned part of the way into an XML document, **ReadXml** will read to the next element node and will treat that as the root element, reading until the end of the element node only.</span></span> <span data-ttu-id="4fcff-151">如果您指定**XmlReadMode**，則不適用此功能。</span><span class="sxs-lookup"><span data-stu-id="4fcff-151">This does not apply if you specify **XmlReadMode.Fragment**.</span></span>  
  
## <a name="dtd-entities"></a><span data-ttu-id="4fcff-152">DTD 實體</span><span class="sxs-lookup"><span data-stu-id="4fcff-152">DTD Entities</span></span>  
 <span data-ttu-id="4fcff-153">如果您的 XML 包含檔案類型定義（DTD）架構中所定義的實體，如果您嘗試藉 <xref:System.Data.DataSet> 由將檔案名、資料流程或非驗證**XmlReader**傳遞至**ReadXml**來載入，則會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="4fcff-153">If your XML contains entities defined in a document type definition (DTD) schema, an exception will be thrown if you attempt to load a <xref:System.Data.DataSet> by passing a file name, stream, or non-validating **XmlReader** to **ReadXml**.</span></span> <span data-ttu-id="4fcff-154">相反地，您必須建立**XmlValidatingReader**，並將**EntityHandling**設定為**EntityHandling entityhandling.expandentities**，並將您的**XmlValidatingReader**傳遞給**ReadXml**。</span><span class="sxs-lookup"><span data-stu-id="4fcff-154">Instead, you must create an **XmlValidatingReader**, with **EntityHandling** set to **EntityHandling.ExpandEntities**, and pass your **XmlValidatingReader** to **ReadXml**.</span></span> <span data-ttu-id="4fcff-155">**XmlValidatingReader**會在讀取之前展開實體 <xref:System.Data.DataSet> 。</span><span class="sxs-lookup"><span data-stu-id="4fcff-155">The **XmlValidatingReader** will expand the entities prior to being read by the <xref:System.Data.DataSet>.</span></span>  
  
 <span data-ttu-id="4fcff-156">下列程式碼範例顯示如何從 XML 資料流載入 <xref:System.Data.DataSet>。</span><span class="sxs-lookup"><span data-stu-id="4fcff-156">The following code examples show how to load a <xref:System.Data.DataSet> from an XML stream.</span></span> <span data-ttu-id="4fcff-157">第一個範例顯示要傳遞給**ReadXml**方法的檔案名。</span><span class="sxs-lookup"><span data-stu-id="4fcff-157">The first example shows a file name being passed to the **ReadXml** method.</span></span> <span data-ttu-id="4fcff-158">第二個範例顯示內含使用 <xref:System.IO.StringReader> 所載入之 XML 的字串。</span><span class="sxs-lookup"><span data-stu-id="4fcff-158">The second example shows a string that contains XML being loaded using a <xref:System.IO.StringReader>.</span></span>  
  
```vb  
Dim dataSet As DataSet = New DataSet  
dataSet.ReadXml("input.xml", XmlReadMode.ReadSchema)  
```  
  
```csharp  
DataSet dataSet = new DataSet();  
dataSet.ReadXml("input.xml", XmlReadMode.ReadSchema);  
```  
  
```vb  
Dim dataSet As DataSet = New DataSet  
Dim dataTable As DataTable = New DataTable("table1")  
dataTable.Columns.Add("col1", Type.GetType("System.String"))  
dataSet.Tables.Add(dataTable)  
  
Dim xmlData As String = "<XmlDS><table1><col1>Value1</col1></table1><table1><col1>Value2</col1></table1></XmlDS>"  
  
Dim xmlSR As System.IO.StringReader = New System.IO.StringReader(xmlData)  
  
dataSet.ReadXml(xmlSR, XmlReadMode.IgnoreSchema)  
```  
  
```csharp  
DataSet dataSet = new DataSet();  
DataTable dataTable = new DataTable("table1");  
dataTable.Columns.Add("col1", typeof(string));  
dataSet.Tables.Add(dataTable);  
  
string xmlData = "<XmlDS><table1><col1>Value1</col1></table1><table1><col1>Value2</col1></table1></XmlDS>";  
  
System.IO.StringReader xmlSR = new System.IO.StringReader(xmlData);  
  
dataSet.ReadXml(xmlSR, XmlReadMode.IgnoreSchema);  
```  
  
> [!NOTE]
> <span data-ttu-id="4fcff-159">如果您呼叫**ReadXml**來載入非常大的檔案，可能會遇到效能變慢的情況。</span><span class="sxs-lookup"><span data-stu-id="4fcff-159">If you call **ReadXml** to load a very large file, you may encounter slow performance.</span></span> <span data-ttu-id="4fcff-160">為確保**ReadXml**的最佳效能，請在大型檔案中， <xref:System.Data.DataTable.BeginLoadData%2A> 針對中的每個資料表呼叫方法， <xref:System.Data.DataSet> 然後呼叫**ReadXml**。</span><span class="sxs-lookup"><span data-stu-id="4fcff-160">To ensure best performance for **ReadXml**, on a large file, call the <xref:System.Data.DataTable.BeginLoadData%2A> method for each table in the <xref:System.Data.DataSet>, and then call **ReadXml**.</span></span> <span data-ttu-id="4fcff-161">最後再針對 <xref:System.Data.DataTable.EndLoadData%2A> 的每個資料表呼叫 <xref:System.Data.DataSet> (如下列範例所示)。</span><span class="sxs-lookup"><span data-stu-id="4fcff-161">Finally, call <xref:System.Data.DataTable.EndLoadData%2A> for each table in the <xref:System.Data.DataSet>, as shown in the following example.</span></span>  
  
```vb  
Dim dataTable As DataTable  
  
For Each dataTable In dataSet.Tables  
   dataTable.BeginLoadData()  
Next  
  
dataSet.ReadXml("file.xml")  
  
For Each dataTable in dataSet.Tables  
   dataTable.EndLoadData()  
Next  
```  
  
```csharp  
foreach (DataTable dataTable in dataSet.Tables)  
   dataTable.BeginLoadData();  
  
dataSet.ReadXml("file.xml");
  
foreach (DataTable dataTable in dataSet.Tables)  
   dataTable.EndLoadData();  
```  
  
> [!NOTE]
> <span data-ttu-id="4fcff-162">如果您的 XSD 架構 <xref:System.Data.DataSet> 包含**targetNamespace**，則可能不會讀取資料，而且您可能會在呼叫**ReadXml**載入 <xref:System.Data.DataSet> 包含沒有限定命名空間之元素的 XML 時，遇到例外狀況。</span><span class="sxs-lookup"><span data-stu-id="4fcff-162">If the XSD schema for your <xref:System.Data.DataSet> includes a **targetNamespace**, data may not be read, and you may encounter exceptions, when calling **ReadXml** to load the <xref:System.Data.DataSet> with XML that contains elements with no qualifying namespace.</span></span> <span data-ttu-id="4fcff-163">若要在此情況下讀取不合格的專案，請在您的 XSD 架構中，將**elementFormDefault**設定為等於 "合格"。</span><span class="sxs-lookup"><span data-stu-id="4fcff-163">To read unqualified elements in this case, set **elementFormDefault** equal to "qualified" in your XSD schema.</span></span> <span data-ttu-id="4fcff-164">例如：</span><span class="sxs-lookup"><span data-stu-id="4fcff-164">For example:</span></span>  
  
```xml  
<xsd:schema id="customDataSet"
  elementFormDefault="qualified"  
  targetNamespace="http://www.tempuri.org/customDataSet.xsd"
  xmlns="http://www.tempuri.org/customDataSet.xsd"
  xmlns:xsd="http://www.w3.org/2001/XMLSchema"
  xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
</xsd:schema>  
```  
  
## <a name="merging-data-from-xml"></a><span data-ttu-id="4fcff-165">從 XML 合併資料</span><span class="sxs-lookup"><span data-stu-id="4fcff-165">Merging Data from XML</span></span>  
 <span data-ttu-id="4fcff-166">如果 <xref:System.Data.DataSet> 已經包含資料，則會將 XML 的新資料加入 <xref:System.Data.DataSet> 中已出現的資料中。</span><span class="sxs-lookup"><span data-stu-id="4fcff-166">If the <xref:System.Data.DataSet> already contains data, the new data from the XML is added to the data already present in the <xref:System.Data.DataSet>.</span></span> <span data-ttu-id="4fcff-167">**ReadXml**不會從 XML 合併到 <xref:System.Data.DataSet> 具有相符主鍵的任何資料列資訊。</span><span class="sxs-lookup"><span data-stu-id="4fcff-167">**ReadXml** does not merge from the XML into the <xref:System.Data.DataSet> any row information with matching primary keys.</span></span> <span data-ttu-id="4fcff-168">若要使用 XML 的新資訊來覆寫現有的資料列資訊，請使用**ReadXml**來建立新的 <xref:System.Data.DataSet> ，然後將 <xref:System.Data.DataSet.Merge%2A> 新的新增 <xref:System.Data.DataSet> 至現有的 <xref:System.Data.DataSet> 。</span><span class="sxs-lookup"><span data-stu-id="4fcff-168">To overwrite existing row information with new information from XML, use **ReadXml** to create a new <xref:System.Data.DataSet>, and then <xref:System.Data.DataSet.Merge%2A> the new <xref:System.Data.DataSet> into the existing <xref:System.Data.DataSet>.</span></span> <span data-ttu-id="4fcff-169">請注意，使用**XmlReadMode**為**diffgram**的**ReadXML**載入 diffgram 時，將會合並具有相同唯一識別碼的資料列。</span><span class="sxs-lookup"><span data-stu-id="4fcff-169">Note that loading a DiffGram using **ReadXML** with an **XmlReadMode** of **DiffGram** will merge rows that have the same unique identifier.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="4fcff-170">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4fcff-170">See also</span></span>

- <xref:System.Data.DataSet.Merge%2A?displayProperty=nameWithType>
- [<span data-ttu-id="4fcff-171">在資料集中使用 XML</span><span class="sxs-lookup"><span data-stu-id="4fcff-171">Using XML in a DataSet</span></span>](using-xml-in-a-dataset.md)
- [<span data-ttu-id="4fcff-172">DiffGram</span><span class="sxs-lookup"><span data-stu-id="4fcff-172">DiffGrams</span></span>](diffgrams.md)
- [<span data-ttu-id="4fcff-173">從 XML 結構描述 (XSD) 衍生資料集關聯式結構</span><span class="sxs-lookup"><span data-stu-id="4fcff-173">Deriving DataSet Relational Structure from XML Schema (XSD)</span></span>](deriving-dataset-relational-structure-from-xml-schema-xsd.md)
- [<span data-ttu-id="4fcff-174">從 XML 推斷資料集關聯式結構</span><span class="sxs-lookup"><span data-stu-id="4fcff-174">Inferring DataSet Relational Structure from XML</span></span>](inferring-dataset-relational-structure-from-xml.md)
- [<span data-ttu-id="4fcff-175">從 XML 載入資料集結構描述資訊</span><span class="sxs-lookup"><span data-stu-id="4fcff-175">Loading DataSet Schema Information from XML</span></span>](loading-dataset-schema-information-from-xml.md)
- [<span data-ttu-id="4fcff-176">DataSet、DataTable 和 DataView</span><span class="sxs-lookup"><span data-stu-id="4fcff-176">DataSets, DataTables, and DataViews</span></span>](index.md)
- <span data-ttu-id="4fcff-177">[ADO.NET 概觀](../ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="4fcff-177">[ADO.NET Overview](../ado-net-overview.md)</span></span>
