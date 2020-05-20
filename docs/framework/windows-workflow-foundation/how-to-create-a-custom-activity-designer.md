---
title: HOW TO：建立自訂活動設計工具
description: 本文說明如何建立具有放置區域的 Workflow Foundation 自訂活動設計工具，其中可以放置任意活動。
ms.date: 03/30/2017
ms.assetid: 2f3aade6-facc-44ef-9657-a407ef8b9b31
ms.openlocfilehash: 015efd1e482e2b531d28b9caec411c76116c9653
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83419781"
---
# <a name="how-to-create-a-custom-activity-designer"></a><span data-ttu-id="efeb8-103">HOW TO：建立自訂活動設計工具</span><span class="sxs-lookup"><span data-stu-id="efeb8-103">How to: Create a Custom Activity Designer</span></span>

<span data-ttu-id="efeb8-104">通常實作自訂活動設計工具的方式，是讓其相關聯活動能夠透過其他活動組合，這些活動的設計工具能夠隨著活動放到設計介面上。</span><span class="sxs-lookup"><span data-stu-id="efeb8-104">Custom activity designers are typically implemented so that their associated activities are composable with other activities whose designers can be dropped on to the design surface with them.</span></span> <span data-ttu-id="efeb8-105">這項功能需要自訂活動設計工具提供可放置任意活動的「卸載區」，以及在設計介面上管理專案所產生之集合的方法。</span><span class="sxs-lookup"><span data-stu-id="efeb8-105">This functionality requires that a custom activity designer provide a "drop zone" where an arbitrary activity can be placed and also the means to manage the resulting collection of elements on the design surface.</span></span> <span data-ttu-id="efeb8-106">本主題說明如何建立包含這種卸除區的自訂活動設計工具，以及如何建立能夠提供管理設計工具項目集合所需之編輯功能的自訂活動設計工具。</span><span class="sxs-lookup"><span data-stu-id="efeb8-106">This topic describes how to create a custom activity designer that contains such a drop zone and how to create a custom activity designer that provides that editing functionality needed to manage the collection of designer elements.</span></span>

<span data-ttu-id="efeb8-107">自訂活動設計工具通常繼承自 <xref:System.Activities.Presentation.ActivityDesigner>，它是任何沒有特定設計工具之活動的預設基底活動設計工具型別。</span><span class="sxs-lookup"><span data-stu-id="efeb8-107">Custom activity designers typically inherit from <xref:System.Activities.Presentation.ActivityDesigner> which is the default base activity designer type for any activities without a specific designer.</span></span> <span data-ttu-id="efeb8-108">這個型別提供與屬性方格互動及設定管理色彩和圖示等基本層面等的設計階段經驗。</span><span class="sxs-lookup"><span data-stu-id="efeb8-108">This type provides the design-time experience of interacting with the property grid and configuring basic aspects such as managing colors and icons.</span></span>

<span data-ttu-id="efeb8-109"><xref:System.Activities.Presentation.ActivityDesigner> 會使用兩項 Helper 控制項 (<xref:System.Activities.Presentation.WorkflowItemPresenter> 和 <xref:System.Activities.Presentation.WorkflowItemsPresenter>) 來簡化自訂活動設計工具的開發。</span><span class="sxs-lookup"><span data-stu-id="efeb8-109"><xref:System.Activities.Presentation.ActivityDesigner> uses two helper controls, <xref:System.Activities.Presentation.WorkflowItemPresenter> and <xref:System.Activities.Presentation.WorkflowItemsPresenter> to make it easier to develop custom activity designers.</span></span> <span data-ttu-id="efeb8-110">這些 Helper 能夠處理拖放子項目、刪除、選取及加入子項目之類的常見功能。</span><span class="sxs-lookup"><span data-stu-id="efeb8-110">They handle common functionality like dragging and dropping of child elements, deletion, selection, and addition of those child elements.</span></span> <span data-ttu-id="efeb8-111"><xref:System.Activities.Presentation.WorkflowItemPresenter>允許內的單一子 UI 專案（提供「卸載區」），而 <xref:System.Activities.Presentation.WorkflowItemsPresenter> 可提供支援多個 UI 元素，包括排序、移動、刪除和加入子專案等其他功能。</span><span class="sxs-lookup"><span data-stu-id="efeb8-111">The <xref:System.Activities.Presentation.WorkflowItemPresenter> allows a single child UI element inside, providing the "drop zone", it while the <xref:System.Activities.Presentation.WorkflowItemsPresenter> can provide support multiple UI elements, including additional functionality like the ordering, moving, deleting, and adding of child elements.</span></span>

