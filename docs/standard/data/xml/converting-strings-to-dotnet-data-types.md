---
title: 將字串轉換成 .NET Framework 資料型別
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 65455ef3-9120-412c-819b-d0f59f88ac09
ms.openlocfilehash: fda5441c58d14b91a9eca16fff9149c8795f95b9
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84289222"
---
# <a name="converting-strings-to-net-framework-data-types"></a><span data-ttu-id="15e9b-102">將字串轉換成 .NET Framework 資料型別</span><span class="sxs-lookup"><span data-stu-id="15e9b-102">Converting Strings to .NET Framework Data Types</span></span>
<span data-ttu-id="15e9b-103">若要將一個字串轉換成 .NET Framework 資料型別，請使用符合應用程式需求的 **XmlConvert** 方法。</span><span class="sxs-lookup"><span data-stu-id="15e9b-103">If you want to convert a string to a .NET Framework data type, use the **XmlConvert** method that fits the application requirements.</span></span> <span data-ttu-id="15e9b-104">如需所有可用於 **XmlConvert** 類別的轉換方法清單，請參閱 <xref:System.Xml.XmlConvert>。</span><span class="sxs-lookup"><span data-stu-id="15e9b-104">For a list of all conversion methods available in the **XmlConvert** class, see <xref:System.Xml.XmlConvert>.</span></span>  
  
 <span data-ttu-id="15e9b-105">**ToString** 方法所傳回的字串是所傳入之資料的字串版本。</span><span class="sxs-lookup"><span data-stu-id="15e9b-105">The string returned from the **ToString** method is a string version of the data that is passed in.</span></span> <span data-ttu-id="15e9b-106">此外，還有幾個 .NET Framework 型別是用 **XmlConvert** 類別來轉換，而不是使用 **System.Convert** 類別中的方法進行轉換。</span><span class="sxs-lookup"><span data-stu-id="15e9b-106">Additionally, there are several .NET Framework types that convert using the **XmlConvert** class yet they do not use the methods in the **System.Convert** class.</span></span> <span data-ttu-id="15e9b-107">**XmlConvert** 類別符合 XML 結構描述 (XSD) 資料型別規格，且擁有一個 **XmlConvert** 可對應的資料型別。</span><span class="sxs-lookup"><span data-stu-id="15e9b-107">The **XmlConvert** class follows the XML Schema (XSD) data type specification and has a data type that the **XmlConvert** can map to.</span></span>  
  
 <span data-ttu-id="15e9b-108">下列表格列出使用 XML 結構描述 (XSD) 資料型別對應所傳回的 .NET Framework 資料型別和字串型別。</span><span class="sxs-lookup"><span data-stu-id="15e9b-108">The following table lists .NET Framework data types and the string types that are returned using XML Schema (XSD) data type mapping.</span></span> <span data-ttu-id="15e9b-109">這些 .NET Framework 型別無法以 **System.Convert** 來處理。</span><span class="sxs-lookup"><span data-stu-id="15e9b-109">These .NET Framework types cannot be processed using **System.Convert**.</span></span>  
  
