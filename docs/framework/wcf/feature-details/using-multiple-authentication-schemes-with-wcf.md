---
title: 搭配 WCF 使用多個驗證配置
ms.date: 03/30/2017
ms.assetid: f32a56a0-e2b2-46bf-a302-29e1275917f9
ms.openlocfilehash: 3aae9bff4300af97f7b179d9d8115340a26e715a
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96289421"
---
# <a name="using-multiple-authentication-schemes-with-wcf"></a><span data-ttu-id="22c03-102">搭配 WCF 使用多個驗證配置</span><span class="sxs-lookup"><span data-stu-id="22c03-102">Using Multiple Authentication Schemes with WCF</span></span>

<span data-ttu-id="22c03-103">WCF 現在允許您在單一端點上指定多個驗證配置。</span><span class="sxs-lookup"><span data-stu-id="22c03-103">WCF now allows you to specify multiple authentication schemes on a single endpoint.</span></span> <span data-ttu-id="22c03-104">此外，Web 裝載服務可以直接從 IIS 繼承驗證設定。</span><span class="sxs-lookup"><span data-stu-id="22c03-104">Furthermore web hosted services can inherit their authentication settings directly from IIS.</span></span> <span data-ttu-id="22c03-105">自我裝載服務可以指定可使用的驗證配置。</span><span class="sxs-lookup"><span data-stu-id="22c03-105">Self-hosted services can specify what authentication schemes can be used.</span></span> <span data-ttu-id="22c03-106">如需在 IIS 中設定驗證設定的詳細資訊，請參閱 [Iis 驗證](https://go.microsoft.com/fwlink/?LinkId=232458)</span><span class="sxs-lookup"><span data-stu-id="22c03-106">For more information about setting authentication settings in IIS, see [IIS Authentication](https://go.microsoft.com/fwlink/?LinkId=232458)</span></span>  
  
## <a name="iis-hosted-services"></a><span data-ttu-id="22c03-107">IIS 裝載的服務</span><span class="sxs-lookup"><span data-stu-id="22c03-107">IIS-Hosted Services</span></span>  

 <span data-ttu-id="22c03-108">對於 IIS 裝載的服務，設定您希望在 IIS 中使用的驗證配置。</span><span class="sxs-lookup"><span data-stu-id="22c03-108">For IIS-hosted services, set the authentication schemes you wish to use in IIS.</span></span> <span data-ttu-id="22c03-109">然後，在您的服務 web.config 檔案中，在您的系結設定中指定 clientCredential 類型為 "InheritedFromHost"，如下列 XML 程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="22c03-109">Then in your service’s web.config file, in your binding configuration specify clientCredential type as "InheritedFromHost" as shown in the following XML snippet:</span></span>  
  
```xml  
<bindings>  
      <basicHttpBinding>  
        <binding name="secureBinding">  
          <security mode="Transport">  
            <transport clientCredentialType="InheritedFromHost" />  
          </security>  
        </binding>  
      </basicHttpBinding>  
    </bindings>  
```  
  
 <span data-ttu-id="22c03-110">您可以使用 ServiceAuthenticationBehavior 或專案，指定您只想要將驗證配置的子集用於服務 \<serviceAuthenticationManager> 。</span><span class="sxs-lookup"><span data-stu-id="22c03-110">You can specify that you only want a subset of authentication schemes to be used with your service using the ServiceAuthenticationBehavior or the \<serviceAuthenticationManager> element.</span></span> <span data-ttu-id="22c03-111">在程式碼中進行這項設定時，請使用 ServiceAuthenticationBehavior，如下列程式碼片段所示。</span><span class="sxs-lookup"><span data-stu-id="22c03-111">When configuring this in code use the ServiceAuthenticationBehavior as shown in the following code snippet.</span></span>  
  
```csharp  
// ...  
ServiceAuthenticationBehavior sab = null;  
sab = serviceHost.Description.Behaviors.Find<ServiceAuthenticationBehavior>();  
  
if (sab == null)  
{  
    sab = new ServiceAuthenticationBehavior();  
    sab.AuthenticationSchemes = AuthenticationSchemes.Basic | AuthenticationSchemes.Negotiate | AuthenticationSchemes.Digest;  
    serviceHost.Description.Behaviors.Add(sab);  
}  
else  
{  
     sab.AuthenticationSchemes = AuthenticationSchemes.Basic | AuthenticationSchemes.Negotiate | AuthenticationSchemes.Digest;  
}  
// ...  
```  
  
 <span data-ttu-id="22c03-112">在設定檔中設定此專案時，請使用 \<serviceAuthenticationManager> 元素，如下列 XML 片段所示。</span><span class="sxs-lookup"><span data-stu-id="22c03-112">When configuring this in a config file, use the \<serviceAuthenticationManager> element as shown in the following XML snippet.</span></span>  
  
```xml  
<behaviors>  
      <serviceBehaviors>  
        <behavior name="limitedAuthBehavior">  
          <serviceAuthenticationManager authenticationSchemes="Negotiate, Digest, Basic"/>  
          <!-- ... -->  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
```  
  
 <span data-ttu-id="22c03-113">這將確保只會根據在 IIS 中選取的部分，考慮將這裡列出的驗證配置子集套用在服務端點。</span><span class="sxs-lookup"><span data-stu-id="22c03-113">This will ensure that only a subset of the authentication schemes listed here will be considered for applying on the service endpoint, depending on what is selected in the IIS.</span></span> <span data-ttu-id="22c03-114">這表示開發人員可以在 serviceAuthenticationManager 清單中省略該項基本驗證，將其從清單中排除，即使已在 IIS 中啟用亦同，這項驗證將不會套用在服務端點上。</span><span class="sxs-lookup"><span data-stu-id="22c03-114">This means that a developer can exclude say Basic auth from the list by omitting it from the serviceAuthenticationManager listing and even if it is enabled in IIS, it will not be applied on the service endpoint</span></span>  
  
## <a name="self-hosted-services"></a><span data-ttu-id="22c03-115">自我裝載的服務</span><span class="sxs-lookup"><span data-stu-id="22c03-115">Self-Hosted Services</span></span>  

 <span data-ttu-id="22c03-116">自我裝載服務的設定方式有點不同，因為沒有可繼承其設定的 IIS。</span><span class="sxs-lookup"><span data-stu-id="22c03-116">Self-hosted services are configured a bit differently since there is no IIS to inherit settings from.</span></span> <span data-ttu-id="22c03-117">您可以在這裡使用 \<serviceAuthenticationManager> 元素或 ServiceAuthenticationBehavior 來指定將繼承的驗證設定。</span><span class="sxs-lookup"><span data-stu-id="22c03-117">Here you use the \<serviceAuthenticationManager> element or ServiceAuthenticationBehavior to specify the authentication settings that will be inherited.</span></span> <span data-ttu-id="22c03-118">在程式碼中，看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="22c03-118">In code it looks like this:</span></span>  
  
```csharp  
// ...  
ServiceAuthenticationBehavior sab = null;  
sab = serviceHost.Description.Behaviors.Find<ServiceAuthenticationBehavior>();  
  
if (sab == null)  
{  
    sab = new ServiceAuthenticationBehavior();  
    sab.AuthenticationSchemes = AuthenticationSchemes.Basic | AuthenticationSchemes.Negotiate | AuthenticationSchemes.Digest;  
    serviceHost.Description.Behaviors.Add(sab);  
}  
else  
{  
     sab.AuthenticationSchemes = AuthenticationSchemes.Basic | AuthenticationSchemes.Negotiate | AuthenticationSchemes.Digest;  
}  
// ...  
```  
  
 <span data-ttu-id="22c03-119">在組態中，看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="22c03-119">In config, it looks like this:</span></span>  
  
```xml  
<behaviors>  
      <serviceBehaviors>  
        <behavior name="limitedAuthBehavior">  
          <serviceAuthenticationManager authenticationSchemes="Negotiate, Digest, Basic"/>  
          <!-- ... -->  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
```  
  
 <span data-ttu-id="22c03-120">然後您可以在繫結設定中指定 InheritFromHost，如下列 XML 片段所示。</span><span class="sxs-lookup"><span data-stu-id="22c03-120">And then you can specify InheritFromHost in your binding settings as shown in the following XML snippet.</span></span>  
  
```xml  
<bindings>  
      <basicHttpBinding>  
        <binding name="secureBinding">  
          <security mode="Transport">  
            <transport clientCredentialType="InheritedFromHost" />  
          </security>  
        </binding>  
      </basicHttpBinding>  
    </bindings>  
```  
  
 <span data-ttu-id="22c03-121">或者，您可在 HTTP 傳輸繫結元素上設定驗證配置，以指定自訂繫結中的驗證配置，如下列組態片段所示。</span><span class="sxs-lookup"><span data-stu-id="22c03-121">Alternatively, you can specify the authentication schemes in a custom binding, by setting the authentication schemes on the HTTP transport binding element, as shown in the following config snippet.</span></span>  
  
```xml  
<binding name="multipleBinding">  
      <textMessageEncoding/>  
      <httpTransport authenticationScheme="Negotiate, Ntlm, Digest, Basic" />  
    </binding>  
```  
  
## <a name="see-also"></a><span data-ttu-id="22c03-122">另請參閱</span><span class="sxs-lookup"><span data-stu-id="22c03-122">See also</span></span>

- [<span data-ttu-id="22c03-123">繫結和安全性</span><span class="sxs-lookup"><span data-stu-id="22c03-123">Bindings and Security</span></span>](bindings-and-security.md)
- [<span data-ttu-id="22c03-124">端點：位址、繫結和合約</span><span class="sxs-lookup"><span data-stu-id="22c03-124">Endpoints: Addresses, Bindings, and Contracts</span></span>](endpoints-addresses-bindings-and-contracts.md)
- [<span data-ttu-id="22c03-125">設定系統提供的繫結</span><span class="sxs-lookup"><span data-stu-id="22c03-125">Configuring System-Provided Bindings</span></span>](configuring-system-provided-bindings.md)
- [<span data-ttu-id="22c03-126">自訂繫結的安全性功能</span><span class="sxs-lookup"><span data-stu-id="22c03-126">Security Capabilities with Custom Bindings</span></span>](security-capabilities-with-custom-bindings.md)
- [<span data-ttu-id="22c03-127">繫結</span><span class="sxs-lookup"><span data-stu-id="22c03-127">Bindings</span></span>](bindings.md)
- [<span data-ttu-id="22c03-128">自訂繫結</span><span class="sxs-lookup"><span data-stu-id="22c03-128">Custom Bindings</span></span>](../extending/custom-bindings.md)
