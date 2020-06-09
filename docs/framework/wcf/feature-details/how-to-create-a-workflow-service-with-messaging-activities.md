---
title: HOW TO：說明如何使用訊息活動建立工作流程服務。
ms.date: 03/30/2017
ms.assetid: 53d094e2-6901-4aa1-88b8-024b27ccf78b
ms.openlocfilehash: b4991fc9f8a6c45cae3943f1506247c42ed2b30b
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84597120"
---
# <a name="how-to-create-a-workflow-service-with-messaging-activities"></a>HOW TO：說明如何使用訊息活動建立工作流程服務。
本主題描述如何使用訊息活動建立簡單的工作流程服務。 本主題的重點在於建立工作流程服務的機制，而該服務主要包含的便是訊息活動。 在真實世界的服務中，工作流程包含許多其他活動。 服務會實作一項稱為 Echo 的作業，該作業會使用字串並將字串傳回呼叫端。 本主題即為兩個主題的第一個。 下一個主題[如何：從工作流應用程式存取服務](how-to-access-a-service-from-a-workflow-application.md)討論如何建立可以呼叫本主題中所建立之服務的工作流程應用程式。  
  
### <a name="to-create-a-workflow-service-project"></a>若要建立工作流程服務專案  
  
1. 啟動 Visual Studio 2012。  
  
2. 依序**按一下 [檔案**] 功能表、[**新增**] 和 [**專案**]，以顯示 [**新增專案] 對話方塊**。 從專案類型清單中選取 [已安裝的範本] 和 [ **WCF 工作流程服務應用程式**] 清單中的 [**工作流程**]。 將專案命名 `MyWFService` 為，並使用預設位置，如下圖所示。  
  
     按一下 [**確定]** 按鈕以關閉 [**新增專案] 對話方塊**。  
  
3. 建立專案後，會在設計工具中開啟 Service1.xamlx 檔案，如下圖所示。  
  
     ![螢幕擷取畫面：在設計工具中顯示開啟的 Service1 service1.xamlx 檔案。](./media/how-to-create-a-workflow-service-with-messaging-activities/default-workflow-service.jpg)  
  
     以滑鼠右鍵按一下標示為 [**連續服務**] 的活動，然後選取 [**刪除**]。  
  
### <a name="to-implement-the-workflow-service"></a>若要實作工作流程服務  
  
1. 選取畫面左側的 [**工具箱**] 索引標籤，以顯示 [工具箱]，然後按一下圖釘讓視窗保持開啟。 展開 [工具箱] 的 [**訊息**] 區段，顯示訊息活動和訊息活動範本，如下圖所示。  
  
     ![顯示已展開 [訊息] 區段的 [工具箱] 的螢幕擷取畫面。](./media/how-to-create-a-workflow-service-with-messaging-activities/toolbox-messaging-section.jpg)  
  
2. 將**receiveandsendreply]** 範本拖放到工作流程設計工具。 這會建立一個 <xref:System.Activities.Statements.Sequence> 活動， **Receive**其後面接著一個活動，如下 <xref:System.ServiceModel.Activities.SendReply> 圖所示。  
  
     ![顯示 Receiveandsendreply] 範本的螢幕擷取畫面。](./media/how-to-create-a-workflow-service-with-messaging-activities/receiveandsendreply-template.jpg)  
  
     注意，<xref:System.ServiceModel.Activities.SendReply> 活動的 <xref:System.ServiceModel.Activities.SendReply.Request%2A> 屬性會設為 `Receive`，也就是 <xref:System.ServiceModel.Activities.Receive> 活動所回覆之 <xref:System.ServiceModel.Activities.SendReply> 活動的名稱。  
  
3. 在活動類型中，加上 <xref:System.ServiceModel.Activities.Receive> `Echo` 標示為**OperationName**的文字方塊。 這樣做會定義服務所實作之作業的名稱。  
  
     ![顯示要在何處指定作業名稱的螢幕擷取畫面。](./media/how-to-create-a-workflow-service-with-messaging-activities/define-operation-name.jpg)  
  
4. <xref:System.ServiceModel.Activities.Receive>選取活動後，按一下 [**流覽**] 功能表並選取 [**屬性視窗]**，開啟 [屬性] 視窗（如果尚未開啟）。 在 [**屬性] 視窗**中，向下**CanCreateInstance** ，直到您看到 []，然後按一下核取方塊，如下圖所示。 這項設定可讓工作流程服務主機在接收訊息時建立新的服務執行個體 (如果需要的話)。  
  
     ![顯示 CanCreateInstance 屬性的螢幕擷取畫面。](./media/how-to-create-a-workflow-service-with-messaging-activities/cancreateinstance-property.jpg)  
  
