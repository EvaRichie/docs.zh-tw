---
title: 作法：建立交易式服務
ms.date: 03/30/2017
ms.assetid: 1bd2e4ed-a557-43f9-ba98-4c70cb75c154
ms.openlocfilehash: c3d094dbd5822f6025e1cc6c90aab04b61459314
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96286288"
---
# <a name="how-to-create-a-transactional-service"></a><span data-ttu-id="a4f84-102">作法：建立交易式服務</span><span class="sxs-lookup"><span data-stu-id="a4f84-102">How to: Create a Transactional Service</span></span>

<span data-ttu-id="a4f84-103">這個範例示範建立異動式服務的各層面，以及使用用戶端初始化的異動以協調服務作業。</span><span class="sxs-lookup"><span data-stu-id="a4f84-103">This sample demonstrates various aspects of creating a transactional service and the use of a client-initiated transaction to coordinate service operations.</span></span>  
  
### <a name="creating-a-transactional-service"></a><span data-ttu-id="a4f84-104">建立交易式服務</span><span class="sxs-lookup"><span data-stu-id="a4f84-104">Creating a transactional service</span></span>  
  
1. <span data-ttu-id="a4f84-105">建立服務合約並使用 <xref:System.ServiceModel.TransactionFlowOption> 列舉的所需設定來標註作業，以指定傳入交易的需求。</span><span class="sxs-lookup"><span data-stu-id="a4f84-105">Create a service contract and annotate the operations with the desired setting from the <xref:System.ServiceModel.TransactionFlowOption> enumeration to specify the incoming transaction requirements.</span></span> <span data-ttu-id="a4f84-106">請注意，您也可以將 <xref:System.ServiceModel.TransactionFlowAttribute> 置於已實作的服務類別上。</span><span class="sxs-lookup"><span data-stu-id="a4f84-106">Note that you can also place the <xref:System.ServiceModel.TransactionFlowAttribute> on the service class being implemented.</span></span> <span data-ttu-id="a4f84-107">這可以讓介面的單一實作 (而不是每個實作) 使用這些異動設定。</span><span class="sxs-lookup"><span data-stu-id="a4f84-107">This allows for a single implementation of an interface to use these transaction settings, instead of every implementation.</span></span>  
  
    ```csharp
    [ServiceContract]  
    public interface ICalculator  
    {  
        [OperationContract]  
        // Use this to require an incoming transaction  
        [TransactionFlow(TransactionFlowOption.Mandatory)]  
        double Add(double n1, double n2);  
        [OperationContract]  
        // Use this to permit an incoming transaction  
        [TransactionFlow(TransactionFlowOption.Allowed)]  
        double Subtract(double n1, double n2);  
    }  
    ```  
  
2. <span data-ttu-id="a4f84-108">建立實作類別，然後使用 <xref:System.ServiceModel.ServiceBehaviorAttribute> 選擇性地指定 <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionIsolationLevel%2A> 和 <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionTimeout%2A>。</span><span class="sxs-lookup"><span data-stu-id="a4f84-108">Create an implementation class, and use the <xref:System.ServiceModel.ServiceBehaviorAttribute> to optionally specify a <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionIsolationLevel%2A> and a <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionTimeout%2A>.</span></span> <span data-ttu-id="a4f84-109">您應該注意到在許多案例中，<xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionTimeout%2A> 預設 60 秒以及 <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionIsolationLevel%2A> 預設 `Unspecified` 是適當的。</span><span class="sxs-lookup"><span data-stu-id="a4f84-109">You should note that in many cases, the default <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionTimeout%2A> of 60 seconds and the default <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionIsolationLevel%2A> of `Unspecified` are appropriate.</span></span> <span data-ttu-id="a4f84-110">針對每個作業，您可以使用 <xref:System.ServiceModel.OperationBehaviorAttribute> 屬性指定在方法內執行的工作，是否應該發生在根據 <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> 屬性值定義的異動範圍內。</span><span class="sxs-lookup"><span data-stu-id="a4f84-110">For each operation, you can use the <xref:System.ServiceModel.OperationBehaviorAttribute> attribute to specify whether work performed within the method should occur within the scope of a transaction scope according to the value of the <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> attribute.</span></span> <span data-ttu-id="a4f84-111">在此例中，`Add` 方法使用的異動與從用戶端流入的強制傳入異動相同，而且 `Subtract` 方法使用的異動會與傳入異動相同 (如果異動從用戶端流入)，或是與本機建立的新隱含異動相同。</span><span class="sxs-lookup"><span data-stu-id="a4f84-111">In this case, the transaction used for the `Add` method is the same as the mandatory incoming transaction that is flowed from the client, and the transaction used for the `Subtract` method is either the same as the incoming transaction if one was flowed from the client, or a new implicitly and locally created transaction.</span></span>  
  
    ```csharp
    [ServiceBehavior(  
        TransactionIsolationLevel = System.Transactions.IsolationLevel.Serializable,  
        TransactionTimeout = "00:00:45")]  
    public class CalculatorService : ICalculator  
    {  
        [OperationBehavior(TransactionScopeRequired = true)]  
        public double Add(double n1, double n2)  
        {  
            // Perform transactional operation  
            RecordToLog($"Adding {n1} to {n2}");
            return n1 + n2;  
        }  
  
        [OperationBehavior(TransactionScopeRequired = true)]  
        public double Subtract(double n1, double n2)  
        {  
            // Perform transactional operation  
            RecordToLog($"Subtracting {n2} from {n1}");
            return n1 - n2;  
        }  
  
        private static void RecordToLog(string recordText)  
        {  
            // Database operations omitted for brevity  
            // This is where the transaction provides specific benefit  
            // - changes to the database will be committed only when  
            // the transaction completes.  
        }  
    }  
    ```  
  
