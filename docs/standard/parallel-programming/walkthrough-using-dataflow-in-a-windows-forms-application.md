---
title: 逐步解說：在 Windows Forms 應用程式中使用資料流程
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- TPL dataflow library, in Windows Forms
- Task Parallel Library, dataflows
- Windows Forms, and TPL
ms.assetid: 9c65cdf7-660c-409f-89ea-59d7ec8e127c
ms.openlocfilehash: 7cd82ffde5fccf938027a6ab6ea15fef226fef6f
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288429"
---
# <a name="walkthrough-using-dataflow-in-a-windows-forms-application"></a><span data-ttu-id="86bfc-102">逐步解說：在 Windows Forms 應用程式中使用資料流程</span><span class="sxs-lookup"><span data-stu-id="86bfc-102">Walkthrough: Using Dataflow in a Windows Forms Application</span></span>
<span data-ttu-id="86bfc-103">本文鍵示範如何建立資料流程區塊網路，其可以在 Windows Forms 應用程式中執行映像處理。</span><span class="sxs-lookup"><span data-stu-id="86bfc-103">This document demonstrates how to create a network of dataflow blocks that perform image processing in a Windows Forms application.</span></span>  
  
 <span data-ttu-id="86bfc-104">這個範例會從指定的資料夾載入映像檔案、建立複合映像，以及顯示結果。</span><span class="sxs-lookup"><span data-stu-id="86bfc-104">This example loads image files from the specified folder, creates a composite image, and displays the result.</span></span> <span data-ttu-id="86bfc-105">這個範例會使用資料流程模型，透過網路路由映像。</span><span class="sxs-lookup"><span data-stu-id="86bfc-105">The example uses the dataflow model to route images through the network.</span></span> <span data-ttu-id="86bfc-106">在資料流程模型中，程式的獨立元件會透過傳送訊息，彼此進行通訊。</span><span class="sxs-lookup"><span data-stu-id="86bfc-106">In the dataflow model, independent components of a program communicate with one another by sending messages.</span></span> <span data-ttu-id="86bfc-107">當元件收到訊息時，它會執行某些動作，然後將結果傳遞給另一個元件。</span><span class="sxs-lookup"><span data-stu-id="86bfc-107">When a component receives a message, it performs some action and then passes the result to another component.</span></span> <span data-ttu-id="86bfc-108">比較資料流程模型與控制流程模型，在其中應用程式會使用控制項結構，例如，條件陳述式、迴圈等等，來控制程式中作業的順序。</span><span class="sxs-lookup"><span data-stu-id="86bfc-108">Compare this with the control flow model, in which an application uses control structures, for example, conditional statements, loops, and so on, to control the order of operations in a program.</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="86bfc-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="86bfc-109">Prerequisites</span></span>  
 <span data-ttu-id="86bfc-110">在開始進行這個逐步解說之前，請先閱讀[資料流程](dataflow-task-parallel-library.md)。</span><span class="sxs-lookup"><span data-stu-id="86bfc-110">Read [Dataflow](dataflow-task-parallel-library.md) before you start this walkthrough.</span></span>  

[!INCLUDE [tpl-install-instructions](../../../includes/tpl-install-instructions.md)]

## <a name="sections"></a><span data-ttu-id="86bfc-111">章節</span><span class="sxs-lookup"><span data-stu-id="86bfc-111">Sections</span></span>  
 <span data-ttu-id="86bfc-112">本逐步解說包含下列各節：</span><span class="sxs-lookup"><span data-stu-id="86bfc-112">This walkthrough contains the following sections:</span></span>  
  
