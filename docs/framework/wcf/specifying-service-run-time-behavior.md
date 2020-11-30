---
title: 指定服務執行階段行為
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 5c5450ea-6af1-4b75-a267-613d0ac54707
ms.openlocfilehash: 61c3b8ebd431c3a16475342984b463d5f8842a89
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/29/2020
ms.locfileid: "96235879"
---
# <a name="specifying-service-run-time-behavior"></a>指定服務執行階段行為

一旦您設計好服務合約 ([Designing Service Contracts](designing-service-contracts.md)) 並實作服務合約 ([Implementing Service Contracts](implementing-service-contracts.md))，就可以設定服務執行階段的作業行為。 本主題討論系統提供的服務與作業行為，並說明哪裡可以找到更多資訊以建立新行為。 儘管有些行為會以屬性形式來套用，許多行為還是需要透過應用程式組態檔或以程式設計方式來套用。 如需設定服務應用程式的詳細資訊，請參閱設定 [服務](configuring-services.md)。  
  
## <a name="overview"></a>概觀  

 合約會定義輸入、輸出、資料型別，以及該類型服務的功能。 實作服務合約會建立一個類別，此類別在使用位址上的繫結進行設定時會實行類別所實作的合約。 合約、繫結和位址資訊皆為用戶端所熟知，若缺乏這些資訊，用戶端就無法使用服務。  
  
 但是，用戶端並不清楚執行緒問題或執行個體管理之類的作業細節。 一旦您實作了服務合約，就可以透過「 *行為*」(Behavior) 來設定大量的作業特性。 行為是一種物件，這些物件會藉由設定執行時間屬性或將自訂類型插入至執行時間，來修改 Windows Communication Foundation (WCF) 執行時間。 如需建立使用者定義行為來修改執行時間的詳細資訊，請參閱 [擴充 ServiceHost 和服務模型層](./extending/extending-servicehost-and-the-service-model-layer.md)。  
  
 <xref:System.ServiceModel.ServiceBehaviorAttribute?displayProperty=nameWithType> 和 <xref:System.ServiceModel.OperationBehaviorAttribute?displayProperty=nameWithType> 屬性都是常用的行為，且會公開最常要求的作業功能。 由於它們是屬性，您可以將它們套用至服務或作業實作中。 儘管您能以程式設計方式來使用諸如 <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=nameWithType> 或 <xref:System.ServiceModel.Description.ServiceDebugBehavior?displayProperty=nameWithType>的其他行為，一般來說您還是需要透過應用程式組態檔來加以套用。  
  
 本主題概要說明 <xref:System.ServiceModel.ServiceBehaviorAttribute> 和 <xref:System.ServiceModel.OperationBehaviorAttribute> 屬性、描述行為可以操作的各種範圍，並提供 WCF 開發人員可能感興趣之各種範圍的許多系統提供行為的快速描述。  
  
## <a name="servicebehaviorattribute-and-operationbehaviorattribute"></a>ServiceBehaviorAttribute 和 OperationBehaviorAttribute  

 最重要的行為是 <xref:System.ServiceModel.ServiceBehaviorAttribute> 和 <xref:System.ServiceModel.OperationBehaviorAttribute> 屬性，可供您用來控制：  
  
- 執行個體存留期  
  
- 並行與同步化支援  
  
- 組態行為  
  
- 交易行為  
  
- 序列化行為  
  
- 中繼資料轉換  
  
- 工作階段存留期  
  
- 位址篩選與標頭處理  
  
- 模擬  
  
