---
title: 服務異動行為
ms.date: 03/30/2017
helpviewer_keywords:
- Service Transaction Behavior Sample [Windows Communication Foundation]
ms.assetid: 1a9842a3-e84d-427c-b6ac-6999cbbc2612
ms.openlocfilehash: 0be5bf0dbe6416febb898fb5150c5a516c8b0969
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84591523"
---
# <a name="service-transaction-behavior"></a><span data-ttu-id="dbc89-102">服務異動行為</span><span class="sxs-lookup"><span data-stu-id="dbc89-102">Service Transaction Behavior</span></span>

<span data-ttu-id="dbc89-103">這個範例會示範如何使用用戶端協調的異動，以及設定 ServiceBehaviorAttribute 和 OperationBehaviorAttribute，以控制服務異動行為。</span><span class="sxs-lookup"><span data-stu-id="dbc89-103">This sample demonstrates the use of a client-coordinated transaction and the settings of ServiceBehaviorAttribute and OperationBehaviorAttribute to control service transaction behavior.</span></span> <span data-ttu-id="dbc89-104">這個範例是以實作為計算機服務的[消費者入門](getting-started-sample.md)為基礎，但是會擴充以維護資料庫資料表中所執行作業的伺服器記錄檔，以及計算機作業的具狀態運行總計。</span><span class="sxs-lookup"><span data-stu-id="dbc89-104">This sample is based on the [Getting Started](getting-started-sample.md) that implements a calculator service, but is extended to maintain a server log of the performed operations in a database table and a stateful running total for the calculator operations.</span></span> <span data-ttu-id="dbc89-105">對伺服器記錄資料表的持續性寫入會依用戶端協調的異動結果而定，如果用戶端異動沒有完成，Web 服務異動就會確保資料庫的更新並未經過認可。</span><span class="sxs-lookup"><span data-stu-id="dbc89-105">Persisted writes to the server log table are dependent upon the outcome of a client coordinated transaction - if the client transaction does not complete, the Web service transaction ensures that the updates to the database are not committed.</span></span>

> [!NOTE]
> <span data-ttu-id="dbc89-106">此範例的安裝程序與建置指示位於本主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="dbc89-106">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>

<span data-ttu-id="dbc89-107">服務的合約會定義所有作業都需要異動與要求一起流動：</span><span class="sxs-lookup"><span data-stu-id="dbc89-107">The contract for the service defines that all of the operations require a transaction to be flowed with requests:</span></span>

```csharp
[ServiceContract(Namespace = "http://Microsoft.ServiceModel.Samples",
                    SessionMode = SessionMode.Required)]
public interface ICalculator
{
    [OperationContract]
    [TransactionFlow(TransactionFlowOption.Mandatory)]
    double Add(double n);
    [OperationContract]
    [TransactionFlow(TransactionFlowOption.Mandatory)]
    double Subtract(double n);
    [OperationContract]
    [TransactionFlow(TransactionFlowOption.Mandatory)]
    double Multiply(double n);
    [OperationContract]
    [TransactionFlow(TransactionFlowOption.Mandatory)]
    double Divide(double n);
}
```

<span data-ttu-id="dbc89-108">為了啟用傳入交易流程，服務是以系統提供的 wsHttpBinding，搭配設定為 `true` 的 transactionFlow 屬性來設定。</span><span class="sxs-lookup"><span data-stu-id="dbc89-108">To enable the incoming transaction flow, the service is configured with the system-provided wsHttpBinding with the transactionFlow attribute set to `true`.</span></span> <span data-ttu-id="dbc89-109">這個繫結使用互通的 WSAtomicTransactionOctober2004 通訊協定：</span><span class="sxs-lookup"><span data-stu-id="dbc89-109">This binding uses the interoperable WSAtomicTransactionOctober2004 protocol:</span></span>

```xml
<bindings>
  <wsHttpBinding>
    <binding name="transactionalBinding" transactionFlow="true" />
  </wsHttpBinding>
</bindings>
```

