---
title: 如何：在 Windows 應用程式中提供說明
ms.date: 03/30/2017
helpviewer_keywords:
- Help [Windows Forms], Windows applications
- HTML Help [Windows Forms], Windows Forms
- Windows applications [Windows Forms], providing Help
- HelpProvider component [Windows Forms]
- forms [Windows Forms], providing Help
ms.assetid: 7c4e5cec-2bd2-4f0b-8d75-c2b88929bd61
ms.openlocfilehash: 405de333ce936a864047e827e60f56a930059e26
ms.sourcegitcommit: ee5b798427f81237a3c23d1fd81fff7fdc21e8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/28/2020
ms.locfileid: "84143587"
---
# <a name="how-to-provide-help-in-a-windows-application"></a><span data-ttu-id="f3023-102">如何：在 Windows 應用程式中提供說明</span><span class="sxs-lookup"><span data-stu-id="f3023-102">How to: Provide Help in a Windows Application</span></span>

<span data-ttu-id="f3023-103">您可以利用元件，將說明檔 <xref:System.Windows.Forms.HelpProvider> 中的說明主題附加至 Windows Forms 上的特定控制項。</span><span class="sxs-lookup"><span data-stu-id="f3023-103">You can make use of the <xref:System.Windows.Forms.HelpProvider> component to attach Help topics within a Help file to specific controls on Windows Forms.</span></span> <span data-ttu-id="f3023-104">說明檔可以是 HTML 或 HTMLHelp 1.x 或更高的格式。</span><span class="sxs-lookup"><span data-stu-id="f3023-104">The Help file can be either HTML or HTMLHelp 1.x or greater format.</span></span>

## <a name="provide-help"></a><span data-ttu-id="f3023-105">提供協助</span><span class="sxs-lookup"><span data-stu-id="f3023-105">Provide Help</span></span>

1. <span data-ttu-id="f3023-106">在 Visual Studio 中，將元件從 [**工具箱**] 拖曳 <xref:System.Windows.Forms.HelpProvider> 至您的表單。</span><span class="sxs-lookup"><span data-stu-id="f3023-106">In Visual Studio, from the **Toolbox**, drag a <xref:System.Windows.Forms.HelpProvider> component to your form.</span></span>

     <span data-ttu-id="f3023-107">此元件將位在 Windows Forms 設計工具底部的系統匣中。</span><span class="sxs-lookup"><span data-stu-id="f3023-107">The component will reside in the tray at the bottom of the Windows Forms Designer.</span></span>

2. <span data-ttu-id="f3023-108">在 [**屬性**] 視窗中，將 <xref:System.Windows.Forms.HelpProvider.HelpNamespace%2A> 屬性設定為 .chm、col 或 .htm 說明檔。</span><span class="sxs-lookup"><span data-stu-id="f3023-108">In the **Properties** window, set the <xref:System.Windows.Forms.HelpProvider.HelpNamespace%2A> property to the .chm, .col, or .htm Help file.</span></span>

3. <span data-ttu-id="f3023-109">選取您在表單上擁有的另一個控制項，然後在 [**屬性**] 視窗中設定 <xref:System.Windows.Forms.HelpProvider.SetHelpKeyword%2A> 屬性。</span><span class="sxs-lookup"><span data-stu-id="f3023-109">Select another control you have on your form, and in the **Properties** window, set the <xref:System.Windows.Forms.HelpProvider.SetHelpKeyword%2A> property.</span></span>

     <span data-ttu-id="f3023-110">這是透過元件傳遞至說明檔的字串， <xref:System.Windows.Forms.HelpProvider> 以啟動適當的說明主題。</span><span class="sxs-lookup"><span data-stu-id="f3023-110">This is the string passed through the <xref:System.Windows.Forms.HelpProvider> component to your Help file to summon the appropriate Help topic.</span></span>

