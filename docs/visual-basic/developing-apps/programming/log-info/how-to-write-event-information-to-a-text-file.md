---
title: 作法：將事件資訊寫入文字檔
ms.date: 07/20/2015
helpviewer_keywords:
- event logs [Visual Studio], writing event information
- text files [Visual Basic], writing event information to a text file
- events [Visual Basic], writing event information to a text file
ms.assetid: 9ca7cc03-bf99-4933-9e5e-61ee28e9a6b4
ms.openlocfilehash: 6e83f8450ca7be8a2dcd5ff43eab3dd2ec0d2f1b
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410058"
---
# <a name="how-to-write-event-information-to-a-text-file-visual-basic"></a>如何：將事件資訊寫入至文字檔 (Visual Basic)

您可以使用 `My.Application.Log` 和 `My.Log` 物件來記錄應用程式中發生之事件的相關資訊。 這個範例示範如何使用 `My.Application.Log.WriteEntry` 方法將追蹤資訊記錄到記錄檔。

### <a name="to-add-and-configure-the-file-log-listener"></a>新增和設定檔案記錄檔接聽程式

1. 在 方案總管 中，以滑鼠右鍵按一下 app.config 並選擇 [開啟]。********

     \- 或 -

     如果沒有 app.config 檔案︰

    1. 在 [ **專案** ] 功能表中，選擇 [ **加入新項目**]。

    2. 在 [加入新項目] **** 對話方塊中，選擇 [應用程式組態檔] ****。

    3. 按一下 [新增] 。

2. 在應用程式組態檔中找出 `<listeners>` 區段。

     您會找到名稱屬性為 "DefaultSource" 之 \<listeners> 區段 (位於最上層 \<source> 區段底下 \<system.diagnostics> 區段中) 中的 \<configuration> 區段。

3. 將此項目加入至該 `<listeners>` 區段︰

    ```xml
    <add name="FileLogListener" />
    ```

4. 找出巢狀於最上層 `<configuration>` 區段中 `<system.diagnostics>` 區段的 `<sharedListeners>` 區段。

5. 將此項目加入至該 `<sharedListeners>` 區段︰

    ```xml
    <add name="FileLogListener"
        type="Microsoft.VisualBasic.Logging.FileLogTraceListener,
              Microsoft.VisualBasic, Version=8.0.0.0, Culture=neutral,
              PublicKeyToken=b03f5f7f11d50a3a"
        initializeData="FileLogListenerWriter"
        location="Custom"
        customlocation="c:\temp\" />
    ```

     將 `customlocation` 屬性的值變更為記錄檔目錄。

    > [!NOTE]
    > 若要設定 listener 屬性的值，請使用與屬性 (property) 同名的屬性 (attribute)，而名稱中的所有字母都是小寫。 例如，`location` 和 `customlocation` 屬性會設定 <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.Location%2A> 和 <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.CustomLocation%2A> 屬性的值。

### <a name="to-write-event-information-to-the-file-log"></a>將事件資訊寫入檔案記錄檔

使用 `My.Application.Log.WriteEntry` 或 `My.Application.Log.WriteException` 方法，將資訊寫入檔案記錄檔。 如需詳細資訊，請參閱[如何：寫入記錄訊息](how-to-write-log-messages.md)和[如何：記錄例外狀況](how-to-log-exceptions.md)。

設定組件的檔案記錄檔接聽程式之後，接聽程式會接收 `My.Application.Log` 從該組件寫入的所有訊息。

## <a name="see-also"></a>另請參閱

- <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteException%2A>
- [使用應用程式記錄檔](working-with-application-logs.md)
- [作法：記錄例外狀況](how-to-log-exceptions.md)
