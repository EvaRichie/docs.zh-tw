---
title: JSON 和 XML 之間的對應
ms.date: 03/30/2017
ms.assetid: 22ee1f52-c708-4024-bbf0-572e0dae64af
ms.openlocfilehash: 649d0f50aae806394587c7b79a7970c2de03e087
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96234644"
---
# <a name="mapping-between-json-and-xml"></a><span data-ttu-id="53828-102">JSON 和 XML 之間的對應</span><span class="sxs-lookup"><span data-stu-id="53828-102">Mapping Between JSON and XML</span></span>

<span data-ttu-id="53828-103"><xref:System.Runtime.Serialization.Json.JsonReaderWriterFactory> 所產生的讀取器與寫入器會透過 JavaScript 物件標記法 (JSON) 內容來提供 XML API。</span><span class="sxs-lookup"><span data-stu-id="53828-103">The readers and writers produced by the <xref:System.Runtime.Serialization.Json.JsonReaderWriterFactory> provide an XML API over JavaScript Object Notation (JSON) content.</span></span> <span data-ttu-id="53828-104">JSON 使用 JavaScript 物件常值的子集對資料進行編碼。</span><span class="sxs-lookup"><span data-stu-id="53828-104">JSON encodes data using a subset of the object literals of JavaScript.</span></span> <span data-ttu-id="53828-105">使用或來 Windows Communication Foundation (WCF) 應用程式傳送或接收 JSON 內容時，也會使用此處理站所產生的讀取器和寫入器 <xref:System.ServiceModel.Channels.WebMessageEncodingBindingElement> <xref:System.ServiceModel.WebHttpBinding> 。</span><span class="sxs-lookup"><span data-stu-id="53828-105">The readers and writers produced by this factory are also used when JSON content is being sent or received by Windows Communication Foundation (WCF) applications using the <xref:System.ServiceModel.Channels.WebMessageEncodingBindingElement> or the <xref:System.ServiceModel.WebHttpBinding>.</span></span>

<span data-ttu-id="53828-106">使用 JSON 內容進行初始化時，JSON 讀取器行為將與 XML 文字讀取器對 XML 執行個體所執行的動作相同。</span><span class="sxs-lookup"><span data-stu-id="53828-106">When initialized with JSON content, the JSON reader behaves in the same way that a textual XML reader does over an instance of XML.</span></span> <span data-ttu-id="53828-107">當您針對 JSON 讀取器進行一系列的呼叫，進而在 XML 文字讀取器產生特定 XML 執行個體時，就會寫出 JSON 內容。</span><span class="sxs-lookup"><span data-stu-id="53828-107">The JSON writer, when given a sequence of calls that on a textual XML reader produces a certain XML instance, writes out JSON content.</span></span> <span data-ttu-id="53828-108">本主題將說明此 XML 執行個體與 JSON 內容之間的對應，以供進階案例使用。</span><span class="sxs-lookup"><span data-stu-id="53828-108">The mapping between this instance of XML and the JSON content is described in this topic for use in advanced scenarios.</span></span>

<span data-ttu-id="53828-109">就內部而言，WCF 會在處理時將 JSON 表示為 XML 資訊集。</span><span class="sxs-lookup"><span data-stu-id="53828-109">Internally, JSON is represented as an XML infoset when processed by WCF.</span></span> <span data-ttu-id="53828-110">一般來說，您不需要關心這個內部表示法，因為對應只是一個邏輯概念：通常，JSON 不會在記憶體中實際轉換為 XML，或是從 XML 轉換為 JSON。</span><span class="sxs-lookup"><span data-stu-id="53828-110">Normally you do not have to be concerned with this internal representation as the mapping is only a logical one: JSON is normally not physically converted to XML in memory or converted to JSON from XML.</span></span> <span data-ttu-id="53828-111">對應代表 XML API 可用來存取 JSON 內容。</span><span class="sxs-lookup"><span data-stu-id="53828-111">The mapping means that XML APIs are used to access JSON content.</span></span>

<span data-ttu-id="53828-112">當 WCF 使用 JSON 時，常見的案例是由 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 行為自動插入，或在適當的情況下 <xref:System.ServiceModel.Description.WebScriptEnablingBehavior> 依 <xref:System.ServiceModel.Description.WebHttpBehavior> 行為自動插入。</span><span class="sxs-lookup"><span data-stu-id="53828-112">When WCF uses JSON, the usual scenario is that the <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> is automatically plugged in by the <xref:System.ServiceModel.Description.WebScriptEnablingBehavior> behavior, or by the <xref:System.ServiceModel.Description.WebHttpBehavior> behavior when appropriate.</span></span> <span data-ttu-id="53828-113"><xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 了解 JSON 和 XML InfoSet 之間的對應關係，其運作方式就好像是直接處理 JSON 一樣 </span><span class="sxs-lookup"><span data-stu-id="53828-113">The <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> understands the mapping between JSON and the XML infoset and acts as if it is dealing with JSON directly.</span></span> <span data-ttu-id="53828-114">(您可以使用 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 來搭配任何的 XML 讀取器或寫入器，前提是您必須了解 XML 需符合下列對應關係)。</span><span class="sxs-lookup"><span data-stu-id="53828-114">(It is possible to use the <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> with any XML reader or writer, with the understanding that the XML conforms to the following mapping.)</span></span>

<span data-ttu-id="53828-115">在進階案例中，您可能需要直接存取下列對應。</span><span class="sxs-lookup"><span data-stu-id="53828-115">In advanced scenarios, it may become necessary to directly access the following mapping.</span></span> <span data-ttu-id="53828-116">這些情況通常會在您想要以自訂方式來序列化或還原序列化 JSON，而且不想仰賴 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>，或是當您針對包含 JSON 的訊息直接處理 <xref:System.ServiceModel.Channels.Message> 型別時才會發生。</span><span class="sxs-lookup"><span data-stu-id="53828-116">These scenarios occur when you want to serialize and deserialize JSON in custom ways, without relying on the <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>, or when dealing with the <xref:System.ServiceModel.Channels.Message> type directly for messages containing JSON.</span></span> <span data-ttu-id="53828-117">JSON-XML 對應同時可適用於訊息記錄。</span><span class="sxs-lookup"><span data-stu-id="53828-117">The JSON-XML mapping is also used for message logging.</span></span> <span data-ttu-id="53828-118">使用 WCF 中的訊息記錄功能時，JSON 訊息會根據下一節所述的對應記錄為 XML。</span><span class="sxs-lookup"><span data-stu-id="53828-118">When using the message logging feature in WCF, JSON messages is logged as XML according to the mapping described in the next section.</span></span>

