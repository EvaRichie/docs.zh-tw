---
title: BinaryMessageEncodingBindingElement
ms.date: 03/30/2017
ms.assetid: e2bb3cdd-3bbd-4bb5-85fe-570457500a66
ms.openlocfilehash: eb174d12731d7f1bc78f4d709cf043daf2346bd2
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96269791"
---
# <a name="binarymessageencodingbindingelement"></a>BinaryMessageEncodingBindingElement

BinaryMessageEncodingBindingElement  
  
## <a name="syntax"></a>Syntax  
  
```csharp  
class BinaryMessageEncodingBindingElement : MessageEncodingBindingElement  
{  
  sint32 MaxReadPoolSize;  
  sint32 MaxSessionSize;  
  sint32 MaxWritePoolSize;  
  XmlDictionaryReaderQuotas ReaderQuotas;  
};  
```  
  
## <a name="methods"></a>方法  

 BinaryMessageEncodingBindingElement 類別並未定義任何方法。  
  
## <a name="properties"></a>屬性  

 BinaryMessageEncodingBindingElement 類別具有下列屬性。  
  
## <a name="maxreadpoolsize"></a>MaxReadPoolSize  

 資料型別：sint32  
  
 存取類型：唯讀  
  
 定義可同時讀取之訊息數目 (在不配置新讀取器的情況下) 的整數。  
  
## <a name="maxsessionsize"></a>MaxSessionSize  

 資料型別：sint32  
  
 存取類型：唯讀  
  
 此值可指定用於編碼的緩衝區大小 (以位元組為單位)。  
  
## <a name="maxwritepoolsize"></a>MaxWritePoolSize  

 資料型別：sint32  
  
 存取類型：唯讀  
  
 定義可同時傳送之訊息數目 (在不配置新寫入器的情況下) 的整數。  
  
## <a name="readerquotas"></a>ReaderQuotas  

 資料型別：XmlDictionaryReaderQuotas  
  
 存取類型：唯讀  
  
 讀取器的配額。  
  
## <a name="requirements"></a>規格需求  
  
|MOF|於 Servicemodel.mof 中宣告。|  
|---------|-----------------------------------|  
|命名空間|於 root\ServiceModel 中定義|  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement>
