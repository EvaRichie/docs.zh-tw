---
title: 作法：檢查及修改服務中的訊息
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 9c5b1cc7-84f3-45f8-9226-d59c278e8c42
ms.openlocfilehash: 8d1ce6ef00462adb38e3d59c3d9bd35694c4dbe9
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96249055"
---
# <a name="how-to-inspect-and-modify-messages-on-the-service"></a>作法：檢查及修改服務中的訊息

您可以藉由執行 <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector?displayProperty=nameWithType> ，並將其插入服務執行時間，在 Windows Communication Foundation (WCF) 用戶端檢查或修改傳入或傳出訊息。 如需詳細資訊，請參閱 [擴充發送器](extending-dispatchers.md)。 服務上對等的功能為 <xref:System.ServiceModel.Dispatcher.IClientMessageInspector?displayProperty=nameWithType>。  
  
### <a name="to-inspect-or-modify-messages"></a>檢查或修改訊息  
  
1. 實作 <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector?displayProperty=nameWithType> 介面。  
  
2. 根據您要輕鬆插入服務訊息偵測器的範圍，決定實作 、或  介面。  
  
3. 在 <xref:System.ServiceModel.ICommunicationObject.Open%2A?displayProperty=nameWithType> 上呼叫 <xref:System.ServiceModel.ServiceHost?displayProperty=nameWithType> 方法之前，請先插入您的行為。 如需詳細資訊，請參閱 [使用行為設定和擴充運行](configuring-and-extending-the-runtime-with-behaviors.md)時間。  
  
## <a name="example"></a>範例  

 下列程式碼範例會依序顯示：  
  
- 服務偵測器實作。  
  
- 插入偵測器的服務行為。  
  
- 在服務應用程式中載入及執行此行為的組態檔。  
  
 [!code-csharp[Interceptors#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/interceptors/cs/interceptors.cs#7)]
 [!code-vb[Interceptors#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/interceptors/vb/interceptors.vb#7)]  
  
 [!code-csharp[Interceptors#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/interceptors/cs/insertingbehaviors.cs#8)]
 [!code-vb[Interceptors#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/interceptors/vb/insertingbehaviors.vb#8)]  
  
 [!code-xml[Interceptors#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/interceptors/cs/hostapplication.exe.config#9)]  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.Dispatcher.IClientMessageInspector?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector?displayProperty=nameWithType>
- [使用行為來設定與擴充執行階段](configuring-and-extending-the-runtime-with-behaviors.md)
