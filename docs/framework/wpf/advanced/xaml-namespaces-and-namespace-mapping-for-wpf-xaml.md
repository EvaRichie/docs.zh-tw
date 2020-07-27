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
# <a name="xaml-namespaces-and-namespace-mapping-for-wpf-xaml"></a><span data-ttu-id="75799-103">WPF XAML 的 XAML 命名空間和命名空間對應</span><span class="sxs-lookup"><span data-stu-id="75799-103">XAML Namespaces and Namespace Mapping for WPF XAML</span></span>
<span data-ttu-id="75799-104">本主題會進一步說明 WPF XAML 檔案根標記中常見的兩個 XAML 命名空間對應之現況與目的。</span><span class="sxs-lookup"><span data-stu-id="75799-104">This topic further explains the presence and purpose of the two XAML namespace mappings as often found in the root tag of a WPF XAML file.</span></span> <span data-ttu-id="75799-105">本文也會說明如何產生類似的對應，以使用自己的程式碼中所定義的項目和 (或) 個別組件內的項目。</span><span class="sxs-lookup"><span data-stu-id="75799-105">It also describes how to produce similar mappings for using elements that are defined in your own code, and/or within separate assemblies.</span></span>  

## <a name="what-is-a-xaml-namespace"></a><span data-ttu-id="75799-106">什麼是 XAML 命名空間？</span><span class="sxs-lookup"><span data-stu-id="75799-106">What is a XAML Namespace?</span></span>  
 <span data-ttu-id="75799-107">XAML 命名空間實際上是 XML 命名空間的延伸模組概念。</span><span class="sxs-lookup"><span data-stu-id="75799-107">A XAML namespace is really an extension of the concept of an XML namespace.</span></span> <span data-ttu-id="75799-108">XAML 命名空間的指定技術仰賴下列項目：XML 命名空間的語法、將 URI 作為命名空間識別項的慣例、利用前置詞以參考來自相同標記來源的多個命名空間等等。</span><span class="sxs-lookup"><span data-stu-id="75799-108">The techniques of specifying a XAML namespace rely on the XML namespace syntax, the convention of using URIs as namespace identifiers, using prefixes to provide a means to reference multiple namespaces from the same markup source, and so on.</span></span> <span data-ttu-id="75799-109">XML 命名空間的 XAML 定義中，有一個新的主要概念：XAML 命名空間一方面代表標記使用範圍的唯一性，也代表它會影響特定 CLR 命名空間和參考組件支援標記實體的可能方式。</span><span class="sxs-lookup"><span data-stu-id="75799-109">The primary concept that is added to the XAML definition of the XML namespace is that a XAML namespace implies both a scope of uniqueness for the markup usages, and also influences how markup entities are potentially backed by specific CLR namespaces and referenced assemblies.</span></span> <span data-ttu-id="75799-110">而 XAML 結構描述內容的概念也會影響後者的考量。</span><span class="sxs-lookup"><span data-stu-id="75799-110">This latter consideration is also influenced by the concept of a XAML schema context.</span></span> <span data-ttu-id="75799-111">但從 WPF 使用 XAML 命名空間的方式與目的來看，總體上，您可以把 XAML 命名空間想成預設的 XAML 命名空間、XAML 語言命名空間，以及任何進一步的 XAML 命名空間 (由您的 XAML 標記直接對應至特定的支援 CLR 命名空間和參考組件)。</span><span class="sxs-lookup"><span data-stu-id="75799-111">But for purposes of how WPF works with XAML namespaces, you can generally think of XAML namespaces in terms of a default XAML namespace, the XAML language namespace, and any further XAML namespaces as mapped by your XAML markup directly to specific backing CLR namespaces and referenced assemblies.</span></span>  
  
