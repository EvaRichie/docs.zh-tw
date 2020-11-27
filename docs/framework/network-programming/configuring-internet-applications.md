---
title: 設定網際網路應用程式
description: 瞭解如何使用 <system.Net> 元素，在 .NET Framework 中設定網際網路應用程式。 本文包含範例程式碼。
ms.date: 03/30/2017
helpviewer_keywords:
- downloading Internet resources, default proxy
- sending data, default proxy
- receiving data, default proxy
- downloading Internet resources, configuring Internet applications
- protocol-specific modules
- custom authentication modules
- receiving data, configuring Internet applications
- configuration settings [.NET Framework], Internet applications
- requesting data from Internet, configuring Internet applications
- requesting data from Internet, default proxy
- response to Internet request, default proxy
- Internet, configuring Internet applications
- response to Internet request, configuring Internet applications
- default proxy
- network resources, default proxy
- sending data, configuring Internet applications
- network resources, configuring Internet applications
- Internet, default proxy
ms.assetid: bb707c72-eed2-4a82-8800-c9e68df2fd4f
ms.openlocfilehash: 796752ebf6e3cc5c3dac2a20213934f35d31b392
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96287458"
---
# <a name="configuring-internet-applications"></a><span data-ttu-id="64298-104">設定網際網路應用程式</span><span class="sxs-lookup"><span data-stu-id="64298-104">Configuring Internet Applications</span></span>

<span data-ttu-id="64298-105">[ \<system.Net> (網路設定) ](../configure-apps/file-schema/network/system-net-element-network-settings.md) configuration 元素的元素包含應用程式的網路設定資訊。</span><span class="sxs-lookup"><span data-stu-id="64298-105">The [\<system.Net> Element (Network Settings)](../configure-apps/file-schema/network/system-net-element-network-settings.md) configuration element contains network configuration information for applications.</span></span> <span data-ttu-id="64298-106">使用專案[ \<system.Net> (網路設定) ](../configure-apps/file-schema/network/system-net-element-network-settings.md)專案中，您可以設定 proxy 伺服器、設定連接管理參數，以及在應用程式中包含自訂驗證和要求模組。</span><span class="sxs-lookup"><span data-stu-id="64298-106">Using the [\<system.Net> Element (Network Settings)](../configure-apps/file-schema/network/system-net-element-network-settings.md) element, you can set proxy servers, set connection management parameters, and include custom authentication and request modules in your application.</span></span>  
  
 <span data-ttu-id="64298-107">專案[ \<defaultProxy> (網路設定) ](../configure-apps/file-schema/network/defaultproxy-element-network-settings.md)元素會定義類別所傳回的 proxy 伺服器 `GlobalProxySelection` 。</span><span class="sxs-lookup"><span data-stu-id="64298-107">The [\<defaultProxy> Element (Network Settings)](../configure-apps/file-schema/network/defaultproxy-element-network-settings.md) element defines the proxy server returned by the `GlobalProxySelection` class.</span></span> <span data-ttu-id="64298-108">任何未將其專屬 <xref:System.Net.HttpWebRequest.Proxy%2A> 屬性設定為特定值的 <xref:System.Net.HttpWebRequest> 都會使用預設 Proxy。</span><span class="sxs-lookup"><span data-stu-id="64298-108">Any <xref:System.Net.HttpWebRequest> that does not have its own <xref:System.Net.HttpWebRequest.Proxy%2A> property set to a specific value uses the default proxy.</span></span> <span data-ttu-id="64298-109">除了設定 Proxy 位址之外，您還可以建立將不會使用 Proxy 的伺服器位址清單，以及指出不應該將 Proxy 用於本機位址。</span><span class="sxs-lookup"><span data-stu-id="64298-109">In addition to setting the proxy address, you can create a list of server addresses that will not use the proxy, and you can indicate that the proxy should not be used for local addresses.</span></span>  
  
 <span data-ttu-id="64298-110">請務必注意，Microsoft Internet Explorer 設定是與組態設定一起使用，但優先使用後者。</span><span class="sxs-lookup"><span data-stu-id="64298-110">It is important to note that the Microsoft Internet Explorer settings are combined with the configuration settings, with the latter taking precedence.</span></span>  
  
 <span data-ttu-id="64298-111">下列範例會將預設 Proxy 伺服器位址設定為 `http://proxyserver`、指出不應該將 Proxy 用作本機位址，以及指定對 contoso.com 網域所在伺服器的所有要求都應該略過 Proxy。</span><span class="sxs-lookup"><span data-stu-id="64298-111">The following example sets the default proxy server address to `http://proxyserver`, indicates that the proxy should not be used for local addresses, and specifies that all requests to servers located in the contoso.com domain should bypass the proxy.</span></span>  
  
