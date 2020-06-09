---
title: 永久性執行個體內容
ms.date: 03/30/2017
ms.assetid: 97bc2994-5a2c-47c7-927a-c4cd273153df
ms.openlocfilehash: 567ca62d48e80993328548b11f8b59c4fcd355fe
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600590"
---
# <a name="durable-instance-context"></a>永久性執行個體內容

這個範例會示範如何自訂 Windows Communication Foundation （WCF）執行時間，以啟用持久實例內容。 它會使用 SQL Server 2005 做為備份存放區 (在此例中為 SQL Server 2005 Express)。 不過，也會提供存取自訂儲存機制的方法。

> [!NOTE]
> 此範例的安裝程序與建置指示位於本主題的結尾。

這個範例牽涉到擴充 WCF 的通道層和服務模型層。 因此，在進入實作的詳細資訊之前，您必須先了解一些基礎概念。

在現實生活中，您經常可以發現永久性執行個體內容的例子。 例如，購物車應用程式可以暫停購物，並在另一天繼續進行。 因此當我們隔天造訪購物車時，已還原原始的內容。 請特別注意，當您中斷連線時，購物車應用程式 (在伺服器上) 不會維護購物車執行個體。 而是將其狀態保存至永久性儲存媒體，並在您對還原的內容建構新執行個體時使用該狀態。 因此，提供相同內容的服務執行個體與之前的執行個體不同 (因為它們沒有相同的記憶體位址)。

永久性執行個體內容可能是由小型通訊協定所產生，而這個小型通訊協定會在用戶端和服務之間交換內容識別碼。 您會在用戶端上建立此內容識別碼，並傳輸至服務。 建立服務執行個體時，服務執行階段會嘗試從持續性儲存體 (Persistent Storage) (預設為 SQL Server 2005 資料庫) 載入對應至此內容識別碼的持續狀態。 如果沒有可用的狀態，則新的實例會有其預設狀態。 服務實作會使用自訂屬性，以標示會變更服務實作狀態的作業，讓執行階段可以在呼叫作業之後儲存服務執行個體。

在前面的描述中，有兩個易辨的步驟可達到目標：

1. 變更在網路上傳送的訊息，以使用內容識別碼。

2. 變更服務本機行為，以實作自訂執行個體邏輯。

因為清單中的第一個會影響網路上的訊息，所以應該實作為自訂通道，並連結至通道層。 後一項只會影響服務本機行為，因此可藉由延伸數個服務擴充點來進行實作。 在接下來的章節中，將會討論這些延伸項目。

## <a name="durable-instancecontext-channel"></a>永久性 InstanceContext 通道

您應該查看的第一項為通道層延伸項目。 撰寫自訂通道的第一個步驟為決定通道的通訊結構。 引進新的有線通訊協定時，通道應該會與通道堆疊中幾乎任何其他通道搭配使用。 因此，該通道支援所有訊息交換模式。 但是不管其通訊結構為何，通道的核心功能都是一樣的。 更具體來說，從用戶端的角度，應該將內容識別碼寫出至訊息；而從服務的角度來看，應該從訊息讀取此內容識別碼，並傳遞至較上層。 因此，將會針對所有永久性執行個體內容通道實作，建立充當為抽象基底類別的 `DurableInstanceContextChannelBase` 類別。 這個類別包含一般狀態電腦管理函式以及兩個受保護的成員，可在訊息之間套用及讀取內容資訊。

```csharp
class DurableInstanceContextChannelBase
{
  //…
  protected void ApplyContext(Message message)
  {
    //…
  }
  protected string ReadContextId(Message message)
  {
    //…
  }
}
```

這兩個方法會使用 `IContextManager` 實作，以在訊息之間寫入和讀取內容識別碼  （ `IContextManager` 是一種自訂介面，可用來定義所有內容管理員的合約）。通道可以在自訂 SOAP 標頭或 HTTP cookie 標頭中包含內容識別碼。 每個內容管理員實作都繼承自 `ContextManagerBase` 類別，而這個類別則包含用於所有內容管理員的一般功能。 您可以使用此類別中的 `GetContextId` 方法，從用戶端產生內容識別碼。 第一次產生內容識別碼時，方法會將此內容識別碼儲存至文字檔，而這個文字檔的名稱則是由遠端端點位址 (將使用 @ 字元取代典型 URI 中無效的檔案名稱字元) 所建構。

