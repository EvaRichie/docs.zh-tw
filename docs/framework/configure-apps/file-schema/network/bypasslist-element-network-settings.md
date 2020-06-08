---
title: <bypasslist> 項目 (網路設定)
description: <bypasslist>網路設定元素會提供一組正則運算式，描述不會在 .NET Framework 中使用 proxy 的位址。
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#bypasslist
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/defaultProxy/bypasslist
helpviewer_keywords:
- bypasslist element
- <bypasslist> element
ms.assetid: 124446b7-abb1-4e5e-a492-b64398f268f1
ms.openlocfilehash: 42b6ddf4c3d09bcf8ef0ada105cefedccc63b505
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504624"
---
# <a name="bypasslist-element-network-settings"></a><span data-ttu-id="45663-103">\<bypasslist> 項目 (網路設定)</span><span class="sxs-lookup"><span data-stu-id="45663-103">\<bypasslist> Element (Network Settings)</span></span>
<span data-ttu-id="45663-104">提供一組正則運算式，描述不使用 proxy 的位址。</span><span class="sxs-lookup"><span data-stu-id="45663-104">Provides a set of regular expressions that describe addresses that do not use a proxy.</span></span>  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<defaultProxy>**](defaultproxy-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<bypasslist>**

## <a name="syntax"></a><span data-ttu-id="45663-105">語法</span><span class="sxs-lookup"><span data-stu-id="45663-105">Syntax</span></span>  
  
```xml  
<bypasslist>
</bypasslist>  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="45663-106">屬性和項目</span><span class="sxs-lookup"><span data-stu-id="45663-106">Attributes and Elements</span></span>  
 <span data-ttu-id="45663-107">下列章節說明屬性、子元素和父元素。</span><span class="sxs-lookup"><span data-stu-id="45663-107">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="45663-108">屬性</span><span class="sxs-lookup"><span data-stu-id="45663-108">Attributes</span></span>  
 <span data-ttu-id="45663-109">無。</span><span class="sxs-lookup"><span data-stu-id="45663-109">None.</span></span>  
  
### <a name="child-elements"></a><span data-ttu-id="45663-110">子元素</span><span class="sxs-lookup"><span data-stu-id="45663-110">Child Elements</span></span>  
  
|<span data-ttu-id="45663-111">**元素**</span><span class="sxs-lookup"><span data-stu-id="45663-111">**Element**</span></span>|<span data-ttu-id="45663-112">**描述**</span><span class="sxs-lookup"><span data-stu-id="45663-112">**Description**</span></span>|  
|-----------------|---------------------|  
|[<span data-ttu-id="45663-113">add</span><span class="sxs-lookup"><span data-stu-id="45663-113">add</span></span>](add-element-for-bypasslist-network-settings.md)|<span data-ttu-id="45663-114">將 IP 位址或 DNS 名稱新增至 proxy 略過清單。</span><span class="sxs-lookup"><span data-stu-id="45663-114">Adds an IP address or DNS name to the proxy bypass list.</span></span>|  
|[<span data-ttu-id="45663-115">明確</span><span class="sxs-lookup"><span data-stu-id="45663-115">clear</span></span>](clear-element-for-bypasslist-network-settings.md)|<span data-ttu-id="45663-116">清除略過清單。</span><span class="sxs-lookup"><span data-stu-id="45663-116">Clears the bypass list.</span></span>|  
|[<span data-ttu-id="45663-117">remove</span><span class="sxs-lookup"><span data-stu-id="45663-117">remove</span></span>](remove-element-for-bypasslist-network-settings.md)|<span data-ttu-id="45663-118">從 proxy 略過清單中移除 IP 位址或 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="45663-118">Removes an IP address or DNS name from the proxy bypass list.</span></span>|  
  
### <a name="parent-elements"></a><span data-ttu-id="45663-119">父項目</span><span class="sxs-lookup"><span data-stu-id="45663-119">Parent Elements</span></span>  
  
|<span data-ttu-id="45663-120">**元素**</span><span class="sxs-lookup"><span data-stu-id="45663-120">**Element**</span></span>|<span data-ttu-id="45663-121">**描述**</span><span class="sxs-lookup"><span data-stu-id="45663-121">**Description**</span></span>|  
|-----------------|---------------------|  
|[<span data-ttu-id="45663-122">defaultProxy</span><span class="sxs-lookup"><span data-stu-id="45663-122">defaultProxy</span></span>](defaultproxy-element-network-settings.md)|<span data-ttu-id="45663-123">設定超文字傳輸協定 (HTTP) 的 Proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="45663-123">Configures the Hypertext Transfer Protocol (HTTP) proxy server.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="45663-124">備註</span><span class="sxs-lookup"><span data-stu-id="45663-124">Remarks</span></span>  
 <span data-ttu-id="45663-125">「略過清單」包含正則運算式，可描述 <xref:System.Net.WebRequest> 實例直接存取而不是透過 proxy 伺服器存取的 uri。</span><span class="sxs-lookup"><span data-stu-id="45663-125">The bypass list contains regular expressions that describe URIs that <xref:System.Net.WebRequest> instances access directly instead of through the proxy server.</span></span>  
  
 <span data-ttu-id="45663-126">為此元素指定正則運算式時，請務必小心。</span><span class="sxs-lookup"><span data-stu-id="45663-126">You should use caution when specifying a regular expression for this element.</span></span> <span data-ttu-id="45663-127">正則運算式 "[a-z] + \\ . contoso \\ .com" 符合 contoso.com 網域中的任何主機，但也符合 contoso.com.cpandl.com 網域中的任何主機。</span><span class="sxs-lookup"><span data-stu-id="45663-127">The regular expression "[a-z]+\\.contoso\\.com" matches any host in the contoso.com domain, but it also matches any host in the contoso.com.cpandl.com domain.</span></span> <span data-ttu-id="45663-128">若只要比對 contoso.com 網域中的主機，請使用錨點（"$"）： "[a-z] + \\ . contoso \\ .com $"。</span><span class="sxs-lookup"><span data-stu-id="45663-128">To match only a host in the contoso.com domain, use an anchor ("$"): "[a-z]+\\.contoso\\.com$".</span></span>  
  
 <span data-ttu-id="45663-129">如需正則運算式的詳細資訊，請參閱。[.NET Framework 正則運算式](../../../../standard/base-types/regular-expressions.md)。</span><span class="sxs-lookup"><span data-stu-id="45663-129">For more information about regular expressions, see .[.NET Framework Regular Expressions](../../../../standard/base-types/regular-expressions.md).</span></span>  
  
## <a name="configuration-files"></a><span data-ttu-id="45663-130">組態檔</span><span class="sxs-lookup"><span data-stu-id="45663-130">Configuration Files</span></span>  
 <span data-ttu-id="45663-131">此項目可以用於應用程式組態檔或電腦組態檔 (Machine.config)。</span><span class="sxs-lookup"><span data-stu-id="45663-131">This element can be used in the application configuration file or the machine configuration file (Machine.config).</span></span>  
  
## <a name="example"></a><span data-ttu-id="45663-132">範例</span><span class="sxs-lookup"><span data-stu-id="45663-132">Example</span></span>  
 <span data-ttu-id="45663-133">下列範例會將兩個位址新增至略過清單。</span><span class="sxs-lookup"><span data-stu-id="45663-133">The following example adds two addresses to the bypass list.</span></span> <span data-ttu-id="45663-134">第一個會略過 contoso.com 網域中所有伺服器的 proxy;第二個會略過其 IP 位址開頭為192.168 的所有伺服器的 proxy。</span><span class="sxs-lookup"><span data-stu-id="45663-134">The first bypasses the proxy for all servers in the contoso.com domain; the second bypasses the proxy for all servers whose IP addresses begin with 192.168.</span></span>  
  
```xml  
<configuration>  
  <system.net>  
    <defaultProxy>  
      <bypasslist>  
        <add address="[a-z]+\.contoso\.com$" />  
        <add address="192\.168\.\d{1,3}\.\d{1,3}" />  
      </bypasslist>  
    </defaultProxy>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a><span data-ttu-id="45663-135">另請參閱</span><span class="sxs-lookup"><span data-stu-id="45663-135">See also</span></span>

- <xref:System.Net.WebProxy?displayProperty=nameWithType>
- [<span data-ttu-id="45663-136">網路設定結構描述</span><span class="sxs-lookup"><span data-stu-id="45663-136">Network Settings Schema</span></span>](index.md)
