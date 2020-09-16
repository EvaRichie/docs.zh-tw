---
title: 使用訊息層級程式設計序列化 Json
ms.date: 03/30/2017
ms.assetid: 5f940ba2-57ee-4c49-a779-957c5e7e71fa
ms.openlocfilehash: 129b39051e5955181c33e6486ec3193383177e60
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90546259"
---
# <a name="serializing-in-json-with-message-level-programming"></a><span data-ttu-id="c0d1d-102">使用訊息層級程式設計序列化 Json</span><span class="sxs-lookup"><span data-stu-id="c0d1d-102">Serializing in Json with Message Level Programming</span></span>
<span data-ttu-id="c0d1d-103">WCF 支援 JSON 格式的序列化資料。</span><span class="sxs-lookup"><span data-stu-id="c0d1d-103">WCF supports serializing data in JSON format.</span></span> <span data-ttu-id="c0d1d-104">本主題描述如何使用 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 來指示 WCF 序列化您的型別。</span><span class="sxs-lookup"><span data-stu-id="c0d1d-104">This topic describes how to tell WCF to serialize your types using the <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>.</span></span>  
  
## <a name="typed-message-programming"></a><span data-ttu-id="c0d1d-105">具型別的訊息程式設計</span><span class="sxs-lookup"><span data-stu-id="c0d1d-105">Typed Message Programming</span></span>  
 <span data-ttu-id="c0d1d-106">將 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 或 <xref:System.ServiceModel.Web.WebGetAttribute> 套用至服務作業時會使用 <xref:System.ServiceModel.Web.WebInvokeAttribute>。</span><span class="sxs-lookup"><span data-stu-id="c0d1d-106">The <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> is used when the <xref:System.ServiceModel.Web.WebGetAttribute> or the <xref:System.ServiceModel.Web.WebInvokeAttribute> is applied to a service operation.</span></span> <span data-ttu-id="c0d1d-107">這兩個屬性可讓您指定 `RequestFormat` 和 `ResponseFormat`。</span><span class="sxs-lookup"><span data-stu-id="c0d1d-107">Both of these attributes allow you to specify the `RequestFormat` and `ResponseFormat`.</span></span> <span data-ttu-id="c0d1d-108">針對要求和回應使用 JSON。</span><span class="sxs-lookup"><span data-stu-id="c0d1d-108">To use JSON for requests and responses.</span></span> <span data-ttu-id="c0d1d-109">將這兩個設定為 `WebMessageFormat.Json` 。</span><span class="sxs-lookup"><span data-stu-id="c0d1d-109">set both of these to `WebMessageFormat.Json`.</span></span>  <span data-ttu-id="c0d1d-110">若要使用 JSON，您必須使用自動設定 <xref:System.ServiceModel.WebHttpBinding> 的 <xref:System.ServiceModel.Description.WebHttpBehavior> 。</span><span class="sxs-lookup"><span data-stu-id="c0d1d-110">In order to use JSON, you must use the <xref:System.ServiceModel.WebHttpBinding>, which automatically configures the <xref:System.ServiceModel.Description.WebHttpBehavior>.</span></span> <span data-ttu-id="c0d1d-111">如需 WCF 序列化的詳細資訊，請參閱 [序列化和還原序列化](serialization-and-deserialization.md)。</span><span class="sxs-lookup"><span data-stu-id="c0d1d-111">For more information about WCF serialization, see [Serialization and Deserialization](serialization-and-deserialization.md).</span></span> <span data-ttu-id="c0d1d-112">如需 JSON 和 WCF 的詳細資訊，請參閱 [Service 站-使用 WCF RESTful 服務的簡介](/archive/msdn-magazine/2009/january/service-station-an-introduction-to-restful-services-with-wcf)。</span><span class="sxs-lookup"><span data-stu-id="c0d1d-112">For more information about JSON and WCF, see [Service Station - An Introduction To RESTful Services With WCF](/archive/msdn-magazine/2009/january/service-station-an-introduction-to-restful-services-with-wcf).</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="c0d1d-113">使用 JSON 需要使用 <xref:System.ServiceModel.WebHttpBinding> 和 <xref:System.ServiceModel.Description.WebHttpBehavior>，但這兩者不支援 SOAP 通訊。</span><span class="sxs-lookup"><span data-stu-id="c0d1d-113">Using JSON requires use of <xref:System.ServiceModel.WebHttpBinding> and <xref:System.ServiceModel.Description.WebHttpBehavior> which do not support SOAP communication.</span></span> <span data-ttu-id="c0d1d-114">與通訊的服務 <xref:System.ServiceModel.WebHttpBinding> 不支援公開服務中繼資料，因此您將無法使用 Visual Studio 的加入服務參考功能或 svcutil 命令列工具來產生用戶端 proxy。</span><span class="sxs-lookup"><span data-stu-id="c0d1d-114">Services that communicate with the <xref:System.ServiceModel.WebHttpBinding> do not support exposing service metadata so you will not be able to use Visual Studio’s Add Service Reference functionality or the svcutil command-line tool to generate a client-side proxy.</span></span> <span data-ttu-id="c0d1d-115">如需如何以程式設計方式呼叫使用之服務的詳細資訊 <xref:System.ServiceModel.WebHttpBinding> ，請參閱 [如何使用 WCF 取用 REST 服務](/archive/blogs/pedram/how-to-consume-rest-services-with-wcf)。</span><span class="sxs-lookup"><span data-stu-id="c0d1d-115">For more information how you can programmatically call services that use <xref:System.ServiceModel.WebHttpBinding>, see [How to Consume REST Services with WCF](/archive/blogs/pedram/how-to-consume-rest-services-with-wcf).</span></span>  
  
