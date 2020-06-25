---
title: 如何：在執行階段時從控制項集合新增或移除
description: 瞭解如何在表單上的任何容器控制項中加入控制項，並移除控制項，例如面板或分組控制項，或甚至表單本身。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- run time [Windows Forms], removing controls
- controls [Windows Forms], adding using collections
- controls collections
- collections [Windows Forms], adding items
- run time [Windows Forms], adding controls
- controls [Windows Forms], removing using collections
ms.assetid: 771bf895-3d5f-469b-a324-3528f343657e
ms.openlocfilehash: 6c3f2d1f42b130de4d808871265b50510cfb8f47
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/24/2020
ms.locfileid: "85325869"
---
# <a name="how-to-add-to-or-remove-from-a-collection-of-controls-at-run-time"></a><span data-ttu-id="4f082-103">如何：在執行階段時從控制項集合新增或移除</span><span class="sxs-lookup"><span data-stu-id="4f082-103">How to: Add to or Remove from a Collection of Controls at Run Time</span></span>
<span data-ttu-id="4f082-104">應用程式開發的一般工作，是將控制項加入至表單上的任何容器控制項，並從中移除控制項（例如 <xref:System.Windows.Forms.Panel> 或 <xref:System.Windows.Forms.GroupBox> 控制項，甚至是表單本身）。</span><span class="sxs-lookup"><span data-stu-id="4f082-104">Common tasks in application development are adding controls to and removing controls from any container control on your forms (such as the <xref:System.Windows.Forms.Panel> or <xref:System.Windows.Forms.GroupBox> control, or even the form itself).</span></span> <span data-ttu-id="4f082-105">在設計階段，可以將控制項直接拖曳至面板或群組方塊。</span><span class="sxs-lookup"><span data-stu-id="4f082-105">At design time, controls can be dragged directly onto a panel or group box.</span></span> <span data-ttu-id="4f082-106">在執行階段，這些控制項會維護 `Controls` 集合，以便持續追蹤有哪些控制項置於其上。</span><span class="sxs-lookup"><span data-stu-id="4f082-106">At run time, these controls maintain a `Controls` collection, which keeps track of what controls are placed on them.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="4f082-107">下列程式碼範例適用於任何可維護內含控制項集合的控制項。</span><span class="sxs-lookup"><span data-stu-id="4f082-107">The following code example applies to any control that maintains a collection of controls within it.</span></span>  
  
### <a name="to-add-a-control-to-a-collection-programmatically"></a><span data-ttu-id="4f082-108">以程式設計方式將控制項新增至集合</span><span class="sxs-lookup"><span data-stu-id="4f082-108">To add a control to a collection programmatically</span></span>  
  
1. <span data-ttu-id="4f082-109">建立要新增之控制項的執行個體。</span><span class="sxs-lookup"><span data-stu-id="4f082-109">Create an instance of the control to be added.</span></span>  
  
2. <span data-ttu-id="4f082-110">設定新控制項的屬性。</span><span class="sxs-lookup"><span data-stu-id="4f082-110">Set properties of the new control.</span></span>  
  
