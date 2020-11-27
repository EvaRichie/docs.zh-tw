---
title: 自訂資料流升級
ms.date: 03/30/2017
ms.assetid: e3da85c8-57f3-4e32-a4cb-50123f30fea6
ms.openlocfilehash: 3ef0f59a5d63c24188b29cb7a38db2d6323d80ee
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96295573"
---
# <a name="custom-stream-upgrades"></a><span data-ttu-id="fda6d-102">自訂資料流升級</span><span class="sxs-lookup"><span data-stu-id="fda6d-102">Custom Stream Upgrades</span></span>

<span data-ttu-id="fda6d-103">以資料流為導向的傳輸 (例如 TCP 和具名管道) 會在用戶端和伺服器之間的連續位元組資料流上進行作業。</span><span class="sxs-lookup"><span data-stu-id="fda6d-103">Stream-oriented transports such as TCP and Named Pipes operate on a continuous stream of bytes between the client and server.</span></span> <span data-ttu-id="fda6d-104">透過 <xref:System.IO.Stream> 物件即可實現此資料流。</span><span class="sxs-lookup"><span data-stu-id="fda6d-104">This stream is realized by a  <xref:System.IO.Stream> object.</span></span> <span data-ttu-id="fda6d-105">在資料流升級中，用戶端會想將選用通訊協定層新增至通道堆疊，並也要求其他通訊通道端也這樣執行。</span><span class="sxs-lookup"><span data-stu-id="fda6d-105">In a stream upgrade, the client wants to add an optional protocol layer to the channel stack, and asks the other end of the communication channel to do so.</span></span> <span data-ttu-id="fda6d-106">資料流升級包含使用升級的物件取代原始的 <xref:System.IO.Stream> 物件。</span><span class="sxs-lookup"><span data-stu-id="fda6d-106">The stream upgrade consists in replacing the original <xref:System.IO.Stream> object with an upgraded one.</span></span>  
  
 <span data-ttu-id="fda6d-107">例如，您可以直接在傳輸資料流的上方建立壓縮資料流。</span><span class="sxs-lookup"><span data-stu-id="fda6d-107">For example, you can build a compression stream directly on top of the transport stream.</span></span> <span data-ttu-id="fda6d-108">在這個情況下，會使用包裝壓縮 <xref:System.IO.Stream> (繞著原始的物件) 的物件取代原始傳輸 <xref:System.IO.Stream>。</span><span class="sxs-lookup"><span data-stu-id="fda6d-108">In this case the original transport <xref:System.IO.Stream> is replaced with one that wraps the compression <xref:System.IO.Stream> around the original one.</span></span>  
  
 <span data-ttu-id="fda6d-109">您可套用多個資料流升級，每一個都包裝前一個。</span><span class="sxs-lookup"><span data-stu-id="fda6d-109">You can apply multiple stream upgrades, each wrapping the preceding one.</span></span>  
  
## <a name="how-stream-upgrades-work"></a><span data-ttu-id="fda6d-110">資料流升級的運作方式</span><span class="sxs-lookup"><span data-stu-id="fda6d-110">How Stream Upgrades Work</span></span>  

 <span data-ttu-id="fda6d-111">資料流升級處理序包含了四個元件。</span><span class="sxs-lookup"><span data-stu-id="fda6d-111">There are four components to the stream upgrade process.</span></span>  
  
1. <span data-ttu-id="fda6d-112">升級資料流程 *啟動器* 會開始處理常式：在執行時間，它可以起始對其連接另一端的要求，以升級通道傳輸層。</span><span class="sxs-lookup"><span data-stu-id="fda6d-112">An upgrade stream *Initiator* begins the process: at run-time it can initiate a request to the other end of its connection to upgrade the channel transport layer.</span></span>  
  
2. <span data-ttu-id="fda6d-113">升級資料流程 *接受器* 執行升級：在執行時間，它會從另一台電腦接收升級要求，並在可能的情況下接受升級。</span><span class="sxs-lookup"><span data-stu-id="fda6d-113">An upgrade stream *Acceptor* carries out the upgrade: at run-time it receives the upgrade request from the other machine, and if possible, accepts the upgrade.</span></span>  
  
