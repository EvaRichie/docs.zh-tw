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
# <a name="durable-instance-context"></a><span data-ttu-id="efa17-102">永久性執行個體內容</span><span class="sxs-lookup"><span data-stu-id="efa17-102">Durable Instance Context</span></span>

<span data-ttu-id="efa17-103">這個範例會示範如何自訂 Windows Communication Foundation （WCF）執行時間，以啟用持久實例內容。</span><span class="sxs-lookup"><span data-stu-id="efa17-103">This sample demonstrates how to customize the Windows Communication Foundation (WCF) runtime to enable durable instance contexts.</span></span> <span data-ttu-id="efa17-104">它會使用 SQL Server 2005 做為備份存放區 (在此例中為 SQL Server 2005 Express)。</span><span class="sxs-lookup"><span data-stu-id="efa17-104">It uses SQL Server 2005 as its backing store (SQL Server 2005 Express in this case).</span></span> <span data-ttu-id="efa17-105">不過，也會提供存取自訂儲存機制的方法。</span><span class="sxs-lookup"><span data-stu-id="efa17-105">However, it also provides a way to access custom storage mechanisms.</span></span>

> [!NOTE]
> <span data-ttu-id="efa17-106">此範例的安裝程序與建置指示位於本主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="efa17-106">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>

<span data-ttu-id="efa17-107">這個範例牽涉到擴充 WCF 的通道層和服務模型層。</span><span class="sxs-lookup"><span data-stu-id="efa17-107">This sample involves extending both the channel layer and the service model layer of the WCF.</span></span> <span data-ttu-id="efa17-108">因此，在進入實作的詳細資訊之前，您必須先了解一些基礎概念。</span><span class="sxs-lookup"><span data-stu-id="efa17-108">Therefore it is necessary to understand the underlying concepts before going into the implementation details.</span></span>

<span data-ttu-id="efa17-109">在現實生活中，您經常可以發現永久性執行個體內容的例子。</span><span class="sxs-lookup"><span data-stu-id="efa17-109">Durable instance contexts can be found in the real world scenarios quite often.</span></span> <span data-ttu-id="efa17-110">例如，購物車應用程式可以暫停購物，並在另一天繼續進行。</span><span class="sxs-lookup"><span data-stu-id="efa17-110">A shopping cart application, for example, has the ability to pause shopping halfway through and continue it on another day.</span></span> <span data-ttu-id="efa17-111">因此當我們隔天造訪購物車時，已還原原始的內容。</span><span class="sxs-lookup"><span data-stu-id="efa17-111">So that when we visit the shopping cart the next day, our original context is restored.</span></span> <span data-ttu-id="efa17-112">請特別注意，當您中斷連線時，購物車應用程式 (在伺服器上) 不會維護購物車執行個體。</span><span class="sxs-lookup"><span data-stu-id="efa17-112">It is important to note that the shopping cart application (on the server) does not maintain the shopping cart instance while we are disconnected.</span></span> <span data-ttu-id="efa17-113">而是將其狀態保存至永久性儲存媒體，並在您對還原的內容建構新執行個體時使用該狀態。</span><span class="sxs-lookup"><span data-stu-id="efa17-113">Instead, it persists its state into a durable storage media and uses it when constructing a new instance for the restored context.</span></span> <span data-ttu-id="efa17-114">因此，提供相同內容的服務執行個體與之前的執行個體不同 (因為它們沒有相同的記憶體位址)。</span><span class="sxs-lookup"><span data-stu-id="efa17-114">Therefore the service instance that may service for the same context is not the same as the previous instance (that is, it does not have the same memory address).</span></span>

<span data-ttu-id="efa17-115">永久性執行個體內容可能是由小型通訊協定所產生，而這個小型通訊協定會在用戶端和服務之間交換內容識別碼。</span><span class="sxs-lookup"><span data-stu-id="efa17-115">Durable instance context is made possible by a small protocol that exchanges a context ID between the client and service.</span></span> <span data-ttu-id="efa17-116">您會在用戶端上建立此內容識別碼，並傳輸至服務。</span><span class="sxs-lookup"><span data-stu-id="efa17-116">This context ID is created on the client and transmitted to the service.</span></span> <span data-ttu-id="efa17-117">建立服務執行個體時，服務執行階段會嘗試從持續性儲存體 (Persistent Storage) (預設為 SQL Server 2005 資料庫) 載入對應至此內容識別碼的持續狀態。</span><span class="sxs-lookup"><span data-stu-id="efa17-117">When the service instance is created, the service runtime tries to load the persisted state that corresponds to this context ID from a persistent storage (by default it is a SQL Server 2005 database).</span></span> <span data-ttu-id="efa17-118">如果沒有可用的狀態，則新的實例會有其預設狀態。</span><span class="sxs-lookup"><span data-stu-id="efa17-118">If no state is available, the new instance has its default state.</span></span> <span data-ttu-id="efa17-119">服務實作會使用自訂屬性，以標示會變更服務實作狀態的作業，讓執行階段可以在呼叫作業之後儲存服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="efa17-119">The service implementation uses a custom attribute to mark operations that change the state of the service implementation so that the runtime can save the service instance after invoking them.</span></span>

<span data-ttu-id="efa17-120">在前面的描述中，有兩個易辨的步驟可達到目標：</span><span class="sxs-lookup"><span data-stu-id="efa17-120">By the previous description, two steps can easily be distinguished to achieve the goal:</span></span>

1. <span data-ttu-id="efa17-121">變更在網路上傳送的訊息，以使用內容識別碼。</span><span class="sxs-lookup"><span data-stu-id="efa17-121">Change the message that goes on the wire to carry the context ID.</span></span>

2. <span data-ttu-id="efa17-122">變更服務本機行為，以實作自訂執行個體邏輯。</span><span class="sxs-lookup"><span data-stu-id="efa17-122">Change the service local behavior to implement custom instancing logic.</span></span>

