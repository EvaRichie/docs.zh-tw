---
title: HttpTransportBindingElement
ms.date: 03/30/2017
ms.assetid: 088a7bce-6bb2-4839-ad74-f68d4b1aa0f9
ms.openlocfilehash: 2be32591c4844cc6d5d0f02916dd1563bb15dc2a
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96288784"
---
# <a name="httptransportbindingelement"></a><span data-ttu-id="492ce-102">HttpTransportBindingElement</span><span class="sxs-lookup"><span data-stu-id="492ce-102">HttpTransportBindingElement</span></span>

<span data-ttu-id="492ce-103">HttpTransportBindingElement</span><span class="sxs-lookup"><span data-stu-id="492ce-103">HttpTransportBindingElement</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="492ce-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="492ce-104">Syntax</span></span>  
  
```csharp
class HttpTransportBindingElement : TransportBindingElement  
{  
  boolean AllowCookies;  
  string AuthenticationScheme;  
  boolean BypassProxyOnLocal;  
  string HostNameComparisonMode;  
  boolean KeepAliveEnabled;  
  sint32 MaxBufferSize;  
  string ProxyAddress;  
  string ProxyAuthenticationScheme;  
  string Realm;  
  string TransferMode;  
  boolean UnsafeConnectionNtlmAuthentication;  
  boolean UseDefaultWebProxy;  
};  
```  
  
## <a name="methods"></a><span data-ttu-id="492ce-105">方法</span><span class="sxs-lookup"><span data-stu-id="492ce-105">Methods</span></span>  

 <span data-ttu-id="492ce-106">HttpTransportBindingElement 類別並未定義任何方法。</span><span class="sxs-lookup"><span data-stu-id="492ce-106">The HttpTransportBindingElement class does not define any methods.</span></span>  
  
## <a name="properties"></a><span data-ttu-id="492ce-107">屬性</span><span class="sxs-lookup"><span data-stu-id="492ce-107">Properties</span></span>  

 <span data-ttu-id="492ce-108">HttpTransportBindingElement 類別具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="492ce-108">The HttpTransportBindingElement class has the following properties:</span></span>  
  
### <a name="allowcookies"></a><span data-ttu-id="492ce-109">AllowCookies</span><span class="sxs-lookup"><span data-stu-id="492ce-109">AllowCookies</span></span>  

 <span data-ttu-id="492ce-110">資料型別：布林值</span><span class="sxs-lookup"><span data-stu-id="492ce-110">Data type: boolean</span></span>  
  
 <span data-ttu-id="492ce-111">存取類型：唯讀</span><span class="sxs-lookup"><span data-stu-id="492ce-111">Access type: Read-only</span></span>  
  
 <span data-ttu-id="492ce-112">表示用戶端是否接受 Cookie 並在未來的要求傳播 Cookie 的值。</span><span class="sxs-lookup"><span data-stu-id="492ce-112">A value that indicates whether the client accepts cookies and propagates them on future requests.</span></span>  
  
### <a name="authenticationscheme"></a><span data-ttu-id="492ce-113">AuthenticationScheme</span><span class="sxs-lookup"><span data-stu-id="492ce-113">AuthenticationScheme</span></span>  

 <span data-ttu-id="492ce-114">資料類型：字串</span><span class="sxs-lookup"><span data-stu-id="492ce-114">Data type: string</span></span>  
  
 <span data-ttu-id="492ce-115">存取類型：唯讀</span><span class="sxs-lookup"><span data-stu-id="492ce-115">Access type: Read-only</span></span>  
  
 <span data-ttu-id="492ce-116">用於驗證由 HTTP 接聽項處理之用戶端要求的驗證配置。</span><span class="sxs-lookup"><span data-stu-id="492ce-116">The authentication scheme used to authenticate client requests being processed by an HTTP listener.</span></span>  
  
### <a name="bypassproxyonlocal"></a><span data-ttu-id="492ce-117">BypassProxyOnLocal</span><span class="sxs-lookup"><span data-stu-id="492ce-117">BypassProxyOnLocal</span></span>  

 <span data-ttu-id="492ce-118">資料型別：布林值</span><span class="sxs-lookup"><span data-stu-id="492ce-118">Data type: boolean</span></span>  
  
 <span data-ttu-id="492ce-119">存取類型：唯讀</span><span class="sxs-lookup"><span data-stu-id="492ce-119">Access type: Read-only</span></span>  
  
 <span data-ttu-id="492ce-120">代表是否針對本機位址略過 Proxy 的值。</span><span class="sxs-lookup"><span data-stu-id="492ce-120">A value that indicates whether proxies are ignored for local addresses.</span></span>  
  
