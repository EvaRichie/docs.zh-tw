---
title: HOW TO：建立安全工作階段
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- security [WCF], creating a session
ms.assetid: b6f42b5a-bbf7-45cf-b917-7ec9fa7ae110
ms.openlocfilehash: 80973a31050cf1ede03d4a3919066c62625ae590
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84593408"
---
# <a name="how-to-create-a-secure-session"></a>HOW TO：建立安全工作階段
除了系結以外 [\<basicHttpBinding>](../../configure-apps/file-schema/wcf/basichttpbinding.md) ，Windows Communication Foundation （WCF）中的系統提供系結會在啟用訊息安全性時，自動使用安全會話。  
  
 根據預設，安全工作階段不會存留回收的 Web 伺服器。 當建立安全工作階段時，用戶端和服務會快取與安全工作階段有關聯的索引鍵。 當交換訊息時，只會交換快取索引鍵的識別碼。 如果回收 Web 伺服器，也會回收快取，讓 Web 伺服器無法為識別碼擷取快取索引鍵。 如果發生這種情況，便會將例外狀況擲回用戶端。 使用可設定狀態之安全性內容權杖 (SCT) 的安全工作階段可以存留已回收的 Web 伺服器。 如需在安全會話中使用可設定狀態之 SCT 的詳細資訊，請參閱[如何：為安全會話建立安全性內容 Token](how-to-create-a-security-context-token-for-a-secure-session.md)。  
  
### <a name="to-specify-that-a-service-uses-secure-sessions-by-using-one-of-the-system-provided-bindings"></a>使用其中一個系統提供的繫結來指定服務使用安全工作階段  
  
- 請將服務設定為使用支援訊息安全性之系統提供的繫結。  
  
     除了系結之外 [\<basicHttpBinding>](../../configure-apps/file-schema/wcf/basichttpbinding.md) ，當系統提供的系結設定為使用訊息安全性時，WCF 會自動使用安全會話。 下表列出了支援訊息安全性之系統提供的繫結，以及訊息安全性是否為預設的安全性機制。  
  
    |系統提供的繫結|設定元素|訊息安全性預設為開啟|  
    |------------------------------|---------------------------|------------------------------------|  
    |<xref:System.ServiceModel.BasicHttpBinding>|[\<basicHttpBinding>](../../configure-apps/file-schema/wcf/basichttpbinding.md)|否|  
    |<xref:System.ServiceModel.WSHttpBinding>|[\<wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md)|是|  
    |<xref:System.ServiceModel.WSDualHttpBinding>|[\<wsDualHttpBinding>](../../configure-apps/file-schema/wcf/wsdualhttpbinding.md)|是|  
    |<xref:System.ServiceModel.WSFederationHttpBinding>|[\<wsFederationHttpBinding>](../../configure-apps/file-schema/wcf/wsfederationhttpbinding.md)|是|  
    |<xref:System.ServiceModel.NetTcpBinding>|[\<netTcpBinding>](../../configure-apps/file-schema/wcf/nettcpbinding.md)|否|  
    |<xref:System.ServiceModel.NetMsmqBinding>|[\<netMsmqBinding>](../../configure-apps/file-schema/wcf/netmsmqbinding.md)|否|  
  
     下列程式碼範例會使用設定來指定名為的系結，該系結 `wsHttpBinding_Calculator` 會使用 [\<wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md) 、訊息安全性和安全會話。  
  
    ```xml  
    <bindings>  
      <WSHttpBinding>  
       <binding name = "wsHttpBinding_Calculator">  
         <security mode="Message">  
           <message clientCredentialType="Windows"/>  
         </security>  
        </binding>  
      </WSHttpBinding>  
    </bindings>  
    ```  
  
     下列程式碼範例 [\<wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md) 會指定使用、訊息安全性和安全會話來保護 `secureCalculator` 服務。  
  
     [!code-csharp[c_CreateSecureSession#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_createsecuresession/cs/secureservice.cs#1)]
     [!code-vb[c_CreateSecureSession#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_createsecuresession/vb/secureservice.vb#1)]  
  
    > [!NOTE]
    > 您可以藉 [\<wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md) 由將屬性設定為，關閉的安全會話 `establishSecurityContext` `false` 。 對於其他系統提供的繫結程序，安全工作階段只能藉由建立自訂繫結程序來關閉。  
  
### <a name="to-specify-that-a-service-uses-secure-sessions-by-using-a-custom-binding"></a>使用自訂繫結來指定服務使用安全工作階段  
  
- 請建立自訂繫結，指定 SOAP 訊息受到安全工作階段的保護。  
  
     如需建立自訂系結的詳細資訊，請參閱[如何：自訂系統提供](../extending/how-to-customize-a-system-provided-binding.md)的系結。  
  
     下列程式碼範例會使用組態來指定使用安全工作階段傳送訊息的自訂繫結。  
  
    ```xml  
    <bindings>  
      <!-- configure a custom binding -->  
      <customBinding>  
        <binding name="customBinding_Calculator">  
          <security authenticationMode="SecureConversation" />  
          <secureConversationBootstrap authenticationMode="SspiNegotiated" />  
          <textMessageEncoding messageVersion="Soap12WSAddressing10" writeEncoding="utf-8"/>  
          <httpTransport/>  
        </binding>  
      </customBinding>  
    </bindings>  
    ```  
  
     下列程式碼範例建立了一個會使用 <xref:System.ServiceModel.Configuration.AuthenticationMode.MutualCertificate> 驗證模式來啟動載入安全工作階段的自訂繫結。  
  
     [!code-csharp[c_CreateSecureSession#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_createsecuresession/cs/secureservice.cs#2)]
     [!code-vb[c_CreateSecureSession#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_createsecuresession/vb/secureservice.vb#2)]  
  
## <a name="see-also"></a>請參閱

- [WCF 繫結概觀](../bindings-overview.md)
