---
title: 將網頁瀏覽器功能新增至應用程式
description: 瞭解如何使用 WebBrowser 控制項將 web 瀏覽器功能新增至 Windows Forms 應用程式。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- WebBrowser control [Windows Forms], adding Web browser capabilities to your application
- WebBrowser control [Windows Forms], examples
- Web browsers [.NET Framework], adding to Windows Forms
- examples [Windows Forms], WebBrowser control
- Windows Forms, adding Web browser functionality
ms.assetid: 3871f072-b57a-435b-9976-e5da28df04a7
ms.openlocfilehash: a5a33961ac8301bda86bb5f34e65ac159308987f
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/09/2020
ms.locfileid: "86174545"
---
# <a name="how-to-add-web-browser-capabilities-to-a-windows-forms-application"></a><span data-ttu-id="4a69d-103">如何將 web 瀏覽器功能新增至 Windows Forms 應用程式</span><span class="sxs-lookup"><span data-stu-id="4a69d-103">How to add web browser capabilities to a Windows Forms application</span></span>

<span data-ttu-id="4a69d-104">利用 <xref:System.Windows.Forms.WebBrowser> 控制項，您可以將 Web 瀏覽器功能加入應用程式。</span><span class="sxs-lookup"><span data-stu-id="4a69d-104">With the <xref:System.Windows.Forms.WebBrowser> control, you can add Web browser functionality to your application.</span></span> <span data-ttu-id="4a69d-105">根據預設，此控制項的作用類似 Web 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="4a69d-105">The control works like a Web browser by default.</span></span> <span data-ttu-id="4a69d-106">設定 <xref:System.Windows.Forms.WebBrowser.Url%2A> 屬性來載入初始 URL 之後，您可以按一下超連結或使用鍵盤快速鍵來巡覽，在巡覽歷程記錄中前後移動。</span><span class="sxs-lookup"><span data-stu-id="4a69d-106">After you load an initial URL by setting the <xref:System.Windows.Forms.WebBrowser.Url%2A> property, you can navigate by clicking hyperlinks or by using keyboard shortcuts to move backward and forward through navigation history.</span></span> <span data-ttu-id="4a69d-107">根據預設，您可以透過滑鼠右鍵捷徑功能表來存取其他瀏覽器功能。</span><span class="sxs-lookup"><span data-stu-id="4a69d-107">By default, you can access additional browser functionality through the right-click shortcut menu.</span></span> <span data-ttu-id="4a69d-108">您也可以將新文件拖曳至控制項加以開啟。</span><span class="sxs-lookup"><span data-stu-id="4a69d-108">You can also open new documents by dropping them onto the control.</span></span> <span data-ttu-id="4a69d-109"><xref:System.Windows.Forms.WebBrowser> 控制項也有數個屬性、方法和事件，可讓您用來實作類似 Internet Explorer 中的使用者介面功能。</span><span class="sxs-lookup"><span data-stu-id="4a69d-109">The <xref:System.Windows.Forms.WebBrowser> control also has several properties, methods, and events that you can use to implement user interface features similar to those found in Internet Explorer.</span></span>

<span data-ttu-id="4a69d-110">下列程式碼範例會實作網址列、一般瀏覽器按鈕、[檔案]\*\*\*\* 功能表、狀態列，以及可顯示目前頁面標題的標題列。</span><span class="sxs-lookup"><span data-stu-id="4a69d-110">The following code example implements an address bar, typical browser buttons, a **File** menu, a status bar, and a title bar that displays the current page title.</span></span>

## <a name="example"></a><span data-ttu-id="4a69d-111">範例</span><span class="sxs-lookup"><span data-stu-id="4a69d-111">Example</span></span>

[!code-cpp[System.Windows.Forms.WebBrowser#0](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser/CPP/form1.cpp#0)]
[!code-csharp[System.Windows.Forms.WebBrowser#0](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser/CS/form1.cs#0)]
[!code-vb[System.Windows.Forms.WebBrowser#0](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser/VB/form1.vb#0)]
  
## <a name="compile-the-code"></a><span data-ttu-id="4a69d-112">編譯程式碼</span><span class="sxs-lookup"><span data-stu-id="4a69d-112">Compile the code</span></span>

<span data-ttu-id="4a69d-113">這個範例需要：</span><span class="sxs-lookup"><span data-stu-id="4a69d-113">This example requires:</span></span>

- <span data-ttu-id="4a69d-114">`System`、`System.Drawing` 和 `System.Windows.Forms` 組件的參考。</span><span class="sxs-lookup"><span data-stu-id="4a69d-114">References to the `System`, `System.Drawing`, and `System.Windows.Forms` assemblies.</span></span>

## <a name="see-also"></a><span data-ttu-id="4a69d-115">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4a69d-115">See also</span></span>

- <xref:System.Windows.Forms.WebBrowser>
- [<span data-ttu-id="4a69d-116">WebBrowser 控制項</span><span class="sxs-lookup"><span data-stu-id="4a69d-116">WebBrowser Control</span></span>](webbrowser-control-windows-forms.md)
