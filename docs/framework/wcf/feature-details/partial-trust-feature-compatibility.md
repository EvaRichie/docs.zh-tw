---
title: 部分信任功能相容性
ms.date: 03/30/2017
ms.assetid: a36a540b-1606-4e63-88e0-b7c59e0e6ab7
ms.openlocfilehash: 85e34e365d125fe4f00756549ba5bda4311b78f8
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84579159"
---
# <a name="partial-trust-feature-compatibility"></a>部分信任功能相容性
Windows Communication Foundation （WCF）在部分信任的環境中執行時，支援有限的功能子集。 部分信任環境所支援的功能，主要是用在如 [Supported Deployment Scenarios](supported-deployment-scenarios.md) 主題所述的特定案例中。  
  
## <a name="minimum-permission-requirements"></a>基本權限需求  
 WCF 支援應用程式中以下列任一標準命名許可權集合執行的功能子集：  
  
- 中度信任權限  
  
- 網際網路區域權限  
  
 嘗試在部分信任的應用程式中使用具有更嚴格許可權的 WCF，可能會在執行時間導致安全性例外狀況。  
  
## <a name="contracts"></a>合約  
 在部分信任環境中執行時，合約有下列限制：  
  
- 實作 `[ServiceContract]` 介面的服務類別必須是 `public` 且具有 `public` 建構函式。 如果此服務類別定義 `[OperationContract]` 方法，這些方法就必須是 `public`。 如果它改為實作 `[ServiceContract]` 介面，這些方法實作可以是明確或 `private`，前提是 `[ServiceContract]` 介面為 `public`。  
  
- 使用 `[ServiceKnownType]` 屬性時，指定的方法必須是 `public`。  
  
- `[MessageContract]` 類別和其成員都可以是 `public`。 如果 `[MessageContract]` 類別在應用程式組件中定義，它可以是 `internal` 且具有 `internal` 成員。  
  
## <a name="system-provided-bindings"></a>系統提供的繫結  
 部分信任環境可充分支援 <xref:System.ServiceModel.BasicHttpBinding> 和 <xref:System.ServiceModel.WebHttpBinding> 。 <xref:System.ServiceModel.WSHttpBinding> 僅支援傳輸安全性模式。  
  
 在部分信任環境中執行時，不支援使用 HTTP 以外 (例如， <xref:System.ServiceModel.NetTcpBinding>、 <xref:System.ServiceModel.NetNamedPipeBinding>，或 <xref:System.ServiceModel.NetMsmqBinding>) 之傳輸的繫結。  
  
## <a name="custom-bindings"></a>自訂繫結  
 自訂繫結可在部分信任環境中建立並加以使用，但是必須遵守本節所指定的限制。  
  
### <a name="transports"></a>傳輸  
 唯一允許使用的傳輸繫結項目為 <xref:System.ServiceModel.Channels.HttpTransportBindingElement> 和 <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>。  
  
### <a name="encoders"></a>編碼器  
 允許使用下列編碼器：  
  
- 文字編碼器 (<xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>)。  
  
- 二進位編碼器 (<xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement>)。  
  
- Web 訊息編碼器 (<xref:System.ServiceModel.Channels.WebMessageEncodingBindingElement>)。  
  
 不支援訊息傳輸最佳化機制 (MTOM) 編碼器。  
  
### <a name="security"></a>安全性  
 部分信任的應用程式可以使用 WCF 的傳輸層級安全性功能來保護其通訊。 不支援訊息層級安全性。 設定繫結來使用訊息層級安全性會導致執行階段出現例外狀況。  
  
### <a name="unsupported-bindings"></a>不支援的繫結  
 不支援使用可信賴傳訊、交易，或訊息層級安全性的繫結。  
  
## <a name="serialization"></a>序列化  
 部分信任環境同時支援 <xref:System.Runtime.Serialization.DataContractSerializer> 和 <xref:System.Xml.Serialization.XmlSerializer> 。 然而， <xref:System.Runtime.Serialization.DataContractSerializer> 的使用需視下列情況而定：  
  
- 所有可序列化的 `[DataContract]` 型別必須是 `public`。  
  
