---
title: 將資料繫結至控制項 (WCF 資料服務)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- client applications, WCF Data Services
- WCF Data Services, client library
- data binding, WCF Data Services
ms.assetid: b32e1d49-c214-4cb1-867e-88fbb3d08c8d
ms.openlocfilehash: f2cb1004ef6316bc67189c4e00930f6086cf0dad
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91152919"
---
# <a name="binding-data-to-controls-wcf-data-services"></a>將資料繫結至控制項 (WCF 資料服務)

使用 WCF Data Services，您可以將控制項（例如和控制項）系結 `ComboBox` `ListView` 至類別的實例 <xref:System.Data.Services.Client.DataServiceCollection%601> 。 繼承自類別的這個集合 <xref:System.Collections.ObjectModel.ObservableCollection%601> 包含開放式資料通訊協定 (OData) 摘要中的資料。 此類別表示動態資料集合會在加入或移除項目時提供通知。 當您使用的實例進行資料系結時 <xref:System.Data.Services.Client.DataServiceCollection%601> ，WCF Data Services 的用戶端程式庫會處理這些事件，以確保所追蹤的物件會與系結 <xref:System.Data.Services.Client.DataServiceContext> UI 專案中的資料保持同步。  
  
 在集合中加入或移除物件時，<xref:System.Data.Services.Client.DataServiceCollection%601> 類別會 (間接) 實作 <xref:System.Collections.Specialized.INotifyCollectionChanged> 介面以警示內容。 與 <xref:System.Data.Services.Client.DataServiceCollection%601> 搭配使用的資料服務類型物件也必須實作 <xref:System.ComponentModel.INotifyPropertyChanged> 介面，以便在繫結集合中的物件屬性發生變更時警示 <xref:System.Data.Services.Client.DataServiceCollection%601>。  
  
> [!NOTE]
> 當您使用 [ **加入服務參考** ] 對話方塊或 [ [DataSvcUtil.exe](wcf-data-service-client-utility-datasvcutil-exe.md) ] 工具搭配 `/dataservicecollection` 選項來產生用戶端資料服務類別時，產生的資料類別會執行 <xref:System.ComponentModel.INotifyPropertyChanged> 介面。 如需詳細資訊，請參閱 [如何：手動產生用戶端資料服務類別](how-to-manually-generate-client-data-service-classes-wcf-data-services.md)。  
  
