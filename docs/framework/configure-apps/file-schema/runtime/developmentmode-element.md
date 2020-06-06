---
title: <developmentMode> 項目
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/developmentMode
- http://schemas.microsoft.com/.NetConfiguration/v2.0#developmentMode
helpviewer_keywords:
- developmentMode element
- container tags, <developmentMode> element
- <developmentMode> element
ms.assetid: 60e79a8c-415a-497d-be29-b9d0fd9bdee3
ms.openlocfilehash: 4a062da31740edb8f0c7a4f4db8b09800c687587
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "73117624"
---
# <a name="developmentmode-element"></a>\<developmentMode> 項目
指定執行階段是否要在 DEVPATH 環境變數所指定的目錄中搜尋組件。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<developmentMode>**  
  
## <a name="syntax"></a>語法  
  
```xml  
<developmentMode developerInstallation="true | false"/>  
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  
 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|**developerInstallation**|指定執行階段是否要在 DEVPATH 環境變數所指定的目錄中搜尋組件。|  
  
## <a name="developerinstallation-attribute"></a>developerInstallation 屬性  
  
|值|描述|  
|-----------|-----------------|  
|**true**|在 DEVPATH 環境變數所指定的目錄中搜尋元件。|  
|**false**|不會在 DEVPATH 環境變數所指定的目錄中搜尋元件。 這是預設值。|  
  
### <a name="child-elements"></a>子元素  
 無。  
  
### <a name="parent-elements"></a>父項目  
  
|元素|描述|  
|-------------|-----------------|  
|`configuration`|通用語言執行平台和 .NET Framework 應用程式所使用之每個組態檔中的根項目。|  
|`runtime`|包含有關組件繫結和記憶體回收的資訊。|  
  
## <a name="remarks"></a>備註  
 請只在開發階段使用此設定。 執行時間不會檢查在 DEVPATH 中找到的強式名稱元件上的版本。 它只會使用所找到的第一個元件。  
  
## <a name="example"></a>範例  
 下列範例顯示如何讓執行時間在 DEVPATH 環境變數所指定的目錄中搜尋元件。  
  
```xml  
<configuration>  
   <runtime>  
      <developmentMode developerInstallation="true"/>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>另請參閱

- [執行時間設定架構](index.md)
- [設定檔架構](../index.md)
- [作法：使用 DEVPATH 找出組件](../../how-to-locate-assemblies-by-using-devpath.md)
