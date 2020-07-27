---
title: 使用 UI 自動化叫用控制項
description: 使用使用者介面自動化來尋找符合特定屬性條件的控制項、建立 AutomationElement、取得 InvokePattern，以及在控制項上使用 Invoke。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- invoking controls
- UI Automation, invoking controls
- controls, invoking
ms.assetid: 5ee2de3f-256c-43ec-b64c-62ace91f9983
ms.openlocfilehash: 2347a620aab848bf6bcc649a9780aa5a3a520822
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87168180"
---
# <a name="invoke-a-control-using-ui-automation"></a><span data-ttu-id="9d71d-103">使用 UI 自動化叫用控制項</span><span class="sxs-lookup"><span data-stu-id="9d71d-103">Invoke a Control Using UI Automation</span></span>
> [!NOTE]
> <span data-ttu-id="9d71d-104">這份文件適用於想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空間中定義之 Managed <xref:System.Windows.Automation> 類別的 .NET Framework 開發人員。</span><span class="sxs-lookup"><span data-stu-id="9d71d-104">This documentation is intended for .NET Framework developers who want to use the managed [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] classes defined in the <xref:System.Windows.Automation> namespace.</span></span> <span data-ttu-id="9d71d-105">如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新資訊，請參閱 [Windows Automation API：UI 自動化](/windows/win32/winauto/entry-uiauto-win32)。</span><span class="sxs-lookup"><span data-stu-id="9d71d-105">For the latest information about [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], see [Windows Automation API: UI Automation](/windows/win32/winauto/entry-uiauto-win32).</span></span>  
  
 <span data-ttu-id="9d71d-106">本主題示範如何執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="9d71d-106">This topic demonstrates how to perform the following tasks:</span></span>  
  
- <span data-ttu-id="9d71d-107">藉由查核目標應用程式之 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構的控制項檢視，尋找符合特定屬性條件的控制項。</span><span class="sxs-lookup"><span data-stu-id="9d71d-107">Find a control that matches specific property conditions by walking the control view of the [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] tree for the target application.</span></span>  
  
- <span data-ttu-id="9d71d-108">建立每個控制項的 <xref:System.Windows.Automation.AutomationElement> 。</span><span class="sxs-lookup"><span data-stu-id="9d71d-108">Create an <xref:System.Windows.Automation.AutomationElement> for each control.</span></span>  
  
- <span data-ttu-id="9d71d-109">從任何找到可支援 <xref:System.Windows.Automation.InvokePattern> 控制項模式的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 項目中，取得 <xref:System.Windows.Automation.InvokePattern> 物件。</span><span class="sxs-lookup"><span data-stu-id="9d71d-109">Obtain an <xref:System.Windows.Automation.InvokePattern> object from any [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] element found that supports the <xref:System.Windows.Automation.InvokePattern> control pattern.</span></span>  
  
- <span data-ttu-id="9d71d-110">使用 <xref:System.Windows.Automation.InvokePattern.Invoke%2A> 以叫用來自用戶端事件處理常式的控制項。</span><span class="sxs-lookup"><span data-stu-id="9d71d-110">Use <xref:System.Windows.Automation.InvokePattern.Invoke%2A> to invoke the control from a client event handler.</span></span>  
  
## <a name="example"></a><span data-ttu-id="9d71d-111">範例</span><span class="sxs-lookup"><span data-stu-id="9d71d-111">Example</span></span>  
 <span data-ttu-id="9d71d-112">此範例使用 <xref:System.Windows.Automation.AutomationElement.TryGetCurrentPattern%2A> 類別的 <xref:System.Windows.Automation.AutomationElement> 方法，產生 <xref:System.Windows.Automation.InvokePattern> 物件並利用 <xref:System.Windows.Automation.InvokePattern.Invoke%2A> 方法叫用控制項。</span><span class="sxs-lookup"><span data-stu-id="9d71d-112">This example uses the <xref:System.Windows.Automation.AutomationElement.TryGetCurrentPattern%2A> method of the <xref:System.Windows.Automation.AutomationElement> class to generate an <xref:System.Windows.Automation.InvokePattern> object and invoke a control by using the <xref:System.Windows.Automation.InvokePattern.Invoke%2A> method.</span></span>  
  
 [!code-csharp[InvokePatternApp#1100](../../../samples/snippets/csharp/VS_Snippets_Wpf/InvokePatternApp/CSharp/InvokePatternApp.cs#1100)]
 [!code-vb[InvokePatternApp#1100](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/InvokePatternApp/VisualBasic/Client.vb#1100)]  
[!code-csharp[InvokePatternApp#1102](../../../samples/snippets/csharp/VS_Snippets_Wpf/InvokePatternApp/CSharp/InvokePatternApp.cs#1102)]
[!code-vb[InvokePatternApp#1102](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/InvokePatternApp/VisualBasic/Client.vb#1102)]  
  
## <a name="see-also"></a><span data-ttu-id="9d71d-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9d71d-113">See also</span></span>

- [<span data-ttu-id="9d71d-114">InvokePattern、ExpandCollapsePattern 和 TogglePattern 範例</span><span class="sxs-lookup"><span data-stu-id="9d71d-114">InvokePattern, ExpandCollapsePattern, and TogglePattern Sample</span></span>](https://github.com/Microsoft/WPF-Samples/tree/master/Accessibility/InvokePattern)
