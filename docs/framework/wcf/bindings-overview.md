---
title: Windows Communication Foundation 繫結概觀
description: 瞭解系結，此系結會指定如何連接至 WCF 服務，包括系結的元素，以及如何指定服務端點的系結。
ms.date: 03/30/2017
helpviewer_keywords:
- bindings [WCF], overview
ms.assetid: cfb5842f-e0f9-4c56-a015-f2b33f258232
ms.openlocfilehash: e918844342a20e7b6c22ef6a9fd3c01fe27db059
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96272471"
---
# <a name="windows-communication-foundation-bindings-overview"></a><span data-ttu-id="7a7aa-103">Windows Communication Foundation 繫結概觀</span><span class="sxs-lookup"><span data-stu-id="7a7aa-103">Windows Communication Foundation Bindings Overview</span></span>

<span data-ttu-id="7a7aa-104">系結是物件，可用來指定連接至 Windows Communication Foundation (WCF) 服務端點所需的通訊詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-104">Bindings are objects that are used to specify the communication details that are required to connect to the endpoint of a Windows Communication Foundation (WCF) service.</span></span> <span data-ttu-id="7a7aa-105">WCF 服務中的每個端點都需要正確指定的繫結。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-105">Each endpoint in a WCF service requires a binding to be well-specified.</span></span> <span data-ttu-id="7a7aa-106">本主題概述系結所定義的通訊詳細資料類型、系結的元素、WCF 中包含的系結，以及如何為端點指定系結。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-106">This topic outlines the types of communication details that the bindings define, the elements of a binding, what bindings are included in WCF, and how a binding can be specified for an endpoint.</span></span>  
  
## <a name="what-a-binding-defines"></a><span data-ttu-id="7a7aa-107">繫結所定義的內容</span><span class="sxs-lookup"><span data-stu-id="7a7aa-107">What a Binding Defines</span></span>  

 <span data-ttu-id="7a7aa-108">繫結中的資訊可能很基本，也可能很複雜。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-108">The information in a binding can be very basic, or very complex.</span></span> <span data-ttu-id="7a7aa-109">最基本的繫結只會指定連線至端點時必須使用的傳輸通訊協定 (例如 HTTP)。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-109">The most basic binding specifies only the transport protocol (such as HTTP) that must be used to connect to the endpoint.</span></span> <span data-ttu-id="7a7aa-110">一般來說，系結所包含有關如何連接到端點的資訊屬於下列其中一個類別：</span><span class="sxs-lookup"><span data-stu-id="7a7aa-110">More generally, the information a binding contains about how to connect to an endpoint falls into one of the following categories:</span></span>  
  
 <span data-ttu-id="7a7aa-111">**通訊協定**</span><span class="sxs-lookup"><span data-stu-id="7a7aa-111">**Protocols**</span></span>  
 <span data-ttu-id="7a7aa-112">判斷使用的安全性機制：可靠的傳訊能力或異動內容流量設定。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-112">Determines the security mechanism being used: either reliable messaging capability or transaction context flow settings.</span></span>  
  
 <span data-ttu-id="7a7aa-113">**編碼方式**</span><span class="sxs-lookup"><span data-stu-id="7a7aa-113">**Encoding**</span></span>  
 <span data-ttu-id="7a7aa-114">判斷訊息的編碼方式 (例如，文字或二進位)。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-114">Determines the message encoding (for example, text or binary).</span></span>  
  
 <span data-ttu-id="7a7aa-115">**傳輸**</span><span class="sxs-lookup"><span data-stu-id="7a7aa-115">**Transport**</span></span>  
 <span data-ttu-id="7a7aa-116">判斷要使用的基礎傳輸通訊協定 (例如，TCP 或 HTTP)。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-116">Determines the underlying transport protocol to use (for example, TCP or HTTP).</span></span>  
  
## <a name="the-elements-of-a-binding"></a><span data-ttu-id="7a7aa-117">繫結項目</span><span class="sxs-lookup"><span data-stu-id="7a7aa-117">The Elements of a Binding</span></span>  

 <span data-ttu-id="7a7aa-118">繫結基本上是由排列順序的繫結項目堆疊所組成，而每個繫結項目都會指定連線至服務端點時所需的部分通訊資訊。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-118">A binding basically consists of an ordered stack of binding elements, each of which specifies part of the communication information required to connect to a service endpoint.</span></span> <span data-ttu-id="7a7aa-119">堆疊中最低的那兩層為必要項。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-119">The two lowest layers in the stack are both required.</span></span> <span data-ttu-id="7a7aa-120">堆疊基底是傳輸繫結項目，而這個項目的正上方是其中含有訊息編碼規格的項目。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-120">At the base of the stack is the transport binding element and just above this is the element that contains the message encoding specifications.</span></span> <span data-ttu-id="7a7aa-121">指定其他通訊協定的選用繫結程序元素則會置於這兩個必要元素之上。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-121">The optional binding elements that specify the other communication protocols are layered above these two required elements.</span></span> <span data-ttu-id="7a7aa-122">如需這些繫結項目及其正確順序的詳細資訊，請參閱 [自訂](./extending/custom-bindings.md)系結。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-122">For more information about these binding elements and their correct ordering, see [Custom Bindings](./extending/custom-bindings.md).</span></span>  
  
