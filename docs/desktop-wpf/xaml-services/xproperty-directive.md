---
title: x:Property 指示詞
ms.date: 03/30/2017
ms.assetid: 618555a8-c893-455c-810f-ac54cd24ef10
ms.openlocfilehash: d4294b39ff262198f8082863d23eb6f4edbc7054
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90549297"
---
# <a name="xproperty-directive"></a>x:Property 指示詞

在標記中宣告 XAML 屬性。

## <a name="xaml-object-element-usage"></a>XAML 物件項目用法

```xaml
<object x:Class="className">
  <x:Members>
    <x:Property Name="propertyName" Type="propertyType"/>
    additionalProperties
  </x:Members>
</object>
```

## <a name="xaml-values"></a>XAML 值

|||
|-|-|
|`className`|XAML 生產的支援類別或部分類別名稱。|
|`propertyName`|正在定義之屬性的成員名稱。|
|`propertyType`|指定這個屬性類型的類型名稱 (或其他特定架構的字串形式)。|

## <a name="remarks"></a>備註

在 .NET XAML 服務的執行中， `x:Property` 沒有直接的類型支援，但受到 <xref:System.Windows.Markup.PropertyDefinition> 類別的支援。 在 XAML 節點資料流中，`x:Property` 項目會以 XAML 語言 XAML 命名空間中名為 `Property` 的成員表示。 成員 `Property` 包含依標記宣告的屬性。

和的意義 `Name` `Type` 不是在 .Net XAML 服務層級指派。 它們會在初始 XAML 節點資料流中儲存為字串值，以便稍後依據特定架構可能加諸的規則解譯。 這個意義可能與 XAML 名稱和 XAML 類型的意義一致，或可能只是在支援類型系統中有效，視實作而定。

若要支援實際使用 `x:Members` 做為在標記中指定成員定義的方法，這些成員必須與可修改的類別相關聯。 預期的模型是 `x:Members` 做為可指定 `x:Class` 之類型成員的形式存在。 不過，.NET XAML 服務層級不支援關聯類型和成員或產生動態成員定義的機制。 這會保留給具有支援 XAML 成員定義之應用程式模型的個別架構。 通常需要 MSBUILD 建置動作以標記編譯 XAML，然後與程式碼後置整合，或是從 XAML 產生純組件，才能支援該功能。

## <a name="xproperty-for-windows-workflow-foundation"></a>Windows Workflow Foundation 的 x:Property

針對 Windows Workflow Foundation，`x:Property` 會定義完全以 XAML 撰寫之自訂活動的成員，或程式碼後置活動設計工具的 XAML 定義動態成員。 `x:Class` 也必須在 XAML 生產的根項目上指定。 這不是 .NET XAML 服務層級的需求，但在 XAML 生產是由支援自訂活動和一般 Windows Workflow Foundation XAML 的 MSBUILD 組建動作載入時，就會成為需求。 Windows Workflow Foundation 不會使用純 XAML 型別名稱做為其預期的 `x:Property` `Type` 屬性值，而是使用此處未記載的慣例。 如需詳細資訊，請參閱 [建立 DynamicActivity](/previous-versions/dotnet/netframework-4.0/dd807392(v=vs.100))。
