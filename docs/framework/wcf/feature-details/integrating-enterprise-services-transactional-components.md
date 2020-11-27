---
title: 整合 Enterprise Services 異動元件
ms.date: 03/30/2017
ms.assetid: 05dab277-b8b2-48cf-b40c-826be128b175
ms.openlocfilehash: d235806ba94d68cadca91a17361bfd5bab1e1332
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96265865"
---
# <a name="integrating-enterprise-services-transactional-components"></a><span data-ttu-id="4f6a5-102">整合 Enterprise Services 異動元件</span><span class="sxs-lookup"><span data-stu-id="4f6a5-102">Integrating Enterprise Services Transactional Components</span></span>

<span data-ttu-id="4f6a5-103">Windows Communication Foundation (WCF) 會提供自動機制，以便與企業服務整合 (查看 [與 COM + 應用程式整合](integrating-with-com-plus-applications.md)) 。</span><span class="sxs-lookup"><span data-stu-id="4f6a5-103">Windows Communication Foundation (WCF) provides an automatic mechanism for integrating with Enterprise Services (see [Integrating with COM+ Applications](integrating-with-com-plus-applications.md)).</span></span> <span data-ttu-id="4f6a5-104">不過，您可能希望能夠彈性地開發出可透過內部方式使用裝載於 Enterprise Services 之異動元件的服務。</span><span class="sxs-lookup"><span data-stu-id="4f6a5-104">However, you may want the flexibility to develop services that internally use transactional components hosted within Enterprise Services.</span></span> <span data-ttu-id="4f6a5-105">因為 WCF 交易功能是以 <xref:System.Transactions> 基礎結構為基礎，所以將企業服務與 WCF 整合的程式與指定和企業服務之間的互通性完全相同 <xref:System.Transactions> ，如 [企業服務和 com + 交易的互通性](/previous-versions/dotnet/netframework-3.0/ms229974(v=vs.85))所述。</span><span class="sxs-lookup"><span data-stu-id="4f6a5-105">Because the WCF Transactions feature is built on the <xref:System.Transactions> infrastructure, the process for integrating Enterprise Services with WCF is identical to that for specifying interoperability between <xref:System.Transactions> and Enterprise Services, as outlined in [Interoperability with Enterprise Services and COM+ Transactions](/previous-versions/dotnet/netframework-3.0/ms229974(v=vs.85)).</span></span>  
  
 <span data-ttu-id="4f6a5-106">為了在傳入的流動異動和 COM+ 內容異動之間提供所需等級的互通性，此服務的實作必須建立 <xref:System.Transactions.TransactionScope> 執行個體並使用適當的 <xref:System.Transactions.EnterpriseServicesInteropOption> 列舉值。</span><span class="sxs-lookup"><span data-stu-id="4f6a5-106">To provide the desired level of interoperability between the incoming flowed transaction and the COM+ context transaction, the service implementation must create a <xref:System.Transactions.TransactionScope> instance and use the appropriate value from the <xref:System.Transactions.EnterpriseServicesInteropOption> enumeration.</span></span>  
  
## <a name="integrating-enterprise-services-with-a-service-operation"></a><span data-ttu-id="4f6a5-107">整合 Enterprise Services 和服務作業</span><span class="sxs-lookup"><span data-stu-id="4f6a5-107">Integrating Enterprise Services with a Service Operation</span></span>  

 <span data-ttu-id="4f6a5-108">下列程式碼範例會示範一項允許異動流程的作業，這項作業會建立具有 <xref:System.Transactions.TransactionScope> 選項的 <xref:System.Transactions.EnterpriseServicesInteropOption.Full>。</span><span class="sxs-lookup"><span data-stu-id="4f6a5-108">The following code demonstrates an operation, with Allowed transaction flow, that creates a <xref:System.Transactions.TransactionScope> with the <xref:System.Transactions.EnterpriseServicesInteropOption.Full> option.</span></span> <span data-ttu-id="4f6a5-109">下列狀況適用於本案例：</span><span class="sxs-lookup"><span data-stu-id="4f6a5-109">The following conditions apply in this scenario:</span></span>  
  
- <span data-ttu-id="4f6a5-110">如果用戶端流動交易，則作業 (包括 Enterprise Services 元件的呼叫) 會在該交易的範圍內執行。</span><span class="sxs-lookup"><span data-stu-id="4f6a5-110">If the client flows a transaction, the operation, including the call to the Enterprise Services component, is executed within the scope of that transaction.</span></span> <span data-ttu-id="4f6a5-111">使用 <xref:System.Transactions.EnterpriseServicesInteropOption.Full> 會確保交易與 <xref:System.EnterpriseServices> 內容為同步處理，也就是說 <xref:System.Transactions> 的環境交易和 <xref:System.EnterpriseServices> 會是相同的。</span><span class="sxs-lookup"><span data-stu-id="4f6a5-111">Using <xref:System.Transactions.EnterpriseServicesInteropOption.Full> ensures that the transaction is synchronized with the <xref:System.EnterpriseServices> context, which means that the ambient transaction for <xref:System.Transactions> and the <xref:System.EnterpriseServices> is the same.</span></span>  
  
