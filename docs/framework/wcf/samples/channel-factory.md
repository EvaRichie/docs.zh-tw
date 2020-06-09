---
title: 通道處理站
ms.date: 03/30/2017
ms.assetid: 09b53aa1-b13c-476c-a461-e82fcacd2a8b
ms.openlocfilehash: 2aa44c4ef274fa548d490b0d8a648457a7b1e03b
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600655"
---
# <a name="channel-factory"></a><span data-ttu-id="2c10b-102">通道處理站</span><span class="sxs-lookup"><span data-stu-id="2c10b-102">Channel Factory</span></span>

<span data-ttu-id="2c10b-103">本範例示範用戶端應用程式如何使用 <xref:System.ServiceModel.ChannelFactory> 類別而非使用產生的用戶端來建立通道。</span><span class="sxs-lookup"><span data-stu-id="2c10b-103">This sample demonstrates how a client application can create a channel with the <xref:System.ServiceModel.ChannelFactory> class instead of a generated client.</span></span> <span data-ttu-id="2c10b-104">這個範例是以執行計算機服務的[消費者入門](getting-started-sample.md)為基礎。</span><span class="sxs-lookup"><span data-stu-id="2c10b-104">This sample is based on the [Getting Started](getting-started-sample.md) that implements a calculator service.</span></span>

> [!NOTE]
> <span data-ttu-id="2c10b-105">此範例的安裝程序與建置指示位於本主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="2c10b-105">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>

