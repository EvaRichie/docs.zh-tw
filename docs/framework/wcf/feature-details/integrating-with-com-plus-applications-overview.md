---
title: 整合 COM+ 應用程式概觀
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Communication Foundation, COM+ integration
- WCF, COM+ integration
ms.assetid: e481e48f-7096-40eb-9f20-7f0098412941
ms.openlocfilehash: 1b9b7e57760c2aba0a8e9eadd53ca8e72529b787
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96248964"
---
# <a name="integrating-with-com-applications-overview"></a><span data-ttu-id="8178c-102">整合 COM+ 應用程式概觀</span><span class="sxs-lookup"><span data-stu-id="8178c-102">Integrating with COM+ Applications Overview</span></span>

<span data-ttu-id="8178c-103">Windows Communication Foundation (WCF) 可提供豐富的環境來建立分散式應用程式。</span><span class="sxs-lookup"><span data-stu-id="8178c-103">Windows Communication Foundation (WCF) provides a rich environment for creating distributed applications.</span></span> <span data-ttu-id="8178c-104">如果您已經使用裝載于 COM + 中的元件架構應用程式邏輯，則可以使用 WCF 來擴充現有的邏輯，而不必重新撰寫它。</span><span class="sxs-lookup"><span data-stu-id="8178c-104">If you are already using component-based application logic hosted in COM+, you can use WCF to extend your existing logic rather than having to rewrite it.</span></span> <span data-ttu-id="8178c-105">一個常見案例就是當您要透過 Web 服務，公開現有的 COM+ 或 Enterprise Services 商務邏輯之時。</span><span class="sxs-lookup"><span data-stu-id="8178c-105">A common scenario is when you want to expose existing COM+ or Enterprise Services business logic through Web Services.</span></span>  
  
 <span data-ttu-id="8178c-106">當 COM+ 元件上的介面公開為 Web 服務時，這些服務的規格和合約就會由在應用程式初始化時所執行的自動對映來決定。</span><span class="sxs-lookup"><span data-stu-id="8178c-106">When an interface on a COM+ component is exposed as a Web service, the specification and contract of these services are determined by an automatic mapping that is performed at application initialization time.</span></span> <span data-ttu-id="8178c-107">下列清單會顯示這個對應的概念模型：</span><span class="sxs-lookup"><span data-stu-id="8178c-107">The following list shows the conceptual model for this mapping:</span></span>  
  
- <span data-ttu-id="8178c-108">對每個公開的 COM 類別定義一個服務。</span><span class="sxs-lookup"><span data-stu-id="8178c-108">One service is defined for each exposed COM class.</span></span>  
  
- <span data-ttu-id="8178c-109">服務的合約是直接衍生自選取之元件的介面定義而得，且組態中可能已定義方法排除。</span><span class="sxs-lookup"><span data-stu-id="8178c-109">The contract for the service is derived directly from the selected component's interface definition with the possibility of method exclusion defined in configuration.</span></span>  
  
- <span data-ttu-id="8178c-110">該合約中的作業直接衍生自元件之介面定義上的方法。</span><span class="sxs-lookup"><span data-stu-id="8178c-110">The operations in that contract are derived directly from the methods on the component's interface definition.</span></span>  
  
