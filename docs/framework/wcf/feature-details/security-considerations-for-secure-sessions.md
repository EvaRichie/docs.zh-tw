---
title: 安全工作階段的安全性考量
ms.date: 03/30/2017
ms.assetid: 0d5be591-9a7b-4a6f-a906-95d3abafe8db
ms.openlocfilehash: abfbb565e06059e05eda3900ba9b8769e3657af8
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96276031"
---
# <a name="security-considerations-for-secure-sessions"></a>安全工作階段的安全性考量

您必須考量下列會在實作安全工作階段時影響安全性的項目。 如需安全性考慮的詳細資訊，請參閱安全性 [考慮](security-considerations-in-wcf.md) 和 [安全性最佳作法](best-practices-for-security-in-wcf.md)。  
  
## <a name="secure-sessions-and-metadata"></a>安全工作階段與中繼資料  

 當建立安全會話，並將 <xref:System.ServiceModel.Security.Tokens.SecureConversationSecurityTokenParameters.RequireCancellation%2A> 屬性設定為時 `false` ，WINDOWS COMMUNICATION FOUNDATION (WCF) 會將判斷提示傳送 `mssp:MustNotSendCancel` 為服務端點的 Web 服務描述語言 (WSDL) 檔中中繼資料的一部分。 `mssp:MustNotSendCancel` 判斷提示會告知用戶端該服務無法對取消安全工作階段的要求做出回應。 當 <xref:System.ServiceModel.Security.Tokens.SecureConversationSecurityTokenParameters.RequireCancellation%2A> 屬性設定為時 `true` ，WCF 不會 `mssp:MustNotSendCancel` 在 WSDL 檔案中發出判斷提示。 當用戶端不再需要安全工作階段時，用戶端應該要傳送取消要求給服務。 當用戶端使用 [System.servicemodel Metadata Utility 工具 ( # A0) ](../servicemodel-metadata-utility-tool-svcutil-exe.md)產生時，用戶端程式代碼會適當地回應是否存在判斷提示 `mssp:MustNotSendCancel` 。  
  
## <a name="secure-conversations-and-custom-tokens"></a>安全對話與自訂權扙  

 由於 WS-SecureConversation 規格中所定義的方式，因此混合使用自訂權扙及衍生金鑰可能會導致一些問題。 規格指出 `wsse:SecurityTokenReference` 是參考衍生權杖的選擇性元素：「 `/wsc:DerivedKeyToken/wsse:SecurityTokenReference` 這個選擇性元素用來指定用於衍生的安全性內容權杖、安全性權杖或共用金鑰/秘密。 如果沒有指定，系統會假定收件者端可以從訊息內文確認共用金鑰。 如果無法判斷內容，則應該引發錯誤（例如） `wsc:UnknownDerivationSource` 。  
  
 這意味著如果您希望衍生自訂權扙，必須將以 `SecurityTokenReference` 項目包裝它的子句型別。 也可以選擇關閉衍生，但是預設值為會衍生金鑰。 如果您無法包裝金鑰，序列化衍生金鑰權杖仍會繼續進行，但是嘗試還原序列化時，便會擲回例外狀況。  
  
## <a name="see-also"></a>另請參閱

- [作法：在 WSFederationHttpBinding 上停用安全工作階段](how-to-disable-secure-sessions-on-a-wsfederationhttpbinding.md)
- [安全性考量](security-considerations-in-wcf.md)
- [安全性的最佳做法](best-practices-for-security-in-wcf.md)
