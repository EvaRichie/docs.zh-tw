---
title: <xmlSerializer> 項目
description: <xmlSerializer>元素會指定是否要進行其他的 XmlSerializer 檢查。
ms.date: 03/30/2017
helpviewer_keywords:
- <xmlSerializer> element
- XML serialization, configuration
- xmlSerializer element
ms.assetid: d129d10c-3eb7-45d9-8098-5fa853825e47
ms.openlocfilehash: 68037959893ec307a896ea86d21e40a9d7aa824c
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/13/2020
ms.locfileid: "83380026"
---
# <a name="xmlserializer-element"></a>\<xmlSerializer> 元素
指定是否已完成 <xref:System.Xml.Serialization.XmlSerializer> 進度的其他檢查。  
  
 \<configuration>  
\<system.xml.serialization>  
  
## <a name="syntax"></a>語法  
  
```xml  
<xmlSerializer checkDeserializerAdvance = "true|false" />  
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  
 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|**checkDeserializeAdvances**|指定是否已檢查 <xref:System.Xml.Serialization.XmlSerializer>的進度。 設定屬性為 "true" 或 "false"。 預設為 "true"。|  
|**useLegacySerializationGeneration**|指定 <xref:System.Xml.Serialization.XmlSerializer> 是否使用舊版序列化產生作業，此作業會將 C# 程式碼寫入至檔案並編譯成組件，藉此產成組件。 預設值為 **false**。|  
  
### <a name="child-elements"></a>子元素  
 無。  
  
### <a name="parent-elements"></a>父項目  
  
|元素|描述|  
|-------------|-----------------|  
|[\<> 元素的 system.object 序列化](../../../docs/standard/serialization/system-xml-serialization-element.md)|包含 <xref:System.Xml.Serialization.XmlSerializer> 及 <xref:System.Xml.Serialization.XmlSchemaImporter> 類別的組態設定。|  
  
## <a name="remarks"></a>備註  
 根據預設， <xref:System.Xml.Serialization.XmlSerializer> 提供額外層級的安全性，在還原序列化未受信任的資料時，避免潛在的拒絕服務攻擊。 做法是嘗試在還原序列化期間，偵測無限迴圈。 若偵測到這樣的狀況，將擲回例外狀況並顯示下列訊息：「內部錯誤: 還原序列化無法處理基礎資料流」。  
  
 接收到此訊息並不表示正在進行阻絕服務攻擊。 在某些罕見的狀況下，無限迴圈偵測機制產生誤判，使得合法的傳入訊息導致擲回例外狀況。 如果您發現自己特定的應用程式合法訊息，遭到此額外的保護層級拒絕，請將 **checkDeserializeAdvances** 屬性設定為 "false"。  
  
## <a name="example"></a>範例  
 下列程式碼範例將 **checkDeserializeAdvances** 屬性設為 "false"。  
  
```xml  
<configuration>  
  <system.xml.serialization>  
    <xmlSerializer checkDeserializeAdvances="false" />  
  </system.xml.serialization>  
</configuration>  
```  
  
## <a name="see-also"></a>請參閱

- <xref:System.Xml.Serialization.XmlSerializer>
- [\<> 元素的 system.object 序列化](../../../docs/standard/serialization/system-xml-serialization-element.md)
- [XML 和 SOAP 序列化](../../../docs/standard/serialization/xml-and-soap-serialization.md)
