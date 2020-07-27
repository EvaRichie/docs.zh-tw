---
title: 使用 UI 自動化周遊文字
description: 請參閱範例，以瞭解如何使用 Microsoft UI 自動化（以 TextUnit 遞增）來流覽檔的文字內容。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- UI Automation, traversing text
- text, traversing
- traversing text
ms.assetid: 3ddb3b7b-1d6b-4dba-8678-5a68e868aadb
ms.openlocfilehash: 0b4269d043fd6cd0cc5da9825714aab4ead701f9
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87168084"
---
# <a name="traverse-text-using-ui-automation"></a>使用 UI 自動化周遊文字
> [!NOTE]
> 這份文件適用於想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空間中定義之 Managed <xref:System.Windows.Automation> 類別的 .NET Framework 開發人員。 如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新資訊，請參閱 [Windows Automation API：UI 自動化](/windows/win32/winauto/entry-uiauto-win32)。  
  
 本主題說明如何使用 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] ，以 <xref:System.Windows.Automation.Text.TextUnit> 遞增來周遊文件的文字內容。  
  
## <a name="example"></a>範例  
 下列程式碼範例示範如何周遊使用者介面自動化文字提供者的內容。 <xref:System.Windows.Automation.Text.TextPatternRange.Move%2A> 方法會移動 <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint.Start> 的 <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint.End> 和 <xref:System.Windows.Automation.Text.TextPatternRange>端點。 這個文字範圍通常是表示文字插入點的變質範圍。  
  
> [!NOTE]
> 因為只有文字基礎的內嵌物件會被視為文字資料流的一部分，所以例如影像之類的內嵌物件不會影響 `Move` 或其傳回值。  
  
[!code-csharp[FindText#StartApp](../../../samples/snippets/csharp/VS_Snippets_Wpf/FindText/CSharp/SearchWindow.cs#startapp)]
[!code-vb[FindText#StartApp](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FindText/VisualBasic/SearchWindow.vb#startapp)]  
[!code-csharp[FindText#FindTextProvider](../../../samples/snippets/csharp/VS_Snippets_Wpf/FindText/CSharp/SearchWindow.cs#findtextprovider)]
[!code-vb[FindText#FindTextProvider](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FindText/VisualBasic/SearchWindow.vb#findtextprovider)]  
[!code-csharp[FindText#Navigate](../../../samples/snippets/csharp/VS_Snippets_Wpf/FindText/CSharp/SearchWindow.cs#navigate)]
[!code-vb[FindText#Navigate](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FindText/VisualBasic/SearchWindow.vb#navigate)]  
  
 如果控制項不支援指定的 <xref:System.Windows.Automation.Text.TextUnit> ，任何使用 <xref:System.Windows.Automation.Text.TextUnit> 的方法就會延後至所支援的下一個最大 <xref:System.Windows.Automation.Text.TextUnit> 。  
  
## <a name="see-also"></a>另請參閱

- [UI 自動化 TextPattern 概觀](ui-automation-textpattern-overview.md)
- [使用 UI 自動化將內容加入至文字方塊](add-content-to-a-text-box-using-ui-automation.md)
- [利用 UI 自動化尋找和反白顯示文字](find-and-highlight-text-using-ui-automation.md)
- [UI 自動化控制項模式概觀](ui-automation-control-patterns-overview.md)
- [用戶端的 UI 自動化控制項模式](ui-automation-control-patterns-for-clients.md)
