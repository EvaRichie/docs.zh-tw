---
title: <compiler> 項目
ms.date: 08/14/2018
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#compiler
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.codedom/compilers/compiler
helpviewer_keywords:
- compiler configuration elements, <compiler> element
- <compiler> element
- compiler configuration attributes
- compiler element
ms.assetid: 7a151659-b803-4c27-b5ce-1c4aa0d5a823
ms.openlocfilehash: 46676f25597f85596598d6f67c98930971cb0447
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "74088048"
---
# <a name="compiler-element"></a>\<compiler> 項目

指定語言提供者的編譯器組態屬性。

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.codedom>**](system-codedom-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<compilers>**](compilers-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<compiler>**

## <a name="syntax"></a>語法

```xml
<compiler
  language="languageName[;...;...]"
  extension="fileExtension[;...;...]"
  type="typeName, assemblyName"
  warningLevel="number"
  compilerOptions="option1 option2"
/>
```

## <a name="attributes-and-elements"></a>屬性和項目

下列章節說明屬性、子元素和父元素。

### <a name="attributes"></a>屬性

|屬性|描述|
|---------------|-----------------|
|`compilerOptions`|選擇性屬性。<br /><br /> 指定編譯的其他編譯器特定引數。 屬性的值 `compilerOptions` 通常會列在編譯器的編譯器選項主題中。|
|`extension`|必要屬性。<br /><br /> 提供語言提供者的原始程式檔所使用的檔案名副檔名清單（以分號分隔）。 例如，".cs"。|
|`language`|必要屬性。<br /><br /> 提供語言提供者所支援的語言名稱清單（以分號分隔）。 例如，"C#;cs;csharp"。|
|`type`|必要屬性。<br /><br /> 指定語言提供者的類型名稱，包括包含提供者實作為元件的名稱。 型別名稱必須符合[指定完整限定型別名稱](../../../reflection-and-codedom/specifying-fully-qualified-type-names.md)中所定義的需求。|
|`warningLevel`|選擇性屬性。<br /><br /> 指定預設的編譯器警告層級;決定語言提供者將編譯警告視為錯誤的層級。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|[\<providerOption>元素](provideroption-element.md)|指定語言提供者的編譯器版本屬性。|

### <a name="parent-elements"></a>父項目

|元素|描述|
|-------------|-----------------|
|[\<configuration>元素](../configuration-element.md)|通用語言執行平台和 .NET Framework 應用程式所使用之每個組態檔中的根項目。|
|[\<system.codedom>元素](system-codedom-element.md)|指定可用語言提供者的編譯器組態設定。|
|[\<compilers>元素](compilers-element.md)|編譯器設定元素的容器;包含零個或多個 `<compiler>` 元素。|

## <a name="remarks"></a>備註

每個 `<compiler>` 元素都會指定特定語言提供者的編譯器設定屬性。 提供者會擴充 <xref:System.CodeDom.Compiler.CodeDomProvider?displayProperty=nameWithType> 特定語言的類別; 元素會 `<compiler>` 定義語言提供者的編譯器和程式碼產生器設定。

.NET Framework 會在電腦組態檔 (Machine.config) 中定義初始編譯器設定。 開發人員和編譯器廠商可以為新的 <xref:System.CodeDom.Compiler.CodeDomProvider> 實作新增組態設定。 使用 <xref:System.CodeDom.Compiler.CodeDomProvider.GetAllCompilerInfo%2A?displayProperty=nameWithType> 方法，以程式設計方式列舉電腦上的語言提供者和編譯器組態設定。

應用程式或 Web 設定檔中的編譯器元素可以補充或覆寫電腦設定檔中的設定。 如果針對相同的語言名稱或相同的副檔名設定了一個以上的提供者，則最後一個比對設定會覆寫任何先前針對該語言名稱或副檔名所設定的提供者。

## <a name="configuration-file"></a>組態檔

此元素可以在電腦設定檔和應用程式佈建檔中使用。

## <a name="example"></a>範例

下列範例說明典型的編譯器設定元素：

```xml
<configuration>
  <system.codedom>
    <compilers>
      <!-- zero or more compiler elements -->
      <compiler
        language="c#;cs;csharp"
        extension=".cs"
        type="Microsoft.CSharp.CSharpCodeProvider, System,
          Version=2.0.3600.0, Culture=neutral,
          PublicKeyToken=b77a5c561934e089"
        compilerOptions="/optimize"
        warningLevel="1" />
    </compilers>
  </system.codedom>
</configuration>
```

## <a name="see-also"></a>另請參閱

- <xref:System.CodeDom.Compiler.CompilerInfo>
- <xref:System.CodeDom.Compiler.CodeDomProvider>
- [設定檔架構](../index.md)
- [\<compilers>元素](compilers-element.md)
- [指定完整的類型名稱](../../../reflection-and-codedom/specifying-fully-qualified-type-names.md)
- [編譯之編譯器的 compiler 項目 (ASP.NET 設定結構描述)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/a15ebt6c(v=vs.100))
