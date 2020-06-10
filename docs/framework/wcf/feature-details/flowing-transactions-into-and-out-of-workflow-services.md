---
title: 進出工作流程服務的異動流動
ms.date: 03/30/2017
ms.assetid: 03ced70e-b540-4dd9-86c8-87f7bd61f609
ms.openlocfilehash: 17c05139b5977c47e20e888e436a311ba145018a
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84597458"
---
# <a name="flowing-transactions-into-and-out-of-workflow-services"></a><span data-ttu-id="a7386-102">進出工作流程服務的異動流動</span><span class="sxs-lookup"><span data-stu-id="a7386-102">Flowing Transactions into and out of Workflow Services</span></span>
<span data-ttu-id="a7386-103">工作流程服務與用戶端都可以參與交易。</span><span class="sxs-lookup"><span data-stu-id="a7386-103">Workflow services and clients can participate in transactions.</span></span>  <span data-ttu-id="a7386-104">若要讓服務作業變成環境交易的一部分，請將 <xref:System.ServiceModel.Activities.Receive> 活動放在 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 活動內。</span><span class="sxs-lookup"><span data-stu-id="a7386-104">For a service operation to become part of an ambient transaction, place a <xref:System.ServiceModel.Activities.Receive> activity within a <xref:System.ServiceModel.Activities.TransactedReceiveScope> activity.</span></span> <span data-ttu-id="a7386-105"><xref:System.ServiceModel.Activities.Send> 或 <xref:System.ServiceModel.Activities.SendReply> 活動在 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 內所進行的任何呼叫也會在環境交易中進行。</span><span class="sxs-lookup"><span data-stu-id="a7386-105">Any calls made by a <xref:System.ServiceModel.Activities.Send> or a <xref:System.ServiceModel.Activities.SendReply> activity within the <xref:System.ServiceModel.Activities.TransactedReceiveScope> will also be made within the ambient transaction.</span></span> <span data-ttu-id="a7386-106">工作流程用戶端應用程式可以使用 <xref:System.Activities.Statements.TransactionScope> 活動建立環境異動，然後使用環境異動呼叫服務作業。</span><span class="sxs-lookup"><span data-stu-id="a7386-106">A workflow client application can create an ambient transaction by using the <xref:System.Activities.Statements.TransactionScope> activity and call service operations using the ambient transaction.</span></span> <span data-ttu-id="a7386-107">本主題逐步帶領您建立參與交易的工作流程服務和工作流程用戶端。</span><span class="sxs-lookup"><span data-stu-id="a7386-107">This topic walks you through creating a workflow service and workflow client that participate in transactions.</span></span>  
  
> [!WARNING]
> <span data-ttu-id="a7386-108">如果工作流程服務實例是在交易內載入，而工作流程包含 <xref:System.Activities.Statements.Persist> 活動，則工作流程實例會封鎖，直到交易超時為止。</span><span class="sxs-lookup"><span data-stu-id="a7386-108">If a workflow service instance is loaded within a transaction and the workflow contains a <xref:System.Activities.Statements.Persist> activity, the workflow instance will block until the transaction times out.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="a7386-109">每當您使用 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 時，建議您將工作流程中的所有 Receive 放在 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 活動內。</span><span class="sxs-lookup"><span data-stu-id="a7386-109">Whenever you use a <xref:System.ServiceModel.Activities.TransactedReceiveScope> it is recommended to place all Receives in the workflow within <xref:System.ServiceModel.Activities.TransactedReceiveScope> activities.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="a7386-110">如果使用 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 而且訊息按照錯誤的順序送達，工作流程就會在嘗試傳送第一則順序錯誤的訊息時中止。</span><span class="sxs-lookup"><span data-stu-id="a7386-110">When using <xref:System.ServiceModel.Activities.TransactedReceiveScope> and messages arrive in the incorrect order, the workflow will be aborted when trying to deliver the first out of order message.</span></span> <span data-ttu-id="a7386-111">當工作流程閒置時，您必須確定工作流程永遠位於一致的停止點。</span><span class="sxs-lookup"><span data-stu-id="a7386-111">You must make sure your workflow is always at a consistent stopping point when the workflow idles.</span></span> <span data-ttu-id="a7386-112">萬一工作流程已中止，這樣做可讓您從上一個保存點重新啟動工作流程。</span><span class="sxs-lookup"><span data-stu-id="a7386-112">This will allow you to restart the workflow from a previous persistence point should the workflow be aborted.</span></span>  
  
### <a name="create-a-shared-library"></a><span data-ttu-id="a7386-113">建立共用程式庫</span><span class="sxs-lookup"><span data-stu-id="a7386-113">Create a shared library</span></span>  
  
1. <span data-ttu-id="a7386-114">建立一個新的空白 Visual Studio 方案。</span><span class="sxs-lookup"><span data-stu-id="a7386-114">Create a new empty Visual Studio Solution.</span></span>  
  
