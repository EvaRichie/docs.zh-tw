---
title: <supportedRuntime>configuration 元素-.NET
ms.date: 04/02/2019
ms.custom: updateeachrelease
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#supportedRuntime
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/startup/supportedRuntime
helpviewer_keywords:
- supportedRuntime element
- <supportedRuntime> element
ms.assetid: 1ae16e23-afbe-4de4-b413-bc457f37b69f
ms.openlocfilehash: ecbe73593e5b8b87909499f6fff7e865e29b1ec8
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82796037"
---
# <a name="supportedruntime-element"></a>\<Supportedruntime>> 元素

指定應用程式支援的 common language runtime 版本和（選擇性） .NET Framework 版本。  

[\<設定>](../configuration-element.md)  
&nbsp;&nbsp;[\<啟動>](startup-element.md)  
&nbsp;&nbsp;&nbsp;&nbsp;**\<Supportedruntime>>**  

## <a name="syntax"></a>語法

```xml
<supportedRuntime version="runtime version" sku="sku id"/>
```

## <a name="attributes"></a>屬性

|屬性|說明|
|---------------|-----------------|
|**version**|選擇性屬性。<br /><br /> 字串值，用於指定這個應用程式支援的通用語言執行平台 (CLR) 版本。 如需`version`屬性的有效值，請參閱「[執行階段版本」值](#version)一節。 **注意：** 透過 .NET Framework 3.5，「*執行階段版本*」值會採用*主要*格式。*次要*。*build*。 從 .NET Framework 4 開始，只需要主要和次要版本號碼（也就是 "v4.0"，而不是 "v 4.0.30319"）。 建議使用較短的字串。|
|**限量**|選擇性屬性。<br /><br /> 字串值，指定庫存單位 (SKU)，進而指定哪些應用程式支援的.NET Framework 版本。<br /><br /> 從 .NET Framework 4.0 開始，建議使用 `sku` 屬性。  該屬性存在時，會指出應用程式作為目標的 .NET Framework 版本。<br /><br /> 如需 sku 屬性的有效值，請參閱「 [sku 識別碼」值](#sku)一節。|

## <a name="remarks"></a>備註

如果** \<supportedruntime>>** 元素不存在於應用程式佈建檔中，則會使用用來建立應用程式的執行階段版本。

Supportedruntime>>元素應該供使用1.1 版或更新版本的執行時間所建立的所有應用程式使用。 ** \< ** 為了僅支援1.0 版執行時間所建立的應用程式，必須使用[ \<r q>](requiredruntime-element.md)元素。

> [!NOTE]
> 如果您使用[CorBindToRuntimeByCfg](../../../unmanaged-api/hosting/corbindtoruntimebycfg-function.md)函數來指定設定檔，您必須針對所有版本的`<requiredRuntime>`執行時間使用元素。 當`<supportedRuntime>`您使用[CorBindToRuntimeByCfg](../../../unmanaged-api/hosting/corbindtoruntimebycfg-function.md)時，會忽略元素。  
  
針對所支援執行階段為 .NET Framework 1.1 到 3.5 版本的應用程式，當支援多個執行階段版本時，第一個項目應該指定最常用的執行階段版本，而最後一個項目則指定最少用的版本。 針對支援 .NET Framework 4.0 或更新版本的應用程式， `version`屬性會指出 CLR 版本，這對 .NET Framework 4 和更新版本而言是通用的，而屬性`sku`則表示應用程式以為目標的單一 .NET Framework 版本。

如果具有`sku`屬性的** \<supportedruntime>>** 專案出現在設定檔中，而已安裝的 .NET Framework 版本低於指定的支援版本，則應用程式無法執行，而是會顯示要求安裝支援版本的訊息。 否則，應用程式會嘗試在任何已安裝的版本上執行，但如果它與該版本不完全相容，則可能會發生非預期的行為。 （如需 .NET Framework 版本之間的相容性差異，請參閱[.NET Framework 中的應用程式相容性](https://docs.microsoft.com/dotnet/framework/migration-guide/application-compatibility)）。因此，我們建議您在應用程式佈建檔中包含這個元素，以便更輕鬆地進行錯誤診斷。 （當建立新專案時，Visual Studio 自動產生的設定檔案已包含此檔案）。
  
> [!NOTE]
> 如果您的應用程式使用舊版啟用路徑，例如[CorBindToRuntimeEx](../../../unmanaged-api/hosting/corbindtoruntimeex-function.md)函式，而您想要讓這些路徑啟動 CLR 的第4版，而不是舊版，或如果您的應用程式是以 .NET Framework 4 建立，但相依于使用舊版 .NET Framework 所建立的混合模式元件，則在支援的執行時間清單中指定 .NET Framework 4 是不夠的。 此外，您必須在設定檔中的[ \<startup> 元素](startup-element.md)中，將`useLegacyV2RuntimeActivationPolicy`屬性設定為`true`。 不過，將此屬性設定`true`為，表示使用舊版 .NET Framework 建立的所有元件都是使用 .NET Framework 4 來執行，而不是以建立它們的執行時間來執行。

建議您使用應用程式能夠執行的所有 .NET Framework 版本進行應用程式測試。

<a name="version"></a>
## <a name="runtime-version-values"></a>「執行階段版本」值
`runtime`屬性會指定給定應用程式所需的 Common Language RUNTIME （CLR）版本。 請注意，所有 .NET Framework v4. x 版本都會`v4.0`指定 CLR。 下表列出`version`屬性的*執行階段版本*值的有效值。

|.NET Framework 版本|`version` 屬性|
|----------------------------|-------------------------|
|1.0|"v1.0.3705"|
|1.1|"v1.1.4322"|
|2.0|"v2.0.50727"|
|3.0|"v2.0.50727"|
|3.5|"v2.0.50727"|
|4.0-4。8|"v4.0"|

## <a name="sku-id-values"></a><a name="sku"></a>「sku 識別碼」值

`sku`屬性會使用目標 framework 名字標記（TFM）來指出應用程式以其為目標且需要執行的 .NET Framework 版本。 下表列出`sku`屬性所支援的有效值，從 .NET Framework 4 開始。

|.NET Framework 版本|`sku` 屬性|
|----------------------------|---------------------|
|4.0|".NETFramework,Version=v4.0"|
|4.0，Client Profile|".NETFramework,Version=v4.0,Profile=Client"|
|4.0，平台更新 1|"..Netframework，Version = v 4.0.1 "|
|4.0，Client Profile，更新 1|"..Netframework，Version = v 4.0.1，Profile = Client "|
|4.0，平台更新 2|"..Netframework，Version = v 4.0.2 "|
|4.0，Client Profile，更新 2|"..Netframework，Version = v 4.0.2，Profile = Client "|
|4.0，平台更新 3|"..Netframework，Version = v 4.0.3 "|
|4.0，Client Profile，更新 3|"..Netframework，Version = v 4.0.3，Profile = Client "|
|4.5|".NETFramework,Version=v4.5"|
|4.5.1|".NETFramework,Version=v4.5.1"|
|4.5.2|".NETFramework,Version=v4.5.2"|
|4.6|".NETFramework,Version=v4.6"|
|4.6.1|".NETFramework,Version=v4.6.1"|
|4.6.2|"..Netframework，Version = v 4.6.2 "|
|4.7|"..Netframework，Version = 4.7 版」|
|4.7.1|"..Netframework，Version = v 4.7.1 "|
|4.7.2|"..Netframework，Version = v 4.7.2 "|
|4.8|"..Netframework，Version = v 4.8 "|

## <a name="example"></a>範例

下列範例將示範如何在設定檔中指定支援的執行階段版本。 設定檔指出應用程式以 .NET Framework 4.7 為目標。

```xml
<configuration>
   <startup>
      <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.7" />
   </startup>
</configuration>
```

## <a name="configuration-file"></a>組態檔

這個項目可以在應用程式組態檔中使用。

## <a name="see-also"></a>請參閱

- [啟動設定架構](index.md)
- [設定檔架構](../index.md)
- [同處理序並存執行](../../../deployment/in-process-side-by-side-execution.md)
