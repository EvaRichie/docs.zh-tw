---
title: 摘要格式器 (JSON)
ms.date: 03/30/2017
ms.assetid: f9c0b295-55e7-48ea-b308-ba51c7d31143
ms.openlocfilehash: 7b535a5090d3c7df59b7faada35fc324a77b5651
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84594669"
---
# <a name="feed-formatter-json"></a><span data-ttu-id="74f18-102">摘要格式器 (JSON)</span><span class="sxs-lookup"><span data-stu-id="74f18-102">Feed Formatter (JSON)</span></span>
<span data-ttu-id="74f18-103">這個範例會示範如何使用自訂 <xref:System.ServiceModel.Syndication.SyndicationFeed> 和 <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter>，序列化採用 JavaScript 物件標記法 (JSON) 格式的 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 類別執行個體。</span><span class="sxs-lookup"><span data-stu-id="74f18-103">This sample shows how to serialize an instance of a <xref:System.ServiceModel.Syndication.SyndicationFeed> class in JavaScript Object Notation (JSON) format by using a custom <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter> and the <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>.</span></span>  
  
## <a name="architecture-of-the-sample"></a><span data-ttu-id="74f18-104">範例架構</span><span class="sxs-lookup"><span data-stu-id="74f18-104">Architecture of the Sample</span></span>  
 <span data-ttu-id="74f18-105">此範例會實作繼承自 `JsonFeedFormatter` 且名為 <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter> 的類別。</span><span class="sxs-lookup"><span data-stu-id="74f18-105">The sample implements a class named `JsonFeedFormatter` that inherits from <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter>.</span></span> <span data-ttu-id="74f18-106">`JsonFeedFormatter` 類別會倚賴 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 來讀取和寫入採用 JSON 格式的資料。</span><span class="sxs-lookup"><span data-stu-id="74f18-106">The `JsonFeedFormatter` class relies on the <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> to read and write the data in JSON format.</span></span> <span data-ttu-id="74f18-107">對內部而言，此格式器會使用名為 `JsonSyndicationFeed` 和 `JsonSyndicationItem` 的自訂資料合約類型集合，控制序列化程序所產生的 JSON 格式資料。</span><span class="sxs-lookup"><span data-stu-id="74f18-107">Internally, the formatter uses a custom set of data contract types named `JsonSyndicationFeed` and `JsonSyndicationItem` to control the format of the JSON data produced by the serializer.</span></span> <span data-ttu-id="74f18-108">這些實作細節已隱藏起來不讓終端使用者看到，而是允許針對標準 <xref:System.ServiceModel.Syndication.SyndicationFeed> 和 <xref:System.ServiceModel.Syndication.SyndicationItem> 類別進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="74f18-108">These implementation details are hidden from the end user, allowing calls to be made against the standard <xref:System.ServiceModel.Syndication.SyndicationFeed> and <xref:System.ServiceModel.Syndication.SyndicationItem> classes.</span></span>  
  
## <a name="writing-json-feeds"></a><span data-ttu-id="74f18-109">寫入 JSON 摘要</span><span class="sxs-lookup"><span data-stu-id="74f18-109">Writing JSON feeds</span></span>  
 <span data-ttu-id="74f18-110">搭配 `JsonFeedFormatter` 使用 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> (已實作於這個範例) 即可寫入 JSON 摘要，如下列範例程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="74f18-110">Writing a JSON feed can be accomplished by using the `JsonFeedFormatter` (implemented in this sample) with the <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> as shown in the following sample code.</span></span>  
  
```csharp  
//Basic feed with sample data  
SyndicationFeed feed = new SyndicationFeed("Custom JSON feed", "A Syndication extensibility sample", null);  
feed.LastUpdatedTime = DateTime.Now;  
feed.Items = from s in new string[] { "hello", "world" }  
select new SyndicationItem()  
{  
    Summary = SyndicationContent.CreatePlaintextContent(s)  
};  
  
//Write the feed out to a MemoryStream in JSON format  
DataContractJsonSerializer writeSerializer = new DataContractJsonSerializer(typeof(JsonFeedFormatter));  
writeSerializer.WriteObject(stream, new JsonFeedFormatter(feed));  
```  
  
## <a name="reading-a-json-feed"></a><span data-ttu-id="74f18-111">讀取 JSON 摘要</span><span class="sxs-lookup"><span data-stu-id="74f18-111">Reading a JSON feed</span></span>  
 <span data-ttu-id="74f18-112">使用 <xref:System.ServiceModel.Syndication.SyndicationFeed>，即可從 JSON 格式化的資料流中取得 `JsonFeedFormatter`，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="74f18-112">Obtaining a <xref:System.ServiceModel.Syndication.SyndicationFeed> from a stream of JSON-formatted data can be accomplished with the `JsonFeedFormatter` as show in the following code.</span></span>  
  
 `//Read in the feed using the DataContractJsonSerializer`  
  
 `DataContractJsonSerializer readSerializer = new DataContractJsonSerializer(typeof(JsonFeedFormatter));`  
  
 `JsonFeedFormatter formatter = readSerializer.ReadObject(stream) as JsonFeedFormatter;`  
  
 `SyndicationFeed feedRead = formatter.Feed;`  
  
#### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="74f18-113">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="74f18-113">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="74f18-114">請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="74f18-114">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2. <span data-ttu-id="74f18-115">若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="74f18-115">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
3. <span data-ttu-id="74f18-116">若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="74f18-116">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="74f18-117">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="74f18-117">The samples may already be installed on your computer.</span></span> <span data-ttu-id="74f18-118">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="74f18-118">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="74f18-119">如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="74f18-119">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="74f18-120">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="74f18-120">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Syndication\JsonFeeds`  