3. <span data-ttu-id="a4f84-112">在組態檔中設定繫結程序、指定應該流動的異動內容，以及要用來執行這些動作的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="a4f84-112">Configure the bindings in the configuration file, specifying that the transaction context should be flowed, and the protocols to be used to do so.</span></span> <span data-ttu-id="a4f84-113">如需詳細資訊，請參閱 [配置的交易](servicemodel-transaction-configuration.md)設定。</span><span class="sxs-lookup"><span data-stu-id="a4f84-113">For more information, see [ServiceModel Transaction Configuration](servicemodel-transaction-configuration.md).</span></span> <span data-ttu-id="a4f84-114">明確地說，在端點項目的 `binding` 屬性中會指定繫結類型。</span><span class="sxs-lookup"><span data-stu-id="a4f84-114">Specifically, the binding type is specified in the endpoint element’s `binding` attribute.</span></span> <span data-ttu-id="a4f84-115">[\<endpoint>](../../configure-apps/file-schema/wcf/endpoint-element.md)元素包含的 `bindingConfiguration` 屬性會參考名為的系結設定 `transactionalOleTransactionsTcpBinding` ，如下列範例設定所示。</span><span class="sxs-lookup"><span data-stu-id="a4f84-115">The [\<endpoint>](../../configure-apps/file-schema/wcf/endpoint-element.md) element contains a `bindingConfiguration` attribute that references a binding configuration named `transactionalOleTransactionsTcpBinding`, as shown in the following sample configuration.</span></span>  
  
    ```xml  
    <service name="CalculatorService">  
      <endpoint address="net.tcp://localhost:8008/CalcService"  
        binding="netTcpBinding"  
        bindingConfiguration="transactionalOleTransactionsTcpBinding"  
        contract="ICalculator"  
        name="OleTransactions_endpoint" />  
    </service>  
    ```  
  
     <span data-ttu-id="a4f84-116">藉由使用 `transactionFlow` 屬性能夠在組態層級啟用異動流程，而使用 `transactionProtocol` 屬性可以指定異動通訊協定，如同下列組態所示。</span><span class="sxs-lookup"><span data-stu-id="a4f84-116">Transaction flow is enabled at the configuration level by using the `transactionFlow` attribute, and the transaction protocol is specified using the `transactionProtocol` attribute, as shown in the following configuration.</span></span>  
  
    ```xml  
    <bindings>  
      <netTcpBinding>  
        <binding name="transactionalOleTransactionsTcpBinding"  
          transactionFlow="true"  
          transactionProtocol="OleTransactions"/>  
      </netTcpBinding>  
    </bindings>  
    ```  
  
