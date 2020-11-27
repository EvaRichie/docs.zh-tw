---
title: 作法：使用相同類型的多個安全性權杖
ms.date: 03/30/2017
ms.assetid: cf179f48-4ed4-4caa-86a5-ef8eecc231cd
ms.openlocfilehash: 7374eebb9e42ef761b7ab8980b3eacf4d5671e6d
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96280698"
---
# <a name="how-to-use-multiple-security-tokens-of-the-same-type"></a>作法：使用相同類型的多個安全性權杖

- 在 .NET Framework 3.0 中，用戶端訊息只會包含任何指定類型的一個 token。 現在，用戶端訊息可以包含某個類型的多個權杖。 本主題說明如何在用戶端訊息中包含相同類型的多個權杖。  
  
- 請注意，設定服務時，服務絕對不可以只包含一個支援權杖。  
  
### <a name="to-use-multiple-security-tokens-of-the-same-type"></a>使用相同類型的多個安全性權杖  
  
1. 建立要填入的空白繫結項目集合。  
  
     [!code-csharp[C_CustomBinding#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_custombinding/cs/c_custombinding.cs#9)]  
  
2. 透過呼叫 <xref:System.ServiceModel.Channels.SecurityBindingElement> 建立 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateMutualCertificateBindingElement%2A>。  
  
     [!code-csharp[C_CustomBinding#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_custombinding/cs/c_custombinding.cs#10)]  
  
3. 建立 <xref:System.ServiceModel.Security.Tokens.SupportingTokenParameters> 集合。  
  
     [!code-csharp[C_CustomBinding#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_custombinding/cs/c_custombinding.cs#11)]  
  
4. 將 SAML 權杖加入至集合。  
  
     [!code-csharp[C_CustomBinding#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_custombinding/cs/c_custombinding.cs#12)]  
  
5. 將集合加入至 <xref:System.ServiceModel.Channels.SecurityBindingElement>。  
  
     [!code-csharp[C_CustomBinding#13](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_custombinding/cs/c_custombinding.cs#13)]  
  
6. 將繫結項目加入至繫結項目集合。  
  
     [!code-csharp[C_CustomBinding#14](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_custombinding/cs/c_custombinding.cs#14)]  
  
7. 從繫結項目集合傳回建立的新自訂繫結。  
  
     [!code-csharp[C_CustomBinding#15](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_custombinding/cs/c_custombinding.cs#15)]  
  
## <a name="example"></a>範例  

 下列是先前程序所述的完整方法。  
  
 [!code-csharp[C_CustomBinding#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_custombinding/cs/c_custombinding.cs#7)]  
