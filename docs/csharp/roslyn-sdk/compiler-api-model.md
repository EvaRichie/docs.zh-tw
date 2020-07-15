---
title: .NET Compiler Platform SDK 概念和物件模型
description: 這個概觀提供有效率地使用 .NET 編譯器 SDK 所需的背景。 您將學習 API 層、所含的主要類型和整體物件模型。
ms.date: 07/13/2020
ms.custom: mvc
ms.openlocfilehash: a65d282dd3c58279bbfd635c0386d50ce3f30055
ms.sourcegitcommit: e7748001b1cee80ced691d8a76ca814c0b02dd9b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/14/2020
ms.locfileid: "86374464"
---
# <a name="understand-the-net-compiler-platform-sdk-model"></a>了解 .NET Compiler Platform SDK 模型

編譯器會處理您遵循結構化規則所撰寫的程式碼，而結構化規則通常與人們閱讀和了解程式碼的方式不同。 編譯器所使用模型的基本了解務必了解您在建置 Roslyn 工具時所使用的 API。

## <a name="compiler-pipeline-functional-areas"></a>編譯器管線功能區域

.NET Compiler Platform SDK 透過提供可鏡像傳統編譯器管線的 API 層，以將 C# 和 Visual Basic 編譯器的程式碼分析公開為取用者。

![編譯器管線將原始程式碼處理為物件程式碼的步驟](media/compiler-api-model/compiler-pipeline.png)

此管線的每個階段都是個別元件。 首先，剖析階段會權杖化，並將原始程式文字剖析為遵循語言文法的語法。 其次，宣告階段會分析來源及匯入的中繼資料，以形成具名符號。 接下來，繫結階段會比對程式碼中的識別碼與符號。 最後，發出階段會發出具有編譯器所建置之所有資訊的組件。

![編譯器管線 API 可存取屬於編譯器管線一部分的每個步驟](media/compiler-api-model/compiler-pipeline-api.png)

對應至所有這些階段，.NET Compiler Platform SDK 會公開物件模型，以允許存取該階段的資訊。 剖析階段會公開語法樹狀結構，宣告階段會公開階層式符號表，系結階段會公開編譯器的語義分析結果，而發出階段是產生 IL 位元組代碼的 API。

![編譯器管線各步驟可從編譯器 API 使用的語言服務](media/compiler-api-model/compiler-pipeline-lang-svc.png)

每個編譯器都會將這些元件一起合併為單一端對端整體。

這些 API 與 Visual Studio 使用的相同。 例如，程式碼大綱和格式化功能會使用語法樹狀結構、**物件瀏覽器**和導覽功能使用符號表、重構和 [**移至定義**] 使用語義模型，而 [**編輯後繼續**] 則會使用所有這些，包括發出 API。

## <a name="api-layers"></a>API 層

.NET 編譯器 SDK 是由數個 Api 層所組成：編譯器 Api、診斷 Api、腳本 Api 和工作區 Api。

### <a name="compiler-apis"></a>編譯器 API

編譯器層所包含的物件模型對應至編譯器管線的每個階段所公開的資訊 (語法和語意)。 編譯器層也包含單一編譯器叫用的不可變快照集，包含組件參考、編譯器選項和原始程式碼檔。 有兩個不同的 API 代表 C# 語言和 Visual Basic 語言。 這兩個 Api 在圖形中很類似，但會針對每個個別語言量身打造。 此層沒有與 Visual Studio 元件的相依性。

### <a name="diagnostic-apis"></a>診斷 API

進行分析時，編譯器可能會產生一組診斷，其涵蓋語法、語意和明確指派錯誤的所有項目，以及各種警告和參考性診斷。 編譯器 API 層會透過允許將使用者定義分析器插入編譯程序的可延伸 API，公開診斷。 它可以產生使用者定義診斷 (例如 StyleCop 或 FxCop 這類工具所產生的診斷) 和編譯器定義診斷。 以這種方式產生診斷，有其優點：使用 MSBuild 和 Visual Studio 之類的工具進行自然整合，這取決於診斷，例如根據原則停止組建，以及在編輯器中顯示即時波浪線，以及建議程式碼修正。

### <a name="scripting-apis"></a>指令碼 API

裝載和指令碼 API 是編譯器層的一部分。 您可以使用它們來執行程式碼片段以及累積執行階段執行內容。
C# 互動 REPL (「讀取、求值、輸出」迴圈) 會使用這些 API。 REPL 可讓您使用 C# 作為指令碼語言，並在撰寫時以互動方式執行程式碼。

### <a name="workspaces-apis"></a>工作區 API

[工作區] 層會包含工作區 API，這是執行程式碼分析以及重構整個方案的起點。 它可協助您將方案中所有專案的相關資訊組織成單一物件模型，讓您直接存取編譯器層物件模型，而不需要剖析檔案、設定選項，或管理專案對專案的相依性。

此外，工作區層具有實作程式碼分析以及重構工具時所使用的一組 API，而這些工具在 Visual Studio IDE 這類主機環境內運作。 範例包含 [尋找所有參考]、[格式] 和 [程式碼產生 API]。

此層沒有與 Visual Studio 元件的相依性。
