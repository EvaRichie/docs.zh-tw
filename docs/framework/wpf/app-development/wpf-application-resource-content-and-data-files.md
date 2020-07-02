---
title: 應用程式資源、內容和資料檔案
description: 瞭解在 Windows Presentation Foundation （WPF）中設定、識別和使用應用程式資料檔案的特殊支援。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WPF application [WPF], files
- loose resources [WPF]
- content files [WPF]
- Site of Origin files [WPF]
- resource files [WPF]
- remote files [WPF]
- embedded resources [WPF]
- files [WPF]
- referencing application files [WPF]
- application development [WPF], files
- application management [WPF]
ms.assetid: 7ad2943b-3961-41d3-8fc6-1582d43f5d99
ms.openlocfilehash: 324b3eb922f0fd1d1d9ad00105a06a7fbdb8effd
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622857"
---
# <a name="wpf-application-resource-content-and-data-files"></a>WPF 應用程式資源、內容和資料檔案
Microsoft Windows 應用程式通常取決於包含非可執行資料的檔案，例如 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 影像、影片和音訊。 Windows Presentation Foundation （WPF）提供設定、識別和使用這些類型的資料檔案（稱為「應用程式資料檔案」）的特殊支援。 這項支援是以一組特定的應用程式資料檔案類型為中心，包括：  
  
- **資源檔**：編譯成可執行檔或程式庫 WPF 元件的資料檔案。  
  
- **內容**檔案：與可執行檔 WPF 元件具有明確關聯的獨立資料檔案。  
  
- **來源網站**檔案：與可執行檔 WPF 元件沒有關聯的獨立資料檔案。  
  
 這三種檔案類型之間的其中一個重要區別是資源檔和內容檔是建置階段的已知檔案；組件並明確知道這兩種檔案。 不過，對於原始網站檔案而言，元件可能完全不知道它們，或透過 pack 統一資源識別元（URI）參考進行隱含知識;如果是後者，則不保證來源參考的網站確實存在。  
  
 若要參考應用程式資料檔案，Windows Presentation Foundation （WPF）使用 Pack 統一資源識別元（URI）配置，在[WPF 的套件 uri](pack-uris-in-wpf.md)中有詳細說明）。  
  
 本主題描述何設定及使用應用程式資料檔案。  

<a name="Resource_Files"></a>
## <a name="resource-files"></a>資源檔  
 若應用程式資料檔案必須一律可供應用程式使用，確保可用性的唯一方法是將檔案編譯成應用程式的主要可執行檔組件或是應用程式的其中一個參考組件。 這種類型的應用程式資料檔案稱為「*資源檔*」。  
  
 應該使用資源檔的時機包括：  
  
- 您不需要在資源檔編譯成組件之後更新該檔案的內容。  
  
- 您想要透過減少檔案相依性數目的方式，簡化複雜的應用程式發佈程序。  
  
- 您的應用程式資料檔案必須是可當地語系化的（請參閱[WPF 全球化和當地語系化總覽](../advanced/wpf-globalization-and-localization-overview.md)）。  
  
> [!NOTE]
> 本節所述的資源檔與[XAML 資源](../../../desktop-wpf/fundamentals/xaml-resources-define.md)中所述的資源檔不同，而且不同于[管理應用程式資源（.net）](/visualstudio/ide/managing-application-resources-dotnet)中所述的內嵌或連結的資源。  
  
### <a name="configuring-resource-files"></a>設定資源檔  
 在 WPF 中，資源檔是包含在 Microsoft build engine （MSBuild）專案中做為專案的檔案 `Resource` 。  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ... >  
  ...  
  <ItemGroup>  
    <Resource Include="ResourceFile.xaml" />  
  </ItemGroup>  
  ...  
