---
title: <appSettings> 的 <clear> 項目
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/appSettings/clear
helpviewer_keywords:
- clear Element
- <clear> Element
ms.assetid: 6d18c7be-27db-438b-8fb5-765d396b0b7b
ms.openlocfilehash: 266d32ccb8b322f0472e0f552f9c0fc877c9a78e
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "77214786"
---
# <a name="clear-element-for-appsettings"></a>\<appSettings> 的 \<clear> 項目

清除自訂應用程式設定。

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<appSettings>**](appsettings-element-for-configuration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<clear>**

## <a name="syntax"></a>語法

```xml
<appSettings>
  <clear />
</appSettings>
```

## <a name="attributes"></a>屬性

無

## <a name="parent-element"></a>父元素

|     | 描述 |
| --- | ----------- |
| [**\<appSettings>**](appsettings-element-for-configuration.md) | 包含自訂應用程式設定，例如檔案路徑、XML Web Service Url，或任何其他自訂應用程式設定資訊。 |

## <a name="child-elements"></a>子元素

None

## <a name="example"></a>範例

下列範例顯示如何清除自訂設定：

```xml
<appSettings>
  <clear />
</appSettings>
```

## <a name="see-also"></a>另請參閱

- [.NET Framework 的設定檔架構](../index.md)