3. <span data-ttu-id="fda6d-114">升級 *提供者* 會在用戶端上建立 *起始* 端，並在伺服器上建立 *接受器* 。</span><span class="sxs-lookup"><span data-stu-id="fda6d-114">An upgrade *Provider* creates the *Initiator* on the client and the *Acceptor* on the server.</span></span>  
  
4. <span data-ttu-id="fda6d-115">資料流程升級 *綁定* 項會加入至服務和用戶端上的系結，並在執行時間建立提供者。</span><span class="sxs-lookup"><span data-stu-id="fda6d-115">A stream upgrade *Binding Element* is added to the bindings on the service and the client, and creates the provider at runtime.</span></span>  
  
 <span data-ttu-id="fda6d-116">在多重升級的狀況中請特別注意，啟動器和接受器會封裝狀態機器，以強制執行可用於每次初始化的升級轉換。</span><span class="sxs-lookup"><span data-stu-id="fda6d-116">Note that in the case of multiple upgrades, the Initiator and Acceptor encapsulate state machines to enforce which upgrade transitions are valid for each Initiation.</span></span>  
  
## <a name="how-to-implement-a-stream-upgrade"></a><span data-ttu-id="fda6d-117">如何實作資料流升級</span><span class="sxs-lookup"><span data-stu-id="fda6d-117">How to Implement a Stream Upgrade</span></span>  

 <span data-ttu-id="fda6d-118">Windows Communication Foundation (WCF) 提供四個 `abstract` 您可以執行的類別：</span><span class="sxs-lookup"><span data-stu-id="fda6d-118">Windows Communication Foundation (WCF) provides four `abstract` classes that you can implement:</span></span>  
  
- <xref:System.ServiceModel.Channels.StreamUpgradeInitiator?displayProperty=nameWithType>  
  
- <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor?displayProperty=nameWithType>  
  
- <xref:System.ServiceModel.Channels.StreamUpgradeProvider?displayProperty=nameWithType>  
  
- <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement?displayProperty=nameWithType>  
  
 <span data-ttu-id="fda6d-119">若要實作自訂資料流升級，請執行下列動作。</span><span class="sxs-lookup"><span data-stu-id="fda6d-119">To implement a custom stream upgrade, do the following.</span></span> <span data-ttu-id="fda6d-120">這個程序會同時在用戶端和伺服器電腦上實作最小的資料流升級處理序。</span><span class="sxs-lookup"><span data-stu-id="fda6d-120">This procedure implements a minimal stream upgrade process on both the client and server machines.</span></span>  
  
1. <span data-ttu-id="fda6d-121">建立會實作 <xref:System.ServiceModel.Channels.StreamUpgradeInitiator> 的類別。</span><span class="sxs-lookup"><span data-stu-id="fda6d-121">Create a class that implements <xref:System.ServiceModel.Channels.StreamUpgradeInitiator>.</span></span>  
  
    1. <span data-ttu-id="fda6d-122">覆寫 <xref:System.ServiceModel.Channels.StreamUpgradeInitiator.InitiateUpgrade%2A> 方法以讓資料流進行升級，並傳回升級的資料流。</span><span class="sxs-lookup"><span data-stu-id="fda6d-122">Override the <xref:System.ServiceModel.Channels.StreamUpgradeInitiator.InitiateUpgrade%2A> method to take in the stream to be upgraded, and return the upgraded stream.</span></span> <span data-ttu-id="fda6d-123">這個方法會以同步方式執行，也會有使用非同步方式初始化升級的類似方法。</span><span class="sxs-lookup"><span data-stu-id="fda6d-123">This method works synchronously; there are analogous methods to initiate the upgrade asynchronously.</span></span>  
  
    2. <span data-ttu-id="fda6d-124">覆寫 <xref:System.ServiceModel.Channels.StreamUpgradeInitiator.GetNextUpgrade%2A> 方法以檢查其他升級。</span><span class="sxs-lookup"><span data-stu-id="fda6d-124">Override the <xref:System.ServiceModel.Channels.StreamUpgradeInitiator.GetNextUpgrade%2A> method to check for additional upgrades.</span></span>  
  
