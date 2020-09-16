---
title: 循環追蹤
ms.date: 03/30/2017
ms.assetid: 5ff139f9-8806-47bc-8f33-47fe6c436b92
ms.openlocfilehash: d9af1f18a507a79c9c287393652e65dcb3372444
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90552514"
---
# <a name="circular-tracing"></a>循環追蹤

這個範例會示範循環緩衝區追蹤接聽項的實作。 實際執行服務的常見案例是產生可長時間使用的服務以及可在低階進行的追蹤記錄。 這些服務會耗用大量的磁碟空間。 在進行服務疑難排解時，追蹤記錄中最近的資料往往最切合問題的解決。 這個範例將示範實作循環緩衝區追蹤接聽項，其中會將最近的追蹤保存在磁碟上，最多到某個可設定的資料數量。 這個範例是以 [消費者入門](getting-started-sample.md) 為基礎，且包含自訂追蹤接聽程式。

> [!NOTE]
> 此範例的安裝程序與建置指示位於本主題的結尾。

此範例假設您熟悉 [追蹤和訊息記錄](tracing-and-message-logging.md) 範例，並已閱讀 [追蹤和訊息記錄](tracing-and-message-logging.md) 範例所提供的檔。

## <a name="circular-buffer-trace-listener"></a>循環緩衝區追蹤接聽項

實作「循環緩衝區追蹤接聽項」的基本概念是產生兩個檔案，而這兩個檔案可以各自儲存多達追蹤記錄資料總共所需數量的一半。 接聽項會先建立一個檔案，再寫入該檔案直到資料大小上限的一半為止，然後於此時切換到第二個檔案。 當接聽項寫入到達第二個檔案的限制時，便會將新的追蹤覆寫到第一個檔案。

此接聽程式衍生自 `XmlWriteTraceListener` ，並可讓您使用 [服務追蹤檢視器工具 ( # A0) ](../service-trace-viewer-tool-svctraceviewer-exe.md)來查看記錄。 當您嘗試檢視記錄時，只要在 [服務追蹤檢視器] 工具中同時開啟這兩個記錄檔，就可以輕易地將兩個記錄檔重新合併。 [服務追蹤檢視器] 工具會自動排序追蹤，讓它們依照正確的順序出現。

## <a name="configuration"></a>組態

您可以為接聽項與來源項目新增下列程式碼，以便將服務設定為使用循環緩衝區追蹤接聽項。 在循環追蹤接聽項的組態中設定 `maxFileSizeKB` 屬性，可以指定檔案大小的上限。 這點會在下列程式碼中示範。

```xml
<system.diagnostics>
  <sources>
    <source name="System.ServiceModel" switchValue="Information,ActivityTracing" propagateActivity="true">
      <listeners>
        <add name="CircularTraceListener" />
      </listeners>
    </source>
  </sources>
  <sharedListeners>
    <add name="CircularTraceListener" type="Microsoft. Samples.ServiceModel.CircularTraceListener,CircularTraceListener"
         initializeData="c:\logs\CircularTracing-service.svclog" maxFileSizeKB="100" />
  </sharedListeners>
  <trace autoflush="true" />
</system.diagnostics>
```

#### <a name="to-set-up-build-and-run-the-sample"></a>若要安裝、建置及執行範例

1. 請確定您已執行 [Windows Communication Foundation 範例的單次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。

2. 若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。

3. 若要在單一或跨電腦的設定中執行範例，請遵循執行 [Windows Communication Foundation 範例](running-the-samples.md)中的指示。

> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Management\CircularTracing`

## <a name="see-also"></a>另請參閱

- [AppFabric 監控範例](/previous-versions/appfabric/ff383407(v=azure.10))
