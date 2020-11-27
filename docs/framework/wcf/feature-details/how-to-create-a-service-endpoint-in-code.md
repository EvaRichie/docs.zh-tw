---
title: 作法：在程式碼中建立服務端點
description: 瞭解如何在類別中執行服務，並以程式設計方式定義其端點。 在 WCF 中，端點通常定義于設定檔中。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 3fbb22fa-2930-48b8-b437-def1de87c6a0
ms.openlocfilehash: 6f5e06154ff19129da0bce77dd70736037c2dc92
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96294413"
---
# <a name="how-to-create-a-service-endpoint-in-code"></a><span data-ttu-id="00066-104">作法：在程式碼中建立服務端點</span><span class="sxs-lookup"><span data-stu-id="00066-104">How to: Create a Service Endpoint in Code</span></span>

<span data-ttu-id="00066-105">在此範例中，已為計算機服務定義了 `ICalculator` 合約、在 `CalculatorService` 類別中實作了服務，並於程式碼中定義其端點，同時指定服務必須使用 <xref:System.ServiceModel.BasicHttpBinding> 類別。</span><span class="sxs-lookup"><span data-stu-id="00066-105">In this example, an `ICalculator` contract is defined for a calculator service, the service is implemented in the `CalculatorService` class, and then its endpoint is defined in code, where it is specified that the service must use the <xref:System.ServiceModel.BasicHttpBinding> class.</span></span>  
  
 <span data-ttu-id="00066-106">通常最佳作法是在組態中以宣告方式指定繫結和位址資訊，而不是在程式碼中強制指定。</span><span class="sxs-lookup"><span data-stu-id="00066-106">It is usually the best practice to specify the binding and address information declaratively in configuration rather than imperatively in code.</span></span> <span data-ttu-id="00066-107">在程式碼中定義端點通常不太實用，因為部署之服務的繫結和位址通常與開發服務時所使用的繫結和位址不同。</span><span class="sxs-lookup"><span data-stu-id="00066-107">Defining endpoints in code is usually not practical because the bindings and addresses for a deployed service are typically different from those used while the service is being developed.</span></span> <span data-ttu-id="00066-108">比較一般性的作法是將繫結和位址資訊留在程式碼外面，如此一來，不需要重新編譯或重新部署應用程式，就可以變更繫結和位址資訊。</span><span class="sxs-lookup"><span data-stu-id="00066-108">More generally, keeping the binding and addressing information out of the code allows them to change without having to recompile or redeploy the application.</span></span>  
  
#### <a name="to-create-a-service-endpoint-in-code"></a><span data-ttu-id="00066-109">若要在程式碼中建立服務端點</span><span class="sxs-lookup"><span data-stu-id="00066-109">To create a service endpoint in code</span></span>  
  
1. <span data-ttu-id="00066-110">建立可定義服務合約的介面。</span><span class="sxs-lookup"><span data-stu-id="00066-110">Create the interface that defines the service contract.</span></span>  
  
     [!code-csharp[c_HowTo_CodeServiceBinding#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#1)]
     [!code-vb[c_HowTo_CodeServiceBinding#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#1)]  
  
2. <span data-ttu-id="00066-111">實作步驟 1 中定義的服務合約。</span><span class="sxs-lookup"><span data-stu-id="00066-111">Implement the service contract defined in step 1.</span></span>  
  
     [!code-csharp[c_HowTo_CodeServiceBinding#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#2)]
     [!code-vb[c_HowTo_CodeServiceBinding#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#2)]  
  
3. <span data-ttu-id="00066-112">在裝載應用程式中，建立服務的基底位址以及要與服務一起搭配使用的繫結。</span><span class="sxs-lookup"><span data-stu-id="00066-112">In the hosting application, create the base address for the service and the binding to be used with the service.</span></span>  
  
     [!code-csharp[c_HowTo_CodeServiceBinding#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#3)]
     [!code-vb[c_HowTo_CodeServiceBinding#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#3)]  
  
4. <span data-ttu-id="00066-113">建立主機並呼叫 <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%28System.Type%2CSystem.ServiceModel.Channels.Binding%2CSystem.String%29?displayProperty=nameWithType> 或其他多載中的一個，為主機新增服務端點。</span><span class="sxs-lookup"><span data-stu-id="00066-113">Create the host and call <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%28System.Type%2CSystem.ServiceModel.Channels.Binding%2CSystem.String%29?displayProperty=nameWithType> or one of the other overloads to add the service endpoint for the host.</span></span>  
  
     [!code-csharp[c_HowTo_CodeServiceBinding#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#6)]
     [!code-vb[c_HowTo_CodeServiceBinding#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#6)]  
  
     <span data-ttu-id="00066-114">若要在程式碼中指定系結，但要使用執行時間提供的預設端點，請在建立時將基底位址傳遞至函式， <xref:System.ServiceModel.ServiceHost> 而不要呼叫 <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%2A?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="00066-114">To specify the binding in code but to use the default endpoints provided by the runtime, pass the base address into the constructor when creating the <xref:System.ServiceModel.ServiceHost>, and do not call <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%2A?displayProperty=nameWithType>.</span></span>  
  
     [!code-csharp[c_HowTo_CodeServiceBinding#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#7)]
     [!code-vb[c_HowTo_CodeServiceBinding#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#7)]  
  
     <span data-ttu-id="00066-115">如需預設端點的詳細資訊，請參閱 [簡化](../simplified-configuration.md) 設定和 [簡化 WCF 服務的](../samples/simplified-configuration-for-wcf-services.md)設定。</span><span class="sxs-lookup"><span data-stu-id="00066-115">For more information about default endpoints, see [Simplified Configuration](../simplified-configuration.md) and [Simplified Configuration for WCF Services](../samples/simplified-configuration-for-wcf-services.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="00066-116">另請參閱</span><span class="sxs-lookup"><span data-stu-id="00066-116">See also</span></span>

- [<span data-ttu-id="00066-117">作法：在程式碼中指定服務繫結</span><span class="sxs-lookup"><span data-stu-id="00066-117">How to: Specify a Service Binding in Code</span></span>](../how-to-specify-a-service-binding-in-code.md)