|<span data-ttu-id="15e9b-110">.NET Framework 類型</span><span class="sxs-lookup"><span data-stu-id="15e9b-110">.NET Framework type</span></span>|<span data-ttu-id="15e9b-111">傳回的字串</span><span class="sxs-lookup"><span data-stu-id="15e9b-111">String returned</span></span>|  
|-------------------------|---------------------|  
|<span data-ttu-id="15e9b-112">Boolean</span><span class="sxs-lookup"><span data-stu-id="15e9b-112">Boolean</span></span>|<span data-ttu-id="15e9b-113">"true"、"false"</span><span class="sxs-lookup"><span data-stu-id="15e9b-113">"true", "false"</span></span>|  
|<span data-ttu-id="15e9b-114">Single.PositiveInfinity</span><span class="sxs-lookup"><span data-stu-id="15e9b-114">Single.PositiveInfinity</span></span>|<span data-ttu-id="15e9b-115">"INF"</span><span class="sxs-lookup"><span data-stu-id="15e9b-115">"INF"</span></span>|  
|<span data-ttu-id="15e9b-116">Single.NegativeInfinity</span><span class="sxs-lookup"><span data-stu-id="15e9b-116">Single.NegativeInfinity</span></span>|<span data-ttu-id="15e9b-117">"-INF"</span><span class="sxs-lookup"><span data-stu-id="15e9b-117">"-INF"</span></span>|  
|<span data-ttu-id="15e9b-118">Double.PositiveInfinity</span><span class="sxs-lookup"><span data-stu-id="15e9b-118">Double.PositiveInfinity</span></span>|<span data-ttu-id="15e9b-119">"INF"</span><span class="sxs-lookup"><span data-stu-id="15e9b-119">"INF"</span></span>|  
|<span data-ttu-id="15e9b-120">Double.NegativeInfinity</span><span class="sxs-lookup"><span data-stu-id="15e9b-120">Double.NegativeInfinity</span></span>|<span data-ttu-id="15e9b-121">"-INF"</span><span class="sxs-lookup"><span data-stu-id="15e9b-121">"-INF"</span></span>|  
|<span data-ttu-id="15e9b-122">Datetime</span><span class="sxs-lookup"><span data-stu-id="15e9b-122">DateTime</span></span>|<span data-ttu-id="15e9b-123">格式為 "yyyy-MM-ddTHH:mm:sszzzzzz" 及其子集。</span><span class="sxs-lookup"><span data-stu-id="15e9b-123">Format is "yyyy-MM-ddTHH:mm:sszzzzzz" and its subsets.</span></span>|  
|<span data-ttu-id="15e9b-124">Timespan</span><span class="sxs-lookup"><span data-stu-id="15e9b-124">Timespan</span></span>|<span data-ttu-id="15e9b-125">格式為 PnYnMnTnHnMnS，即 `P2Y10M15DT10H30M20S` 代表期間為 2 年 10 個月 15 天 10 小時 30 分鐘 20 秒。</span><span class="sxs-lookup"><span data-stu-id="15e9b-125">Format is PnYnMnTnHnMnS that is, `P2Y10M15DT10H30M20S` is a duration of 2 years, 10 months, 15 days, 10 hours, 30 minutes, and 20 seconds.</span></span>|  
  
> [!NOTE]
> <span data-ttu-id="15e9b-126">若使用 **ToString** 方法將上表所列的任何 .NET Framework 型別轉換成字串，則傳回的字串將會是 XML 結構描述 (XSD) 字串型別，而不是基底型別。</span><span class="sxs-lookup"><span data-stu-id="15e9b-126">If converting any of the .NET Framework types listed in the table to a string using the **ToString** method, the returned string is not the base type, but the XML Schema (XSD) string type.</span></span>  
  
 <span data-ttu-id="15e9b-127">**DateTime** 和 **Timespan** 數值型別的差別在於，**DateTime** 代表某一個時間，而 **TimeSpan** 代表時間間隔。</span><span class="sxs-lookup"><span data-stu-id="15e9b-127">The **DateTime** and **Timespan** value type differs in that a **DateTime** represents an instant in time, whereas a **TimeSpan** represents a time interval.</span></span> <span data-ttu-id="15e9b-128">**DateTime** 和 **Timespan** 格式已指定於 XML 結構描述 (XSD) 資料型別規格中。</span><span class="sxs-lookup"><span data-stu-id="15e9b-128">The **DateTime** and **Timespan** formats are specified in the XML Schema (XSD) data types specification.</span></span> <span data-ttu-id="15e9b-129">例如：</span><span class="sxs-lookup"><span data-stu-id="15e9b-129">For example:</span></span>  
  
```vb  
Dim writer As New XmlTextWriter("myfile.xml", Nothing)  
Dim [date] As New DateTime(2001, 8, 4)  
writer.WriteElementString("Date", XmlConvert.ToString([date]))  
```  
  
```csharp  
XmlTextWriter writer = new XmlTextWriter("myfile.xml", null);  
DateTime date = new DateTime (2001, 08, 04);  
writer.WriteElementString("Date", XmlConvert.ToString(date));  
```  
  
 <span data-ttu-id="15e9b-130">**輸出**</span><span class="sxs-lookup"><span data-stu-id="15e9b-130">**Output**</span></span>  
  
 <span data-ttu-id="15e9b-131">`<Date>2001-08-04T00:00:00</Date>`.</span><span class="sxs-lookup"><span data-stu-id="15e9b-131">`<Date>2001-08-04T00:00:00</Date>`.</span></span>  
  
 <span data-ttu-id="15e9b-132">下列程式碼會將整數轉換成字串：</span><span class="sxs-lookup"><span data-stu-id="15e9b-132">The following code converts an integer to a string:</span></span>  
  
```vb  
Dim writer As New XmlTextWriter("myfile.xml", Nothing)  
Dim value As Int32 = 200  
writer.WriteElementString("Number", XmlConvert.ToString(value))  
```  
  
