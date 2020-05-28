---
title: 如何：在 Windows 應用程式中提供說明
ms.date: 03/30/2017
helpviewer_keywords:
- Help [Windows Forms], Windows applications
- HTML Help [Windows Forms], Windows Forms
- Windows applications [Windows Forms], providing Help
- HelpProvider component [Windows Forms]
- forms [Windows Forms], providing Help
ms.assetid: 7c4e5cec-2bd2-4f0b-8d75-c2b88929bd61
ms.openlocfilehash: 405de333ce936a864047e827e60f56a930059e26
ms.sourcegitcommit: ee5b798427f81237a3c23d1fd81fff7fdc21e8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/28/2020
ms.locfileid: "84143587"
---
# <a name="how-to-provide-help-in-a-windows-application"></a>如何：在 Windows 應用程式中提供說明

您可以利用元件，將說明檔 <xref:System.Windows.Forms.HelpProvider> 中的說明主題附加至 Windows Forms 上的特定控制項。 說明檔可以是 HTML 或 HTMLHelp 1.x 或更高的格式。

## <a name="provide-help"></a>提供協助

1. 在 Visual Studio 中，將元件從 [**工具箱**] 拖曳 <xref:System.Windows.Forms.HelpProvider> 至您的表單。

     此元件將位在 Windows Forms 設計工具底部的系統匣中。

2. 在 [**屬性**] 視窗中，將 <xref:System.Windows.Forms.HelpProvider.HelpNamespace%2A> 屬性設定為 .chm、col 或 .htm 說明檔。

3. 選取您在表單上擁有的另一個控制項，然後在 [**屬性**] 視窗中設定 <xref:System.Windows.Forms.HelpProvider.SetHelpKeyword%2A> 屬性。

     這是透過元件傳遞至說明檔的字串， <xref:System.Windows.Forms.HelpProvider> 以啟動適當的說明主題。

4. 在 [**屬性**] 視窗中，將 <xref:System.Windows.Forms.HelpProvider.SetHelpNavigator%2A> 屬性設定為列舉的 <xref:System.Windows.Forms.HelpNavigator> 值。

     這會決定將 **HelpKeyword** 屬性傳遞給說明系統的方式。 下表顯示可能的設定和其描述。

    |成員名稱|描述|
    |-----------------|-----------------|
    |AssociateIndex|指定在指定的 URL 中執行所指定主題的索引。|
    |Find|指定顯示所指定 URL 的搜尋頁面。|
    |索引|指定顯示所指定 URL 的索引。|
    |KeywordIndex|指定要搜尋的關鍵字以及要在指定的 URL 中採取的動作。|
    |TableOfContents|指定顯示 HTML 1.0 說明檔的目錄。|
    |主題|指定顯示指定之 URL 所參考的主題。|

 在執行時間，當控制項（已設定 [ **HelpKeyword** ] 和 [ **HelpNavigator** ] 屬性）上按下 F1 時，焦點會開啟您與該元件相關聯的說明檔 <xref:System.Windows.Forms.HelpProvider> 。

 目前，**HelpNamespace** 屬性支援下列三種格式的說明檔：HTMLHelp 1.x、HTMLHelp 2.0 和 HTML。 因此，您可以將**HelpNamespace**屬性設定為 `http://` 位址，例如網頁。 如果這麼做，則會開啟將 **HelpKeyword** 屬性中所指定的字串用作錨點之網頁的預設瀏覽器。 錨點是用來跳到 HTML 網頁的特定組件。

> [!IMPORTANT]
> 請先仔細檢查用戶端所傳送的任何資訊，再將它用於應用程式中。 惡意使用者可能會嘗試傳送或插入可執行的指令碼、SQL 陳述式或其他程式碼。 在顯示使用者的輸入、將它儲存在資料庫中，或使用它之前，請先檢查它未包含可能不安全的資訊。 一般檢查方式是在您收到來自使用者的輸入時，使用規則運算式來尋找關鍵字，例如 "SCRIPT"。

您也可以使用 <xref:System.Windows.Forms.HelpProvider> 元件來顯示快顯說明，即使您已將它設定為顯示 Windows Forms 上控制項的說明檔。 如需詳細資訊，請參閱[如何：顯示快顯說明](how-to-display-pop-up-help.md)。

## <a name="see-also"></a>另請參閱

- [如何：顯示快顯說明](how-to-display-pop-up-help.md)
- [使用工具提示來顯示控制項說明](control-help-using-tooltips.md)
- [整合 Windows Forms 中的使用者說明](integrating-user-help-in-windows-forms.md)
- [Windows Forms](../index.md)
