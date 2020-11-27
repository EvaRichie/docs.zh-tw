---
title: 衍生自 WebResponse
ms.date: 03/30/2017
helpviewer_keywords:
- Deriving from WebResponse
ms.assetid: f11d4866-a199-4087-9306-a5a4c18b13db
ms.openlocfilehash: 793533b632952df3f0866bb6377efd0e313cd007
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96287523"
---
# <a name="deriving-from-webresponse"></a><span data-ttu-id="88f99-102">衍生自 WebResponse</span><span class="sxs-lookup"><span data-stu-id="88f99-102">Deriving from WebResponse</span></span>

<span data-ttu-id="88f99-103"><xref:System.Net.WebResponse> 類別是抽象的基底類別，提供基本的方法和屬性以建立有特定通訊協定回應，符合 .NET Framework 插入式通訊協定模型的處理常式。</span><span class="sxs-lookup"><span data-stu-id="88f99-103">The <xref:System.Net.WebResponse> class is an abstract base class that provides the basic methods and properties for creating a protocol-specific response that fits the .NET Framework pluggable protocol model.</span></span> <span data-ttu-id="88f99-104">使用 <xref:System.Net.WebRequest> 類別向資源要求資料的應用程式，會收到 **WebResponse** 的回應。</span><span class="sxs-lookup"><span data-stu-id="88f99-104">Applications that use the <xref:System.Net.WebRequest> class to request data from resources receive the responses in a **WebResponse**.</span></span> <span data-ttu-id="88f99-105">通訊協定特定的 **WebResponse** 子代必須實作 **WebResponse** 類別的抽象成員。</span><span class="sxs-lookup"><span data-stu-id="88f99-105">Protocol-specific **WebResponse** descendants must implement the abstract members of the **WebResponse** class.</span></span>  
  
 <span data-ttu-id="88f99-106">相關聯的 **WebRequest** 類別必須建立 **WebResponse** 子代。</span><span class="sxs-lookup"><span data-stu-id="88f99-106">The associated **WebRequest** class must create **WebResponse** descendants.</span></span> <span data-ttu-id="88f99-107">例如，只有呼叫 <xref:System.Net.HttpWebRequest.GetResponse%2A?displayProperty=nameWithType> 或 <xref:System.Net.HttpWebRequest.EndGetResponse%2A?displayProperty=nameWithType> 才會建立 <xref:System.Net.HttpWebResponse> 執行個體。</span><span class="sxs-lookup"><span data-stu-id="88f99-107">For example, <xref:System.Net.HttpWebResponse> instances are created only as the result of calling <xref:System.Net.HttpWebRequest.GetResponse%2A?displayProperty=nameWithType> or <xref:System.Net.HttpWebRequest.EndGetResponse%2A?displayProperty=nameWithType>.</span></span> <span data-ttu-id="88f99-108">每個 **WebResponse** 都包含向資源提出要求的結果，而且不能重複使用。</span><span class="sxs-lookup"><span data-stu-id="88f99-108">Each **WebResponse** contains the result of a request to a resource and is not intended to be reused.</span></span>  
  
## <a name="contentlength-property"></a><span data-ttu-id="88f99-109">ContentLength 屬性</span><span class="sxs-lookup"><span data-stu-id="88f99-109">ContentLength Property</span></span>  

 <span data-ttu-id="88f99-110"><xref:System.Net.WebResponse.ContentLength%2A> 屬性指出從 <xref:System.Net.WebResponse.GetResponseStream%2A> 方法傳回的資料流中可取得的資料位元組數目。</span><span class="sxs-lookup"><span data-stu-id="88f99-110">The <xref:System.Net.WebResponse.ContentLength%2A> property indicates the number of bytes of data that are available from the stream returned by the <xref:System.Net.WebResponse.GetResponseStream%2A> method.</span></span> <span data-ttu-id="88f99-111">**ContentLength** 屬性不會指出伺服器所傳回的標頭或中繼資料資訊的位元組數目，它只會指出所要求資源本身的資料位元組數目。</span><span class="sxs-lookup"><span data-stu-id="88f99-111">The **ContentLength** property does not indicate the number of bytes of header or metadata information returned by the server; it indicates only the number of bytes of data in the requested resource itself.</span></span>  
  