之後相同的遠端端點需要此內容識別碼時，就會檢查是否有適當的檔案。 如果有，就會讀取內容識別碼並傳回。 否則會傳回新產生的內容識別碼，並儲存至檔案。 使用預設設定時，這些檔案會放在名為 CoNtextStore 的目錄中，其位於目前使用者的臨時目錄中。 不過，您可以使用繫結項目來設定這個位置。

您可以設定傳輸內容識別碼的機制。 這個內容識別碼可以寫入 HTTP Cookie 標頭或自訂 SOAP 標頭。 自訂 SOAP 標頭方法可讓您使用此通訊協定搭配非 HTTP 通訊協定 (例如，TCP 或具名管道)。 有兩個可實作這兩個選項的類別，`MessageHeaderContextManager` 和 `HttpCookieContextManager`。

這兩個類別會將內容識別碼適當地寫入訊息。 例如，`MessageHeaderContextManager` 類別會將內容識別碼寫入 `WriteContext` 方法的 SOAP 標頭。

```csharp
public override void WriteContext(Message message)
{
  string contextId = this.GetContextId();

  MessageHeader contextHeader =
    MessageHeader.CreateHeader(DurableInstanceContextUtility.HeaderName,
      DurableInstanceContextUtility.HeaderNamespace,
      contextId,
      true);

  message.Headers.Add(contextHeader);
}
```

`ApplyContext` 類別中的 `ReadContextId` 和 `DurableInstanceContextChannelBase` 方法，可以分別叫用 `IContextManager.ReadContext` 和 `IContextManager.WriteContext`。 不過，不是由 `DurableInstanceContextChannelBase` 類別直接建立這些內容管理員。 而是會使用 `ContextManagerFactory` 類別來建立。

```csharp
IContextManager contextManager =
                ContextManagerFactory.CreateContextManager(contextType,
                this.contextStoreLocation,
                this.endpointAddress);
```

傳送通道時即可叫用 `ApplyContext` 方法。 然後將內容識別碼插入傳出訊息。 接收通道便會叫用 `ReadContextId` 方法。 這個方法會確定可在傳入訊息中使用內容識別碼，並將該內容識別碼新增至 `Properties` 類別的 `Message` 集合中。 也會在無法讀取內容識別碼時擲回 `CommunicationException`，因而導致中止通道。

```csharp
message.Properties.Add(DurableInstanceContextUtility.ContextIdProperty, contextId);
```

在繼續處理之前，您需要已了解如何使用 `Properties` 類別中的 `Message` 集合。 一般來說，在通道層中將資料從較低層傳遞至較高層時，就會使用此 `Properties` 集合。 如此一來，就可以使用一致的方法對較高層提供需要的資料，而不用在意通訊協定詳細資料。 換句話說，通道層可以將內容識別碼當做 SOAP 標頭或 HTTP cookie 標頭來傳送和接收。 但這些較高層不需要知道這些細節，因為通道層會在 `Properties` 擊盒中提供此資訊。

現在使用 `DurableInstanceContextChannelBase` 類別時，就必須實作將這十個必要的介面放置在適當的位置 (IOutputChannel、IInputChannel、IOutputSessionChannel、IInputSessionChannel、IRequestChannel、IReplyChannel、IRequestSessionChannel、IReplySessionChannel、IDuplexChannel、IDuplexSessionChannel)。 它們類似每個可用的訊息交換模式（資料包、單工、雙工和其會話變異）。 這些每一個執行都會繼承先前所述的基類， `ApplyContext` 並 `ReadContextId` 適當地呼叫和。 例如實作 IOutputChannel 介面的 `DurableInstanceContextOutputChannel`，它會從傳送訊息的每個方法中呼叫 `ApplyContext` 方法。

