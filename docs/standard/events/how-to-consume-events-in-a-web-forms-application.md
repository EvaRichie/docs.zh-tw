---
title: 如何：使用 Web Form 應用程式中的事件
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- events [.NET Framework], Web Forms
- Web Forms controls, and events
- event handlers [.NET Framework], Web Forms
- events [.NET Framework], consuming
- Web Forms, event handling
ms.assetid: 73bf8638-c4ec-4069-b0bb-a1dc79b92e32
ms.openlocfilehash: 3490b6fb89bfe6d7ac778078f58381bb5172e2fe
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288481"
---
# <a name="how-to-consume-events-in-a-web-forms-application"></a><span data-ttu-id="21d32-102">如何：使用 Web Form 應用程式中的事件</span><span class="sxs-lookup"><span data-stu-id="21d32-102">How to: Consume Events in a Web Forms Application</span></span>
<span data-ttu-id="21d32-103">ASP.NET Web Form 應用程式中的常見使用情況是使用控制項填入網頁，然後根據使用者所按的控制項，執行特定動作。</span><span class="sxs-lookup"><span data-stu-id="21d32-103">A common scenario in ASP.NET Web Forms applications is to populate a webpage with controls, and then perform a specific action based on which control the user clicks.</span></span> <span data-ttu-id="21d32-104">例如，當使用者在網頁中按一下 <xref:System.Web.UI.WebControls.Button?displayProperty=nameWithType> 控制項時，控制項就會引發事件。</span><span class="sxs-lookup"><span data-stu-id="21d32-104">For example, a <xref:System.Web.UI.WebControls.Button?displayProperty=nameWithType> control raises an event when the user clicks it in the webpage.</span></span> <span data-ttu-id="21d32-105">藉由處理事件，您的應用程式可以針對按一下按鈕執行適當的應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="21d32-105">By handling the event, your application can perform the appropriate application logic for that button click.</span></span>  
  
### <a name="to-handle-a-button-click-event-on-a-webpage"></a><span data-ttu-id="21d32-106">若要處理網頁上按鈕的 Click 事件</span><span class="sxs-lookup"><span data-stu-id="21d32-106">To handle a button click event on a webpage</span></span>  
  
1. <span data-ttu-id="21d32-107">建立具有 <xref:System.Web.UI.WebControls.Button> 控制項的 ASP.NET Web Form 網頁 (網頁)，其中 `OnClick` 值設定為您將在下一個步驟中定義的方法名稱。</span><span class="sxs-lookup"><span data-stu-id="21d32-107">Create a ASP.NET Web Forms page (webpage) that has a <xref:System.Web.UI.WebControls.Button> control with the `OnClick` value set to the name of method that you will define in the next step.</span></span>  
  
    ```xml  
    <asp:Button ID="Button1" runat="server" Text="Click Me" OnClick="Button1_Click" />  
    ```  
  
2. <span data-ttu-id="21d32-108">定義比對 <xref:System.Web.UI.WebControls.Button.Click> 事件委派簽章且採用您為 `OnClick` 值所定義名稱的事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="21d32-108">Define an event handler that matches the <xref:System.Web.UI.WebControls.Button.Click> event delegate signature and that has the name you defined for the `OnClick` value.</span></span>  
  
    ```csharp  
    protected void Button1_Click(object sender, EventArgs e)  
    {  
        // perform action  
    }  
    ```  
  
    ```vb  
    Protected Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click  
        ' perform action  
    End Sub  
    ```  
  
     <span data-ttu-id="21d32-109"><xref:System.Web.UI.WebControls.Button.Click> 事件針對 <xref:System.EventHandler> 使用委派類型，並針對事件資料使用 <xref:System.EventArgs> 類別。</span><span class="sxs-lookup"><span data-stu-id="21d32-109">The <xref:System.Web.UI.WebControls.Button.Click> event uses the <xref:System.EventHandler> class for the delegate type and the <xref:System.EventArgs> class for the event data.</span></span> <span data-ttu-id="21d32-110">ASP.NET 網頁架構會自動產生程式碼，該程式碼會建立<xref:System.EventHandler> 執行個體，並將這個委派執行個體加入至 <xref:System.Web.UI.WebControls.Button.Click> 介面的 <xref:System.Web.UI.WebControls.Button> 事件。</span><span class="sxs-lookup"><span data-stu-id="21d32-110">The ASP.NET page framework automatically generates code that creates an instance of <xref:System.EventHandler> and adds this delegate instance to the <xref:System.Web.UI.WebControls.Button.Click> event of the <xref:System.Web.UI.WebControls.Button> instance.</span></span>  
  
3. <span data-ttu-id="21d32-111">在步驟 2 中定義的事件處理常式方法中加入程式碼，在事件發生時執行所需的任何動作。</span><span class="sxs-lookup"><span data-stu-id="21d32-111">In the event handler method that you defined in step 2, add code to perform any actions that are required when the event occurs.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="21d32-112">另請參閱</span><span class="sxs-lookup"><span data-stu-id="21d32-112">See also</span></span>

- [<span data-ttu-id="21d32-113">事件</span><span class="sxs-lookup"><span data-stu-id="21d32-113">Events</span></span>](index.md)
