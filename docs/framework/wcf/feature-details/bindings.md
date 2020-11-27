---
title: Windows Communication Foundation 繫結
ms.date: 03/30/2017
helpviewer_keywords:
- WCF [WCF], bindings
- Windows Communication Foundation [WCF], bindings
- bindings [WCF]
ms.assetid: 83639133-89f7-43f0-b4ef-8d9e57c08d25
ms.openlocfilehash: 50c430489144589f6deb0930aeb3006bcb7efe8c
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96262095"
---
# <a name="windows-communication-foundation-bindings"></a><span data-ttu-id="3ec27-102">Windows Communication Foundation 繫結</span><span class="sxs-lookup"><span data-stu-id="3ec27-102">Windows Communication Foundation Bindings</span></span>

<span data-ttu-id="3ec27-103">Windows Communication Foundation (WCF) 讓應用程式的軟體與其他軟體的通訊方式分開。</span><span class="sxs-lookup"><span data-stu-id="3ec27-103">Windows Communication Foundation (WCF) separates how the software for an application is written from how it communicates with other software.</span></span> <span data-ttu-id="3ec27-104">繫結可用來指定必要的傳輸、編碼與通訊協定詳細資料，以供用戶端與服務彼此通訊。</span><span class="sxs-lookup"><span data-stu-id="3ec27-104">Bindings are used to specify the transport, encoding, and protocol details required for clients and services to communicate with each other.</span></span> <span data-ttu-id="3ec27-105">WCF 會使用系結來產生端點的基礎線路標記法，因此大部分的系結詳細資料都必須由通訊的合作物件來同意。</span><span class="sxs-lookup"><span data-stu-id="3ec27-105">WCF uses bindings to generate the underlying wire representation of the endpoint, so most of the binding details must be agreed upon by the parties that are communicating.</span></span> <span data-ttu-id="3ec27-106">要達到這個目的之最簡單方式，就是讓服務用戶端使用服務端點所使用的相同繫結。</span><span class="sxs-lookup"><span data-stu-id="3ec27-106">The easiest way to achieve this is for clients of a service to use the same binding that the endpoint for the service uses.</span></span> <span data-ttu-id="3ec27-107">如需如何進行此作業的詳細資訊，請參閱使用系結 [來設定服務和用戶端](../using-bindings-to-configure-services-and-clients.md)。</span><span class="sxs-lookup"><span data-stu-id="3ec27-107">For more information about how to do this, see [Using Bindings to Configure Services and Clients](../using-bindings-to-configure-services-and-clients.md).</span></span>  
  
 <span data-ttu-id="3ec27-108">繫結是由繫結項目集合所組成。</span><span class="sxs-lookup"><span data-stu-id="3ec27-108">A binding is made up of a collection of binding elements.</span></span> <span data-ttu-id="3ec27-109">每個項目負責針對端點與用戶端通訊的方式稍加描述。</span><span class="sxs-lookup"><span data-stu-id="3ec27-109">Each element describes some aspect of how the endpoint communicates with clients.</span></span> <span data-ttu-id="3ec27-110">繫結必須包含至少一個傳輸繫結項目、一個訊息編碼繫結項目 (根據預設，可由傳輸繫結項目來提供)，以及任意數量的其他通訊協定繫結項目。</span><span class="sxs-lookup"><span data-stu-id="3ec27-110">A binding must include at least one transport binding element, at least one message-encoding binding element (which the transport binding element can provide by default), and any number of other protocol binding elements.</span></span> <span data-ttu-id="3ec27-111">由此描述來建立執行階段的處理序，可讓每個繫結項目將程式碼撰寫到該執行階段中。</span><span class="sxs-lookup"><span data-stu-id="3ec27-111">The process that builds a runtime out of this description allows each binding element to contribute code to that runtime.</span></span>  
  
 <span data-ttu-id="3ec27-112">WCF 提供的系結包含了繫結項目的一般選擇。</span><span class="sxs-lookup"><span data-stu-id="3ec27-112">WCF provides bindings that contain common selections of binding elements.</span></span> <span data-ttu-id="3ec27-113">您可以搭配預設設定來使用它們，或是根據使用者需求來修改這些預設值。</span><span class="sxs-lookup"><span data-stu-id="3ec27-113">These can be used with their default settings or you can modify those default values according to user requirements.</span></span> <span data-ttu-id="3ec27-114">這些系統提供的繫結所包含的屬性可讓您直接控制繫結項目與其設定。</span><span class="sxs-lookup"><span data-stu-id="3ec27-114">These system-provided bindings have properties that allow direct control over the binding elements and their settings.</span></span> <span data-ttu-id="3ec27-115">您也可以輕鬆地同時使用多個版本的繫結，只需為每個繫結版本提供屬於自己的名稱即可。</span><span class="sxs-lookup"><span data-stu-id="3ec27-115">You can also easily work side-by-side with multiple versions of a binding by giving each version of the binding its own name.</span></span> <span data-ttu-id="3ec27-116">如需詳細資訊，請參閱設定 [System-Provided](configuring-system-provided-bindings.md)系結。</span><span class="sxs-lookup"><span data-stu-id="3ec27-116">For details, see [Configuring System-Provided Bindings](configuring-system-provided-bindings.md).</span></span>  
  
 <span data-ttu-id="3ec27-117">如果您需要繫結項目的集合 (尚未由這些系統提供繫結之任意繫結所提供)，可以建立包含所需繫結項目集合的自訂繫結。</span><span class="sxs-lookup"><span data-stu-id="3ec27-117">If you need a collection of binding elements not provided by one of these system-provided bindings, you can create a custom binding that consists of the collection of binding elements required.</span></span> <span data-ttu-id="3ec27-118">這些自訂繫結很容易建立，而且不需要新的類別，但是它們無法提供屬性讓您控制繫結項目或其設定。</span><span class="sxs-lookup"><span data-stu-id="3ec27-118">These custom bindings are easy to create and do not require a new class, but they do not provide properties for controlling the binding elements or their settings.</span></span> <span data-ttu-id="3ec27-119">您可以存取繫結項目並透過包含這些繫結項目的集合來修改其設定。</span><span class="sxs-lookup"><span data-stu-id="3ec27-119">You can access the binding elements and modify their settings through the collection that contains them.</span></span> <span data-ttu-id="3ec27-120">如需詳細資訊，請參閱 [自訂](../extending/custom-bindings.md)系結。</span><span class="sxs-lookup"><span data-stu-id="3ec27-120">For details, see [Custom Bindings](../extending/custom-bindings.md).</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="3ec27-121">本節內容</span><span class="sxs-lookup"><span data-stu-id="3ec27-121">In This Section</span></span>  

 [<span data-ttu-id="3ec27-122">設定系統提供的繫結</span><span class="sxs-lookup"><span data-stu-id="3ec27-122">Configuring System-Provided Bindings</span></span>](configuring-system-provided-bindings.md)  
 <span data-ttu-id="3ec27-123">說明如何使用和修改 WCF 提供來支援一般案例的系結。</span><span class="sxs-lookup"><span data-stu-id="3ec27-123">Describes how to use and modify the bindings that WCF provides to support common scenarios.</span></span>  
  
 [<span data-ttu-id="3ec27-124">使用繫結來設定服務和用戶端</span><span class="sxs-lookup"><span data-stu-id="3ec27-124">Using Bindings to Configure Services and Clients</span></span>](../using-bindings-to-configure-services-and-clients.md)  
 <span data-ttu-id="3ec27-125">描述如何在程式碼中，以宣告方式使用設定來定義服務和用戶端 Windows Communication Foundation (WCF) 系結。</span><span class="sxs-lookup"><span data-stu-id="3ec27-125">Describes how to define Windows Communication Foundation (WCF) bindings for services and clients imperatively in code and declaratively using configuration.</span></span>  
  
 [<span data-ttu-id="3ec27-126">自訂繫結</span><span class="sxs-lookup"><span data-stu-id="3ec27-126">Custom Bindings</span></span>](../extending/custom-bindings.md)  
 <span data-ttu-id="3ec27-127">說明何謂 <xref:System.ServiceModel.Channels.CustomBinding> 與其使用時機。</span><span class="sxs-lookup"><span data-stu-id="3ec27-127">Describes what a <xref:System.ServiceModel.Channels.CustomBinding> is and when it is used.</span></span>  
  
## <a name="reference"></a><span data-ttu-id="3ec27-128">參考</span><span class="sxs-lookup"><span data-stu-id="3ec27-128">Reference</span></span>  

 <xref:System.ServiceModel.Channels.Binding>  
  
 <xref:System.ServiceModel.Channels.BindingElement>  
  
 <xref:System.ServiceModel.Channels.CustomBinding>  
  
## <a name="related-sections"></a><span data-ttu-id="3ec27-129">相關章節</span><span class="sxs-lookup"><span data-stu-id="3ec27-129">Related Sections</span></span>  

 [<span data-ttu-id="3ec27-130">擴充繫結</span><span class="sxs-lookup"><span data-stu-id="3ec27-130">Extending Bindings</span></span>](../extending/extending-bindings.md)
