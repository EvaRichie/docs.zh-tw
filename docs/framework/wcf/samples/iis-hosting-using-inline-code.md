---
title: 使用內嵌程式碼的 IIS 裝載
ms.date: 03/30/2017
helpviewer_keywords:
- Web hosted service
- IIS Hosting Using Inline Code Sample [Windows Communication Foundation]
ms.assetid: 56fe3687-a34b-4661-8e30-b33770f413fa
ms.openlocfilehash: 41e19c318953d7e97eb5183c5a16a3780813f94c
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90558989"
---
# <a name="iis-hosting-using-inline-code"></a>使用內嵌程式碼的 IIS 裝載

這個範例會示範如何實作由網際網路資訊服務 (IIS) 裝載的服務，此時服務程式碼內嵌在 .svc 檔中並且視需要進行編譯。 服務程式碼也可以直接實作在位於應用程式之 \App_Code 目錄的原始程式碼檔中，或是編譯成部署在 \bin 中的組件。 這個範例不會示範這些技術。

> [!NOTE]
> 此範例的安裝程序與建置指示位於本主題的結尾。

> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Hosting\WebHost\InlineCode`

此範例會示範將合約實作成定義要求-回覆通訊模式的一般服務。 該服務會裝載於 IIS，而且其服務程式碼會完整包含在 Service.svc 檔中。 該服務是由主機啟動，並且會根據傳送至服務之第一個訊息的需要進行編譯。 因此不需要先行編譯。 此服務會實作 `ICalculator` 合約，如下列程式碼中所定義：

```csharp
// Define a service contract.
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]
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
}
```

服務實作會計算並傳回適當結果。

`<%@ServiceHost language=c# Debug="true" Service="Microsoft.ServiceModel.Samples.CalculatorService" %>`

```csharp
// Service class that implements the service contract.
public class CalculatorService : ICalculator
{
    public double Add(double n1, double n2)
    {
        return n1 + n2;
    }
    public double Subtract(double n1, double n2)
    {
        return n1 - n2;
    }
    public double Multiply(double n1, double n2)
    {
        return n1 * n2;
    }
    public double Divide(double n1, double n2)
    {
        return n1 / n2;
    }
}
```

當您執行範例時，作業要求和回應會顯示在用戶端主控台視窗中。 在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。

```console
Add(100,15.99) = 115.99
Subtract(145,76.54) = 68.46
Multiply(9,81.25) = 731.25
Divide(22,7) = 3.14285714285714

Press <ENTER> to terminate client.
```

### <a name="to-set-up-build-and-run-the-sample"></a>若要安裝、建置及執行範例

1. 確定您已 [針對 Windows Communication Foundation 範例執行一次性安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。

2. 若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。

3. 建立解決方案之後，請執行 setup.bat 在 IIS 7.0 中設定 ServiceModelSamples 應用程式。 ServiceModelSamples 目錄現在應該會顯示為 IIS 7.0 應用程式。

4. 若要在單一或跨電腦的設定中執行範例，請遵循執行 [Windows Communication Foundation 範例](running-the-samples.md)中的指示。 如需如何建立可呼叫此服務之用戶端應用程式的範例，請參閱 [如何：建立用戶端](../how-to-create-a-wcf-client.md)。

## <a name="see-also"></a>另請參閱

- [AppFabric 主控與持續性範例](/previous-versions/appfabric/ff383418(v=azure.10))
