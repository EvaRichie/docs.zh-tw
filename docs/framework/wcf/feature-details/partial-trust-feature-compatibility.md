---
title: 部分信任功能相容性
ms.date: 03/30/2017
ms.assetid: a36a540b-1606-4e63-88e0-b7c59e0e6ab7
ms.openlocfilehash: 6d009482037efac8e0f90d255e198f10a1234187
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90551968"
---
# <a name="partial-trust-feature-compatibility"></a><span data-ttu-id="841fb-102">部分信任功能相容性</span><span class="sxs-lookup"><span data-stu-id="841fb-102">Partial Trust Feature Compatibility</span></span>
<span data-ttu-id="841fb-103">在部分信任的環境中執行時，Windows Communication Foundation (WCF) 支援有限的功能子集。</span><span class="sxs-lookup"><span data-stu-id="841fb-103">Windows Communication Foundation (WCF) supports a limited subset of functionality when running in a partially-trusted environment.</span></span> <span data-ttu-id="841fb-104">部分信任環境所支援的功能，主要是用在如 [Supported Deployment Scenarios](supported-deployment-scenarios.md) 主題所述的特定案例中。</span><span class="sxs-lookup"><span data-stu-id="841fb-104">The features supported in partial trust are designed around a specific set of scenarios as described in the [Supported Deployment Scenarios](supported-deployment-scenarios.md) topic.</span></span>  
  
## <a name="minimum-permission-requirements"></a><span data-ttu-id="841fb-105">基本權限需求</span><span class="sxs-lookup"><span data-stu-id="841fb-105">Minimum Permission Requirements</span></span>  
 <span data-ttu-id="841fb-106">WCF 支援應用程式中，以下列其中一個標準命名許可權集合執行的功能子集：</span><span class="sxs-lookup"><span data-stu-id="841fb-106">WCF supports a subset of features in applications running under either of the following standard named permission sets:</span></span>  
  
- <span data-ttu-id="841fb-107">中度信任權限</span><span class="sxs-lookup"><span data-stu-id="841fb-107">Medium Trust permissions</span></span>  
  
- <span data-ttu-id="841fb-108">網際網路區域權限</span><span class="sxs-lookup"><span data-stu-id="841fb-108">Internet Zone permissions</span></span>  
  
 <span data-ttu-id="841fb-109">在部分信任的應用程式中嘗試使用具有較嚴格許可權的 WCF，可能會在執行時間導致安全性例外狀況。</span><span class="sxs-lookup"><span data-stu-id="841fb-109">Attempting to use WCF in partially-trusted applications with more restrictive permissions may result in security exceptions at runtime.</span></span>  
  
## <a name="contracts"></a><span data-ttu-id="841fb-110">合約</span><span class="sxs-lookup"><span data-stu-id="841fb-110">Contracts</span></span>  
 <span data-ttu-id="841fb-111">在部分信任環境中執行時，合約有下列限制：</span><span class="sxs-lookup"><span data-stu-id="841fb-111">Contracts are subject to the following restrictions when running under partial trust:</span></span>  
  
- <span data-ttu-id="841fb-112">實作 `[ServiceContract]` 介面的服務類別必須是 `public` 且具有 `public` 建構函式。</span><span class="sxs-lookup"><span data-stu-id="841fb-112">The service class that implements the `[ServiceContract]` interface must be `public` and have a `public` constructor.</span></span> <span data-ttu-id="841fb-113">如果此服務類別定義 `[OperationContract]` 方法，這些方法就必須是 `public`。</span><span class="sxs-lookup"><span data-stu-id="841fb-113">If it defines `[OperationContract]` methods, these must be `public`.</span></span> <span data-ttu-id="841fb-114">如果它改為實作 `[ServiceContract]` 介面，這些方法實作可以是明確或 `private`，前提是 `[ServiceContract]` 介面為 `public`。</span><span class="sxs-lookup"><span data-stu-id="841fb-114">If it instead implements a `[ServiceContract]` interface, those method implementations can be explicit or `private`, provided that the `[ServiceContract]` interface is `public`.</span></span>  
  
- <span data-ttu-id="841fb-115">使用 `[ServiceKnownType]` 屬性時，指定的方法必須是 `public`。</span><span class="sxs-lookup"><span data-stu-id="841fb-115">When using the `[ServiceKnownType]` attribute, the method specified must be `public`.</span></span>  
  
- <span data-ttu-id="841fb-116">`[MessageContract]` 類別和其成員都可以是 `public`。</span><span class="sxs-lookup"><span data-stu-id="841fb-116">`[MessageContract]` classes and their members can be `public`.</span></span> <span data-ttu-id="841fb-117">如果 `[MessageContract]` 類別在應用程式組件中定義，它可以是 `internal` 且具有 `internal` 成員。</span><span class="sxs-lookup"><span data-stu-id="841fb-117">If the `[MessageContract]` class is defined in the application assembly it can be `internal` and have `internal` members.</span></span>  
  
