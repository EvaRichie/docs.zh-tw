---
title: 服務版本控制
ms.date: 03/30/2017
ms.assetid: 37575ead-d820-4a67-8059-da11a2ab48e2
ms.openlocfilehash: fae0a5eca5737c3d7885cbe6c678678adabbea01
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96245341"
---
# <a name="service-versioning"></a><span data-ttu-id="b5d75-102">服務版本控制</span><span class="sxs-lookup"><span data-stu-id="b5d75-102">Service Versioning</span></span>

<span data-ttu-id="b5d75-103">在初始部署以及存留期間可能的數次部署之後，服務 (以及公開的端點) 可能因各種不同的原因而需要變更，例如變更業務需要、資訊技術需求，或解決其他問題等。</span><span class="sxs-lookup"><span data-stu-id="b5d75-103">After initial deployment, and potentially several times during their lifetime, services (and the endpoints they expose) may need to be changed for a variety of reasons, such as changing business needs, information technology requirements, or to address other issues.</span></span> <span data-ttu-id="b5d75-104">每個變更都會產生新的服務版本。</span><span class="sxs-lookup"><span data-stu-id="b5d75-104">Each change introduces a new version of the service.</span></span> <span data-ttu-id="b5d75-105">本主題說明如何考慮 Windows Communication Foundation (WCF) 中的版本設定。</span><span class="sxs-lookup"><span data-stu-id="b5d75-105">This topic explains how to consider versioning in Windows Communication Foundation (WCF).</span></span>  
  
## <a name="four-categories-of-service-changes"></a><span data-ttu-id="b5d75-106">四種服務變更的分類</span><span class="sxs-lookup"><span data-stu-id="b5d75-106">Four Categories of Service Changes</span></span>  

 <span data-ttu-id="b5d75-107">可能需要的服務變更可分成四個分類：</span><span class="sxs-lookup"><span data-stu-id="b5d75-107">The changes to services that may be required can be classified into four categories:</span></span>  
  
- <span data-ttu-id="b5d75-108">合約變更：例如，可能加入作業，或是可能加入或變更訊息中的資料項目。</span><span class="sxs-lookup"><span data-stu-id="b5d75-108">Contract changes: For example, an operation might be added, or a data element in a message might be added or changed.</span></span>  
  
- <span data-ttu-id="b5d75-109">位址變更：例如，服務移到不同的位置，而使端點使用新的位址。</span><span class="sxs-lookup"><span data-stu-id="b5d75-109">Address changes: For example, a service moves to a different location where endpoints have new addresses.</span></span>  
  
- <span data-ttu-id="b5d75-110">繫結變更：例如，安全性機制變更或其設定變更。</span><span class="sxs-lookup"><span data-stu-id="b5d75-110">Binding changes: For example, a security mechanism changes or its settings change.</span></span>  
  
- <span data-ttu-id="b5d75-111">實作變更：例如，內部方法實作變更時。</span><span class="sxs-lookup"><span data-stu-id="b5d75-111">Implementation changes: For example, when an internal method implementation changes.</span></span>  
  
 <span data-ttu-id="b5d75-112">其中某些變更稱為「中斷」，其他則稱為「非中斷」變更。</span><span class="sxs-lookup"><span data-stu-id="b5d75-112">Some of these changes are called "breaking" and others are "nonbreaking."</span></span> <span data-ttu-id="b5d75-113">如果在舊版本中成功處理的所有訊息都會在新版本中成功處理 *，則變更* 不會中斷。</span><span class="sxs-lookup"><span data-stu-id="b5d75-113">A change is *nonbreaking* if all messages that would have been processed successfully in the previous version are processed successfully in the new version.</span></span> <span data-ttu-id="b5d75-114">任何不符合該準則的變更都是 *重大* 變更。</span><span class="sxs-lookup"><span data-stu-id="b5d75-114">Any change that does not meet that criterion is a *breaking* change.</span></span>  
  
## <a name="service-orientation-and-versioning"></a><span data-ttu-id="b5d75-115">服務方向與版本控制</span><span class="sxs-lookup"><span data-stu-id="b5d75-115">Service Orientation and Versioning</span></span>  

 <span data-ttu-id="b5d75-116">其中一個服務方向的原則是，服務和用戶端都是自發的 (或獨立的)。</span><span class="sxs-lookup"><span data-stu-id="b5d75-116">One of the tenets of service orientation is that services and clients are autonomous (or independent).</span></span> <span data-ttu-id="b5d75-117">除此之外，這還暗示服務開發人員不得假設其控制了，甚至了解所有服務用戶端。</span><span class="sxs-lookup"><span data-stu-id="b5d75-117">Among other things, this implies that service developers cannot assume that they control or even know about all service clients.</span></span> <span data-ttu-id="b5d75-118">如此即可消除服務變更版本時，重新建置及部署所有用戶端的選擇。</span><span class="sxs-lookup"><span data-stu-id="b5d75-118">This eliminates the option of rebuilding and redeploying all clients when a service changes versions.</span></span> <span data-ttu-id="b5d75-119">本主題假設服務符合這個原則，因此必須獨立於其用戶端進行變更或「版本控制」。</span><span class="sxs-lookup"><span data-stu-id="b5d75-119">This topic assumes the service adheres to this tenet and therefore must be changed or "versioned" independent of its clients.</span></span>  
  
 <span data-ttu-id="b5d75-120">在發生非預期或無法避免的中斷變更情況下，應用程式可以選擇忽略這個原則，並且要求以新版服務重建及重新部署用戶端。</span><span class="sxs-lookup"><span data-stu-id="b5d75-120">In cases where a breaking change is unexpected and cannot be avoided, an application may choose to ignore this tenet and require that clients be rebuilt and redeployed with a new version of the service.</span></span>  
  
