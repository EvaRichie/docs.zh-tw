---
title: 作法：在程式碼中指定服務繫結
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 67ab5dd8-79c1-4e62-aa75-828ea918a53a
ms.openlocfilehash: 7cf54754661182dca1e91c75b158d9b0a34a1f5e
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96236477"
---
# <a name="how-to-specify-a-service-binding-in-code"></a><span data-ttu-id="72709-102">作法：在程式碼中指定服務繫結</span><span class="sxs-lookup"><span data-stu-id="72709-102">How to: Specify a Service Binding in Code</span></span>

<span data-ttu-id="72709-103">在此範例中，已為計算機服務定義了 `ICalculator` 合約、在 `CalculatorService` 類別中實作了服務，並於程式碼中定義其端點，同時指定服務必須使用 <xref:System.ServiceModel.BasicHttpBinding> 類別。</span><span class="sxs-lookup"><span data-stu-id="72709-103">In this example, an `ICalculator` contract is defined for a calculator service, the service is implemented in the `CalculatorService` class, and then its endpoint is defined in code, where it is specified that the service must use the <xref:System.ServiceModel.BasicHttpBinding> class.</span></span>  
  
 <span data-ttu-id="72709-104">通常最佳作法是在組態中以宣告方式指定繫結和位址資訊，而不是在程式碼中強制指定。</span><span class="sxs-lookup"><span data-stu-id="72709-104">It is usually the best practice to specify the binding and address information declaratively in configuration rather than imperatively in code.</span></span> <span data-ttu-id="72709-105">在程式碼中定義端點通常不太實用，因為部署之服務的繫結和位址通常與開發服務時所使用的繫結和位址不同。</span><span class="sxs-lookup"><span data-stu-id="72709-105">Defining endpoints in code is usually not practical because the bindings and addresses for a deployed service are typically different from those used while the service is being developed.</span></span> <span data-ttu-id="72709-106">比較一般性的作法是將繫結和位址資訊留在程式碼外面，如此一來，不需要重新編譯或重新部署應用程式，就可以變更繫結和位址資訊。</span><span class="sxs-lookup"><span data-stu-id="72709-106">More generally, keeping the binding and addressing information out of the code allows them to change without having to recompile or redeploy the application.</span></span>  
  
 <span data-ttu-id="72709-107">如需如何使用設定元素而非程式碼來設定此服務的說明，請參閱 [如何：在設定中指定服務](how-to-specify-a-service-binding-in-configuration.md)系結。</span><span class="sxs-lookup"><span data-stu-id="72709-107">For a description of how to configure this service using configuration elements instead of code, see [How to: Specify a Service Binding in Configuration](how-to-specify-a-service-binding-in-configuration.md).</span></span>  
  
### <a name="to-specify-in-code-to-use-the-basichttpbinding-for-the-service"></a><span data-ttu-id="72709-108">若要在程式碼中指定使用服務的 BasicHttpBinding</span><span class="sxs-lookup"><span data-stu-id="72709-108">To specify in code to use the BasicHttpBinding for the service</span></span>  
  
1. <span data-ttu-id="72709-109">定義服務類型的服務合約。</span><span class="sxs-lookup"><span data-stu-id="72709-109">Define a service contract for the type of service.</span></span>  
  
     [!code-csharp[C_HowTo_CodeServiceBinding#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#1)]
     [!code-vb[C_HowTo_CodeServiceBinding#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#1)]  
  
2. <span data-ttu-id="72709-110">在服務類別中實作服務合約。</span><span class="sxs-lookup"><span data-stu-id="72709-110">Implement the service contract in a service class.</span></span>  
  
     [!code-csharp[C_HowTo_CodeServiceBinding#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#2)]
     [!code-vb[C_HowTo_CodeServiceBinding#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#2)]  
  
3. <span data-ttu-id="72709-111">在裝載的應用程式中，建立服務起始位址以及要與服務一起搭配使用的繫結。</span><span class="sxs-lookup"><span data-stu-id="72709-111">In the hosting application, create the base address for the service and the binding to use with the service.</span></span>  
  
     [!code-csharp[C_HowTo_CodeServiceBinding#3](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#3)]
     [!code-vb[C_HowTo_CodeServiceBinding#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#3)]  
  
4. <span data-ttu-id="72709-112">建立服務的主機、新增端點，然後開啟主機。</span><span class="sxs-lookup"><span data-stu-id="72709-112">Create the host for the service, add the endpoint, and then open the host.</span></span>  
  
     [!code-csharp[C_HowTo_CodeServiceBinding#4](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#4)]
     [!code-vb[C_HowTo_CodeServiceBinding#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#4)]  
  
### <a name="to-modify-the-default-values-of-the-binding-properties"></a><span data-ttu-id="72709-113">若要修改繫結屬性的預設值</span><span class="sxs-lookup"><span data-stu-id="72709-113">To modify the default values of the binding properties</span></span>  
  
1. <span data-ttu-id="72709-114">若要修改 <xref:System.ServiceModel.BasicHttpBinding> 類別的一個預設屬性值，請在建立主機之前，先將繫結上的屬性值設為新值。</span><span class="sxs-lookup"><span data-stu-id="72709-114">To modify one of the default property values of the <xref:System.ServiceModel.BasicHttpBinding> class, set the property value on the binding to the new value before creating the host.</span></span> <span data-ttu-id="72709-115">例如，若要將預設的開啟與關閉逾時值由 1 分鐘改為 2 分鐘，請使用下列值。</span><span class="sxs-lookup"><span data-stu-id="72709-115">For example, to change the default open and close timeout values of 1 minute to 2 minutes, use the following.</span></span>  
  
     [!code-csharp[C_HowTo_CodeServiceBinding#5](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#5)]
     [!code-vb[C_HowTo_CodeServiceBinding#5](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#5)]  
  
## <a name="see-also"></a><span data-ttu-id="72709-116">另請參閱</span><span class="sxs-lookup"><span data-stu-id="72709-116">See also</span></span>

- [<span data-ttu-id="72709-117">使用繫結來設定服務和用戶端</span><span class="sxs-lookup"><span data-stu-id="72709-117">Using Bindings to Configure Services and Clients</span></span>](using-bindings-to-configure-services-and-clients.md)
- [<span data-ttu-id="72709-118">指定端點位址</span><span class="sxs-lookup"><span data-stu-id="72709-118">Specifying an Endpoint Address</span></span>](specifying-an-endpoint-address.md)
