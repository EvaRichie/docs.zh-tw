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
# <a name="how-to-inspect-and-modify-messages-on-the-service"></a><span data-ttu-id="15ceb-102">作法：檢查及修改服務中的訊息</span><span class="sxs-lookup"><span data-stu-id="15ceb-102">How to: Inspect and Modify Messages on the Service</span></span>

<span data-ttu-id="15ceb-103">您可以藉由執行 <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector?displayProperty=nameWithType> ，並將其插入服務執行時間，在 Windows Communication Foundation (WCF) 用戶端檢查或修改傳入或傳出訊息。</span><span class="sxs-lookup"><span data-stu-id="15ceb-103">You can inspect or modify the incoming or outgoing messages across a Windows Communication Foundation (WCF) client by implementing a <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector?displayProperty=nameWithType> and inserting it into the service runtime.</span></span> <span data-ttu-id="15ceb-104">如需詳細資訊，請參閱 [擴充發送器](extending-dispatchers.md)。</span><span class="sxs-lookup"><span data-stu-id="15ceb-104">For more information, see [Extending Dispatchers](extending-dispatchers.md).</span></span> <span data-ttu-id="15ceb-105">服務上對等的功能為 <xref:System.ServiceModel.Dispatcher.IClientMessageInspector?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="15ceb-105">The equivalent feature on the service is the <xref:System.ServiceModel.Dispatcher.IClientMessageInspector?displayProperty=nameWithType>.</span></span>  
  
### <a name="to-inspect-or-modify-messages"></a><span data-ttu-id="15ceb-106">檢查或修改訊息</span><span class="sxs-lookup"><span data-stu-id="15ceb-106">To inspect or modify messages</span></span>  
  
1. <span data-ttu-id="15ceb-107">實作 <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector?displayProperty=nameWithType> 介面。</span><span class="sxs-lookup"><span data-stu-id="15ceb-107">Implement the <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector?displayProperty=nameWithType> interface.</span></span>  
  
2. <span data-ttu-id="15ceb-108">根據您要輕鬆插入服務訊息偵測器的範圍，決定實作 、或  介面。</span><span class="sxs-lookup"><span data-stu-id="15ceb-108">Implement a <xref:System.ServiceModel.Description.IServiceBehavior?displayProperty=nameWithType>, <xref:System.ServiceModel.Description.IEndpointBehavior?displayProperty=nameWithType>, or <xref:System.ServiceModel.Description.IContractBehavior?displayProperty=nameWithType> interface depending upon the scope at which you want to easily insert your service message inspector.</span></span>  
  
3. <span data-ttu-id="15ceb-109">在 <xref:System.ServiceModel.ICommunicationObject.Open%2A?displayProperty=nameWithType> 上呼叫 <xref:System.ServiceModel.ServiceHost?displayProperty=nameWithType> 方法之前，請先插入您的行為。</span><span class="sxs-lookup"><span data-stu-id="15ceb-109">Insert your behavior prior to calling the <xref:System.ServiceModel.ICommunicationObject.Open%2A?displayProperty=nameWithType> method on the <xref:System.ServiceModel.ServiceHost?displayProperty=nameWithType>.</span></span> <span data-ttu-id="15ceb-110">如需詳細資訊，請參閱 [使用行為設定和擴充運行](configuring-and-extending-the-runtime-with-behaviors.md)時間。</span><span class="sxs-lookup"><span data-stu-id="15ceb-110">For details, see [Configuring and Extending the Runtime with Behaviors](configuring-and-extending-the-runtime-with-behaviors.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="15ceb-111">範例</span><span class="sxs-lookup"><span data-stu-id="15ceb-111">Example</span></span>  

 <span data-ttu-id="15ceb-112">下列程式碼範例會依序顯示：</span><span class="sxs-lookup"><span data-stu-id="15ceb-112">The following code examples show, in order:</span></span>  
  
- <span data-ttu-id="15ceb-113">服務偵測器實作。</span><span class="sxs-lookup"><span data-stu-id="15ceb-113">A service inspector implementation.</span></span>  
  
- <span data-ttu-id="15ceb-114">插入偵測器的服務行為。</span><span class="sxs-lookup"><span data-stu-id="15ceb-114">A service behavior that inserts the inspector.</span></span>  
  
- <span data-ttu-id="15ceb-115">在服務應用程式中載入及執行此行為的組態檔。</span><span class="sxs-lookup"><span data-stu-id="15ceb-115">A configuration file that loads and runs the behavior in a service application.</span></span>  
  
 [!code-csharp[Interceptors#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/interceptors/cs/interceptors.cs#7)]
 [!code-vb[Interceptors#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/interceptors/vb/interceptors.vb#7)]  
  
 [!code-csharp[Interceptors#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/interceptors/cs/insertingbehaviors.cs#8)]
 [!code-vb[Interceptors#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/interceptors/vb/insertingbehaviors.vb#8)]  
  
 [!code-xml[Interceptors#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/interceptors/cs/hostapplication.exe.config#9)]  
  
## <a name="see-also"></a><span data-ttu-id="15ceb-116">另請參閱</span><span class="sxs-lookup"><span data-stu-id="15ceb-116">See also</span></span>

- <xref:System.ServiceModel.Dispatcher.IClientMessageInspector?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector?displayProperty=nameWithType>
- [<span data-ttu-id="15ceb-117">使用行為來設定與擴充執行階段</span><span class="sxs-lookup"><span data-stu-id="15ceb-117">Configuring and Extending the Runtime with Behaviors</span></span>](configuring-and-extending-the-runtime-with-behaviors.md)
