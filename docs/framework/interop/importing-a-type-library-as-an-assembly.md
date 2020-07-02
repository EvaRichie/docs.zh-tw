---
title: 匯入類型程式庫做為組件
description: 匯入類型程式庫（其中包含 COM 類型定義）做為元件。 瞭解從型別程式庫建立中繼資料的方式，產生 interop 元件。
ms.date: 03/30/2017
helpviewer_keywords:
- importing type library
- type metadata
- custom wrappers
- metadata
- exposing COM components to .NET Framework
- Type Library Importer
- interoperation with unmanaged code, importing type library
- interoperation with unmanaged code, exposing COM components
- type libraries
- TypeLibConverter class, importing type library as assembly
- COM interop, importing type library
- COM interop, exposing COM components
ms.assetid: d1898229-cd40-426e-a275-f3eb65fbc79f
ms.openlocfilehash: e5187e3c2ce533f25a38e93bc3715dd3e2e47c11
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622714"
---
# <a name="importing-a-type-library-as-an-assembly"></a>匯入類型程式庫做為組件

COM 類型定義通常位於型別程式庫中。 反之，符合 CLS 的編譯器則是在組件中產生型別中繼資料。 這兩種類型資訊的來源有相當大的差異。 本主題描述從型別程式庫產生中繼資料的技術。 產生的組件稱為 Interop 組件，其包含的類型資訊可讓 .NET Framework 應用程式使用 COM 類型。

有兩種方式可讓此類型資訊能夠用於應用程式中：

- 使用僅限設計階段的 interop 元件：從 .NET Framework 4 開始，您可以指示編譯器將 interop 元件的類型資訊內嵌到可執行檔。 編譯器只會內嵌應用程式使用的類型資訊。 您不必與應用程式一起部署 Interop 組件。 這是建議使用的技巧。

- 部署 Interop 組件：您可以建立 Interop 組件的標準參考。 在此情況下，Interop 組件必須與您的應用程式一起部署。 如果您運用這項技巧，但不使用私用的 COM 元件，請一律參考 COM 元件作者發佈的主要 Interop 組件 (PIA)，這是您想要併入 Managed 程式碼的 COM 元件。 如需產生和使用主要 Interop 組件的詳細資訊，請參閱[主要 Interop 組件](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/aax7sdch(v=vs.100))。

當您使用僅限設計階段的 Interop 組件時，可以內嵌 COM 元件作者所發佈之主要 Interop 組件的類型資訊。 不過，您不必與應用程式一起部署主要 Interop 組件。

使用僅限設計階段 Interop 組件會減少應用程式的大小，因為大部分的應用程式不會使用 COM 元件的所有功能。 編譯器在內嵌類型資訊時非常有效；如果應用程式只使用 COM 介面的部分方法，則編譯器不會內嵌未使用的方法。 當具有內嵌類型資訊的應用程式與其他此類應用程式互動，或與使用主要 Interop 組件的應用程式互動時，通用語言執行平台會使用類型相等規則，來判斷兩個類型是否使用相同的名稱表示相同的 COM 類型。 您不需要知道這些規則，就可使用 COM 物件。 不過，如果對這些規則感興趣，請參閱[類型相等和內嵌 Interop 類型](type-equivalence-and-embedded-interop-types.md)。

## <a name="generating-metadata"></a>產生中繼資料

COM 類型程式庫可以是單獨的檔案，副檔名為 .tlb (例如 Loanlib.tlb)。 有些型別程式庫則會嵌入在 .dll 或 .exe 檔案的資源區段中。 型別程式庫資訊的其他來源為 .olb 和 .ocx 檔案。

找到包含目標 COM 類型實作的型別程式庫之後，您可以使用下列選項，產生包含類型中繼資料的 Interop 組件：

- Visual Studio

  Visual Studio 會自動將型別程式庫中的 COM 類型轉換為組件中的中繼資料。 如需指示，請參閱[如何：將參考加入至類型程式庫](how-to-add-references-to-type-libraries.md)。

- [型別程式庫匯入工具 (Tlbimp.exe)](../tools/tlbimp-exe-type-library-importer.md)

  型別程式庫匯入工具提供命令列選項，可以調整產生的 Interop 檔案的中繼資料、從現有型別程式庫匯入型別，以及產生 Interop 組件和命名空間。 如需指示，請參閱[何：從型別程式庫產生 Interop 組件](how-to-generate-interop-assemblies-from-type-libraries.md)。

- <xref:System.Runtime.InteropServices.TypeLibConverter?displayProperty=nameWithType> 類別

  這個類別提供將型別程式庫中的 coclass 和介面轉換為組件內中繼資料的方法。 它會產生與 Tlbimp.exe 相同的中繼資料輸出。 不過，不同於 Tlbimp.exe，<xref:System.Runtime.InteropServices.TypeLibConverter> 類別可以將記憶體內部型別程式庫轉換為中繼資料。

- 自訂包裝函式

  當型別程式庫無法使用或不正確時，其中一項選擇就是在 Managed 原始程式碼中建立類別或介面的重複定義。 然後，您可以使用以執行階段為目標的編譯器編譯這個原始程式碼，以產生組件中的中繼資料。

  若要以手動方式定義 COM 類型，您必須擁有下列項目的存取權：

  - 要定義的 coclass 和介面的精確描述。

  - 可產生適當 .NET Framework 類別定義的編譯器，例如 C# 編譯器。

  - 型別程式庫轉換為組件的轉換規則知識。

  撰寫自訂包裝函式是進階技術。 如需如何產生自訂包裝函式的詳細資訊，請參閱[自訂標準包裝函式](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/h7hx9abd(v=vs.100))。

 如需 COM Interop 匯入處理序的詳細資訊，請參閱[型別程式庫至組件轉換的摘要](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/k83zzh38(v=vs.100))。

## <a name="see-also"></a>另請參閱

- <xref:System.Runtime.InteropServices.TypeLibConverter>
- [將 COM 元件公開給 .NET Framework](exposing-com-components.md)
- [型別程式庫至組件轉換的摘要](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/k83zzh38(v=vs.100))
- [Tlbimp.exe （類型程式庫匯入工具）](../tools/tlbimp-exe-type-library-importer.md)
- [自訂標準包裝函式](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/h7hx9abd(v=vs.100))
- [在受控程式碼中使用 COM 型別](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/3y76b69k(v=vs.100))
- [編譯 Interop 專案](compiling-an-interop-project.md)
- [部署 Interop 應用程式](deploying-an-interop-application.md)
- [作法：將參考新增至型別程式庫](how-to-add-references-to-type-libraries.md)
- [作法：從型別程式庫產生 Interop 組件](how-to-generate-interop-assemblies-from-type-libraries.md)