<a name="The_WPF_and_XAML_Namespace_Declarations"></a>
## <a name="the-wpf-and-xaml-namespace-declarations"></a><span data-ttu-id="75799-112">WPF 和 XAML 命名空間宣告</span><span class="sxs-lookup"><span data-stu-id="75799-112">The WPF and XAML Namespace Declarations</span></span>  
 <span data-ttu-id="75799-113">在許多 XAML 檔案根標記中的命名空間宣告內，您通常會看到兩個 XML 命名空間宣告。</span><span class="sxs-lookup"><span data-stu-id="75799-113">Within the namespace declarations in the root tag of many XAML files, you will see that there are typically two XML namespace declarations.</span></span> <span data-ttu-id="75799-114">第一個宣告會依預設方式進行整體 WPF 用戶端/架構 XAML 命名空間的對應：</span><span class="sxs-lookup"><span data-stu-id="75799-114">The first declaration maps the overall WPF client / framework XAML namespace as the default:</span></span>  
  
 `xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"`  
  
 <span data-ttu-id="75799-115">第二個宣告 (通常) 會將個別的 XAML 命名空間對應到 `x:` 前置詞。</span><span class="sxs-lookup"><span data-stu-id="75799-115">The second declaration maps a separate XAML namespace, mapping it (typically) to the `x:` prefix.</span></span>  
  
 `xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"`  
  
 <span data-ttu-id="75799-116">這些宣告的關聯性在於 `x:` 前置詞對應可支援 XAML 語言定義當中的內建函式，而 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 是一個將 XAML 作為語言的實作，並會針對 XAML 定義其物件的詞彙。</span><span class="sxs-lookup"><span data-stu-id="75799-116">The relationship between these declarations is that the `x:` prefix mapping supports the intrinsics that are part of the XAML language definition, and [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] is one implementation that uses XAML as a language and defines a vocabulary of its objects for XAML.</span></span> <span data-ttu-id="75799-117">由於 WPF 詞彙比 XAML 內建函式更加普遍，因此會以預設方式來進行 WPF 詞彙的對應。</span><span class="sxs-lookup"><span data-stu-id="75799-117">Because the WPF vocabulary's usages will be far more common than the XAML intrinsics usages, the WPF vocabulary is mapped as the default.</span></span>  
  
 <span data-ttu-id="75799-118">對應 `x:` XAML 語言內建支援的前置詞慣例，接著是專案範本、範例程式碼，以及此 SDK 中語言功能的檔。</span><span class="sxs-lookup"><span data-stu-id="75799-118">The `x:` prefix convention for mapping the XAML language intrinsics support is followed by project templates, sample code, and the documentation of language features within this SDK.</span></span> <span data-ttu-id="75799-119">XAML 命名空間定義了許多常用功能，甚至基本 WPF 應用程式也需要這些功能。</span><span class="sxs-lookup"><span data-stu-id="75799-119">The XAML namespace defines many commonly-used features that are necessary even for basic WPF  applications.</span></span> <span data-ttu-id="75799-120">比方說，若要透過部分類別將任何程式碼後置加入 XAML 檔案中，您必須將該類別命名為相關 XAML 檔案之根項目中的 `x:Class` 屬性。</span><span class="sxs-lookup"><span data-stu-id="75799-120">For instance, in order to join any code-behind to a XAML file through a partial class, you must name that class as the `x:Class` attribute in the root element of the relevant XAML file.</span></span> <span data-ttu-id="75799-121">或者，如果您想要以索引資源形式存取 XAML 頁面中所定義的任何項目，這些項目就必須設定 `x:Key` 屬性。</span><span class="sxs-lookup"><span data-stu-id="75799-121">Or, any element as defined in a XAML page that you wish to access as a keyed resource should have the `x:Key` attribute set on the element in question.</span></span> <span data-ttu-id="75799-122">如需 XAML 上述方面與其他方面的詳細資訊，請參閱 [XAML 概觀 (WPF)](../../../desktop-wpf/fundamentals/xaml.md) 或 [XAML 語法詳細資料](xaml-syntax-in-detail.md)。</span><span class="sxs-lookup"><span data-stu-id="75799-122">For more information on these and other aspects of XAML see [XAML Overview (WPF)](../../../desktop-wpf/fundamentals/xaml.md) or [XAML Syntax In Detail](xaml-syntax-in-detail.md).</span></span>  
  
