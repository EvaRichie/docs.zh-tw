---
title: WCF 疑難排解快速入門
ms.date: 03/30/2017
helpviewer_keywords:
- WCF [WCF], troubleshooting
- Windows Communication Foundation [WCF], troubleshooting
ms.assetid: a9ea7a53-f31a-46eb-806e-898e465a4992
ms.openlocfilehash: 7df178334ca3ef5b901e3e82bf39592434ee059e
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96279723"
---
# <a name="wcf-troubleshooting-quickstart"></a><span data-ttu-id="d5ca8-102">WCF 疑難排解快速入門</span><span class="sxs-lookup"><span data-stu-id="d5ca8-102">WCF Troubleshooting Quickstart</span></span>

<span data-ttu-id="d5ca8-103">本主題列出客戶在開發 WCF 用戶端和服務時會碰到的幾個已知問題。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-103">This topic lists a number of known issues customers have run into while developing WCF clients and services.</span></span> <span data-ttu-id="d5ca8-104">如果您遇到的問題不在此清單中，建議您為您的服務設定追蹤。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-104">If the issue you are running into is not in this list, we recommend you configure tracing for your service.</span></span> <span data-ttu-id="d5ca8-105">這會產生一個追蹤檔案，您可以使用追蹤檔案檢視器檢視這個檔案，並取得服務中可能會發生之例外狀況的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-105">This will generate a trace file that you can view with the trace file viewer and get detailed information about exceptions that may be occurring within the service.</span></span> <span data-ttu-id="d5ca8-106">如需設定追蹤的詳細資訊，請參閱： [Configuring Tracing](./diagnostics/tracing/configuring-tracing.md)。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-106">For more information on configuring tracing, see: [Configuring Tracing](./diagnostics/tracing/configuring-tracing.md).</span></span> <span data-ttu-id="d5ca8-107">如需追蹤檔案檢視器的詳細資訊，請參閱： [Service Trace Viewer Tool (SvcTraceViewer.exe)](service-trace-viewer-tool-svctraceviewer-exe.md)。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-107">For more information on the trace file viewer, see: [Service Trace Viewer Tool (SvcTraceViewer.exe)](service-trace-viewer-tool-svctraceviewer-exe.md).</span></span>  
  
