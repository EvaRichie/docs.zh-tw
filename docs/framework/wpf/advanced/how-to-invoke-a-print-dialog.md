---
title: 如何：叫用列印對話方塊
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- invoking print dialogs [WPF]
- print dialogs [WPF], invoking
ms.assetid: e3a2c84c-74fe-45a4-8501-5813f9dbfed2
ms.openlocfilehash: 75a4160366766efbd19d6e8ae26fbec102e7f95b
ms.sourcegitcommit: 40de8df14289e1e05b40d6e5c1daabd3c286d70c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86924496"
---
# <a name="how-to-invoke-a-print-dialog"></a><span data-ttu-id="131b3-102">如何：叫用列印對話方塊</span><span class="sxs-lookup"><span data-stu-id="131b3-102">How to: Invoke a Print Dialog</span></span>
<span data-ttu-id="131b3-103">若要提供從您的應用程式列印的功能，您可以直接建立並開啟 <xref:System.Windows.Controls.PrintDialog> 物件。</span><span class="sxs-lookup"><span data-stu-id="131b3-103">To provide the ability to print from you application, you can simply create and open a <xref:System.Windows.Controls.PrintDialog> object.</span></span>  
  
## <a name="example"></a><span data-ttu-id="131b3-104">範例</span><span class="sxs-lookup"><span data-stu-id="131b3-104">Example</span></span>  
 <span data-ttu-id="131b3-105"><xref:System.Windows.Controls.PrintDialog>控制項提供 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 、設定和 XPS 工作提交的單一進入點。</span><span class="sxs-lookup"><span data-stu-id="131b3-105">The <xref:System.Windows.Controls.PrintDialog> control provides a single entry point for [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)], configuration, and XPS job submission.</span></span> <span data-ttu-id="131b3-106">控制項很容易使用，而且可以使用標記或程式碼來具現化 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="131b3-106">The control is easy to use and can be instantiated by using [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] markup or code.</span></span> <span data-ttu-id="131b3-107">下列範例示範如何在程式碼中具現化和開啟控制項，以及如何從它進行列印。</span><span class="sxs-lookup"><span data-stu-id="131b3-107">The following example demonstrates how to instantiate and open the control in code and how to print from it.</span></span> <span data-ttu-id="131b3-108">它也會示範如何確保對話方塊會提供使用者設定特定頁面範圍的選項。</span><span class="sxs-lookup"><span data-stu-id="131b3-108">It also shows how to ensure that the dialog will give the user the option of setting a specific range of pages.</span></span> <span data-ttu-id="131b3-109">範例程式碼假設 C：磁片磁碟機的根目錄中有一個檔案 FixedDocumentSequence。</span><span class="sxs-lookup"><span data-stu-id="131b3-109">The example code assumes that there is a file FixedDocumentSequence.xps in the root of the C: drive.</span></span>  
  
 [!code-csharp[printdialog#1](~/samples/snippets/csharp/VS_Snippets_Wpf/PrintDialog/CSharp/Window1.xaml.cs#1)]
 [!code-vb[printdialog#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PrintDialog/visualbasic/window1.xaml.vb#1)]  
  
 <span data-ttu-id="131b3-110">對話方塊開啟之後，使用者就可以從安裝在其電腦上的印表機中選取。</span><span class="sxs-lookup"><span data-stu-id="131b3-110">Once the dialog is open, users will be able to select from the printers installed on their computer.</span></span> <span data-ttu-id="131b3-111">他們也可以選擇選取[MICROSOFT XPS Document Writer](/windows/win32/printdocs/microsoft-xps-document-writer)來建立 XML 檔規格（Xps）檔案，而不是列印。</span><span class="sxs-lookup"><span data-stu-id="131b3-111">They will also have the option of selecting the [Microsoft XPS Document Writer](/windows/win32/printdocs/microsoft-xps-document-writer) to create an XML Paper Specification (XPS) file instead of printing.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="131b3-112"><xref:System.Windows.Controls.PrintDialog?displayProperty=nameWithType>WPF 的控制項（將在本主題中討論）不應該與 Windows Forms 的元件混淆 <xref:System.Windows.Forms.PrintDialog?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="131b3-112">The <xref:System.Windows.Controls.PrintDialog?displayProperty=nameWithType> control of WPF, which is discussed in this topic, should not be confused with the <xref:System.Windows.Forms.PrintDialog?displayProperty=nameWithType> component of Windows Forms.</span></span>  
  
 <span data-ttu-id="131b3-113">嚴格來說，您可以使用 <xref:System.Windows.Controls.PrintDialog.PrintDocument%2A> 方法，而不需要開啟對話方塊。</span><span class="sxs-lookup"><span data-stu-id="131b3-113">Strictly speaking, you can use the <xref:System.Windows.Controls.PrintDialog.PrintDocument%2A> method without ever opening the dialog.</span></span> <span data-ttu-id="131b3-114">就這一點而言，控制項可用來做為看不見的列印元件。</span><span class="sxs-lookup"><span data-stu-id="131b3-114">In that sense, the control can be used as an unseen printing component.</span></span> <span data-ttu-id="131b3-115">但基於效能的考慮，最好是使用 <xref:System.Printing.PrintQueue.AddJob%2A> 方法或的多個 <xref:System.Windows.Xps.XpsDocumentWriter.Write%2A> 和方法其中之一 <xref:System.Windows.Xps.XpsDocumentWriter.WriteAsync%2A> <xref:System.Windows.Xps.XpsDocumentWriter> 。</span><span class="sxs-lookup"><span data-stu-id="131b3-115">But for performance reasons, it would be better to use either the <xref:System.Printing.PrintQueue.AddJob%2A> method or one of the many <xref:System.Windows.Xps.XpsDocumentWriter.Write%2A> and <xref:System.Windows.Xps.XpsDocumentWriter.WriteAsync%2A> methods of the <xref:System.Windows.Xps.XpsDocumentWriter>.</span></span> <span data-ttu-id="131b3-116">如需詳細資訊，請參閱以程式設計[方式列印 XPS](how-to-programmatically-print-xps-files.md)檔案。</span><span class="sxs-lookup"><span data-stu-id="131b3-116">For more about this, see [Programmatically Print XPS Files](how-to-programmatically-print-xps-files.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="131b3-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="131b3-117">See also</span></span>

- <xref:System.Windows.Controls.PrintDialog>
- [<span data-ttu-id="131b3-118">WPF 中的文件</span><span class="sxs-lookup"><span data-stu-id="131b3-118">Documents in WPF</span></span>](documents-in-wpf.md)
- [<span data-ttu-id="131b3-119">列印概觀</span><span class="sxs-lookup"><span data-stu-id="131b3-119">Printing Overview</span></span>](printing-overview.md)
- [<span data-ttu-id="131b3-120">Microsoft XPS Document Writer</span><span class="sxs-lookup"><span data-stu-id="131b3-120">Microsoft XPS Document Writer</span></span>](/windows/win32/printdocs/microsoft-xps-document-writer)