2. <span data-ttu-id="fda6d-125">建立會實作 <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor> 的類別。</span><span class="sxs-lookup"><span data-stu-id="fda6d-125">Create a class that implements <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor>.</span></span>  
  
    1. <span data-ttu-id="fda6d-126">覆寫 <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor.AcceptUpgrade%2A> 方法以讓資料流進行升級，並傳回升級的資料流。</span><span class="sxs-lookup"><span data-stu-id="fda6d-126">Override the <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor.AcceptUpgrade%2A> method to take in the stream to be upgraded, and return the upgraded stream.</span></span> <span data-ttu-id="fda6d-127">這個方法會以同步方式執行，也會有使用非同步方式接受升級的類似方法。</span><span class="sxs-lookup"><span data-stu-id="fda6d-127">This method works synchronously; there are analogous methods to accept the upgrade asynchronously.</span></span>  
  
    2. <span data-ttu-id="fda6d-128">覆寫 <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor.CanUpgrade%2A> 方法以判斷此時升級處理序中的升級接受器是否支援所要求的升級。</span><span class="sxs-lookup"><span data-stu-id="fda6d-128">Override the <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor.CanUpgrade%2A> method to determine if the upgrade requested is supported by this upgrade acceptor at this point in the upgrade process.</span></span>  
  
3. <span data-ttu-id="fda6d-129">建立會實作 <xref:System.ServiceModel.Channels.StreamUpgradeProvider> 的類別。</span><span class="sxs-lookup"><span data-stu-id="fda6d-129">Create a class the implements <xref:System.ServiceModel.Channels.StreamUpgradeProvider>.</span></span> <span data-ttu-id="fda6d-130">覆寫 <xref:System.ServiceModel.Channels.StreamUpgradeProvider.CreateUpgradeAcceptor%2A> 和 <xref:System.ServiceModel.Channels.StreamUpgradeProvider.CreateUpgradeInitiator%2A> 方法，以傳回在步驟 2 和 1 中所定義的接受器和啟動器執行個體。</span><span class="sxs-lookup"><span data-stu-id="fda6d-130">Override the <xref:System.ServiceModel.Channels.StreamUpgradeProvider.CreateUpgradeAcceptor%2A> and the <xref:System.ServiceModel.Channels.StreamUpgradeProvider.CreateUpgradeInitiator%2A> methods to return instances of the acceptor and initiator defined in steps 2 and 1.</span></span>  
  
4. <span data-ttu-id="fda6d-131">建立會實作 <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement> 的類別。</span><span class="sxs-lookup"><span data-stu-id="fda6d-131">Create a class that implements <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement>.</span></span>  
  
    1. <span data-ttu-id="fda6d-132">覆寫用戶端上的 <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement.BuildClientStreamUpgradeProvider%2A> 方法和服務上的 <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement.BuildServerStreamUpgradeProvider%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="fda6d-132">Override the <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement.BuildClientStreamUpgradeProvider%2A> method on the client and the <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement.BuildServerStreamUpgradeProvider%2A> method on the service.</span></span>  
  
    2. <span data-ttu-id="fda6d-133">覆寫用戶端上的 <xref:System.ServiceModel.Channels.BindingElement.BuildChannelFactory%2A> 方法和服務上的 <xref:System.ServiceModel.Channels.BindingElement.BuildChannelListener%2A> 方法，以將升級繫結項目新增至 <xref:System.ServiceModel.Channels.BindingContext.BindingParameters%2A>。</span><span class="sxs-lookup"><span data-stu-id="fda6d-133">Override the <xref:System.ServiceModel.Channels.BindingElement.BuildChannelFactory%2A> method on the client and the <xref:System.ServiceModel.Channels.BindingElement.BuildChannelListener%2A> method on the service to add the upgrade Binding Element to <xref:System.ServiceModel.Channels.BindingContext.BindingParameters%2A>.</span></span>  
  
5. <span data-ttu-id="fda6d-134">將新資料流升級繫結項目新增至伺服器和用戶端電腦上的繫結。</span><span class="sxs-lookup"><span data-stu-id="fda6d-134">Add the new stream upgrade binding element to bindings on the server and client machines.</span></span>  
  