- 若要使用這些屬性，請以適用該範圍的屬性 (Attribute) 來標記服務或作業實作，然後設定屬性 (Property)。 例如，下列程式碼範例說明的作業實作會透過 <xref:System.ServiceModel.OperationBehaviorAttribute.Impersonation%2A?displayProperty=nameWithType> 屬性要求此作業的呼叫端支援模擬。  
  
 [!code-csharp[OperationBehaviorAttribute_Impersonation#1](../../../samples/snippets/csharp/VS_Snippets_CFX/operationbehaviorattribute_impersonation/cs/services.cs#1)]
 [!code-vb[OperationBehaviorAttribute_Impersonation#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/operationbehaviorattribute_impersonation/vb/services.vb#1)]  
  
 許多屬性都要求來自繫結的額外支援。 例如，要求來自用戶端之交易的作業必須設為使用可支援流動交易的繫結。  
  
### <a name="well-known-singleton-services"></a>已知的單一服務  

 您可以使用 <xref:System.ServiceModel.ServiceBehaviorAttribute> 和 <xref:System.ServiceModel.OperationBehaviorAttribute> 屬性控制特定存留期，存留期可以分別屬於實作作業的 <xref:System.ServiceModel.InstanceContext> 和服務物件。  
  
 例如， <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=nameWithType> 屬性會控制多久釋放一次 <xref:System.ServiceModel.InstanceContext> ，而 <xref:System.ServiceModel.OperationBehaviorAttribute.ReleaseInstanceMode%2A?displayProperty=nameWithType> 和 <xref:System.ServiceModel.ServiceBehaviorAttribute.ReleaseServiceInstanceOnTransactionComplete%2A?displayProperty=nameWithType> 屬性則控制釋放服務物件的時機。  
  
 但是，您也可以自行建立服務物件，並透過該物件來建立服務主機。 若要這麼做，您必須同時將 <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=nameWithType> 屬性設定為 <xref:System.ServiceModel.InstanceContextMode.Single> ，否則在開啟服務主機時會擲回例外狀況。  
  
 請使用 <xref:System.ServiceModel.ServiceHost.%23ctor%28System.Object%2CSystem.Uri%5B%5D%29> 建構函式建立此類服務。 當您想要將特定物件執行個體提供給單一服務使用時，它提供了另一種實作自訂 <xref:System.ServiceModel.Dispatcher.IInstanceContextInitializer?displayProperty=nameWithType> 的方式。 當您的服務實類型很難建立時，您可以使用這個多載 (例如，如果它不會執行無參數的公用函式) 。
  
 請注意，當物件提供給此函式時，與 Windows Communication Foundation (WCF) 實例行為相關的某些功能會以不同的方式運作。 例如，提供已知物件執行個體時，呼叫 <xref:System.ServiceModel.InstanceContext.ReleaseServiceInstance%2A?displayProperty=nameWithType> 將沒有任何作用。 同樣的，也會忽略任何其他執行個體的釋放機制。 <xref:System.ServiceModel.ServiceHost> 類別的行為就像是所有作業的 <xref:System.ServiceModel.OperationBehaviorAttribute.ReleaseInstanceMode%2A?displayProperty=nameWithType> 屬性都已設為 <xref:System.ServiceModel.ReleaseInstanceMode.None?displayProperty=nameWithType> 。  
  
## <a name="other-service-endpoint-contract-and-operation-behaviors"></a>其他服務、端點、合約與作業行為  

 服務行為，例如 <xref:System.ServiceModel.ServiceBehaviorAttribute> 屬性，會在整個服務上作業。 例如，如果您將 <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A?displayProperty=nameWithType> 屬性設為 <xref:System.ServiceModel.ConcurrencyMode.Multiple?displayProperty=nameWithType> ，就必須自行處理該服務中每項作業的執行緒同步化問題。 端點行為會在整個端點上作業；許多系統提供的端點行為都是因應用戶端功能而生。 合約行為會在合約層級作業，而作業行為則會修改作業遞送。  
  
 這些行為當中，有許多都是在屬性上實作的，而您能以使用 <xref:System.ServiceModel.ServiceBehaviorAttribute> 和 <xref:System.ServiceModel.OperationBehaviorAttribute> 屬性的方式來使用它們，方法是將它們套用至適當的服務類別或作業實作上。 儘管您能以程式設計方式來使用諸如 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 或 <xref:System.ServiceModel.Description.ServiceDebugBehavior> 物件的其他行為，一般來說您還是需要透過應用程式組態檔來加以套用。  
  
 例如，您可以透過 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 物件來設定中繼資料的發行。 下列應用程式組態檔說明最常見的用法。  
  
 [!code-xml[ServiceMetadataBehavior#1](../../../samples/snippets/csharp/VS_Snippets_CFX/servicemetadatabehavior/cs/hostapplication.exe.config#1)]  
  
 下列章節說明最好用的系統提供行為，供您用來修改服務或用戶端的執行階段遞送。 請參閱參考主題來判斷如何使用每一個項目。  
  
### <a name="service-behaviors"></a>服務行為  

 下列行為可在服務上作業。  
  
- <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsAttribute>. 套用至 WCF 服務，以指出是否可以在 ASP.NET 相容性模式中執行該服務。  
  
- <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>. 控制服務如何授權用戶端宣告。  
  
- <xref:System.ServiceModel.Description.ServiceCredentials>. 設定服務認證。 使用此類別來指定服務認證，例如 X.509 憑證。  
  
- <xref:System.ServiceModel.Description.ServiceDebugBehavior>. 啟用 WCF 服務的偵錯工具和說明資訊功能。  
  
- <xref:System.ServiceModel.Description.ServiceMetadataBehavior>. 控制服務中繼資料與相關資訊的發行。  
  
- <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior>. 指定安全性事件的稽核行為。  
  
- <xref:System.ServiceModel.Description.ServiceThrottlingBehavior>. 設定可讓您調整服務效能的執行階段輸送量設定。  
  
### <a name="endpoint-behaviors"></a>端點行為  

 下列行為可在端點上作業。 這類行為大多可用於用戶端應用程式中。  
  
- <xref:System.ServiceModel.CallbackBehaviorAttribute>. 設定雙工用戶端應用程式中的回呼服務實作。  
  
- <xref:System.ServiceModel.Description.CallbackDebugBehavior>. 啟用 WCF 回呼物件的服務偵錯工具。  
  
- <xref:System.ServiceModel.Description.ClientCredentials>. 允許使用者設定用戶端與服務認證，以及服務認證驗證設定，以用在用戶端上。  
  
- <xref:System.ServiceModel.Description.ClientViaBehavior>. 用戶端用來針對應該建立的傳輸通道指定統一資源識別項 (URI)。  
  
- <xref:System.ServiceModel.Description.MustUnderstandBehavior>. 指示 WCF 停用 `MustUnderstand` 處理。  
  
- <xref:System.ServiceModel.Description.SynchronousReceiveBehavior>. 指示執行階段針對通道使用同步接收處理序。  
  
- <xref:System.ServiceModel.Description.TransactedBatchingBehavior>. 針對支援交易接收的傳輸最佳化其接收作業。  
  
### <a name="contract-behaviors"></a>合約行為  

 <xref:System.ServiceModel.DeliveryRequirementsAttribute>. 指定繫結必須提供給服務或用戶端實作的功能需求。  
  
### <a name="operation-behaviors"></a>作業行為  

 下列作業行為指定作業的序列化與交易控制。  
  
- <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior>. 表示 <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType>的執行階段行為。  
  
- <xref:System.ServiceModel.Description.XmlSerializerOperationBehavior>. 控制 `XmlSerializer` 的執行階段行為並將其與作業相關聯。  
  
- <xref:System.ServiceModel.TransactionFlowAttribute>. 指定服務作業接受異動標頭時所在的層級。  
  
## <a name="see-also"></a>另請參閱

- [設定服務](configuring-services.md)
- [作法：控制服務執行個體](./feature-details/how-to-control-service-instancing.md)
