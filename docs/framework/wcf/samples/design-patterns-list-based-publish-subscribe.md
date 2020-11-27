---
title: 設計模式：以清單為基礎的發行訂閱
ms.date: 03/30/2017
ms.assetid: f4257abc-12df-4736-a03b-0731becf0fd4
ms.openlocfilehash: 4e679980df8a720eb4aa22741bbdd067940c7723
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96292671"
---
# <a name="design-patterns-list-based-publish-subscribe"></a>設計模式：以清單為基礎的發行訂閱

此範例說明如何將以清單為基礎的 Publish-Subscribe 模式實作為 Windows Communication Foundation (WCF) 程式。  
  
> [!NOTE]
> 此範例的安裝程序與建置指示位於本主題的結尾。  
  
 以清單為基礎的 Publish-Subscribe 設計模式將在 Microsoft 模式中說明 & 實務的發行集、 [整合模式](/previous-versions/msp-n-p/ff647309(v=pandp.10))。 發行訂閱模式會傳遞資訊給已訂閱某個資訊主題的收件者集合。 以清單為基礎的發行訂閱會維護訂閱者的清單。 當有要分享的資訊時，清單上的每個訂閱者都會接獲一份複本。 這個範例示範動態的清單架構發行訂閱模式，用戶端可以視需要在這裡訂閱或取消訂閱。  
  
 以清單為基礎的發行訂閱範例是由用戶端、服務和資料來源程式所組成。 可以有一個以上的用戶端和一個以上的資料來源程式在其中執行。 用戶端會訂閱服務、接收通知和取消訂閱。 資料來源程式會將資訊傳送至服務，以供目前所有訂閱者分享。  
  
 在這個範例中，用戶端和資料來源是主控台程式 (.exe 檔案)，而服務是裝載於網際網路資訊服務 (IIS) 的程式庫 (.dll) 。 您可以在桌面上看見用戶端和資料來源活動。  
  
 服務會使用雙工通訊。 `ISampleContract` 服務合約會和 `ISampleClientCallback` 回呼合約配成一組。 服務會實作用戶端用來加入或離開訂閱者清單的訂閱與取消訂閱服務作業。 服務還會實作 `PublishPriceChange` 服務作業，資料來源程式將呼叫此作業以提供新資訊給服務。 用戶端程式會實作 `PriceChange` 服務作業，服務將呼叫此作業以通知所有訂閱者關於價格的變更。  
  
```csharp  
// Create a service contract and define the service operations.  
// NOTE: The service operations must be declared explicitly.  
[ServiceContract(SessionMode=SessionMode.Required,  
      CallbackContract=typeof(ISampleClientContract))]  
public interface ISampleContract  
{  
    [OperationContract(IsOneWay = false, IsInitiating=true)]  
    void Subscribe();  
    [OperationContract(IsOneWay = false, IsTerminating=true)]  
    void Unsubscribe();  
    [OperationContract(IsOneWay = true)]  
    void PublishPriceChange(string item, double price,
                                     double change);  
}  
  
public interface ISampleClientContract  
{  
    [OperationContract(IsOneWay = true)]  
    void PriceChange(string item, double price, double change);  
}  
```  
  
 服務會使用 .NET Framework 事件做為告知所有訂閱者新資訊的機制。 當用戶端呼叫訂閱以加入服務時，它會提供事件處理常式。 當用戶端離開時，則會從事件取消訂閱其事件處理常式。 當資料來源呼叫服務以報告價格變更時，服務會引發事件。 這會呼叫服務的每個執行個體 (每個已訂閱的用戶端各一個)，而促使其事件處理常式開始執行。 每個事件處理常式都會透過各自的回呼函式，傳遞資訊至其用戶端。  
  
