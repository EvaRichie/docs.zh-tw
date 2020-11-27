---
title: 使用 Windows 市集用戶端應用程式存取 WCF 服務
ms.date: 03/30/2017
ms.assetid: e2002ef4-5dee-4a54-9d87-03b33d35fc52
ms.openlocfilehash: ab57adbe0effa2b74541053aa0fcc5b572a6b7fd
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96293932"
---
# <a name="access-wcf-services-with-a-windows-store-client-app"></a>使用 Windows Store 用戶端應用程式存取 WCF 服務

Windows 8 引入新的應用程式型別，稱為 Windows 市集應用程式。 這些應用程式都是以觸控式螢幕介面為設計主軸。 .NET Framework 4.5 可讓 Windows 市集應用程式呼叫 WCF 服務。  
  
## <a name="wcf-support-in-windows-store-applications"></a>Windows 市集應用程式中的 WCF 支援  

 Windows 市集應用程式中提供部分的 WCF 功能，請參閱下列各節中的詳細資訊。  
  
> [!IMPORTANT]
> 使用 WinRT 新聞訂閱應用程式開發介面，而不使用由 WCF 所公開的介面。 如需詳細資訊，請參閱 [WinRT 新聞訂閱應用程式開發介面](xref:Windows.Web.Syndication)  
  
> [!WARNING]
> 不支援使用加入服務參考將 web 服務參考加入至 Windows 執行階段元件。  
  
### <a name="supported-bindings"></a>支援的繫結  

 Windows 市集應用程式支援下列 WCF 繫結：  
  
1. <xref:System.ServiceModel.BasicHttpBinding>  
  
2. <xref:System.ServiceModel.NetTcpBinding>  
  
3. <xref:System.ServiceModel.NetHttpBinding>  
  
4. <xref:System.ServiceModel.Channels.CustomBinding>
  
 Windows 市集應用程式支援下列繫結項目  
  
1. <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement>  
  
2. <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>  
  
3. <xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement>  
  
4. <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement>  
  
5. <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement>  
  
6. <xref:System.ServiceModel.Channels.TcpTransportBindingElement>  
  
7. <xref:System.ServiceModel.Channels.HttpTransportBindingElement>  
  
8. <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>  
  
9. <xref:System.ServiceModel.Channels.TransportSecurityBindingElement>  
  
 同時支援二進位和文字編碼方式。 支援所有 WCF 傳輸模式。 如需詳細資訊，請參閱 [Streaming Message Transfer](streaming-message-transfer.md)。  
  
### <a name="add-service-reference"></a>中的 [  

 若要從 Windows 市集應用程式呼叫 WCF 服務，請使用 Visual Studio 2012 的 [加入服務參考] 功能。 在 Windows 市集應用程式中執行時，您會發現 [加入服務參考] 的功能有一些變更。 首先是沒有產生組態檔。 Windows 市集應用程式不使用組態檔，因此必須在程式碼中進行設定。 您可以在 [加入服務參考] 產生的 References.cs 檔案中找到這個組態程式碼。 若要查看這個檔案，請務必選取 [方案瀏覽器] 中的 [顯示所有檔案]。 檔案位於 [服務參考] 底下，專案內的 Reference.svcmap 節點中。 在 Windows 市集應用程式中，針對 WCF 服務產生的所有作業都會使用以工作為基礎的非同步模式，且都是非同步。 如需詳細資訊，請參閱 [非同步工作-使用工作簡化非同步程式設計](/archive/msdn-magazine/2010/september/async-tasks-simplify-asynchronous-programming-with-tasks)。  
  
 由於組態現在是以程式碼來產生，因此每次服務參考更新時，在 Reference.cs 檔案中所做的任何變更都會被覆寫。 若要補救這種情況，您可以在用戶端 Proxy 類別中實作部分方法，讓組態程式碼由部分方法來產生。 部分方法的宣告如下：  
  
```csharp  
static partial void Configure(System.ServiceModel.Description.ServiceEndpoint serviceEndpoint,  
            System.ServiceModel.Description.ClientCredentials clientCredentials);  
```  
  
 然後，您可以在用戶端 Proxy 類別中，實作這個部分方法並變更繫結或端點，如下所示：  
  