<a name="Mapping_To_Custom_Classes_and_Assemblies"></a>
## <a name="mapping-to-custom-classes-and-assemblies"></a><span data-ttu-id="75799-123">對應至自訂類別和組件</span><span class="sxs-lookup"><span data-stu-id="75799-123">Mapping to Custom Classes and Assemblies</span></span>  
 <span data-ttu-id="75799-124">您可以使用 `xmlns` 前置詞宣告內的一系列語彙基元，將 XML 命名空間對應至組件，其類似於將標準 WPF 和 XAML 內建函式的 XAML 命名空間對應至前置詞的方式。</span><span class="sxs-lookup"><span data-stu-id="75799-124">You can map XML namespaces to assemblies using a series of tokens within an `xmlns` prefix declaration, similar to how the standard WPF and XAML-intrinsics XAML namespaces are mapped to prefixes.</span></span>  
  
 <span data-ttu-id="75799-125">語法會採用下列可能的具名語彙基元和值：</span><span class="sxs-lookup"><span data-stu-id="75799-125">The syntax takes the following possible named tokens and following values:</span></span>  
  
 <span data-ttu-id="75799-126">`clr-namespace:` CLR 命名空間，其宣告位置是在包含要以項目形式公開之公用型別的組件中。</span><span class="sxs-lookup"><span data-stu-id="75799-126">`clr-namespace:` The CLR namespace declared within the assembly that contains the public types to expose as elements.</span></span>  
  
 <span data-ttu-id="75799-127">`assembly=`包含部分或所有參考之 CLR 命名空間的元件。</span><span class="sxs-lookup"><span data-stu-id="75799-127">`assembly=` The assembly that contains some or all of the referenced CLR namespace.</span></span> <span data-ttu-id="75799-128">這個值通常只是組件的名稱，而不是路徑，亦不包含副檔名 (例如 .dll 或 .exe)。</span><span class="sxs-lookup"><span data-stu-id="75799-128">This value is typically just the name of the assembly, not the path, and does not include the extension (such as .dll or .exe).</span></span> <span data-ttu-id="75799-129">您必須將該組件的路徑建立為專案檔中的專案參考，且專案檔中包含您要對應的 XAML。</span><span class="sxs-lookup"><span data-stu-id="75799-129">The path to that assembly must be established as a project reference in the project file that contains the XAML you are trying to map.</span></span> <span data-ttu-id="75799-130">為了併入版本控制和強式名稱簽署，此 `assembly` 值可以是所定義的字串 <xref:System.Reflection.AssemblyName> ，而不是簡單的字串名稱。</span><span class="sxs-lookup"><span data-stu-id="75799-130">In order to incorporate versioning and strong-name signing, the `assembly` value can be a string as defined by <xref:System.Reflection.AssemblyName>, rather than the simple string name.</span></span>  
  
 <span data-ttu-id="75799-131">請注意，用來分隔 `clr-namespace` 語彙基元與其值的字元是冒號 (:)，而用來分隔 `assembly` 語彙基元與其值的字元是等號 (=)。</span><span class="sxs-lookup"><span data-stu-id="75799-131">Note that the character separating the `clr-namespace` token from its value is a colon (:) whereas the character separating the `assembly` token from its value is an equals sign (=).</span></span> <span data-ttu-id="75799-132">這兩個語彙基元之間要用的字元則是分號。</span><span class="sxs-lookup"><span data-stu-id="75799-132">The character to use between these two tokens is a semicolon.</span></span> <span data-ttu-id="75799-133">此外，請勿在宣告中的任何位置包含任何空白字元。</span><span class="sxs-lookup"><span data-stu-id="75799-133">Also, do not include any white space anywhere in the declaration.</span></span>  
  
