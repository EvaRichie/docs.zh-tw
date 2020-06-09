---
title: 雙工
ms.date: 03/30/2017
helpviewer_keywords:
- Duplex Service Contract
ms.assetid: bc5de6b6-1a63-42a3-919a-67d21bae24e0
ms.openlocfilehash: 77eab6a4975fc67c20558a53f399c7e709215587
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84575195"
---
# <a name="duplex"></a>雙工

雙工範例示範如何定義和實作雙工合約。 用戶端建立與服務的工作階段，並提供服務所需的通道以供服務將訊息傳回用戶端，這個程序即是所謂的雙工通訊。 這個範例是以[消費者入門](getting-started-sample.md)為基礎。 雙工合約被定義為一對介面，其中的主要介面從用戶端到服務，回呼介面從服務到用戶端。 在此範例中，`ICalculatorDuplex` 介面允許用戶端執行數學運算，透過工作階段執行結果。 服務傳回 `ICalculatorDuplexCallback` 介面上的結果。 雙工合約需要一個工作階段，因為必須建立內容，將用戶端與服務之間傳送的訊息關聯在一起。

> [!NOTE]
> 此範例的安裝程序與建置指示位於本主題的結尾。

在這個範例中，用戶端是主控台應用程式 (.exe)，而服務則是由網際網路資訊服務 (IIS) 所裝載。 雙工合約的定義如下：

```csharp
[ServiceContract(Namespace = "http://Microsoft.ServiceModel.Samples", SessionMode=SessionMode.Required,
                 CallbackContract=typeof(ICalculatorDuplexCallback))]
public interface ICalculatorDuplex
{
    [OperationContract(IsOneWay = true)]
    void Clear();
    [OperationContract(IsOneWay = true)]
    void AddTo(double n);
    [OperationContract(IsOneWay = true)]
    void SubtractFrom(double n);
    [OperationContract(IsOneWay = true)]
    void MultiplyBy(double n);
    [OperationContract(IsOneWay = true)]
    void DivideBy(double n);
}

public interface ICalculatorDuplexCallback
{
    [OperationContract(IsOneWay = true)]
    void Result(double result);
    [OperationContract(IsOneWay = true)]
    void Equation(string eqn);
}
```

`CalculatorService` 類別會實作主要的 `ICalculatorDuplex` 介面。 服務會使用 <xref:System.ServiceModel.InstanceContextMode.PerSession> 執行個體模式維持各工作階段的結果。 而名為 `Callback` 的私用屬性用於存取用戶端的回呼通道。 服務會使用回呼，以透過回呼介面將訊息傳回用戶端。

```csharp
[ServiceBehavior(InstanceContextMode = InstanceContextMode.PerSession)]
public class CalculatorService : ICalculatorDuplex
{
    double result = 0.0D;
    string equation;

    public CalculatorService()
    {
        equation = result.ToString();
    }

    public void Clear()
    {
        Callback.Equation($"{equation} = {result}");
        equation = result.ToString();
    }

    public void AddTo(double n)
    {
        result += n;
        equation += $" + {n}";
        Callback.Result(result);
    }

    //...

    ICalculatorDuplexCallback Callback
    {
        get
        {
            return OperationContext.Current.GetCallbackChannel<ICalculatorDuplexCallback>();
        }
    }
}
```

用戶端必須提供實作雙工合約回呼介面的類別，用於接收來自服務的訊息。 在範例中，定義 `CallbackHandler` 類別以實作 `ICalculatorDuplexCallback` 介面。

```csharp
public class CallbackHandler : ICalculatorDuplexCallback
{
   public void Result(double result)
   {
      Console.WriteLine("Result({0})", result);
   }

   public void Equation(string equation)
   {
      Console.WriteLine("Equation({0}", equation);
   }
}
```

針對雙工合約所產生的 Proxy，會要求在建構時提供 <xref:System.ServiceModel.InstanceContext>。 這個 <xref:System.ServiceModel.InstanceContext> 會用來做為站台，讓物件實作回呼介面並處理服務傳回的訊息。 <xref:System.ServiceModel.InstanceContext> 是以 `CallbackHandler` 類別的執行個體所建構。 這個物件會處理回呼介面上，從服務傳回至用戶端的訊息。

```csharp
// Construct InstanceContext to handle messages on callback interface.
InstanceContext instanceContext = new InstanceContext(new CallbackHandler());

// Create a client.
CalculatorDuplexClient client = new CalculatorDuplexClient(instanceContext);

Console.WriteLine("Press <ENTER> to terminate client once the output is displayed.");
Console.WriteLine();

// Call the AddTo service operation.
double value = 100.00D;
client.AddTo(value);

// Call the SubtractFrom service operation.
value = 50.00D;
client.SubtractFrom(value);

// Call the MultiplyBy service operation.
value = 17.65D;
client.MultiplyBy(value);

// Call the DivideBy service operation.
value = 2.00D;
client.DivideBy(value);

// Complete equation.
client.Clear();

Console.ReadLine();

//Closing the client gracefully closes the connection and cleans up resources.
client.Close();
```

組態已經過修改，以提供同時支援工作階段通訊和雙工通訊的繫結。 `wsDualHttpBinding` 支援工作階段通訊，並且藉由提供雙重 HTTP 連接 (一個方向一個連接) 允許雙工通訊。 在服務上，組態中的唯一差異是所使用的繫結。 在用戶端上，您必須設定伺服器可用來連接用戶端的位址，如下面的範例組態中所示。

```xml
<client>
  <endpoint name=""
            address="http://localhost/servicemodelsamples/service.svc"
            binding="wsDualHttpBinding"
            bindingConfiguration="DuplexBinding"
            contract="Microsoft.ServiceModel.Samples.ICalculatorDuplex" />
</client>

<bindings>
  <!-- Configure a binding that support duplex communication. -->
  <wsDualHttpBinding>
    <binding name="DuplexBinding"
             clientBaseAddress="http://localhost:8000/myClient/">
    </binding>
  </wsDualHttpBinding>
</bindings>
```

執行範例時，您會看到傳回用戶端的訊息，該用戶端位於從服務傳送出的回呼介面上。 顯示每個中繼結果，接著顯示在完成所有操作時的整個方程式。 按 ENTER 鍵關閉用戶端。

### <a name="to-set-up-build-and-run-the-sample"></a>若要安裝、建置及執行範例

1. 請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。

2. 若要建立解決方案的 c #、c + + 或 Visual Basic .NET 版本，請遵循[建立 Windows Communication Foundation 範例](building-the-samples.md)中的指示。

3. 若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。

    > [!IMPORTANT]
    > 在跨電腦設定中執行用戶端時，請務必以適當電腦的名稱取代專案的 `address` 屬性[ \<endpoint> \<client> ](../../configure-apps/file-schema/wcf/endpoint-of-client.md)中的 "localhost"，以及專案之專案的屬性（如下所 `clientBaseAddress` [\<binding>](../../configure-apps/file-schema/wcf/bindings.md) [\<wsDualHttpBinding>](../../configure-apps/file-schema/wcf/wsdualhttpbinding.md) 示）：

    ```xml
    <client>
        <endpoint name = ""
        address="http://service_machine_name/servicemodelsamples/service.svc"
        ... />
    </client>
    ...
    <wsDualHttpBinding>
        <binding name="DuplexBinding" clientBaseAddress="http://client_machine_name:8000/myClient/">
        </binding>
    </wsDualHttpBinding>
    ```

> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Contract\Service\Duplex`
