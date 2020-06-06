---
title: <defaultProxy> 項目 (網路設定)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#defaultProxy
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/defaultProxy
helpviewer_keywords:
- defaultProxy element
- <defaultProxy> element
ms.assetid: 9d663c4b-07b4-4f6f-9b12-efbd3630354f
ms.openlocfilehash: 0945629c1395917bc1cf825f2ba84d20afa99957
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "71698200"
---
# <a name="defaultproxy-element-network-settings"></a><span data-ttu-id="2807c-102">\<defaultProxy> 項目 (網路設定)</span><span class="sxs-lookup"><span data-stu-id="2807c-102">\<defaultProxy> Element (Network Settings)</span></span>
<span data-ttu-id="2807c-103">設定超文字傳輸協定 (HTTP) 的 Proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="2807c-103">Configures the Hypertext Transfer Protocol (HTTP) proxy server.</span></span>  
  
[**\<configuration>**](../configuration-element.md)  
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)  
&nbsp;&nbsp;&nbsp;&nbsp;**\<defaultProxy>**  
  
## <a name="syntax"></a><span data-ttu-id="2807c-104">語法</span><span class="sxs-lookup"><span data-stu-id="2807c-104">Syntax</span></span>  
  
```xml  
<defaultProxy  
  enabled="true|false"  
  useDefaultCredentials="true|false">  
    <bypasslist>...</bypasslist>  
    <proxy>...</proxy>  
    <module>...</module>  
</defaultProxy>
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="2807c-105">屬性和項目</span><span class="sxs-lookup"><span data-stu-id="2807c-105">Attributes and Elements</span></span>  
 <span data-ttu-id="2807c-106">下列章節說明屬性、子元素和父元素。</span><span class="sxs-lookup"><span data-stu-id="2807c-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="2807c-107">屬性</span><span class="sxs-lookup"><span data-stu-id="2807c-107">Attributes</span></span>  
  
|<span data-ttu-id="2807c-108">**元素**</span><span class="sxs-lookup"><span data-stu-id="2807c-108">**Element**</span></span>|<span data-ttu-id="2807c-109">**說明**</span><span class="sxs-lookup"><span data-stu-id="2807c-109">**Description**</span></span>|  
|-----------------|---------------------|  
|`enabled`|<span data-ttu-id="2807c-110">指定是否使用 Web Proxy。</span><span class="sxs-lookup"><span data-stu-id="2807c-110">Specifies whether a web proxy is used.</span></span> <span data-ttu-id="2807c-111">預設值是 `true`。</span><span class="sxs-lookup"><span data-stu-id="2807c-111">The default value is `true`.</span></span>|  
|`useDefaultCredentials`|<span data-ttu-id="2807c-112">指定此主機的預設認證是否用來存取 Web Proxy。</span><span class="sxs-lookup"><span data-stu-id="2807c-112">Specifies whether the default credentials for this host are used to access the web proxy.</span></span> <span data-ttu-id="2807c-113">預設值是 `false`。</span><span class="sxs-lookup"><span data-stu-id="2807c-113">The default value is `false`.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="2807c-114">子元素</span><span class="sxs-lookup"><span data-stu-id="2807c-114">Child Elements</span></span>  
  
|<span data-ttu-id="2807c-115">**元素**</span><span class="sxs-lookup"><span data-stu-id="2807c-115">**Element**</span></span>|<span data-ttu-id="2807c-116">**說明**</span><span class="sxs-lookup"><span data-stu-id="2807c-116">**Description**</span></span>|  
|-----------------|---------------------|  
|[<span data-ttu-id="2807c-117">bypasslist</span><span class="sxs-lookup"><span data-stu-id="2807c-117">bypasslist</span></span>](bypasslist-element-network-settings.md)|<span data-ttu-id="2807c-118">提供一組位址的規則運算式，說明不使用 Proxy。</span><span class="sxs-lookup"><span data-stu-id="2807c-118">Provides a set of regular expressions that describe addresses that do not use the proxy.</span></span>|  
|[<span data-ttu-id="2807c-119">module</span><span class="sxs-lookup"><span data-stu-id="2807c-119">module</span></span>](module-element-network-settings.md)|<span data-ttu-id="2807c-120">將新的 Proxy 模組加入至應用程式。</span><span class="sxs-lookup"><span data-stu-id="2807c-120">Adds a new proxy module to the application.</span></span>|  
|[<span data-ttu-id="2807c-121">proxy</span><span class="sxs-lookup"><span data-stu-id="2807c-121">proxy</span></span>](proxy-element-network-settings.md)|<span data-ttu-id="2807c-122">定義 Proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="2807c-122">Defines a proxy server.</span></span>|  
  
### <a name="parent-elements"></a><span data-ttu-id="2807c-123">父項目</span><span class="sxs-lookup"><span data-stu-id="2807c-123">Parent Elements</span></span>  
  
|<span data-ttu-id="2807c-124">**元素**</span><span class="sxs-lookup"><span data-stu-id="2807c-124">**Element**</span></span>|<span data-ttu-id="2807c-125">**說明**</span><span class="sxs-lookup"><span data-stu-id="2807c-125">**Description**</span></span>|  
|-----------------|---------------------|  
|[<span data-ttu-id="2807c-126">system.net</span><span class="sxs-lookup"><span data-stu-id="2807c-126">system.net</span></span>](system-net-element-network-settings.md)|<span data-ttu-id="2807c-127">包含會指定 .NET Framework 如何連接至網路的設定。</span><span class="sxs-lookup"><span data-stu-id="2807c-127">Contains settings that specify how the .NET Framework connects to the network.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="2807c-128">備註</span><span class="sxs-lookup"><span data-stu-id="2807c-128">Remarks</span></span>  
 <span data-ttu-id="2807c-129">如果 defaultProxy 項目是空的，則會使用來自 Internet Explorer 的 Proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="2807c-129">If the defaultProxy element is empty, the proxy settings from Internet Explorer will be used.</span></span> <span data-ttu-id="2807c-130">這個行為與 .NET Framework 1.1 版的不同。</span><span class="sxs-lookup"><span data-stu-id="2807c-130">This behavior is different from version 1.1 of the .NET Framework.</span></span>  
  
 <span data-ttu-id="2807c-131">如果[module](module-element-network-settings.md)元素指定非公用類型、類型不是衍生自 <xref:System.Net.IWebProxy> 類別、這個物件的無參數的函式發生例外狀況，或在抓取系統指定的預設 proxy 時發生例外狀況，就會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="2807c-131">An exception is thrown if the [module](module-element-network-settings.md) element specifies a non-public type, the type is not deriving from the <xref:System.Net.IWebProxy> class, an exception from the parameterless constructor of this object occurred, or an exception occurred while retrieving the system-specified default proxy.</span></span> <span data-ttu-id="2807c-132">例外狀況的 <xref:System.Exception.InnerException%2A> 屬性應該會有此錯誤的根本原因之詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="2807c-132">The <xref:System.Exception.InnerException%2A> property on the exception should have more information about the root cause of the error.</span></span>  
  
## <a name="configuration-files"></a><span data-ttu-id="2807c-133">組態檔</span><span class="sxs-lookup"><span data-stu-id="2807c-133">Configuration Files</span></span>  
 <span data-ttu-id="2807c-134">此項目可以用於應用程式組態檔或電腦組態檔 (Machine.config)。</span><span class="sxs-lookup"><span data-stu-id="2807c-134">This element can be used in the application configuration file or the machine configuration file (Machine.config).</span></span>  
  
## <a name="example"></a><span data-ttu-id="2807c-135">範例</span><span class="sxs-lookup"><span data-stu-id="2807c-135">Example</span></span>  
 <span data-ttu-id="2807c-136">下列範例會使用 Internet Explorer proxy 的預設值、指定 proxy 位址，並略過 proxy 以進行本機存取和 contoso.com。</span><span class="sxs-lookup"><span data-stu-id="2807c-136">The following example uses the defaults from the Internet Explorer proxy, specifies the proxy address, and bypasses the proxy for local access and contoso.com.</span></span>  
  
```xml  
<configuration>  
  <system.net>  
    <defaultProxy>  
      <proxy  
        usesystemdefault="true"  
        proxyaddress="http://192.168.1.10:3128"  
        bypassonlocal="true"  
      />  
      <bypasslist>  
        <add address="[a-z]+\.contoso\.com$" />  
      </bypasslist>  
    </defaultProxy>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a><span data-ttu-id="2807c-137">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2807c-137">See also</span></span>

- <xref:System.Net.WebProxy?displayProperty=nameWithType>
- [<span data-ttu-id="2807c-138">網路設定結構描述</span><span class="sxs-lookup"><span data-stu-id="2807c-138">Network Settings Schema</span></span>](index.md)
