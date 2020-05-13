---
title: HOW TO：序列化物件
description: 本文說明如何序列化物件。 選取用來儲存 XML 資料流程的傳輸格式，做為資料流程或檔案。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- serializing objects
- objects, serializing steps
ms.assetid: a1207d05-32b2-4953-8582-959607991227
ms.openlocfilehash: 63446df3fa2c931c839eda91c648cee961715f93
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/13/2020
ms.locfileid: "83377548"
---
# <a name="how-to-serialize-an-object"></a>HOW TO：序列化物件
若要序列化物件，首先建立要序列化的物件，並設定其公用屬性與欄位。 若要執行這項作業，您必須判斷 XML 資料流儲存 (無論是資料流或檔案) 的傳輸格式。 例如，若 XML 資料流必須以永久形式儲存，請建立 <xref:System.IO.FileStream> 物件。  
  
> [!NOTE]
> 如需 XML 序列化的其他範例，請參閱 [XML 序列化的範例](../../../docs/standard/serialization/examples-of-xml-serialization.md)。  
  
### <a name="to-serialize-an-object"></a>序列化物件  
  
1. 建立物件並設定其公用欄位與屬性。  
  
2. 使用物件的型別，建構 <xref:System.Xml.Serialization.XmlSerializer>。 如需詳細資訊，請參閱 <xref:System.Xml.Serialization.XmlSerializer> 類別建構函式。  
  
3. 呼叫 <xref:System.Xml.Serialization.XmlSerializer.Serialize%2A> 方法，產生 XML 資料流或物件之公用屬性與欄位的檔案表示方式。 下列範例將建立檔案。  
  
    ```vb  
    Dim myObject As MySerializableClass = New MySerializableClass()  
    ' Insert code to set properties and fields of the object.  
    Dim mySerializer As XmlSerializer = New XmlSerializer(GetType(MySerializableClass))  
    ' To write to a file, create a StreamWriter object.  
    Dim myWriter As StreamWriter = New StreamWriter("myFileName.xml")  
    mySerializer.Serialize(myWriter, myObject)  
    myWriter.Close()  
    ```  
  
    ```csharp  
    MySerializableClass myObject = new MySerializableClass();  
    // Insert code to set properties and fields of the object.  
    XmlSerializer mySerializer = new
    XmlSerializer(typeof(MySerializableClass));  
    // To write to a file, create a StreamWriter object.  
    StreamWriter myWriter = new StreamWriter("myFileName.xml");  
    mySerializer.Serialize(myWriter, myObject);  
    myWriter.Close();  
    ```  
  
## <a name="see-also"></a>請參閱

- [XML 序列化簡介](../../../docs/standard/serialization/introducing-xml-serialization.md)
- [如何：還原序列化物件](../../../docs/standard/serialization/how-to-deserialize-an-object.md)