<span data-ttu-id="dbc89-110">初始化服務和異動的連線之後，用戶端會存取該異動範圍內的數個服務作業，然後完成異動並關閉連線：</span><span class="sxs-lookup"><span data-stu-id="dbc89-110">After initiating both a connection to the service and a transaction, the client accesses several service operations within the scope of that transaction and then completes the transaction and closes the connection:</span></span>

```csharp
// Create a client
CalculatorClient client = new CalculatorClient();

// Create a transaction scope with the default isolation level of Serializable
using (TransactionScope tx = new TransactionScope())
{
    Console.WriteLine("Starting transaction");

    // Call the Add service operation.
    double value = 100.00D;
    Console.WriteLine("  Adding {0}, running total={1}",
                                        value, client.Add(value));

    // Call the Subtract service operation.
    value = 45.00D;
    Console.WriteLine("  Subtracting {0}, running total={1}",
                                        value, client.Subtract(value));

    // Call the Multiply service operation.
    value = 9.00D;
    Console.WriteLine("  Multiplying by {0}, running total={1}",
                                        value, client.Multiply(value));

    // Call the Divide service operation.
    value = 15.00D;
    Console.WriteLine("  Dividing by {0}, running total={1}",
                                        value, client.Divide(value));

    Console.WriteLine("  Completing transaction");
    tx.Complete();
}

Console.WriteLine("Transaction committed");

// Closing the client gracefully closes the connection and cleans up resources
client.Close();
```

<span data-ttu-id="dbc89-111">在服務上，有三個屬性會影響服務異動行為，而影響的方式如下：</span><span class="sxs-lookup"><span data-stu-id="dbc89-111">On the service, there are three attributes that affect the service transaction behavior, and they do so in the following ways:</span></span>

- <span data-ttu-id="dbc89-112">在 `ServiceBehaviorAttribute` 上：</span><span class="sxs-lookup"><span data-stu-id="dbc89-112">On the `ServiceBehaviorAttribute`:</span></span>

  - <span data-ttu-id="dbc89-113">`TransactionTimeout` 屬性會指定異動必須完成的期間。</span><span class="sxs-lookup"><span data-stu-id="dbc89-113">The `TransactionTimeout` property specifies the time period within which a transaction must complete.</span></span> <span data-ttu-id="dbc89-114">在這個範例中，此屬性設定為 30 秒。</span><span class="sxs-lookup"><span data-stu-id="dbc89-114">In this sample it is set to 30 seconds.</span></span>

  - <span data-ttu-id="dbc89-115">`TransactionIsolationLevel` 屬性會指定服務支援的隔離等級。</span><span class="sxs-lookup"><span data-stu-id="dbc89-115">The `TransactionIsolationLevel` property specifies the isolation level that the service supports.</span></span> <span data-ttu-id="dbc89-116">這是比對用戶端隔離等級的必要項。</span><span class="sxs-lookup"><span data-stu-id="dbc89-116">This is required to match the client's isolation level.</span></span>

  - <span data-ttu-id="dbc89-117">`ReleaseServiceInstanceOnTransactionComplete` 屬性會指定是否要在交易完成時回收服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="dbc89-117">The `ReleaseServiceInstanceOnTransactionComplete` property specifies whether the service instance is recycled when a transaction completes.</span></span> <span data-ttu-id="dbc89-118">設定為 `false` 時，服務會維護多個作業要求中的相同服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="dbc89-118">By setting it to `false`, the service maintains the same service instance across the operation requests.</span></span> <span data-ttu-id="dbc89-119">這是維護執行總數的必要項。</span><span class="sxs-lookup"><span data-stu-id="dbc89-119">This is required to maintain the running total.</span></span> <span data-ttu-id="dbc89-120">如果設定為 `true`，就會在每次完成動作之後產生新執行個體。</span><span class="sxs-lookup"><span data-stu-id="dbc89-120">If set to `true`, a new instance is generated after each completed action.</span></span>

  - <span data-ttu-id="dbc89-121">`TransactionAutoCompleteOnSessionClose` 屬性會指定是否要在工作階段關閉時完成未完成的異動。</span><span class="sxs-lookup"><span data-stu-id="dbc89-121">The `TransactionAutoCompleteOnSessionClose` property specifies whether outstanding transactions are completed when the session closes.</span></span> <span data-ttu-id="dbc89-122">將它設定為 `false` ，就需要個別作業將 <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete?displayProperty=nameWithType> 屬性設為 `true` 或，以明確要求呼叫 <xref:System.ServiceModel.OperationContext.SetTransactionComplete?displayProperty=nameWithType> 方法來完成交易。</span><span class="sxs-lookup"><span data-stu-id="dbc89-122">By setting it to `false`, the individual operations are required to either set the <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete?displayProperty=nameWithType> property to `true` or to explicitly require a call to the <xref:System.ServiceModel.OperationContext.SetTransactionComplete?displayProperty=nameWithType> method to complete transactions.</span></span> <span data-ttu-id="dbc89-123">這個範例會示範這兩種方法。</span><span class="sxs-lookup"><span data-stu-id="dbc89-123">This sample demonstrates both approaches.</span></span>

