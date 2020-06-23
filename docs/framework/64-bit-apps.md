---
title: 64 位元應用程式
description: 取得在 Windows 64 位作業系統上設定應用程式的相關資訊，例如原生64位應用程式或 WOW64 （windows 64 位上的 Windows 32 位）。
ms.date: 03/30/2017
helpviewer_keywords:
- applications [C++], 64-bit
- 64-bit applications [C++]
- 64-bit programming [C++]
ms.assetid: fd4026bc-2c3d-4b27-86dc-ec5e96018181
ms.openlocfilehash: 4589d7a070a477dcb229fbaea686f6c6ff7d7e08
ms.sourcegitcommit: 45c8eed045779b70a47b23169897459d0323dc89
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "84989990"
---
# <a name="64-bit-applications"></a>64 位元應用程式
您在編譯應用程式時，可以指定其應以原生應用程式在 Windows 64 位元作業系統上或在 WOW64 下 (Windows 64 位元上的 Windows 32 位元) 執行。 WOW64 是讓 32 位元應用程式可在 64 位元系統上執行的相容性環境。 所有 64 位元版本的 Windows 作業系統中都包含 WOW64。  
  
## <a name="running-32-bit-vs-64-bit-applications-on-windows"></a>在 Windows 上執行 32 位元與 64 位元應用程式的比較  
 所有在 .NET Framework 1.0 或 1.1 上建置的應用程式都會被視為在 64 位元作業系統上的 32 位元應用程式，並一律在 WOW64 和 32 位元 Common Language Runtime (CLR) 下執行。 在 .NET Framework 4 或更新版本上建置的 32 位元應用程式也會在 64 位元系統的 WOW64 下執行。  
  
 Visual Studio 在 x86 電腦上安裝 CLR 32 位元版本，而在 64 位元 Windows 電腦上同時安裝 32 位元版本和適當的 CLR 64 位元版本。 (由於 Visual Studio 是 32 位元應用程式，所以安裝在 64 位元系統上時，會在 WOW64 下執行。)  
  
> [!NOTE]
> X86 模擬和 Itanium 處理器系列之 WOW64 子系統的設計會限制應用程式在一個處理器上執行。 這些因素會降低在 Itanium 系統上執行之 32 位元 .NET Framework 應用程式的效能和延展性。 為了增加效能和延展性，我們建議您使用包含 Itanium 系統原生 64 位元支援的 .NET Framework 4。  
  
 根據預設，當您在 64 位元 Windows 作業系統上執行 64 位元 Managed 應用程式時，可以建立不超過 2 GB 的物件。 不過，在 .NET Framework 4.5 中，您可以提高上限。  如需詳細資訊，請參閱[ \<gcAllowVeryLargeObjects> 元素](./configure-apps/file-schema/runtime/gcallowverylargeobjects-element.md)。  
  
 許多組件在 32 位元 CLR 和 64 位元 CLR 上以相同方式執行。 不過，取決於 CLR，有些程式可能會有不同的行為，若它們包含下列一或多項情形：  
  
- 包含視平台而變更大小之成員的結構，(例如任何指標類型)。  
  
- 包含常數大小的指標算術。  
  
- 不正確的平台叫用，或是使用 `Int32` 而不是 `IntPtr` 作為控點的 COM 宣告。  
  
- 將 `IntPtr` 轉換到 `Int32` 的程式碼。  
  
 如需如何將 32 位元應用程式移植到 64 位元 CLR 上執行的詳細資訊，請參閱[將 32 位元受控碼移轉至 64 位元](https://docs.microsoft.com/previous-versions/dotnet/articles/ms973190(v=msdn.10))。  
  
## <a name="general-64-bit-programming-information"></a>64 位元程式設計的一般資訊  
 如需 64 位元程式設計的一般資訊，請參閱下列文件：  
  
- 在 Windows SDK 文件中，請參閱 [64 位元 Windows 程式設計指南](/windows/win32/winprog64/programming-guide-for-64-bit-windows)。  
  
- 如需 Visual Studio 支援建立 64 位元應用程式的相關資訊，請參閱 [Visual Studio IDE 64 位元支援](/visualstudio/ide/visual-studio-ide-64-bit-support)。  
  
## <a name="compiler-support-for-creating-64-bit-applications"></a>建立 64 位元應用程式的編譯器支援  
 根據預設，當您在 32 位元或 64 位元的電腦上使用 .NET Framework 應用程式建置應用程式時，應用程式會以原生應用程式在 64 位元電腦上執行 (也就是不在 WOW64 下)。 下表列出說明如何使用 Visual Studio 編譯器來建立將會在 WOW64 下以原生執行 (或兩者) 之 64 位元應用程式的文件。  
  
|編譯器|編譯器選項|  
|--------------|---------------------|  
|Visual Basic|[-platform （Visual Basic）](../visual-basic/reference/command-line-compiler/platform.md)|  
|Visual C#|[-platform （c # 編譯器選項）](../csharp/language-reference/compiler-options/platform-compiler-option.md)|  
|Visual C++|您可以使用 **/clr:safe** 建立各平台適用的 Microsoft 中繼語言 (MSIL) 應用程式。 如需詳細資訊，請參閱[-clr （Common Language Runtime 編譯）](/cpp/build/reference/clr-common-language-runtime-compilation)。<br /><br /> Visual C++ 針對每個 64 位元作業系統包含了個別的編譯器。 如需如何使用 Visual C++ 建立可在 64 位元 Windows 作業系統上執行之原生應用程式的詳細資訊，請參閱 [64 位元程式設計](/cpp/build/configuring-programs-for-64-bit-visual-cpp)。|  
  
## <a name="determining-the-status-of-an-exe-file-or-dll-file"></a>判斷 .exe 檔或 .dll 檔的狀態  
 若要判斷 .exe 檔或 .dll 檔案是否只能在特定平台上或在 WOW64 下執行，請使用不含選項的 [CorFlags.exe (CorFlags 轉換工具)](./tools/corflags-exe-corflags-conversion-tool.md)。 您也可以使用 CorFlags.exe 來變更 .exe 檔或 .dll 檔的平台狀態。 Visual Studio 組件的 CLR 標頭中的執行階段主要版本號碼設為 2，而執行階段次要版本號碼設為 5。 將次要執行階段版本設定為 0 的應用程式會被視為舊版應用程式，並一律在 WOW64 下執行。  
  
 若要以程式設計方式查詢 .exe 或 .dll 以查看其是否只在特定平台上或在 WOW64 下執行，請使用 <xref:System.Reflection.Module.GetPEKind%2A?displayProperty=nameWithType> 方法。
