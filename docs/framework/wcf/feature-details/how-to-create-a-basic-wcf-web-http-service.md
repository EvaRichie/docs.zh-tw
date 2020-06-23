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
# <a name="how-to-create-a-basic-wcf-web-http-service"></a>HOW TO：建立基本 WCF Web HTTP 服務

Windows Communication Foundation （WCF）可讓您建立公開 Web 端點的服務。 Web 端點會透過 XML 或 JSON 來傳送資料，而且不使用任何 SOAP 封套。 本主題示範如何公開這類端點。

> [!NOTE]
> 保護 Web 端點的唯一方式，就是透過 HTTPS 運用傳輸安全性來加以公開。 使用訊息安全性時，安全性資訊通常會放在 SOAP 標頭中，而傳送至非 SOAP 端點的訊息不包含任何 SOAP 封套，也就沒地方可以放置安全性資訊，因此您必須仰賴傳輸安全性。

## <a name="to-create-a-web-endpoint"></a>若要建立 Web 端點

1. 透過加上 <xref:System.ServiceModel.ServiceContractAttribute>、<xref:System.ServiceModel.Web.WebInvokeAttribute> 和 <xref:System.ServiceModel.Web.WebGetAttribute> 屬性標示的介面來定義服務合約。

     [!code-csharp[htBasicService#0](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#0)]
     [!code-vb[htBasicService#0](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#0)]

    > [!NOTE]
    > 根據預設，<xref:System.ServiceModel.Web.WebInvokeAttribute> 會將 POST 呼叫對應至作業。 但是，您可以指定 "method=" 參數，以指定要對應至作業的 HTTP 方法 (例如，HEAD、PUT 和 DELETE)。 <xref:System.ServiceModel.Web.WebGetAttribute> 沒有 "method=" 參數，只能將 GET 呼叫對應至服務作業。

2. 實作服務合約。

     [!code-csharp[htBasicService#1](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#1)]
     [!code-vb[htBasicService#1](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#1)]

## <a name="to-host-the-service"></a>若要裝載服務

1. 建立 <xref:System.ServiceModel.Web.WebServiceHost> 物件。

     [!code-csharp[htBasicService#2](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#2)]
     [!code-vb[htBasicService#2](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#2)]

2. 新增包含 <xref:System.ServiceModel.Description.ServiceEndpoint> 的 <xref:System.ServiceModel.Description.WebHttpBehavior>。

     [!code-csharp[htBasicService#3](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#3)]
     [!code-vb[htBasicService#3](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#3)]

    > [!NOTE]
    > 如果您沒有加入端點，<xref:System.ServiceModel.Web.WebServiceHost> 會自動建立預設端點。 <xref:System.ServiceModel.Web.WebServiceHost> 也會加入 <xref:System.ServiceModel.Description.WebHttpBehavior>，並停用 HTTP 說明網頁和 Web 服務描述語言 (WSDL) 的 GET 功能，使中繼資料端點不會干擾預設 HTTP 端點。
    >
    >  如果新增包含 "" 的 URL 非 SOAP 端點，會在嘗試呼叫端點上的作業時導致未預期的行為。 這種情況的原因是端點的接聽 URI 與 [說明] 頁面（當您流覽至 WCF 服務的基底位址時所顯示的頁面）的 URI 相同。

     您可以執行下列其中一項動作來預防發生這種情況：

    - 一律為非 SOAP 端點指定非空白的 URI。

    - 關閉說明頁面。 這可以使用下列程式碼來完成：

     [!code-csharp[htBasicService#4](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/snippets.cs#4)]
     [!code-vb[htBasicService#4](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/snippets.vb#4)]

3. 開啟服務主機並等候使用者按下 ENTER。

     [!code-csharp[htBasicService#5](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/snippets.cs#5)]
     [!code-vb[htBasicService#5](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/snippets.vb#5)]

     此範例示範如何使用主控台應用程式來裝載 Web 樣式服務。 您也可以透過 IIS 裝載這類服務。 若要這麼做，請在 .svc 檔案中指定 <xref:System.ServiceModel.Activation.WebServiceHostFactory> 類別，如下列程式碼所示。

    ```text
    <%ServiceHost
        language=c#
        Debug="true"
        Service="Microsoft.Samples.Service"
        Factory=System.ServiceModel.Activation.WebServiceHostFactory%>
    ```

## <a name="to-call-service-operations-mapped-to-get-in-internet-explorer"></a>若要在 Internet Explorer 中呼叫對應至 GET 的服務作業

1. 開啟 Internet Explorer 並輸入 " `http://localhost:8000/EchoWithGet?s=Hello, world!` "，然後按 enter。 URL 包含服務的基底位址（ `http://localhost:8000/` ）、端點的相對位址（""）、要呼叫的服務作業（"EchoWithGet"），以及後面接著以連字號（&）分隔之具名引數清單的問號。

## <a name="to-call-service-operations-in-code"></a>若要透過程式碼呼叫服務作業

1. 在 <xref:System.ServiceModel.ChannelFactory%601> 區塊中建立 `using` 的執行個體。

     [!code-csharp[htBasicService#6](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#6)]
     [!code-vb[htBasicService#6](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#6)]

2. 將 <xref:System.ServiceModel.Description.WebHttpBehavior> 加入至 <xref:System.ServiceModel.ChannelFactory%601> 所呼叫的端點。

     [!code-csharp[htBasicService#7](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#7)]
     [!code-vb[htBasicService#7](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#7)]

3. 建立通道並呼叫服務。

     [!code-csharp[htBasicService#8](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#8)]
     [!code-vb[htBasicService#8](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#8)]

4. 關閉 <xref:System.ServiceModel.Web.WebServiceHost>。

     [!code-csharp[htBasicService#9](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#9)]
     [!code-vb[htBasicService#9](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#9)]

## <a name="example"></a>範例

以下是這個範例的完整程式碼清單。

[!code-csharp[htBasicService#10](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#10)]
[!code-vb[htBasicService#10](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#10)]

## <a name="compiling-the-code"></a>編譯程式碼

編譯 Service.cs 時，請參考 System.ServiceModel.dll 和 System.ServiceModel.Web.dll。

## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.WebHttpBinding>
- <xref:System.ServiceModel.Web.WebGetAttribute>
- <xref:System.ServiceModel.Web.WebInvokeAttribute>
- <xref:System.ServiceModel.Web.WebServiceHost>
- <xref:System.ServiceModel.Description.WebHttpBehavior>
- [WCF Web HTTP 程式設計模型](wcf-web-http-programming-model.md)