- [<span data-ttu-id="86bfc-113">建立 Windows Forms 應用程式</span><span class="sxs-lookup"><span data-stu-id="86bfc-113">Creating the Windows Forms Application</span></span>](#winforms)  
  
- [<span data-ttu-id="86bfc-114">建立資料流程網路</span><span class="sxs-lookup"><span data-stu-id="86bfc-114">Creating the Dataflow Network</span></span>](#network)  
  
- [<span data-ttu-id="86bfc-115">連接資料流程網路與使用者介面</span><span class="sxs-lookup"><span data-stu-id="86bfc-115">Connecting the Dataflow Network to the User Interface</span></span>](#ui)  
  
- [<span data-ttu-id="86bfc-116">完整範例</span><span class="sxs-lookup"><span data-stu-id="86bfc-116">The Complete Example</span></span>](#complete)  
  
<a name="winforms"></a>
## <a name="creating-the-windows-forms-application"></a><span data-ttu-id="86bfc-117">建立 Windows Forms 應用程式</span><span class="sxs-lookup"><span data-stu-id="86bfc-117">Creating the Windows Forms Application</span></span>  
 <span data-ttu-id="86bfc-118">本節描述如何建立基本 Windows Forms 應用程式，並且將控制項新增至主要表單。</span><span class="sxs-lookup"><span data-stu-id="86bfc-118">This section describes how to create the basic Windows Forms application and add controls to the main form.</span></span>  
  
### <a name="to-create-the-windows-forms-application"></a><span data-ttu-id="86bfc-119">若要建立 Windows Forms 應用程式</span><span class="sxs-lookup"><span data-stu-id="86bfc-119">To Create the Windows Forms Application</span></span>  
  
1. <span data-ttu-id="86bfc-120">在 Visual Studio 中，建立 Visual C# 或 Visual Basic **Windows Forms 應用程式**專案。</span><span class="sxs-lookup"><span data-stu-id="86bfc-120">In Visual Studio, create a Visual C# or Visual Basic **Windows Forms Application** project.</span></span> <span data-ttu-id="86bfc-121">在本文件中，專案命名為 `CompositeImages`。</span><span class="sxs-lookup"><span data-stu-id="86bfc-121">In this document, the project is named `CompositeImages`.</span></span>  
  
2. <span data-ttu-id="86bfc-122">在主要表單 Form1.cs (在 Visual Basic 中為 Form1.vb) 的表單設計工具上，新增 <xref:System.Windows.Forms.ToolStrip> 控制項。</span><span class="sxs-lookup"><span data-stu-id="86bfc-122">On the form designer for the main form, Form1.cs (Form1.vb for Visual Basic), add a <xref:System.Windows.Forms.ToolStrip> control.</span></span>  
  
3. <span data-ttu-id="86bfc-123">將 <xref:System.Windows.Forms.ToolStripButton> 控制項加入 <xref:System.Windows.Forms.ToolStrip> 控制項。</span><span class="sxs-lookup"><span data-stu-id="86bfc-123">Add a <xref:System.Windows.Forms.ToolStripButton> control to the <xref:System.Windows.Forms.ToolStrip> control.</span></span> <span data-ttu-id="86bfc-124">將 <xref:System.Windows.Forms.ToolStripItem.DisplayStyle%2A> 屬性設為 <xref:System.Windows.Forms.ToolStripItemDisplayStyle.Text>，並將 <xref:System.Windows.Forms.ToolStripItem.Text%2A> 屬性設為 **Choose Folder**。</span><span class="sxs-lookup"><span data-stu-id="86bfc-124">Set the <xref:System.Windows.Forms.ToolStripItem.DisplayStyle%2A> property to <xref:System.Windows.Forms.ToolStripItemDisplayStyle.Text> and the <xref:System.Windows.Forms.ToolStripItem.Text%2A> property to **Choose Folder**.</span></span>  
  
4. <span data-ttu-id="86bfc-125">將第二個 <xref:System.Windows.Forms.ToolStripButton> 控制項加入 <xref:System.Windows.Forms.ToolStrip> 控制項。</span><span class="sxs-lookup"><span data-stu-id="86bfc-125">Add a second <xref:System.Windows.Forms.ToolStripButton> control to the <xref:System.Windows.Forms.ToolStrip> control.</span></span> <span data-ttu-id="86bfc-126">將 <xref:System.Windows.Forms.ToolStripItem.DisplayStyle%2A> 屬性設為 <xref:System.Windows.Forms.ToolStripItemDisplayStyle.Text>，將 <xref:System.Windows.Forms.ToolStripItem.Text%2A> 屬性設為 **Cancel**，然後將 <xref:System.Windows.Forms.ToolStripItem.Enabled%2A> 屬性設為 `False`。</span><span class="sxs-lookup"><span data-stu-id="86bfc-126">Set the <xref:System.Windows.Forms.ToolStripItem.DisplayStyle%2A> property to <xref:System.Windows.Forms.ToolStripItemDisplayStyle.Text>, the <xref:System.Windows.Forms.ToolStripItem.Text%2A> property to **Cancel**, and the <xref:System.Windows.Forms.ToolStripItem.Enabled%2A> property to `False`.</span></span>  
  
5. <span data-ttu-id="86bfc-127">將 <xref:System.Windows.Forms.PictureBox> 物件加入主要表單。</span><span class="sxs-lookup"><span data-stu-id="86bfc-127">Add a <xref:System.Windows.Forms.PictureBox> object to the main form.</span></span> <span data-ttu-id="86bfc-128">將 <xref:System.Windows.Forms.Control.Dock%2A> 屬性設為 <xref:System.Windows.Forms.DockStyle.Fill>。</span><span class="sxs-lookup"><span data-stu-id="86bfc-128">Set the <xref:System.Windows.Forms.Control.Dock%2A> property to <xref:System.Windows.Forms.DockStyle.Fill>.</span></span>  
  
<a name="network"></a>
## <a name="creating-the-dataflow-network"></a><span data-ttu-id="86bfc-129">建立資料流程網路</span><span class="sxs-lookup"><span data-stu-id="86bfc-129">Creating the Dataflow Network</span></span>  
 <span data-ttu-id="86bfc-130">本節描述如何建立會執行映像處理的資料流程網路。</span><span class="sxs-lookup"><span data-stu-id="86bfc-130">This section describes how to create the dataflow network that performs image processing.</span></span>  
  
### <a name="to-create-the-dataflow-network"></a><span data-ttu-id="86bfc-131">若要建立資料流程網路</span><span class="sxs-lookup"><span data-stu-id="86bfc-131">To Create the Dataflow Network</span></span>  
  
1. <span data-ttu-id="86bfc-132">將 System.Threading.Tasks.Dataflow.dll 參考新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="86bfc-132">Add a reference to System.Threading.Tasks.Dataflow.dll to your project.</span></span>  
  
2. <span data-ttu-id="86bfc-133">確定 Form1.cs (在 Visual Basic 中為 Form1.vb) 包含下列 `using` (在 Visual Basic 中為 `Using`) 陳述式：</span><span class="sxs-lookup"><span data-stu-id="86bfc-133">Ensure that Form1.cs (Form1.vb for Visual Basic) contains the following `using` (`Using` in Visual Basic) statements:</span></span>  
  
     [!code-csharp[TPLDataflow_CompositeImages#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_compositeimages/cs/compositeimages/form1.cs#1)]  
  
3. <span data-ttu-id="86bfc-134">將下列資料成員新增至 `Form1` 類別：</span><span class="sxs-lookup"><span data-stu-id="86bfc-134">Add the following data members to the `Form1` class:</span></span>  
  
     [!code-csharp[TPLDataflow_CompositeImages#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_compositeimages/cs/compositeimages/form1.cs#2)]  
  
4. <span data-ttu-id="86bfc-135">將下列 `CreateImageProcessingNetwork` 方法新增至 `Form1` 類別。</span><span class="sxs-lookup"><span data-stu-id="86bfc-135">Add the following method, `CreateImageProcessingNetwork`, to the `Form1` class.</span></span> <span data-ttu-id="86bfc-136">這個方法會建立映像處理網路。</span><span class="sxs-lookup"><span data-stu-id="86bfc-136">This method creates the image processing network.</span></span>  
  
     [!code-csharp[TPLDataflow_CompositeImages#3](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_compositeimages/cs/compositeimages/form1.cs#3)]  
  
5. <span data-ttu-id="86bfc-137">實作 `LoadBitmaps` 方法。</span><span class="sxs-lookup"><span data-stu-id="86bfc-137">Implement the `LoadBitmaps` method.</span></span>  
  
     [!code-csharp[TPLDataflow_CompositeImages#4](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_compositeimages/cs/compositeimages/form1.cs#4)]  
  
6. <span data-ttu-id="86bfc-138">實作 `CreateCompositeBitmap` 方法。</span><span class="sxs-lookup"><span data-stu-id="86bfc-138">Implement the `CreateCompositeBitmap` method.</span></span>  
  
     [!code-csharp[TPLDataflow_CompositeImages#5](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_compositeimages/cs/compositeimages/form1.cs#5)]  
  
    > [!NOTE]
    > <span data-ttu-id="86bfc-139">C# 版本的 `CreateCompositeBitmap` 方法會使用指標，以便有效處理 <xref:System.Drawing.Bitmap?displayProperty=nameWithType> 物件。</span><span class="sxs-lookup"><span data-stu-id="86bfc-139">The C# version of the `CreateCompositeBitmap` method uses pointers to enable efficient processing of the <xref:System.Drawing.Bitmap?displayProperty=nameWithType> objects.</span></span> <span data-ttu-id="86bfc-140">因此，您必須在專案中啟用 [容許 Unsafe 程式碼]\*\*\*\* 選項，以便使用 [unsafe](../../csharp/language-reference/keywords/unsafe.md) 關鍵字。</span><span class="sxs-lookup"><span data-stu-id="86bfc-140">Therefore, you must enable the **Allow unsafe code** option in your project in order to use the [unsafe](../../csharp/language-reference/keywords/unsafe.md) keyword.</span></span> <span data-ttu-id="86bfc-141">如需如何在 Visual C# 專案中啟用不安全程式碼的詳細資訊，請參閱[專案設計工具、建置頁 (C#)](/visualstudio/ide/reference/build-page-project-designer-csharp)。</span><span class="sxs-lookup"><span data-stu-id="86bfc-141">For more information about how to enable unsafe code in a Visual C# project, see [Build Page, Project Designer (C#)](/visualstudio/ide/reference/build-page-project-designer-csharp).</span></span>  
  
 <span data-ttu-id="86bfc-142">下表描述網路的成員。</span><span class="sxs-lookup"><span data-stu-id="86bfc-142">The following table describes the members of the network.</span></span>  
  
|<span data-ttu-id="86bfc-143">成員</span><span class="sxs-lookup"><span data-stu-id="86bfc-143">Member</span></span>|<span data-ttu-id="86bfc-144">類型</span><span class="sxs-lookup"><span data-stu-id="86bfc-144">Type</span></span>|<span data-ttu-id="86bfc-145">描述</span><span class="sxs-lookup"><span data-stu-id="86bfc-145">Description</span></span>|  
|------------|----------|-----------------|  
|`loadBitmaps`|<xref:System.Threading.Tasks.Dataflow.TransformBlock%602>|<span data-ttu-id="86bfc-146">採用資料夾路徑做為輸入，並且產生 <xref:System.Drawing.Bitmap> 物件的集合作為輸出。</span><span class="sxs-lookup"><span data-stu-id="86bfc-146">Takes a folder path as input and produces a collection of <xref:System.Drawing.Bitmap> objects as output.</span></span>|  
|`createCompositeBitmap`|<xref:System.Threading.Tasks.Dataflow.TransformBlock%602>|<span data-ttu-id="86bfc-147">採用 <xref:System.Drawing.Bitmap> 物件的集合做為輸入，並且產生複合點陣圖做為輸出。</span><span class="sxs-lookup"><span data-stu-id="86bfc-147">Takes a collection of <xref:System.Drawing.Bitmap> objects as input and produces a composite bitmap as output.</span></span>|  
|`displayCompositeBitmap`|<xref:System.Threading.Tasks.Dataflow.ActionBlock%601>|<span data-ttu-id="86bfc-148">在表單上顯示複合點陣圖。</span><span class="sxs-lookup"><span data-stu-id="86bfc-148">Displays the composite bitmap on the form.</span></span>|  
|`operationCancelled`|<xref:System.Threading.Tasks.Dataflow.ActionBlock%601>|<span data-ttu-id="86bfc-149">顯示映像以表示作業已取消，讓使用者選取另一個資料夾。</span><span class="sxs-lookup"><span data-stu-id="86bfc-149">Displays an image to indicate that the operation is canceled and enables the user to select another folder.</span></span>|  
  
 <span data-ttu-id="86bfc-150">為了連線資料流程區塊以形成網路，此範例會使用 <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601.LinkTo%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="86bfc-150">To connect the dataflow blocks to form a network, this example uses the <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601.LinkTo%2A> method.</span></span> <span data-ttu-id="86bfc-151"><xref:System.Threading.Tasks.Dataflow.ISourceBlock%601.LinkTo%2A> 方法包含採用 <xref:System.Predicate%601> 物件的多載版本，該物件會判斷目標區塊是否接受或拒絕訊息。</span><span class="sxs-lookup"><span data-stu-id="86bfc-151">The <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601.LinkTo%2A> method contains an overloaded version that takes a <xref:System.Predicate%601> object that determines whether the target block accepts or rejects a message.</span></span> <span data-ttu-id="86bfc-152">這個篩選機制可讓訊息區塊僅接收特定的值。</span><span class="sxs-lookup"><span data-stu-id="86bfc-152">This filtering mechanism enables message blocks to receive only certain values.</span></span> <span data-ttu-id="86bfc-153">在此範例中，網路可以使用兩種方式之一進行分支。</span><span class="sxs-lookup"><span data-stu-id="86bfc-153">In this example, the network can branch in one of two ways.</span></span> <span data-ttu-id="86bfc-154">主要分支會從磁碟載入映像、建立複合映像，以及在表單上顯示該映像。</span><span class="sxs-lookup"><span data-stu-id="86bfc-154">The main branch loads the images from disk, creates the composite image, and displays that image on the form.</span></span> <span data-ttu-id="86bfc-155">替代分支會取消目前的作業。</span><span class="sxs-lookup"><span data-stu-id="86bfc-155">The alternate branch cancels the current operation.</span></span> <span data-ttu-id="86bfc-156"><xref:System.Predicate%601> 物件會啟用主要分支上的資料流程區塊，以藉由拒絕特定訊息來切換至替代分支。</span><span class="sxs-lookup"><span data-stu-id="86bfc-156">The <xref:System.Predicate%601> objects enable the dataflow blocks along the main branch to switch to the alternative branch by rejecting certain messages.</span></span> <span data-ttu-id="86bfc-157">例如，如果使用者取消作業，資料流程區塊 `createCompositeBitmap` 會產生 `null` (在 Visual Basic 中為 `Nothing`) 作為其輸出。</span><span class="sxs-lookup"><span data-stu-id="86bfc-157">For example, if the user cancels the operation, the dataflow block `createCompositeBitmap` produces `null` (`Nothing` in Visual Basic) as its output.</span></span> <span data-ttu-id="86bfc-158">資料流程區塊 `displayCompositeBitmap` 會拒絕 `null` 輸入值，因此，訊息會提供給 `operationCancelled`。</span><span class="sxs-lookup"><span data-stu-id="86bfc-158">The dataflow block `displayCompositeBitmap` rejects `null` input values, and therefore, the message is offered to `operationCancelled`.</span></span> <span data-ttu-id="86bfc-159">資料流程區塊 `operationCancelled` 接受所有訊息，因此，會顯示映像表示作業取消。</span><span class="sxs-lookup"><span data-stu-id="86bfc-159">The dataflow block `operationCancelled` accepts all messages and therefore, displays an image to indicate that the operation is canceled.</span></span>  
  
 <span data-ttu-id="86bfc-160">下圖顯示影像處理網路：</span><span class="sxs-lookup"><span data-stu-id="86bfc-160">The following illustration shows the image processing network:</span></span>  
  
 ![顯示影像處理網路的圖例。](./media/walkthrough-using-dataflow-in-a-windows-forms-application/dataflow-winforms-image-processing.png)  
  
 <span data-ttu-id="86bfc-162">由於 `displayCompositeBitmap` 和 `operationCancelled`資料流程區塊會在使用者介面上進行處理，因此這個動作一定要在使用者介面執行緒上發生。</span><span class="sxs-lookup"><span data-stu-id="86bfc-162">Because the `displayCompositeBitmap` and `operationCancelled` dataflow blocks act on the user interface, it is important that these actions occur on the user-interface thread.</span></span> <span data-ttu-id="86bfc-163">為了要完成這項作業，這些物件在建構時會提供 <xref:System.Threading.Tasks.Dataflow.ExecutionDataflowBlockOptions> 物件，而且其 <xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.TaskScheduler%2A> 屬性會設定為 <xref:System.Threading.Tasks.TaskScheduler.FromCurrentSynchronizationContext%2A?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="86bfc-163">To accomplish this, during construction, these objects each provide a <xref:System.Threading.Tasks.Dataflow.ExecutionDataflowBlockOptions> object that has the <xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.TaskScheduler%2A> property set to <xref:System.Threading.Tasks.TaskScheduler.FromCurrentSynchronizationContext%2A?displayProperty=nameWithType>.</span></span> <span data-ttu-id="86bfc-164"><xref:System.Threading.Tasks.TaskScheduler.FromCurrentSynchronizationContext%2A?displayProperty=nameWithType> 方法會建立 <xref:System.Threading.Tasks.TaskScheduler> 物件，該物件會在目前的同步處理內容上執行工作。</span><span class="sxs-lookup"><span data-stu-id="86bfc-164">The <xref:System.Threading.Tasks.TaskScheduler.FromCurrentSynchronizationContext%2A?displayProperty=nameWithType> method creates a <xref:System.Threading.Tasks.TaskScheduler> object that performs work on the current synchronization context.</span></span> <span data-ttu-id="86bfc-165">因為 `CreateImageProcessingNetwork` 方法是從 [選擇資料夾]\*\*\*\* 按鈕的處理常式呼叫，它會在使用者介面執行緒上執行，`displayCompositeBitmap` 和 `operationCancelled` 資料流程區塊的動作也會在使用者介面執行緒上執行。</span><span class="sxs-lookup"><span data-stu-id="86bfc-165">Because the `CreateImageProcessingNetwork` method is called from the handler of the **Choose Folder** button, which runs on the user-interface thread, the actions for the `displayCompositeBitmap` and `operationCancelled` dataflow blocks also run on the user-interface thread.</span></span>  
  
 <span data-ttu-id="86bfc-166">此範例使用共用取消權杖，而非設定 <xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.CancellationToken%2A> 屬性，因為 <xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.CancellationToken%2A> 屬性會永久取消資料流程區塊的執行。</span><span class="sxs-lookup"><span data-stu-id="86bfc-166">This example uses a shared cancellation token instead of setting the <xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.CancellationToken%2A> property because the <xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.CancellationToken%2A> property permanently cancels dataflow block execution.</span></span> <span data-ttu-id="86bfc-167">取消語彙基元可讓此範例重複使用相同的資料流程網路多次，即使使用者取消一或多個作業。</span><span class="sxs-lookup"><span data-stu-id="86bfc-167">A cancellation token enables this example to reuse the same dataflow network multiple times, even when the user cancels one or more operations.</span></span> <span data-ttu-id="86bfc-168">如需使用 <xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.CancellationToken%2A> 以永久取消資料流程區塊執行的範例，請參閱[如何：取消資料流程區塊](how-to-cancel-a-dataflow-block.md)。</span><span class="sxs-lookup"><span data-stu-id="86bfc-168">For an example that uses <xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.CancellationToken%2A> to permanently cancel the execution of a dataflow block, see [How to: Cancel a Dataflow Block](how-to-cancel-a-dataflow-block.md).</span></span>  
  
<a name="ui"></a>
## <a name="connecting-the-dataflow-network-to-the-user-interface"></a><span data-ttu-id="86bfc-169">連接資料流程網路與使用者介面</span><span class="sxs-lookup"><span data-stu-id="86bfc-169">Connecting the Dataflow Network to the User Interface</span></span>  
 <span data-ttu-id="86bfc-170">本節描述如何連接資料流程網路與使用者介面。</span><span class="sxs-lookup"><span data-stu-id="86bfc-170">This section describes how to connect the dataflow network to the user interface.</span></span> <span data-ttu-id="86bfc-171">建立複合映像和取消作業是從 [選擇資料夾]\*\*\*\* 和 [取消]\*\*\*\* 按鈕起始。</span><span class="sxs-lookup"><span data-stu-id="86bfc-171">The creation of the composite image and cancellation of the operation are initiated from the **Choose Folder** and **Cancel** buttons.</span></span> <span data-ttu-id="86bfc-172">當使用者選擇任一個按鈕時，會以非同步方式起始適當的動作。</span><span class="sxs-lookup"><span data-stu-id="86bfc-172">When the user chooses either of these buttons, the appropriate action is initiated in an asynchronous manner.</span></span>  
  
### <a name="to-connect-the-dataflow-network-to-the-user-interface"></a><span data-ttu-id="86bfc-173">若要連接資料流程網路與使用者介面</span><span class="sxs-lookup"><span data-stu-id="86bfc-173">To Connect the Dataflow Network to the User Interface</span></span>  
  
1. <span data-ttu-id="86bfc-174">在主要表單的表單設計工具上，為 **Choose Folder** 按鈕的 <xref:System.Windows.Forms.ToolStripItem.Click> 事件建立事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="86bfc-174">On the form designer for the main form, create an event handler for the <xref:System.Windows.Forms.ToolStripItem.Click> event for the **Choose Folder** button.</span></span>  
  
2. <span data-ttu-id="86bfc-175">實作 **Choose Folder** 按鈕的 <xref:System.Windows.Forms.ToolStripItem.Click> 事件。</span><span class="sxs-lookup"><span data-stu-id="86bfc-175">Implement the <xref:System.Windows.Forms.ToolStripItem.Click> event for the **Choose Folder** button.</span></span>  
  
     [!code-csharp[TPLDataflow_CompositeImages#6](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_compositeimages/cs/compositeimages/form1.cs#6)]  
  
3. <span data-ttu-id="86bfc-176">在主要表單的表單設計工具上，為 **Cancel** 按鈕的 <xref:System.Windows.Forms.ToolStripItem.Click> 事件建立事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="86bfc-176">On the form designer for the main form, create an event handler for the <xref:System.Windows.Forms.ToolStripItem.Click> event for the **Cancel** button.</span></span>  
  
4. <span data-ttu-id="86bfc-177">實作 **Cancel** 按鈕的 <xref:System.Windows.Forms.ToolStripItem.Click> 事件。</span><span class="sxs-lookup"><span data-stu-id="86bfc-177">Implement the <xref:System.Windows.Forms.ToolStripItem.Click> event for the **Cancel** button.</span></span>  
  
     [!code-csharp[TPLDataflow_CompositeImages#7](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_compositeimages/cs/compositeimages/form1.cs#7)]  
  
<a name="complete"></a>
## <a name="the-complete-example"></a><span data-ttu-id="86bfc-178">完整範例</span><span class="sxs-lookup"><span data-stu-id="86bfc-178">The Complete Example</span></span>  
 <span data-ttu-id="86bfc-179">下列範例將示範本逐步解說的完整程式碼。</span><span class="sxs-lookup"><span data-stu-id="86bfc-179">The following example shows the complete code for this walkthrough.</span></span>  
  
 [!code-csharp[TPLDataflow_CompositeImages#100](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_compositeimages/cs/compositeimages/form1.cs#100)]  
  
 <span data-ttu-id="86bfc-180">下圖顯示通用 \Sample Pictures\ 資料夾的一般輸出。</span><span class="sxs-lookup"><span data-stu-id="86bfc-180">The following illustration shows typical output for the common \Sample Pictures\ folder.</span></span>  
  
 <span data-ttu-id="86bfc-181">![Windows Form 應用程式](media/tpldataflow-compositeimages.gif "TPLDataflow_CompositeImages")</span><span class="sxs-lookup"><span data-stu-id="86bfc-181">![The Windows Forms Application](media/tpldataflow-compositeimages.gif "TPLDataflow_CompositeImages")</span></span>  

## <a name="see-also"></a><span data-ttu-id="86bfc-182">另請參閱</span><span class="sxs-lookup"><span data-stu-id="86bfc-182">See also</span></span>

- [<span data-ttu-id="86bfc-183">資料流程</span><span class="sxs-lookup"><span data-stu-id="86bfc-183">Dataflow</span></span>](dataflow-task-parallel-library.md)
