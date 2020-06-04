---
title: 使用 .NET Framework 方法管理檔案
ms.date: 07/20/2015
helpviewer_keywords:
- I/O [Visual Basic], walkthroughs
- text files [Visual Basic], writing to
- reading text files [Visual Basic]
- text, writing to files
- files [Visual Basic], searching
- StreamReader class, walkthroughs
- files [Visual Basic], accessing
- I/O [Visual Basic], writing text to files
- writing to files [Visual Basic], walkthroughs
- StreamWriter class, walkthroughs
- text files [Visual Basic], reading
- I/O [Visual Basic], reading text from files
ms.assetid: 7d2109eb-f98a-4389-b43d-30f384aaa7d5
ms.openlocfilehash: 9abb87f3f6cdefefef29eb37c2c2d4d15155e93d
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84406647"
---
# <a name="walkthrough-manipulating-files-by-using-net-framework-methods-visual-basic"></a>逐步解說：使用 .NET Framework 方法管理檔案 (Visual Basic)

本逐步解說示範如何使用 <xref:System.IO.StreamReader> 類別開啟和讀取檔案、檢查是否正在存取檔案、在 <xref:System.IO.StreamReader> 類別執行個體讀取的檔案內搜尋字串，並使用 <xref:System.IO.StreamWriter> 類別寫入檔案。

[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]

## <a name="creating-the-application"></a>建立應用程式

若要啟動 Visual Studio 並開始專案，您可以建立表單，以供使用者寫入至指定的檔案。

### <a name="to-create-the-project"></a>若要建立專案

1. 在 [檔案]**** 功能表上，選取 [新增專案]****。

2. 按一下 [新增專案] 窗格的 [Windows 應用程式]。********

3. 在 [**名稱**] 方塊中輸入 `MyDiary` ，然後按一下 **[確定]**。

     Visual Studio 會將專案加入**方案總管**， **Windows Form 設計工具**隨即開啟。

4. 將下表的控制項新增至表單，並設定其屬性的對應值。

|**Object**|**屬性**|**ReplTest1**|
|---|---|---|
|<xref:System.Windows.Forms.Button>|**名稱**<br /><br /> **文字**|`Submit`<br /><br /> **提交項目**|
|<xref:System.Windows.Forms.Button>|**名稱**<br /><br /> **文字**|`Clear`<br /><br /> **清除項目**|
|<xref:System.Windows.Forms.TextBox>|**名稱**<br /><br /> **文字**<br /><br /> **多行**|`Entry`<br /><br /> **請輸入某些內容。**<br /><br /> `False`|

## <a name="writing-to-the-file"></a>寫入檔案

若要新增透過應用程式寫入檔案的功能，請使用 <xref:System.IO.StreamWriter> 類別。 <xref:System.IO.StreamWriter> 是專為以特定的編碼方式輸出字元而量身打造，而<xref:System.IO.Stream> 類別則是針對位元組輸入和輸出而設計。 使用 <xref:System.IO.StreamWriter> 將資訊行寫入標準文字檔案。 如需 <xref:System.IO.StreamWriter> 類別的詳細資訊，請參閱 <xref:System.IO.StreamWriter>。

### <a name="to-add-writing-functionality"></a>若要新增寫入功能

1. 從 [檢視] 功能表上，選擇 [程式碼] 以開啟程式碼編輯器。********

