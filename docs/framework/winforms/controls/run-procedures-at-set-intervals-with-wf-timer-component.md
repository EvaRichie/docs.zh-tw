---
title: 使用計時器元件以設定的間隔執行程式
description: 瞭解如何使用 Windows Form 計時器元件，以設定的間隔來執行程式，或在設定的時間間隔經過時執行。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- examples [Windows Forms], timers
- timers [Windows Forms], event intervals
- initialization [Windows Forms], Timer components
- timers [Windows Forms], Windows-based
- Timer component [Windows Forms], initializing
- procedures [Windows Forms], specific time intervals
ms.assetid: 8025247a-2de4-4d86-b8ab-a8cb8aeab2ea
ms.openlocfilehash: 6847819fcec98d01d38b8e44604a259f06be7c02
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/24/2020
ms.locfileid: "85325771"
---
# <a name="how-to-run-procedures-at-set-intervals-with-the-windows-forms-timer-component"></a><span data-ttu-id="35e48-103">如何：使用 Windows Form Timer 元件以設定的間隔執行程序</span><span class="sxs-lookup"><span data-stu-id="35e48-103">How to: Run Procedures at Set Intervals with the Windows Forms Timer Component</span></span>
<span data-ttu-id="35e48-104">您有時可能會想要建立一個程序，依特定時間間隔執行，直到迴圈完成，或是在經過設定的時間間隔之後執行。</span><span class="sxs-lookup"><span data-stu-id="35e48-104">You might sometimes want to create a procedure that runs at specific time intervals until a loop has finished or that runs when a set time interval has elapsed.</span></span> <span data-ttu-id="35e48-105"><xref:System.Windows.Forms.Timer> 元件可讓您建立這樣的程序。</span><span class="sxs-lookup"><span data-stu-id="35e48-105">The <xref:System.Windows.Forms.Timer> component makes such a procedure possible.</span></span>  
  
 <span data-ttu-id="35e48-106">這個元件是專為 Windows Form 環境所設計。</span><span class="sxs-lookup"><span data-stu-id="35e48-106">This component is designed for a Windows Forms environment.</span></span> <span data-ttu-id="35e48-107">如果您需要適用於伺服器環境的計時器，請參閱[伺服器架構的計時器簡介](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/tb9yt5e6(v=vs.90))。</span><span class="sxs-lookup"><span data-stu-id="35e48-107">If you need a timer that is suitable for a server environment, see [Introduction to Server-Based Timers](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/tb9yt5e6(v=vs.90)).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="35e48-108">使用 <xref:System.Windows.Forms.Timer> 元件時，有一些限制。</span><span class="sxs-lookup"><span data-stu-id="35e48-108">There are some limitations when using the <xref:System.Windows.Forms.Timer> component.</span></span> <span data-ttu-id="35e48-109">如需詳細資訊，請參閱[Windows Forms Timer 元件的 Interval 屬性的限制](limitations-of-the-timer-component-interval-property.md)。</span><span class="sxs-lookup"><span data-stu-id="35e48-109">For more information, see [Limitations of the Windows Forms Timer Component's Interval Property](limitations-of-the-timer-component-interval-property.md).</span></span>  
  
## <a name="to-run-a-procedure-at-set-intervals-with-the-timer-component"></a><span data-ttu-id="35e48-110">若要使用計時器元件，依設定的間隔來執行程序</span><span class="sxs-lookup"><span data-stu-id="35e48-110">To run a procedure at set intervals with the Timer component</span></span>  
  
1. <span data-ttu-id="35e48-111">加入 <xref:System.Windows.Forms.Timer> 至您的表單。</span><span class="sxs-lookup"><span data-stu-id="35e48-111">Add a <xref:System.Windows.Forms.Timer> to your form.</span></span> <span data-ttu-id="35e48-112">請參閱下面的＜範例＞一節，以取得以程式設計方式執行此動作的範例。</span><span class="sxs-lookup"><span data-stu-id="35e48-112">See the following Example section for an illustration of how to do this programmatically.</span></span> <span data-ttu-id="35e48-113">Visual Studio 也支援將元件新增至表單。</span><span class="sxs-lookup"><span data-stu-id="35e48-113">Visual Studio also has support for adding components to a form.</span></span> <span data-ttu-id="35e48-114">另請參閱[如何：將沒有使用者介面的控制項加入至 Windows Forms](how-to-add-controls-without-a-user-interface-to-windows-forms.md)。</span><span class="sxs-lookup"><span data-stu-id="35e48-114">Also see [How to: Add Controls Without a User Interface to Windows Forms](how-to-add-controls-without-a-user-interface-to-windows-forms.md).</span></span>  
  
2. <span data-ttu-id="35e48-115">設定計時器的 <xref:System.Windows.Forms.Timer.Interval%2A> 屬性 (以毫秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="35e48-115">Set the <xref:System.Windows.Forms.Timer.Interval%2A> property (in milliseconds) for the timer.</span></span> <span data-ttu-id="35e48-116">此屬性可決定，經過多少時間之後，會再執行該程序。</span><span class="sxs-lookup"><span data-stu-id="35e48-116">This property determines how much time will pass before the procedure is run again.</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="35e48-117">計時器事件發生的頻率愈高，就會用愈多的處理器時間來回應事件。</span><span class="sxs-lookup"><span data-stu-id="35e48-117">The more often a timer event occurs, the more processor time is used in responding to the event.</span></span> <span data-ttu-id="35e48-118">這會降低整體效能。</span><span class="sxs-lookup"><span data-stu-id="35e48-118">This can slow down overall performance.</span></span> <span data-ttu-id="35e48-119">請不要設定小於您所需的間隔。</span><span class="sxs-lookup"><span data-stu-id="35e48-119">Do not set a smaller interval than you need.</span></span>  
  
3. <span data-ttu-id="35e48-120">在 <xref:System.Windows.Forms.Timer.Tick> 事件處理常式中撰寫適當的程式碼。</span><span class="sxs-lookup"><span data-stu-id="35e48-120">Write appropriate code in the <xref:System.Windows.Forms.Timer.Tick> event handler.</span></span> <span data-ttu-id="35e48-121">您在這個事件中撰寫的程式碼，將會依 <xref:System.Windows.Forms.Timer.Interval%2A> 屬性中指定的間隔執行。</span><span class="sxs-lookup"><span data-stu-id="35e48-121">The code you write in this event will run at the interval specified in the <xref:System.Windows.Forms.Timer.Interval%2A> property.</span></span>  
  
4. <span data-ttu-id="35e48-122">請將 <xref:System.Windows.Forms.Timer.Enabled%2A> 屬性設為 `true`，以啟動計時器。</span><span class="sxs-lookup"><span data-stu-id="35e48-122">Set the <xref:System.Windows.Forms.Timer.Enabled%2A> property to `true` to start the timer.</span></span> <span data-ttu-id="35e48-123"><xref:System.Windows.Forms.Timer.Tick> 事件會開始發生，依所設定的間隔來執行您的程序。</span><span class="sxs-lookup"><span data-stu-id="35e48-123">The <xref:System.Windows.Forms.Timer.Tick> event will begin to occur, running your procedure at the set interval.</span></span>  
  
5. <span data-ttu-id="35e48-124">在適當的時間，將 <xref:System.Windows.Forms.Timer.Enabled%2A> 屬性設為 `false`，使程序停止再次執行。</span><span class="sxs-lookup"><span data-stu-id="35e48-124">At the appropriate time, set the <xref:System.Windows.Forms.Timer.Enabled%2A> property to `false` to stop the procedure from running again.</span></span> <span data-ttu-id="35e48-125">將間隔設定為 `0` 並不會使計時器停止。</span><span class="sxs-lookup"><span data-stu-id="35e48-125">Setting the interval to `0` does not cause the timer to stop.</span></span>  
  
## <a name="example"></a><span data-ttu-id="35e48-126">範例</span><span class="sxs-lookup"><span data-stu-id="35e48-126">Example</span></span>  
 <span data-ttu-id="35e48-127">第一個程式碼範例會追蹤一天的時間，以一秒為增量單位。</span><span class="sxs-lookup"><span data-stu-id="35e48-127">This first code example tracks the time of day in one-second increments.</span></span> <span data-ttu-id="35e48-128">它會在表單上使用 <xref:System.Windows.Forms.Button>、<xref:System.Windows.Forms.Label> 和 <xref:System.Windows.Forms.Timer> 元件。</span><span class="sxs-lookup"><span data-stu-id="35e48-128">It uses a <xref:System.Windows.Forms.Button>, a <xref:System.Windows.Forms.Label>, and a <xref:System.Windows.Forms.Timer> component on a form.</span></span> <span data-ttu-id="35e48-129"><xref:System.Windows.Forms.Timer.Interval%2A> 屬性設為 1000 (等於 1 秒)。</span><span class="sxs-lookup"><span data-stu-id="35e48-129">The <xref:System.Windows.Forms.Timer.Interval%2A> property is set to 1000 (equal to one second).</span></span> <span data-ttu-id="35e48-130">在 <xref:System.Windows.Forms.Timer.Tick> 事件中，標籤的標題設為目前的時間。</span><span class="sxs-lookup"><span data-stu-id="35e48-130">In the <xref:System.Windows.Forms.Timer.Tick> event, the label's caption is set to the current time.</span></span> <span data-ttu-id="35e48-131">按一下按鈕時，<xref:System.Windows.Forms.Timer.Enabled%2A> 屬性會設為 `false`，使計時器停止更新標籤的標題。</span><span class="sxs-lookup"><span data-stu-id="35e48-131">When the button is clicked, the <xref:System.Windows.Forms.Timer.Enabled%2A> property is set to `false`, stopping the timer from updating the label's caption.</span></span> <span data-ttu-id="35e48-132">下列程式碼範例要求您的表單具有 <xref:System.Windows.Forms.Button> 名為的控制項 `Button1` 、 <xref:System.Windows.Forms.Timer> 名為的控制項 `Timer1` ，以及 <xref:System.Windows.Forms.Label> 名為的控制項 `Label1` 。</span><span class="sxs-lookup"><span data-stu-id="35e48-132">The following code example requires that you have a form with a <xref:System.Windows.Forms.Button> control named `Button1`, a <xref:System.Windows.Forms.Timer> control named `Timer1`, and a <xref:System.Windows.Forms.Label> control named `Label1`.</span></span>  
  
```vb  
Private Sub InitializeTimer()  
   ' Run this procedure in an appropriate event.  
   ' Set to 1 second.  
   Timer1.Interval = 1000  
   ' Enable timer.  
   Timer1.Enabled = True  
   Button1.Text = "Enabled"  
End Sub  
x  
Private Sub Timer1_Tick(ByVal Sender As Object, ByVal e As EventArgs) Handles Timer1.Tick  
' Set the caption to the current time.  
   Label1.Text = DateTime.Now  
End Sub  
  
Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click  
      If Button1.Text = "Stop" Then  
         Button1.Text = "Start"  
         Timer1.Enabled = False  
      Else  
         Button1.Text = "Stop"  
         Timer1.Enabled = True  
      End If  
End Sub  
```  
  
```csharp  
private void InitializeTimer()  
{  
    // Call this procedure when the application starts.  
    // Set to 1 second.  
    Timer1.Interval = 1000;  
    Timer1.Tick += new EventHandler(Timer1_Tick);  
  
    // Enable timer.  
    Timer1.Enabled = true;  
  
    Button1.Text = "Stop";  
    Button1.Click += new EventHandler(Button1_Click);  
}  
  
private void Timer1_Tick(object Sender, EventArgs e)
{  
   // Set the caption to the current time.  
   Label1.Text = DateTime.Now.ToString();  
}  
  
private void Button1_Click(object sender, EventArgs e)  
{  
  if ( Button1.Text == "Stop" )  
  {  
    Button1.Text = "Start";  
    Timer1.Enabled = false;  
  }  
  else  
  {  
    Button1.Text = "Stop";  
    Timer1.Enabled = true;  
  }  
}  
```  
  
```cpp  
private:  
   void InitializeTimer()  
   {  
      // Run this procedure in an appropriate event.  
      // Set to 1 second.  
      timer1->Interval = 1000;  
      // Enable timer.  
      timer1->Enabled = true;  
      this->timer1->Tick += gcnew System::EventHandler(this,
                               &Form1::timer1_Tick);  
  
      button1->Text = S"Stop";  
      this->button1->Click += gcnew System::EventHandler(this,
                               &Form1::button1_Click);  
   }  
  
   void timer1_Tick(System::Object ^ sender,  
      System::EventArgs ^ e)  
   {  
      // Set the caption to the current time.  
      label1->Text = DateTime::Now.ToString();  
   }  
  
   void button1_Click(System::Object ^ sender,  
      System::EventArgs ^ e)  
   {  
      if ( button1->Text == "Stop" )  
      {  
         button1->Text = "Start";  
         timer1->Enabled = false;  
      }  
      else  
      {  
         button1->Text = "Stop";  
         timer1->Enabled = true;  
      }  
   }  
```  
  
## <a name="example"></a><span data-ttu-id="35e48-133">範例</span><span class="sxs-lookup"><span data-stu-id="35e48-133">Example</span></span>  
 <span data-ttu-id="35e48-134">這個第二個程式碼範例會每隔 600 毫秒執行一次程序，直到迴圈完成為止。</span><span class="sxs-lookup"><span data-stu-id="35e48-134">This second code example runs a procedure every 600 milliseconds until a loop has finished.</span></span> <span data-ttu-id="35e48-135">下列程式碼範例要求您的表單具有 <xref:System.Windows.Forms.Button> 名為的控制項 `Button1` 、 <xref:System.Windows.Forms.Timer> 名為的控制項 `Timer1` ，以及 <xref:System.Windows.Forms.Label> 名為的控制項 `Label1` 。</span><span class="sxs-lookup"><span data-stu-id="35e48-135">The following code example requires that you have a form with a <xref:System.Windows.Forms.Button> control named `Button1`, a <xref:System.Windows.Forms.Timer> control named `Timer1`, and a <xref:System.Windows.Forms.Label> control named `Label1`.</span></span>  
  
```vb  
' This variable will be the loop counter.  
Private counter As Integer  
  
Private Sub InitializeTimer()  
   ' Run this procedure in an appropriate event.  
   counter = 0  
   Timer1.Interval = 600  
   Timer1.Enabled = True  
End Sub  
  
Private Sub Timer1_Tick(ByVal sender As Object, ByVal e As System.EventArgs) Handles Timer1.Tick  
   If counter => 10 Then  
      ' Exit loop code.  
      Timer1.Enabled = False  
      counter = 0  
   Else  
      ' Run your procedure here.  
      ' Increment counter.  
      counter = counter + 1  
      Label1.Text = "Procedures Run: " & counter.ToString  
   End If  
End Sub  
```  
  
```csharp  
// This variable will be the loop counter.  
private int counter;  
  
private void InitializeTimer()  
{  
   // Run this procedure in an appropriate event.  
   counter = 0;  
   timer1.Interval = 600;  
   timer1.Enabled = true;  
   // Hook up timer's tick event handler.  
   this.timer1.Tick += new System.EventHandler(this.timer1_Tick);  
}  
  
private void timer1_Tick(object sender, System.EventArgs e)
{  
   if (counter >= 10)
   {  
      // Exit loop code.  
      timer1.Enabled = false;  
      counter = 0;  
   }  
   else  
   {  
      // Run your procedure here.  
      // Increment counter.  
      counter = counter + 1;  
      label1.Text = "Procedures Run: " + counter.ToString();  
      }  
}  
```  
  
```cpp  
private:  
   int counter;  
  
   void InitializeTimer()  
   {  
      // Run this procedure in an appropriate event.  
      counter = 0;  
      timer1->Interval = 600;  
      timer1->Enabled = true;  
      // Hook up timer's tick event handler.  
      this->timer1->Tick += gcnew System::EventHandler(this, &Form1::timer1_Tick);  
   }  
  
   void timer1_Tick(System::Object ^ sender,  
      System::EventArgs ^ e)  
   {  
      if (counter >= 10)
      {  
         // Exit loop code.  
         timer1->Enabled = false;  
         counter = 0;  
      }  
      else  
      {  
         // Run your procedure here.  
         // Increment counter.  
         counter = counter + 1;  
         label1->Text = String::Concat("Procedures Run: ",  
            counter.ToString());  
      }  
   }  
```  
  
## <a name="see-also"></a><span data-ttu-id="35e48-136">另請參閱</span><span class="sxs-lookup"><span data-stu-id="35e48-136">See also</span></span>

- <xref:System.Windows.Forms.Timer>
- [<span data-ttu-id="35e48-137">Timer 元件</span><span class="sxs-lookup"><span data-stu-id="35e48-137">Timer Component</span></span>](timer-component-windows-forms.md)
- [<span data-ttu-id="35e48-138">Timer 元件概觀</span><span class="sxs-lookup"><span data-stu-id="35e48-138">Timer Component Overview</span></span>](timer-component-overview-windows-forms.md)