<span data-ttu-id="efa17-123">因為清單中的第一個會影響網路上的訊息，所以應該實作為自訂通道，並連結至通道層。</span><span class="sxs-lookup"><span data-stu-id="efa17-123">Because the first one in the list affects the messages on the wire, it should be implemented as a custom channel and be hooked up to the channel layer.</span></span> <span data-ttu-id="efa17-124">後一項只會影響服務本機行為，因此可藉由延伸數個服務擴充點來進行實作。</span><span class="sxs-lookup"><span data-stu-id="efa17-124">The latter only affects the service local behavior and therefore can be implemented by extending several service extensibility points.</span></span> <span data-ttu-id="efa17-125">在接下來的章節中，將會討論這些延伸項目。</span><span class="sxs-lookup"><span data-stu-id="efa17-125">In the next few sections, each of these extensions are discussed.</span></span>

## <a name="durable-instancecontext-channel"></a><span data-ttu-id="efa17-126">永久性 InstanceContext 通道</span><span class="sxs-lookup"><span data-stu-id="efa17-126">Durable InstanceContext Channel</span></span>

<span data-ttu-id="efa17-127">您應該查看的第一項為通道層延伸項目。</span><span class="sxs-lookup"><span data-stu-id="efa17-127">The first thing to look at is a channel layer extension.</span></span> <span data-ttu-id="efa17-128">撰寫自訂通道的第一個步驟為決定通道的通訊結構。</span><span class="sxs-lookup"><span data-stu-id="efa17-128">The first step in writing a custom channel is to decide the communication structure of the channel.</span></span> <span data-ttu-id="efa17-129">引進新的有線通訊協定時，通道應該會與通道堆疊中幾乎任何其他通道搭配使用。</span><span class="sxs-lookup"><span data-stu-id="efa17-129">As a new wire protocol is being introduced, the channel should work with almost any other channel in the channel stack.</span></span> <span data-ttu-id="efa17-130">因此，該通道支援所有訊息交換模式。</span><span class="sxs-lookup"><span data-stu-id="efa17-130">Therefore it should support all the message exchange patterns.</span></span> <span data-ttu-id="efa17-131">但是不管其通訊結構為何，通道的核心功能都是一樣的。</span><span class="sxs-lookup"><span data-stu-id="efa17-131">However, the core functionality of the channel is the same regardless of its communication structure.</span></span> <span data-ttu-id="efa17-132">更具體來說，從用戶端的角度，應該將內容識別碼寫出至訊息；而從服務的角度來看，應該從訊息讀取此內容識別碼，並傳遞至較上層。</span><span class="sxs-lookup"><span data-stu-id="efa17-132">More specifically, from the client it should write the context ID to the messages and from the service it should read this context ID from the messages and pass it to the upper levels.</span></span> <span data-ttu-id="efa17-133">因此，將會針對所有永久性執行個體內容通道實作，建立充當為抽象基底類別的 `DurableInstanceContextChannelBase` 類別。</span><span class="sxs-lookup"><span data-stu-id="efa17-133">Because of that, a `DurableInstanceContextChannelBase` class is created that acts as the abstract base class for all durable instance context channel implementations.</span></span> <span data-ttu-id="efa17-134">這個類別包含一般狀態電腦管理函式以及兩個受保護的成員，可在訊息之間套用及讀取內容資訊。</span><span class="sxs-lookup"><span data-stu-id="efa17-134">This class contains the common state machine management functions and two protected members to apply and read the context information to and from messages.</span></span>

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

<span data-ttu-id="efa17-135">這兩個方法會使用 `IContextManager` 實作，以在訊息之間寫入和讀取內容識別碼 </span><span class="sxs-lookup"><span data-stu-id="efa17-135">These two methods make use of `IContextManager` implementations to write and read the context ID to or from the message.</span></span> <span data-ttu-id="efa17-136">（ `IContextManager` 是一種自訂介面，可用來定義所有內容管理員的合約）。通道可以在自訂 SOAP 標頭或 HTTP cookie 標頭中包含內容識別碼。</span><span class="sxs-lookup"><span data-stu-id="efa17-136">(`IContextManager` is a custom interface used to define the contract for all context managers.) The channel can either include the context ID in a custom SOAP header or in an HTTP cookie header.</span></span> <span data-ttu-id="efa17-137">每個內容管理員實作都繼承自 `ContextManagerBase` 類別，而這個類別則包含用於所有內容管理員的一般功能。</span><span class="sxs-lookup"><span data-stu-id="efa17-137">Each context manager implementation inherits from the `ContextManagerBase` class that contains the common functionality for all context managers.</span></span> <span data-ttu-id="efa17-138">您可以使用此類別中的 `GetContextId` 方法，從用戶端產生內容識別碼。</span><span class="sxs-lookup"><span data-stu-id="efa17-138">The `GetContextId` method in this class is used to originate the context ID from the client.</span></span> <span data-ttu-id="efa17-139">第一次產生內容識別碼時，方法會將此內容識別碼儲存至文字檔，而這個文字檔的名稱則是由遠端端點位址 (將使用 @ 字元取代典型 URI 中無效的檔案名稱字元) 所建構。</span><span class="sxs-lookup"><span data-stu-id="efa17-139">When a context ID is originated for the first time, this method saves it into a text file whose name is constructed by the remote endpoint address (the invalid file name characters in the typical URIs are replaced with @ characters).</span></span>

<span data-ttu-id="efa17-140">之後相同的遠端端點需要此內容識別碼時，就會檢查是否有適當的檔案。</span><span class="sxs-lookup"><span data-stu-id="efa17-140">Later when the context ID is required for the same remote endpoint, it checks whether an appropriate file exists.</span></span> <span data-ttu-id="efa17-141">如果有，就會讀取內容識別碼並傳回。</span><span class="sxs-lookup"><span data-stu-id="efa17-141">If it does, it reads the context ID and returns.</span></span> <span data-ttu-id="efa17-142">否則會傳回新產生的內容識別碼，並儲存至檔案。</span><span class="sxs-lookup"><span data-stu-id="efa17-142">Otherwise it returns a newly generated context ID and saves it to a file.</span></span> <span data-ttu-id="efa17-143">使用預設設定時，這些檔案會放在名為 CoNtextStore 的目錄中，其位於目前使用者的臨時目錄中。</span><span class="sxs-lookup"><span data-stu-id="efa17-143">With the default configuration, these files are placed in a directory called ContextStore, which resides in the current user's temp directory.</span></span> <span data-ttu-id="efa17-144">不過，您可以使用繫結項目來設定這個位置。</span><span class="sxs-lookup"><span data-stu-id="efa17-144">However this location is configurable using the binding element.</span></span>

