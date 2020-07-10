---
title: 將 [載入]、[儲存] 和 [取消] 按鈕新增至 BindingNavigator 控制項
description: 瞭解如何將 [載入]、[儲存] 和 [取消] 按鈕新增至 Windows Forms BindingNavigator 控制項。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [Windows Forms], manipulating
- BindingNavigator control [Windows Forms], adding buttons
ms.assetid: faa33042-186e-4bb2-8798-17ceb987ec62
ms.openlocfilehash: d4db91b8cfaf2df253d0c4cf5d8a66e9157d4986
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/09/2020
ms.locfileid: "86173415"
---
# <a name="how-to-add-load-save-and-cancel-buttons-to-the-windows-forms-bindingnavigator-control"></a><span data-ttu-id="213bd-103">如何：將載入、儲存和取消按鈕加入至 Windows Form BindingNavigator 控制項</span><span class="sxs-lookup"><span data-stu-id="213bd-103">How to: Add Load, Save, and Cancel Buttons to the Windows Forms BindingNavigator Control</span></span>

<span data-ttu-id="213bd-104"><xref:System.Windows.Forms.BindingNavigator>控制項是一個特殊用途的 <xref:System.Windows.Forms.ToolStrip> 控制項，用於導覽和操作表單上系結至資料的控制項。</span><span class="sxs-lookup"><span data-stu-id="213bd-104">The <xref:System.Windows.Forms.BindingNavigator> control is a special-purpose <xref:System.Windows.Forms.ToolStrip> control that is intended for navigating and manipulating controls on your form that are bound to data.</span></span>

<span data-ttu-id="213bd-105">因為它是 <xref:System.Windows.Forms.ToolStrip> 控制項，所以 <xref:System.Windows.Forms.BindingNavigator> 可以輕鬆地修改元件以包含使用者的其他或替代命令。</span><span class="sxs-lookup"><span data-stu-id="213bd-105">Because it's a <xref:System.Windows.Forms.ToolStrip> control, the <xref:System.Windows.Forms.BindingNavigator> component can be easily modified to include additional or alternative commands for the user.</span></span>

<span data-ttu-id="213bd-106">在下列程式中，控制項系結 <xref:System.Windows.Forms.TextBox> 至資料，而 <xref:System.Windows.Forms.ToolStrip> 新增至表單的控制項則會修改為包含 [載入]、[儲存] 和 [取消] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="213bd-106">In the following procedure, a <xref:System.Windows.Forms.TextBox> control is bound to data, and the <xref:System.Windows.Forms.ToolStrip> control that is added to the form is modified to include load, save, and cancel buttons.</span></span>

## <a name="add-load-save-and-cancel-buttons-to-the-bindingnavigator-component"></a><span data-ttu-id="213bd-107">將 [載入]、[儲存] 和 [取消] 按鈕新增至 BindingNavigator 元件</span><span class="sxs-lookup"><span data-stu-id="213bd-107">Add load, save, and cancel buttons to the BindingNavigator component</span></span>

1. <span data-ttu-id="213bd-108">在 Visual Studio 中，將 <xref:System.Windows.Forms.TextBox> 控制項新增至表單。</span><span class="sxs-lookup"><span data-stu-id="213bd-108">In Visual Studio, add a <xref:System.Windows.Forms.TextBox> control to your form.</span></span>

2. <span data-ttu-id="213bd-109">將它系結至系結 <xref:System.Windows.Forms.BindingSource> 至資料來源的。</span><span class="sxs-lookup"><span data-stu-id="213bd-109">Bind it to a <xref:System.Windows.Forms.BindingSource>, which is bound to a data source.</span></span> <span data-ttu-id="213bd-110">在此範例中， <xref:System.Windows.Forms.BindingSource> 會系結至資料庫。</span><span class="sxs-lookup"><span data-stu-id="213bd-110">For this example, the <xref:System.Windows.Forms.BindingSource> is bound to a database.</span></span>