```csharp
public void Send(Message message, TimeSpan timeout)
{
    // Apply the context information before sending the message.
    this.ApplyContext(message);
    //…
}
```

另一方面， `DurableInstanceContextInputChannel` -這會執行 `IInputChannel` 介面-呼叫 `ReadContextId` 每個方法中的方法，以接收訊息。

```csharp
public Message Receive(TimeSpan timeout)
{
    //…
      ReadContextId(message);
      return message;
}
```

此外，這些通道實作會將方法叫用委派給通道堆疊中位置更低的通道。 不過，工作階段變數會有一些基本邏輯，確定針對導致建立工作階段的第一個訊息而言，會傳送內容識別碼而且此內容識別碼為唯讀。

```csharp
if (isFirstMessage)
{
//…
    this.ApplyContext(message);
    isFirstMessage = false;
}
```

然後， `DurableInstanceContextBindingElement` 類別和類別會適當地將這些通道實現新增至 WCF 通道執行時間 `DurableInstanceContextBindingElementSection` 。 如需繫結項目和繫結項目區段的詳細資訊，請參閱[HttpCookieSession](httpcookiesession.md)通道範例檔。

## <a name="service-model-layer-extensions"></a>服務模型層延伸項目

現在內容識別碼已周遊至各個通道層，您就可以實作服務行為以自訂執行個體化 (Instantiation)。 在此範例中，可以使用存放管理員，在持續存放區中載入及儲存狀態。 如先前所述，這個範例提供使用 SQL Server 2005 做為其備份存放區的存放管理員。 不過，您也可以將自訂存放機制新增至此延伸項目。 若要這樣做，將會宣告公用介面，而所有存放管理員都必須實作此公用介面。

```csharp
public interface IStorageManager
{
    object GetInstance(string contextId, Type type);
    void SaveInstance(string contextId, object state);
}
```

`SqlServerStorageManager` 類別包含預設 `IStorageManager` 實作。 在其 `SaveInstance` 方法中，會使用 XmlSerializer 序列化給定的物件，並將它儲存到 SQL Server 資料庫。

```csharp
XmlSerializer serializer = new XmlSerializer(state.GetType());
string data;

using (StringWriter writer = new StringWriter(CultureInfo.InvariantCulture))
{
    serializer.Serialize(writer, state);
    data = writer.ToString();
}

using (SqlConnection connection = new SqlConnection(GetConnectionString()))
{
    connection.Open();

    string update = @"UPDATE Instances SET Instance = @instance WHERE ContextId = @contextId";

    using (SqlCommand command = new SqlCommand(update, connection))
    {
        command.Parameters.Add("@instance", SqlDbType.VarChar, 2147483647).Value = data;
        command.Parameters.Add("@contextId", SqlDbType.VarChar, 256).Value = contextId;

        int rows = command.ExecuteNonQuery();

        if (rows == 0)
        {
            string insert = @"INSERT INTO Instances(ContextId, Instance) VALUES(@contextId, @instance)";
            command.CommandText = insert;
            command.ExecuteNonQuery();
        }
    }
}
```

在 `GetInstance` 方法中，會針對指定的內容識別碼讀取序列化資料，而從它所建立的物件會傳回給呼叫者。

```csharp
object data;
using (SqlConnection connection = new SqlConnection(GetConnectionString()))
{
    connection.Open();

    string select = "SELECT Instance FROM Instances WHERE ContextId = @contextId";
    using (SqlCommand command = new SqlCommand(select, connection))
    {
        command.Parameters.Add("@contextId", SqlDbType.VarChar, 256).Value = contextId;
        data = command.ExecuteScalar();
    }
}

if (data != null)
{
    XmlSerializer serializer = new XmlSerializer(type);
    using (StringReader reader = new StringReader((string)data))
    {
        object instance = serializer.Deserialize(reader);
        return instance;
    }
}
```

