---
title: 控制編碼 SOAP 序列化的屬性
description: 本文列出在 system.string 命名空間中找到的一組特殊屬性，以符合 SOAP 規格。
ms.date: 03/30/2017
helpviewer_keywords:
- SOAP, XML serialization
- XML serialization, SOAP
- XML serialization, attributes
- attributes [.NET Framework], XML serialization
- serialization, attributes
ms.assetid: 93ee258c-9c0f-4a08-897c-c10db7a00f91
ms.openlocfilehash: 9e99856c3ac70b122c0def23e36bbc3059c5891c
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/13/2020
ms.locfileid: "83378465"
---
# <a name="attributes-that-control-encoded-soap-serialization"></a>控制編碼 SOAP 序列化的屬性

名為「[簡單物件存取通訊協定（SOAP） 1.1](https://www.w3.org/TR/2000/NOTE-SOAP-20000508/) 」的全球資訊網協會（W3C）檔包含一個選擇性區段（第5節），描述如何編碼 SOAP 參數。 若要遵循第 5 節的規格，您必須使用在 <xref:System.Xml.Serialization> 命名空間中的特殊屬性集。 套用適合類別與類別成員的那些屬性，然後使用 <xref:System.Xml.Serialization.XmlSerializer> 序列化類別的執行個體。

下表顯示屬性、其可套用位置及作用。 如需使用這些屬性來控制 XML 序列化的詳細資訊，請參閱[如何：將物件序列化為 SOAP 編碼的 XML 資料流](how-to-serialize-an-object-as-a-soap-encoded-xml-stream.md)和[如何：覆寫編碼的 SOAP XML 序列化](how-to-override-encoded-soap-xml-serialization.md)。

如需屬性的詳細資訊，請參閱[屬性](../../../docs/standard/attributes/index.md)。

|屬性|適用對象|指定|
|---------------|----------------|---------------|
|<xref:System.Xml.Serialization.SoapAttributeAttribute>|公用欄位、屬性、參數或傳回值。|類別成員將會序列化成 XML 屬性。|
|<xref:System.Xml.Serialization.SoapElementAttribute>|公用欄位、屬性、參數或傳回值。|類別將會序列化成 XML 項目。|
|<xref:System.Xml.Serialization.SoapEnumAttribute>|為列舉識別項的公用欄位。|列舉成員的項目名稱。|
|<xref:System.Xml.Serialization.SoapIgnoreAttribute>|公用屬性與欄位。|所屬類別序列化時，略過屬性或欄位。|
|<xref:System.Xml.Serialization.SoapIncludeAttribute>|公用衍生類別宣告以及 Web 服務描述語言 (WSDL) 文件的公用方法。|當產生結構描述時應包含型別 (在序列化時辨認)。|
|<xref:System.Xml.Serialization.SoapTypeAttribute>|公用類別宣告|類別應序列化成 XML 型別。|

## <a name="see-also"></a>請參閱

- [XML 和 SOAP 序列化](xml-and-soap-serialization.md)
- [如何：將物件序列化為 SOAP 編碼的 XML 資料流](how-to-serialize-an-object-as-a-soap-encoded-xml-stream.md)
- [如何：覆寫已編碼的 SOAP XML 序列化](how-to-override-encoded-soap-xml-serialization.md)
- [屬性](../../../docs/standard/attributes/index.md)
- <xref:System.Xml.Serialization.XmlSerializer>
- [HOW TO：序列化物件](how-to-serialize-an-object.md)
- [如何：還原序列化物件](how-to-deserialize-an-object.md)