### <a name="a-basic-custom-mapping-example"></a><span data-ttu-id="75799-134">基本的自訂對應範例</span><span class="sxs-lookup"><span data-stu-id="75799-134">A Basic Custom Mapping Example</span></span>  
 <span data-ttu-id="75799-135">下列程式碼可定義範例自訂類別：</span><span class="sxs-lookup"><span data-stu-id="75799-135">The following code defines an example custom class:</span></span>  
  
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
  
 <span data-ttu-id="75799-136">系統即會將這個自訂類別編譯到程式庫中，並將每個專案設定 (未顯示) 命名為 `SDKSampleLibrary`。</span><span class="sxs-lookup"><span data-stu-id="75799-136">This custom class is then compiled into a library, which per the project settings (not shown) is named `SDKSampleLibrary`.</span></span>  
  
 <span data-ttu-id="75799-137">若要參考此自訂類別，您還需要將它納入目前的專案以作為參考；一般來說，您可以使用 Visual Studio 中的方案總管 UI 來執行此作業。</span><span class="sxs-lookup"><span data-stu-id="75799-137">In order to reference this custom class, you also need to include it as a reference for your current project, which you would typically do using the Solution Explorer UI in Visual Studio.</span></span>  
  
 <span data-ttu-id="75799-138">現在，您的程式庫已含有類別，專案設定中也有該類別的參考，即可將下列前置詞對應新增為 XAML 中根項目的一部分：</span><span class="sxs-lookup"><span data-stu-id="75799-138">Now that you have a library containing a class, and a reference to it in project settings, you can add the following prefix mapping as part of your root element in XAML:</span></span>  
  
 `xmlns:custom="clr-namespace:SDKSample;assembly=SDKSampleLibrary"`  
  
 <span data-ttu-id="75799-139">為了將所有項目組合在一起，下列 XAML 是包含典型的預設值和 x (根標記中的對應) 的自訂對應，其會使用前置的參考來具現化該 UI 中的 `ExampleClass`：</span><span class="sxs-lookup"><span data-stu-id="75799-139">To put it all together, the following is XAML that includes the custom mapping along with the typical default and x: mappings in the root tag, then uses a prefixed reference to instantiate `ExampleClass` in that UI:</span></span>  
  
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
  
### <a name="mapping-to-current-assemblies"></a><span data-ttu-id="75799-140">對應至目前的組件</span><span class="sxs-lookup"><span data-stu-id="75799-140">Mapping to Current Assemblies</span></span>  
 <span data-ttu-id="75799-141">如果參考的 `clr-namespace` 其定義組件位置與參考自訂類別的應用程式程式碼相同，您就可以省略 `assembly`。</span><span class="sxs-lookup"><span data-stu-id="75799-141">`assembly` can be omitted if the `clr-namespace` referenced is being defined within the same assembly as the application code that is referencing the custom classes.</span></span> <span data-ttu-id="75799-142">或者，此案例的對等語法是指定 `assembly=`，且等號後面不用字串語彙基元。</span><span class="sxs-lookup"><span data-stu-id="75799-142">Or, an equivalent syntax for this case is to specify `assembly=`, with no string token following the equals sign.</span></span>  
  
 <span data-ttu-id="75799-143">如果自訂類別是在相同的組件中定義，就不能作為頁面的根項目。</span><span class="sxs-lookup"><span data-stu-id="75799-143">Custom classes cannot be used as the root element of a page if defined in the same assembly.</span></span> <span data-ttu-id="75799-144">部分類別不需要對應；如果您想要將部分類別作為 XAML 中的參考項目，則僅需要針對不屬於應用程式頁面之部分類別的類別，進行對應。</span><span class="sxs-lookup"><span data-stu-id="75799-144">Partial classes do not need to be mapped; only classes that are not the partial class of a page in your application need to be mapped if you intend to reference them as elements in XAML.</span></span>  
  
