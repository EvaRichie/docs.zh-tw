---
title: <localServiceSettings> 項目
ms.date: 03/30/2017
ms.assetid: 0658549c-3f65-46dd-8c5c-9895441ed734
ms.openlocfilehash: 3043c07afd316d90cc5525a67bef144f33d9b136
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91204927"
---
# <a name="localservicesettings-element"></a><span data-ttu-id="4a200-102">\<localServiceSettings> 項目</span><span class="sxs-lookup"><span data-stu-id="4a200-102">\<localServiceSettings> element</span></span>

<span data-ttu-id="4a200-103">指定此繫結之本機服務的安全性設定。</span><span class="sxs-lookup"><span data-stu-id="4a200-103">Specifies the security settings of a local service for this binding.</span></span>  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<customBinding>**](custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<binding>**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<security>**](security-of-custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<localServiceSettings>**  
  
## <a name="syntax"></a><span data-ttu-id="4a200-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="4a200-104">Syntax</span></span>  
  
```xml  
<security>
  <localServiceSettings detectReplays="Boolean"
                        inactivityTimeout="TimeSpan"
                        issuedCookieLifeTime="TimeSpan"
                        maxCachedCookies="Integer"
                        maxClockSkew="TimeSpan"
                        maxPendingSessions="Integer"
                        maxStatefulNegotiations="Integer"
                        negotiationTimeout="TimeSpan"
                        reconnectTransportOnFailure="Boolean"
                        replayCacheSize="Integer"
                        replayWindow="TimeSpan"
                        sessionKeyRenewalInterval="TimeSpan"
                        sessionKeyRolloverInterval="TimeSpan"
                        timestampValidityDuration="TimeSpan" />
</security>
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="4a200-105">屬性和項目</span><span class="sxs-lookup"><span data-stu-id="4a200-105">Attributes and Elements</span></span>  

 <span data-ttu-id="4a200-106">下列章節說明屬性、子元素和父元素。</span><span class="sxs-lookup"><span data-stu-id="4a200-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="4a200-107">屬性</span><span class="sxs-lookup"><span data-stu-id="4a200-107">Attributes</span></span>  
  
|<span data-ttu-id="4a200-108">屬性</span><span class="sxs-lookup"><span data-stu-id="4a200-108">Attribute</span></span>|<span data-ttu-id="4a200-109">描述</span><span class="sxs-lookup"><span data-stu-id="4a200-109">Description</span></span>|  
|---------------|-----------------|  
|`detectReplays`|<span data-ttu-id="4a200-110">布林值，這個值會指定是否會偵測及自動處理對通道所發出的重新執行攻擊。</span><span class="sxs-lookup"><span data-stu-id="4a200-110">A Boolean value that specifies whether replay attacks against the channel are detected and dealt with automatically.</span></span> <span data-ttu-id="4a200-111">預設值為 `false`。</span><span class="sxs-lookup"><span data-stu-id="4a200-111">The default is `false`.</span></span>|  
|`inactivityTimeout`|<span data-ttu-id="4a200-112">正數 <xref:System.TimeSpan> ，指定通道在經過一段時間後等待的非使用狀態。預設值為 "01:00:00"。</span><span class="sxs-lookup"><span data-stu-id="4a200-112">A positive <xref:System.TimeSpan> that specifies the duration of inactivity the channel waits before it times out. The default is "01:00:00".</span></span>|  
|`issuedCookieLifeTime`|<span data-ttu-id="4a200-113"><xref:System.TimeSpan>，指定發出給所有新的安全性 Cookie 的存留期。</span><span class="sxs-lookup"><span data-stu-id="4a200-113">A <xref:System.TimeSpan> that specifies the lifetime issued to all new security cookies.</span></span> <span data-ttu-id="4a200-114">超過存留期的 Cookie 會回收，而且必須再次交涉。</span><span class="sxs-lookup"><span data-stu-id="4a200-114">Cookies that exceed their lifetime are recycled and need to be negotiated again.</span></span> <span data-ttu-id="4a200-115">預設值為 "10:00:00"。</span><span class="sxs-lookup"><span data-stu-id="4a200-115">The default value is "10:00:00".</span></span>|  
|`maxCachedCookies`|<span data-ttu-id="4a200-116">正整數，這個值會指定可以快取的 Cookie 數目上限。</span><span class="sxs-lookup"><span data-stu-id="4a200-116">A positive integer that specifies the maximum number of cookies that can be cached.</span></span> <span data-ttu-id="4a200-117">預設值是 1000。</span><span class="sxs-lookup"><span data-stu-id="4a200-117">The default is 1000.</span></span>|  
|`maxClockSkew`|<span data-ttu-id="4a200-118"><xref:System.TimeSpan>，指定通訊雙方之系統時鐘之間的最大時間差異。</span><span class="sxs-lookup"><span data-stu-id="4a200-118">A <xref:System.TimeSpan> that specifies the maximum time difference between the system clocks of the two communicating parties.</span></span> <span data-ttu-id="4a200-119">預設值為 "00:05:00"。</span><span class="sxs-lookup"><span data-stu-id="4a200-119">The default value is "00:05:00".</span></span><br /><br /> <span data-ttu-id="4a200-120">當這個值設定為預設值時，接收者接受之訊息的傳送時間時間戳記會比收到訊息的時間早或晚 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="4a200-120">When this value is set to the default, the receiver accepts messages with send-time time stamps up to 5 minutes later or earlier than the time the message was received.</span></span> <span data-ttu-id="4a200-121">沒有通過傳送時間測試的訊息會遭到拒絕。</span><span class="sxs-lookup"><span data-stu-id="4a200-121">Messages that do not pass the send-time test are rejected.</span></span> <span data-ttu-id="4a200-122">這個設定會配合 `replayWindow` 屬性使用。</span><span class="sxs-lookup"><span data-stu-id="4a200-122">This setting is used in conjunction with the `replayWindow` attribute.</span></span>|  
|`maxPendingSessions`|<span data-ttu-id="4a200-123">正整數，這個值會指定服務支援之擱置中安全性工作階段數目上限。</span><span class="sxs-lookup"><span data-stu-id="4a200-123">A positive integer that specifies the maximum number of pending security sessions that the service supports.</span></span> <span data-ttu-id="4a200-124">當達到這個限制時，所有新的用戶端都會收到 SOAP 錯誤。</span><span class="sxs-lookup"><span data-stu-id="4a200-124">When this limit is reached, all new clients receive SOAP faults.</span></span> <span data-ttu-id="4a200-125">預設值為 1000。</span><span class="sxs-lookup"><span data-stu-id="4a200-125">The default value is 1000.</span></span>|  
|`maxStatefulNegotiations`|<span data-ttu-id="4a200-126">正整數，這個值會指定可以同時為作用中的安全性交涉數目。</span><span class="sxs-lookup"><span data-stu-id="4a200-126">A positive integer that specifies the number of security negotiations that can be active concurrently.</span></span> <span data-ttu-id="4a200-127">超過限制的交涉工作階段會排入佇列，而且只有在低於限制的空間可供使用時才能完成。</span><span class="sxs-lookup"><span data-stu-id="4a200-127">Negotiation sessions in excess of the limit are queued and can only be completed when a space below the limit becomes available.</span></span> <span data-ttu-id="4a200-128">預設值為 1024。</span><span class="sxs-lookup"><span data-stu-id="4a200-128">The default value is 1024.</span></span>|  
|`negotiationTimeout`|<span data-ttu-id="4a200-129"><xref:System.TimeSpan>，指定通道所使用之安全性原則的存留期。</span><span class="sxs-lookup"><span data-stu-id="4a200-129">A <xref:System.TimeSpan> that specifies the lifetime of the security policy used by channel.</span></span> <span data-ttu-id="4a200-130">超過此時間時，通道會與用戶端重新交涉新安全性原則。</span><span class="sxs-lookup"><span data-stu-id="4a200-130">When the time expires, the channel renegotiates with the client for a new security policy.</span></span> <span data-ttu-id="4a200-131">預設值為 "00:02:00"。</span><span class="sxs-lookup"><span data-stu-id="4a200-131">The default value is "00:02:00".</span></span>|  
|`reconnectTransportOnFailure`|<span data-ttu-id="4a200-132">布林值，指定使用 WS-Reliable 訊息的連線是否會在傳輸失敗之後嘗試重新連線。</span><span class="sxs-lookup"><span data-stu-id="4a200-132">A Boolean value that specifies whether connections using WS-Reliable messaging will attempt to reconnect after transport failures.</span></span> <span data-ttu-id="4a200-133">預設為 `true`，表示無限次嘗試重新連線。</span><span class="sxs-lookup"><span data-stu-id="4a200-133">The default is `true`, which means that infinite attempts to reconnect are attempted.</span></span> <span data-ttu-id="4a200-134">無活動逾時會打破這個循環，而這樣會使得通道在無法重新連線時擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="4a200-134">The cycle is broken by the inactivity time-out, which causes the channel to throw an exception when it cannot be reconnected.</span></span>|  
|`replayCacheSize`|<span data-ttu-id="4a200-135">正整數，指定用於偵測重新執行攻擊之已快取 Nonce 數目。</span><span class="sxs-lookup"><span data-stu-id="4a200-135">A positive integer that specifies the number of cached nonces used for replay detection.</span></span> <span data-ttu-id="4a200-136">如果超過這個限制，便會移除最舊的 Nonce，然後為新訊息建立新的 Nonce。</span><span class="sxs-lookup"><span data-stu-id="4a200-136">If this limit is exceeded, the oldest nonce is removed and a new nonce is created for the new message.</span></span> <span data-ttu-id="4a200-137">預設值為 500000。</span><span class="sxs-lookup"><span data-stu-id="4a200-137">The default value is 500000.</span></span>|  
|`replayWindow`|<span data-ttu-id="4a200-138"><xref:System.TimeSpan>，指定個別訊息 Nonce 有效的持續期間。</span><span class="sxs-lookup"><span data-stu-id="4a200-138">A <xref:System.TimeSpan> that specifies the duration in which individual message nonces are valid.</span></span><br /><br /> <span data-ttu-id="4a200-139">過了這段時間後，將不會接受與先前所傳送之訊息擁有相同 Nonce 的訊息。</span><span class="sxs-lookup"><span data-stu-id="4a200-139">After this duration, a message sent with the same nonce as the one sent before will not be accepted.</span></span> <span data-ttu-id="4a200-140">這個屬性是配合 `maxClockSkew` 屬性使用，以防止重新執行攻擊。</span><span class="sxs-lookup"><span data-stu-id="4a200-140">This attribute is used in conjunction with the `maxClockSkew` attribute to prevent replay attacks.</span></span> <span data-ttu-id="4a200-141">攻擊者可以在重新執行視窗逾期之後重新執行訊息。</span><span class="sxs-lookup"><span data-stu-id="4a200-141">An attacker could replay a message after its replay window has expired.</span></span> <span data-ttu-id="4a200-142">然而，這個訊息無法通過 `maxClockSkew` 測試，因為它會拒絕傳送時間之時間戳記比收到訊息的時間早或晚的訊息。</span><span class="sxs-lookup"><span data-stu-id="4a200-142">This message, however, would fail the `maxClockSkew` test which rejects messages with send-time timestamps up to a specified time later or earlier than the time the message was received.</span></span>|  
|`sessionKeyRenewalInterval`|<span data-ttu-id="4a200-143">指定持續期間的 <xref:System.TimeSpan>，啟動器將在這段期間過後更新安全性工作階段的金鑰。</span><span class="sxs-lookup"><span data-stu-id="4a200-143">A <xref:System.TimeSpan> that specifies the duration after which the initiator will renew the key for the security session.</span></span> <span data-ttu-id="4a200-144">預設為 "10:00:00"。</span><span class="sxs-lookup"><span data-stu-id="4a200-144">The default is "10:00:00".</span></span>|  
|`sessionKeyRolloverInterval`|<span data-ttu-id="4a200-145"><xref:System.TimeSpan>，指定前一個工作階段金鑰在金鑰更新期間對傳入訊息屬有效的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="4a200-145">A <xref:System.TimeSpan> that specifies the time interval a previous session key is valid on incoming messages during a key renewal.</span></span> <span data-ttu-id="4a200-146">預設為 "00:05:00"。</span><span class="sxs-lookup"><span data-stu-id="4a200-146">The default is "00:05:00".</span></span><br /><br /> <span data-ttu-id="4a200-147">在金鑰更新之後，用戶端和伺服器都必須使用最新的可用金鑰來傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="4a200-147">During key renewal, the client and server must always send messages using the most current available key.</span></span> <span data-ttu-id="4a200-148">雙方都會接受由前一個工作階段金鑰保護的傳入訊息，直到變換時間逾期。</span><span class="sxs-lookup"><span data-stu-id="4a200-148">Both parties will accept incoming messages secured with the previous session key until the rollover time expires.</span></span>|  
|`timestampValidityDuration`|<span data-ttu-id="4a200-149">正的 <xref:System.TimeSpan>，指定時間戳記有效的持續期間。</span><span class="sxs-lookup"><span data-stu-id="4a200-149">A positive <xref:System.TimeSpan> that specifies the duration in which a time stamp is valid.</span></span> <span data-ttu-id="4a200-150">預設為 "00:15:00"。</span><span class="sxs-lookup"><span data-stu-id="4a200-150">The default is "00:15:00".</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="4a200-151">子元素</span><span class="sxs-lookup"><span data-stu-id="4a200-151">Child Elements</span></span>  

 <span data-ttu-id="4a200-152">無。</span><span class="sxs-lookup"><span data-stu-id="4a200-152">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="4a200-153">父項目</span><span class="sxs-lookup"><span data-stu-id="4a200-153">Parent Elements</span></span>  
  
|<span data-ttu-id="4a200-154">項目</span><span class="sxs-lookup"><span data-stu-id="4a200-154">Element</span></span>|<span data-ttu-id="4a200-155">描述</span><span class="sxs-lookup"><span data-stu-id="4a200-155">Description</span></span>|  
|-------------|-----------------|  
|[\<security>](security-of-custombinding.md)|<span data-ttu-id="4a200-156">指定自訂繫結的安全性選項。</span><span class="sxs-lookup"><span data-stu-id="4a200-156">Specifies the security options for a custom binding.</span></span>|  
|[\<secureConversationBootstrap>](secureconversationbootstrap.md)|<span data-ttu-id="4a200-157">指定用於啟始安全對話服務的預設值。</span><span class="sxs-lookup"><span data-stu-id="4a200-157">Specifies the default values used for initiating a secure conversation service.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="4a200-158">備註</span><span class="sxs-lookup"><span data-stu-id="4a200-158">Remarks</span></span>  

 <span data-ttu-id="4a200-159">這些是本機設定，因為它們並未發行成為服務之安全性原則的一部分，因此不會影響用戶端的繫結。</span><span class="sxs-lookup"><span data-stu-id="4a200-159">The settings are local because they are not published as part of the security policy of the service and do not affect the client's binding.</span></span>  
  
 <span data-ttu-id="4a200-160">`localServiceSecuritySettings` 項目的下列屬性有助於降低阻絕服務 (DOS) 安全性攻擊：</span><span class="sxs-lookup"><span data-stu-id="4a200-160">The following attributes of the `localServiceSecuritySettings` element can help mitigate a denial-of-service (DOS) security attack:</span></span>  
  
- <span data-ttu-id="4a200-161">`maxCachedCookies`：控制在執行 SPNEGO 或 SSL 交涉之後，伺服器所快取有時間界限之 SecurityContextToken 的上限。</span><span class="sxs-lookup"><span data-stu-id="4a200-161">`maxCachedCookies`: controls the maximum number of time-bounded SecurityContextTokens that are cached by the server after doing SPNEGO or SSL negotiation.</span></span>  
  
- <span data-ttu-id="4a200-162">`issuedCookieLifetime`：控制在 SPNEGO 或 SSL 交涉之後，伺服器所發出的 SecurityContextToken 的存留期 (Lifetime)。</span><span class="sxs-lookup"><span data-stu-id="4a200-162">`issuedCookieLifetime`: controls the lifetime of the SecurityContextTokens that are issued by the server following SPNEGO or SSL negotiation.</span></span> <span data-ttu-id="4a200-163">伺服器會在這段時間內快取 SecurityContextToken。</span><span class="sxs-lookup"><span data-stu-id="4a200-163">The server caches the SecurityContextTokens for this period of time.</span></span>  
  
- <span data-ttu-id="4a200-164">`maxPendingSessions`：控制在伺服器中建立的安全對話上限，但是不會針對這些對話處理應用程式訊息。</span><span class="sxs-lookup"><span data-stu-id="4a200-164">`maxPendingSessions`: controls the maximum number of secure conversations that are established at the server but for which no application messages have been processed.</span></span> <span data-ttu-id="4a200-165">這個配額會防止用戶端在服務中建立安全對話，由此服務會針對每個用戶端保留對話狀態，但不會使用這些對話。</span><span class="sxs-lookup"><span data-stu-id="4a200-165">This quota prevents clients from establishing secure conversations at the service, thereby causing the service to maintain state for each client, but never using them.</span></span>  
  
- <span data-ttu-id="4a200-166">`inactivityTimeout`：控制服務讓安全對話保持運作，而不會從中接收應用程式訊息的時間上限。</span><span class="sxs-lookup"><span data-stu-id="4a200-166">`inactivityTimeout`: controls the maximum time that the service keeps a secure conversation alive without ever receiving an application message on it.</span></span> <span data-ttu-id="4a200-167">這個配額會防止用戶端在服務中建立安全對話，由此服務會針對每個用戶端保留對話狀態，但不會使用這些對話。</span><span class="sxs-lookup"><span data-stu-id="4a200-167">This quota prevents clients from establishing secure conversations at the service, thereby causing the service to maintain state for each client, but never using them.</span></span>  
  
 <span data-ttu-id="4a200-168">在安全對話工作階段中，請注意繫結上的 `inactivityTimeout` 和 `receiveTimeout` 屬性都會影響工作階段逾時。</span><span class="sxs-lookup"><span data-stu-id="4a200-168">In a secure conversation session, note that both `inactivityTimeout` and the `receiveTimeout` attributes on the binding affect session timeout.</span></span> <span data-ttu-id="4a200-169">其中時間較短的屬性值會決定逾時發生的時間。</span><span class="sxs-lookup"><span data-stu-id="4a200-169">The shorter of the two determines when timeouts occur.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="4a200-170">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4a200-170">See also</span></span>

- <xref:System.ServiceModel.Configuration.LocalServiceSecuritySettingsElement>
- <xref:System.ServiceModel.Configuration.SecurityElementBase.LocalServiceSettings%2A>
- <xref:System.ServiceModel.Channels.SecurityBindingElement.LocalServiceSettings%2A>
- <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [<span data-ttu-id="4a200-171">繫結</span><span class="sxs-lookup"><span data-stu-id="4a200-171">Bindings</span></span>](../../../wcf/bindings.md)
- [<span data-ttu-id="4a200-172">擴充繫結</span><span class="sxs-lookup"><span data-stu-id="4a200-172">Extending Bindings</span></span>](../../../wcf/extending/extending-bindings.md)
- [<span data-ttu-id="4a200-173">自訂繫結</span><span class="sxs-lookup"><span data-stu-id="4a200-173">Custom Bindings</span></span>](../../../wcf/extending/custom-bindings.md)
- [\<customBinding>](custombinding.md)
- [<span data-ttu-id="4a200-174">作法：使用 SecurityBindingElement 建立自訂繫結</span><span class="sxs-lookup"><span data-stu-id="4a200-174">How to: Create a Custom Binding Using the SecurityBindingElement</span></span>](../../../wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)
- [<span data-ttu-id="4a200-175">自訂繫結安全性</span><span class="sxs-lookup"><span data-stu-id="4a200-175">Custom Binding Security</span></span>](../../../wcf/samples/custom-binding-security.md)