3. <span data-ttu-id="213bd-111">產生資料集和資料表介面卡之後，將 <xref:System.Windows.Forms.BindingNavigator> 控制項拖曳至表單。</span><span class="sxs-lookup"><span data-stu-id="213bd-111">After the dataset and table adapter are generated, drag a <xref:System.Windows.Forms.BindingNavigator> control to the form.</span></span>

4. <span data-ttu-id="213bd-112">在系結 <xref:System.Windows.Forms.BindingNavigator> <xref:System.Windows.Forms.BindingNavigator.BindingSource%2A> <xref:System.Windows.Forms.BindingSource> 至控制項的表單上，將控制項的屬性設定為。</span><span class="sxs-lookup"><span data-stu-id="213bd-112">Set the <xref:System.Windows.Forms.BindingNavigator> control's <xref:System.Windows.Forms.BindingNavigator.BindingSource%2A> property to the <xref:System.Windows.Forms.BindingSource> on the form that is bound to the controls.</span></span>

5. <span data-ttu-id="213bd-113">選取 <xref:System.Windows.Forms.BindingNavigator> 控制項。</span><span class="sxs-lookup"><span data-stu-id="213bd-113">Select the <xref:System.Windows.Forms.BindingNavigator> control.</span></span>

6. <span data-ttu-id="213bd-114">按一下 [設計工具動作] 圖像 (![ 小型黑色箭號 ](./media/designer-actions-glyph.gif)) 讓 [ **BindingNavigator**工作] 對話方塊出現，然後選取 [**編輯專案**]。</span><span class="sxs-lookup"><span data-stu-id="213bd-114">Click the designer actions glyph (![Small black arrow](./media/designer-actions-glyph.gif)) so the **BindingNavigator Tasks** dialog appears and select **Edit Items**.</span></span>

     <span data-ttu-id="213bd-115">[**專案集合編輯器**] 隨即出現。</span><span class="sxs-lookup"><span data-stu-id="213bd-115">The **Items Collection Editor** appears.</span></span>

7. <span data-ttu-id="213bd-116">在 [**專案集合編輯器**] 中，完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="213bd-116">In the **Items Collection Editor**, complete the following:</span></span>

    1. <span data-ttu-id="213bd-117"><xref:System.Windows.Forms.ToolStripSeparator> <xref:System.Windows.Forms.ToolStripButton> 選取適當的類型 <xref:System.Windows.Forms.ToolStripItem> ，然後按一下 [**新增**] 按鈕，以新增 a 和三個專案。</span><span class="sxs-lookup"><span data-stu-id="213bd-117">Add a <xref:System.Windows.Forms.ToolStripSeparator> and three <xref:System.Windows.Forms.ToolStripButton> items by selecting the appropriate type of <xref:System.Windows.Forms.ToolStripItem> and clicking the **Add** button.</span></span>

    2. <span data-ttu-id="213bd-118">將 <xref:System.Windows.Forms.ToolStripItem.Name%2A> 按鈕的屬性分別設定為**LoadButton**、 **SaveButton**和**CancelButton**。</span><span class="sxs-lookup"><span data-stu-id="213bd-118">Set the <xref:System.Windows.Forms.ToolStripItem.Name%2A> property of the buttons to **LoadButton**, **SaveButton**, and **CancelButton**, respectively.</span></span>

    3. <span data-ttu-id="213bd-119">將 <xref:System.Windows.Forms.ToolStripItem.Text%2A> 按鈕的屬性設定為 [**載入**]、[**儲存**] 和 [**取消**]。</span><span class="sxs-lookup"><span data-stu-id="213bd-119">Set the <xref:System.Windows.Forms.ToolStripItem.Text%2A> property of the buttons to **Load**, **Save**, and **Cancel**.</span></span>

    4. <span data-ttu-id="213bd-120">將 <xref:System.Windows.Forms.ToolStripItem.DisplayStyle%2A> 每個按鈕的屬性設為 [**文字**]。</span><span class="sxs-lookup"><span data-stu-id="213bd-120">Set the <xref:System.Windows.Forms.ToolStripItem.DisplayStyle%2A> property for each of the buttons to **Text**.</span></span> <span data-ttu-id="213bd-121">或者，您可以將此屬性設定為**Image**或**ImageAndText**，並設定要在屬性中顯示的影像 <xref:System.Windows.Forms.ToolStripItem.Image%2A> 。</span><span class="sxs-lookup"><span data-stu-id="213bd-121">Alternatively, you can set this property to **Image** or **ImageAndText**, and set the image to be displayed in the <xref:System.Windows.Forms.ToolStripItem.Image%2A> property.</span></span>

    5. <span data-ttu-id="213bd-122">按一下 [確定]  關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="213bd-122">Click **OK** to close the dialog box.</span></span> <span data-ttu-id="213bd-123">這些按鈕會新增至 <xref:System.Windows.Forms.ToolStrip> 。</span><span class="sxs-lookup"><span data-stu-id="213bd-123">The buttons are added to the <xref:System.Windows.Forms.ToolStrip>.</span></span>

