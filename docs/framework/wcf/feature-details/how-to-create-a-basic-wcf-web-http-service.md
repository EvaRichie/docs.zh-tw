---
title: HOW TO：建立基本 WCF Web HTTP 服務
description: 瞭解如何建立可在 WCF 中公開 web 端點的服務。 Web 端點會使用 XML 或 JSON 來傳送資料。 沒有 SOAP 封套。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 877662d3-d372-4e08-b417-51f66a0095cd
ms.openlocfilehash: 7481367f27d973ba809dff5ca1c4a4f168fbbb98
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85247100"
---
# <a name="how-to-create-a-basic-wcf-web-http-service"></a><span data-ttu-id="5a218-105">HOW TO：建立基本 WCF Web HTTP 服務</span><span class="sxs-lookup"><span data-stu-id="5a218-105">How to: Create a Basic WCF Web HTTP Service</span></span>

<span data-ttu-id="5a218-106">Windows Communication Foundation （WCF）可讓您建立公開 Web 端點的服務。</span><span class="sxs-lookup"><span data-stu-id="5a218-106">Windows Communication Foundation (WCF) allows you to create a service that exposes a Web endpoint.</span></span> <span data-ttu-id="5a218-107">Web 端點會透過 XML 或 JSON 來傳送資料，而且不使用任何 SOAP 封套。</span><span class="sxs-lookup"><span data-stu-id="5a218-107">Web endpoints send data by XML or JSON, there is no SOAP envelope.</span></span> <span data-ttu-id="5a218-108">本主題示範如何公開這類端點。</span><span class="sxs-lookup"><span data-stu-id="5a218-108">This topic demonstrates how to expose such an endpoint.</span></span>

> [!NOTE]
> <span data-ttu-id="5a218-109">保護 Web 端點的唯一方式，就是透過 HTTPS 運用傳輸安全性來加以公開。</span><span class="sxs-lookup"><span data-stu-id="5a218-109">The only way to secure a Web endpoint is to expose it through HTTPS, using transport security.</span></span> <span data-ttu-id="5a218-110">使用訊息安全性時，安全性資訊通常會放在 SOAP 標頭中，而傳送至非 SOAP 端點的訊息不包含任何 SOAP 封套，也就沒地方可以放置安全性資訊，因此您必須仰賴傳輸安全性。</span><span class="sxs-lookup"><span data-stu-id="5a218-110">When using message-based security, security information is usually placed in SOAP headers and because the messages sent to non-SOAP endpoints contain no SOAP envelope, there is nowhere to place the security information and you must rely on transport security.</span></span>

## <a name="to-create-a-web-endpoint"></a><span data-ttu-id="5a218-111">若要建立 Web 端點</span><span class="sxs-lookup"><span data-stu-id="5a218-111">To create a Web endpoint</span></span>