<span data-ttu-id="53828-119">若要釐清對應的概念，請參閱下列 JSON 文件範例。</span><span class="sxs-lookup"><span data-stu-id="53828-119">To clarify the concept of a mapping, the following example is of a JSON document.</span></span>

```json
{"product":"pencil","price":12}
```

<span data-ttu-id="53828-120">若要使用先前所述的其中一種讀取器來讀取此 JSON 文件，請使用您通常用來讀取下列文件的相同 <xref:System.Xml.XmlDictionaryReader> 呼叫序列。</span><span class="sxs-lookup"><span data-stu-id="53828-120">To read this JSON document using one of the readers previously mentioned, use the same sequence of <xref:System.Xml.XmlDictionaryReader> calls as you would to read the following XML document.</span></span>

```xml
<root type="object">
    <product type="string">pencil</product>
    <price type="number">12</price>
</root>
```

<span data-ttu-id="53828-121">此外，如果 WCF 收到範例中的 JSON 訊息並記錄，您就會在先前的記錄檔中看到 XML 片段。</span><span class="sxs-lookup"><span data-stu-id="53828-121">Furthermore, if the JSON message in the example is received by WCF and logged, you would see the XML fragment in the preceding log.</span></span>

## <a name="mapping-between-json-and-the-xml-infoset"></a><span data-ttu-id="53828-122">JSON 和 XML InfoSet 之間的對應</span><span class="sxs-lookup"><span data-stu-id="53828-122">Mapping Between JSON and the XML Infoset</span></span>

