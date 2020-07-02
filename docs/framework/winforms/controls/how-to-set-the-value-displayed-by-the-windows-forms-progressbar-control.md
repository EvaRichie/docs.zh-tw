---
title: 設定 ProgressBar 控制項顯示的值
description: 瞭解如何設定 Windows Forms ProgressBar 控制項所顯示的值。 有多種方法可供您選擇使用。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ProgressBar control [Windows Forms], setting value displayed
- progress controls [Windows Forms], setting value displayed
ms.assetid: 0e5010ad-1e9a-4271-895e-5a3d24d37a26
ms.openlocfilehash: 75fe1b416636471d797a39134f45a05c972c9d39
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85618099"
---
# <a name="how-to-set-the-value-displayed-by-the-windows-forms-progressbar-control"></a><span data-ttu-id="7ae27-104">如何：設定 Windows Form ProgressBar 控制項顯示的值</span><span class="sxs-lookup"><span data-stu-id="7ae27-104">How to: Set the Value Displayed by the Windows Forms ProgressBar Control</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7ae27-105"><xref:System.Windows.Forms.ToolStripProgressBar> 控制項會取代 <xref:System.Windows.Forms.ProgressBar> 控制項並加入其他功能，不過您也可以選擇保留 <xref:System.Windows.Forms.ProgressBar> 控制項，以提供回溯相容性及未來使用。</span><span class="sxs-lookup"><span data-stu-id="7ae27-105">The <xref:System.Windows.Forms.ToolStripProgressBar> control replaces and adds functionality to the <xref:System.Windows.Forms.ProgressBar> control; however, the <xref:System.Windows.Forms.ProgressBar> control is retained for both backward compatibility and future use, if you choose.</span></span>  
  
 <span data-ttu-id="7ae27-106">.NET Framework 提供幾種不同的方式，讓您在控制項中顯示指定的值 <xref:System.Windows.Forms.ProgressBar> 。</span><span class="sxs-lookup"><span data-stu-id="7ae27-106">The .NET Framework gives you several different ways to display a given value within the <xref:System.Windows.Forms.ProgressBar> control.</span></span> <span data-ttu-id="7ae27-107">您選擇的方法取決於手邊的工作或您要解決的問題。</span><span class="sxs-lookup"><span data-stu-id="7ae27-107">Which approach you choose will depend on the task at hand or the problem you are solving.</span></span> <span data-ttu-id="7ae27-108">下表顯示您可以選擇的方法。</span><span class="sxs-lookup"><span data-stu-id="7ae27-108">The following table shows the approaches you can choose.</span></span>  
  
|<span data-ttu-id="7ae27-109">方法</span><span class="sxs-lookup"><span data-stu-id="7ae27-109">Approach</span></span>|<span data-ttu-id="7ae27-110">描述</span><span class="sxs-lookup"><span data-stu-id="7ae27-110">Description</span></span>|  
|--------------|-----------------|  
|<span data-ttu-id="7ae27-111">直接設定控制項的值 <xref:System.Windows.Forms.ProgressBar> 。</span><span class="sxs-lookup"><span data-stu-id="7ae27-111">Set the value of the <xref:System.Windows.Forms.ProgressBar> control directly.</span></span>|<span data-ttu-id="7ae27-112">如果您知道將牽涉到的專案總數（例如從資料來源讀取記錄），這種方法就很有用。</span><span class="sxs-lookup"><span data-stu-id="7ae27-112">This approach is useful for tasks where you know the total of the item measured that will be involved, such as reading records from a data source.</span></span> <span data-ttu-id="7ae27-113">此外，如果您只需要設定一次或兩次的值，這就是簡單的方法。</span><span class="sxs-lookup"><span data-stu-id="7ae27-113">Additionally, if you only need to set the value once or twice, this is an easy way to do it.</span></span> <span data-ttu-id="7ae27-114">最後，如果您需要減少進度列所顯示的值，請使用此程式。</span><span class="sxs-lookup"><span data-stu-id="7ae27-114">Finally, use this process if you need to decrease the value displayed by the progress bar.</span></span>|  
|<span data-ttu-id="7ae27-115"><xref:System.Windows.Forms.ProgressBar>以固定值增加顯示。</span><span class="sxs-lookup"><span data-stu-id="7ae27-115">Increase the <xref:System.Windows.Forms.ProgressBar> display by a fixed value.</span></span>|<span data-ttu-id="7ae27-116">當您要顯示介於最小值和最大值之間的簡單計數（例如已耗用時間或已從已知總計處理的檔案數目）時，這個方法很有用。</span><span class="sxs-lookup"><span data-stu-id="7ae27-116">This approach is useful when you are displaying a simple count between the minimum and maximum, such as elapsed time or the number of files that have been processed out of a known total.</span></span>|  
|<span data-ttu-id="7ae27-117">以不同的值來增加 <xref:System.Windows.Forms.ProgressBar> 顯示。</span><span class="sxs-lookup"><span data-stu-id="7ae27-117">Increase the <xref:System.Windows.Forms.ProgressBar> display by a value that varies.</span></span>|<span data-ttu-id="7ae27-118">當您需要將顯示的值變更為不同數量的次數時，這個方法很有用。</span><span class="sxs-lookup"><span data-stu-id="7ae27-118">This approach is useful when you need to change the displayed value a number of times in different amounts.</span></span> <span data-ttu-id="7ae27-119">其中一個範例會顯示將一系列檔案寫入磁片時所耗用的硬碟空間量。</span><span class="sxs-lookup"><span data-stu-id="7ae27-119">An example would be showing the amount of hard-disk space being consumed while writing a series of files to the disk.</span></span>|  
  
 <span data-ttu-id="7ae27-120">若要設定進度列所顯示的值，最直接的方式是設定 <xref:System.Windows.Forms.ProgressBar.Value%2A> 屬性。</span><span class="sxs-lookup"><span data-stu-id="7ae27-120">The most direct way to set the value displayed by a progress bar is by setting the <xref:System.Windows.Forms.ProgressBar.Value%2A> property.</span></span> <span data-ttu-id="7ae27-121">這可以在設計階段或執行時間執行。</span><span class="sxs-lookup"><span data-stu-id="7ae27-121">This can be done either at design time or at run time.</span></span>  
  
