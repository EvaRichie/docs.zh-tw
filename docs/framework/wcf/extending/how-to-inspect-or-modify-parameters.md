---
title: 作法：檢查或修改參數
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: ab6c0ac7-aac4-45ba-93d6-a0e9afd1756f
ms.openlocfilehash: e8b2674d8efc0ef3ac2f1dd6ab0df559195c274c
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96249029"
---
# <a name="how-to-inspect-or-modify-parameters"></a>作法：檢查或修改參數

您可以藉由執行 <xref:System.ServiceModel.Dispatcher.IParameterInspector?displayProperty=nameWithType> 介面並將其插入用戶端或服務執行時間中，在 Windows Communication Foundation (WCF) 用戶端物件或 wcf 服務上檢查或修改單一作業的傳入或傳出訊息。 一般來說，作業行為是用於新增單一作業的參數偵測器；其他行為可用於提供範圍更大之執行階段的簡易存取。 如需詳細資訊，請參閱 [擴充用戶端](extending-clients.md) 和 [延伸發送器](extending-dispatchers.md)。  
  
### <a name="inspecting-or-modifying-parameters"></a>檢查或修改參數  
  
1. 實作 <xref:System.ServiceModel.Dispatcher.IParameterInspector?displayProperty=nameWithType> 介面。  
  
2. 請實作 <xref:System.ServiceModel.Description.IOperationBehavior?displayProperty=nameWithType>、<xref:System.ServiceModel.Description.IEndpointBehavior?displayProperty=nameWithType>、<xref:System.ServiceModel.Description.IServiceBehavior?displayProperty=nameWithType> 或 <xref:System.ServiceModel.Description.IContractBehavior?displayProperty=nameWithType> (視所需要的範圍而定)，將您的參數偵測器新增至 <xref:System.ServiceModel.Dispatcher.ClientOperation.ParameterInspectors%2A?displayProperty=nameWithType> 或 <xref:System.ServiceModel.Dispatcher.DispatchOperation.ParameterInspectors%2A?displayProperty=nameWithType> 屬性。  
  
3. 在 <xref:System.ServiceModel.ClientBase%601.Open%2A?displayProperty=nameWithType> 上呼叫 <xref:System.ServiceModel.ICommunicationObject.Open%2A?displayProperty=nameWithType> 或 <xref:System.ServiceModel.ChannelFactory%601?displayProperty=nameWithType> 方法之前，請先插入您的行為。 如需詳細資訊，請參閱 [使用行為設定和擴充運行](configuring-and-extending-the-runtime-with-behaviors.md)時間。  
  
## <a name="example"></a>範例  

 下列程式碼範例會依序顯示：  
  
- 參數偵測器實作。  
  
- 使用 <xref:System.ServiceModel.Description.IOperationBehavior?displayProperty=nameWithType>、<xref:System.ServiceModel.Description.IEndpointBehavior?displayProperty=nameWithType> 和 <xref:System.ServiceModel.Description.IServiceBehavior?displayProperty=nameWithType> 插入參數偵測器的行為實作。  
  
- 在用戶端應用程式中載入及執行端點行為，以在用戶端上插入參數偵測器的組態檔。  
  
 [!code-csharp[Interceptors#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/interceptors/cs/interceptors.cs#4)]
 [!code-vb[Interceptors#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/interceptors/vb/interceptors.vb#4)]  
  
 [!code-csharp[Interceptors#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/interceptors/cs/insertingbehaviors.cs#5)]
 [!code-vb[Interceptors#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/interceptors/vb/insertingbehaviors.vb#5)]  
  
 [!code-xml[Interceptors#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/interceptors/cs/client.exe.config#3)]  
  
## <a name="see-also"></a>另請參閱

- [使用行為來設定與擴充執行階段](configuring-and-extending-the-runtime-with-behaviors.md)