<span data-ttu-id="53828-123">正式來說，此對應是在 JSON 中所述的 JSON [4627](https://www.ietf.org/rfc/rfc4627.txt) (，但不會放寬某些限制，以及新增) 和 Xml 資訊集 (而非文字 xml) ，如 [xml 資訊集](https://www.w3.org/TR/2004/REC-xml-infoset-20040204/)所述。</span><span class="sxs-lookup"><span data-stu-id="53828-123">Formally, the mapping is between JSON as described in [RFC 4627](https://www.ietf.org/rfc/rfc4627.txt) (except with certain restrictions relaxed and certain other restrictions added) and the XML infoset (and not textual XML) as described in [XML Information Set](https://www.w3.org/TR/2004/REC-xml-infoset-20040204/).</span></span> <span data-ttu-id="53828-124">請參閱本主題，以瞭解 [方括弧] 中的 *資訊專案* 和欄位的定義。</span><span class="sxs-lookup"><span data-stu-id="53828-124">See this topic for the definitions of *information items* and fields in [square brackets].</span></span>

<span data-ttu-id="53828-125">空白的 JSON 檔會對應至空白的 XML 檔，而空白的 XML 檔會對應至空白的 JSON 檔。</span><span class="sxs-lookup"><span data-stu-id="53828-125">A blank JSON document maps to a blank XML document, and a blank XML document maps to a blank JSON document.</span></span> <span data-ttu-id="53828-126">在 XML 對 JSON 的對應中，不允許在檔前面加上空格和尾端空白字元。</span><span class="sxs-lookup"><span data-stu-id="53828-126">On the XML to JSON mapping, preceding white space and trailing white space after the document are not allowed.</span></span>

<span data-ttu-id="53828-127">此對應會在文件資訊項目 (Document Information Item，DII) 或項目資訊項目 (Element Information Item，EII) 與 JSON 之間定義。</span><span class="sxs-lookup"><span data-stu-id="53828-127">The mapping is defined between either a Document Information Item (DII) or an Element Information Item (EII) and JSON.</span></span> <span data-ttu-id="53828-128">EII (或 DII 之 [document element] 屬性)，將稱為 JSON 根項目。</span><span class="sxs-lookup"><span data-stu-id="53828-128">The EII, or the DII’s [document element] property, is referred to as the Root JSON Element.</span></span> <span data-ttu-id="53828-129">請注意，本對應不支援文件片段 (包含多個根項目的 XML)。</span><span class="sxs-lookup"><span data-stu-id="53828-129">Note that document fragments (XML with multiple root elements) are not supported in this mapping.</span></span>

<span data-ttu-id="53828-130">範例：下列文件：</span><span class="sxs-lookup"><span data-stu-id="53828-130">Example: The following document:</span></span>

```xml
<?xml version="1.0"?>
<root type="number">42</root>
```

<span data-ttu-id="53828-131">以及下列項目：</span><span class="sxs-lookup"><span data-stu-id="53828-131">And the following element:</span></span>

```xml
<root type="number">42</root>
```

<span data-ttu-id="53828-132">兩者都對應至 JSON。</span><span class="sxs-lookup"><span data-stu-id="53828-132">Both have a mapping to JSON.</span></span> <span data-ttu-id="53828-133">`root`在這兩種情況下，<> 元素都是根 JSON 元素。</span><span class="sxs-lookup"><span data-stu-id="53828-133">The <`root`> element is the Root JSON Element in both cases.</span></span>

<span data-ttu-id="53828-134">此外，在 DII 情況中，您應該考量下列事項：</span><span class="sxs-lookup"><span data-stu-id="53828-134">Furthermore, in the case of a DII, the following should be considered:</span></span>

- <span data-ttu-id="53828-135">某些 [children] 清單中的項目不得出現。</span><span class="sxs-lookup"><span data-stu-id="53828-135">Some items in the [children] list must not be present.</span></span> <span data-ttu-id="53828-136">當您讀取從 JSON 開始對應的 XML 時，請勿以此事實為基準。</span><span class="sxs-lookup"><span data-stu-id="53828-136">Do not rely on this fact when reading XML mapped from JSON.</span></span>

- <span data-ttu-id="53828-137">[children] 清單不包含任何註解資訊項目。</span><span class="sxs-lookup"><span data-stu-id="53828-137">The [children] list holds no comment information items.</span></span>

- <span data-ttu-id="53828-138">[children] 清單不包含任何 DTD 資訊項目。</span><span class="sxs-lookup"><span data-stu-id="53828-138">The [children] list holds no DTD information items.</span></span>

- <span data-ttu-id="53828-139">[子系] 清單不會 (PI) 資訊專案中保存任何個人資訊， (宣告 `<?xml…>` 不會被視為 PI 資訊專案) </span><span class="sxs-lookup"><span data-stu-id="53828-139">The [children] list holds no personal Information (PI) information items (the `<?xml…>` declaration is not considered a PI information item)</span></span>

- <span data-ttu-id="53828-140">[notations] 集合是空的。</span><span class="sxs-lookup"><span data-stu-id="53828-140">The [notations] set is empty.</span></span>

- <span data-ttu-id="53828-141">[unparsed entities] 集合是空的。</span><span class="sxs-lookup"><span data-stu-id="53828-141">The [unparsed entities] set is empty.</span></span>

<span data-ttu-id="53828-142">範例：下列文件未對應至 JSON，因為 [children] 保留一個 PI 和文件。</span><span class="sxs-lookup"><span data-stu-id="53828-142">Example: The following document has no mapping to JSON because [children] holds a PI and a comment.</span></span>

```xml
<?xml version="1.0"?>
<!--comment--><?pi?>
<root type="number">42</root>
```

<span data-ttu-id="53828-143">JSON 根項目的 EII 具有下列特性：</span><span class="sxs-lookup"><span data-stu-id="53828-143">The EII for the Root JSON Element has the following characteristics:</span></span>

- <span data-ttu-id="53828-144">[local name] 包含值 "root"。</span><span class="sxs-lookup"><span data-stu-id="53828-144">[local name] has the value "root".</span></span>

- <span data-ttu-id="53828-145">[namespace name] 沒有值。</span><span class="sxs-lookup"><span data-stu-id="53828-145">[namespace name] has no value.</span></span>

- <span data-ttu-id="53828-146">[prefix] 沒有值。</span><span class="sxs-lookup"><span data-stu-id="53828-146">[prefix] has no value.</span></span>

- <span data-ttu-id="53828-147">[children] 可能包含 EII (代表將進一步介紹的「內部項目」) 或 CII (將進一步介紹的字元資訊項目) 或不包含任何一項，但並非兩者都不包含。</span><span class="sxs-lookup"><span data-stu-id="53828-147">[children] may either contain EIIs (which represent Inner Elements as described further) or CIIs (Character Information Items as described further) or none of these, but not both.</span></span>

- <span data-ttu-id="53828-148">[attributes] 可能包含下列選擇性屬性資訊項目 (AII)</span><span class="sxs-lookup"><span data-stu-id="53828-148">[attributes] may contain the following optional attribute information items (AIIs)</span></span>

- <span data-ttu-id="53828-149">如進一步介紹的 JSON 型別屬性 ("type")。</span><span class="sxs-lookup"><span data-stu-id="53828-149">The JSON Type Attribute ("type") as described further.</span></span> <span data-ttu-id="53828-150">此屬性可用來保存對應 XML 中的 JSON 型別 (字串、數字、布林值、物件、陣列或 Null)。</span><span class="sxs-lookup"><span data-stu-id="53828-150">This attribute is used to preserve the JSON type (string, number, boolean, object, array or null) in the mapped XML.</span></span>

- <span data-ttu-id="53828-151">如進一步說明，資料合約名稱屬性 ( 「 \_ \_ 類型」 ) 。</span><span class="sxs-lookup"><span data-stu-id="53828-151">The Data Contract Name Attribute ("\_\_type") as described further.</span></span> <span data-ttu-id="53828-152">如果 JSON 型別屬性同時存在，且其 [normalized value] 為 "object" 的話，才會存在此屬性。</span><span class="sxs-lookup"><span data-stu-id="53828-152">This attribute is can only be present if the JSON type attribute is also present and its [normalized value] is "object".</span></span> <span data-ttu-id="53828-153">`DataContractJsonSerializer` 可使用此屬性來保存資料合約型別資訊，例如，一個衍生型別已序列化且預期基底型別的多型案例。</span><span class="sxs-lookup"><span data-stu-id="53828-153">This attribute is used by the `DataContractJsonSerializer` to preserve data contract type information - for example, in polymorphic cases where a derived type is serialized and where a base type is expected.</span></span> <span data-ttu-id="53828-154">如果您不是使用 `DataContractJsonSerializer`，在大部分情況下會忽略此屬性。</span><span class="sxs-lookup"><span data-stu-id="53828-154">If you are not working with the `DataContractJsonSerializer`, in most cases, this attribute is ignored.</span></span>

- <span data-ttu-id="53828-155">[範圍內的命名空間] 包含將 "xml" 系結至 `http://www.w3.org/XML/1998/namespace` 資訊集規格所規定的系結。</span><span class="sxs-lookup"><span data-stu-id="53828-155">[in-scope namespaces] contains the binding of "xml" to `http://www.w3.org/XML/1998/namespace` as mandated by the infoset specification.</span></span>

- <span data-ttu-id="53828-156">[children]、[attributes] 和 [in-scope namespaces] 只能包含先前指定的項目，而 [namespace attributes] 不得包含任何成員，但是在讀取從 JSON 對應過來的 XML 時，不能以這些事實為基礎。</span><span class="sxs-lookup"><span data-stu-id="53828-156">[children], [attributes] and [in-scope namespaces] must not have any items other than as specified previously and [namespace attributes] must have no members, but do not rely on these facts when reading XML mapped from JSON.</span></span>

<span data-ttu-id="53828-157">範例：下列文件未對應至 JSON，因為 [namespace attributes] 不是空的。</span><span class="sxs-lookup"><span data-stu-id="53828-157">Example: The following document has no mapping to JSON because [namespace attributes] is not empty.</span></span>

```xml
<?xml version="1.0"?>
<root xmlns:a="myattributevalue">42</root>
```

<span data-ttu-id="53828-158">JSON 型別屬性的 AII 具有下列特性：</span><span class="sxs-lookup"><span data-stu-id="53828-158">The AII for the JSON Type Attribute has the following characteristics:</span></span>

- <span data-ttu-id="53828-159">[namespace name] 沒有值。</span><span class="sxs-lookup"><span data-stu-id="53828-159">[namespace name] has no value.</span></span>
- <span data-ttu-id="53828-160">[prefix] 沒有值。</span><span class="sxs-lookup"><span data-stu-id="53828-160">[prefix] has no value.</span></span>
- <span data-ttu-id="53828-161">[local name] 為 "type"。</span><span class="sxs-lookup"><span data-stu-id="53828-161">[local name] is "type".</span></span>
- <span data-ttu-id="53828-162">[normalized value] 是將於下一節中說明的其中一個可能的型別值。</span><span class="sxs-lookup"><span data-stu-id="53828-162">[normalized value] is one of the possible type values described in the following section.</span></span>
- <span data-ttu-id="53828-163">[specified] 為 `true`。</span><span class="sxs-lookup"><span data-stu-id="53828-163">[specified] is `true`.</span></span>
- <span data-ttu-id="53828-164">[attribute type] 沒有值。</span><span class="sxs-lookup"><span data-stu-id="53828-164">[attribute type] has no value.</span></span>
- <span data-ttu-id="53828-165">[references] 沒有值。</span><span class="sxs-lookup"><span data-stu-id="53828-165">[references] has no value.</span></span>

<span data-ttu-id="53828-166">資料合約名稱屬性的 AII 具有下列特性：</span><span class="sxs-lookup"><span data-stu-id="53828-166">The AII for the Data Contract Name Attribute has the following characteristics:</span></span>

- <span data-ttu-id="53828-167">[namespace name] 沒有值。</span><span class="sxs-lookup"><span data-stu-id="53828-167">[namespace name] has no value.</span></span>
- <span data-ttu-id="53828-168">[prefix] 沒有值。</span><span class="sxs-lookup"><span data-stu-id="53828-168">[prefix] has no value.</span></span>
- <span data-ttu-id="53828-169">[local name] 為 " \_ \_ type" (兩個底線，然後 ) 的 "type"。</span><span class="sxs-lookup"><span data-stu-id="53828-169">[local name] is "\_\_type" (two underscores and then "type").</span></span>
- <span data-ttu-id="53828-170">[normalized value] 是任何有效的 Unicode 字串 – 下一節將說明此字串與 JSON 的對應。</span><span class="sxs-lookup"><span data-stu-id="53828-170">[normalized value] is any valid Unicode string – the mapping of this string to JSON is described in the following section.</span></span>
- <span data-ttu-id="53828-171">[specified] 為 `true`。</span><span class="sxs-lookup"><span data-stu-id="53828-171">[specified] is `true`.</span></span>
- <span data-ttu-id="53828-172">[attribute type] 沒有值。</span><span class="sxs-lookup"><span data-stu-id="53828-172">[attribute type] has no value.</span></span>
- <span data-ttu-id="53828-173">[references] 沒有值。</span><span class="sxs-lookup"><span data-stu-id="53828-173">[references] has no value.</span></span>

<span data-ttu-id="53828-174">包含在 JSON 根項目的內部項目或其他內部項目都具有下列特性：</span><span class="sxs-lookup"><span data-stu-id="53828-174">Inner elements contained within the Root JSON Element or other inner elements have the following characteristics:</span></span>

- <span data-ttu-id="53828-175">[本機名稱] 可能會有進一步的描述值。</span><span class="sxs-lookup"><span data-stu-id="53828-175">[local name] may have any value as described further.</span></span>
- <span data-ttu-id="53828-176">[namespace name]、[prefix]、[children]、[attributes]、[namespace attributes]，和 [in-scope namespaces] 都和 JSON 根項目受制於相同的規則。</span><span class="sxs-lookup"><span data-stu-id="53828-176">[namespace name], [prefix], [children], [attributes], [namespace attributes], and [in-scope namespaces] are subject to the same rules as the Root JSON Element.</span></span>

<span data-ttu-id="53828-177">同時在 JSON 根項目與內部項目之中，JSON 型別屬性會定義對 JSON 及可能的 [children] 和其解譯的對應關係。</span><span class="sxs-lookup"><span data-stu-id="53828-177">In both the Root JSON Element and the inner elements, the JSON Type Attribute defines the mapping to JSON and the possible [children] and their interpretation.</span></span> <span data-ttu-id="53828-178">屬性的 [正規化值] 會區分大小寫，而且必須是小寫，而且不能包含空白字元。</span><span class="sxs-lookup"><span data-stu-id="53828-178">The attribute’s [normalized value] is case-sensitive and must be lowercase, and cannot contain white space.</span></span>

|<span data-ttu-id="53828-179">[正規化值] 的 JSON 型別屬性的 AII</span><span class="sxs-lookup"><span data-stu-id="53828-179">[normalized value] of JSON Type Attribute’s AII</span></span>|<span data-ttu-id="53828-180">對應 EII 的已允許 [children]</span><span class="sxs-lookup"><span data-stu-id="53828-180">Allowed [children] of the corresponding EII</span></span>|<span data-ttu-id="53828-181">JSON 對應</span><span class="sxs-lookup"><span data-stu-id="53828-181">Mapping to JSON</span></span>|
|---------------------------------------------------------|---------------------------------------------------|---------------------|
|<span data-ttu-id="53828-182">`string` (或缺乏 JSON 型別 AII)</span><span class="sxs-lookup"><span data-stu-id="53828-182">`string` (or absence of the JSON type AII)</span></span><br /><br /> <span data-ttu-id="53828-183">`string` 與 JSON 型別 AII 的缺席，雙雙都會導致 `string` 成為預設值。</span><span class="sxs-lookup"><span data-stu-id="53828-183">A `string` and the absence of the JSON type AII are the same makes `string` the default.</span></span><br /><br /> <span data-ttu-id="53828-184">因此，`<root> string1</root>` 會對應至 JSON `string` "string1"。</span><span class="sxs-lookup"><span data-stu-id="53828-184">So, `<root> string1</root>` maps to the JSON `string` "string1".</span></span>|<span data-ttu-id="53828-185">0或更多 Cii</span><span class="sxs-lookup"><span data-stu-id="53828-185">0 or more CIIs</span></span>|<span data-ttu-id="53828-186">JSON `string` (JSON RFC，2.5 節)。</span><span class="sxs-lookup"><span data-stu-id="53828-186">A JSON `string` (JSON RFC, section 2.5).</span></span> <span data-ttu-id="53828-187">每個 `char` 字元都會對應至 CII 的 [character code]。</span><span class="sxs-lookup"><span data-stu-id="53828-187">Each `char` is a character that corresponds to the [character code] from the CII.</span></span> <span data-ttu-id="53828-188">如果沒有任何 CII，就會對應至空的 JSON `string`。</span><span class="sxs-lookup"><span data-stu-id="53828-188">If there are no CIIs, it maps to an empty JSON `string`.</span></span><br /><br /> <span data-ttu-id="53828-189">範例：下列項目對應至 JSON 片段：</span><span class="sxs-lookup"><span data-stu-id="53828-189">Example: The following element maps to a JSON fragment:</span></span><br /><br /> `<root type="string">42</root>`<br /><br /> <span data-ttu-id="53828-190">JSON 片段為 "42"。</span><span class="sxs-lookup"><span data-stu-id="53828-190">The JSON fragment is "42".</span></span><br /><br /> <span data-ttu-id="53828-191">在 XML 對 JSON 的對應中，必須逸出的字元會對應至逸出字元，其他所有字元則是對應至尚未逸出的字元。</span><span class="sxs-lookup"><span data-stu-id="53828-191">On XML to JSON mapping, characters that must be escaped map to escaped characters, all others map to characters that are not escaped.</span></span> <span data-ttu-id="53828-192">"/" 字元是特殊的-即使不需要 (寫出為 "/" ) ，也會將它進行轉義 \\ 。</span><span class="sxs-lookup"><span data-stu-id="53828-192">The "/" character is special – it is escaped even though it does not have to be (written out as "\\/").</span></span><br /><br /> <span data-ttu-id="53828-193">範例：下列項目對應至 JSON 片段。</span><span class="sxs-lookup"><span data-stu-id="53828-193">Example: The following element maps to a JSON fragment.</span></span><br /><br /> `<root type="string">the "da/ta"</root>`<br /><br /> <span data-ttu-id="53828-194">JSON 片段為 "" \\ da \\ /ta \\ ""。</span><span class="sxs-lookup"><span data-stu-id="53828-194">The JSON fragment is "the \\"da\\/ta\\"".</span></span><br /><br /> <span data-ttu-id="53828-195">在 JSON 對 XML 的對應中，任何逸出的字元和尚未逸出的字元會正確地對應至相對應的 [character code]。</span><span class="sxs-lookup"><span data-stu-id="53828-195">On JSON to XML mapping, any escaped characters and characters that are not escaped map correctly to the corresponding [character code].</span></span><br /><br /> <span data-ttu-id="53828-196">範例：JSON 片段 "\u0041BC" 會對應至下列 XML 項目。</span><span class="sxs-lookup"><span data-stu-id="53828-196">Example: The JSON fragment "\u0041BC", maps to the following XML element.</span></span><br /><br /> `<root type="string">ABC</root>`<br /><br /> <span data-ttu-id="53828-197">在 JSON RFC) 的第2節中，此字串可以用空白字元括住 ( ' ws '，而不會對應至 XML。</span><span class="sxs-lookup"><span data-stu-id="53828-197">The string can be surrounded by white space ('ws' in section 2 of the JSON RFC) that does not get mapped to XML.</span></span><br /><br /> <span data-ttu-id="53828-198">範例：JSON 片段 "ABC" (在第一個雙引號之前留有一些空格) 會對應至下列 XML 項目。</span><span class="sxs-lookup"><span data-stu-id="53828-198">Example: The JSON fragment           "ABC", (there are spaces before the first double quote), maps to the following XML element.</span></span><br /><br /> `<root type="string">ABC</root>`<br /><br /> <span data-ttu-id="53828-199">XML 中的任何空白字元都會對應至 JSON 中的空白字元。</span><span class="sxs-lookup"><span data-stu-id="53828-199">Any white space in XML maps to white space in JSON.</span></span><br /><br /> <span data-ttu-id="53828-200">範例：下列 XML 項目對應至 JSON 片段。</span><span class="sxs-lookup"><span data-stu-id="53828-200">Example: The following XML element maps to a JSON fragment.</span></span><br /><br /> `<root type="string">  A BC      </root>`<br /><br /> <span data-ttu-id="53828-201">JSON 片段為 " A BC "。</span><span class="sxs-lookup"><span data-stu-id="53828-201">The JSON fragment is " A BC ".</span></span>|
|`number`|<span data-ttu-id="53828-202">1 或更多 CII</span><span class="sxs-lookup"><span data-stu-id="53828-202">1 or more CIIs</span></span>|<span data-ttu-id="53828-203">JSON `number` (JSON RFC，區段 2.4) ，可能會以空白字元括住。</span><span class="sxs-lookup"><span data-stu-id="53828-203">A JSON `number` (JSON RFC, section 2.4), possibly surrounded by white space.</span></span> <span data-ttu-id="53828-204">Number/空白字元組合中的每個字元都是對應至 CII 中 [字元碼] 的字元。</span><span class="sxs-lookup"><span data-stu-id="53828-204">Each character in the number/white space combination is a character that corresponds to the [character code] from the CII.</span></span><br /><br /> <span data-ttu-id="53828-205">範例：下列項目對應至 JSON 片段。</span><span class="sxs-lookup"><span data-stu-id="53828-205">Example: The following element maps to a JSON fragment.</span></span><br /><br /> `<root type="number">    42</root>`<br /><br /> <span data-ttu-id="53828-206">JSON 片段為 42 </span><span class="sxs-lookup"><span data-stu-id="53828-206">The JSON fragment is    42</span></span><br /><br /> <span data-ttu-id="53828-207"> (空白字元會保留) 。</span><span class="sxs-lookup"><span data-stu-id="53828-207">(White space is preserved).</span></span>|
|`boolean`|<span data-ttu-id="53828-208">4或 5 Cii 對應至 `true` 或) 的 (`false` ，可能會以額外的空白字元 cii 括住。</span><span class="sxs-lookup"><span data-stu-id="53828-208">4 or 5 CIIs (which corresponds to `true` or `false`), possibly surrounded by additional white-space CIIs.</span></span>|<span data-ttu-id="53828-209">對應至字串 "true" 的 CII 序列會對應至常值 `true`，而對應至字串 "false" 的 CII 序列則是對應至常值 `false`。</span><span class="sxs-lookup"><span data-stu-id="53828-209">A CII sequence that corresponds to the string "true" is mapped to the literal `true`, and a CII sequence that corresponds to the string "false" is mapped to the literal `false`.</span></span> <span data-ttu-id="53828-210">會保留周圍的空白字元。</span><span class="sxs-lookup"><span data-stu-id="53828-210">Surrounding white space is preserved.</span></span><br /><br /> <span data-ttu-id="53828-211">範例：下列項目對應至 JSON 片段。</span><span class="sxs-lookup"><span data-stu-id="53828-211">Example: The following element maps to a JSON fragment.</span></span><br /><br /> `<root type="boolean"> false</root>`<br /><br /> <span data-ttu-id="53828-212">JSON 片段為 `false`。</span><span class="sxs-lookup"><span data-stu-id="53828-212">The JSON fragment is `false`.</span></span>|
|`null`|<span data-ttu-id="53828-213">全都不允許。</span><span class="sxs-lookup"><span data-stu-id="53828-213">None allowed.</span></span>|<span data-ttu-id="53828-214">常值 `null`。</span><span class="sxs-lookup"><span data-stu-id="53828-214">The literal `null`.</span></span> <span data-ttu-id="53828-215">在 JSON 對 XML 的對應中，可能會在 `null` 第2節中以空白字元括住 ( ' ws '，但未對應至 xml 的) 。</span><span class="sxs-lookup"><span data-stu-id="53828-215">On JSON to XML mapping, the `null` may be surrounded by white space (‘ws’ in section 2) that does not get mapped to XML.</span></span><br /><br /> <span data-ttu-id="53828-216">範例：下列項目對應至 JSON 片段。</span><span class="sxs-lookup"><span data-stu-id="53828-216">Example: The following element maps to a JSON fragment.</span></span><br /><br /> `<root type="null"/>`<br /><br /> <span data-ttu-id="53828-217">或</span><span class="sxs-lookup"><span data-stu-id="53828-217">or</span></span><br /><br /> `<root type="null"></root>`<br /><br /> <span data-ttu-id="53828-218">:</span><span class="sxs-lookup"><span data-stu-id="53828-218">:</span></span><br /><br /> <span data-ttu-id="53828-219">兩個案例中的 JSON 片段都是 `Null`。</span><span class="sxs-lookup"><span data-stu-id="53828-219">The JSON fragment in both cases is `Null`.</span></span>|
|`object`|<span data-ttu-id="53828-220">0 或更多 EII</span><span class="sxs-lookup"><span data-stu-id="53828-220">0 or more EIIs.</span></span>|<span data-ttu-id="53828-221">如 JSON RFC，2.2 小節中所述之 `begin-object` (左側大括號)，後面接著每個 EII 的成員記錄 (如進一步介紹中所述)。</span><span class="sxs-lookup"><span data-stu-id="53828-221">A `begin-object` (left curly brace) as in section 2.2 of the JSON RFC, followed by a member record for each EII as described further.</span></span> <span data-ttu-id="53828-222">如果有一個以上的 EII，成員記錄之間就會存在數值分隔符號 (逗號)。</span><span class="sxs-lookup"><span data-stu-id="53828-222">If there is more than one EII, there are value-separators (commas) between the member records.</span></span> <span data-ttu-id="53828-223">這些全部都會接著一個結尾物件 (右側大括號)。</span><span class="sxs-lookup"><span data-stu-id="53828-223">All this is followed by an end-object (right curly brace).</span></span><br /><br /> <span data-ttu-id="53828-224">範例：下列項目對應至 JSON 片段。</span><span class="sxs-lookup"><span data-stu-id="53828-224">Example: The following element maps to the JSON fragment.</span></span><br /><br /> `<root type="object">`<br /><br /> `<type1 type="string">aaa\</type1>`<br /><br /> `<type2 type="string">bbb\</type2>`<br /><br /> `</root >`<br /><br /> <span data-ttu-id="53828-225">JSON 片段為 `{"type1":"aaa","type2":"bbb"}`。</span><span class="sxs-lookup"><span data-stu-id="53828-225">The JSON fragment is `{"type1":"aaa","type2":"bbb"}`.</span></span><br /><br /> <span data-ttu-id="53828-226">如果資料合約型別屬性存在 XML 對 JSON 的對應中，則會在開頭插入額外的成員記錄。</span><span class="sxs-lookup"><span data-stu-id="53828-226">If the Data Contract Type Attribute is present on XML to JSON mapping, then an additional Member Record is inserted at the beginning.</span></span> <span data-ttu-id="53828-227">它的名稱是資料合約類型屬性的 [本機名稱] ( " \_ \_ Type" ) ，而其值為屬性的 [正規化值]。</span><span class="sxs-lookup"><span data-stu-id="53828-227">Its name is the [local name] of the Data Contract Type Attribute ("\_\_type"), and its value is the attribute's [normalized value].</span></span> <span data-ttu-id="53828-228">相反地，在 JSON 對 XML 的對應中，如果第一個成員記錄的名稱是資料合約類型屬性的 [本機名稱] (也就是 " \_ \_ Type" ) ，對應的 XML 中會有對應的資料合約型別屬性，但是對應的 EII 不存在。</span><span class="sxs-lookup"><span data-stu-id="53828-228">Conversely, on JSON to XML mapping, if the first member-record’s name is the [local name] of the Data Contract Type Attribute (that is, "\_\_type"), a corresponding Data Contract Type Attribute is present in the mapped XML, but a corresponding EII is not present.</span></span> <span data-ttu-id="53828-229">請注意，若要套用這個特殊對應，這項成員記錄必須先出現在 JSON 物件中。</span><span class="sxs-lookup"><span data-stu-id="53828-229">Note that this member record must occur first in the JSON object for this special mapping to apply.</span></span> <span data-ttu-id="53828-230">這代表了從一般 JSON 處理中離開，其中成員記錄的順序並不重要。</span><span class="sxs-lookup"><span data-stu-id="53828-230">This represents a departure from usual JSON processing, where the order of member records is not significant.</span></span><br /><br /> <span data-ttu-id="53828-231">範例：</span><span class="sxs-lookup"><span data-stu-id="53828-231">Example:</span></span><br /><br /> <span data-ttu-id="53828-232">下列 JSON 片段會對應至 XML。</span><span class="sxs-lookup"><span data-stu-id="53828-232">The following JSON fragment maps to XML.</span></span><br /><br /> `{"__type":"Person","name":"John"}`<br /><br /> <span data-ttu-id="53828-233">下列為 XML 程式碼。</span><span class="sxs-lookup"><span data-stu-id="53828-233">The XML is the following code.</span></span><br /><br /> `<root type="object" __type="Person">   <name type="string">John</name> </root>`<br /><br /> <span data-ttu-id="53828-234">請注意， \_ \_ 類型 AII 存在，但沒有 \_ \_ 類型 EII。</span><span class="sxs-lookup"><span data-stu-id="53828-234">Notice that the \_\_type AII is present, but there is no \_\_type EII.</span></span><br /><br /> <span data-ttu-id="53828-235">但是，如果 JSON 中的順序如下列範例所示反轉過來的話，</span><span class="sxs-lookup"><span data-stu-id="53828-235">However, if the order in the JSON is reversed as shown in the following example.</span></span><br /><br /> `{"name":"John","\_\_type":"Person"}`<br /><br /> <span data-ttu-id="53828-236">就會顯示相對應的 XML。</span><span class="sxs-lookup"><span data-stu-id="53828-236">The corresponding XML is shown.</span></span><br /><br /> `<root type="object">   <name type="string">John</name>   <__type type="string">Person</__type> </root>`<br /><br /> <span data-ttu-id="53828-237">也就是說， \_ _type 不會有特殊意義，而且會如往常般對應至 EII，而不是 AII。</span><span class="sxs-lookup"><span data-stu-id="53828-237">That is, \__type ceases to have special meaning and maps to an EII as usual, not AII.</span></span><br /><br /> <span data-ttu-id="53828-238">當 AII 對應至 JSON 值時，其 [normalized value] 的逸出/未逸出規則與 JSON 值的逸出/未逸出規則相同，下表中的 "string" 列將指定此規則。</span><span class="sxs-lookup"><span data-stu-id="53828-238">Escaping/unescaping rules for the AII’s [normalized value] when mapped to a JSON value are the same as for JSON strings, specified in the "string" row of this table.</span></span><br /><br /> <span data-ttu-id="53828-239">範例：</span><span class="sxs-lookup"><span data-stu-id="53828-239">Example:</span></span><br /><br /> `<root type="object" __type="\abc" />`<br /><br /> <span data-ttu-id="53828-240">先前範例可對應至下列 JSON。</span><span class="sxs-lookup"><span data-stu-id="53828-240">to the previous example can be mapped to the following JSON.</span></span><br /><br /> `{"__type":"\\abc"}`<br /><br /> <span data-ttu-id="53828-241">在 XML 對 JSON 的對應中，第一個 EII 的 [本機名稱] 不得為 " \_ \_ type"。</span><span class="sxs-lookup"><span data-stu-id="53828-241">On an XML to JSON mapping, the first EII’s [local name] must not be "\_\_type".</span></span><br /><br /> <span data-ttu-id="53828-242">空白 (`ws`) 不會針對物件在 XML 與 json 的對應上產生，而是在 json 對 XML 的對應中忽略。</span><span class="sxs-lookup"><span data-stu-id="53828-242">White space (`ws`) is never generated on XML to JSON mapping for objects and is ignored on JSON to XML mapping.</span></span><br /><br /> <span data-ttu-id="53828-243">範例：下列 JSON 片段會對應至 XML 項目。</span><span class="sxs-lookup"><span data-stu-id="53828-243">Example: The following JSON fragment maps to an XML element.</span></span><br /><br /> `{ "ccc" : "aaa", "ddd" :"bbb"}`<br /><br /> <span data-ttu-id="53828-244">下列程式碼說明 XML 項目。</span><span class="sxs-lookup"><span data-stu-id="53828-244">The XML element is shown in the following code.</span></span><br /><br /> `<root type="object">    <ccc type="string">aaa</ccc>    <ddd type="string">bbb</bar> </root >`|
|<span data-ttu-id="53828-245">array</span><span class="sxs-lookup"><span data-stu-id="53828-245">array</span></span>|<span data-ttu-id="53828-246">0 或更多 EII</span><span class="sxs-lookup"><span data-stu-id="53828-246">0 or more EIIs</span></span>|<span data-ttu-id="53828-247">如 JSON RFC，2.3 小節中所述之開始-陣列 (左側大括號)，後面接著每個 EII 的陣列記錄 (如進一步介紹中所述)。</span><span class="sxs-lookup"><span data-stu-id="53828-247">A begin-array (left square bracket) as in section 2.3 of the JSON RFC, followed by an array record for each EII as described further.</span></span> <span data-ttu-id="53828-248">如果有一個以上的 EII，陣列記錄之間就會存在數值分隔符號 (逗號)。</span><span class="sxs-lookup"><span data-stu-id="53828-248">If there is more than one EII, there are value-separators (commas) between the array records.</span></span> <span data-ttu-id="53828-249">這些全部都會緊跟著結束-陣列。</span><span class="sxs-lookup"><span data-stu-id="53828-249">All this is followed by an end-array.</span></span><br /><br /> <span data-ttu-id="53828-250">範例：下列 XML 項目對應至 JSON 片段。</span><span class="sxs-lookup"><span data-stu-id="53828-250">Example: The following XML element maps to a JSON fragment.</span></span><br /><br /> `<root type="array"/>    <item type="string">aaa</item>    <item type="string">bbb</item> </root >`<br /><br /> <span data-ttu-id="53828-251">JSON 片段為 `["aaa","bbb"]`</span><span class="sxs-lookup"><span data-stu-id="53828-251">The JSON fragment is `["aaa","bbb"]`</span></span><br /><br /> <span data-ttu-id="53828-252">空白 (`ws`) 不會針對陣列在 XML 與 json 的對應上產生，而且在 json 對 XML 的對應中則會忽略。</span><span class="sxs-lookup"><span data-stu-id="53828-252">White space (`ws`) is never generated on XML to JSON mapping for arrays and is ignored on JSON to XML mapping.</span></span><br /><br /> <span data-ttu-id="53828-253">範例： JSON 片段。</span><span class="sxs-lookup"><span data-stu-id="53828-253">Example: A JSON fragment.</span></span><br /><br />`["aaa", "bbb"]`<br /><br /> <span data-ttu-id="53828-254">它所對應的 XML 項目。</span><span class="sxs-lookup"><span data-stu-id="53828-254">The XML element that it maps to.</span></span><br /><br /> `<root type="array"/>    <item type="string">aaa</item>    <item type="string">bbb</item> </root >`|

<span data-ttu-id="53828-255">成員記錄使用方式如下：</span><span class="sxs-lookup"><span data-stu-id="53828-255">Member Records work as follows:</span></span>

- <span data-ttu-id="53828-256">內部項目的 [local name] 會對應至 `string` 的 `member` 部分，如 JSON RFC，2.2 小節中所定義。</span><span class="sxs-lookup"><span data-stu-id="53828-256">Inner element’s [local name] maps to the `string` part of the `member` as defined in section 2.2 of the JSON RFC.</span></span>

<span data-ttu-id="53828-257">範例：下列項目對應至 JSON 片段。</span><span class="sxs-lookup"><span data-stu-id="53828-257">Example: The following element maps to a JSON fragment.</span></span>

```xml
<root type="object">
    <myLocalName type="string">aaa</myLocalName>
</root>
```

<span data-ttu-id="53828-258">下列將顯示 JSON 片段。</span><span class="sxs-lookup"><span data-stu-id="53828-258">The following JSON fragment is displayed.</span></span>

```json
{"myLocalName":"aaa"}
```

- <span data-ttu-id="53828-259">在 XML 對 JSON 的對應中，JSON 中必須逸出的字元會逸出，其他字元則不會逸出。</span><span class="sxs-lookup"><span data-stu-id="53828-259">On the XML to JSON mapping, the characters that must be escaped in JSON are escaped, and the others are not escaped.</span></span> <span data-ttu-id="53828-260">雖然 "/" 不是必須逸出的字元，還是會逸出 (在 JSON 對 XML 的對應中，它不需要逸出)。</span><span class="sxs-lookup"><span data-stu-id="53828-260">The "/" character, even though it is not a character that must be escaped, is escaped nevertheless (it does not have to be escaped on JSON to XML mapping).</span></span> <span data-ttu-id="53828-261">若您需要針對 JSON 中的 `DateTime` 資料支援使用 ASP.NET AJAX 格式，這是必要的條件。</span><span class="sxs-lookup"><span data-stu-id="53828-261">This is required to support the ASP.NET AJAX format for `DateTime` data in JSON.</span></span>

- <span data-ttu-id="53828-262">在 JSON 對 XML 的對應中，會採用所有的字元 (必要時包括尚未逸出的字元) 來形成 `string` 以產生 [local name]。</span><span class="sxs-lookup"><span data-stu-id="53828-262">On the JSON to XML mapping, all characters (including the not escaped characters, if necessary) are taken to form a `string` that produces a [local name].</span></span>

- <span data-ttu-id="53828-263">根據 `JSON Type Attribute`，內部項目 [children] 會對應至 2.2 小節中的值，就像是 `Root JSON Element` 一樣。</span><span class="sxs-lookup"><span data-stu-id="53828-263">Inner elements [children] map to the value in section 2.2, according to the `JSON Type Attribute` just like for the `Root JSON Element`.</span></span> <span data-ttu-id="53828-264">可允許使用多層的巢狀 EII (包含陣列中的巢狀結構)。</span><span class="sxs-lookup"><span data-stu-id="53828-264">Multiple levels of nesting of EIIs (including nesting within arrays) are allowed.</span></span>

<span data-ttu-id="53828-265">範例：下列項目對應至 JSON 片段。</span><span class="sxs-lookup"><span data-stu-id="53828-265">Example: The following element maps to a JSON fragment.</span></span>

```xml
<root type="object">
    <myLocalName1 type="string">myValue1</myLocalName1>
    <myLocalName2 type="number">2</myLocalName2>
    <myLocalName3 type="object">
        <myNestedName1 type="boolean">true</myNestedName1>
        <myNestedName2 type="null"/>
    </myLocalName3>
</root >
```

<span data-ttu-id="53828-266">下列為它所對應的 JSON 片段。</span><span class="sxs-lookup"><span data-stu-id="53828-266">The following JSON fragment is what it maps to.</span></span>

```json
{"myLocalName1":"myValue1","myLocalName2":2,"myLocalName3":{"myNestedName1":true,"myNestedName2":null}}
```

> [!NOTE]
> <span data-ttu-id="53828-267">在先前的對應中，沒有 XML 編碼步驟。</span><span class="sxs-lookup"><span data-stu-id="53828-267">There is no XML encoding step in the preceding mapping.</span></span> <span data-ttu-id="53828-268">因此，WCF 只支援 JSON 檔，其中索引鍵名稱中的所有字元都是 XML 元素名稱中的有效字元。</span><span class="sxs-lookup"><span data-stu-id="53828-268">Therefore, WCF only supports JSON documents where all characters in key names are valid characters in XML element names.</span></span> <span data-ttu-id="53828-269">例如，不支援 JSON 檔 {"<"： "a"}，因為 < 不是 XML 元素的有效名稱。</span><span class="sxs-lookup"><span data-stu-id="53828-269">For example, the JSON document {"<":"a"} is not supported because < is not a valid name for an XML element.</span></span>

<span data-ttu-id="53828-270">相反的情況 (在 XML 中為有效字元，但是在 JSON 中卻為無效) 並不會導致任何問題，因為先前的對應已經包含了 JSON 逸出/未逸出步驟。</span><span class="sxs-lookup"><span data-stu-id="53828-270">The reverse situation (characters valid in XML but not in JSON) does not cause any problems because the preceding mapping includes JSON escaping/unescaping steps.</span></span>

<span data-ttu-id="53828-271">陣列記錄使用方式如下：</span><span class="sxs-lookup"><span data-stu-id="53828-271">Array Records work as follows:</span></span>

- <span data-ttu-id="53828-272">內部項目的 [local name] 為 "item"。</span><span class="sxs-lookup"><span data-stu-id="53828-272">Inner element’s [local name] is "item".</span></span>

- <span data-ttu-id="53828-273">內部項目的 [children] 會根據 JSON 型別屬性對應至 2.3 小節中的值，對 JSON 的根項目也是這麼做。</span><span class="sxs-lookup"><span data-stu-id="53828-273">Inner element’s [children] map to the value in section 2.3, according to the JSON Type Attribute as is does for the Root JSON Element.</span></span> <span data-ttu-id="53828-274">可允許使用多層的巢狀 EII (包含物件中的巢狀結構)。</span><span class="sxs-lookup"><span data-stu-id="53828-274">Multiple levels of nesting of EIIs (including nesting within objects) are allowed.</span></span>

<span data-ttu-id="53828-275">範例：下列項目對應至 JSON 片段。</span><span class="sxs-lookup"><span data-stu-id="53828-275">Example: The following element maps to a JSON fragment.</span></span>

```xml
<root type="array">
    <item type="string">myValue1</item>
    <item type="number">2</item>
    <item type="array">
    <item type="boolean">true</item>
    <item type="null"/></item>
</root>
```

<span data-ttu-id="53828-276">下列為 JSON 片段。</span><span class="sxs-lookup"><span data-stu-id="53828-276">The following is the JSON fragment.</span></span>

```json
["myValue1",2,[true,null]]
```

## <a name="see-also"></a><span data-ttu-id="53828-277">另請參閱</span><span class="sxs-lookup"><span data-stu-id="53828-277">See also</span></span>

- <xref:System.Runtime.Serialization.Json.JsonReaderWriterFactory>
- <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>
- [<span data-ttu-id="53828-278">獨立 JSON 序列化</span><span class="sxs-lookup"><span data-stu-id="53828-278">Stand-Alone JSON Serialization</span></span>](stand-alone-json-serialization.md)