### <a name="supporting-multiple-transaction-protocols"></a><span data-ttu-id="a4f84-117">支援多個交易通訊協定</span><span class="sxs-lookup"><span data-stu-id="a4f84-117">Supporting multiple transaction protocols</span></span>  
  
1. <span data-ttu-id="a4f84-118">為了達到最佳效能，您應該針對牽涉到使用 Windows Communication Foundation (WCF) 所撰寫之用戶端和服務的案例使用 OleTransactions 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="a4f84-118">For optimal performance, you should use the OleTransactions protocol for scenarios involving a client and service written using Windows Communication Foundation (WCF).</span></span> <span data-ttu-id="a4f84-119">但是，WS-AtomicTransaction (WS-AT) 通訊協定在需要協力廠商堆疊之互通性的案例中很有用。</span><span class="sxs-lookup"><span data-stu-id="a4f84-119">However, the WS-AtomicTransaction (WS-AT) protocol is useful for scenarios when interoperability with third-party protocol stacks is required.</span></span> <span data-ttu-id="a4f84-120">您可以使用適當的通訊協定特定系結來提供多個端點，以設定 WCF 服務接受這兩個通訊協定，如下列範例設定所示。</span><span class="sxs-lookup"><span data-stu-id="a4f84-120">You can configure WCF services to accept both protocols by providing multiple endpoints with appropriate protocol-specific bindings, as shown in the following sample configuration.</span></span>  
  
    ```xml  
    <service name="CalculatorService">  
      <endpoint address="http://localhost:8000/CalcService"  
        binding="wsHttpBinding"  
        bindingConfiguration="transactionalWsatHttpBinding"  
        contract="ICalculator"  
        name="WSAtomicTransaction_endpoint" />  
      <endpoint address="net.tcp://localhost:8008/CalcService"  
        binding="netTcpBinding"  
        bindingConfiguration="transactionalOleTransactionsTcpBinding"  
        contract="ICalculator"  
        name="OleTransactions_endpoint" />  
    </service>  
    ```  
  
     <span data-ttu-id="a4f84-121">使用 `transactionProtocol` 屬性可以指定異動通訊協定。</span><span class="sxs-lookup"><span data-stu-id="a4f84-121">The transaction protocol is specified using the `transactionProtocol` attribute.</span></span> <span data-ttu-id="a4f84-122">但是，系統提供的 `wsHttpBinding` 並沒有這個屬性，因為這個繫結只能夠使用 WS-AT 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="a4f84-122">However, this attribute is absent from the system-provided `wsHttpBinding`, because this binding can only use the WS-AT protocol.</span></span>  
  
    ```xml  
    <bindings>  
      <wsHttpBinding>  
        <binding name="transactionalWsatHttpBinding"  
          transactionFlow="true" />  
      </wsHttpBinding>  
      <netTcpBinding>  
        <binding name="transactionalOleTransactionsTcpBinding"  
          transactionFlow="true"  
          transactionProtocol="OleTransactions"/>  
      </netTcpBinding>  
    </bindings>  
    ```  
  
### <a name="controlling-the-completion-of-a-transaction"></a><span data-ttu-id="a4f84-123">控制交易完成</span><span class="sxs-lookup"><span data-stu-id="a4f84-123">Controlling the completion of a transaction</span></span>  
  
