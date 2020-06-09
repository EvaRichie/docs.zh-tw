---
title: HOW TO：停用數位簽章加密
ms.date: 03/30/2017
ms.assetid: fd174313-ad81-4dca-898a-016ccaff8187
ms.openlocfilehash: 7ef305fdfd9a4ee61dfd89fdd46f2dc03a350977
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84595397"
---
# <a name="how-to-disable-encryption-of-digital-signatures"></a>HOW TO：停用數位簽章加密
根據預設，訊息會經過簽署，並且簽章會經過數位加密。 這是透過使用 <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement> 或 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> 的執行個體建立自訂繫結，並將其中一個的 `MessageProtectionOrder` 屬性設定為 <xref:System.ServiceModel.Security.MessageProtectionOrder> 列舉值的方式來控制。 預設值為 <xref:System.ServiceModel.Security.MessageProtectionOrder.SignBeforeEncryptAndEncryptSignature>。 這個程序會比僅僅進行簽署和加密多花最多 30% 的時間，依整體訊息大小而定 (訊息越小，對效能影響越大)。 然而，停用簽章加密可能會使攻擊者得以猜測訊息內容。 這是有可能的，因為簽章項目包含訊息中每個簽署部分的純文字雜湊程式碼。 例如，雖然訊息本文預設會經過加密，但未加密的簽章會包含訊息本文加密前的雜湊程式碼。 如果簽署和加密部分的可能值組合很小，攻擊者可能會參考雜湊值來推算內容。 將簽章加密可以降低遭受這個攻擊的可能性。  
  
 因此，請在內容的價值很低，或可能的內容值組合很大且非決定性，並且獲得效能比降低前述攻擊可能性來得重要時，才停用簽章加密。  
  
> [!NOTE]
> 如果訊息本身沒有加密，則簽章項目也不會加密，即使 <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement.MessageProtectionOrder%2A?displayProperty=nameWithType> 或 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement.MessageProtectionOrder%2A?displayProperty=nameWithType> 屬性設定為 <xref:System.ServiceModel.Security.MessageProtectionOrder.SignBeforeEncryptAndEncryptSignature> 也一樣。 即使是系統提供的繫結，也會發生這種情形，所有系統提供的繫結都已將訊息保護順序設定為 `SignBeforeEncryptAndEncryptSignature`。 不過，WCF 產生的 Web 服務描述語言（WSDL）仍會包含判斷提示 `<sp:EncryptSignature>` 。  
  
### <a name="to-disable-digital-signing"></a>若要停用數位簽章  
  
1. 建立 <xref:System.ServiceModel.Channels.CustomBinding>。 如需詳細資訊，請參閱[如何：使用 SecurityBindingElement 建立自訂](how-to-create-a-custom-binding-using-the-securitybindingelement.md)系結。  
  
2. 在繫結集合中加入 <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement> 或 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>。  
  
3. 將 <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement.MessageProtectionOrder%2A?displayProperty=nameWithType> 屬性設定為 <xref:System.ServiceModel.Security.MessageProtectionOrder.SignBeforeEncrypt>，或將 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement.MessageProtectionOrder%2A?displayProperty=nameWithType> 屬性設定為 <xref:System.ServiceModel.Security.MessageProtectionOrder.SignBeforeEncrypt>。  
  
## <a name="see-also"></a>請參閱

- [自訂繫結的安全性功能](security-capabilities-with-custom-bindings.md)
