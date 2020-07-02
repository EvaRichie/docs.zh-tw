---
title: 取得並設定 DataGridView 控制項中的目前儲存格
description: 瞭解如何藉由取得並設定 Windows Forms DataGridView 控制項中的目前儲存格，以程式設計方式探索目前作用中的儲存格。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataGridView control [Windows Forms], getting current cell
- DataGridView control [Windows Forms], setting current cell
- cells [Windows Forms], getting and setting current
ms.assetid: b0e41e57-493a-4bd0-9376-a6f76723540c
ms.openlocfilehash: 1651ca9c8fa0329f9435a70ce777bce68f15ff63
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622207"
---
# <a name="how-to-get-and-set-the-current-cell-in-the-windows-forms-datagridview-control"></a>如何：取得和設定 Windows Form DataGridView 控制項中目前的儲存格
與互動 <xref:System.Windows.Forms.DataGridView> 通常需要您以程式設計方式探索目前使用中的儲存格。 您也可能需要變更目前的儲存格。 您可以使用屬性來執行這些工作 <xref:System.Windows.Forms.DataGridView.CurrentCell%2A> 。  
  
> [!NOTE]
> 您無法在其屬性設定為的資料列或資料行中，設定目前的儲存格 <xref:System.Windows.Forms.DataGridViewBand.Visible%2A> `false` 。  
  
 根據 <xref:System.Windows.Forms.DataGridView> 控制項的選取模式，變更目前的儲存格可以變更選取範圍。 如需詳細資訊，請參閱[Windows Forms DataGridView 控制項中的選取模式](selection-modes-in-the-windows-forms-datagridview-control.md)。  
  
### <a name="to-get-the-current-cell-programmatically"></a>以程式設計方式取得目前的儲存格  
  
- 使用 <xref:System.Windows.Forms.DataGridView> 控制項的 <xref:System.Windows.Forms.DataGridView.CurrentCell%2A> 屬性。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#080](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#080)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#080](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#080)]  
  
### <a name="to-set-the-current-cell-programmatically"></a>以程式設計方式設定目前的儲存格  
  
- 設定 <xref:System.Windows.Forms.DataGridView.CurrentCell%2A> 控制項的屬性 <xref:System.Windows.Forms.DataGridView> 。 在下列程式碼範例中，目前儲存格設定為數據列0，資料行1。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#085](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#085)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#085](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#085)]  
  
## <a name="compiling-the-code"></a>編譯程式碼  
 這個範例需要：  
  
- <xref:System.Windows.Forms.Button>名為 `getCurrentCellButton` 和 `setCurrentCellButton` 的控制項。 在 Visual c # 中，您必須將 <xref:System.Windows.Forms.Control.Click> 每個按鈕的事件附加至範例程式碼中相關聯的事件處理常式。  
  
- 名為 `dataGridView1` 的 <xref:System.Windows.Forms.DataGridView> 控制項。  
  
- <xref:System?displayProperty=nameWithType> 和 <xref:System.Windows.Forms?displayProperty=nameWithType> 組件的參考。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridView.CurrentCell%2A?displayProperty=nameWithType>
- [Windows Forms DataGridView 控制項中的基本資料行、資料列和儲存格功能](basic-column-row-and-cell-features-wf-datagridview-control.md)
- [Windows Forms DataGridView 控制項中的選取模式](selection-modes-in-the-windows-forms-datagridview-control.md)
