---
title: 使用繫結來設定服務和用戶端
description: 系結包含 WFC 用戶端或服務所使用的設定資訊。 瞭解如何定義系結，以及如何指定服務端點的系結。
ms.date: 03/30/2017
helpviewer_keywords:
- bindings [WCF], using
ms.assetid: c39479c3-0766-4a17-ba4c-97a74607f392
ms.openlocfilehash: 38fa4a928c74f9fff7b67f2479f9304331361fef
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96289876"
---
# <a name="using-bindings-to-configure-services-and-clients"></a><span data-ttu-id="f25e9-104">使用繫結來設定服務和用戶端</span><span class="sxs-lookup"><span data-stu-id="f25e9-104">Using Bindings to Configure Services and Clients</span></span>

<span data-ttu-id="f25e9-105">繫結是指定連接端點所需要之通訊詳細資料的物件。</span><span class="sxs-lookup"><span data-stu-id="f25e9-105">Bindings are objects that specify the communication details required to connect to an endpoint.</span></span> <span data-ttu-id="f25e9-106">更明確的說，繫結包含藉由定義傳輸、網路格式 (訊息編碼) 的細節，用於建立用戶端或服務執行階段的組態資訊，以及用於個別端點或用戶端通道的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="f25e9-106">More specifically, bindings contain configuration information that is used to create the client or service runtime by defining the specifics of transports, wire-formats (message encoding), and protocols to use for the respective endpoint or client channel.</span></span> <span data-ttu-id="f25e9-107">若要建立可運作的 Windows Communication Foundation (WCF) 服務，服務中的每個端點都需要系結。</span><span class="sxs-lookup"><span data-stu-id="f25e9-107">To create a functioning Windows Communication Foundation (WCF) service, each endpoint in the service requires a binding.</span></span> <span data-ttu-id="f25e9-108">本主題將說明什麼是繫結、如何定義繫結，以及如何為端點指定特定繫結。</span><span class="sxs-lookup"><span data-stu-id="f25e9-108">This topic explains what bindings are, how they are defined, and how a particular binding is specified for an endpoint.</span></span>  
  
## <a name="what-a-binding-defines"></a><span data-ttu-id="f25e9-109">繫結所定義的內容</span><span class="sxs-lookup"><span data-stu-id="f25e9-109">What a Binding Defines</span></span>  

 <span data-ttu-id="f25e9-110">繫結中的資訊可能很基本，也可能很複雜。</span><span class="sxs-lookup"><span data-stu-id="f25e9-110">The information in a binding can be very basic or very complex.</span></span> <span data-ttu-id="f25e9-111">最基本的繫結只會指定連線至端點時必須使用的傳輸通訊協定 (例如 HTTP)。</span><span class="sxs-lookup"><span data-stu-id="f25e9-111">The most basic binding specifies only the transport protocol (such as HTTP) that must be used to connect to the endpoint.</span></span> <span data-ttu-id="f25e9-112">說的更簡單一點，繫結中所含有關如何連線至端點的資訊，屬於下表其中一種類別。</span><span class="sxs-lookup"><span data-stu-id="f25e9-112">More generally, the information a binding contains about how to connect to an endpoint falls into one of the categories in the following table.</span></span>  
  
 <span data-ttu-id="f25e9-113">通訊協定</span><span class="sxs-lookup"><span data-stu-id="f25e9-113">Protocols</span></span>  
 <span data-ttu-id="f25e9-114">判斷使用的安全性機制，是可靠的傳訊能力或交易內容流量設定。</span><span class="sxs-lookup"><span data-stu-id="f25e9-114">Determines the security mechanism being used, either reliable messaging capability or transaction context flow settings.</span></span>  
  
 <span data-ttu-id="f25e9-115">傳輸</span><span class="sxs-lookup"><span data-stu-id="f25e9-115">Transport</span></span>  
 <span data-ttu-id="f25e9-116">判斷要使用的基礎傳輸通訊協定 (例如，TCP 或 HTTP)。</span><span class="sxs-lookup"><span data-stu-id="f25e9-116">Determines the underlying transport protocol to use (for example, TCP or HTTP).</span></span>  
  
 <span data-ttu-id="f25e9-117">編碼</span><span class="sxs-lookup"><span data-stu-id="f25e9-117">Encoding</span></span>  
 <span data-ttu-id="f25e9-118">判斷訊息編碼，例如 text/XML、二進位或 Message Transmission Optimization Mechanism (MTOM)，它會決定在網路上如何將訊息表示為位元組資料流。</span><span class="sxs-lookup"><span data-stu-id="f25e9-118">Determines the message encoding, for example, text/XML, binary, or Message Transmission Optimization Mechanism (MTOM), which determines how messages are represented as byte streams on the wire.</span></span>  
  
