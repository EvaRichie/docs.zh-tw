---
title: AppCoNtextSwitchOverrides 元素
ms.custom: updateeachrelease
ms.date: 04/18/2019
helpviewer_keywords:
- AppContextSwitchOverrides
- compatibility switches
- configuration switches
- configuration
ms.assetid: 4ce07f47-7ddb-4d91-b067-501bd8b88752
ms.openlocfilehash: 8d5cd73bb9393533cb669581420e24297cb5ff71
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "82102927"
---
# <a name="appcontextswitchoverrides-element"></a>\<AppContextSwitchOverrides> 項目

定義一或多個由 <xref:System.AppContext> 類別所使用的參數，以提供新功能的退出機制。

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<AppContextSwitchOverrides>**

## <a name="syntax"></a>語法

```xml
<AppContextSwitchOverrides value="name1=value1[[;name2=value2];...]" />
```

## <a name="attributes-and-elements"></a>屬性和項目
 下列章節說明屬性、子元素和父元素。

### <a name="attributes"></a>屬性

|屬性|描述|
|---------------|-----------------|
|`value`|必要屬性。<br /><br /> 定義一或多個參數名稱及其相關聯的布林值。|

### <a name="value-attribute"></a>value 屬性

|值|描述|
|-----------|-----------------|
|「名稱 = 值」|預先定義的參數名稱以及其值（ `true` 或 `false` ）。 多個交換器名稱/值組會以分號（";"）分隔。 如需 .NET Framework 支援的預先定義參數名稱清單，請參閱備註一節。|

### <a name="child-elements"></a>子元素
 無。

### <a name="parent-elements"></a>父項目

|元素|描述|
|-------------|-----------------|
|`configuration`|通用語言執行平台和 .NET Framework 應用程式所使用之每個組態檔中的根項目。|
|`runtime`|包含有關執行階段初始化選項的資訊。|

## <a name="remarks"></a>備註
 從 .NET Framework 4.6 開始， `<AppContextSwitchOverrides>` 設定檔中的專案可讓 API 的呼叫者判斷其應用程式是否可以利用新功能，或保留與舊版程式庫的相容性。 例如，如果 API 的行為在兩個版本的程式庫之間已變更， `<AppContextSwitchOverrides>` 元素可讓該 api 的呼叫者選擇不支援新功能之程式庫版本的新行為。 對於在 .NET Framework 中呼叫 Api 的應用程式， `<AppContextSwitchOverrides>` 如果應用程式是在包含該功能的 .NET Framework 版本上執行，則專案也可以允許其應用程式以較早版本的 .NET Framework 為目標的呼叫者選擇新功能。

 `value`元素的屬性 `<AppContextSwitchOverrides>` 包含單一字串，其中包含一或多個以分號分隔的名稱/值配對。  每個名稱都會識別相容性參數，而其對應的值是布林（ `true` 或 `false` ），表示是否已設定參數。 根據預設，參數為 `false` ，而程式庫會提供新的功能。 它們只會在設定參數時提供先前的功能（亦即，其值為 `true` ）。 這可讓程式庫提供現有 API 的新行為，同時允許相依于先前行為的呼叫端選擇不使用新的功能。

.NET Framework 支援下列參數：

