---
title: <customBinding>
ms.date: 03/30/2017
ms.assetid: 9da4f960-f64e-4d8a-894d-2b09eba5ce4b
ms.openlocfilehash: cdaaacf0dfa75209d001f6e8d6ac7175816048aa
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "74140790"
---
# \<customBinding>

<span data-ttu-id="08314-101">對使用者提供訊息堆疊的完整控制權。</span><span class="sxs-lookup"><span data-stu-id="08314-101">Provides full control over the messaging stack for the user.</span></span>

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<customBinding>**  

## <a name="syntax"></a><span data-ttu-id="08314-102">語法</span><span class="sxs-lookup"><span data-stu-id="08314-102">Syntax</span></span>

```xml
<customBinding>
  <binding name="String"
           closeTimeout="TimeSpan"
           openTimeout="TimeSpan"
           receiveTimeout="TimeSpan"
           sendTimeout="TimeSpan">
    <compositeDuplex clientBaseAddress="Uri" />
    <reliableSession acknowledgementInterval="TimeSpan"
                     advancedFlowControl="Boolean"
                     bufferedMessagesQuota="Integer"
                     inactivityTimeout="TimeSpan"
                     maxPendingChannels="Integer"
                     maxRetryCount="Integer"
                     ordered="Boolean" />
    <pnrpPeerResolver />
    <windowsStreamSecurity protectionLevel="None/Sign/EncryptAndSign" />
    <sslStreamSecurity requireClientCertificate="Boolean" />
    <transactionFlow transactionProtocol="OleTransactions/WSAtomicTransactionOctober2004" />
    <security defaultAlgorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"
              authenticationMode="UserNameForAnonymous"
              contextMode="Cookie"
              defaultProtectionLevel="Sign"
              enableKeyDerivation="false"
              keyEntropyMode="ClientEntropy"
              messageProtectionOrder="SignBeforeEncryptAndEncryptSignature"
              securityVersion="WSSecurityXXX2005">
      <localClientSettings cacheCookies="false"
                           detectReplays="false"
                           maxCookieCachingTime="00:07:24" />
      <localServiceSettings replayCacheSize="9"
                            maxClockSkew="00:00:03"
                            replayWindow="00:07:22.2190000" />
    </security>
    <binaryMessageEncoding maxReadPoolSize="Integer"
                           maxWritePoolSize="Integer"
                           maxSessionSize="Integer" />
    <httpsTransport manualAddressing="Boolean"
                    maxMessageSize="Integer"
                    authenticationScheme="Negotiate"
                    bypassProxyOnLocal="Boolean"
                    hostNameComparisonMode="Exact"
                    mapAddressingHeadersToHttpHeaders="Boolean"
                    proxyaddress="Uri"
                    realm="String"
                    requireClientCertificate="Boolean" />
    <peerTransport manualAddressing="false"
                   maxMessageSize="20002"
                   listenIPAddress="202.10.1.9"
                   messageAuthentication="false"
                   peerNodeAuthenticationMode="None"
                   port="1000" />
    <security defaultAlgorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"
              authenticationMode="UserNameForAnonymous"
              bootstrapBindingConfiguration="String"
              bootstrapBindingSectionName="String"
              defaultProtectionLevel="None/Sign/EncryptAndSign"
              requireDerivedKeys="Boolean"
              securityHeaderLayout="Strict/Lax/LaxTimestampFirst/LaxTimestampLast"
              includeTimestamp="Boolean"
              keyEntropyMode="ClientEntropy/ServerEntropy/CombinedEntropy"
              messageProtectionOrder="SignBeforeEncrypt/SignBeforeEncryptAndEncryptSignature/EncryptBeforeSign"
              protectTokens="Boolean"
              requireSecurityContextCancellation="Boolean"
              securityVersion=" WSSecurityJan2004/WSSecurityXXX2005"
              requireSignatureConfirmation="Boolean">
      <localClientSettings cacheCookies="Boolean"
                           detectReplays="Boolean"
                           replayCacheSize="Integer"
                           maxClockSkew="TimeSpan"
                           maxCookieCachingTime="TimeSpan"
                           replayWindow="TimeSpan"
                           sessionKeyRenewalInterval="TimeSpan"
                           sessionKeyRolloverInterval="TimeSpan"
                           reconnectOnTransportFailure="Boolean"
                           timestampValidityDuration="TimeSpan"
                           cookieRenewalThresholdPercentage="Integer" />
      <localServiceSettings detectReplays="Boolean"
                            issuedCookieLifeTime="TimeSpan"
                            maxStatefulNegotiations="Integer"
                            replayCacheSize="Integer"
                            maxClockSkew="TimeSpan"
                            negotiationTimeout="TimeSpan"
                            replayWindow="TimeSpan"
                            inactivityTimeout="TimeSpan"
                            sessionKeyRenewalInterval="TimeSpan"
                            sessionKeyRolloverInterval="TimeSpan"
                            reconnectOnTransportFailure="Boolean"
                            maxConcurrentSessions="Integer"
                            timestampValidityDuration="TimeSpan" />
      <federationParameters trustVersion="WSTrustApr2004/WSTrustFeb2005" />
    </security>
    <security defaultAlgorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"
              authenticationMode="UserNameForAnonymous"
              bootstrapBindingConfiguration="String"
              bootstrapBindingSectionName="String"
              defaultProtectionLevel="None/Sign/EncryptAndSign"
              requireDerivedKeys="Boolean"
              securityHeaderLayout="Strict/Lax/LaxTimestampFirst/LaxTimestampLast"
              includeTimestamp="Boolean"
              keyEntropyMode="ClientEntropy/ServerEntropy/CombinedEntropy"
              messageProtectionOrder="SignBeforeEncrypt/SignBeforeEncryptAndEncryptSignature/EncryptBeforeSign"
              protectTokens="Boolean"
              requireSecurityContextCancellation="Boolean"
              securityVersion=" WSSecurityJan2004/WSSecurityXXX2005"
              requireSignatureConfirmation="Boolean" >
      <localClientSettings cacheCookies="Boolean"
                           detectReplays="Boolean"
                           replayCacheSize="Integer"
                           maxClockSkew="TimeSpan"
                           maxCookieCachingTime="TimeSpan"
                           replayWindow="TimeSpan"
                           sessionKeyRenewalInterval="TimeSpan"
                           sessionKeyRolloverInterval="TimeSpan"
                           reconnectOnTransportFailure="Boolean"
                           timestampValidityDuration="TimeSpan"
                           cookieRenewalThresholdPercentage="Integer" />
      <localServiceSettings detectReplays="Boolean"
                           issuedCookieLifeTime="TimeSpan"
                           maxStatefulNegotiations="Integer"
                           replayCacheSize="Integer"
                           maxClockSkew="TimeSpan"
                           negotiationTimeout="TimeSpan"
                           replayWindow="TimeSpan"
                           inactivityTimeout="TimeSpan"
                           sessionKeyRenewalInterval="TimeSpan"
                           sessionKeyRolloverInterval="TimeSpan"
                           reconnectOnTransportFailure="Boolean"
                           maxConcurrentSessions="Integer"
                           timestampValidityDuration="TimeSpan" />
      <federationParameters trustVersion="WSTrustApr2004/WSTrustFeb2005" />
      <genericIssuedTokenParameters>
        <localIssuerIssuedTokenParameters keyType="SymmetricKey/PublicKey"
                                          keySize="Integer"
                                          tokenType="String" />
        <issuedTokenParametersEndpointAddress address="URI"
                                              bindingConfiguration="String"
                                              binding="String" />
        <issuedTokenClient localIssuerChannelBehaviors="String"
                           cacheIssuedTokens="Boolean"
                           maxIssuedTokenCachingTime="TimeSpan"
                           keyEntropyMode="ClientEntropy/ServerEntropy/CombinedEntropy" />
        <issuedTokenClientBehavior issuerAddress="String"
                                   behaviorConfiguration="String" />
        <issuedTokenClientBehavior address="URI"
                                   bindingConfiguration="String"
                                   binding="String" />
      </genericIssuedTokenParameters>
    </security>
  </binding>
</customBinding>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="08314-103">屬性和項目</span><span class="sxs-lookup"><span data-stu-id="08314-103">Attributes and Elements</span></span>

<span data-ttu-id="08314-104">下列各節說明屬性、子元素和父元素</span><span class="sxs-lookup"><span data-stu-id="08314-104">The following sections describe attributes, child elements, and parent elements</span></span>

### <a name="attributes"></a><span data-ttu-id="08314-105">屬性</span><span class="sxs-lookup"><span data-stu-id="08314-105">Attributes</span></span>

|<span data-ttu-id="08314-106">屬性</span><span class="sxs-lookup"><span data-stu-id="08314-106">Attribute</span></span>|<span data-ttu-id="08314-107">描述</span><span class="sxs-lookup"><span data-stu-id="08314-107">Description</span></span>|
|---------------|-----------------|
|<span data-ttu-id="08314-108">closeTimeout</span><span class="sxs-lookup"><span data-stu-id="08314-108">closeTimeout</span></span>|<span data-ttu-id="08314-109"><xref:System.TimeSpan> 值，指定提供用來讓關閉作業完成的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="08314-109">A <xref:System.TimeSpan> value that specifies the interval of time provided for a close operation to complete.</span></span> <span data-ttu-id="08314-110">這個值應該大於或等於 <xref:System.TimeSpan.Zero>。</span><span class="sxs-lookup"><span data-stu-id="08314-110">This value should be greater than or equal to <xref:System.TimeSpan.Zero>.</span></span> <span data-ttu-id="08314-111">預設為 00:01:00。</span><span class="sxs-lookup"><span data-stu-id="08314-111">The default is 00:01:00.</span></span>|
|<span data-ttu-id="08314-112">NAME</span><span class="sxs-lookup"><span data-stu-id="08314-112">name</span></span>|<span data-ttu-id="08314-113">包含繫結之組態名稱的字串。</span><span class="sxs-lookup"><span data-stu-id="08314-113">A string that contains the configuration name of the binding.</span></span> <span data-ttu-id="08314-114">這個值是使用者定義的字串，它會充當自訂繫結的識別字串。</span><span class="sxs-lookup"><span data-stu-id="08314-114">This value is a user-defined string that acts as the identification string for the custom binding.</span></span> <span data-ttu-id="08314-115">從 .NET Framework 4 開始，系結和行為都不需要有名稱。</span><span class="sxs-lookup"><span data-stu-id="08314-115">Starting with .NET Framework 4, bindings and behaviors are not required to have a name.</span></span> <span data-ttu-id="08314-116">如需預設設定和無相關系結和行為的詳細資訊，請參閱[簡化](../../../wcf/simplified-configuration.md)的設定和[WCF 服務的簡化](../../../wcf/samples/simplified-configuration-for-wcf-services.md)設定。</span><span class="sxs-lookup"><span data-stu-id="08314-116">For more information about default configuration and nameless bindings and behaviors, see [Simplified Configuration](../../../wcf/simplified-configuration.md) and [Simplified Configuration for WCF Services](../../../wcf/samples/simplified-configuration-for-wcf-services.md).</span></span>|
|<span data-ttu-id="08314-117">openTimeout</span><span class="sxs-lookup"><span data-stu-id="08314-117">openTimeout</span></span>|<span data-ttu-id="08314-118"><xref:System.TimeSpan> 值，指定提供用來讓開啟作業完成的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="08314-118">A <xref:System.TimeSpan> value that specifies the interval of time provided for an open operation to complete.</span></span> <span data-ttu-id="08314-119">這個值應該大於或等於 <xref:System.TimeSpan.Zero>。</span><span class="sxs-lookup"><span data-stu-id="08314-119">This value should be greater than or equal to <xref:System.TimeSpan.Zero>.</span></span> <span data-ttu-id="08314-120">預設為 00:01:00。</span><span class="sxs-lookup"><span data-stu-id="08314-120">The default is 00:01:00.</span></span>|
|<span data-ttu-id="08314-121">receiveTimeout</span><span class="sxs-lookup"><span data-stu-id="08314-121">receiveTimeout</span></span>|<span data-ttu-id="08314-122"><xref:System.TimeSpan> 值，指定接收作業完成其作業之時間間隔。</span><span class="sxs-lookup"><span data-stu-id="08314-122">A <xref:System.TimeSpan> value that specifies the interval of time provided for a receive operation to complete.</span></span> <span data-ttu-id="08314-123">這個值應該大於或等於 <xref:System.TimeSpan.Zero>。</span><span class="sxs-lookup"><span data-stu-id="08314-123">This value should be greater than or equal to <xref:System.TimeSpan.Zero>.</span></span> <span data-ttu-id="08314-124">預設為 00:01:00。</span><span class="sxs-lookup"><span data-stu-id="08314-124">The default is 00:01:00.</span></span>|
|<span data-ttu-id="08314-125">sendTimeout</span><span class="sxs-lookup"><span data-stu-id="08314-125">sendTimeout</span></span>|<span data-ttu-id="08314-126"><xref:System.TimeSpan> 值，指定提供用來讓傳送作業完成的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="08314-126">A <xref:System.TimeSpan> value that specifies the interval of time provided for a send operation to complete.</span></span> <span data-ttu-id="08314-127">這個值應該大於或等於 <xref:System.TimeSpan.Zero>。</span><span class="sxs-lookup"><span data-stu-id="08314-127">This value should be greater than or equal to <xref:System.TimeSpan.Zero>.</span></span> <span data-ttu-id="08314-128">預設為 00:01:00。</span><span class="sxs-lookup"><span data-stu-id="08314-128">The default is 00:01:00.</span></span>|

### <a name="child-elements"></a><span data-ttu-id="08314-129">子元素</span><span class="sxs-lookup"><span data-stu-id="08314-129">Child Elements</span></span>

|<span data-ttu-id="08314-130">元素</span><span class="sxs-lookup"><span data-stu-id="08314-130">Element</span></span>|<span data-ttu-id="08314-131">描述</span><span class="sxs-lookup"><span data-stu-id="08314-131">Description</span></span>|
|-------------|-----------------|
|[\<compositeDuplex>](compositeduplex.md)|<span data-ttu-id="08314-132">指定自訂繫結的雙向傳訊。</span><span class="sxs-lookup"><span data-stu-id="08314-132">Specifies two-way messaging to the custom binding.</span></span> <span data-ttu-id="08314-133">它是和本身不允許雙工通訊的傳輸一起使用，例如 HTTP。</span><span class="sxs-lookup"><span data-stu-id="08314-133">It is used with transports that do not allow duplex communications natively, for example, HTTP.</span></span> <span data-ttu-id="08314-134">相反地，TCP 本身就允許雙工通訊，因此不需要使用這個繫結項目也可讓服務將訊息傳回用戶端。</span><span class="sxs-lookup"><span data-stu-id="08314-134">TCP, by contrast, allows duplex communications natively, and does not require the use of this binding element for the service to send messages back to a client.</span></span><br /><br /> <span data-ttu-id="08314-135">用戶端必須公開位址，才能讓服務接觸並建立連接。</span><span class="sxs-lookup"><span data-stu-id="08314-135">The client must expose an address for the service to make contact and establish a connection.</span></span> <span data-ttu-id="08314-136">這個用戶端位址是由 `ClientBaseAddress` 屬性提供。</span><span class="sxs-lookup"><span data-stu-id="08314-136">This client address is provided by the `ClientBaseAddress` attribute.</span></span><br /><br /> <span data-ttu-id="08314-137">此項目的型別為 <xref:System.ServiceModel.Configuration.CompositeDuplexElement>。</span><span class="sxs-lookup"><span data-stu-id="08314-137">This element is of type <xref:System.ServiceModel.Configuration.CompositeDuplexElement>.</span></span>|
|[\<pnrpPeerResolver>](pnrppeerresolver.md)|<span data-ttu-id="08314-138">指定對等名稱解析通訊協定 (PNRP) 對等名稱解析程式。</span><span class="sxs-lookup"><span data-stu-id="08314-138">Specifies a Peer Name Resolution Protocol (PNRP) peer name resolver.</span></span> <span data-ttu-id="08314-139">此項目的型別為 <xref:System.ServiceModel.Configuration.PnrpPeerResolverElement>。</span><span class="sxs-lookup"><span data-stu-id="08314-139">This element is of type <xref:System.ServiceModel.Configuration.PnrpPeerResolverElement>.</span></span>|
|[\<reliableSession>](reliablesession.md)|<span data-ttu-id="08314-140">指定 WS-Reliable 訊息設定。</span><span class="sxs-lookup"><span data-stu-id="08314-140">Specifies the setting for WS-Reliable Messaging.</span></span> <span data-ttu-id="08314-141">將這個項目新增至自訂繫結時，產生的通道可支援確實傳送一次保證。</span><span class="sxs-lookup"><span data-stu-id="08314-141">When this element is added to a custom binding, the resulting channel can support exactly-once delivery assurances.</span></span> <span data-ttu-id="08314-142">此項目的型別為 <xref:System.ServiceModel.Configuration.ReliableSessionElement>。</span><span class="sxs-lookup"><span data-stu-id="08314-142">This element is of type <xref:System.ServiceModel.Configuration.ReliableSessionElement>.</span></span>|
|[\<security>](security-of-custombinding.md)|<span data-ttu-id="08314-143">指定自訂繫結的安全性選項。</span><span class="sxs-lookup"><span data-stu-id="08314-143">Specifies the options for security of the custom binding.</span></span> <span data-ttu-id="08314-144">此項目的型別為 <xref:System.ServiceModel.Configuration.SecurityElement>。</span><span class="sxs-lookup"><span data-stu-id="08314-144">This element is of type <xref:System.ServiceModel.Configuration.SecurityElement>.</span></span>|
|[\<sslStreamSecurity>](sslstreamsecurity.md)|<span data-ttu-id="08314-145">指定 SSL 資料流繫結的安全性設定。</span><span class="sxs-lookup"><span data-stu-id="08314-145">Specifies the security settings for a SSL stream binding.</span></span> <span data-ttu-id="08314-146">此項目的型別為 <xref:System.ServiceModel.Configuration.SslStreamSecurityElement>。</span><span class="sxs-lookup"><span data-stu-id="08314-146">This element is of type <xref:System.ServiceModel.Configuration.SslStreamSecurityElement>.</span></span>|
|[\<transactionFlow>](transactionflow.md)|<span data-ttu-id="08314-147">指定繫結應支援交易流程，並指定 `transactionProtocol` 屬性使用的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="08314-147">Specifies that the binding supports transaction flow, and the protocol to be used by the `transactionProtocol` attribute.</span></span> <span data-ttu-id="08314-148">此項目的型別為 <xref:System.ServiceModel.Configuration.TransactionFlowElement>。</span><span class="sxs-lookup"><span data-stu-id="08314-148">This element is of type <xref:System.ServiceModel.Configuration.TransactionFlowElement>.</span></span>|
|[\<windowsStreamSecurity>](windowsstreamsecurity.md)|<span data-ttu-id="08314-149">指定自訂繫結的資料流 (Streaming) 安全性選項。</span><span class="sxs-lookup"><span data-stu-id="08314-149">Specifies the options for streaming security of the custom binding.</span></span> <span data-ttu-id="08314-150">此項目的型別為 <xref:System.ServiceModel.Configuration.WindowsStreamSecurityElement>。</span><span class="sxs-lookup"><span data-stu-id="08314-150">This element is of type <xref:System.ServiceModel.Configuration.WindowsStreamSecurityElement>.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="08314-151">父項目</span><span class="sxs-lookup"><span data-stu-id="08314-151">Parent Elements</span></span>

|<span data-ttu-id="08314-152">元素</span><span class="sxs-lookup"><span data-stu-id="08314-152">Element</span></span>|<span data-ttu-id="08314-153">描述</span><span class="sxs-lookup"><span data-stu-id="08314-153">Description</span></span>|
|-------------|-----------------|
|<span data-ttu-id="08314-154">繫結</span><span class="sxs-lookup"><span data-stu-id="08314-154">bindings</span></span>|<span data-ttu-id="08314-155">包含 Windows Communication Foundation 應用程式的所有繫結。</span><span class="sxs-lookup"><span data-stu-id="08314-155">Contains all bindings for Windows Communication Foundation applications.</span></span>|

## <a name="remarks"></a><span data-ttu-id="08314-156">備註</span><span class="sxs-lookup"><span data-stu-id="08314-156">Remarks</span></span>

<span data-ttu-id="08314-157">自訂繫結會提供對於 WCF 訊息堆疊的完整控制權。</span><span class="sxs-lookup"><span data-stu-id="08314-157">Custom bindings provide full control over the WCF messaging stack.</span></span> <span data-ttu-id="08314-158">您可以新增特定實體的組態項目，來建立特別量身訂作的繫結。</span><span class="sxs-lookup"><span data-stu-id="08314-158">Special tailored bindings can be created my adding the configuration elements for specific entities.</span></span> <span data-ttu-id="08314-159">例如，使用者可結合 `httpsTransport` 區段、`reliableSession` 區段和 `security` 區段來建立可靠且安全的 https 繫結。</span><span class="sxs-lookup"><span data-stu-id="08314-159">For example, the user can combine the `httpsTransport` section, `reliableSession` section and the `security` section to create a reliable and secure https based binding.</span></span>

<span data-ttu-id="08314-160">個別繫結定義訊息堆疊的方式，是依據堆疊項目在堆疊中的出現順序來指定其組態項目。</span><span class="sxs-lookup"><span data-stu-id="08314-160">An individual binding defines the message stack by specifying the configuration elements for the stack elements in the order they appear on the stack.</span></span> <span data-ttu-id="08314-161">每個項目都會定義及設定堆疊的一個項目。</span><span class="sxs-lookup"><span data-stu-id="08314-161">Each element defines and configures the one element of the stack.</span></span> <span data-ttu-id="08314-162">各個自訂繫結中一定要出現一個而且是唯一一個的傳輸項目。</span><span class="sxs-lookup"><span data-stu-id="08314-162">There must be one and only one transport element in each custom binding.</span></span> <span data-ttu-id="08314-163">如果沒有這個項目，訊息堆疊就不完整。</span><span class="sxs-lookup"><span data-stu-id="08314-163">Without this element, the messaging stack is incomplete.</span></span>

<span data-ttu-id="08314-164">項目在堆疊中的出現順序很重要，因為這是作業套用至訊息的順序。</span><span class="sxs-lookup"><span data-stu-id="08314-164">The order in which elements appear in the stack matters, because it is the order in which operations are applied to the message.</span></span> <span data-ttu-id="08314-165">建議的堆疊項目順序如下所示：</span><span class="sxs-lookup"><span data-stu-id="08314-165">The recommended order of stack elements is the following:</span></span>

1. <span data-ttu-id="08314-166">交易 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="08314-166">Transactions (optional)</span></span>

2. <span data-ttu-id="08314-167">可信賴傳訊 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="08314-167">Reliable Messaging (optional)</span></span>

3. <span data-ttu-id="08314-168">安全性 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="08314-168">Security (optional)</span></span>

4. <span data-ttu-id="08314-169">傳輸</span><span class="sxs-lookup"><span data-stu-id="08314-169">Transport</span></span>

5. <span data-ttu-id="08314-170">編碼器 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="08314-170">Encoder (optional)</span></span>

<span data-ttu-id="08314-171">當系統提供的其中一個繫結程序不符合服務的需求時，請使用自訂繫結程序。</span><span class="sxs-lookup"><span data-stu-id="08314-171">Use a custom binding when one of the system-provided bindings does not meet the requirements of your service.</span></span> <span data-ttu-id="08314-172">例如，若要在服務端點上啟用新的傳輸或新的編碼器，可以使用自訂繫結。</span><span class="sxs-lookup"><span data-stu-id="08314-172">A custom binding could be used, for example, to enable the use of a new transport or a new encoder at a service endpoint.</span></span>

<span data-ttu-id="08314-173">在建構自訂繫結時，會使用依據特定順序堆疊之繫結項目集合中的其中一個 <xref:System.ServiceModel.Channels.CustomBinding.%23ctor%2A>：</span><span class="sxs-lookup"><span data-stu-id="08314-173">A custom binding is constructed using one of the <xref:System.ServiceModel.Channels.CustomBinding.%23ctor%2A> from a collection of binding elements that are "stacked" in a specific order:</span></span>

- <span data-ttu-id="08314-174">在最上方為允許流動異動的選擇性 <xref:System.ServiceModel.Channels.TransactionFlowBindingElement>。</span><span class="sxs-lookup"><span data-stu-id="08314-174">At the top is an optional <xref:System.ServiceModel.Channels.TransactionFlowBindingElement> that allows flowing transactions.</span></span>

- <span data-ttu-id="08314-175">接下來是選擇性 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement>，它會提供 WS-ReliableMessaging 規格中所定義的工作階段和排序機制。</span><span class="sxs-lookup"><span data-stu-id="08314-175">Next is an optional <xref:System.ServiceModel.Channels.ReliableSessionBindingElement> that provides a session and ordering mechanism as defined in the WS-ReliableMessaging specification.</span></span> <span data-ttu-id="08314-176">這個工作階段概念可以跨越 SOAP 和傳輸媒介。</span><span class="sxs-lookup"><span data-stu-id="08314-176">This notion of a session can cross SOAP and transport intermediaries.</span></span>

- <span data-ttu-id="08314-177">接下來是選擇性安全性繫結項目，它會提供類似授權、驗證 (Authentication)、保護和機密性等安全性功能。</span><span class="sxs-lookup"><span data-stu-id="08314-177">Next is an optional security binding element that provides security features like authorization, authentication, protection, and confidentiality.</span></span> <span data-ttu-id="08314-178">下列安全性繫結項目是由 Windows Communication Foundation （WCF）所提供：</span><span class="sxs-lookup"><span data-stu-id="08314-178">The following security binding elements are provided by Windows Communication Foundation (WCF):</span></span>

  - <xref:System.ServiceModel.Channels.SecurityBindingElement>

  - <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement>

  - <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>

  - <xref:System.ServiceModel.Channels.TransportSecurityBindingElement>

- <span data-ttu-id="08314-179">接下來是繫結項目所指定的選擇性訊息模式：</span><span class="sxs-lookup"><span data-stu-id="08314-179">Next are the optional message-patterns specified by binding elements:</span></span>

- <xref:System.ServiceModel.Channels.CompositeDuplexBindingElement>

- <span data-ttu-id="08314-180">接下來是選擇性傳輸升級/helper 繫結項目：</span><span class="sxs-lookup"><span data-stu-id="08314-180">Next are the optional transport upgrades/helpers binding elements:</span></span>

  - <xref:System.ServiceModel.Channels.PnrpPeerResolverBindingElement>

  - <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement>

  - <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement>

- <span data-ttu-id="08314-181">再來是必要的訊息編碼繫結項目。</span><span class="sxs-lookup"><span data-stu-id="08314-181">Next is a required message encoding binding element.</span></span> <span data-ttu-id="08314-182">您可以使用自己的傳輸或是使用下列其中一個訊息編碼繫結：</span><span class="sxs-lookup"><span data-stu-id="08314-182">You can use your own transport or use one of the following message encoding bindings:</span></span>

  - <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>

  - <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement>

  - <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement>

- <span data-ttu-id="08314-183">最下方是必要的傳輸項目。</span><span class="sxs-lookup"><span data-stu-id="08314-183">At the bottom is a required transport element.</span></span> <span data-ttu-id="08314-184">您可以使用自己的傳輸，或使用 Windows Communication Foundation （WCF）所提供的其中一個傳輸繫結項目：</span><span class="sxs-lookup"><span data-stu-id="08314-184">You can use your own transport or use one of transport binding elements provided by Windows Communication Foundation (WCF):</span></span>

  - <xref:System.ServiceModel.Channels.TcpTransportBindingElement>

  - <xref:System.ServiceModel.Channels.NamedPipeTransportBindingElement>

  - <xref:System.ServiceModel.Channels.HttpTransportBindingElement>

  - <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>

  - <xref:System.ServiceModel.Channels.MsmqTransportBindingElement>

  - <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBindingElement>

  - <xref:System.ServiceModel.Channels.PeerTransportBindingElement>

<span data-ttu-id="08314-185">下表摘要列出每一層的選項。</span><span class="sxs-lookup"><span data-stu-id="08314-185">The following table summarizes the options for each layer.</span></span>

|<span data-ttu-id="08314-186">階層</span><span class="sxs-lookup"><span data-stu-id="08314-186">Layer</span></span>|<span data-ttu-id="08314-187">選項</span><span class="sxs-lookup"><span data-stu-id="08314-187">Options</span></span>|<span data-ttu-id="08314-188">必要</span><span class="sxs-lookup"><span data-stu-id="08314-188">Required</span></span>|
|-----------|-------------|--------------|
|<span data-ttu-id="08314-189">異動流程</span><span class="sxs-lookup"><span data-stu-id="08314-189">Transaction Flow</span></span>|<xref:System.ServiceModel.Channels.TransactionFlowBindingElement>|<span data-ttu-id="08314-190">否</span><span class="sxs-lookup"><span data-stu-id="08314-190">No</span></span>|
|<span data-ttu-id="08314-191">可靠性</span><span class="sxs-lookup"><span data-stu-id="08314-191">Reliability</span></span>|<xref:System.ServiceModel.Channels.ReliableSessionBindingElement>|<span data-ttu-id="08314-192">否</span><span class="sxs-lookup"><span data-stu-id="08314-192">No</span></span>|
|<span data-ttu-id="08314-193">安全性</span><span class="sxs-lookup"><span data-stu-id="08314-193">Security</span></span>|<span data-ttu-id="08314-194">對稱、不對稱、傳輸層級</span><span class="sxs-lookup"><span data-stu-id="08314-194">Symmetric, Asymmetric, Transport-Level</span></span>|<span data-ttu-id="08314-195">否</span><span class="sxs-lookup"><span data-stu-id="08314-195">No</span></span>|
|<span data-ttu-id="08314-196">形狀變更</span><span class="sxs-lookup"><span data-stu-id="08314-196">Shape Change</span></span>|<xref:System.ServiceModel.Channels.CompositeDuplexBindingElement>|<span data-ttu-id="08314-197">否</span><span class="sxs-lookup"><span data-stu-id="08314-197">No</span></span>|
|<span data-ttu-id="08314-198">傳輸升級</span><span class="sxs-lookup"><span data-stu-id="08314-198">Transport Upgrades</span></span>|<span data-ttu-id="08314-199">SSL 資料流、Windows 資料流、對等解析程式</span><span class="sxs-lookup"><span data-stu-id="08314-199">SSL stream, Windows stream, Peer Resolver</span></span>|<span data-ttu-id="08314-200">否</span><span class="sxs-lookup"><span data-stu-id="08314-200">No</span></span>|
|<span data-ttu-id="08314-201">編碼</span><span class="sxs-lookup"><span data-stu-id="08314-201">Encoding</span></span>|<span data-ttu-id="08314-202">文字、二進位、MTOM、自訂</span><span class="sxs-lookup"><span data-stu-id="08314-202">Text, Binary, MTOM, Custom</span></span>|<span data-ttu-id="08314-203">是</span><span class="sxs-lookup"><span data-stu-id="08314-203">Yes</span></span>|
|<span data-ttu-id="08314-204">傳輸</span><span class="sxs-lookup"><span data-stu-id="08314-204">Transport</span></span>|<span data-ttu-id="08314-205">TCP、具名管道、HTTP、HTTPS、MSMQ 的類別、自訂</span><span class="sxs-lookup"><span data-stu-id="08314-205">TCP, Named Pipes, HTTP, HTTPS, flavors of MSMQ, Custom</span></span>|<span data-ttu-id="08314-206">是</span><span class="sxs-lookup"><span data-stu-id="08314-206">Yes</span></span>|

<span data-ttu-id="08314-207">此外，您也可以定義自己的繫結項目，並將其插入上述任何定義層之間。</span><span class="sxs-lookup"><span data-stu-id="08314-207">In addition, you can define your own binding elements and insert them between any of the preceding defined layers.</span></span>

<span data-ttu-id="08314-208">如需如何使用自訂系結來修改系統提供之系結的討論，請參閱[如何：自訂系統提供](../../../wcf/extending/how-to-customize-a-system-provided-binding.md)的系結。</span><span class="sxs-lookup"><span data-stu-id="08314-208">For a discussion on how to use a custom binding to modify a system-provided binding, see [How to: Customize a System-Provided Binding](../../../wcf/extending/how-to-customize-a-system-provided-binding.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="08314-209">另請參閱</span><span class="sxs-lookup"><span data-stu-id="08314-209">See also</span></span>

- <xref:System.ServiceModel.Channels.Binding>
- <xref:System.ServiceModel.Channels.BindingElement>
- <xref:System.ServiceModel.Configuration.BindingsSection>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [\<binding>](bindings.md)
- [<span data-ttu-id="08314-210">繫結</span><span class="sxs-lookup"><span data-stu-id="08314-210">Bindings</span></span>](../../../wcf/bindings.md)
- [<span data-ttu-id="08314-211">擴充繫結</span><span class="sxs-lookup"><span data-stu-id="08314-211">Extending Bindings</span></span>](../../../wcf/extending/extending-bindings.md)
- [<span data-ttu-id="08314-212">自訂繫結</span><span class="sxs-lookup"><span data-stu-id="08314-212">Custom Bindings</span></span>](../../../wcf/extending/custom-bindings.md)
- [<span data-ttu-id="08314-213">customBinding 元素</span><span class="sxs-lookup"><span data-stu-id="08314-213">customBinding Element</span></span>](custombinding.md)
- [<span data-ttu-id="08314-214">繫結</span><span class="sxs-lookup"><span data-stu-id="08314-214">Bindings</span></span>](../../../wcf/bindings.md)
- [<span data-ttu-id="08314-215">設定系統提供的繫結</span><span class="sxs-lookup"><span data-stu-id="08314-215">Configuring System-Provided Bindings</span></span>](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [<span data-ttu-id="08314-216">使用繫結設定服務與用戶端</span><span class="sxs-lookup"><span data-stu-id="08314-216">Using Bindings to Configure Services and Clients</span></span>](../../../wcf/using-bindings-to-configure-services-and-clients.md)