<a name="Mapping_CLR_Namespaces_to_XML_Namespaces_in_an"></a>
## <a name="mapping-clr-namespaces-to-xml-namespaces-in-an-assembly"></a><span data-ttu-id="75799-145">將 CLR 命名空間對應至組件中的 XML 命名空間</span><span class="sxs-lookup"><span data-stu-id="75799-145">Mapping CLR Namespaces to XML Namespaces in an Assembly</span></span>  
 <span data-ttu-id="75799-146">WPF 定義的 CLR 屬性是由 XAML 處理器使用，以便將多個 CLR 命名空間對應至單一的 XAML 命名空間。</span><span class="sxs-lookup"><span data-stu-id="75799-146">WPF defines a CLR attribute that is consumed by XAML processors in order to map multiple CLR namespaces to a single XAML namespace.</span></span> <span data-ttu-id="75799-147">這個屬性（attribute） <xref:System.Windows.Markup.XmlnsDefinitionAttribute> 會放在產生元件之原始程式碼中的元件層級。</span><span class="sxs-lookup"><span data-stu-id="75799-147">This attribute, <xref:System.Windows.Markup.XmlnsDefinitionAttribute>, is placed at the assembly level in the source code that produces the assembly.</span></span> <span data-ttu-id="75799-148">WPF 元件原始程式碼會使用這個屬性，將各種通用命名空間（例如 <xref:System.Windows> 和）對應 <xref:System.Windows.Controls> 至 `http://schemas.microsoft.com/winfx/2006/xaml/presentation` 命名空間。</span><span class="sxs-lookup"><span data-stu-id="75799-148">The WPF assembly source code uses this attribute to map the various common namespaces, such as <xref:System.Windows> and <xref:System.Windows.Controls>, to the `http://schemas.microsoft.com/winfx/2006/xaml/presentation` namespace.</span></span>  
  
 <span data-ttu-id="75799-149"><xref:System.Windows.Markup.XmlnsDefinitionAttribute>會採用兩個參數： XML/XAML 命名空間名稱和 CLR 命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="75799-149">The <xref:System.Windows.Markup.XmlnsDefinitionAttribute> takes two parameters: the XML/XAML namespace name, and the CLR namespace name.</span></span> <span data-ttu-id="75799-150">有多個 <xref:System.Windows.Markup.XmlnsDefinitionAttribute> CLR 命名空間可以對應到相同的 XML 命名空間。</span><span class="sxs-lookup"><span data-stu-id="75799-150">More than one <xref:System.Windows.Markup.XmlnsDefinitionAttribute> can exist to map multiple CLR namespaces to the same XML namespace.</span></span> <span data-ttu-id="75799-151">一旦對應之後，即可在部分類別程式碼後置頁面中提供適當的 `using` 陳述式，視需要參考這些命名空間的成員，而不使用完整限定性條件。</span><span class="sxs-lookup"><span data-stu-id="75799-151">Once mapped, members of those namespaces can also be referenced without full qualification if desired by providing the appropriate `using` statement in the partial-class code-behind page.</span></span> <span data-ttu-id="75799-152">如需詳細資訊，請參閱 <xref:System.Windows.Markup.XmlnsDefinitionAttribute>。</span><span class="sxs-lookup"><span data-stu-id="75799-152">For more details, see <xref:System.Windows.Markup.XmlnsDefinitionAttribute>.</span></span>  
  