## <a name="contract-versioning"></a><span data-ttu-id="b5d75-121">合約版本控制</span><span class="sxs-lookup"><span data-stu-id="b5d75-121">Contract Versioning</span></span>  

 <span data-ttu-id="b5d75-122">用戶端使用的合約不需要與服務使用的合約相同，兩者只需相容即可。</span><span class="sxs-lookup"><span data-stu-id="b5d75-122">Contracts used by a client do not need to be the same as the contract used by the service; they need only to be compatible.</span></span>  
  
 <span data-ttu-id="b5d75-123">對於服務合約而言，相容性是指可以加入服務所公開的新作業，但是語意上不可移除或變更現有作業。</span><span class="sxs-lookup"><span data-stu-id="b5d75-123">For service contracts, compatibility means new operations exposed by the service can be added but existing operations cannot be removed or changed semantically.</span></span>  
  
 <span data-ttu-id="b5d75-124">對於資料合約而言，相容性是指可以加入新的結構描述型別定義，但是不可以中斷的方式變更現有的結構描述型別定義。</span><span class="sxs-lookup"><span data-stu-id="b5d75-124">For data contracts, compatibility means new schema type definitions can be added but existing schema type definitions cannot be changed in breaking ways.</span></span> <span data-ttu-id="b5d75-125">中斷變更可能包括移除資料成員，或是以不相容的方式變更其資料型別。</span><span class="sxs-lookup"><span data-stu-id="b5d75-125">Breaking changes might include removing data members or changing their data type incompatibly.</span></span> <span data-ttu-id="b5d75-126">這個功能為服務提供了一些變更其合約版本的空間，而不需中斷用戶端。</span><span class="sxs-lookup"><span data-stu-id="b5d75-126">This feature allows the service some latitude in changing the version of its contracts without breaking clients.</span></span> <span data-ttu-id="b5d75-127">接下來的兩節將說明可對 WCF 資料和服務合約進行的不間斷和重大變更。</span><span class="sxs-lookup"><span data-stu-id="b5d75-127">The next two sections explain nonbreaking and breaking changes that can be made to WCF data and service contracts.</span></span>  
  
## <a name="data-contract-versioning"></a><span data-ttu-id="b5d75-128">資料合約版本控制</span><span class="sxs-lookup"><span data-stu-id="b5d75-128">Data Contract Versioning</span></span>  

 <span data-ttu-id="b5d75-129">本章節說明使用 <xref:System.Runtime.Serialization.DataContractSerializer> 和 <xref:System.Runtime.Serialization.DataContractAttribute> 類別時的資料版本控制。</span><span class="sxs-lookup"><span data-stu-id="b5d75-129">This section deals with data versioning when using the <xref:System.Runtime.Serialization.DataContractSerializer> and <xref:System.Runtime.Serialization.DataContractAttribute> classes.</span></span>  
  
### <a name="strict-versioning"></a><span data-ttu-id="b5d75-130">嚴格的版本控制</span><span class="sxs-lookup"><span data-stu-id="b5d75-130">Strict Versioning</span></span>  

 <span data-ttu-id="b5d75-131">在許多變更版本會是問題的情況下，服務開發人員無法控制用戶端，因此無法假設用戶端對於訊息 XML 或結構描述中的變更會如何反應。</span><span class="sxs-lookup"><span data-stu-id="b5d75-131">In many scenarios when changing versions is an issue, the service developer does not have control over the clients and therefore cannot make assumptions about how they would react to changes in the message XML or schema.</span></span> <span data-ttu-id="b5d75-132">在這些情況下，您必須保證新的訊息將對舊的結構描述驗證，原因有兩個：</span><span class="sxs-lookup"><span data-stu-id="b5d75-132">In these cases, you must guarantee that the new messages will validate against the old schema, for two reasons:</span></span>  
  
- <span data-ttu-id="b5d75-133">舊的用戶端是在結構描述不會變更的假設下開發。</span><span class="sxs-lookup"><span data-stu-id="b5d75-133">The old clients were developed with the assumption that the schema will not change.</span></span> <span data-ttu-id="b5d75-134">因此可能無法處理不屬於其設計目的的訊息。</span><span class="sxs-lookup"><span data-stu-id="b5d75-134">They may fail to process messages that they were never designed for.</span></span>  
  
- <span data-ttu-id="b5d75-135">舊的用戶端甚至會在嘗試處理訊息之前，就先根據舊的結構描述執行實際結構描述驗證。</span><span class="sxs-lookup"><span data-stu-id="b5d75-135">The old clients may perform actual schema validation against the old schema before even attempting to process the messages.</span></span>  
  
 <span data-ttu-id="b5d75-136">在這類情況下，建議的方法是將現有資料合約視為固定不變，並且以唯一的 XML 限定名稱建立新合約。</span><span class="sxs-lookup"><span data-stu-id="b5d75-136">The recommended approach in such scenarios is to treat existing data contracts as immutable and create new ones with unique XML qualified names.</span></span> <span data-ttu-id="b5d75-137">接著服務開發人員會將新方法加入至現有服務合約中，或是建立新的服務合約，其中包含使用新資料合約的方法。</span><span class="sxs-lookup"><span data-stu-id="b5d75-137">The service developer would then either add new methods to an existing service contract or create a new service contract with methods that use the new data contract.</span></span>  
  
 <span data-ttu-id="b5d75-138">一般常見的情況是，服務開發人員需要寫入一些商務邏輯，這些邏輯應在所有資料合約版本以及每一個資料合約版本的版本專屬商務程式碼內執行。</span><span class="sxs-lookup"><span data-stu-id="b5d75-138">It will often be the case that a service developer needs to write some business logic that should run within all versions of a data contract plus version-specific business code for each version of the data contract.</span></span> <span data-ttu-id="b5d75-139">本主題最後的附錄將說明，如何使用介面滿足這項需要。</span><span class="sxs-lookup"><span data-stu-id="b5d75-139">The appendix at the end of this topic explains how interfaces can be used to satisfy this need.</span></span>  
  
