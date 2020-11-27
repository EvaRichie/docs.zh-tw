---
title: 公司購買程序
ms.date: 03/30/2017
ms.assetid: a5e57336-4290-41ea-936d-435593d97055
ms.openlocfilehash: aa2ca2577eb68204ffcb755ce1b16b9354348ee3
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96293464"
---
# <a name="corporate-purchase-process"></a>公司購買程序

這個範例示範如何建立一個具有自動最佳提案選取、非常基本的提案徵求書 (RFP) 架構採購程序。 它結合 <xref:System.Activities.Statements.Parallel>、<xref:System.Activities.Statements.ParallelForEach%601> 和 <xref:System.Activities.Statements.ForEach%601>，以及自訂活動，建立代表此程序的工作流程。

 此範例包含 ASP.NET 用戶端應用程式，可讓您以與原始要求者或特定廠商) 不同的參與者 (來與進程互動。

## <a name="requirements"></a>規格需求

- Visual Studio 2012。

- [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)].

## <a name="demonstrates"></a>示範

- 自訂活動。

- 活動撰寫。

- 書籤。

- 持續性。

- 結構描述化的持續性。

- 追蹤。

- 追查。

- [!INCLUDE[wf1](../../../../includes/wf1-md.md)]在不同的用戶端中裝載 (ASP.NET Web 應用程式和 WinForms 應用程式) 。

> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> 如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。  
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Application\PurchaseProcess`  
  
## <a name="description-of-the-process"></a>程序說明  

 此範例示範如何執行 Windows Workflow Foundation (WF) 程式，以向一般公司的廠商收集提案。  
  
1. X 公司的員工建立提案徵求書 (RFP)。  
  
    1. 員工輸入 RFP 標題和描述。  
  
    2. 員工選取要邀請的廠商提交提案。  
  
2. 員工提交提案。  
  
    1. 建立工作流程執行個體。  
  
    2. 工作流程等候所有供應商提交提案。  
  
3. 收到所有提案之後，工作流程逐一查看所有收到的提案並選取最佳提案。  
  
    1. 每個供應商都有評價 (這個範例將評價清單儲存在 VendorRepository.cs)。  
  
    2. 提案的總值是由 (供應商輸入的值) * (供應商記錄評價) / 100 所決定。  
  
4. 原始要求者可以看到所有提交的提案。 在報表的特殊區段中呈現最佳提案。  
  
## <a name="process-definition"></a>流程定義  

 此範例的核心邏輯使用 <xref:System.Activities.Statements.ParallelForEach%601> 活動，等候每個供應商的供應項目 (使用可建立書籤的自訂活動)，而且將供應商提案註冊為 RFP (使用 <xref:System.Activities.Statements.InvokeMethod> 活動)。  
  
 範例接著逐一查看儲存在 `RfpRepository` 中所有收到的提案，計算調整值 (使用 <xref:System.Activities.Statements.Assign> 活動和 <xref:System.Activities.Expressions> 活動)，如果調整值優於上一個最佳供應項目，則會將新值指派為最佳供應項目 (使用 <xref:System.Activities.Statements.If> 和 <xref:System.Activities.Statements.Assign> 活動)。  
  
## <a name="projects-in-this-sample"></a>這個範例中的專案  

 這個範例包含下列專案。  
  
|專案|描述|  
|-------------|-----------------|  
|通用|程序中使用的實體物件 (Request for Proposal、Vendor 和 Vendor Proposal)。|  
|WfDefinition|用戶端應用程式用來建立及使用採購程序工作流程執行個體之程序 ([!INCLUDE[wf1](../../../../includes/wf1-md.md)] 程式) 和主機 (`PurchaseProcessHost`) 的定義。|  
|WebClient|ASP.NET 用戶端應用程式，可讓使用者建立及參與採購程式的實例。 它使用自訂建立的主機，以便與工作流程引擎互動。|  
|WinFormsClient|Windows Form 用戶端應用程式，讓使用者建立及參與採購程序的執行個體。 它使用自訂建立的主機，以便與工作流程引擎互動。|  
  
### <a name="wfdefinition"></a>WfDefinition  

 下表包含 WfDefinition 專案中最重要檔案的描述。  
  
|檔案|描述|  
|----------|-----------------|  
|IPurchaseProcessHost.cs|工作流程主機的介面。|  
|PurchaseProcessHost.cs|工作流程主機的實作。 此主機摘要工作流程執行階段的詳細資料，在所有用戶端應用程式中用來載入、執行 `PurchaseProcess` 工作流程執行個體，並與之互動。|  
|PurchaseProcessWorkflow.cs|包含採購程序工作流程定義的活動 (衍生自 <xref:System.Activities.Activity>)。<br /><br /> 衍生自 <xref:System.Activities.Activity> 的活動藉由組裝現有的自訂活動以及 [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] 活動程式庫中的活動來撰寫功能。 組裝這些活動是建立自訂功能最基本的方式。|  
|WaitForVendorProposal.cs|這個自訂活動衍生自 <xref:System.Activities.NativeActivity>，並且會建立具名書籤，供應商稍後在提交提案時必須繼續執行該書籤。<br /><br /> 衍生自 <xref:System.Activities.NativeActivity> 的活動，就像衍生自 <xref:System.Activities.CodeActivity> 的活動一樣，會覆寫 <xref:System.Activities.NativeActivity.Execute%2A> 來建立命令式功能，但也可透過傳遞至 <xref:System.Activities.ActivityContext> 方法的 `Execute` 來存取工作流程執行階段的所有功能。 此內容支援排程和取消子活動、設定不保存的區域 (執行區塊，而執行時間不會保存工作流程的資料（例如，在不可部分完成的) 交易中），以及 <xref:System.Activities.Bookmark> (可繼續暫停的工作流程) 的物件。|  
|TrackingParticipant.cs|接收所有追蹤事件並將其儲存至文字檔的 <xref:System.Activities.Tracking.TrackingParticipant>。<br /><br /> 追蹤參與者會加入至工作流程執行個體做為延伸。|  
|XmlWorkflowInstanceStore.cs|將工作流程應用程式儲存至 XML 檔案的自訂 <xref:System.Runtime.DurableInstancing.InstanceStore>。|  
|XmlPersistenceParticipant.cs|將提案徵求書執行個體儲存至 XML 檔案的自訂 <xref:System.Activities.Persistence.PersistenceParticipant>。|  
|AsyncResult.cs / CompletedAsyncResult.cs|在持續性元件中用來實作非同步模式的協助程式類別。|  
  
### <a name="common"></a>通用  

 下表包含通用專案中最重要類別的描述。  
  
|類別|描述|  
|-----------|-----------------|  
|廠商|在提案徵求書中提交提案的供應商。|  
|RequestForProposal|提案徵求書 (RFP) 是希望供應商對特定商品或服務提交提案的邀請。|  
|VendorProposal|供應商提交到具象 RFP 的提案。|  
|VendorRepository|供應商的儲存機制。 這個實作包含供應商執行個體的記憶體中集合以及公開這些執行個體的方法。|  
|RfpRepository|提案徵求書的儲存機制。 這個實作包含使用 Linq to XML 查詢結構描述化的持續性所產生的提案徵求書 XML 檔案。 |  
|IOHelper|這個類別處理所有 I/O 相關問題 (資料夾、路徑等等)。|  
  
### <a name="web-client"></a>網頁用戶端  

 下表包含 Web 用戶端專案中最重要網頁的描述。  
  
|檔案|描述|  
|-|-|  
|CreateRfp.aspx|建立及提交新的提案徵求書。|  
|Default.aspx|顯示所有作用中和已完成的提案徵求書。|  
|GetVendorProposal.aspx|在具象提案徵求書中取得供應商的提案。 此網頁僅由供應商使用。|  
|ShowRfp.aspx|顯示提案徵求書的所有相關資訊 (收到的提案、日期、值和其他資訊)。 此網頁僅由提案徵求書建立者使用。|  
  
### <a name="winforms-client"></a>WinForms 用戶端  

 下表包含 Win Form 專案中最重要表單的描述。  
  
|表單|描述|  
|-|-|  
|NewRfp|建立及提交新的提案徵求書。|  
|ShowProposals|顯示所有作用中和已完成的提案徵求書。 **注意：**  當您建立或修改提案的要求之後，您可能需要按一下 UI 中的 [重新整理] 按鈕，才能看到該畫面 **中的變更** 。|  
|SubmitProposal|在具象提案徵求書中取得供應商的提案。 此視窗僅由供應商使用。|  
|ViewRfp|顯示提案徵求書的所有相關資訊 (收到的提案、日期、值和其他資訊)。 此視窗僅由提案徵求書建立者使用。|  
  
### <a name="persistence-files"></a>持續性檔案  

 下表顯示持續性提供者 (`XmlPersistenceProvider`) 所產生的檔案，這些檔案位於目前系統的暫存資料夾路徑 (使用 <xref:System.IO.Path.GetTempPath%2A>)。 追蹤檔案是在目前執行路徑中建立的。  
  
|檔案名稱|描述|路徑|  
|-|-|-|  
|rfps.xml|具有所有作用中和已完成之提案徵求書的 XML 檔案。|<xref:System.IO.Path.GetTempPath%2A>|  
|[instanceid]|這個檔案包含工作流程執行個體的所有相關資訊。<br /><br /> 這個檔案是由結構描述化的持續性實作 (XmlPersistenceProvider 中的 PersistenceParticipant) 所產生的。|<xref:System.IO.Path.GetTempPath%2A>|  
|[instanceId].tracking|文字檔，其中有具象執行個體中發生的所有事件。<br /><br /> 這個檔案是由 TrackingParticipant 所產生。|<xref:System.IO.Path.GetTempPath%2A>|  
|PurchaseProcess.Tracing.TraceLog.txt|工作流程根據 App.config 或 Web.config 檔案中的組態參數所產生的追蹤檔案。|目前執行路徑|  
  
#### <a name="to-use-this-sample"></a>若要使用這個範例  
  
1. 使用 Visual Studio 2010，開啟 PurchaseProcess .sln 方案檔。  
  
2. 若要執行 Web 用戶端專案，請開啟 **方案總管** ，然後以滑鼠右鍵按一下 **web 用戶端** 專案。 選取 [ **設定為啟始專案**]。  
  
3. 若要執行 WinForms 用戶端專案，請開啟 **方案總管** ，然後以滑鼠右鍵按一下 **WinForms 用戶端** 專案。 選取 [ **設定為啟始專案**]。  
  
4. 若要建置此方案，請按 CTRL+SHIFT+B。  
  
5. 若要執行此方案，請按下 CTRL+F5。  
  
### <a name="web-client-options"></a>Web 用戶端選項  
  
- **建立新的 RFP**：為提案 (RFP) 建立新的要求，並開始購買程式工作流程。  
  
- 重新 **整理：重新** 整理主視窗中的作用中和已完成的 rfp 清單。  
  
- **View**：顯示現有 RFP 的內容。 供應商可以提交提案 (如果受邀或 RFP 未完成)。  
  
- View As：使用者可以使用不同的識別來存取 RFP，方法是在作用中 Rfp 方格的 [ **View As** ] 下拉式方塊中選取所需的參與者。  
  
### <a name="winforms-client-options"></a>WinForms 用戶端選項  
  
- **建立 RFP**：為提案 (RFP) 建立新的要求，並開始購買程式工作流程。  
  
- 重新 **整理：重新** 整理主視窗中的作用中和已完成的 rfp 清單。  
  
- **視圖 rfp**：顯示現有 RFP 的內容。 供應商可以提交提案 (如果受邀或 RFP 未完成)。  
  
- **連接** 身分：使用者可以使用不同的識別來存取 RFP，方法是在作用中 rfp 方格的 [ **View As** ] 下拉式方塊中選取所需的參與者。