存放管理員的使用者不應該直接執行個體化這些存放管理員。 使用者會使用擷取自存放管理員建立詳細資料的 `StorageManagerFactory` 類別。 這個類別包含 `GetStorageManager` 這個靜態成員，此成員會建立提供之存放管理員型別的執行個體。 如果型別參數為 `null`，這個方法就會建立預設 `SqlServerStorageManager` 類別的執行個體，並傳回之。 也會驗證提供的型別，以確定會實作 `IStorageManager` 介面。

```csharp
public static IStorageManager GetStorageManager(Type storageManagerType)
{
IStorageManager storageManager = null;

if (storageManagerType == null)
{
    return new SqlServerStorageManager();
}
else
{
    object obj = Activator.CreateInstance(storageManagerType);

    // Throw if the specified storage manager type does not
    // implement IStorageManager.
    if (obj is IStorageManager)
    {
        storageManager = (IStorageManager)obj;
    }
    else
    {
        throw new InvalidOperationException(
                  ResourceHelper.GetString("ExInvalidStorageManager"));
    }

    return storageManager;
}
}
```

現在已實作從持續性儲存體 (Persistent Storage) 中讀取及寫入執行個體的必要基礎結構。 接著便需要採取變更服務行為的必要步驟。

此處理序的第一個步驟為儲存內容識別碼，而這個內容識別碼會從通道層周遊至目前的 InstanceContext。 InstanceCoNtext 是一個執行時間元件，可做為 WCF 發送器與服務實例之間的連結。 可以用於對服務執行個體提供額外的狀態和行為。 而這是很重要的一點，因為在工作階段通訊中，只有第一個訊息會一起傳送內容識別碼。

WCF 允許擴充其 InstanceCoNtext 執行時間元件，方法是使用其可延伸物件模式來新增新的狀態和行為。 可延伸物件模式用於 WCF 中，以新功能來擴充現有執行時間類別，或將新的狀態功能加入至物件。 可擴充物件模式中有三個介面-Iextensibleobject<t> \<T> 、IExtension \<T> 和 IExtensionCollection \<T> ：

- Iextensibleobject<t> \<T> 介面是由允許自訂其功能之延伸模組的物件所執行。

- IExtension \<T> 介面是由屬於 T 類型類別之延伸的物件所執行。

- IExtensionCollection \<T> 介面是 IExtensions 的集合，可讓您依其類型來抓取 IExtensions。

因此，您應該建立 InstanceContextExtension 類別，並實作 IExtension 介面及定義必要的狀態以儲存內容識別碼。 這個類別也會提供一種狀態，保留正在使用的存放管理員。 一旦儲存新狀態，就無法進行修改。 所以您應該在建構執行個體時提供狀態，並將該狀態儲存至執行個體，並只能透過唯讀屬性來進行存取。

```csharp
// Constructor
public DurableInstanceContextExtension(string contextId,
            IStorageManager storageManager)
{
    this.contextId = contextId;
    this.storageManager = storageManager;
}

// Read only properties
public string ContextId
{
    get { return this.contextId; }
}

public IStorageManager StorageManager
{
    get { return this.storageManager; }
}
```

InstanceContextInitializer 類別會實作 IInstanceContextInitializer 介面，並將執行個體內容延伸項目新增至已建構之 InstanceContext 的 Extensions 集合中。

```csharp
public void Initialize(InstanceContext instanceContext, Message message)
{
    string contextId =
  (string)message.Properties[DurableInstanceContextUtility.ContextIdProperty];

    DurableInstanceContextExtension extension =
                new DurableInstanceContextExtension(contextId,
                     storageManager);
    instanceContext.Extensions.Add(extension);
}
```

如先前所述，您會從 `Properties` 類別的 `Message` 集合中讀取內容識別碼，並將它傳遞至延伸類別的建構函式。 這樣便可示範如何使用一致的方法，在各層之間交換資訊。

下一個重要的步驟為覆寫服務執行個體的建立處理序。 WCF 允許執行自訂的具現化行為，並使用 IInstanceProvider 介面將它們連結至執行時間。 將實作新 `InstanceProvider` 類別以執行該工作。 在此函數中，接受來自執行個體提供者的服務類型。 稍後將使用此服務類型來建立新的執行個體。 在 `GetInstance` 執行期間，會建立存放管理員的實例來尋找保存的實例。 如果 `null` 傳回，則會具現化服務類型的新實例，並將其傳回給呼叫端。