1. <span data-ttu-id="a4f84-124">根據預設，如果沒有擲回未處理的例外狀況，WCF 作業會自動完成交易。</span><span class="sxs-lookup"><span data-stu-id="a4f84-124">By default, WCF operations automatically complete transactions if no unhandled exceptions are thrown.</span></span> <span data-ttu-id="a4f84-125">您可以藉由使用 <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A> 屬性和 <xref:System.ServiceModel.OperationContext.SetTransactionComplete%2A> 方法修改這個行為。</span><span class="sxs-lookup"><span data-stu-id="a4f84-125">You can modify this behavior by using the <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A> property and the <xref:System.ServiceModel.OperationContext.SetTransactionComplete%2A> method.</span></span> <span data-ttu-id="a4f84-126">當作業需要發生在與其他作業相同的異動中 (例如，借貸作業) 時，您可以將 <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A> 屬性設定為 `false` 以停用自動完成行為，如同下列 `Debit` 作業範例所示。</span><span class="sxs-lookup"><span data-stu-id="a4f84-126">When an operation is required to occur within the same transaction as another operation (for example, a debit and credit operation), you can disable the autocomplete behavior by setting the <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A> property to `false` as shown in the following `Debit` operation example.</span></span> <span data-ttu-id="a4f84-127">在呼叫 `Debit` 屬性設定為 <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A> 的方法 (如同作業 `true` 中所示)，或是呼叫 `Credit1` 方法以明確標記異動完成 (如同作業 <xref:System.ServiceModel.OperationContext.SetTransactionComplete%2A> 中所示) 後，`Credit2` 作業使用的異動才完成。</span><span class="sxs-lookup"><span data-stu-id="a4f84-127">The transaction the `Debit` operation uses is not completed until a method with the <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A> property set to `true` is called, as shown in the operation `Credit1`, or when the <xref:System.ServiceModel.OperationContext.SetTransactionComplete%2A> method is called to explicitly mark the transaction as complete, as shown in the operation `Credit2`.</span></span> <span data-ttu-id="a4f84-128">請注意，這兩個貸款作業是為了示範目的，而單一貸款作業會更單純。</span><span class="sxs-lookup"><span data-stu-id="a4f84-128">Note that the two credit operations are shown for illustration purposes, and that a single credit operation would be more typical.</span></span>  
  
    ```csharp
    [ServiceBehavior]  
    public class CalculatorService : IAccount  
    {  
        [OperationBehavior(  
            TransactionScopeRequired = true, TransactionAutoComplete = false)]  
        public void Debit(double n)  
        {  
            // Perform debit operation  
  
            return;  
        }  
  
        [OperationBehavior(  
            TransactionScopeRequired = true, TransactionAutoComplete = true)]  
        public void Credit1(double n)  
        {  
            // Perform credit operation  
  
            return;  
        }  
  
        [OperationBehavior(  
            TransactionScopeRequired = true, TransactionAutoComplete = false)]  
        public void Credit2(double n)  
        {  
            // Perform alternate credit operation  
  
            OperationContext.Current.SetTransactionComplete();  
            return;  
        }  
    }  
    ```  
  
2. <span data-ttu-id="a4f84-129">為了交易相互關聯目的，將 <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A> 屬性設定為 `false` 需要使用工作階段繫結。</span><span class="sxs-lookup"><span data-stu-id="a4f84-129">For the purposes of transaction correlation, setting the <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A> property to `false` requires the use of a sessionful binding.</span></span> <span data-ttu-id="a4f84-130">`SessionMode` 的 <xref:System.ServiceModel.ServiceContractAttribute> 屬性會指定這項需求。</span><span class="sxs-lookup"><span data-stu-id="a4f84-130">This requirement is specified with the `SessionMode` property on the <xref:System.ServiceModel.ServiceContractAttribute>.</span></span>  
  
    ```csharp
    [ServiceContract(SessionMode = SessionMode.Required)]  
    public interface IAccount  
    {  
        [OperationContract]  
        [TransactionFlow(TransactionFlowOption.Allowed)]  
        void Debit(double n);  
        [OperationContract]  
        [TransactionFlow(TransactionFlowOption.Allowed)]  
        void Credit1(double n);  
        [OperationContract]  
        [TransactionFlow(TransactionFlowOption.Allowed)]  
        void Credit2(double n);  
    }  
    ```  
  
### <a name="controlling-the-lifetime-of-a-transactional-service-instance"></a><span data-ttu-id="a4f84-131">控制異動式服務執行個體的存留時間</span><span class="sxs-lookup"><span data-stu-id="a4f84-131">Controlling the lifetime of a transactional service instance</span></span>  
  
