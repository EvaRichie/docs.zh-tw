---
title: HOW TO：建立循序工作流程
description: 本文會建立同時使用內建活動的工作流程，例如 [序列] 活動和自訂活動。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 5280e816-ae17-48c4-8de0-a1e6895dd8f0
ms.openlocfilehash: f80ac471fdcc425504b11b5fb17effa888aa9590
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83419690"
---
# <a name="how-to-create-a-sequential-workflow"></a>HOW TO：建立循序工作流程

工作流程可以從內建活動建構，也可以從自訂活動建構。 本主題將逐步說明如何建立使用內建活動（例如活動）的工作流程， <xref:System.Activities.Statements.Sequence> 以及先前[如何：建立活動](how-to-create-an-activity.md)主題中的自訂活動。 此工作流程會以數字猜測遊戲為模型。

> [!NOTE]
> 「快速入門」教學課程中的每個主題都與之前的主題息息相關。 若要完成本主題，您必須先完成[如何：建立活動](how-to-create-an-activity.md)。

> [!NOTE]
> 若要下載教學課程的完整版本，請參閱 [Windows Workflow Foundation (WF45) - 快速入門教學課程](https://go.microsoft.com/fwlink/?LinkID=248976)。

## <a name="to-create-the-workflow"></a>建立工作流程

1. 以滑鼠右鍵按一下**方案總管**中的 **[numberguessworkflowactivities]** ，然後選取 [**加入**]、[**新增專案**]。

2. 在 [**已安裝**的**通用專案**] 節點中，選取 [**工作流程**]。 從 **[工作流程]** 清單中選取 **[活動]**。

3. `SequentialNumberGuessWorkflow`在 [**名稱**] 方塊中輸入，然後按一下 [**新增**]。

4. 從 [**工具箱**] 的 [**控制流程**] 區段，將 [**序列**] 活動拖放到工作流程設計介面上的 [在**此放置活動**] 標籤上。

## <a name="to-create-the-workflow-variables-and-arguments"></a>若要建立工作流程變數和引數

1. 按兩下**方案總管**中的 [ **SequentialNumberGuessWorkflow** ]，在設計工具中顯示工作流程（如果尚未顯示）。

2. 在工作流程設計工具的左下方按一下 [**引數**]，以顯示 [**引數**] 窗格。

3. 按一下 **[建立引數]**。

4. 在 `MaxNumber` [**名稱**] 方塊中輸入，從 [**方向**] 下拉式清單中選取 [In]，選取 [自**變數型**別] 下拉式清單**中**的 [ **Int32** ]，然後按下 enter 以儲存引數。

5. 按一下 **[建立引數]**。

6. 在 `Turns` 新加入的引數下方輸入 [**名稱**] 方塊 `MaxNumber` ，從 [**方向**] 下拉式清單中選取 [ **Out** ]，選取 [自**變數型**別] 下拉式清單中的 [ **Int32** ]，然後按 enter。

7. 在活動設計工具的左下方按一下 **[引數]**，以關閉 **[引數]** 窗格。

8. 按一下工作流程設計工具左下方的 [**變數**]，以顯示 [**變數**] 窗格。

9. 按一下 **[建立變數]**。

    > [!TIP]
    > 如果沒有顯示 [**建立變數**] 方塊，請按一下工作流程設計工具介面上的 [**序列**] 活動加以選取。

10. 在 `Guess` [**名稱**] 方塊中輸入，從 [**變數類型**] 下拉式清單中選取 [ **Int32** ]，然後按 enter 儲存變數。

11. 按一下 **[建立變數]**。

12. 在 `Target` [**名稱**] 方塊中輸入，從 [**變數類型**] 下拉式清單中選取 [ **Int32** ]，然後按 enter 儲存變數。

13. 在活動設計工具的左下方按一下 **[變數]**，以關閉 **[變數]** 窗格。

## <a name="to-add-the-workflow-activities"></a>若要加入工作流程活動

1. 將 [ **Assign** ] 活動從 [**工具箱**] 的 [**基本**] 區段拖放到 [ **Sequence** ] 活動上。 在 [到] 方塊中輸入 `Target` ，並在 [**輸入 c # 運算式**] 或 [**輸入 VB 運算式**] 方塊中輸入下列運算式。 **To**

    ```vb
    New System.Random().Next(1, MaxNumber + 1)
    ```

    ```csharp
    new System.Random().Next(1, MaxNumber + 1)
    ```

    > [!TIP]
    > 若 **[工具箱]** 視窗並未顯示，請從 **[檢視]** 功能表中選取 **[工具箱]**。

2. 從 [**工具箱**] 的 [**控制流程**] 區段，將 [ **DoWhile** ] 活動拖放到工作流程上，使其位於 [**指派**] 活動下方。

3. 在 [ **DoWhile** ] 活動的 [ **Condition** ] 屬性值方塊中輸入下列運算式。

    ```vb
    Guess <> Target
    ```

    ```csharp
    Guess != Target
    ```

     <xref:System.Activities.Statements.DoWhile> 活動會執行其子活動，然後評估其 <xref:System.Activities.Statements.DoWhile.Condition%2A>。 如果 <xref:System.Activities.Statements.DoWhile.Condition%2A> 判斷值為 `True`，則會再次執行 <xref:System.Activities.Statements.DoWhile> 中的活動。 此範例中會評估使用者的猜測，而 <xref:System.Activities.Statements.DoWhile> 會繼續，直到猜測正確為止。

4. 從 [**工具箱**] 的 [ **[numberguessworkflowactivities]** ] 區段拖曳 [**提示**] 活動，並將它放在上一個步驟的 [ **DoWhile** ] 活動中。

5. 在 [**屬性] 視窗**中，于 [ `"EnterGuess"` **提示**] 活動的 [ **BookmarkName** ] 屬性值方塊中輸入包含引號。 `Guess`在 [**結果**] 屬性值方塊中輸入，然後在 [ **Text** ] 屬性方塊中輸入下列運算式。

    ```vb
    "Please enter a number between 1 and " & MaxNumber
    ```

    ```csharp
    "Please enter a number between 1 and " + MaxNumber
    ```

    > [!TIP]
    > 如果沒有顯示 [**屬性] 視窗**，請從 [**視圖**] 功能表中選取 [**屬性視窗]** 。

6. 將 [ **Assign** ] 活動從 [**工具箱**] 的 [**基本**] 區段拖放到 [ **DoWhile** ] 活動中，使其遵循 [**提示**] 活動。

    > [!NOTE]
    > 當您卸載 [**指派**] 活動時，請注意工作流程設計工具如何自動加入 [ **Sequence** ] 活動，以同時包含 [**提示**] 活動和新加入的 [**指派**] 活動。

7. 在 `Turns` [**到**] 方塊中輸入，然後 `Turns + 1` 在 [**輸入 c # 運算式**] 或 [**輸入 VB 運算式**] 方塊中。

8. 從 [**工具箱**] 的 [**控制流程**] 區段，將 [ **If** ] 活動拖放到 [ **Sequence** ] 活動中，使其遵循新加入的 [**指派**] 活動。

9. 在 [ **If** ] 活動的 [ **Condition** ] 屬性值方塊中輸入下列運算式。

    ```vb
    Guess <> Target
    ```

    ```csharp
    Guess != Target
    ```

10. 從 [**工具箱**] 的 [**控制流程**] 區段中，將另一個 [ **if** ] 活動拖放到第一個 [ **if** ] 活動的 [ **Then** ] 區段中。

11. 在新加入的 [ **If** ] 活動的 [ **Condition** ] 屬性值方塊中輸入下列運算式。

    ```text
    Guess < Target
    ```

12. 從 [**工具箱**] 的 [**基本**] 區段拖放兩個 [ **WriteLine** ] 活動，使其成為新加入之 [ **If** ] 活動的 [ **Then** ] 區段，另一個則位於 [ **Else** ] 區段中。

13. 按一下 [ **Then** ] 區段中的 [ **WriteLine** ] 活動加以選取，然後在 [ **Text** ] 屬性值方塊中輸入下列運算式。

    ```text
    "Your guess is too low."
    ```

14. 按一下 [ **Else** ] 區段中的 [ **WriteLine** ] 活動加以選取，然後在 [ **Text** ] 屬性值方塊中輸入下列運算式。

    ```text
    "Your guess is too high."
    ```

     下列範例說明完成的工作流程：

     ![顯示已完成之順序工作流程的螢幕擷取畫面。](./media/how-to-create-a-sequential-workflow/complete-sequential-workflow.jpg)

## <a name="to-build-the-workflow"></a>若要建置工作流程

1. 按 CTRL+SHIFT+B 建置解決方案。

     如需有關如何執行工作流程的指示，請參閱下一個主題[：如何：執行工作流程](how-to-run-a-workflow.md)。 如果您已經完成如何：以不同的工作流程樣式[執行工作流程](how-to-run-a-workflow.md)步驟，而且想要使用此步驟中的順序工作流程執行，請直接跳至[如何：執行工作流程](how-to-run-a-workflow.md)中的[建立並執行應用程式](how-to-run-a-workflow.md#BKMK_ToRunTheApplication)一節。

## <a name="see-also"></a>另請參閱

- <xref:System.Activities.Statements.Flowchart>
- <xref:System.Activities.Statements.FlowDecision>
- [Windows Workflow Foundation 程式設計](programming.md)
- [設計工作流程](designing-workflows.md)
- [消費者入門教學課程](getting-started-tutorial.md)
- [如何：建立活動](how-to-create-an-activity.md)
- [如何：執行工作流程](how-to-run-a-workflow.md)