## <a name="system-provided-bindings"></a><span data-ttu-id="841fb-118">系統提供的繫結</span><span class="sxs-lookup"><span data-stu-id="841fb-118">System-Provided Bindings</span></span>  
 <span data-ttu-id="841fb-119">部分信任環境可充分支援 <xref:System.ServiceModel.BasicHttpBinding> 和 <xref:System.ServiceModel.WebHttpBinding> 。</span><span class="sxs-lookup"><span data-stu-id="841fb-119">The <xref:System.ServiceModel.BasicHttpBinding> and <xref:System.ServiceModel.WebHttpBinding> are fully supported in a partial trust environment.</span></span> <span data-ttu-id="841fb-120"><xref:System.ServiceModel.WSHttpBinding> 僅支援傳輸安全性模式。</span><span class="sxs-lookup"><span data-stu-id="841fb-120">The <xref:System.ServiceModel.WSHttpBinding> is supported for Transport security mode only.</span></span>  
  
 <span data-ttu-id="841fb-121">在部分信任環境中執行時，不支援使用 HTTP 以外 (例如， <xref:System.ServiceModel.NetTcpBinding>、 <xref:System.ServiceModel.NetNamedPipeBinding>，或 <xref:System.ServiceModel.NetMsmqBinding>) 之傳輸的繫結。</span><span class="sxs-lookup"><span data-stu-id="841fb-121">Bindings that use transports other than HTTP, such as the <xref:System.ServiceModel.NetTcpBinding>, the <xref:System.ServiceModel.NetNamedPipeBinding>, or the <xref:System.ServiceModel.NetMsmqBinding>, are not supported when running in a partial trust environment.</span></span>  
  
## <a name="custom-bindings"></a><span data-ttu-id="841fb-122">自訂繫結</span><span class="sxs-lookup"><span data-stu-id="841fb-122">Custom Bindings</span></span>  
 <span data-ttu-id="841fb-123">自訂繫結可在部分信任環境中建立並加以使用，但是必須遵守本節所指定的限制。</span><span class="sxs-lookup"><span data-stu-id="841fb-123">Custom bindings can be created and used in a partial trust environment, but must follow the restrictions specified in this section.</span></span>  
  
### <a name="transports"></a><span data-ttu-id="841fb-124">傳輸</span><span class="sxs-lookup"><span data-stu-id="841fb-124">Transports</span></span>  
 <span data-ttu-id="841fb-125">唯一允許使用的傳輸繫結項目為 <xref:System.ServiceModel.Channels.HttpTransportBindingElement> 和 <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>。</span><span class="sxs-lookup"><span data-stu-id="841fb-125">The only allowed transport binding elements are <xref:System.ServiceModel.Channels.HttpTransportBindingElement> and <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>.</span></span>  
  
### <a name="encoders"></a><span data-ttu-id="841fb-126">編碼器</span><span class="sxs-lookup"><span data-stu-id="841fb-126">Encoders</span></span>  
 <span data-ttu-id="841fb-127">允許使用下列編碼器：</span><span class="sxs-lookup"><span data-stu-id="841fb-127">The following encoders are allowed:</span></span>  
  
- <span data-ttu-id="841fb-128">文字編碼器 (<xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>)。</span><span class="sxs-lookup"><span data-stu-id="841fb-128">The text encoder (<xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>).</span></span>  
  
- <span data-ttu-id="841fb-129">二進位編碼器 (<xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement>)。</span><span class="sxs-lookup"><span data-stu-id="841fb-129">The binary encoder (<xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement>).</span></span>  
  
- <span data-ttu-id="841fb-130">Web 訊息編碼器 (<xref:System.ServiceModel.Channels.WebMessageEncodingBindingElement>)。</span><span class="sxs-lookup"><span data-stu-id="841fb-130">The Web Message encoder (<xref:System.ServiceModel.Channels.WebMessageEncodingBindingElement>).</span></span>  
  
 <span data-ttu-id="841fb-131">不支援訊息傳輸最佳化機制 (MTOM) 編碼器。</span><span class="sxs-lookup"><span data-stu-id="841fb-131">The Message Transmission Optimization Mechanism (MTOM) encoders are not supported.</span></span>  
  
