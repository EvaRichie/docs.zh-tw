---
title: 使用 UI 自動化周遊文字
description: 若要瞭解如何使用 Microsoft 消費者介面自動化（以 TextUnit 增量）來遍歷檔的文字內容，請參閱範例。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- UI Automation, traversing text
- text, traversing
- traversing text
ms.assetid: 3ddb3b7b-1d6b-4dba-8678-5a68e868aadb
ms.openlocfilehash: 1413cac56e3d6358eb58d55eb2fc0ca583147571
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96242028"
---
# <a name="traverse-text-using-ui-automation"></a><span data-ttu-id="6e9a0-103">使用 UI 自動化周遊文字</span><span class="sxs-lookup"><span data-stu-id="6e9a0-103">Traverse Text Using UI Automation</span></span>

> [!NOTE]
> <span data-ttu-id="6e9a0-104">這份文件適用於想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空間中定義之 Managed <xref:System.Windows.Automation> 類別的 .NET Framework 開發人員。</span><span class="sxs-lookup"><span data-stu-id="6e9a0-104">This documentation is intended for .NET Framework developers who want to use the managed [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] classes defined in the <xref:System.Windows.Automation> namespace.</span></span> <span data-ttu-id="6e9a0-105">如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新資訊，請參閱 [Windows Automation API：UI 自動化](/windows/win32/winauto/entry-uiauto-win32)。</span><span class="sxs-lookup"><span data-stu-id="6e9a0-105">For the latest information about [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], see [Windows Automation API: UI Automation](/windows/win32/winauto/entry-uiauto-win32).</span></span>  
  
 <span data-ttu-id="6e9a0-106">本主題說明如何使用 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] ，以 <xref:System.Windows.Automation.Text.TextUnit> 遞增來周遊文件的文字內容。</span><span class="sxs-lookup"><span data-stu-id="6e9a0-106">This topic shows how to use [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] to traverse the textual content of a document by <xref:System.Windows.Automation.Text.TextUnit> increments.</span></span>  
  
## <a name="example"></a><span data-ttu-id="6e9a0-107">範例</span><span class="sxs-lookup"><span data-stu-id="6e9a0-107">Example</span></span>  

 <span data-ttu-id="6e9a0-108">下列程式碼範例示範如何周遊使用者介面自動化文字提供者的內容。</span><span class="sxs-lookup"><span data-stu-id="6e9a0-108">The following code example demonstrates how to traverse the content of a UI Automation text provider.</span></span> <span data-ttu-id="6e9a0-109"><xref:System.Windows.Automation.Text.TextPatternRange.Move%2A> 方法會移動 <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint.Start> 的 <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint.End> 和 <xref:System.Windows.Automation.Text.TextPatternRange>端點。</span><span class="sxs-lookup"><span data-stu-id="6e9a0-109">The <xref:System.Windows.Automation.Text.TextPatternRange.Move%2A> method moves the <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint.Start> and <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint.End> endpoints of a <xref:System.Windows.Automation.Text.TextPatternRange>.</span></span> <span data-ttu-id="6e9a0-110">這個文字範圍通常是表示文字插入點的變質範圍。</span><span class="sxs-lookup"><span data-stu-id="6e9a0-110">This text range is typically a degenerate range representing the text insertion point.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="6e9a0-111">因為只有文字基礎的內嵌物件會被視為文字資料流的一部分，所以例如影像之類的內嵌物件不會影響 `Move` 或其傳回值。</span><span class="sxs-lookup"><span data-stu-id="6e9a0-111">Since only text-based embedded objects are considered part of the text stream, embedded objects such as images do not affect `Move` or its return value.</span></span>  
  
[!code-csharp[FindText#StartApp](../../../samples/snippets/csharp/VS_Snippets_Wpf/FindText/CSharp/SearchWindow.cs#startapp)]
[!code-vb[FindText#StartApp](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FindText/VisualBasic/SearchWindow.vb#startapp)]  
[!code-csharp[FindText#FindTextProvider](../../../samples/snippets/csharp/VS_Snippets_Wpf/FindText/CSharp/SearchWindow.cs#findtextprovider)]
[!code-vb[FindText#FindTextProvider](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FindText/VisualBasic/SearchWindow.vb#findtextprovider)]  
[!code-csharp[FindText#Navigate](../../../samples/snippets/csharp/VS_Snippets_Wpf/FindText/CSharp/SearchWindow.cs#navigate)]
[!code-vb[FindText#Navigate](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FindText/VisualBasic/SearchWindow.vb#navigate)]  
  
 <span data-ttu-id="6e9a0-112">如果控制項不支援指定的 <xref:System.Windows.Automation.Text.TextUnit> ，任何使用 <xref:System.Windows.Automation.Text.TextUnit> 的方法就會延後至所支援的下一個最大 <xref:System.Windows.Automation.Text.TextUnit> 。</span><span class="sxs-lookup"><span data-stu-id="6e9a0-112">Any method using <xref:System.Windows.Automation.Text.TextUnit> will defer to the next largest <xref:System.Windows.Automation.Text.TextUnit> supported if the given <xref:System.Windows.Automation.Text.TextUnit> is not supported by the control.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="6e9a0-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6e9a0-113">See also</span></span>

- [<span data-ttu-id="6e9a0-114">UI 自動化 TextPattern 概觀</span><span class="sxs-lookup"><span data-stu-id="6e9a0-114">UI Automation TextPattern Overview</span></span>](ui-automation-textpattern-overview.md)
- [<span data-ttu-id="6e9a0-115">使用 UI 自動化將內容加入至文字方塊</span><span class="sxs-lookup"><span data-stu-id="6e9a0-115">Add Content to a Text Box Using UI Automation</span></span>](add-content-to-a-text-box-using-ui-automation.md)
- [<span data-ttu-id="6e9a0-116">利用 UI 自動化尋找和反白顯示文字</span><span class="sxs-lookup"><span data-stu-id="6e9a0-116">Find and Highlight Text Using UI Automation</span></span>](find-and-highlight-text-using-ui-automation.md)
- [<span data-ttu-id="6e9a0-117">UI 自動化控制項模式概觀</span><span class="sxs-lookup"><span data-stu-id="6e9a0-117">UI Automation Control Patterns Overview</span></span>](ui-automation-control-patterns-overview.md)
- [<span data-ttu-id="6e9a0-118">用戶端的 UI 自動化控制項模式</span><span class="sxs-lookup"><span data-stu-id="6e9a0-118">UI Automation Control Patterns for Clients</span></span>](ui-automation-control-patterns-for-clients.md)