- <span data-ttu-id="4f6a5-112">如果用戶端沒有流動異動，此時將 <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> 設定為 `true` 便會建立供作業使用的新異動範圍。</span><span class="sxs-lookup"><span data-stu-id="4f6a5-112">If the client does not flow a transaction, setting <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> to `true` creates a new transaction scope for the operation.</span></span> <span data-ttu-id="4f6a5-113">同樣地，使用 <xref:System.Transactions.EnterpriseServicesInteropOption.Full> 可確保作業的交易與 <xref:System.EnterpriseServices> 元件內容中所使用的交易是相同的。</span><span class="sxs-lookup"><span data-stu-id="4f6a5-113">Similarly, using <xref:System.Transactions.EnterpriseServicesInteropOption.Full> ensures that the operation’s transaction is the same as the transaction used inside the <xref:System.EnterpriseServices> component's context.</span></span>  
  
 <span data-ttu-id="4f6a5-114">任何其他的方法呼叫也會發生在相同作業的交易範圍內。</span><span class="sxs-lookup"><span data-stu-id="4f6a5-114">Any additional method calls also occur within the scope of the same operation’s transaction.</span></span>  
  
```csharp
[ServiceContract()]  
public interface ICustomerServiceContract  
{  
   [OperationContract]  
   [TransactionFlow(TransactionFlowOption.Allowed)]  
   void UpdateCustomerNameOperation(int customerID, string newCustomerName);  
}  
  
[ServiceBehavior(TransactionIsolationLevel = System.Transactions.IsolationLevel.Serializable)]  
public class CustomerService : ICustomerServiceContract  
{  
   [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = true)]  
   public void UpdateCustomerNameOperation(int customerID, string newCustomerName)  
   {  
   // Create a transaction scope with full ES interop  
      using (TransactionScope ts = new TransactionScope(  
                     TransactionScopeOption.Required,  
                     new TransactionOptions(),  
                     EnterpriseServicesInteropOption.Full))  
      {  
         // Create an Enterprise Services component  
         // Call UpdateCustomer method on an Enterprise Services
         // component
  
         // Call UpdateOtherCustomerData method on an Enterprise
         // Services component
         ts.Complete();  
      }  
  
      // Do UpdateAdditionalData on an non-Enterprise Services  
      // component  
   }  
}  
```  
  
 <span data-ttu-id="4f6a5-115">如果作業的目前交易和 Enterprise Services 交易元件的呼叫之間不需要同步處理，那麼請在初始化 <xref:System.Transactions.EnterpriseServicesInteropOption.None> 執行個體時使用 <xref:System.Transactions.TransactionScope> 選項。</span><span class="sxs-lookup"><span data-stu-id="4f6a5-115">If no synchronization is required between an operation’s current transaction and calls to transactional Enterprise Services components, then use the <xref:System.Transactions.EnterpriseServicesInteropOption.None> option when instantiating the <xref:System.Transactions.TransactionScope> instance.</span></span>  
  
## <a name="integrating-enterprise-services-with-a-client"></a><span data-ttu-id="4f6a5-116">整合 Enterprise Services 和用戶端</span><span class="sxs-lookup"><span data-stu-id="4f6a5-116">Integrating Enterprise Services with a Client</span></span>  

 <span data-ttu-id="4f6a5-117">下列程式碼會示範以 <xref:System.Transactions.TransactionScope> 設定來使用 <xref:System.Transactions.EnterpriseServicesInteropOption.Full> 執行個體的用戶端程式碼。</span><span class="sxs-lookup"><span data-stu-id="4f6a5-117">The following code demonstrates client code using a <xref:System.Transactions.TransactionScope> instance with the <xref:System.Transactions.EnterpriseServicesInteropOption.Full> setting.</span></span> <span data-ttu-id="4f6a5-118">在此案例中，支援異動流程的服務作業呼叫會發生於呼叫 Enterprise Services 元件的相同異動範圍內，</span><span class="sxs-lookup"><span data-stu-id="4f6a5-118">In this scenario, calls to service operations that support transaction flow occur within the scope of the same transaction as the calls to Enterprise Services components.</span></span>  
  
```csharp
static void Main()  
{  
    // Create a client  
    CalculatorClient client = new CalculatorClient();  
  
    // Create a transaction scope with full ES interop  
    using (TransactionScope ts = new TransactionScope(  
          TransactionScopeOption.Required,  
          new TransactionOptions(),  
          EnterpriseServicesInteropOption.Full))  
    {  
        // Call Add calculator service operation  
  
        // Create an Enterprise Services component  
  
        // Call UpdateCustomer method on an Enterprise Services
        // component
  
        ts.Complete();  
    }  
  
    // Closing the client gracefully closes the connection and
    // cleans up resources  
    client.Close();  
}  
```  
  
## <a name="see-also"></a><span data-ttu-id="4f6a5-119">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4f6a5-119">See also</span></span>

- [<span data-ttu-id="4f6a5-120">與 COM + 應用程式整合</span><span class="sxs-lookup"><span data-stu-id="4f6a5-120">Integrating with COM+ Applications</span></span>](integrating-with-com-plus-applications.md)
- [<span data-ttu-id="4f6a5-121">整合 COM 應用程式</span><span class="sxs-lookup"><span data-stu-id="4f6a5-121">Integrating with COM Applications</span></span>](integrating-with-com-applications.md)