8. <span data-ttu-id="213bd-124">以滑鼠右鍵按一下表單，然後選擇 [ **View Code**]。</span><span class="sxs-lookup"><span data-stu-id="213bd-124">Right-click the form and choose **View Code**.</span></span>

9. <span data-ttu-id="213bd-125">在 [程式碼編輯器] 中，尋找將資料載入資料表介面卡的程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="213bd-125">In the Code Editor, find the line of code that loads data into the table adapter.</span></span> <span data-ttu-id="213bd-126">當您在步驟2中設定資料系結時，就會產生此程式碼。</span><span class="sxs-lookup"><span data-stu-id="213bd-126">This code was generated when you set up the data binding in step 2.</span></span> <span data-ttu-id="213bd-127">程式碼應如下所示： `TableAdapterName.Fill(DataSetName.TableName)` 。</span><span class="sxs-lookup"><span data-stu-id="213bd-127">The code should be similar to the following: `TableAdapterName.Fill(DataSetName.TableName)`.</span></span> <span data-ttu-id="213bd-128">這很可能會在表單的 <xref:System.Windows.Forms.Form.Load> 事件中。</span><span class="sxs-lookup"><span data-stu-id="213bd-128">It will most likely be in the form's <xref:System.Windows.Forms.Form.Load> event.</span></span>

10. <span data-ttu-id="213bd-129">針對 <xref:System.Windows.Forms.ToolStripItem.Click> 您稍早建立之**負載**的事件建立事件處理常式 <xref:System.Windows.Forms.ToolStripButton> ，並將此資料載入程式碼移至其中。</span><span class="sxs-lookup"><span data-stu-id="213bd-129">Create an event handler for the <xref:System.Windows.Forms.ToolStripItem.Click> event of the **Load** <xref:System.Windows.Forms.ToolStripButton> you created earlier and move this data-loading code into it.</span></span>

     <span data-ttu-id="213bd-130">您的程式碼現在看起來應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="213bd-130">Your code should now look similar to the following:</span></span>

    ```vb
    Private Sub LoadButton_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles LoadButton.Click
        TableAdapterName.Fill(DataSetName.TableName)
    End Sub
    ```

    ```csharp
    private void LoadButton_Click(System.Object sender,
        System.EventArgs e)
    {
        TableAdapterName.Fill(DataSetName.TableName);
    }
    ```