<span data-ttu-id="efa17-145">您可以設定傳輸內容識別碼的機制。</span><span class="sxs-lookup"><span data-stu-id="efa17-145">The mechanism used to transport the context ID is configurable.</span></span> <span data-ttu-id="efa17-146">這個內容識別碼可以寫入 HTTP Cookie 標頭或自訂 SOAP 標頭。</span><span class="sxs-lookup"><span data-stu-id="efa17-146">It could be either written to the HTTP cookie header or to a custom SOAP header.</span></span> <span data-ttu-id="efa17-147">自訂 SOAP 標頭方法可讓您使用此通訊協定搭配非 HTTP 通訊協定 (例如，TCP 或具名管道)。</span><span class="sxs-lookup"><span data-stu-id="efa17-147">The custom SOAP header approach makes it possible to use this protocol with non-HTTP protocols (for example, TCP or Named Pipes).</span></span> <span data-ttu-id="efa17-148">有兩個可實作這兩個選項的類別，`MessageHeaderContextManager` 和 `HttpCookieContextManager`。</span><span class="sxs-lookup"><span data-stu-id="efa17-148">There are two classes, namely `MessageHeaderContextManager` and `HttpCookieContextManager`, which implement these two options.</span></span>

<span data-ttu-id="efa17-149">這兩個類別會將內容識別碼適當地寫入訊息。</span><span class="sxs-lookup"><span data-stu-id="efa17-149">Both of them write the context ID to the message appropriately.</span></span> <span data-ttu-id="efa17-150">例如，`MessageHeaderContextManager` 類別會將內容識別碼寫入 `WriteContext` 方法的 SOAP 標頭。</span><span class="sxs-lookup"><span data-stu-id="efa17-150">For example, the `MessageHeaderContextManager` class writes it to a SOAP header in the `WriteContext` method.</span></span>

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

<span data-ttu-id="efa17-151">`ApplyContext` 類別中的 `ReadContextId` 和 `DurableInstanceContextChannelBase` 方法，可以分別叫用 `IContextManager.ReadContext` 和 `IContextManager.WriteContext`。</span><span class="sxs-lookup"><span data-stu-id="efa17-151">Both the `ApplyContext` and `ReadContextId` methods in the `DurableInstanceContextChannelBase` class invoke the `IContextManager.ReadContext` and `IContextManager.WriteContext`, respectively.</span></span> <span data-ttu-id="efa17-152">不過，不是由 `DurableInstanceContextChannelBase` 類別直接建立這些內容管理員。</span><span class="sxs-lookup"><span data-stu-id="efa17-152">However, these context managers are not directly created by the `DurableInstanceContextChannelBase` class.</span></span> <span data-ttu-id="efa17-153">而是會使用 `ContextManagerFactory` 類別來建立。</span><span class="sxs-lookup"><span data-stu-id="efa17-153">Instead it uses the `ContextManagerFactory` class to do that job.</span></span>

```csharp
IContextManager contextManager =
                ContextManagerFactory.CreateContextManager(contextType,
                this.contextStoreLocation,
                this.endpointAddress);
```

<span data-ttu-id="efa17-154">傳送通道時即可叫用 `ApplyContext` 方法。</span><span class="sxs-lookup"><span data-stu-id="efa17-154">The `ApplyContext` method is invoked by the sending channels.</span></span> <span data-ttu-id="efa17-155">然後將內容識別碼插入傳出訊息。</span><span class="sxs-lookup"><span data-stu-id="efa17-155">It injects the context ID to the outgoing messages.</span></span> <span data-ttu-id="efa17-156">接收通道便會叫用 `ReadContextId` 方法。</span><span class="sxs-lookup"><span data-stu-id="efa17-156">The `ReadContextId` method is invoked by the receiving channels.</span></span> <span data-ttu-id="efa17-157">這個方法會確定可在傳入訊息中使用內容識別碼，並將該內容識別碼新增至 `Properties` 類別的 `Message` 集合中。</span><span class="sxs-lookup"><span data-stu-id="efa17-157">This method ensures that the context ID is available in the incoming messages and adds it to the `Properties` collection of the `Message` class.</span></span> <span data-ttu-id="efa17-158">也會在無法讀取內容識別碼時擲回 `CommunicationException`，因而導致中止通道。</span><span class="sxs-lookup"><span data-stu-id="efa17-158">It also throws a `CommunicationException` in case of a failure to read the context ID and thus causes the channel to be aborted.</span></span>

```csharp
message.Properties.Add(DurableInstanceContextUtility.ContextIdProperty, contextId);
```

<span data-ttu-id="efa17-159">在繼續處理之前，您需要已了解如何使用 `Properties` 類別中的 `Message` 集合。</span><span class="sxs-lookup"><span data-stu-id="efa17-159">Before proceeding, it is important to understand the usage of the `Properties` collection in the `Message` class.</span></span> <span data-ttu-id="efa17-160">一般來說，在通道層中將資料從較低層傳遞至較高層時，就會使用此 `Properties` 集合。</span><span class="sxs-lookup"><span data-stu-id="efa17-160">Typically, this `Properties` collection is used when passing data from lower to the upper levels from the channel layer.</span></span> <span data-ttu-id="efa17-161">如此一來，就可以使用一致的方法對較高層提供需要的資料，而不用在意通訊協定詳細資料。</span><span class="sxs-lookup"><span data-stu-id="efa17-161">This way the desired data can be provided to the upper levels in a consistent manner regardless of the protocol details.</span></span> <span data-ttu-id="efa17-162">換句話說，通道層可以將內容識別碼當做 SOAP 標頭或 HTTP cookie 標頭來傳送和接收。</span><span class="sxs-lookup"><span data-stu-id="efa17-162">In other words, the channel layer can send and receive the context ID either as a SOAP header or an HTTP cookie header.</span></span> <span data-ttu-id="efa17-163">但這些較高層不需要知道這些細節，因為通道層會在 `Properties` 擊盒中提供此資訊。</span><span class="sxs-lookup"><span data-stu-id="efa17-163">But it is not necessary for the upper levels to know about these details because the channel layer makes this information available in the `Properties` collection.</span></span>

