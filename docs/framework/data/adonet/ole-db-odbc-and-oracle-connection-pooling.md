---
title: OLE DB、ODBC 和 Oracle 連接共用
ms.date: 03/30/2017
ms.assetid: 2bd83b1e-3ea9-43c4-bade-d9cdb9bbbb04
ms.openlocfilehash: 0ff3cbd89482645ff8d52e3144f1a82fd05d8013
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91150683"
---
# <a name="ole-db-odbc-and-oracle-connection-pooling"></a>OLE DB、ODBC 和 Oracle 連接共用

共用連接可顯著提高應用程式的效能及延展性。 本節討論 OLE DB、ODBC 及 Oracle 的 .NET Framework 資料提供者的連接共用。

## <a name="oledb"></a>OleDb

OLE DB 的 .NET Framework 資料提供者會自動使用 OLE DB 工作階段共用來共用連接。 連接字串引數可用於啟用或停用 OLE DB 服務 (包括共用)。 例如，下列連接字串會停用 OLE DB 工作階段共用及自動異動登記。

```csharp
Provider=SQLOLEDB;OLE DB Services=-4;Data Source=localhost;Integrated Security=SSPI;
```

 建議您在完成使用連接後，一定要關閉或處置該連接，以便將連接傳回集區。 未明確關閉的連接可能無法傳回集區。 例如，已離開範圍但尚未明確關閉的連接僅會在已達到最大集區大小，且連接仍然有效時，才會回到連接集區。

 如需 OLE DB 會話或資源分享的詳細資訊，以及如何藉由覆寫 OLE DB 提供者服務預設值來停用共用的詳細資訊，請參閱 OLE DB 程式設計 [人員手冊](/previous-versions/windows/desktop/ms713643(v=vs.85))。

## <a name="odbc"></a>ODBC

 ODBC 的 .NET Framework 資料提供者連接共用由用於連接的 ODBC 驅動程式管理員管理，並且不受 ODBC 的 .NET Framework 資料提供者的影響。

 若要啟用或停用連接共用，請在主控台的 [系統管理工具] 資料夾中開啟 [ **ODBC 資料來源管理員** ]。 [ **連接** 共用] 索引標籤可讓您指定每個已安裝 ODBC 驅動程式的連接共用參數。 特定 ODBC 驅動程式的連接共用變更會影響使用該 ODBC 驅動程式的所有應用程式。

## <a name="oracleclient"></a>OracleClient

 Oracle 的 .NET Framework 資料提供者會自動為 ADO.NET 用戶端應用程式提供連接共用。 您也可以提供數個連接字串修飾詞，以控制連接共用行為 (請參閱本主題稍後的＜使用連接字串關鍵字控制連接共用＞)。

### <a name="create-and-assign-pools"></a>建立和指派集區

 當開啟連接時，會依據將集區與連接中連接字串相關聯的精確比對演算法，建立連接集區。 每個連接集區與不同的連接字串相關聯。 開啟新連接時，如果連接字串與現有集區並不完全相符，則會建立新集區。

 一旦建立，便無法損毀連接集區，直到作用中處理序結束為止。 維護非作用中或空的集區所耗用的系統資源極少。

### <a name="connection-addition"></a>加入連接

 針對每個唯一連接字串可建立連接集區。 建立集區時，會建立多個連接物件並加入集區，以滿足最小集區大小需求。 視需要將連接加入集區，不超過最大集區大小。

 當要求 <xref:System.Data.OracleClient.OracleConnection> 物件時，若有可用的連接，則會從集區取得該物件。 若要可用，連接目前必須為未使用，並具有相符的異動內容，或未與任何異動內容關聯，同時具有到伺服器的有效連結。

 如果已達到最大集區大小，但仍沒有可用的連接，則會將要求排入佇列。 連接共用器會在連接釋放回集區後，重新配置連接以滿足這些要求。 連接關閉或處置時，會被釋放回集區。

### <a name="connection-removal"></a>移除連接

 連接共用器會在閒置一段時間之後，從集區中移除連接，或者，如果共用器偵測到與伺服器的連接已中斷。 只有在嘗試與伺服器通訊之後，才可以偵測到此情況。 如果發現連接已不再連接到伺服器，則會將其標記為無效。 連接共用器會定期掃描連接集區，以尋找已釋放回集區及標記為無效的物件。 然後會永久移除這些連接。

 如果連接是與已消失的伺服器連接，且連接共用器尚未偵測到已嚴重損毀的連接並將其標記為無效，則會從集區中描繪連接。 此類情況發生時，會產生例外狀況。 然而，您仍需關閉連接，以將它釋放回集區。

 請不要在您類別之 `Close` 方法中的 `Dispose`、`Connection` 或任何其他 Managed 物件上呼叫 `DataReader` 或 `Finalize`。 在完成項中，只需釋放類別直接擁有的 Unmanaged 資源。 如果類別未擁有任何 Unmanaged 資源，請不要在類別定義中包含 `Finalize` 方法。 如需詳細資訊，請參閱 [垃圾收集](../../../standard/garbage-collection/index.md)。

### <a name="transaction-support"></a>異動支援

 從集區中描繪連接，並根據異動內容進行指派。 要求執行緒的內容必須與指派的連接相符。 因此，每個連接集區都會細分為沒有相關聯交易內容的連接，並分成 *N* 個分割區，每個都包含與特定交易內容的連接。

 連接關閉時，會根據其異動內容將其釋放回集區，並置於適當的子區塊中。 因此，即使分散式交易仍處於暫止狀態，您仍可以關閉連接，而不會產生錯誤。 這可讓您稍後認可或中止分散式異動。

### <a name="control-connection-pooling-with-connection-string-keywords"></a>使用連接字串關鍵字控制連接共用

 <xref:System.Data.OracleClient.OracleConnection.ConnectionString%2A> 物件的 <xref:System.Data.OracleClient.OracleConnection> 屬性支援連接字串索引鍵/值配對，這些配對可用於調整連接共用邏輯的行為。

 下表說明可用於調整連接共用行為的 <xref:System.Data.OracleClient.OracleConnection.ConnectionString%2A> 值。

|名稱|預設|描述|
|----------|-------------|-----------------|
|`Connection Lifetime`|0|當連接傳回集區時，會將其建立時間與目前時間進行比較，如果該時間範圍 (秒) 超過 `Connection Lifetime` 指定的值，則會損毀連接。 這在叢集組態中很有用，可在執行中伺服器與剛連線的伺服器之間強制負載平衡。<br /><br /> 值零 (0) 將導致共用的連接具有最大逾時。|
|`Enlist`|'true'|為 `true` 時，如果交易內容存在，則共用器會自動在建立執行緒之目前交易內容中登記連接。|
|`Max Pool Size`|100|集區中所允許的最大連接數。|
|`Min Pool Size`|0|集區中保留的最小連接數。|
|`Pooling`|'true'|為 `true` 時，會從適當的集區描繪連接，或視需要在適當的集區中建立及加入連接。|

## <a name="see-also"></a>另請參閱

- [連接共用](connection-pooling.md)
- [效能計數器](performance-counters.md)
- [ADO.NET 概觀](ado-net-overview.md) \(部分機器翻譯\)
