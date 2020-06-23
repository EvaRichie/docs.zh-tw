---
title: 多檔案組件
description: 使用以 .NET 為目標的多檔案元件，或使用命令列編譯器或 Visual Studio 搭配 Visual C++。 元件中的檔案必須包含組件資訊清單。
ms.date: 08/20/2019
helpviewer_keywords:
- assemblies [.NET Framework], multifile
- entry point for assembly
- compiling assemblies
- command-line compilers
- assembly manifest, multifile assemblies
- code modules
- multifile assemblies
ms.assetid: 13509e73-db77-4645-8165-aad8dfaedff6
ms.openlocfilehash: a5fb41b3b136a325e6b8658da521cba3176e929f
ms.sourcegitcommit: 1c37a894c923bea021a3cc38ce7cba946357bbe1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2020
ms.locfileid: "85104635"
---
# <a name="multifile-assemblies"></a>多檔案組件

您可以使用命令列編譯器或使用 Visual C++ Visual Studio，建立以 .NET Framework 為目標的多檔案元件。 組件中的一個檔案必須包含組件資訊清單。 啟動應用程式的元件也必須包含進入點，例如 `Main` 或 `WinMain` 方法。

例如，假設您有一個應用程式，其中包含兩個程式碼模組： *Client.cs*和*Stringer.cs*。 *Stringer.cs*會建立 `myStringer` *Client.cs*中的程式碼所參考的命名空間。 *Client.cs*包含 `Main` 方法，這是應用程式的進入點。 在此範例中，您會編譯這兩個程式碼模組，然後建立包含組件資訊清單的第三個檔案，而組件資訊清單可啟動應用程式。 組件資訊清單會同時參考*用戶端*和*Stringer*模組。

> [!NOTE]
> 多檔案組件只能有一個進入點，即使組件有多個程式碼模組也是一樣。

您有數個原因可能想要建立多檔案組件：

- 合併以不同語言撰寫的模組。 這是建立多檔案組件的最常見原因。

- 將很少使用的類型放在需要時才下載的模組中，以最佳化應用程式的下載。

    > [!NOTE]
    > 如果您要使用 Microsoft Internet Explorer 建立將使用 `<object>` 標記所下載的應用程式，則一定要建立多檔案組件。 在此情況下，您會建立與程式碼模組不同的檔案，而此檔案只包含組件資訊清單。 Internet Explorer 會先下載組件資訊清單，然後建立背景工作執行緒來下載所需的任何額外模組或組件。 正在下載包含組件資訊清單的檔案時，Internet Explorer 不會回應使用者輸入。 包含組件資訊清單的檔案越小，Internet Explorer 無回應的時間就越短。

- 合併數個開發人員所撰寫的程式碼模組。 雖然每個開發人員都可以將每個程式碼模組編譯為組件，但是將所有模組都放入多檔案組件時，這個動作會將某些未公開的類型強制為公開。

建立元件之後，您可以簽署包含組件資訊清單的檔案，也就是元件，也可以為檔案和元件指定強式名稱，並將它放在全域組件快取中。

## <a name="see-also"></a>另請參閱

- [作法：建置多檔案組件](build-multifile-assembly.md)
- [具有組件的程式](../../standard/assembly/index.md)