```csharp  
XmlTextWriter writer = new XmlTextWriter("myfile.xml", null);  
Int32 value = 200;  
writer.WriteElementString("Number", XmlConvert.ToString(value));  
```  
  
 <span data-ttu-id="15e9b-133">**輸出**</span><span class="sxs-lookup"><span data-stu-id="15e9b-133">**Output**</span></span>  
  
 `<Number>200</Number>`  
  
 <span data-ttu-id="15e9b-134">不過，如果您將字串轉換成 **Boolean**、**Single** 或 **Double**，則傳回的 .NET Framework 型別就會不同於使用 **System.Convert** 類別時所傳回的型別。</span><span class="sxs-lookup"><span data-stu-id="15e9b-134">However, if you are converting a string to **Boolean**, **Single**, or **Double**, the .NET Framework type that is returned is not the same as the type returned when using the **System.Convert** class.</span></span>  
  
## <a name="string-to-boolean"></a><span data-ttu-id="15e9b-135">字串轉成 Boolean</span><span class="sxs-lookup"><span data-stu-id="15e9b-135">String to Boolean</span></span>  
 <span data-ttu-id="15e9b-136">下列表格說明使用 **ToBoolean** 方法將字串轉換成 **Boolean** 時，給定的輸入字串會產生哪種型別。</span><span class="sxs-lookup"><span data-stu-id="15e9b-136">The following table shows what type is generated for the given input strings, when converting a string to **Boolean** using the **ToBoolean** method.</span></span>  
  
|<span data-ttu-id="15e9b-137">有效的字串輸入參數</span><span class="sxs-lookup"><span data-stu-id="15e9b-137">Valid string input parameter</span></span>|<span data-ttu-id="15e9b-138">.NET Framework 輸出型別</span><span class="sxs-lookup"><span data-stu-id="15e9b-138">.NET Framework output type</span></span>|  
|----------------------------------|--------------------------------|  
|<span data-ttu-id="15e9b-139">"true"</span><span class="sxs-lookup"><span data-stu-id="15e9b-139">"true"</span></span>|<span data-ttu-id="15e9b-140">Boolean.True</span><span class="sxs-lookup"><span data-stu-id="15e9b-140">Boolean.True</span></span>|  
|<span data-ttu-id="15e9b-141">「1」</span><span class="sxs-lookup"><span data-stu-id="15e9b-141">"1"</span></span>|<span data-ttu-id="15e9b-142">Boolean.True</span><span class="sxs-lookup"><span data-stu-id="15e9b-142">Boolean.True</span></span>|  
|<span data-ttu-id="15e9b-143">"false"</span><span class="sxs-lookup"><span data-stu-id="15e9b-143">"false"</span></span>|<span data-ttu-id="15e9b-144">Boolean.False</span><span class="sxs-lookup"><span data-stu-id="15e9b-144">Boolean.False</span></span>|  
|<span data-ttu-id="15e9b-145">"0"</span><span class="sxs-lookup"><span data-stu-id="15e9b-145">"0"</span></span>|<span data-ttu-id="15e9b-146">Boolean.False</span><span class="sxs-lookup"><span data-stu-id="15e9b-146">Boolean.False</span></span>|  
  
 <span data-ttu-id="15e9b-147">例如，假設有以下的 XML：</span><span class="sxs-lookup"><span data-stu-id="15e9b-147">For example, given the following XML:</span></span>  
  
 <span data-ttu-id="15e9b-148">**輸入**</span><span class="sxs-lookup"><span data-stu-id="15e9b-148">**Input**</span></span>  
  
```xml  
<Boolean>true</Boolean>  
<Boolean>1</Boolean>
```  
  
 <span data-ttu-id="15e9b-149">這兩者都可由下列程式碼辨識，其中 **bvalue** 為 **System.Boolean.True**：</span><span class="sxs-lookup"><span data-stu-id="15e9b-149">Both can be understood by the following code, and **bvalue** is **System.Boolean.True**:</span></span>  
  
```vb  
Dim bvalue As Boolean = _  
   XmlConvert.ToBoolean(reader.ReadElementString())  
Console.WriteLine(bvalue)  
```  
  
```csharp  
Boolean bvalue = XmlConvert.ToBoolean(reader.ReadElementString());  
Console.WriteLine(bvalue);  
```  
  