### <a name="hostnamecomparisonmode"></a><span data-ttu-id="492ce-121">HostNameComparisonMode</span><span class="sxs-lookup"><span data-stu-id="492ce-121">HostNameComparisonMode</span></span>  

 <span data-ttu-id="492ce-122">資料類型：字串</span><span class="sxs-lookup"><span data-stu-id="492ce-122">Data type: string</span></span>  
  
 <span data-ttu-id="492ce-123">存取類型：唯讀</span><span class="sxs-lookup"><span data-stu-id="492ce-123">Access type: Read-only</span></span>  
  
 <span data-ttu-id="492ce-124">代表主機名稱是否用於連線到服務的值 (當符合 URI 時)。</span><span class="sxs-lookup"><span data-stu-id="492ce-124">A value that indicates whether the hostname is used to reach the service when matching on the URI.</span></span>  
  
### <a name="keepaliveenabled"></a><span data-ttu-id="492ce-125">KeepAliveEnabled</span><span class="sxs-lookup"><span data-stu-id="492ce-125">KeepAliveEnabled</span></span>  

 <span data-ttu-id="492ce-126">資料型別：布林值</span><span class="sxs-lookup"><span data-stu-id="492ce-126">Data type: boolean</span></span>  
  
 <span data-ttu-id="492ce-127">存取類型：唯讀</span><span class="sxs-lookup"><span data-stu-id="492ce-127">Access type: Read-only</span></span>  
  
 <span data-ttu-id="492ce-128">啟用時，不論活動等級為何，HTTP 連線會維持開啟。</span><span class="sxs-lookup"><span data-stu-id="492ce-128">When enabled, HTTP connections are kept alive regardless of activity level.</span></span>  
  
### <a name="maxbuffersize"></a><span data-ttu-id="492ce-129">MaxBufferSize</span><span class="sxs-lookup"><span data-stu-id="492ce-129">MaxBufferSize</span></span>  

 <span data-ttu-id="492ce-130">資料型別：sint32</span><span class="sxs-lookup"><span data-stu-id="492ce-130">Data type: sint32</span></span>  
  
 <span data-ttu-id="492ce-131">存取類型：唯讀</span><span class="sxs-lookup"><span data-stu-id="492ce-131">Access type: Read-only</span></span>  
  
 <span data-ttu-id="492ce-132">緩衝集區的大小上限。</span><span class="sxs-lookup"><span data-stu-id="492ce-132">The maximum size of the buffer pool.</span></span>  
  
### <a name="proxyaddress"></a><span data-ttu-id="492ce-133">ProxyAddress</span><span class="sxs-lookup"><span data-stu-id="492ce-133">ProxyAddress</span></span>  

 <span data-ttu-id="492ce-134">資料類型：字串</span><span class="sxs-lookup"><span data-stu-id="492ce-134">Data type: string</span></span>  
  
 <span data-ttu-id="492ce-135">存取類型：唯讀</span><span class="sxs-lookup"><span data-stu-id="492ce-135">Access type: Read-only</span></span>  
  
 <span data-ttu-id="492ce-136">包含用於 HTTP 要求之 Proxy 位址的 URI。</span><span class="sxs-lookup"><span data-stu-id="492ce-136">A URI that contains the address of the proxy to use for HTTP requests.</span></span>  
  
### <a name="proxyauthenticationscheme"></a><span data-ttu-id="492ce-137">ProxyAuthenticationScheme</span><span class="sxs-lookup"><span data-stu-id="492ce-137">ProxyAuthenticationScheme</span></span>  

 <span data-ttu-id="492ce-138">資料類型：字串</span><span class="sxs-lookup"><span data-stu-id="492ce-138">Data type: string</span></span>  
  
 <span data-ttu-id="492ce-139">存取類型：唯讀</span><span class="sxs-lookup"><span data-stu-id="492ce-139">Access type: Read-only</span></span>  
  
 <span data-ttu-id="492ce-140">用於驗證由 HTTP Proxy 處理之用戶端要求的驗證配置。</span><span class="sxs-lookup"><span data-stu-id="492ce-140">The authentication scheme used to authenticate client requests being processed by an HTTP proxy.</span></span>  
  