<span data-ttu-id="efeb8-112">在自訂活動設計工具的執行中，需要反白顯示的另一個重要部分，就是使用 WPF 資料系結，將視覺編輯系結至儲存在設計工具中所編輯之記憶體的實例。</span><span class="sxs-lookup"><span data-stu-id="efeb8-112">The other key part of the story that needs highlighting in the implementation of a custom activity designer concerns the way in which the visual edits are bound using WPF data binding to the instance stored in memory of what we are editing in the designer.</span></span> <span data-ttu-id="efeb8-113">這項操作可透過模型項目樹狀完成，該樹狀也負責進行變更通知，以及追蹤如狀態變更這類事件。</span><span class="sxs-lookup"><span data-stu-id="efeb8-113">This is accomplished by the Model Item tree, which is also responsible for enabling change notification and the tracking of events like changes in states.</span></span>

<span data-ttu-id="efeb8-114">本主題將說明兩種程序。</span><span class="sxs-lookup"><span data-stu-id="efeb8-114">This topic outlines two procedures.</span></span>

1. <span data-ttu-id="efeb8-115">第一種程序描述如何使用提供接收其他活動之卸除區的 <xref:System.Activities.Presentation.WorkflowItemPresenter> 建立自訂活動設計工具。</span><span class="sxs-lookup"><span data-stu-id="efeb8-115">The first procedure describes how to create a custom activity designer with a <xref:System.Activities.Presentation.WorkflowItemPresenter> that provides the drop zone that receives other activities.</span></span> <span data-ttu-id="efeb8-116">此程式是以[自訂複合設計工具-工作流程專案展示者](./samples/custom-composite-designers-workflow-item-presenter.md)範例為基礎。</span><span class="sxs-lookup"><span data-stu-id="efeb8-116">This procedure is based on the [Custom Composite Designers - Workflow Item Presenter](./samples/custom-composite-designers-workflow-item-presenter.md) sample.</span></span>

2. <span data-ttu-id="efeb8-117">第二種程序描述如何使用提供編輯所包含項目集合時需要之功能的 <xref:System.Activities.Presentation.WorkflowItemsPresenter> 建立自訂活動設計工具。</span><span class="sxs-lookup"><span data-stu-id="efeb8-117">The second procedure describes how to create a custom activity designer with a <xref:System.Activities.Presentation.WorkflowItemsPresenter> that provides the functionality needed to edit of a collection of contained elements.</span></span> <span data-ttu-id="efeb8-118">此程式是以[自訂複合設計工具-工作流程專案展示者](./samples/custom-composite-designers-workflow-items-presenter.md)範例為基礎。</span><span class="sxs-lookup"><span data-stu-id="efeb8-118">This procedure is based on the [Custom Composite Designers - Workflow Items Presenter](./samples/custom-composite-designers-workflow-items-presenter.md) sample.</span></span>

## <a name="to-create-a-custom-activity-designer-with-a-drop-zone-using-workflowitempresenter"></a><span data-ttu-id="efeb8-119">若要使用 WorkflowItemPresenter 建立含有卸除區的自訂活動設計工具</span><span class="sxs-lookup"><span data-stu-id="efeb8-119">To create a custom activity designer with a drop zone using WorkflowItemPresenter</span></span>

1. <span data-ttu-id="efeb8-120">啟動 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="efeb8-120">Start Visual Studio 2010.</span></span>

2. <span data-ttu-id="efeb8-121">**在 [檔案**] 功能表上，指向 [**新增**]，然後選取 [**專案**]。</span><span class="sxs-lookup"><span data-stu-id="efeb8-121">On the **File** menu, point to **New**, and then select **Project…**.</span></span>

     <span data-ttu-id="efeb8-122">此時會開啟 [新增專案]\*\*\*\* 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="efeb8-122">The **New Project** dialog box opens.</span></span>

