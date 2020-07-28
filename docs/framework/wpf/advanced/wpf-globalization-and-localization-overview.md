---
title: 全球化和當地語系化總覽
description: 瞭解 Windows Presentation Foundation 的當地語系化和全球化，包括自動版面配置、附屬元件和當地語系化的屬性。
ms.date: 03/30/2017
helpviewer_keywords:
- globalization [WPF], about globalization
- localization [WPF], about localization
ms.assetid: 56e5a5c8-6c96-4d19-b8e1-a5be1dc564af
ms.openlocfilehash: 9a54ce2c265b989f99383ff9cdec961c80dd655c
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87168289"
---
# <a name="wpf-globalization-and-localization-overview"></a>WPF 全球化和當地語系化概觀

當您將產品的可用性限制為只有一種語言時，您可以將潛在客戶基座限制為全球7500000000擴展的一小部分。 如果您想要全球對象都可以使用應用程式，則具成本效益的產品當地語系化是更多客戶可以使用的一種最佳且最經濟的方法。

本總覽介紹中的全球化和當地語系化 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 。 全球化是在多個位置執行之應用程式的設計和開發。 例如，全球化支援不同文化特性中使用者的當地語系化使用者介面和地區資料。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]提供全球化設計功能，包括自動版面配置、附屬元件，以及當地語系化屬性和批註。

