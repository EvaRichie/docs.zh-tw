---
title: <localClientSettings> 項目
ms.date: 03/30/2017
ms.assetid: 4680ace5-f4e1-4fcb-b9d8-a4a4af5cd7ae
ms.openlocfilehash: 3ec0394943c030a8866087c98a912682a2a2112e
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "70400313"
---
# <a name="localclientsettings-element"></a><span data-ttu-id="89c8a-102">\<localClientSettings> 項目</span><span class="sxs-lookup"><span data-stu-id="89c8a-102">\<localClientSettings> element</span></span>
<span data-ttu-id="89c8a-103">指定此繫結之本機用戶端的安全性設定。</span><span class="sxs-lookup"><span data-stu-id="89c8a-103">Specifies the security settings of a local client for this binding.</span></span>  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<customBinding>**](custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<binding>**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<security>**](security-of-custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<localClientSettings>**  
  
## <a name="syntax"></a><span data-ttu-id="89c8a-104">語法</span><span class="sxs-lookup"><span data-stu-id="89c8a-104">Syntax</span></span>  
  
```xml  
<security>
   <localClientSettings cacheCookies="Boolean"
                        cookieRenewalThresholdPercentage="Integer"
                        detectReplays="Boolean"
                        maxClockSkew="TimeSpan"
                        maxCookieCachingTime="TimeSpan"
                        reconnectTransportOnFailure="Boolean"
                        replayCacheSize="Integer"
                        replayWindow="TimeSpan"
                        sessionKeyRenewalInterval="TimeSpan"
                        sessionKeyRolloverInterval="TimeSpan"
                        timestampValidityDuration="TimeSpan" />
</security>
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="89c8a-105">屬性和項目</span><span class="sxs-lookup"><span data-stu-id="89c8a-105">Attributes and Elements</span></span>  
 <span data-ttu-id="89c8a-106">下列章節說明屬性、子元素和父元素。</span><span class="sxs-lookup"><span data-stu-id="89c8a-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="89c8a-107">屬性</span><span class="sxs-lookup"><span data-stu-id="89c8a-107">Attributes</span></span>  
  
|<span data-ttu-id="89c8a-108">屬性</span><span class="sxs-lookup"><span data-stu-id="89c8a-108">Attribute</span></span>|<span data-ttu-id="89c8a-109">描述</span><span class="sxs-lookup"><span data-stu-id="89c8a-109">Description</span></span>|  
|---------------|-----------------|  
|`cacheCookies`|<span data-ttu-id="89c8a-110">布林值，指定是否啟用 Cookie 快取。</span><span class="sxs-lookup"><span data-stu-id="89c8a-110">A Boolean value that specifies whether cookie caching is enabled.</span></span> <span data-ttu-id="89c8a-111">預設值為 `false`。</span><span class="sxs-lookup"><span data-stu-id="89c8a-111">The default is `false`.</span></span>|  
|`cookieRenewalThresholdPercentage`|<span data-ttu-id="89c8a-112">整數，指定可更新的 Cookie 百分比上限。</span><span class="sxs-lookup"><span data-stu-id="89c8a-112">An integer that specifies the maximum percentage of cookies that can be renewed.</span></span> <span data-ttu-id="89c8a-113">這個值應介於 0 到 100 之間 (含 0 和 100)。</span><span class="sxs-lookup"><span data-stu-id="89c8a-113">This value should be between 0 and 100 inclusively.</span></span> <span data-ttu-id="89c8a-114">預設值為 90。</span><span class="sxs-lookup"><span data-stu-id="89c8a-114">The default is 90.</span></span>|  
|`detectReplays`|<span data-ttu-id="89c8a-115">布林值，這個值會指定是否會偵測及自動處理對通道所發出的重新執行攻擊。</span><span class="sxs-lookup"><span data-stu-id="89c8a-115">A Boolean value that specifies whether replay attacks against the channel are detected and dealt with automatically.</span></span> <span data-ttu-id="89c8a-116">預設值為 `false`。</span><span class="sxs-lookup"><span data-stu-id="89c8a-116">The default is `false`.</span></span>|  
|`maxClockSkew`|<span data-ttu-id="89c8a-117"><xref:System.TimeSpan>，指定通訊雙方之系統時鐘之間的最大時間差異。</span><span class="sxs-lookup"><span data-stu-id="89c8a-117">A <xref:System.TimeSpan> that specifies the maximum time difference between the system clocks of the two communicating parties.</span></span> <span data-ttu-id="89c8a-118">預設值為 "00:05:00"。</span><span class="sxs-lookup"><span data-stu-id="89c8a-118">The default value is "00:05:00".</span></span><br /><br /> <span data-ttu-id="89c8a-119">當這個值設定為預設值時，接收者接受之訊息的傳送時間時間戳記會比收到訊息的時間早或晚 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="89c8a-119">When this value is set to the default, the receiver accepts messages with send-time time stamps up to 5 minutes later or earlier than the time the message was received.</span></span> <span data-ttu-id="89c8a-120">沒有通過傳送時間測試的訊息會遭到拒絕。</span><span class="sxs-lookup"><span data-stu-id="89c8a-120">Messages that do not pass the send-time test are rejected.</span></span> <span data-ttu-id="89c8a-121">這個設定會配合 `replayWindow` 屬性使用。</span><span class="sxs-lookup"><span data-stu-id="89c8a-121">This setting is used in conjunction with the `replayWindow` attribute.</span></span>|  
|`maxCookieCachingTime`|<span data-ttu-id="89c8a-122"><xref:System.TimeSpan>，指定 Cookie 的最長存留期。</span><span class="sxs-lookup"><span data-stu-id="89c8a-122">A <xref:System.TimeSpan> that specifies the maximum lifetime of cookies.</span></span> <span data-ttu-id="89c8a-123">預設值為 "10675199.02:48:05.4775807"。</span><span class="sxs-lookup"><span data-stu-id="89c8a-123">The default value is "10675199.02:48:05.4775807".</span></span>|  
|`reconnectTransportOnFailure`|<span data-ttu-id="89c8a-124">布林值，指定使用 WS-Reliable 訊息的連線是否會在傳輸失敗之後嘗試重新連線。</span><span class="sxs-lookup"><span data-stu-id="89c8a-124">A Boolean value that specifies whether connections using WS-Reliable messaging will attempt to reconnect after transport failures.</span></span> <span data-ttu-id="89c8a-125">預設為 `true`，表示無限次嘗試重新連線。</span><span class="sxs-lookup"><span data-stu-id="89c8a-125">The default is `true`, which means that infinite attempts to reconnect are attempted.</span></span> <span data-ttu-id="89c8a-126">無活動逾時會打破這個循環，而這樣會使得通道在無法重新連線時擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="89c8a-126">The cycle is broken by the inactivity time-out, which causes the channel to throw an exception when it cannot be reconnected.</span></span>|  
|`replayCacheSize`|<span data-ttu-id="89c8a-127">正整數，指定用於偵測重新執行攻擊之已快取 Nonce 數目。</span><span class="sxs-lookup"><span data-stu-id="89c8a-127">A positive integer that specifies the number of cached nonces used for replay detection.</span></span> <span data-ttu-id="89c8a-128">如果超過這個限制，便會移除最舊的 Nonce，然後為新訊息建立新的 Nonce。</span><span class="sxs-lookup"><span data-stu-id="89c8a-128">If this limit is exceeded, the oldest nonce is removed and a new nonce is created for the new message.</span></span> <span data-ttu-id="89c8a-129">預設值為 500000。</span><span class="sxs-lookup"><span data-stu-id="89c8a-129">The default value is 500000.</span></span>|  
|`replayWindow`|<span data-ttu-id="89c8a-130"><xref:System.TimeSpan>，指定個別訊息 Nonce 有效的持續期間。</span><span class="sxs-lookup"><span data-stu-id="89c8a-130">A <xref:System.TimeSpan> that specifies the duration in which individual message nonces are valid.</span></span><br /><br /> <span data-ttu-id="89c8a-131">過了這段時間後，將不會接受與先前所傳送之訊息擁有相同 Nonce 的訊息。</span><span class="sxs-lookup"><span data-stu-id="89c8a-131">After this duration, a message sent with the same nonce as the one sent before will not be accepted.</span></span> <span data-ttu-id="89c8a-132">這個屬性是配合 `maxClockSkew` 屬性使用，以防止重新執行攻擊。</span><span class="sxs-lookup"><span data-stu-id="89c8a-132">This attribute is used in conjunction with the `maxClockSkew` attribute to prevent replay attacks.</span></span> <span data-ttu-id="89c8a-133">攻擊者可以在重新執行視窗逾期之後重新執行訊息。</span><span class="sxs-lookup"><span data-stu-id="89c8a-133">An attacker could replay a message after its replay window has expired.</span></span> <span data-ttu-id="89c8a-134">然而，這個訊息無法通過 `maxClockSkew` 測試，因為它會拒絕傳送時間之時間戳記比收到訊息的時間早或晚的訊息。</span><span class="sxs-lookup"><span data-stu-id="89c8a-134">This message, however, would fail the `maxClockSkew` test which rejects messages with send-time timestamps up to a specified time later or earlier than the time the message was received.</span></span>|  
|`sessionKeyRenewalInterval`|<span data-ttu-id="89c8a-135">指定持續期間的 <xref:System.TimeSpan>，啟動器將在這段期間過後更新安全性工作階段的金鑰。</span><span class="sxs-lookup"><span data-stu-id="89c8a-135">A <xref:System.TimeSpan> that specifies the duration after which the initiator will renew the key for the security session.</span></span> <span data-ttu-id="89c8a-136">預設為 "10:00:00"。</span><span class="sxs-lookup"><span data-stu-id="89c8a-136">The default is "10:00:00".</span></span>|  
|`sessionKeyRolloverInterval`|<span data-ttu-id="89c8a-137"><xref:System.TimeSpan>，指定前一個工作階段金鑰在金鑰更新期間對傳入訊息屬有效的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="89c8a-137">A <xref:System.TimeSpan> that specifies the time interval a previous session key is valid on incoming messages during a key renewal.</span></span> <span data-ttu-id="89c8a-138">預設為 "00:05:00"。</span><span class="sxs-lookup"><span data-stu-id="89c8a-138">The default is "00:05:00".</span></span><br /><br /> <span data-ttu-id="89c8a-139">在金鑰更新之後，用戶端和伺服器都必須使用最新的可用金鑰來傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="89c8a-139">During key renewal, the client and server must always send messages using the most current available key.</span></span> <span data-ttu-id="89c8a-140">雙方都會接受由前一個工作階段金鑰保護的傳入訊息，直到變換時間逾期。</span><span class="sxs-lookup"><span data-stu-id="89c8a-140">Both parties will accept incoming messages secured with the previous session key until the rollover time expires.</span></span>|  
|`timestampValidityDuration`|<span data-ttu-id="89c8a-141">正的 <xref:System.TimeSpan>，指定時間戳記有效的持續期間。</span><span class="sxs-lookup"><span data-stu-id="89c8a-141">A positive <xref:System.TimeSpan> that specifies the duration in which a time stamp is valid.</span></span> <span data-ttu-id="89c8a-142">預設為 "00:15:00"。</span><span class="sxs-lookup"><span data-stu-id="89c8a-142">The default is "00:15:00".</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="89c8a-143">子元素</span><span class="sxs-lookup"><span data-stu-id="89c8a-143">Child Elements</span></span>  
 <span data-ttu-id="89c8a-144">無</span><span class="sxs-lookup"><span data-stu-id="89c8a-144">None</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="89c8a-145">父項目</span><span class="sxs-lookup"><span data-stu-id="89c8a-145">Parent Elements</span></span>  
  
|<span data-ttu-id="89c8a-146">元素</span><span class="sxs-lookup"><span data-stu-id="89c8a-146">Element</span></span>|<span data-ttu-id="89c8a-147">描述</span><span class="sxs-lookup"><span data-stu-id="89c8a-147">Description</span></span>|  
|-------------|-----------------|  
|[\<security>](security-of-custombinding.md)|<span data-ttu-id="89c8a-148">指定自訂繫結的安全性選項。</span><span class="sxs-lookup"><span data-stu-id="89c8a-148">Specifies the security options for a custom binding.</span></span>|  
|[\<secureConversationBootstrap>](secureconversationbootstrap.md)|<span data-ttu-id="89c8a-149">指定用於啟始安全對話服務的預設值。</span><span class="sxs-lookup"><span data-stu-id="89c8a-149">Specifies the default values used for initiating a secure conversation service.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="89c8a-150">備註</span><span class="sxs-lookup"><span data-stu-id="89c8a-150">Remarks</span></span>  
 <span data-ttu-id="89c8a-151">這些是本機設定，這意味著它們不是衍生自服務之安全性原則的設定。</span><span class="sxs-lookup"><span data-stu-id="89c8a-151">The settings are local in the sense that they are not settings derived from the security policy of the service.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="89c8a-152">另請參閱</span><span class="sxs-lookup"><span data-stu-id="89c8a-152">See also</span></span>

- <xref:System.ServiceModel.Configuration.LocalClientSecuritySettingsElement>
- <xref:System.ServiceModel.Configuration.SecurityElementBase.LocalClientSettings%2A>
- <xref:System.ServiceModel.Channels.SecurityBindingElement.LocalClientSettings%2A>
- <xref:System.ServiceModel.Channels.LocalClientSecuritySettings>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [<span data-ttu-id="89c8a-153">繫結</span><span class="sxs-lookup"><span data-stu-id="89c8a-153">Bindings</span></span>](../../../wcf/bindings.md)
- [<span data-ttu-id="89c8a-154">擴充繫結</span><span class="sxs-lookup"><span data-stu-id="89c8a-154">Extending Bindings</span></span>](../../../wcf/extending/extending-bindings.md)
- [<span data-ttu-id="89c8a-155">自訂繫結</span><span class="sxs-lookup"><span data-stu-id="89c8a-155">Custom Bindings</span></span>](../../../wcf/extending/custom-bindings.md)
- [\<customBinding>](custombinding.md)
- [<span data-ttu-id="89c8a-156">HOW TO：使用 SecurityBindingElement 建立自訂繫結</span><span class="sxs-lookup"><span data-stu-id="89c8a-156">How to: Create a Custom Binding Using the SecurityBindingElement</span></span>](../../../wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)
- [<span data-ttu-id="89c8a-157">自訂繫結安全性</span><span class="sxs-lookup"><span data-stu-id="89c8a-157">Custom Binding Security</span></span>](../../../wcf/samples/custom-binding-security.md)