```csharp
public object GetInstance(InstanceContext instanceContext, Message message)
{
    object instance = null;

    DurableInstanceContextExtension extension =
    instanceContext.Extensions.Find<DurableInstanceContextExtension>();

    string contextId = extension.ContextId;
    IStorageManager storageManager = extension.StorageManager;

    instance = storageManager.GetInstance(contextId, serviceType);

    instance ??= Activator.CreateInstance(serviceType);
    return instance;
}
```

下一個重要步驟是將 `InstanceContextExtension` 、 `InstanceContextInitializer` 和 `InstanceProvider` 類別安裝到服務模型執行時間。 您可以使用自訂屬性以標示服務實作類別，便可安裝行為。 `DurableInstanceContextAttribute` 中包含這個屬性的實作，並且會實作 `IServiceBehavior` 介面以擴充整個服務執行階段。

這個類別所擁有的屬性，可以接受要使用的存放管理員類型。 如此一來，此實作為可讓使用者指定自己 `IStorageManager` 的實作為這個屬性的參數。

在 `ApplyDispatchBehavior` 執行 `InstanceContextMode` 時， `ServiceBehavior` 會驗證目前屬性的。 如果這個屬性設定為 Singleton，就無法啟用永久性執行個體，並且會擲回 `InvalidOperationException` 以通知主機。

```csharp
ServiceBehaviorAttribute serviceBehavior =
    serviceDescription.Behaviors.Find<ServiceBehaviorAttribute>();

if (serviceBehavior != null &&
     serviceBehavior.InstanceContextMode == InstanceContextMode.Single)
{
    throw new InvalidOperationException(
       ResourceHelper.GetString("ExSingletonInstancingNotSupported"));
}
```

之後，便會在針對每個端點所建立的 `DispatchRuntime` 中，建立並安裝存放管理員執行個體、執行個體內容初始設定式和執行個體提供者。

```csharp
IStorageManager storageManager =
    StorageManagerFactory.GetStorageManager(storageManagerType);

InstanceContextInitializer contextInitializer =
    new InstanceContextInitializer(storageManager);

InstanceProvider instanceProvider =
    new InstanceProvider(description.ServiceType);

foreach (ChannelDispatcherBase cdb in serviceHostBase.ChannelDispatchers)
{
    ChannelDispatcher cd = cdb as ChannelDispatcher;

    if (cd != null)
    {
        foreach (EndpointDispatcher ed in cd.Endpoints)
        {
            ed.DispatchRuntime.InstanceContextInitializers.Add(contextInitializer);
            ed.DispatchRuntime.InstanceProvider = instanceProvider;
        }
    }
}
```

到目前為止，這個範例產生的通道可對自訂內容識別碼交換啟用自訂網路通訊協定，也會覆寫預設執行個體行為以從持續性儲存體載入執行個體。

不會變得是將服務執行個體儲存至持續性儲存體。 如前所述，已提供必要的功能讓您在 `IStorageManager` 實作中儲存狀態。 我們現在必須將此與 WCF 執行時間進行整合。 也需要適用於服務實作類別方法的其他屬性。 而這個屬性應該會套用至變更服務執行個體狀態的方法。

`SaveStateAttribute` 類別會實作此功能。 它也會 `IOperationBehavior` 執行類別，以修改每個作業的 WCF 執行時間。 當使用這個屬性來標記方法時，WCF 執行時間會在 `ApplyBehavior` 結構化適當的時叫用方法 `DispatchOperation` 。 這個方法的實行中有一行程式碼：

```csharp
dispatch.Invoker = new OperationInvoker(dispatch.Invoker);
```

