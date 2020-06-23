---
title: HOW TO：使用 Windows 認證來確保服務安全
description: 瞭解如何在位於 Windows 網域中的 WCF 服務上啟用傳輸安全性，並由相同網域中的用戶端呼叫。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, security
ms.assetid: d171b5ca-96ef-47ff-800c-c138023cf76e
ms.openlocfilehash: 8ef164e1475bfd5f047a99426a2bed43a7aa7353
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85244629"
---
# <a name="how-to-secure-a-service-with-windows-credentials"></a>HOW TO：使用 Windows 認證來確保服務安全

本主題說明如何在位於 Windows 網域中的 Windows Communication Foundation （WCF）服務上啟用傳輸安全性，並由相同網域中的用戶端呼叫。 如需此案例的詳細資訊，請參閱[使用 Windows 驗證的傳輸安全性](./feature-details/transport-security-with-windows-authentication.md)。 如需範例應用程式，請參閱[WSHttpBinding](./samples/wshttpbinding.md)範例。

這個主題假設您擁有現有的合約介面、已定義了實作 (Implementation)，以及一些附加內容。 您也可以修改現有的服務和用戶端。

您可以完全使用程式碼，透過 Windows 認證來確保服務安全。 或者，您也可以使用組態檔來省略部分程式碼。 這個主題會說明這兩種方式。 請務必只使用其中一種方式，不要兩種都使用。

前三個程序會說明如何使用程式碼來保護服務安全。 第四和第五個程序會說明如何使用組態檔來執行這項作業。

## <a name="using-code"></a>使用程式碼

服務和用戶端的完整程式碼已提供於本主題結尾的「範例」一節。

第一個程序會逐步解說如何使用程式碼建立和設定 <xref:System.ServiceModel.WSHttpBinding> 類別。 繫結會使用 HTTP 傳輸。 用戶端上會使用相同的繫結。

#### <a name="to-create-a-wshttpbinding-that-uses-windows-credentials-and-message-security"></a>建立會使用 Windows 認證和訊息安全性的 WSHttpBinding

1. 這個程序的程式碼會插入至「範例」一節服務程式碼中 `Run` 類別的 `Test` 方法開頭。

2. 建立 <xref:System.ServiceModel.WSHttpBinding> 類別的執行個體。

3. 將 <xref:System.ServiceModel.WSHttpSecurity.Mode%2A> 類別的 <xref:System.ServiceModel.WSHttpSecurity> 屬性設定為 <xref:System.ServiceModel.SecurityMode.Message>。

4. 將 <xref:System.ServiceModel.MessageSecurityOverHttp.ClientCredentialType%2A> 類別的 <xref:System.ServiceModel.MessageSecurityOverHttp> 屬性設定為 <xref:System.ServiceModel.MessageCredentialType.Windows>。