## <a name="designer-namespaces-and-other-prefixes-from-xaml-templates"></a><span data-ttu-id="75799-153">設計工具命名空間和其他來自 XAML 範本的前置詞</span><span class="sxs-lookup"><span data-stu-id="75799-153">Designer Namespaces and Other Prefixes From XAML Templates</span></span>  
 <span data-ttu-id="75799-154">如果您是使用 WPF XAML 的開發環境及/或設計工具，您可能會注意到 XAML 標記內含有其他已定義的 XAML 命名空間/前置詞。</span><span class="sxs-lookup"><span data-stu-id="75799-154">If you are working with development environments and/or design tools for WPF XAML, you may notice that there are other defined XAML namespaces / prefixes within the XAML markup.</span></span>  
  
 <span data-ttu-id="75799-155">Visual Studio 的 WPF 設計工具會使用通常會對應至前置詞的設計工具命名空間 `d:` 。</span><span class="sxs-lookup"><span data-stu-id="75799-155">WPF Designer for Visual Studio uses a designer namespace that is typically mapped to the prefix `d:`.</span></span> <span data-ttu-id="75799-156">WPF 的較新專案範本可能會預先對應這個 XAML 命名空間，以支援 Visual Studio 和其他設計環境的 WPF 設計工具之間的 XAML 交換。</span><span class="sxs-lookup"><span data-stu-id="75799-156">More recent project templates for WPF might pre-map this XAML namespace to support interchange of the XAML between WPF Designer for Visual Studio and other design environments.</span></span> <span data-ttu-id="75799-157">這種 XAML 命名空間的設計用意是為了在設計工具中以 XAML 為基礎的 UI 之間來回時，永久保存設計狀態。</span><span class="sxs-lookup"><span data-stu-id="75799-157">This design XAML namespace is used to perpetuate design state while roundtripping XAML-based UI in the designer.</span></span> <span data-ttu-id="75799-158">它也會用於 `d:IsDataSource` 這類功能，以啟用設計工具中的執行階段資料來源。</span><span class="sxs-lookup"><span data-stu-id="75799-158">It is also used for features such as `d:IsDataSource`, which enable runtime data sources in a designer.</span></span>  
  
 <span data-ttu-id="75799-159">另一個您可能會看到的對應前置詞是 `mc:`。</span><span class="sxs-lookup"><span data-stu-id="75799-159">Another prefix you might see mapped is `mc:`.</span></span> <span data-ttu-id="75799-160">`mc:` 適用於標記相容性，其可運用的標記相容性模式不一定為 XAML 特有。</span><span class="sxs-lookup"><span data-stu-id="75799-160">`mc:` is for markup compatibility, and is leveraging a markup compatibility pattern that is not necessarily XAML-specific.</span></span> <span data-ttu-id="75799-161">標記相容性功能在某種程度來說，可以用來在架構之間或跨支援實作的其他界限交換 XAML、進行 XAML 結構描述內容之間的工作、在設計工具中的限制模式提供相容性等等。</span><span class="sxs-lookup"><span data-stu-id="75799-161">To some extent, the markup compatibility features can be used to exchange XAML between frameworks or across other boundaries of backing implementation, work between XAML schema contexts, provide compatibility for limited modes in designers, and so on.</span></span> <span data-ttu-id="75799-162">如需標記相容性概念以及其與 WPF 之關聯的詳細資訊，請參閱[標記相容性 (mc:) 語言功能](markup-compatibility-mc-language-features.md)。</span><span class="sxs-lookup"><span data-stu-id="75799-162">For more information on markup compatibility concepts and how they relate to WPF, see  [Markup Compatibility (mc:) Language Features](markup-compatibility-mc-language-features.md).</span></span>  
  
## <a name="wpf-and-assembly-loading"></a><span data-ttu-id="75799-163">WPF 和組件載入</span><span class="sxs-lookup"><span data-stu-id="75799-163">WPF and Assembly Loading</span></span>  
 <span data-ttu-id="75799-164">WPF 的 XAML 架構內容會與 WPF 應用程式模型整合，而這又會使用的 CLR 定義概念 <xref:System.AppDomain> 。</span><span class="sxs-lookup"><span data-stu-id="75799-164">The XAML schema context for WPF integrates with the WPF application model, which in turn uses the CLR-defined concept of <xref:System.AppDomain>.</span></span> <span data-ttu-id="75799-165">下列順序描述 XAML 架構內容如何根據 WPF 使用和其他因素，在執行時間或設計階段中，解釋如何載入元件或尋找類型 <xref:System.AppDomain> 。</span><span class="sxs-lookup"><span data-stu-id="75799-165">The following sequence describes how XAML schema context interprets how to either load assemblies or find types at run time or design time, based on the WPF use of <xref:System.AppDomain> and other factors.</span></span>  
  
