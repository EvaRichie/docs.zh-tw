---
title: TCP 啟用
ms.date: 03/30/2017
ms.assetid: bf8c215c-0228-4f4f-85c2-e33794ec09a7
ms.openlocfilehash: 0fa737adbdc7acc51511557877799c89849149bc
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84598654"
---
# <a name="tcp-activation"></a>TCP 啟用

這個範例會示範裝載使用 Windows Process Activation Service (WAS) 的服務，以便啟用透過 net.tcp 通訊協定進行通訊的服務。 這個範例是以[消費者入門](getting-started-sample.md)為基礎。

> [!NOTE]
> 此範例的安裝程序與建置指示位於本主題的結尾。

> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Hosting\WASHost\TCPActivation`

這個範例包括用戶端主控台程式 (.exe)，以及透過 WAS 啟用之背景工作處理序所裝載的服務程式庫 (.dll)。 您可以在主控台視窗中看到用戶端活動。

服務會實作定義要求-回覆通訊模式的合約。 合約是由 `ICalculator` 介面所定義，這個介面會公開數學運算 (加、減、乘、除)，如下列範例程式碼中所示：

```csharp
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

服務實作會計算並傳回適當結果：

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

此範例會使用 net.tcp 繫結的變化，其 TCP 連接埠共用已啟用，而安全性已關閉。 如果您想要使用安全的 TCP 繫結，請將伺服器的安全性模式變更為需要的設定，並在用戶端上重新執行 Svcutil.exe 以產生更新的用戶端組態檔。

下列範例會示範此服務的組態：

```xml
<system.serviceModel>

    <services>
      <service name="Microsoft.ServiceModel.Samples.CalculatorService"
               behaviorConfiguration="CalculatorServiceBehavior">
        <!-- This endpoint is exposed at the base address provided by host: net.tcp://localhost/servicemodelsamples/service.svc  -->
        <endpoint binding="netTcpBinding" bindingConfiguration="PortSharingBinding"
          contract="Microsoft.ServiceModel.Samples.ICalculator" />
        <!-- the mex endpoint is exposed at net.tcp://localhost/servicemodelsamples/service.svc/mex -->
        <endpoint address="mex"
                  binding="mexTcpBinding"
                  contract="IMetadataExchange" />
      </service>
    </services>
    <bindings>
      <netTcpBinding>
        <binding name="PortSharingBinding" portSharingEnabled="true">
          <security mode="None" />
        </binding>
      </netTcpBinding>
    </bindings>

    <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->
    <behaviors>
      <serviceBehaviors>
        <behavior name="CalculatorServiceBehavior">
          <serviceMetadata />
          <serviceDebug includeExceptionDetailInFaults="False" />
        </behavior>
      </serviceBehaviors>
    </behaviors>

  </system.serviceModel>
```

用戶端的端點設定如下列範例程式碼所示：

```xml
<system.serviceModel>
    <bindings>
        <netTcpBinding>
          <binding name="NetTcpBinding_ICalculator">
            <security mode="None"/>
          </binding>
        </netTcpBinding>
    </bindings>
    <client>
        <endpoint address="net.tcp://localhost/servicemodelsamples/service.svc"
            binding="netTcpBinding" bindingConfiguration="NetTcpBinding_ICalculator"
            contract="Microsoft.ServiceModel.Samples.ICalculator" name="NetTcpBinding_ICalculator" />
    </client>
</system.serviceModel>
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

1. 請確定已安裝 IIS 7.0。 WAS 啟用需要 IIS 7.0。

2. 請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。

    此外，您必須安裝 WCF 非 HTTP 啟用元件：

    1. 在 [開始]**** 功能表內選擇 [控制台]****。

    2. 選取 [**程式和功能**]。

    3. 按一下 [**開啟或關閉 Windows 元件**]。

    4. 展開 [ **Microsoft .NET Framework 3.0** ] 節點，並檢查 [ **Windows Communication Foundation 非 HTTP 啟用**] 功能。

3. 設定 WAS 成支援 TCP 啟動。

    為了方便起見，下列兩個步驟會以範例目錄中名為 AddNetTcpSiteBinding.cmd 的批次檔來加以實作。

    1. 若要支援 net.tcp 啟動，預設的網站必須先繫結至 net.tcp 連接埠。 使用 Internet Information Services 7.0 (IIS) 管理工具組所安裝的 Appcmd.exe，便可做到這點。 從系統管理員層級的命令提示字元執行下列命令：

        ```console
        %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site" -+bindings.[protocol='net.tcp',bindingInformation='808:*']
        ```

        > [!TIP]
        > 這個命令是單行文字。 這個命令會將 net.tcp 網站繫結新增至預設網站，此網站會接聽含有任何主機名稱的 TCP 連接埠 808。

    2. 雖然網站中的所有應用程式共用常見的 net.tcp 繫結，但每個應用程式都可以個別啟用 net.tcp 支援。 若要為 /servicemodelsamples 應用程式啟用 net.tcp，請從系統管理員層級命令提示字元中執行下列命令：

        ```console
        %windir%\system32\inetsrv\appcmd.exe set app
        "Default Web Site/servicemodelsamples" /enabledProtocols:http,net.tcp
        ```

        > [!NOTE]
        > 這個命令是單行文字。 此命令可讓您使用和來存取/servicemodelsamples 應用 `http://localhost/servicemodelsamples` 程式 `net.tcp://localhost/servicemodelsamples` 。

4. 若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。

5. 若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。

    移除您為此範例新增的 net.tcp 網站繫結。

    為了方便起見，下列兩個步驟會以範例目錄中名為 RemoveNetTcpSiteBinding.cmd 的批次檔來加以實作。

    1. 從啟用的通訊協定清單中移除 net.tcp，方法是從系統管理員層級命令提示字元中執行下列命令：

        ```console
        %windir%\system32\inetsrv\appcmd.exe set app
        "Default Web Site/servicemodelsamples" /enabledProtocols:http
        ```

        > [!NOTE]
        > 這個命令必須輸入為單行文字。

    2. 移除 net.tcp 網站繫結，方法是從系統管理員層級命令提示字元中執行下列命令：

        ```console
        %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site"
        --bindings.[protocol='net.tcp',bindingInformation='808:*']
        ```

        > [!NOTE]
        > 這個命令必須輸入為單行文字。

## <a name="see-also"></a>請參閱

- [AppFabric 主控與持續性範例](https://docs.microsoft.com/previous-versions/appfabric/ff383418(v=azure.10))
