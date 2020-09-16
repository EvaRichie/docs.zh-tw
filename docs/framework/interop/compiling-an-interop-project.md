---
title: 編譯 Interop 專案
description: 複習如何編譯 COM interop 專案，如果它們參考一或多個包含已匯入 COM 類型的元件，則這些專案會像 managed 專案一樣編譯。
ms.date: 03/30/2017
helpviewer_keywords:
- interoperation with unmanaged code, compiling
- COM interop, compiling
- exposing COM components to .NET Framework
- compiling interop projects
- interoperation with unmanaged code, exposing COM components
- COM interop, exposing COM components
ms.assetid: 6fcf6588-5e25-41af-b4ae-780974f2c3df
ms.openlocfilehash: 1cf5bdbedd53227e812b0d2ed97778ab34a81444
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90557093"
---
# <a name="compiling-an-interop-project"></a>編譯 Interop 專案

會編譯參考一或多個包含已匯入 COM 類型之組件的 COM Interop 專案，就像任何其他 Managed 專案一樣。 您可以參考 Visual Studio 這類開發環境中的 Interop 組件，也可以在使用命令列編譯器時參考它們。 在任一情況下，若要正常編譯，則 Interop 組件必須與其他專案檔位於相同的目錄中。

 有兩種方法可以參考 Interop 組件：

- 內嵌的 interop 類型：從 .NET Framework 4 和 Visual Studio 2010 開始，您可以指示編譯器將 interop 元件的類型資訊內嵌到可執行檔。 這是建議使用的技巧。

- 部署 Interop 組件：您可以建立 Interop 組件的標準參考。 在此情況下，Interop 組件必須與您的應用程式一起部署。

 [在 Managed 程式碼中使用 COM 類型](/previous-versions/dotnet/netframework-4.0/3y76b69k(v=vs.100))會更詳細討論這兩種技術之間的差異。

 [逐步解說：在 Visual Studio 中內嵌來自 Managed 元件的類型](../../standard/assembly/embed-types-visual-studio.md)，以 Visual Studio 內嵌 interop 類型。

 若要使用命令列編譯器來參考 interop 元件，並將類型資訊內嵌至可執行檔，請使用 [-link (c # 編譯器選項) ](../../csharp/language-reference/compiler-options/link-compiler-option.md) 或 [-link (Visual Basic) ](../../visual-basic/reference/command-line-compiler/link.md) 編譯器參數，並指定 interop 元件的名稱。

> [!NOTE]
> Visual C++ 應用程式無法內嵌類型資訊，但可以與執行的應用程式或增益集交互操作。

 若要在部署包含主要 Interop 組件的應用程式時進行編譯，請使用 **/reference** 編譯器參數，並指定 Interop 組件的名稱。

## <a name="see-also"></a>另請參閱

- [將 COM 元件公開給 .NET Framework](exposing-com-components.md)
- [語言獨立性以及與語言無關的元件](../../standard/language-independence-and-language-independent-components.md)
- [在受控程式碼中使用 COM 型別](/previous-versions/dotnet/netframework-4.0/3y76b69k(v=vs.100))
- [逐步解說：在 Visual Studio 中內嵌來自 Managed 組件的型別](../../standard/assembly/embed-types-visual-studio.md)
- [匯入類型程式庫做為組件](importing-a-type-library-as-an-assembly.md)
