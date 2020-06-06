---
title: <mailSettings> 項目 (網路設定)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#mailSettings
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/mailSettings
helpviewer_keywords:
- mailSettings element
- <mailSettings> element
ms.assetid: 54f0f153-17e5-4f49-afdc-deadb940c9c1
ms.openlocfilehash: 4e8bf23ce39edadf80f019315c690b597b3d7361
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "74089224"
---
# <a name="mailsettings-element-network-settings"></a><span data-ttu-id="240d2-102">\<mailSettings> 項目 (網路設定)</span><span class="sxs-lookup"><span data-stu-id="240d2-102">\<mailSettings> Element (Network Settings)</span></span>
<span data-ttu-id="240d2-103">設定郵件傳送選項。</span><span class="sxs-lookup"><span data-stu-id="240d2-103">Configures mail sending options.</span></span>  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<mailSettings>**

## <a name="syntax"></a><span data-ttu-id="240d2-104">語法</span><span class="sxs-lookup"><span data-stu-id="240d2-104">Syntax</span></span>  
  
```xml  
<mailSettings>
  <smtp>...</smtp>  
</mailSettings>
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="240d2-105">屬性和項目</span><span class="sxs-lookup"><span data-stu-id="240d2-105">Attributes and Elements</span></span>  
 <span data-ttu-id="240d2-106">下列章節說明屬性、子元素和父元素。</span><span class="sxs-lookup"><span data-stu-id="240d2-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="240d2-107">屬性</span><span class="sxs-lookup"><span data-stu-id="240d2-107">Attributes</span></span>  
 <span data-ttu-id="240d2-108">無。</span><span class="sxs-lookup"><span data-stu-id="240d2-108">None.</span></span>  
  
### <a name="child-elements"></a><span data-ttu-id="240d2-109">子元素</span><span class="sxs-lookup"><span data-stu-id="240d2-109">Child Elements</span></span>  
  
|<span data-ttu-id="240d2-110">屬性</span><span class="sxs-lookup"><span data-stu-id="240d2-110">Attribute</span></span>|<span data-ttu-id="240d2-111">描述</span><span class="sxs-lookup"><span data-stu-id="240d2-111">Description</span></span>|  
|---------------|-----------------|  
|[<span data-ttu-id="240d2-112">\<smtp>元素（網路設定）</span><span class="sxs-lookup"><span data-stu-id="240d2-112">\<smtp> Element (Network Settings)</span></span>](smtp-element-network-settings.md)|<span data-ttu-id="240d2-113">設定簡單郵件傳輸通訊協定選項。</span><span class="sxs-lookup"><span data-stu-id="240d2-113">Configures Simple Mail Transport Protocol options.</span></span>|  
  
### <a name="parent-elements"></a><span data-ttu-id="240d2-114">父項目</span><span class="sxs-lookup"><span data-stu-id="240d2-114">Parent Elements</span></span>  
  
|<span data-ttu-id="240d2-115">**元素**</span><span class="sxs-lookup"><span data-stu-id="240d2-115">**Element**</span></span>|<span data-ttu-id="240d2-116">**說明**</span><span class="sxs-lookup"><span data-stu-id="240d2-116">**Description**</span></span>|  
|-----------------|---------------------|  
|[<span data-ttu-id="240d2-117">\<system.Net>元素（網路設定）</span><span class="sxs-lookup"><span data-stu-id="240d2-117">\<system.Net> Element (Network Settings)</span></span>](system-net-element-network-settings.md)|<span data-ttu-id="240d2-118">包含會指定 .NET Framework 如何連接至網路的設定。</span><span class="sxs-lookup"><span data-stu-id="240d2-118">Contains settings that specify how the .NET Framework connects to the network.</span></span>|  
  
## <a name="example"></a><span data-ttu-id="240d2-119">範例</span><span class="sxs-lookup"><span data-stu-id="240d2-119">Example</span></span>  
 <span data-ttu-id="240d2-120">下列範例會指定適當的 SMTP 參數，以使用預設網路認證來傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="240d2-120">The following example specifies the appropriate SMTP parameters to send email using the default network credentials.</span></span>  
  
```xml  
<configuration>  
  <system.net>  
    <mailSettings>  
      <smtp deliveryMethod="Network">  
        <network  
          host="localhost"  
          port="25"  
          defaultCredentials="true"  
        />  
      </smtp>  
    </mailSettings>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a><span data-ttu-id="240d2-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="240d2-121">See also</span></span>

- <xref:System.Net.Mail.SmtpClient>
- [<span data-ttu-id="240d2-122">網路設定結構描述</span><span class="sxs-lookup"><span data-stu-id="240d2-122">Network Settings Schema</span></span>](index.md)
