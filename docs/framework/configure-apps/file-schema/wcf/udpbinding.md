---
title: <udpBinding>
ms.date: 03/30/2017
ms.assetid: fa291901-8340-45c6-9c44-5d9281c70bc3
ms.openlocfilehash: 7fa72d233d6489ab6a2c534f69c66a55a22d0f59
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "74429840"
---
# \<udpBinding>
<span data-ttu-id="9ae1a-101">用來設定 <xref:System.ServiceModel.UdpBinding> 繫結的組態元素。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-101">A configuration element used to configure the <xref:System.ServiceModel.UdpBinding> binding.</span></span>  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<udpBinding>**  
  
## <a name="syntax"></a><span data-ttu-id="9ae1a-102">語法</span><span class="sxs-lookup"><span data-stu-id="9ae1a-102">Syntax</span></span>  
  
```xml  
<udpBinding>
  <binding closeTimeout="TimeSpan"
           duplicateMessageHistoryLength="Integer"
           maxBufferPoolSize="Integer"
           maxBufferSize="Integer"
           maxPendingMessagesTotalSize="Integer"
           maxReceivedMessageSize="Integer"
           maxRetransmitCount="Integer"
           multicastInterfaceId="Integer"
           name="String"
           openTimeout="TimeSpan"
           receiveTimeout="TimeSpan"
           sendTimeout="TimeSpan"
           textEncoding="UnicodeFffeTextEncoding/Utf16TextEncoding/Utf8TextEncoding"
           timeToLive="TimeSpan">
    <readerQuotas maxArrayLength="Integer"
                  maxBytesPerRead="Integer"
                  maxDepth="Integer"
                  maxNameTableCharCount="Integer"
                  maxStringContentLength="Integer" />
  </binding>
</basicHttpBinding>
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="9ae1a-103">屬性和項目</span><span class="sxs-lookup"><span data-stu-id="9ae1a-103">Attributes and Elements</span></span>  
 <span data-ttu-id="9ae1a-104">下列章節說明屬性、子元素和父元素。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-104">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="9ae1a-105">屬性</span><span class="sxs-lookup"><span data-stu-id="9ae1a-105">Attributes</span></span>  
  
|<span data-ttu-id="9ae1a-106">屬性</span><span class="sxs-lookup"><span data-stu-id="9ae1a-106">Attribute</span></span>|<span data-ttu-id="9ae1a-107">描述</span><span class="sxs-lookup"><span data-stu-id="9ae1a-107">Description</span></span>|  
|---------------|-----------------|  
|`closeTimeout`|<span data-ttu-id="9ae1a-108"><xref:System.TimeSpan> 值，指定提供用來讓關閉作業完成的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-108">A <xref:System.TimeSpan> value that specifies the interval of time provided for a close operation to complete.</span></span> <span data-ttu-id="9ae1a-109">這個值應該大於或等於 <xref:System.TimeSpan.Zero>。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-109">This value should be greater than or equal to <xref:System.TimeSpan.Zero>.</span></span> <span data-ttu-id="9ae1a-110">預設為 00:01:00。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-110">The default is 00:01:00.</span></span>|  
|`duplicateMessageHistoryLength`|<span data-ttu-id="9ae1a-111">指定重複訊息記錄長度的整數值。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-111">An integer value that specifies the duplicate message history length.</span></span>|  
|`maxBufferPoolSize`|<span data-ttu-id="9ae1a-112">整數值，指定配置供從通道接收訊息之訊息緩衝區管理員使用的最大記憶體量。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-112">An integer value that specifies the maximum amount of memory that is allocated for use by the manager of the message buffers that receive messages from the channel.</span></span> <span data-ttu-id="9ae1a-113">預設值為 524288 (0x80000) 位元組。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-113">The default value is 524288 (0x80000) bytes.</span></span>|  
|`maxBufferSize`|<span data-ttu-id="9ae1a-114">整數值，指定儲存訊息之緩衝區的大小上限 (以位元組為單位)。在為此繫結設定的端點處理訊息時，可以將訊息儲存在緩衝區中。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-114">An integer value that specifies the maximum size, in bytes, of a buffer that stores messages while they are processed for an endpoint configured with this binding.</span></span> <span data-ttu-id="9ae1a-115">預設值為 65,536 位元組。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-115">The default value is 65,536 bytes.</span></span>|  
|`maxPendingMessagesTotalSize`|<span data-ttu-id="9ae1a-116">整數值，指定已接收但尚未從個別通道執行個體的輸入佇列移除的訊息數目上限。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-116">An integer value that specifies the maximum number of messages that are received but not yet removed from the input queue for an individual channel instance.</span></span>|  
|`maxReceivedMessageSize`|<span data-ttu-id="9ae1a-117">正整數，定義在使用此繫結設定之通道上可以接收的訊息大小上限 (以位元組為單位，包括標頭)。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-117">A positive integer that defines the maximum message size, in bytes, including headers, for a message that can be received on a channel configured with this binding.</span></span> <span data-ttu-id="9ae1a-118">如果對收件者而言訊息太大，寄件者便會收到 SOAP 錯誤。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-118">The sender receives a SOAP fault if the message is too large for the receiver.</span></span> <span data-ttu-id="9ae1a-119">收件者會捨棄訊息，然後在追蹤記錄檔中建立此事件的項目。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-119">The receiver drops the message and creates an entry of the event in the trace log.</span></span> <span data-ttu-id="9ae1a-120">預設值為 65,536 個位元組。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-120">The default is 65,536 bytes.</span></span>|  
|`maxRetransmitCount`|<span data-ttu-id="9ae1a-121">指定重新傳輸訊息數目上限的整數值。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-121">An integer value that specifies the maximum number of retransmit messages.</span></span>|  
|`multicastInterfaceId`|<span data-ttu-id="9ae1a-122">指定多點傳送介面 ID 的整數值。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-122">An integer value that specifies the multicast interface ID.</span></span>|  
|`name`|<span data-ttu-id="9ae1a-123">包含繫結之組態名稱的字串。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-123">A string that contains the configuration name of the binding.</span></span> <span data-ttu-id="9ae1a-124">這個值應該是唯一的，因為它會當做繫結的識別使用。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-124">This value should be unique because it is used as an identification for the binding.</span></span> <span data-ttu-id="9ae1a-125">從 .NET Framework 4 開始，系結和行為都不需要有名稱。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-125">Starting with .NET Framework 4, bindings and behaviors are not required to have a name.</span></span> <span data-ttu-id="9ae1a-126">如需預設設定和無相關系結和行為的詳細資訊，請參閱[簡化](../../../wcf/simplified-configuration.md)的設定和[WCF 服務的簡化](../../../wcf/samples/simplified-configuration-for-wcf-services.md)設定。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-126">For more information about default configuration and nameless bindings and behaviors, see [Simplified Configuration](../../../wcf/simplified-configuration.md) and [Simplified Configuration for WCF Services](../../../wcf/samples/simplified-configuration-for-wcf-services.md).</span></span>|  
|`openTimeout`|<span data-ttu-id="9ae1a-127"><xref:System.TimeSpan> 值，指定提供用來讓開啟作業完成的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-127">A <xref:System.TimeSpan> value that specifies the interval of time provided for an open operation to complete.</span></span> <span data-ttu-id="9ae1a-128">這個值應該大於或等於 <xref:System.TimeSpan.Zero>。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-128">This value should be greater than or equal to <xref:System.TimeSpan.Zero>.</span></span> <span data-ttu-id="9ae1a-129">預設為 00:01:00。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-129">The default is 00:01:00.</span></span>|  
|`receiveTimeout`|<span data-ttu-id="9ae1a-130"><xref:System.TimeSpan> 值，指定接收作業完成其作業之時間間隔。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-130">A <xref:System.TimeSpan> value that specifies the interval of time provided for a receive operation to complete.</span></span> <span data-ttu-id="9ae1a-131">這個值應該大於或等於 <xref:System.TimeSpan.Zero>。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-131">This value should be greater than or equal to <xref:System.TimeSpan.Zero>.</span></span> <span data-ttu-id="9ae1a-132">預設為 00:10:00。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-132">The default is 00:10:00.</span></span>|  
|`sendTimeout`|<span data-ttu-id="9ae1a-133"><xref:System.TimeSpan> 值，指定提供用來讓傳送作業完成的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-133">A <xref:System.TimeSpan> value that specifies the interval of time provided for a send operation to complete.</span></span> <span data-ttu-id="9ae1a-134">這個值應該大於或等於 <xref:System.TimeSpan.Zero>。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-134">This value should be greater than or equal to <xref:System.TimeSpan.Zero>.</span></span> <span data-ttu-id="9ae1a-135">預設為 00:01:00。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-135">The default is 00:01:00.</span></span>|  
|`textEncoding`|<span data-ttu-id="9ae1a-136">設定要在繫結上發出訊息時使用的字元集編碼方式。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-136">Sets the character set encoding to be used for emitting messages on the binding.</span></span> <span data-ttu-id="9ae1a-137">有效值如下：</span><span class="sxs-lookup"><span data-stu-id="9ae1a-137">Valid values include the following:</span></span><br /><br /> <span data-ttu-id="9ae1a-138">-BigEndianUnicode： Unicode BigEndian 編碼方式。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-138">-   BigEndianUnicode: Unicode BigEndian encoding.</span></span><br /><span data-ttu-id="9ae1a-139">-Unicode：16位編碼方式。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-139">-   Unicode: 16-bit encoding.</span></span><br /><span data-ttu-id="9ae1a-140">-UTF8：8位編碼</span><span class="sxs-lookup"><span data-stu-id="9ae1a-140">-   UTF8: 8-bit encoding</span></span><br /><br /> <span data-ttu-id="9ae1a-141">預設值為 UTF8。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-141">The default is UTF8.</span></span> <span data-ttu-id="9ae1a-142">此屬性的型別為 <xref:System.Text.Encoding>。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-142">This attribute is of type <xref:System.Text.Encoding>.</span></span>|  
|`timeToLive`|<span data-ttu-id="9ae1a-143">指定繫結存留時間的 timespan 值。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-143">A timespan value that specifies the time to live for the binding.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="9ae1a-144">子元素</span><span class="sxs-lookup"><span data-stu-id="9ae1a-144">Child Elements</span></span>  
  
|<span data-ttu-id="9ae1a-145">元素</span><span class="sxs-lookup"><span data-stu-id="9ae1a-145">Element</span></span>|<span data-ttu-id="9ae1a-146">描述</span><span class="sxs-lookup"><span data-stu-id="9ae1a-146">Description</span></span>|  
|-------------|-----------------|  
|[\<readerQuotas>](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms731325(v=vs.100))|<span data-ttu-id="9ae1a-147">定義 SOAP 訊息複雜度的條件約束，而這些條件約束可由以此繫結所設定的端點處理。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-147">Defines the constraints on the complexity of SOAP messages that can be processed by endpoints configured with this binding.</span></span> <span data-ttu-id="9ae1a-148">此項目的型別為 <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement>。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-148">This element is of type <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement>.</span></span>|  
  
### <a name="parent-elements"></a><span data-ttu-id="9ae1a-149">父項目</span><span class="sxs-lookup"><span data-stu-id="9ae1a-149">Parent Elements</span></span>  
  
|<span data-ttu-id="9ae1a-150">元素</span><span class="sxs-lookup"><span data-stu-id="9ae1a-150">Element</span></span>|<span data-ttu-id="9ae1a-151">描述</span><span class="sxs-lookup"><span data-stu-id="9ae1a-151">Description</span></span>|  
|-------------|-----------------|  
|[\<bindings>](bindings.md)|<span data-ttu-id="9ae1a-152">這個項目會保存標準和自訂繫結的集合。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-152">This element holds a collection of standard and custom bindings.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="9ae1a-153">備註</span><span class="sxs-lookup"><span data-stu-id="9ae1a-153">Remarks</span></span>  
 <span data-ttu-id="9ae1a-154">UdpBinding 允許 WCF 服務透過 UDP 傳輸進行通訊。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-154">The UdpBinding allows WCF services to communicate over the UDP transport.</span></span> <span data-ttu-id="9ae1a-155">它允許「引發並忘記」訊息交換，其中用戶端會將訊息傳送至服務，並預期不會傳迴響應。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-155">It allows for "fire and forget" message exchanges where a client sends a message to a service and expects no response back.</span></span>  
  
## <a name="example"></a><span data-ttu-id="9ae1a-156">範例</span><span class="sxs-lookup"><span data-stu-id="9ae1a-156">Example</span></span>  
 <span data-ttu-id="9ae1a-157">下列範例示範如何 <xref:System.ServiceModel.UdpBinding> 使用 <`udpBinding`> 元素來設定。</span><span class="sxs-lookup"><span data-stu-id="9ae1a-157">The following example shows how to configure the <xref:System.ServiceModel.UdpBinding> using the <`udpBinding`> element.</span></span>  
  
```xml  
<udpBinding>
  <binding  closeTimeout="00:10:00"
            duplicateMessageHistoryLength="100"
            maxBufferPoolSize="100"
            maxPendingMessagesTotalSize="100000"
            maxReceivedMessageSize="65536"
            maxRetransmitCount="10"
            multicastInterfaceId="00000"
            name="myUdpBinding"
            openTimeout="00:10:00"
            receiveTimeout="00:10:00"
            sendTimeout="00:10:00"
            textEncoding="utf-8"
            timeToLive="00:10:00">
    <readerQuotas />
  </binding>
</udpBinding>
```  
  
## <a name="see-also"></a><span data-ttu-id="9ae1a-158">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9ae1a-158">See also</span></span>

- <xref:System.ServiceModel.Channels.Binding>
- <xref:System.ServiceModel.Channels.BindingElement>
- <xref:System.ServiceModel.BasicHttpBinding>
- <xref:System.ServiceModel.Configuration.BasicHttpBindingElement>
- [<span data-ttu-id="9ae1a-159">繫結</span><span class="sxs-lookup"><span data-stu-id="9ae1a-159">Bindings</span></span>](../../../wcf/bindings.md)
- [<span data-ttu-id="9ae1a-160">設定系統提供的繫結</span><span class="sxs-lookup"><span data-stu-id="9ae1a-160">Configuring System-Provided Bindings</span></span>](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [<span data-ttu-id="9ae1a-161">使用繫結設定服務與用戶端</span><span class="sxs-lookup"><span data-stu-id="9ae1a-161">Using Bindings to Configure Services and Clients</span></span>](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](bindings.md)