### <a name="to-set-the-progressbar-value-directly"></a><span data-ttu-id="7ae27-122">若要直接設定 ProgressBar 值</span><span class="sxs-lookup"><span data-stu-id="7ae27-122">To set the ProgressBar value directly</span></span>  
  
1. <span data-ttu-id="7ae27-123">設定 <xref:System.Windows.Forms.ProgressBar> 控制項的 <xref:System.Windows.Forms.ProgressBar.Minimum%2A> 和 <xref:System.Windows.Forms.ProgressBar.Maximum%2A> 值。</span><span class="sxs-lookup"><span data-stu-id="7ae27-123">Set the <xref:System.Windows.Forms.ProgressBar> control's <xref:System.Windows.Forms.ProgressBar.Minimum%2A> and <xref:System.Windows.Forms.ProgressBar.Maximum%2A> values.</span></span>  
  
2. <span data-ttu-id="7ae27-124">在程式碼中，將控制項的 <xref:System.Windows.Forms.ProgressBar.Value%2A> 屬性設定為您所建立之最小值和最大值之間的整數值。</span><span class="sxs-lookup"><span data-stu-id="7ae27-124">In code, set the control's <xref:System.Windows.Forms.ProgressBar.Value%2A> property to an integer value between the minimum and maximum values you have established.</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="7ae27-125">如果您將屬性設定在 <xref:System.Windows.Forms.ProgressBar.Value%2A> 和屬性所建立的界限之外，控制項就會擲回 <xref:System.Windows.Forms.ProgressBar.Minimum%2A> <xref:System.Windows.Forms.ProgressBar.Maximum%2A> 例外狀況 <xref:System.ArgumentException> 。</span><span class="sxs-lookup"><span data-stu-id="7ae27-125">If you set the <xref:System.Windows.Forms.ProgressBar.Value%2A> property outside the boundaries established by the <xref:System.Windows.Forms.ProgressBar.Minimum%2A> and <xref:System.Windows.Forms.ProgressBar.Maximum%2A> properties, the control throws an <xref:System.ArgumentException> exception.</span></span>  
  
     <span data-ttu-id="7ae27-126">下列程式碼範例說明如何 <xref:System.Windows.Forms.ProgressBar> 直接設定值。</span><span class="sxs-lookup"><span data-stu-id="7ae27-126">The following code example illustrates how to set the <xref:System.Windows.Forms.ProgressBar> value directly.</span></span> <span data-ttu-id="7ae27-127">程式碼會從資料來源讀取記錄，並在每次讀取資料記錄時更新進度列和標籤。</span><span class="sxs-lookup"><span data-stu-id="7ae27-127">The code reads records from a data source and updates the progress bar and label every time a data record is read.</span></span> <span data-ttu-id="7ae27-128">這個範例要求您的表單具有 <xref:System.Windows.Forms.Label> 控制項、 <xref:System.Windows.Forms.ProgressBar> 控制項，以及具有和欄位的資料列的資料表 `CustomerRow` `FirstName` `LastName` 。</span><span class="sxs-lookup"><span data-stu-id="7ae27-128">This example requires that your form has a <xref:System.Windows.Forms.Label> control, a <xref:System.Windows.Forms.ProgressBar> control, and a data table with a row called `CustomerRow` with `FirstName` and `LastName` fields.</span></span>  
  
    ```vb  
    Public Sub CreateNewRecords()  
       ' Sets the progress bar's Maximum property to  
       ' the total number of records to be created.  
       ProgressBar1.Maximum = 20  
  
       ' Creates a new record in the dataset.  
       ' NOTE: The code below will not compile, it merely  
       ' illustrates how the progress bar would be used.  
       Dim anyRow As CustomerRow = DatasetName.ExistingTable.NewRow  
       anyRow.FirstName = "Stephen"  
       anyRow.LastName = "James"  
       ExistingTable.Rows.Add(anyRow)  
  
       ' Increases the value displayed by the progress bar.  
       ProgressBar1.Value += 1  
       ' Updates the label to show that a record was read.  
       Label1.Text = "Records Read = " & ProgressBar1.Value.ToString()  
    End Sub  
    ```  
  
    ```csharp  
    public void createNewRecords()  
    {  
       // Sets the progress bar's Maximum property to  
       // the total number of records to be created.  
       progressBar1.Maximum = 20;  
  
       // Creates a new record in the dataset.  
       // NOTE: The code below will not compile, it merely  
       // illustrates how the progress bar would be used.  
       CustomerRow anyRow = DatasetName.ExistingTable.NewRow();  
       anyRow.FirstName = "Stephen";  
       anyRow.LastName = "James";  
       ExistingTable.Rows.Add(anyRow);  
  
       // Increases the value displayed by the progress bar.  
       progressBar1.Value += 1;  
       // Updates the label to show that a record was read.  
       label1.Text = "Records Read = " + progressBar1.Value.ToString();  
    }  
    ```  
  
     如果您要顯示以固定間隔繼續進行的進度，您可以設定值，然後呼叫方法， <xref:System.Windows.Forms.ProgressBar> 依該間隔增加控制項的值。 <span data-ttu-id="7ae27-130">這適用于不是以整體百分比測量進度的計時器和其他案例。</span><span class="sxs-lookup"><span data-stu-id="7ae27-130">This is useful for timers and other scenarios where you are not measuring progress as a percentage of the whole.</span></span>  
  