## <a name="system-provided-bindings"></a><span data-ttu-id="f25e9-119">系統提供的繫結</span><span class="sxs-lookup"><span data-stu-id="f25e9-119">System-Provided Bindings</span></span>  

 <span data-ttu-id="f25e9-120">WCF 包含一組系統提供的系結，其設計目的是要涵蓋大部分的應用程式需求和案例。</span><span class="sxs-lookup"><span data-stu-id="f25e9-120">WCF includes a set of system-provided bindings that are designed to cover most application requirements and scenarios.</span></span> <span data-ttu-id="f25e9-121">下列類別則表示系統提供之繫結的一些範例：</span><span class="sxs-lookup"><span data-stu-id="f25e9-121">The following classes represent some examples of system-provided bindings:</span></span>  
  
- <span data-ttu-id="f25e9-122"><xref:System.ServiceModel.BasicHttpBinding>：一種 HTTP 通訊協定繫結，適用於連線至 Web 服務，並符合 WS-I Basic Profile 1.1 規格 (例如，以 ASP.NET Web 服務 [ASMX] 為基礎的服務)。</span><span class="sxs-lookup"><span data-stu-id="f25e9-122"><xref:System.ServiceModel.BasicHttpBinding>: An HTTP protocol binding suitable for connecting to Web services that conforms to the WS-I Basic Profile 1.1 specification (for example, ASP.NET Web services [ASMX]-based services).</span></span>  
  
- <span data-ttu-id="f25e9-123"><xref:System.ServiceModel.WSHttpBinding>：一種 HTTP 通訊協定繫結，適用於連線至符合 Web 服務規格通訊協定的端點。</span><span class="sxs-lookup"><span data-stu-id="f25e9-123"><xref:System.ServiceModel.WSHttpBinding>: An HTTP protocol binding suitable for connecting to endpoints that conform to the Web services specifications protocols.</span></span>  
  
- <span data-ttu-id="f25e9-124"><xref:System.ServiceModel.NetNamedPipeBinding>：使用 .NET 二進位編碼和框架技術搭配 Windows 具名管道傳輸，以連接到同一部電腦上的其他 WCF 端點。</span><span class="sxs-lookup"><span data-stu-id="f25e9-124"><xref:System.ServiceModel.NetNamedPipeBinding>: Uses the .NET binary encoding and framing technologies in conjunction with the Windows named pipe transport to connect to other WCF endpoints on the same machine.</span></span>  
  
- <span data-ttu-id="f25e9-125"><xref:System.ServiceModel.NetMsmqBinding>：使用 .NET 二進位編碼和框架技術搭配訊息佇列 (也稱為 MSMQ) ，以建立與其他 WCF 端點的佇列訊息連接。</span><span class="sxs-lookup"><span data-stu-id="f25e9-125"><xref:System.ServiceModel.NetMsmqBinding>: Uses the .NET binary encoding and framing technologies in conjunction with the Message Queuing (also known as MSMQ) to create queued message connections with other WCF endpoints.</span></span>  
  
 <span data-ttu-id="f25e9-126">如需系統提供之系結的完整清單和描述，請參閱 [系統提供](system-provided-bindings.md)的系結。</span><span class="sxs-lookup"><span data-stu-id="f25e9-126">For a complete list of system-provided bindings, with descriptions, see [System-Provided Bindings](system-provided-bindings.md).</span></span>  
  
