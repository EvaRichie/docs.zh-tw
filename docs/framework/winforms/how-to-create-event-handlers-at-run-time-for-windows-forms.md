---
title: 如何：在執行時間建立事件處理常式
description: 瞭解如何在執行時間使用 Visual Studio 中的 Windows Form 設計工具來建立事件處理常式。 這個動作可讓您在執行時間連接事件處理常式。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Windows Forms, event handling
- event handlers [Windows Forms], creating
- run time [Windows Forms], creating event handlers at
- examples [Windows Forms], event handling
- Button control [Windows Forms], event handlers
ms.assetid: 2e7c9e1a-61fe-444d-8113-3c5bacf1c8cb
ms.openlocfilehash: 857076c46377b3276154d9b193d4bbe51841828f
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/24/2020
ms.locfileid: "85325805"
---
# <a name="how-to-create-event-handlers-at-run-time-for-windows-forms"></a><span data-ttu-id="b2eae-104">作法：在執行階段建立 Windows Forms 的事件處理常式</span><span class="sxs-lookup"><span data-stu-id="b2eae-104">How to: Create Event Handlers at Run Time for Windows Forms</span></span>

<span data-ttu-id="b2eae-105">除了使用 Visual Studio 中的 Windows Form 設計工具來建立事件以外，您也可以在執行時間建立事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="b2eae-105">In addition to creating events using the Windows Forms Designer in Visual Studio, you can also create an event handler at run time.</span></span> <span data-ttu-id="b2eae-106">這個動作可讓您在執行階段根據程式碼中的條件來連接事件處理常式，而不需要程式一開始啟動時進行連接。</span><span class="sxs-lookup"><span data-stu-id="b2eae-106">This action allows you to connect event handlers based on conditions in code at run time as opposed to having them connected when the program initially starts.</span></span>

## <a name="create-an-event-handler-at-run-time"></a><span data-ttu-id="b2eae-107">在執行時間建立事件處理常式</span><span class="sxs-lookup"><span data-stu-id="b2eae-107">Create an event handler at run time</span></span>

1. <span data-ttu-id="b2eae-108">開啟您想要加入事件處理常式的表單。</span><span class="sxs-lookup"><span data-stu-id="b2eae-108">Open the form that you want to add an event handler to.</span></span>

2. <span data-ttu-id="b2eae-109">使用您要處理之事件的方法簽章，將方法新增至您的表單。</span><span class="sxs-lookup"><span data-stu-id="b2eae-109">Add a method to your form with the method signature for the event that you want to handle.</span></span>

     <span data-ttu-id="b2eae-110">例如，如果您正在處理控制項的 <xref:System.Windows.Forms.Control.Click> 事件 <xref:System.Windows.Forms.Button> ，您會建立如下的方法：</span><span class="sxs-lookup"><span data-stu-id="b2eae-110">For example, if you were handling the <xref:System.Windows.Forms.Control.Click> event of a <xref:System.Windows.Forms.Button> control, you would create a method such as the following:</span></span>

    ```vb
    Private Sub Button1_Click(ByVal sender As Object, ByVal e As EventArgs)
       ' Add event handler code here.
    End Sub
    ```

    ```csharp
    private void button1_Click(object sender, System.EventArgs e)
    {
    // Add event handler code here.
    }
    ```

    ```cpp
    private:
       void button1_Click(System::Object ^ sender,
          System::EventArgs ^ e)
       {
          // Add event handler code here.
       }
    ```

3. <span data-ttu-id="b2eae-111">將程式碼新增至您的應用程式的適當事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="b2eae-111">Add code to the event handler as appropriate to your application.</span></span>

4. <span data-ttu-id="b2eae-112">決定您要為其建立事件處理常式的表單或控制項。</span><span class="sxs-lookup"><span data-stu-id="b2eae-112">Determine which form or control you want to create an event handler for.</span></span>

5. <span data-ttu-id="b2eae-113">在您表單類別內的方法中，新增程式碼以指定要處理事件的事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="b2eae-113">In a method within your form's class, add code that specifies the event handler to handle the event.</span></span> <span data-ttu-id="b2eae-114">例如，下列程式碼會指定事件處理常式 `button1_Click` 處理 <xref:System.Windows.Forms.Control.Click> 控制項的事件 <xref:System.Windows.Forms.Button> ：</span><span class="sxs-lookup"><span data-stu-id="b2eae-114">For example, the following code specifies the event handler `button1_Click` handles the <xref:System.Windows.Forms.Control.Click> event of a <xref:System.Windows.Forms.Button> control:</span></span>

    ```vb
    AddHandler Button1.Click, AddressOf Button1_Click
    ```

    ```csharp
    button1.Click += new EventHandler(button1_Click);
    ```

    ```cpp
    button1->Click += gcnew System::EventHandler(this, &Form1::button1_Click);
    ```

     <span data-ttu-id="b2eae-115"><xref:System.ComponentModel.EventHandlerList.AddHandler%2A>上述 Visual Basic 程式碼中所示範的方法會建立按鈕的 click 事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="b2eae-115">The <xref:System.ComponentModel.EventHandlerList.AddHandler%2A> method demonstrated in the Visual Basic code above establishes a click event handler for the button.</span></span>

## <a name="see-also"></a><span data-ttu-id="b2eae-116">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b2eae-116">See also</span></span>

- [<span data-ttu-id="b2eae-117">在 Windows Form 中建立事件處理常式</span><span class="sxs-lookup"><span data-stu-id="b2eae-117">Creating Event Handlers in Windows Forms</span></span>](creating-event-handlers-in-windows-forms.md)
- [<span data-ttu-id="b2eae-118">事件處理常式概觀</span><span class="sxs-lookup"><span data-stu-id="b2eae-118">Event Handlers Overview</span></span>](event-handlers-overview-windows-forms.md)
- [<span data-ttu-id="b2eae-119">Visual Basic 中的繼承事件處理常式疑難排解</span><span class="sxs-lookup"><span data-stu-id="b2eae-119">Troubleshooting Inherited Event Handlers in Visual Basic</span></span>](../../visual-basic/programming-guide/language-features/events/troubleshooting-inherited-event-handlers.md)