### <a name="to-increase-the-progress-bar-by-a-fixed-value"></a><span data-ttu-id="7ae27-131">以固定值增加進度列</span><span class="sxs-lookup"><span data-stu-id="7ae27-131">To increase the progress bar by a fixed value</span></span>  
  
1. <span data-ttu-id="7ae27-132">設定 <xref:System.Windows.Forms.ProgressBar> 控制項的 <xref:System.Windows.Forms.ProgressBar.Minimum%2A> 和 <xref:System.Windows.Forms.ProgressBar.Maximum%2A> 值。</span><span class="sxs-lookup"><span data-stu-id="7ae27-132">Set the <xref:System.Windows.Forms.ProgressBar> control's <xref:System.Windows.Forms.ProgressBar.Minimum%2A> and <xref:System.Windows.Forms.ProgressBar.Maximum%2A> values.</span></span>  
  
2. <span data-ttu-id="7ae27-133">將控制項的 <xref:System.Windows.Forms.ProgressBar.Step%2A> 屬性設定為整數，代表要增加進度列顯示值的數量。</span><span class="sxs-lookup"><span data-stu-id="7ae27-133">Set the control's <xref:System.Windows.Forms.ProgressBar.Step%2A> property to an integer representing the amount to increase the progress bar's displayed value.</span></span>  
  