3. <span data-ttu-id="4f082-111">將控制項新增至父控制項的 `Controls` 集合。</span><span class="sxs-lookup"><span data-stu-id="4f082-111">Add the control to the `Controls` collection of the parent control.</span></span>  
  
     <span data-ttu-id="4f082-112">下列程式碼範例顯示如何建立控制項的實例 <xref:System.Windows.Forms.Button> 。</span><span class="sxs-lookup"><span data-stu-id="4f082-112">The following code example shows how to create an instance of the <xref:System.Windows.Forms.Button> control.</span></span> <span data-ttu-id="4f082-113">它需要具有控制項的表單， <xref:System.Windows.Forms.Panel> 而且所建立之按鈕的事件處理方法 `NewPanelButton_Click` 已經存在。</span><span class="sxs-lookup"><span data-stu-id="4f082-113">It requires a form with a <xref:System.Windows.Forms.Panel> control and that the event-handling method for the button being created, `NewPanelButton_Click`, already exists.</span></span>  
  
    ```vb  
    Public NewPanelButton As New Button()  
  
    Public Sub AddNewControl()  
       ' The Add method will accept as a parameter any object that derives  
       ' from the Control class. In this case, it is a Button control.  
       Panel1.Controls.Add(NewPanelButton)  
       ' The event handler indicated for the Click event in the code
       ' below is used as an example. Substite the appropriate event  
       ' handler for your application.  
       AddHandler NewPanelButton.Click, AddressOf NewPanelButton_Click  
    End Sub  
    ```  
  
    ```csharp  
    public Button newPanelButton = new Button();  
  
    public void addNewControl()  
    {
       // The Add method will accept as a parameter any object that derives  
       // from the Control class. In this case, it is a Button control.  
       panel1.Controls.Add(newPanelButton);  
       // The event handler indicated for the Click event in the code
       // below is used as an example. Substitute the appropriate event  
       // handler for your application.  
       this.newPanelButton.Click += new System.EventHandler(this. NewPanelButton_Click);  
    }  
    ```  
  
### <a name="to-remove-controls-from-a-collection-programmatically"></a><span data-ttu-id="4f082-114">以程式設計方式移除集合中的控制項</span><span class="sxs-lookup"><span data-stu-id="4f082-114">To remove controls from a collection programmatically</span></span>  
  
1. <span data-ttu-id="4f082-115">移除事件的事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="4f082-115">Remove the event handler from the event.</span></span> <span data-ttu-id="4f082-116">在 Visual Basic 中，使用[RemoveHandler 語句](../../../visual-basic/language-reference/statements/removehandler-statement.md)關鍵字;在 c # 中，使用[-= 運算子](../../../csharp/language-reference/operators/subtraction-operator.md)。</span><span class="sxs-lookup"><span data-stu-id="4f082-116">In Visual Basic, use the [RemoveHandler Statement](../../../visual-basic/language-reference/statements/removehandler-statement.md) keyword; in C#, use the [-= operator](../../../csharp/language-reference/operators/subtraction-operator.md).</span></span>  
  
2. <span data-ttu-id="4f082-117">使用 `Remove` 方法，從面板的 `Controls` 集合中刪除所需控制項。</span><span class="sxs-lookup"><span data-stu-id="4f082-117">Use the `Remove` method to delete the desired control from the panel's `Controls` collection.</span></span>  
  
3. <span data-ttu-id="4f082-118">呼叫 <xref:System.Windows.Forms.Control.Dispose%2A> 方法以釋放控制項所使用的所有資源。</span><span class="sxs-lookup"><span data-stu-id="4f082-118">Call the <xref:System.Windows.Forms.Control.Dispose%2A> method to release all the resources used by the control.</span></span>  
  
    ```vb  
    Public Sub RemoveControl()  
    ' NOTE: The code below uses the instance of
    ' the button (NewPanelButton) from the previous example.  
       If Panel1.Controls.Contains(NewPanelButton) Then  
          RemoveHandler NewPanelButton.Click, AddressOf _
             NewPanelButton_Click  
          Panel1.Controls.Remove(NewPanelButton)  
          NewPanelButton.Dispose()  
       End If  
    End Sub  
    ```  
  
    ```csharp  
    private void removeControl(object sender, System.EventArgs e)  
    {  
    // NOTE: The code below uses the instance of
    // the button (newPanelButton) from the previous example.  
       if(panel1.Controls.Contains(newPanelButton))  
       {  
          this.newPanelButton.Click -= new System.EventHandler(this.
             NewPanelButton_Click);  
          panel1.Controls.Remove(newPanelButton);  
          newPanelButton.Dispose();  
       }  
    }  
    ```  
  
## <a name="see-also"></a><span data-ttu-id="4f082-119">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4f082-119">See also</span></span>

- <xref:System.Windows.Forms.Panel>
- [<span data-ttu-id="4f082-120">Panel 控制項</span><span class="sxs-lookup"><span data-stu-id="4f082-120">Panel Control</span></span>](panel-control-windows-forms.md)
