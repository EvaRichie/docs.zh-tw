---
title: 基本範例
ms.date: 03/30/2017
ms.assetid: c1910bc1-3d0a-4fa6-b12a-4ed6fe759620
ms.openlocfilehash: db560ec7dea3912ecec8d84943cc9a01512d1f33
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84575767"
---
# <a name="basic-sample"></a>基本範例

這個範例示範如何建立可探索的服務，以及如何搜尋和呼叫可探索的服務。 這個範例包含二個專案：服務和用戶端。

> [!NOTE]
> 這個範例會在程式碼中實作探索。  如需在設定中執行探索的範例，請參閱[configuration](configuration-sample.md)。

## <a name="service"></a>服務

這是簡單的計算機服務實作。 與探索相關的程式碼位於 `Main` 中，其中 <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior> 會加入至服務主機，並且加入 <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>，如下列程式碼所示。

```csharp
using (ServiceHost serviceHost = new ServiceHost(typeof(CalculatorService), baseAddress))
{
    serviceHost.AddServiceEndpoint(typeof(ICalculatorService), new
      WSHttpBinding(), String.Empty);

    // Make the service discoverable over UDP multicast
    serviceHost.Description.Behaviors.Add(new ServiceDiscoveryBehavior());
    serviceHost.AddServiceEndpoint(new UdpDiscoveryEndpoint());

    serviceHost.Open();
    // ...
}
```

## <a name="client"></a>用戶端

用戶端會使用 <xref:System.ServiceModel.Discovery.DynamicEndpoint> 尋找服務。 <xref:System.ServiceModel.Discovery.DynamicEndpoint> 是標準端點，會在用戶端開啟時解析服務的端點。 在此案例中，<xref:System.ServiceModel.Discovery.DynamicEndpoint> 會根據服務合約尋找服務。 根據預設，<xref:System.ServiceModel.Discovery.DynamicEndpoint> 會透過 <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> 進行搜尋。 一旦找到服務端點，用戶端就會透過指定的繫結連線到該服務。

```csharp
public static void Main()
{
   DynamicEndpoint dynamicEndpoint = new DynamicEndpoint( ContractDescription.GetContract(typeof(ICalculatorService)), new WSHttpBinding());
   // ...
}
```

用戶端會定義稱為 `InvokeCalculatorService` 的方法，該方法會使用 <xref:System.ServiceModel.Discovery.DiscoveryClient> 類別搜尋服務。 <xref:System.ServiceModel.Discovery.DynamicEndpoint> 繼承自 <xref:System.ServiceModel.Description.ServiceEndpoint>，因此可以傳遞至 `InvokeCalculatorService` 方法。 接著在範例中會使用 <xref:System.ServiceModel.Discovery.DynamicEndpoint> 建立 `CalculatorServiceClient` 的執行個體，然後呼叫計算機服務的各項作業。

```csharp
static void InvokeCalculatorService(ServiceEndpoint serviceEndpoint)
{
   // Create a client
   CalculatorServiceClient client = new CalculatorServiceClient(serviceEndpoint);

   Console.WriteLine("Invoking CalculatorService");
   Console.WriteLine();

   double value1 = 100.00D;
   double value2 = 15.99D;

   // Call the Add service operation.
   double result = client.Add(value1, value2);
   Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);

   // Call the Subtract service operation.
   result = client.Subtract(value1, value2);
   Console.WriteLine("Subtract({0},{1}) = {2}", value1, value2, result);

   // Call the Multiply service operation.
   result = client.Multiply(value1, value2);
   Console.WriteLine("Multiply({0},{1}) = {2}", value1, value2, result);

   // Call the Divide service operation.
   result = client.Divide(value1, value2);
   Console.WriteLine("Divide({0},{1}) = {2}", value1, value2, result);
   Console.WriteLine();

   //Closing the client gracefully closes the connection and cleans up resources
   client.Close();
}
```

#### <a name="to-use-this-sample"></a>若要使用這個範例

1. 這個範例使用 HTTP 端點，若要執行這個範例，則必須加入正確的 URL ACL。 如需詳細資訊，請參閱設定[HTTP 和 HTTPS](../feature-details/configuring-http-and-https.md)。 以更高的權限執行下列命令應該就能加入適當的 ACL。 如果命令未正確執行，您可能要將 Domain 和 Username 替換成下列引數。 `netsh http add urlacl url=http://+:8000/ user=%DOMAIN%\%UserName%`

2. 使用 Visual Studio 2012，開啟基本 .sln 並建立範例。

3. 執行 service.exe 應用程式。

4. 在啟動服務之後，執行 client.exe。

5. 請注意，用戶端不需知道位址，就能找到此服務。

> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Discovery\Basic`