```xml  
<configuration>  
    <system.net>  
        <defaultProxy>  
            <proxy  
                usesystemdefault = "false"  
                proxyaddress = "http://proxyserver:80"  
                bypassonlocal = "true"  
            />  
            <bypasslist>  
                <add address="http://[a-z]+\.contoso\.com/" />  
            </bypasslist>  
        </defaultProxy>  
    </system.net>  
</configuration>  
```  
  
 <span data-ttu-id="64298-112">使用[ \<connectionManagement> (網路設定) ](../configure-apps/file-schema/network/connectionmanagement-element-network-settings.md)專案的元素，設定可對特定伺服器或所有其他伺服器進行的持續連線數目。</span><span class="sxs-lookup"><span data-stu-id="64298-112">Use the [\<connectionManagement> Element (Network Settings)](../configure-apps/file-schema/network/connectionmanagement-element-network-settings.md) element to configure the number of persistent connections that can be made to a specific server or to all other servers.</span></span> <span data-ttu-id="64298-113">下列範例會設定應用程式使用兩個與 `www.contoso.com` 伺服器的持續連線、四個 IP 位址為 192.168.1.2 之伺服器的持續連線，以及一個與所有其他伺服器的持續連線。</span><span class="sxs-lookup"><span data-stu-id="64298-113">The following example configures the application to use two persistent connections to the server `www.contoso.com`, four persistent connections to the server with the IP address 192.168.1.2, and one persistent connection to all other servers.</span></span>  
  
```xml  
<configuration>  
    <system.net>  
        <connectionManagement>  
            <add address="http://www.contoso.com" maxconnection="2" />  
            <add address="192.168.1.2" maxconnection="4" />  
            <add address="*" maxconnection="1" />  
        </connectionManagement>  
    </system.net>  
</configuration>  
```  
  
 <span data-ttu-id="64298-114">自訂驗證模組是使用[ \<authenticationModules> 元素 (網路設定) ](../configure-apps/file-schema/network/authenticationmodules-element-network-settings.md)元素來設定。</span><span class="sxs-lookup"><span data-stu-id="64298-114">Custom authentication modules are configured with the [\<authenticationModules> Element (Network Settings)](../configure-apps/file-schema/network/authenticationmodules-element-network-settings.md) element.</span></span> <span data-ttu-id="64298-115">自訂驗證模組必須實作 <xref:System.Net.IAuthenticationModule> 介面。</span><span class="sxs-lookup"><span data-stu-id="64298-115">Custom authentication modules must implement the <xref:System.Net.IAuthenticationModule> interface.</span></span>  
  
 <span data-ttu-id="64298-116">下列範例設定自訂驗證模組。</span><span class="sxs-lookup"><span data-stu-id="64298-116">The following example configures a custom authentication module.</span></span>  
  
```xml  
<configuration>  
    <system.net>  
        <authenticationModules>  
            <add type="MyAuthModule, MyAuthModule.dll" />  
        </authenticationModules>  
    </system.net>  
</configuration>  
```  
  
 <span data-ttu-id="64298-117">您可以使用專案[ \<webRequestModules> (網路設定) ](../configure-apps/file-schema/network/webrequestmodules-element-network-settings.md)專案，將您的應用程式設定為使用自訂的通訊協定特定模組來要求來自網際網路資源的資訊。</span><span class="sxs-lookup"><span data-stu-id="64298-117">You can use the [\<webRequestModules> Element (Network Settings)](../configure-apps/file-schema/network/webrequestmodules-element-network-settings.md) element to configure your application to use custom protocol-specific modules to request information from Internet resources.</span></span> <span data-ttu-id="64298-118">指定的模組必須實作 <xref:System.Net.IWebRequestCreate> 介面。</span><span class="sxs-lookup"><span data-stu-id="64298-118">The specified modules must implement the <xref:System.Net.IWebRequestCreate> interface.</span></span> <span data-ttu-id="64298-119">您可以在組態檔中指定自訂模組來覆寫預設 HTTP、HTTPS 和檔案要求模組，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="64298-119">You can override the default HTTP, HTTPS, and file request modules by specifying your custom module in the configuration file, as in the following example.</span></span>  
  
```xml  
<configuration>  
    <system.net>  
        <webRequestModules>  
            <add  
                prefix="HTTP"  
                type = "MyHttpRequest.dll, MyHttpRequestCreator"  
            />  
        </webRequestModules>  
    </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a><span data-ttu-id="64298-120">另請參閱</span><span class="sxs-lookup"><span data-stu-id="64298-120">See also</span></span>

- [<span data-ttu-id="64298-121">以 .NET Framework 進行網路程式設計</span><span class="sxs-lookup"><span data-stu-id="64298-121">Network Programming in the .NET Framework</span></span>](index.md)
- [<span data-ttu-id="64298-122">網路設定架構</span><span class="sxs-lookup"><span data-stu-id="64298-122">Network Settings Schema</span></span>](../configure-apps/file-schema/network/index.md)
- [<span data-ttu-id="64298-123">\<system.Net> (網路設定的元素) </span><span class="sxs-lookup"><span data-stu-id="64298-123">\<system.Net> Element (Network Settings)</span></span>](../configure-apps/file-schema/network/system-net-element-network-settings.md)