4. <span data-ttu-id="f3023-111">在 [**屬性**] 視窗中，將 <xref:System.Windows.Forms.HelpProvider.SetHelpNavigator%2A> 屬性設定為列舉的 <xref:System.Windows.Forms.HelpNavigator> 值。</span><span class="sxs-lookup"><span data-stu-id="f3023-111">In the **Properties** window, set the <xref:System.Windows.Forms.HelpProvider.SetHelpNavigator%2A> property to a value of the <xref:System.Windows.Forms.HelpNavigator> enumeration.</span></span>

     <span data-ttu-id="f3023-112">這會決定將 **HelpKeyword** 屬性傳遞給說明系統的方式。</span><span class="sxs-lookup"><span data-stu-id="f3023-112">This determines the way in which the **HelpKeyword** property is passed to the Help system.</span></span> <span data-ttu-id="f3023-113">下表顯示可能的設定和其描述。</span><span class="sxs-lookup"><span data-stu-id="f3023-113">The following table shows the possible settings and their descriptions.</span></span>

    |<span data-ttu-id="f3023-114">成員名稱</span><span class="sxs-lookup"><span data-stu-id="f3023-114">Member Name</span></span>|<span data-ttu-id="f3023-115">描述</span><span class="sxs-lookup"><span data-stu-id="f3023-115">Description</span></span>|
    |-----------------|-----------------|
    |<span data-ttu-id="f3023-116">AssociateIndex</span><span class="sxs-lookup"><span data-stu-id="f3023-116">AssociateIndex</span></span>|<span data-ttu-id="f3023-117">指定在指定的 URL 中執行所指定主題的索引。</span><span class="sxs-lookup"><span data-stu-id="f3023-117">Specifies that the index for a specified topic is performed in the specified URL.</span></span>|
    |<span data-ttu-id="f3023-118">Find</span><span class="sxs-lookup"><span data-stu-id="f3023-118">Find</span></span>|<span data-ttu-id="f3023-119">指定顯示所指定 URL 的搜尋頁面。</span><span class="sxs-lookup"><span data-stu-id="f3023-119">Specifies that the search page of a specified URL is displayed.</span></span>|
    |<span data-ttu-id="f3023-120">索引</span><span class="sxs-lookup"><span data-stu-id="f3023-120">Index</span></span>|<span data-ttu-id="f3023-121">指定顯示所指定 URL 的索引。</span><span class="sxs-lookup"><span data-stu-id="f3023-121">Specifies that the index of a specified URL is displayed.</span></span>|
    |<span data-ttu-id="f3023-122">KeywordIndex</span><span class="sxs-lookup"><span data-stu-id="f3023-122">KeywordIndex</span></span>|<span data-ttu-id="f3023-123">指定要搜尋的關鍵字以及要在指定的 URL 中採取的動作。</span><span class="sxs-lookup"><span data-stu-id="f3023-123">Specifies a keyword to search for and the action to take in the specified URL.</span></span>|
    |<span data-ttu-id="f3023-124">TableOfContents</span><span class="sxs-lookup"><span data-stu-id="f3023-124">TableOfContents</span></span>|<span data-ttu-id="f3023-125">指定顯示 HTML 1.0 說明檔的目錄。</span><span class="sxs-lookup"><span data-stu-id="f3023-125">Specifies that the table of contents of the HTML 1.0 Help file is displayed.</span></span>|
    |<span data-ttu-id="f3023-126">主題</span><span class="sxs-lookup"><span data-stu-id="f3023-126">Topic</span></span>|<span data-ttu-id="f3023-127">指定顯示指定之 URL 所參考的主題。</span><span class="sxs-lookup"><span data-stu-id="f3023-127">Specifies that the topic referenced by the specified URL is displayed.</span></span>|

 <span data-ttu-id="f3023-128">在執行時間，當控制項（已設定 [ **HelpKeyword** ] 和 [ **HelpNavigator** ] 屬性）上按下 F1 時，焦點會開啟您與該元件相關聯的說明檔 <xref:System.Windows.Forms.HelpProvider> 。</span><span class="sxs-lookup"><span data-stu-id="f3023-128">At run time, pressing F1 when the control—for which you have set the **HelpKeyword** and **HelpNavigator** properties—has focus will open the Help file you associated with that <xref:System.Windows.Forms.HelpProvider> component.</span></span>

 <span data-ttu-id="f3023-129">目前，**HelpNamespace** 屬性支援下列三種格式的說明檔：HTMLHelp 1.x、HTMLHelp 2.0 和 HTML。</span><span class="sxs-lookup"><span data-stu-id="f3023-129">Currently, the **HelpNamespace** property supports Help files in the following three formats: HTMLHelp 1.x, HTMLHelp 2.0, and HTML.</span></span> <span data-ttu-id="f3023-130">因此，您可以將**HelpNamespace**屬性設定為 `http://` 位址，例如網頁。</span><span class="sxs-lookup"><span data-stu-id="f3023-130">Thus, you can set the **HelpNamespace** property to an `http://` address, such as a Web page.</span></span> <span data-ttu-id="f3023-131">如果這麼做，則會開啟將 **HelpKeyword** 屬性中所指定的字串用作錨點之網頁的預設瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="f3023-131">If this is done, it will open the default browser to the Web page with the string specified in the **HelpKeyword** property used as the anchor.</span></span> <span data-ttu-id="f3023-132">錨點是用來跳到 HTML 網頁的特定組件。</span><span class="sxs-lookup"><span data-stu-id="f3023-132">The anchor is used to jump to a specific part of an HTML page.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f3023-133">請先仔細檢查用戶端所傳送的任何資訊，再將它用於應用程式中。</span><span class="sxs-lookup"><span data-stu-id="f3023-133">Be careful to check any information that is sent from a client before using it in your application.</span></span> <span data-ttu-id="f3023-134">惡意使用者可能會嘗試傳送或插入可執行的指令碼、SQL 陳述式或其他程式碼。</span><span class="sxs-lookup"><span data-stu-id="f3023-134">Malicious users might try to send or inject executable script, SQL statements, or other code.</span></span> <span data-ttu-id="f3023-135">在顯示使用者的輸入、將它儲存在資料庫中，或使用它之前，請先檢查它未包含可能不安全的資訊。</span><span class="sxs-lookup"><span data-stu-id="f3023-135">Before you display a user's input, store it in a database, or work with it, check that it does not contain potentially unsafe information.</span></span> <span data-ttu-id="f3023-136">一般檢查方式是在您收到來自使用者的輸入時，使用規則運算式來尋找關鍵字，例如 "SCRIPT"。</span><span class="sxs-lookup"><span data-stu-id="f3023-136">A typical way to check is to use a regular expression to look for keywords such as "SCRIPT" when you receive input from a user.</span></span>