<span data-ttu-id="efa17-164">現在使用 `DurableInstanceContextChannelBase` 類別時，就必須實作將這十個必要的介面放置在適當的位置 (IOutputChannel、IInputChannel、IOutputSessionChannel、IInputSessionChannel、IRequestChannel、IReplyChannel、IRequestSessionChannel、IReplySessionChannel、IDuplexChannel、IDuplexSessionChannel)。</span><span class="sxs-lookup"><span data-stu-id="efa17-164">Now with the `DurableInstanceContextChannelBase` class in place all ten of the necessary interfaces (IOutputChannel, IInputChannel, IOutputSessionChannel, IInputSessionChannel, IRequestChannel, IReplyChannel, IRequestSessionChannel, IReplySessionChannel, IDuplexChannel, IDuplexSessionChannel) must be implemented.</span></span> <span data-ttu-id="efa17-165">它們類似每個可用的訊息交換模式（資料包、單工、雙工和其會話變異）。</span><span class="sxs-lookup"><span data-stu-id="efa17-165">They resemble every available message exchange pattern (datagram, simplex, duplex, and their sessionful variants).</span></span> <span data-ttu-id="efa17-166">這些每一個執行都會繼承先前所述的基類， `ApplyContext` 並 `ReadContextId` 適當地呼叫和。</span><span class="sxs-lookup"><span data-stu-id="efa17-166">Each of these implementations inherits the base class previously described and calls `ApplyContext` and `ReadContextId` appropriately.</span></span> <span data-ttu-id="efa17-167">例如實作 IOutputChannel 介面的 `DurableInstanceContextOutputChannel`，它會從傳送訊息的每個方法中呼叫 `ApplyContext` 方法。</span><span class="sxs-lookup"><span data-stu-id="efa17-167">For example, `DurableInstanceContextOutputChannel` - which implements the IOutputChannel interface - calls the `ApplyContext` method from each method that sends the messages.</span></span>

```csharp
public void Send(Message message, TimeSpan timeout)
{
    // Apply the context information before sending the message.
    this.ApplyContext(message);
    //…
}
```

<span data-ttu-id="efa17-168">另一方面， `DurableInstanceContextInputChannel` -這會執行 `IInputChannel` 介面-呼叫 `ReadContextId` 每個方法中的方法，以接收訊息。</span><span class="sxs-lookup"><span data-stu-id="efa17-168">On the other hand, `DurableInstanceContextInputChannel` - which implements the `IInputChannel` interface - calls the `ReadContextId` method in each method, which receives the messages.</span></span>

```csharp
public Message Receive(TimeSpan timeout)
{
    //…
      ReadContextId(message);
      return message;
}
```

<span data-ttu-id="efa17-169">此外，這些通道實作會將方法叫用委派給通道堆疊中位置更低的通道。</span><span class="sxs-lookup"><span data-stu-id="efa17-169">Apart from this, these channel implementations delegate the method invocations to the channel below them in the channel stack.</span></span> <span data-ttu-id="efa17-170">不過，工作階段變數會有一些基本邏輯，確定針對導致建立工作階段的第一個訊息而言，會傳送內容識別碼而且此內容識別碼為唯讀。</span><span class="sxs-lookup"><span data-stu-id="efa17-170">However, sessionful variants have a basic logic to make sure that the context ID is sent and is read only for the first message that causes the session to be created.</span></span>

```csharp
if (isFirstMessage)
{
//…
    this.ApplyContext(message);
    isFirstMessage = false;
}
```

<span data-ttu-id="efa17-171">然後， `DurableInstanceContextBindingElement` 類別和類別會適當地將這些通道實現新增至 WCF 通道執行時間 `DurableInstanceContextBindingElementSection` 。</span><span class="sxs-lookup"><span data-stu-id="efa17-171">These channel implementations are then added to the WCF channel runtime by the `DurableInstanceContextBindingElement` class and `DurableInstanceContextBindingElementSection` class appropriately.</span></span> <span data-ttu-id="efa17-172">如需繫結項目和繫結項目區段的詳細資訊，請參閱[HttpCookieSession](httpcookiesession.md)通道範例檔。</span><span class="sxs-lookup"><span data-stu-id="efa17-172">See the [HttpCookieSession](httpcookiesession.md) channel sample documentation for more details about binding elements and binding element sections.</span></span>

## <a name="service-model-layer-extensions"></a><span data-ttu-id="efa17-173">服務模型層延伸項目</span><span class="sxs-lookup"><span data-stu-id="efa17-173">Service Model Layer Extensions</span></span>

<span data-ttu-id="efa17-174">現在內容識別碼已周遊至各個通道層，您就可以實作服務行為以自訂執行個體化 (Instantiation)。</span><span class="sxs-lookup"><span data-stu-id="efa17-174">Now that the context ID has traveled through the channel layer, the service behavior can be implemented to customize the instantiation.</span></span> <span data-ttu-id="efa17-175">在此範例中，可以使用存放管理員，在持續存放區中載入及儲存狀態。</span><span class="sxs-lookup"><span data-stu-id="efa17-175">In this sample, a storage manager is used to load and save state from or to the persistent store.</span></span> <span data-ttu-id="efa17-176">如先前所述，這個範例提供使用 SQL Server 2005 做為其備份存放區的存放管理員。</span><span class="sxs-lookup"><span data-stu-id="efa17-176">As explained previously, this sample provides a storage manager that uses SQL Server 2005 as its backing store.</span></span> <span data-ttu-id="efa17-177">不過，您也可以將自訂存放機制新增至此延伸項目。</span><span class="sxs-lookup"><span data-stu-id="efa17-177">However, it is also possible to add custom storage mechanisms to this extension.</span></span> <span data-ttu-id="efa17-178">若要這樣做，將會宣告公用介面，而所有存放管理員都必須實作此公用介面。</span><span class="sxs-lookup"><span data-stu-id="efa17-178">To do that a public interface is declared, which must be implemented by all storage managers.</span></span>

