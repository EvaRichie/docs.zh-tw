---
title: XAML 命名空間和命名空間對應
description: 深入瞭解在 Windows Presentation Foundation XAML 檔案的根標記中，通常會找到兩個 XAML 命名空間對應的存在和用途。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- custom classes [WPF], mapping namespaces to
- XAML [WPF], namespaces
- namespace mapping [WPF]
- assemblies [WPF], mapping namespaces to
- mapping namespaces [WPF]
- XAML [WPF], namespace mapping
- classes [WPF], mapping namespaces to
- namespaces [WPF]
ms.assetid: 5c0854e3-7470-435d-9fe2-93eec9d3634e
ms.openlocfilehash: 42808df8e7483f60b1420fda890fe374493538f1
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87168370"
---
# <a name="xaml-namespaces-and-namespace-mapping-for-wpf-xaml"></a>WPF XAML 的 XAML 命名空間和命名空間對應
本主題會進一步說明 WPF XAML 檔案根標記中常見的兩個 XAML 命名空間對應之現況與目的。 本文也會說明如何產生類似的對應，以使用自己的程式碼中所定義的項目和 (或) 個別組件內的項目。  

## <a name="what-is-a-xaml-namespace"></a>什麼是 XAML 命名空間？  
 XAML 命名空間實際上是 XML 命名空間的延伸模組概念。 XAML 命名空間的指定技術仰賴下列項目：XML 命名空間的語法、將 URI 作為命名空間識別項的慣例、利用前置詞以參考來自相同標記來源的多個命名空間等等。 XML 命名空間的 XAML 定義中，有一個新的主要概念：XAML 命名空間一方面代表標記使用範圍的唯一性，也代表它會影響特定 CLR 命名空間和參考組件支援標記實體的可能方式。 而 XAML 結構描述內容的概念也會影響後者的考量。 但從 WPF 使用 XAML 命名空間的方式與目的來看，總體上，您可以把 XAML 命名空間想成預設的 XAML 命名空間、XAML 語言命名空間，以及任何進一步的 XAML 命名空間 (由您的 XAML 標記直接對應至特定的支援 CLR 命名空間和參考組件)。  
  
<a name="The_WPF_and_XAML_Namespace_Declarations"></a>
## <a name="the-wpf-and-xaml-namespace-declarations"></a>WPF 和 XAML 命名空間宣告  
 在許多 XAML 檔案根標記中的命名空間宣告內，您通常會看到兩個 XML 命名空間宣告。 第一個宣告會依預設方式進行整體 WPF 用戶端/架構 XAML 命名空間的對應：  
  
 `xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"`  
  
 第二個宣告 (通常) 會將個別的 XAML 命名空間對應到 `x:` 前置詞。  
  
 `xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"`  
  
 這些宣告的關聯性在於 `x:` 前置詞對應可支援 XAML 語言定義當中的內建函式，而 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 是一個將 XAML 作為語言的實作，並會針對 XAML 定義其物件的詞彙。 由於 WPF 詞彙比 XAML 內建函式更加普遍，因此會以預設方式來進行 WPF 詞彙的對應。  
  
 對應 `x:` XAML 語言內建支援的前置詞慣例，接著是專案範本、範例程式碼，以及此 SDK 中語言功能的檔。 XAML 命名空間定義了許多常用功能，甚至基本 WPF 應用程式也需要這些功能。 比方說，若要透過部分類別將任何程式碼後置加入 XAML 檔案中，您必須將該類別命名為相關 XAML 檔案之根項目中的 `x:Class` 屬性。 或者，如果您想要以索引資源形式存取 XAML 頁面中所定義的任何項目，這些項目就必須設定 `x:Key` 屬性。 如需 XAML 上述方面與其他方面的詳細資訊，請參閱 [XAML 概觀 (WPF)](../../../desktop-wpf/fundamentals/xaml.md) 或 [XAML 語法詳細資料](xaml-syntax-in-detail.md)。  
  