## <a name="custom-bindings"></a><span data-ttu-id="f25e9-127">自訂繫結</span><span class="sxs-lookup"><span data-stu-id="f25e9-127">Custom Bindings</span></span>  

 <span data-ttu-id="f25e9-128">如果系統提供的繫結集合沒有服務應用程式所需的正確功能組合，您可以建立 <xref:System.ServiceModel.Channels.CustomBinding> 繫結。</span><span class="sxs-lookup"><span data-stu-id="f25e9-128">If the system-provided binding collection does not have the correct combination of features that a service application requires, you can create a <xref:System.ServiceModel.Channels.CustomBinding> binding.</span></span> <span data-ttu-id="f25e9-129">如需系結元素的詳細資訊 <xref:System.ServiceModel.Channels.CustomBinding> ，請參閱 [\<customBinding>](../configure-apps/file-schema/wcf/custombinding.md) 和 [自訂](./extending/custom-bindings.md)系結。</span><span class="sxs-lookup"><span data-stu-id="f25e9-129">For more information about the elements of a <xref:System.ServiceModel.Channels.CustomBinding> binding, see [\<customBinding>](../configure-apps/file-schema/wcf/custombinding.md) and [Custom Bindings](./extending/custom-bindings.md).</span></span>  
  
## <a name="using-bindings"></a><span data-ttu-id="f25e9-130">使用繫結</span><span class="sxs-lookup"><span data-stu-id="f25e9-130">Using Bindings</span></span>  

 <span data-ttu-id="f25e9-131">使用繫結牽涉到兩個基本步驟：</span><span class="sxs-lookup"><span data-stu-id="f25e9-131">Using bindings entails two basic steps:</span></span>  
  
1. <span data-ttu-id="f25e9-132">選取或定義繫結。</span><span class="sxs-lookup"><span data-stu-id="f25e9-132">Select or define a binding.</span></span> <span data-ttu-id="f25e9-133">最簡單的方法是選擇其中一個系統提供的繫結，並使用其預設值。</span><span class="sxs-lookup"><span data-stu-id="f25e9-133">The easiest method is to choose one of the system-provided bindings and use its default settings.</span></span> <span data-ttu-id="f25e9-134">也可以選擇系統提供的繫結程序，並重設其屬性值以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="f25e9-134">You can also choose a system-provided binding and reset its property values to suit your requirements.</span></span> <span data-ttu-id="f25e9-135">或者，您可以建立自訂繫結並依需要設定每個屬性。</span><span class="sxs-lookup"><span data-stu-id="f25e9-135">Alternatively, you can create a custom binding and set every property as required.</span></span>  
  
2. <span data-ttu-id="f25e9-136">請建立使用這個繫結的端點。</span><span class="sxs-lookup"><span data-stu-id="f25e9-136">Create an endpoint that uses this binding.</span></span>  
  
