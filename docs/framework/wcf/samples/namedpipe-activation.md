---
title: NamedPipe 啟用
ms.date: 03/30/2017
ms.assetid: f3c0437d-006c-442e-bfb0-6b29216e4e29
ms.openlocfilehash: 8d9a10b94c52514db611144352653b911d109056
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84602462"
---
# <a name="namedpipe-activation"></a>NamedPipe 啟用

此範例示範裝載服務，該服務使用 Windows Process Activation Service (WAS) 啟用透過名稱管道通訊的服務。 這個範例是以[消費者入門](getting-started-sample.md)為基礎，而且需要 Windows Vista 才能執行。

> [!NOTE]
> 此範例的安裝程序與建置指示位於本主題的結尾。

> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Hosting\WASHost\NamedPipeActivation`

## <a name="sample-details"></a>範例詳細資料

此範例由用戶端主控台程式 (.exe) 和 Windows Process Activation Services (WAS) 啟動的工作處理序中裝載的服務程式庫 (.dll) 所組成。 您可以在主控台視窗中看到用戶端活動。

服務會實作定義要求-回覆通訊模式的合約。 合約是由 `ICalculator` 介面所定義，這個介面會公開數學運算 (加、減、乘、除)，如下列範例程式碼中所示。

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

用戶端會對指定的數學運算提出同步要求，然後服務實作計算並傳回適當結果。

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

範例使用沒有安全性且經過修改的 `netNamedPipeBinding` 繫結。 用戶端和服務的組態檔中會指定繫結。 服務的繫結類型在端點項目的 `binding` 屬性中指定，如下列範例組態中所示。

如果您要使用安全的具名管理繫結，請將伺服器的安全性模式變更為需要的安全性設定，並在用戶端上再次執行 svcutil.exe 以取得更新的用戶端組態檔。

```xml
<system.serviceModel>
        <services>
            <service name="Microsoft.ServiceModel.Samples.CalculatorService"
               behaviorConfiguration="CalculatorServiceBehavior">

        <!-- This endpoint is exposed at the base address provided by host: net.pipe://localhost/servicemodelsamples/service.svc  -->
        <endpoint address=""
                  binding="netNamedPipeBinding"
                  bindingConfiguration="Binding1"
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />
        <!-- the mex endpoint is exposed at net.pipe://localhost/servicemodelsamples/service.svc/mex -->
        <endpoint address="mex"
                  binding="mexNamedPipeBinding"
                  contract="IMetadataExchange" />
      </service>
        </services>
        <bindings>
            <netNamedPipeBinding>
                <binding name="Binding1" >
                    <security mode = "None">
                    </security>
                </binding >
            </netNamedPipeBinding>
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

用戶端的端點資訊設定如下列範例程式碼中所示。

```xml
<system.serviceModel>

    <client>
      <endpoint name=""
                          address="net.pipe://localhost/servicemodelsamples/service.svc"
                          binding="netNamedPipeBinding"
                          bindingConfiguration="Binding1"
                          contract="Microsoft.ServiceModel.Samples.ICalculator" />
    </client>

    <bindings>

      <!--  Following is the expanded configuration section for a NetNamedPipeBinding.
            Each property is configured with the default value. -->

      <netNamedPipeBinding>
        <binding name="Binding1"
                         maxBufferSize="65536"
                         maxConnections="10">
          <security mode = "None">
          </security>
        </binding >

      </netNamedPipeBinding>
    </bindings>

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

3. 設定 Windows Process Activation Service (WAS) 以支援具名管道啟動。

    為了方便起見，在位於範例目錄中稱為 AddNetPipeSiteBinding.cmd 的批次檔中實作下列兩個步驟。

    1. 若要支援 net.pipe 啟動，預設的網站必須先繫結至 net.pipe 通訊協定。 使用以 IIS 7.0 管理工具集安裝的 appcmd.exe 完成此操作。 從提高權限的 (系統管理員) 命令提示字元中執行下列命令。

        ```console
        %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site"
        -+bindings.[protocol='net.pipe',bindingInformation='*']
        ```

        > [!NOTE]
        > 這個命令是單行文字。

        此命令新增繫結至預設網站的 net.pipe 網站。

    2. 雖然網站中的所有應用程式共用常見的 net.pipe 繫結，但每個應用程式都可以個別啟用 net.pipe 支援。 若要啟用 /servicemodelsamples 應用程式的 net.pipe，請從提高權限的命令提示字元中執行下列命令。

        ```console
        %windir%\system32\inetsrv\appcmd.exe set app "Default Web Site/servicemodelsamples" /enabledProtocols:http,net.pipe
        ```

        > [!NOTE]
        > 這個命令是單行文字。

        此命令可讓您使用和來存取/servicemodelsamples 應用 `http://localhost/servicemodelsamples` 程式 `net.tcp://localhost/servicemodelsamples` 。

4. 若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。

5. 移除您為此範例新增的 net.pipe 網站繫結。

    為了方便起見，下列兩個步驟會以位於範例目錄中的 RemoveNetPipeSiteBinding.cmd 批次檔實作：

    1. 從提高權限的命令提示字元中執行下列命令，以從啟用的通訊協定清單中移除 net.tcp。

        ```console
        %windir%\system32\inetsrv\appcmd.exe set app "Default Web Site/servicemodelsamples" /enabledProtocols:http
        ```

        > [!NOTE]
        > 這個命令必須輸入為單行文字。

    2. 從提高權限的命令提示字元中執行下列命令以移除 net.tcp 網站繫結。

        ```console
        %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site" --bindings.[protocol='net.pipe',bindingInformation='*']
        ```

        > [!NOTE]
        > 這個命令必須輸入為單行文字。

## <a name="see-also"></a>請參閱

- [AppFabric 主控與持續性範例](https://docs.microsoft.com/previous-versions/appfabric/ff383418(v=azure.10))
