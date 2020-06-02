---
title: 全球化與當地語系化 .NET 應用程式
ms.date: 06/08/2018
ms.technology: dotnet-standard
helpviewer_keywords:
- international applications [.NET]
- globalization [.NET], encoding
- global applications
- internationalization
- world-ready applications
- application development [.NET], globalization
- multilingual application development
ms.assetid: 9a59696b-d89b-45bd-946d-c75da4732d02
ms.openlocfilehash: 10d07a02a7ff744a87b920fd97df24b076c22cc3
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288286"
---
# <a name="globalizing-and-localizing-net-applications"></a>全球化與當地語系化 .NET 應用程式

開發世界通用的應用程式，包括可以當地語系化為一或多種語言的應用程式，這個開發過程包含三個步驟：全球化、檢閱是否可當地語系化，以及當地語系化。

[全球化](globalization.md)

這個步驟包含設計和撰寫文化特性中性和語言中性的應用程式程式碼，且該應用程式支援當地語系化使用者介面和所有使用者的區域資料。 這個步驟包含不是根據文化特性假設做出的設計和開發決策。 即使全球化的應用程式並未當地語系化，但是它的設計和撰寫方式讓後續能夠相對方便地進行一種或多種語言的當地語系化。

[當地語系化可行性檢閱](localizability-review.md)

這個步驟包含檢閱應用程式的程式碼和設計，確保它可以輕鬆地當地語系化並識別當地語系化時可能發生的阻礙，以及確認應用程式的可執行碼與其資源分開。 如果全球化階段有效，則當地語系化能力檢閱將確認全球化期間所選擇的設計和編碼。 當地語系化能力階段也可能會找出任何其餘的問題，如此應用程式的原始程式碼就不需要在當地語系化階段進行修改。

[當地語系化](localization.md)

這個步驟包含自訂特定文化特性或地區的應用程式。 如果已正確執行全球化和當地語系化能力的步驟，則當地語系化的主要工作就是轉譯使用者介面。

依照下列三個步驟執行可提供兩項優點：

- 您不需要重新設計用於支援單一文化特性 (例如英文 (美國)) 的應用程式，即可支援其他文化特性。

- 可產生更穩定且較少 Bug 的當地語系化應用程式。

.NET 提供各種開發全球通用及當地語系化應用程式的支援。 特別是，.NET 類別庫中的許多類型成員，會傳回反映目前使用者文化特性或特定文化特性慣例的值，藉以協助全球化。 此外，.NET 還支援附屬組件，可簡化當地語系化應用程式的程序。

如需其他資訊，請參閱[全球化文件](/globalization/)。

## <a name="in-this-section"></a>本節內容

[全球化](globalization.md)

討論建立世界通用應用程式的第一個階段，包括設計和撰寫文化特性中性和語言中性之應用程式的程式碼。

[.NET 全球化和 ICU](globalization-icu.md)

描述 .NET 全球化如何使用[Unicode （ICU）的國際元件](http://site.icu-project.org/home)。

[當地語系化可行性檢閱](localizability-review.md)

討論建立當地語系化應用程式的第二個階段，包括識別當地語系化過程中可能遭遇到的阻礙。

[當地語系化](localization.md)

討論建立當地語系化應用程式的最後一個階段，包括自訂特定區域或文化特性的應用程式使用者介面。

[不區分文化特性 (Culture) 的字串作業](culture-insensitive-string-operations.md)

說明如何使用預設為區分文化特性的 .NET 方法與類別，來取得不區分文化特性的結果。

[開發世界性的應用程式的最佳做法](best-practices-for-developing-world-ready-apps.md)

說明進行全球化、當地語系化和開發世界性的 ASP.NET 的最佳實施方針。

## <a name="reference"></a>參考

- <xref:System.Globalization?displayProperty=nameWithType> 命名空間

   包含類別，定義與文化特性相關的資訊，包括語言、國家/地區、使用中的日曆、日期、貨幣和數字的格式模式，以及字串的排序順序。

- <xref:System.Resources> 命名空間

   提供建立、管理和使用資源的類別。

- <xref:System.Text> 命名空間

   包含表示 ASCII、ANSI、Unicode 和其他字元編碼方式的類別。

- [Resgen.exe （資源檔產生器）](../../framework/tools/resgen-exe-resource-file-generator.md)

   描述如何使用 Resgen.exe 來轉換 .txt 檔案和 XML 資源格式 (.resx) 檔案到通用語言執行平台二進位資源檔。

- [Winres.exe .exe （Windows Forms 資源編輯器）](../../framework/tools/winres-exe-windows-forms-resource-editor.md)

   描述如何使用 Winres.exe 將 Windows Form 表單當地語系化。
