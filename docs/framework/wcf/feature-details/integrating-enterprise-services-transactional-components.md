---
title: 整合 Enterprise Services 異動元件
ms.date: 03/30/2017
ms.assetid: 05dab277-b8b2-48cf-b40c-826be128b175
ms.openlocfilehash: 1c4fabfadb113c79b216fa10ff80b551ba0f9716
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84596847"
---
# <a name="integrating-enterprise-services-transactional-components"></a>整合 Enterprise Services 異動元件

Windows Communication Foundation （WCF）提供與企業服務整合的自動機制（請參閱[整合 COM + 應用程式](integrating-with-com-plus-applications.md)）。 不過，您可能希望能夠彈性地開發出可透過內部方式使用裝載於 Enterprise Services 之異動元件的服務。 因為 WCF 交易功能是建置於 <xref:System.Transactions> 基礎結構上，所以整合企業服務與 WCF 的程式等同于指定和企業服務之間的互通性， <xref:System.Transactions> 如[與企業服務和 com + 交易的互通性](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.0/ms229974(v=vs.85))中所述。  
  
 為了在傳入的流動異動和 COM+ 內容異動之間提供所需等級的互通性，此服務的實作必須建立 <xref:System.Transactions.TransactionScope> 執行個體並使用適當的 <xref:System.Transactions.EnterpriseServicesInteropOption> 列舉值。  
  
## <a name="integrating-enterprise-services-with-a-service-operation"></a>整合 Enterprise Services 和服務作業  
 下列程式碼範例會示範一項允許異動流程的作業，這項作業會建立具有 <xref:System.Transactions.TransactionScope> 選項的 <xref:System.Transactions.EnterpriseServicesInteropOption.Full>。 下列狀況適用於本案例：  
  
- 如果用戶端流動交易，則作業 (包括 Enterprise Services 元件的呼叫) 會在該交易的範圍內執行。 使用 <xref:System.Transactions.EnterpriseServicesInteropOption.Full> 會確保交易與 <xref:System.EnterpriseServices> 內容為同步處理，也就是說 <xref:System.Transactions> 的環境交易和 <xref:System.EnterpriseServices> 會是相同的。  
  
- 如果用戶端沒有流動異動，此時將 <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> 設定為 `true` 便會建立供作業使用的新異動範圍。 同樣地，使用 <xref:System.Transactions.EnterpriseServicesInteropOption.Full> 可確保作業的交易與 <xref:System.EnterpriseServices> 元件內容中所使用的交易是相同的。  
  
 任何其他的方法呼叫也會發生在相同作業的交易範圍內。  
  
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
  
 如果作業的目前交易和 Enterprise Services 交易元件的呼叫之間不需要同步處理，那麼請在初始化 <xref:System.Transactions.EnterpriseServicesInteropOption.None> 執行個體時使用 <xref:System.Transactions.TransactionScope> 選項。  
  
## <a name="integrating-enterprise-services-with-a-client"></a>整合 Enterprise Services 和用戶端  
 下列程式碼會示範以 <xref:System.Transactions.TransactionScope> 設定來使用 <xref:System.Transactions.EnterpriseServicesInteropOption.Full> 執行個體的用戶端程式碼。 在此案例中，支援異動流程的服務作業呼叫會發生於呼叫 Enterprise Services 元件的相同異動範圍內，  
  
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
  
## <a name="see-also"></a>請參閱

- [與 COM + 應用程式整合](integrating-with-com-plus-applications.md)
- [整合 COM 應用程式](integrating-with-com-applications.md)