3. <span data-ttu-id="7ae27-134">呼叫 <xref:System.Windows.Forms.ProgressBar.PerformStep%2A> 方法，以變更屬性中設定的數量所顯示的值 <xref:System.Windows.Forms.ProgressBar.Step%2A> 。</span><span class="sxs-lookup"><span data-stu-id="7ae27-134">Call the <xref:System.Windows.Forms.ProgressBar.PerformStep%2A> method to change the value displayed by the amount set in the <xref:System.Windows.Forms.ProgressBar.Step%2A> property.</span></span>  
  
     <span data-ttu-id="7ae27-135">下列程式碼範例說明進度列可以如何在複製作業中維護檔案的計數。</span><span class="sxs-lookup"><span data-stu-id="7ae27-135">The following code example illustrates how a progress bar can maintain a count of the files in a copy operation.</span></span>  
  
     <span data-ttu-id="7ae27-136">在下列範例中，當每個檔案讀入記憶體時，進度列和標籤會更新，以反映讀取的檔案總數。</span><span class="sxs-lookup"><span data-stu-id="7ae27-136">In the following example, as each file is read into memory, the progress bar and label are updated to reflect the total files read.</span></span> <span data-ttu-id="7ae27-137">此範例會要求您的表單具有 <xref:System.Windows.Forms.Label> 控制項和 <xref:System.Windows.Forms.ProgressBar> 控制項。</span><span class="sxs-lookup"><span data-stu-id="7ae27-137">This example requires that your form has a <xref:System.Windows.Forms.Label> control and a <xref:System.Windows.Forms.ProgressBar> control.</span></span>  
  
    ```vb  
    Public Sub LoadFiles()  
       ' Sets the progress bar's minimum value to a number representing  
       ' no operations complete -- in this case, no files read.  
       ProgressBar1.Minimum = 0  
       ' Sets the progress bar's maximum value to a number representing  
       ' all operations complete -- in this case, all five files read.  
       ProgressBar1.Maximum = 5  
       ' Sets the Step property to amount to increase with each iteration.  
       ' In this case, it will increase by one with every file read.  
       ProgressBar1.Step = 1  
  
       ' Dimensions a counter variable.  
       Dim i As Integer  
       ' Uses a For...Next loop to iterate through the operations to be  
       ' completed. In this case, five files are to be copied into memory,  
       ' so the loop will execute 5 times.  
       For i = 0 To 4  
          ' Insert code to copy a file  
          ProgressBar1.PerformStep()  
          ' Update the label to show that a file was read.  
          Label1.Text = "# of Files Read = " & ProgressBar1.Value.ToString  
       Next i  
    End Sub  
    ```  
  
    ```csharp  
    public void loadFiles()  
    {  
       // Sets the progress bar's minimum value to a number representing  
       // no operations complete -- in this case, no files read.  
       progressBar1.Minimum = 0;  
       // Sets the progress bar's maximum value to a number representing  
       // all operations complete -- in this case, all five files read.  
       progressBar1.Maximum = 5;  
       // Sets the Step property to amount to increase with each iteration.  
       // In this case, it will increase by one with every file read.  
       progressBar1.Step = 1;  
  
       // Uses a for loop to iterate through the operations to be  
       // completed. In this case, five files are to be copied into memory,  
       // so the loop will execute 5 times.  
       for (int i = 0; i <= 4; i++)  
       {  
          // Inserts code to copy a file  
          progressBar1.PerformStep();  
          // Updates the label to show that a file was read.  
          label1.Text = "# of Files Read = " + progressBar1.Value.ToString();  
       }  
    }  
    ```  
  
     最後，您可以增加進度列所顯示的值，讓每個增加都是唯一的金額。 <span data-ttu-id="7ae27-139">當您要追蹤一系列獨特的作業（例如將不同大小的檔案寫入硬碟），或以整體百分比測量進度時，這會很有用。</span><span class="sxs-lookup"><span data-stu-id="7ae27-139">This is useful when you are keeping track of a series of unique operations, such as writing files of different sizes to a hard disk, or measuring progress as a percentage of the whole.</span></span>  
  
### <a name="to-increase-the-progress-bar-by-a-dynamic-value"></a><span data-ttu-id="7ae27-140">以動態值增加進度列</span><span class="sxs-lookup"><span data-stu-id="7ae27-140">To increase the progress bar by a dynamic value</span></span>  
  
1. <span data-ttu-id="7ae27-141">設定 <xref:System.Windows.Forms.ProgressBar> 控制項的 <xref:System.Windows.Forms.ProgressBar.Minimum%2A> 和 <xref:System.Windows.Forms.ProgressBar.Maximum%2A> 值。</span><span class="sxs-lookup"><span data-stu-id="7ae27-141">Set the <xref:System.Windows.Forms.ProgressBar> control's <xref:System.Windows.Forms.ProgressBar.Minimum%2A> and <xref:System.Windows.Forms.ProgressBar.Maximum%2A> values.</span></span>  
  
