---
title: 取得支援的 UI 自動化控制項模式
description: 閱讀示範如何從消費者介面自動化元素取出支援的控制項模式物件的範例。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- control patterns, getting
- UI Automation, getting control patterns
- getting, control patterns
ms.assetid: 006c54c9-50bf-48d9-a855-9d62eb95603a
ms.openlocfilehash: 68abe272e91c40932aba5bcf99394c4a8f815c53
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96276447"
---
# <a name="get-supported-ui-automation-control-patterns"></a><span data-ttu-id="733c9-103">取得支援的 UI 自動化控制項模式</span><span class="sxs-lookup"><span data-stu-id="733c9-103">Get Supported UI Automation Control Patterns</span></span>

> [!NOTE]
> <span data-ttu-id="733c9-104">這份文件適用於想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空間中定義之 Managed <xref:System.Windows.Automation> 類別的 .NET Framework 開發人員。</span><span class="sxs-lookup"><span data-stu-id="733c9-104">This documentation is intended for .NET Framework developers who want to use the managed [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] classes defined in the <xref:System.Windows.Automation> namespace.</span></span> <span data-ttu-id="733c9-105">如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新資訊，請參閱 [Windows Automation API：UI 自動化](/windows/win32/winauto/entry-uiauto-win32)。</span><span class="sxs-lookup"><span data-stu-id="733c9-105">For the latest information about [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], see [Windows Automation API: UI Automation](/windows/win32/winauto/entry-uiauto-win32).</span></span>  
  
 <span data-ttu-id="733c9-106">本主題顯示如何從 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 項目擷取控制項模式物件。</span><span class="sxs-lookup"><span data-stu-id="733c9-106">This topic shows how to retrieve control pattern objects from [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] elements.</span></span>  
  
### <a name="obtain-all-control-patterns"></a><span data-ttu-id="733c9-107">取得所有控制項模式</span><span class="sxs-lookup"><span data-stu-id="733c9-107">Obtain All Control Patterns</span></span>  
  
1. <span data-ttu-id="733c9-108">取得您對其控制項模式有興趣的 <xref:System.Windows.Automation.AutomationElement>。</span><span class="sxs-lookup"><span data-stu-id="733c9-108">Get the <xref:System.Windows.Automation.AutomationElement> whose control patterns you are interested in.</span></span>  
  
2. <span data-ttu-id="733c9-109">呼叫 <xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A> 以取得項目的所有控制項模式。</span><span class="sxs-lookup"><span data-stu-id="733c9-109">Call <xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A> to get all control patterns from the element.</span></span>  
  
> [!CAUTION]
> <span data-ttu-id="733c9-110">強烈建議用戶端不要使用 <xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A>。</span><span class="sxs-lookup"><span data-stu-id="733c9-110">It is strongly recommended that a client not use <xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A>.</span></span> <span data-ttu-id="733c9-111">可能會嚴重影響效能，因為這個方法會在內部針對每個現有的控制項模式呼叫 <xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A>。</span><span class="sxs-lookup"><span data-stu-id="733c9-111">Performance can be severely affected as this method calls <xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A> internally for each existing control pattern.</span></span> <span data-ttu-id="733c9-112">可能的話，用戶端應該針對感興趣的重要模式呼叫 <xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A>。</span><span class="sxs-lookup"><span data-stu-id="733c9-112">If possible, a client should call <xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A> for the key patterns of interest.</span></span>  
  
### <a name="obtain-a-specific-control-pattern"></a><span data-ttu-id="733c9-113">取得特定的控制項模式</span><span class="sxs-lookup"><span data-stu-id="733c9-113">Obtain a Specific Control Pattern</span></span>  
  
1. <span data-ttu-id="733c9-114">取得您對其控制項模式有興趣的 <xref:System.Windows.Automation.AutomationElement>。</span><span class="sxs-lookup"><span data-stu-id="733c9-114">Get the <xref:System.Windows.Automation.AutomationElement> whose control patterns you are interested in.</span></span>  
  
2. <span data-ttu-id="733c9-115">呼叫 <xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A> 或 <xref:System.Windows.Automation.AutomationElement.TryGetCurrentPattern%2A> 以查詢特定模式。</span><span class="sxs-lookup"><span data-stu-id="733c9-115">Call <xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A> or <xref:System.Windows.Automation.AutomationElement.TryGetCurrentPattern%2A> to query for a specific pattern.</span></span> <span data-ttu-id="733c9-116">這些方法很相似，但如果找不到模式，<xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A> 會引發例外狀況，且 <xref:System.Windows.Automation.AutomationElement.TryGetCurrentPattern%2A> 會傳回 `false`。</span><span class="sxs-lookup"><span data-stu-id="733c9-116">These methods are similar, but if the pattern is not found, <xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A> raises an exception, and <xref:System.Windows.Automation.AutomationElement.TryGetCurrentPattern%2A> returns `false`.</span></span>  
  
## <a name="example"></a><span data-ttu-id="733c9-117">範例</span><span class="sxs-lookup"><span data-stu-id="733c9-117">Example</span></span>  

 <span data-ttu-id="733c9-118">下列範例會擷取清單項目的 <xref:System.Windows.Automation.AutomationElement>，並從該項目取得 <xref:System.Windows.Automation.SelectionItemPattern>。</span><span class="sxs-lookup"><span data-stu-id="733c9-118">The following example retrieves an <xref:System.Windows.Automation.AutomationElement> for a list item and obtains a <xref:System.Windows.Automation.SelectionItemPattern> from that element.</span></span>  
  
 [!code-csharp[UIAClient_snip#103](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#103)]
 [!code-vb[UIAClient_snip#103](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#103)]  
  
## <a name="see-also"></a><span data-ttu-id="733c9-119">另請參閱</span><span class="sxs-lookup"><span data-stu-id="733c9-119">See also</span></span>

- [<span data-ttu-id="733c9-120">用戶端的 UI 自動化控制項模式</span><span class="sxs-lookup"><span data-stu-id="733c9-120">UI Automation Control Patterns for Clients</span></span>](ui-automation-control-patterns-for-clients.md)
