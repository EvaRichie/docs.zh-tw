---
title: 具備傳輸安全性的 BasicBinding
ms.date: 03/30/2017
ms.assetid: f49b1de6-0254-4362-8ef2-fccd8ff9688b
ms.openlocfilehash: adf245d29ca57d919957276dfc54d82a0f45373b
ms.sourcegitcommit: ee5b798427f81237a3c23d1fd81fff7fdc21e8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/28/2020
ms.locfileid: "84144873"
---
# <a name="basicbinding-with-transport-security"></a>具備傳輸安全性的 BasicBinding

這個範例會示範透過基本繫結來使用 SSL 傳輸安全性。 這個範例是以執行計算機服務的[消費者入門](../../../../docs/framework/wcf/samples/getting-started-sample.md)為基礎。

> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\Basic\TransportSecurity`

## <a name="sample-details"></a>範例詳細資料

根據預設，基本繫結支援 HTTP 通訊。 此範例會示範如何啟用基本繫結的傳輸安全性。 在執行範例之前，您必須使用 [Web 伺服器憑證精靈] 建立並指派憑證。

> [!NOTE]
> 此範例的安裝程序與建置指示位於本主題的結尾。

範例中的程式碼與[消費者入門](../../../../docs/framework/wcf/samples/getting-started-sample.md)服務相同。 組態檔設定中的端點定義與繫結定義會修改成啟用安全通訊，如下列範例組態所示。

```xml
<system.serviceModel>
  <services>
    <service type="Microsoft.ServiceModel.Samples.CalculatorService"
             behaviorConfiguration="CalculatorServiceBehavior">
      <endpoint address=""
                binding="basicHttpBinding"
                bindingConfiguration="Binding1"
                contract="Microsoft.ServiceModel.Samples.ICalculator" />
    </service>
   </services>
  <bindings>
    <basicHttpBinding>
      <!-- Configure basicHttpBinding with Transport security -->
      <!-- mode and clientCredentialType set to None. -->
      <binding name="Binding1">
        <security mode="Transport">
          <transport clientCredentialType="None"/>
        </security>
      </binding>
    </basicHttpBinding>
  </bindings>
</system.serviceModel>
```

因為此範例中使用的憑證是使用 Makecert 建立的測試憑證，所以當您嘗試在瀏覽器中存取 HTTPS：位址時（例如），就會出現安全性警示 `https://localhost/servicemodelsamples/service.svc` 。 為了讓 Windows Communication Foundation （WCF）用戶端使用測試憑證，會將一些額外的程式碼新增至用戶端，以隱藏安全性警示。 使用實際憑證時，不需要這個程式碼及伴隨的類別。

```csharp
// This code is required only for test certificates such as those
// created by Makecert.exe.
PermissiveCertificatePolicy.Enact("CN=ServiceModelSamples-HTTPS-Server");
```

當您執行範例時，作業要求和回應會顯示在用戶端主控台視窗中。 在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。

```console
Add(100,15.99) = 115.99
Subtract(145,76.54) = 68.46
Multiply(9,81.25) = 731.25
Divide(22,7) = 3.14285714285714

Press <ENTER> to terminate client.
```

#### <a name="to-set-up-build-and-run-the-sample"></a>若要安裝、建置及執行範例

1. 使用下列命令安裝 ASP.NET 4.0：

    ```console
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable
    ```

2. 請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。

3. 請確定您已執行[Internet Information Services （IIS）伺服器憑證安裝指示](../../../../docs/framework/wcf/samples/iis-server-certificate-installation-instructions.md)。

4. 若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)中的指示。

5. 若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](../../../../docs/framework/wcf/samples/running-the-samples.md)中的指示。
