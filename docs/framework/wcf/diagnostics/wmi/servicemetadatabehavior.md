---
title: ServiceMetadataBehavior
ms.date: 03/30/2017
ms.assetid: 0f194476-72f1-467e-bdce-674306316e64
ms.openlocfilehash: 921a880dad0d77558a70dff8a09f75c25a3cbb8a
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96262277"
---
# <a name="servicemetadatabehavior"></a>ServiceMetadataBehavior

ServiceMetadataBehavior  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class ServiceMetadataBehavior : Behavior  
{  
  string ExternalMetadataLocation;  
  boolean HttpGetEnabled;  
  string HttpGetUrl;  
  boolean HttpsGetEnabled;  
  string HttpsGetUrl;  
};  
```  
  
## <a name="methods"></a>方法  

 ServiceMetadataBehavior 類別並未定義任何方法。  
  
## <a name="properties"></a>屬性  

 ServiceMetadataBehavior 類別具有下列屬性：  
  
### <a name="externalmetadatalocation"></a>ExternalMetadataLocation  

 資料類型：字串  
  
 存取類型：唯讀  
  
 設定服務重新導向中繼資料要求的位置。  
  
### <a name="httpgetenabled"></a>HttpGetEnabled  

 資料型別：布林值  
  
 存取類型：唯讀  
  
 控制服務是否會在由 `HttpGetUrl` 屬性控制的位址發行其 WSDL。  
  
### <a name="httpgeturl"></a>HttpGetUrl  

 資料類型：字串  
  
 存取類型：唯讀  
  
 設定服務 WSDL 的發行位置，以供使用 HTTP 擷取。  
  
### <a name="httpsgetenabled"></a>HttpsGetEnabled  

 資料型別：布林值  
  
 存取類型：唯讀  
  
 控制服務是否會透過 HTTPS，在由 `HttpsGetUrl` 屬性控制的位址發行其 WSDL。  
  
### <a name="httpsgeturl"></a>HttpsGetUrl  

 資料類型：字串  
  
 存取類型：唯讀  
  
 設定服務 WSDL 的發行位置，以供使用 HTTPS 擷取。  
  
## <a name="requirements"></a>規格需求  
  
|MOF|於 Servicemodel.mof 中宣告。|  
|---------|-----------------------------------|  
|命名空間|於 root\ServiceModel 中定義|  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.Description.ServiceMetadataBehavior>