## <a name="string-to-single"></a><span data-ttu-id="15e9b-150">字串轉成 Single</span><span class="sxs-lookup"><span data-stu-id="15e9b-150">String to Single</span></span>  
 <span data-ttu-id="15e9b-151">下列表格說明使用 **ToSingle** 方法將字串轉換成 **Single**，給定的輸入字串會產生哪些型別。</span><span class="sxs-lookup"><span data-stu-id="15e9b-151">The following table shows what type is generated for the given input strings, when converting a string to a **Single** using the **ToSingle** method.</span></span>  
  
|<span data-ttu-id="15e9b-152">有效的字串輸入參數</span><span class="sxs-lookup"><span data-stu-id="15e9b-152">Valid string input parameter</span></span>|<span data-ttu-id="15e9b-153">.NET Framework 輸出型別</span><span class="sxs-lookup"><span data-stu-id="15e9b-153">.NET Framework output type</span></span>|  
|----------------------------------|--------------------------------|  
|<span data-ttu-id="15e9b-154">"INF"</span><span class="sxs-lookup"><span data-stu-id="15e9b-154">"INF"</span></span>|<span data-ttu-id="15e9b-155">Single.PositiveInfinity</span><span class="sxs-lookup"><span data-stu-id="15e9b-155">Single.PositiveInfinity</span></span>|  
|<span data-ttu-id="15e9b-156">"-INF"</span><span class="sxs-lookup"><span data-stu-id="15e9b-156">"-INF"</span></span>|<span data-ttu-id="15e9b-157">Single.NegativeInfinity</span><span class="sxs-lookup"><span data-stu-id="15e9b-157">Single.NegativeInfinity</span></span>|  
  
## <a name="string-to-double"></a><span data-ttu-id="15e9b-158">字串轉成 Double</span><span class="sxs-lookup"><span data-stu-id="15e9b-158">String to Double</span></span>  
 <span data-ttu-id="15e9b-159">下列表格說明使用 **ToDouble** 方法將字串轉換成 **Single**，給定的輸入字串會產生哪些型別。</span><span class="sxs-lookup"><span data-stu-id="15e9b-159">The following table shows what type is generated for the given input strings, when converting a string to a **Single** using the **ToDouble** method.</span></span>  
  
|<span data-ttu-id="15e9b-160">有效的字串輸入參數</span><span class="sxs-lookup"><span data-stu-id="15e9b-160">Valid string input parameter</span></span>|<span data-ttu-id="15e9b-161">.NET Framework 輸出型別</span><span class="sxs-lookup"><span data-stu-id="15e9b-161">.NET Framework output type</span></span>|  
|----------------------------------|--------------------------------|  
|<span data-ttu-id="15e9b-162">"INF"</span><span class="sxs-lookup"><span data-stu-id="15e9b-162">"INF"</span></span>|<span data-ttu-id="15e9b-163">Double.PositiveInfinity</span><span class="sxs-lookup"><span data-stu-id="15e9b-163">Double.PositiveInfinity</span></span>|  
|<span data-ttu-id="15e9b-164">"-INF"</span><span class="sxs-lookup"><span data-stu-id="15e9b-164">"-INF"</span></span>|<span data-ttu-id="15e9b-165">Double.NegativeInfinity</span><span class="sxs-lookup"><span data-stu-id="15e9b-165">Double.NegativeInfinity</span></span>|  
  
 <span data-ttu-id="15e9b-166">下列程式碼寫入 `<Infinity>INF</Infinity>`：</span><span class="sxs-lookup"><span data-stu-id="15e9b-166">The following code writes `<Infinity>INF</Infinity>`:</span></span>  
  
```vb  
Dim value As Double = Double.PositiveInfinity  
writer.WriteElementString("Infinity", XmlConvert.ToString(value))  
```  
  
```csharp  
Double value = Double.PositiveInfinity;  
writer.WriteElementString("Infinity", XmlConvert.ToString(value));  
```  
  
## <a name="see-also"></a><span data-ttu-id="15e9b-167">另請參閱</span><span class="sxs-lookup"><span data-stu-id="15e9b-167">See also</span></span>

- [<span data-ttu-id="15e9b-168">XML 資料型別轉換</span><span class="sxs-lookup"><span data-stu-id="15e9b-168">Conversion of XML Data Types</span></span>](conversion-of-xml-data-types.md)
- [<span data-ttu-id="15e9b-169">將 .NET Framework 型別轉換成字串</span><span class="sxs-lookup"><span data-stu-id="15e9b-169">Converting .NET Framework Types to Strings</span></span>](converting-dotnet-types-to-strings.md)