## <a name="contenttype-property"></a><span data-ttu-id="88f99-112">ContentType 屬性</span><span class="sxs-lookup"><span data-stu-id="88f99-112">ContentType Property</span></span>  

 <span data-ttu-id="88f99-113"><xref:System.Net.WebResponse.ContentType%2A> 屬性會提供您的通訊協定要求您傳送至用戶端的任何特殊資訊，以識別伺服器要傳送的內容類型。</span><span class="sxs-lookup"><span data-stu-id="88f99-113">The <xref:System.Net.WebResponse.ContentType%2A> property provides any special information that your protocol requires you to send to the client to identify the type of content being sent by the server.</span></span> <span data-ttu-id="88f99-114">這通常是任何傳回資料的 MIME 內容類型。</span><span class="sxs-lookup"><span data-stu-id="88f99-114">Typically this is the MIME content type of any data returned.</span></span>  
  
## <a name="headers-property"></a><span data-ttu-id="88f99-115">Headers 屬性</span><span class="sxs-lookup"><span data-stu-id="88f99-115">Headers Property</span></span>  

 <span data-ttu-id="88f99-116"><xref:System.Net.WebResponse.Headers%2A> 屬性包含與回應建立關聯的中繼資料名稱/值組任意集合。</span><span class="sxs-lookup"><span data-stu-id="88f99-116">The <xref:System.Net.WebResponse.Headers%2A> property contains an arbitrary collection of name/value pairs of metadata associated with the response.</span></span> <span data-ttu-id="88f99-117">**Headers** 屬性可以包含可表示為名稱/值組的通訊協定所需要的任何中繼資料。</span><span class="sxs-lookup"><span data-stu-id="88f99-117">Any metadata needed by the protocol that can be expressed as a name/value pair can be included in the **Headers** property.</span></span>  
  
 <span data-ttu-id="88f99-118">您不需要使用 **Headers** 屬性，也能使用標頭中繼資料。</span><span class="sxs-lookup"><span data-stu-id="88f99-118">You are not required to use the **Headers** property to use header metadata.</span></span> <span data-ttu-id="88f99-119">通訊協定特定的中繼資料可以公開為屬性。例如，<xref:System.Net.HttpWebResponse.LastModified%2A?displayProperty=nameWithType> 屬性會公開 **Last-Modified** HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="88f99-119">Protocol-specific metadata can be exposed as properties; for example, the <xref:System.Net.HttpWebResponse.LastModified%2A?displayProperty=nameWithType> property exposes the **Last-Modified** HTTP header.</span></span> <span data-ttu-id="88f99-120">當您將標頭中繼資料公開為屬性時，您不應該允許使用 **Headers** 屬性設定相同的屬性。</span><span class="sxs-lookup"><span data-stu-id="88f99-120">When you expose header metadata as a property, you should not allow the same property to be set using the **Headers** property.</span></span>  
  
## <a name="responseuri-property"></a><span data-ttu-id="88f99-121">ResponseUri 屬性</span><span class="sxs-lookup"><span data-stu-id="88f99-121">ResponseUri Property</span></span>  

 <span data-ttu-id="88f99-122"><xref:System.Net.WebResponse.ResponseUri%2A> 屬性包含實際提供回應的資源 URI。</span><span class="sxs-lookup"><span data-stu-id="88f99-122">The <xref:System.Net.WebResponse.ResponseUri%2A> property contains the URI of the resource that actually provided the response.</span></span> <span data-ttu-id="88f99-123">至於不支援重新導向的通訊協定，**ResponseUri** 會和建立回應的 **WebRequest** 的 <xref:System.Net.WebRequest.RequestUri%2A> 屬性相同。</span><span class="sxs-lookup"><span data-stu-id="88f99-123">For protocols that do not support redirection, **ResponseUri** will be the same as the <xref:System.Net.WebRequest.RequestUri%2A> property of the **WebRequest** that created the response.</span></span> <span data-ttu-id="88f99-124">如果通訊協定支援重新導向要求，**ResponseUri** 會包含回應的 URI。</span><span class="sxs-lookup"><span data-stu-id="88f99-124">If the protocol supports redirecting the request, **ResponseUri** will contain the URI of the response.</span></span>  
  
