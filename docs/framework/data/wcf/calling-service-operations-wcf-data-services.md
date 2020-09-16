---
title: 呼叫服務作業 (WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 1767f3a7-29d2-4834-a763-7d169693fa8b
ms.openlocfilehash: 63c6e903fa811d5c61550d086b4f1ce84973f2bc
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90553619"
---
# <a name="calling-service-operations-wcf-data-services"></a>呼叫服務作業 (WCF Data Services)
開放式資料通訊協定 (OData) 會定義資料服務的服務作業。 WCF Data Services 可讓您將這類作業定義為數據服務上的方法。 就像其他資料服務資源，這些服務作業會使用 URI 來定址。 服務作業可以傳回實體類型集合、單一實體類型執行個體以及整數和字串等基本類型。 服務作業還可以傳回 `null` (在 Visual Basic 中為 `Nothing`)。 WCF Data Services 用戶端程式庫可以用來存取支援 HTTP GET 要求的服務作業。 這些服務作業類型是定義為已套用 <xref:System.ServiceModel.Web.WebGetAttribute> 的方法。 如需詳細資訊，請參閱 [服務作業](service-operations-wcf-data-services.md)。  
  
 服務作業會在執行 OData 的資料服務所傳回的中繼資料中公開。 在中繼資料中，服務作業會以 `FunctionImport` 元素來表示。 產生強型別時 <xref:System.Data.Services.Client.DataServiceContext> ，加入服務參考和 DataSvcUtil.exe 工具會忽略這個元素。 因此，您在內容上找不到可用來直接呼叫服務作業的方法。 不過，您仍然可以使用 WCF Data Services 用戶端，以下列兩種方式之一來呼叫服務作業：  
  
- 提供服務作業的 URI 並搭配任何參數，以呼叫 <xref:System.Data.Services.Client.DataServiceContext.Execute%2A> 上的 <xref:System.Data.Services.Client.DataServiceContext> 方法。 此方法用於呼叫任何 GET 服務作業。  
  
- 在 <xref:System.Data.Services.Client.DataServiceContext.CreateQuery%2A> 上使用 <xref:System.Data.Services.Client.DataServiceContext> 方法，以建立 <xref:System.Data.Services.Client.DataServiceQuery%601> 物件。 呼叫 <xref:System.Data.Services.Client.DataServiceContext.CreateQuery%2A> 時，要將服務作業的名稱提供給 `entitySetName` 參數。 列舉時或呼叫 <xref:System.Data.Services.Client.DataServiceQuery%601> 方法時，此方法會傳回呼叫服務作業的 <xref:System.Data.Services.Client.DataServiceQuery%601.Execute%2A> 物件。 此方法用於呼叫傳回集合的 GET 服務作業。 可以使用 <xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> 方法提供單一參數。 此方法傳回的 <xref:System.Data.Services.Client.DataServiceQuery%601> 物件就像任何查詢物件一樣，可以進一步加以撰寫。 如需詳細資訊，請參閱 [查詢資料服務](querying-the-data-service-wcf-data-services.md)。  
  
## <a name="considerations-for-calling-service-operations"></a>呼叫服務作業的考量  
 使用 WCF Data Services 用戶端來呼叫服務作業時，適用下列考慮事項。  
  
- 以非同步方式存取資料服務時，您必須在上使用對等的非同步 <xref:System.Data.Services.Client.DataServiceContext.BeginExecute%2A> / <xref:System.Data.Services.Client.DataServiceContext.EndExecute%2A> 方法， <xref:System.Data.Services.Client.DataServiceContext> 或是在上使用 <xref:System.Data.Services.Client.DataServiceQuery%601.BeginExecute%2A> / <xref:System.Data.Services.Client.DataServiceQuery%601.EndExecute%2A> 方法 <xref:System.Data.Services.Client.DataServiceQuery%601> 。  
  
- WCF Data Services 用戶端程式庫無法從傳回基本類型集合的服務作業具體化結果。  
  
- WCF Data Services 用戶端程式庫不支援呼叫 POST 服務作業。 HTTP POST 呼叫的服務作業是使用 <xref:System.ServiceModel.Web.WebInvokeAttribute> 搭配 `Method="POST"` 參數所定義。 若要使用 HTTP POST 要求呼叫服務作業，您必須改用 <xref:System.Net.HttpWebRequest>。  
  
- 您不能使用 <xref:System.Data.Services.Client.DataServiceContext.CreateQuery%2A> 來呼叫傳回實體或基本類型單一結果或需要多個輸入參數的 GET 服務作業。 您必須改為呼叫 <xref:System.Data.Services.Client.DataServiceContext.Execute%2A> 方法。  
  
- 請考慮在由工具產生的強型別部分類別上建立擴充方法， <xref:System.Data.Services.Client.DataServiceContext> <xref:System.Data.Services.Client.DataServiceContext.CreateQuery%2A> 以使用或 <xref:System.Data.Services.Client.DataServiceContext.Execute%2A> 方法來呼叫服務作業。 這可讓您直接從內容中呼叫服務作業。 如需詳細資訊，請參閱 blog post [服務作業和 WCF Data Services 用戶端](/archive/blogs/astoriateam/service-operations-and-the-wcf-data-services-client)。  
  
- 當您使用 <xref:System.Data.Services.Client.DataServiceContext.CreateQuery%2A> 來呼叫服務作業時，用戶端程式庫會透過 <xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> 執行保留字元的百分比編碼（例如，& ( # A0) ），並在字串中進行單引號的轉義，自動將提供給的字元加上引號。 但是，當您呼叫其中一個 *Execute* 方法來呼叫服務作業時，您必須記得對任何使用者提供的字串值執行這項的轉義。 URI 中的單引號是以一對單引號的形式來逸出。  
  
## <a name="examples-of-calling-service-operations"></a>呼叫服務作業的範例  
 本節包含下列範例，說明如何使用 WCF Data Services 用戶端程式庫呼叫服務作業：  
  
- [呼叫 Execute &lt; T &gt; 以傳回實體集合](calling-service-operations-wcf-data-services.md#ExecuteIQueryable)  
  
- [使用 CreateQuery &lt; T 傳回 &gt; 實體集合](calling-service-operations-wcf-data-services.md#CreateQueryIQueryable)  
  
- [呼叫 Execute &lt; T &gt; 以傳回單一實體](calling-service-operations-wcf-data-services.md#ExecuteSingleEntity)  
  
- [呼叫 Execute &lt; T &gt; 以傳回基本值的集合](calling-service-operations-wcf-data-services.md#ExecutePrimitiveCollection)  
  
- [呼叫 Execute &lt; T &gt; 以傳回單一基本值](calling-service-operations-wcf-data-services.md#ExecutePrimitiveValue)  
  
- [呼叫不傳回任何資料的服務作業](calling-service-operations-wcf-data-services.md#ExecuteVoid)  
  
- [非同步呼叫服務作業](calling-service-operations-wcf-data-services.md#ExecuteAsync)  
  
<a name="ExecuteIQueryable"></a>
### <a name="calling-executet-to-return-a-collection-of-entities"></a>呼叫 Execute \<T> 以傳回實體集合  
 下列範例會呼叫名為 GetOrdersByCity 的服務作業，這項作業接受字串參數 `city` 並傳回 <xref:System.Linq.IQueryable%601>：  
  
 [!code-csharp[Astoria Northwind Client#CallServiceOperationIQueryable](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#callserviceoperationiqueryable)]
 [!code-vb[Astoria Northwind Client#CallServiceOperationIQueryable](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#callserviceoperationiqueryable)]  
  
 在此範例中，服務作業會傳回 `Order` 物件集合與相關的 `Order_Detail` 物件。  
  
<a name="CreateQueryIQueryable"></a>
### <a name="using-createqueryt-to-return-a-collection-of-entities"></a>使用 CreateQuery 傳回 \<T> 實體集合  
 下列範例會使用 <xref:System.Data.Services.Client.DataServiceContext.CreateQuery%2A> 傳回用來呼叫相同 GetOrdersByCity 服務作業的 <xref:System.Data.Services.Client.DataServiceQuery%601>：  
  
 [!code-csharp[Astoria Northwind Client#CallServiceOperationCreateQuery](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#callserviceoperationcreatequery)]
 [!code-vb[Astoria Northwind Client#CallServiceOperationCreateQuery](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#callserviceoperationcreatequery)]  
  
 在此範例中，<xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> 方法用於將參數加入至查詢中，而 <xref:System.Data.Services.Client.DataServiceQuery%601.Expand%2A> 方法則用於將相關的 Order_Details 物件包含在結果中。  
  
<a name="ExecuteSingleEntity"></a>
### <a name="calling-executet-to-return-a-single-entity"></a>呼叫 Execute \<T> 以傳回單一實體  
 下列範例會呼叫名為 GetNewestOrder 的服務作業，這項作業只傳回單一 Order 實體：  
  
 [!code-csharp[Astoria Northwind Client#CallServiceOperationSingleEntity](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#callserviceoperationsingleentity)]
 [!code-vb[Astoria Northwind Client#CallServiceOperationSingleEntity](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#callserviceoperationsingleentity)]  
  
 此範例會使用 <xref:System.Linq.Enumerable.FirstOrDefault%2A> 方法，在執行時只要求單一 Order 實體。  
  
<a name="ExecutePrimitiveCollection"></a>
### <a name="calling-executet-to-return-a-collection-of-primitive-values"></a>呼叫 Execute \<T> 以傳回基本值的集合  
 下列範例會呼叫傳回字串值集合的服務作業：  
  
 [!code-csharp[Astoria Northwind Client#CallServiceOperationEnumString](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#callserviceoperationenumstring)]  
  
<a name="ExecutePrimitiveValue"></a>
### <a name="calling-executet-to-return-a-single-primitive-value"></a>呼叫 Execute \<T> 以傳回單一基本值  
 下列範例會呼叫傳回單一字串值的服務作業：  
  
 [!code-csharp[Astoria Northwind Client#CallServiceOperationSingleInt](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#callserviceoperationsingleint)]
 [!code-vb[Astoria Northwind Client#CallServiceOperationSingleInt](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#callserviceoperationsingleint)]  
  
 此範例又一次使用 <xref:System.Linq.Enumerable.FirstOrDefault%2A> 方法，在執行時只要求單一整數值。  
  
<a name="ExecuteVoid"></a>
### <a name="calling-a-service-operation-that-returns-no-data"></a>呼叫不傳回任何資料的服務作業  
 下列範例會呼叫不傳回任何資料的服務作業：  
  
 [!code-csharp[Astoria Northwind Client#CallServiceOperationVoid](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#callserviceoperationvoid)]
 [!code-vb[Astoria Northwind Client#CallServiceOperationVoid](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#callserviceoperationvoid)]  
  
 由於不傳回資料，因此沒有指派執行的值。 指出要求已成功的唯一表示就是沒有引發 <xref:System.Data.Services.Client.DataServiceQueryException>。  
  
<a name="ExecuteAsync"></a>
### <a name="calling-a-service-operation-asynchronously"></a>非同步呼叫服務作業  
 下列範例會藉由呼叫 <xref:System.Data.Services.Client.DataServiceContext.BeginExecute%2A> 和 <xref:System.Data.Services.Client.DataServiceContext.EndExecute%2A>，非同步呼叫服務作業：  
  
 [!code-csharp[Astoria Northwind Client#CallServiceOperationAsync](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#callserviceoperationasync)]
 [!code-vb[Astoria Northwind Client#CallServiceOperationAsync](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#callserviceoperationasync)]  
  
 [!code-csharp[Astoria Northwind Client#OnAsyncExecutionComplete](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#onasyncexecutioncomplete)]
 [!code-vb[Astoria Northwind Client#OnAsyncExecutionComplete](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#onasyncexecutioncomplete)]  
  
 由於不傳回資料，因此沒有指派執行傳回的值。 指出要求已成功的唯一表示就是沒有引發 <xref:System.Data.Services.Client.DataServiceQueryException>。  
  
 下列範例會使用 <xref:System.Data.Services.Client.DataServiceContext.CreateQuery%2A>，非同步呼叫相同的服務作業：  
  
 [!code-csharp[Astoria Northwind Client#CallServiceOperationQueryAsync](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#callserviceoperationqueryasync)]
 [!code-vb[Astoria Northwind Client#CallServiceOperationQueryAsync](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#callserviceoperationqueryasync)]  
  
 [!code-csharp[Astoria Northwind Client#OnAsyncQueryExecutionComplete](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#onasyncqueryexecutioncomplete)]
 [!code-vb[Astoria Northwind Client#OnAsyncQueryExecutionComplete](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#onasyncqueryexecutioncomplete)]  
  
## <a name="see-also"></a>另請參閱

- [WCF 資料服務用戶端程式庫](wcf-data-services-client-library.md)