1. <span data-ttu-id="75799-166">逐一 <xref:System.AppDomain> 查看，尋找已載入的元件，以符合名稱的所有層面，從最近載入的元件開始。</span><span class="sxs-lookup"><span data-stu-id="75799-166">Iterate through the <xref:System.AppDomain>, looking for an already-loaded assembly that matches all aspects of the name, starting from the most recently loaded assembly.</span></span>  
  
2. <span data-ttu-id="75799-167">如果名稱是合格的，請 <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=nameWithType> 在限定名稱上呼叫。</span><span class="sxs-lookup"><span data-stu-id="75799-167">If the name is qualified, call <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=nameWithType> on the qualified name.</span></span>  
  
3. <span data-ttu-id="75799-168">如果限定名稱的簡短名稱 + 公開金鑰語彙基元與載入標記的組件相符，即會傳回這個組件。</span><span class="sxs-lookup"><span data-stu-id="75799-168">If the short name + public key token of a qualified name matches the assembly that the markup was loaded from, return that assembly.</span></span>  
  
4. <span data-ttu-id="75799-169">使用簡短名稱 + 公開金鑰標記來呼叫 <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="75799-169">Use the short name + public key token to call <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=nameWithType>.</span></span>  
  
5. <span data-ttu-id="75799-170">如果名稱不合格，請呼叫 <xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="75799-170">If the name is unqualified, call <xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=nameWithType>.</span></span>  
  
 <span data-ttu-id="75799-171">鬆散式 XAML 不會使用步驟 3；因為沒有任何載入來源組件。</span><span class="sxs-lookup"><span data-stu-id="75799-171">Loose XAML does not use Step 3; there is no loaded-from assembly.</span></span>  
  
 <span data-ttu-id="75799-172">適用于 WPF 的已編譯 XAML （透過 XamlBuildTask 產生）不會使用中已載入的元件 <xref:System.AppDomain> （步驟1）。</span><span class="sxs-lookup"><span data-stu-id="75799-172">Compiled XAML for WPF (generated via XamlBuildTask) does not use the already-loaded assemblies from <xref:System.AppDomain> (Step 1).</span></span> <span data-ttu-id="75799-173">此外，名稱不得為來自 XamlBuildTask 輸出的非限定名稱，因此不適用步驟 5。</span><span class="sxs-lookup"><span data-stu-id="75799-173">Also, the name should never be unqualified from XamlBuildTask output, so Step 5 does not apply.</span></span>  
  
 <span data-ttu-id="75799-174">雖然 BAML 也不應包含非限定的組件名稱，但編譯的 BAML (透過 PresentationBuildTask 產生) 仍會使用所有的步驟。</span><span class="sxs-lookup"><span data-stu-id="75799-174">Compiled BAML (generated via PresentationBuildTask) uses all steps, although BAML also should not contain unqualified assembly names.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="75799-175">另請參閱</span><span class="sxs-lookup"><span data-stu-id="75799-175">See also</span></span>

- <span data-ttu-id="75799-176">[了解 XML 命名空間](https://docs.microsoft.com/previous-versions/aa468565(v=msdn.10))</span><span class="sxs-lookup"><span data-stu-id="75799-176">[Understanding XML Namespaces](https://docs.microsoft.com/previous-versions/aa468565(v=msdn.10))</span></span>
- [<span data-ttu-id="75799-177">XAML 概觀 (WPF)</span><span class="sxs-lookup"><span data-stu-id="75799-177">XAML Overview (WPF)</span></span>](../../../desktop-wpf/fundamentals/xaml.md)