## <a name="system-provided-bindings"></a><span data-ttu-id="7a7aa-123">系統提供的繫結</span><span class="sxs-lookup"><span data-stu-id="7a7aa-123">System-Provided Bindings</span></span>  

 <span data-ttu-id="7a7aa-124">繫結中的資訊可能很複雜，而有些設定也可能彼此不相容。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-124">The information in a binding can be complex, and some settings may not be compatible with others.</span></span> <span data-ttu-id="7a7aa-125">基於這個理由，WCF 包含一組系統提供的系結。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-125">For this reason, WCF includes a set of system-provided bindings.</span></span> <span data-ttu-id="7a7aa-126">這些繫結程序設計為滿足大多數應用程式需求。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-126">These bindings are designed to cover most application requirements.</span></span> <span data-ttu-id="7a7aa-127">下列類別則表示系統提供之繫結的一些範例：</span><span class="sxs-lookup"><span data-stu-id="7a7aa-127">The following classes represent some examples of system-provided bindings:</span></span>  
  
- <span data-ttu-id="7a7aa-128"><xref:System.ServiceModel.BasicHttpBinding>：一種 HTTP 通訊協定繫結，可用於連線至 Web 服務，並符合 WS-I Basic Profile 規格 (例如，以 ASP.NET Web 服務為基礎的服務)。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-128"><xref:System.ServiceModel.BasicHttpBinding>: An HTTP protocol binding suitable for connecting to Web services that conforms to the WS-I Basic Profile specification (for example, ASP.NET Web services-based services).</span></span>  
  
- <span data-ttu-id="7a7aa-129"><xref:System.ServiceModel.WSHttpBinding>：一種互通的繫結，可用於連線至符合 WS-\* 通訊協定的端點。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-129"><xref:System.ServiceModel.WSHttpBinding>: An interoperable binding suitable for connecting to endpoints that conform to the WS-\* protocols.</span></span>  
  
- <span data-ttu-id="7a7aa-130"><xref:System.ServiceModel.NetNamedPipeBinding>：使用 .NET Framework 連接到同一部電腦上的其他 WCF 端點。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-130"><xref:System.ServiceModel.NetNamedPipeBinding>: Uses the .NET Framework to connect to other WCF endpoints on the same machine.</span></span>  
  
- <span data-ttu-id="7a7aa-131"><xref:System.ServiceModel.NetMsmqBinding>：使用 .NET Framework 建立與其他 WCF 端點的佇列訊息連接。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-131"><xref:System.ServiceModel.NetMsmqBinding>: Uses the .NET Framework to create queued message connections with other WCF endpoints.</span></span>  

- <span data-ttu-id="7a7aa-132"><xref:System.ServiceModel.NetTcpBinding>：這個系結提供的效能高於 HTTP 系結，而且非常適合用於區域網路。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-132"><xref:System.ServiceModel.NetTcpBinding>: This binding offers higher performance than HTTP bindings and is ideal for use in a local network.</span></span>
  
 <span data-ttu-id="7a7aa-133">如需所有 WCF 提供系結的完整清單和描述，請參閱 [系統提供](system-provided-bindings.md)的系結。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-133">For a complete list, with descriptions, of all the WCF-provided bindings, see [System-Provided Bindings](system-provided-bindings.md).</span></span>  
  
## <a name="using-your-own-bindings"></a><span data-ttu-id="7a7aa-134">使用您自己的繫結</span><span class="sxs-lookup"><span data-stu-id="7a7aa-134">Using Your Own Bindings</span></span>  

 <span data-ttu-id="7a7aa-135">如果所含之系統提供的繫結都沒有服務應用程式需要的正確功能組合，您可以建立自己的繫結。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-135">If none of the system-provided bindings included has the right combination of features that a service application requires, you can create your own binding.</span></span> <span data-ttu-id="7a7aa-136">做法有二種。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-136">There are two ways to do this.</span></span> <span data-ttu-id="7a7aa-137">您可以使用 <xref:System.ServiceModel.Channels.CustomBinding> 物件從已存在的繫結元素中建立新的繫結，或者藉由從 <xref:System.ServiceModel.Channels.Binding> 繫結衍生，而建立完整的使用者定義繫結。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-137">You can either create a new binding from pre-existing binding elements using a <xref:System.ServiceModel.Channels.CustomBinding> object or you can create a completely user-defined binding by deriving from the <xref:System.ServiceModel.Channels.Binding> binding.</span></span> <span data-ttu-id="7a7aa-138">如需使用這兩種方法建立您專屬系結的詳細資訊，請參閱 [自訂](./extending/custom-bindings.md) 系結和 [建立 User-Defined](./extending/creating-user-defined-bindings.md)系結。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-138">For more information about creating your own binding using these two approaches, see [Custom Bindings](./extending/custom-bindings.md) and [Creating User-Defined Bindings](./extending/creating-user-defined-bindings.md).</span></span>  
  