- <span data-ttu-id="dbc89-124">在 `ServiceContractAttribute` 上：</span><span class="sxs-lookup"><span data-stu-id="dbc89-124">On the `ServiceContractAttribute`:</span></span>

  - <span data-ttu-id="dbc89-125">`SessionMode` 屬性會指定服務是否要將適當的要求與邏輯工作階段相互關聯。</span><span class="sxs-lookup"><span data-stu-id="dbc89-125">The `SessionMode` property specifies whether the service correlates the appropriate requests into a logical session.</span></span> <span data-ttu-id="dbc89-126">由於這個服務包含 OperationBehaviorAttribute TransactionAutoComplete 屬性設定為 `false` 的作業 (Multiply 和 Divide)，因此必須指定 `SessionMode.Required`。</span><span class="sxs-lookup"><span data-stu-id="dbc89-126">Because this service includes operations where the OperationBehaviorAttribute TransactionAutoComplete property is set to `false` (Multiply and Divide), `SessionMode.Required` must be specified.</span></span> <span data-ttu-id="dbc89-127">例如，Multiply 作業不會完成它的異動，而會透過使用 `SetTransactionComplete` 方法，依賴稍後的 Divide 呼叫來完成，因此服務必須能夠判斷這些作業正在相同的工作階段內進行。</span><span class="sxs-lookup"><span data-stu-id="dbc89-127">For example, the Multiply operation does not complete its transaction and instead relies upon a later call to Divide to complete using the `SetTransactionComplete` method; the service must be able to determine that these operations are occurring within the same session.</span></span>

