---
title: 新增控制項
description: 瞭解如何在 Windows Form 上繪製控制項。 控制項是表單上的元件，您可以用來顯示資訊或接受使用者輸入。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Windows Forms controls, adding to form
- controls [Windows Forms], adding
ms.assetid: 2af86001-9d62-4154-87fb-66db2c3cd9fd
ms.openlocfilehash: d9ab0d78fa0153cce20fb17d22f6e9e781229ece
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/24/2020
ms.locfileid: "85325889"
---
# <a name="how-to-add-controls-to-windows-forms"></a>如何：將控制項加入至 Windows Form

大部分的表單都是藉由將控制項新增至表單介面來定義使用者介面（UI）而設計。 *控制項*是表單上用來顯示資訊或接受使用者輸入的元件。 如需控制項的詳細資訊，請參閱[Windows Forms 控制項](index.md)。

## <a name="to-draw-a-control-on-a-form"></a>若要在表單上繪製控制項

1. 開啟表單。 如需詳細資訊，請參閱[如何：在設計工具中顯示 Windows Forms](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/w5yd62ts(v=vs.100))。

2. 在 [**工具箱**] 中，按一下您想要新增至表單的控制項。

3. 在表單上，按一下您想要找出控制項左上角的位置，並將其拖曳至您想要放置控制項右下角的位置。

    控制項會以指定的位置和大小加入表單中。

    > [!NOTE]
    > 每個控制項都有定義的預設大小。 您可以將控制項從 [**工具箱**] 拖曳至表單，以將控制項的預設大小加入表單中。

## <a name="to-drag-a-control-to-a-form"></a>將控制項拖曳至表單

1. 開啟表單。 如需詳細資訊，請參閱[如何：在設計工具中顯示 Windows Forms](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/w5yd62ts(v=vs.100))。

2. 在 [**工具箱**] 中，按一下您想要的控制項，並將它拖曳至您的表單。

    控制項會在其預設大小的指定位置加入表單中。

    > [!NOTE]
    > 您可以在 [**工具箱**] 中按兩下控制項，將它新增至表單的左上角（其預設大小）。

    您也可以在執行時間以動態方式將控制項新增至表單。 在下列程式碼範例中， <xref:System.Windows.Forms.TextBox> 當您按一下控制項時，控制項就會加入表單中 <xref:System.Windows.Forms.Button> 。

    > [!NOTE]
    > 下列程式需要具有**Button** `Button1` 已放在其上之按鈕控制項的表單存在。

## <a name="to-add-a-control-to-a-form-programmatically"></a>以程式設計方式將控制項新增至表單

1. 在處理 `Click` 表單類別內按鈕之事件的方法中，插入與下列類似的程式碼，以將參考加入控制項變數、設定控制項的 `Location` ，以及加入控制項。

    ```vb
    Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click
       Dim MyText As New TextBox()
       MyText.Location = New Point(25, 25)
       Me.Controls.Add(MyText)
    End Sub
    ```

    ```csharp
    private void button1_Click(object sender, System.EventArgs e)
    {
       TextBox myText = new TextBox();
       myText.Location = new Point(25,25);
       this.Controls.Add (myText);
    }
    ```

    ```cpp
    private:
      System::Void button1_Click(System::Object ^  sender,
        System::EventArgs ^  e)
      {
        TextBox ^ myText = gcnew TextBox();
        myText->Location = Point(25,25);
        this->Controls->Add(myText);
      }
    ```

    > [!NOTE]
    > 您也可以加入程式碼來初始化控制項的其他屬性。

    > [!IMPORTANT]
    > 藉由參考惡意，您可能會透過網路將本機電腦暴露在安全性風險中 `UserControl` 。 這只是在惡意人士建立損毀的自訂控制項，然後誤將它新增至專案時的問題。

## <a name="see-also"></a>另請參閱

- [Windows Forms 控制項](index.md)
- [如何：重新調整 Windows Form 上控制項的大小](how-to-resize-controls-on-windows-forms.md)
- [如何：設定由 Windows Form 控制項所顯示的文字](how-to-set-the-text-displayed-by-a-windows-forms-control.md)
- [在 Windows Form 上使用的控制項](controls-to-use-on-windows-forms.md)
