---
title: ClientCredentials
ms.date: 03/30/2017
ms.assetid: 41dffd6b-8f14-4fed-aefb-2a1bb168efb3
ms.openlocfilehash: c63e1b3de464b306f46e2f0935b1208d7262925a
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96274188"
---
# <a name="clientcredentials"></a>ClientCredentials

ClientCredentials  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class ClientCredentials : Behavior  
{  
  string ClientCertificate;  
  string HttpDigest;  
  string IssuedToken;  
  string Peer;  
  string ServiceCertificate;  
  boolean SupportInteractive;  
  string UserName;  
  string Windows;  
};  
```  
  
## <a name="methods"></a>方法  

 ClientCredentials 類別不會定義任何方法。  
  
## <a name="properties"></a>屬性  

 ClientCredentials 類別具有下列屬性：  
  
### <a name="clientcertificate"></a>ClientCertificate  

 資料類型：字串  
  
 存取類型：唯讀  
  
 用戶端用來向服務驗證的 X.509 憑證。  
  
### <a name="httpdigest"></a>HttpDigest  

 資料類型：字串  
  
 存取類型：唯讀  
  
 目前的 Http 摘要式認證。  
  
### <a name="issuedtoken"></a>IssuedToken  

 資料類型：字串  
  
 存取類型：唯讀  
  
 用來聯繫本機安全性權杖服務的端點位址與繫結。  
  
### <a name="peer"></a>對等  

 資料類型：字串  
  
 存取類型：唯讀  
  
 對等節點用來向 mesh 中的其他節點驗證自己時使用的認證。  
  
### <a name="servicecertificate"></a>ServiceCertificate  

 資料類型：字串  
  
 存取類型：唯讀  
  
 服務的 X.509 憑證。  
  
### <a name="supportinteractive"></a>SupportInteractive  

 資料型別：布林值  
  
 存取類型：唯讀  
  
 指定認證是否支援互動式交涉的布林值。  
  
### <a name="username"></a>UserName  

 資料類型：字串  
  
 存取類型：唯讀  
  
 用戶端用來向服務驗證自身的使用者名稱和密碼。  
  
### <a name="windows"></a>Windows  

 資料類型：字串  
  
 存取類型：唯讀  
  
 用戶端用來向服務驗證自身的 Windows 認證。  
  
## <a name="requirements"></a>規格需求  
  
|MOF|於 Servicemodel.mof 中宣告。|  
|---------|-----------------------------------|  
|命名空間|於 root\ServiceModel 中定義|  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.Description.ClientCredentials>