```csharp  
public partial class Service1Client : System.ServiceModel.ClientBase<MetroWcfClient.ServiceRefMultiEndpt.IService1>, MetroWcfClient.ServiceRefMultiEndpt.IService1  
    {
        static partial void Configure(System.ServiceModel.Description.ServiceEndpoint serviceEndpoint,
            System.ServiceModel.Description.ClientCredentials clientCredentials)  
        {  
            if (serviceEndpoint.Name ==
                    ServiceRefMultiEndpt.Service1Client.EndpointConfiguration.BasicHttpBinding_IService1.ToString())  
            {  
                serviceEndpoint.Binding.SendTimeout = new System.TimeSpan(0, 1, 0);  
            }  
            else if (serviceEndpoint.Name ==
                    ServiceRefMultiEndpt.Service1Client.EndpointConfiguration.BasicHttpBinding_IService11.ToString())  
            {  
                serviceEndpoint.Binding.SendTimeout = new System.TimeSpan(0, 1, 0);  
                clientCredentials.UserName.UserName = "username1";  
                clientCredentials.UserName.Password = "password";  
            }  
            else if (serviceEndpoint.Name ==
                    ServiceRefMultiEndpt.Service1Client.EndpointConfiguration.NetTcpBinding_IService1.ToString())  
            {  
                serviceEndpoint.Binding.Name = "MyTcpBinding";  
                serviceEndpoint.Address = new System.ServiceModel.EndpointAddress("net.tcp://localhost/tcp");  
            }  
        }  
    }  
```  
  
### <a name="serialization"></a>序列化  

 Windows 市集應用程式支援下列序列化程式：  
  
1. DataContractSerializer  
  
2. DataContractJsonSerializer  
  
3. XmlSerializer  
  
> [!WARNING]
> XmlDictionaryWriter.Write(DateTime) 現在會將 DateTime 物件當做字串寫入。  
  
### <a name="security"></a>安全性  

Windows Store 應用程式支援下列安全性模式：
  
1. <xref:System.ServiceModel.SecurityMode.None>  
  
2. <xref:System.ServiceModel.SecurityMode.Transport>  
  
3. <xref:System.ServiceModel.SecurityMode.TransportWithMessageCredential>
  
4. <xref:System.ServiceModel.SecurityMode.Message>
  
以下是 Windows Store 應用程式中支援的用戶端認證類型：
  
1. 無  
  
2. 基本  
  
3. Digest  
  
4. 交涉  
  
5. NTLM  
  
6. Windows  
  
7. 使用者名稱 (訊息安全性)  
  
8. Windows (傳輸安全性)  
  
 若要讓 Windows 市集應用程式存取和傳送預設 Windows 認證，您必須在 Package.appmanifest 檔案中啟用這個功能。 開啟此檔案，並選取 [功能] 索引標籤，然後選取 [預設的 Windows 認證]。 這可讓應用程式連接至需要網域認證的內部網路資源。  
  
> [!IMPORTANT]
> 為了讓 Windows Store 應用程式進行跨電腦呼叫，您必須啟用另一項稱為「家用/工作網路」的功能。 這項設定也會在 [功能] 索引標籤下的 appmanifest 檔案中。選取 [家用/工作網路] 核取方塊。 這可讓您的應用程式對使用者的受信任位置（例如首頁和工作）的網路進行輸入和輸出存取。 永遠封鎖關鍵的傳入連接埠。 如果是存取網際網路上的服務，您還必須啟用網際網路 (用戶端) 功能。  
  
### <a name="misc"></a>其他  

 Windows 市集應用程式支援使用下列類別：  
  
1. <xref:System.ServiceModel.ChannelFactory>  
  
2. <xref:System.ServiceModel.DuplexChannelFactory%601>
  
3. <xref:System.ServiceModel.CallbackBehaviorAttribute>  
  
### <a name="defining-service-contracts"></a>定義服務合約  

 建議您只定義使用以工作為基礎之非同步模式的非同步服務作業。 這樣可以確保 Windows 市集應用程式在呼叫服務作業時仍能保持回應。  
  
> [!WARNING]
> 雖然定義同步作業並不會擲回例外狀況，還是強烈建議您只定義非同步作業。  
  
### <a name="calling-wcf-services-from-windows-store-applications"></a>從 Windows 市集應用程式呼叫 WCF 服務  

 正如前面提到的，所有組態都必須在所產生 Proxy 類別的 GetBindingForEndpoint 方法中，以程式碼來設定。 呼叫服務作業的方式與呼叫任何以工作為基礎的非同步方法相同，如下列程式碼片段中所示。  
  
```csharp  
void async SomeMethod()  
{  
    ServiceClient proxy = new ServiceClient();  
    Task<T> results = await proxy.CallAsync(param1, param2);  
    T result = results.Result;  
    if (result.Success)  
    {  
       // Do something with result  
    }  
}  
```  
  
 請注意，在進行非同步呼叫的方法上使用 async 關鍵字，並在呼叫非同步方法時使用 await 關鍵字。  
  
## <a name="see-also"></a>另請參閱

- [WCF 安全性程式設計](programming-wcf-security.md)
- [繫結](../bindings.md)