- <span data-ttu-id="8178c-111">那些作業的參數則直接衍生自 COM 互通性型別，而此型別會對應至元件的方法參數。</span><span class="sxs-lookup"><span data-stu-id="8178c-111">The parameters for those operations are derived directly from the COM interoperability type that corresponds to the component's method parameters.</span></span>  
  
 <span data-ttu-id="8178c-112">在服務組態檔中提供服務的預設位址和傳輸繫結，不過可依需求重新設定這些項目。</span><span class="sxs-lookup"><span data-stu-id="8178c-112">Default addresses and transport bindings for the service are provided in a service configuration file, but these can be reconfigured as required.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="8178c-113">只要 COM+ 介面和組態保持不變，已公開的 Web 服務合約就會保持不變。</span><span class="sxs-lookup"><span data-stu-id="8178c-113">The contracts for the exposed Web services remain constant as long as the COM+ interfaces and configuration remain unchanged.</span></span> <span data-ttu-id="8178c-114">對有些介面的修改並不會自動更新可用的服務，並且需要重新執行 COM+ 服務模型組態工具 (ComSvcConfig.exe)。</span><span class="sxs-lookup"><span data-stu-id="8178c-114">A modification to several interfaces does not automatically update the available services and requires re-running the COM+ Service Model Configuration tool (ComSvcConfig.exe).</span></span>  
  
 <span data-ttu-id="8178c-115">以 Web 服務使用時，會繼續強制執行 COM+ 應用程式與其元件的驗證和授權需求。</span><span class="sxs-lookup"><span data-stu-id="8178c-115">The authentication and authorization requirements of the COM+ application and its components continue to be enforced when used as a Web service.</span></span>  
  
 <span data-ttu-id="8178c-116">如果呼叫端初始化 Web 服務交易，則標示為可交易的元件就會在該交易範圍內登記。</span><span class="sxs-lookup"><span data-stu-id="8178c-116">If the caller initiates a Web service transaction, components marked as transactional enlist within that transaction scope.</span></span>  
  
 <span data-ttu-id="8178c-117">下列為將 COM+ 元件的介面公開為 Web 服務、而不用修改元件的必要步驟：</span><span class="sxs-lookup"><span data-stu-id="8178c-117">The following steps are required to expose a COM+ component's interface as a Web service without modifying the component:</span></span>  
  
1. <span data-ttu-id="8178c-118">判斷 COM+ 元件的介面是否可以公開為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="8178c-118">Determine whether the COM+ component's interface can be exposed as a Web service.</span></span>  
  
2. <span data-ttu-id="8178c-119">選取適當的裝載模式。</span><span class="sxs-lookup"><span data-stu-id="8178c-119">Select an appropriate hosting mode.</span></span>  
  
3. <span data-ttu-id="8178c-120">使用 COM+ 服務模型組態工具 (ComSvcConfig.exe) 以新增介面的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="8178c-120">Use the COM+ Service Model Configuration tool (ComSvcConfig.exe) to add a Web service for the interface.</span></span> <span data-ttu-id="8178c-121">如需如何使用 ComSvcConfig.exe 的詳細資訊，請參閱 [如何：使用 COM + 服務模型設定工具](how-to-use-the-com-service-model-configuration-tool.md)。</span><span class="sxs-lookup"><span data-stu-id="8178c-121">For more information about how to use ComSvcConfig.exe, see [How to: Use the COM+ Service Model Configuration Tool](how-to-use-the-com-service-model-configuration-tool.md).</span></span>  
  
