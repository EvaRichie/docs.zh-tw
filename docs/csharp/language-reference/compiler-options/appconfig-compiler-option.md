---
description: -appconfig (C# 編譯器選項)
title: -appconfig (C# 編譯器選項)
ms.date: 07/20/2015
f1_keywords:
- /appconfig
helpviewer_keywords:
- /appconfig compiler option [C#]
- -appconfig compiler option [C#]
- appconfig compiler option [C#]
ms.assetid: 1cdbcbcc-7813-4010-b5b8-e67c107c5a98
ms.openlocfilehash: 8ee481851dc02bed5eb0a7c26fa8893e52d54a9f
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91157963"
---
# <a name="-appconfig-c-compiler-options"></a>-appconfig (C# 編譯器選項)

**-appconfig** 編譯器選項可讓 C# 應用程式將組件應用程式組態檔 (app.config) 的位置指定到組件繫結時間的通用語言執行平台 (CLR)。  
  
## <a name="syntax"></a>語法  
  
```console  
-appconfig:file  
```  
  
## <a name="arguments"></a>引數  

 `file`  
 必要。 包含組件繫結設定的應用程式組態檔。  
  
## <a name="remarks"></a>備註  

 **-appconfig** 的其中一種用法就是進階案例；在此案例中，組件必須同時參考特定參考組件的 .NET Framework 版本以及 .NET Framework for Silverlight 版本。 例如，以 Windows Presentation Foundation (WPF) 撰寫的 XAML 設計工具，可能必須同時參考 WPF Desktop (設計工具的使用者介面) 和 Silverlight 所附的 WPF 子集。 相同的設計工具組件必須存取這兩個組件。 根據預設，不同的參考會導致編譯器錯誤，因為組件繫結關係會將兩個組件視為對等項目。  
  
 **-appconfig** 編譯器選項可讓您使用 `<supportPortability>` 標記指定停用預設行為的 app.config 檔案位置，如下列範例所示。  
  
 `<supportPortability PKT="7cec85d7bea7798e" enable="false"/>`  
  
 編譯器會將檔案位置傳遞至 CLR 的組件繫結關係邏輯。  
  
> [!NOTE]
> 如果使用 Microsoft Build Engine (MSBuild) 來建置應用程式，您可以將屬性標記新增至 .csproj 檔案，以設定 **-appconfig** 編譯器選項。 若要使用專案中已設定的 app.config 檔案，請將屬性標記 `<UseAppConfigForCompiler>` 新增至 .csproj 檔案，並將其值設定為 `true`。 若要指定不同的 app.config 檔案，請新增屬性標記 `<AppConfigForCompiler>` 並將其值設定為檔案位置。  
  
## <a name="example"></a>範例  

 下例示範的 app.config 檔案，可讓應用程式同時參考存在於兩個實作中之任何 .NET Framework 組件的 .NET Framework 實作和 .NET Framework for Silverlight 實作。 **-appconfig** 編譯器選項會指定此 app.config 檔案的位置。  
  
```xml  
<configuration>  
      <runtime>  
      <assemblyBinding>  
            <supportPortability PKT="7cec85d7bea7798e" enable="false"/>  
            <supportPortability PKT="31bf3856ad364e35" enable="false"/>  
      </assemblyBinding>  
      </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>另請參閱

- [\<supportPortability> 元素](../../../framework/configure-apps/file-schema/runtime/supportportability-element.md)
- [依字母順序列出 C# 編譯器選項](./listed-alphabetically.md)