<a name="Mapping_To_Custom_Classes_and_Assemblies"></a>
## <a name="mapping-to-custom-classes-and-assemblies"></a>對應至自訂類別和組件  
 您可以使用 `xmlns` 前置詞宣告內的一系列語彙基元，將 XML 命名空間對應至組件，其類似於將標準 WPF 和 XAML 內建函式的 XAML 命名空間對應至前置詞的方式。  
  
 語法會採用下列可能的具名語彙基元和值：  
  
 `clr-namespace:` CLR 命名空間，其宣告位置是在包含要以項目形式公開之公用型別的組件中。  
  
 `assembly=`包含部分或所有參考之 CLR 命名空間的元件。 這個值通常只是組件的名稱，而不是路徑，亦不包含副檔名 (例如 .dll 或 .exe)。 您必須將該組件的路徑建立為專案檔中的專案參考，且專案檔中包含您要對應的 XAML。 為了併入版本控制和強式名稱簽署，此 `assembly` 值可以是所定義的字串 <xref:System.Reflection.AssemblyName> ，而不是簡單的字串名稱。  
  
 請注意，用來分隔 `clr-namespace` 語彙基元與其值的字元是冒號 (:)，而用來分隔 `assembly` 語彙基元與其值的字元是等號 (=)。 這兩個語彙基元之間要用的字元則是分號。 此外，請勿在宣告中的任何位置包含任何空白字元。  
  
### <a name="a-basic-custom-mapping-example"></a>基本的自訂對應範例  
 下列程式碼可定義範例自訂類別：  
  
```csharp  
namespace SDKSample {  
    public class ExampleClass : ContentControl {  
        public ExampleClass() {  
        ...  
        }  
    }  
}  
```  
  
```vb  
Namespace SDKSample  
    Public Class ExampleClass  
        Inherits ContentControl  
         ...  
        Public Sub New()  
        End Sub  
    End Class  
End Namespace  
```  
  
 系統即會將這個自訂類別編譯到程式庫中，並將每個專案設定 (未顯示) 命名為 `SDKSampleLibrary`。  
  
 若要參考此自訂類別，您還需要將它納入目前的專案以作為參考；一般來說，您可以使用 Visual Studio 中的方案總管 UI 來執行此作業。  
  
 現在，您的程式庫已含有類別，專案設定中也有該類別的參考，即可將下列前置詞對應新增為 XAML 中根項目的一部分：  
  
 `xmlns:custom="clr-namespace:SDKSample;assembly=SDKSampleLibrary"`  
  
 為了將所有項目組合在一起，下列 XAML 是包含典型的預設值和 x (根標記中的對應) 的自訂對應，其會使用前置的參考來具現化該 UI 中的 `ExampleClass`：  
  
```xaml  
<Page x:Class="WPFApplication1.MainPage"  
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
    xmlns:custom="clr-namespace:SDKSample;assembly=SDKSampleLibrary">  
  ...  
  <custom:ExampleClass/>  
...  
</Page>  
```  
  
### <a name="mapping-to-current-assemblies"></a>對應至目前的組件  
 如果參考的 `clr-namespace` 其定義組件位置與參考自訂類別的應用程式程式碼相同，您就可以省略 `assembly`。 或者，此案例的對等語法是指定 `assembly=`，且等號後面不用字串語彙基元。  
  
 如果自訂類別是在相同的組件中定義，就不能作為頁面的根項目。 部分類別不需要對應；如果您想要將部分類別作為 XAML 中的參考項目，則僅需要針對不屬於應用程式頁面之部分類別的類別，進行對應。  
  