4. <span data-ttu-id="8178c-122">在應用程式組態檔中進行其他服務設定。</span><span class="sxs-lookup"><span data-stu-id="8178c-122">Configure any additional service settings in the application configuration file.</span></span> <span data-ttu-id="8178c-123">如需如何設定元件的詳細資訊，請參閱 [如何：設定 COM + 服務設定](how-to-configure-com-service-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="8178c-123">For more information about how to configure a component, see [How to: Configure COM+ Service Settings](how-to-configure-com-service-settings.md).</span></span>  
  
## <a name="supported-interfaces"></a><span data-ttu-id="8178c-124">支援的介面</span><span class="sxs-lookup"><span data-stu-id="8178c-124">Supported Interfaces</span></span>  

 <span data-ttu-id="8178c-125">對於可公開為 Web 服務之介面的型別，有一些限制存在。</span><span class="sxs-lookup"><span data-stu-id="8178c-125">There are some restrictions on the type of interfaces that can be exposed as a Web service.</span></span> <span data-ttu-id="8178c-126">不支援下列介面型別：</span><span class="sxs-lookup"><span data-stu-id="8178c-126">The following types of interfaces are not supported:</span></span>  
  
- <span data-ttu-id="8178c-127">將物件參考做為參數進行傳遞的介面：將會在＜限制的物件參考支援＞這一節描述下列限制的物件參考方法。</span><span class="sxs-lookup"><span data-stu-id="8178c-127">Interfaces that pass object references as parameters - the following limited object reference approach is described in the Limited Object Reference Support section.</span></span>  
  
- <span data-ttu-id="8178c-128">傳遞與 .NET Framework COM 互通性轉換不相容之類型的介面。</span><span class="sxs-lookup"><span data-stu-id="8178c-128">Interfaces that pass types that are not compatible with the .NET Framework COM interoperability conversions.</span></span>  
  
- <span data-ttu-id="8178c-129">應用程式的介面，該介面由 COM+ 裝載時，會啟用應用程式共用。</span><span class="sxs-lookup"><span data-stu-id="8178c-129">Interfaces for applications that have application pooling enabled when hosted by COM+.</span></span>  
  
- <span data-ttu-id="8178c-130">元件的介面，這些介面已對應用程式標示為私用。</span><span class="sxs-lookup"><span data-stu-id="8178c-130">Interfaces of components that are marked as private to the application.</span></span>  
  
- <span data-ttu-id="8178c-131">COM+ 基礎結構介面。</span><span class="sxs-lookup"><span data-stu-id="8178c-131">COM+ infrastructure interfaces.</span></span>  
  
- <span data-ttu-id="8178c-132">來自系統應用程式的介面。</span><span class="sxs-lookup"><span data-stu-id="8178c-132">Interfaces from the system application.</span></span>  
  
- <span data-ttu-id="8178c-133">來自 Enterprise Services 元件的介面，這些元件尚未加入至全域組件快取。</span><span class="sxs-lookup"><span data-stu-id="8178c-133">Interfaces from Enterprise Services components that have not been added to the global assembly cache.</span></span>  
  
### <a name="limited-object-reference-support"></a><span data-ttu-id="8178c-134">限制的物件參考支援</span><span class="sxs-lookup"><span data-stu-id="8178c-134">Limited Object Reference Support</span></span>  

 <span data-ttu-id="8178c-135">由於一些已部署的 COM+ 元件確實會依參考參數而使用物件 (例如，傳回 ADO 資料錄集 (Recordset) 物件)，因此 COM+ 整合中就包括物件參考參數的限制支援。</span><span class="sxs-lookup"><span data-stu-id="8178c-135">Because a number of deployed COM+ components do use objects by reference parameters, such as returning an ADO Recordset object, COM+ integration includes limited support for object reference parameters.</span></span> <span data-ttu-id="8178c-136">支援會受限於實作 `IPersistStream` COM 介面的物件。</span><span class="sxs-lookup"><span data-stu-id="8178c-136">The support is limited to objects that implement the `IPersistStream` COM interface.</span></span> <span data-ttu-id="8178c-137">其中包括 ADO 資料錄集物件，並且可針對特定於應用程式的 COM 物件來實作。</span><span class="sxs-lookup"><span data-stu-id="8178c-137">This includes ADO Recordset objects and can be implemented for application specific COM objects.</span></span>  
  
 <span data-ttu-id="8178c-138">為了啟用此支援，ComSvcConfig.exe 工具會提供停用一般方法簽章參數的 **allowreferences** 參數，並檢查工具是否執行，以確保不會使用物件參考參數。</span><span class="sxs-lookup"><span data-stu-id="8178c-138">To enable this support, the ComSvcConfig.exe tool provides the **allowreferences** switch that disables the regular method signature parameter and checks that the tool runs to ensure that object reference parameters are not being used.</span></span> <span data-ttu-id="8178c-139">此外，您以參數傳遞的物件型別必須在 <`persistableTypes`> 設定元素（<> 專案的子系）中命名和識別 `comContract` 。</span><span class="sxs-lookup"><span data-stu-id="8178c-139">In addition, the object types that you pass as parameters must be named and identified within the <`persistableTypes`> configuration element that is a child of the <`comContract`> element.</span></span>  
  
 <span data-ttu-id="8178c-140">使用這個功能時，COM+ 整合服務會使用 `IPersistStream` 介面來序列化或還原序列化物件執行個體。</span><span class="sxs-lookup"><span data-stu-id="8178c-140">When this feature is used, the COM+ integration service uses the `IPersistStream` interface to serialize or deserialize the object instance.</span></span> <span data-ttu-id="8178c-141">如果物件執行個體不支援 `IPersistStream`，就會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="8178c-141">If the object instance does not support `IPersistStream`, an exception is thrown.</span></span>  
  
 <span data-ttu-id="8178c-142">在用戶端應用程式中，您可以使用 <xref:System.ServiceModel.ComIntegration.PersistStreamTypeWrapper> 物件上的方法，將物件傳遞至服務並以類似方法接收物件。</span><span class="sxs-lookup"><span data-stu-id="8178c-142">Within a client application, the methods on the <xref:System.ServiceModel.ComIntegration.PersistStreamTypeWrapper> object can be used to pass an object in to a service and similarly to retrieve an object.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="8178c-143">由於序列化方法的自訂和平臺特定的本質，因此最適合用於 WCF 用戶端與 WCF 服務。</span><span class="sxs-lookup"><span data-stu-id="8178c-143">Due to the custom and platform-specific nature of the serialization approach, this is best suited for use between WCF clients and WCF services.</span></span>  
  
## <a name="selecting-the-hosting-mode"></a><span data-ttu-id="8178c-144">選取主控模式</span><span class="sxs-lookup"><span data-stu-id="8178c-144">Selecting the Hosting Mode</span></span>  

 <span data-ttu-id="8178c-145">COM+ 會以下列其中一個主控模式公開 Web 服務：</span><span class="sxs-lookup"><span data-stu-id="8178c-145">COM+ exposes Web services in one of the following hosting modes:</span></span>  
  
- <span data-ttu-id="8178c-146">COM+ 主控</span><span class="sxs-lookup"><span data-stu-id="8178c-146">COM+-hosted</span></span>  
  
     <span data-ttu-id="8178c-147">會在應用程式的專用 COM+ 伺服器處理序 (Dllhost.exe) 內主控 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="8178c-147">The Web service is hosted within the application's dedicated COM+ server process (Dllhost.exe).</span></span> <span data-ttu-id="8178c-148">使用這個模式時，需要先明確的啟動應用程式，它才可以接收 Web 服務要求。</span><span class="sxs-lookup"><span data-stu-id="8178c-148">This mode requires the application to be explicitly started before it can receive Web service requests.</span></span> <span data-ttu-id="8178c-149">可以使用 COM+ [以 NT 服務執行] 或 [當閒置時仍繼續執行] 選項，防止應用程式與其服務因閒置而導致關機。</span><span class="sxs-lookup"><span data-stu-id="8178c-149">The COM+ options "Run as an NT Service" or "Leave running when idle" can be used to prevent idle shutdown of the application and its services.</span></span> <span data-ttu-id="8178c-150">這個模式會對伺服器應用程式提供 Web 服務和 DCOM 存取。</span><span class="sxs-lookup"><span data-stu-id="8178c-150">This mode provides both Web service and DCOM access to the server application.</span></span>  
  
- <span data-ttu-id="8178c-151">Web 主控</span><span class="sxs-lookup"><span data-stu-id="8178c-151">Web-hosted</span></span>  
  
     <span data-ttu-id="8178c-152">Web 服務會在 Web 伺服器工作處理序內主控。</span><span class="sxs-lookup"><span data-stu-id="8178c-152">The Web service is hosted within a Web server worker process.</span></span> <span data-ttu-id="8178c-153">這個模式在接收初始化要求時，不需要使用 COM+。</span><span class="sxs-lookup"><span data-stu-id="8178c-153">This mode does not require COM+ to be active when the initial request is received.</span></span> <span data-ttu-id="8178c-154">如果收到這個要求時應用程式不在使用中，會在處理要求之前自動啟動該應用程式。</span><span class="sxs-lookup"><span data-stu-id="8178c-154">If the application is not active when this request is received, it is automatically activated prior to processing the request.</span></span> <span data-ttu-id="8178c-155">這個模式也會對伺服器應用程式提供 Web 服務和 DCOM 存取，但會對 Web 服務要求造成處理序躍點。</span><span class="sxs-lookup"><span data-stu-id="8178c-155">This mode also provides both Web service and DCOM access to the server application, but causes a process hop for Web service requests.</span></span> <span data-ttu-id="8178c-156">通常會需要用戶端啟用模擬。</span><span class="sxs-lookup"><span data-stu-id="8178c-156">This typically requires the client to enable impersonation.</span></span> <span data-ttu-id="8178c-157">在 WCF 中，這可以透過類別的屬性來完成，該 <xref:System.ServiceModel.Security.WindowsClientCredential.AllowedImpersonationLevel%2A> <xref:System.ServiceModel.Security.WindowsClientCredential> 類別是以泛型類別的屬性來存取 <xref:System.ServiceModel.ChannelFactory%601> ，也可以是 <xref:System.Security.Principal.TokenImpersonationLevel.Impersonation> 列舉值。</span><span class="sxs-lookup"><span data-stu-id="8178c-157">In WCF, this can be done with the <xref:System.ServiceModel.Security.WindowsClientCredential.AllowedImpersonationLevel%2A> property of the <xref:System.ServiceModel.Security.WindowsClientCredential> class, which is accessed as a property of the generic <xref:System.ServiceModel.ChannelFactory%601> class, as well as the <xref:System.Security.Principal.TokenImpersonationLevel.Impersonation> enumeration value.</span></span>  
  
- <span data-ttu-id="8178c-158">Web 主控同處理序</span><span class="sxs-lookup"><span data-stu-id="8178c-158">Web-hosted in-process</span></span>  
  
     <span data-ttu-id="8178c-159">會在 Web 伺服器工作處理序內主控 Web 服務和 COM+ 應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="8178c-159">The Web service and the COM+ application logic are hosted within the Web server worker process.</span></span> <span data-ttu-id="8178c-160">如此可自動啟動 Web 主控模式，而不會對 Web 服務要求造成處理序躍點。</span><span class="sxs-lookup"><span data-stu-id="8178c-160">This provides automatic activation of the Web-hosted mode without causing a process hop for Web service requests.</span></span> <span data-ttu-id="8178c-161">缺點則為無法透過 DCOM 存取伺服器應用程式。</span><span class="sxs-lookup"><span data-stu-id="8178c-161">The disadvantage is that the server application cannot be accessed through DCOM.</span></span>  
  
### <a name="security-considerations"></a><span data-ttu-id="8178c-162">安全性考量</span><span class="sxs-lookup"><span data-stu-id="8178c-162">Security Considerations</span></span>  

 <span data-ttu-id="8178c-163">就像其他 WCF 服務一樣，公開服務的安全性設定也是透過 WCF 通道的設定來管理。</span><span class="sxs-lookup"><span data-stu-id="8178c-163">Like other WCF services, the security settings for the exposed service are administered through configuration settings for the WCF channel.</span></span> <span data-ttu-id="8178c-164">但不會強制執行傳統 DCOM 安全性設定，例如 DCOM 全機器的權限設定。</span><span class="sxs-lookup"><span data-stu-id="8178c-164">Traditional DCOM security settings such as the DCOM machine-wide permissions settings are not enforced.</span></span> <span data-ttu-id="8178c-165">若要強制執行 COM+ 應用程式角色，則必須對元件啟用「元件層級存取檢查」授權。</span><span class="sxs-lookup"><span data-stu-id="8178c-165">To enforce COM+ application roles, "component-level access checks" authorization must be enabled for the component.</span></span>  
  
 <span data-ttu-id="8178c-166">使用未受保護的繫結時，通訊就會因開放而遭到竄改或導致資訊洩漏。</span><span class="sxs-lookup"><span data-stu-id="8178c-166">The use of a non-secured binding can leave communication open to tampering or information disclosure.</span></span> <span data-ttu-id="8178c-167">若要避免發生這個情況，建議您使用受到保護的繫結。</span><span class="sxs-lookup"><span data-stu-id="8178c-167">To prevent this, it is recommended that you use a secured binding.</span></span>  
  
 <span data-ttu-id="8178c-168">針對 COM+ 主控和 Web 主控的模式，用戶端應用程式必須讓伺服器處理序可模擬用戶端使用者。</span><span class="sxs-lookup"><span data-stu-id="8178c-168">For the COM+-hosted and Web-hosted modes, client applications must permit the server process to impersonate the client user.</span></span> <span data-ttu-id="8178c-169">您可以藉由將模擬等級設定為，在 WCF 用戶端中完成這項操作 <xref:System.Security.Principal.TokenImpersonationLevel.Impersonation> 。</span><span class="sxs-lookup"><span data-stu-id="8178c-169">This can be done in WCF clients by setting the impersonation level to <xref:System.Security.Principal.TokenImpersonationLevel.Impersonation>.</span></span>  
  
 <span data-ttu-id="8178c-170">使用 Internet Information Services (IIS) 或 Windows Process Activation Service (WAS) 搭配 HTTP 傳輸時，就可以使用 Httpcfg.exe 工具來保留傳輸端點位址。</span><span class="sxs-lookup"><span data-stu-id="8178c-170">With Internet Information Services (IIS) or Windows Process Activation Service (WAS) using the HTTP transport, the Httpcfg.exe tool can be used to reserve a transport endpoint address.</span></span> <span data-ttu-id="8178c-171">在其他組態中，保護不受充當為預期服務之惡意服務的攻擊可說是相當重要。</span><span class="sxs-lookup"><span data-stu-id="8178c-171">In other configurations, it is important to protect against rogue services that act as the intended service.</span></span> <span data-ttu-id="8178c-172">若要防止在目的端點上啟動惡意服務，可以將合法的服務設定為以 NT 服務來執行。</span><span class="sxs-lookup"><span data-stu-id="8178c-172">To prevent a rogue service from starting at the desired endpoint, the legitimate service can be configured to run as an NT service.</span></span> <span data-ttu-id="8178c-173">這樣可讓合法服務在任何惡意服務之前，先宣告端點位址。</span><span class="sxs-lookup"><span data-stu-id="8178c-173">This enables the legitimate service to claim the endpoint address prior to any rogue services.</span></span>  
  
 <span data-ttu-id="8178c-174">使用已設定的 COM + 角色作為 Web 裝載服務來公開 COM + 應用程式時，必須將「啟動 IIS 進程帳戶」新增至其中一個應用程式的角色。</span><span class="sxs-lookup"><span data-stu-id="8178c-174">When exposing a COM+ application with configured COM+ roles as a Web-hosted service, the "Launch IIS Process Account" must be added to one of the application’s roles.</span></span> <span data-ttu-id="8178c-175">必須新增這個帳戶 (其名稱通常為 IWAM_machinename)，才能在使用之後讓物件正常關機。</span><span class="sxs-lookup"><span data-stu-id="8178c-175">This account, typically with the name IWAM_machinename, must be added to enable clean shutdown of objects after use.</span></span> <span data-ttu-id="8178c-176">這個帳戶不應該授與任何其他的權限。</span><span class="sxs-lookup"><span data-stu-id="8178c-176">The account should not be granted any additional permissions.</span></span>  
  
 <span data-ttu-id="8178c-177">在整合應用程式上無法使用 COM+ 處理序回收功能。</span><span class="sxs-lookup"><span data-stu-id="8178c-177">The COM+ process recycling features cannot be used on integrated applications.</span></span> <span data-ttu-id="8178c-178">如果應用程式是設定為使用處理序回收，而且是在 COM+ 主控的處理序中執行元件，將無法啟動服務。</span><span class="sxs-lookup"><span data-stu-id="8178c-178">If the application is configured to use process recycling and the components are running in a COM+ hosted process, the service fails to start.</span></span> <span data-ttu-id="8178c-179">這項需求不包括使用 Web 主控同處理序模式的服務，因為這個服務中未套用處理序回收設定。</span><span class="sxs-lookup"><span data-stu-id="8178c-179">This requirement does not include services using the Web-hosted in-process mode because the process recycling settings are not applied.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8178c-180">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8178c-180">See also</span></span>

- [<span data-ttu-id="8178c-181">整合 COM 應用程式概觀</span><span class="sxs-lookup"><span data-stu-id="8178c-181">Integrating with COM Applications Overview</span></span>](integrating-with-com-applications-overview.md)
