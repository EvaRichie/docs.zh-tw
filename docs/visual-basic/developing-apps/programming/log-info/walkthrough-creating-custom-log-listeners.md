---
title: 建立自訂記錄檔接聽程式
ms.date: 07/20/2015
helpviewer_keywords:
- custom log listeners
- My.Application.Log object, custom log listeners
ms.assetid: 0e019115-4b25-4820-afb1-af8c6e391698
ms.openlocfilehash: 5a140607a4fe7e1e13de54e8d56cab53e52aaa2a
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84398262"
---
# <a name="walkthrough-creating-custom-log-listeners-visual-basic"></a>逐步解說：建立自訂的記錄檔接聽程式 (Visual Basic)

本逐步解說示範如何建立自訂記錄檔接聽程式，並將它設定為接聽 `My.Application.Log` 物件的輸出。

## <a name="getting-started"></a>開始使用

記錄檔接聽程式必須繼承自 <xref:System.Diagnostics.TraceListener> 類別。

#### <a name="to-create-the-listener"></a>若要建立接聽程式

- 在應用程式中，建立一個繼承自 <xref:System.Diagnostics.TraceListener>，且命名為 `SimpleListener` 的類別。

     [!code-vb[VbVbalrMyApplicationLog#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#16)]

     基底類別所需的 <xref:System.Diagnostics.TraceListener.Write%2A> 和 <xref:System.Diagnostics.TraceListener.WriteLine%2A> 方法會呼叫 `MsgBox` 來顯示其輸入。

     <xref:System.Security.Permissions.HostProtectionAttribute> 屬性會套用至 <xref:System.Diagnostics.TraceListener.Write%2A> 和 <xref:System.Diagnostics.TraceListener.WriteLine%2A> 方法，使其屬性符合基底類別方法。 <xref:System.Security.Permissions.HostProtectionAttribute> 屬性可讓執行程式碼的主機決定讓程式碼公開主機保護同步處理。

    > [!NOTE]
    > <xref:System.Security.Permissions.HostProtectionAttribute> 屬性只適用於裝載通用語言執行平台以及實作主機保護的 Unmanaged 應用程式，例如 SQL Server。

為了確保 `My.Application.Log` 使用記錄檔接聽程式，您應該建立強式名稱的組件以包含記錄檔接聽程式。

下一個程序提供一些簡單的步驟，以建立強式名稱的記錄檔接聽程式組件。 如需詳細資訊，請參閱[建立和使用強式名稱的組件](../../../../standard/assembly/create-use-strong-named.md)。

#### <a name="to-strongly-name-the-log-listener-assembly"></a>若要建立強式名稱的記錄檔接聽程式組件

1. 在 **方案總管**中選取專案。 在 [**專案**] 功能表上，選擇 [**屬性**]。

2. 按一下 [ **簽署** ] 索引標籤。

3. 選取 [簽署組件]**** 方塊。

4. **\<New>** 從 [**選擇強式名稱金鑰**檔] 下拉式清單中選取。

     隨即開啟 [建立強式名稱金鑰]對話方塊。****

5. 在 [金鑰檔案名稱]方塊中，提供金鑰檔名稱。****

6. 將密碼輸入 [輸入密碼] 和 [確認密碼] 方塊。********

7. 按一下 [確定]。

8. 重建應用程式。

## <a name="adding-the-listener"></a>新增接聽程式

現在，組件已具有強式名稱，您必須決定接聽程式的強式名稱，以讓 `My.Application.Log` 使用您的記錄檔接聽程式。

具備強式名稱的類型格式如下：

\<type name>, \<assembly name>, \<version number>, \<culture>, \<strong name>

#### <a name="to-determine-the-strong-name-of-the-listener"></a>若要決定接聽程式的強式名稱

- 下列程式碼示範如何決定以強式名稱命名 `SimpleListener` 的類型名稱。

     [!code-vb[VbVbalrMyApplicationLog#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#17)]

     強式名稱的類型取決於您的專案而定。

使用強式名稱時，您可以將接聽程式新增至 `My.Application.Log` 記錄檔接聽程式集合。

#### <a name="to-add-the-listener-to-myapplicationlog"></a>若要將接聽程式新增至 My.Application.Log

1. 在方案總管中，以滑鼠右鍵按一下 app.config，並選擇 [開啟]。********

     -或-

     如果已有 app.config 檔案︰

    1. 在 [ **專案** ] 功能表中，選擇 [ **加入新項目**]。

    2. 在 [加入新項目] **** 對話方塊中，選擇 [應用程式組態檔] ****。

    3. 按一下 [新增] 。

2. 在 `<listeners>` 區段下，具有 `<source>` 屬性 "DefaultSource" 的 `name` 區段中找出 `<sources>` 區段。 `<sources>` 區段位於最上層 `<system.diagnostics>` 區段中的 `<configuration>` 區段內。

3. 將此項目新增至 `<listeners>` 區段：

    ```xml
    <add name="SimpleLog" />
    ```

4. 找出位於最上層 `<sharedListeners>` 區段中 `<system.diagnostics>` 區段的 `<configuration>` 區段。

5. 將此項目加入至該 `<sharedListeners>` 區段︰

    ```xml
    <add name="SimpleLog" type="SimpleLogStrongName" />
    ```

     將 `SimpleLogStrongName` 的值變更為接聽程式的強式名稱。

## <a name="see-also"></a>另請參閱

- <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=nameWithType>
- [使用應用程式記錄檔](working-with-application-logs.md)
- [作法：記錄例外狀況](how-to-log-exceptions.md)
- [作法：寫入記錄檔訊息](how-to-write-log-messages.md)
- [逐步解說：變更 My.Application.Log 寫入資訊的位置](walkthrough-changing-where-my-application-log-writes-information.md)
