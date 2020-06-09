---
title: Windows Presentation Foundation 用戶端中的資料繫結
ms.date: 03/30/2017
ms.assetid: bb8c8293-5973-4aef-9b07-afeff5d3293c
ms.openlocfilehash: fe7b1934fa2abfa8d2f812caca2363c1cc603d1a
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84602605"
---
# <a name="data-binding-in-a-windows-presentation-foundation-client"></a>Windows Presentation Foundation 用戶端中的資料繫結
這個範例示範使用 Windows Presentation Foundation (WPF) 用戶端中的資料繫結。 此範例會使用 Windows Communication Foundation （WCF）服務，隨機產生專輯陣列以傳回用戶端。 每張專輯各有名稱、價格和曲目表。 曲目有名稱和時間長度。 服務所傳回的資訊會自動系結至 Windows Presentation Foundation （WPF）用戶端所提供的使用者介面（UI）。  
  
> [!NOTE]
> 此範例的安裝程序與建置指示位於本主題的結尾。  
  
 資料繫結允許資料來源自動繫結至 UI。 這可以簡化程式設計模型，因為您不必透過程式設計方式，使用資料物件或資料物件陣列中的資料來更新每個 UI 項目。 您可以將物件繫結至單一 UI 項目，或是將陣列繫結至接受多個輸入的控制項，例如`ListBox`。 下列程式碼示範如何將資料繫結至 UI 項目的 `DataContext`。  
  
```csharp  
// Event handler executed when call is complete  
void client_GetAlbumListCompleted(object sender, GetAlbumListCompletedEventArgs e)  
{  
    // This is on the UI thread, myPanel can be accessed directly  
    myPanel.DataContext = e.Result;
}  
```  
  
 在前面的範例中，名為 `DataContext` 之 `grid` 配置項目的 `myPanel` 會設定為 `GetAlbumList` 方法所傳回的資料。 `DataContext` 允許項目從父項目繼承有關用於繫結之資料來源的資訊，以及繫結的其他特性 (例如，路徑)。 每次更新伺服器上的資料時都必須執行此一程式碼行。 例如，當初始化視窗以及增加新專輯時，就會執行它。  
  
 在下列範例 XAML 程式碼中，`ListBox` 會指定 `ItemsSource="{Binding }"`。  
  
```xml  
<ListBox
          ItemTemplate="{StaticResource AlbumStyle}"  
          ItemsSource="{Binding }"
          IsSynchronizedWithCurrentItem="true" />  
```  
  
 這會指定繫結於最上層 UI 項目的資料也要繫結至這個控制項 (即專輯的陣列)。 此外，`ItemTemplate="{StaticResource AlbumStyle}"` 還會指定要用於 `ListBox` 中每個項目的資料範本。 您也可以定義資料範本來指定資料的格式化方式。 您可以對應用程式中的其他 UI 項目重複使用這些資料範本，其好處是只需在同一處定義和維護資料範本。  
  
 `AlbumStyle` 資料範本會將方格與兩個 `TextBlock` 並排配置在一起。 一個指定專輯的名稱，另一個則指定專輯中的曲目。  
  
```xaml  
<DataTemplate x:Key="AlbumStyle">  
    <Grid>  
        <Grid.ColumnDefinitions>  
            <ColumnDefinition Width="260" />  
            <ColumnDefinition Width="60" />  
        </Grid.ColumnDefinitions>  
        <TextBlock Grid.Column="0" TextContent="{Binding Path=Title}" />  
        <TextBlock Grid.Column="1" TextContent="{Binding Path=Tracks#.Count}" HorizontalAlignment="Right" />  
    </Grid>  
</DataTemplate>  
```  
  
 下列 XAML 程式碼會建立第二個 `ListBox`。  
  
```xaml  
<ListBox Grid.Row="2"
            Grid.ColumnSpan="2"
            ItemTemplate="{StaticResource TrackStyle}"  
            ItemsSource="{Binding Path=Tracks}" />  
```  
  
 程式碼會指定 `ItemsSource` 的路徑。 這表示繫結至此控制項的資料不是最上層資料，而是名為 `Tracks` 之最上層資料的屬性。 這個屬性代表專輯內所含曲目的陣列。 此外，還會指定不同的 `DataTemplate`，其名稱為 `TrackStyle`。 `TrackStyle` 範本的配置與 `AlbumStyle` 範本的配置相似，但 `TextBlock` 是繫結於不同的屬性。 這是因為兩個範本各自使用於不同的資料物件。  
  
### <a name="to-set-up-build-and-run-the-sample"></a>若要安裝、建置及執行範例  
  
1. 請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2. 若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。  
  
3. 若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。  
  
> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> 如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Scenario\DataBinding\WPFDataBinding`  
