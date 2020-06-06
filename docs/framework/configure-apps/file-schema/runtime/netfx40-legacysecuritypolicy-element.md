---
title: <NetFx40_LegacySecurityPolicy> 項目
ms.date: 03/30/2017
helpviewer_keywords:
- <NetFx40_LegacySecurityPolicy> element
- NetFx40_LegacySecurityPolicy element
ms.assetid: 07132b9c-4a72-4710-99d7-e702405e02d4
ms.openlocfilehash: d5192eb56bb8b640544bdc52a0bb9d8a5277efef
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "73116245"
---
# <a name="netfx40_legacysecuritypolicy-element"></a>\<NetFx40_LegacySecurityPolicy> 項目

指定執行階段是否使用舊版程式碼存取安全性 (CAS) 原則。

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<NetFx40_LegacySecurityPolicy>**  

## <a name="syntax"></a>語法

```xml
<NetFx40_LegacySecurityPolicy
   enabled="true|false"/>
```

## <a name="attributes-and-elements"></a>屬性和項目

下列章節說明屬性、子元素和父元素。

### <a name="attributes"></a>屬性

|屬性|描述|
|---------------|-----------------|
|`enabled`|必要屬性。<br /><br /> 指定執行時間是否使用舊版 CAS 原則。|

## <a name="enabled-attribute"></a>啟用屬性

|值|描述|
|-----------|-----------------|
|`false`|執行時間不會使用舊版的 CAS 原則。 此為預設值。|
|`true`|執行時間會使用舊版的 CAS 原則。|

### <a name="child-elements"></a>子元素

無。

### <a name="parent-elements"></a>父項目

|元素|描述|
|-------------|-----------------|
|`configuration`|通用語言執行平台和 .NET Framework 應用程式所使用之每個組態檔中的根項目。|
|`runtime`|包含有關執行階段初始化選項的資訊。|

## <a name="remarks"></a>備註

在 .NET Framework 版本3.5 和更早版本中，CAS 原則一律會生效。 在 .NET Framework 4 中，必須啟用 CAS 原則。

CAS 原則是特定版本。 存在於舊版 .NET Framework 中的自訂 CAS 原則必須在 .NET Framework 4 中 respecified。

將 `<NetFx40_LegacySecurityPolicy>` 元素套用至 .NET Framework 4 元件並不會影響[安全性透明](../../../misc/security-transparent-code.md)的程式碼; 透明度規則仍然適用。

> [!IMPORTANT]
> 套用 `<NetFx40_LegacySecurityPolicy>` 元素可能會對原[生映射產生器（ngen.exe）](../../../tools/ngen-exe-native-image-generator.md)所建立的原生映射元件（未安裝在[全域組件快取](../../../app-domains/gac.md)中）造成明顯的效能損失。 效能降低的原因是，當套用屬性時，執行時間無法將元件載入為原生映射，導致其載入為即時元件。

> [!NOTE]
> 如果您在 Visual Studio 專案的專案設定中指定早于 .NET Framework 4 的目標 .NET Framework 版本，將會啟用 CAS 原則，包括您為該版本指定的任何自訂 CAS 原則。 不過，您將無法使用新的 .NET Framework 4 種類型和成員。 您也可以使用[應用程式佈建檔](../../index.md)中 [啟動設定] [ \<supportedRuntime> 架構的專案，指定](../startup/supportedruntime-element.md)舊版的 .NET Framework。

> [!NOTE]
> 設定檔語法會區分大小寫。 您應該使用語法和範例小節中所提供的語法。

## <a name="configuration-file"></a>組態檔

這個元素只能用在應用程式佈建檔中。

## <a name="example"></a>範例

下列範例顯示如何為應用程式啟用舊版 CAS 原則。

```xml
<configuration>
   <runtime>
      <NetFx40_LegacySecurityPolicy enabled="true"/>
   </runtime>
</configuration>
```

## <a name="see-also"></a>另請參閱

- [執行時間設定架構](index.md)
- [設定檔架構](../index.md)