```csharp
public interface IStorageManager
{
    object GetInstance(string contextId, Type type);
    void SaveInstance(string contextId, object state);
}
```

<span data-ttu-id="efa17-179">`SqlServerStorageManager` 類別包含預設 `IStorageManager` 實作。</span><span class="sxs-lookup"><span data-stu-id="efa17-179">The `SqlServerStorageManager` class contains the default `IStorageManager` implementation.</span></span> <span data-ttu-id="efa17-180">在其 `SaveInstance` 方法中，會使用 XmlSerializer 序列化給定的物件，並將它儲存到 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="efa17-180">In its `SaveInstance` method, the given object is serialized using the XmlSerializer and is saved to the SQL Server database.</span></span>

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

<span data-ttu-id="efa17-181">在 `GetInstance` 方法中，會針對指定的內容識別碼讀取序列化資料，而從它所建立的物件會傳回給呼叫者。</span><span class="sxs-lookup"><span data-stu-id="efa17-181">In the `GetInstance` method, the serialized data is read for a given context ID and the object constructed from it is returned to the caller.</span></span>

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

<span data-ttu-id="efa17-182">存放管理員的使用者不應該直接執行個體化這些存放管理員。</span><span class="sxs-lookup"><span data-stu-id="efa17-182">Users of these storage managers are not supposed to instantiate them directly.</span></span> <span data-ttu-id="efa17-183">使用者會使用擷取自存放管理員建立詳細資料的 `StorageManagerFactory` 類別。</span><span class="sxs-lookup"><span data-stu-id="efa17-183">They use the `StorageManagerFactory` class, which abstracts from the storage manager creation details.</span></span> <span data-ttu-id="efa17-184">這個類別包含 `GetStorageManager` 這個靜態成員，此成員會建立提供之存放管理員型別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="efa17-184">This class has one static member, `GetStorageManager`, which creates an instance of a given storage manager type.</span></span> <span data-ttu-id="efa17-185">如果型別參數為 `null`，這個方法就會建立預設 `SqlServerStorageManager` 類別的執行個體，並傳回之。</span><span class="sxs-lookup"><span data-stu-id="efa17-185">If the type parameter is `null`, this method creates an instance of the default `SqlServerStorageManager` class and returns it.</span></span> <span data-ttu-id="efa17-186">也會驗證提供的型別，以確定會實作 `IStorageManager` 介面。</span><span class="sxs-lookup"><span data-stu-id="efa17-186">It also validates the given type to make sure that it implements the `IStorageManager` interface.</span></span>

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

<span data-ttu-id="efa17-187">現在已實作從持續性儲存體 (Persistent Storage) 中讀取及寫入執行個體的必要基礎結構。</span><span class="sxs-lookup"><span data-stu-id="efa17-187">The necessary infrastructure to read and write instances from the persistent storage is implemented.</span></span> <span data-ttu-id="efa17-188">接著便需要採取變更服務行為的必要步驟。</span><span class="sxs-lookup"><span data-stu-id="efa17-188">Now the necessary steps to change the service behavior have to be taken.</span></span>

<span data-ttu-id="efa17-189">此處理序的第一個步驟為儲存內容識別碼，而這個內容識別碼會從通道層周遊至目前的 InstanceContext。</span><span class="sxs-lookup"><span data-stu-id="efa17-189">As the first step of this process we have to save the context ID, which came through the channel layer to the current InstanceContext.</span></span> <span data-ttu-id="efa17-190">InstanceCoNtext 是一個執行時間元件，可做為 WCF 發送器與服務實例之間的連結。</span><span class="sxs-lookup"><span data-stu-id="efa17-190">InstanceContext is a runtime component that acts as the link between the WCF dispatcher and the service instance.</span></span> <span data-ttu-id="efa17-191">可以用於對服務執行個體提供額外的狀態和行為。</span><span class="sxs-lookup"><span data-stu-id="efa17-191">It can be used to provide additional state and behavior to the service instance.</span></span> <span data-ttu-id="efa17-192">而這是很重要的一點，因為在工作階段通訊中，只有第一個訊息會一起傳送內容識別碼。</span><span class="sxs-lookup"><span data-stu-id="efa17-192">This is essential because in sessionful communication the context ID is sent only with the first message.</span></span>

<span data-ttu-id="efa17-193">WCF 允許擴充其 InstanceCoNtext 執行時間元件，方法是使用其可延伸物件模式來新增新的狀態和行為。</span><span class="sxs-lookup"><span data-stu-id="efa17-193">WCF allows extending its InstanceContext runtime component by adding a new state and behavior using its extensible object pattern.</span></span> <span data-ttu-id="efa17-194">可延伸物件模式用於 WCF 中，以新功能來擴充現有執行時間類別，或將新的狀態功能加入至物件。</span><span class="sxs-lookup"><span data-stu-id="efa17-194">The extensible object pattern is used in WCF to either extend existing runtime classes with new functionality or to add new state features to an object.</span></span> <span data-ttu-id="efa17-195">可擴充物件模式中有三個介面-Iextensibleobject<t> \<T> 、IExtension \<T> 和 IExtensionCollection \<T> ：</span><span class="sxs-lookup"><span data-stu-id="efa17-195">There are three interfaces in the extensible object pattern - IExtensibleObject\<T>, IExtension\<T>, and IExtensionCollection\<T>:</span></span>

- <span data-ttu-id="efa17-196">Iextensibleobject<t> \<T> 介面是由允許自訂其功能之延伸模組的物件所執行。</span><span class="sxs-lookup"><span data-stu-id="efa17-196">The IExtensibleObject\<T> interface is implemented by objects that allow extensions that customize their functionality.</span></span>

- <span data-ttu-id="efa17-197">IExtension \<T> 介面是由屬於 T 類型類別之延伸的物件所執行。</span><span class="sxs-lookup"><span data-stu-id="efa17-197">The IExtension\<T> interface is implemented by objects that are extensions of classes of type T.</span></span>

- <span data-ttu-id="efa17-198">IExtensionCollection \<T> 介面是 IExtensions 的集合，可讓您依其類型來抓取 IExtensions。</span><span class="sxs-lookup"><span data-stu-id="efa17-198">The IExtensionCollection\<T> interface is a collection of IExtensions that allows for retrieving IExtensions by their type.</span></span>

