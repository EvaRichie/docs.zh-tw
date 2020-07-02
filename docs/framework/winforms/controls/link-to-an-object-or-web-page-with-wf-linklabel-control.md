---
title: 使用 LinkLabel 控制項連結至物件或網頁
description: 瞭解如何使用 Windows Forms LinkLabel 控制項，建立物件或網頁的 Web 樣式連結。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- examples [Windows Forms], LinkLabel control
- Windows Forms, linking to objects
- Web page link control
- linking [Windows Forms], to other forms
- Windows Forms, linking to Web pages
- links [Windows Forms], to other forms
- LinkLabel control [Windows Forms], linking to object or Web page
- LinkLabel control [Windows Forms], examples
ms.assetid: 6c91c975-3cb7-4504-82f0-fc6255f8fb85
ms.openlocfilehash: a5fb1c03e9a8d82fe77f4133ba04c42114787d23
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85618308"
---
# <a name="how-to-link-to-an-object-or-web-page-with-the-windows-forms-linklabel-control"></a>如何：使用 Windows Form LinkLabel 控制項連結至物件或 Web 網頁

Windows Forms <xref:System.Windows.Forms.LinkLabel> 控制項可讓您在表單上建立 Web 樣式連結。 按一下連結時，您可以變更其色彩，以表示已流覽過該連結。 如需變更色彩的詳細資訊，請參閱[如何：變更 Windows Forms LinkLabel 控制項的外觀](how-to-change-the-appearance-of-the-windows-forms-linklabel-control.md)。

## <a name="linking-to-another-form"></a>連結至另一個表單

#### <a name="to-link-to-another-form-with-a-linklabel-control"></a>若要使用 LinkLabel 控制項連結至另一個表單

1. 將 <xref:System.Windows.Forms.LinkLabel.Text%2A> 屬性設定為適當的標題。

2. 設定 <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> 屬性，以決定要將哪一部分的標題指定為連結。 其表示方式取決於連結標籤的外觀相關屬性。 此 <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> 值以 <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> 包含兩個數字的物件、起始字元位置和字元數來表示。 <xref:System.Windows.Forms.LinkLabel.LinkArea%2A>屬性可以在屬性視窗或程式碼中，以類似下列的方式設定：

    ```vb
    ' In this code example, the link area has been set to begin
    ' at the first character and extend for eight characters.
    ' You may need to modify this based on the text entered in Step 1.
    LinkLabel1.LinkArea = New LinkArea(0, 8)
    ```

    ```csharp
    // In this code example, the link area has been set to begin
    // at the first character and extend for eight characters.
    // You may need to modify this based on the text entered in Step 1.
    linkLabel1.LinkArea = new LinkArea(0,8);
    ```

    ```cpp
    // In this code example, the link area has been set to begin
    // at the first character and extend for eight characters.
    // You may need to modify this based on the text entered in Step 1.
    linkLabel1->LinkArea = LinkArea(0,8);
    ```

3. 在 <xref:System.Windows.Forms.LinkLabel.LinkClicked> 事件處理常式中，叫用 <xref:System.Windows.Forms.Form.Show%2A> 方法以在專案中開啟另一個表單，並將 <xref:System.Windows.Forms.LinkLabel.LinkVisited%2A> 屬性設定為 `true` 。

    > [!NOTE]
    > 類別的實例 <xref:System.Windows.Forms.LinkLabelLinkClickedEventArgs> 會攜帶已按下之控制項的參考 <xref:System.Windows.Forms.LinkLabel> ，因此不需要轉換 `sender` 物件。

    ```vb
    Protected Sub LinkLabel1_LinkClicked(ByVal Sender As System.Object, _
       ByVal e As System.Windows.Forms.LinkLabelLinkClickedEventArgs) _
       Handles LinkLabel1.LinkClicked
       ' Show another form.
       Dim f2 As New Form()
       f2.Show
       LinkLabel1.LinkVisited = True
    End Sub
    ```

    ```csharp
    protected void linkLabel1_LinkClicked(object sender, System. Windows.Forms.LinkLabelLinkClickedEventArgs e)
    {
       // Show another form.
       Form f2 = new Form();
       f2.Show();
       linkLabel1.LinkVisited = true;
    }
    ```

    ```cpp
    private:
       void linkLabel1_LinkClicked(System::Object ^  sender,
          System::Windows::Forms::LinkLabelLinkClickedEventArgs ^  e)
       {
          // Show another form.
          Form ^ f2 = new Form();
          f2->Show();
          linkLabel1->LinkVisited = true;
       }
    ```

