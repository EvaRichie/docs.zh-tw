---
title: 位址標頭
ms.date: 03/30/2017
ms.assetid: b0c94d4a-3bde-4b4d-bb6d-9f12bc3a6940
ms.openlocfilehash: 133826bbbea62b660bdcdd884ce657528ad30873
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84576001"
---
# <a name="address-headers"></a><span data-ttu-id="15007-102">位址標頭</span><span class="sxs-lookup"><span data-stu-id="15007-102">Address Headers</span></span>

<span data-ttu-id="15007-103">位址標頭範例會示範用戶端如何使用 Windows Communication Foundation （WCF）將參考參數傳遞至服務。</span><span class="sxs-lookup"><span data-stu-id="15007-103">The Address Headers sample demonstrates how clients can pass reference parameters to a service using Windows Communication Foundation (WCF).</span></span>

> [!NOTE]
> <span data-ttu-id="15007-104">此範例的安裝程序與建置指示位於本主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="15007-104">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>

<span data-ttu-id="15007-105">WS-Addressing 規格會將端點參考的概念定義成針對特定 Web 服務端點的定址方式。</span><span class="sxs-lookup"><span data-stu-id="15007-105">The WS-Addressing specification defines the notion of an endpoint reference as a way to address a particular Web service endpoint.</span></span> <span data-ttu-id="15007-106">在 WCF 中，端點參考是使用類別來模型化， `EndpointAddress` `EndpointAddress` 而是類別的位址欄位的型別 `ServiceEndpoint` 。</span><span class="sxs-lookup"><span data-stu-id="15007-106">In WCF, endpoint references are modeled using the `EndpointAddress` class - `EndpointAddress` is the type of the Address field of the `ServiceEndpoint` class.</span></span>

<span data-ttu-id="15007-107">端點參考模型的一部分，是每個參考可以包含一些會新增額外識別資訊的參考參數。</span><span class="sxs-lookup"><span data-stu-id="15007-107">Part of the endpoint reference model is that each reference can carry some reference parameters that add extra identifying information.</span></span> <span data-ttu-id="15007-108">在 WCF 中，這些參考參數會模型化為類別的實例 `AddressHeader` 。</span><span class="sxs-lookup"><span data-stu-id="15007-108">In WCF, these reference parameters are modeled as instances of `AddressHeader` class.</span></span>

<span data-ttu-id="15007-109">在這個範例中，用戶端會新增用戶端端點之 `EndpointAddress` 的參考參數。</span><span class="sxs-lookup"><span data-stu-id="15007-109">In this sample, the client adds a reference parameter to the `EndpointAddress` of the client endpoint.</span></span> <span data-ttu-id="15007-110">服務會尋找這個參考參數，然後在其 "Hello" 服務作業的邏輯中使用這個參數的值。</span><span class="sxs-lookup"><span data-stu-id="15007-110">The service looks for this reference parameter and uses its value in the logic of its "Hello" service operation.</span></span>

## <a name="client"></a><span data-ttu-id="15007-111">用戶端</span><span class="sxs-lookup"><span data-stu-id="15007-111">Client</span></span>

<span data-ttu-id="15007-112">對於要傳送參考參數的用戶端，它必須將 `AddressHeader` 新增至 `EndpointAddress` 的 `ServiceEndpoint`。</span><span class="sxs-lookup"><span data-stu-id="15007-112">For the client to send a reference parameter, it must add an `AddressHeader` to the `EndpointAddress` of the `ServiceEndpoint`.</span></span> <span data-ttu-id="15007-113">因為 `EndpointAddress` 類別是不變的，所以必須使用 `EndpointAddressBuilder` 類別才能修改端點位址。</span><span class="sxs-lookup"><span data-stu-id="15007-113">Because the `EndpointAddress` class is immutable, modification of an endpoint address must be done using the `EndpointAddressBuilder` class.</span></span> <span data-ttu-id="15007-114">下列程式碼會初始化用戶端，以便將參考參數當做其訊息部分來傳送。</span><span class="sxs-lookup"><span data-stu-id="15007-114">The following code initializes the client to send a reference parameter as part of its message.</span></span>

```csharp
HelloClient client = new HelloClient();
EndpointAddressBuilder builder =
    new EndpointAddressBuilder(client.Endpoint.Address);
AddressHeader header =
    AddressHeader.CreateAddressHeader(IDName, IDNamespace, "John");
builder.Headers.Add(header);
client.Endpoint.Address = builder.ToEndpointAddress();
```

