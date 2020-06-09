---
title: 服務偵錯行為
ms.date: 03/30/2017
ms.assetid: 9d8fd3fb-dc39-427a-8235-336a7e7162ba
ms.openlocfilehash: 53f21129860c644d09d1a2eb9cb956aecf8ab0ad
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84596633"
---
# <a name="service-debug-behavior"></a>服務偵錯行為

這個範例會示範如何設定服務偵錯行為設定。 此範例是以執行服務合約的[消費者入門](getting-started-sample.md)為基礎 `ICalculator` 。 這個範例會在組態檔中明確地定義服務偵錯行為。 這個行為也可以透過程式碼，以命令方式定義。

在這個範例中，用戶端是主控台應用程式 (.exe)，而服務則是由網際網路資訊服務 (IIS) 所裝載。

> [!NOTE]
> 此範例的安裝程序與建置指示位於本主題的結尾。

伺服器的 Web.config 檔會定義服務偵錯行為，以啟用說明網頁與例外狀況處理，如下列範例所示。

```xml
<behaviors>
     <serviceBehaviors>
         <behavior name="CalculatorServiceBehavior">
         <!-- WARNING: Setting includeExceptionDetailInFaults = "True" could result in leaking secured server information to the client.-->
         <!-- Please set this to false when deploying -->
             <serviceDebug includeExceptionDetailInFaults="True" httpHelpPageEnabled="True"/>
         </behavior>
     </serviceBehaviors>
</behaviors>
```

[\<serviceDebug>](../../configure-apps/file-schema/wcf/servicedebug.md)這是允許變更服務 debug 行為屬性的 configuration 元素。 使用者可以修改這項行為以達到下列目的：

- 這可允許服務傳回應用程式碼擲回的任何例外狀況，即使例外狀況未使用 <xref:System.ServiceModel.FaultContractAttribute> 宣告。 將 `includeExceptionDetailInFaults` 設定為 `true`，便可達成這個目的。 當在伺服器擲回非預期例外狀況的案例中偵錯時，這個設定非常有用。

  > [!IMPORTANT]
  > 在實際執行環境中開啟這項設定是不安全的。 未預期的伺服器例外狀況可能會包含某些不想要讓用戶端檢視的資訊，所以將 `includeExceptionDetailsInFaults` 設定為 `true` 可能會導致資訊洩漏。

- [\<serviceDebug>](../../configure-apps/file-schema/wcf/servicedebug.md)也可讓使用者啟用或停用 [說明] 頁面。 每個服務都可以選擇公開一份說明網頁，其中包含的服務相關資訊可以包括取得服務之 WSDL 的端點。 將 `httpHelpPageEnabled` 設定為 `true`，便可啟用這項功能。 如此就可讓說明網頁傳回至要求服務基底位址的 GET 要求。 您可以藉由設定另一個 `httpHelpPageUrl` 屬性來變更這個位址。 如果改用 HTTPS 而非 HTTP，則可以保護其安全。 設定 `httpsHelpPageEnabled` 和 `httpsHelpPageUrl`，便可達成這個目的。

當您執行範例時，作業要求和回應會顯示在用戶端主控台視窗中。 前三項作業 (加法、減法以及乘法) 一定會成功。 最後一個作業 (「除法」) 會因為除數為零例外狀況而失敗。

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
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Behaviors\ServiceDebug`