11. <span data-ttu-id="213bd-131">針對 <xref:System.Windows.Forms.ToolStripItem.Click> 您稍早建立之**儲存**的事件建立事件處理常式 <xref:System.Windows.Forms.ToolStripButton> ，並撰寫程式碼以更新控制項所系結之資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="213bd-131">Create an event handler for the <xref:System.Windows.Forms.ToolStripItem.Click> event of the **Save**<xref:System.Windows.Forms.ToolStripButton> you created earlier and write code to update the data within the table the control is bound to.</span></span>

    ```vb
    Private Sub SaveButton_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles SaveButton.Click
        TableAdapterName.Update(DataSetName.TableName)
    End Sub
    ```

    ```csharp
    private void SaveButton_Click(System.Object sender,
        System.EventArgs e)
    {
        TableAdapterName.Update(DataSetName.TableName);
    }
    ```

    > [!NOTE]
    > <span data-ttu-id="213bd-132">在某些情況下， <xref:System.Windows.Forms.BindingNavigator> 元件已經有 [**儲存**] 按鈕，但 Windows Form 設計工具未產生任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="213bd-132">In some cases, the <xref:System.Windows.Forms.BindingNavigator> component already has a **Save** button, but no code has been generated by the Windows Forms Designer.</span></span> <span data-ttu-id="213bd-133">在這種情況下，您可以將上述程式碼放在 <xref:System.Windows.Forms.ToolStripItem.Click> 該按鈕的事件處理常式中，而不是在上建立全新的按鈕 <xref:System.Windows.Forms.ToolStrip> 。</span><span class="sxs-lookup"><span data-stu-id="213bd-133">In this case, you can place the preceding code in the <xref:System.Windows.Forms.ToolStripItem.Click> event handler for that button, rather than creating an entirely new button on the <xref:System.Windows.Forms.ToolStrip>.</span></span> <span data-ttu-id="213bd-134">不過，按鈕預設為停用，因此您必須將按鈕的 <xref:System.Windows.Forms.ToolBarButton.Enabled%2A> 屬性設定為， `true` 才能讓按鈕正常運作。</span><span class="sxs-lookup"><span data-stu-id="213bd-134">However, the button is disabled by default, so you must set the <xref:System.Windows.Forms.ToolBarButton.Enabled%2A> property of the button to `true` to have the button function correctly.</span></span>

12. <span data-ttu-id="213bd-135">針對您稍早建立的取消事件建立事件處理常式 <xref:System.Windows.Forms.ToolStripItem.Click> **Cancel** <xref:System.Windows.Forms.ToolStripButton> ，然後撰寫程式碼以取消對所顯示資料記錄所做的任何變更。</span><span class="sxs-lookup"><span data-stu-id="213bd-135">Create an event handler for the <xref:System.Windows.Forms.ToolStripItem.Click> event of the **Cancel** <xref:System.Windows.Forms.ToolStripButton> you created earlier and write code to cancel any changes to the data record that is displayed.</span></span>

    ```vb
    Private Sub CancelButton_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles CancelButton.Click
        BindingSourceName.CancelEdit()
    End Sub
    ```

    ```csharp
    private void CancelButton_Click(System.Object sender, System.EventArgs e)
    {
        BindingSourceName.CancelEdit();
    }
    ```

    > [!NOTE]
    > <span data-ttu-id="213bd-136"><xref:System.Windows.Forms.BindingSource.CancelEdit%2A>方法的範圍是資料列。</span><span class="sxs-lookup"><span data-stu-id="213bd-136">The <xref:System.Windows.Forms.BindingSource.CancelEdit%2A> method is scoped to the row of data.</span></span> <span data-ttu-id="213bd-137">在流覽至下一個記錄之前，請先儲存您在查看該個別記錄時所做的任何變更。</span><span class="sxs-lookup"><span data-stu-id="213bd-137">Save any changes you make while viewing that individual record before navigating to the next record.</span></span>

## <a name="see-also"></a><span data-ttu-id="213bd-138">另請參閱</span><span class="sxs-lookup"><span data-stu-id="213bd-138">See also</span></span>

- <xref:System.Windows.Forms.BindingNavigator>
- <xref:System.Windows.Forms.BindingSource>
- <xref:System.Windows.Forms.ToolStrip>
- [<span data-ttu-id="213bd-139">BindingNavigator 控制項</span><span class="sxs-lookup"><span data-stu-id="213bd-139">BindingNavigator Control</span></span>](bindingnavigator-control-windows-forms.md)
- [<span data-ttu-id="213bd-140">BindingSource 元件概觀</span><span class="sxs-lookup"><span data-stu-id="213bd-140">BindingSource Component Overview</span></span>](bindingsource-component-overview.md)
