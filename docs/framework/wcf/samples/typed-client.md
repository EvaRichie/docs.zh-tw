---
title: 型別用戶端
ms.date: 03/30/2017
ms.assetid: 62c40e8f-e9b4-4b1a-939a-93c37393d343
ms.openlocfilehash: fe10a967a184666ad17f3ef93ecb3c4cffce46c7
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84591172"
---
# <a name="typed-client"></a>型別用戶端
此範例會示範如何從由[System.servicemodel 中繼資料公用程式工具（Svcutil）](../servicemodel-metadata-utility-tool-svcutil-exe.md)產生的具型別用戶端取得資訊。 這個範例是以執行計算機服務的[消費者入門](getting-started-sample.md)為基礎。 在這個範例中，用戶端是主控台應用程式 (.exe)，而服務則是由網際網路資訊服務 (IIS) 所裝載。  
  
> [!NOTE]
> 此範例的安裝程序與建置指示位於本主題的結尾。  
  
 用戶端的 `Endpoint` 屬性允許存取正在與用戶端通訊之服務端點的相關資訊，其中包含位址、繫結與合約資訊。 用戶端的 `InnerChannel` 屬性是 <xref:System.ServiceModel.IClientChannel> 的執行個體，其允許存取有關基礎通道的資訊，例如其狀態與工作階段識別項。  
  
```csharp
// Create a client.  
CalculatorClient client = new CalculatorClient();  
...  
Console.WriteLine("Client - endpoint:  " + client.Endpoint.Address);  
Console.WriteLine("Client - binding:  " + client.Endpoint.Binding.Name);  
Console.WriteLine("Client - contract: " + client.Endpoint.Contract.Name);  
  
IClientChannel channel = client.InnerChannel;  
Console.WriteLine("Client channel - state: " + channel.State);  
Console.WriteLine("Client channel - session identifier: " + channel.SessionId);  
  
//Closing the client gracefully closes the connection and cleans up resources.  
client.Close();  
```  
  
 當您執行範例時，作業要求和回應會顯示在用戶端主控台視窗中。 在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。  
  
```console  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Client - endpoint:  http://localhost/servicemodelsamples/service.svc  
Client - binding:  WSHttpBinding  
Client - contract: ICalculator  
Client channel - state: Opened  
Client channel - session identifier: urn:uuid:ae16fbc4-2964-4e87-9fb1-c5aa78fc567e  
  
Press <ENTER> to terminate client.  
```  
  
### <a name="to-set-up-build-and-run-the-sample"></a>若要安裝、建置及執行範例  
  
1. 請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2. 若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。  
  
3. 若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。  
  
> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> 如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Client\TypedClient`  