5. 選取 <xref:System.Activities.Statements.Sequence> 活動，然後按一下設計工具左下角的 [**變數**] 按鈕。 如此將會顯示變數編輯器。 按一下 [**建立變數**] 連結以新增變數，以儲存傳送至作業的字串。 將變數命名為 `msg` ，並將其**變數**類型設定為 [字串]，如下圖所示。  
  
     ![顯示如何新增變數的螢幕擷取畫面。](./media/how-to-create-a-workflow-service-with-messaging-activities/add-variable-msg-string.jpg)  
  
     再次按一下 [**變數**] 按鈕，以關閉 [變數編輯器]。  
  
6. 按一下 [**定義]。** 在活動的 [**內容**] 文字方塊中連結 <xref:System.ServiceModel.Activities.Receive> ，以顯示 [**內容定義**] 對話方塊。 選取 [**參數**] 選項按鈕，按一下 [**加入新的參數**] 連結， `inMsg` 在 [**名稱**] 文字方塊中輸入，在 [**類型**] 下拉式清單方塊中選取 [**字串**]，然後在 [指派給] 文字方塊中輸入，如下 `msg` 圖所示。 **Assign To**  
  
     ![顯示新增參數內容的螢幕擷取畫面。](./media/how-to-create-a-workflow-service-with-messaging-activities/adding-parameters-content.jpg)  
  
     這樣會指定 [接收] 活動接收字串參數，且該資料繫結至 `msg` 變數。 按一下 **[確定**] 以關閉 [**內容定義**] 對話方塊。  
  
7. 在活動的 [**內容**] 方塊中按一下 [**定義**] 連結 <xref:System.ServiceModel.Activities.SendReply> ，以顯示 [**內容定義**] 對話方塊。 選取 [**參數**] 選項按鈕，按一下 [**加入新的參數**] 連結， `outMsg` 在 [**名稱**] 文字方塊中輸入，在 [**類型**] 下拉式清單方塊中選取 [**字串**]，然後 `msg` 在 [**值**] 文字方塊中顯示，如下圖所示。  
  
     ![顯示如何新增 outMsg 參數的螢幕擷取畫面。](./media/how-to-create-a-workflow-service-with-messaging-activities/outmsg-parameters-content.jpg)  
  
     這樣會指定 <xref:System.ServiceModel.Activities.SendReply> 活動傳送訊息或訊息合約型別，且該資料繫結至 `msg` 變數。 由於此為 <xref:System.ServiceModel.Activities.SendReply> 活動，代表 `msg` 中的資料是用來填入由活動傳回用戶端的訊息。 按一下 **[確定**] 以關閉 [**內容定義**] 對話方塊。  
  
8. 按一下 [**建立**] 功能表，然後選取 [**建立方案**]，以儲存並建立解決方案。  
  
## <a name="configure-the-workflow-service-project"></a>設定工作流程服務專案。  
 工作流程執行服務已完成。 本節說明如何設定工作流程服務方案，讓裝載和執行更順利。 此方案是使用 ASP.NET 程式開發伺服器來裝載服務。  
  
#### <a name="to-set-project-start-up-options"></a>若要設定專案啟動選項  
  
1. 在 [**方案總管**中，以滑鼠右鍵按一下 [ **MyWFService** ]，然後選取 [**屬性**] 以顯示 [**專案屬性**] 對話方塊。  
  
2. 選取 [ **Web** ] 索引標籤，並選取 [**起始動作**] 底下的 [**特定頁面**]，然後 `Service1.xamlx` 在文字方塊中輸入，如下圖所示。  
  
     ![顯示 [專案屬性] 對話方塊的螢幕擷取畫面。](./media/how-to-create-a-workflow-service-with-messaging-activities/project-properties-dialog.jpg)  
  
     這樣做會裝載在 ASP.NET 程式開發伺服器的 Service1.xamlx 中所定義的服務。  
  
3. 按 Ctrl+F5 啟動服務。 [ASP.NET 程式開發伺服器] 圖示會顯示在桌面的右下角，如下圖所示。  
  
     ![顯示 ASP.NET 開發人員伺服器圖示的螢幕擷取畫面。](./media/how-to-create-a-workflow-service-with-messaging-activities/asp-net-dev-server-icon.jpg)  
  
     此外，Internet Explorer 還會顯示該服務的 WCF 服務說明網頁。  
  
     ![顯示 [WCF 服務說明] 頁面的螢幕擷取畫面。](./media/how-to-create-a-workflow-service-with-messaging-activities/wcf-service-help-page.jpg)  
  
4. 繼續前往[如何：從工作流應用程式存取服務](how-to-access-a-service-from-a-workflow-application.md)主題，以建立呼叫此服務的工作流程用戶端。  
  
## <a name="see-also"></a>請參閱

- [工作流程服務](workflow-services.md)
- [裝載工作流程服務概觀](hosting-workflow-services-overview.md)
- [傳訊活動](messaging-activities.md)
