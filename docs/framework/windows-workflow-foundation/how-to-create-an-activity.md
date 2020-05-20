---
title: HOW TO：建立活動
description: 本文說明如何在 Workflow Foundation 中建立兩個活動：一個使用程式碼來執行其邏輯，另一個則是使用其他活動所定義。
ms.date: 09/14/2018
dev_langs:
- csharp
- vb
ms.assetid: c09b1e99-21b5-4d96-9c04-ec31db3f4436
ms.openlocfilehash: dae099d102b0c85d09a1ef8bcce56e8a9096bd20
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83419586"
---
# <a name="how-to-create-an-activity"></a><span data-ttu-id="db5c4-103">HOW TO：建立活動</span><span class="sxs-lookup"><span data-stu-id="db5c4-103">How to: Create an Activity</span></span>

<span data-ttu-id="db5c4-104">活動是 [!INCLUDE[wf1](../../../includes/wf1-md.md)] 中的行為核心單位。</span><span class="sxs-lookup"><span data-stu-id="db5c4-104">Activities are the core unit of behavior in [!INCLUDE[wf1](../../../includes/wf1-md.md)].</span></span> <span data-ttu-id="db5c4-105">活動的執行邏輯可以實作在 Managed 程式碼中，或是使用其他活動來實作。</span><span class="sxs-lookup"><span data-stu-id="db5c4-105">The execution logic of an activity can be implemented in managed code or it can be implemented by using other activities.</span></span> <span data-ttu-id="db5c4-106">本主題示範如何建立兩個活動。</span><span class="sxs-lookup"><span data-stu-id="db5c4-106">This topic demonstrates how to create two activities.</span></span> <span data-ttu-id="db5c4-107">第一個活動是簡單的活動，使用程式碼來實作其執行邏輯。</span><span class="sxs-lookup"><span data-stu-id="db5c4-107">The first activity is a simple activity that uses code to implement its execution logic.</span></span> <span data-ttu-id="db5c4-108">第二個活動的實作則是使用其他活動來定義。</span><span class="sxs-lookup"><span data-stu-id="db5c4-108">The implementation of the second activity is defined by using other activities.</span></span> <span data-ttu-id="db5c4-109">教學課程中的下列步驟將會使用這些活動。</span><span class="sxs-lookup"><span data-stu-id="db5c4-109">These activities are used in following steps in the tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="db5c4-110">若要下載教學課程的完整版本，請參閱 [Windows Workflow Foundation (WF45) - 快速入門教學課程](https://go.microsoft.com/fwlink/?LinkID=248976)。</span><span class="sxs-lookup"><span data-stu-id="db5c4-110">To download a completed version of the tutorial, see [Windows Workflow Foundation (WF45) - Getting Started Tutorial](https://go.microsoft.com/fwlink/?LinkID=248976).</span></span>

## <a name="create-the-activity-library-project"></a><span data-ttu-id="db5c4-111">建立活動程式庫專案</span><span class="sxs-lookup"><span data-stu-id="db5c4-111">Create the activity library project</span></span>

1. <span data-ttu-id="db5c4-112">開啟 Visual Studio，然後**New**  >  從 [檔案] 功能表中**選擇 [** 新增**專案**]。</span><span class="sxs-lookup"><span data-stu-id="db5c4-112">Open Visual Studio and choose **New** > **Project** from the **File** menu.</span></span>

2. <span data-ttu-id="db5c4-113">在 [**新增專案**] 對話方塊的 [**已安裝**] 類別之下，選取 [ **Visual c #**  >  **工作流程**] （或 [ **Visual Basic**  >  **工作流程**]）。</span><span class="sxs-lookup"><span data-stu-id="db5c4-113">In the **New Project** dialog, under the **Installed** category, select **Visual C#** > **Workflow** (or **Visual Basic** > **Workflow**).</span></span>

    > [!NOTE]
    > <span data-ttu-id="db5c4-114">如果您沒有看到 [**工作流程**] 範本類別目錄，您可能需要安裝 Visual Studio 的**Windows Workflow Foundation**元件。</span><span class="sxs-lookup"><span data-stu-id="db5c4-114">If you don't see the **Workflow** template category, you may need to install the **Windows Workflow Foundation** component of Visual Studio.</span></span> <span data-ttu-id="db5c4-115">選擇 [**新增專案**] 對話方塊左側的 [**開啟 Visual Studio 安裝程式**] 連結。</span><span class="sxs-lookup"><span data-stu-id="db5c4-115">Choose the **Open Visual Studio Installer** link on the left-hand side of the **New Project** dialog.</span></span> <span data-ttu-id="db5c4-116">在 Visual Studio 安裝程式中，選取 [**個別元件**] 索引標籤。然後，在 [**開發活動**] 類別底下，選取 [ **Windows Workflow Foundation** ] 元件。</span><span class="sxs-lookup"><span data-stu-id="db5c4-116">In Visual Studio Installer, select the **Individual components** tab. Then, under the **Development activities** category, select the **Windows Workflow Foundation** component.</span></span> <span data-ttu-id="db5c4-117">選擇 [**修改**] 以安裝元件。</span><span class="sxs-lookup"><span data-stu-id="db5c4-117">Choose **Modify** to install the component.</span></span>

3. <span data-ttu-id="db5c4-118">選取 [**活動程式庫**] 專案範本。</span><span class="sxs-lookup"><span data-stu-id="db5c4-118">Select the **Activity Library** project template.</span></span> <span data-ttu-id="db5c4-119">在 [名稱]\*\*\*\* 方塊中輸入 `NumberGuessWorkflowActivities`，然後按一下 [確定]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="db5c4-119">Type `NumberGuessWorkflowActivities` in the **Name** box and then click **OK**.</span></span>

4. <span data-ttu-id="db5c4-120">在 **[方案總管]** 中的 **[Activity1.xaml]** 上按一下滑鼠右鍵，並選擇 **[刪除]**。</span><span class="sxs-lookup"><span data-stu-id="db5c4-120">Right-click **Activity1.xaml** in **Solution Explorer** and choose **Delete**.</span></span> <span data-ttu-id="db5c4-121">按一下 **[確定]** 以確認。</span><span class="sxs-lookup"><span data-stu-id="db5c4-121">Click **OK** to confirm.</span></span>

## <a name="create-the-readint-activity"></a><span data-ttu-id="db5c4-122">建立 ReadInt 活動</span><span class="sxs-lookup"><span data-stu-id="db5c4-122">Create the ReadInt activity</span></span>

1. <span data-ttu-id="db5c4-123">從 [**專案**] 功能表中選擇 [**加入新專案**]。</span><span class="sxs-lookup"><span data-stu-id="db5c4-123">Choose **Add New Item** from the **Project** menu.</span></span>

2. <span data-ttu-id="db5c4-124">在 [**已安裝**的  >  **通用專案**] 節點中，選取 [**工作流程**]。</span><span class="sxs-lookup"><span data-stu-id="db5c4-124">In the **Installed** > **Common Items** node, select **Workflow**.</span></span> <span data-ttu-id="db5c4-125">從 [**工作流程**] 清單中選取 [程式**代碼活動**]。</span><span class="sxs-lookup"><span data-stu-id="db5c4-125">Select **Code Activity** from the **Workflow** list.</span></span>

3. <span data-ttu-id="db5c4-126">在 [名稱]\*\*\*\* 方塊中輸入 `ReadInt`，然後按一下 [加入]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="db5c4-126">Type `ReadInt` into the **Name** box and then click **Add**.</span></span>

4. <span data-ttu-id="db5c4-127">以下列定義取代現有的 `ReadInt` 定義。</span><span class="sxs-lookup"><span data-stu-id="db5c4-127">Replace the existing `ReadInt` definition with the following definition.</span></span>

     [!code-csharp[CFX_WF_GettingStarted#1](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_wf_gettingstarted/cs/readint.cs#1)]
     [!code-vb[CFX_WF_GettingStarted#1](~/samples/snippets/visualbasic/VS_Snippets_CFX/cfx_wf_gettingstarted/vb/readint.vb#1)]

    > [!NOTE]
    > <span data-ttu-id="db5c4-128">`ReadInt` 活動衍生自 <xref:System.Activities.NativeActivity%601>，而不是程式碼活動範本預設的 <xref:System.Activities.CodeActivity>。</span><span class="sxs-lookup"><span data-stu-id="db5c4-128">The `ReadInt` activity derives from <xref:System.Activities.NativeActivity%601> instead of <xref:System.Activities.CodeActivity>, which is the default for the code activity template.</span></span> <span data-ttu-id="db5c4-129">如果活動提供單一結果 (透過 <xref:System.Activities.CodeActivity%601> 引數公開)，則可使用 <xref:System.Activities.Activity%601.Result%2A>，但 <xref:System.Activities.CodeActivity%601> 不支援使用書籤，因而會使用 <xref:System.Activities.NativeActivity%601>。</span><span class="sxs-lookup"><span data-stu-id="db5c4-129"><xref:System.Activities.CodeActivity%601> can be used if the activity provides a single result, which is exposed through the <xref:System.Activities.Activity%601.Result%2A> argument, but <xref:System.Activities.CodeActivity%601> does not support the use of bookmarks, so <xref:System.Activities.NativeActivity%601> is used.</span></span>

## <a name="create-the-prompt-activity"></a><span data-ttu-id="db5c4-130">建立提示活動</span><span class="sxs-lookup"><span data-stu-id="db5c4-130">Create the Prompt activity</span></span>

1. <span data-ttu-id="db5c4-131">按**Ctrl** + **Shift** + **B**以建立專案。</span><span class="sxs-lookup"><span data-stu-id="db5c4-131">Press **Ctrl**+**Shift**+**B** to build the project.</span></span> <span data-ttu-id="db5c4-132">建置專案可將此專案中的 `ReadInt` 活動用來建置此步驟中的自訂活動。</span><span class="sxs-lookup"><span data-stu-id="db5c4-132">Building the project enables the `ReadInt` activity in this project to be used to build the custom activity from this step.</span></span>

2. <span data-ttu-id="db5c4-133">從 [**專案**] 功能表中選擇 [**加入新專案**]。</span><span class="sxs-lookup"><span data-stu-id="db5c4-133">Choose **Add New Item** from the **Project** menu.</span></span>

3. <span data-ttu-id="db5c4-134">在 [**已安裝**的  >  **通用專案**] 節點中，選取 [**工作流程**]。</span><span class="sxs-lookup"><span data-stu-id="db5c4-134">In the **Installed** > **Common Items** node, select **Workflow**.</span></span> <span data-ttu-id="db5c4-135">從 **[工作流程]** 清單中選取 **[活動]**。</span><span class="sxs-lookup"><span data-stu-id="db5c4-135">Select **Activity** from the **Workflow** list.</span></span>

4. <span data-ttu-id="db5c4-136">在 [名稱]\*\*\*\* 方塊中輸入 `Prompt`，然後按一下 [加入]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="db5c4-136">Type `Prompt` into the **Name** box and then click **Add**.</span></span>

5. <span data-ttu-id="db5c4-137">按兩下 [Prompt]，**方案總管**中的**xaml**將它顯示在設計工具中（如果尚未顯示）。</span><span class="sxs-lookup"><span data-stu-id="db5c4-137">Double-click **Prompt.xaml** in **Solution Explorer** to display it in the designer if it is not already displayed.</span></span>

6. <span data-ttu-id="db5c4-138">在活動設計工具的左下方按一下 **[引數]**，以顯示 **[引數]** 窗格。</span><span class="sxs-lookup"><span data-stu-id="db5c4-138">Click **Arguments** in the lower-left side of the activity designer to display the **Arguments** pane.</span></span>

7. <span data-ttu-id="db5c4-139">按一下 **[建立引數]**。</span><span class="sxs-lookup"><span data-stu-id="db5c4-139">Click **Create Argument**.</span></span>

8. <span data-ttu-id="db5c4-140">`BookmarkName`在 [**名稱**] 方塊中輸入，從 [**方向**] 下拉式清單中選取 [ **In** ]，從 [**引數型**別] 下拉式清單中選取 [**字串**]，然後按下**enter**以儲存引數。</span><span class="sxs-lookup"><span data-stu-id="db5c4-140">Type `BookmarkName` into the **Name** box, select **In** from the **Direction** drop-down list, select **String** from the **Argument type** drop-down list, and then press **Enter** to save the argument.</span></span>

9. <span data-ttu-id="db5c4-141">按一下 **[建立引數]**。</span><span class="sxs-lookup"><span data-stu-id="db5c4-141">Click **Create Argument**.</span></span>

10. <span data-ttu-id="db5c4-142">在 `Result` 新加入之引數底下的 [**名稱**] 方塊中輸入 `BookmarkName` ，從 [**方向**] 下拉式清單中選取 [ **Out** ]，選取 [自**變數型**別] 下拉式清單中的 [ **Int32** ]，然後按**enter**。</span><span class="sxs-lookup"><span data-stu-id="db5c4-142">Type `Result` into the **Name** box that is underneath the newly added `BookmarkName` argument, select **Out** from the **Direction** drop-down list, select **Int32** from the **Argument type** drop-down list, and then press **Enter**.</span></span>

11. <span data-ttu-id="db5c4-143">按一下 **[建立引數]**。</span><span class="sxs-lookup"><span data-stu-id="db5c4-143">Click **Create Argument**.</span></span>

12. <span data-ttu-id="db5c4-144">`Text`在 [**名稱**] 方塊中輸入，從 [**方向**] 下拉式清單中選取 [ **In** ]，從 [**引數型**別] 下拉式清單中選取 [**字串**]，然後按下**enter**以儲存引數。</span><span class="sxs-lookup"><span data-stu-id="db5c4-144">Type `Text` into the **Name** box, select **In** from the **Direction** drop-down list, select **String** from the **Argument type** drop-down list, and then press **Enter** to save the argument.</span></span>

     <span data-ttu-id="db5c4-145">這三個引數會繫結至下列步驟中加入至 <xref:System.Activities.Statements.WriteLine> 活動之 `ReadInt` 和 `Prompt` 活動的對應引數。</span><span class="sxs-lookup"><span data-stu-id="db5c4-145">These three arguments are bound to the corresponding arguments of the <xref:System.Activities.Statements.WriteLine> and `ReadInt` activities that are added to the `Prompt` activity in the following steps.</span></span>

13. <span data-ttu-id="db5c4-146">在活動設計工具的左下方按一下 **[引數]**，以關閉 **[引數]** 窗格。</span><span class="sxs-lookup"><span data-stu-id="db5c4-146">Click **Arguments** in the lower-left side of the activity designer to close the **Arguments** pane.</span></span>

14. <span data-ttu-id="db5c4-147">從 [工具箱] 的 [**控制流程**] 區段，將 [**序列**] 活動拖放到 [**提示**] 活動設計**工具**的 [在**此放置活動**] 標籤上。</span><span class="sxs-lookup"><span data-stu-id="db5c4-147">Drag a **Sequence** activity from the **Control Flow** section of the **Toolbox** and drop it onto the **Drop activity here** label of the **Prompt** activity designer.</span></span>

    > [!TIP]
    > <span data-ttu-id="db5c4-148">若 **[工具箱]** 視窗並未顯示，請從 **[檢視]** 功能表中選取 **[工具箱]**。</span><span class="sxs-lookup"><span data-stu-id="db5c4-148">If the **Toolbox** window is not displayed, select **Toolbox** from the **View** menu.</span></span>

15. <span data-ttu-id="db5c4-149">將 [ **WriteLine** ] 活動從 [**工具箱**] 的 [**基本**] 區段拖放到 [ **Sequence** ] 活動的 [在**此放置活動**] 標籤上。</span><span class="sxs-lookup"><span data-stu-id="db5c4-149">Drag a **WriteLine** activity from the **Primitives** section of the **Toolbox** and drop it onto the **Drop activity here** label of the **Sequence** activity.</span></span>

16. <span data-ttu-id="db5c4-150">在 [ **Text** **Text** **Prompt** **WriteLine** `Text` **屬性**] 視窗中輸入 [**輸入 c # 運算式**] 或 [**輸入 VB 運算式**] 方塊，將 [WriteLine] 活動的 [文字] 引數系結至 [提示] 活動的 [text] 引數，然後按兩次**tab**鍵。</span><span class="sxs-lookup"><span data-stu-id="db5c4-150">Bind the **Text** argument of the **WriteLine** activity to the **Text** argument of the **Prompt** activity by typing `Text` into the **Enter a C# expression** or **Enter a VB expression** box in the **Properties** window, and then press the **Tab** key two times.</span></span> <span data-ttu-id="db5c4-151">這樣會將選項移出屬性外，以關閉 IntelliSense 清單成員視窗並儲存屬性值。</span><span class="sxs-lookup"><span data-stu-id="db5c4-151">This dismisses the IntelliSense list members window and saves the property value by moving the selection off the property.</span></span> <span data-ttu-id="db5c4-152">您也可以在 `Text` 活動本身的 [**輸入 c # 運算式**] 或 [**輸入 VB 運算式**] 方塊中鍵入，來設定這個屬性。</span><span class="sxs-lookup"><span data-stu-id="db5c4-152">This property can also be set by typing `Text` into the **Enter a C# expression** or **Enter a VB expression** box on the activity itself.</span></span>

    > [!TIP]
    > <span data-ttu-id="db5c4-153">如果沒有顯示 [**屬性] 視窗**，請從 [**視圖**] 功能表中選取 [**屬性視窗]** 。</span><span class="sxs-lookup"><span data-stu-id="db5c4-153">If the **Properties Window** is not displayed, select **Properties Window** from the **View** menu.</span></span>

17. <span data-ttu-id="db5c4-154">從 [**工具箱**] 的 [ **[numberguessworkflowactivities]** ] 區段中，將 [ **ReadInt** ] 活動拖放到 [ **Sequence** ] 活動中，使其遵循 [ **WriteLine** ] 活動。</span><span class="sxs-lookup"><span data-stu-id="db5c4-154">Drag a **ReadInt** activity from the **NumberGuessWorkflowActivities** section of the **Toolbox** and drop it in the **Sequence** activity so that it follows the **WriteLine** activity.</span></span>

18. <span data-ttu-id="db5c4-155">將**ReadInt**活動的**BookmarkName**引數系結至 [**提示**] 活動的**BookmarkName**引數，方法是在 `BookmarkName` [**屬性] 視窗**中輸入**BookmarkName**引數右邊的 [**輸入 VB 運算式**] 方塊，然後按兩次**tab**鍵以關閉 [IntelliSense 清單成員] 視窗並儲存屬性。</span><span class="sxs-lookup"><span data-stu-id="db5c4-155">Bind the **BookmarkName** argument of the **ReadInt** activity to the **BookmarkName** argument of the **Prompt** activity by typing `BookmarkName` into the **Enter a VB expression** box to the right of the **BookmarkName** argument in the **Properties Window**, and then press the **Tab** key two times to close the IntelliSense list members window and save the property.</span></span>

19. <span data-ttu-id="db5c4-156">在 [屬性] 視窗中，將 [ **ReadInt** ] 活動的**結果**引數系結至 [**提示**] 活動**的 [結果**] 引數，然後 `Result` 按兩次**Properties Window** **Enter a VB expression** **tab**鍵。 **Result**</span><span class="sxs-lookup"><span data-stu-id="db5c4-156">Bind the **Result** argument of the **ReadInt** activity to the **Result** argument of the **Prompt** activity by typing `Result` into the **Enter a VB expression** box to the right of the **Result** argument in the **Properties Window**, and then press the **Tab** key two times.</span></span>

20. <span data-ttu-id="db5c4-157">按**Ctrl** + **Shift** + **B**以建立方案。</span><span class="sxs-lookup"><span data-stu-id="db5c4-157">Press **Ctrl**+**Shift**+**B** to build the solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db5c4-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="db5c4-158">Next steps</span></span>

<span data-ttu-id="db5c4-159">如需如何使用這些活動來建立工作流程的指示，請參閱教學課程 how [to：建立工作流程](how-to-create-a-workflow.md)中的下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="db5c4-159">For instructions on how to create a workflow by using these activities, see the next step in the tutorial, [How to: Create a Workflow](how-to-create-a-workflow.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="db5c4-160">另請參閱</span><span class="sxs-lookup"><span data-stu-id="db5c4-160">See also</span></span>

- <xref:System.Activities.CodeActivity>
- <xref:System.Activities.NativeActivity%601>
- [<span data-ttu-id="db5c4-161">設計及實作自訂活動</span><span class="sxs-lookup"><span data-stu-id="db5c4-161">Designing and Implementing Custom Activities</span></span>](designing-and-implementing-custom-activities.md)
- [<span data-ttu-id="db5c4-162">消費者入門教學課程</span><span class="sxs-lookup"><span data-stu-id="db5c4-162">Getting Started Tutorial</span></span>](getting-started-tutorial.md)
- [<span data-ttu-id="db5c4-163">如何：建立工作流程</span><span class="sxs-lookup"><span data-stu-id="db5c4-163">How to: Create a Workflow</span></span>](how-to-create-a-workflow.md)
- [<span data-ttu-id="db5c4-164">在自訂活動設計工具中使用 ExpressionTextBox</span><span class="sxs-lookup"><span data-stu-id="db5c4-164">Using the ExpressionTextBox in a Custom Activity Designer</span></span>](./samples/using-the-expressiontextbox-in-a-custom-activity-designer.md)