|交換器名稱|描述|引導|
|-----------------|-----------------|----------------|
|`Switch.MS.Internal.`<br/>`DoNotApplyLayoutRoundingToMarginsAndBorderThickness`|控制 Windows Presentation Foundation 是否使用舊版的控制項配置演算法。 如需詳細資訊，請參閱[風險降低：WPF 版面配置](../../../migration-guide/mitigation-wpf-layout.md)。|.NET Framework 4.6|
|`Switch.MS.Internal.`<br/>`UseSha1AsDefaultHashAlgorithmForDigitalSignatures`|控制用於 PackageDigitalSignatureManager 封裝元件的預設演算法是否為 SHA1 或 SHA256。<br>由於 SHA1 的衝突問題，Microsoft 建議使用 SHA256。|.NET Framework 4.7.1|
|`Switch.System.Activities.`<br/>`UseMD5CryptoServiceProviderForWFDebugger`|設定為時 `false` ，允許在啟用 FIPS 時，使用 Visual Studio 來進行 XAML 型工作流程專案的調試。 如果沒有它， <xref:System.NullReferenceException> 就會在對 system.object 元件中方法的呼叫中擲回。|.NET Framework 4.7|
|`Switch.System.Activities.`<br/>`UseMD5ForWFDebugger`|控制偵錯工具中的工作流程實例總和檢查碼是否使用 MD5 或 SHA1。 | .NET Framework 4.7|
|`Switch.System.Activities.`<br/>`UseSHA1HashForDebuggerSymbols`|控制工作流程總和檢查碼雜湊是否使用在 .NET Framework 4.7 （）中引進為預設值的 SHA1 演算法 `true` ，或是否使用 .NET Framework 4.8 （）中導入為預設值的預設 SHA256 演算法 `false` 。<br>由於 SHA1 的衝突問題，Microsoft 建議使用 SHA256。|.NET Framework 4.8|
|`Switch.System.Diagnostics.`<br/>`IgnorePortablePDBsInStackTraces`|控制使用可移植 Pdb 時是否取得堆疊追蹤，可以包含原始程式檔和行資訊。 `false`包含原始程式檔和行資訊;否則為 `true` 。|.NET Framework 4.7.2|
|`Switch.System.Drawing.`<br/>`DontSupportPngFramesInIcons`|控制 <xref:System.Drawing.Icon.ToBitmap%2A?displayProperty=nameWithType> 當 <xref:System.Drawing.Icon> 物件具有 PNG 畫面格時，方法是否擲回例外狀況。 如需詳細資訊，請參閱[風險降低：Icon 物件中的 PNG 畫面格](../../../migration-guide/mitigation-png-frames-in-icon-objects.md)。|.NET Framework 4.6|
|`Switch.System.Drawing.Text.`<br/>`DoNotRemoveGdiFontsResourcesFromFontCollection`|判斷 <xref:System.Drawing.Text.PrivateFontCollection?displayProperty=nameWithType> 當方法將物件新增至集合時，是否已正確處置物件 <xref:System.Drawing.Text.PrivateFontCollection.AddFontFile(System.String)?displayProperty=nameWithType> 。 `true`若要維護舊版行為，`false`以處置所有私用字型物件。 |.NET Framework 4.7.2|
|`Switch.System.Drawing.Printing.`<br>`OptimizePrintPreview`|控制是否 <xref:System.Windows.Forms.PrintPreviewDialog> 針對網路印表機優化的效能。 如需詳細資訊，請參閱[PrintPreviewDialog 控制項總覽](../../../winforms/controls/printpreviewdialog-control-overview-windows-forms.md)。|.NET Framework 4.6|
|`Switch.System.Globalization.EnforceJapaneseEraYearRanges`|控制是否強制執行日文日曆紀元的年份範圍檢查。 `true`強制執行年份範圍檢查，並 `false` 將其停用（預設行為）。 如需詳細資訊，請參閱[使用行事曆](../../../../standard/datetime/working-with-calendars.md)。|.NET Framework 4.6|
|`Switch.System.Globalization.EnforceLegacyJapaneseDateParsing`|控制是否只在剖析作業中，將 "1" 辨識為日本日曆紀元的第一年。 `true`僅辨識 "1";表示 `false` 要辨識 "1" 或 Gannen （預設行為）。 如需詳細資訊，請參閱[使用行事曆](../../../../standard/datetime/working-with-calendars.md)。|.NET Framework 4.6|
|`Switch.System.Globalization.FormatJapaneseFirstYearAsANumber`|控制日本日曆紀元的第一年是否在格式化作業中表示為 "1" 或 Gannen。 `true`將紀元的第一年格式化為 "1";`false`將其格式化為 Gannen （預設行為）。 如需詳細資訊，請參閱[使用行事曆](../../../../standard/datetime/working-with-calendars.md)。|.NET Framework 4.6|
|`Switch.System.Globalization.NoAsyncCurrentCulture`|控制非同步作業是否不會從呼叫執行緒的內容流動。 如需詳細資訊，請參閱跨工作的[CurrentCulture 和 CurrentUICulture 流程](../../../migration-guide/retargeting/4.5.2-4.6.md#currentculture-and-currentuiculture-flow-across-tasks)。|.NET Framework 4.6|
|`Switch.System.IdentityModel.`<br/>`DisableMultipleDNSEntriesInSANCertificate`|控制方法是否 <xref:System.IdentityModel.Claims.X509CertificateClaimSet.FindClaims%2A?displayProperty=nameWithType> 只嘗試比對宣告類型與最後一個 DNS 專案。 如需詳細資訊，請參閱[風險降低：X509CertificateClaimSet.FindClaims 方法](../../../migration-guide/mitigation-x509certificateclaimset-findclaims-method.md)。|.NET Framework 4.6.1|
|`Switch.System.IdentityModel.`<br/>`EnableCachedEmptyDefaultAuthorizationContext`|控制是否允許 AuthorizationCoNtext 傳回可變物件。|.NET Framework 4.6|
|`Switch.System.IO.BlockLongPaths`|控制路徑長度超過 `MAX_PATH` （260個字元）是否擲回 <xref:System.IO.PathTooLongException> 。 如需詳細資訊，請參閱[長路徑支援](../../../migration-guide/retargeting/4.6.1-4.6.2.md#long-path-support)。|.NET Framework 4.6.2|
|`Switch.System.IO.Compression.`<br/>`DoNotUseNativeZipLibraryForDecompression`|控制類別是否使用原生 OS 常式進行解壓縮 <xref:System.IO.Compression.DeflateStream> 。 `false`使用原生 Api;`true`使用實作為 <xref:System.IO.Compression.DeflateStream> 。|.NET Framework 4.7.2|
|`Switch.System.IO.Compression.ZipFile.`<br/>`UseBackslash`|使用反斜線（" \\ "），而不是正斜線（"/"）做為屬性中的路徑分隔符號 <xref:System.IO.Compression.ZipArchiveEntry.FullName%2A?displayProperty=nameWithType> 。 如需詳細資訊，請參閱[風險降低： ziparchiveentry 中. FullName 路徑分隔符號](../../../migration-guide/mitigation-ziparchiveentry-fullname-path-separator.md)。|.NET Framework 4.6.1|
|`Switch.System.IO.Ports.`<br/>`DoNotCatchSerialStreamThreadExceptions`|控制在以資料流程建立的背景執行緒上擲回的作業系統例外狀況是否 <xref:System.IO.Ports.SerialPort> 終止進程。|.NET Framework 4.7.1|
|`Switch.System.IO.`<br/>`UseLegacyPathHandling`|控制是否使用舊版路徑正規化，以及和方法是否支援 URI 路徑 <xref:System.IO.Path.GetDirectoryName%2A?displayProperty=nameWithType> <xref:System.IO.Path.GetPathRoot%2A?displayProperty=nameWithType> 。 如需詳細資訊，請參閱[風險降低：路徑](../../../migration-guide/mitigation-path-normalization.md)正規化和[緩和：路徑冒號檢查](../../../migration-guide/mitigation-path-colon-checks.md)。|.NET Framework 4.6.2|
|`Switch.System.`<br/>`MemberDescriptorEqualsReturnsFalseIfEquivalent`|控制是否相等的測試會比較 <xref:System.ComponentModel.MemberDescriptor.Category%2A?displayProperty=nameWithType> 一個物件的屬性與 <xref:System.ComponentModel.MemberDescriptor.Description%2A?displayProperty=nameWithType> 第二個物件的屬性。 如需詳細資訊，請參閱[System.componentmodel.memberdescriptor.equals 不正確的執行](../../../migration-guide/retargeting/4.6.1-4.6.2.md#incorrect-implementation-of-memberdescriptorequals)。|.NET Framework 4.6.2|
 `Switch.System.Net.`<br/>`DontCheckCertificateEKUs`|停用憑證增強金鑰使用方法（EKU）物件識別碼（OID）驗證。 增強金鑰使用方法 (EKU) 延伸模組是表示使用金鑰之應用程式的物件識別碼 (OID) 集合。|.NET Framework 4.6|
|`Switch.System.Net.`<br/>`DontEnableSchSendAuxRecord`|停用 SCH_SEND_AUX_RECORD，藉此停用 TLS 1.0 瀏覽器，以避免 SSL/TLS （BEAST）緩和。|.NET Framework 4.6|
|`Switch.System.Net.`<br/>`DontEnableSchUseStrongCrypto`|控制 <xref:System.Net.ServicePointManager?displayProperty=nameWithType> 和類別是否 <xref:System.Net.Security.SslStream?displayProperty=nameWithType> 可以使用 SSL 3.0 通訊協定。 如需詳細資訊，請參閱[風險降低：TLS 通訊協定](../../../migration-guide/mitigation-tls-protocols.md)。|.NET Framework 4.6|
|`Switch.System.Net.`<br/>`DontEnableSystemDefaultTlsVersions`|停用 SystemDefault 的 TLS 版本還原為預設的 Tls12、Tls11、Tls。|.NET Framework 4.7|
|`Switch.System.Net.`<br/>`DontEnableTlsAlerts`|停用 SslStream TLS 伺服器端警示。|.NET Framework 4.7|
|`Switch.System.Runtime.InteropServices.`<br/>`DoNotMarshalOutByrefSafeArrayOnInvoke`|控制 COM Interop 事件上的 ByRef SafeArray 參數是否會封送處理回機器碼（ `false` ），或是否已停用送回機器碼（ `true` ）。|.NET Framework 4.8|
|`Switch.System.Runtime.Serialization.`<br/>`DoNotUseECMAScriptV6EscapeControlCharacter` |控制[DataContractJsonSerializer](xref:System.Runtime.Serialization.Json.DataContractJsonSerializer)是否會根據 ECMAScript V6 和 V8 標準序列化某些控制字元。 如需詳細資訊，請參閱[風險降低︰使用 DataContractJsonSerializer 控制字元的序列化](../../../migration-guide/mitigation-serialization-control-characters.md)| .NET Framework 4.7 |
|`Switch.System.Runtime.Serialization.`<br/>`DoNotUseTimeZoneInfo`|控制是否 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 支援多個調整，或只針對某個時區進行單一調整。 如果為 `true` ，則會使用 <xref:System.TimeZoneInfo> 類型來序列化和還原序列化日期和時間資料; 否則，它 <xref:System.TimeZone> 會使用不支援多個調整規則的類型。|.NET Framework 4.6.2|
|`Switch.System.Runtime.Serialization.UseNewMaxArraySize`|控制 <xref:System.Runtime.Serialization.ObjectManager?displayProperty=nameWithType> 物件序列化和還原序列化期間，是否使用較大的陣列大小。 將此參數設定為 `true` ，可依類型（例如）改善大型物件圖形的序列化和還原序列化效能 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> 。 |.NET Framework 4.7.2|
|`Switch.System.Security.ClaimsIdentity.`<br/>`SetActorAsReferenceWhenCopyingClaimsIdentity`|控制此函 <xref:System.Security.Claims.ClaimsIdentity.%23ctor%28System.Security.Principal.IIdentity%29> <xref:System.Security.Claims.ClaimsIdentity.Actor%2A?displayProperty=nameWithType> 式是否使用現有的物件參考來設定新物件的屬性。 如需詳細資訊，請參閱[風險降低︰ClaimsIdentity 建構函式](../../../migration-guide/retargeting/4.6.1-4.6.2.md)。|.NET Framework 4.6.2|
|`Switch.System.Security.Cryptography.`<br/>`AesCryptoServiceProvider.DontCorrectlyResetDecryptor`|控制是否嘗試重複使用解密程式會擲回 <xref:System.Security.Cryptography.AesCryptoServiceProvider> <xref:System.Security.Cryptography.CryptographicException> 。 如需詳細資訊，請參閱[AesCryptoServiceProvider 解密程式提供可重複使用的轉換](../../../migration-guide/retargeting/4.6.1-4.6.2.md#aescryptoserviceprovider-decryptor-provides-a-reusable-transform)。|.NET Framework 4.6.2|
|`Switch.System.Security.Cryptography.`<br/>`DoNotAddrOfCspParentWindowHandle`|控制[CspParameters. system.security.cryptography.cspparameters.parentwindowhandle](xref:System.Security.Cryptography.CspParameters.ParentWindowHandle)屬性的值是否為代表視窗控制碼之記憶體位置的[IntPtr](xref:System.IntPtr) ，或其是否為視窗控制碼（HWND）。 如需詳細資訊，請參閱[風險降低︰CspParameters.ParentWindowHandle 應該有 HWND](../../../migration-guide/retargeting/4.6.2-4.7.md#cspparametersparentwindowhandle-now-expects-hwnd-value)。 |.NET Framework 4.7|
|`Switch.System.Security.Cryptography.`<br/>`UseLegacyFipsThrow`|控制在 FIPS 模式中使用受管理的加密類別是否會擲回 <xref:System.Security.Cryptography.CryptographicException> （ `true` ），或依賴系統程式庫（ `false` ）的執行。|.NET Framework 4.8|
|`Switch.System.Security.Cryptography.Pkcs.`<br/>`UseInsecureHashAlgorithms`|判斷某些 SignedCMS 作業的預設值為 SHA1 或 SHA256。<br>由於 SHA1 的衝突問題，Microsoft 建議使用 SHA256。|.NET Framework 4.7.1|
|`Switch.System.Security.Cryptography.X509Certificates.`<br/>`ECDsaCertificateExtensions.UseLegacyPublicKeyReader`|控制方法是否 <xref:System.Security.Cryptography.X509Certificates.ECDsaCertificateExtensions.GetECDsaPublicKey%2A?displayProperty=nameWithType> 正確地處理作業系統所支援的所有命名曲線（ `false` ），或還原成舊版行為。|.NET Framework 4.8|
|`Switch.System.Security.Cryptography.Xml.`<br/>`UseInsecureHashAlgorithms`|判斷某些 SignedXML 作業的預設值為 SHA1 或 SHA256。<br>由於 SHA1 的衝突問題，Microsoft 建議使用 SHA256。|.NET Framework 4.7.1|
|`Switch.System.ServiceModel.`<br/>`AllowUnsignedToHeader`|判斷 `TransportWithMessageCredential` 安全性模式是否允許具有不帶正負號 "to" 標頭的訊息。 這是選擇性參數。 如需詳細資訊，請參閱[.NET Framework 4.6.1 中的執行時間變更](../../../migration-guide/runtime/4.5.2-4.6.1.md#windows-communication-foundation-wcf)。|.NET Framework 4.6.1|
|`Switch.System.ServiceModel.`<br/>`DisableAddressHeaderCollectionValidation`>|控制 <xref:System.ServiceModel.Channels.AddressHeaderCollection.%23ctor(System.Collections.Generic.IEnumerable{System.ServiceModel.Channels.AddressHeader})> <xref:System.ArgumentException> 如果其中一個專案為，則此函式是否擲回 `null` 。|.NET Framework 4.7.1|
|`Switch.System.ServiceModel.`<br />`DisableCngCertificates`|判斷嘗試搭配 CSG 金鑰儲存提供者使用 X509 憑證是否擲回例外狀況。 如需詳細資訊，請參閱[WCF 傳輸安全性支援使用 CNG 儲存的憑證](../../../migration-guide/retargeting/4.6.1-4.6.2.md#wcf-transport-security-supports-certificates-stored-using-cng)。|.NET Framework 4.6.1|
|`Switch.System.ServiceModel.`<br/>`DisableExplicitConnectionCloseHeader`|搭配自我裝載服務使用 HTTP 傳輸時，將此值設定為， `true` 會讓 WCF 忽略應用程式將 `Connection: close` 標頭新增至要求的回應標頭。 將此值設定為可 `false` 將 `Connection: close` 標頭新增至回應標頭，這會導致在傳送回應之後關閉要求通訊端。|.NET Framework 4.6|
|`Switch.System.ServiceModel.`<br/>`DisableOperationContextAsyncFlow`|處理因為將重新進入服務的實例限制為一次執行單一執行緒而產生的鎖死。|.NET Framework 4.6.2|
|`Switch.System.ServiceModel.`<br/>`DisableUsingServicePointManagerSecurityProtocols`|除了之外 `Switch.System.Net.DontEnableSchUseStrongCrypto` ，還會判斷 WCF 訊息安全性是否使用 tls 1.1 和 tls 1.2。|.NET Framework 4.7 |
|`Switch.System.ServiceModel.`<br/>`DontEnableSystemDefaultTlsVersions`|的值會 `false` 設定預設值，以允許作業系統選擇通訊協定。 值會 `true` 將預設值設為最高可用的通訊協定。 （也適用于舊版架構的服務分支）|.NET Framework 4.7.1|
|`Switch.System.ServiceModel.`<br/>`UseSha1InMsmqEncryptionAlgorithm`|判斷 WCF 中 MSMQ 訊息的預設訊息簽署演算法是 SHA1 或 SHA256。<br>由於 SHA1 的衝突問題，Microsoft 建議使用 SHA256。|.NET Framework 4.7.1|
|`Switch.System.ServiceModel.`<br/>`UseSha1InPipeConnectionGetHashAlgorithm`|控制 WCF 是否使用 SHA1 或 SHA256 雜湊來產生具名管道的隨機名稱。<br>由於 SHA1 的衝突問題，Microsoft 建議使用 SHA256。|.NET Framework 4.7.1|
|`Switch.System.ServiceModel.Internals`<br/>`IncludeNullExceptionMessageInETWTrace`|控制是否要在例外狀況訊息為 null 時擲回[NullReferenceException](xref:System.NullReferenceException) 。|.NET Framework 4.7|
|`Switch.System.ServiceProcess.`<br/>`DontThrowExceptionsOnStart`|控制在服務啟動時擲回的例外狀況是否會傳播到方法的呼叫端 <xref:System.ServiceProcess.ServiceBase.Run%2A?displayProperty=nameWithType> 。|.NET Framework 4.7.1|
|`Switch.System.Threading.UseNetCoreTimer`|控制 <xref:System.Threading.Timer> 實例是否利用高擴充環境的效能改進。 如果為 `true` ，則會啟用效能改善; 如果為 `false` （預設值），則會停用。|.NET Framework 4.8|
|`Switch.System.Uri.`<br/>`DontEnableStrictRFC3986ReservedCharacterSets`|判斷有時已解碼的特定百分比編碼字元，現在是否一致地保持編碼。 如果為 `true` ，則會解碼，否則 `false` 為。|.NET Framework 4.7.2|
|`Switch.System.Uri.`<br/>`DontKeepUnicodeBidiFormattingCharacters`|決定 Uri 中 Unicode 雙向字元的處理方式。 `true`若要從 Uri 中去除它們，會 `false` 保留並對其進行百分比編碼。|.NET Framework 4.7.2|
|`Switch.System.Windows.Controls.Grid.`<br/>`StarDefinitionsCanExceedAvailableSpace` |判斷 Windows Presentation Foundation 是否套用舊的演算法（ `true` ） `false` ，或在配置空間給-columns 的新演算法（） \* 。 如需詳細資訊，請參閱[風險降低︰方格控制項對 Star-columns 的空間配置](../../../migration-guide/retargeting/4.6.2-4.7.md#wpf-grid-allocation-of-space-to-star-columns)。 |.NET Framework 4.7 |
|`Switch.System.Windows.Controls.TabControl.`<br/>`SelectionPropertiesCanLagBehindSelectionChangedEvent`|控制選取器或索引標籤控制項是否一律會在引發選取範圍變更事件之前更新其選取值屬性的值。|.NET Framework 4.7.1|
|`Switch.System.Windows.Controls.Text.`<br/>`UseAdornerForTextboxSelectionRendering`|判斷非以裝飾項為基礎的選取範圍呈現是否適用于 <xref:System.Windows.Controls.TextBox> 和 <xref:System.Windows.Controls.PasswordBox> 控制項，以防止 pixels occluded `false` 的文字（），或文字是否只在裝飾項層（）中轉譯 `true` 。|.NET Framework 4.7.2|
|`Switch.System.Windows.Data.Binding.`<br/>`IListIndexerHidesCustomIndexer`|控制類別是否使用了不正確（ `true` ）或正確（）的自訂 IList 索引子 `false` <xref:System.Windows.Data.Binding?displayProperty=nameWithType> 。|.NET Framework 4.8|
|`Switch.System.Windows.DoNotScaleForDpiChanges`|決定是否要在每個系統（的值 `false` ）或每個監視器（的值）上發生 DPI 變更 `true` 。|.NET Framework 4.6.2|
|`Switch.System.Windows.`<br/>`DoNotUsePresentationDpiCapabilityTier2OrGreater`|控制 <xref:System.Windows.Interop.HwndHost?displayProperty=nameWithType> 當 WPF 在每個監視器感知模式下執行時，是否要改善中的控制項大小，已停用（ `true` ）或啟用（ `false` ）。|.NET Framework 4.8|
|`Switch.System.Windows.Forms.`<br/>`DomainUpDown.UseLegacyScrolling`|決定開發人員是否需要 <xref:System.Windows.Forms.DomainUpDown.UpButton?displayProperty=nameWithType> 在有控制項文字時，特別處理該動作。 `true`若要處理 <xref:System.Windows.Forms.DomainUpDown.UpButton> 動作，則 `false` 為 <xref:System.Windows.Forms.DomainUpDown.UpButton?displayProperty=nameWithType> ，讓和 <xref:System.Windows.Forms.DomainUpDown.DownButton?displayProperty=nameWithType> 動作正確地同步。|.NET Framework 4.7.2|
|`Switch.System.Windows.Forms.`<br />`DontSupportReentrantFilterMessage`|退出宣告程式碼，可讓自訂的 <xref:System.Windows.Forms.IMessageFilter.PreFilterMessage%2A?displayProperty=nameWithType> 執行安全地篩選訊息，而不會在 <xref:System.Windows.Forms.Application.FilterMessage%2A?displayProperty=nameWithType> 呼叫方法時擲回例外狀況。 如需詳細資訊，請參閱[風險降低：自訂 IMessageFilter.PreFilterMessage 實作](../../../migration-guide/mitigation-custom-imessagefilter-prefiltermessage-implementations.md)。|.NET Framework 4.6.1|
|`Switch.System.Windows.Forms.`<br/>`UseLegacyContextMenuStripSourceControlValue`|判斷 <xref:System.Windows.Forms.ContextMenuStrip.SourceControl?displayProperty=nameWithType> 當使用者從嵌套控制項開啟功能表時，屬性是否會傳回原始檔控制 <xref:System.Windows.Forms.ToolStripMenuItem> 。 `true`要傳回的 `null` 舊版行為，則表示傳回 `false` 原始檔控制。|.NET Framework 4.7.2|
|`Switch.System.Windows.Forms.UseLegacyToolTipDisplay`|控制工具提示調用支援是否停用（ `true` ）或啟用（ `false` ）。 啟用工具提示調用支援也需要由、和定義的舊版存取範圍功能， `Switch.UseLegacyAccessibilityFeatures` `Switch.UseLegacyAccessibilityFeatures.2` 而且 `Switch.UseLegacyAccessibilityFeatures.3` 全部都是停用的（設定為 `false` ）。|.NET Framework 4.8|
|`Switch.System.Windows.Input.Stylus.`<br/>`EnablePointerSupport`|決定是否 `WM_POINTER` 在 WPF 應用程式中啟用選擇性的觸控/手寫筆堆疊。 如需詳細資訊，請參閱[緩和：以指標為基礎的觸控和手寫筆支援](../../../migration-guide/mitigation-pointer-based-touch-and-stylus-support.md)|.NET Framework 4.7|
|`Switch.System.Windows.Markup.`<br/>`DoNotUseSha256ForMarkupCompilerChecksumAlgorithm`|判斷用於總和檢查碼的預設雜湊演算法是 SHA256 （ `false` ）或 SHA1 （ `true` ）。<br>由於 SHA1 的衝突問題，Microsoft 建議使用 SHA256。|.NET Framework 4.7.2|
|`Switch.System.Windows.Media.ImageSourceConverter.`<br/>`OverrideExceptionWithNullReferenceException`|控制是否擲回舊版[NullReferenceException](xref:System.NullReferenceException) ，而不是例外狀況，更明確地指出例外狀況的原因（例如[DirectoryNotFoundException](xref:System.IO.DirectoryNotFoundException)或[FileNotFoundException](xref:System.IO.FileNotFoundException)）。 其目的是要讓相依于處理[NullReferenceException](xref:System.NullReferenceException)的程式碼使用。 | .NET Framework 4.7 |
|`Switch.System.Workflow.ComponentModel.`<br/>`UseLegacyHashForXomlFileChecksum`|控制工作流程專案組建中 XOML 檔的總和檢查碼雜湊是否使用 MD5 演算法（ `true` ），或是否使用在 .NET Framework 4.8 中引進為預設值的 SHA256 演算法。<br>由於 MD5 的衝突問題，Microsoft 建議使用 SHA256。|.NET Framework 4.8|
|`Switch.System.Workflow.Runtime.`<br/>`UseLegacyHashForSqlTrackingCacheKey`|控制 SqlTrackingService 的總和檢查碼雜湊是否針對快取的字串使用 MD5 演算法（ `true` ），或是否使用在 .NET Framework 4.8 中引進為預設值的 SHA256 演算法。<br>由於 MD5 的衝突問題，Microsoft 建議使用 SHA256。|.NET Framework 4.8|
|`Switch.System.Workflow.Runtime.`<br/>`UseLegacyHashForWorkflowDefinitionDispenserCacheKey`|控制工作流程執行時間的總和檢查碼雜湊是否針對快取 `true` 的工作流程定義使用 MD5 演算法（），或是否使用在 .NET Framework 4.8 中引進為預設值的 SHA256 演算法。<br>由於 MD5 的衝突問題，Microsoft 建議使用 SHA256。|.NET Framework 4.8|
|`Switch.UseLegacyAccessibilityFeatures`|控制是否啟用或停用從 .NET Framework 4.7.1 開始提供的協助工具功能。 | .NET Framework 4.7.1 |
|`Switch.UseLegacyAccessibilityFeatures.2`|控制是否啟用（）或停用 .NET Framework 4.7.2 中可用的協助工具功能（ `false` `true` ）。 如果 `true` 為，則 `Switch.UseLegacyAccessibilityFeatures` 也必須是， `true` 才能啟用 .NET Framework 4.7.1 協助工具功能。|.NET Framework 4.7.2|
|`Switch.UseLegacyAccessibilityFeatures.3`|控制是否啟用（ `false` ）或停用（） .NET Framework 4.8 中引進的協助工具功能 `true` 。 如果 `true` 、 `Switch.UseLegacyAccessibilityFeatures` 和 `Switch.UseLegacyAccessibilityFeatures.2` 也必須是 `true` 。|.NET Framework 4.8|
|`Switch.UseLegacyToolTipDisplay`|控制當使用者將滑鼠游標停留在 WPF 控制項上時，是否要顯示工具提示（ `true` ），或者是否要在鍵盤焦點和透過鍵盤快速鍵（ `false` 預設行為）顯示。 對於在 .NET Framework 4.8 上執行但以舊版 .NET Framework 為目標的應用程式，同時啟用鍵盤焦點和快速鍵支援時 `Switch.UseLegacyAccessibilityFeatures` ， `Switch.UseLegacyAccessibilityFeatures.2` 會要求、和 `Switch.UseLegacyAccessibilityFeatures.3` 全都設定為 `false` 。|.NET Framework 4.8|
|`Switch.System.Xml.`<br />`IgnoreEmptyKeySequences`|控制 XSD 架構驗證是否忽略複合索引鍵中的空白索引鍵序列。 如需詳細資訊，請參閱[風險降低： XML 架構驗證](../../../migration-guide/mitigation-xml-schema-validation.md)。|.NET Framework 4.6|

> [!NOTE]
> 除了將專案新增 `AppContextSwitchOverrides` 至應用程式佈建檔，您也可以呼叫 `static` （在 c # 中）或 `Shared` （在 Visual Basic）方法，以程式設計方式設定參數 <xref:System.AppContext.SetSwitch%2A?displayProperty=nameWithType> 。

 程式庫開發人員也可以定義自訂參數，以允許呼叫者選擇不要在較新版本的程式庫中引進變更的功能。 如需詳細資訊，請參閱 <xref:System.AppContext> 類別。

## <a name="switches-in-aspnet-apps"></a>ASP.NET apps 中的交換器

您可以將專案新增至 web.config 檔案的區段，以將 ASP.NET 應用程式設定為使用相容性設定 [\<Add>](../appsettings/add-element-for-appsettings.md) [\<appSettings>](../appsettings/index.md) 。

下列範例會使用 `<add>` 元素，將兩個設定加入 web.config 檔案的 `<appSettings>` 區段中：

```xml
<appSettings>
  <add key="AppContext.SetSwitch:Switch.System.Globalization.NoAsyncCurrentCulture" value="true" />
  <add key="AppContext.SetSwitch:Switch.System.Uri.DontEnableStrictRFC3986ReservedCharacterSets" value="true" />
</appSettings>
```

## <a name="example"></a>範例

 下列範例 `AppContextSwitchOverrides` 會使用元素來定義單一應用程式相容性參數，以 `Switch.System.Globalization.NoAsyncCurrentCulture` 防止文化特性在非同步方法呼叫中跨執行緒流動。

```xml
<configuration>
   <runtime>
      <AppContextSwitchOverrides value="Switch.System.Globalization.NoAsyncCurrentCulture=true" />
   </runtime>
</configuration>
```

 下列範例會使用 `AppContextSwitchOverrides` 元素來定義兩個應用程式相容性參數 `Switch.System.Globalization.NoAsyncCurrentCulture` 和 `Switch.System.IO.BlockLongPaths` 。 分號會分隔兩個名稱/值組。

```xml
<configuration>
    <runtime>
       <AppContextSwitchOverrides
          value="Switch.System.Globalization.NoAsyncCurrentCulture=true;Switch.System.IO.BlockLongPaths=true" />
    </runtime>
</configuration>
```

## <a name="see-also"></a>另請參閱

- [緩和 .NET Framework 4.6 和更新版本中的新行為](../../../migration-guide/mitigations.md)
- <xref:System.AppContext?displayProperty=nameWithType>
- [\<runtime>元素](runtime-element.md)
- [\<configuration>元素](../configuration-element.md)