- <span data-ttu-id="dbc89-128">在 `OperationBehaviorAttribute` 上：</span><span class="sxs-lookup"><span data-stu-id="dbc89-128">On the `OperationBehaviorAttribute`:</span></span>

  - <span data-ttu-id="dbc89-129">`TransactionScopeRequired` 屬性會指定是否應該在交易範圍內執行作業的動作。</span><span class="sxs-lookup"><span data-stu-id="dbc89-129">The `TransactionScopeRequired` property specifies whether the operation's actions should be executed within a transaction scope.</span></span> <span data-ttu-id="dbc89-130">在這個範例的所有作業中，這都設定為 `true`，而且因為用戶端會將它的交易流動至所有作業，所以，此動作會在該用戶端交易的範圍內進行。</span><span class="sxs-lookup"><span data-stu-id="dbc89-130">This is set to `true` for all operations in this sample and, because the client flows its transaction to all operations, the actions occur within the scope of that client transaction.</span></span>

  - <span data-ttu-id="dbc89-131">`TransactionAutoComplete` 屬性會指定是否自動完成方法執行所在的異動 (如果沒有發生未處理的例外狀況)。</span><span class="sxs-lookup"><span data-stu-id="dbc89-131">The `TransactionAutoComplete` property specifies whether the transaction in which the method executes is automatically completed if no unhandled exceptions occur.</span></span> <span data-ttu-id="dbc89-132">如先前所述，Add 和 Subtract 作業的這個屬性設定為 `true`，但 Multiply 和 Divide 作業則是設定為 `false`。</span><span class="sxs-lookup"><span data-stu-id="dbc89-132">As previously described, this is set to `true` for the Add and Subtract operations but `false` for the Multiply and Divide operations.</span></span> <span data-ttu-id="dbc89-133">Add 和 Subtract 作業會自動完成它們的動作，Divide 則會透過明確呼叫 `SetTransactionComplete` 方法來完成動作，Multiply 不會完成動作，而是需要稍後呼叫 (例如呼叫 Divide) 來完成動作。</span><span class="sxs-lookup"><span data-stu-id="dbc89-133">The Add and Subtract operations complete their actions automatically, the Divide completes its actions through an explicit call to the `SetTransactionComplete` method, and the Multiply does not complete its actions but instead relies upon and requires a later call, such as to Divide, to complete the actions.</span></span>

<span data-ttu-id="dbc89-134">屬性化服務實作如下所示：</span><span class="sxs-lookup"><span data-stu-id="dbc89-134">The attributed service implementation is as follows:</span></span>

```csharp
[ServiceBehavior(
    TransactionIsolationLevel = System.Transactions.IsolationLevel.Serializable,
    TransactionTimeout = "00:00:30",
    ReleaseServiceInstanceOnTransactionComplete = false,
    TransactionAutoCompleteOnSessionClose = false)]
public class CalculatorService : ICalculator
{
    double runningTotal;

    public CalculatorService()
    {
        Console.WriteLine("Creating new service instance...");
    }

    [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = true)]
    public double Add(double n)
    {
        RecordToLog(String.Format(CultureInfo.CurrentCulture, "Adding {0} to {1}", n, runningTotal));
        runningTotal = runningTotal + n;
        return runningTotal;
    }

    [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = true)]
    public double Subtract(double n)
    {
        RecordToLog(String.Format(CultureInfo.CurrentCulture, "Subtracting {0} from {1}", n, runningTotal));
        runningTotal = runningTotal - n;
        return runningTotal;
    }

    [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = false)]
    public double Multiply(double n)
    {
        RecordToLog(String.Format(CultureInfo.CurrentCulture, "Multiplying {0} by {1}", runningTotal, n));
        runningTotal = runningTotal * n;
        return runningTotal;
    }

    [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = false)]
    public double Divide(double n)
    {
        RecordToLog(String.Format(CultureInfo.CurrentCulture, "Dividing {0} by {1}", runningTotal, n));
        runningTotal = runningTotal / n;
        OperationContext.Current.SetTransactionComplete();
        return runningTotal;
    }

    // Logging method omitted for brevity
}
```

<span data-ttu-id="dbc89-135">當您執行範例時，作業要求和回應會顯示在用戶端主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="dbc89-135">When you run the sample, the operation requests and responses are displayed in the client console window.</span></span> <span data-ttu-id="dbc89-136">在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。</span><span class="sxs-lookup"><span data-stu-id="dbc89-136">Press ENTER in the client window to shut down the client.</span></span>

```console
Starting transaction
Performing calculations...
  Adding 100, running total=100
  Subtracting 45, running total=55
  Multiplying by 9, running total=495
  Dividing by 15, running total=33
  Completing transaction
Transaction committed
Press <ENTER> to terminate client.
```