1. [<span data-ttu-id="d5ca8-108">在安裝 Windows 7 和 IIS 後，如果嘗試瀏覽至 WCF 服務，我會收到下列錯誤訊息：HTTP 錯誤 404.3 - 找不到。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-108">After installing Windows 7 and IIS, when I attempt to browse to a WCF service I get the following error message: HTTP Error 404.3 – Not Found</span></span>](#bkmk_0)  
  
     <span data-ttu-id="d5ca8-109">HTTP 錯誤 404.3 – 找不到。由於延伸組態的緣故，無法提供您要求的網頁。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-109">HTTP Error 404.3 – Not FoundThe page you are requesting cannot be served because of the extension configuration.</span></span> <span data-ttu-id="d5ca8-110">若網頁是指令碼，請加入處理常式。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-110">If the page is a script, add a handler.</span></span> <span data-ttu-id="d5ca8-111">如應下載檔案，請加入 MIME 對應。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-111">If the file should be downloaded, add a MIME map.</span></span> <span data-ttu-id="d5ca8-112">詳細的錯誤 InformationModule StaticFileModule。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-112">Detailed Error InformationModule StaticFileModule.</span></span>  
  
2. [<span data-ttu-id="d5ca8-113">如果我的用戶端在第一個要求之後閒置一段時間，則有時會在第二個要求收到 MessageSecurityException。發生了什麼事情？</span><span class="sxs-lookup"><span data-stu-id="d5ca8-113">Sometimes I receive a MessageSecurityException on the second request if my client is idle for a while after the first request. What is happening?</span></span>](#BKMK_q1)  
  
3. [<span data-ttu-id="d5ca8-114">我的服務會在大約10個用戶端與其互動之後，開始拒絕新的用戶端。發生了什麼事情？</span><span class="sxs-lookup"><span data-stu-id="d5ca8-114">My service starts to reject new clients after about 10 clients are interacting with it. What is happening?</span></span>](#BKMK_q2)  
  
4. [<span data-ttu-id="d5ca8-115">我可以從 WCF 應用程式的組態檔以外的地方載入我的服務組態嗎？</span><span class="sxs-lookup"><span data-stu-id="d5ca8-115">Can I load my service configuration from somewhere other than the WCF application’s configuration file?</span></span>](#BKMK_q3)  
  
5. [<span data-ttu-id="d5ca8-116">我的服務和用戶端運作良好，但是當用戶端在另一台電腦上時，我無法讓它們正常運作嗎？發生了什麼事情？</span><span class="sxs-lookup"><span data-stu-id="d5ca8-116">My service and client work great, but I can’t get them to work when the client is on another computer? What’s happening?</span></span>](#BKMK_q4)  
  
6. [<span data-ttu-id="d5ca8-117">當我擲回類型為例外狀況的 FaultException 時 \<Exception> ，我一律會在用戶端上收到一般 FaultException 類型，而不是在泛型型別上。發生了什麼事情？</span><span class="sxs-lookup"><span data-stu-id="d5ca8-117">When I throw a FaultException\<Exception> where the type is an exception, I always receive a general FaultException type on the client and not the generic type. What’s happening?</span></span>](#BKMK_q5)  
  
7. [<span data-ttu-id="d5ca8-118">當回復未包含任何資料時，看起來像單向和要求-回復作業會以大致相同的速度傳回。發生了什麼事情？</span><span class="sxs-lookup"><span data-stu-id="d5ca8-118">It seems like one-way and request-reply operations return at roughly the same speed when the reply contains no data. What's happening?</span></span>](#BKMK_q6)  
  
8. [<span data-ttu-id="d5ca8-119">我使用的是 x.509 憑證與我的服務，並取得 System.security.cryptography.cryptographicexception 的安全密碼。發生了什麼事情？</span><span class="sxs-lookup"><span data-stu-id="d5ca8-119">I’m using an X.509 certificate with my service and I get a System.Security.Cryptography.CryptographicException. What’s happening?</span></span>](#BKMK_q77)  
  
9. [<span data-ttu-id="d5ca8-120">我將作業的第一個參數從大寫變更為小寫;現在我的用戶端擲回例外狀況。發生了什麼事情？</span><span class="sxs-lookup"><span data-stu-id="d5ca8-120">I changed the first parameter of an operation from uppercase to lowercase; now my client throws an exception. What's happening?</span></span>](#BKMK_q88)  
  
10. [<span data-ttu-id="d5ca8-121">我正在使用我的其中一種追蹤工具，而我得到 EndpointNotFoundException。發生了什麼事情？</span><span class="sxs-lookup"><span data-stu-id="d5ca8-121">I’m using one of my tracing tools and I get an EndpointNotFoundException. What’s happening?</span></span>](#BKMK_q99)  
  
11. [<span data-ttu-id="d5ca8-122">從 WCF SOAP 應用程式呼叫 WCF Web HTTP 應用程式時，服務傳回下列錯誤：405 不允許的方法。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-122">When calling a WCF Web HTTP application from a WCF SOAP application the service returns the following error: 405 Method Not Allowed</span></span>](#BK_MK99)  
  
 [<span data-ttu-id="d5ca8-123">基本位址是什麼？它與端點位址有何關聯？</span><span class="sxs-lookup"><span data-stu-id="d5ca8-123">What is the base address? How does it relate to an endpoint address?</span></span>](#BKMK_q10)  
  
<a name="bkmk_0"></a>

## <a name="after-installing-windows-7-and-iis-when-i-attempt-to-browse-to-a-wcf-service-i-get-the-following-error-message-http-error-4043--not-found"></a><span data-ttu-id="d5ca8-124">在安裝 Windows 7 和 IIS 後，如果嘗試瀏覽至 WCF 服務，我會收到下列錯誤訊息：HTTP 錯誤 404.3 - 找不到。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-124">After installing Windows 7 and IIS, when I attempt to browse to a WCF service I get the following error message: HTTP Error 404.3 – Not Found</span></span>  

 <span data-ttu-id="d5ca8-125">完整的錯誤訊息是：</span><span class="sxs-lookup"><span data-stu-id="d5ca8-125">The full error message is:</span></span>  
  
 <span data-ttu-id="d5ca8-126">HTTP 錯誤 404.3 – 找不到。由於延伸組態的緣故，無法提供您要求的網頁。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-126">HTTP Error 404.3 – Not FoundThe page you are requesting cannot be served because of the extension configuration.</span></span> <span data-ttu-id="d5ca8-127">若網頁是指令碼，請加入處理常式。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-127">If the page is a script, add a handler.</span></span> <span data-ttu-id="d5ca8-128">如應下載檔案，請加入 MIME 對應。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-128">If the file should be downloaded, add a MIME map.</span></span> <span data-ttu-id="d5ca8-129">詳細的錯誤 InformationModule StaticFileModule。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-129">Detailed Error InformationModule StaticFileModule.</span></span>  
  
 <span data-ttu-id="d5ca8-130">當主控台未明確設定「Windows Communication Foundation HTTP 啟動」時，就會出現此錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-130">This error message occurs when "Windows Communication Foundation HTTP Activation" is not explicitly set in the Control Panel.</span></span> <span data-ttu-id="d5ca8-131">若要設定此項，請移至主控台，按一下視窗左下角的 [程式]。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-131">To set this go to the Control Panel, click Programs in the lower left-hand corner of the window.</span></span> <span data-ttu-id="d5ca8-132">按一下 [開啟或關閉 Windows 功能]。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-132">Click Turn Windows features on or off.</span></span> <span data-ttu-id="d5ca8-133">展開 [Microsoft .NET Framework 3.5.1]，並選取 [Windows Communication Foundation Http 啟動]。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-133">Expand Microsoft .NET Framework 3.5.1 and select Windows Communication Foundation HTTP Activation.</span></span>  
  
<a name="BKMK_q1"></a>

## <a name="sometimes-i-receive-a-messagesecurityexception-on-the-second-request-if-my-client-is-idle-for-a-while-after-the-first-request-what-is-happening"></a><span data-ttu-id="d5ca8-134">如果我的用戶端在第一個要求之後閒置一陣子，有時我會在第二個要求收到 MessageSecurityException。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-134">Sometimes I receive a MessageSecurityException on the second request if my client is idle for a while after the first request.</span></span> <span data-ttu-id="d5ca8-135">發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="d5ca8-135">What is happening?</span></span>  

 <span data-ttu-id="d5ca8-136">第二個要求會失敗的主要原因有兩個：(1) 工作階段已逾時或 (2) 主控服務的 Web 伺服器已回收。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-136">The second request can fail primarily for two reasons: (1) the session has timed out or (2) the Web server that is hosting the service is recycled.</span></span> <span data-ttu-id="d5ca8-137">在第一種情況下，會話會一直有效，直到服務超時為止。當服務在服務系結中指定的期間內，未收到來自用戶端的要求 (<xref:System.ServiceModel.Channels.Binding.ReceiveTimeout%2A>) 時，服務會終止安全性會話。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-137">In the first case, the session is valid until the service times out. When the service does not receive a request from the client within the period of time specified in the service's binding (<xref:System.ServiceModel.Channels.Binding.ReceiveTimeout%2A>), the service terminates the security session.</span></span> <span data-ttu-id="d5ca8-138">後續的用戶端訊息會造成 <xref:System.ServiceModel.Security.MessageSecurityException>。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-138">Subsequent client messages result in the <xref:System.ServiceModel.Security.MessageSecurityException>.</span></span> <span data-ttu-id="d5ca8-139">用戶端必須以此服務重新建立安全工作階段，以傳送未來的訊息或使用可設定狀態的安全性內容權杖。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-139">The client must re-establish a secure session with the service to send future messages or use a stateful security context token.</span></span> <span data-ttu-id="d5ca8-140">可設定狀態的安全性內容權杖也允許安全工作階段存留已回收的 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-140">Stateful security context tokens also allow a secure session to survive a Web server being recycled.</span></span> <span data-ttu-id="d5ca8-141">如需在安全會話中使用具狀態安全內容權杖的詳細資訊，請參閱 how [to：為安全會話建立安全性內容權杖](./feature-details/how-to-create-a-security-context-token-for-a-secure-session.md)。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-141">For more information about using stateful secure context tokens in a secure session, see [How to: Create a Security Context Token for a Secure Session](./feature-details/how-to-create-a-security-context-token-for-a-secure-session.md).</span></span> <span data-ttu-id="d5ca8-142">或者，您可以停用安全工作階段。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-142">Alternatively, you can disable secure sessions.</span></span> <span data-ttu-id="d5ca8-143">當您使用系結時 [\<wsHttpBinding>](../configure-apps/file-schema/wcf/wshttpbinding.md) ，可以將 `establishSecurityContext` 屬性設定為， `false` 以停用安全會話。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-143">When you use the [\<wsHttpBinding>](../configure-apps/file-schema/wcf/wshttpbinding.md) binding, you can set the `establishSecurityContext` property to `false` to disable secure sessions.</span></span> <span data-ttu-id="d5ca8-144">如果要為其他繫結停用安全工作階段，必須建立自訂繫結。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-144">To disable secure sessions for other bindings, you must create a custom binding.</span></span> <span data-ttu-id="d5ca8-145">如需有關建立自訂繫結的詳細資料，請參閱 [How to: Create a Custom Binding Using the SecurityBindingElement](./feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-145">For details about creating a custom binding, see [How to: Create a Custom Binding Using the SecurityBindingElement](./feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md).</span></span> <span data-ttu-id="d5ca8-146">在您套用其中任何一種選項之前，必須瞭解您應用程式的安全性需求。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-146">Before you apply any of these options, you must understand your application's security requirements.</span></span>  
  
<a name="BKMK_q2"></a>

## <a name="my-service-starts-to-reject-new-clients-after-about-10-clients-are-interacting-with-it-what-is-happening"></a><span data-ttu-id="d5ca8-147">我的服務在與大約 10 個用戶端互動之後，開始拒絕新的用戶端。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-147">My service starts to reject new clients after about 10 clients are interacting with it.</span></span> <span data-ttu-id="d5ca8-148">發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="d5ca8-148">What is happening?</span></span>  

 <span data-ttu-id="d5ca8-149">根據預設，服務同時只能有 10 個工作階段。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-149">By default, services can have only 10 concurrent sessions.</span></span> <span data-ttu-id="d5ca8-150">因此，如果服務繫結使用工作階段，服務會接受新用戶端連線直到到達該數目，然後拒絕新用戶端連線，直到其中一個目前工作階段結束為止。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-150">Therefore, if the service bindings use sessions, the service accepts new client connections until it reaches that number, after which it refuses new client connections until one of the current sessions ends.</span></span> <span data-ttu-id="d5ca8-151">您可以使用許多種方法來支援多個用戶端。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-151">You can support more clients in a number of ways.</span></span> <span data-ttu-id="d5ca8-152">如果您的服務不需要工作階段，請勿使用工作階段繫結</span><span class="sxs-lookup"><span data-stu-id="d5ca8-152">If your service does not require sessions, do not use a sessionful binding.</span></span> <span data-ttu-id="d5ca8-153"> (需詳細資訊，請參閱 [使用會話](using-sessions.md)。 ) 另一個選項是將屬性的值變更 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentSessions%2A> 為適合您情況的數目，以增加會話限制。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-153">(For more information, see [Using Sessions](using-sessions.md).) Another option is to increase the session limit by changing the value of the <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentSessions%2A> property to the number appropriate to your circumstance.</span></span>  
  
<a name="BKMK_q3"></a>

## <a name="can-i-load-my-service-configuration-from-somewhere-other-than-the-wcf-applications-configuration-file"></a><span data-ttu-id="d5ca8-154">我可以從 WCF 應用程式的組態檔以外的地方載入我的服務組態嗎？</span><span class="sxs-lookup"><span data-stu-id="d5ca8-154">Can I load my service configuration from somewhere other than the WCF application’s configuration file?</span></span>  

 <span data-ttu-id="d5ca8-155">可以，不過您必須建立覆寫 <xref:System.ServiceModel.ServiceHost> 方法的自訂 <xref:System.ServiceModel.ServiceHostBase.ApplyConfiguration%2A> 類別。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-155">Yes, however, you have to create a custom <xref:System.ServiceModel.ServiceHost> class that overrides the <xref:System.ServiceModel.ServiceHostBase.ApplyConfiguration%2A> method.</span></span> <span data-ttu-id="d5ca8-156">在該方法中，您可以呼叫基底先載入組態 (如果您也想要載入標準組態資訊)，但您也可以完全取代組態載入系統。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-156">Inside that method, you can call the base to load configuration first (if you want to load the standard configuration information as well) but you can also entirely replace the configuration loading system.</span></span> <span data-ttu-id="d5ca8-157">如果您想要從不同于應用程式佈建檔的設定檔載入設定，您必須自行剖析設定檔並載入設定。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-157">If you want to load configuration from a configuration file that is different from the application configuration file, you must parse the configuration file yourself and load the configuration.</span></span>  
  
 <span data-ttu-id="d5ca8-158">下列程式碼範例將示範如何覆寫 <xref:System.ServiceModel.ServiceHostBase.ApplyConfiguration%2A> 方法，以及直接設定端點。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-158">The following code example shows how to override the <xref:System.ServiceModel.ServiceHostBase.ApplyConfiguration%2A> method and directly configure an endpoint.</span></span>  
  
```csharp
public class MyServiceHost : ServiceHost  
{  
    public MyServiceHost(Type serviceType, params Uri[] baseAddresses)
      : base(serviceType, baseAddresses)  
    {
        Console.WriteLine("MyServiceHost Constructor");
    }  
  
    protected override void ApplyConfiguration()  
    {  
        string straddress = GetAddress();  
        Uri address = new Uri(straddress);  
        Binding binding = GetBinding();  
        base.AddServiceEndpoint(typeof(IData), binding, address);  
    }  
  
    string GetAddress()  
    {
        return "http://MyMachine:7777/MyEndpointAddress/";
    }  
  
    Binding GetBinding()  
    {  
        WSHttpBinding binding = new WSHttpBinding();  
        binding.Security.Mode = SecurityMode.None;  
        return binding;  
    }  
}  
```  
  
<a name="BKMK_q4"></a>

## <a name="my-service-and-client-work-great-but-i-cant-get-them-to-work-when-the-client-is-on-another-computer-whats-happening"></a><span data-ttu-id="d5ca8-159">我的服務和用戶端運作良好，但是當用戶端在另一台電腦上時，它們就無法運作。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-159">My service and client work great, but I can’t get them to work when the client is on another computer?</span></span> <span data-ttu-id="d5ca8-160">發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="d5ca8-160">What’s happening?</span></span>  

 <span data-ttu-id="d5ca8-161">根據例外狀況，可能有幾個問題：</span><span class="sxs-lookup"><span data-stu-id="d5ca8-161">Depending upon the exception, there may be several issues:</span></span>  
  
- <span data-ttu-id="d5ca8-162">您可能需要將用戶端端點位址變更為主機名稱而非 "localhost"。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-162">You might need to change the client endpoint addresses to the host name and not "localhost".</span></span>  
  
- <span data-ttu-id="d5ca8-163">您可能需要對應用程式開放連接埠。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-163">You might need to open the port to the application.</span></span> <span data-ttu-id="d5ca8-164">如需詳細資料，請參閱 SDK 範例的 [Firewall Instructions](./samples/firewall-instructions.md) 。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-164">For details, see [Firewall Instructions](./samples/firewall-instructions.md) from the SDK samples.</span></span>  
  
- <span data-ttu-id="d5ca8-165">如需其他可能的問題，請參閱執行 [Windows Communication Foundation 範例](./samples/running-the-samples.md)的範例主題。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-165">For other possible issues, see the samples topic [Running the Windows Communication Foundation Samples](./samples/running-the-samples.md).</span></span>  
  
- <span data-ttu-id="d5ca8-166">如果您的用戶端是使用 Windows 認證，且例外狀況為 <xref:System.ServiceModel.Security.SecurityNegotiationException>，請設定 Kerberos 如下。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-166">If your client is using Windows credentials and the exception is a <xref:System.ServiceModel.Security.SecurityNegotiationException>, configure Kerberos as follows.</span></span>  
  
    1. <span data-ttu-id="d5ca8-167">將身分識別認證新增至用戶端的 App.config 檔案中的端點項目：</span><span class="sxs-lookup"><span data-stu-id="d5ca8-167">Add the identity credentials to the endpoint element in the client’s App.config file:</span></span>  
  
        ```xml
        <endpoint
          address="http://MyServer:8000/MyService/"
          binding="wsHttpBinding"
          bindingConfiguration="WSHttpBinding_IServiceExample"
          contract="IServiceExample"
          behaviorConfiguration="ClientCredBehavior"
          name="WSHttpBinding_IServiceExample">  
          <identity>  
            <userPrincipalName value="name@corp.contoso.com"/>  
          </identity>  
        </endpoint>  
        ```  
  
    2. <span data-ttu-id="d5ca8-168">在 System 或 NetworkService 帳戶下執行自我主控的服務。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-168">Run the self-hosted service under the System or NetworkService account.</span></span> <span data-ttu-id="d5ca8-169">您可以執行這個命令，在 System 帳戶下建立命令視窗：</span><span class="sxs-lookup"><span data-stu-id="d5ca8-169">You can run this command to create a command window under the System account:</span></span>  
  
        ```console
        at 12:36 /interactive "cmd.exe"  
        ```  
  
    3. <span data-ttu-id="d5ca8-170">在網際網路資訊服務 (IIS) 下主控服務，根據預設，它會使用服務主要名稱 (SPN) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-170">Host the service under Internet Information Services (IIS), which, by default, uses the service principal name (SPN) account.</span></span>  
  
    4. <span data-ttu-id="d5ca8-171">使用 SetSPN 向網域註冊新的 SPN。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-171">Register a new SPN with the domain using SetSPN.</span></span> <span data-ttu-id="d5ca8-172">您必須是網域系統管理員，才能這樣做。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-172">You need to be a domain administrator in order to do this.</span></span>  
  
 <span data-ttu-id="d5ca8-173">如需 Kerberos 通訊協定的詳細資訊，請參閱 [WCF 中使用的安全性概念](./feature-details/security-concepts-used-in-wcf.md) 和：</span><span class="sxs-lookup"><span data-stu-id="d5ca8-173">For more information about the Kerberos protocol, see [Security Concepts Used in WCF](./feature-details/security-concepts-used-in-wcf.md) and:</span></span>  
  
- [<span data-ttu-id="d5ca8-174">偵錯 Windows 驗證錯誤</span><span class="sxs-lookup"><span data-stu-id="d5ca8-174">Debugging Windows Authentication Errors</span></span>](./feature-details/debugging-windows-authentication-errors.md)  
  
- <span data-ttu-id="d5ca8-175">[使用 Http.sys 登錄 Kerberos 服務主要名稱](/previous-versions/sql/sql-server-2008-r2/ms178119(v=sql.105))</span><span class="sxs-lookup"><span data-stu-id="d5ca8-175">[Registering Kerberos Service Principal Names by Using Http.sys](/previous-versions/sql/sql-server-2008-r2/ms178119(v=sql.105))</span></span>  
  
- <span data-ttu-id="d5ca8-176">[Kerberos 說明](/previous-versions/windows/it-pro/windows-2000-server/bb742516(v=technet.10))</span><span class="sxs-lookup"><span data-stu-id="d5ca8-176">[Kerberos Explained](/previous-versions/windows/it-pro/windows-2000-server/bb742516(v=technet.10))</span></span>  
  
<a name="BKMK_q5"></a>

## <a name="when-i-throw-a-faultexceptionexception-where-the-type-is-an-exception-i-always-receive-a-general-faultexception-type-on-the-client-and-not-the-generic-type-whats-happening"></a><span data-ttu-id="d5ca8-177">當我擲回類型為例外狀況的 FaultException 時 \<Exception> ，我一律會在用戶端上收到一般 FaultException 類型，而不是在泛型型別上。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-177">When I throw a FaultException\<Exception> where the type is an exception, I always receive a general FaultException type on the client and not the generic type.</span></span> <span data-ttu-id="d5ca8-178">發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="d5ca8-178">What’s happening?</span></span>  

 <span data-ttu-id="d5ca8-179">強烈建議您建議自己的自訂錯誤資料型別，並宣告為您的錯誤合約中的詳細型別。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-179">It is highly recommended that you create your own custom error data type and declare that as the detail type in your fault contract.</span></span> <span data-ttu-id="d5ca8-180">原因是使用系統提供的例外狀況類型：</span><span class="sxs-lookup"><span data-stu-id="d5ca8-180">The reason is that using system-provided exception types:</span></span>  
  
- <span data-ttu-id="d5ca8-181">建立類型依存性，移除服務導向應用程式的其中一個最大的強度。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-181">Creates a type dependency that removes one of the biggest strengths of service-oriented applications.</span></span>  
  
- <span data-ttu-id="d5ca8-182">無法依存以標準方式序列化的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-182">Cannot depend upon exceptions serializing in a standard way.</span></span> <span data-ttu-id="d5ca8-183">有些 (例如 <xref:System.Security.SecurityException>) 可能完全不能序列化。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-183">Some—like <xref:System.Security.SecurityException>—may not be serializable at all.</span></span>  
  
- <span data-ttu-id="d5ca8-184">對用戶端公開內部實作詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-184">Exposes internal implementation details to clients.</span></span> <span data-ttu-id="d5ca8-185">如需詳細資訊，請參閱 [指定和處理合約和服務中的錯誤](specifying-and-handling-faults-in-contracts-and-services.md)。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-185">For more information, see [Specifying and Handling Faults in Contracts and Services](specifying-and-handling-faults-in-contracts-and-services.md).</span></span>  
  
 <span data-ttu-id="d5ca8-186">然而，如果您是對應用程式進行偵錯，可以使用 <xref:System.ServiceModel.Description.ServiceDebugBehavior> 類別來序列化例外狀況資訊，並傳回用戶端。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-186">If you are debugging an application, however, you can serialize exception information and return it to the client by using the <xref:System.ServiceModel.Description.ServiceDebugBehavior> class.</span></span>  
  
<a name="BKMK_q6"></a>

## <a name="it-seems-like-one-way-and-request-reply-operations-return-at-roughly-the-same-speed-when-the-reply-contains-no-data-whats-happening"></a><span data-ttu-id="d5ca8-187">當回覆未包含任何資料時，單向和要求與回覆作業似乎會以大約相同的速度傳回。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-187">It seems like one-way and request-reply operations return at roughly the same speed when the reply contains no data.</span></span> <span data-ttu-id="d5ca8-188">這是為什麼？</span><span class="sxs-lookup"><span data-stu-id="d5ca8-188">What's happening?</span></span>  

 <span data-ttu-id="d5ca8-189">將作業指定為單向只是表示作業合約接受輸入訊息，而沒有傳回輸出訊息。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-189">Specifying that an operation is one way means only that the operation contract accepts an input message and does not return an output message.</span></span> <span data-ttu-id="d5ca8-190">在 WCF 中，當輸出資料已寫入網路或擲回例外狀況時，所有用戶端調用都會傳回。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-190">In WCF, all client invocations return when the outbound data has been written to the wire or an exception is thrown.</span></span> <span data-ttu-id="d5ca8-191">單向作業的運作方式相同，如果找不到服務可以擲回，或如果服務尚未準備好從網路接受資料便會封鎖。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-191">One-way operations work the same way, and they can throw if the service cannot be located or block if the service is not prepared to accept the data from the network.</span></span> <span data-ttu-id="d5ca8-192">一般來說，在 WCF 中，這會導致單向呼叫傳回用戶端的速度比要求-回復更快;但減緩透過網路傳送輸出資料的任何狀況，都會使單向作業和要求-回復作業變慢。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-192">Typically in WCF, this results in one-way calls returning to the client more quickly than request-reply; but any condition that slows the sending of the outbound data over the network slows one-way operations as well as request-reply operations.</span></span> <span data-ttu-id="d5ca8-193">如需詳細資訊，請參閱 [單向服務](./feature-details/one-way-services.md) 和 [使用 WCF 用戶端存取服務](./feature-details/accessing-services-using-a-client.md)。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-193">For more information, see [One-Way Services](./feature-details/one-way-services.md) and [Accessing Services Using a WCF Client](./feature-details/accessing-services-using-a-client.md).</span></span>  
  
<a name="BKMK_q77"></a>

## <a name="im-using-an-x509-certificate-with-my-service-and-i-get-a-systemsecuritycryptographycryptographicexception-whats-happening"></a><span data-ttu-id="d5ca8-194">我使用 X.509 憑證搭配我的服務，然後得到 System.Security.Cryptography.CryptographicException。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-194">I’m using an X.509 certificate with my service and I get a System.Security.Cryptography.CryptographicException.</span></span> <span data-ttu-id="d5ca8-195">發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="d5ca8-195">What’s happening?</span></span>  

 <span data-ttu-id="d5ca8-196">這常常發生在變更用來執行 IIS 背景工作處理序的使用者帳戶之後。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-196">This commonly occurs after changing the user account under which the IIS worker process runs.</span></span> <span data-ttu-id="d5ca8-197">例如，在 Windows XP 中，如果您將 Aspnet_wp.exe 從 ASPNET 下執行的預設使用者帳戶變更為自訂使用者帳戶，您可能會看到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-197">For example, in Windows XP, if you change the default user account that the Aspnet_wp.exe runs under from ASPNET to a custom user account, you may see this error.</span></span> <span data-ttu-id="d5ca8-198">如果使用私密金鑰，使用它的處理序將會需要有權限才能存取儲存該金鑰的檔案。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-198">If using a private key, the process that uses it will need to have permissions to access the file storing that key.</span></span>  
  
 <span data-ttu-id="d5ca8-199">如果是這種情況，您必須提供存取權限給處理序的帳戶，檔案才能包含私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-199">If this is the case, you must give read access privileges to the process's account for the file containing the private key.</span></span> <span data-ttu-id="d5ca8-200">例如，如果 IIS 背景工作處理序正在 Bob 帳戶下執行，則您會需要為 Bob 提供含有私密金鑰的檔案的讀取權。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-200">For example, if the IIS worker process is running under the Bob account, then you will need to give Bob read access to the file containing the private key.</span></span>  
  
 <span data-ttu-id="d5ca8-201">如需如何為正確的使用者帳戶授與特定 x.509 憑證私密金鑰之檔案的存取權，請參閱 how [to：讓 WCF 可存取 x.509 的憑證](./feature-details/how-to-make-x-509-certificates-accessible-to-wcf.md)。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-201">For more information about how to give the correct user account access to the file that contains the private key for a specific X.509 certificate, see [How to: Make X.509 Certificates Accessible to WCF](./feature-details/how-to-make-x-509-certificates-accessible-to-wcf.md).</span></span>  
  
<a name="BKMK_q88"></a>

## <a name="i-changed-the-first-parameter-of-an-operation-from-uppercase-to-lowercase-now-my-client-throws-an-exception-whats-happening"></a><span data-ttu-id="d5ca8-202">我將作業的第一個參數從大寫變更為小寫；現在我的用戶端擲回了例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-202">I changed the first parameter of an operation from uppercase to lowercase; now my client throws an exception.</span></span> <span data-ttu-id="d5ca8-203">這是為什麼？</span><span class="sxs-lookup"><span data-stu-id="d5ca8-203">What's happening?</span></span>  

 <span data-ttu-id="d5ca8-204">作業簽章中參數名稱的值是合約的一部分，而且會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-204">The values of the parameter names in the operation signature are part of the contract and are case-sensitive.</span></span> <span data-ttu-id="d5ca8-205">當您需要區分本機參數名稱和描述用戶端應用程式的作業的中繼資料時，請使用 <xref:System.ServiceModel.MessageParameterAttribute?displayProperty=nameWithType> 屬性。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-205">Use the <xref:System.ServiceModel.MessageParameterAttribute?displayProperty=nameWithType> attribute when you need to distinguish between the local parameter name and the metadata that describes the operation for client applications.</span></span>  
  
<a name="BKMK_q99"></a>

## <a name="im-using-one-of-my-tracing-tools-and-i-get-an-endpointnotfoundexception-whats-happening"></a><span data-ttu-id="d5ca8-206">我正在使用我的其中一種追蹤工具，而我得到 EndpointNotFoundException。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-206">I’m using one of my tracing tools and I get an EndpointNotFoundException.</span></span> <span data-ttu-id="d5ca8-207">發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="d5ca8-207">What’s happening?</span></span>  

 <span data-ttu-id="d5ca8-208">如果您使用的追蹤工具不是系統提供的 WCF 追蹤機制，且您收到指出 <xref:System.ServiceModel.EndpointNotFoundException> 位址篩選不相符的訊息，您必須使用 <xref:System.ServiceModel.Description.ClientViaBehavior> 類別將訊息導向追蹤公用程式，並讓公用程式將這些訊息重新導向至服務位址。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-208">If you are using a tracing tool that is not the system-provided WCF tracing mechanism and you receive an <xref:System.ServiceModel.EndpointNotFoundException> that indicates that there was an address filter mismatch, you need to use the <xref:System.ServiceModel.Description.ClientViaBehavior> class to direct the messages to the tracing utility and have the utility redirect those messages to the service address.</span></span> <span data-ttu-id="d5ca8-209"><xref:System.ServiceModel.Description.ClientViaBehavior> 類別會變更 `Via` 位址標頭，以指定與最終接收者不同的下一個網路位址，由 `To` 位址標頭指示。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-209">The <xref:System.ServiceModel.Description.ClientViaBehavior> class alters the `Via` addressing header to specify the next network address separately from the ultimate receiver, indicated by the `To` addressing header.</span></span> <span data-ttu-id="d5ca8-210">然而，執行這項操作時，請勿變更端點位址，它是用於建立 `To` 值的。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-210">When doing this, however, do not change the endpoint address, which is used to establish the `To` value.</span></span>  
  
 <span data-ttu-id="d5ca8-211">下列程式碼範例顯示用戶端組態檔範例。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-211">The following code example shows an example client configuration file.</span></span>  
  
```xml
<endpoint
  address="http://localhost:8000/MyServer/"  
  binding="wsHttpBinding"  
  bindingConfiguration="WSHttpBinding_IMyContract"  
  behaviorConfiguration="MyClient"
  contract="IMyContract"
  name="WSHttpBinding_IMyContract">  
</endpoint>  
<behaviors>  
  <endpointBehaviors>  
    <behavior name="MyClient">  
      <clientVia viaUri="http://localhost:8001/MyServer/"/>  
    </behavior>  
  </endpointBehaviors>  
</behaviors>  
```  
  
<a name="BKMK_q10"></a>

## <a name="what-is-the-base-address-how-does-it-relate-to-an-endpoint-address"></a><span data-ttu-id="d5ca8-212">什麼是基底位址？</span><span class="sxs-lookup"><span data-stu-id="d5ca8-212">What is the base address?</span></span> <span data-ttu-id="d5ca8-213">它與端點位址如何產生關聯？</span><span class="sxs-lookup"><span data-stu-id="d5ca8-213">How does it relate to an endpoint address?</span></span>  

 <span data-ttu-id="d5ca8-214">基底位址是 <xref:System.ServiceModel.ServiceHost> 類別的根位址。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-214">A base address is the root address for a <xref:System.ServiceModel.ServiceHost> class.</span></span> <span data-ttu-id="d5ca8-215">根據預設，如果您將 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 類別新增至服務組態中，會從 HTTP 基底位址擷取主機發行的所有端點的 Web 服務描述語言 (WSDL)，加上提供給中繼資料行為的相對位址，加上 "?wsdl"。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-215">By default, if you add a <xref:System.ServiceModel.Description.ServiceMetadataBehavior> class into your service configuration, the Web Services Description Language (WSDL) for all endpoints the host publishes are retrieved from the HTTP base address, plus any relative address provided to the metadata behavior, plus "?wsdl".</span></span> <span data-ttu-id="d5ca8-216">如果您熟悉 ASP.NET 和 IIS，基底位址就相當於虛擬目錄。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-216">If you are familiar with ASP.NET and IIS, the base address is equivalent to the virtual directory.</span></span>  
  
## <a name="sharing-a-port-between-a-service-endpoint-and-a-mex-endpoint-using-the-nettcpbinding"></a><span data-ttu-id="d5ca8-217">使用 NetTcpBinding 在服務端點與 MEX 端點之間共用通訊埠</span><span class="sxs-lookup"><span data-stu-id="d5ca8-217">Sharing a port between a service endpoint and a mex endpoint using the NetTcpBinding</span></span>  

 <span data-ttu-id="d5ca8-218">如果您將服務的基底位址指定為 net.tcp://MyServer:8080/MyService，並且加入下列端點：</span><span class="sxs-lookup"><span data-stu-id="d5ca8-218">If you specify the base address for a service as net.tcp://MyServer:8080/MyService and add the following endpoints:</span></span>  
  
```xml  
<services>  
  <service name="Microsoft.Samples.NetTcp.CalculatorService">  
    <endpoint address="calcsvc" binding ="netTcpBinding" contract="Microsoft.Samples.NetTcp.ICalculator"/>  
    <endpoint address="mex" binding="mexTcpBinding" contract="IMetadataExchange" />  
  </service>  
</services>  
```  
  
 <span data-ttu-id="d5ca8-219">而且，如果您修改其中一個 NetTcpBinding 設定，如下列組態片段所示：</span><span class="sxs-lookup"><span data-stu-id="d5ca8-219">And if you modify one of the NetTcpBinding settings as shown in the following configuration snippet:</span></span>  
  
```xml  
<bindings>  
  <netTcpBinding>  
    <binding closeTimeout="00:01:00" openTimeout="00:01:00" receiveTimeout="00:10:00" sendTimeout="00:01:00" transactionFlow="false" transferMode="Buffered" transactionProtocol="OleTransactions" hostNameComparisonMode="StrongWildcard" listenBacklog="10" maxBufferPoolSize="524288" maxBufferSize="65536" maxConnections="11" maxReceivedMessageSize="65536">  
      <readerQuotas maxDepth="32" maxStringContentLength="8192" maxArrayLength="16384" maxBytesPerRead="4096" maxNameTableCharCount="16384"/>  
      <reliableSession ordered="true" inactivityTimeout="00:10:00" enabled="false"/>  
      <security mode="Transport">  
        <transport clientCredentialType="Windows" protectionLevel="EncryptAndSign"/>  
      </security>  
    </binding>  
  </netTcpBinding>  
</bindings>  
```  
  
 <span data-ttu-id="d5ca8-220">您將看見類似下面的錯誤：未處理的例外狀況: System.ServiceModel.AddressAlreadyInUseException: IP 端點 0.0.0.0:9000 已有接聽項。您可以使用 MEX 端點的不同通訊埠來指定完整 URL，藉以解決這個錯誤，如下列組態片段所示：</span><span class="sxs-lookup"><span data-stu-id="d5ca8-220">You will see an error like the following: Unhandled Exception: System.ServiceModel.AddressAlreadyInUseException: There is already a listener on IP endpoint 0.0.0.0:9000 You can work around this error by specifying a fully qualified URL with a different port for the MEX endpoint as shown in the following configuration snippet:</span></span>  
  
```xml
<services>  
  <service name="Microsoft.Samples.NetTcp.CalculatorService">  
    <endpoint address="calcsvc" binding ="netTcpBinding" contract="Microsoft.Samples.NetTcp.ICalculator"/>  
    <endpoint address="net.tcp://localhost:9001/servicemodelsamples/mex" binding="mexTcpBinding" contract="IMetadataExchange" />  
  </service>  
</services>  
```  
  
<a name="BK_MK99"></a>

## <a name="when-calling-a-wcf-web-http-application-from-a-wcf-soap-application-the-service-returns-the-following-error-405-method-not-allowed"></a><span data-ttu-id="d5ca8-221">從 WCF SOAP 應用程式呼叫 WCF Web HTTP 應用程式時，服務傳回下列錯誤：405 不允許的方法。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-221">When calling a WCF Web HTTP application from a WCF SOAP application the service returns the following error: 405 Method Not Allowed</span></span>  

 <span data-ttu-id="d5ca8-222">呼叫 WCF Web HTTP 應用程式 (<xref:System.ServiceModel.WebHttpBinding> 從 WCF 服務使用和) 的服務， <xref:System.ServiceModel.Description.WebHttpBehavior> 可能會產生下列例外狀況： ``Unhandled Exception: System.ServiceModel.FaultException`1[System.ServiceModel.ExceptionDetail]: The remote server returned an unexpected response: (405) Method Not Allowed.`` 此例外狀況是因為 WCF 覆寫了傳入的外寄 <xref:System.ServiceModel.OperationContext> <xref:System.ServiceModel.OperationContext> 。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-222">Calling a WCF Web HTTP application (a service that uses the <xref:System.ServiceModel.WebHttpBinding> and <xref:System.ServiceModel.Description.WebHttpBehavior>) from a WCF service may generate the following exception: ``Unhandled Exception: System.ServiceModel.FaultException`1[System.ServiceModel.ExceptionDetail]: The remote server returned an unexpected response: (405) Method Not Allowed.`` This exception occurs because WCF overwrites the outgoing <xref:System.ServiceModel.OperationContext> with the incoming <xref:System.ServiceModel.OperationContext>.</span></span> <span data-ttu-id="d5ca8-223">若要解決這個問題，請 <xref:System.ServiceModel.OperationContextScope> 在 WCF WEB HTTP 服務作業中建立。</span><span class="sxs-lookup"><span data-stu-id="d5ca8-223">To solve this problem, create an <xref:System.ServiceModel.OperationContextScope> within the WCF Web HTTP service operation.</span></span> <span data-ttu-id="d5ca8-224">例如：</span><span class="sxs-lookup"><span data-stu-id="d5ca8-224">For example:</span></span>  
  
```csharp
public string Echo(string input)  
{  
    using (new OperationContextScope(this.InnerChannel))  
    {  
        return base.Channel.Echo(input);  
    }  
}  
```  
  
## <a name="see-also"></a><span data-ttu-id="d5ca8-225">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d5ca8-225">See also</span></span>

- [<span data-ttu-id="d5ca8-226">偵錯 Windows 驗證錯誤</span><span class="sxs-lookup"><span data-stu-id="d5ca8-226">Debugging Windows Authentication Errors</span></span>](./feature-details/debugging-windows-authentication-errors.md)