2. <span data-ttu-id="7ae27-142">呼叫 <xref:System.Windows.Forms.ProgressBar.Increment%2A> 方法，以變更您指定的整數所顯示的值。</span><span class="sxs-lookup"><span data-stu-id="7ae27-142">Call the <xref:System.Windows.Forms.ProgressBar.Increment%2A> method to change the value displayed by an integer you specify.</span></span>  
  
     <span data-ttu-id="7ae27-143">下列程式碼範例說明在複製作業期間，進度列可以如何計算已使用的磁碟空間量。</span><span class="sxs-lookup"><span data-stu-id="7ae27-143">The following code example illustrates how a progress bar can calculate how much disk space has been used during a copy operation.</span></span>  
  
     <span data-ttu-id="7ae27-144">在下列範例中，當每個檔案寫入硬碟時，會更新進度列和標籤以反映可用的硬碟空間量。</span><span class="sxs-lookup"><span data-stu-id="7ae27-144">In the following example, as each file is written to the hard disk, the progress bar and label are updated to reflect the amount of hard-disk space available.</span></span> <span data-ttu-id="7ae27-145">此範例會要求您的表單具有 <xref:System.Windows.Forms.Label> 控制項和 <xref:System.Windows.Forms.ProgressBar> 控制項。</span><span class="sxs-lookup"><span data-stu-id="7ae27-145">This example requires that your form has a <xref:System.Windows.Forms.Label> control and a <xref:System.Windows.Forms.ProgressBar> control.</span></span>  
  
    ```vb  
    Public Sub ReadFiles()  
       ' Sets the progress bar's minimum value to a number
       ' representing the hard disk space before the files are read in.  
       ' You will most likely have to set this using a system call.  
       ' NOTE: The code below is meant to be an example and  
       ' will not compile.  
       ProgressBar1.Minimum = AvailableDiskSpace()  
       ' Sets the progress bar's maximum value to a number
       ' representing the total hard disk space.  
       ' You will most likely have to set this using a system call.  
       ' NOTE: The code below is meant to be an example
       ' and will not compile.  
       ProgressBar1.Maximum = TotalDiskSpace()  
  
       ' Dimension a counter variable.  
       Dim i As Integer  
       ' Uses a For...Next loop to iterate through the operations to be  
       ' completed. In this case, five files are to be written to the disk,  
       ' so it will execute the loop 5 times.  
       For i = 1 To 5  
          ' Insert code to read a file into memory and update file size.  
          ' Increases the progress bar's value based on the size of
          ' the file currently being written.  
          ProgressBar1.Increment(FileSize)  
          ' Updates the label to show available drive space.  
          Label1.Text = "Current Disk Space Used = " &_
          ProgressBar1.Value.ToString()  
       Next i  
    End Sub  
    ```  
  
    ```csharp  
    public void readFiles()  
    {  
       // Sets the progress bar's minimum value to a number
       // representing the hard disk space before the files are read in.  
       // You will most likely have to set this using a system call.  
       // NOTE: The code below is meant to be an example and
       // will not compile.  
       progressBar1.Minimum = AvailableDiskSpace();  
       // Sets the progress bar's maximum value to a number
       // representing the total hard disk space.  
       // You will most likely have to set this using a system call.  
       // NOTE: The code below is meant to be an example
       // and will not compile.  
       progressBar1.Maximum = TotalDiskSpace();  
  
       // Uses a for loop to iterate through the operations to be  
       // completed. In this case, five files are to be written  
       // to the disk, so it will execute the loop 5 times.  
       for (int i = 1; i<= 5; i++)  
       {  
          // Insert code to read a file into memory and update file size.  
          // Increases the progress bar's value based on the size of
          // the file currently being written.  
          progressBar1.Increment(FileSize);  
          // Updates the label to show available drive space.  
          label1.Text = "Current Disk Space Used = " + progressBar1.Value.ToString();  
       }  
    }  
    ```  
  
## <a name="see-also"></a><span data-ttu-id="7ae27-146">另請參閱</span><span class="sxs-lookup"><span data-stu-id="7ae27-146">See also</span></span>

- <xref:System.Windows.Forms.ProgressBar>
- <xref:System.Windows.Forms.ToolStripProgressBar>
- [<span data-ttu-id="7ae27-147">ProgressBar 控制項概觀</span><span class="sxs-lookup"><span data-stu-id="7ae27-147">ProgressBar Control Overview</span></span>](progressbar-control-overview-windows-forms.md)
- [<span data-ttu-id="7ae27-148">ProgressBar 控制項</span><span class="sxs-lookup"><span data-stu-id="7ae27-148">ProgressBar Control</span></span>](progressbar-control-windows-forms.md)
