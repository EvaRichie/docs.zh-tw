---
title: 滑鼠事件
description: 瞭解如何從滑鼠事件取得滑鼠位置，並瞭解在 Windows Forms 控制項中引發滑鼠點擊事件的順序。
ms.date: 03/30/2017
helpviewer_keywords:
- MouseLeave event [Windows Forms]
- events [Windows Forms], mouse
- Click event [Windows Forms], raising order
- Windows Forms controls, click events
- MouseDoubleClick event [Windows Forms]
- MouseEnter event [Windows Forms]
- MouseHover event [Windows Forms]
- MouseDown event [Windows Forms]
- MouseClick event [Windows Forms]
- MouseMove event [Windows Forms]
- mouse [Windows Forms], events
- MouseUp event
ms.assetid: 8cf0070d-793b-4876-b09e-d20d28280fab
ms.openlocfilehash: 640448109961ea5fdf3600ef9e72d7d10e8c9e49
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/09/2020
ms.locfileid: "86174376"
---
# <a name="mouse-events-in-windows-forms"></a>Windows Form 中的滑鼠事件

當您處理滑鼠輸入時，您通常會要知道滑鼠指標的位置，以及滑鼠按鈕的狀態。 本主題提供如何從滑鼠事件取得此資訊的詳細說明，並說明在 Windows Form 控制項中引發滑鼠點按事件的順序。 如需所有滑鼠事件的清單和描述，請參閱[Windows Forms 中的滑鼠輸入運作方式](how-mouse-input-works-in-windows-forms.md)。  另請參閱[事件處理常式總覽 (Windows Forms) ](event-handlers-overview-windows-forms.md)和[事件總覽 (Windows Forms ](events-overview-windows-forms.md)) 。

## <a name="mouse-information"></a>滑鼠資訊

<xref:System.Windows.Forms.MouseEventArgs> 會傳送至有關點按滑鼠按鈕和追蹤滑鼠移動之滑鼠事件的處理常式。 <xref:System.Windows.Forms.MouseEventArgs> 提供滑鼠目前狀態的相關資訊，包括滑鼠指標在用戶端座標中的位置、按了哪個滑鼠按鈕，以及是否已捲動滑鼠滾輪。 有幾個滑鼠事件 (例如只是通知滑鼠指標何時進入或離開控制項界限的事件) 會傳送 <xref:System.EventArgs> 至事件處理常式，而沒有進一步的資訊。

如果您想要知道滑鼠按鈕的目前狀態或滑鼠指標的位置，而且您想要避免處理滑鼠事件，您也可以使用 <xref:System.Windows.Forms.Control> 類別的 <xref:System.Windows.Forms.Control.MouseButtons%2A> 和 <xref:System.Windows.Forms.Control.MousePosition%2A> 屬性。 <xref:System.Windows.Forms.Control.MouseButtons%2A> 會傳回目前按下哪些滑鼠按鈕的相關資訊。 <xref:System.Windows.Forms.Control.MousePosition%2A> 會傳回滑鼠指標的螢幕座標，等於 <xref:System.Windows.Forms.Cursor.Position%2A> 所傳回的值。

## <a name="converting-between-screen-and-client-coordinates"></a>在螢幕與用戶端座標之間轉換

因為有些滑鼠位置資訊是在用戶端座標中，而有些是在螢幕座標中，所以您可能需要將某個點從一個座標系統轉換到另一個座標系統。 使用 <xref:System.Windows.Forms.Control> 類別中所提供的 <xref:System.Windows.Forms.Control.PointToClient%2A> 和 <xref:System.Windows.Forms.Control.PointToScreen%2A> 方法，可讓您輕鬆執行此作業。

## <a name="standard-click-event-behavior"></a>標準點按事件行為

如果您想要以適當順序來處理滑鼠點按事件，您需要知道在 Windows Form 控制項中引發點按事件的順序。 除了下列清單中註明的個別控制項，當按下並放開滑鼠按鈕時 (不論哪一個滑鼠按鈕)，所有 Windows Form 控制項都是以相同順序引發點按事件。 以下是針對按一下滑鼠按鈕時，所引發的事件順序：

1. <xref:System.Windows.Forms.Control.MouseDown> 事件。