<a name="Mapping_CLR_Namespaces_to_XML_Namespaces_in_an"></a>
## <a name="mapping-clr-namespaces-to-xml-namespaces-in-an-assembly"></a>將 CLR 命名空間對應至組件中的 XML 命名空間  
 WPF 定義的 CLR 屬性是由 XAML 處理器使用，以便將多個 CLR 命名空間對應至單一的 XAML 命名空間。 這個屬性（attribute） <xref:System.Windows.Markup.XmlnsDefinitionAttribute> 會放在產生元件之原始程式碼中的元件層級。 WPF 元件原始程式碼會使用這個屬性，將各種通用命名空間（例如 <xref:System.Windows> 和）對應 <xref:System.Windows.Controls> 至 `http://schemas.microsoft.com/winfx/2006/xaml/presentation` 命名空間。  
  
 <xref:System.Windows.Markup.XmlnsDefinitionAttribute>會採用兩個參數： XML/XAML 命名空間名稱和 CLR 命名空間名稱。 有多個 <xref:System.Windows.Markup.XmlnsDefinitionAttribute> CLR 命名空間可以對應到相同的 XML 命名空間。 一旦對應之後，即可在部分類別程式碼後置頁面中提供適當的 `using` 陳述式，視需要參考這些命名空間的成員，而不使用完整限定性條件。 如需詳細資訊，請參閱 <xref:System.Windows.Markup.XmlnsDefinitionAttribute>。  
  
## <a name="designer-namespaces-and-other-prefixes-from-xaml-templates"></a>設計工具命名空間和其他來自 XAML 範本的前置詞  
 如果您是使用 WPF XAML 的開發環境及/或設計工具，您可能會注意到 XAML 標記內含有其他已定義的 XAML 命名空間/前置詞。  
  
 Visual Studio 的 WPF 設計工具會使用通常會對應至前置詞的設計工具命名空間 `d:` 。 WPF 的較新專案範本可能會預先對應這個 XAML 命名空間，以支援 Visual Studio 和其他設計環境的 WPF 設計工具之間的 XAML 交換。 這種 XAML 命名空間的設計用意是為了在設計工具中以 XAML 為基礎的 UI 之間來回時，永久保存設計狀態。 它也會用於 `d:IsDataSource` 這類功能，以啟用設計工具中的執行階段資料來源。  
  
 另一個您可能會看到的對應前置詞是 `mc:`。 `mc:` 適用於標記相容性，其可運用的標記相容性模式不一定為 XAML 特有。 標記相容性功能在某種程度來說，可以用來在架構之間或跨支援實作的其他界限交換 XAML、進行 XAML 結構描述內容之間的工作、在設計工具中的限制模式提供相容性等等。 如需標記相容性概念以及其與 WPF 之關聯的詳細資訊，請參閱[標記相容性 (mc:) 語言功能](markup-compatibility-mc-language-features.md)。  
  
## <a name="wpf-and-assembly-loading"></a>WPF 和組件載入  
 WPF 的 XAML 架構內容會與 WPF 應用程式模型整合，而這又會使用的 CLR 定義概念 <xref:System.AppDomain> 。 下列順序描述 XAML 架構內容如何根據 WPF 使用和其他因素，在執行時間或設計階段中，解釋如何載入元件或尋找類型 <xref:System.AppDomain> 。  
  
1. 逐一 <xref:System.AppDomain> 查看，尋找已載入的元件，以符合名稱的所有層面，從最近載入的元件開始。  
  
2. 如果名稱是合格的，請 <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=nameWithType> 在限定名稱上呼叫。  
  
3. 如果限定名稱的簡短名稱 + 公開金鑰語彙基元與載入標記的組件相符，即會傳回這個組件。  
  
4. 使用簡短名稱 + 公開金鑰標記來呼叫 <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=nameWithType> 。  
  
5. 如果名稱不合格，請呼叫 <xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=nameWithType> 。  
  
 鬆散式 XAML 不會使用步驟 3；因為沒有任何載入來源組件。  
  
 適用于 WPF 的已編譯 XAML （透過 XamlBuildTask 產生）不會使用中已載入的元件 <xref:System.AppDomain> （步驟1）。 此外，名稱不得為來自 XamlBuildTask 輸出的非限定名稱，因此不適用步驟 5。  
  
 雖然 BAML 也不應包含非限定的組件名稱，但編譯的 BAML (透過 PresentationBuildTask 產生) 仍會使用所有的步驟。  
  
## <a name="see-also"></a>另請參閱

- [了解 XML 命名空間](https://docs.microsoft.com/previous-versions/aa468565(v=msdn.10))
- [XAML 概觀 (WPF)](../../../desktop-wpf/fundamentals/xaml.md)