<span data-ttu-id="f3023-137">您也可以使用 <xref:System.Windows.Forms.HelpProvider> 元件來顯示快顯說明，即使您已將它設定為顯示 Windows Forms 上控制項的說明檔。</span><span class="sxs-lookup"><span data-stu-id="f3023-137">You can also use the <xref:System.Windows.Forms.HelpProvider> component to show pop-up Help, even if you have it configured to display Help files for the controls on your Windows Forms.</span></span> <span data-ttu-id="f3023-138">如需詳細資訊，請參閱[如何：顯示快顯說明](how-to-display-pop-up-help.md)。</span><span class="sxs-lookup"><span data-stu-id="f3023-138">For more information, see [How to: Display Pop-up Help](how-to-display-pop-up-help.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="f3023-139">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f3023-139">See also</span></span>

- [<span data-ttu-id="f3023-140">如何：顯示快顯說明</span><span class="sxs-lookup"><span data-stu-id="f3023-140">How to: Display Pop-up Help</span></span>](how-to-display-pop-up-help.md)
- [<span data-ttu-id="f3023-141">使用工具提示來顯示控制項說明</span><span class="sxs-lookup"><span data-stu-id="f3023-141">Control Help Using ToolTips</span></span>](control-help-using-tooltips.md)
- [<span data-ttu-id="f3023-142">整合 Windows Forms 中的使用者說明</span><span class="sxs-lookup"><span data-stu-id="f3023-142">Integrating User Help in Windows Forms</span></span>](integrating-user-help-in-windows-forms.md)
- [<span data-ttu-id="f3023-143">Windows Forms</span><span class="sxs-lookup"><span data-stu-id="f3023-143">Windows Forms</span></span>](../index.md)