2. <xref:System.Windows.Forms.Control.Click> 事件。

3. <xref:System.Windows.Forms.Control.MouseClick> 事件。

4. <xref:System.Windows.Forms.Control.MouseUp> 事件。

以下是按兩下滑鼠按鍵時所引發的事件順序：

1. <xref:System.Windows.Forms.Control.MouseDown> 事件。

2. <xref:System.Windows.Forms.Control.Click> 事件。

3. <xref:System.Windows.Forms.Control.MouseClick> 事件。

4. <xref:System.Windows.Forms.Control.MouseUp> 事件。

5. <xref:System.Windows.Forms.Control.MouseDown> 事件。

6. <xref:System.Windows.Forms.Control.DoubleClick> 事件。 (依據有問題的控制項是否將 <xref:System.Windows.Forms.ControlStyles.StandardDoubleClick> 樣式位元設為 `true`，這會有所不同。 如需有關如何設定 <xref:System.Windows.Forms.ControlStyles> 位元的詳細資訊，請參閱 <xref:System.Windows.Forms.Control.SetStyle%2A> 方法。)

7. <xref:System.Windows.Forms.Control.MouseDoubleClick> 事件。

8. <xref:System.Windows.Forms.Control.MouseUp> 事件。

如需示範滑鼠點按事件順序的程式碼範例，請參閱[如何：處理 Windows Forms 控制項中的使用者輸入事件](how-to-handle-user-input-events-in-windows-forms-controls.md)。

### <a name="individual-controls"></a>個別控制項

下列控制項不符合標準滑鼠點按事件行為：

- <xref:System.Windows.Forms.Button>
- <xref:System.Windows.Forms.CheckBox>
- <xref:System.Windows.Forms.ComboBox>
- <xref:System.Windows.Forms.RadioButton>

  > [!NOTE]
  > 針對 <xref:System.Windows.Forms.ComboBox> 控制項，如果使用者按一下編輯欄位、按鈕或是清單中的項目，就會發生下述事件行為。

  - 按一下滑鼠左鍵：<xref:System.Windows.Forms.Control.Click>、<xref:System.Windows.Forms.Control.MouseClick>

  - 按一下滑鼠右鍵：不會引發點按事件

  - 按兩下滑鼠左鍵：<xref:System.Windows.Forms.Control.Click>、<xref:System.Windows.Forms.Control.MouseClick>；<xref:System.Windows.Forms.Control.Click>、<xref:System.Windows.Forms.Control.MouseClick>

  - 按兩下滑鼠右鍵：不會引發點按事件

- <xref:System.Windows.Forms.TextBox>、<xref:System.Windows.Forms.RichTextBox>、<xref:System.Windows.Forms.ListBox>、<xref:System.Windows.Forms.MaskedTextBox> 和 <xref:System.Windows.Forms.CheckedListBox> 控制項

  > [!NOTE]
  > 當使用者在這些控制項內的任何位置按一下，就會發生下述事件行為。

  - 按一下滑鼠左鍵：<xref:System.Windows.Forms.Control.Click>、<xref:System.Windows.Forms.Control.MouseClick>

  - 按一下滑鼠右鍵：不會引發點按事件

  - 按兩下滑鼠左鍵：<xref:System.Windows.Forms.Control.Click>、<xref:System.Windows.Forms.Control.MouseClick>、<xref:System.Windows.Forms.Control.DoubleClick>、<xref:System.Windows.Forms.Control.MouseDoubleClick>

  - 按兩下滑鼠右鍵：不會引發點按事件