2. 由於應用程式會參考 <xref:System.IO> 命名空間，因此請在表單類別宣告開始之前 (其會開始 `Public Class Form1`)，於程式碼開頭加入下列陳述式。

     [!code-vb[VbVbcnMyFileSystem#35](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#35)]

     在寫入檔案之前，您必須建立 <xref:System.IO.StreamWriter> 類別的執行個體。

3. 從 [檢視] 功能表上，選擇 [設計工具] 以返回 Windows Forms 設計工具。************ 按兩下 `Submit` 按鈕，建立該按鈕的 <xref:System.Windows.Forms.Control.Click> 事件處理常式，然後加入下列程式碼。

     [!code-vb[VbVbcnMyFileSystem#36](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#36)]

> [!NOTE]
> Visual Studio 整合式開發環境 (IDE) 會返回程式碼編輯器，並在事件處理常式中放入您應該新增程式碼的位置插入點。

1. 若要寫入檔案，請使用 <xref:System.IO.StreamWriter> 類別的 <xref:System.IO.StreamWriter.Write%2A> 方法。 將下列程式碼新增至 `Dim fw As StreamWriter` 正後方。 您不用擔心系統會在找不到檔案時擲回例外狀況，因為若檔案不存在，系統會加以建立。

     [!code-vb[VbVbcnMyFileSystem#37](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#37)]

2. 您可在 `Dim ReadString As String` 正後方加入下列程式碼，確定使用者無法提交空白項目。

     [!code-vb[VbVbcnMyFileSystem#38](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#38)]

3. 由於此為日記，因此使用者會需要針對每個項目指派日期。 在 `fw = New StreamWriter("C:\MyDiary.txt", True)` 之後插入下列程式碼，以將 `Today` 變數設為目前的日期。

     [!code-vb[VbVbcnMyFileSystem#39](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#39)]

4. 最後，附加程式碼來清除 <xref:System.Windows.Forms.TextBox>。 將下列程式碼加入 `Clear` 按鈕的 <xref:System.Windows.Forms.Control.Click> 事件。

     [!code-vb[VbVbcnMyFileSystem#40](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#40)]

## <a name="adding-display-features-to-the-diary"></a>新增日記的顯示功能

在本節中，您會新增功能以顯示 `DisplayEntry`<xref:System.Windows.Forms.TextBox> 中的最新項目。 您也可以加入 <xref:System.Windows.Forms.ComboBox> 以顯示各種項目，使用者可以從中選取要在 `DisplayEntry`<xref:System.Windows.Forms.TextBox> 中顯示的項目。 <xref:System.IO.StreamReader> 類別的執行個體會讀取 `MyDiary.txt`。 像 <xref:System.IO.StreamWriter> 類別一樣，<xref:System.IO.StreamReader> 適用於文字檔案。

在本節逐步解說中，請將下表的控制項新增至表單，並設定其屬性的對應值。

|控制|屬性|值|
|-------------|----------------|------------|
|<xref:System.Windows.Forms.TextBox>|**名稱**<br /><br /> **亮起**<br /><br /> **大小**<br /><br /> **多行**|`DisplayEntry`<br /><br /> `False`<br /><br /> `120,60`<br /><br /> `True`|
|<xref:System.Windows.Forms.Button>|**名稱**<br /><br /> **文字**|`Display`<br /><br /> **顯示器**|
|<xref:System.Windows.Forms.Button>|**名稱**<br /><br /> **文字**|`GetEntries`<br /><br /> **取得項目**|
|<xref:System.Windows.Forms.ComboBox>|**名稱**<br /><br /> **文字**<br /><br /> **已啟用**|`PickEntries`<br /><br /> **選取項目**<br /><br /> `False`|

### <a name="to-populate-the-combo-box"></a>若要填入下拉式方塊

1. 系統會使用 `PickEntries`<xref:System.Windows.Forms.ComboBox> 來顯示使用者提交每個項目的日期，因此使用者可以選取特定日期的項目。 對 `GetEntries` 按鈕建立 <xref:System.Windows.Forms.Control.Click> 事件處理常式，並加入下列程式碼。

     [!code-vb[VbVbcnMyFileSystem#41](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#41)]

2. 若要測試您的程式碼，請按 F5 以編譯應用程式，然後按一下 [取得項目]。**** 在 <xref:System.Windows.Forms.ComboBox> 中按一下下拉式箭號以顯示項目日期。

### <a name="to-choose-and-display-individual-entries"></a>若要選擇並顯示個別項目

1. 為 `Display` 按鈕建立 <xref:System.Windows.Forms.Control.Click> 事件處理常式，並加入下列程式碼。

     [!code-vb[VbVbcnMyFileSystem#42](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#42)]

2. 若要測試您的程式碼，請按 F5 以編譯應用程式，然後提交項目。 按一下 [取得項目]****，從 <xref:System.Windows.Forms.ComboBox> 選取項目，然後按一下 [顯示]****。 選取項目的內容會出現在 `DisplayEntry`<xref:System.Windows.Forms.TextBox> 中。

## <a name="enabling-users-to-delete-or-modify-entries"></a>讓使用者可以刪除或修改項目

最後，您可以包含其他功能，讓使用者可以利用 `DeleteEntry` 和 `EditEntry` 按鈕，刪除或修改項目。 未顯示項目時，這兩個按鈕皆為停用狀態。

將下表的控制項新增至表單，並設定其屬性的對應值。

|控制|屬性|值|
|-------------|----------------|------------|
|<xref:System.Windows.Forms.Button>|**名稱**<br /><br /> **文字**<br /><br /> **已啟用**|`DeleteEntry`<br /><br /> **刪除項目**<br /><br /> `False`|
|<xref:System.Windows.Forms.Button>|**名稱**<br /><br /> **文字**<br /><br /> **已啟用**|`EditEntry`<br /><br /> **編輯項目**<br /><br /> `False`|
|<xref:System.Windows.Forms.Button>|**名稱**<br /><br /> **文字**<br /><br /> **已啟用**|`SubmitEdit`<br /><br /> **提交編輯**<br /><br /> `False`|

### <a name="to-enable-deletion-and-modification-of-entries"></a>若要啟用項目的刪除和修改功能

1. 將下列程式碼加入 `Display` 按鈕的 <xref:System.Windows.Forms.Control.Click> 事件，放在 `DisplayEntry.Text = ReadString` 之後。

     [!code-vb[VbVbcnMyFileSystem#43](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#43)]

2. 為 `DeleteEntry` 按鈕建立 <xref:System.Windows.Forms.Control.Click> 事件處理常式，並加入下列程式碼。

     [!code-vb[VbVbcnMyFileSystem#44](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#44)]

3. 當使用者顯示項目時，`EditEntry` 按鈕即變成啟用。 將下列程式碼加入 `Display` 按鈕的 <xref:System.Windows.Forms.Control.Click> 事件，放在 `DisplayEntry.Text = ReadString` 之後。

     [!code-vb[VbVbcnMyFileSystem#45](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#45)]

4. 為 `EditEntry` 按鈕建立 <xref:System.Windows.Forms.Control.Click> 事件處理常式，並加入下列程式碼。

     [!code-vb[VbVbcnMyFileSystem#46](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#46)]

5. 為 `SubmitEdit` 按鈕建立 <xref:System.Windows.Forms.Control.Click> 事件處理常式，並加入下列程式碼

     [!code-vb[VbVbcnMyFileSystem#47](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#47)]

若要測試您的程式碼，請按 F5 以編譯應用程式。 按一下 [取得項目]，並選取項目，然後按一下 [顯示]。******** 此項目會出現在 `DisplayEntry`<xref:System.Windows.Forms.TextBox> 中。 按一下 [編輯項目]****。 此項目會出現在 `Entry`<xref:System.Windows.Forms.TextBox> 中。 編輯中的專案 `Entry` <xref:System.Windows.Forms.TextBox> ，然後按一下 [**提交編輯**]。 開啟 `MyDiary.txt` 檔案，確認您的修正。 現在，選取項目，然後按一下 [刪除項目]****。 當 <xref:System.Windows.Forms.MessageBox> 要求確認時，請按一下 [確定]****。 關閉應用程式，並開啟 `MyDiary.txt` 以確認刪除。

## <a name="see-also"></a>另請參閱

- <xref:System.IO.StreamReader>
- <xref:System.IO.StreamWriter>
- [逐步解說](../../../walkthroughs.md)
