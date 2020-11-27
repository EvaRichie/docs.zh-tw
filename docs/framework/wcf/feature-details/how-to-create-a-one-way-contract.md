---
title: 作法：建立單向合約
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 85084cd9-31cc-4e95-b667-42ef01336622
ms.openlocfilehash: 7f0285ba4824ac842b3644d0834782139fd90657
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96268686"
---
# <a name="how-to-create-a-one-way-contract"></a><span data-ttu-id="de01c-102">作法：建立單向合約</span><span class="sxs-lookup"><span data-stu-id="de01c-102">How to: Create a One-Way Contract</span></span>

<span data-ttu-id="de01c-103">本主題說明的基本步驟可用來建立使用單向合約的方法。</span><span class="sxs-lookup"><span data-stu-id="de01c-103">This topic shows the basic steps to create methods that use a one-way contract.</span></span> <span data-ttu-id="de01c-104">這類方法會從用戶端叫用 Windows Communication Foundation (WCF) 服務的作業，但不預期會有回復。</span><span class="sxs-lookup"><span data-stu-id="de01c-104">Such methods invoke operations on a Windows Communication Foundation (WCF) service from a client but do not expect a reply.</span></span> <span data-ttu-id="de01c-105">例如，您可以使用此合約類型，將通知發行給許多訂閱者。</span><span class="sxs-lookup"><span data-stu-id="de01c-105">This type of contract can be used, for example, to publish notifications to many subscribers.</span></span> <span data-ttu-id="de01c-106">您也可以在建立雙工 (雙向) 合約時使用單向合約，以供用戶端與伺服器彼此各自進行通訊，並方便任何一方初始化對另一方的呼叫。</span><span class="sxs-lookup"><span data-stu-id="de01c-106">You can also use one-way contracts when creating a duplex (two-way) contract, which allows clients and servers to communicate with each other independently so that either can initiate calls to the other.</span></span> <span data-ttu-id="de01c-107">這麼做可以特別允許伺服器對用戶端進行單向呼叫，而用戶端會將此呼叫視為事件。</span><span class="sxs-lookup"><span data-stu-id="de01c-107">This can allow, in particular, the server to make one-way calls to the client that the client can treat as events.</span></span> <span data-ttu-id="de01c-108">如需指定單向方法的詳細資訊，請參閱 <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> 屬性與 <xref:System.ServiceModel.OperationContractAttribute> 類別。</span><span class="sxs-lookup"><span data-stu-id="de01c-108">For detailed information about specifying one-way methods, see the <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> property and the <xref:System.ServiceModel.OperationContractAttribute> class.</span></span>  
  
 <span data-ttu-id="de01c-109">如需有關為雙工合約建立用戶端應用程式的詳細資訊，請參閱 [如何：使用 One-Way 和 Request-Reply 合約存取服務](how-to-access-wcf-services-with-one-way-and-request-reply-contracts.md)。</span><span class="sxs-lookup"><span data-stu-id="de01c-109">For more information about creating a client application for a duplex contract, see [How to: Access Services with One-Way and Request-Reply Contracts](how-to-access-wcf-services-with-one-way-and-request-reply-contracts.md).</span></span> <span data-ttu-id="de01c-110">如需實用的範例，請參閱 [單向](../samples/one-way.md) 範例。</span><span class="sxs-lookup"><span data-stu-id="de01c-110">For a working sample, see the [One-Way](../samples/one-way.md) sample.</span></span>  
  
### <a name="to-create-a-one-way-contract"></a><span data-ttu-id="de01c-111">若要建立單向合約</span><span class="sxs-lookup"><span data-stu-id="de01c-111">To create a one-way contract</span></span>  
  
1. <span data-ttu-id="de01c-112">將 <xref:System.ServiceModel.ServiceContractAttribute> 類別套用至用來定義服務要實作之方法的介面，以建立服務合約。</span><span class="sxs-lookup"><span data-stu-id="de01c-112">Create the service contract by applying the <xref:System.ServiceModel.ServiceContractAttribute> class to the interface that defines the methods the service is to implement.</span></span>  
  
2. <span data-ttu-id="de01c-113">指出介面中可供用戶端叫用的方法，方法是將 <xref:System.ServiceModel.OperationContractAttribute> 類別套用到這些方法上。</span><span class="sxs-lookup"><span data-stu-id="de01c-113">Indicate which methods in the interface a client can invoked by applying the <xref:System.ServiceModel.OperationContractAttribute> class to them.</span></span>  
  
3. <span data-ttu-id="de01c-114">將 <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> 屬性設為 `true`，以便將不得包含輸出的作業 (沒有傳回值，也沒有 out 或 ref 參數) 指定為單向。</span><span class="sxs-lookup"><span data-stu-id="de01c-114">Designate operations that must have no output (no return value and no out or ref parameters) as one-way by setting the <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> property to `true`.</span></span> <span data-ttu-id="de01c-115">請注意，帶有 <xref:System.ServiceModel.OperationContractAttribute> 類別的作業預設都會滿足要求-回覆合約，因為 <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> 屬性會預設為 `false`。</span><span class="sxs-lookup"><span data-stu-id="de01c-115">Note that the operations that carry the <xref:System.ServiceModel.OperationContractAttribute> class satisfy a request-reply contract by default because the <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> property is `false` by default.</span></span> <span data-ttu-id="de01c-116">因此如果您希望方法使用單向合約，就必須明確地將屬性值指定為 `true`。</span><span class="sxs-lookup"><span data-stu-id="de01c-116">So you must explicitly specify the value of the attribute property to be `true` if you want a one-way contract for the method.</span></span>  
  
## <a name="example"></a><span data-ttu-id="de01c-117">範例</span><span class="sxs-lookup"><span data-stu-id="de01c-117">Example</span></span>  

 <span data-ttu-id="de01c-118">下列程式碼範例定義包含數個單向方法的服務合約。</span><span class="sxs-lookup"><span data-stu-id="de01c-118">The following code example defines a contract for a service that includes several one-way methods.</span></span> <span data-ttu-id="de01c-119">所有的方法都具有單向合約，除了 `Equals` 以外，因為它會預設為要求-回覆，並傳回結果。</span><span class="sxs-lookup"><span data-stu-id="de01c-119">All of the methods have one-way contracts except `Equals`, which defaults to request-reply and returns a result.</span></span>  
  
 [!code-csharp[S_Service_Session#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_service_session/cs/service.cs#1)]
 [!code-vb[S_Service_Session#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_service_session/vb/service.vb#1)]  
  
## <a name="see-also"></a><span data-ttu-id="de01c-120">另請參閱</span><span class="sxs-lookup"><span data-stu-id="de01c-120">See also</span></span>

- <xref:System.ServiceModel.ServiceContractAttribute>
- <xref:System.ServiceModel.OperationContractAttribute>
- [<span data-ttu-id="de01c-121">設計與實作服務</span><span class="sxs-lookup"><span data-stu-id="de01c-121">Designing and Implementing Services</span></span>](../designing-and-implementing-services.md)
- [<span data-ttu-id="de01c-122">如何：定義服務合約</span><span class="sxs-lookup"><span data-stu-id="de01c-122">How to: Define a Service Contract</span></span>](../how-to-define-a-wcf-service-contract.md)
- [<span data-ttu-id="de01c-123">工作階段</span><span class="sxs-lookup"><span data-stu-id="de01c-123">Session</span></span>](../samples/session.md)
- [<span data-ttu-id="de01c-124">作法：建立雙面合約</span><span class="sxs-lookup"><span data-stu-id="de01c-124">How to: Create a Duplex Contract</span></span>](how-to-create-a-duplex-contract.md)