### <a name="realm"></a><span data-ttu-id="492ce-141">Realm</span><span class="sxs-lookup"><span data-stu-id="492ce-141">Realm</span></span>  

 <span data-ttu-id="492ce-142">資料類型：字串</span><span class="sxs-lookup"><span data-stu-id="492ce-142">Data type: string</span></span>  
  
 <span data-ttu-id="492ce-143">存取類型：唯讀</span><span class="sxs-lookup"><span data-stu-id="492ce-143">Access type: Read-only</span></span>  
  
 <span data-ttu-id="492ce-144">驗證領域。</span><span class="sxs-lookup"><span data-stu-id="492ce-144">The authentication realm.</span></span>  
  
### <a name="transfermode"></a><span data-ttu-id="492ce-145">TransferMode</span><span class="sxs-lookup"><span data-stu-id="492ce-145">TransferMode</span></span>  

 <span data-ttu-id="492ce-146">資料類型：字串</span><span class="sxs-lookup"><span data-stu-id="492ce-146">Data type: string</span></span>  
  
 <span data-ttu-id="492ce-147">存取類型：唯讀</span><span class="sxs-lookup"><span data-stu-id="492ce-147">Access type: Read-only</span></span>  
  
 <span data-ttu-id="492ce-148">代表訊息是經過緩衝處理或資料流處理，或為要求或回應的值。</span><span class="sxs-lookup"><span data-stu-id="492ce-148">A value that specifies whether messages are buffered or streamed or a request or response.</span></span>  
  
### <a name="unsafeconnectionntlmauthentication"></a><span data-ttu-id="492ce-149">UnsafeConnectionNtlmAuthentication</span><span class="sxs-lookup"><span data-stu-id="492ce-149">UnsafeConnectionNtlmAuthentication</span></span>  

 <span data-ttu-id="492ce-150">資料型別：布林值</span><span class="sxs-lookup"><span data-stu-id="492ce-150">Data type: boolean</span></span>  
  
 <span data-ttu-id="492ce-151">存取類型：唯讀</span><span class="sxs-lookup"><span data-stu-id="492ce-151">Access type: Read-only</span></span>  
  
 <span data-ttu-id="492ce-152">代表是否已在伺服器啟用「不安全的連線共用」的值。</span><span class="sxs-lookup"><span data-stu-id="492ce-152">A value that indicates whether Unsafe Connection Sharing is enabled on the server.</span></span>  
  
### <a name="usedefaultwebproxy"></a><span data-ttu-id="492ce-153">UseDefaultWebProxy</span><span class="sxs-lookup"><span data-stu-id="492ce-153">UseDefaultWebProxy</span></span>  

 <span data-ttu-id="492ce-154">資料型別：布林值</span><span class="sxs-lookup"><span data-stu-id="492ce-154">Data type: boolean</span></span>  
  
 <span data-ttu-id="492ce-155">存取類型：唯讀</span><span class="sxs-lookup"><span data-stu-id="492ce-155">Access type: Read-only</span></span>  
  
 <span data-ttu-id="492ce-156">代表是否使用全機器追蹤 Proxy 設定，而非使用者特定設定的值。</span><span class="sxs-lookup"><span data-stu-id="492ce-156">A value that indicates whether the machine-wide proxy settings are used rather than the user specific settings.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="492ce-157">規格需求</span><span class="sxs-lookup"><span data-stu-id="492ce-157">Requirements</span></span>  
  
|<span data-ttu-id="492ce-158">MOF</span><span class="sxs-lookup"><span data-stu-id="492ce-158">MOF</span></span>|<span data-ttu-id="492ce-159">於 Servicemodel.mof 中宣告。</span><span class="sxs-lookup"><span data-stu-id="492ce-159">Declared in Servicemodel.mof.</span></span>|  
|---------|-----------------------------------|  
|<span data-ttu-id="492ce-160">命名空間</span><span class="sxs-lookup"><span data-stu-id="492ce-160">Namespace</span></span>|<span data-ttu-id="492ce-161">於 root\ServiceModel 中定義</span><span class="sxs-lookup"><span data-stu-id="492ce-161">Defined in root\ServiceModel</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="492ce-162">另請參閱</span><span class="sxs-lookup"><span data-stu-id="492ce-162">See also</span></span>

- <xref:System.ServiceModel.Channels.HttpTransportBindingElement>