## <a name="linking-to-a-web-page"></a>連結至網頁

<xref:System.Windows.Forms.LinkLabel>控制項也可以用來顯示具有預設瀏覽器的網頁。

#### <a name="to-start-internet-explorer-and-link-to-a-web-page-with-a-linklabel-control"></a>啟動 Internet Explorer 並連結至具有 LinkLabel 控制項的網頁

1. 將 <xref:System.Windows.Forms.LinkLabel.Text%2A> 屬性設定為適當的標題。

2. 設定 <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> 屬性，以決定要將哪一部分的標題指定為連結。

3. 在 <xref:System.Windows.Forms.LinkLabel.LinkClicked> 事件處理常式中，在例外狀況處理區塊的過程中呼叫第二個程式，將 <xref:System.Windows.Forms.LinkLabel.LinkVisited%2A> 屬性設定為 `true` ，並使用 <xref:System.Diagnostics.Process.Start%2A> 方法來啟動具有 URL 的預設瀏覽器。 若要使用 <xref:System.Diagnostics.Process.Start%2A> 方法，您必須加入命名空間的參考 <xref:System.Diagnostics?displayProperty=nameWithType> 。

    > [!IMPORTANT]
    > 如果下列程式碼是在部分信任環境中執行（例如在共用磁片磁碟機上），則在呼叫方法時，JIT 編譯程式會失敗 `VisitLink` 。 `System.Diagnostics.Process.Start`語句會導致連結要求失敗。 藉由在呼叫方法時攔截例外狀況 `VisitLink` ，下列程式碼可確保如果 JIT 編譯程式失敗，則會正常處理錯誤。

    ```vb
    Private Sub LinkLabel1_LinkClicked(ByVal sender As System.Object, _
       ByVal e As System.Windows.Forms.LinkLabelLinkClickedEventArgs) _
       Handles LinkLabel1.LinkClicked
       Try
          VisitLink()
       Catch ex As Exception
          ' The error message
          MessageBox.Show("Unable to open link that was clicked.")
       End Try
    End Sub

    Sub VisitLink()
       ' Change the color of the link text by setting LinkVisited
       ' to True.
       LinkLabel1.LinkVisited = True
       ' Call the Process.Start method to open the default browser
       ' with a URL:
       System.Diagnostics.Process.Start("http://www.microsoft.com")
    End Sub
    ```

    ```csharp
    private void linkLabel1_LinkClicked(object sender, System.Windows.Forms.LinkLabelLinkClickedEventArgs e)
    {
       try
       {
          VisitLink();
       }
       catch (Exception ex )
       {
          MessageBox.Show("Unable to open link that was clicked.");
       }
    }

    private void VisitLink()
    {
       // Change the color of the link text by setting LinkVisited
       // to true.
       linkLabel1.LinkVisited = true;
       //Call the Process.Start method to open the default browser
       //with a URL:
       System.Diagnostics.Process.Start("http://www.microsoft.com");
    }
    ```

    ```cpp
    private:
       void linkLabel1_LinkClicked(System::Object ^  sender,
          System::Windows::Forms::LinkLabelLinkClickedEventArgs ^  e)
       {
          try
          {
             VisitLink();
          }
          catch (Exception ^ ex)
          {
             MessageBox::Show("Unable to open link that was clicked.");
          }
       }
    private:
       void VisitLink()
       {
          // Change the color of the link text by setting LinkVisited
          // to true.
          linkLabel1->LinkVisited = true;
          // Call the Process.Start method to open the default browser
          // with a URL:
          System::Diagnostics::Process::Start("http://www.microsoft.com");
       }
    ```

## <a name="see-also"></a>另請參閱

- <xref:System.Diagnostics.Process.Start%2A?displayProperty=nameWithType>
- [LinkLabel 控制項概觀](linklabel-control-overview-windows-forms.md)
- [操作說明：變更 Windows Forms LinkLabel 控制項的外觀](how-to-change-the-appearance-of-the-windows-forms-linklabel-control.md)
- [LinkLabel 控制項](linklabel-control-windows-forms.md)
