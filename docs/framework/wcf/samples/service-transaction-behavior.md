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
# <a name="service-transaction-behavior"></a>服務異動行為

這個範例會示範如何使用用戶端協調的異動，以及設定 ServiceBehaviorAttribute 和 OperationBehaviorAttribute，以控制服務異動行為。 這個範例是以實作為計算機服務的[消費者入門](getting-started-sample.md)為基礎，但是會擴充以維護資料庫資料表中所執行作業的伺服器記錄檔，以及計算機作業的具狀態運行總計。 對伺服器記錄資料表的持續性寫入會依用戶端協調的異動結果而定，如果用戶端異動沒有完成，Web 服務異動就會確保資料庫的更新並未經過認可。

> [!NOTE]
> 此範例的安裝程序與建置指示位於本主題的結尾。

服務的合約會定義所有作業都需要異動與要求一起流動：

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

為了啟用傳入交易流程，服務是以系統提供的 wsHttpBinding，搭配設定為 `true` 的 transactionFlow 屬性來設定。 這個繫結使用互通的 WSAtomicTransactionOctober2004 通訊協定：

```xml
<bindings>
  <wsHttpBinding>
    <binding name="transactionalBinding" transactionFlow="true" />
  </wsHttpBinding>
</bindings>
```

初始化服務和異動的連線之後，用戶端會存取該異動範圍內的數個服務作業，然後完成異動並關閉連線：

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

在服務上，有三個屬性會影響服務異動行為，而影響的方式如下：

- 在 `ServiceBehaviorAttribute` 上：

  - `TransactionTimeout` 屬性會指定異動必須完成的期間。 在這個範例中，此屬性設定為 30 秒。

  - `TransactionIsolationLevel` 屬性會指定服務支援的隔離等級。 這是比對用戶端隔離等級的必要項。

  - `ReleaseServiceInstanceOnTransactionComplete` 屬性會指定是否要在交易完成時回收服務執行個體。 設定為 `false` 時，服務會維護多個作業要求中的相同服務執行個體。 這是維護執行總數的必要項。 如果設定為 `true`，就會在每次完成動作之後產生新執行個體。

  - `TransactionAutoCompleteOnSessionClose` 屬性會指定是否要在工作階段關閉時完成未完成的異動。 將它設定為 `false` ，就需要個別作業將 <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete?displayProperty=nameWithType> 屬性設為 `true` 或，以明確要求呼叫 <xref:System.ServiceModel.OperationContext.SetTransactionComplete?displayProperty=nameWithType> 方法來完成交易。 這個範例會示範這兩種方法。

- 在 `ServiceContractAttribute` 上：

  - `SessionMode` 屬性會指定服務是否要將適當的要求與邏輯工作階段相互關聯。 由於這個服務包含 OperationBehaviorAttribute TransactionAutoComplete 屬性設定為 `false` 的作業 (Multiply 和 Divide)，因此必須指定 `SessionMode.Required`。 例如，Multiply 作業不會完成它的異動，而會透過使用 `SetTransactionComplete` 方法，依賴稍後的 Divide 呼叫來完成，因此服務必須能夠判斷這些作業正在相同的工作階段內進行。

- 在 `OperationBehaviorAttribute` 上：

  - `TransactionScopeRequired` 屬性會指定是否應該在交易範圍內執行作業的動作。 在這個範例的所有作業中，這都設定為 `true`，而且因為用戶端會將它的交易流動至所有作業，所以，此動作會在該用戶端交易的範圍內進行。

  - `TransactionAutoComplete` 屬性會指定是否自動完成方法執行所在的異動 (如果沒有發生未處理的例外狀況)。 如先前所述，Add 和 Subtract 作業的這個屬性設定為 `true`，但 Multiply 和 Divide 作業則是設定為 `false`。 Add 和 Subtract 作業會自動完成它們的動作，Divide 則會透過明確呼叫 `SetTransactionComplete` 方法來完成動作，Multiply 不會完成動作，而是需要稍後呼叫 (例如呼叫 Divide) 來完成動作。

屬性化服務實作如下所示：

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

當您執行範例時，作業要求和回應會顯示在用戶端主控台視窗中。 在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。

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

服務作業要求的記錄會顯示在服務的主控台視窗中。 在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。