### <a name="security"></a><span data-ttu-id="841fb-132">安全性</span><span class="sxs-lookup"><span data-stu-id="841fb-132">Security</span></span>  
 <span data-ttu-id="841fb-133">部分信任的應用程式可以使用 WCF 的傳輸層級安全性功能來保護其通訊。</span><span class="sxs-lookup"><span data-stu-id="841fb-133">Partially-trusted applications can use WCF's transport-level security features for securing their communication.</span></span> <span data-ttu-id="841fb-134">不支援訊息層級安全性。</span><span class="sxs-lookup"><span data-stu-id="841fb-134">Message-level security is not supported.</span></span> <span data-ttu-id="841fb-135">設定繫結來使用訊息層級安全性會導致執行階段出現例外狀況。</span><span class="sxs-lookup"><span data-stu-id="841fb-135">Configuring a binding to use message-level security results in an exception at runtime.</span></span>  
  
### <a name="unsupported-bindings"></a><span data-ttu-id="841fb-136">不支援的繫結</span><span class="sxs-lookup"><span data-stu-id="841fb-136">Unsupported Bindings</span></span>  
 <span data-ttu-id="841fb-137">不支援使用可信賴傳訊、交易，或訊息層級安全性的繫結。</span><span class="sxs-lookup"><span data-stu-id="841fb-137">Bindings that use reliable messaging, transactions, or message-level security are not supported.</span></span>  
  
## <a name="serialization"></a><span data-ttu-id="841fb-138">序列化</span><span class="sxs-lookup"><span data-stu-id="841fb-138">Serialization</span></span>  
 <span data-ttu-id="841fb-139">部分信任環境同時支援 <xref:System.Runtime.Serialization.DataContractSerializer> 和 <xref:System.Xml.Serialization.XmlSerializer> 。</span><span class="sxs-lookup"><span data-stu-id="841fb-139">Both the <xref:System.Runtime.Serialization.DataContractSerializer> and the <xref:System.Xml.Serialization.XmlSerializer> are supported in a partial trust environment.</span></span> <span data-ttu-id="841fb-140">然而， <xref:System.Runtime.Serialization.DataContractSerializer> 的使用需視下列情況而定：</span><span class="sxs-lookup"><span data-stu-id="841fb-140">However, use of the <xref:System.Runtime.Serialization.DataContractSerializer> is subject to the following conditions:</span></span>  
  
- <span data-ttu-id="841fb-141">所有可序列化的 `[DataContract]` 型別必須是 `public`。</span><span class="sxs-lookup"><span data-stu-id="841fb-141">All serializable `[DataContract]` types must be `public`.</span></span>  
  
