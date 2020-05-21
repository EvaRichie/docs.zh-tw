---
ms.openlocfilehash: 43da6233b70927e7320874772976b9e93a0bd69f
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/20/2020
ms.locfileid: "83721533"
---
### <a name="jsonfactoryconvertercreateconverter-signature-changed"></a>JsonFactoryConverter. CreateConverter 簽章已變更

為了簡化類別的撰寫 <xref:System.Text.Json.Serialization.JsonConverterFactory> ，已將 <xref:System.Text.Json.Serialization.JsonConverterFactory.CreateConverter%2A> 方法設為公用，並提供類型的第二個引數 <xref:System.Text.Json.JsonSerializerOptions> 。

#### <a name="change-description"></a>變更描述

`CreateConverter`版本 3.0 Preview 8 之前 .Net Core 中方法的簽章為：

```csharp
namespace System.Text.Json.Serialization
{
    public abstract class JsonConverterFactory : JsonConverter
    {
        protected abstract JsonConverter CreateConverter(Type typeToConvert);
    }
}
```

在 .NET Core 3.0 Preview 8 和更新版本中，它是：

```csharp
namespace System.Text.Json.Serialization
{
    public abstract class JsonConverterFactory : JsonConverter
    {
        public abstract JsonConverter CreateConverter(Type typeToConvert, JsonSerializerOptions options);
    }
}
```

在此變更之前，很難撰寫密封的 factory 轉換器，因為沒有簡單的方法可以 <xref:System.Text.Json.Serialization.JsonConverter%601> 從它取得。 將 factory 方法設為公用，同時傳遞目前的 <xref:System.Text.Json.JsonSerializerOptions> 允許更具彈性的組合。

#### <a name="version-introduced"></a>引進的版本

3.0 Preview 8

#### <a name="recommended-action"></a>建議的動作

衍生類別需要更新並重新編譯。

#### <a name="affected-apis"></a>受影響的 API

- <xref:System.Text.Json.Serialization.JsonConverterFactory.CreateConverter(System.Type,System.Text.Json.JsonSerializerOptions)?displayProperty=nameWithType>

<!-- For tool use only

#### Affected APIs

- `M:System.Text.Json.Serialization.JsonConverterFactory.CreateConverter(System.Type,System.Text.Json.JsonSerializerOptions)`

-->