這個指示會建立 `OperationInvoker` 型別的執行個體，並將它指派至已建構之 `Invoker` 的 `DispatchOperation` 屬性。 `OperationInvoker` 類別則是對 `DispatchOperation` 所建立之預設作業啟動程式的包裝函式。 此類別會實作 `IOperationInvoker` 介面。 在 `Invoke` 方法執行中，會將實際的方法叫用委派給內部作業啟動項。 但是在傳回結果之前，可以使用 `InstanceContext` 中的存放管理員來儲存服務執行個體。

```csharp
object result = innerOperationInvoker.Invoke(instance,
    inputs, out outputs);

// Save the instance using the storage manager saved in the
// current InstanceContext.
InstanceContextExtension extension =
    OperationContext.Current.InstanceContext.Extensions.Find<InstanceContextExtension>();

extension.StorageManager.SaveInstance(extension.ContextId, instance);
return result;
```

## <a name="using-the-extension"></a>使用延伸項目

通道層和服務模型層延伸都已完成，而且現在可以在 WCF 應用程式中使用。 服務必須使用自訂系結將通道新增至通道堆疊，然後以適當的屬性標示服務執行類別。

```csharp
[DurableInstanceContext]
[ServiceBehavior(InstanceContextMode=InstanceContextMode.PerSession)]
public class ShoppingCart : IShoppingCart
{
//…
     [SaveState]
     public int AddItem(string item)
     {
         //…
     }
//…
 }
```

用戶端應用程式必須使用自訂繫結，將 DurableInstanceContextChannel 新增至通道堆疊。 若要以宣告方式在組態檔中設定通道，則必須將繫結項目區段新增至繫結項目延伸集合中。

```xml
<system.serviceModel>
 <extensions>
   <bindingElementExtensions>
     <add name="durableInstanceContext"
type="Microsoft.ServiceModel.Samples.DurableInstanceContextBindingElementSection, DurableInstanceContextExtension, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"/>
   </bindingElementExtensions>
 </extensions>
</system.serviceModel>
```

現在繫結程序項目就和其他標準繫結程序項目一樣，都可以搭配使用自訂繫結程序：

```xml
<bindings>
 <customBinding>
   <binding name="TextOverHttp">
     <durableInstanceContext contextType="HttpCookie"/>
     <reliableSession />
     <textMessageEncoding />
     <httpTransport />
   </binding>
 </customBinding>
</bindings>
```

## <a name="conclusion"></a>結論

這個範例會顯示如何建立自訂通訊協定通道，以及如何自訂服務行為進而啟用它。

讓使用者使用組態區段指定 `IStorageManager` 實作，將可進一步增進延伸項目的功能。 這樣做便可修改備份存放區，而不需要重新編譯服務程式碼。

您甚至可以嘗試實作類別 (例如，`StateBag`)，而這個類別會封裝執行個體的狀態。 該類別也負責在變更狀態時保存狀態。 透過這個方法，您就可以避免使用 `SaveState` 屬性並更精確地執行保存工作 (例如，可以在實際上變更狀態時保存狀態，而不是每次呼叫具有 `SaveState` 屬性的方法時就儲存狀態)。

當您執行範例時，會顯示如下的輸出。 用戶端會將兩個項目新增至購物車，然後從服務中取得其購物車的項目清單。 在每個主控台視窗中按下 ENTER 鍵，即可關閉服務與用戶端。

```console
Enter the name of the product: apples
Enter the name of the product: bananas

Shopping cart currently contains the following items.
apples
bananas
Press ENTER to shut down client
```

> [!NOTE]
> 重建服務則會覆寫資料庫檔案。 若要觀察每次執行範例時所保留的狀態，請在各個執行動作之間務必不要重建範例。

#### <a name="to-set-up-build-and-run-the-sample"></a>若要安裝、建置及執行範例

1. 請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。

2. 若要建立方案，請依照[建立 Windows Communication Foundation 範例](building-the-samples.md)中的指示進行。

3. 若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。

> [!NOTE]
> 您必須執行 SQL Server 2005 或 SQL Express 2005，才能執行此範例。 如果正在執行 SQL Server 2005，則必須修改服務之連線字串的組態。 在多台電腦中執行時，只有伺服器電腦上需要 SQL Server。

> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Instancing\Durable`
