---
title: <certificateValidator>
ms.date: 03/30/2017
ms.assetid: 86161897-c20f-4ad8-9d7f-050c247251bf
author: BrucePerlerMS
ms.openlocfilehash: 8476600769b6099bb885566de4c908c78a2dbbda
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91201367"
---
# \<certificateValidator>

指定憑證驗證的自訂類型。 只有當 `certificateValidationMode` 元素的屬性 [\<certificateValidation>](certificatevalidation.md) 設為 "Custom" 時，才會使用這個型別。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.identityModel>**](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<identityConfiguration>**](identityconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<certificateValidation>**](certificatevalidation.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<certificateValidator>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <certificateValidation>  
      <certificateValidator type=xs:string>  
      </certificateValidator>  
    </certificateValidation>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  

 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|type|指定衍生自類別的自訂型別 <xref:System.IdentityModel.Selectors.X509CertificateValidator> 。 將專案的 `certificateValidationMode` 屬性設定 [\<certificateValidation>](certificatevalidation.md) 為 [自訂]，以使用此類型。 如需如何指定屬性的詳細資訊 `type` ，請參閱 [自訂型別參考](../windows-workflow-foundation/index.md)。 選擇性。|  
  
### <a name="child-elements"></a>子元素  

 無  
  
### <a name="parent-elements"></a>父項目  
  
|項目|描述|  
|-------------|-----------------|  
|[\<certificateValidation>](certificatevalidation.md)|控制權杖處理常式用來驗證憑證的設定。|  
  
## <a name="example"></a>範例  
  
```xml  
<certificateValidation certificateValidationMode="Custom"  
                       revocationMode="Online"  
                       trustedStoreLocation="LocalMachine">  
    <certificateValidator type="MyNamespace.CustomValidator, MyAssembly" />
</certificateValidation>
```