1. <span data-ttu-id="5a218-112">透過加上 <xref:System.ServiceModel.ServiceContractAttribute>、<xref:System.ServiceModel.Web.WebInvokeAttribute> 和 <xref:System.ServiceModel.Web.WebGetAttribute> 屬性標示的介面來定義服務合約。</span><span class="sxs-lookup"><span data-stu-id="5a218-112">Define a service contract using an interface marked with the <xref:System.ServiceModel.ServiceContractAttribute>, <xref:System.ServiceModel.Web.WebInvokeAttribute> and the <xref:System.ServiceModel.Web.WebGetAttribute> attributes.</span></span>

     [!code-csharp[htBasicService#0](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#0)]
     [!code-vb[htBasicService#0](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#0)]

    > [!NOTE]
    > <span data-ttu-id="5a218-113">根據預設，<xref:System.ServiceModel.Web.WebInvokeAttribute> 會將 POST 呼叫對應至作業。</span><span class="sxs-lookup"><span data-stu-id="5a218-113">By default, <xref:System.ServiceModel.Web.WebInvokeAttribute> maps POST calls to the operation.</span></span> <span data-ttu-id="5a218-114">但是，您可以指定 "method=" 參數，以指定要對應至作業的 HTTP 方法 (例如，HEAD、PUT 和 DELETE)。</span><span class="sxs-lookup"><span data-stu-id="5a218-114">You can, however, specify the HTTP method (for example, HEAD, PUT, or DELETE) to map to the operation by specifying a "method=" parameter.</span></span> <span data-ttu-id="5a218-115"><xref:System.ServiceModel.Web.WebGetAttribute> 沒有 "method=" 參數，只能將 GET 呼叫對應至服務作業。</span><span class="sxs-lookup"><span data-stu-id="5a218-115"><xref:System.ServiceModel.Web.WebGetAttribute> does not have a "method=" parameter and only maps GET calls to the service operation.</span></span>

2. <span data-ttu-id="5a218-116">實作服務合約。</span><span class="sxs-lookup"><span data-stu-id="5a218-116">Implement the service contract.</span></span>

     [!code-csharp[htBasicService#1](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#1)]
     [!code-vb[htBasicService#1](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#1)]

## <a name="to-host-the-service"></a><span data-ttu-id="5a218-117">若要裝載服務</span><span class="sxs-lookup"><span data-stu-id="5a218-117">To host the service</span></span>

1. <span data-ttu-id="5a218-118">建立 <xref:System.ServiceModel.Web.WebServiceHost> 物件。</span><span class="sxs-lookup"><span data-stu-id="5a218-118">Create a <xref:System.ServiceModel.Web.WebServiceHost> object.</span></span>

     [!code-csharp[htBasicService#2](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#2)]
     [!code-vb[htBasicService#2](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#2)]

2. <span data-ttu-id="5a218-119">新增包含 <xref:System.ServiceModel.Description.ServiceEndpoint> 的 <xref:System.ServiceModel.Description.WebHttpBehavior>。</span><span class="sxs-lookup"><span data-stu-id="5a218-119">Add a <xref:System.ServiceModel.Description.ServiceEndpoint> with the <xref:System.ServiceModel.Description.WebHttpBehavior>.</span></span>

     [!code-csharp[htBasicService#3](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#3)]
     [!code-vb[htBasicService#3](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#3)]

    > [!NOTE]
    > <span data-ttu-id="5a218-120">如果您沒有加入端點，<xref:System.ServiceModel.Web.WebServiceHost> 會自動建立預設端點。</span><span class="sxs-lookup"><span data-stu-id="5a218-120">If you do not add an endpoint, <xref:System.ServiceModel.Web.WebServiceHost> automatically creates a default endpoint.</span></span> <span data-ttu-id="5a218-121"><xref:System.ServiceModel.Web.WebServiceHost> 也會加入 <xref:System.ServiceModel.Description.WebHttpBehavior>，並停用 HTTP 說明網頁和 Web 服務描述語言 (WSDL) 的 GET 功能，使中繼資料端點不會干擾預設 HTTP 端點。</span><span class="sxs-lookup"><span data-stu-id="5a218-121"><xref:System.ServiceModel.Web.WebServiceHost> also adds <xref:System.ServiceModel.Description.WebHttpBehavior> and disables the HTTP Help page and the Web Services Description Language (WSDL) GET functionality so the metadata endpoint does not interfere with the default HTTP endpoint.</span></span>
    >
    >  <span data-ttu-id="5a218-122">如果新增包含 "" 的 URL 非 SOAP 端點，會在嘗試呼叫端點上的作業時導致未預期的行為。</span><span class="sxs-lookup"><span data-stu-id="5a218-122">Adding a non-SOAP endpoint with a URL of "" causes unexpected behavior when an attempt is made to call an operation on the endpoint.</span></span> <span data-ttu-id="5a218-123">這種情況的原因是端點的接聽 URI 與 [說明] 頁面（當您流覽至 WCF 服務的基底位址時所顯示的頁面）的 URI 相同。</span><span class="sxs-lookup"><span data-stu-id="5a218-123">The reason for this is the listen URI of the endpoint is the same as the URI for the help page (the page that is displayed when you browse to the base address of a WCF service).</span></span>

     <span data-ttu-id="5a218-124">您可以執行下列其中一項動作來預防發生這種情況：</span><span class="sxs-lookup"><span data-stu-id="5a218-124">You can do one of the following actions to prevent this from happening:</span></span>

    - <span data-ttu-id="5a218-125">一律為非 SOAP 端點指定非空白的 URI。</span><span class="sxs-lookup"><span data-stu-id="5a218-125">Always specify a non-blank URI for a non-SOAP endpoint.</span></span>

    - <span data-ttu-id="5a218-126">關閉說明頁面。</span><span class="sxs-lookup"><span data-stu-id="5a218-126">Turn off the help page.</span></span> <span data-ttu-id="5a218-127">這可以使用下列程式碼來完成：</span><span class="sxs-lookup"><span data-stu-id="5a218-127">This can be done with the following code:</span></span>

     [!code-csharp[htBasicService#4](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/snippets.cs#4)]
     [!code-vb[htBasicService#4](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/snippets.vb#4)]

3. <span data-ttu-id="5a218-128">開啟服務主機並等候使用者按下 ENTER。</span><span class="sxs-lookup"><span data-stu-id="5a218-128">Open the service host and wait until the user presses ENTER.</span></span>

     [!code-csharp[htBasicService#5](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/snippets.cs#5)]
     [!code-vb[htBasicService#5](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/snippets.vb#5)]

     <span data-ttu-id="5a218-129">此範例示範如何使用主控台應用程式來裝載 Web 樣式服務。</span><span class="sxs-lookup"><span data-stu-id="5a218-129">This sample demonstrates how to host a Web-Style service with a console application.</span></span> <span data-ttu-id="5a218-130">您也可以透過 IIS 裝載這類服務。</span><span class="sxs-lookup"><span data-stu-id="5a218-130">You can also host such a service within IIS.</span></span> <span data-ttu-id="5a218-131">若要這麼做，請在 .svc 檔案中指定 <xref:System.ServiceModel.Activation.WebServiceHostFactory> 類別，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="5a218-131">To do this, specify the <xref:System.ServiceModel.Activation.WebServiceHostFactory> class in a .svc file as the following code demonstrates.</span></span>

    ```text
    <%ServiceHost
        language=c#
        Debug="true"
        Service="Microsoft.Samples.Service"
        Factory=System.ServiceModel.Activation.WebServiceHostFactory%>
    ```

## <a name="to-call-service-operations-mapped-to-get-in-internet-explorer"></a><span data-ttu-id="5a218-132">若要在 Internet Explorer 中呼叫對應至 GET 的服務作業</span><span class="sxs-lookup"><span data-stu-id="5a218-132">To call service operations mapped to GET in Internet Explorer</span></span>

1. <span data-ttu-id="5a218-133">開啟 Internet Explorer 並輸入 " `http://localhost:8000/EchoWithGet?s=Hello, world!` "，然後按 enter。</span><span class="sxs-lookup"><span data-stu-id="5a218-133">Open Internet Explorer and type "`http://localhost:8000/EchoWithGet?s=Hello, world!`" and press ENTER.</span></span> <span data-ttu-id="5a218-134">URL 包含服務的基底位址（ `http://localhost:8000/` ）、端點的相對位址（""）、要呼叫的服務作業（"EchoWithGet"），以及後面接著以連字號（&）分隔之具名引數清單的問號。</span><span class="sxs-lookup"><span data-stu-id="5a218-134">The URL contains the base address of the service (`http://localhost:8000/`), the relative address of the endpoint (""), the service operation to call ("EchoWithGet"), and a question mark followed by a list of named parameters separated by an ampersand (&).</span></span>

## <a name="to-call-service-operations-in-code"></a><span data-ttu-id="5a218-135">若要透過程式碼呼叫服務作業</span><span class="sxs-lookup"><span data-stu-id="5a218-135">To call service operations in code</span></span>

1. <span data-ttu-id="5a218-136">在 <xref:System.ServiceModel.ChannelFactory%601> 區塊中建立 `using` 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="5a218-136">Create an instance of <xref:System.ServiceModel.ChannelFactory%601> within a `using` block.</span></span>

     [!code-csharp[htBasicService#6](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#6)]
     [!code-vb[htBasicService#6](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#6)]

2. <span data-ttu-id="5a218-137">將 <xref:System.ServiceModel.Description.WebHttpBehavior> 加入至 <xref:System.ServiceModel.ChannelFactory%601> 所呼叫的端點。</span><span class="sxs-lookup"><span data-stu-id="5a218-137">Add <xref:System.ServiceModel.Description.WebHttpBehavior> to the endpoint the <xref:System.ServiceModel.ChannelFactory%601> calls.</span></span>

     [!code-csharp[htBasicService#7](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#7)]
     [!code-vb[htBasicService#7](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#7)]

3. <span data-ttu-id="5a218-138">建立通道並呼叫服務。</span><span class="sxs-lookup"><span data-stu-id="5a218-138">Create the channel and call the service.</span></span>

     [!code-csharp[htBasicService#8](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#8)]
     [!code-vb[htBasicService#8](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#8)]

4. <span data-ttu-id="5a218-139">關閉 <xref:System.ServiceModel.Web.WebServiceHost>。</span><span class="sxs-lookup"><span data-stu-id="5a218-139">Close the <xref:System.ServiceModel.Web.WebServiceHost>.</span></span>

     [!code-csharp[htBasicService#9](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#9)]
     [!code-vb[htBasicService#9](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#9)]

## <a name="example"></a><span data-ttu-id="5a218-140">範例</span><span class="sxs-lookup"><span data-stu-id="5a218-140">Example</span></span>

<span data-ttu-id="5a218-141">以下是這個範例的完整程式碼清單。</span><span class="sxs-lookup"><span data-stu-id="5a218-141">The following is the full code listing for this example.</span></span>

[!code-csharp[htBasicService#10](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#10)]
[!code-vb[htBasicService#10](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#10)]

## <a name="compiling-the-code"></a><span data-ttu-id="5a218-142">編譯程式碼</span><span class="sxs-lookup"><span data-stu-id="5a218-142">Compiling the code</span></span>

<span data-ttu-id="5a218-143">編譯 Service.cs 時，請參考 System.ServiceModel.dll 和 System.ServiceModel.Web.dll。</span><span class="sxs-lookup"><span data-stu-id="5a218-143">When compiling Service.cs reference System.ServiceModel.dll and System.ServiceModel.Web.dll.</span></span>

## <a name="see-also"></a><span data-ttu-id="5a218-144">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5a218-144">See also</span></span>

- <xref:System.ServiceModel.WebHttpBinding>
- <xref:System.ServiceModel.Web.WebGetAttribute>
- <xref:System.ServiceModel.Web.WebInvokeAttribute>
- <xref:System.ServiceModel.Web.WebServiceHost>
- <xref:System.ServiceModel.Description.WebHttpBehavior>
- [<span data-ttu-id="5a218-145">WCF Web HTTP 程式設計模型</span><span class="sxs-lookup"><span data-stu-id="5a218-145">WCF Web HTTP Programming Model</span></span>](wcf-web-http-programming-model.md)