1. <span data-ttu-id="a4f84-132">WCF 使用 <xref:System.ServiceModel.ServiceBehaviorAttribute.ReleaseServiceInstanceOnTransactionComplete%2A> 屬性來指定是否要在交易完成時釋放基礎服務實例。</span><span class="sxs-lookup"><span data-stu-id="a4f84-132">WCF uses the <xref:System.ServiceModel.ServiceBehaviorAttribute.ReleaseServiceInstanceOnTransactionComplete%2A> property to specify whether the underlying service instance is released when a transaction completes.</span></span> <span data-ttu-id="a4f84-133">由於這預設為 `true` ，除非另外設定，否則 WCF 會展示有效率且可預測的「及時」啟用行為。</span><span class="sxs-lookup"><span data-stu-id="a4f84-133">Since this defaults to `true`, unless configured otherwise, WCF exhibits an efficient and predictable "just-in-time" activation behavior.</span></span> <span data-ttu-id="a4f84-134">呼叫後續交易的服務，可以確保新服務執行個體不會有之前交易狀態的殘餘資料。</span><span class="sxs-lookup"><span data-stu-id="a4f84-134">Calls to a service on a subsequent transaction are assured a new service instance with no remnants of the previous transaction's state.</span></span> <span data-ttu-id="a4f84-135">雖然這方法通常很有用，但是有時候您可能會想要在異動完成之外維護服務執行個體中的狀態。</span><span class="sxs-lookup"><span data-stu-id="a4f84-135">While this is often useful, sometimes you may want to maintain state within the service instance beyond the transaction completion.</span></span> <span data-ttu-id="a4f84-136">這種情況的範例是，當必要的狀態或資源控制代碼很難擷取或重組時。</span><span class="sxs-lookup"><span data-stu-id="a4f84-136">Examples of this would be when required state or handles to resources are expensive to retrieve or reconstitute.</span></span> <span data-ttu-id="a4f84-137">藉由將 <xref:System.ServiceModel.ServiceBehaviorAttribute.ReleaseServiceInstanceOnTransactionComplete%2A> 屬性設定為 `false`，您可以達到這個目的。</span><span class="sxs-lookup"><span data-stu-id="a4f84-137">You can do this by setting the <xref:System.ServiceModel.ServiceBehaviorAttribute.ReleaseServiceInstanceOnTransactionComplete%2A> property to `false`.</span></span> <span data-ttu-id="a4f84-138">使用這項設定時，後續呼叫就可以使用執行個體與任何關聯的狀態。</span><span class="sxs-lookup"><span data-stu-id="a4f84-138">With that setting, the instance and any associated state will be available on subsequent calls.</span></span> <span data-ttu-id="a4f84-139">當使用這項功能時，請特別考量清除與完成狀態及異動的時機與方式。</span><span class="sxs-lookup"><span data-stu-id="a4f84-139">When using this, give careful consideration to when and how state and transactions will be cleared and completed.</span></span> <span data-ttu-id="a4f84-140">下列範例示範如何使用 `runningTotal` 變數來維護執行個體以進行這項作業。</span><span class="sxs-lookup"><span data-stu-id="a4f84-140">The following sample demonstrates how to do this by maintaining the instance with the `runningTotal` variable.</span></span>  
  
    ```csharp
    [ServiceBehavior(TransactionIsolationLevel = [ServiceBehavior(  
        ReleaseServiceInstanceOnTransactionComplete = false)]  
    public class CalculatorService : ICalculator  
    {  
        double runningTotal = 0;  
  
        [OperationBehavior(TransactionScopeRequired = true)]  
        public double Add(double n)  
        {  
            // Perform transactional operation  
            RecordToLog($"Adding {n} to {runningTotal}");
            runningTotal = runningTotal + n;  
            return runningTotal;  
        }  
  
        [OperationBehavior(TransactionScopeRequired = true)]  
        public double Subtract(double n)  
        {  
            // Perform transactional operation  
            RecordToLog($"Subtracting {n} from {runningTotal}");
            runningTotal = runningTotal - n;  
            return runningTotal;  
        }  
  
        private static void RecordToLog(string recordText)  
        {  
            // Database operations omitted for brevity  
        }  
    }  
    ```  
  
    > [!NOTE]
    > <span data-ttu-id="a4f84-141">因為執行個體的存留時間是服務的內部行為，並且透過 <xref:System.ServiceModel.ServiceBehaviorAttribute> 屬性控制，所以不需要修改服務組態或服務合約來設定執行個體行為。</span><span class="sxs-lookup"><span data-stu-id="a4f84-141">Since the instance lifetime is a behavior that is internal to the service, and controlled through the <xref:System.ServiceModel.ServiceBehaviorAttribute> property, no modification to the service configuration or service contract is required to set the instance behavior.</span></span> <span data-ttu-id="a4f84-142">此外，網路中不會包含任何表示法。</span><span class="sxs-lookup"><span data-stu-id="a4f84-142">In addition, the wire will contain no representation of this.</span></span>