<span data-ttu-id="efa17-199">因此，您應該建立 InstanceContextExtension 類別，並實作 IExtension 介面及定義必要的狀態以儲存內容識別碼。</span><span class="sxs-lookup"><span data-stu-id="efa17-199">Therefore an InstanceContextExtension class should be created that implements the IExtension interface and defines the required state to save the context ID.</span></span> <span data-ttu-id="efa17-200">這個類別也會提供一種狀態，保留正在使用的存放管理員。</span><span class="sxs-lookup"><span data-stu-id="efa17-200">This class also provides the state to hold the storage manager being used.</span></span> <span data-ttu-id="efa17-201">一旦儲存新狀態，就無法進行修改。</span><span class="sxs-lookup"><span data-stu-id="efa17-201">Once the new state is saved, it should not be possible to modify it.</span></span> <span data-ttu-id="efa17-202">所以您應該在建構執行個體時提供狀態，並將該狀態儲存至執行個體，並只能透過唯讀屬性來進行存取。</span><span class="sxs-lookup"><span data-stu-id="efa17-202">Therefore the state is provided and saved to the instance at the time it is being constructed and then only accessible using read-only properties.</span></span>

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

<span data-ttu-id="efa17-203">InstanceContextInitializer 類別會實作 IInstanceContextInitializer 介面，並將執行個體內容延伸項目新增至已建構之 InstanceContext 的 Extensions 集合中。</span><span class="sxs-lookup"><span data-stu-id="efa17-203">The InstanceContextInitializer class implements the IInstanceContextInitializer interface and adds the instance context extension to the Extensions collection of the InstanceContext being constructed.</span></span>

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

<span data-ttu-id="efa17-204">如先前所述，您會從 `Properties` 類別的 `Message` 集合中讀取內容識別碼，並將它傳遞至延伸類別的建構函式。</span><span class="sxs-lookup"><span data-stu-id="efa17-204">As described earlier the context ID is read from the `Properties` collection of the `Message` class and passed to the constructor of the extension class.</span></span> <span data-ttu-id="efa17-205">這樣便可示範如何使用一致的方法，在各層之間交換資訊。</span><span class="sxs-lookup"><span data-stu-id="efa17-205">This demonstrates how information can be exchanged between the layers in a consistent manner.</span></span>

<span data-ttu-id="efa17-206">下一個重要的步驟為覆寫服務執行個體的建立處理序。</span><span class="sxs-lookup"><span data-stu-id="efa17-206">The next important step is overriding the service instance creation process.</span></span> <span data-ttu-id="efa17-207">WCF 允許執行自訂的具現化行為，並使用 IInstanceProvider 介面將它們連結至執行時間。</span><span class="sxs-lookup"><span data-stu-id="efa17-207">WCF allows implementing custom instantiation behaviors and hooking them up to the runtime using the IInstanceProvider interface.</span></span> <span data-ttu-id="efa17-208">將實作新 `InstanceProvider` 類別以執行該工作。</span><span class="sxs-lookup"><span data-stu-id="efa17-208">The new `InstanceProvider` class is implemented to do that job.</span></span> <span data-ttu-id="efa17-209">在此函數中，接受來自執行個體提供者的服務類型。</span><span class="sxs-lookup"><span data-stu-id="efa17-209">The service type expected from the instance provider is accepted in the constructor.</span></span> <span data-ttu-id="efa17-210">稍後將使用此服務類型來建立新的執行個體。</span><span class="sxs-lookup"><span data-stu-id="efa17-210">Later this is used to create new instances.</span></span> <span data-ttu-id="efa17-211">在 `GetInstance` 執行期間，會建立存放管理員的實例來尋找保存的實例。</span><span class="sxs-lookup"><span data-stu-id="efa17-211">In the `GetInstance` implementation, an instance of a storage manager is created looking for a persisted instance.</span></span> <span data-ttu-id="efa17-212">如果 `null` 傳回，則會具現化服務類型的新實例，並將其傳回給呼叫端。</span><span class="sxs-lookup"><span data-stu-id="efa17-212">If it returns `null`, then a new instance of the service type is instantiated and returned to the caller.</span></span>

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

<span data-ttu-id="efa17-213">下一個重要步驟是將 `InstanceContextExtension` 、 `InstanceContextInitializer` 和 `InstanceProvider` 類別安裝到服務模型執行時間。</span><span class="sxs-lookup"><span data-stu-id="efa17-213">The next important step is to install the `InstanceContextExtension`, `InstanceContextInitializer`, and `InstanceProvider` classes into the service model runtime.</span></span> <span data-ttu-id="efa17-214">您可以使用自訂屬性以標示服務實作類別，便可安裝行為。</span><span class="sxs-lookup"><span data-stu-id="efa17-214">A custom attribute could be used to mark the service implementation classes to install the behavior.</span></span> <span data-ttu-id="efa17-215">`DurableInstanceContextAttribute` 中包含這個屬性的實作，並且會實作 `IServiceBehavior` 介面以擴充整個服務執行階段。</span><span class="sxs-lookup"><span data-stu-id="efa17-215">The `DurableInstanceContextAttribute` contains the implementation for this attribute and it implements the `IServiceBehavior` interface to extend the entire service runtime.</span></span>

<span data-ttu-id="efa17-216">這個類別所擁有的屬性，可以接受要使用的存放管理員類型。</span><span class="sxs-lookup"><span data-stu-id="efa17-216">This class has a property that accepts the type of the storage manager to be used.</span></span> <span data-ttu-id="efa17-217">如此一來，此實作為可讓使用者指定自己 `IStorageManager` 的實作為這個屬性的參數。</span><span class="sxs-lookup"><span data-stu-id="efa17-217">In this way, the implementation enables the users to specify their own `IStorageManager` implementation as parameter of this attribute.</span></span>