<span data-ttu-id="dbc89-137">服務作業要求的記錄會顯示在服務的主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="dbc89-137">The logging of the service operation requests are displayed in the service's console window.</span></span> <span data-ttu-id="dbc89-138">在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。</span><span class="sxs-lookup"><span data-stu-id="dbc89-138">Press ENTER in the client window to shut down the client.</span></span>

```console
Press <ENTER> to terminate service.
Creating new service instance...
  Writing row 1 to database: Adding 100 to 0
  Writing row 2 to database: Subtracting 45 from 100
  Writing row 3 to database: Multiplying 55 by 9
  Writing row 4 to database: Dividing 495 by 15
```

<span data-ttu-id="dbc89-139">請注意，除了持續計算執行總數以外，服務還會報告執行個體的建立動作 (這個範例建立一個執行個體)，並將作業要求記錄至資料庫。</span><span class="sxs-lookup"><span data-stu-id="dbc89-139">Note that in addition to keeping the running total of the calculations, the service reports the creation of instances (one instance for this sample) and logs the operation requests to a database.</span></span> <span data-ttu-id="dbc89-140">由於所有要求都會流動用戶端的交易，若發生任何失敗而無法完成該交易，就會導致回復所有資料庫作業。</span><span class="sxs-lookup"><span data-stu-id="dbc89-140">Because all of the requests flow the client's transaction, any failure to complete that transaction results in all of the database operations being rolled back.</span></span> <span data-ttu-id="dbc89-141">下列方式可以示範此情形：</span><span class="sxs-lookup"><span data-stu-id="dbc89-141">This can be demonstrated in a number of ways:</span></span>

- <span data-ttu-id="dbc89-142">註解 `tx.Complete`() 的用戶端呼叫並重新執行 - 這會使用戶端離開異動範圍，而不會完成它的異動。</span><span class="sxs-lookup"><span data-stu-id="dbc89-142">Comment out the client's call to `tx.Complete`() and rerun - this results in the client exiting the transaction scope without completing its transaction.</span></span>

- <span data-ttu-id="dbc89-143">註解 Divide 服務作業的呼叫 - 這會導致 Multiply 作業初始化的動作無法完成，最後用戶端的交易也因此而無法完成。</span><span class="sxs-lookup"><span data-stu-id="dbc89-143">Comment out the call to the Divide service operation - this results prevent the action initiated by the Multiply operation from completing and thus the client's transaction ultimately also fails to complete.</span></span>

- <span data-ttu-id="dbc89-144">在用戶端異動範圍的任何地方擲回未處理的例外狀況 - 這同樣會令用戶端無法完成它的異動。</span><span class="sxs-lookup"><span data-stu-id="dbc89-144">Throw an unhandled exception anywhere in the client's transaction scope - this similarly prevents the client from completing its transaction.</span></span>

<span data-ttu-id="dbc89-145">在上述情況中，最後的結果都是不會認可該範圍內執行的作業，而且不會增加保存至資料庫的資料列計數。</span><span class="sxs-lookup"><span data-stu-id="dbc89-145">The result of any of these is that none of the operations performed within that scope are committed and the count of rows persisted to the database do not increment.</span></span>

> [!NOTE]
> <span data-ttu-id="dbc89-146">在建置程序中，資料庫檔案會複製至 bin 資料夾。</span><span class="sxs-lookup"><span data-stu-id="dbc89-146">As part of the build process the database file is copied to the bin folder.</span></span> <span data-ttu-id="dbc89-147">您必須查看該資料庫檔案的複本，以觀察保存至記錄檔的資料列，而不是觀察 Visual Studio 專案中隨附的檔案。</span><span class="sxs-lookup"><span data-stu-id="dbc89-147">You must look at that copy of the database file to observe the rows that are persisted to the log rather than the file that is included in the Visual Studio project.</span></span>

### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="dbc89-148">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="dbc89-148">To set up, build, and run the sample</span></span>

