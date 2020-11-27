---
title: 傳輸：自訂跨 UDP 異動範例
ms.date: 03/30/2017
ms.assetid: 6cebf975-41bd-443e-9540-fd2463c3eb23
ms.openlocfilehash: 1a5b6afd7dc078b0e6e270888973b34a91bfdb9f
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96295661"
---
# <a name="transport-custom-transactions-over-udp-sample"></a>傳輸：自訂跨 UDP 異動範例

這個範例是以 Windows Communication Foundation (WCF) [傳輸](transport-extensibility.md)擴充性中的[傳輸： UDP](transport-udp.md)範例為基礎。 它會延伸 UDP 傳輸範例以支援自訂異動流程，並示範 <xref:System.ServiceModel.Channels.TransactionMessageProperty> 屬性的使用方式。  
  
## <a name="code-changes-in-the-udp-transport-sample"></a>變更 UDP 傳輸範例中的程式碼  

 為了示範交易流程，此範例變更了服務合約，讓 `ICalculatorContract` 可以要求 `CalculatorService.Add()` 的交易範圍。 範例還另外將 `System.Guid` 參數新增至 `Add` 作業的合約。 這個參數是用來將用戶端異動識別碼傳遞給服務。  
  
```csharp  
class CalculatorService : IDatagramContract, ICalculatorContract  
{  
    [OperationBehavior(TransactionScopeRequired=true)]  
    public int Add(int x, int y, Guid clientTransactionId)  
    {  
        if(Transaction.Current.TransactionInformation.DistributedIdentifier == clientTransactionId)  
    {  
        Console.WriteLine("The client transaction has flowed to the service");  
    }  
    else  
    {  
     Console.WriteLine("The client transaction has NOT flowed to the service");  
    }  
  
    Console.WriteLine("   adding {0} + {1}", x, y);
    return (x + y);  
    }  
  
    [...]  
}  
```  
  
 [Transport： UDP](transport-udp.md)範例會使用 udp 封包，在用戶端與服務之間傳遞訊息。 [傳輸：自訂傳輸範例](transport-custom-transactions-over-udp-sample.md)會使用相同的機制來傳輸訊息，但是當交易流動時，會將它與編碼的訊息一起插入 UDP 封包中。  
  
```csharp  
byte[] txmsgBuffer = TransactionMessageBuffer.WriteTransactionMessageBuffer(txPropToken, messageBuffer);  
  
int bytesSent = this.socket.SendTo(txmsgBuffer, 0, txmsgBuffer.Length, SocketFlags.None, this.remoteEndPoint);  
```  
  
 `TransactionMessageBuffer.WriteTransactionMessageBuffer` 是 Helper 方法，其中包含的新功能可以將目前交易的傳播權杖與訊息實體 (Entity) 合併，再將它放在緩衝區中。  
  
 針對自訂交易流程傳輸，用戶端必須知道哪些服務作業需要交易流程，並將此資訊傳遞至 WCF。 其中也必須有可以用來傳輸使用者交易至傳輸層的機制。 此範例會使用「WCF 訊息偵測器」來取得此資訊。 此處實作的用戶端訊息偵測器稱為 `TransactionFlowInspector`，它會執行下列工作：  
  
- 判斷交易是否必須針對指定的訊息動作流動 (這會在 `IsTxFlowRequiredForThisOperation()` 中進行)。  
  
- 在需要流動異動時，使用 `TransactionFlowProperty` 將目前環境異動附加至訊息 (這會在 `BeforeSendRequest()` 中完成)。  
  
```csharp  
public class TransactionFlowInspector : IClientMessageInspector  
{  
   void IClientMessageInspector.AfterReceiveReply(ref           System.ServiceModel.Channels.Message reply, object correlationState)  
  {  
  }  
  
   public object BeforeSendRequest(ref System.ServiceModel.Channels.Message request, System.ServiceModel.IClientChannel channel)  
   {  
       // obtain the tx propagation token  
       byte[] propToken = null;
       if (Transaction.Current != null && IsTxFlowRequiredForThisOperation(request.Headers.Action))  
       {  
           try  
           {  
               propToken = TransactionInterop.GetTransmitterPropagationToken(Transaction.Current);  
           }  
           catch (TransactionException e)  
           {  
              throw new CommunicationException("TransactionInterop.GetTransmitterPropagationToken failed.", e);  
           }  
       }  
  
      // set the propToken on the message in a TransactionFlowProperty  
       TransactionFlowProperty.Set(propToken, request);  
  
       return null;
    }  
  }  
  
  static bool IsTxFlowRequiredForThisOperation(String action)  
 {  
       // In general, this should contain logic to identify which operations (actions)      require transaction flow.  
      [...]  
 }  
}  
```  
  
 `TransactionFlowInspector` 本身是使用自訂行為 (`TransactionFlowBehavior`) 傳遞給架構。  
  
```csharp  
public class TransactionFlowBehavior : IEndpointBehavior  
{  
       public void AddBindingParameters(ServiceEndpoint endpoint,            System.ServiceModel.Channels.BindingParameterCollection bindingParameters)  
      {  
      }  
  
       public void ApplyClientBehavior(ServiceEndpoint endpoint, System.ServiceModel.Dispatcher.ClientRuntime clientRuntime)  
      {  
            TransactionFlowInspector inspector = new TransactionFlowInspector();  
            clientRuntime.MessageInspectors.Add(inspector);  
      }  
  
      public void ApplyDispatchBehavior(ServiceEndpoint endpoint, System.ServiceModel.Dispatcher.EndpointDispatcher endpointDispatcher)  
     {  
     }  
  
      public void Validate(ServiceEndpoint endpoint)  
      {  
      }  
}  
```  
  
 備妥前述機制之後，使用者程式碼會在呼叫服務作業之前建立 `TransactionScope`。 如果需要讓交易流動至服務作業，訊息偵測器可以確保交易傳遞給傳輸。  
  