- <span data-ttu-id="841fb-142">`[DataMember]` 型別中所有可序列化的 `[DataContract]` 欄位或屬性必須具有公用和讀/寫性質。</span><span class="sxs-lookup"><span data-stu-id="841fb-142">All serializable `[DataMember]` fields or properties in a `[DataContract]` type must be public and read/write.</span></span> <span data-ttu-id="841fb-143">在部分信任的應用程式中執行 WCF 時，不支援 [readonly](https://go.microsoft.com/fwlink/?LinkID=98854) 欄位的序列化和還原序列化。</span><span class="sxs-lookup"><span data-stu-id="841fb-143">The serialization and deserialization of [readonly](https://go.microsoft.com/fwlink/?LinkID=98854) fields is not supported when running WCF in a partially-trusted application.</span></span>  
  
- <span data-ttu-id="841fb-144">部分信任的環境不支援 `[Serializable]`/ISerializable 程式撰寫模型 (Programming Model)。</span><span class="sxs-lookup"><span data-stu-id="841fb-144">The `[Serializable]`/ISerializable programming model is not supported in a partial trust environment.</span></span>  
  
- <span data-ttu-id="841fb-145">已知型別必須在程式碼或電腦層級組態 (machine.config) 中指定。</span><span class="sxs-lookup"><span data-stu-id="841fb-145">Known types must be specified in code or machine-level configuration (machine.config).</span></span> <span data-ttu-id="841fb-146">為了安全起見，已知型別無法在應用程式層級的組態中指定。</span><span class="sxs-lookup"><span data-stu-id="841fb-146">Known types cannot be specified in application-level configuration for security reasons.</span></span>  
  
- <span data-ttu-id="841fb-147">在部分信任環境中，實作 <xref:System.Runtime.Serialization.IObjectReference> 的型別會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="841fb-147">Types that implement <xref:System.Runtime.Serialization.IObjectReference> throw an exception in a partially-trusted environment.</span></span>  
  
 <span data-ttu-id="841fb-148">如需在部分信任應用程式中安全使用 [Partial Trust Best Practices](partial-trust-best-practices.md) 的詳細資訊，請參閱 <xref:System.Runtime.Serialization.DataContractSerializer> 中的＜序列化＞一節。</span><span class="sxs-lookup"><span data-stu-id="841fb-148">See the Serialization section in [Partial Trust Best Practices](partial-trust-best-practices.md) for more information about security when using <xref:System.Runtime.Serialization.DataContractSerializer> safely in a partially-trusted application.</span></span>  
  
### <a name="collection-types"></a><span data-ttu-id="841fb-149">集合型別</span><span class="sxs-lookup"><span data-stu-id="841fb-149">Collection Types</span></span>  
 <span data-ttu-id="841fb-150">有些集合型別會同時實作 <xref:System.Collections.Generic.IEnumerable%601> 和 <xref:System.Collections.IEnumerable>。</span><span class="sxs-lookup"><span data-stu-id="841fb-150">Some collection types implement both <xref:System.Collections.Generic.IEnumerable%601> and <xref:System.Collections.IEnumerable>.</span></span> <span data-ttu-id="841fb-151">例如，可實作 <xref:System.Collections.Generic.ICollection%601>的型別。</span><span class="sxs-lookup"><span data-stu-id="841fb-151">Examples include types that implement <xref:System.Collections.Generic.ICollection%601>.</span></span> <span data-ttu-id="841fb-152">此類型別可實作 `public` 的 `GetEnumerator()`實作，以及 `GetEnumerator()`的明確實作。</span><span class="sxs-lookup"><span data-stu-id="841fb-152">Such types can implement a `public` implementation of `GetEnumerator()`, and an explicit implementation of `GetEnumerator()`.</span></span> <span data-ttu-id="841fb-153">在此情況下， <xref:System.Runtime.Serialization.DataContractSerializer> 會叫用 `public` 的 `GetEnumerator()`實作，而不是叫用 `GetEnumerator()`的明確實作。</span><span class="sxs-lookup"><span data-stu-id="841fb-153">In this case, <xref:System.Runtime.Serialization.DataContractSerializer> invokes the `public` implementation of `GetEnumerator()`, and not the explicit implementation of `GetEnumerator()`.</span></span> <span data-ttu-id="841fb-154">如果所有 `GetEnumerator()` 實作都不是 `public` ，且都是明確的實作，則 <xref:System.Runtime.Serialization.DataContractSerializer> 會叫用 `IEnumerable.GetEnumerator()`。</span><span class="sxs-lookup"><span data-stu-id="841fb-154">If none of the `GetEnumerator()` implementations are `public` and all are explicit implementations, then <xref:System.Runtime.Serialization.DataContractSerializer> invokes `IEnumerable.GetEnumerator()`.</span></span>  
  
 <span data-ttu-id="841fb-155">針對在部分信任環境中執行 WCF 的集合類型，如果沒有任何執行 `GetEnumerator()` `public` ，或它們都不是明確的介面執行，則會擲回安全性例外狀況。</span><span class="sxs-lookup"><span data-stu-id="841fb-155">For collection types when WCF is running in a partial trust environment, if none of the `GetEnumerator()` implementations are `public`, or none of them are explicit interface implementations, then a security exception is thrown.</span></span>  
  
### <a name="netdatacontractserializer"></a><span data-ttu-id="841fb-156">NetDataContractSerializer</span><span class="sxs-lookup"><span data-stu-id="841fb-156">NetDataContractSerializer</span></span>  
 <span data-ttu-id="841fb-157">在部分信任中， <xref:System.Collections.Generic.List%601>不支援許多 .NET Framework 集合型別，例如 <xref:System.Collections.ArrayList>、 <xref:System.Collections.Generic.Dictionary%602> 、 <xref:System.Collections.Hashtable> 和 <xref:System.Runtime.Serialization.NetDataContractSerializer> 。</span><span class="sxs-lookup"><span data-stu-id="841fb-157">Many .NET Framework collection types such as <xref:System.Collections.Generic.List%601>, <xref:System.Collections.ArrayList>, <xref:System.Collections.Generic.Dictionary%602> and <xref:System.Collections.Hashtable> are not supported by the <xref:System.Runtime.Serialization.NetDataContractSerializer> in partial trust.</span></span> <span data-ttu-id="841fb-158">這些型別的 `[Serializable]` 屬性都已經過設定，如前面「序列化」一節所述，部分信任的環境不支援這個屬性。</span><span class="sxs-lookup"><span data-stu-id="841fb-158">These types have the `[Serializable]` attribute set, and as stated previously in the Serialization section, this attribute is not supported in partial trust.</span></span> <span data-ttu-id="841fb-159"><xref:System.Runtime.Serialization.DataContractSerializer> 會以特殊方式處理集合，因此能夠解決這個限制，但 <xref:System.Runtime.Serialization.NetDataContractSerializer> 沒有這類機制來避免這個限制。</span><span class="sxs-lookup"><span data-stu-id="841fb-159">The <xref:System.Runtime.Serialization.DataContractSerializer> treats collections in a special way and is thus able to get around this restriction, but the <xref:System.Runtime.Serialization.NetDataContractSerializer> has no such mechanism to circumvent this restriction.</span></span>  
  
 <span data-ttu-id="841fb-160">在部分信任中， <xref:System.DateTimeOffset> 不支援 <xref:System.Runtime.Serialization.NetDataContractSerializer> 型別。</span><span class="sxs-lookup"><span data-stu-id="841fb-160">The <xref:System.DateTimeOffset> type is not supported by the <xref:System.Runtime.Serialization.NetDataContractSerializer> in partial trust.</span></span>  
  
 <span data-ttu-id="841fb-161">在部分信任中執行時，無法搭配 <xref:System.Runtime.Serialization.NetDataContractSerializer> 使用代理 (透過 <xref:System.Runtime.Serialization.SurrogateSelector> 機制)。</span><span class="sxs-lookup"><span data-stu-id="841fb-161">A surrogate cannot be used with the <xref:System.Runtime.Serialization.NetDataContractSerializer> (using the <xref:System.Runtime.Serialization.SurrogateSelector> mechanism) when running in partial trust.</span></span> <span data-ttu-id="841fb-162">請注意，這個限制只適用於使用代理時，不適用於序列化代理時。</span><span class="sxs-lookup"><span data-stu-id="841fb-162">Note that this restriction applies to using a surrogate, not to serializing it.</span></span>  
  
## <a name="enabling-common-behaviors-to-run"></a><span data-ttu-id="841fb-163">讓通用行為執行</span><span class="sxs-lookup"><span data-stu-id="841fb-163">Enabling Common Behaviors to Run</span></span>  
 <span data-ttu-id="841fb-164"><xref:System.Security.AllowPartiallyTrustedCallersAttribute>當應用程式在部分信任環境中執行時，不會執行未以屬性標示 (APTCA) 的服務或端點行為，因為當 [\<commonBehaviors>](../../configure-apps/file-schema/wcf/commonbehaviors.md) 應用程式在部分信任環境中執行，而且發生此情況時，不會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="841fb-164">Service or endpoint behaviors not marked with the <xref:System.Security.AllowPartiallyTrustedCallersAttribute> attribute (APTCA) that are added to the [\<commonBehaviors>](../../configure-apps/file-schema/wcf/commonbehaviors.md) section of a configuration file are not run when the application runs in a partial trust environment and no exception is thrown when this occurs.</span></span> <span data-ttu-id="841fb-165">若要強制執行通用行為，您必須執行下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="841fb-165">To enforce the running of common behaviors, you must do one of the following options:</span></span>  
  
- <span data-ttu-id="841fb-166">使用 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> 屬性標記您的通用行為，讓它可以在部署為部分信任應用程式時執行。</span><span class="sxs-lookup"><span data-stu-id="841fb-166">Mark your common behavior with the <xref:System.Security.AllowPartiallyTrustedCallersAttribute> attribute so that it can run when deployed as a partial trust application.</span></span> <span data-ttu-id="841fb-167">請注意，您可以在電腦上設定登錄項目，以防止已標記 APTCA 的組件執行。</span><span class="sxs-lookup"><span data-stu-id="841fb-167">Note that a registry entry can be set on the computer to prevent APTCA-marked assemblies from running.</span></span> <span data-ttu-id="841fb-168">.</span><span class="sxs-lookup"><span data-stu-id="841fb-168">.</span></span>  
  
- <span data-ttu-id="841fb-169">確定應用程式是否會部署為完全信任的應用程式，而使用者無法修改程式碼存取安全性設定以在部分信任環境中執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="841fb-169">Ensure that if the application is deployed as a fully-trusted application that users cannot modify the code-access security settings to run the application in a partial trust environment.</span></span> <span data-ttu-id="841fb-170">如果可以執行這項操作，行為就不會執行，也不會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="841fb-170">If they can do so, the behavior does not run and no exception is thrown.</span></span> <span data-ttu-id="841fb-171">若要確保這一點，請參閱使用[Caspol.exe (代碼啟用安全性原則工具) ](../../tools/caspol-exe-code-access-security-policy-tool.md)的 [ **levelfinal** ] 選項。</span><span class="sxs-lookup"><span data-stu-id="841fb-171">To ensure this, see the **levelfinal** option using [Caspol.exe (Code Access Security Policy Tool)](../../tools/caspol-exe-code-access-security-policy-tool.md).</span></span>  
  
 <span data-ttu-id="841fb-172">如需常見行為的範例，請參閱 [如何：鎖定企業中的端點](../extending/how-to-lock-down-endpoints-in-the-enterprise.md)。</span><span class="sxs-lookup"><span data-stu-id="841fb-172">For an example of a common behavior, see [How to: Lock Down Endpoints in the Enterprise](../extending/how-to-lock-down-endpoints-in-the-enterprise.md).</span></span>  
  
## <a name="configuration"></a><span data-ttu-id="841fb-173">組態</span><span class="sxs-lookup"><span data-stu-id="841fb-173">Configuration</span></span>  
 <span data-ttu-id="841fb-174">有一個例外狀況，部分信任程式碼只能在本機檔案中載入 WCF 設定區段 `app.config` 。</span><span class="sxs-lookup"><span data-stu-id="841fb-174">With one exception, partially-trusted code can only load WCF configuration sections in the local `app.config` file.</span></span> <span data-ttu-id="841fb-175">若要載入參考 machine.config 中或根 web.config 檔案中 WCF 區段的 WCF 設定區段，需要 ConfigurationPermission (不受限制的) 。</span><span class="sxs-lookup"><span data-stu-id="841fb-175">To load WCF configuration sections that reference WCF sections in machine.config or in a root web.config file requires ConfigurationPermission(Unrestricted).</span></span> <span data-ttu-id="841fb-176">若沒有此許可權，對 WCF 設定區段的參考 (行為、在本機設定檔之外) 系結，會導致載入設定時發生例外狀況。</span><span class="sxs-lookup"><span data-stu-id="841fb-176">Without this permission, references to WCF configuration sections (behaviors, bindings) outside of the local configuration file results in an exception when the configuration is loaded.</span></span>  
  
 <span data-ttu-id="841fb-177">唯一的例外是序列化的已知型別組態，如本主題的「序列化」一節所述。</span><span class="sxs-lookup"><span data-stu-id="841fb-177">The one exception is known-type configuration for serialization, as described in the Serialization section of this topic.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="841fb-178">只有在完全信任下執行時，才支援設定延伸。</span><span class="sxs-lookup"><span data-stu-id="841fb-178">Configuration extensions are only supported when running under Full Trust.</span></span>  
  
## <a name="diagnostics"></a><span data-ttu-id="841fb-179">診斷</span><span class="sxs-lookup"><span data-stu-id="841fb-179">Diagnostics</span></span>  
  
### <a name="event-logging"></a><span data-ttu-id="841fb-180">事件記錄</span><span class="sxs-lookup"><span data-stu-id="841fb-180">Event Logging</span></span>  
 <span data-ttu-id="841fb-181">在部分信任下，只支援有限的事件記錄。</span><span class="sxs-lookup"><span data-stu-id="841fb-181">Limited event logging is supported under partial trust.</span></span> <span data-ttu-id="841fb-182">只有服務啟動錯誤以及追蹤/訊息記錄失敗，才會記錄至事件記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="841fb-182">Only service activation faults and tracing/message logging failures are logged to the Event Log.</span></span> <span data-ttu-id="841fb-183">處理序最多可以記錄 5 個事件數目，以避免事件記錄檔中寫入過多訊息。</span><span class="sxs-lookup"><span data-stu-id="841fb-183">The maximum number of events that can be logged by a process is 5, to avoid writing excessive messages to the Event Log.</span></span>  
  
### <a name="message-logging"></a><span data-ttu-id="841fb-184">訊息記錄</span><span class="sxs-lookup"><span data-stu-id="841fb-184">Message Logging</span></span>  
 <span data-ttu-id="841fb-185">當 WCF 在部分信任環境中執行時，訊息記錄無法運作。</span><span class="sxs-lookup"><span data-stu-id="841fb-185">Message logging does not work when WCF is run in a partial trust environment.</span></span> <span data-ttu-id="841fb-186">如果在部分信任情況下啟用的話，儘管不會導致服務啟動失敗，但也無法記錄訊息。</span><span class="sxs-lookup"><span data-stu-id="841fb-186">If enabled under partial trust, it does not fail service activation, but no message is logged.</span></span>  
  
### <a name="tracing"></a><span data-ttu-id="841fb-187">追蹤</span><span class="sxs-lookup"><span data-stu-id="841fb-187">Tracing</span></span>  
 <span data-ttu-id="841fb-188">在部分信任環境中執行時，可使用受限制的追蹤功能。</span><span class="sxs-lookup"><span data-stu-id="841fb-188">Restricted tracing functionality is available when running in a partial trust environment.</span></span> <span data-ttu-id="841fb-189">在設定檔的 <> 專案中 `listeners` ，您可以新增的唯一類型是 <xref:System.Diagnostics.TextWriterTraceListener> 和新的 <xref:System.Diagnostics.EventSchemaTraceListener> 。</span><span class="sxs-lookup"><span data-stu-id="841fb-189">In the <`listeners`> element in the configuration file, the only types that you can add are <xref:System.Diagnostics.TextWriterTraceListener> and the new <xref:System.Diagnostics.EventSchemaTraceListener>.</span></span> <span data-ttu-id="841fb-190">使用標準 <xref:System.Diagnostics.XmlWriterTraceListener> 可能導致不完整或不正確的記錄。</span><span class="sxs-lookup"><span data-stu-id="841fb-190">Use of the standard <xref:System.Diagnostics.XmlWriterTraceListener> may result in incomplete or incorrect logs.</span></span>  
  
 <span data-ttu-id="841fb-191">下列為支援的追蹤來源：</span><span class="sxs-lookup"><span data-stu-id="841fb-191">Supported trace sources are:</span></span>  
  
- <xref:System.ServiceModel>  
  
- <xref:System.Runtime.Serialization>  
  
- <span data-ttu-id="841fb-192"><xref:System.IdentityModel.Claims>、<xref:System.IdentityModel.Policy>、<xref:System.IdentityModel.Selectors> 和 <xref:System.IdentityModel.Tokens>。</span><span class="sxs-lookup"><span data-stu-id="841fb-192"><xref:System.IdentityModel.Claims>, <xref:System.IdentityModel.Policy>, <xref:System.IdentityModel.Selectors>, and <xref:System.IdentityModel.Tokens>.</span></span>  
  
 <span data-ttu-id="841fb-193">下列為不支援的追蹤來源：</span><span class="sxs-lookup"><span data-stu-id="841fb-193">The following trace sources are not supported:</span></span>  
  
- <span data-ttu-id="841fb-194">CardSpace</span><span class="sxs-lookup"><span data-stu-id="841fb-194">CardSpace</span></span>  
  
- <xref:System.IO.Log>  

- <span data-ttu-id="841fb-195">[System.servicemodel. transactionbridge 發生](/previous-versions/aa346556(v=vs.110))]</span><span class="sxs-lookup"><span data-stu-id="841fb-195">[System.ServiceModel.Internal.TransactionBridge](/previous-versions/aa346556(v=vs.110))]</span></span>
  
 <span data-ttu-id="841fb-196">您不應該指定下列 <xref:System.Diagnostics.TraceOptions> 列舉成員：</span><span class="sxs-lookup"><span data-stu-id="841fb-196">The following members of the <xref:System.Diagnostics.TraceOptions> enumeration should not be specified:</span></span>  
  
