---
title: XmlReader 範例
ms.date: 03/30/2017
helpviewer_keywords:
- XML Reader
ms.assetid: 60e5848d-7d9c-4ea5-bed9-22758c9ac16c
ms.openlocfilehash: 470a3ad0d3241e51676928b77dd93e5d31249515
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84594812"
---
# <a name="xmlreader-sample"></a><span data-ttu-id="d9297-102">XmlReader 範例</span><span class="sxs-lookup"><span data-stu-id="d9297-102">XmlReader Sample</span></span>

<span data-ttu-id="d9297-103">XmlReader 範例會示範使用 <xref:System.Xml.XmlReader> 處理訊息本文。</span><span class="sxs-lookup"><span data-stu-id="d9297-103">The XmlReader sample demonstrates the processing of a message body using an <xref:System.Xml.XmlReader>.</span></span> <span data-ttu-id="d9297-104">此範例是以執行計算機服務的[消費者入門](getting-started-sample.md)為基礎。</span><span class="sxs-lookup"><span data-stu-id="d9297-104">The sample is based on the [Getting Started](getting-started-sample.md), which implements a calculator service.</span></span> <span data-ttu-id="d9297-105">範例中所新增的另一項服務作業 `Sum`，會接受內含要一起加總之值陣列的訊息。</span><span class="sxs-lookup"><span data-stu-id="d9297-105">An additional service operation, `Sum`, has been added that accepts a message that contains an array of values to add together.</span></span> <span data-ttu-id="d9297-106">服務會使用 <xref:System.Xml.XmlReader> 讀取訊息。</span><span class="sxs-lookup"><span data-stu-id="d9297-106">The service reads the message using an <xref:System.Xml.XmlReader>.</span></span>

> [!NOTE]
> <span data-ttu-id="d9297-107">此範例的安裝程序與建置指示位於本主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="d9297-107">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>

<span data-ttu-id="d9297-108">計算機介面會包含名為 `Sum` 的服務作業，此作業會接受 <xref:System.ServiceModel.Channels.Message> 參數，如下列範例程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="d9297-108">The calculator interface includes a service operation named `Sum` that accepts a <xref:System.ServiceModel.Channels.Message> parameter, as shown in the following sample code.</span></span>

```csharp
public interface ICalculator
{
    [OperationContract]
    double Add(double n1, double n2);
    [OperationContract]
    double Subtract(double n1, double n2);
    [OperationContract]
    double Multiply(double n1, double n2);
    [OperationContract]
    double Divide(double n1, double n2);
    [OperationContract]
    Message Sum(Message message);
}
```

<span data-ttu-id="d9297-109">用戶端存取 `Sum` 的方式是先建立整數值陣列，然後從該陣列建立訊息，接著使用所建立的訊息呼叫 `Sum` 方法，如下列範例程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="d9297-109">The client accesses `Sum` by first creating an array of integer values, then creating a message from the array, and then calling the `Sum` method using the created message, as shown in the following sample code.</span></span>

```csharp
CalculatorClient client = new CalculatorClient();
//...

// Call the Sum service operation.
int[] values = { 1, 2, 3, 4, 5 };
using (new OperationContextScope(client.InnerChannel))
{
    Message request = Message.CreateMessage(OperationContext.Current.OutgoingMessageHeaders.MessageVersion, "http://Microsoft.ServiceModel.Samples/ICalculator/Sum", values);
    Message reply = client.Sum(request);
    int sum = reply.GetBody<int>();

    Console.WriteLine("Sum(1,2,3,4,5) = {0}", sum);
}
```

<span data-ttu-id="d9297-110">在進行此服務時，服務作業 `Sum` 的實作會使用 <xref:System.Xml.XmlReader> 物件來存取訊息本文，以便逐一查看要加總的值。</span><span class="sxs-lookup"><span data-stu-id="d9297-110">In the service, the implementation of the service operation `Sum` accesses the message body using an <xref:System.Xml.XmlReader> object to iterate through the values to sum.</span></span> <span data-ttu-id="d9297-111">此時會呼叫 <xref:System.ServiceModel.Channels.Message.GetReaderAtBodyContents%2A> 方法來存取訊息本文，如下列範例程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="d9297-111">The <xref:System.ServiceModel.Channels.Message.GetReaderAtBodyContents%2A> method is called to access the message body, as shown in the following sample code.</span></span>

```csharp
public int Sum(Message message)
{
    int sum = 0;
    string text = "";

    //The body of the message contains a list of numbers that are read
    //directly using an XmlReader.
    XmlReader body = message.GetReaderAtBodyContents ();
    while (body.Read())
    {
        text = body.ReadString().Trim();
        if (text.Length>0)
        {
            sum += Convert.ToInt32(text);
        }
    }
    body.Close();
    Message response = Message.CreateMessage(
       "http://Microsoft.ServiceModel.Samples/ICalculator/SumResponse",
       sum);
    return response;
}
```

<span data-ttu-id="d9297-112">當您執行範例時，作業的要求和回應會顯示在用戶端主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="d9297-112">When you run the sample, the requests and responses of the operation are displayed in the client console window.</span></span> <span data-ttu-id="d9297-113">在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。</span><span class="sxs-lookup"><span data-stu-id="d9297-113">Press ENTER in the client window to shut down the client.</span></span>

```console
Add(100,15.99) = 115.99
Subtract(145,76.54) = 68.46
Multiply(9,81.25) = 731.25
Divide(22,7) = 3.14285714285714
Sum(1,2,3,4,5) = 15

Press <ENTER> to terminate client.
```

### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="d9297-114">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="d9297-114">To set up, build, and run the sample</span></span>

1. <span data-ttu-id="d9297-115">請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="d9297-115">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>

2. <span data-ttu-id="d9297-116">若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="d9297-116">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>

3. <span data-ttu-id="d9297-117">若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="d9297-117">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d9297-118">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="d9297-118">The samples may already be installed on your machine.</span></span> <span data-ttu-id="d9297-119">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="d9297-119">Check for the following (default) directory before continuing.</span></span>
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> <span data-ttu-id="d9297-120">如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="d9297-120">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="d9297-121">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="d9297-121">This sample is located in the following directory.</span></span>
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Contract\Message\XmlReader`
