---
ms.openlocfilehash: 7f8f97adcca7e66fa5756212bb977daadd92b8b6
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/05/2020
ms.locfileid: "89496504"
---
### <a name="x509certificate2tostringboolean-does-not-throw-now-when-net-cannot-handle-the-certificate"></a>現在，當 .NET 無法處理憑證時，X509Certificate2.ToString(Boolean) 不會擲回例外狀況

#### <a name="details"></a>詳細資料

在 .NET Framework 4.5.2 和更早版本中，如果將 <code>true</code> 傳遞給詳細資訊參數，但 .NET Framework 不支援已安裝的憑證時，此方法會擲回例外狀況。 現在，此方法會成功，並傳回省略無法存取之憑證部分的有效字串。

#### <a name="suggestion"></a>建議

您應該更新所有相依於 <xref:System.Security.Cryptography.X509Certificates.X509Certificate2.ToString(System.Boolean)?displayProperty=nameWithType> 的程式碼，以確保傳回字串可在 API 先前擲回例外狀況的特定情況下排除某些憑證資料 (例如公開金鑰、私密金鑰和延伸內容)。

| 名稱    | 值       |
|:--------|:------------|
| 範圍   |Edge|
|版本|4.6|
|類型|執行階段|

#### <a name="affected-apis"></a>受影響的 API

- <xref:System.Security.Cryptography.X509Certificates.X509Certificate2.ToString(System.Boolean)?displayProperty=nameWithType>

<!--

#### Affected APIs

- `M:System.Security.Cryptography.X509Certificates.X509Certificate2.ToString(System.Boolean)`

-->