1. <span data-ttu-id="dbc89-149">確定您已安裝 SQL Server 2005 Express Edition 或 SQL Server 2005。</span><span class="sxs-lookup"><span data-stu-id="dbc89-149">Ensure that you have installed SQL Server 2005 Express Edition or SQL Server 2005.</span></span> <span data-ttu-id="dbc89-150">在服務的 App.config 檔案中，可能會設定資料庫 `connectionString`，或者可能將 appSettings 的 `usingSql` 值設定為 `false` 來停用資料庫互動。</span><span class="sxs-lookup"><span data-stu-id="dbc89-150">In the service's App.config file, the database `connectionString` may be set or the database interactions may be disabled by setting the appSettings `usingSql` value to `false`.</span></span>

2. <span data-ttu-id="dbc89-151">若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="dbc89-151">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>

3. <span data-ttu-id="dbc89-152">若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="dbc89-152">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>

<span data-ttu-id="dbc89-153">如果您跨電腦執行範例，您必須設定 Microsoft 分散式交易協調器（MSDTC）以啟用網路交易流程，並使用 Wsatconfig.exe 工具來啟用 Windows Communication Foundation （WCF）交易網路支援。</span><span class="sxs-lookup"><span data-stu-id="dbc89-153">If you run the sample across machines, you must configure the Microsoft Distributed Transaction Coordinator (MSDTC) to enable network transaction flow and use the WsatConfig.exe tool to enable Windows Communication Foundation (WCF) transactions network support.</span></span>

### <a name="to-configure-the-microsoft-distributed-transaction-coordinator-msdtc-to-support-running-the-sample-across-machines"></a><span data-ttu-id="dbc89-154">若要設定 Microsoft Distributed Transaction Coordinator (MSDTC) 以支援跨電腦執行範例</span><span class="sxs-lookup"><span data-stu-id="dbc89-154">To configure the Microsoft Distributed Transaction Coordinator (MSDTC) to support running the sample across machines</span></span>

1. <span data-ttu-id="dbc89-155">在服務電腦上，設定 MSDTC 以允許傳入網路交易。</span><span class="sxs-lookup"><span data-stu-id="dbc89-155">On the service machine, configure MSDTC to allow incoming network transactions.</span></span>

    1. <span data-ttu-id="dbc89-156">在 [**開始**] 功能表中，依序流覽至 [**控制台**]、[系統**管理工具**] 和 [**元件服務**]。</span><span class="sxs-lookup"><span data-stu-id="dbc89-156">From the **Start** menu, navigate to **Control Panel**, then **Administrative Tools**, and then **Component Services**.</span></span>

    2. <span data-ttu-id="dbc89-157">以滑鼠右鍵按一下**我的電腦**，然後選取 [**屬性**]。</span><span class="sxs-lookup"><span data-stu-id="dbc89-157">Right-click **My Computer** and select **Properties**.</span></span>

    3. <span data-ttu-id="dbc89-158">在 [ **MSDTC** ] 索引標籤上，按一下 [**安全性**設定]。</span><span class="sxs-lookup"><span data-stu-id="dbc89-158">On the **MSDTC** tab, click **Security Configuration**.</span></span>

    4. <span data-ttu-id="dbc89-159">檢查**網路 DTC 存取**並**允許輸入**。</span><span class="sxs-lookup"><span data-stu-id="dbc89-159">Check **Network DTC Access** and **Allow Inbound**.</span></span>

    5. <span data-ttu-id="dbc89-160">按一下 **[是]** 以重新開機 MS DTC 服務，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="dbc89-160">Click **Yes** to restart the MS DTC service and then click **OK**.</span></span>

    6. <span data-ttu-id="dbc89-161">按一下 [確定]  關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="dbc89-161">Click **OK** to close the dialog box.</span></span>

