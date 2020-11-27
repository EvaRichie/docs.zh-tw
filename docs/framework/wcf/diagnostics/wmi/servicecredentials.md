---
title: ServiceCredentials
ms.date: 03/30/2017
ms.assetid: 9c780793-4785-46f7-add9-ac1ebeadb614
ms.openlocfilehash: d7e89acedc8fc1004b0198172e58813944df85f3
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96262303"
---
# <a name="servicecredentials"></a>ServiceCredentials

ServiceCredentials  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class ServiceCredentials : Behavior  
{  
  string ClientCertificate;  
  string IssuedTokenAuthentication;  
  string Peer;  
  string SecureConversationAuthentication;  
  string ServiceCertificate;  
  string UserNameAuthentication;  
  string WindowsAuthentication;  
};  
```  
  
## <a name="methods"></a>方法  

 ServiceCredentials 類別不會定義任何方法。  
  
## <a name="properties"></a>屬性  

 ServiceCredentials 類別有下列屬性：  
  
### <a name="clientcertificate"></a>ClientCertificate  

 資料類型：字串  
  
 存取類型：唯讀  
  
 用戶端憑證驗證與此服務的佈建設定。  
  
### <a name="issuedtokenauthentication"></a>IssuedTokenAuthentication  

 資料類型：字串  
  
 存取類型：唯讀  
  
 這項服務目前發行的權杖驗證設定。  
  
### <a name="peer"></a>對等  

 資料類型：字串  
  
 存取類型：唯讀  
  
 目前的認證驗證與對等傳輸端點將使用的佈建設定。  
  
### <a name="secureconversationauthentication"></a>SecureConversationAuthentication  

 資料類型：字串  
  
 存取類型：唯讀  
  
 指定目前的安全對話設定。  
  
### <a name="servicecertificate"></a>ServiceCertificate  

 資料類型：字串  
  
 存取類型：唯讀  
  
 與這項服務關聯的憑證。  
  
### <a name="usernameauthentication"></a>UserNameAuthentication  

 資料類型：字串  
  
 存取類型：唯讀  
  
 這項服務的使用者名稱和密碼設定。  
  
### <a name="windowsauthentication"></a>WindowsAuthentication  

 資料類型：字串  
  
 存取類型：唯讀  
  
 這項服務的 Windows 驗證設定。  
  
## <a name="requirements"></a>規格需求  
  
|MOF|於 Servicemodel.mof 中宣告。|  
|---------|-----------------------------------|  
|命名空間|於 root\ServiceModel 中定義|  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.Description.ServiceCredentials>