2. <span data-ttu-id="a7386-115">加入稱為 `Common` 的新類別庫專案。</span><span class="sxs-lookup"><span data-stu-id="a7386-115">Add a new class library project called `Common`.</span></span> <span data-ttu-id="a7386-116">加入下列組件的參考：</span><span class="sxs-lookup"><span data-stu-id="a7386-116">Add references to the following assemblies:</span></span>  
  
    - <span data-ttu-id="a7386-117">System.Activities.dll</span><span class="sxs-lookup"><span data-stu-id="a7386-117">System.Activities.dll</span></span>  
  
    - <span data-ttu-id="a7386-118">System.ServiceModel.dll</span><span class="sxs-lookup"><span data-stu-id="a7386-118">System.ServiceModel.dll</span></span>  
  
    - <span data-ttu-id="a7386-119">System.ServiceModel.Activities.dll</span><span class="sxs-lookup"><span data-stu-id="a7386-119">System.ServiceModel.Activities.dll</span></span>  
  
    - <span data-ttu-id="a7386-120">System.Transactions.dll</span><span class="sxs-lookup"><span data-stu-id="a7386-120">System.Transactions.dll</span></span>  
  
3. <span data-ttu-id="a7386-121">將稱為 `PrintTransactionInfo` 的新類別加入至 `Common` 專案。</span><span class="sxs-lookup"><span data-stu-id="a7386-121">Add a new class called `PrintTransactionInfo` to the `Common` project.</span></span> <span data-ttu-id="a7386-122">此類別衍生自 <xref:System.Activities.NativeActivity>，而且會多載 <xref:System.Activities.NativeActivity.Execute%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="a7386-122">This class is derived from <xref:System.Activities.NativeActivity> and overloads the <xref:System.Activities.NativeActivity.Execute%2A> method.</span></span>  
  
    ```csharp
    using System;  
    using System;  
    using System.Activities;  
    using System.Transactions;  
  
    namespace Common  
    {  
        public class PrintTransactionInfo : NativeActivity  
        {  
            protected override void Execute(NativeActivityContext context)  
            {  
                RuntimeTransactionHandle rth = context.Properties.Find(typeof(RuntimeTransactionHandle).FullName) as RuntimeTransactionHandle;  
  
                if (rth == null)  
                {  
                    Console.WriteLine("There is no ambient RuntimeTransactionHandle");  
                }  
  
                Transaction t = rth.GetCurrentTransaction(context);  
  
                if (t == null)  
                {  
                    Console.WriteLine("There is no ambient transaction");  
                }  
                else  
                {  
                    Console.WriteLine("Transaction: {0} is {1}", t.TransactionInformation.DistributedIdentifier, t.TransactionInformation.Status);  
                }  
            }  
        }  
  
    }  
    ```  
  
     <span data-ttu-id="a7386-123">這是一種原生活動，該活動可顯示環境異動的相關資訊，而且可同時用於本主題中所使用的服務和用戶端工作流程。</span><span class="sxs-lookup"><span data-stu-id="a7386-123">This is a native activity that displays information about the ambient transaction and is used in both the service and client workflows used in this topic.</span></span> <span data-ttu-id="a7386-124">建立解決方案，讓此活動可在 [**工具箱**] 的 [**一般**] 區段中使用。</span><span class="sxs-lookup"><span data-stu-id="a7386-124">Build the solution to make this activity available in the **Common** section of the **Toolbox**.</span></span>  
  
### <a name="implement-the-workflow-service"></a><span data-ttu-id="a7386-125">實作工作流程服務</span><span class="sxs-lookup"><span data-stu-id="a7386-125">Implement the workflow service</span></span>  
  