```console
Press <ENTER> to terminate service.
Creating new service instance...
  Writing row 1 to database: Adding 100 to 0
  Writing row 2 to database: Subtracting 45 from 100
  Writing row 3 to database: Multiplying 55 by 9
  Writing row 4 to database: Dividing 495 by 15
```

請注意，除了持續計算執行總數以外，服務還會報告執行個體的建立動作 (這個範例建立一個執行個體)，並將作業要求記錄至資料庫。 由於所有要求都會流動用戶端的交易，若發生任何失敗而無法完成該交易，就會導致回復所有資料庫作業。 下列方式可以示範此情形：

- 註解 `tx.Complete`() 的用戶端呼叫並重新執行 - 這會使用戶端離開異動範圍，而不會完成它的異動。

- 註解 Divide 服務作業的呼叫 - 這會導致 Multiply 作業初始化的動作無法完成，最後用戶端的交易也因此而無法完成。

- 在用戶端異動範圍的任何地方擲回未處理的例外狀況 - 這同樣會令用戶端無法完成它的異動。

在上述情況中，最後的結果都是不會認可該範圍內執行的作業，而且不會增加保存至資料庫的資料列計數。

> [!NOTE]
> 在建置程序中，資料庫檔案會複製至 bin 資料夾。 您必須查看該資料庫檔案的複本，以觀察保存至記錄檔的資料列，而不是觀察 Visual Studio 專案中隨附的檔案。

### <a name="to-set-up-build-and-run-the-sample"></a>若要安裝、建置及執行範例

1. 確定您已安裝 SQL Server 2005 Express Edition 或 SQL Server 2005。 在服務的 App.config 檔案中，可能會設定資料庫 `connectionString`，或者可能將 appSettings 的 `usingSql` 值設定為 `false` 來停用資料庫互動。

2. 若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。

3. 若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。

如果您跨電腦執行範例，您必須設定 Microsoft 分散式交易協調器（MSDTC）以啟用網路交易流程，並使用 Wsatconfig.exe 工具來啟用 Windows Communication Foundation （WCF）交易網路支援。

### <a name="to-configure-the-microsoft-distributed-transaction-coordinator-msdtc-to-support-running-the-sample-across-machines"></a>若要設定 Microsoft Distributed Transaction Coordinator (MSDTC) 以支援跨電腦執行範例

1. 在服務電腦上，設定 MSDTC 以允許傳入網路交易。

    1. 在 [**開始**] 功能表中，依序流覽至 [**控制台**]、[系統**管理工具**] 和 [**元件服務**]。

    2. 以滑鼠右鍵按一下**我的電腦**，然後選取 [**屬性**]。

    3. 在 [ **MSDTC** ] 索引標籤上，按一下 [**安全性**設定]。

    4. 檢查**網路 DTC 存取**並**允許輸入**。

    5. 按一下 **[是]** 以重新開機 MS DTC 服務，然後按一下 **[確定]**。

    6. 按一下 [確定]  關閉對話方塊。

2. 在服務電腦和用戶端電腦上，設定 [Windows 防火牆] 將 Microsoft Distributed Transaction Coordinator (MSDTC) 加入預期應用程式清單中：

    1. 從 [控制台] 執行 [Windows 防火牆] 應用程式。

    2. 在 [**例外**狀況] 索引標籤上，按一下 [**新增程式**]。

    3. 瀏覽至資料夾 C:\WINDOWS\System32。

    4. 選取 [Msdtc]，然後按一下 [**開啟**]。

    5. 按一下 **[確定**] 以關閉 [**新增程式**] 對話方塊，然後再按一下 **[確定]** 以關閉 Windows 防火牆小程式。

3. 在用戶端電腦上，設定 MSDTC 以允許傳出網路交易：

    1. 在 [**開始**] 功能表中，依序流覽至 [**控制台**]、[系統**管理工具**] 和 [**元件服務**]。

    2. 以滑鼠右鍵按一下**我的電腦**，然後選取 [**屬性**]。

    3. 在 [ **MSDTC** ] 索引標籤上，按一下 [**安全性**設定]。

    4. 檢查 [**網路 DTC 存取**] 和 [**允許輸出**]。

    5. 按一下 **[是]** 以重新開機 MS DTC 服務，然後按一下 **[確定]**。

    6. 按一下 [確定]  關閉對話方塊。

> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Behaviors\Transactions`