當地語系化會將應用程式資源翻譯為應用程式所支援之特定文化特性的當地語系化版本。 當您在中進行當地語系化時 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ，會使用命名空間中的 api <xref:System.Windows.Markup.Localizer> 。 這些 Api 會增強[LocBaml 工具範例](https://github.com/microsoft/WPF-Samples/tree/master/Tools/LocBaml)命令列工具。 如需如何建立和使用 LocBaml 的相關資訊，請參閱[將應用程式當地語系化](how-to-localize-an-application.md)。

## <a name="best-practices-for-globalization-and-localization-in-wpf"></a>WPF 中的全球化和當地語系化最佳做法

您可以 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 遵循本節所提供的 UI 設計和當地語系化相關秘訣，來充分利用內建的全球化和當地語系化功能。

### <a name="best-practices-for-wpf-ui-design"></a>WPF UI 設計最佳做法

當您設計以為 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 基礎時，請考慮採用 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 下列最佳作法：

- 寫入您 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ，避免 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 在程式碼中建立。 當您使用建立時 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ，您可以透過內建的當地語系化 api 加以公開。

- 避免使用絕對位置和固定大小來配置內容;相反地，請使用相對或自動調整大小。

  - 使用 <xref:System.Windows.Window.SizeToContent%2A> ，並將寬度和高度設定為 `Auto` 。

  - 請避免使用 <xref:System.Windows.Controls.Canvas> 來配置 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 。

  - 使用 <xref:System.Windows.Controls.Grid> 及其大小分享功能。

- 因為當地語系化文字通常需要更多空間，所以請在邊界提供額外空間。 額外空間可放置可能突出的字元。

- <xref:System.Windows.Controls.TextBlock.TextWrapping%2A>在上啟用 <xref:System.Windows.Controls.TextBlock> 以避免裁剪。

- 設定 `xml:lang` 屬性。 此屬性描述特定專案及其子專案的文化特性。 這個屬性的值會變更中數個功能的行為 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 。 例如，它會變更斷字、拼字檢查、數字替代、複雜指令碼形成和字型遞補的行為。 如需[在 XAML 中設定 xml： Lang 處理](../../../desktop-wpf/xaml-services/xml-language-handling.md)的詳細資訊，請參閱[WPF 的全球化](globalization-for-wpf.md)。

- 建立自訂的複合字型，以取得針對不同語言使用之字型的更佳控制。 根據預設，會 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 在您的 Windows\Fonts 目錄中使用 GlobalUserInterface 複合字型。

- 當您建立的導覽應用程式可能會以由右至左格式呈現文字的文化特性中進行當地語系化時，請明確設定 <xref:System.Windows.FlowDirection> 每個頁面的，以確保頁面不會繼承 <xref:System.Windows.FlowDirection> 自 <xref:System.Windows.Navigation.NavigationWindow> 。

- 當您建立裝載于瀏覽器外部的獨立導覽應用程式時，請將 <xref:System.Windows.Application.StartupUri%2A> 初始應用程式的設定為， <xref:System.Windows.Navigation.NavigationWindow> 而不是頁面（例如 `<Application StartupUri="NavigationWindow.xaml">` ）。 這項設計可讓您變更 <xref:System.Windows.FlowDirection> 視窗和導覽列的。 如需詳細資訊和範例，請參閱[全球化首頁範例](https://github.com/microsoft/WPF-Samples/tree/master/Globalization%20and%20Localization/GlobalizationHomepage)。

### <a name="best-practices-for-wpf-localization"></a>WPF 當地語系化最佳做法

當您以當地語系化 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 為基礎的應用程式時，請考慮執行下列最佳作法：

- 使用當地語系化批註為當地語系化人員提供額外的內容。

- 使用當地語系化屬性來控制當地語系化，而不是選擇性地省略 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 元素上的屬性。 如需詳細資訊，請參閱[當地語系化屬性和批註](localization-attributes-and-comments.md)。

- 使用 `msbuild -t:updateuid` 和 `-t:checkuid` 來新增和檢查 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 中的屬性 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 。 使用 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 屬性來追蹤開發和當地語系化之間的變更。 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A>屬性可協助您將新的開發變更當地語系化。 如果您手動將 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 屬性加入至 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] ，則工作通常單調乏味且較不精確。

  - <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A>開始當地語系化之後，請勿編輯或變更屬性。

  - 請勿使用重複 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 的屬性（當您使用複製並貼上命令時，請記住此提示）。

  - 設定 `UltimateResourceFallback` AssemblyInfo 中的位置。 \* 指定適當的回溯語言（例如 `[assembly: NeutralResourcesLanguage("en-US",   UltimateResourceFallbackLocation.Satellite)]` ）。

    如果您決定藉由省略專案檔中的標記，將來源語言包含在主要元件中 `<UICulture>` ，請將 `UltimateResourceFallback` 位置設定為主要元件，而不是附屬元件（例如 `[assembly: NeutralResourcesLanguage("en-US", UltimateResourceFallbackLocation.MainAssembly)]` ）。

## <a name="localize-a-wpf-application"></a>將 WPF 應用程式當地語系化

當您將 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 應用程式當地語系化時，您會有數個選項。 例如，您可以將應用程式中可當地語系化的資源系結至 XML 檔案、將可當地語系化的文字儲存在 resx 資料表中，或讓您的當地語系化人員使用檔案 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 。 本節描述使用 BAML 形式 XAML 的當地語系化工作流程，其提供數個優點：

- 您可以在建立之後當地語系化。

- 您可以使用舊版 BAML 格式的當地語系化，以較舊版本的 xaml 更新為新版本的 BAML 形式的 XAML，以便在您開發的同時進行當地語系化。

- 您可以在編譯時期驗證原始來源專案和語義，因為 BAML 形式的 XAML 是的編譯形式 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 。

### <a name="localization-build-process"></a>當地語系化建置程序

當您開發 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 應用程式時，當地語系化的組建流程如下所示：

- 開發人員會建立並全球化 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 應用程式。 在開發人員所設定的專案檔中 `<UICulture>en-US</UICulture>` ，當編譯應用程式時，就會產生語言中性的主要元件。 此組件具有包含所有可當地語系化資源的附屬 .resources.dll 檔案。 （選擇性）您可以保留主要元件中的來源語言，因為我們的當地語系化 Api 支援從主要元件進行解壓縮。

- 當檔案編譯成組建時， [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 會轉換成 XAML 的 BAML 形式。 文化特性中性 `MyDialog.exe` 和區分文化特性（英文）檔案 `MyDialog.resources.dll` 會發行給英文的客戶。

### <a name="localization-workflow"></a>當地語系化工作流程

當地語系化程式會在未當地語系化檔案建立後開始 `MyDialog.resources.dll` 。 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]原始中的專案和屬性 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 會使用中的 api，從 BAML 形式的 XAML 解壓縮至索引鍵/值組 <xref:System.Windows.Markup.Localizer> 。 當地語系化人員會使用鍵值組來當地語系化應用程式。 當地語系化完成之後，即可從新值產生新的 .resource.dll。

索引鍵/值組的索引鍵是 `x:Uid` 由開發人員在原始中放置的值 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 。 這些 `x:Uid` 值可讓 API 追蹤和合併在當地語系化期間，開發人員和當地語系化工具之間發生的變更。 例如，如果開發人員在完成當地語系化 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 之後變更，則您可以合併開發變更與已完成的當地語系化工作，以降低轉譯工作的最小需求。

下圖顯示根據 BAML 形式之 XAML 的一般當地語系化工作流程。 此圖表假設開發人員以英文撰寫應用程式。 開發人員會建立和全球化 WPF 應用程式。 在開發人員所設定的專案檔中 `<UICulture>en-US</UICulture>` ，在組建上會產生語言中性主要元件，其中包含所有可當地語系化資源的附屬 .resources.dll。 或者，有人保持主要組件中的來源語言，因為 WPF 當地語系化 API 支援從主要組件進行擷取。 建置程序之後，XAML 會編譯到 BAML。 與文化特性無關的 MyDialog.exe.resources.dll 會傳送給英語系的客戶。

![顯示當地語系化工作流程的圖表。](./media/wpf-globalization-and-localization-overview/localization-workflow.png)

![顯示未當地語系化工作流程的圖表。](./media/wpf-globalization-and-localization-overview/unlocalized-workflow.png)

## <a name="examples-of-wpf-localization"></a>WPF 當地語系化範例

本節包含當地語系化應用程式的範例，可協助您瞭解如何建立和當地語系化 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 應用程式。

### <a name="run-dialog-box-example"></a>執行對話方塊範例

下列圖形顯示 [**執行**] 對話方塊範例的輸出。

**英語：**

![顯示英文 [執行] 對話方塊的螢幕擷取畫面。](./media/wpf-globalization-and-localization-overview/run-dialog-box-english.png)

**德語：**

![顯示 [德文執行] 對話方塊的螢幕擷取畫面。](./media/wpf-globalization-and-localization-overview/run-dialog-box-german.png)

**設計全域執行對話方塊**

這個範例會使用和來產生 [**執行**] 對話方塊 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 。 這個對話方塊相當於可從 Microsoft Windows [開始] 功能表取得的 [**執行**] 對話方塊。

建立全域對話方塊的一些重點如下︰

**自動版面配置**

*在 Window1.xaml 中：*

`<Window SizeToContent="WidthAndHeight">`

前一個 Window 屬性會根據內容的大小來自動調整視窗大小。 此屬性會防止視窗中在當地語系化因大小增加而裁切內容；內容在當地語系化後大小減少時，它也會移除不必要的空間。

`<Grid x:Uid="Grid_1">`

<xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A>需要有屬性， [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 當地語系化 api 才能正常運作。

當地語系化 Api 會使用它們 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 來追蹤開發和當地語系化之間的變更 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 。 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A>屬性可讓您將較新的版本 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 與的舊版當地語系化合併 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 。 您可以藉 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 由 `msbuild -t:updateuid RunDialog.csproj` 在命令 shell 中執行來新增屬性。 這是建議的新增屬性方法， <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 因為手動新增它們通常相當耗時且較不精確。 您可以藉由執行來檢查 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 屬性是否已正確設定 `msbuild -t:checkuid RunDialog.csproj` 。

[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]是使用控制項來結構化 <xref:System.Windows.Controls.Grid> ，這是在中利用自動版面配置的實用控制項 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 。 請注意，對話方塊分成三個資料列和五個資料行。 不是其中一個資料列和資料行定義具有固定的大小;因此，位於 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 每個資料格中的元素可在當地語系化期間適應大小的增加和減少。

[!code-xaml[GlobalizationRunDialog#GridColumnDef](~/samples/snippets/csharp/VS_Snippets_Wpf/GlobalizationRunDialog/CS/Window1.xaml#gridcolumndef)]

**開啟的：** 標籤和所放置的前兩個數據行會 <xref:System.Windows.Controls.ComboBox> 使用總寬度的 10% [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 。

[!code-xaml[GlobalizationRunDialog#GridColumnDef2](~/samples/snippets/csharp/VS_Snippets_Wpf/GlobalizationRunDialog/CS/Window1.xaml#gridcolumndef2)]

請注意，此範例使用的共用調整大小功能 <xref:System.Windows.Controls.Grid> 。 最後三個數據行將其本身放在相同的中，即可利用此功能 <xref:System.Windows.Controls.DefinitionBase.SharedSizeGroup%2A> 。 因為其中一個預期來自屬性名稱，所以這可讓資料行共用相同的大小。 所以當「流覽 ...」會當地語系化為較長的字串 "Durchsuchen ... ..."，所有按鈕會以寬度成長，而不會有小型的「確定」按鈕和不太大的「Durchsuchen ... ...」button.

**xml： lang**

`xml:lang="en-US"`

請注意， [XAML 中的 xml： Lang 處理](../../../desktop-wpf/xaml-services/xml-language-handling.md)會放在的根項目中 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 。 此屬性描述所指定項目的文化特性和其子項目。 這個值是由中的數個功能所使用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ，而且應該在當地語系化期間適當地變更。 此值可變更使用何種語言字典來進行斷字和拼字檢查。 它也會影響顯示的位數，以及字型遞補系統如何選取要使用的字型。 最後，此屬性會影響數字顯示方式，以及使用複雜指令碼所撰寫之文字的形成方式。 預設值是 "en-US"。

**建置附屬資源組件**

*在 .csproj 中：*

編輯檔案 `.csproj` ，並將下列標記新增至無條件 `<PropertyGroup>` ：

`<UICulture>en-US</UICulture>`

請注意加入 `UICulture` 值。 當此值設定為有效值（ <xref:System.Globalization.CultureInfo> 例如 en-us）時，建立專案將會產生附屬元件，其中包含所有可當地語系化的資源。

`<Resource Include="RunIcon.JPG">`

`<Localizable>False</Localizable>`

`</Resource>`

不 `RunIcon.JPG` 需要當地語系化，因為所有文化特性的外觀應該都相同。 `Localizable`設定為， `false` 因此它會保留在語言中性主要元件中，而不是附屬元件。 所有 noncompilable 資源的預設值都會 `Localizable` 設定為 `true` 。

**將執行對話方塊當地語系化**

**剖析**

建置應用程式之後，將它當地語系化的第一個步驟是剖析附屬組件的可當地語系化資源。 基於本主題的目的，請使用可在[LocBaml 工具範例](https://github.com/microsoft/WPF-Samples/tree/master/Tools/LocBaml)中找到的範例 LocBaml 工具。 請注意，LocBaml 只是一種範例工具，旨在協助您開始建置符合當地語系化程序的當地語系化工具。 使用 LocBaml，執行下列來剖析： **LocBaml/parse RunDialog.resources.dll/out：** 產生 "RunDialog.resources.dll.CSV" 檔案。

**當地語系化**

使用支援 Unicode 的慣用 CSV 編輯器，才能編輯這個檔案。 篩選出當地語系化分類為 "None" 的所有項目。 您應該會看到下列項目：

|資源索引鍵|當地語系化分類|值|
|-|-|-|
|Button_1:System.Windows.Controls.Button.$Content|按鈕|[確定]|
|Button_2:System.Windows.Controls.Button.$Content|按鈕|取消|
|Button_3:System.Windows.Controls.Button.$Content|按鈕|瀏覽...|
|ComboBox_1:System.Windows.Controls.ComboBox.$Content|ComboBox||
|TextBlock_1:System.Windows.Controls.TextBlock.$Content|Text|輸入程式、資料夾、文件或網際網路資源的名稱，Windows 會自動開啟。|
|TextBlock_2:System.Windows.Controls.TextBlock.$Content|Text|未處理：|
|Window_1:System.Windows.Window.Title|標題|執行|

將應用程式當地語系化為德文需要下列翻譯︰

|資源索引鍵|當地語系化分類|值|
|-|-|-|
|Button_1:System.Windows.Controls.Button.$Content|按鈕|[確定]|
|Button_2:System.Windows.Controls.Button.$Content|按鈕|Abbrechen|
|Button_3:System.Windows.Controls.Button.$Content|按鈕|Durchsuchen…|
|ComboBox_1:System.Windows.Controls.ComboBox.$Content|ComboBox||
|TextBlock_1:System.Windows.Controls.TextBlock.$Content|Text|Geben Sie den Namen eines Programms, Ordners, Dokuments oder einer Internetresource an.|
|TextBlock_2:System.Windows.Controls.TextBlock.$Content|Text|開啟：|
|Window_1:System.Windows.Window.Title|標題|執行|

**Generate**

當地語系化的最後一個步驟包括建立新的當地語系化附屬組件。 使用下列 LocBaml 命令，即可完成這項作業：

**LocBaml.exe /generate RunDialog.resources.dll /trans:RunDialog.resources.dll.CSV /out: . /cul:de-DE**

在德文視窗上，如果此 resources.dll 放在主要元件旁的解除鎖定資料夾中，此資源將會自動載入，而不是 en-us 資料夾中的。 如果您沒有德文版的 Windows 來進行測試，請將文化特性設定為您所使用的任何 Windows 文化特性（例如， `en-US` ），並取代原始的資源 DLL。

**附屬資源載入**

|MyDialog.exe|en-US\MyDialog.resources.dll|de-DE\MyDialog.resources.dll|
|------------------|------------------------------------|------------------------------------|
|程式碼|附屬資源 BAML|當地語系化 BAML|
|文化特性中性資源|英文的其他資源|當地語系化為德文的其他資源|

.NET 會根據應用程式的，自動選擇要載入的附屬資源元件 <xref:System.Threading.Thread.CurrentUICulture%2A?displayProperty=nameWithType> 。 這會預設為 Windows 作業系統的文化特性。 如果您使用德文的 Windows，則會載入*de-DE\MyDialog.resources.dll*檔案。 如果您使用的是英文 Windows，則會載入*en-US\MyDialog.resources.dll*檔案。 您可以 `NeutralResourcesLanguage` 在專案的*AssemblyInfo*檔中指定屬性，以設定應用程式的終極回溯資源。 例如，如果您指定：

`[assembly: NeutralResourcesLanguage("en-US", UltimateResourceFallbackLocation.Satellite)]`

然後，如果下列兩個檔案都無法使用，則會將*en-US\MyDialog.resources.dll*檔案用於德文視窗： *de-DE\MyDialog.resources.dll*或*de\MyDialog.resources.dll*。

### <a name="microsoft-saudi-arabia-homepage"></a>Microsoft Saudi Arabia 首頁

下圖顯示英文和阿拉伯文首頁。 如需產生這些圖形的完整範例，請參閱[全球化首頁範例](https://github.com/microsoft/WPF-Samples/tree/master/Globalization%20and%20Localization/GlobalizationHomepage)。

**英語：**

![顯示英文首頁的螢幕擷取畫面。](./media/wpf-globalization-and-localization-overview/english-home-page-sample.jpg)

**阿拉伯文：**

![顯示阿拉伯文首頁的螢幕擷取畫面。](./media/wpf-globalization-and-localization-overview/arabic-home-page-sample.jpg)

### <a name="designing-a-global-microsoft-home-page"></a>設計全域 Microsoft 首頁

這個模擬的 Microsoft Saudi Arabia 網站說明針對 RightToLeft 語言所提供的全球化功能。 希伯來文和阿拉伯文這類語言具有由右至左的讀取順序，因此的配置 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 通常必須與以由左至右的語言（例如英文）完全不同。 從由左至右語言當地語系化為由右至左語言 (反之亦然) 可能相當困難。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 設計成讓這類當地語系化更為簡單。

**FlowDirection**

*Homepage.xaml：*

[!code-xaml[GlobalizationHomepage#Homepage](~/samples/snippets/csharp/VS_Snippets_Wpf/GlobalizationHomepage/CS/Homepage.xaml#homepage)]

請注意 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 上的屬性 <xref:System.Windows.Controls.Page> 。 將這個屬性變更為將會變更及其子專案的，如此一來，就能將這個的配置轉換 <xref:System.Windows.FlowDirection.RightToLeft> 成由 <xref:System.Windows.FrameworkElement.FlowDirection%2A> <xref:System.Windows.Controls.Page> [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 阿拉伯文使用者所預期的由右至左。 您可以在任何專案上指定明確的來覆寫繼承行為 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 。 <xref:System.Windows.FrameworkElement.FlowDirection%2A>屬性可在任何 <xref:System.Windows.FrameworkElement> 或檔相關元素上使用，而且具有的隱含值 <xref:System.Windows.FlowDirection.LeftToRight> 。

請注意，當根變更時，背景漸層筆刷會正確翻轉 <xref:System.Windows.FrameworkElement.FlowDirection%2A> ：

**FlowDirection="LeftToRight"**

![螢幕擷取畫面，顯示從左至右的漸層流程。](./media/wpf-globalization-and-localization-overview/gradient-flow-left-right.png)

**FlowDirection="RightToLeft"**

![顯示由右至左的漸層流程的螢幕擷取畫面。](./media/wpf-globalization-and-localization-overview/gradient-flow-right-left.png)

**避免面板和控制項使用固定維度**

請看一下首頁。 xaml，請注意，除了在頂端指定的固定寬度和高度外 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] <xref:System.Windows.Controls.DockPanel> ，沒有其他固定的維度。 請避免使用固定維度，防止裁剪長度超過來源文字的當地語系化文字。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 面板和控制項將會根據所含的內容來自動調整大小。 大部分的控制項也都有您可以設定以進行更多控制的最小和最大維度（例如，MinWidth = "20"）。 使用 <xref:System.Windows.Controls.Grid> ，您也可以使用 ' \* ' （例如 `Width="0.25*"` ），或使用其資料格大小共用功能來設定相對的寬度和高度。

**當地語系化註解**

在許多情況下，內容可能會模稜兩可，而不容易翻譯。 開發人員或設計人員可以透過當地語系化註解來提供額外內容和註解。 例如，下列批註說明字元 ' &#124; ' 的使用方式。

[!code-xaml[GlobalizationHomepage#LocalizationComment](~/samples/snippets/csharp/VS_Snippets_Wpf/GlobalizationHomepage/CS/Homepage.xaml#localizationcomment)]

此批註會與 TextBlock_1 的內容相關聯，而且在 LocBaml 工具的情況下（請參閱[當地語系化應用程式](how-to-localize-an-application.md)），它可以在輸出 .csv 檔案中 TextBlock_1 資料列的第6個數據行中看到：

|資源索引鍵|類別|可讀取|可修改|註解|值|
|-|-|-|-|-|-|
|TextBlock_1:System.Windows.Controls.TextBlock.$Content|Text|TRUE|TRUE|此字元是當成裝飾規則使用。|&#124;|

使用下列語法，可以放入任何項目之內容或屬性的註解︰

[!code-xaml[GlobalizationHomepage#LocalizationCommentsProp](~/samples/snippets/csharp/VS_Snippets_Wpf/GlobalizationHomepage/CS/Homepage.xaml#localizationcommentsprop)]

**當地語系化屬性**

開發人員或當地語系化管理員通常需要控制當地語系化人員可以讀取和修改的內容。 例如，您可能不想要當地語系化人員翻譯公司名稱或法律用語。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]提供屬性，可讓您設定專案內容或屬性的可讀性、可修改性和分類，而您的當地語系化工具可以用來鎖定、隱藏或排序元素。 如需詳細資訊，請參閱 <xref:System.Windows.Localization.Attributes%2A>。 基於此範例的目的，LocBaml 工具只會輸出這些屬性的值。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控制項都會有這些屬性的預設值，但您可以覆寫它們。 例如，下列範例會覆寫的預設當地語系化屬性 `TextBlock_1` ，並將內容設定為可讀取但無法修改的當地語系化。

[!code-xaml[LocalizationComAtt#LocalizationAttributes](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizationComAtt/CSharp/Attributes.xaml#localizationattributes)]

除了 [可讀性] 和 [可修改性] 屬性之外， [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 還提供通用 UI 類別的列舉（ <xref:System.Windows.LocalizationCategory> ），可用來為當地語系化人員提供更多的內容。 您 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 也可以在中覆寫平臺控制項的預設類別 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ：

[!code-xaml[LocalizationComAtt#LocalizationAttributesOverridden](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizationComAtt/CSharp/Attributes.xaml#localizationattributesoverridden)]

所提供的預設當地語系化屬性 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 也可以透過程式碼覆寫，因此您可以正確地為自訂控制項設定正確的預設值。 例如：

```csharp
[Localizability(Readability = Readability.Readable, Modifiability=Modifiability.Unmodifiable, LocalizationCategory.None)]
public class CorporateLogo : TextBlock
{
    // ...
}
```

在中設定的每個實例屬性， [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 會優先于在自訂控制項上的程式碼中設定的值。 如需屬性和批註的詳細資訊，請參閱[當地語系化屬性和批註](localization-attributes-and-comments.md)。

**字型遞補和複合字型**

如果您指定的字型不支援指定的「點」範圍，則 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 會自動切換為使用位於您 Windows\Fonts 目錄中的全域使用者介面的 compositefont。 複合字型的執行方式就像任何其他字型一樣，而且可以藉由設定元素的 `FontFamily` （例如，）來明確地使用 `FontFamily="Global User Interface"` 。 建立您自己的複合字型並指定要用於特定字碼指標範圍和語言的字型，即可指定自己的字型遞補喜好設定。

如需複合字型的詳細資訊，請參閱 <xref:System.Windows.Media.FontFamily> 。

**將 Microsoft 首頁當地語系化**

您可以遵循「執行對話方塊」範例中的相同步驟，將此應用程式當地語系化。 您可以在[全球化首頁範例](https://github.com/microsoft/WPF-Samples/tree/master/Globalization%20and%20Localization/GlobalizationHomepage)中，取得適用于阿拉伯文的當地語系化 .csv 檔案。