```csharp
public class PriceChangeEventArgs : EventArgs  
    {  
        public string Item;  
        public double Price;  
        public double Change;  
    }  
  
    // The Service implementation implements your service contract.  
    [ServiceBehavior(InstanceContextMode=InstanceContextMode.PerSession)]  
    public class SampleService : ISampleContract  
    {  
        public static event PriceChangeEventHandler PriceChangeEvent;  
        public delegate void PriceChangeEventHandler(object sender, PriceChangeEventArgs e);  
  
        ISampleClientContract callback = null;  
  
        PriceChangeEventHandler priceChangeHandler = null;  
  
        //Clients call this service operation to subscribe.  
        //A price change event handler is registered for this client instance.  
  
        public void Subscribe()  
        {  
            callback = OperationContext.Current.GetCallbackChannel<ISampleClientContract>();  
            priceChangeHandler = new PriceChangeEventHandler(PriceChangeHandler);  
            PriceChangeEvent += priceChangeHandler;  
        }  
  
        //Clients call this service operation to unsubscribe.  
        //The previous price change event handler is unregistered.  
  
        public void Unsubscribe()  
        {  
            PriceChangeEvent -= priceChangeHandler;  
        }  
  
        //Information source clients call this service operation to report a price change.  
        //A price change event is raised. The price change event handlers for each subscriber will execute.  
  
        public void PublishPriceChange(string item, double price, double change)  
        {  
            PriceChangeEventArgs e = new PriceChangeEventArgs();  
            e.Item = item;  
            e.Price = price;  
            e.Change = change;  
            PriceChangeEvent(this, e);  
        }  
  
        //This event handler runs when a PriceChange event is raised.  
        //The client's PriceChange service operation is invoked to provide notification about the price change.  
  
        public void PriceChangeHandler(object sender, PriceChangeEventArgs e)  
        {  
            callback.PriceChange(e.Item, e.Price, e.Change);  
        }  
  
    }  
```  
  
 當您執行範例時，請啟動數個用戶端。 用戶端會訂閱服務， 然後執行資料來源程式，後者再將資訊傳送給服務。 服務則傳遞資訊給所有訂閱者。 您可以看見每個用戶端主控台上的活動，確認已收到資訊。 在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。  
  
### <a name="to-set-up-and-build-the-sample"></a>若要設定和建置範例  
  
1. 確定您已 [針對 Windows Communication Foundation 範例執行一次性安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2. 若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。  
  
### <a name="to-run-the-sample-on-the-same-machine"></a>若要在同一部機器上執行範例  
  
1. 藉由輸入下列位址，測試您是否可以使用瀏覽器來存取服務： `http://localhost/servicemodelsamples/service.svc` 。 確認頁面應該會顯示在回應中。  
  
2. 從 \client\bin 執行 Client.exe \\ ，從語言特定資料夾下。 用戶端活動會顯示在用戶端主控台視窗上。 啟動數個用戶端。  
  
3. 從 \datasource\bin 執行 Datasource.exe \\ ，從語言特定資料夾下。 資料來源活動會顯示在主控台視窗上。 一旦資料來源將資訊傳送至服務，服務就必須將它傳遞給每個用戶端。  
  
4. 如果用戶端、資料來源和服務程式無法通訊，請參閱 [WCF 範例的疑難排解提示](/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))。  
  
### <a name="to-run-the-sample-across-machines"></a>若要跨機器執行範例  
  
1. 設定服務機器：  
  
    1. 在服務機器上，建立一個名稱為 ServiceModelSamples 的虛擬目錄。 批次檔 Setupvroot.bat 從 [Windows Communication Foundation 範例的單次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md) 中，可以用來建立磁碟目錄與虛擬目錄。  
  
    2. 將服務程式檔案從 %SystemDrive%\Inetpub\wwwroot\servicemodelsamples 複製到服務機器上的 ServiceModelSamples 虛擬目錄。 請務必將檔案放在 \bin 目錄中。  
  
    3. 測試您是否能夠使用瀏覽器，從用戶端機器存取服務。  
  
2. 設定用戶端機器：  
  
    1. 將語言特定資料夾下 \client\bin\ 資料夾中的用戶端程式檔案複製到用戶端機器。  
  
    2. 在每個用戶端組態檔中，將端點定義的位址值變更成符合服務的新位址。 以位址中的完整網域名稱取代 "localhost" 的任何參考。  
  
3. 設定資料來源機器：  
  
    1. 將語言特定資料夾下 \datasource\bin\ 資料夾中的資料來源程式檔複製到資料來源機器中。  
  
    2. 在資料來源組態檔中，將端點定義的位址值變更成符合服務的新位址。 以位址中的完整網域名稱取代 "localhost" 的任何參考。  
  
4. 在用戶端機器上，從命令提示字元啟動 Client.exe。  
  
5. 在資料來源機器上，從命令提示字元啟動 Datasource.exe。  
  
> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> 如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Scenario\DesignPatterns/ListBasedPublishSubscribe`