## <a name="untyped-message-programming"></a><span data-ttu-id="c0d1d-116">不具型別的訊息程式設計</span><span class="sxs-lookup"><span data-stu-id="c0d1d-116">Untyped Message Programming</span></span>  
 <span data-ttu-id="c0d1d-117">直接使用不具型別的訊息物件時，您必須明確設定不具型別訊息上的屬性，以將其序列化為 JSON。</span><span class="sxs-lookup"><span data-stu-id="c0d1d-117">When working directly with untyped Message objects, you must explicitly set the properties on the untyped message to serialize it as JSON.</span></span> <span data-ttu-id="c0d1d-118">下列程式碼片段示範如何執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="c0d1d-118">The following code snippet shows how to do this.</span></span>  
  
```csharp
 Message response = Message.CreateMessage(  
                  MessageVersion.None,    // No SOAP message version  
                             "*",                     // SOAP action, ignored since this is JSON  
                             "Response string: JSON format specified", // Message body  
                             new DataContractJsonSerializer(typeof(string))); // Specify DataContractJsonSerializer  
      response.Properties.Add( WebBodyFormatMessageProperty.Name,
                    new WebBodyFormatMessageProperty(WebContentFormat.Json)); // Use JSON format  
```  
  
## <a name="see-also"></a><span data-ttu-id="c0d1d-119">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c0d1d-119">See also</span></span>

- [<span data-ttu-id="c0d1d-120">AJAX 整合與 JSON 支援</span><span class="sxs-lookup"><span data-stu-id="c0d1d-120">AJAX Integration and JSON Support</span></span>](ajax-integration-and-json-support.md)
- [<span data-ttu-id="c0d1d-121">獨立 JSON 序列化</span><span class="sxs-lookup"><span data-stu-id="c0d1d-121">Stand-Alone JSON Serialization</span></span>](stand-alone-json-serialization.md)
- [<span data-ttu-id="c0d1d-122">JSON 序列化</span><span class="sxs-lookup"><span data-stu-id="c0d1d-122">JSON Serialization</span></span>](../samples/json-serialization.md)