- `[DataMember]` 型別中所有可序列化的 `[DataContract]` 欄位或屬性必須具有公用和讀/寫性質。 在部分信任的應用程式中執行 WCF 時，不支援[唯讀](https://go.microsoft.com/fwlink/?LinkID=98854)欄位的序列化和還原序列化。  
  
- 部分信任的環境不支援 `[Serializable]`/ISerializable 程式撰寫模型 (Programming Model)。  
  
- 已知型別必須在程式碼或電腦層級組態 (machine.config) 中指定。 為了安全起見，已知型別無法在應用程式層級的組態中指定。  
  
- 在部分信任環境中，實作 <xref:System.Runtime.Serialization.IObjectReference> 的型別會擲回例外狀況。  
  
 如需在部分信任應用程式中安全使用 [Partial Trust Best Practices](partial-trust-best-practices.md) 的詳細資訊，請參閱 <xref:System.Runtime.Serialization.DataContractSerializer> 中的＜序列化＞一節。  
  
### <a name="collection-types"></a>集合型別  
 有些集合型別會同時實作 <xref:System.Collections.Generic.IEnumerable%601> 和 <xref:System.Collections.IEnumerable>。 例如，可實作 <xref:System.Collections.Generic.ICollection%601>的型別。 此類型別可實作 `public` 的 `GetEnumerator()`實作，以及 `GetEnumerator()`的明確實作。 在此情況下， <xref:System.Runtime.Serialization.DataContractSerializer> 會叫用 `public` 的 `GetEnumerator()`實作，而不是叫用 `GetEnumerator()`的明確實作。 如果所有 `GetEnumerator()` 實作都不是 `public` ，且都是明確的實作，則 <xref:System.Runtime.Serialization.DataContractSerializer> 會叫用 `IEnumerable.GetEnumerator()`。  
  
 針對在部分信任環境中執行 WCF 時的集合類型，如果沒有任何實作為 `GetEnumerator()` `public` ，或它們都不是明確介面的執行，則會擲回安全性例外狀況。  
  
### <a name="netdatacontractserializer"></a>NetDataContractSerializer  
 在部分信任中， <xref:System.Collections.Generic.List%601>不支援許多 .NET Framework 集合型別，例如 <xref:System.Collections.ArrayList>、 <xref:System.Collections.Generic.Dictionary%602> 、 <xref:System.Collections.Hashtable> 和 <xref:System.Runtime.Serialization.NetDataContractSerializer> 。 這些型別的 `[Serializable]` 屬性都已經過設定，如前面「序列化」一節所述，部分信任的環境不支援這個屬性。 <xref:System.Runtime.Serialization.DataContractSerializer> 會以特殊方式處理集合，因此能夠解決這個限制，但 <xref:System.Runtime.Serialization.NetDataContractSerializer> 沒有這類機制來避免這個限制。  
  
 在部分信任中， <xref:System.DateTimeOffset> 不支援 <xref:System.Runtime.Serialization.NetDataContractSerializer> 型別。  
  
 在部分信任中執行時，無法搭配 <xref:System.Runtime.Serialization.NetDataContractSerializer> 使用代理 (透過 <xref:System.Runtime.Serialization.SurrogateSelector> 機制)。 請注意，這個限制只適用於使用代理時，不適用於序列化代理時。  
  
## <a name="enabling-common-behaviors-to-run"></a>讓通用行為執行  
 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> [\<commonBehaviors>](../../configure-apps/file-schema/wcf/commonbehaviors.md) 當應用程式在部分信任環境中執行時，未以屬性（APTCA）標記的服務或端點行為，將不會執行，而且當發生這種情況時，不會擲回任何例外狀況。 若要強制執行通用行為，您必須執行下列其中一項：  
  
- 使用 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> 屬性標記您的通用行為，讓它可以在部署為部分信任應用程式時執行。 請注意，您可以在電腦上設定登錄項目，以防止已標記 APTCA 的組件執行。 .  
  
- 確定應用程式是否會部署為完全信任的應用程式，而使用者無法修改程式碼存取安全性設定以在部分信任環境中執行應用程式。 如果可以執行這項操作，行為就不會執行，也不會擲回例外狀況。 若要確保此情況，請參閱使用[caspol.exe （代碼啟用安全性原則工具）](../../tools/caspol-exe-code-access-security-policy-tool.md)的**levelfinal**選項。  
  
 如需常見行為的範例，請參閱[如何：鎖定企業中的端點](../extending/how-to-lock-down-endpoints-in-the-enterprise.md)。  
  
## <a name="configuration"></a>組態  
 有一個例外，部分信任的程式碼只能載入本機檔案中的 WCF 設定區段 `app.config` 。 若要載入在 machine.config 或根 web.config 檔案中參考 WCF 區段的 WCF 設定區段，需要 ConfigurationPermission （無限制）。 若沒有此許可權，在載入設定時，本機設定檔外部的 WCF 設定區段（行為、系結）參考會導致例外狀況。  
  
 唯一的例外是序列化的已知型別組態，如本主題的「序列化」一節所述。  
  
> [!IMPORTANT]
> 只有在完全信任下執行時，才支援設定延伸。  
  
## <a name="diagnostics"></a>診斷  
  
### <a name="event-logging"></a>事件記錄  
 在部分信任下，只支援有限的事件記錄。 只有服務啟動錯誤以及追蹤/訊息記錄失敗，才會記錄至事件記錄檔中。 處理序最多可以記錄 5 個事件數目，以避免事件記錄檔中寫入過多訊息。  
  
### <a name="message-logging"></a>訊息記錄  
 當 WCF 在部分信任環境中執行時，訊息記錄無法運作。 如果在部分信任情況下啟用的話，儘管不會導致服務啟動失敗，但也無法記錄訊息。  
  
### <a name="tracing"></a>追蹤  
 在部分信任環境中執行時，可使用受限制的追蹤功能。 在設定檔中的 <`listeners`> 元素中，您唯一可以新增的類型是 <xref:System.Diagnostics.TextWriterTraceListener> 和新的 <xref:System.Diagnostics.EventSchemaTraceListener> 。 使用標準 <xref:System.Diagnostics.XmlWriterTraceListener> 可能導致不完整或不正確的記錄。  
  
 下列為支援的追蹤來源：  
  
- <xref:System.ServiceModel>  
  
- <xref:System.Runtime.Serialization>  
  
- <xref:System.IdentityModel.Claims>、 <xref:System.IdentityModel.Policy>、 <xref:System.IdentityModel.Selectors>和 <xref:System.IdentityModel.Tokens>。  
  
 下列為不支援的追蹤來源：  
  
- CardSpace  
  
- <xref:System.IO.Log>  

- [System.servicemodel. transactionbridge 發生](https://docs.microsoft.com/previous-versions/aa346556(v=vs.110))]
  
 您不應該指定下列 <xref:System.Diagnostics.TraceOptions> 列舉成員：  
  
- <xref:System.Diagnostics.TraceOptions.Callstack?displayProperty=nameWithType>  
  
- <xref:System.Diagnostics.TraceOptions.ProcessId?displayProperty=nameWithType>  
  
 在部分信任環境中使用追蹤時，請確定應用程式擁有足夠的權限來儲存追蹤接聽項的輸出。 例如，使用 <xref:System.Diagnostics.TextWriterTraceListener> 將追蹤輸出寫入至文字檔時，請確定應用程式具有必要的 FileIOPermission 來順利寫入追蹤檔。  
  
> [!NOTE]
> 為了避免發生重複錯誤的追蹤檔案，WCF 會在第一次安全性失敗之後，停用資源或動作的追蹤。 第一次嘗試存取資源或執行動作時，會針對每個失敗的資源存取產生一個例外狀況追蹤。  
  
## <a name="wcf-service-host"></a>WCF 服務主機  
 WCF 服務主機不支援部分信任。 如果您想要在部分信任中使用 WCF 服務，請不要使用 Visual Studio 中的 [WCF 服務程式庫] 專案範本來建立您的服務。 而是在 Visual Studio 中，選擇 [WCF 服務網站] 範本來建立新的網站，這可以在支援 WCF 部分信任的 Web 服務器中裝載服務。  
  
## <a name="other-limitations"></a>其他限制  

  WCF 通常僅限於裝載應用程式對其施加的安全性考慮。 例如，如果 WCF 裝載于 XAML 瀏覽器應用程式（XBAP），則會受限於 XBAP 限制，如[Windows Presentation Foundation 部分信任安全性](../../wpf/wpf-partial-trust-security.md)中所述。  
  
 在部分信任環境中執行 indigo2 時，不會啟用下列額外的功能：  
  
- Windows Management Instrumentation (WMI)  
  
- 僅部分啟用事件記錄 (請參閱「 **診斷** 」一節中的討論)。  
  
- 效能計數器  
  
 在部分信任環境中使用不受支援的 WCF 功能，可能會在執行時間導致例外狀況。  
  
## <a name="unlisted-features"></a>未列出的功能  
 在部分信任環境中執行時，要找到不可用的資訊片段或動作的最好方式，就是嘗試在 `try` 區塊內部存取資源或執行動作，然後捕捉 ( `catch` ) 失敗。 為了避免發生重複錯誤的追蹤檔案，WCF 會在第一次安全性失敗之後，停用資源或動作的追蹤。 第一次嘗試存取資源或執行動作時，會針對每個失敗的資源存取產生一個例外狀況追蹤。  
  
## <a name="see-also"></a>請參閱

- <xref:System.ServiceModel.Channels.HttpTransportBindingElement>
- <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>
- <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>
- <xref:System.ServiceModel.Channels.WebMessageEncodingBindingElement>
- [Supported Deployment Scenarios](supported-deployment-scenarios.md)
- [Partial Trust Best Practices](partial-trust-best-practices.md)
