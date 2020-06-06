---
title: <smtp> 項目 (網路設定)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/mailSettings/smtp
- http://schemas.microsoft.com/.NetConfiguration/v2.0#smtp
helpviewer_keywords:
- <smtp> element
- smtp element
ms.assetid: 220b0329-e384-4e0c-86b4-0945ad17efd9
ms.openlocfilehash: 625c3cb82a8659c742b540724e5cf31be65a705e
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "74089105"
---
# <a name="smtp-element-network-settings"></a><span data-ttu-id="de64d-102">\<smtp> 項目 (網路設定)</span><span class="sxs-lookup"><span data-stu-id="de64d-102">\<smtp> Element (Network Settings)</span></span>
<span data-ttu-id="de64d-103">設定傳送電子郵件的傳遞格式、傳遞方法和寄件者位址。</span><span class="sxs-lookup"><span data-stu-id="de64d-103">Configures the delivery format, delivery method, and from address for sending emails.</span></span>  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<mailSettings>**](mailsettings-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<smtp>**
  
## <a name="syntax"></a><span data-ttu-id="de64d-104">語法</span><span class="sxs-lookup"><span data-stu-id="de64d-104">Syntax</span></span>  
  
```xml  
<smtp  
  deliveryFormat="format"  
  deliveryMethod="method"  
  from="from address">
    <specifiedPickupDirectory>...</specifiedPickupDirectory>  
    <network>...</network>  
</smtp>  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="de64d-105">屬性和項目</span><span class="sxs-lookup"><span data-stu-id="de64d-105">Attributes and Elements</span></span>  
 <span data-ttu-id="de64d-106">下列章節說明屬性、子元素和父元素。</span><span class="sxs-lookup"><span data-stu-id="de64d-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="de64d-107">屬性</span><span class="sxs-lookup"><span data-stu-id="de64d-107">Attributes</span></span>  
  
|<span data-ttu-id="de64d-108">屬性</span><span class="sxs-lookup"><span data-stu-id="de64d-108">Attribute</span></span>|<span data-ttu-id="de64d-109">描述</span><span class="sxs-lookup"><span data-stu-id="de64d-109">Description</span></span>|  
|---------------|-----------------|  
|`deliveryFormat`|<span data-ttu-id="de64d-110">指定外寄電子郵件的傳遞格式。</span><span class="sxs-lookup"><span data-stu-id="de64d-110">Specifies the delivery format for outgoing emails.</span></span> <span data-ttu-id="de64d-111">可接受的值為 SevenBit 和 International。</span><span class="sxs-lookup"><span data-stu-id="de64d-111">Acceptable values are SevenBit and International.</span></span>|  
|`deliveryMethod`|<span data-ttu-id="de64d-112">指定電子郵件的傳遞方法。</span><span class="sxs-lookup"><span data-stu-id="de64d-112">Specifies the delivery method for emails.</span></span> <span data-ttu-id="de64d-113">可接受的值為 Network、PickupDirectoryFromIis 和 SpecifiedPickupDirectory。</span><span class="sxs-lookup"><span data-stu-id="de64d-113">Acceptable values are Network, PickupDirectoryFromIis, and SpecifiedPickupDirectory.</span></span>|  
|`from`|<span data-ttu-id="de64d-114">指定外寄電子郵件的寄件者位址。</span><span class="sxs-lookup"><span data-stu-id="de64d-114">Specifies the from address for outgoing emails.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="de64d-115">子元素</span><span class="sxs-lookup"><span data-stu-id="de64d-115">Child Elements</span></span>  
  
|<span data-ttu-id="de64d-116">屬性</span><span class="sxs-lookup"><span data-stu-id="de64d-116">Attribute</span></span>|<span data-ttu-id="de64d-117">描述</span><span class="sxs-lookup"><span data-stu-id="de64d-117">Description</span></span>|  
|---------------|-----------------|  
|`specifiedPickupDirectory`|<span data-ttu-id="de64d-118">設定簡單郵件傳輸通訊協定（SMTP）伺服器的本機目錄。</span><span class="sxs-lookup"><span data-stu-id="de64d-118">Configures the local directory for a Simple Mail Transport Protocol (SMTP) server.</span></span>|  
|`network`|<span data-ttu-id="de64d-119">設定外部 SMTP 伺服器的網路選項。</span><span class="sxs-lookup"><span data-stu-id="de64d-119">Configures the network options for an external SMTP server.</span></span>|  
  
### <a name="parent-elements"></a><span data-ttu-id="de64d-120">父項目</span><span class="sxs-lookup"><span data-stu-id="de64d-120">Parent Elements</span></span>  
  
|<span data-ttu-id="de64d-121">**元素**</span><span class="sxs-lookup"><span data-stu-id="de64d-121">**Element**</span></span>|<span data-ttu-id="de64d-122">**說明**</span><span class="sxs-lookup"><span data-stu-id="de64d-122">**Description**</span></span>|  
|-----------------|---------------------|  
|[<span data-ttu-id="de64d-123">\<mailSettings>元素（網路設定）</span><span class="sxs-lookup"><span data-stu-id="de64d-123">\<mailSettings> Element (Network Settings)</span></span>](mailsettings-element-network-settings.md)|<span data-ttu-id="de64d-124">設定郵件傳送選項。</span><span class="sxs-lookup"><span data-stu-id="de64d-124">Configures mail sending options.</span></span>|  
  
## <a name="example"></a><span data-ttu-id="de64d-125">範例</span><span class="sxs-lookup"><span data-stu-id="de64d-125">Example</span></span>  
 <span data-ttu-id="de64d-126">下列範例會指定適當的 SMTP 參數，以使用預設網路認證來傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="de64d-126">The following example specifies the appropriate SMTP parameters to send email using the default network credentials.</span></span>  
  
```xml  
<configuration>  
  <system.net>  
    <mailSettings>  
      <smtp deliveryMethod="Network" deliveryFormat="SevenBit"  from="ben@contoso.com">  
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
  
## <a name="see-also"></a><span data-ttu-id="de64d-127">另請參閱</span><span class="sxs-lookup"><span data-stu-id="de64d-127">See also</span></span>

- <xref:System.Net.Configuration.SmtpSection?displayProperty=nameWithType>
- <xref:System.Net.Mail.SmtpClient?displayProperty=nameWithType>
- <xref:System.Net.Mail.SmtpDeliveryFormat>
- <xref:System.Net.Mail.SmtpDeliveryMethod>
- [<span data-ttu-id="de64d-128">網路設定結構描述</span><span class="sxs-lookup"><span data-stu-id="de64d-128">Network Settings Schema</span></span>](index.md)