```csharp  
CalculatorContractClient calculatorClient = new CalculatorContractClient("SampleProfileUdpBinding_ICalculatorContract");  
calculatorClient.Endpoint.Behaviors.Add(new TransactionFlowBehavior());
  
try  
{  
       for (int i = 0; i < 5; ++i)  
      {  
              // call the 'Add' service operation under a transaction scope  
             using (TransactionScope ts = new TransactionScope())  
             {  
        [...]  
        Console.WriteLine(calculatorClient.Add(i, i * 2));  
         }  
      }
       calculatorClient.Close();  
}  
catch (TimeoutException)  
{  
    calculatorClient.Abort();  
}  
catch (CommunicationException)  
{  
    calculatorClient.Abort();  
}  
catch (Exception)  
{  
    calculatorClient.Abort();  
    throw;  
}  
```  
  
 從用戶端收到 UDP 封包時，服務會將它還原序列化，以擷取訊息及可能的交易。  
  
```csharp  
count = listenSocket.EndReceiveFrom(result, ref dummy);  
  
// read the transaction and message                       TransactionMessageBuffer.ReadTransactionMessageBuffer(buffer, count, out transaction, out msg);  
```  
  
 `TransactionMessageBuffer.ReadTransactionMessageBuffer()` 是 Helper 方法，它會反轉 `TransactionMessageBuffer.WriteTransactionMessageBuffer()` 所執行的序列化 (Serialization) 程序。  
  
 如果有異動流入，就會將它附加至 `TransactionMessageProperty` 中的訊息。  
  
```csharp  
message = MessageEncoderFactory.Encoder.ReadMessage(msg, bufferManager);  
  
if (transaction != null)  
{  
       TransactionMessageProperty.Set(transaction, message);  
}  
```  
  
 這可以確保發送器在分派階段收到異動，且在呼叫訊息所定址的服務作業時使用此異動。  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>若要安裝、建置及執行範例  
  
1. 若要建立方案，請依照 [建立 Windows Communication Foundation 範例](building-the-samples.md)中的指示進行。  
  
2. 目前的範例應以與 [Transport： UDP](transport-udp.md) 範例類似的方式執行。 若要執行，請使用 UdpTestService.exe 啟動服務。 如果您執行的是 Windows Vista，則必須以較高的許可權啟動服務。 若要這樣做，請以滑鼠右鍵按一下檔案總管中的 UdpTestService.exe，然後按一下 [以 **系統管理員身分執行**]。  
  
3. 此程序產生以下輸出。  
  
    ```console  
    Testing Udp From Code.  
    Service is started from code...  
    Press <ENTER> to terminate the service and start service from config...  
    ```  
  
4. 此時，您可以執行 UdpTestClient.exe 以啟動用戶端。 用戶端所產生的輸出如下所示。  
  
    ```console
    0  
    3  
    6  
    9  
    12  
    Press <ENTER> to complete test.  
    ```  
  
5. 服務輸出如下。  
  
    ```console
    Hello, world!  
    Hello, world!  
    Hello, world!  
    Hello, world!  
    Hello, world!  
    The client transaction has flowed to the service  
       adding 0 + 0  
    The client transaction has flowed to the service  
       adding 1 + 2  
    The client transaction has flowed to the service  
       adding 2 + 4  
    The client transaction has flowed to the service  
       adding 3 + 6  
    The client transaction has flowed to the service  
       adding 4 + 8  
    ```  
  
6. 如果服務應用程式可以找到與用戶端傳送的異動識別碼 (在 `The client transaction has flowed to the service` 作業的 `clientTransactionId` 參數中傳送) 相符的服務異動識別碼，就會顯示`CalculatorService.Add()`訊息。 只有在用戶端異動已流至服務時，才能取得相符的異動識別項。  
  
7. 若要使用組態來對已發行的端點執行用戶端應用程式，請在服務應用程式視窗上按下 ENTER，然後再執行測試用戶端一次。 您應該會在服務上看見下列輸出。  
  
    ```console  
    Testing Udp From Config.  
    Service is started from config...  
    Press <ENTER> to terminate the service and exit...  
    ```  
  
8. 現在，針對服務執行用戶端，就會產生跟前面相似的輸出。  
  
9. 若要使用 Svcutil.exe 重新產生用戶端程式碼和組態，請啟動服務應用程式，然後從範例的根目錄執行下列 Svcutil.exe 命令。  
  
    ```console  
    svcutil http://localhost:8000/udpsample/ /reference:UdpTransport\bin\UdpTransport.dll /svcutilConfig:svcutil.exe.config  
    ```  
  
10. 請注意，Svcutil.exe 不會為 `sampleProfileUdpBinding` 產生繫結延伸組態，您必須以手動方式新增。  
  
    ```xml  
    <configuration>  
        <system.serviceModel>
            …  
            <extensions>  
                <!-- This was added manually because svcutil.exe does not add this extension to the file -->  
                <bindingExtensions>  
                    <add name="sampleProfileUdpBinding" type="Microsoft.ServiceModel.Samples.SampleProfileUdpBindingCollectionElement, UdpTransport" />  
                </bindingExtensions>  
            </extensions>  
        </system.serviceModel>  
    </configuration>  
    ```  
  
> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> 如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Transactions\TransactionMessagePropertyUDPTransport`  
  
## <a name="see-also"></a>另請參閱

- [傳輸：UDP](transport-udp.md)