</Project>  
```  
  
> [!NOTE]
> 在 Visual Studio 中，您可以藉由將檔案新增至專案，並將其設定為，來建立資源檔 `Build Action` `Resource` 。  
  
 建立專案時，MSBuild 會將資源編譯成元件。  
  
### <a name="using-resource-files"></a>使用資源檔  
 若要載入資源檔，您可以呼叫 <xref:System.Windows.Application.GetResourceStream%2A> 類別的方法 <xref:System.Windows.Application> ，並傳遞識別所需資源檔的 pack URI。 <xref:System.Windows.Application.GetResourceStream%2A>傳回 <xref:System.Windows.Resources.StreamResourceInfo> 物件，它會將資源檔公開為 <xref:System.IO.Stream> ，並描述其內容類型。  
  
 例如，下列程式碼會示範如何使用 <xref:System.Windows.Application.GetResourceStream%2A> 載入 <xref:System.Windows.Controls.Page> 資源檔，並將它設定為 <xref:System.Windows.Controls.Frame> （）的內容 `pageFrame` ：  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadAPageResourceFileManuallyCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml.cs#loadapageresourcefilemanuallycode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadAPageResourceFileManuallyCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml.vb#loadapageresourcefilemanuallycode)]  
  
 當呼叫可 <xref:System.Windows.Application.GetResourceStream%2A> 讓您存取時 <xref:System.IO.Stream> ，您必須執行其他工作，將它轉換成您將設定它的屬性類型。 相反地，您可以讓 WPF <xref:System.IO.Stream> 使用程式碼，將資源檔直接載入至型別的屬性，以處理開啟和轉換。  
  
 下列範例顯示如何使用程式碼，將 <xref:System.Windows.Controls.Page> 直接載入 <xref:System.Windows.Controls.Frame> （ `pageFrame` ）。  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadPageResourceFileFromCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml.cs#loadpageresourcefilefromcode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadPageResourceFileFromCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml.vb#loadpageresourcefilefromcode)]  
  
 下列範例相當於前一個範例的標記對等用法。  
  
 [!code-xaml[WPFAssemblyResourcesSnippets#LoadPageResourceFileFromXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml#loadpageresourcefilefromxaml)]  
  
### <a name="application-code-files-as-resource-files"></a>應用程式程式碼檔案作為資源檔  
 您可以使用套件 Uri 來參考一組特殊的 WPF 應用程式程式碼檔案，包括視窗、頁面、非固定格式檔和資源字典。 例如，您可以 <xref:System.Windows.Application.StartupUri%2A?displayProperty=nameWithType> 使用一個 PACK URI 來設定屬性，該元件會參考您想要在應用程式啟動時載入的視窗或頁面。  
  
 [!code-xaml[WPFAssemblyResourcesSnippets#SetApplicationStartupURI](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/App.xaml#setapplicationstartupuri)]  
  
 當 MSBuild 專案中包含 XAML 檔案做為專案時，您可以執行此動作 `Page` 。  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ... >  
  ...  
  <ItemGroup>  
    <Page Include="MainWindow.xaml" />  
  </ItemGroup>  
  ...  
</Project>  
```  
  
> [!NOTE]
> 在 Visual Studio 中，您會在專案中加入新的 <xref:System.Windows.Window> 、、 <xref:System.Windows.Navigation.NavigationWindow> <xref:System.Windows.Controls.Page> 、 <xref:System.Windows.Documents.FlowDocument> 或 <xref:System.Windows.ResourceDictionary> ，而標記檔案的 `Build Action` 預設值為 `Page` 。  
  
 編譯具有專案的專案時 `Page` ，會將 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 專案轉換成二進位格式，並編譯成相關聯的元件。 因此，這些檔案可以比照一般資源檔的方式來使用。  
  
> [!NOTE]
> 如果檔案 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 設定為 `Resource` 專案，而且沒有程式碼後置檔案，則會將原始 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 編譯成元件，而不是原始的二進位版本 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 。  
  
<a name="Content_Files"></a>
## <a name="content-files"></a>內容檔  
 *內容*檔案會與可執行檔元件一起散發為鬆散檔案。 雖然這種檔案並未編譯成組件，但是編譯組件時使用的中繼資料會建立與每個內容檔的關聯。  
  
 如果應用程式需要一組特定的應用程式資料檔案，而您不想在更新這些檔案時重新編譯使用它們的組件，您應該使用內容檔。  
  
### <a name="configuring-content-files"></a>設定內容檔  
 若要將內容檔案加入至專案，必須將應用程式資料檔案包含為 `Content` 專案。 此外，由於內容檔案不會直接編譯到元件中，因此您必須設定 MSBuild `CopyToOutputDirectory` 中繼資料專案，以指定將內容檔案複製到與建立元件相對的位置。 如果您想要在每次建立專案時，將資源複製到組建輸出檔案夾，您可以 `CopyToOutputDirectory` 使用值來設定中繼資料 `Always` 元素。 否則，您可以使用值，確保只有最新版本的資源會複製到組建輸出檔案夾 `PreserveNewest` 。  
  
 以下顯示設定為內容檔的檔案；只有在將新版本的資源新增至專案時，這個內容檔才會複製到建置輸出資料夾。  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ... >  
  ...  
  <ItemGroup>  
    <Content Include="ContentFile.xaml">  
      <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>  
    </Content>  
  </ItemGroup>  
  ...  