## <a name="code-and-configuration"></a><span data-ttu-id="f25e9-137">程式碼和組態</span><span class="sxs-lookup"><span data-stu-id="f25e9-137">Code and Configuration</span></span>  

 <span data-ttu-id="f25e9-138">您可以透過程式碼或組態來定義或設定繫結。</span><span class="sxs-lookup"><span data-stu-id="f25e9-138">You can define or configure bindings through code or configuration.</span></span> <span data-ttu-id="f25e9-139">這兩種方法與所使用的繫結型別無關，例如，您是否使用系統提供的或 <xref:System.ServiceModel.Channels.CustomBinding> 繫結。</span><span class="sxs-lookup"><span data-stu-id="f25e9-139">These two approaches are independent of the type of binding used, for example, whether you are using a system-provided or a <xref:System.ServiceModel.Channels.CustomBinding> binding.</span></span> <span data-ttu-id="f25e9-140">一般來說，使用程式碼可讓您在編譯時完全控制繫結的定義。</span><span class="sxs-lookup"><span data-stu-id="f25e9-140">In general, using code gives you complete control over the definition of a binding when you compile.</span></span> <span data-ttu-id="f25e9-141">另一方面，使用設定可讓 WCF 服務或用戶端的系統管理員或使用者變更系結的參數。</span><span class="sxs-lookup"><span data-stu-id="f25e9-141">Using configuration, on the other hand, allows a system administrator or the user of a WCF service or client to change the parameters of bindings.</span></span> <span data-ttu-id="f25e9-142">這種彈性通常很理想，因為沒有任何方法可以預測要部署 WCF 應用程式的特定電腦需求和網路狀況。</span><span class="sxs-lookup"><span data-stu-id="f25e9-142">This flexibility is often desirable because there is no way to predict the specific machine requirements and network conditions into which a WCF application is to be deployed.</span></span> <span data-ttu-id="f25e9-143">將繫結 (和位址) 資訊和程式碼分開可讓系統管理員變更繫結詳細資料，而不需要重新編譯或重新部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="f25e9-143">Separating the binding (and addressing) information from the code allows administrators to change the binding details without having to recompile or redeploy the application.</span></span> <span data-ttu-id="f25e9-144">請注意，如果繫結是以程式碼定義的，它會覆寫組態檔中任何以組態為基礎所做的定義。</span><span class="sxs-lookup"><span data-stu-id="f25e9-144">Note that if the binding is defined in code, it overwrites any configuration-based definitions made in the configuration file.</span></span> <span data-ttu-id="f25e9-145">如需這些方法的範例，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="f25e9-145">For examples of these approaches, see the following topics:</span></span>  
  
- <span data-ttu-id="f25e9-146">[如何：在 Managed 應用程式中裝載 WCF 服務](how-to-host-a-wcf-service-in-a-managed-application.md) 提供在程式碼中建立系結的範例。</span><span class="sxs-lookup"><span data-stu-id="f25e9-146">[How to: Host a WCF Service in a Managed Application](how-to-host-a-wcf-service-in-a-managed-application.md) provides an example of creating a binding in code.</span></span>  
  
- <span data-ttu-id="f25e9-147">[教學課程：建立 Windows Communication Foundation 用戶端](how-to-create-a-wcf-client.md) 提供使用設定建立用戶端的範例。</span><span class="sxs-lookup"><span data-stu-id="f25e9-147">[Tutorial: Create a Windows Communication Foundation client](how-to-create-a-wcf-client.md) provides an example of creating a client by using configuration.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f25e9-148">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f25e9-148">See also</span></span>

- [<span data-ttu-id="f25e9-149">端點建立概觀</span><span class="sxs-lookup"><span data-stu-id="f25e9-149">Endpoint Creation Overview</span></span>](endpoint-creation-overview.md)
- [<span data-ttu-id="f25e9-150">作法：在組態中指定服務繫結</span><span class="sxs-lookup"><span data-stu-id="f25e9-150">How to: Specify a Service Binding in Configuration</span></span>](how-to-specify-a-service-binding-in-configuration.md)
- [<span data-ttu-id="f25e9-151">作法：在程式碼中指定服務繫結</span><span class="sxs-lookup"><span data-stu-id="f25e9-151">How to: Specify a Service Binding in Code</span></span>](how-to-specify-a-service-binding-in-code.md)
- [<span data-ttu-id="f25e9-152">作法：在組態中指定用戶端繫結</span><span class="sxs-lookup"><span data-stu-id="f25e9-152">How to: Specify a Client Binding in Configuration</span></span>](how-to-specify-a-client-binding-in-configuration.md)
- [<span data-ttu-id="f25e9-153">作法：在程式碼中指定用戶端繫結</span><span class="sxs-lookup"><span data-stu-id="f25e9-153">How to: Specify a Client Binding in Code</span></span>](how-to-specify-a-client-binding-in-code.md)