### <a name="lax-versioning"></a><span data-ttu-id="b5d75-140">Lax 版本控制</span><span class="sxs-lookup"><span data-stu-id="b5d75-140">Lax Versioning</span></span>  

 <span data-ttu-id="b5d75-141">在其他許多情況中，服務開發人員可能假設，加入新的選擇性成員至資料合約將不會中斷現有用戶端。</span><span class="sxs-lookup"><span data-stu-id="b5d75-141">In many other scenarios, the service developer can make the assumption that adding a new, optional member to the data contract will not break existing clients.</span></span> <span data-ttu-id="b5d75-142">這需要服務開發人員調查現有用戶端是否未執行結構描述驗證，以及他們是否忽略未知的資料成員。</span><span class="sxs-lookup"><span data-stu-id="b5d75-142">This requires the service developer to investigate whether existing clients are not performing schema validation and that they ignore unknown data members.</span></span> <span data-ttu-id="b5d75-143">在這些情況中，可能會利用資料合約功能以非中斷的方式加入新成員。</span><span class="sxs-lookup"><span data-stu-id="b5d75-143">In these scenarios, it is possible to take advantage of data contract features for adding new members in a nonbreaking way.</span></span> <span data-ttu-id="b5d75-144">如果進行版本控制的資料合約功能在服務的第一個版本就已使用，那麼服務開發人員就可以很有信心地進行這項假設。</span><span class="sxs-lookup"><span data-stu-id="b5d75-144">The service developer can make this assumption with confidence if the data contract features for versioning were already used for the first version of the service.</span></span>  
  
 <span data-ttu-id="b5d75-145">WCF、ASP.NET Web 服務及許多其他 Web 服務堆疊支援不 *嚴格的版本控制*，也就是它們不會針對收到的資料中新的未知資料成員擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b5d75-145">WCF, ASP.NET Web Services, and many other Web service stacks support *lax versioning*: that is, they do not throw exceptions for new unknown data members in received data.</span></span>  
  
 <span data-ttu-id="b5d75-146">一般很容易誤信，加入新成員不會中斷現有用戶端。</span><span class="sxs-lookup"><span data-stu-id="b5d75-146">It is easy to mistakenly believe that adding a new member will not break existing clients.</span></span> <span data-ttu-id="b5d75-147">如果您不確定所有用戶端都能處理 lax 版本控制，則建議您使用嚴格版本控制方針，並且將資料合約視為固定不變。</span><span class="sxs-lookup"><span data-stu-id="b5d75-147">If you are unsure that all clients can handle lax versioning, the recommendation is to use the strict versioning guidelines and treat data contracts as immutable.</span></span>  
  
 <span data-ttu-id="b5d75-148">如需資料合約之寬鬆和嚴格版本控制的詳細指導方針，請參閱 [最佳做法：資料合約版本控制](best-practices-data-contract-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="b5d75-148">For detailed guidelines for both lax and strict versioning of data contracts, see [Best Practices: Data Contract Versioning](best-practices-data-contract-versioning.md).</span></span>  
  
### <a name="distinguishing-between-data-contract-and-net-types"></a><span data-ttu-id="b5d75-149">分辨資料合約與 .NET 型別</span><span class="sxs-lookup"><span data-stu-id="b5d75-149">Distinguishing Between Data Contract and .NET Types</span></span>  

 <span data-ttu-id="b5d75-150">.NET 類別或結構可藉由將 <xref:System.Runtime.Serialization.DataContractAttribute> 屬性套用至該類別，而予以投射為資料合約。</span><span class="sxs-lookup"><span data-stu-id="b5d75-150">A .NET class or structure can be projected as a data contract by applying the <xref:System.Runtime.Serialization.DataContractAttribute> attribute to the class.</span></span> <span data-ttu-id="b5d75-151">.NET 型別及其資料合約規劃是兩件不同的事。</span><span class="sxs-lookup"><span data-stu-id="b5d75-151">The .NET type and its data contract projections are two distinct matters.</span></span> <span data-ttu-id="b5d75-152">您可以擁有多個 .NET 型別使用相同的資料合約規劃。</span><span class="sxs-lookup"><span data-stu-id="b5d75-152">It is possible to have multiple .NET types with the same data contract projection.</span></span> <span data-ttu-id="b5d75-153">這項分別相當實用，可讓您在變更 .NET 型別的同時維持規劃的資料合約，甚至在用字嚴格的情況下也能藉此維持與現有用戶端的相容性。</span><span class="sxs-lookup"><span data-stu-id="b5d75-153">This distinction is especially useful in allowing you to change the .NET type while maintaining the projected data contract, thereby maintaining compatibility with existing clients even in the strict sense of the word.</span></span> <span data-ttu-id="b5d75-154">若要維持 .NET 型別和資料合約之間的這項區別，有兩件事您務必要做到：</span><span class="sxs-lookup"><span data-stu-id="b5d75-154">There are two things you should always do to maintain this distinction between .NET type and data contract:</span></span>  
  
- <span data-ttu-id="b5d75-155">請指定 <xref:System.Runtime.Serialization.DataContractAttribute.Name%2A> 和 <xref:System.Runtime.Serialization.DataContractAttribute.Namespace%2A>。</span><span class="sxs-lookup"><span data-stu-id="b5d75-155">Specify a <xref:System.Runtime.Serialization.DataContractAttribute.Name%2A> and <xref:System.Runtime.Serialization.DataContractAttribute.Namespace%2A>.</span></span> <span data-ttu-id="b5d75-156">您務必要指定資料合約的名稱和命名空間，以避免在合約中公開 .NET 型別的名稱和命名空間。</span><span class="sxs-lookup"><span data-stu-id="b5d75-156">You should always specify the name and namespace of your data contract to prevent your .NET type’s name and namespace from being exposed in the contract.</span></span> <span data-ttu-id="b5d75-157">如此一來，即使您之後決定變更 .NET 命名空間或型別名稱，資料合約仍會維持不變。</span><span class="sxs-lookup"><span data-stu-id="b5d75-157">This way, if you decide later to change the .NET namespace or type name, your data contract remains the same.</span></span>  
  
- <span data-ttu-id="b5d75-158">請指定 <xref:System.Runtime.Serialization.DataMemberAttribute.Name%2A>。</span><span class="sxs-lookup"><span data-stu-id="b5d75-158">Specify <xref:System.Runtime.Serialization.DataMemberAttribute.Name%2A>.</span></span> <span data-ttu-id="b5d75-159">您務必要指定資料成員的名稱，以避免在合約中公開 .NET 成員的名稱。</span><span class="sxs-lookup"><span data-stu-id="b5d75-159">You should always specify the name of your data members to prevent your .NET member name from being exposed in the contract.</span></span> <span data-ttu-id="b5d75-160">如此一來，即使您之後決定變更成員的 .NET 名稱，資料合約仍會維持不變。</span><span class="sxs-lookup"><span data-stu-id="b5d75-160">This way, if you decide later to change the .NET name of the member, your data contract remains the same.</span></span>  
  
### <a name="changing-or-removing-members"></a><span data-ttu-id="b5d75-161">變更或移除成員</span><span class="sxs-lookup"><span data-stu-id="b5d75-161">Changing or Removing Members</span></span>  

 <span data-ttu-id="b5d75-162">即使在允許 lax 版本控制的情況下，變更成員的名稱或資料，或是移除資料成員即屬於中斷變更。</span><span class="sxs-lookup"><span data-stu-id="b5d75-162">Changing the name or data type of a member, or removing data members is a breaking change even if lax versioning is allowed.</span></span> <span data-ttu-id="b5d75-163">如果這是必要的，請建立新的資料合約。</span><span class="sxs-lookup"><span data-stu-id="b5d75-163">If this is necessary, create a new data contract.</span></span>  
  
 <span data-ttu-id="b5d75-164">如果服務相容性相當重要，您或許會考慮忽略程式碼中未使用的資料成員，並讓它們留在原處。</span><span class="sxs-lookup"><span data-stu-id="b5d75-164">If service compatibility is of high importance, you might consider ignoring unused data members in your code and leave them in place.</span></span> <span data-ttu-id="b5d75-165">如果要將資料成員分割成多個成員，您或許會考慮保留現有的成員，做為可執行低階用戶端 (未升級為最新版本的用戶端) 所需分割及重新彙總的屬性。</span><span class="sxs-lookup"><span data-stu-id="b5d75-165">If you are splitting up a data member into multiple members, you might consider leaving the existing member in place as a property that can perform the required splitting and re-aggregation for down-level clients (clients that are not upgraded to the latest version).</span></span>  
  
 <span data-ttu-id="b5d75-166">資料合約名稱或命名空間的變更同樣是中斷變更。</span><span class="sxs-lookup"><span data-stu-id="b5d75-166">Similarly, changes to the data contract’s name or namespace are breaking changes.</span></span>  
  
### <a name="round-trips-of-unknown-data"></a><span data-ttu-id="b5d75-167">反覆存取未知的資料</span><span class="sxs-lookup"><span data-stu-id="b5d75-167">Round-Trips of Unknown Data</span></span>  

 <span data-ttu-id="b5d75-168">在某些情況下，會需要「反覆存取」來自新版本中所加入之成員的未知資料。</span><span class="sxs-lookup"><span data-stu-id="b5d75-168">In some scenarios, there is a need to "round-trip" unknown data that comes from members added in a new version.</span></span> <span data-ttu-id="b5d75-169">例如，"versionNew" 服務會將包含新加入之成員的資料傳送至 "versionOld" 用戶端。</span><span class="sxs-lookup"><span data-stu-id="b5d75-169">For example, a "versionNew" service sends data with some newly added members to a "versionOld" client.</span></span> <span data-ttu-id="b5d75-170">用戶端會在處理訊息時忽略新加入的成員，但是會將包括新加入之成員的相同資料再次傳送回 versionNew 服務。</span><span class="sxs-lookup"><span data-stu-id="b5d75-170">The client ignores the newly added members when processing the message, but it resends that same data, including the newly added members, back to the versionNew service.</span></span> <span data-ttu-id="b5d75-171">這種情況常見的案例為資料更新，其中資料會從服務擷取、變更，再傳回。</span><span class="sxs-lookup"><span data-stu-id="b5d75-171">The typical scenario for this is data updates where data is retrieved from the service, changed, and returned.</span></span>  
  
 <span data-ttu-id="b5d75-172">若要啟用特定類型的往返，類型必須實作 <xref:System.Runtime.Serialization.IExtensibleDataObject> 介面，</span><span class="sxs-lookup"><span data-stu-id="b5d75-172">To enable round-tripping for a particular type, the type must implement the <xref:System.Runtime.Serialization.IExtensibleDataObject> interface.</span></span> <span data-ttu-id="b5d75-173">這個介面包含一個屬性 <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A>，會傳回 <xref:System.Runtime.Serialization.ExtensionDataObject> 型別。</span><span class="sxs-lookup"><span data-stu-id="b5d75-173">The interface contains one property, <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A> that returns the <xref:System.Runtime.Serialization.ExtensionDataObject> type.</span></span> <span data-ttu-id="b5d75-174">這個屬性是用來儲存資料合約未來版本中的任何資料，而此資料合約對目前版本來說是未知的。</span><span class="sxs-lookup"><span data-stu-id="b5d75-174">The property is used to store any data from future versions of the data contract that is unknown to the current version.</span></span> <span data-ttu-id="b5d75-175">這個資料不會讓用戶端看見，但是當執行個體序列化時，就會將其餘資料合約成員的資料寫入 <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A> 屬性的內容。</span><span class="sxs-lookup"><span data-stu-id="b5d75-175">This data is opaque to the client, but when the instance is serialized, the content of the <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A> property is written with the rest of the data contract members' data.</span></span>  
  
 <span data-ttu-id="b5d75-176">建議所有的型別都實作此介面，以納入新的和未知的未來成員。</span><span class="sxs-lookup"><span data-stu-id="b5d75-176">It is recommended that all your types implement this interface to accommodate new and unknown future members.</span></span>  
  
### <a name="data-contract-libraries"></a><span data-ttu-id="b5d75-177">資料合約程式庫</span><span class="sxs-lookup"><span data-stu-id="b5d75-177">Data Contract Libraries</span></span>  

 <span data-ttu-id="b5d75-178">資料合約的程式庫可能存在，合約會在其中發行至中央儲存機制，而服務和型別實作器會從該儲存機制實作和公開資料合約。</span><span class="sxs-lookup"><span data-stu-id="b5d75-178">There may be libraries of data contracts where a contract is published to a central repository, and service and type implementers implement and expose data contracts from that repository.</span></span> <span data-ttu-id="b5d75-179">在此情況下，將資料合約發行至儲存機制時，您無法控制誰會建立實作該合約之型別。</span><span class="sxs-lookup"><span data-stu-id="b5d75-179">In that case, when you publish a data contract to the repository, you have no control over who creates types that implement it.</span></span> <span data-ttu-id="b5d75-180">因此，一旦合約發行之後，就無法進行修改，而產生有效的固定不變狀態。</span><span class="sxs-lookup"><span data-stu-id="b5d75-180">Thus, you cannot modify the contract once it is published, rendering it effectively immutable.</span></span>  
  
### <a name="when-using-the-xmlserializer"></a><span data-ttu-id="b5d75-181">使用 XmlSerializer</span><span class="sxs-lookup"><span data-stu-id="b5d75-181">When Using the XmlSerializer</span></span>  

 <span data-ttu-id="b5d75-182">使用 <xref:System.Xml.Serialization.XmlSerializer> 類別時適用相同的版本控制準則。</span><span class="sxs-lookup"><span data-stu-id="b5d75-182">The same versioning principles apply when using the <xref:System.Xml.Serialization.XmlSerializer> class.</span></span> <span data-ttu-id="b5d75-183">需要嚴格版本控制時，請將資料合約視為固定不變，並且以唯一的限定名稱為新版本建立新的資料合約。</span><span class="sxs-lookup"><span data-stu-id="b5d75-183">When strict versioning is required, treat data contracts as immutable and create new data contracts with unique, qualified names for the new versions.</span></span> <span data-ttu-id="b5d75-184">如果您確定可以使用 lax 版本控制，則可在新版本中加入新的可序列化成員，但是不變更或移除現有成員。</span><span class="sxs-lookup"><span data-stu-id="b5d75-184">When you are sure that lax versioning can be used, you can add new serializable members in new versions but not change or remove existing members.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="b5d75-185"><xref:System.Xml.Serialization.XmlSerializer> 會使用 <xref:System.Xml.Serialization.XmlAnyElementAttribute> 和 <xref:System.Xml.Serialization.XmlAnyAttributeAttribute> 屬性支援未知資料的反覆存取。</span><span class="sxs-lookup"><span data-stu-id="b5d75-185">The <xref:System.Xml.Serialization.XmlSerializer> uses the <xref:System.Xml.Serialization.XmlAnyElementAttribute> and <xref:System.Xml.Serialization.XmlAnyAttributeAttribute> attributes to support round-tripping of unknown data.</span></span>  
  
## <a name="message-contract-versioning"></a><span data-ttu-id="b5d75-186">訊息合約版本控制</span><span class="sxs-lookup"><span data-stu-id="b5d75-186">Message Contract Versioning</span></span>  

 <span data-ttu-id="b5d75-187">訊息合約版本控制的方針與資料合約版本控制十分相似。</span><span class="sxs-lookup"><span data-stu-id="b5d75-187">The guidelines for message contract versioning are very similar to versioning data contracts.</span></span> <span data-ttu-id="b5d75-188">如果需要嚴格版本控制，則不應變更訊息本文，而是以唯一的限定名稱建立新的訊息合約。</span><span class="sxs-lookup"><span data-stu-id="b5d75-188">If strict versioning is required, you should not change your message body but instead create a new message contract with a unique qualified name.</span></span> <span data-ttu-id="b5d75-189">如果您確認可以使用 lax 版本控制，則可以加入新的訊息本文部分，但不變更或移除現有部分。</span><span class="sxs-lookup"><span data-stu-id="b5d75-189">If you know that you can use lax versioning, you can add new message body parts but not change or remove existing ones.</span></span> <span data-ttu-id="b5d75-190">本指引同時適用不包裝和包裝的訊息合約。</span><span class="sxs-lookup"><span data-stu-id="b5d75-190">This guidance applies both to bare and wrapped message contracts.</span></span>  
  
 <span data-ttu-id="b5d75-191">即使使用嚴格版本控制，仍可以加入訊息標頭。</span><span class="sxs-lookup"><span data-stu-id="b5d75-191">Message headers can always be added, even if strict versioning is in use.</span></span> <span data-ttu-id="b5d75-192">MustUnderstand 旗標可能會影響版本控制。</span><span class="sxs-lookup"><span data-stu-id="b5d75-192">The MustUnderstand flag may affect versioning.</span></span> <span data-ttu-id="b5d75-193">一般而言，WCF 中的標頭版本控制模型如 SOAP 規格中所述。</span><span class="sxs-lookup"><span data-stu-id="b5d75-193">In general, the versioning model for headers in WCF is as described in the SOAP specification.</span></span>  
  
## <a name="service-contract-versioning"></a><span data-ttu-id="b5d75-194">服務合約版本控制</span><span class="sxs-lookup"><span data-stu-id="b5d75-194">Service Contract Versioning</span></span>  

 <span data-ttu-id="b5d75-195">服務合約版本控制與資料合約版本控制相似，同樣包含加入、變更和移除作業。</span><span class="sxs-lookup"><span data-stu-id="b5d75-195">Similar to data contract versioning, service contract versioning also involves adding, changing, and removing operations.</span></span>  
  
### <a name="specifying-name-namespace-and-action"></a><span data-ttu-id="b5d75-196">指定名稱、命名空間和動作</span><span class="sxs-lookup"><span data-stu-id="b5d75-196">Specifying Name, Namespace, and Action</span></span>  

 <span data-ttu-id="b5d75-197">根據預設，服務合約的名稱即是介面的名稱。</span><span class="sxs-lookup"><span data-stu-id="b5d75-197">By default, the name of a service contract is the name of the interface.</span></span> <span data-ttu-id="b5d75-198">其預設命名空間為 " http://tempuri.org "，而且每個作業的動作為 " http://tempuri.org/contractname/methodname "。</span><span class="sxs-lookup"><span data-stu-id="b5d75-198">Its default namespace is "http://tempuri.org", and each operation’s action is "http://tempuri.org/contractname/methodname".</span></span> <span data-ttu-id="b5d75-199">建議您明確指定服務合約的名稱和命名空間，以及每項作業的動作，以避免使用 " http://tempuri.org " 和來防止介面和方法名稱公開在服務的合約中。</span><span class="sxs-lookup"><span data-stu-id="b5d75-199">It is recommended that you explicitly specify a name and namespace for the service contract, and an action for each operation to avoid using "http://tempuri.org" and to prevent interface and method names from being exposed in the service’s contract.</span></span>  
  
### <a name="adding-parameters-and-operations"></a><span data-ttu-id="b5d75-200">加入參數和作業</span><span class="sxs-lookup"><span data-stu-id="b5d75-200">Adding Parameters and Operations</span></span>  

 <span data-ttu-id="b5d75-201">加入服務所公開的服務作業為非中斷變更，因為現有用戶端不需考量這些新作業。</span><span class="sxs-lookup"><span data-stu-id="b5d75-201">Adding service operations exposed by the service is a nonbreaking change because existing clients need not be concerned about those new operations.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="b5d75-202">將作業加入至雙工回呼合約為中斷變更。</span><span class="sxs-lookup"><span data-stu-id="b5d75-202">Adding operations to a duplex callback contract is a breaking change.</span></span>  
  
### <a name="changing-operation-parameter-or-return-types"></a><span data-ttu-id="b5d75-203">變更作業參數或傳回型別</span><span class="sxs-lookup"><span data-stu-id="b5d75-203">Changing Operation Parameter or Return Types</span></span>  

 <span data-ttu-id="b5d75-204">一般來說，變更參數或傳回型別是中斷變更，除非新型別與舊型別實作的資料合約相同。</span><span class="sxs-lookup"><span data-stu-id="b5d75-204">Changing parameter or return types generally is a breaking change unless the new type implements the same data contract implemented by the old type.</span></span> <span data-ttu-id="b5d75-205">若要進行這類變更，請將新作業加入服務合約或定義新的服務合約。</span><span class="sxs-lookup"><span data-stu-id="b5d75-205">To make such a change, add a new operation to the service contract or define a new service contract.</span></span>  
  
### <a name="removing-operations"></a><span data-ttu-id="b5d75-206">移除作業</span><span class="sxs-lookup"><span data-stu-id="b5d75-206">Removing Operations</span></span>  

 <span data-ttu-id="b5d75-207">移除作業同樣屬於中斷變更。</span><span class="sxs-lookup"><span data-stu-id="b5d75-207">Removing operations is also a breaking change.</span></span> <span data-ttu-id="b5d75-208">若要進行這類變更，請定義新的服務合約並且在新端點上公開。</span><span class="sxs-lookup"><span data-stu-id="b5d75-208">To make such a change, define a new service contract and expose it on a new endpoint.</span></span>  
  
### <a name="fault-contracts"></a><span data-ttu-id="b5d75-209">錯誤合約</span><span class="sxs-lookup"><span data-stu-id="b5d75-209">Fault Contracts</span></span>  

 <span data-ttu-id="b5d75-210"><xref:System.ServiceModel.FaultContractAttribute> 屬性可讓服務合約開發人員指定可從合約作業傳回的錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="b5d75-210">The <xref:System.ServiceModel.FaultContractAttribute> attribute enables a service contract developer to specify information about faults that can be returned from the contract's operations.</span></span>  
  
 <span data-ttu-id="b5d75-211">服務合約中所述的錯誤清單並不詳盡。</span><span class="sxs-lookup"><span data-stu-id="b5d75-211">The list of faults described in a service's contract is not considered exhaustive.</span></span> <span data-ttu-id="b5d75-212">作業可能隨時傳回未於其合約中說明的錯誤。</span><span class="sxs-lookup"><span data-stu-id="b5d75-212">At any time, an operation may return faults that are not described in its contract.</span></span> <span data-ttu-id="b5d75-213">因此，變更合約中所述的錯誤集不視為中斷。</span><span class="sxs-lookup"><span data-stu-id="b5d75-213">Therefore changing the set of faults described in the contract is not considered breaking.</span></span> <span data-ttu-id="b5d75-214">例如，使用 <xref:System.ServiceModel.FaultContractAttribute> 將新錯誤加入至合約中，或從合約中移除現有錯誤。</span><span class="sxs-lookup"><span data-stu-id="b5d75-214">For example, adding a new fault to the contract using the <xref:System.ServiceModel.FaultContractAttribute> or removing an existing fault from the contract.</span></span>  
  
### <a name="service-contract-libraries"></a><span data-ttu-id="b5d75-215">服務合約程式庫</span><span class="sxs-lookup"><span data-stu-id="b5d75-215">Service Contract Libraries</span></span>  

 <span data-ttu-id="b5d75-216">組織可能擁有合約的程式庫，合約會在其中發行至中央儲存機制，而服務實作器會從該儲存機制實作合約。</span><span class="sxs-lookup"><span data-stu-id="b5d75-216">Organizations may have libraries of contracts where a contract is published to a central repository and service implementers implement contracts from that repository.</span></span> <span data-ttu-id="b5d75-217">在此情況下，將服務合約發行至儲存機制時，您無法控制誰會建立實作該合約之服務。</span><span class="sxs-lookup"><span data-stu-id="b5d75-217">In this case, when you publish a service contract to the repository you have no control over who creates services that implement it.</span></span> <span data-ttu-id="b5d75-218">因此，一旦服務合約發行之後，就無法進行修改，形成實際上不可變的狀態。</span><span class="sxs-lookup"><span data-stu-id="b5d75-218">Therefore, you cannot modify the service contract once published, rendering it effectively immutable.</span></span> <span data-ttu-id="b5d75-219">WCF 支援合約繼承，可用來建立可延伸現有合約的新合約。</span><span class="sxs-lookup"><span data-stu-id="b5d75-219">WCF supports contract inheritance, which can be used to create a new contract that extends existing contracts.</span></span> <span data-ttu-id="b5d75-220">若要使用此功能，請定義繼承自舊服務合約介面的新服務合約介面，然後將方法加入至新介面。</span><span class="sxs-lookup"><span data-stu-id="b5d75-220">To use this feature, define a new service contract interface that inherits from the old service contract interface, then add methods to the new interface.</span></span> <span data-ttu-id="b5d75-221">接著將實作舊合約的服務變更為實作新合約，並且將 "versionOld" 端點定義變更為使用新的合約。</span><span class="sxs-lookup"><span data-stu-id="b5d75-221">You then change the service that implements the old contract to implement the new contract and change the "versionOld" endpoint definition to use the new contract.</span></span> <span data-ttu-id="b5d75-222">對於 "versionOld" 用戶端而言，端點將隨公開 "versionOld" 合約繼續出現，而對於 "versionNew" 用戶端而言，端點將出現以公開 "versionNew" 合約。</span><span class="sxs-lookup"><span data-stu-id="b5d75-222">To "versionOld" clients, the endpoint will continue to appear as exposing the "versionOld" contract; to "versionNew" clients, the endpoint will appear to expose the "versionNew" contract.</span></span>  
  
## <a name="address-and-binding-versioning"></a><span data-ttu-id="b5d75-223">位址與繫結版本控制</span><span class="sxs-lookup"><span data-stu-id="b5d75-223">Address and Binding Versioning</span></span>  

 <span data-ttu-id="b5d75-224">端點位址和繫結的變更屬於中斷變更，除非用戶端能夠動態地發現新端點位址或繫結。</span><span class="sxs-lookup"><span data-stu-id="b5d75-224">Changes to endpoint address and binding are breaking changes unless clients are capable of dynamically discovering the new endpoint address or binding.</span></span> <span data-ttu-id="b5d75-225">實作此功能的一項機制是藉由使用通用探索、描述和整合 (UDDI) 登錄以及 UDDI 引動模式，其中用戶端會嘗試與端點進行通訊，並且在發生錯誤時，查詢已知 UDDI 登錄中目前端點的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="b5d75-225">One mechanism for implementing this capability is by using a Universal Discovery Description and Integration (UDDI) registry and the UDDI Invocation Pattern where a client attempts to communicate with an endpoint and, upon failure, queries a well-known UDDI registry for the current endpoint metadata.</span></span> <span data-ttu-id="b5d75-226">然後用戶端會使用來自這項中繼資料的位址和繫結與端點進行通訊。</span><span class="sxs-lookup"><span data-stu-id="b5d75-226">The client then uses the address and binding from this metadata to communicate with the endpoint.</span></span> <span data-ttu-id="b5d75-227">如果此通訊成功，用戶端就會快取位址和繫結資訊以供未來使用。</span><span class="sxs-lookup"><span data-stu-id="b5d75-227">If this communication succeeds, the client caches the address and binding information for future use.</span></span>  
  
## <a name="routing-service-and-versioning"></a><span data-ttu-id="b5d75-228">路由服務與版本控制</span><span class="sxs-lookup"><span data-stu-id="b5d75-228">Routing Service and Versioning</span></span>  

 <span data-ttu-id="b5d75-229">如果對服務所做的變更是中斷變更，而且您必須同時執行兩個以上不同的服務版本，就可以使用 WCF 路由服務，將訊息路由傳送至適當的服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="b5d75-229">If the changes made to a service are breaking changes and you need to have two or more different versions of a service running simultaneously you can use the WCF Routing Service to route messages to the appropriate service instance.</span></span> <span data-ttu-id="b5d75-230">WCF 路由服務會使用以內容為基礎的路由，換言之，它會使用訊息內部的資訊來判斷要路由傳送訊息的目標位置。</span><span class="sxs-lookup"><span data-stu-id="b5d75-230">The WCF Routing Service uses content-based routing, in other words, it uses information within the message to determine where to route the message.</span></span> <span data-ttu-id="b5d75-231">如需 WCF 路由服務的詳細資訊，請參閱 [路由服務](./feature-details/routing-service.md)。</span><span class="sxs-lookup"><span data-stu-id="b5d75-231">For more information about the WCF Routing Service see [Routing Service](./feature-details/routing-service.md).</span></span> <span data-ttu-id="b5d75-232">如需如何使用 WCF 路由服務進行服務版本設定的範例，請參閱 [如何：服務版本控制](./feature-details/how-to-service-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="b5d75-232">For an example of how to use the WCF Routing Service for service versioning see [How To: Service Versioning](./feature-details/how-to-service-versioning.md).</span></span>  
  
## <a name="appendix"></a><span data-ttu-id="b5d75-233">附錄</span><span class="sxs-lookup"><span data-stu-id="b5d75-233">Appendix</span></span>  

 <span data-ttu-id="b5d75-234">需要嚴格版本控制時的一般資料合約版本控制方針，是將資料合約視為固定不變，並且在需要變更時建立新的合約。</span><span class="sxs-lookup"><span data-stu-id="b5d75-234">The general data contract versioning guidance when strict versioning is needed is to treat data contracts as immutable and create new ones when changes are required.</span></span> <span data-ttu-id="b5d75-235">您必須針對每個新的資料合約建立新類別，因此需要有機制避免採用根據舊資料合約類別撰寫的現有程式碼之後，還須再根據新資料合約類別重新撰寫。</span><span class="sxs-lookup"><span data-stu-id="b5d75-235">A new class needs to be created for each new data contract, so a mechanism is needed to avoid having to take existing code that was written in terms of the old data contract class and rewrite it in terms of the new data contract class.</span></span>  
  
 <span data-ttu-id="b5d75-236">這類機制的其中一種是使用介面定義各資料合約的成員，並且根據介面而非實作介面的資料合約類別，撰寫內部實作程式碼。</span><span class="sxs-lookup"><span data-stu-id="b5d75-236">One such mechanism is to use interfaces to define the members of each data contract and write internal implementation code in terms of the interfaces rather than the data contract classes that implement the interfaces.</span></span> <span data-ttu-id="b5d75-237">以下第 1 版服務的程式碼示範 `IPurchaseOrderV1` 介面和 `PurchaseOrderV1`。</span><span class="sxs-lookup"><span data-stu-id="b5d75-237">The following code for version 1 of a service shows an `IPurchaseOrderV1` interface and a `PurchaseOrderV1`:</span></span>  
  
```csharp  
public interface IPurchaseOrderV1  
{  
    string OrderId { get; set; }  
    string CustomerId { get; set; }  
}  
  
[DataContract(  
Name = "PurchaseOrder",  
Namespace = "http://examples.microsoft.com/WCF/2005/10/PurchaseOrder")]  
public class PurchaseOrderV1 : IPurchaseOrderV1  
{  
    [DataMember(...)]  
    public string OrderId {...}  
    [DataMember(...)]  
    public string CustomerId {...}  
}  
```  
  
 <span data-ttu-id="b5d75-238">即使服務合約的作業可以根據 `PurchaseOrderV1` 撰寫，實際商務邏輯仍會根據 `IPurchaseOrderV1`。</span><span class="sxs-lookup"><span data-stu-id="b5d75-238">While the service contract’s operations would be written in terms of `PurchaseOrderV1`, the actual business logic would be in terms of `IPurchaseOrderV1`.</span></span> <span data-ttu-id="b5d75-239">接著在第 2 版中，會有一個新的 `IPurchaseOrderV2` 介面和新的 `PurchaseOrderV2` 類別，如以下程式碼中所示：</span><span class="sxs-lookup"><span data-stu-id="b5d75-239">Then, in version 2, there would be a new `IPurchaseOrderV2` interface and a new `PurchaseOrderV2` class as shown in the following code:</span></span>  
  
```csharp
public interface IPurchaseOrderV2  
{  
    DateTime OrderDate { get; set; }  
}

[DataContract(
Name = "PurchaseOrder",  
Namespace = "http://examples.microsoft.com/WCF/2006/02/PurchaseOrder")]  
public class PurchaseOrderV2 : IPurchaseOrderV1, IPurchaseOrderV2  
{  
    [DataMember(...)]  
    public string OrderId {...}  
    [DataMember(...)]  
    public string CustomerId {...}  
    [DataMember(...)]  
    public DateTime OrderDate { ... }  
}  
```  
  
 <span data-ttu-id="b5d75-240">服務合約會更新，以加入根據 `PurchaseOrderV2` 所撰寫的新作業。</span><span class="sxs-lookup"><span data-stu-id="b5d75-240">The service contract would be updated to include new operations that are written in terms of `PurchaseOrderV2`.</span></span> <span data-ttu-id="b5d75-241">根據 `IPurchaseOrderV1` 撰寫的現有商務邏輯會在 `PurchaseOrderV2` 中繼續運作，而需要 `OrderDate` 屬性的新商務邏輯則會根據 `IPurchaseOrderV2` 撰寫。</span><span class="sxs-lookup"><span data-stu-id="b5d75-241">Existing business logic written in terms of `IPurchaseOrderV1` would continue to work for `PurchaseOrderV2` and new business logic that needs the `OrderDate` property would be written in terms of `IPurchaseOrderV2`.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b5d75-242">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b5d75-242">See also</span></span>

- <xref:System.Runtime.Serialization.DataContractSerializer>
- <xref:System.Runtime.Serialization.DataContractAttribute>
- <xref:System.Runtime.Serialization.DataContractAttribute.Name%2A>
- <xref:System.Runtime.Serialization.DataContractAttribute.Namespace%2A>
- <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A>
- <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A>
- <xref:System.Runtime.Serialization.IExtensibleDataObject>
- <xref:System.Runtime.Serialization.ExtensionDataObject>
- <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A>
- <xref:System.Xml.Serialization.XmlSerializer>
- [<span data-ttu-id="b5d75-243">資料合約等價</span><span class="sxs-lookup"><span data-stu-id="b5d75-243">Data Contract Equivalence</span></span>](./feature-details/data-contract-equivalence.md)
- [<span data-ttu-id="b5d75-244">版本相容序列化回呼</span><span class="sxs-lookup"><span data-stu-id="b5d75-244">Version-Tolerant Serialization Callbacks</span></span>](./feature-details/version-tolerant-serialization-callbacks.md)