</Project>  
```  
  
> [!NOTE]
> 在 Visual Studio 中，您可以藉由將檔案新增至專案並將其設定為，來建立內容檔案 `Build Action` `Content` ，並將其設定 `Copy to Output Directory` 為 `Copy always` （與相同 `Always` ）和 `Copy if newer` （與相同 `PreserveNewest` ）。  
  
 建立專案時， <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> 會將屬性編譯成每個內容檔案之元件的中繼資料。  
  
 `[assembly: AssemblyAssociatedContentFile("ContentFile.xaml")]`  
  
 的值 <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> 表示內容檔相對於專案中位置的路徑。 例如，如果內容檔案位於專案子資料夾中，則會將其他路徑資訊併入 <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> 值中。  
  
 `[assembly: AssemblyAssociatedContentFile("Resources/ContentFile.xaml")]`  
  
 此 <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> 值也是 [組建輸出] 資料夾中內容檔案的路徑值。  
  
### <a name="using-content-files"></a>使用內容檔  
 若要載入內容檔案，您可以呼叫 <xref:System.Windows.Application.GetContentStream%2A> 類別的方法 <xref:System.Windows.Application> ，並傳遞可識別所需內容檔案的 pack URI。 <xref:System.Windows.Application.GetContentStream%2A>傳回 <xref:System.Windows.Resources.StreamResourceInfo> 物件，它會將內容檔公開為 <xref:System.IO.Stream> ，並描述其內容類型。  
  
 例如，下列程式碼會示範如何使用 <xref:System.Windows.Application.GetContentStream%2A> 載入 <xref:System.Windows.Controls.Page> 內容檔案，並將它設定為 <xref:System.Windows.Controls.Frame> （）的內容 `pageFrame` 。  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadAPageContentFileManuallyCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml.cs#loadapagecontentfilemanuallycode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadAPageContentFileManuallyCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml.vb#loadapagecontentfilemanuallycode)]  
  
 當呼叫可 <xref:System.Windows.Application.GetContentStream%2A> 讓您存取時 <xref:System.IO.Stream> ，您必須執行其他工作，將它轉換成您將設定它的屬性類型。 相反地，您可以讓 WPF <xref:System.IO.Stream> 使用程式碼，將資源檔直接載入至型別的屬性，以處理開啟和轉換。  
  
 下列範例顯示如何使用程式碼，將 <xref:System.Windows.Controls.Page> 直接載入 <xref:System.Windows.Controls.Frame> （ `pageFrame` ）。  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadPageContentFileFromCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml.cs#loadpagecontentfilefromcode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadPageContentFileFromCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml.vb#loadpagecontentfilefromcode)]  
  
 下列範例相當於前一個範例的標記對等用法。  
  
 [!code-xaml[WPFAssemblyResourcesSnippets#LoadPageContentFileFromXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml#loadpagecontentfilefromxaml)]  
  
<a name="Site_of_Origin_Files"></a>
## <a name="site-of-origin-files"></a>來源網站檔  
 資源檔與一起散發的元件具有明確的關聯性，如所定義 <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> 。 但是在某些情況下，您可能想在組件和應用程式資料檔案之間建立隱含或不存在的關聯性，這些情況包括：  
  
- 在編譯時期，檔案不存在。  
  
- 在執行階段之前，您不知道組件需要哪些檔案。  
  
- 您不想在更新檔案時重新編譯其關聯的組件。  
  
- 應用程式使用大型的資料檔案，例如音訊和視訊，而您只想讓使用者自行選擇是否下載這些檔案。  
  
 您可以使用傳統的 URI 配置（例如和架構）來載入這些類型的檔案 `file:///` `http://` 。  
  
 [!code-xaml[WPFAssemblyResourcesSnippets#AbsolutePackUriFileHttpReferenceXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/AbsolutePackUriPage.xaml#absolutepackurifilehttpreferencexaml)]  
  
 不過， `file:///` 和配置 `http://` 需要您的應用程式具有完全信任。 如果您的應用程式是從網際網路或內部網路啟動的 XAML 瀏覽器應用程式（XBAP），而且它只會要求從那些位置啟動之應用程式所允許的許可權集，就只能從應用程式的來源網站（啟動位置）載入鬆散檔案。 這類檔案稱為「*來源網站*」檔案。  
  
 來源網站檔是部分信任應用程式的唯一選擇，但並不是只適用於部分信任應用程式。 完全信任應用程式可能還是需要載入它們在建置階段並不知道的應用程式資料檔案；雖然完全信任應用程式可以使用 file:///，但是應用程式資料檔案可能會安裝在應用程式組件的相同資料夾或子資料夾中。 在此情況下，使用來源網站參考比使用 file:/// 簡單，因為使用 file:/// 時，您必須找出檔案的完整路徑。  
  
> [!NOTE]
> 來源網站檔案不會使用用戶端電腦上的 XAML 瀏覽器應用程式（XBAP）進行快取，而內容檔案則是。 因此，只有在特別要求時，才會下載來源網站檔。 如果 XAML 瀏覽器應用程式（XBAP）應用程式有大型媒體檔案，將它們設定為「原始網站」檔案，表示初始應用程式啟動速度會更快，而且只會視需要下載檔案。  
  
### <a name="configuring-site-of-origin-files"></a>設定來源網站檔  
 如果您的原始網站檔案在編譯時期不存在或不明，您必須使用傳統部署機制，以確保在執行時間可使用所需的檔案，包括使用 `XCopy` 命令列程式或 Microsoft Windows Installer。  
  
 如果您在編譯時期知道您想要在來源網站上找到的檔案，但仍想要避免明確的相依性，您可以將這些檔案新增至 MSBuild 專案做為 `None` 專案。 如同內容檔案，您必須設定 MSBuild `CopyToOutputDirectory` 屬性，以指定將來源網站檔案複製到相對於所建立元件的位置，方法是指定 `Always` 值或 `PreserveNewest` 值。  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ... >  
  ...  
  <None Include="PageSiteOfOriginFile.xaml">  
    <CopyToOutputDirectory>Always</CopyToOutputDirectory>  
  </None>  
  ...  
</Project>  
```  
  
> [!NOTE]
> 在 Visual Studio 中，您可以藉由將檔案新增至專案，並將其設定為，來建立來源網站檔案 `Build Action` `None` 。  
  
 建立專案時，MSBuild 會將指定的檔案複製到組建輸出檔案夾。  
  
### <a name="using-site-of-origin-files"></a>使用來源網站檔  
 若要載入原始網站檔案，您可以呼叫類別的 <xref:System.Windows.Application.GetRemoteStream%2A> 方法 <xref:System.Windows.Application> ，並傳遞識別所需來源網站檔案的 pack URI。 <xref:System.Windows.Application.GetRemoteStream%2A>傳回 <xref:System.Windows.Resources.StreamResourceInfo> 物件，它會將來源網站檔案公開為 <xref:System.IO.Stream> ，並描述其內容類型。  
  
 例如，下列程式碼會示範如何使用 <xref:System.Windows.Application.GetRemoteStream%2A> 載入 <xref:System.Windows.Controls.Page> 原始網站檔案，並將它設定為 <xref:System.Windows.Controls.Frame> （）的內容 `pageFrame` 。  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadAPageSOOFileManuallyCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/SOOPage.xaml.cs#loadapagesoofilemanuallycode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadAPageSOOFileManuallyCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/SOOPage.xaml.vb#loadapagesoofilemanuallycode)]  
  
 當呼叫可 <xref:System.Windows.Application.GetRemoteStream%2A> 讓您存取時 <xref:System.IO.Stream> ，您必須執行其他工作，將它轉換成您將設定它的屬性類型。 相反地，您可以讓 WPF <xref:System.IO.Stream> 使用程式碼，將資源檔直接載入至型別的屬性，以處理開啟和轉換。  
  
 下列範例顯示如何使用程式碼，將 <xref:System.Windows.Controls.Page> 直接載入 <xref:System.Windows.Controls.Frame> （ `pageFrame` ）。  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadPageSOOFileFromCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/SOOPage.xaml.cs#loadpagesoofilefromcode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadPageSOOFileFromCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/SOOPage.xaml.vb#loadpagesoofilefromcode)]  
  
 下列範例相當於前一個範例的標記對等用法。  
  
 [!code-xaml[WPFAssemblyResourcesSnippets#LoadPageSOOFileFromXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/SOOPage.xaml#loadpagesoofilefromxaml)]  
  
<a name="Rebuilding_after_Changing_Build_Type"></a>
## <a name="rebuilding-after-changing-build-type"></a>在變更組建類型之後重建  
 在變更應用程式資料檔案的組建類型之後，您必須重建整個應用程式，以確認套用這些變更。 若您只建置應用程式，則不會套用變更。  
  
## <a name="see-also"></a>另請參閱

- [WPF 中的 Pack URI](pack-uris-in-wpf.md)
