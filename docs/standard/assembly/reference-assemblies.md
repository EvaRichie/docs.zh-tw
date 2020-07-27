---
title: 參考組件
description: 瞭解參考元件，這是 .NET 中只包含程式庫公用 API 介面的特殊元件類型
author: MSDN-WhiteKnight
ms.date: 09/12/2019
ms.technology: dotnet-standard
ms.openlocfilehash: 43a9dab037f4d0f1926ff67f8f38eaa6734a6d67
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87164527"
---
# <a name="reference-assemblies"></a>參考組件

*參考元件*是一種特殊類型的元件，其中只包含代表程式庫公用 API 介面所需的最小中繼資料量。 其中包括在建立工具中參考元件時，所有重要成員的宣告，但會排除所有成員的執行，以及對其 API 合約沒有明顯影響的私用成員宣告。 相反地，一般元件稱為「*實做元件*」。

無法載入參考元件來執行，但是可以用相同的方式將它們當做編譯器輸入來傳遞。 參考元件通常會與特定平臺或程式庫的軟體發展工具組（SDK）一起散發。

使用參考元件可讓開發人員建立以特定程式庫版本為目標的程式，而不需要該版本的完整執行元件。 假設您的電腦上只有部分程式庫的最新版本，但您想要建立以該程式庫較舊版本為目標的程式。 如果您直接針對執行元件進行編譯，可能會不小心使用舊版中未提供的 API 成員。 在目的電腦上測試程式時，您只會發現這個錯誤。 如果您針對較早版本的參考元件進行編譯，則會立即收到編譯時期錯誤。

參考元件也可以代表合約，也就是不會對應到具體執行元件的一組 Api。 這類參考元件（稱為*合約元件*）可用來以支援同一組 api 的多個平臺為目標。 例如，.NET Standard 提供合約元件， *netstandard.dll*，代表不同 .net 平臺之間共用的一組通用 api。 這些 Api 的執行包含在不同平臺上的不同元件中，例如在 .NET Core 上 .NET Framework 或*System.Private.CoreLib.dll*上*mscorlib.dll* 。 以 .NET Standard 為目標的程式庫可以在支援 .NET Standard 的所有平臺上執行。

## <a name="using-reference-assemblies"></a>使用參考元件

若要使用專案中的特定 Api，您必須加入其元件的參考。 您可以將參考加入至其中一個執行元件或參考元件。 我們建議您在每次有參考元件時使用它們。 這麼做可確保您只會使用目標版本中支援的 API 成員，以供 API 設計人員使用。 使用參考元件可確保您不會依賴執行的詳細資料。

