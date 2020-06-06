---
title: webRequestModules 的 <remove> 項目 (網路設定)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/webRequestModules/remove
- http://schemas.microsoft.com/.NetConfiguration/v2.0#remove
helpviewer_keywords:
- remove element, webRequestModules
- webRequestModules, remove element
- <remove> element, webRequestModules
- <webRequestModules>, remove element
ms.assetid: dd84d2fe-2f4f-457a-9d3c-441d0d21cc10
ms.openlocfilehash: afa1aef8ea71f43a136987ec5b6e1925c6d9fb40
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "79154721"
---
# <a name="remove-element-for-webrequestmodules-network-settings"></a><span data-ttu-id="9f900-102">webRequestModules 的 \<remove> 項目 (網路設定)</span><span class="sxs-lookup"><span data-stu-id="9f900-102">\<remove> Element for webRequestModules (Network Settings)</span></span>
<span data-ttu-id="9f900-103">從應用程式中移除自訂 Web 要求模組。</span><span class="sxs-lookup"><span data-stu-id="9f900-103">Removes a custom Web request module from the application.</span></span>  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<webRequestModules>**](webrequestmodules-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<remove>**
  
## <a name="syntax"></a><span data-ttu-id="9f900-104">語法</span><span class="sxs-lookup"><span data-stu-id="9f900-104">Syntax</span></span>  
  
```xml  
<remove
  prefix="URI prefix"
/>  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="9f900-105">屬性和項目</span><span class="sxs-lookup"><span data-stu-id="9f900-105">Attributes and Elements</span></span>  
 <span data-ttu-id="9f900-106">下列章節說明屬性、子元素和父元素。</span><span class="sxs-lookup"><span data-stu-id="9f900-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="9f900-107">屬性</span><span class="sxs-lookup"><span data-stu-id="9f900-107">Attributes</span></span>  
  
|<span data-ttu-id="9f900-108">**屬性**</span><span class="sxs-lookup"><span data-stu-id="9f900-108">**Attribute**</span></span>|<span data-ttu-id="9f900-109">**說明**</span><span class="sxs-lookup"><span data-stu-id="9f900-109">**Description**</span></span>|  
|-------------------|---------------------|  
|`prefix`|<span data-ttu-id="9f900-110">此 Web 要求模組所處理之要求的 URI 前置詞。</span><span class="sxs-lookup"><span data-stu-id="9f900-110">The URI prefix for requests handled by this Web request module.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="9f900-111">子元素</span><span class="sxs-lookup"><span data-stu-id="9f900-111">Child Elements</span></span>  
 <span data-ttu-id="9f900-112">無。</span><span class="sxs-lookup"><span data-stu-id="9f900-112">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="9f900-113">父項目</span><span class="sxs-lookup"><span data-stu-id="9f900-113">Parent Elements</span></span>  
  
|<span data-ttu-id="9f900-114">**元素**</span><span class="sxs-lookup"><span data-stu-id="9f900-114">**Element**</span></span>|<span data-ttu-id="9f900-115">**說明**</span><span class="sxs-lookup"><span data-stu-id="9f900-115">**Description**</span></span>|  
|-----------------|---------------------|  
|[<span data-ttu-id="9f900-116">webRequestModules</span><span class="sxs-lookup"><span data-stu-id="9f900-116">webRequestModules</span></span>](webrequestmodules-element-network-settings.md)|<span data-ttu-id="9f900-117">指定要用來要求網路主機資訊的模組。</span><span class="sxs-lookup"><span data-stu-id="9f900-117">Specifies modules to use to request information from network hosts.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="9f900-118">備註</span><span class="sxs-lookup"><span data-stu-id="9f900-118">Remarks</span></span>  
 <span data-ttu-id="9f900-119">`remove`元素會移除所指定 URI 前置詞的已註冊 Web 要求模組。</span><span class="sxs-lookup"><span data-stu-id="9f900-119">The `remove` element removes the registered Web request module for the specified URI prefix.</span></span>  
  
 <span data-ttu-id="9f900-120">屬性的值 `prefix` 應該是有效 URI 的前置字元，例如 " `http` " 或 " `http://www.contoso.com` "。</span><span class="sxs-lookup"><span data-stu-id="9f900-120">The value for the `prefix` attribute should be the leading characters of a valid URI -- for example, "`http`", or "`http://www.contoso.com`".</span></span>  
  
## <a name="configuration-files"></a><span data-ttu-id="9f900-121">組態檔</span><span class="sxs-lookup"><span data-stu-id="9f900-121">Configuration Files</span></span>  
 <span data-ttu-id="9f900-122">此項目可以用於應用程式組態檔或電腦組態檔 (Machine.config)。</span><span class="sxs-lookup"><span data-stu-id="9f900-122">This element can be used in the application configuration file or the machine configuration file (Machine.config).</span></span>  
  
## <a name="example"></a><span data-ttu-id="9f900-123">範例</span><span class="sxs-lookup"><span data-stu-id="9f900-123">Example</span></span>  

<span data-ttu-id="9f900-124">下列範例會移除 HTTP 的現有 Web 要求模組，然後針對 HTTP 要求註冊新的自訂 Web 要求模組 `www.contoso.com` 。</span><span class="sxs-lookup"><span data-stu-id="9f900-124">The following example removes the existing Web request module for HTTP and then registers a new custom Web request module for HTTP requests to `www.contoso.com`.</span></span>
  
```xml  
<configuration>  
  <system.net>  
    <webRequestModules>  
      <remove prefix="http">  
      <add prefix="http"  
           type="System.Net.HttpRequestCreator, System, Version=2.0.3600.0,  
           Culture=neutral, PublicKeyToken=b77a5c561934e089"  
      />  
    </webRequestModules>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a><span data-ttu-id="9f900-125">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9f900-125">See also</span></span>

- <xref:System.Net.WebRequest>
- [<span data-ttu-id="9f900-126">網路設定結構描述</span><span class="sxs-lookup"><span data-stu-id="9f900-126">Network Settings Schema</span></span>](index.md)