## <a name="using-bindings"></a><span data-ttu-id="7a7aa-139">使用繫結</span><span class="sxs-lookup"><span data-stu-id="7a7aa-139">Using Bindings</span></span>  

 <span data-ttu-id="7a7aa-140">使用繫結牽涉到兩個基本步驟：</span><span class="sxs-lookup"><span data-stu-id="7a7aa-140">Using bindings entails two basic steps:</span></span>  
  
1. <span data-ttu-id="7a7aa-141">選取或定義繫結。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-141">Select or define a binding.</span></span> <span data-ttu-id="7a7aa-142">最簡單的方法是選擇 WCF 所含的其中一個系統提供系結，並使用其預設設定。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-142">The easiest method is to choose one of the system-provided bindings included with WCF and use it with its default settings.</span></span> <span data-ttu-id="7a7aa-143">也可以選擇系統提供的繫結程序，並重設其屬性值以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-143">You can also choose a system-provided binding and reset its property values to suit your requirements.</span></span> <span data-ttu-id="7a7aa-144">此外，您可以建立自訂繫結或使用者定義的繫結，以對這些繫結擁有更高程度的控制權和自訂權。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-144">Alternatively, you can create a custom binding or a user-defined binding to have higher degrees of control and customization.</span></span>  
  
2. <span data-ttu-id="7a7aa-145">建立使用已選取或已定義之繫結的端點。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-145">Create an endpoint that uses the binding selected or defined.</span></span>  
  
## <a name="code-and-configuration"></a><span data-ttu-id="7a7aa-146">程式碼和組態</span><span class="sxs-lookup"><span data-stu-id="7a7aa-146">Code and Configuration</span></span>  

 <span data-ttu-id="7a7aa-147">有兩種方法可讓您定義繫結：透過程示碼或透過組態。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-147">You can define bindings in two ways: through code or through configuration.</span></span> <span data-ttu-id="7a7aa-148">這兩個方法與您是使用系統提供的繫結或自訂繫結無關。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-148">These two approaches do not depend on whether you are using a system-provided binding or a custom binding.</span></span> <span data-ttu-id="7a7aa-149">一般來說，使用程式碼可讓您在設計階段時完全控制繫結的定義。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-149">In general, using code gives you complete control over the definition of a binding at design time.</span></span> <span data-ttu-id="7a7aa-150">另一方面，使用設定可讓 WCF 服務或用戶端的系統管理員或使用者變更系結的參數，而不需要重新編譯服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-150">Using configuration, on the other hand, allows a system administrator or the user of a WCF service or client to change the parameters of a binding without having to recompile the service application.</span></span> <span data-ttu-id="7a7aa-151">這種彈性通常很理想，因為沒有任何方法可以預測要部署 WCF 應用程式的特定電腦需求。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-151">This flexibility is often desirable because there is no way to predict specific machine requirements on which a WCF application is to be deployed.</span></span> <span data-ttu-id="7a7aa-152">將繫結 (和位址) 資訊留在程式碼外面，可在不需要重新編譯或重新部署應用程式的情況下，就可以變更繫結和位址資訊。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-152">Keeping the binding (and the addressing) information out of the code allows them to change without requiring recompilation or redeployment of the application.</span></span> <span data-ttu-id="7a7aa-153">請注意，會先建立在組態中指定繫結，之後才建立在程式碼中定義的繫結，這樣可讓程式碼定義的繫結覆寫任何組態定義的繫結。</span><span class="sxs-lookup"><span data-stu-id="7a7aa-153">Note that bindings defined in code are created after bindings specified in configuration, allowing the code-defined bindings to overwrite any configuration-defined bindings.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="7a7aa-154">另請參閱</span><span class="sxs-lookup"><span data-stu-id="7a7aa-154">See also</span></span>

- [<span data-ttu-id="7a7aa-155">使用繫結來設定服務和用戶端</span><span class="sxs-lookup"><span data-stu-id="7a7aa-155">Using Bindings to Configure Services and Clients</span></span>](using-bindings-to-configure-services-and-clients.md)
