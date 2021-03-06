---
title: 修剪選項
description: 瞭解如何控制獨立應用程式的修剪。
author: sbomer
ms.author: svbomer
ms.date: 08/25/2020
ms.openlocfilehash: e36aca3aadb6968f73a439ca985dc410d1bc88d8
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95704652"
---
# <a name="trimming-options"></a>修剪選項

下列 MSBuild 屬性和專案會影響已修剪的 [獨立部署](trim-self-contained.md)行為。 有些選項 `ILLink` 會提及，也就是執行修剪的基礎工具名稱。 如需基礎工具的詳細資訊，請參閱 [連結器檔](https://github.com/mono/linker/tree/master/docs)。

## <a name="enable-trimming"></a>啟用修剪

- `<PublishTrimmed>true</PublishTrimmed>`

   使用 SDK 所定義的預設設定，在發佈期間啟用修剪。

使用時 `Microsoft.NET.Sdk` ，會從 netcoreapp 執行時間套件執行架構元件的元件層級修剪。 應用程式程式碼和非架構程式庫不會被修剪。 其他 Sdk 可能會定義不同的預設值。

## <a name="trimming-granularity"></a>修剪細微性

下列資料細微性設定可控制如何捨棄未使用的 IL。 這可以設定為屬性，或做為 [個別元件](#trimmed-assemblies)上的中繼資料。

- `<TrimMode>copyused</TrimMode>`

   啟用元件層級的修剪，如果使用任何部分的元件，則會以靜態瞭解的方式) ，以保持整個元件的 (。

- `<TrimMode>link</TrimMode>`

    啟用成員層級修剪，以從類型中移除未使用的成員。

具有 `<IsTrimmable>true</IsTrimmable>` 中繼資料但沒有明確的元件 `TrimMode` 會使用全域 `TrimMode` 。 的預設值為 `TrimMode` `Microsoft.NET.Sdk` `copyused` 。

## <a name="trimmed-assemblies"></a>修剪的元件

發佈已修剪的應用程式時，SDK `ItemGroup` 會計算呼叫 `ManagedAssemblyToLink` ，以代表要處理的一組檔案進行修剪。 `ManagedAssemblyToLink` 可能有可控制每個元件之修剪行為的中繼資料。 若要設定此中繼資料，請建立在內建目標之前執行的目標 `PrepareForILLink` 。 下列範例顯示如何啟用的修剪 `MyAssembly` 。

```xml
<Target Name="ConfigureTrimming"
        BeforeTargets="PrepareForILLink">
  <ItemGroup>
    <ManagedAssemblyToLink Condition="'%(Filename)' == 'MyAssembly'">
      <IsTrimmable>true</IsTrimmable>
    </ManagedAssemblyToLink>
  </ItemGroup>
</Target>
```

請勿在中加入或移除專案 `ManagedAssemblyToLink` ，因為 SDK 會在發行期間計算此集合，並預期不會變更。 支援的中繼資料為：

- `<IsTrimmable>true</IsTrimmable>`

  控制是否修剪指定的元件。

- `<TrimMode>copyused</TrimMode>` 或 `<TrimMode>link</TrimMode>`

  控制這個元件的 [修剪資料細微性](#trimming-granularity) 。 這優先于全域 `TrimMode` 。 `TrimMode`元件上的設定暗示 `<IsTrimmable>true</IsTrimmable>` 。

## <a name="root-assemblies"></a>根元件

所有不具有的元件 `<IsTrimmable>true</IsTrimmable>` 都會被視為分析的根目錄，這表示會保留它們及其所有靜態瞭解的相依性。 其他元件可能會以名稱「根目錄」 (沒有 `.dll` 副檔名) ：

```xml
<ItemGroup>
  <TrimmerRootAssembly Include="MyAssembly" />
</ItemGroup>
```

## <a name="root-descriptors"></a>根描述元

另一種指定根以進行分析的方式，就是使用使用連結器 [描述元格式](https://github.com/mono/linker/blob/master/docs/data-formats.md#descriptor-format)的 XML 檔。 這可讓您指定根特定的成員，而不是整個元件。

```xml
<ItemGroup>
  <TrimmerRootDescriptor Include="MyRoots.xml" />
</ItemGroup>
```

例如， `MyRoots.xml` 可能是應用程式動態存取的特定方法的根：

```xml
<linker>
  <assembly fullname="MyAssembly">
    <type fullname="MyAssembly.MyClass">
      <method name="DynamicallyAccessedMethod" />
    </type>
  </assembly>
</linker>
```

## <a name="analysis-warnings"></a>分析警告

修剪將會移除無法以靜態方式連線的 IL。 使用反映的應用程式或其他建立動態相依性的模式，可能會藉由修剪來中斷。 若要對這類模式發出警告：

- `<SuppressTrimAnalysisWarnings>false</SuppressTrimAnalysisWarnings>`

    啟用 trim 分析警告。

這會包含整個應用程式的相關警告，包括您自己的程式碼、程式庫程式碼和架構程式碼。

## <a name="warning-versions"></a>警告版本

Trim 分析採用 [`AnalysisLevel`](../project-sdk/msbuild-props.md#analysislevel) 控制 SDK 之間分析警告版本的屬性。 另外還有另一個屬性，可控制個別的 trim 分析警告版本， (類似于 `WarningLevel` 編譯器) ：

- `<ILLinkWarningLevel>5</ILLinkWarningLevel>`

    只發出指定層級或更低的警告。 這可以 `9999` 包含所有警告版本。

## <a name="suppressing-warnings"></a>隱藏警告

您可以使用工具鏈所遵守的一般 MSBuild 屬性來隱藏個別的 [警告碼](https://github.com/mono/linker/blob/master/docs/error-codes.md#warning-codes) ，包括 `NoWarn` 、、 `WarningsAsErrors` `WarningsNotAsErrors` 和 `TreatWarningsAsErrors` 。 另外還有另一個選項，可個別控制 ILLink 警告錯誤行為：

- `<ILLinkTreatWarningsAsErrors>false</ILLinkTreatWarningsAsErrors>`

    請勿將 ILLink 警告視為錯誤。 這有助於避免在全域將編譯器警告視為錯誤時，將 trim 分析警告轉換成錯誤。

## <a name="removing-symbols"></a>移除符號

通常會修剪符號以符合修剪的元件。 您也可以移除所有符號：

- `<TrimmerRemoveSymbols>true</TrimmerRemoveSymbols>`

    從修剪的應用程式中移除符號，包括內嵌的 Pdb 和個別的 PDB 檔案。 這同時適用于應用程式程式碼和符號隨附的任何相依性。

SDK 也可以使用屬性來停用偵錯工具支援 `DebuggerSupport` 。 停用偵錯工具支援時，修剪會自動移除符號 (`TrimmerRemoveSymbols` 預設為 true) 。

## <a name="trimming-framework-library-features"></a>修剪架構程式庫功能

架構程式庫的數個功能區域隨附連結器指示詞，可讓您移除停用功能的程式碼。

- `<DebuggerSupport>false</DebuggerSupport>`

    移除可進行更佳的偵錯工具的程式碼。 這也會 [移除符號](#removing-symbols)。

- `<EnableUnsafeBinaryFormatterSerialization>false</EnableUnsafeBinaryFormatterSerialization>`

    移除 BinaryFormatter 序列化支援。 如需詳細資訊，請參閱 [BinaryFormatter 序列化方法已過時](../compatibility/core-libraries/5.0/binaryformatter-serialization-obsolete.md)。

- `<EnableUnsafeUTF7Encoding>false</EnableUnsafeUTF7Encoding>`

    移除不安全的 UTF-7 編碼程式碼。 如需詳細資訊，請參閱 [utf-7 程式碼路徑已淘汰](../compatibility/core-libraries/5.0/utf-7-code-paths-obsolete.md)。

- `<EventSourceSupport>false</EventSourceSupport>`

    移除 EventSource 相關的程式碼或邏輯。

- `<HttpActivityPropagationSupport>false</HttpActivityPropagationSupport>`

    移除與系統 .Net 的診斷支援相關的程式碼。

- `<InvariantGlobalization>true</InvariantGlobalization>`

    移除全球化的特定程式碼和資料。 如需詳細資訊，請參閱不 [變模式](../run-time-config/globalization.md#invariant-mode)。

- `<UseSystemResourceKeys>true</UseSystemResourceKeys>`

    去除元件的例外狀況訊息 `System.*` 。 從元件擲回例外狀況時 `System.*` ，訊息會是簡化的資源識別碼，而不是完整的訊息。

 這些屬性會造成相關的程式碼遭到修剪，也會透過 [>.runtimeconfig.json](../run-time-config/index.md) 檔停用功能。 如需這些屬性的詳細資訊，包括對應的 >.runtimeconfig.json 選項，請參閱 [功能參數](https://github.com/dotnet/runtime/blob/master/docs/workflow/trimming/feature-switches.md)。 某些 Sdk 可能會有這些屬性的預設值。