- <xref:System.Diagnostics.TraceOptions.Callstack?displayProperty=nameWithType>  
  
- <xref:System.Diagnostics.TraceOptions.ProcessId?displayProperty=nameWithType>  
  
 <span data-ttu-id="841fb-197">在部分信任環境中使用追蹤時，請確定應用程式擁有足夠的權限來儲存追蹤接聽項的輸出。</span><span class="sxs-lookup"><span data-stu-id="841fb-197">When using tracing in a partial trust environment, ensure that the application has sufficient permissions to store the output of the trace listener.</span></span> <span data-ttu-id="841fb-198">例如，使用 <xref:System.Diagnostics.TextWriterTraceListener> 將追蹤輸出寫入至文字檔時，請確定應用程式具有必要的 FileIOPermission 來順利寫入追蹤檔。</span><span class="sxs-lookup"><span data-stu-id="841fb-198">For example, when using the <xref:System.Diagnostics.TextWriterTraceListener> to write trace output to a text file, ensure that the application has the necessary FileIOPermission required to successfully write to the trace file.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="841fb-199">為了避免在發生重複錯誤的情況下擴散追蹤檔案，WCF 會在第一次安全性失敗之後停用資源或動作的追蹤。</span><span class="sxs-lookup"><span data-stu-id="841fb-199">To avoid flooding the trace files with duplicate errors, WCF disables tracing of the resource or action after the first security failure.</span></span> <span data-ttu-id="841fb-200">第一次嘗試存取資源或執行動作時，會針對每個失敗的資源存取產生一個例外狀況追蹤。</span><span class="sxs-lookup"><span data-stu-id="841fb-200">There is one exception trace for each failed resource access, the first time an attempt is made to access the resource or perform the action.</span></span>  
  
