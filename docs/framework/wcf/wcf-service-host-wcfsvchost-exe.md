---
title: WCF 服務主機 (WcfSvcHost.exe)
description: 使用 WCF 服務主機來裝載和測試您已執行的服務。 您可以使用 WCF 測試用戶端或您自己的用戶端來測試服務。
ms.date: 03/30/2017
ms.assetid: 8643a63d-a357-4c39-bd6c-cdfdf71e370e
ms.openlocfilehash: 2ac1d6318d8a82a82c08f38305ee6f92ad3f52a2
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90544592"
---
# <a name="wcf-service-host-wcfsvchostexe"></a>WCF 服務主機 (WcfSvcHost.exe)

Windows Communication Foundation (WCF) 服務主機 ( # A0) 可讓您啟動 Visual Studio 偵錯工具 (F5) ，以自動裝載和測試您已執行的服務。 然後，您可以使用 WCF 測試用戶端 ( # A0) 或您自己的用戶端來測試服務，以尋找並修正任何可能的錯誤。

## <a name="wcf-service-host"></a>WCF 服務主機

WCF 服務主機會列舉 WCF 服務專案中的服務、載入專案的設定，並為它找到的每個服務具現化主機。 此工具會透過 WCF 服務範本整合至 Visual Studio，並在您開始對專案進行程式化時叫用。

使用 WCF 服務主機，您可以在 WCF 服務程式庫專案中裝載 WCF 服務 (，) 不需要撰寫額外的程式碼，或在開發期間認可至特定的主機。

> [!NOTE]
> WCF 服務主機不支援部分信任。 如果您想要在部分信任中使用 WCF 服務，請不要使用 Visual Studio 中的 [WCF 服務程式庫] 專案範本來建立您的服務。 相反地，請選擇 WCF 服務網站範本，在 Visual Studio 中建立新的網站，此範本可以在支援 WCF 部分信任的 Web 服務器上裝載服務。

## <a name="project-types-hosted-by-wcf-service-host"></a>WCF 服務主機裝載的專案類型

WCF 服務主機可以裝載下列 WCF 服務程式庫專案類型： WCF 服務程式庫、連續工作流程服務程式庫、狀態機器工作流程服務程式庫和新聞訂閱服務程式庫。 WCF 服務主機也可以裝載這些服務，這些服務可以使用 [ **新增專案** ] 功能加入至服務程式庫專案。 這包括 WCF 服務、WF 狀態機器服務、WF 順序服務、XAML WF 狀態機器服務和 XAML WF 順序服務。

但是，您應該注意到，此工具無法協助您設定主機。 對於這項工作，您必須手動編輯 App.config 檔案。 此工具也不會驗證使用者定義的組態檔。

> [!CAUTION]
> 您不應該在生產環境中使用 WCF 服務主機來裝載服務，因為它不是針對此用途所設計。  WCF 服務主機不支援這類環境的可靠性、安全性和管理性需求。 請改用 IIS，因為它提供比較好的可靠性和監視功能，而且是一般慣用於裝載服務的解決方案。 完成服務的開發之後，您應該將服務從 WCF 服務主機遷移至 IIS。

## <a name="scenarios-for-using-wcf-service-host-inside-visual-studio"></a>在 Visual Studio 內使用 WCF 服務主機的案例

下表列出 [ **命令列引數** ] 對話方塊中的所有參數，您可以在 Visual Studio 的 [ **方案瀏覽器** ] 中，以滑鼠右鍵按一下專案，選取 [ **屬性**]，然後選取 [ **調試** 程式] 索引標籤並按一下 [ **啟動專案**]，即可找到此對話方塊。 這些參數在設定 WCF 服務主機時會很有用。

|參數|意義|
|---------------|-------------|
|`/client`|選擇性參數，會指定要在裝載服務後執行之可執行檔的路徑。 這會在裝載之後啟動 WCF 測試用戶端。|
|`/clientArg`|會指定字串做為傳遞給自訂用戶端應用程式的引數。|
|`/?`|顯示說明文字。|

#### <a name="using-wcf-test-client"></a>使用 WCF 測試用戶端

建立新的 WCF 服務專案並按下 F5 啟動偵錯工具之後，WCF 服務主機會開始裝載它在您的專案中找到的所有服務。 WCF 測試用戶端會自動開啟並顯示設定檔中定義的服務端點清單。 您可以從主視窗中測試參數並叫用服務。

若要確定使用 WCF 測試用戶端，請在 [ **方案瀏覽器** ] 的 [Visual Studio 中，以滑鼠右鍵按一下您的專案，選取 [ **屬性**]，然後選取 [ **Debug** ] 索引標籤按一下 [ **起始專案** ]，並確定下列專案出現在 [ **命令列引數** ] 對話方塊中。

`/client:WcfTestClient.exe`

#### <a name="using-a-custom-client"></a>使用自訂用戶端

若要使用自訂用戶端，請在 [**方案瀏覽器**] 的 [Visual Studio] 中，以滑鼠右鍵按一下您的專案，**選取 [** **屬性**]，然後選取 [按一下 [**開始專案**]，然後 `/client` 在 [**命令列引數**] 對話方塊中編輯參數，以指向您的自訂用戶端，如下列範例所示。

`/client:"path/CustomClient.exe"`

當您按下 F5 重新開機服務時，WCF 服務主機會在您啟動偵錯工具時自動啟動您的自訂用戶端。

您也可以使用 `/clientArg:` 參數，指定字串做為傳遞給自訂用戶端應用程式的引數，如下列範例所示。

`/client:"path/CustomClient.exe" /clientArg:"arguments that are passed to Client"`

例如，如果您使用新聞訂閱服務程式庫範本，就可以使用下列命令列引數：

`/client:iexplore.exe /clientArgs:http://localhost:8731/Design_Time_Addresses/Feed1/`

#### <a name="specifying-no-client"></a>不指定任何用戶端

若要指定在 WCF 服務裝載之後不會使用任何用戶端，請在 [ **方案瀏覽器** ] 的 [Visual Studio 中，以滑鼠右鍵按一下您的專案，選取 [ **屬性**]，然後選取 [ **調試** 程式]按一下 [ **開始專案** ]，並將 [ **命令列引數** ] 對話方塊保留空白。

#### <a name="using-a-custom-host"></a>使用自訂主機

若要使用自訂主機，請在 [ **方案瀏覽器** ] 的 [Visual Studio 中，以滑鼠右鍵按一下您的專案，選取 [ **屬性**]，然後選取 [ **Debug** ]按一下 [ **啟動外部程式** ]，然後輸入自訂主機的完整路徑。 您也可以使用 [ **命令列引數** ] 對話方塊來指定要傳遞至主機的引數。

## <a name="wcf-service-host-user-interface"></a>WCF 服務主機使用者介面

當您一開始在 Visual Studio) 內按 F5 叫用 WCF 服務主機 (時，[ **Wcf 服務主機** ] 視窗會自動開啟。 當 WCF 服務主機正在執行時，程式的圖示會出現在通知區域中。 按兩下圖示以開啟 [ **WCF 服務主機** ] 視窗

服務裝載期間發生錯誤時，[WCF 服務主機] 對話方塊會開啟以顯示相關的資訊。

**WCF 服務主機**主視窗包含兩個功能表：

- **File**：包含 **Close** 和 **Exit** 命令。 當您按一下 [ **關閉**] 時，[ **WCF 服務主機** ] 對話方塊會關閉，但服務會繼續裝載。 當 **您按一下 [** 結束] 時，WCF 服務主機也會關閉。 這還會停止所有裝載的服務。

- **Help**：包含包含版本資訊的 **About** 命令。 它也包含可開啟說明檔的 **help** 命令。

主要的 **WCF 服務** 主視窗包含兩個區域：

- 第一個區域是 **服務**。 其中包含一份顯示所有服務基本資訊的清單。 這些資訊包括：

  - **服務**：列出所有服務。

  - **狀態**：列出服務的狀態。 有效的值為「已啟動」、「已停止」和「錯誤」。

  - **中繼資料位址**：顯示服務的中繼資料位址。

- 第二個區域是 **額外的資訊**。 當您在 **服務** 區域中選取特定的服務線時，它會顯示服務狀態的詳細說明。 如果狀態為「錯誤」，您就可以在螢幕上檢視完整的錯誤訊息。

## <a name="stopping-wcf-service-host"></a>停止 WCF 服務主機

您可以透過下列四種方式來關閉 WCF 服務主機：

- 在 Visual Studio 中停止調試會話。

- 從 [ **WCF 服務主機**] 視窗**的 [檔案**]**功能表中選取**[結束]。

- 從 **[** 系統通知] 區域中的 [WCF 服務主機系統匣] 圖示的內容功能表選取 [結束]。

- 結束 WCF 測試用戶端（如果正在使用）。

## <a name="using-service-host-without-administrator-privilege"></a>在沒有系統管理員權限的情況下使用服務主機

若要讓沒有系統管理員許可權的使用者開發 WCF 服務，安裝 Visual Studio 期間會為命名空間 "" 建立 ACL (存取控制清單) http://+:8731/Design_Time_Addresses 。 ACL 會設定為 (UI)，其中包含已登入電腦的所有互動使用者。 系統管理員可以在這個 ACL 中新增或移除使用者，或是開啟其他埠。此 ACL 可讓使用者在不授與系統管理員許可權的情況下，使用 WCF Service Auto Host ( # A0) 。

您可以使用 Windows Vista 中的 [netsh.exe] 工具，以提高許可權的系統管理員帳戶修改存取權。 下列是使用 netsh.exe 的範例。

```console
netsh http add urlacl url=http://+:8001/MyService user=<domain>\<user>
```

如需 netsh.exe 的詳細資訊，請參閱「[如何使用 Netsh.exe 工具和命令列參數](/previous-versions/tn-archive/bb490939(v=technet.10))」。

## <a name="see-also"></a>另請參閱

- [WCF 測試用戶端 (WcfTestClient.exe)](wcf-test-client-wcftestclient-exe.md)
