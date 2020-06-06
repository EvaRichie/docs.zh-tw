---
title: <soapProcessing>
ms.date: 03/30/2017
ms.assetid: e8707027-e6b8-4539-893d-3cd7c13fbc18
ms.openlocfilehash: 0728e22205d4ac2c7674f7690e142aed51d42440
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "70399545"
---
# \<soapProcessing>

<span data-ttu-id="f8f3a-101">定義用戶端端點行為，這個行為會用來封送處理不同繫結型別和訊息版本之間的訊息。</span><span class="sxs-lookup"><span data-stu-id="f8f3a-101">Defines the client endpoint behavior used to marshal messages between different binding types and message versions.</span></span>

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<endpointBehaviors>**](endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<soapProcessing>**
  
## <a name="syntax"></a><span data-ttu-id="f8f3a-102">語法</span><span class="sxs-lookup"><span data-stu-id="f8f3a-102">Syntax</span></span>  
  
```xml  
<soapProcessing processMessages="true|false" />
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="f8f3a-103">屬性和元素</span><span class="sxs-lookup"><span data-stu-id="f8f3a-103">Attributes and elements</span></span>  
  
<span data-ttu-id="f8f3a-104">下列章節說明屬性、子元素和父元素。</span><span class="sxs-lookup"><span data-stu-id="f8f3a-104">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="f8f3a-105">屬性</span><span class="sxs-lookup"><span data-stu-id="f8f3a-105">Attributes</span></span>  
  
|                   | <span data-ttu-id="f8f3a-106">描述</span><span class="sxs-lookup"><span data-stu-id="f8f3a-106">Description</span></span> |
| ----------------- | ----------- |
| `processMessages` | <span data-ttu-id="f8f3a-107">布林值，這個值指定是否應該在 SOAP 訊息版本之間封送處理訊息。</span><span class="sxs-lookup"><span data-stu-id="f8f3a-107">A Boolean value that specifies whether messages should be marshaled between SOAP message versions.</span></span> |

### <a name="child-elements"></a><span data-ttu-id="f8f3a-108">子元素</span><span class="sxs-lookup"><span data-stu-id="f8f3a-108">Child elements</span></span>

<span data-ttu-id="f8f3a-109">無</span><span class="sxs-lookup"><span data-stu-id="f8f3a-109">None</span></span>

### <a name="parent-elements"></a><span data-ttu-id="f8f3a-110">父元素</span><span class="sxs-lookup"><span data-stu-id="f8f3a-110">Parent elements</span></span>

|     | <span data-ttu-id="f8f3a-111">描述</span><span class="sxs-lookup"><span data-stu-id="f8f3a-111">Description</span></span> |
| --- | ----------- |
| [**\<behavior>**](behavior-of-endpointbehaviors.md) | <span data-ttu-id="f8f3a-112">指定端點行為。</span><span class="sxs-lookup"><span data-stu-id="f8f3a-112">Specifies an endpoint behavior.</span></span> |

## <a name="remarks"></a><span data-ttu-id="f8f3a-113">備註</span><span class="sxs-lookup"><span data-stu-id="f8f3a-113">Remarks</span></span>

<span data-ttu-id="f8f3a-114">SOAP 處理是在訊息版本之間轉換訊息的程序。</span><span class="sxs-lookup"><span data-stu-id="f8f3a-114">SOAP processing is the process where messages are converted between message versions.</span></span>

<span data-ttu-id="f8f3a-115">Windows Communication Foundation （WCF）路由服務可以將訊息從一個通訊協定轉換成另一個。</span><span class="sxs-lookup"><span data-stu-id="f8f3a-115">The Windows Communication Foundation (WCF) Routing Service can convert messages from one protocol to another.</span></span> <span data-ttu-id="f8f3a-116">如果傳入及傳出的訊息版本不同，會建立正確版本的新訊息。</span><span class="sxs-lookup"><span data-stu-id="f8f3a-116">If the incoming and outgoing Message Versions are different, a new message of the correct version is created.</span></span> <span data-ttu-id="f8f3a-117">在 <xref:System.ServiceModel.Channels.MessageVersion> 之間處理訊息，是透過建構包含來自傳入 WCF 訊息的主體部分和相關標頭的新 WCF 訊息來完成。</span><span class="sxs-lookup"><span data-stu-id="f8f3a-117">Processing messages from one <xref:System.ServiceModel.Channels.MessageVersion> to another is accomplished by constructing a new WCF message that contains the body part and relevant headers from the incoming WCF message.</span></span> <span data-ttu-id="f8f3a-118">定址專用或是在路由器層級辨識的標頭，不會在建構新 WCF 訊息期間使用，因為這些標頭不是屬於不同的版本 (若為定址標頭)，就是已做為用戶端和路由器之間通訊的一部分處理。</span><span class="sxs-lookup"><span data-stu-id="f8f3a-118">Headers that are specific to addressing, or that are understood at the router level, are not used during construction of the new WCF message because these headers are either of a different version (in the case of addressing headers) or have been processed as part of the communication between the client and the router.</span></span>

<span data-ttu-id="f8f3a-119">標頭是否放置在傳出訊息內，是透過標頭是否在通過傳入通道層時標記為辨識所決定。</span><span class="sxs-lookup"><span data-stu-id="f8f3a-119">Whether a header is placed in the outbound message is determined by whether or not it was marked as understood as it passed through the incoming channel layer.</span></span> <span data-ttu-id="f8f3a-120">未經辨識的標題 (例如自訂標題) 不會被移除，因此會透過複製到傳出訊息中的方式通過路由服務。</span><span class="sxs-lookup"><span data-stu-id="f8f3a-120">Headers that are not understood (such as custom headers) are not removed and so pass through the routing service by being copied to the outbound message.</span></span> <span data-ttu-id="f8f3a-121">訊息的主體會複製到傳出訊息中。</span><span class="sxs-lookup"><span data-stu-id="f8f3a-121">The body of the message is copied to the outbound message.</span></span> <span data-ttu-id="f8f3a-122">接著，會將訊息傳出到輸出通道，此時會建立並加入該通訊協定/傳輸專用的所有標題和其他封套資料。</span><span class="sxs-lookup"><span data-stu-id="f8f3a-122">The message is then sent out the outbound channel, at which point all of the headers and other envelope data specific to that communication protocol/transport will be created and added.</span></span>

<span data-ttu-id="f8f3a-123">此類處理步驟會在指定 SOAP 處理行為時發生。</span><span class="sxs-lookup"><span data-stu-id="f8f3a-123">Such processing steps take place when the SOAP processing behavior is specified.</span></span> <span data-ttu-id="f8f3a-124">此 [\<soapProcessingExtension>](soapprocessing.md) 行為是端點行為，會在路由服務啟動時套用至所有用戶端（傳出）端點。</span><span class="sxs-lookup"><span data-stu-id="f8f3a-124">This [\<soapProcessingExtension>](soapprocessing.md) behavior is an endpoint behavior that is applied to all client (outgoing) endpoints when the Routing Service starts up.</span></span> <span data-ttu-id="f8f3a-125">根據預設， [\<routing>](routing-of-servicebehavior.md) 行為會建立並附加新的行為，並 [\<soapProcessingExtension>](soapprocessing.md) `processMessages` 將 `true` 每個用戶端端點的設為。</span><span class="sxs-lookup"><span data-stu-id="f8f3a-125">default, the [\<routing>](routing-of-servicebehavior.md) behavior creates and attaches a new [\<soapProcessingExtension>](soapprocessing.md) behavior with `processMessages` set to `true` for each client endpoint.</span></span> <span data-ttu-id="f8f3a-126">如果路由服務無法辨識您的通訊協定，或者您想要覆寫預設的處理行為，可以停用整個路由服務的 SOAP 處理，或者只停用特定端點的 SOAP 處理。</span><span class="sxs-lookup"><span data-stu-id="f8f3a-126">If you have a protocol that the Routing Service does not understand, or wish to override the default processing behavior, you can disable SOAP processing either for the entire Routing Service or just for particular endpoints.</span></span>  <span data-ttu-id="f8f3a-127">若要在所有端點上停用整個路由服務的 SOAP 處理，請將 `soapProcessing` 行為的屬性設定 [\<routing>](routing-of-servicebehavior.md) 為 `false` 。</span><span class="sxs-lookup"><span data-stu-id="f8f3a-127">To disable SOAP processing for the entire routing service on all endpoints, set the `soapProcessing` attribute of the [\<routing>](routing-of-servicebehavior.md) behavior to `false`.</span></span> <span data-ttu-id="f8f3a-128">若要關閉特定端點的 SOAP 處理，請使用這個行為，並將其 `processMessages` 屬性設定為 `false`，然後將這個屬性附加至某個端點 (您不希望預設處理程式碼在此端點上執行)。</span><span class="sxs-lookup"><span data-stu-id="f8f3a-128">To turn off SOAP processing for a particular endpoint, use this behavior and set its `processMessages` attribute to `false`, then attach this behavior to the endpoint you do not want the default processing code to run at.</span></span>  <span data-ttu-id="f8f3a-129">當 [\<routing>](routing-of-servicebehavior.md) 行為設定路由服務時，它會略過重新套用端點行為，因為其中一個已存在。</span><span class="sxs-lookup"><span data-stu-id="f8f3a-129">When the [\<routing>](routing-of-servicebehavior.md) behavior sets up the Routing Service, it will skip reapplying the endpoint behavior since one already exists.</span></span>