<span data-ttu-id="2c10b-106">此範例使用 <xref:System.ServiceModel.ChannelFactory%601> 類別來建立服務端點的通道。</span><span class="sxs-lookup"><span data-stu-id="2c10b-106">This sample uses the <xref:System.ServiceModel.ChannelFactory%601> class to create a channel to a service endpoint.</span></span> <span data-ttu-id="2c10b-107">一般而言，若要建立服務端點的通道，您可以使用[System.servicemodel 中繼資料公用程式工具（Svcutil）](../servicemodel-metadata-utility-tool-svcutil-exe.md)來產生用戶端類型，並建立所產生類型的實例。</span><span class="sxs-lookup"><span data-stu-id="2c10b-107">Typically, to create a channel to a service endpoint you generate a client type with the [ServiceModel Metadata Utility Tool (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md) and create an instance of the generated type.</span></span> <span data-ttu-id="2c10b-108">您也可以使用 <xref:System.ServiceModel.ChannelFactory%601> 類別來建立通道，如此範例所示。</span><span class="sxs-lookup"><span data-stu-id="2c10b-108">You can also create a channel by using the <xref:System.ServiceModel.ChannelFactory%601> class, as demonstrated in this sample.</span></span> <span data-ttu-id="2c10b-109">下列範例程式碼所建立的服務，與[消費者入門](getting-started-sample.md)中的服務相同。</span><span class="sxs-lookup"><span data-stu-id="2c10b-109">The service created by the following sample code is identical to the service in the [Getting Started](getting-started-sample.md).</span></span>

```csharp
EndpointAddress address = new EndpointAddress("http://localhost/servicemodelsamples/service.svc");
WSHttpBinding binding = new WSHttpBinding();
ChannelFactory<ICalculator> factory = new
                    ChannelFactory<ICalculator>(binding, address);
ICalculator channel = factory.CreateChannel();
```

> [!IMPORTANT]
> <span data-ttu-id="2c10b-110">如果您是在跨電腦的情況中執行此範例，必須使用正在執行服務的電腦完整名稱來取代先前程式碼中的 "localhost"。</span><span class="sxs-lookup"><span data-stu-id="2c10b-110">If you are running this sample in a cross-machine scenario, you must replace "localhost" in the preceding code with the fully-qualified name of the machine that is running the service.</span></span> <span data-ttu-id="2c10b-111">此範例不會使用組態來設定端點位址，因此必須透過程式碼來完成。</span><span class="sxs-lookup"><span data-stu-id="2c10b-111">This sample does not use configuration to set the endpoint address, so this must be done in code.</span></span>

<span data-ttu-id="2c10b-112">一旦建立了通道，即可透過叫用已產生用戶端的相同方式來叫用服務作業。</span><span class="sxs-lookup"><span data-stu-id="2c10b-112">Once the channel is created, service operations can be invoked just as with a generated client.</span></span>

```csharp
// Call the Add service operation.
double value1 = 100.00D;
double value2 = 15.99D;
double result = channel.Add(value1, value2);
Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);
```

<span data-ttu-id="2c10b-113">若要關閉通道，必須先將通道轉換為 <xref:System.ServiceModel.IClientChannel> 介面。</span><span class="sxs-lookup"><span data-stu-id="2c10b-113">To close the channel, it must first be cast to an <xref:System.ServiceModel.IClientChannel> interface.</span></span> <span data-ttu-id="2c10b-114">這是因為產生的通道會使用 `ICalculator` 介面在用戶端應用程式中宣告，且使用的方法與 `Add` 和 `Subtract` 類似，但和 `Close` 不同。</span><span class="sxs-lookup"><span data-stu-id="2c10b-114">This is because the channel as generated is declared in the client application using the `ICalculator` interface, which has methods like `Add` and `Subtract` but not `Close`.</span></span> <span data-ttu-id="2c10b-115">`Close` 方法源自 <xref:System.ServiceModel.ICommunicationObject> 介面。</span><span class="sxs-lookup"><span data-stu-id="2c10b-115">The `Close` method originates on the <xref:System.ServiceModel.ICommunicationObject> interface.</span></span>

```csharp
// Close the channel.
 ((IClientChannel)client).Close();
```

<span data-ttu-id="2c10b-116">當您執行範例時，作業要求和回應會顯示在用戶端主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="2c10b-116">When you run the sample, the operation requests and responses are displayed in the client console window.</span></span> <span data-ttu-id="2c10b-117">在用戶端視窗中按 ENTER 鍵，關閉用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c10b-117">Press ENTER in the client window to shut down the client application.</span></span>

```console
Add(100,15.99) = 115.99
Subtract(145,76.54) = 68.46
Multiply(9,81.25) = 731.25
Divide(22,7) = 3.14285714285714

Press <ENTER> to terminate client.
```

### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="2c10b-118">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="2c10b-118">To set up, build, and run the sample</span></span>

1. <span data-ttu-id="2c10b-119">請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="2c10b-119">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>

2. <span data-ttu-id="2c10b-120">若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="2c10b-120">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span> <span data-ttu-id="2c10b-121">請注意，此範例不會啟用中繼資料發行。</span><span class="sxs-lookup"><span data-stu-id="2c10b-121">Note that this sample does not enable metadata publishing.</span></span> <span data-ttu-id="2c10b-122">您必須先為此範例啟用中繼資料發行，以重新產生用戶端類型。</span><span class="sxs-lookup"><span data-stu-id="2c10b-122">You must first enable metadata publishing for this sample to regenerate the client type.</span></span>

3. <span data-ttu-id="2c10b-123">若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="2c10b-123">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>

### <a name="to-run-the-sample-cross-machine"></a><span data-ttu-id="2c10b-124">若要執行跨電腦範例</span><span class="sxs-lookup"><span data-stu-id="2c10b-124">To run the sample cross machine</span></span>

1. <span data-ttu-id="2c10b-125">請使用正在執行服務的電腦完整名稱來取代下列程式碼中的 "localhost"。</span><span class="sxs-lookup"><span data-stu-id="2c10b-125">Replace "localhost" in the following code with the fully-qualified name of the machine that is running the service.</span></span>

    ```csharp
    EndpointAddress address = new EndpointAddress("http://localhost/servicemodelsamples/service.svc");
    ```

> [!IMPORTANT]
> <span data-ttu-id="2c10b-126">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="2c10b-126">The samples may already be installed on your machine.</span></span> <span data-ttu-id="2c10b-127">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="2c10b-127">Check for the following (default) directory before continuing.</span></span>
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> <span data-ttu-id="2c10b-128">如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="2c10b-128">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="2c10b-129">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="2c10b-129">This sample is located in the following directory.</span></span>
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Client\ChannelFactory`
