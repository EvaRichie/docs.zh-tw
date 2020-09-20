---
title: F# 互動 (dotnet) 參考
description: '瞭解如何使用 F# 互動 (dotnet fsi) ，以互動方式在主控台執行 F # 程式碼，或執行 F # 腳本。'
ms.date: 08/20/2020
f1_keywords:
- VS.ToolsOptionsPages.F#_Tools.F#_Interactive
ms.openlocfilehash: ae8d68140ddec8e18ee23e9a43b548907e1ab5c4
ms.sourcegitcommit: fe8877e564deb68d77fa4b79f55584ac8d7e8997
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/17/2020
ms.locfileid: "90720318"
---
# <a name="interactive-programming-with-f"></a>使用 F 的互動式程式設計\#

F# 互動 (dotnet fsi) 用來以互動方式在主控台執行 F # 程式碼，或執行 F # 腳本。 換句話說，F# Interactive 會執行 F# 語言的 REPL (讀取、評估、列印迴圈)。

若要從主控台執行 F# 互動，請執行 `dotnet fsi` 。 您將可以 `dotnet fsi` 在任何 .NET SDK 中找到。

如需可用命令列選項的資訊，請參閱 [F# Interactive 選項](../../language-reference/fsharp-interactive-options.md)。

若要透過 Visual Studio 執行 F# Interactive，您可以按一下標示為 **F# Interactive** 的合適工具列按鈕，或使用按鍵 **Ctrl+Alt+F**。 如此會開啟互動式視窗，也就是執行 F# Interactive 工作階段的工具視窗。 您也可以選取要在互動式視窗中執行的一些程式碼，然後按按鍵組合 **Alt + Enter**。 F# Interactive 會隨即在標示為 **F# Interactive** 的工具視窗中啟動。 當您使用這個按鍵組合時，請確定編輯器視窗具有焦點。

不論是使用主控台還是否 Visual Studio，命令提示字元都會出現，表示解譯器在等待您輸入。 您可以如同在程式碼檔案中一樣輸入程式碼。 若要編譯並執行程式碼，請輸入兩個分號 (**;;**) 以終止一或數行的輸入。

F# Interactive 會嘗試編譯程式碼，如果成功的話，它會執行程式碼，並列印它所編譯的類型與值的簽章。 如果發生錯誤，解譯器就會列印錯誤訊息。

在同一個工作階段中輸入的程式碼，可以存取先前輸入的所有建構，因此您可以建置程式。 若有需要，可利用 [工具] 視窗中的延伸緩衝區，視需要將程式碼複製到檔案。

在 Visual Studio 中執行 F# Interactive 時，會與專案分開執行，因此，舉例來說，除非您將函式的程式碼複製到 [互動] 視窗，否則無法使用在 F# Interactive 中專案內所定義的建構。

若您開啟了參考某些程式庫的專案，則可以透過方案總管**** 參考 F# Interactive 中的這些程式庫。 若要參考 F# Interactive 中的程式庫，請展開 [參考] **** 節點，開啟程式庫的捷徑功能表，然後選擇 [傳送至 F# Interactive]****。

您可以調整設定來控制 F# Interactive 命令列引數 (選項)。 在 [工具]**** 功能表上，選取 [選項...]****，然後展開 [F# 工具]****。 您只能變更 F# Interactive 選項和 [64 位元 F# Interactive] **** 這兩項設定，而且只有在 64 位元電腦上執行 F# Interactive 時才相關。 這項設定會判斷您要執行專用的 64 位元版 fsi.exe 或 fsianycpu.exe，它會使用電腦架構判斷要以 32 位元或 64 位元處理序執行。

## <a name="scripting-with-f"></a>使用 F 編寫腳本\#

指令碼使用副檔名 **.fsx** 或 **.fsscript**。 您可以直接執行 **dotnet fsi** 並指定 f # 原始程式碼的指令檔名，而 f # interactive 會即時讀取程式碼並執行它，而不是編譯原始程式碼，然後稍後再執行已編譯的元件。

## <a name="differences-between-the-interactive-scripting-and-compiled-environments"></a>互動式、腳本和編譯環境之間的差異

當您編譯 F# Interactive 中的程式碼時，無論是以互動方式執行或是執行指令碼，都會定義符號 **INTERACTIVE**。 當您在編譯器中編譯程式碼時，會定義符號 **COMPILED**。 因此，如果已編譯模式和互動式模式中的程式碼必須不同，可以使用條件式編譯的前置處理器指示詞，決定要使用哪一種模式。

當您要在 F# Interactive 中執行在執行編譯器時無法使用的指令碼時，有一些指示詞可用。 下表摘要說明使用 F# Interactive 時可用的指示詞。

|指示詞|描述|
|---------|-----------|
|**#help**|顯示可用指示詞的詳細資訊。|
|**#I**|指定加上引號的組件搜尋路徑。|
|**#load**|讀取原始程式檔、進行編譯，並加以執行。|
|**#quit**|終止 F# Interactive 工作階段。|
|**#r**|參考組件。|
|**#time ["on"&#124;"off"]**|**#time** 會自行切換是否顯示效能資訊。 當它啟用時，F# Interactive 會測量所解譯及執行的每個程式碼區段之即時、CPU 時間及記憶體回收資訊。|

當您在 F# Interactive 中指定檔案或路徑時，應該要有一個字串常值。 因此，檔案和路徑必須以引號括住，並遵循一般的逸出字元。 此外，您可以使用 @ 字元，讓 F# Interactive 能將包含路徑的字串，解譯為逐字字串。 這會導致 F# Interactive 會忽略所有逸出字元。

已編譯模式和互動式模式之間，其中一項差異是存取命令列引數的方式。 在編譯模式中是使用 **System.Environment.GetCommandLineArgs**。 而在指令碼中則是使用 **fsi.CommandLineArgs**。

下列程式碼說明如何建立可讀取指令碼中命令列引數的函式，同時也會示範如何從指令碼參考另一個組件。 第一個程式碼檔案 **MyAssembly.fs** 是要參考之組件的程式碼。 請使用命令列 **fsc -a MyAssembly.fs** 編譯這個檔案，然後使用下列命令列以指令碼形式執行第二個檔案：**fsi --exec file1.fsx** test

```fsharp
// MyAssembly.fs
module MyAssembly
let myFunction x y = x + 2 * y
```

```fsharp
// file1.fsx
#r "MyAssembly.dll"

printfn "Command line arguments: "

for arg in fsi.CommandLineArgs do
    printfn "%s" arg

printfn "%A" (MyAssembly.myFunction 10 40)
```

輸出如下所示：

```console
Command line arguments:
file1.fsx
test
90
```

## <a name="package-management-in-f-interactive"></a>F# 互動中的套件管理

[!NOTE] 封裝管理可作為的預覽功能 `dotnet fsi` ，隨附于 `3.1.300` 和更高版本的 .net sdk，以及所有 `5.*` 版本的 .net sdk。 若要在此預覽版本中啟用它，請 `dotnet fsi` 使用 `--langversion:preview` 引數執行。

`#r`在 F# 互動中參考 DLL 的語法也可以透過下列語法來參考 nuget 套件：

```fsharp
#r "nuget: <package name>
```

例如，若要參考 `FSharp.Data` 封裝，請使用下列 `#r` 參考：

```fsharp
#r "nuget: FSharp.Data"
```

執行這一行之後，最新版本的 `FSharp.Data` 套件將會下載至您的 nuget 快取，並在目前的 F# 互動會話中參考。

除了封裝名稱之外，還可以透過簡短的語法參考封裝的特定版本：

```fsharp
#r "nuget: FSharp.Data, 3.3.2"
```

或以更明確的方式：

```fsharp
#r "nuget: FSharp.Data, Version=3.3.2"
```

## <a name="related-articles"></a>相關文章

|Title|描述|
|-----|-----------|
|[F# Interactive 選項](../../language-reference/fsharp-interactive-options.md)|描述 F# 互動、fsi.exe 的命令列語法和選項。|
