---
title: 作法：在組態中指定用戶端繫結
description: 瞭解如何在設定檔中以宣告方式指定 WCF 用戶端的系結。 用戶端會存取此範例中的服務。
ms.date: 03/30/2017
ms.assetid: 4a7c79aa-50ee-4991-891e-adc0599323a7
ms.openlocfilehash: e8a552211b28c1323b2afd595c5b060db6b2824a
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96236503"
---
# <a name="how-to-specify-a-client-binding-in-configuration"></a>作法：在組態中指定用戶端繫結

在此範例中，建立了一個使用計算機服務的用戶端主控台應用程式，並在組態中以宣告方式指定用戶端的繫結。 用戶端會存取 `CalculatorService` (該服務會實作 `ICalculator` 介面)，而服務和用戶端都會使用 <xref:System.ServiceModel.BasicHttpBinding> 類別。  
  
 所述的程序假設計算機服務正在執行中。 如需有關如何建立服務的詳細資訊，請參閱 [如何：在設定中指定服務](how-to-specify-a-service-binding-in-configuration.md)系結。 此外，它也會使用 Windows Communication Foundation (WCF) 提供來自動產生用戶端元件 [ ( # A0) 的 System.servicemodel 中繼資料公用程式工具 ](servicemodel-metadata-utility-tool-svcutil-exe.md) 。 此工具會產生用戶端程式碼，以及存取服務的組態。  
  
 用戶端會建置成兩個部分。 Svcutil.exe 會產生 `ClientCalculator`，而該元件會實作 `ICalculator` 介面。 接著會藉由建構 `ClientCalculator` 的執行個體，以建構此用戶端應用程式。  
  
 通常最佳作法是在組態中以宣告方式指定繫結和位址資訊，而不是在程式碼中強制指定。 在程式碼中定義端點通常不太實用，因為部署之服務的繫結和位址通常與開發服務時所使用的繫結和位址不同。 比較一般性的作法是將繫結和位址資訊留在程式碼外面，如此一來，不需要重新編譯或重新部署應用程式，就可以變更繫結和位址資訊。  
  
 您可以使用設定 [編輯器工具 ( # A0) ](configuration-editor-tool-svcconfigeditor-exe.md)來執行下列所有設定步驟。  
  
 如需此範例的來源複本，請參閱 [BasicBinding](./samples/basicbinding.md) 範例。  
  
### <a name="specifying-a-client-binding-in-configuration"></a>指定組態中的用戶端繫結  
  
1. 從命令列使用 Svcutil.exe 產生取自服務中繼資料的程式碼。  
  
    ```console  
    Svcutil.exe <service's Metadata Exchange (MEX) address or HTTP GET address>
    ```  
  
2. 所產生的用戶端會包含 `ICalculator` 介面，其中定義了用戶端實作所必須滿足的服務合約。  
  
     [!code-csharp[C_HowTo_ConfigureClientBinding#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureclientbinding/cs/generatedclient.cs#1)]
     [!code-csharp[C_HowTo_ConfigureClientBinding#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureclientbinding/cs/source.cs#1)]  
  
3. 產生的用戶端也會包含 `ClientCalculator` 的實作。  
  
     [!code-csharp[C_HowTo_ConfigureClientBinding#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureclientbinding/cs/generatedclient.cs#2)]
     [!code-csharp[C_HowTo_ConfigureClientBinding#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureclientbinding/cs/source.cs#2)]  
  
4. Svcutil.exe 也會為使用 <xref:System.ServiceModel.BasicHttpBinding> 類別的用戶端產生組態。 使用 Visual Studio 時，請將此檔案命名為 App.config。請注意，在服務的任何位置中，都不會指定位址和系結資訊。 同時，您不需要撰寫可從組態檔擷取該資訊的程式碼。  
  
     [!code-xml[C_HowTo_ConfigureClientBinding#100](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureclientbinding/common/client.exe.config#100)]

5. 在應用程式內建立 `ClientCalculator` 的執行個體，然後呼叫服務作業。  
  
     [!code-csharp[C_HowTo_ConfigureClientBinding#3](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureclientbinding/cs/client.cs#3)]  
  
6. 請編譯並執行用戶端。  
  
## <a name="see-also"></a>另請參閱

- [使用繫結來設定服務和用戶端](using-bindings-to-configure-services-and-clients.md)
