---
title: HOW TO：建立需要工作階段的服務
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8a7613ef-0df9-47c3-b8dc-47f42cb1fd8b
ms.openlocfilehash: 29c2a87daaf763a50aa657c9badc002ff2fa27e1
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84593330"
---
# <a name="how-to-create-a-service-that-requires-sessions"></a>HOW TO：建立需要工作階段的服務
工作階段會在兩個或更多的端點之間建立共用狀態，以啟用諸如回呼、多重躍點安全性之類的有用功能，並在用戶端與服務執行個體之間建立關聯。 如需 Windows Communication Foundation （WCF）應用程式中會話的詳細資訊，請參閱[使用會話](../using-sessions.md)。  
  
### <a name="to-specify-that-a-contract-require-its-binding-to-support-sessions"></a>指定合約需要自身繫結來支援工作階段  
  
1. 建立其中至少包含一個作業的服務合約。 如需如何建立服務合約的範例，請參閱[如何：定義服務合約](../how-to-define-a-wcf-service-contract.md)。  
  
2. 將 <xref:System.ServiceModel.ServiceContractAttribute?displayProperty=nameWithType> 屬性設為下列其中一項，以修改宣告合約的 <xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A?displayProperty=nameWithType>：  
  
    - <xref:System.ServiceModel.SessionMode.Required?displayProperty=nameWithType> (如果必須在工作階段內執行合約的話)。  
  
    - <xref:System.ServiceModel.SessionMode.Allowed?displayProperty=nameWithType> (如果可以在工作階段內執行合約的話)。  
  
    - <xref:System.ServiceModel.SessionMode.NotAllowed?displayProperty=nameWithType> (如果不得在工作階段內執行合約的話)。  
  
3. 將您的服務端點設定為使用支援工作階段的繫結。 下列組態範例說明可支援 WS<xref:System.ServiceModel.WSDualHttpBinding?displayProperty=nameWithType>ReliableMessaging 工作階段的 `-` 用法。  
  
     [!code-xml[SCA.Session#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/sca.session/cs/hostapplication.exe.config#2)]
  
## <a name="example"></a>範例  
 下列程式碼範例說明如何指定合約層級的工作階段需求，以及透過組態檔並使用 <xref:System.ServiceModel.WSDualHttpBinding?displayProperty=nameWithType> 繫結程序來支援該需求。  
  
 [!code-csharp[SCA.Session#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/sca.session/cs/services.cs#1)]
 [!code-vb[SCA.Session#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/sca.session/vb/services.vb#1)]
 [!code-xml[SCA.Session#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/sca.session/cs/hostapplication.exe.config#2)]
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.ServiceContractAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A?displayProperty=nameWithType>
- <xref:System.ServiceModel.SessionMode?displayProperty=nameWithType>