## <a name="creating-the-binding-collection"></a>建立繫結集合  

 以提供的 <xref:System.Data.Services.Client.DataServiceCollection%601> 執行個體及選擇性的 <xref:System.Data.Services.Client.DataServiceContext> 或 LINQ 查詢 (執行此查詢時會傳回 <xref:System.Data.Services.Client.DataServiceQuery%601> 執行個體) 呼叫其中一個類別建構函式方法，建立一個新的 <xref:System.Collections.Generic.IEnumerable%601> 類別執行個體。 這 <xref:System.Collections.Generic.IEnumerable%601> 會提供系結集合的物件來源，這些物件是從 OData 摘要具體化而來。 如需詳細資訊，請參閱 [物件具體化](object-materialization-wcf-data-services.md)。 根據預設，<xref:System.Data.Services.Client.DataServiceContext>會自動追蹤對插入於集合中的繫結物件和項目所進行的變更。 如果您需要手動追蹤這些變更，請呼叫其中一個採用參數的方法， `trackingMode` 並指定的值 <xref:System.Data.Services.Client.TrackingMode.None> 。  
  
 下列範例示範如何根據所提供的 <xref:System.Data.Services.Client.DataServiceCollection%601> 以及傳回所有客戶與相關訂單的 <xref:System.Data.Services.Client.DataServiceContext> 建立 <xref:System.Data.Services.Client.DataServiceQuery%601> 執行個體。  
  
 [!code-csharp[Astoria Northwind Client#CustomersOrders2Binding](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorders2.cs#customersorders2binding)]
 [!code-vb[Astoria Northwind Client#CustomersOrders2Binding](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorders2.vb#customersorders2binding)]  
  
## <a name="binding-data-to-windows-presentation-foundation-elements"></a>繫結資料至 Windows Presentation Foundation 項目  

 由於 <xref:System.Data.Services.Client.DataServiceCollection%601> 類別繼承自 <xref:System.Collections.ObjectModel.ObservableCollection%601> 類別，因此您可以在 Windows Presentation Foundation (WPF) 應用程式中將物件繫結至項目或控制項，就像使用 <xref:System.Collections.ObjectModel.ObservableCollection%601> 類別進行繫結一樣。 如需詳細資訊，請參閱 [ (Windows Presentation Foundation) 的資料 ](../../../desktop-wpf/data/data-binding-overview.md)系結。 繫結資料服務資料至 WPF 控制項的其中一個方法是將項目的 `DataContext` 屬性設定為包含查詢結果之 <xref:System.Data.Services.Client.DataServiceCollection%601> 類別的執行個體。 在這種情況下，您可以使用 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 屬性來設定控制項的物件來源。 使用 <xref:System.Windows.Controls.ItemsControl.DisplayMemberPath%2A> 屬性來指定要顯示繫結物件的哪一個屬性。 如果您要將項目繫結程序至導覽屬性所傳回的相關物件，請在為 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 屬性定義的繫結程序中加入路徑。 這個路徑是相對於父控制項 <xref:System.Windows.FrameworkElement.DataContext%2A> 屬性所設定根物件的位置。 下列範例會設定 <xref:System.Windows.FrameworkElement.DataContext%2A> 項目的 <xref:System.Windows.Controls.StackPanel> 屬性，將父控制項繫結至客戶物件的 <xref:System.Data.Services.Client.DataServiceCollection%601>：  
  
 [!code-csharp[Astoria Northwind Client#MasterDetailBinding](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorderscustom.xaml.cs#masterdetailbinding)]
 [!code-csharp[Astoria Northwind Client#MasterDetailBinding](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorderswpf.xaml.cs#masterdetailbinding)]
 [!code-vb[Astoria Northwind Client#MasterDetailBinding](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderscustom.xaml.vb#masterdetailbinding)]
 [!code-vb[Astoria Northwind Client#MasterDetailBinding](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderswpf.xaml.vb#masterdetailbinding)]
 [!code-vb[Astoria Northwind Client#MasterDetailBinding](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderscustom2.xaml.vb#masterdetailbinding)]  
  
 下列範例顯示子控制項 <xref:System.Windows.Controls.DataGrid> 和 <xref:System.Windows.Controls.ComboBox> 的 XAML 繫結定義：  
  
 [!code-xaml[Astoria Northwind Client#MasterDetailXaml](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderswpf.xaml#masterdetailxaml)]  
  
 如需詳細資訊，請參閱 [如何：將資料系結至 Windows Presentation Foundation 元素](bind-data-to-wpf-elements-wcf-data-services.md)。  
  
 實體加入一對多或多對多關聯性時，關聯性的導覽屬性會傳回相關物件集合。 當您使用 [ **加入服務參考** ] 對話方塊或 DataSvcUtil.exe 工具來產生用戶端資料服務類別時，導覽屬性會傳回的實例 <xref:System.Data.Services.Client.DataServiceCollection%601> 。 這樣可讓您將相關物件繫結至控制項，同時支援一般的 WPF 繫結案例，例如相關實體的主版詳細資料繫結模式。 在前述的 XAML 範例中，XAML 程式碼會將主版 <xref:System.Data.Services.Client.DataServiceCollection%601> 繫結至根資料項目。 接著會將訂單 <xref:System.Windows.Controls.DataGrid> 繫結至從所選 Customers 物件傳回的 Orders <xref:System.Data.Services.Client.DataServiceCollection%601>，然後再繫結至 <xref:System.Windows.Window> 的根項目。  
  
## <a name="binding-data-to-windows-forms-controls"></a>將資料繫結至 Windows Form 控制項  

 若要將物件繫結至 Windows Form 控制項，請將控制項的 `DataSource` 屬性設定為包含查詢結果之 <xref:System.Data.Services.Client.DataServiceCollection%601> 類別的執行個體。  
  
> [!NOTE]
> 只有接聽變更事件的控制項才支援資料繫結，透過的方式是實作 <xref:System.Collections.Specialized.INotifyCollectionChanged> 和 <xref:System.ComponentModel.INotifyPropertyChanged> 介面。 當控制項不支援這種變更通知時，對基礎 <xref:System.Data.Services.Client.DataServiceCollection%601> 所做的變更不會反映在繫結控制項中。  
  
 下列範例會將 <xref:System.Data.Services.Client.DataServiceCollection%601> 繫結到 <xref:System.Windows.Forms.ComboBox> 控制項：  
  
 [!code-csharp[Astoria Northwind Client#CustomersOrdersDataBindingSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorders.cs#customersordersdatabindingspecific)]
 [!code-vb[Astoria Northwind Client#CustomersOrdersDataBindingSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorders.vb#customersordersdatabindingspecific)]  
  
 當您使用 **加入服務參考** 對話方塊來產生用戶端資料服務類別時，也會根據產生的來建立專案資料來源 <xref:System.Data.Services.Client.DataServiceContext> 。 透過此資料來源，您只要從 [ **資料來源** ] 視窗將專案拖曳至設計工具，即可建立 UI 元素或控制項，以顯示資料服務中的資料。 這些項目會成為繫結至資料來源之應用程式 UI 中的項目。 如需詳細資訊，請參閱 how [to：使用專案資料來源](how-to-bind-data-using-a-project-data-source-wcf-data-services.md)系結資料。  
  
## <a name="binding-paged-data"></a>繫結分頁資料  

 您可以設定資料服務來限制單一回應訊息中傳回的查詢資料量。 如需詳細資訊，請參閱設定 [資料服務](configuring-the-data-service-wcf-data-services.md)。 當資料服務分頁回應資料時，每個回應都會包含一個連結以傳回下一頁結果。 如需詳細資訊，請參閱 [載入延遲的內容](loading-deferred-content-wcf-data-services.md)。 在這個情況下，您必須傳遞從 <xref:System.Data.Services.Client.DataServiceCollection%601.Load%2A> 屬性取得的 URI，在  <xref:System.Data.Services.Client.DataServiceCollection%601> 呼叫 <xref:System.Data.Services.Client.DataServiceQueryContinuation.NextLinkUri%2A> 方法，以明確地載入頁面，如下列範例所示：  
  
 [!code-csharp[Astoria Northwind Client#BindPagedDataSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorderswpf3.xaml.cs#bindpageddataspecific)]
 [!code-vb[Astoria Northwind Client#BindPagedDataSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderswpf3.xaml.vb#bindpageddataspecific)]  
  
 相關物件會以類似的方式載入。 如需詳細資訊，請參閱 [如何：將資料系結至 Windows Presentation Foundation 元素](bind-data-to-wpf-elements-wcf-data-services.md)。  
  
## <a name="customizing-data-binding-behaviors"></a>自訂資料繫結行為  

 <xref:System.Data.Services.Client.DataServiceCollection%601> 類別可讓您攔截變更集合時所引發的事件，例如加入或移除物件，以及變更集合中物件的屬性時所引發的事件。 您可以修改資料繫結事件以覆寫預設的行為，包括下列條件約束：  
  
- 委派內未執行驗證。  
  
- 加入實體時會自動加入相關的實體。  
  
- 刪除實體時不會刪除相關的實體。  
  
 當您建立新的 <xref:System.Data.Services.Client.DataServiceCollection%601> 執行個體時，您可以選擇指定下列參數，這些參數會定義處理變更繫結物件時引發之事件的方法委派。  
  
- `entityChanged`：繫結物件變更時會呼叫此方法。 此 <xref:System.Func%602> 委派接受 <xref:System.Data.Services.Client.EntityChangedParams> 物件並傳回布林值，指出是否仍應發生預設行為 (呼叫 <xref:System.Data.Services.Client.DataServiceContext.UpdateObject%2A> 的 <xref:System.Data.Services.Client.DataServiceContext>)。  
  
- `entityCollectionChanged`：在繫結集合中加入或移除物件時會呼叫此方法。 此 <xref:System.Func%602> 委派接受 <xref:System.Data.Services.Client.EntityCollectionChangedParams> 物件並傳回布林值，指出是否仍應發生預設行為 (呼叫 <xref:System.Data.Services.Client.DataServiceContext.AddObject%2A> 動作的 <xref:System.Collections.Specialized.NotifyCollectionChangedAction.Add>，或在 <xref:System.Data.Services.Client.DataServiceContext.DeleteObject%2A> 呼叫 <xref:System.Collections.Specialized.NotifyCollectionChangedAction.Remove> 動作的 <xref:System.Data.Services.Client.DataServiceContext>)。  
  
> [!NOTE]
> WCF Data Services 不會驗證您在這些委派中執行的自訂行為。  
  
 下列範例會自訂 <xref:System.Collections.Specialized.NotifyCollectionChangedAction.Remove> 動作以呼叫 <xref:System.Data.Services.Client.DataServiceContext.DeleteLink%2A> 和 <xref:System.Data.Services.Client.DataServiceContext.DeleteObject%2A> 方法來移除屬於已刪除之 `Orders_Details` 實體的 `Orders` 方法。 由於刪除父實體時不會自動刪除相依實體，因此會執行這個自訂行為。  
  
 [!code-csharp[Astoria Northwind Client#CustomersOrdersDeleteRelated](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorderscustom.xaml.cs#customersordersdeleterelated)]
 [!code-vb[Astoria Northwind Client#CustomersOrdersDeleteRelated](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderscustom.xaml.vb#customersordersdeleterelated)]
 [!code-vb[Astoria Northwind Client#CustomersOrdersDeleteRelated](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderscustom2.xaml.vb#customersordersdeleterelated)]  
  
 如需詳細資訊，請參閱 [如何：自訂資料](how-to-customize-data-binding-behaviors-wcf-data-services.md)系結行為。  
  
 使用 <xref:System.Data.Services.Client.DataServiceCollection%601> 方法移除 <xref:System.Collections.ObjectModel.Collection%601.Remove%2A> 中的物件時，預設行為是在 <xref:System.Data.Services.Client.DataServiceContext> 中將該物件也標記為已刪除。 若要變更此行為，您可以將委派指定為發生 `entityCollectionChanged` 事件時呼叫之 <xref:System.Collections.Specialized.INotifyCollectionChanged.CollectionChanged> 參數中的方法。  
  
## <a name="data-binding-with-custom-client-data-classes"></a>使用自訂用戶端資料類別資料繫結  

 若要將物件載入至 <xref:System.Data.Services.Client.DataServiceCollection%601>，物件本身必須實作 <xref:System.ComponentModel.INotifyPropertyChanged> 介面。 資料服務當您使用 [ **加入服務參考** ] 對話方塊或 [DataSvcUtil.exe](wcf-data-service-client-utility-datasvcutil-exe.md) 工具來執行此介面時所產生的用戶端類別。 如果您自行提供用戶端資料類別，則必須使用另一種集合類型進行資料繫結。 物件變更時，您必須在資料繫結控制項中處理事件，以呼叫 <xref:System.Data.Services.Client.DataServiceContext> 類別的下列方法：  
  
- <xref:System.Data.Services.Client.DataServiceContext.AddObject%2A>：將新的物件加入至集合中時。  
  
- <xref:System.Data.Services.Client.DataServiceContext.DeleteObject%2A>：自集合移除物件時。  
  
- <xref:System.Data.Services.Client.DataServiceContext.UpdateObject%2A>：集合中的物件屬性變更時。  
  
- <xref:System.Data.Services.Client.DataServiceContext.AddLink%2A>：將物件加入至相關物件集合中時。  
  
- <xref:System.Data.Services.Client.DataServiceContext.SetLink%2A>：將物件加入至相關物件集合中時。  
  
 如需詳細資訊，請參閱 [更新資料服務](updating-the-data-service-wcf-data-services.md)。  
  
## <a name="see-also"></a>另請參閱

- [作法：手動產生用戶端資料服務類別](how-to-manually-generate-client-data-service-classes-wcf-data-services.md)
- [作法：新增資料服務參考](how-to-add-a-data-service-reference-wcf-data-services.md)
