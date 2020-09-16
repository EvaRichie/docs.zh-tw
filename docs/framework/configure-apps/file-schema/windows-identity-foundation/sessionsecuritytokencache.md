---
title: <sessionSecurityTokenCache>
ms.date: 03/30/2017
ms.assetid: d43e676c-0153-485c-ab31-0257a2db7507
author: BrucePerlerMS
ms.openlocfilehash: 4169fe307e9ef7c391500a2292fcc247f435caa9
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90555883"
---
# \<sessionSecurityTokenCache>
<span data-ttu-id="738d0-101">使用服務或安全性權杖處理常式集合來註冊會話權杖的快取。</span><span class="sxs-lookup"><span data-stu-id="738d0-101">Registers a cache for session tokens with a service or a security token handler collection.</span></span>  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.identityModel>**](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<identityConfiguration>**](identityconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<caches>**](caches.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<sessionSecurityTokenCache>**  
  
## <a name="syntax"></a><span data-ttu-id="738d0-102">語法</span><span class="sxs-lookup"><span data-stu-id="738d0-102">Syntax</span></span>  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <caches>  
      <sessionSecurityTokenCache type=xs:string>  
      </sessionSecurityTokenCache>  
    </caches>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="738d0-103">屬性和項目</span><span class="sxs-lookup"><span data-stu-id="738d0-103">Attributes and Elements</span></span>  
 <span data-ttu-id="738d0-104">下列章節說明屬性、子元素和父元素。</span><span class="sxs-lookup"><span data-stu-id="738d0-104">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="738d0-105">屬性</span><span class="sxs-lookup"><span data-stu-id="738d0-105">Attributes</span></span>  
  
|<span data-ttu-id="738d0-106">屬性</span><span class="sxs-lookup"><span data-stu-id="738d0-106">Attribute</span></span>|<span data-ttu-id="738d0-107">描述</span><span class="sxs-lookup"><span data-stu-id="738d0-107">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="738d0-108">type</span><span class="sxs-lookup"><span data-stu-id="738d0-108">type</span></span>|<span data-ttu-id="738d0-109">衍生自類別的型別 <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache> 。</span><span class="sxs-lookup"><span data-stu-id="738d0-109">A type that derives from the <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache> class.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="738d0-110">子元素</span><span class="sxs-lookup"><span data-stu-id="738d0-110">Child Elements</span></span>  
 <span data-ttu-id="738d0-111">None</span><span class="sxs-lookup"><span data-stu-id="738d0-111">None</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="738d0-112">父項目</span><span class="sxs-lookup"><span data-stu-id="738d0-112">Parent Elements</span></span>  
  
|<span data-ttu-id="738d0-113">項目</span><span class="sxs-lookup"><span data-stu-id="738d0-113">Element</span></span>|<span data-ttu-id="738d0-114">描述</span><span class="sxs-lookup"><span data-stu-id="738d0-114">Description</span></span>|  
|-------------|-----------------|  
|[\<caches>](caches.md)|<span data-ttu-id="738d0-115">註冊服務或安全性權杖處理常式集合所使用的快取。</span><span class="sxs-lookup"><span data-stu-id="738d0-115">Registers the caches used by a service or a security token handler collection.</span></span>|  
  
## <a name="example"></a><span data-ttu-id="738d0-116">範例</span><span class="sxs-lookup"><span data-stu-id="738d0-116">Example</span></span>  
 <span data-ttu-id="738d0-117">下列 XML 會顯示 () 保存會話安全性權杖的自訂快取設定 <xref:System.IdentityModel.Tokens.SessionSecurityToken> 。</span><span class="sxs-lookup"><span data-stu-id="738d0-117">The following XML shows the configuration of a custom cache for holding session security tokens (<xref:System.IdentityModel.Tokens.SessionSecurityToken>).</span></span> <span data-ttu-id="738d0-118">設定取自 `ClaimsAwareWebFarm` 範例。</span><span class="sxs-lookup"><span data-stu-id="738d0-118">The configuration is taken from the `ClaimsAwareWebFarm` sample.</span></span> <span data-ttu-id="738d0-119">如需此範例的詳細資訊，請參閱 [WIF 程式碼範例索引](/previous-versions/dotnet/framework/security/wif-code-sample-index)。</span><span class="sxs-lookup"><span data-stu-id="738d0-119">For more information about this sample, see [WIF Code Sample Index](/previous-versions/dotnet/framework/security/wif-code-sample-index).</span></span>  
  
```xml  
<caches>  
  <sessionSecurityTokenCache type="CacheLibrary.SharedSessionSecurityTokenCache, CacheLibrary">  
    <!--cacheServiceAddress points to the centralized session security token cache service running in the web farm.-->  
    <cacheServiceAddress url="http://localhost:4161/SessionSecurityTokenCacheService.svc" />  
  </sessionSecurityTokenCache>  
</caches>  
```  
  
## <a name="see-also"></a><span data-ttu-id="738d0-120">另請參閱</span><span class="sxs-lookup"><span data-stu-id="738d0-120">See also</span></span>

- <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache>