.NET Framework 程式庫的參考元件會與目標套件一起散發。 您可以藉由下載獨立安裝程式或在 Visual Studio 安裝程式中選取元件來取得它們。 如需詳細資訊，請參閱[安裝適用于開發人員的 .NET Framework](../../framework/install/guide-for-developers.md)。 針對 .NET Core 和 .NET Standard，參考元件會視需要自動下載（透過 NuGet）並加以參考。 針對 .NET Core 3.0 和更新版本，核心架構的參考元件位於[NETCore](https://www.nuget.org/packages/Microsoft.NETCore.App.Ref)中，而不是使用[NETCore 應用程式](https://www.nuget.org/packages/Microsoft.NETCore.App)套件（3.0 之前的版本）。

當您使用 [**加入參考**] 對話方塊在 Visual Studio 中加入 .NET Framework 元件的參考時，會從清單中選取元件，而且 Visual Studio 會自動尋找對應至專案中所選目標 Framework 版本的參考元件。 這同樣適用于使用[參考](/visualstudio/msbuild/common-msbuild-project-items#reference)專案專案，直接在 MSBuild 專案中加入參考：您只需要指定元件名稱，而不是完整的檔案路徑。 當您使用 `-reference` 編譯器選項（[c # 中](../../csharp/language-reference/compiler-options/reference-compiler-option.md)的和[Visual Basic](../../visual-basic/reference/command-line-compiler/reference.md)中的），或使用 Roslyn API 中的方法，在命令列中加入這些元件的參考時 <xref:Microsoft.CodeAnalysis.Compilation.AddReferences%2A?displayProperty=nameWithType> ，您必須手動指定正確目標平臺版本的參考元件檔案。 .NET Framework 參考元件檔案位於 *% ProgramFiles （x86）% \\ reference assembly \\ Microsoft \\ Framework \\ 。.Netframework*目錄。 針對 .NET Core，您可以藉由將專案屬性設定為，強制發行作業將目標平臺的參考元件複製到輸出目錄的*publish/refs*子目錄中 `PreserveCompilationContext` `true` 。 然後您可以將這些參考元件檔案傳遞給編譯器。 使用 `DependencyContext` [DependencyModel](https://www.nuget.org/packages/Microsoft.Extensions.DependencyModel/)封裝有助於找出其路徑。

因為它們不包含任何實作為，所以無法載入參考元件來執行。 嘗試這麼做會導致 <xref:System.BadImageFormatException?displayProperty=nameWithType> 。 如果您想要檢查參考元件的內容，您可以在 .NET Framework （使用 <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A?displayProperty=nameWithType> 方法）或 .Net Core 的中，將它載入至僅限反映的內容中 <xref:System.Reflection.MetadataLoadContext> 。

## <a name="generating-reference-assemblies"></a>產生參考元件

當您的程式庫取用者需要針對許多不同版本的程式庫建立其程式時，為您的程式庫產生參考元件會很有用。 散發所有這些版本的實做元件，可能會因為大小龐大而不實際。 參考元件的大小較小，並將它們散發為程式庫 SDK 的一部分，可減少下載大小並節省磁碟空間。

Ide 和 build 工具也可以利用參考元件，在包含多個類別庫的大型解決方案時，減少組建時間。 通常，在累加組建案例中，當任何輸入檔變更時，會重建專案，包括它所相依的元件。 每當程式設計人員變更任何成員的執行時，就會變更執行元件。 參考元件只會在其公用 API 受到影響時變更。 因此，在某些情況下，使用參考元件做為輸入檔，而不是執行元件，可以略過相依專案的組建。

您可以產生參考元件：

- 在 MSBuild 專案中，使用[ `ProduceReferenceAssembly` 專案屬性](/visualstudio/msbuild/common-msbuild-project-properties)。
- 從命令列編譯器時，請依指定 `-refonly` （[c #](../../csharp/language-reference/compiler-options/refonly-compiler-option.md)  /  [Visual Basic](../../visual-basic/reference/command-line-compiler/refonly-compiler-option.md) ）或 `-refout` （[c #](../../csharp/language-reference/compiler-options/refout-compiler-option.md)  /  [Visual Basic](../../visual-basic/reference/command-line-compiler/refout-compiler-option.md)）編譯器選項。
- 使用 Roslyn API 時，會 <xref:Microsoft.CodeAnalysis.Emit.EmitOptions.EmitMetadataOnly?displayProperty=nameWithType> `true` <xref:Microsoft.CodeAnalysis.Emit.EmitOptions.IncludePrivateMembers?displayProperty=nameWithType> `false` 在傳遞至方法的物件中，將設定為和 <xref:Microsoft.CodeAnalysis.Compilation.Emit%2A?displayProperty=nameWithType> 。

如果您想要使用 NuGet 套件散發參考元件，您必須將它們包含在封裝目錄下的*ref \\ *子目錄中，而不是在用於執行元件的*lib \\ *子目錄中。

## <a name="reference-assemblies-structure"></a>參考元件結構

參考元件是相關概念的擴充，*僅限中繼資料的元件*。 僅中繼資料組件以單一的 `throw null` 主體取代其方法主體，但包含匿名型別以外的所有成員。 使用 `throw null` 主體（而不是任何主體）的原因，是為了讓**PEVerify**能夠執行和傳遞（進而驗證中繼資料的完整性）。

參考組件會進一步移除來自僅中繼資料組件的中繼資料 (私用成員)：

- 參考組件只有在 API 介面中所需項目的參考。 實際的組件可能有與特定實作相關的其他參考。 例如，的參考元件 `class C { private void M() { dynamic d = 1; ... } }` 不會參考所需的任何類型 `dynamic` 。
- 如果移除它們不會明顯影響編譯的話，則會移除私用函式的成員 (方法、屬性和事件)。 如果沒有[InternalsVisibleTo](xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute)屬性，內部函式成員也會一併移除。

參考元件中的中繼資料會繼續保留下列資訊：

- 所有類型，包括私用和巢狀型別。
- 所有屬性，甚至是內部屬性。
- 所有的虛擬方法。
- 明確介面的實現。
- 明確實作為屬性和事件，因為它們的存取子是虛擬的。
- 結構的所有欄位。

參考元件包含元件層級的[ReferenceAssembly](xref:System.Runtime.CompilerServices.ReferenceAssemblyAttribute)屬性。 可以在來源中指定這個屬性。然後編譯器不需要合成它。 由於這個屬性，執行時間會拒絕載入參考元件以執行（但可以在僅限反映模式中載入）。

確切的參考元件結構詳細資料取決於編譯器版本。 如果判斷為不會影響公用 API 介面，較新版本可能會選擇排除更多的中繼資料。

> [!NOTE]
> 本節中的資訊僅適用于從 c # 版本7.1 或 Visual Basic 版本15.3 開始的 Roslyn 編譯器所產生的參考元件。 .NET Framework 和 .NET Core 程式庫的參考元件結構在某些詳細資料中可能會有不同，因為它們會使用自己產生參考元件的機制。 例如，它們可能會有完全空白的方法主體，而不是 `throw null` 主體。 但是一般原則仍然適用：它們沒有可使用的方法，而且只包含對公用 API 觀點有明顯影響的成員的中繼資料。

## <a name="see-also"></a>另請參閱

- [.NET 中的組件](index.md)
- [Framework 目標概觀](/visualstudio/ide/visual-studio-multi-targeting-overview)
- [如何：使用參考管理員加入或移除參考](/visualstudio/ide/how-to-add-or-remove-references-by-using-the-reference-manager)