3. <span data-ttu-id="efeb8-123">在 [**已安裝的範本**] 窗格中，從您慣用的語言類別中選取 [ **Windows** ]。</span><span class="sxs-lookup"><span data-stu-id="efeb8-123">In the **Installed Templates** pane, select **Windows** from your preferred language category.</span></span>

4. <span data-ttu-id="efeb8-124">在 [**範本**] 窗格中，選取 [ **WPF 應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="efeb8-124">In the **Templates** pane, select **WPF Application**.</span></span>

5. <span data-ttu-id="efeb8-125">在 [**名稱**] 方塊中，輸入 `UsingWorkflowItemPresenter` 。</span><span class="sxs-lookup"><span data-stu-id="efeb8-125">In the **Name** box, enter `UsingWorkflowItemPresenter`.</span></span>

6. <span data-ttu-id="efeb8-126">在 [**位置**] 方塊中，輸入您要儲存專案的目錄，或按一下 **[流覽]** 以流覽至它。</span><span class="sxs-lookup"><span data-stu-id="efeb8-126">In the **Location** box, enter the directory in which you want to save your project, or click **Browse** to navigate to it.</span></span>

7. <span data-ttu-id="efeb8-127">在 [**方案**] 方塊中，接受預設值。</span><span class="sxs-lookup"><span data-stu-id="efeb8-127">In the **Solution** box, accept the default value.</span></span>

8. <span data-ttu-id="efeb8-128">按一下 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="efeb8-128">Click **OK**.</span></span>

9. <span data-ttu-id="efeb8-129">以滑鼠右鍵按一下**方案總管**中的*mainwindows.xaml* ，在 [ **Microsoft Visual Studio** ] 對話方塊中選取 [**刪除**]，然後確認 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="efeb8-129">Right-click the *MainWindows.xaml* file in the **Solution Explorer**, select **Delete** and confirm **OK** in the **Microsoft Visual Studio** dialog box.</span></span>

10. <span data-ttu-id="efeb8-130">以滑鼠右鍵按一下**方案總管**中的 UsingWorkflowItemPresenter 專案，然後依序選取 [**加入**] 和 [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="efeb8-130">Right-click the UsingWorkflowItemPresenter project in **Solution Explorer**, select **Add**, then **New Item…**</span></span> <span data-ttu-id="efeb8-131">以顯示 [**新增專案**] 對話方塊，然後從左側的 [**已安裝的範本**] 區段中選取 [ **WPF** ] 分類。</span><span class="sxs-lookup"><span data-stu-id="efeb8-131">to bring up the **Add New Item** dialog and select the **WPF** category from the **Installed Templates** section on the left.</span></span>

11. <span data-ttu-id="efeb8-132">選取**視窗（WPF）** 範本，將它命名為 `RehostingWFDesigner` ，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="efeb8-132">Select the  **Window (WPF)** template, name it `RehostingWFDesigner`, and click **Add**.</span></span>

12. <span data-ttu-id="efeb8-133">開啟*rehostingwfdesigner.xaml* ，並將下列程式碼貼入其中，以定義應用程式的 UI：</span><span class="sxs-lookup"><span data-stu-id="efeb8-133">Open the *RehostingWFDesigner.xaml* file and paste the following code into it to define the UI for the application:</span></span>

    ```xaml
    <Window x:Class=" UsingWorkflowItemPresenter.RehostingWFDesigner"
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
            xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
            xmlns:sapt="clr-namespace:System.Activities.Presentation.Toolbox;assembly=System.Activities.Presentation"
            xmlns:sys="clr-namespace:System;assembly=mscorlib"
            Title="Window1" Height="600" Width="900">
        <Window.Resources>
            <sys:String x:Key="AssemblyName">System.Activities, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35</sys:String>
        </Window.Resources>
        <Grid>
            <Grid.ColumnDefinitions>
                <ColumnDefinition Width="2*"/>
                <ColumnDefinition Width="7*"/>
                <ColumnDefinition Width="3*"/>
            </Grid.ColumnDefinitions>
            <Border Grid.Column="0">
                <sapt:ToolboxControl Name="Toolbox">
                    <sapt:ToolboxCategory CategoryName="Basic">
                        <sapt:ToolboxItemWrapper AssemblyName="{StaticResource AssemblyName}" >
                            <sapt:ToolboxItemWrapper.ToolName>
                                System.Activities.Statements.Sequence
                            </sapt:ToolboxItemWrapper.ToolName>
                           </sapt:ToolboxItemWrapper>
                        <sapt:ToolboxItemWrapper  AssemblyName="{StaticResource AssemblyName}">
                            <sapt:ToolboxItemWrapper.ToolName>
                                System.Activities.Statements.WriteLine
                            </sapt:ToolboxItemWrapper.ToolName>

                        </sapt:ToolboxItemWrapper>
                        <sapt:ToolboxItemWrapper  AssemblyName="{StaticResource AssemblyName}">
                            <sapt:ToolboxItemWrapper.ToolName>
                                System.Activities.Statements.If
                            </sapt:ToolboxItemWrapper.ToolName>

                        </sapt:ToolboxItemWrapper>
                        <sapt:ToolboxItemWrapper  AssemblyName="{StaticResource AssemblyName}">
                            <sapt:ToolboxItemWrapper.ToolName>
                                System.Activities.Statements.While
                            </sapt:ToolboxItemWrapper.ToolName>

                        </sapt:ToolboxItemWrapper>
                    </sapt:ToolboxCategory>
                </sapt:ToolboxControl>
            </Border>
            <Border Grid.Column="1" Name="DesignerBorder"/>
            <Border Grid.Column="2" Name="PropertyBorder"/>
        </Grid>
    </Window>
    ```

13. <span data-ttu-id="efeb8-134">若要關聯活動設計工具與活動型別，您必須在中繼資料存放區中註冊該活動設計工具。</span><span class="sxs-lookup"><span data-stu-id="efeb8-134">To associate an activity designer with an activity type, you must register that activity designer with the metadata store.</span></span> <span data-ttu-id="efeb8-135">若要執行這項操作，請將 `RegisterMetadata` 方法加入至 `RehostingWFDesigner` 類別。</span><span class="sxs-lookup"><span data-stu-id="efeb8-135">To do this, add the `RegisterMetadata` method to the `RehostingWFDesigner` class.</span></span> <span data-ttu-id="efeb8-136">在 `RegisterMetadata` 方法的範圍內，建立 <xref:System.Activities.Presentation.Metadata.AttributeTableBuilder> 物件，然後呼叫 <xref:System.Activities.Presentation.Metadata.AttributeTableBuilder.AddCustomAttributes%2A> 方法以便加入屬性。</span><span class="sxs-lookup"><span data-stu-id="efeb8-136">Within the scope of the  `RegisterMetadata` method, create an <xref:System.Activities.Presentation.Metadata.AttributeTableBuilder> object and call the <xref:System.Activities.Presentation.Metadata.AttributeTableBuilder.AddCustomAttributes%2A> method to add the attributes to it.</span></span> <span data-ttu-id="efeb8-137">呼叫 <xref:System.Activities.Presentation.Metadata.MetadataStore.AddAttributeTable%2A> 方法，將 <xref:System.Activities.Presentation.Metadata.AttributeTable> 加入至中繼資料存放區。</span><span class="sxs-lookup"><span data-stu-id="efeb8-137">Call the <xref:System.Activities.Presentation.Metadata.MetadataStore.AddAttributeTable%2A> method to add the <xref:System.Activities.Presentation.Metadata.AttributeTable> to the metadata store.</span></span> <span data-ttu-id="efeb8-138">下列程式碼包含設計工具的重新裝載邏輯。</span><span class="sxs-lookup"><span data-stu-id="efeb8-138">The following code contains the rehosting logic for the designer.</span></span> <span data-ttu-id="efeb8-139">它會註冊中繼資料，將 `SimpleNativeActivity` 放入工具箱，然後建立工作流程。</span><span class="sxs-lookup"><span data-stu-id="efeb8-139">It registers the metadata, puts the `SimpleNativeActivity` into the toolbox, and creates the workflow.</span></span> <span data-ttu-id="efeb8-140">將此程式碼放入*RehostingWFDesigner.xaml.cs*檔案中。</span><span class="sxs-lookup"><span data-stu-id="efeb8-140">Put this code into the *RehostingWFDesigner.xaml.cs* file.</span></span>

    ```csharp
    using System;
    using System.Activities.Core.Presentation;
    using System.Activities.Presentation;
    using System.Activities.Presentation.Metadata;
    using System.Activities.Presentation.Toolbox;
    using System.Activities.Statements;
    using System.ComponentModel;
    using System.Windows;

    namespace UsingWorkflowItemPresenter
    {
        // Interaction logic for RehostingWFDesigner.xaml
        public partial class RehostingWFDesigner
        {
            public RehostingWFDesigner()
            {
                InitializeComponent();
            }

            protected override void OnInitialized(EventArgs e)
            {
                base.OnInitialized(e);
                // Register metadata.
                (new DesignerMetadata()).Register();
                RegisterCustomMetadata();
                // Add custom activity to toolbox.
                Toolbox.Categories.Add(new ToolboxCategory("Custom activities"));
                Toolbox.Categories[1].Add(new ToolboxItemWrapper(typeof(SimpleNativeActivity)));

                // Create the workflow designer.
                var wd = new WorkflowDesigner();
                wd.Load(new Sequence());
                DesignerBorder.Child = wd.View;
                PropertyBorder.Child = wd.PropertyInspectorView;

            }

            void RegisterCustomMetadata()
            {
                var builder = new AttributeTableBuilder();
                builder.AddCustomAttributes(typeof(SimpleNativeActivity), new DesignerAttribute(typeof(SimpleNativeDesigner)));
                MetadataStore.AddAttributeTable(builder.CreateTable());
            }
        }
    }
    ```

14. <span data-ttu-id="efeb8-141">以滑鼠右鍵按一下方案總管中的 [參考] 目錄，然後選取 [**新增參考 ...** ]。</span><span class="sxs-lookup"><span data-stu-id="efeb8-141">Right-click the References directory in Solution Explorer and select **Add Reference …**</span></span> <span data-ttu-id="efeb8-142">以顯示 [**加入參考**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="efeb8-142">to bring up the **Add Reference** dialog.</span></span>

15. <span data-ttu-id="efeb8-143">按一下 [ **.net** ] 索引標籤，找出名為 [System.string **. Presentation**] 的元件，選取它並按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="efeb8-143">Click the **.NET** tab, locate the assembly named **System.Activities.Core.Presentation**, select it and click **OK**.</span></span>

16. <span data-ttu-id="efeb8-144">使用相同的程序將參考加入至下列組件：</span><span class="sxs-lookup"><span data-stu-id="efeb8-144">Using the same procedure, add references to the following assemblies:</span></span>

    1. <span data-ttu-id="efeb8-145">System.Data.DataSetExtensions.dll</span><span class="sxs-lookup"><span data-stu-id="efeb8-145">System.Data.DataSetExtensions.dll</span></span>

    2. <span data-ttu-id="efeb8-146">System.Activities.Presentation.dll</span><span class="sxs-lookup"><span data-stu-id="efeb8-146">System.Activities.Presentation.dll</span></span>

    3. <span data-ttu-id="efeb8-147">System.ServiceModel.Activities.dll</span><span class="sxs-lookup"><span data-stu-id="efeb8-147">System.ServiceModel.Activities.dll</span></span>

17. <span data-ttu-id="efeb8-148">開啟*app.xaml*檔案，然後將 StartUpUri 的值變更為 "rehostingwfdesigner.xaml"。</span><span class="sxs-lookup"><span data-stu-id="efeb8-148">Open the *App.xaml* file and change the value of the StartUpUri to "RehostingWFDesigner.xaml".</span></span>

18. <span data-ttu-id="efeb8-149">以滑鼠右鍵按一下**方案總管**中的 UsingWorkflowItemPresenter 專案，然後依序選取 [**加入**] 和 [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="efeb8-149">Right-click the UsingWorkflowItemPresenter project in **Solution Explorer**, select **Add**, then **New Item…**</span></span> <span data-ttu-id="efeb8-150">若要顯示 [**新增專案**] 對話方塊，並選取左側的 [**已安裝的範本**] 區段中的 [**工作流程**] 類別。</span><span class="sxs-lookup"><span data-stu-id="efeb8-150">to bring up the **Add New Item** dialog and select the **Workflow** category form the **Installed Templates** section on the left.</span></span>

19. <span data-ttu-id="efeb8-151">選取 [**活動設計**工具] 範本，將它命名為 `SimpleNativeDesigner` ，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="efeb8-151">Select the **Activity Designer** template, name it `SimpleNativeDesigner`, and click **Add**.</span></span>

20. <span data-ttu-id="efeb8-152">開啟*SimpleNativeDesigner* ，並將下列程式碼貼入其中。</span><span class="sxs-lookup"><span data-stu-id="efeb8-152">Open the *SimpleNativeDesigner.xaml* file and paste the following code into it.</span></span> <span data-ttu-id="efeb8-153">請注意，這個程式碼會使用 <xref:System.Activities.Presentation.ActivityDesigner> 做為根項目，並且示範如何使用繫結將 <xref:System.Activities.Presentation.WorkflowItemPresenter> 整合至設計工具中，以便在複合活動設計工具中顯示子型別。</span><span class="sxs-lookup"><span data-stu-id="efeb8-153">Note this code uses <xref:System.Activities.Presentation.ActivityDesigner> as your root element and shows how binding is used to integrate <xref:System.Activities.Presentation.WorkflowItemPresenter> into your designer so a child type can be displayed in your composite activity designer.</span></span>

    > [!NOTE]
    > <span data-ttu-id="efeb8-154"><xref:System.Activities.Presentation.ActivityDesigner> 的結構描述允許只將一個子項目加入自訂活動設計工具定義中，不過，這個項目可以是 `StackPanel`、`Grid`，也可以是其他複合 UI 項目。</span><span class="sxs-lookup"><span data-stu-id="efeb8-154">The schema for <xref:System.Activities.Presentation.ActivityDesigner> allows the addition of only one child element to your custom activity designer definition; however, this element could be a `StackPanel`, `Grid`, or some other composite UI element.</span></span>

    ```xaml
    <sap:ActivityDesigner x:Class=" UsingWorkflowItemPresenter.SimpleNativeDesigner"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:sap="clr-namespace:System.Activities.Presentation;assembly=System.Activities.Presentation"
        xmlns:sapv="clr-namespace:System.Activities.Presentation.View;assembly=System.Activities.Presentation">
        <sap:ActivityDesigner.Resources>
            <DataTemplate x:Key="Collapsed">
                <StackPanel>
                    <TextBlock>This is the collapsed view</TextBlock>
                </StackPanel>
            </DataTemplate>
            <DataTemplate x:Key="Expanded">
                <StackPanel>
                    <TextBlock>Custom Text</TextBlock>
                    <sap:WorkflowItemPresenter Item="{Binding Path=ModelItem.Body, Mode=TwoWay}"
                                            HintText="Please drop an activity here" />
                </StackPanel>
            </DataTemplate>
            <Style x:Key="ExpandOrCollapsedStyle" TargetType="{x:Type ContentPresenter}">
                <Setter Property="ContentTemplate" Value="{DynamicResource Collapsed}"/>
                <Style.Triggers>
                    <DataTrigger Binding="{Binding Path=ShowExpanded}" Value="true">
                        <Setter Property="ContentTemplate" Value="{DynamicResource Expanded}"/>
                    </DataTrigger>
                </Style.Triggers>
            </Style>
        </sap:ActivityDesigner.Resources>
        <Grid>
            <ContentPresenter Style="{DynamicResource ExpandOrCollapsedStyle}" Content="{Binding}" />
        </Grid>
    </sap:ActivityDesigner>
    ```

21. <span data-ttu-id="efeb8-155">以滑鼠右鍵按一下**方案總管**中的 UsingWorkflowItemPresenter 專案，然後依序選取 [**加入**] 和 [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="efeb8-155">Right-click the UsingWorkflowItemPresenter project in **Solution Explorer**, select **Add**, then **New Item…**</span></span> <span data-ttu-id="efeb8-156">若要顯示 [**新增專案**] 對話方塊，並選取左側的 [**已安裝的範本**] 區段中的 [**工作流程**] 類別。</span><span class="sxs-lookup"><span data-stu-id="efeb8-156">to bring up the **Add New Item** dialog and select the **Workflow** category form the **Installed Templates** section on the left.</span></span>

22. <span data-ttu-id="efeb8-157">選取 [ **Code] 活動**範本，將它命名為 `SimpleNativeActivity` ，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="efeb8-157">Select the  **Code Activity** template, name it `SimpleNativeActivity`, and click **Add**.</span></span>

23. <span data-ttu-id="efeb8-158">在 `SimpleNativeActivity` *SimpleNativeActivity.cs*檔案中輸入下列程式碼，以執行類別：</span><span class="sxs-lookup"><span data-stu-id="efeb8-158">Implement the `SimpleNativeActivity` class by entering the following code into the *SimpleNativeActivity.cs* file:</span></span>

    ```csharp
    using System.Activities;

    namespace UsingWorkflowItemPresenter
    {
        public sealed class SimpleNativeActivity : NativeActivity
        {
            // this property contains an activity that will be scheduled in the execute method
            // the WorkflowItemPresenter in the designer is bound to this to enable editing
            // of the value
            public Activity Body { get; set; }

            protected override void CacheMetadata(NativeActivityMetadata metadata)
            {
               metadata.AddChild(Body);
               base.CacheMetadata(metadata);

            }

            protected override void Execute(NativeActivityContext context)
            {
                context.ScheduleActivity(Body);
            }
        }
    }
    ```

24. <span data-ttu-id="efeb8-159">從 [**建立**] 功能表中選取 [**建立方案**]。</span><span class="sxs-lookup"><span data-stu-id="efeb8-159">Select **Build Solution** from the **Build** menu.</span></span>

25. <span data-ttu-id="efeb8-160">從 [**調試**] 功能表中選取 [**啟動但不進行調試**]，以開啟 [重新裝載自訂設計] 視窗。</span><span class="sxs-lookup"><span data-stu-id="efeb8-160">Select **Start Without Debugging** from the **Debug** menu to open the rehosted custom design window.</span></span>

### <a name="to-create-a-custom-activity-designer-using-workflowitemspresenter"></a><span data-ttu-id="efeb8-161">若要使用 WorkflowItemsPresenter 建立自訂活動設計工具</span><span class="sxs-lookup"><span data-stu-id="efeb8-161">To create a custom activity designer using WorkflowItemsPresenter</span></span>

1. <span data-ttu-id="efeb8-162">第二個自訂活動設計工具的程式是第一個只有一些修改，第一個則是為第二個應用程式命名 `UsingWorkflowItemsPresenter` 。</span><span class="sxs-lookup"><span data-stu-id="efeb8-162">The procedure for the second custom activity designer is the parallels the first with a few modifications, the first of which is to name the second application `UsingWorkflowItemsPresenter`.</span></span> <span data-ttu-id="efeb8-163">此外，這個應用程式不會定義新的自訂活動。</span><span class="sxs-lookup"><span data-stu-id="efeb8-163">Also this application does not define a new custom activity.</span></span>

2. <span data-ttu-id="efeb8-164">主要差異包含在*CustomParallelDesigner*和*RehostingWFDesigner.xaml.cs*檔案中。</span><span class="sxs-lookup"><span data-stu-id="efeb8-164">Key differences are contained in the *CustomParallelDesigner.xaml* and *RehostingWFDesigner.xaml.cs* files.</span></span> <span data-ttu-id="efeb8-165">以下是*CustomParallelDesigner*檔案中定義 UI 的程式碼：</span><span class="sxs-lookup"><span data-stu-id="efeb8-165">Here is the code from the *CustomParallelDesigner.xaml* file that defines the UI:</span></span>

    ```xaml
    <sap:ActivityDesigner x:Class=" UsingWorkflowItemsPresenter.CustomParallelDesigner"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:sap="clr-namespace:System.Activities.Presentation;assembly=System.Activities.Presentation"
        xmlns:sapv="clr-namespace:System.Activities.Presentation.View;assembly=System.Activities.Presentation">
        <sap:ActivityDesigner.Resources>
            <DataTemplate x:Key="Collapsed">
                <TextBlock>This is the Collapsed View</TextBlock>
            </DataTemplate>
            <DataTemplate x:Key="Expanded">
                <StackPanel>
                    <TextBlock HorizontalAlignment="Center">This is the</TextBlock>
                    <TextBlock HorizontalAlignment="Center">extended view</TextBlock>
                    <sap:WorkflowItemsPresenter HintText="Drop Activities Here"
                                        Items="{Binding Path=ModelItem.Branches}">
                        <sap:WorkflowItemsPresenter.SpacerTemplate>
                            <DataTemplate>
                                <Ellipse Width="10" Height="10" Fill="Black"/>
                            </DataTemplate>
                        </sap:WorkflowItemsPresenter.SpacerTemplate>
                        <sap:WorkflowItemsPresenter.ItemsPanel>
                            <ItemsPanelTemplate>
                                <StackPanel Orientation="Horizontal"/>
                            </ItemsPanelTemplate>
                        </sap:WorkflowItemsPresenter.ItemsPanel>
                    </sap:WorkflowItemsPresenter>
                </StackPanel>
            </DataTemplate>
            <Style x:Key="ExpandOrCollapsedStyle" TargetType="{x:Type ContentPresenter}">
                <Setter Property="ContentTemplate" Value="{DynamicResource Collapsed}"/>
                <Style.Triggers>
                    <DataTrigger Binding="{Binding Path=ShowExpanded}" Value="true">
                        <Setter Property="ContentTemplate" Value="{DynamicResource Expanded}"/>
                    </DataTrigger>
                </Style.Triggers>
            </Style>
        </sap:ActivityDesigner.Resources>
        <Grid>
            <ContentPresenter Style="{DynamicResource ExpandOrCollapsedStyle}" Content="{Binding}"/>
        </Grid>
    </sap:ActivityDesigner>
    ```

3. <span data-ttu-id="efeb8-166">以下是*RehostingWFDesigner.xaml.cs*檔案中提供重新裝載邏輯的程式碼：</span><span class="sxs-lookup"><span data-stu-id="efeb8-166">Here is the code from the *RehostingWFDesigner.xaml.cs* file that provides the rehosting logic:</span></span>

    ```csharp
    using System;
    using System.Activities.Core.Presentation;
    using System.Activities.Presentation;
    using System.Activities.Presentation.Metadata;
    using System.Activities.Statements;
    using System.ComponentModel;
    using System.Windows;

    namespaceUsingWorkflowItemsPresenter
    {
        public partial class RehostingWfDesigner : Window
        {
            public RehostingWfDesigner()
            {
                InitializeComponent();
            }

            protected override void OnInitialized(EventArgs e)
            {
                base.OnInitialized(e);
                // Register metadata.
                (new DesignerMetadata()).Register();
                RegisterCustomMetadata();

                // Create the workflow designer.
                var wd = new WorkflowDesigner();
                wd.Load(new Sequence());
                DesignerBorder.Child = wd.View;
                PropertyBorder.Child = wd.PropertyInspectorView;

            }

            void RegisterCustomMetadata()
            {
                var builder = new AttributeTableBuilder();
                builder.AddCustomAttributes(typeof(Parallel), new DesignerAttribute(typeof(CustomParallelDesigner)));
                MetadataStore.AddAttributeTable(builder.CreateTable());
            }
        }
    }
    ```

## <a name="see-also"></a><span data-ttu-id="efeb8-167">另請參閱</span><span class="sxs-lookup"><span data-stu-id="efeb8-167">See also</span></span>

- <xref:System.Activities.Presentation.ActivityDesigner>
- <xref:System.Activities.Presentation.WorkflowItemPresenter>
- <xref:System.Activities.Presentation.WorkflowItemsPresenter>
- <xref:System.Activities.Presentation.WorkflowViewElement>
- <xref:System.Activities.Presentation.Model.ModelItem>
- [<span data-ttu-id="efeb8-168">自訂工作流程設計體驗</span><span class="sxs-lookup"><span data-stu-id="efeb8-168">Customizing the Workflow Design Experience</span></span>](customizing-the-workflow-design-experience.md)