<span data-ttu-id="efa17-218">在 `ApplyDispatchBehavior` 執行 `InstanceContextMode` 時， `ServiceBehavior` 會驗證目前屬性的。</span><span class="sxs-lookup"><span data-stu-id="efa17-218">In the `ApplyDispatchBehavior` implementation, the `InstanceContextMode` of the current `ServiceBehavior` attribute is being verified.</span></span> <span data-ttu-id="efa17-219">如果這個屬性設定為 Singleton，就無法啟用永久性執行個體，並且會擲回 `InvalidOperationException` 以通知主機。</span><span class="sxs-lookup"><span data-stu-id="efa17-219">If this property is set to Singleton, enabling durable instancing is not possible and an `InvalidOperationException` is thrown to notify the host.</span></span>

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

<span data-ttu-id="efa17-220">之後，便會在針對每個端點所建立的 `DispatchRuntime` 中，建立並安裝存放管理員執行個體、執行個體內容初始設定式和執行個體提供者。</span><span class="sxs-lookup"><span data-stu-id="efa17-220">After this the instances of the storage manager, instance context initializer, and the instance provider are created and installed in the `DispatchRuntime` created for every endpoint.</span></span>

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

<span data-ttu-id="efa17-221">到目前為止，這個範例產生的通道可對自訂內容識別碼交換啟用自訂網路通訊協定，也會覆寫預設執行個體行為以從持續性儲存體載入執行個體。</span><span class="sxs-lookup"><span data-stu-id="efa17-221">In summary so far, this sample has produced a channel that enabled the custom wire protocol for custom context ID exchange and it also overwrites the default instancing behavior to load the instances from the persistent storage.</span></span>

<span data-ttu-id="efa17-222">不會變得是將服務執行個體儲存至持續性儲存體。</span><span class="sxs-lookup"><span data-stu-id="efa17-222">What is left is a way to save the service instance to the persistent storage.</span></span> <span data-ttu-id="efa17-223">如前所述，已提供必要的功能讓您在 `IStorageManager` 實作中儲存狀態。</span><span class="sxs-lookup"><span data-stu-id="efa17-223">As discussed previously, there is already the required functionality to save the state in an `IStorageManager` implementation.</span></span> <span data-ttu-id="efa17-224">我們現在必須將此與 WCF 執行時間進行整合。</span><span class="sxs-lookup"><span data-stu-id="efa17-224">We now must integrate this with the WCF runtime.</span></span> <span data-ttu-id="efa17-225">也需要適用於服務實作類別方法的其他屬性。</span><span class="sxs-lookup"><span data-stu-id="efa17-225">Another attribute is required that is applicable to the methods in the service implementation class.</span></span> <span data-ttu-id="efa17-226">而這個屬性應該會套用至變更服務執行個體狀態的方法。</span><span class="sxs-lookup"><span data-stu-id="efa17-226">This attribute is supposed to be applied to the methods that change the state of the service instance.</span></span>

<span data-ttu-id="efa17-227">`SaveStateAttribute` 類別會實作此功能。</span><span class="sxs-lookup"><span data-stu-id="efa17-227">The `SaveStateAttribute` class implements this functionality.</span></span> <span data-ttu-id="efa17-228">它也會 `IOperationBehavior` 執行類別，以修改每個作業的 WCF 執行時間。</span><span class="sxs-lookup"><span data-stu-id="efa17-228">It also implements `IOperationBehavior` class to modify the WCF runtime for each operation.</span></span> <span data-ttu-id="efa17-229">當使用這個屬性來標記方法時，WCF 執行時間會在 `ApplyBehavior` 結構化適當的時叫用方法 `DispatchOperation` 。</span><span class="sxs-lookup"><span data-stu-id="efa17-229">When a method is marked with this attribute, the WCF runtime invokes the `ApplyBehavior` method while the appropriate `DispatchOperation` is being constructed.</span></span> <span data-ttu-id="efa17-230">這個方法的實行中有一行程式碼：</span><span class="sxs-lookup"><span data-stu-id="efa17-230">There is a single line of code in this method implementation:</span></span>

```csharp
dispatch.Invoker = new OperationInvoker(dispatch.Invoker);
```

<span data-ttu-id="efa17-231">這個指示會建立 `OperationInvoker` 型別的執行個體，並將它指派至已建構之 `Invoker` 的 `DispatchOperation` 屬性。</span><span class="sxs-lookup"><span data-stu-id="efa17-231">This instruction creates an instance of `OperationInvoker` type and assigns it to the `Invoker` property of the `DispatchOperation` being constructed.</span></span> <span data-ttu-id="efa17-232">`OperationInvoker` 類別則是對 `DispatchOperation` 所建立之預設作業啟動程式的包裝函式。</span><span class="sxs-lookup"><span data-stu-id="efa17-232">The `OperationInvoker` class is a wrapper for the default operation invoker created for the `DispatchOperation`.</span></span> <span data-ttu-id="efa17-233">此類別會實作 `IOperationInvoker` 介面。</span><span class="sxs-lookup"><span data-stu-id="efa17-233">This class implements the `IOperationInvoker` interface.</span></span> <span data-ttu-id="efa17-234">在 `Invoke` 方法執行中，會將實際的方法叫用委派給內部作業啟動項。</span><span class="sxs-lookup"><span data-stu-id="efa17-234">In the `Invoke` method implementation, the actual method invocation is delegated to the inner operation invoker.</span></span> <span data-ttu-id="efa17-235">但是在傳回結果之前，可以使用 `InstanceContext` 中的存放管理員來儲存服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="efa17-235">However, before returning the results the storage manager in the `InstanceContext` is used to save the service instance.</span></span>

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

## <a name="using-the-extension"></a><span data-ttu-id="efa17-236">使用延伸項目</span><span class="sxs-lookup"><span data-stu-id="efa17-236">Using the Extension</span></span>

<span data-ttu-id="efa17-237">通道層和服務模型層延伸都已完成，而且現在可以在 WCF 應用程式中使用。</span><span class="sxs-lookup"><span data-stu-id="efa17-237">Both the channel layer and service model layer extensions are done and they can now be used in WCF applications.</span></span> <span data-ttu-id="efa17-238">服務必須使用自訂系結將通道新增至通道堆疊，然後以適當的屬性標示服務執行類別。</span><span class="sxs-lookup"><span data-stu-id="efa17-238">Services must add the channel into the channel stack using a custom binding and then mark the service implementation classes with the appropriate attributes.</span></span>

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