2. <span data-ttu-id="dbc89-162">在服務電腦和用戶端電腦上，設定 [Windows 防火牆] 將 Microsoft Distributed Transaction Coordinator (MSDTC) 加入預期應用程式清單中：</span><span class="sxs-lookup"><span data-stu-id="dbc89-162">On the service machine and the client machine, configure the Windows Firewall to include the Microsoft Distributed Transaction Coordinator (MSDTC) to the list of excepted applications:</span></span>

    1. <span data-ttu-id="dbc89-163">從 [控制台] 執行 [Windows 防火牆] 應用程式。</span><span class="sxs-lookup"><span data-stu-id="dbc89-163">Run the Windows Firewall application from Control Panel.</span></span>

    2. <span data-ttu-id="dbc89-164">在 [**例外**狀況] 索引標籤上，按一下 [**新增程式**]。</span><span class="sxs-lookup"><span data-stu-id="dbc89-164">From the **Exceptions** tab, click **Add Program**.</span></span>

    3. <span data-ttu-id="dbc89-165">瀏覽至資料夾 C:\WINDOWS\System32。</span><span class="sxs-lookup"><span data-stu-id="dbc89-165">Browse to the folder C:\WINDOWS\System32.</span></span>

    4. <span data-ttu-id="dbc89-166">選取 [Msdtc]，然後按一下 [**開啟**]。</span><span class="sxs-lookup"><span data-stu-id="dbc89-166">Select Msdtc.exe and click **Open**.</span></span>

    5. <span data-ttu-id="dbc89-167">按一下 **[確定**] 以關閉 [**新增程式**] 對話方塊，然後再按一下 **[確定]** 以關閉 Windows 防火牆小程式。</span><span class="sxs-lookup"><span data-stu-id="dbc89-167">Click **OK** to close the **Add Program** dialog box, and click **OK** again to close the Windows Firewall applet.</span></span>

3. <span data-ttu-id="dbc89-168">在用戶端電腦上，設定 MSDTC 以允許傳出網路交易：</span><span class="sxs-lookup"><span data-stu-id="dbc89-168">On the client machine, configure MSDTC to allow outgoing network transactions:</span></span>

    1. <span data-ttu-id="dbc89-169">在 [**開始**] 功能表中，依序流覽至 [**控制台**]、[系統**管理工具**] 和 [**元件服務**]。</span><span class="sxs-lookup"><span data-stu-id="dbc89-169">From the **Start** menu, navigate to **Control Panel**, then **Administrative Tools**, and then **Component Services**.</span></span>

    2. <span data-ttu-id="dbc89-170">以滑鼠右鍵按一下**我的電腦**，然後選取 [**屬性**]。</span><span class="sxs-lookup"><span data-stu-id="dbc89-170">Right-click **My Computer** and select **Properties**.</span></span>

    3. <span data-ttu-id="dbc89-171">在 [ **MSDTC** ] 索引標籤上，按一下 [**安全性**設定]。</span><span class="sxs-lookup"><span data-stu-id="dbc89-171">On the **MSDTC** tab, click **Security Configuration**.</span></span>

    4. <span data-ttu-id="dbc89-172">檢查 [**網路 DTC 存取**] 和 [**允許輸出**]。</span><span class="sxs-lookup"><span data-stu-id="dbc89-172">Check **Network DTC Access** and **Allow Outbound**.</span></span>

    5. <span data-ttu-id="dbc89-173">按一下 **[是]** 以重新開機 MS DTC 服務，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="dbc89-173">Click **Yes** to restart the MS DTC service and then click **OK**.</span></span>

    6. <span data-ttu-id="dbc89-174">按一下 [確定]  關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="dbc89-174">Click **OK** to close the dialog box.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dbc89-175">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="dbc89-175">The samples may already be installed on your machine.</span></span> <span data-ttu-id="dbc89-176">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="dbc89-176">Check for the following (default) directory before continuing.</span></span>
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> <span data-ttu-id="dbc89-177">如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="dbc89-177">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="dbc89-178">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="dbc89-178">This sample is located in the following directory.</span></span>
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Behaviors\Transactions`