## <a name="wcf-service-host"></a><span data-ttu-id="841fb-201">WCF 服務主機</span><span class="sxs-lookup"><span data-stu-id="841fb-201">WCF Service Host</span></span>  
 <span data-ttu-id="841fb-202">WCF 服務主機不支援部分信任。</span><span class="sxs-lookup"><span data-stu-id="841fb-202">WCF service host does not support partial trust.</span></span> <span data-ttu-id="841fb-203">如果您想要在部分信任中使用 WCF 服務，請不要使用 Visual Studio 中的 [WCF 服務程式庫] 專案範本來建立您的服務。</span><span class="sxs-lookup"><span data-stu-id="841fb-203">If you want to use a WCF service in partial trust, do not use the WCF Service Library Project template in Visual Studio to build your service.</span></span> <span data-ttu-id="841fb-204">請改為在 Visual Studio 中建立新的網站，方法是選擇 WCF 服務網站範本，此範本可以在支援 WCF 部分信任的 Web 服務器上裝載服務。</span><span class="sxs-lookup"><span data-stu-id="841fb-204">Instead, create a new Web site in Visual Studio by choosing the WCF service Web site template, which can host the service in a Web server on which WCF partial trust is supported.</span></span>  
  
## <a name="other-limitations"></a><span data-ttu-id="841fb-205">其他限制</span><span class="sxs-lookup"><span data-stu-id="841fb-205">Other Limitations</span></span>  

  <span data-ttu-id="841fb-206">WCF 通常僅限於裝載應用程式所強加的安全性考慮。</span><span class="sxs-lookup"><span data-stu-id="841fb-206">WCF is generally limited to the security considerations imposed upon it by the hosting application.</span></span> <span data-ttu-id="841fb-207">例如，如果 WCF 裝載于 XAML 瀏覽器應用程式 (XBAP) ，它會受限於 XBAP 限制，如 [Windows Presentation Foundation 部分信任安全性](/dotnet/desktop/wpf/wpf-partial-trust-security)所述。</span><span class="sxs-lookup"><span data-stu-id="841fb-207">For example, if WCF is hosted in a XAML Browser Application (XBAP), it is subject to XBAP limitations, as described in [Windows Presentation Foundation Partial Trust Security](/dotnet/desktop/wpf/wpf-partial-trust-security).</span></span>  
  
 <span data-ttu-id="841fb-208">在部分信任環境中執行 indigo2 時，不會啟用下列額外的功能：</span><span class="sxs-lookup"><span data-stu-id="841fb-208">The following additional features are not enabled when running indigo2 in a partial trust environment:</span></span>  
  