- <xref:System.Windows.Forms.ListView> 控制項

  > [!NOTE]
  > 唯有當使用者按一下 <xref:System.Windows.Forms.ListView> 控制項中的項目，才會發生下述事件行為。 在控制項上任何其他地方按一下，都會不引發任何事件。 如果您想要使用驗證來搭配 <xref:System.Windows.Forms.ListView> 控制項，除了下述事件，您可能也會想要了解 <xref:System.Windows.Forms.ListView.BeforeLabelEdit> 和 <xref:System.Windows.Forms.ListView.AfterLabelEdit> 事件。

  - 按一下滑鼠左鍵：<xref:System.Windows.Forms.Control.Click>、<xref:System.Windows.Forms.Control.MouseClick>

  - 按一下滑鼠右鍵：<xref:System.Windows.Forms.Control.Click>、<xref:System.Windows.Forms.Control.MouseClick>

  - 按兩下滑鼠左鍵：<xref:System.Windows.Forms.Control.Click>、<xref:System.Windows.Forms.Control.MouseClick>；<xref:System.Windows.Forms.Control.DoubleClick>、<xref:System.Windows.Forms.Control.MouseDoubleClick>

  - 按兩下滑鼠右鍵：<xref:System.Windows.Forms.Control.Click>、<xref:System.Windows.Forms.Control.MouseClick>；<xref:System.Windows.Forms.Control.DoubleClick>、<xref:System.Windows.Forms.Control.MouseDoubleClick>

- <xref:System.Windows.Forms.TreeView> 控制項

  > [!NOTE]
  > 唯有當使用者按一下 <xref:System.Windows.Forms.TreeView> 控制項中的項目本身，或是項目右邊，才會發生下述事件行為。 在控制項上任何其他地方按一下，都會不引發任何事件。 如果您想要使用驗證來搭配 <xref:System.Windows.Forms.TreeView> 控制項，除了下述事件，您可能也會想要了解 <xref:System.Windows.Forms.TreeView.BeforeCheck>、<xref:System.Windows.Forms.TreeView.BeforeSelect>、<xref:System.Windows.Forms.TreeView.BeforeLabelEdit>、<xref:System.Windows.Forms.TreeView.AfterSelect>、<xref:System.Windows.Forms.TreeView.AfterCheck> 和 <xref:System.Windows.Forms.TreeView.AfterLabelEdit> 事件。

  - 按一下滑鼠左鍵：<xref:System.Windows.Forms.Control.Click>、<xref:System.Windows.Forms.Control.MouseClick>

  - 按一下滑鼠右鍵：<xref:System.Windows.Forms.Control.Click>、<xref:System.Windows.Forms.Control.MouseClick>

  - 按兩下滑鼠左鍵：<xref:System.Windows.Forms.Control.Click>、<xref:System.Windows.Forms.Control.MouseClick>；<xref:System.Windows.Forms.Control.DoubleClick>、<xref:System.Windows.Forms.Control.MouseDoubleClick>

  - 按兩下滑鼠右鍵：<xref:System.Windows.Forms.Control.Click>、<xref:System.Windows.Forms.Control.MouseClick>；<xref:System.Windows.Forms.Control.DoubleClick>、<xref:System.Windows.Forms.Control.MouseDoubleClick>

### <a name="painting-behavior-of-toggle-controls"></a>切換控制項的繪製行為

切換控制項 (例如衍生自 <xref:System.Windows.Forms.ButtonBase> 類別的控制項) 與滑鼠點按事件搭配組合，具有下列特殊繪圖行為：

1. 使用者按下滑鼠按鈕。

2. 控制項會以所按下的狀態繪製。

3. 便會引發 <xref:System.Windows.Forms.Control.MouseDown> 事件。

4. 使用者放開滑鼠按鈕。

5. 控制項會以所引發的狀態繪製。

6. 便會引發 <xref:System.Windows.Forms.Control.Click> 事件。

7. 便會引發 <xref:System.Windows.Forms.Control.MouseClick> 事件。

8. 便會引發 <xref:System.Windows.Forms.Control.MouseUp> 事件。

    > [!NOTE]
    > 如果使用者在按下滑鼠按鈕的同時，將指標移出切換控制項 (例如在按下滑鼠按鈕的同時，將滑鼠從 <xref:System.Windows.Forms.Button> 控制項移開)，切換控制項將會以所引發的狀態繪製，而且只會發生 <xref:System.Windows.Forms.Control.MouseUp> 事件。 在此情況下，不會發生 <xref:System.Windows.Forms.Control.Click> 或 <xref:System.Windows.Forms.Control.MouseClick> 事件。

## <a name="see-also"></a>另請參閱

- [Windows Forms 應用程式中的滑鼠輸入](mouse-input-in-a-windows-forms-application.md)