5. 這項程序的程式碼如下所示：

    [!code-csharp[c_SecureWindowsService#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewindowsservice/cs/secureservice.cs#1)]
    [!code-vb[c_SecureWindowsService#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewindowsservice/vb/secureservice.vb#1)]

### <a name="using-the-binding-in-a-service"></a>在服務中使用繫結

這是第二個程序，說明如何在自我裝載的服務中使用繫結。 如需裝載服務的詳細資訊，請參閱[裝載服務](hosting-services.md)。

##### <a name="to-use-a-binding-in-a-service"></a>在服務中使用繫結

1. 將這個程序的程式碼插入到前一個程序的程式碼後面。

2. 建立名稱為 <xref:System.Type> 的 `contractType` 變數，並將其類型指派為介面 (`ICalculator`)。 使用 Visual Basic 時，請使用 `GetType` 運算子; 使用 c # 時，請使用 `typeof` 關鍵字。

3. 建立第二個名稱為 <xref:System.Type> 的 `serviceType` 變數，並將其類型指派為實作的合約 (`Calculator`)。

4. 使用服務的基底位址，建立名稱為 <xref:System.Uri> 之 `baseAddress` 類別的執行個體。 基底位址必須具有符合傳輸的配置。 在此情況下，傳輸配置為 HTTP，而位址包含特殊的統一資源識別元（URI） "localhost" 和埠號碼（8036），以及基底端點位址（"serviceModelSamples/）： `http://localhost:8036/serviceModelSamples/` 。

5. 使用 <xref:System.ServiceModel.ServiceHost> 和 `serviceType` 變數，建立 `baseAddress` 類別的執行個體。

6. 使用 `contractType`、繫結和端點名稱 (secureCalculator)，將端點新增至服務。 初始化服務的呼叫時，用戶端必須串連基底位址和端點名稱。

7. 呼叫 <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A> 方法啟動服務。 這項程序的程式碼如下所示：

    [!code-csharp[c_SecureWindowsService#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewindowsservice/cs/secureservice.cs#2)]
    [!code-vb[c_SecureWindowsService#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewindowsservice/vb/secureservice.vb#2)]

### <a name="using-the-binding-in-a-client"></a>在用戶端中使用繫結

這項程序會說明如何產生與服務進行通訊的 Proxy。 此 proxy 是使用使用服務中繼資料建立 proxy 的[System.servicemodel 中繼資料公用程式工具（Svcutil.exe）](servicemodel-metadata-utility-tool-svcutil-exe.md)所產生。

此程序還會建立可與服務進行通訊之 <xref:System.ServiceModel.WSHttpBinding> 類別的執行個體，然後呼叫該服務。

這個範例只會使用程式碼來建立用戶端。 或者，您可以使用組態檔，該檔案會在此程序之後的章節中說明。

#### <a name="to-use-a-binding-in-a-client-with-code"></a>搭配程式碼在用戶端中使用繫結

1. 使用 SvcUtil.exe 工具，從服務的中繼資料產生 Proxy 程式碼。 如需詳細資訊，請參閱[如何：建立用戶端](how-to-create-a-wcf-client.md)。 產生的 proxy 程式碼會繼承自 <xref:System.ServiceModel.ClientBase%601> 類別，這可確保每個用戶端都具有必要的方法和屬性，以便與 WCF 服務進行通訊。 在這個範例中，產生的程式碼包含 `CalculatorClient` 類別，這個類別會實作 `ICalculator` 介面，因此就會與服務程式碼相容。

2. 此程序的程式碼會插入至用戶端程式的 `Main` 方法開頭。

3. 建立 <xref:System.ServiceModel.WSHttpBinding> 類別的執行個體，將其安全性模式設定為 `Message`，並將其用戶端認證類型設定為 `Windows`。 這個範例會將變數命名為 `clientBinding`。

4. 建立名稱為 <xref:System.ServiceModel.EndpointAddress> 之 `serviceAddress` 類別的執行個體。 使用與端點名稱串連的基底位址初始化執行個體。

5. 使用 `serviceAddress` 和 `clientBinding` 變數，建立產生之用戶端類別的執行個體。

6. 呼叫 <xref:System.ServiceModel.ClientBase%601.Open%2A> 方法，如下列程式碼所示。

7. 呼叫服務並顯示結果。

    [!code-csharp[c_secureWindowsClient#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewindowsclient/cs/secureclient.cs#1)]
    [!code-vb[c_secureWindowsClient#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewindowsclient/vb/secureclient.vb#1)]

## <a name="using-the-configuration-file"></a>使用組態檔

如果不使用程序程式碼建立繫結，您可以改用下面針對組態檔之繫結區段所顯示的程式碼。

如果您尚未定義服務，請參閱[設計和執行服務](designing-and-implementing-services.md)和設定[服務](configuring-services.md)。

> [!NOTE]
> 此設定程式碼用於服務和用戶端設定檔中。

#### <a name="to-enable-transfer-security-on-a-service-in-a-windows-domain-using-configuration"></a>使用組態在 Windows 網域的服務上啟用傳輸安全性

1. 將 [\<wsHttpBinding>](../configure-apps/file-schema/wcf/wshttpbinding.md) 元素新增至 [\<bindings>](../configure-apps/file-schema/wcf/bindings.md) 設定檔的元素區段。

2. 將 <`binding`> 元素新增至 <`WSHttpBinding`> 專案，並將 `configurationName` 屬性設定為適用于您應用程式的值。

3. 新增 <`security`> 元素，並將 `mode` 屬性設定為 Message。

4. 新增 <`message`> 元素，並將 `clientCredentialType` 屬性設定為 Windows。

5. 在服務的組態檔中，將 `<bindings>` 區段取代為下列程式碼。 如果您還沒有服務設定檔，請參閱使用系結[來設定服務和用戶端](using-bindings-to-configure-services-and-clients.md)。

    ```xml
    <bindings>
      <wsHttpBinding>
       <binding name = "wsHttpBinding_Calculator">
         <security mode="Message">
           <message clientCredentialType="Windows"/>
         </security>
        </binding>
      </wsHttpBinding>
    </bindings>
    ```

### <a name="using-the-binding-in-a-client"></a>在用戶端中使用繫結

此程序會說明如何產生兩個檔案：與服務進行通訊的 Proxy 及組態檔。 此外還會說明用戶端程式的變更，也就是用戶端上使用的第三個檔案。

#### <a name="to-use-a-binding-in-a-client-with-configuration"></a>搭配組態在用戶端中使用繫結

1. 使用 SvcUtil.exe 工具，從服務的中繼資料產生 Proxy 程式碼和組態檔。 如需詳細資訊，請參閱[如何：建立用戶端](how-to-create-a-wcf-client.md)。

2. [\<bindings>](../configure-apps/file-schema/wcf/bindings.md)將產生之設定檔的區段取代為上一節中的設定程式碼。

3. 程序程式碼會插入至用戶端程式的 `Main` 方法開頭。

4. 建立已產生之用戶端類別的執行個體，將組態檔中繫結的名稱當做輸入參數傳遞。

5. 呼叫 <xref:System.ServiceModel.ClientBase%601.Open%2A> 方法，如下列程式碼所示。

6. 呼叫服務並顯示結果。

    [!code-csharp[c_secureWindowsClient#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewindowsclient/cs/secureclient.cs#2)]

## <a name="example"></a>範例

[!code-csharp[c_SecureWindowsService#0](../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewindowsservice/cs/secureservice.cs#0)]

[!code-csharp[c_SecureWindowsClient#0](../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewindowsclient/cs/secureclient.cs#0)]
[!code-vb[c_SecureWindowsClient#0](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewindowsclient/vb/secureclient.vb#0)]

## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.WSHttpBinding>
- [ServiceModel 中繼資料公用程式工具 (Svcutil.exe)](servicemodel-metadata-utility-tool-svcutil-exe.md)
- [如何：建立用戶端](how-to-create-a-wcf-client.md)
- [保護服務安全](securing-services.md)
- [安全性總覽](./feature-details/security-overview.md)