## <a name="security-upgrades"></a><span data-ttu-id="fda6d-135">安全性升級</span><span class="sxs-lookup"><span data-stu-id="fda6d-135">Security Upgrades</span></span>  

 <span data-ttu-id="fda6d-136">新增安全性升級是一般資料流升級處理序的特殊版本。</span><span class="sxs-lookup"><span data-stu-id="fda6d-136">Adding a security upgrade is a specialized version of the general stream upgrade process.</span></span>  
  
 <span data-ttu-id="fda6d-137">WCF 已提供兩個用來升級資料流程安全性的繫結項目。</span><span class="sxs-lookup"><span data-stu-id="fda6d-137">WCF already provides two binding elements for upgrading stream security.</span></span> <span data-ttu-id="fda6d-138">傳輸層安全性的組態是由 <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement> 和 <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement> 所封裝，而您可以設定這兩項並新增至自訂繫結。</span><span class="sxs-lookup"><span data-stu-id="fda6d-138">The configuration of transport-level security is encapsulated by the <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement> and the <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement> which can be configured and added to a custom binding.</span></span> <span data-ttu-id="fda6d-139">這些繫結項目會擴充 <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement> 類別，而這個類別會建置用戶端和伺服器的資料流升級提供者。</span><span class="sxs-lookup"><span data-stu-id="fda6d-139">These binding elements extend the <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement> class that builds the client and server stream upgrade providers.</span></span> <span data-ttu-id="fda6d-140">這些繫結項目擁有的方法會建立特殊的安全性資料流升級提供者類別 (這些類別不是 `public`)，因此對於這兩個類別來說，您只需要將繫結項目新增至繫結即可。</span><span class="sxs-lookup"><span data-stu-id="fda6d-140">These binding elements have methods that create the specialized security stream upgrade provider classes, which are not `public`, so for these two cases all you need to do is to add the binding element to the binding.</span></span>  
  
 <span data-ttu-id="fda6d-141">針對上述兩個繫結項目不符合的安全性案例，這三個與安全性相關的 `abstract` 類別都是衍生自上述的啟動器、接受器和提供者基底類別：</span><span class="sxs-lookup"><span data-stu-id="fda6d-141">For security scenarios not met by the above two binding elements, three security-related `abstract` classes are derived from the above initiator, acceptor and provider base classes:</span></span>  
  
1. <xref:System.ServiceModel.Channels.StreamSecurityUpgradeInitiator?displayProperty=nameWithType>  
  
2. <xref:System.ServiceModel.Channels.StreamSecurityUpgradeAcceptor?displayProperty=nameWithType>  
  
3. <xref:System.ServiceModel.Channels.StreamSecurityUpgradeProvider?displayProperty=nameWithType>  
  
 <span data-ttu-id="fda6d-142">實作安全性資料流升級的處理序和先前所述一樣，差別在於您需要從這三個類別中衍生其他項目。</span><span class="sxs-lookup"><span data-stu-id="fda6d-142">The process of implementing a security stream upgrade is the same as before, with the difference that you would derive from these three classes.</span></span> <span data-ttu-id="fda6d-143">覆寫這些類別中的其他屬性，以對執行階段提供安全性資訊。</span><span class="sxs-lookup"><span data-stu-id="fda6d-143">Override the additional properties in these classes to supply security information to the runtime.</span></span>  
  
