---
title: MTOM 編碼方式
ms.date: 03/30/2017
ms.assetid: 820e316f-4ee1-4eb5-ae38-b6a536e8a14f
ms.openlocfilehash: cf048e1e6b2e2785accc1bde0336f07e3d84ae5e
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84602528"
---
# <a name="mtom-encoding"></a><span data-ttu-id="4a817-102">MTOM 編碼方式</span><span class="sxs-lookup"><span data-stu-id="4a817-102">MTOM Encoding</span></span>
<span data-ttu-id="4a817-103">這個範例透過 WSHttpBinding 使用「訊息傳輸最佳化機制」(Message Transmission Optimization Mechanism，MTOM) 訊息編碼。</span><span class="sxs-lookup"><span data-stu-id="4a817-103">This sample demonstrates the use of the Message Transmission Optimization Mechanism (MTOM) message encoding with a WSHttpBinding.</span></span> <span data-ttu-id="4a817-104">MTOM 是以未經處理位元組的形式，將大型二進位附件與 SOAP 訊息一起傳輸的機制，可以提供較小的訊息。</span><span class="sxs-lookup"><span data-stu-id="4a817-104">MTOM is a mechanism for transmitting large binary attachments with SOAP messages as raw bytes, allowing for smaller messages.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="4a817-105">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="4a817-105">The samples may already be installed on your machine.</span></span> <span data-ttu-id="4a817-106">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="4a817-106">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="4a817-107">如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="4a817-107">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="4a817-108">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="4a817-108">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\WS\MTOM`  
  
 <span data-ttu-id="4a817-109">根據預設，WSHttpBinding 會將訊息當做一般文字 XML 來傳送和接收。</span><span class="sxs-lookup"><span data-stu-id="4a817-109">By default, the WSHttpBinding sends and received messages as normal text XML.</span></span> <span data-ttu-id="4a817-110">若要啟用傳送和接收 MTOM 訊息的功能，請在繫結的組態 (例如，在下列範例程式碼) 中設定 `messageEncoding` 屬性 (Attribute)，或是使用 `MessageEncoding` 屬性 (Property) 直接在繫結上設定。</span><span class="sxs-lookup"><span data-stu-id="4a817-110">To enable sending and receiving MTOM messages, set the `messageEncoding` attribute on the binding's configuration (as in the following example code), or directly on the binding using the `MessageEncoding` property.</span></span> <span data-ttu-id="4a817-111">現在，服務或用戶端可以傳送和接收 MTOM 訊息。</span><span class="sxs-lookup"><span data-stu-id="4a817-111">The service or client can now send and receive MTOM messages.</span></span>  
  
```xml  
<wsHttpBinding>  
  <binding name="WSHttpBinding_IUpload" messageEncoding="Mtom" />  
</wsHttpBinding>  
```  
  
 <span data-ttu-id="4a817-112">MTOM 編碼器可以將位元組陣列和資料流最佳化。</span><span class="sxs-lookup"><span data-stu-id="4a817-112">The MTOM encoder can optimize arrays of bytes and streams.</span></span> <span data-ttu-id="4a817-113">在這個範例中，作業會使用 `Stream` 參數，因此可加以最佳化。</span><span class="sxs-lookup"><span data-stu-id="4a817-113">In this sample, the operation uses a `Stream` parameter and can therefore be optimized.</span></span>  

```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
  public interface IUpload  
  {  
      [OperationContract]  
      int Upload(Stream data);  
  }  
```
  
 <span data-ttu-id="4a817-114">這個範例選用的合約會將二進位資料傳輸至服務，然後接收已上傳的位元組數目做為傳回值。</span><span class="sxs-lookup"><span data-stu-id="4a817-114">The contract chosen for this sample transmits binary data to the service and receives the number of bytes uploaded as the return value.</span></span> <span data-ttu-id="4a817-115">當安裝了服務並執行用戶端後，範例會列出數字 1000，表示總共收到 1000 個位元組。</span><span class="sxs-lookup"><span data-stu-id="4a817-115">When the service is installed and the client is run, it prints out the number 1000, which indicates that all 1000 bytes were received.</span></span> <span data-ttu-id="4a817-116">輸出的其餘部分則列出各種承載的最佳化與非最佳化訊息大小。</span><span class="sxs-lookup"><span data-stu-id="4a817-116">The remainder of the output lists optimized and non-optimized message sizes for various payloads.</span></span>  
  
```console
Output:  
1000  
  
Text encoding with a 100 byte payload: 433  
MTOM encoding with a 100 byte payload: 912  
  
Text encoding with a 1000 byte payload: 1633  
MTOM encoding with a 1000 byte payload: 2080  
  
Text encoding with a 10000 byte payload: 13633  
MTOM encoding with a 10000 byte payload: 11080  
  
Text encoding with a 100000 byte payload: 133633  
MTOM encoding with a 100000 byte payload: 101080  
  
Text encoding with a 1000000 byte payload: 1333633  
MTOM encoding with a 1000000 byte payload: 1001080  
  
Press <ENTER> to terminate client.  
```  
  
 <span data-ttu-id="4a817-117">使用 MTOM 的目的在最佳化大型二進位承載的傳輸。</span><span class="sxs-lookup"><span data-stu-id="4a817-117">The purpose for using MTOM is to optimize the transmission of large binary payloads.</span></span> <span data-ttu-id="4a817-118">對小型二進位承載來說，使用 MTOM 傳送 SOAP 訊息會造成可觀的資源耗用，但是當它擴增到數千位元組以上時，反而會節省大量資源。</span><span class="sxs-lookup"><span data-stu-id="4a817-118">Sending a SOAP message using MTOM has a noticeable overhead for small binary payloads, but becomes a great savings when they grow over a few thousand bytes.</span></span> <span data-ttu-id="4a817-119">這是因為一般文字 XML 會使用 Base64 (每三個位元組需要四個字元) 來編碼二進位資料，使得資料大小增加三分之一。</span><span class="sxs-lookup"><span data-stu-id="4a817-119">The reason for this is that normal text XML encodes binary data using Base64, which requires four characters for every three bytes, and increases the size of the data by one third.</span></span> <span data-ttu-id="4a817-120">MTOM 能夠將二進位資料當做未經處理的位元組傳輸，不但節省編碼/解碼時間，而且也產生較小的訊息。</span><span class="sxs-lookup"><span data-stu-id="4a817-120">MTOM is able to transmit binary data as raw bytes, saving the encoding/decoding time and resulting is smaller messages.</span></span> <span data-ttu-id="4a817-121">相較於現今的商務文件和數位相片，數千位元組的臨界值實在是微不足道。</span><span class="sxs-lookup"><span data-stu-id="4a817-121">The threshold of a few thousand bytes is small when compared to today's business documents and digital photographs.</span></span>  
  
### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="4a817-122">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="4a817-122">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="4a817-123">使用下列命令安裝 ASP.NET 4.0。</span><span class="sxs-lookup"><span data-stu-id="4a817-123">Install ASP.NET 4.0 using the following command.</span></span>  
  
    ```console
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable  
    ```  
  
2. <span data-ttu-id="4a817-124">請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="4a817-124">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
3. <span data-ttu-id="4a817-125">若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="4a817-125">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
4. <span data-ttu-id="4a817-126">若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="4a817-126">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>  