- <span data-ttu-id="841fb-209">Windows Management Instrumentation (WMI)</span><span class="sxs-lookup"><span data-stu-id="841fb-209">Windows Management Instrumentation (WMI)</span></span>  
  
- <span data-ttu-id="841fb-210">僅部分啟用事件記錄 (請參閱「 **診斷** 」一節中的討論)。</span><span class="sxs-lookup"><span data-stu-id="841fb-210">Event logging is only partially enabled (see discussion in **Diagnostics** section).</span></span>  
  
- <span data-ttu-id="841fb-211">效能計數器</span><span class="sxs-lookup"><span data-stu-id="841fb-211">Performance counters</span></span>  
  
 <span data-ttu-id="841fb-212">在部分信任環境中使用不支援的 WCF 功能，可能會在執行時間導致例外狀況。</span><span class="sxs-lookup"><span data-stu-id="841fb-212">Use of WCF features that are not supported in a partial trust environment may result in exceptions at runtime.</span></span>  
  
## <a name="unlisted-features"></a><span data-ttu-id="841fb-213">未列出的功能</span><span class="sxs-lookup"><span data-stu-id="841fb-213">Unlisted Features</span></span>  
 <span data-ttu-id="841fb-214">在部分信任環境中執行時，要找到不可用的資訊片段或動作的最好方式，就是嘗試在 `try` 區塊內部存取資源或執行動作，然後捕捉 ( `catch` ) 失敗。</span><span class="sxs-lookup"><span data-stu-id="841fb-214">The best way to discover that a piece of information or action is unavailable when running in a partial trust environment is to try to access the resource or do the action inside of a `try` block, and then `catch` the failure.</span></span> <span data-ttu-id="841fb-215">為了避免在發生重複錯誤的情況下擴散追蹤檔案，WCF 會在第一次安全性失敗之後停用資源或動作的追蹤。</span><span class="sxs-lookup"><span data-stu-id="841fb-215">To avoid flooding the trace files with duplicate errors, WCF disables tracing of the resource or action after the first security failure.</span></span> <span data-ttu-id="841fb-216">第一次嘗試存取資源或執行動作時，會針對每個失敗的資源存取產生一個例外狀況追蹤。</span><span class="sxs-lookup"><span data-stu-id="841fb-216">There is one exception trace for each failed resource access, the first time an attempt is made to access the resource or perform the action.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="841fb-217">另請參閱</span><span class="sxs-lookup"><span data-stu-id="841fb-217">See also</span></span>

- <xref:System.ServiceModel.Channels.HttpTransportBindingElement>
- <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>
- <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>
- <xref:System.ServiceModel.Channels.WebMessageEncodingBindingElement>
- [<span data-ttu-id="841fb-218">支援的部署案例</span><span class="sxs-lookup"><span data-stu-id="841fb-218">Supported Deployment Scenarios</span></span>](supported-deployment-scenarios.md)
- [<span data-ttu-id="841fb-219">部分信任最佳做法</span><span class="sxs-lookup"><span data-stu-id="841fb-219">Partial Trust Best Practices</span></span>](partial-trust-best-practices.md)