## <a name="multiple-upgrades"></a><span data-ttu-id="fda6d-144">多重升級</span><span class="sxs-lookup"><span data-stu-id="fda6d-144">Multiple Upgrades</span></span>  

 <span data-ttu-id="fda6d-145">若要建立其他升級要求，請重複上述處理序：建立 <xref:System.ServiceModel.Channels.StreamUpgradeProvider> 和繫結項目的其他延伸項目。</span><span class="sxs-lookup"><span data-stu-id="fda6d-145">To create additional upgrade requests repeat the above process: create additional extensions of <xref:System.ServiceModel.Channels.StreamUpgradeProvider> and binding elements.</span></span> <span data-ttu-id="fda6d-146">將繫結項目新增至繫結。</span><span class="sxs-lookup"><span data-stu-id="fda6d-146">Add the binding elements to the binding.</span></span> <span data-ttu-id="fda6d-147">從第一個新增至繫結的繫結項目開始，循序處理其他繫結項目。</span><span class="sxs-lookup"><span data-stu-id="fda6d-147">The additional binding elements are processed sequentially, starting with the first binding element added to the binding.</span></span> <span data-ttu-id="fda6d-148">在 <xref:System.ServiceModel.Channels.BindingElement.BuildChannelFactory%2A> 和 <xref:System.ServiceModel.Channels.BindingElement.BuildChannelListener%2A> 中，每個升級提供者都可以判斷如何在之前存在的升級繫結參數上自行分層。</span><span class="sxs-lookup"><span data-stu-id="fda6d-148">In <xref:System.ServiceModel.Channels.BindingElement.BuildChannelFactory%2A> and <xref:System.ServiceModel.Channels.BindingElement.BuildChannelListener%2A> each upgrade provider can determine how to layer itself on any pre-existing upgrade binding parameters.</span></span> <span data-ttu-id="fda6d-149">接著應該以新的複合升級繫結參數來取代現有的升級繫結參數。</span><span class="sxs-lookup"><span data-stu-id="fda6d-149">It should then replace the existing upgrade binding parameter with a new composite upgrade binding parameter.</span></span>  
  
 <span data-ttu-id="fda6d-150">此外，一個升級提供者可以支援多個升級。</span><span class="sxs-lookup"><span data-stu-id="fda6d-150">Alternatively, one upgrade provider can support multiple upgrades.</span></span> <span data-ttu-id="fda6d-151">例如，您可能想要實作可同時支援安全性和壓縮的自訂資料流升級提供者。</span><span class="sxs-lookup"><span data-stu-id="fda6d-151">For example, you might want to implement a custom stream upgrade provider that supports both security and compression.</span></span> <span data-ttu-id="fda6d-152">請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="fda6d-152">Do the following steps:</span></span>  
  
1. <span data-ttu-id="fda6d-153">子類別化 <xref:System.ServiceModel.Channels.StreamSecurityUpgradeProvider> 以撰寫會建立啟動器和接受器的提供者類別。</span><span class="sxs-lookup"><span data-stu-id="fda6d-153">Subclass <xref:System.ServiceModel.Channels.StreamSecurityUpgradeProvider> to write the provider class that creates the Initiator and Acceptor.</span></span>  
  
2. <span data-ttu-id="fda6d-154">子類別化 <xref:System.ServiceModel.Channels.StreamSecurityUpgradeInitiator> 以確定覆寫 <xref:System.ServiceModel.Channels.StreamUpgradeInitiator.GetNextUpgrade%2A> 方法，進而按照順序傳回壓縮資料流和安全資料流的內容類型。</span><span class="sxs-lookup"><span data-stu-id="fda6d-154">Subclass the <xref:System.ServiceModel.Channels.StreamSecurityUpgradeInitiator> making sure to override the <xref:System.ServiceModel.Channels.StreamUpgradeInitiator.GetNextUpgrade%2A> method to return the content types for the compression stream and the secure stream in order.</span></span>  
  
3. <span data-ttu-id="fda6d-155">子類別化瞭解其 <xref:System.ServiceModel.Channels.StreamSecurityUpgradeAcceptor> 方法之自訂內容類型的 <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor.CanUpgrade%2A>。</span><span class="sxs-lookup"><span data-stu-id="fda6d-155">Subclass the <xref:System.ServiceModel.Channels.StreamSecurityUpgradeAcceptor> that understands the custom content types in its <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor.CanUpgrade%2A> method.</span></span>  
  
4. <span data-ttu-id="fda6d-156">每次呼叫 <xref:System.ServiceModel.Channels.StreamUpgradeInitiator.GetNextUpgrade%2A> 和 <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor.CanUpgrade%2A> 之後，就會升級資料流。</span><span class="sxs-lookup"><span data-stu-id="fda6d-156">The stream will be upgraded after each call to <xref:System.ServiceModel.Channels.StreamUpgradeInitiator.GetNextUpgrade%2A> and <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor.CanUpgrade%2A>.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="fda6d-157">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fda6d-157">See also</span></span>

- <xref:System.ServiceModel.Channels.StreamUpgradeInitiator>
- <xref:System.ServiceModel.Channels.StreamSecurityUpgradeInitiator>
- <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor>
- <xref:System.ServiceModel.Channels.StreamSecurityUpgradeAcceptor>
- <xref:System.ServiceModel.Channels.StreamUpgradeProvider>
- <xref:System.ServiceModel.Channels.StreamSecurityUpgradeProvider>
- <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement>
- <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement>
- <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement>