## <a name="close-method"></a><span data-ttu-id="88f99-125">Close 方法</span><span class="sxs-lookup"><span data-stu-id="88f99-125">Close Method</span></span>  

 <span data-ttu-id="88f99-126"><xref:System.Net.WebResponse.Close%2A> 方法關閉要求和回應所建立的任何連線，並清除回應所使用的資源。</span><span class="sxs-lookup"><span data-stu-id="88f99-126">The <xref:System.Net.WebResponse.Close%2A> method closes any connections made by the request and response and cleans up resources used by the response.</span></span> <span data-ttu-id="88f99-127">**Close** 方法會關閉回應所使用的任何資料流執行個體，但如果 <xref:System.IO.Stream.Close%2A?displayProperty=nameWithType> 方法的呼叫之前已關閉回應資料流，它不會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="88f99-127">The **Close** method closes any stream instances used by the response, but it does not throw an exception if the response stream was previously closed by a call to the <xref:System.IO.Stream.Close%2A?displayProperty=nameWithType> method.</span></span>  
  
## <a name="getresponsestream-method"></a><span data-ttu-id="88f99-128">GetResponseStream 方法</span><span class="sxs-lookup"><span data-stu-id="88f99-128">GetResponseStream Method</span></span>  

 <span data-ttu-id="88f99-129"><xref:System.Net.WebResponse.GetResponseStream%2A> 方法傳回的資料流會包含來自所要求資源的回應。</span><span class="sxs-lookup"><span data-stu-id="88f99-129">The <xref:System.Net.WebResponse.GetResponseStream%2A> method returns a stream containing the response from the requested resource.</span></span> <span data-ttu-id="88f99-130">回應資料流只包含資源傳回的資料，回應中包含的任何標頭或中繼資料都應從回應中移除，並透過通訊協定特有的屬性或 **Headers** 屬性向應用程式公開。</span><span class="sxs-lookup"><span data-stu-id="88f99-130">The response stream contains only the data returned by the resource; any header or metadata included in the response should be stripped from the response and exposed to the application through protocol-specific properties or the **Headers** property.</span></span>  
  
 <span data-ttu-id="88f99-131">**GetResponseStream** 方法所傳回的資料流執行個體為應用程式所擁有，而且不用關閉 **WebResponse** 即可關閉。</span><span class="sxs-lookup"><span data-stu-id="88f99-131">The stream instance returned by the **GetResponseStream** method is owned by the application and can be closed without closing the **WebResponse**.</span></span> <span data-ttu-id="88f99-132">依照慣例，呼叫 **WebResponse.Close** 方法也會關閉 **GetResponse** 傳回的資料流。</span><span class="sxs-lookup"><span data-stu-id="88f99-132">By convention, calling the **WebResponse.Close** method also closes the stream returned by **GetResponse**.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="88f99-133">另請參閱</span><span class="sxs-lookup"><span data-stu-id="88f99-133">See also</span></span>

- <xref:System.Net.WebResponse>
- <xref:System.Net.HttpWebResponse>
- <xref:System.Net.FileWebResponse>
- [<span data-ttu-id="88f99-134">可插式通訊協定程式設計</span><span class="sxs-lookup"><span data-stu-id="88f99-134">Programming Pluggable Protocols</span></span>](programming-pluggable-protocols.md)
- [<span data-ttu-id="88f99-135">衍生自 WebRequest</span><span class="sxs-lookup"><span data-stu-id="88f99-135">Deriving from WebRequest</span></span>](deriving-from-webrequest.md)