<span data-ttu-id="efa17-239">用戶端應用程式必須使用自訂繫結，將 DurableInstanceContextChannel 新增至通道堆疊。</span><span class="sxs-lookup"><span data-stu-id="efa17-239">Client applications must add the DurableInstanceContextChannel into the channel stack using a custom binding.</span></span> <span data-ttu-id="efa17-240">若要以宣告方式在組態檔中設定通道，則必須將繫結項目區段新增至繫結項目延伸集合中。</span><span class="sxs-lookup"><span data-stu-id="efa17-240">To configure the channel declaratively in the configuration file, the binding element section has to be added to the binding element extensions collection.</span></span>

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

<span data-ttu-id="efa17-241">現在繫結程序項目就和其他標準繫結程序項目一樣，都可以搭配使用自訂繫結程序：</span><span class="sxs-lookup"><span data-stu-id="efa17-241">Now the binding element can be used with a custom binding just like other standard binding elements:</span></span>

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

## <a name="conclusion"></a><span data-ttu-id="efa17-242">結論</span><span class="sxs-lookup"><span data-stu-id="efa17-242">Conclusion</span></span>

<span data-ttu-id="efa17-243">這個範例會顯示如何建立自訂通訊協定通道，以及如何自訂服務行為進而啟用它。</span><span class="sxs-lookup"><span data-stu-id="efa17-243">This sample showed how to create a custom protocol channel and how to customize the service behavior to enable it.</span></span>

<span data-ttu-id="efa17-244">讓使用者使用組態區段指定 `IStorageManager` 實作，將可進一步增進延伸項目的功能。</span><span class="sxs-lookup"><span data-stu-id="efa17-244">The extension can be further improved by letting users specify the `IStorageManager` implementation using a configuration section.</span></span> <span data-ttu-id="efa17-245">這樣做便可修改備份存放區，而不需要重新編譯服務程式碼。</span><span class="sxs-lookup"><span data-stu-id="efa17-245">This makes it possible to modify the backing store without recompiling the service code.</span></span>

<span data-ttu-id="efa17-246">您甚至可以嘗試實作類別 (例如，`StateBag`)，而這個類別會封裝執行個體的狀態。</span><span class="sxs-lookup"><span data-stu-id="efa17-246">Furthermore you could try to implement a class (for example, `StateBag`), which encapsulates the state of the instance.</span></span> <span data-ttu-id="efa17-247">該類別也負責在變更狀態時保存狀態。</span><span class="sxs-lookup"><span data-stu-id="efa17-247">That class is responsible for persisting the state whenever it changes.</span></span> <span data-ttu-id="efa17-248">透過這個方法，您就可以避免使用 `SaveState` 屬性並更精確地執行保存工作 (例如，可以在實際上變更狀態時保存狀態，而不是每次呼叫具有 `SaveState` 屬性的方法時就儲存狀態)。</span><span class="sxs-lookup"><span data-stu-id="efa17-248">This way you can avoid using the `SaveState` attribute and perform the persisting work more accurately (for example, you could persist the state when the state is actually changed rather than saving it each time when a method with the `SaveState` attribute is called).</span></span>

<span data-ttu-id="efa17-249">當您執行範例時，會顯示如下的輸出。</span><span class="sxs-lookup"><span data-stu-id="efa17-249">When you run the sample, the following output is displayed.</span></span> <span data-ttu-id="efa17-250">用戶端會將兩個項目新增至購物車，然後從服務中取得其購物車的項目清單。</span><span class="sxs-lookup"><span data-stu-id="efa17-250">The client adds two items to its shopping cart and then gets the list of items in its shopping cart from the service.</span></span> <span data-ttu-id="efa17-251">在每個主控台視窗中按下 ENTER 鍵，即可關閉服務與用戶端。</span><span class="sxs-lookup"><span data-stu-id="efa17-251">Press ENTER in each console window to shut down the service and client.</span></span>

```console
Enter the name of the product: apples
Enter the name of the product: bananas

Shopping cart currently contains the following items.
apples
bananas
Press ENTER to shut down client
```

> [!NOTE]
> <span data-ttu-id="efa17-252">重建服務則會覆寫資料庫檔案。</span><span class="sxs-lookup"><span data-stu-id="efa17-252">Rebuilding the service overwrites the database file.</span></span> <span data-ttu-id="efa17-253">若要觀察每次執行範例時所保留的狀態，請在各個執行動作之間務必不要重建範例。</span><span class="sxs-lookup"><span data-stu-id="efa17-253">To observe state preserved across multiple runs of the sample, be sure not to rebuild the sample between runs.</span></span>

#### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="efa17-254">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="efa17-254">To set up, build, and run the sample</span></span>

1. <span data-ttu-id="efa17-255">請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="efa17-255">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>

2. <span data-ttu-id="efa17-256">若要建立方案，請依照[建立 Windows Communication Foundation 範例](building-the-samples.md)中的指示進行。</span><span class="sxs-lookup"><span data-stu-id="efa17-256">To build the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>

3. <span data-ttu-id="efa17-257">若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="efa17-257">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>

> [!NOTE]
> <span data-ttu-id="efa17-258">您必須執行 SQL Server 2005 或 SQL Express 2005，才能執行此範例。</span><span class="sxs-lookup"><span data-stu-id="efa17-258">You must be running SQL Server 2005 or SQL Express 2005 to run this sample.</span></span> <span data-ttu-id="efa17-259">如果正在執行 SQL Server 2005，則必須修改服務之連線字串的組態。</span><span class="sxs-lookup"><span data-stu-id="efa17-259">If you are running SQL Server 2005, you must modify the configuration of the service's connection string.</span></span> <span data-ttu-id="efa17-260">在多台電腦中執行時，只有伺服器電腦上需要 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="efa17-260">When running cross-machine, SQL Server is only required on the server machine.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="efa17-261">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="efa17-261">The samples may already be installed on your machine.</span></span> <span data-ttu-id="efa17-262">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="efa17-262">Check for the following (default) directory before continuing.</span></span>
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> <span data-ttu-id="efa17-263">如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="efa17-263">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="efa17-264">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="efa17-264">This sample is located in the following directory.</span></span>
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Instancing\Durable`