<span data-ttu-id="15007-115">這段程式碼會建立以原始 `EndpointAddressBuilder` 做為初始值的 `EndpointAddress`。</span><span class="sxs-lookup"><span data-stu-id="15007-115">The code creates an `EndpointAddressBuilder` using the original `EndpointAddress` as an initial value.</span></span> <span data-ttu-id="15007-116">然後，它會新增新建立的位址標頭;呼叫會 `CreateAddressHeader` 建立具有特定名稱、命名空間和值的標頭。</span><span class="sxs-lookup"><span data-stu-id="15007-116">It then adds a newly created address header; the call to `CreateAddressHeader` creates a header with a particular name, namespace, and value.</span></span> <span data-ttu-id="15007-117">此時的值為 "John"。</span><span class="sxs-lookup"><span data-stu-id="15007-117">Here the value is "John".</span></span> <span data-ttu-id="15007-118">一旦標頭新增至產生器後，`ToEndpointAddress()` 方法便會將產生器 (可變的) 轉換回端點位址 (不變的)，此位址已指派回該用戶端端點的 [位址] 欄位。</span><span class="sxs-lookup"><span data-stu-id="15007-118">Once the header is added to the builder, the `ToEndpointAddress()` method converts the (mutable) builder back into an (immutable) endpoint address, which is assigned back to the client endpoint's Address field.</span></span>

<span data-ttu-id="15007-119">現在，當用戶端呼叫 `Console.WriteLine(client.Hello());` 時，服務就能夠取得這個位址參數的值，即顯示於用戶端結果輸出中的值。</span><span class="sxs-lookup"><span data-stu-id="15007-119">Now when the client calls `Console.WriteLine(client.Hello());`, the service is able to get the value of this address parameter, as seen in the resulting output of the client.</span></span>

`Hello, John`

## <a name="server"></a><span data-ttu-id="15007-120">伺服器</span><span class="sxs-lookup"><span data-stu-id="15007-120">Server</span></span>

<span data-ttu-id="15007-121">服務作業 `Hello()` 的實作會使用目前 `OperationContext`，檢查傳入訊息上的標頭值。</span><span class="sxs-lookup"><span data-stu-id="15007-121">The implementation of the service operation `Hello()` uses the current `OperationContext` to inspect the values of the headers on the incoming message.</span></span>

```csharp
string id = null;
// look at headers on incoming message
for (int i = 0;
     i < OperationContext.Current.IncomingMessageHeaders.Count;
     ++i)
{
    MessageHeaderInfo h = OperationContext.Current.IncomingMessageHeaders[i];
    // for any reference parameters with the correct name & namespace
    if (h.IsReferenceParameter &&
        h.Name == IDName &&
        h.Namespace == IDNamespace)
    {
        // read the value of that header
        XmlReader xr = OperationContext.Current.IncomingMessageHeaders.GetReaderAtHeader(i);
        id = xr.ReadElementContentAsString();
    }
}
return "Hello, " + id;
```

<span data-ttu-id="15007-122">這段程式碼會逐一查看傳入訊息上的所有標頭，以便尋找屬於含有特定名稱之參考參數的標頭。</span><span class="sxs-lookup"><span data-stu-id="15007-122">The code iterates over all the headers on the incoming message, looking for headers that are reference parameters with the particular name and.</span></span> <span data-ttu-id="15007-123">如果有找到該參數，它會讀取參數的值，然後將該值儲存在 "id" 變數中。</span><span class="sxs-lookup"><span data-stu-id="15007-123">When the parameter is found, it reads the value of the parameter and stores it in the "id" variable.</span></span>

#### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="15007-124">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="15007-124">To set up, build, and run the sample</span></span>

1. <span data-ttu-id="15007-125">請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="15007-125">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>

2. <span data-ttu-id="15007-126">若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="15007-126">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>

3. <span data-ttu-id="15007-127">若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="15007-127">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="15007-128">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="15007-128">The samples may already be installed on your machine.</span></span> <span data-ttu-id="15007-129">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="15007-129">Check for the following (default) directory before continuing.</span></span>
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> <span data-ttu-id="15007-130">如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="15007-130">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="15007-131">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="15007-131">This sample is located in the following directory.</span></span>
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Client\AddressHeaders`