1. <span data-ttu-id="a7386-126">將名為的新 WCF 工作流程服務加入 `WorkflowService` 至 `Common` 專案。</span><span class="sxs-lookup"><span data-stu-id="a7386-126">Add a new WCF Workflow Service, called `WorkflowService` to the `Common` project.</span></span> <span data-ttu-id="a7386-127">若要執行此動作，請以滑鼠右鍵按一下 `Common` 專案，選取 [**加入**]、[**新增專案**]，選取**WCF Workflow Service**[**已安裝的範本**] 底下的 [**工作流程**]，然後選取 [</span><span class="sxs-lookup"><span data-stu-id="a7386-127">To do this right click the `Common` project, select **Add**, **New Item ...**, Select **Workflow** under **Installed Templates** and select **WCF Workflow Service**.</span></span>  
  
     ![加入工作流程服務](./media/flowing-transactions-into-and-out-of-workflow-services/add-workflow-service.jpg)  
  
2. <span data-ttu-id="a7386-129">刪除預設的 `ReceiveRequest` 和 `SendResponse` 活動。</span><span class="sxs-lookup"><span data-stu-id="a7386-129">Delete the default `ReceiveRequest` and `SendResponse` activities.</span></span>  
  
3. <span data-ttu-id="a7386-130">將 <xref:System.Activities.Statements.WriteLine> 活動拖放到 `Sequential Service` 活動中。</span><span class="sxs-lookup"><span data-stu-id="a7386-130">Drag and drop a <xref:System.Activities.Statements.WriteLine> activity into the `Sequential Service` activity.</span></span> <span data-ttu-id="a7386-131">將文字屬性設定為 `"Workflow Service starting ..."`，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="a7386-131">Set the text property to `"Workflow Service starting ..."` as shown in the following example.</span></span>  
  
     <span data-ttu-id="a7386-132">![將 WriteLine 活動加入至順序服務活動（./media/flowing-transactions-into-and-out-of-workflow-services/add-writeline-sequential-service.jpg）</span><span class="sxs-lookup"><span data-stu-id="a7386-132">![Adding a WriteLine activity to the Sequential Service activity(./media/flowing-transactions-into-and-out-of-workflow-services/add-writeline-sequential-service.jpg)</span></span>  
  
4. <span data-ttu-id="a7386-133">將 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 拖放到 <xref:System.Activities.Statements.WriteLine> 活動後面。</span><span class="sxs-lookup"><span data-stu-id="a7386-133">Drag and drop a <xref:System.ServiceModel.Activities.TransactedReceiveScope> after the <xref:System.Activities.Statements.WriteLine> activity.</span></span> <span data-ttu-id="a7386-134"><xref:System.ServiceModel.Activities.TransactedReceiveScope>活動可以在 [**工具箱**] 的 [**訊息**] 區段中找到。</span><span class="sxs-lookup"><span data-stu-id="a7386-134">The <xref:System.ServiceModel.Activities.TransactedReceiveScope> activity can be found in the **Messaging** section of the **Toolbox**.</span></span> <span data-ttu-id="a7386-135"><xref:System.ServiceModel.Activities.TransactedReceiveScope>活動是由兩個區段**要求**和**主體**所組成。</span><span class="sxs-lookup"><span data-stu-id="a7386-135">The <xref:System.ServiceModel.Activities.TransactedReceiveScope> activity is composed of two sections **Request** and **Body**.</span></span> <span data-ttu-id="a7386-136">**Request**區段包含 <xref:System.ServiceModel.Activities.Receive> 活動。</span><span class="sxs-lookup"><span data-stu-id="a7386-136">The **Request** section contains the <xref:System.ServiceModel.Activities.Receive> activity.</span></span> <span data-ttu-id="a7386-137">[內文] 區段包含在收到訊息**之後，要**在交易內執行的活動。</span><span class="sxs-lookup"><span data-stu-id="a7386-137">The **Body** section contains the activities to execute within a transaction after a message has been received.</span></span>  
  
     ![加入 TransactedReceiveScope 活動](./media/flowing-transactions-into-and-out-of-workflow-services/transactedreceivescope-activity.jpg)  
  
5. <span data-ttu-id="a7386-139">選取 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 活動，然後按一下 [**變數**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a7386-139">Select the <xref:System.ServiceModel.Activities.TransactedReceiveScope> activity and click the **Variables** button.</span></span> <span data-ttu-id="a7386-140">加入下列變數。</span><span class="sxs-lookup"><span data-stu-id="a7386-140">Add the following variables.</span></span>  
  
     ![將變數加入至 TransactedReceiveScope](./media/flowing-transactions-into-and-out-of-workflow-services/add-transactedreceivescope-variables.jpg)  
  
    > [!NOTE]
    > <span data-ttu-id="a7386-142">根據預設，您可以刪除現有的資料變數。</span><span class="sxs-lookup"><span data-stu-id="a7386-142">You can delete the data variable that is there by default.</span></span> <span data-ttu-id="a7386-143">您也可以使用現有的控制碼變數。</span><span class="sxs-lookup"><span data-stu-id="a7386-143">You can also use the existing handle variable.</span></span>  
  
6. <span data-ttu-id="a7386-144">將活動拖放到 <xref:System.ServiceModel.Activities.Receive> 活動的 [**要求**] 區段內 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 。</span><span class="sxs-lookup"><span data-stu-id="a7386-144">Drag and drop a <xref:System.ServiceModel.Activities.Receive> activity within the **Request** section of the <xref:System.ServiceModel.Activities.TransactedReceiveScope> activity.</span></span> <span data-ttu-id="a7386-145">設定下列屬性：</span><span class="sxs-lookup"><span data-stu-id="a7386-145">Set the following properties:</span></span>  
  
    |<span data-ttu-id="a7386-146">屬性</span><span class="sxs-lookup"><span data-stu-id="a7386-146">Property</span></span>|<span data-ttu-id="a7386-147">值</span><span class="sxs-lookup"><span data-stu-id="a7386-147">Value</span></span>|  
    |--------------|-----------|  
    |<span data-ttu-id="a7386-148">CanCreateInstance</span><span class="sxs-lookup"><span data-stu-id="a7386-148">CanCreateInstance</span></span>|<span data-ttu-id="a7386-149">True (核取此核取方塊)</span><span class="sxs-lookup"><span data-stu-id="a7386-149">True (check the checkbox)</span></span>|  
    |<span data-ttu-id="a7386-150">OperationName</span><span class="sxs-lookup"><span data-stu-id="a7386-150">OperationName</span></span>|<span data-ttu-id="a7386-151">StartSample</span><span class="sxs-lookup"><span data-stu-id="a7386-151">StartSample</span></span>|  
    |<span data-ttu-id="a7386-152">ServiceContractName</span><span class="sxs-lookup"><span data-stu-id="a7386-152">ServiceContractName</span></span>|<span data-ttu-id="a7386-153">ITransactionSample</span><span class="sxs-lookup"><span data-stu-id="a7386-153">ITransactionSample</span></span>|  
  
     <span data-ttu-id="a7386-154">工作流程的外觀應該如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="a7386-154">The workflow should look like this:</span></span>  
  
     ![加入 Receive 活動](./media/flowing-transactions-into-and-out-of-workflow-services/add-receive-activity.jpg)  
  
7. <span data-ttu-id="a7386-156">按一下活動中的 [**定義**] 連結 <xref:System.ServiceModel.Activities.Receive> ，然後進行下列設定：</span><span class="sxs-lookup"><span data-stu-id="a7386-156">Click the **Define...** link in the <xref:System.ServiceModel.Activities.Receive> activity and make the following settings:</span></span>  
  
     ![設定 Receive 活動的訊息設定](./media/flowing-transactions-into-and-out-of-workflow-services/receive-message-settings.jpg)  
  
8. <span data-ttu-id="a7386-158">將 <xref:System.Activities.Statements.Sequence> 活動拖放到 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 的 [主體] 區段內。</span><span class="sxs-lookup"><span data-stu-id="a7386-158">Drag and drop a <xref:System.Activities.Statements.Sequence> activity into the Body section of the <xref:System.ServiceModel.Activities.TransactedReceiveScope>.</span></span> <span data-ttu-id="a7386-159">拖放 <xref:System.Activities.Statements.Sequence> 活動內的兩個 <xref:System.Activities.Statements.WriteLine> 活動，並設定 <xref:System.Activities.Statements.WriteLine.Text%2A> 屬性，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="a7386-159">Within the <xref:System.Activities.Statements.Sequence> activity drag and drop two <xref:System.Activities.Statements.WriteLine> activities and set the <xref:System.Activities.Statements.WriteLine.Text%2A> properties as shown in the following table.</span></span>  
  
    |<span data-ttu-id="a7386-160">活動</span><span class="sxs-lookup"><span data-stu-id="a7386-160">Activity</span></span>|<span data-ttu-id="a7386-161">值</span><span class="sxs-lookup"><span data-stu-id="a7386-161">Value</span></span>|  
    |--------------|-----------|  
    |<span data-ttu-id="a7386-162">第一個 WriteLine</span><span class="sxs-lookup"><span data-stu-id="a7386-162">1st WriteLine</span></span>|<span data-ttu-id="a7386-163">「服務：接收已完成」</span><span class="sxs-lookup"><span data-stu-id="a7386-163">"Service: Receive Completed"</span></span>|  
    |<span data-ttu-id="a7386-164">第二個 WriteLine</span><span class="sxs-lookup"><span data-stu-id="a7386-164">2nd WriteLine</span></span>|<span data-ttu-id="a7386-165">"Service: Received = " + requestMessage</span><span class="sxs-lookup"><span data-stu-id="a7386-165">"Service: Received = " + requestMessage</span></span>|  
  
     <span data-ttu-id="a7386-166">工作流程的外觀現在應該如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="a7386-166">The workflow should now look like this:</span></span>  
  
     ![新增 WriteLine 活動之後的順序](./media/flowing-transactions-into-and-out-of-workflow-services/after-adding-writelines.jpg)  
  
9. <span data-ttu-id="a7386-168">將活動拖放到 `PrintTransactionInfo` <xref:System.Activities.Statements.WriteLine> 活動內**主體**中的第二個活動之後 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 。</span><span class="sxs-lookup"><span data-stu-id="a7386-168">Drag and drop the `PrintTransactionInfo` activity after the second <xref:System.Activities.Statements.WriteLine> activity in the **Body** in the <xref:System.ServiceModel.Activities.TransactedReceiveScope> activity.</span></span>  
  
     ![新增 Printtransactioninfo 之後之後的順序](./media/flowing-transactions-into-and-out-of-workflow-services/after-adding-printtransactioninfo.jpg )  
  
10. <span data-ttu-id="a7386-170">將 <xref:System.Activities.Statements.Assign> 活動拖放到 `PrintTransactionInfo` 活動後面，然後根據下表設定其屬性。</span><span class="sxs-lookup"><span data-stu-id="a7386-170">Drag and drop an <xref:System.Activities.Statements.Assign> activity after the `PrintTransactionInfo` activity and set its properties according to the following table.</span></span>  
  
    |<span data-ttu-id="a7386-171">屬性</span><span class="sxs-lookup"><span data-stu-id="a7386-171">Property</span></span>|<span data-ttu-id="a7386-172">值</span><span class="sxs-lookup"><span data-stu-id="a7386-172">Value</span></span>|  
    |--------------|-----------|  
    |<span data-ttu-id="a7386-173">至</span><span class="sxs-lookup"><span data-stu-id="a7386-173">To</span></span>|<span data-ttu-id="a7386-174">replyMessage</span><span class="sxs-lookup"><span data-stu-id="a7386-174">replyMessage</span></span>|  
    |<span data-ttu-id="a7386-175">值</span><span class="sxs-lookup"><span data-stu-id="a7386-175">Value</span></span>|<span data-ttu-id="a7386-176">"Service: Sending reply."</span><span class="sxs-lookup"><span data-stu-id="a7386-176">"Service: Sending reply."</span></span>|  
  
11. <span data-ttu-id="a7386-177">將 <xref:System.Activities.Statements.WriteLine> 活動拖放到 <xref:System.Activities.Statements.Assign> 活動後面，並將其 <xref:System.Activities.Statements.WriteLine.Text%2A> 屬性設定為 "Service: Begin reply"。</span><span class="sxs-lookup"><span data-stu-id="a7386-177">Drag and drop a <xref:System.Activities.Statements.WriteLine> activity after the <xref:System.Activities.Statements.Assign> activity and set its <xref:System.Activities.Statements.WriteLine.Text%2A> property to "Service: Begin reply."</span></span>  
  
     <span data-ttu-id="a7386-178">工作流程的外觀現在應該如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="a7386-178">The workflow should now look like this:</span></span>  
  
     ![加入 Assign 和 WriteLine 之後](./media/flowing-transactions-into-and-out-of-workflow-services/after-adding-sbr-writeline.jpg)  
  
12. <span data-ttu-id="a7386-180">以滑鼠右鍵按一下 <xref:System.ServiceModel.Activities.Receive> 活動，然後選取 [**建立 SendReply** ]，並將它貼到最後一個 <xref:System.Activities.Statements.WriteLine> 活動之後。</span><span class="sxs-lookup"><span data-stu-id="a7386-180">Right click the <xref:System.ServiceModel.Activities.Receive> activity and select **Create SendReply** and paste it after the last <xref:System.Activities.Statements.WriteLine> activity.</span></span> <span data-ttu-id="a7386-181">按一下活動中的 [**定義**] 連結 `SendReplyToReceive` ，然後進行下列設定。</span><span class="sxs-lookup"><span data-stu-id="a7386-181">Click the **Define...** link in the `SendReplyToReceive` activity and make the following settings.</span></span>  
  
     ![回覆訊息設定](./media/flowing-transactions-into-and-out-of-workflow-services/reply-message-settings.jpg)  
  
13. <span data-ttu-id="a7386-183">將活動拖放 <xref:System.Activities.Statements.WriteLine> `SendReplyToReceive` 到活動後面，並將其 <xref:System.Activities.Statements.WriteLine.Text%2A> 屬性設定為 "Service： Reply sent"。</span><span class="sxs-lookup"><span data-stu-id="a7386-183">Drag and drop a <xref:System.Activities.Statements.WriteLine> activity after the `SendReplyToReceive` activity and set it’s <xref:System.Activities.Statements.WriteLine.Text%2A> property to "Service: Reply sent."</span></span>  
  
14. <span data-ttu-id="a7386-184">將 <xref:System.Activities.Statements.WriteLine> 活動拖放到工作流程的底部，然後將其 <xref:System.Activities.Statements.WriteLine.Text%2A> 屬性設定為 "Service: Workflow ends, press ENTER to exit"。</span><span class="sxs-lookup"><span data-stu-id="a7386-184">Drag and drop a <xref:System.Activities.Statements.WriteLine> activity at the bottom of the workflow and set its <xref:System.Activities.Statements.WriteLine.Text%2A> property to "Service: Workflow ends, press ENTER to exit."</span></span>  
  
     <span data-ttu-id="a7386-185">完成的服務工作流程外觀應該如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="a7386-185">The completed service workflow should look like this:</span></span>  
  
     ![完成服務工作流程](./media/flowing-transactions-into-and-out-of-workflow-services/service-complete-workflow.jpg)  
  
### <a name="implement-the-workflow-client"></a><span data-ttu-id="a7386-187">實作工作流程用戶端</span><span class="sxs-lookup"><span data-stu-id="a7386-187">Implement the workflow client</span></span>  
  
1. <span data-ttu-id="a7386-188">將稱為 `WorkflowClient` 的新 WCF 工作流程應用程式加入至 `Common` 專案。</span><span class="sxs-lookup"><span data-stu-id="a7386-188">Add a new WCF Workflow application, called `WorkflowClient` to the `Common` project.</span></span> <span data-ttu-id="a7386-189">若要執行這項操作，請以滑鼠右鍵按一下 `Common` 專案，選取 [新增]、[**新增專案**]， **Activity**選取 [**已安裝\*\*\*\*的**範本] 底下的 [**工作流程**]</span><span class="sxs-lookup"><span data-stu-id="a7386-189">To do this right click the `Common` project, select **Add**, **New Item ...**, Select **Workflow** under **Installed Templates** and select **Activity**.</span></span>  
  
     ![加入 [活動] 專案](./media/flowing-transactions-into-and-out-of-workflow-services/add-activity-project.jpg)  
  
2. <span data-ttu-id="a7386-191">將 <xref:System.Activities.Statements.Sequence> 活動拖放至設計介面上。</span><span class="sxs-lookup"><span data-stu-id="a7386-191">Drag and drop a <xref:System.Activities.Statements.Sequence> activity onto the design surface.</span></span>  
  
3. <span data-ttu-id="a7386-192">拖放 <xref:System.Activities.Statements.Sequence> 活動內的 <xref:System.Activities.Statements.WriteLine> 活動，並將其 <xref:System.Activities.Statements.WriteLine.Text%2A> 屬性設定為 `"Client: Workflow starting"`。</span><span class="sxs-lookup"><span data-stu-id="a7386-192">Within the <xref:System.Activities.Statements.Sequence> activity drag and drop a <xref:System.Activities.Statements.WriteLine> activity and set its <xref:System.Activities.Statements.WriteLine.Text%2A> property to `"Client: Workflow starting"`.</span></span> <span data-ttu-id="a7386-193">工作流程的外觀現在應該如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="a7386-193">The workflow should now look like this:</span></span>  
  
     ![加入 WriteLine 活動](./media/flowing-transactions-into-and-out-of-workflow-services/add-writeline-activity.jpg)  
  
4. <span data-ttu-id="a7386-195">將 <xref:System.Activities.Statements.TransactionScope> 活動拖放到 <xref:System.Activities.Statements.WriteLine> 活動後面。</span><span class="sxs-lookup"><span data-stu-id="a7386-195">Drag and drop a <xref:System.Activities.Statements.TransactionScope> activity after the <xref:System.Activities.Statements.WriteLine> activity.</span></span>  <span data-ttu-id="a7386-196">選取 <xref:System.Activities.Statements.TransactionScope> 活動，按一下 [變數] 按鈕，然後加入下列變數。</span><span class="sxs-lookup"><span data-stu-id="a7386-196">Select the <xref:System.Activities.Statements.TransactionScope> activity, click the Variables button and add the following variables.</span></span>  
  
     ![將變數加入至 TransactionScope](./media/flowing-transactions-into-and-out-of-workflow-services/transactionscope-variables.jpg)  
  
5. <span data-ttu-id="a7386-198">將 <xref:System.Activities.Statements.Sequence> 活動拖放到 <xref:System.Activities.Statements.TransactionScope> 活動的主體內。</span><span class="sxs-lookup"><span data-stu-id="a7386-198">Drag and drop a <xref:System.Activities.Statements.Sequence> activity into the body of the <xref:System.Activities.Statements.TransactionScope> activity.</span></span>  
  
6. <span data-ttu-id="a7386-199">將 `PrintTransactionInfo` 活動拖放到 <xref:System.Activities.Statements.Sequence> 內</span><span class="sxs-lookup"><span data-stu-id="a7386-199">Drag and drop a `PrintTransactionInfo` activity within the <xref:System.Activities.Statements.Sequence></span></span>  
  
7. <span data-ttu-id="a7386-200">將活動拖放 <xref:System.Activities.Statements.WriteLine> `PrintTransactionInfo` 到活動後面，並將其 <xref:System.Activities.Statements.WriteLine.Text%2A> 屬性設定為「用戶端：開始傳送」。</span><span class="sxs-lookup"><span data-stu-id="a7386-200">Drag and drop a <xref:System.Activities.Statements.WriteLine> activity after the `PrintTransactionInfo` activity and set its <xref:System.Activities.Statements.WriteLine.Text%2A> property to "Client: Beginning Send".</span></span> <span data-ttu-id="a7386-201">工作流程的外觀現在應該如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="a7386-201">The workflow should now look like this:</span></span>  
  
     ![新增用戶端：開始傳送活動](./media/flowing-transactions-into-and-out-of-workflow-services/client-add-cbs-writeline.jpg)  
  
8. <span data-ttu-id="a7386-203">將 <xref:System.ServiceModel.Activities.Send> 活動拖放到 <xref:System.Activities.Statements.Assign> 活動後面，然後設定下列屬性：</span><span class="sxs-lookup"><span data-stu-id="a7386-203">Drag and drop a <xref:System.ServiceModel.Activities.Send> activity after the <xref:System.Activities.Statements.Assign> activity and set the following properties:</span></span>  
  
    |<span data-ttu-id="a7386-204">屬性</span><span class="sxs-lookup"><span data-stu-id="a7386-204">Property</span></span>|<span data-ttu-id="a7386-205">值</span><span class="sxs-lookup"><span data-stu-id="a7386-205">Value</span></span>|  
    |--------------|-----------|  
    |<span data-ttu-id="a7386-206">EndpointConfigurationName</span><span class="sxs-lookup"><span data-stu-id="a7386-206">EndpointConfigurationName</span></span>|<span data-ttu-id="a7386-207">workflowServiceEndpoint</span><span class="sxs-lookup"><span data-stu-id="a7386-207">workflowServiceEndpoint</span></span>|  
    |<span data-ttu-id="a7386-208">OperationName</span><span class="sxs-lookup"><span data-stu-id="a7386-208">OperationName</span></span>|<span data-ttu-id="a7386-209">StartSample</span><span class="sxs-lookup"><span data-stu-id="a7386-209">StartSample</span></span>|  
    |<span data-ttu-id="a7386-210">ServiceContractName</span><span class="sxs-lookup"><span data-stu-id="a7386-210">ServiceContractName</span></span>|<span data-ttu-id="a7386-211">ITransactionSample</span><span class="sxs-lookup"><span data-stu-id="a7386-211">ITransactionSample</span></span>|  
  
     <span data-ttu-id="a7386-212">工作流程的外觀現在應該如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="a7386-212">The workflow should now look like this:</span></span>  
  
     ![設定 Send 活動屬性](./media/flowing-transactions-into-and-out-of-workflow-services/client-send-activity-settings.jpg)  
  
9. <span data-ttu-id="a7386-214">按一下 [**定義**] 連結，然後進行下列設定：</span><span class="sxs-lookup"><span data-stu-id="a7386-214">Click the **Define...** link and make the following settings:</span></span>  
  
     ![傳送活動訊息設定](./media/flowing-transactions-into-and-out-of-workflow-services/send-message-settings.jpg)  
  
10. <span data-ttu-id="a7386-216">以滑鼠右鍵按一下 <xref:System.ServiceModel.Activities.Send> 活動，然後選取 [**建立 ReceiveReply**]。</span><span class="sxs-lookup"><span data-stu-id="a7386-216">Right click the <xref:System.ServiceModel.Activities.Send> activity and select **Create ReceiveReply**.</span></span> <span data-ttu-id="a7386-217"><xref:System.ServiceModel.Activities.ReceiveReply> 活動將會自動放在 <xref:System.ServiceModel.Activities.Send> 活動後面。</span><span class="sxs-lookup"><span data-stu-id="a7386-217">The <xref:System.ServiceModel.Activities.ReceiveReply> activity will be automatically placed after the <xref:System.ServiceModel.Activities.Send> activity.</span></span>  
  
11. <span data-ttu-id="a7386-218">按一下 ReceiveReplyForSend 活動中的 [定義] 連結，然後進行下列設定：</span><span class="sxs-lookup"><span data-stu-id="a7386-218">Click the Define... link on the ReceiveReplyForSend activity and make the following settings:</span></span>  
  
     ![設定 ReceiveForSend 訊息設定](./media/flowing-transactions-into-and-out-of-workflow-services/client-reply-message-settings.jpg)  
  
12. <span data-ttu-id="a7386-220">將 <xref:System.Activities.Statements.WriteLine> 活動拖放到 <xref:System.ServiceModel.Activities.Send> 和 <xref:System.ServiceModel.Activities.ReceiveReply> 活動之間，然後將其 <xref:System.Activities.Statements.WriteLine.Text%2A> 屬性設定為 "Client: Send complete"。</span><span class="sxs-lookup"><span data-stu-id="a7386-220">Drag and drop a <xref:System.Activities.Statements.WriteLine> activity between the <xref:System.ServiceModel.Activities.Send> and <xref:System.ServiceModel.Activities.ReceiveReply> activities and set its <xref:System.Activities.Statements.WriteLine.Text%2A> property to "Client: Send complete."</span></span>  
  
13. <span data-ttu-id="a7386-221">將 <xref:System.Activities.Statements.WriteLine> 活動拖放到 <xref:System.ServiceModel.Activities.ReceiveReply> 活動後面，並將其 <xref:System.Activities.Statements.WriteLine.Text%2A> 屬性設定為 "Client side: Reply received = " + replyMessage</span><span class="sxs-lookup"><span data-stu-id="a7386-221">Drag and drop a <xref:System.Activities.Statements.WriteLine> activity after the <xref:System.ServiceModel.Activities.ReceiveReply> activity and set its <xref:System.Activities.Statements.WriteLine.Text%2A> property to "Client side: Reply received = " + replyMessage</span></span>  
  
14. <span data-ttu-id="a7386-222">將 `PrintTransactionInfo` 活動拖放到 <xref:System.Activities.Statements.WriteLine> 活動後面。</span><span class="sxs-lookup"><span data-stu-id="a7386-222">Drag and drop a `PrintTransactionInfo` activity after the <xref:System.Activities.Statements.WriteLine> activity.</span></span>  
  
15. <span data-ttu-id="a7386-223">將 <xref:System.Activities.Statements.WriteLine> 活動拖放到工作流程的結尾，然後將其 <xref:System.Activities.Statements.WriteLine.Text%2A> 屬性設定為 "Client workflow ends"。</span><span class="sxs-lookup"><span data-stu-id="a7386-223">Drag and drop a <xref:System.Activities.Statements.WriteLine> activity at the end of the workflow and set its <xref:System.Activities.Statements.WriteLine.Text%2A> property to "Client workflow ends."</span></span> <span data-ttu-id="a7386-224">完成的工作流程外觀應該如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="a7386-224">The completed client workflow should look like the following diagram.</span></span>  
  
     ![完成的用戶端工作流程](./media/flowing-transactions-into-and-out-of-workflow-services/client-complete-workflow.jpg)  
  
16. <span data-ttu-id="a7386-226">建置方案。</span><span class="sxs-lookup"><span data-stu-id="a7386-226">Build the solution.</span></span>  
  
### <a name="create-the-service-application"></a><span data-ttu-id="a7386-227">建立服務應用程式</span><span class="sxs-lookup"><span data-stu-id="a7386-227">Create the Service application</span></span>  
  
1. <span data-ttu-id="a7386-228">將稱為 `Service` 的新主控台應用程式專案加入至方案。</span><span class="sxs-lookup"><span data-stu-id="a7386-228">Add a new Console Application project called `Service` to the solution.</span></span> <span data-ttu-id="a7386-229">加入下列組件的參考：</span><span class="sxs-lookup"><span data-stu-id="a7386-229">Add references to the following assemblies:</span></span>  
  
    1. <span data-ttu-id="a7386-230">System.Activities.dll</span><span class="sxs-lookup"><span data-stu-id="a7386-230">System.Activities.dll</span></span>  
  
    2. <span data-ttu-id="a7386-231">System.ServiceModel.dll</span><span class="sxs-lookup"><span data-stu-id="a7386-231">System.ServiceModel.dll</span></span>  
  
    3. <span data-ttu-id="a7386-232">System.ServiceModel.Activities.dll</span><span class="sxs-lookup"><span data-stu-id="a7386-232">System.ServiceModel.Activities.dll</span></span>  
  
2. <span data-ttu-id="a7386-233">開啟產生的 Program.cs 檔案以及下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="a7386-233">Open the generated Program.cs file and the following code:</span></span>  
  
    ```csharp
          static void Main()  
          {  
              Console.WriteLine("Building the server.");  
              using (WorkflowServiceHost host = new WorkflowServiceHost(new DeclarativeServiceWorkflow(), new Uri("net.tcp://localhost:8000/TransactedReceiveService/Declarative")))  
              {
                  //Start the server  
                  host.Open();  
                  Console.WriteLine("Service started.");  
  
                  Console.WriteLine();  
                  Console.ReadLine();  
                  //Shutdown  
                  host.Close();  
              };
          }  
    ```  
  
3. <span data-ttu-id="a7386-234">將下列 app.config 檔案加入至專案。</span><span class="sxs-lookup"><span data-stu-id="a7386-234">Add the following app.config file to the project.</span></span>  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <!-- Copyright © Microsoft Corporation.  All rights reserved. -->  
    <configuration>  
        <system.serviceModel>  
            <bindings>  
                <netTcpBinding>  
                    <binding transactionFlow="true" />  
                </netTcpBinding>  
            </bindings>  
        </system.serviceModel>  
    </configuration>  
    ```  
  
### <a name="create-the-client-application"></a><span data-ttu-id="a7386-235">建立用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="a7386-235">Create the client application</span></span>  
  
1. <span data-ttu-id="a7386-236">將稱為 `Client` 的新主控台應用程式專案加入至方案。</span><span class="sxs-lookup"><span data-stu-id="a7386-236">Add a new Console Application project called `Client` to the solution.</span></span> <span data-ttu-id="a7386-237">將參考加入到 System.Activities.dll。</span><span class="sxs-lookup"><span data-stu-id="a7386-237">Add a reference to System.Activities.dll.</span></span>  
  
2. <span data-ttu-id="a7386-238">開啟 program.cs 檔案並加入下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="a7386-238">Open the program.cs file and add the following code.</span></span>  
  
    ```csharp
    class Program  
    {  

        private static AutoResetEvent syncEvent = new AutoResetEvent(false);  
  
        static void Main(string[] args)  
        {  
            //Build client  
            Console.WriteLine("Building the client.");  
            WorkflowApplication client = new WorkflowApplication(new DeclarativeClientWorkflow());  
            client.Completed = Program.Completed;  
            client.Aborted = Program.Aborted;  
            client.OnUnhandledException = Program.OnUnhandledException;  
            //Wait for service to start  
            Console.WriteLine("Press ENTER once service is started.");  
            Console.ReadLine();  
  
            //Start the client
            Console.WriteLine("Starting the client.");  
            client.Run();  
            syncEvent.WaitOne();  
  
            //Sample complete  
            Console.WriteLine();  
            Console.WriteLine("Client complete. Press ENTER to exit.");  
            Console.ReadLine();  
        }  
  
        private static void Completed(WorkflowApplicationCompletedEventArgs e)  
        {  
            Program.syncEvent.Set();  
        }  
  
        private static void Aborted(WorkflowApplicationAbortedEventArgs e)  
        {  
            Console.WriteLine("Client Aborted: {0}", e.Reason);  
            Program.syncEvent.Set();  
        }  
  
        private static UnhandledExceptionAction OnUnhandledException(WorkflowApplicationUnhandledExceptionEventArgs e)  
        {  
            Console.WriteLine("Client had an unhandled exception: {0}", e.UnhandledException);  
            return UnhandledExceptionAction.Cancel;  
        }  
    }  
    ```  
  
## <a name="see-also"></a><span data-ttu-id="a7386-239">請參閱</span><span class="sxs-lookup"><span data-stu-id="a7386-239">See also</span></span>

- [<span data-ttu-id="a7386-240">工作流程服務</span><span class="sxs-lookup"><span data-stu-id="a7386-240">Workflow Services</span></span>](workflow-services.md)
- [<span data-ttu-id="a7386-241">Windows Communication Foundation 異動概觀</span><span class="sxs-lookup"><span data-stu-id="a7386-241">Windows Communication Foundation Transactions Overview</span></span>](transactions-overview.md)
