---
description: -platform (C# 編譯器選項)
title: -platform (C# 編譯器選項)
ms.date: 07/20/2015
f1_keywords:
- /platform
helpviewer_keywords:
- platform compiler option [C#]
- -platform compiler option [C#]
- /platform compiler option [C#]
ms.assetid: c290ff5e-47f4-4a85-9bb3-9c2525b0be04
ms.openlocfilehash: 3fdb030dfc141b011f5faa827a4e4bb45ae38d19
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "89466010"
---
# <a name="-platform-c-compiler-options"></a>-platform (C# 編譯器選項)

指定哪個 Common Language Runtime (CLR) 版本可以執行組件。

## <a name="syntax"></a>語法

```console
-platform:string
```

## <a name="parameters"></a>參數

`string` \
anycpu (預設值)、anycpu32bitpreferred、ARM、x64、x86 或 Itanium。

## <a name="remarks"></a>備註

- **anycpu** (預設值) 會將組件編譯為可在所有平台上執行。 您的應用程式會盡可能做為 64 位元處理序執行，而且只有在 32 位元模式可用時才會回到該模式。

- **anycpu32bitpreferred** 會將組件編譯為可在所有平台上執行。 您的應用程式在同時支援 64 位元和 32 位元應用程式的系統上會以 32 位元模式執行。 您只能針對以 .NET Framework 4.5 或更新版本為目標的專案指定此選項。

- **ARM** 會將您的組件編譯為可在採用 Advanced RISC Machine (ARM) 處理器的電腦上執行。

- **ARM64** 會編譯您的組件，使其可由具備支援 A64 指令集進階 RISC 機器 (ARM) 處理器電腦上的 64 位元 CLR 執行。

- 在支援 AMD64 或 EM64T 指令集的電腦上，**x64** 會將組件編譯成由 64 位元 CLR 執行。

- **x86** 會將組件編譯為以 32 位元、與 x86 相容的 CLR 執行。

- **Itanium** 會將組件編譯為可以在使用 Itanium 處理器的電腦上以 64 位元 CLR 執行。

在 64 位元 Windows 作業系統上：

- 使用 **-platform:x86** 所編譯的組件會在 WOW64 下執行的 32 位元 CLR 上執行。

- 使用 **-platform:anycpu** 所編譯的 DLL 會在與載入它的程序相同的 CLR 上執行。

- 使用 **-platform:anycpu** 所編譯的可執行檔會在 64 位元 CLR 上執行。

- 使用 **-platform:anycpu32bitpreferred** 所編譯的可執行檔會在 32 位元 CLR 上執行。

**Anycpu32bitpreferred** 設定只對可執行檔 ( 有效。EXE) 檔案，且需要 .NET Framework 4.5 或更新版本。

如需開發要在 Windows 64 位元作業系統上執行之應用程式的詳細資訊，請參閱 [64 位元應用程式](../../../framework/64-bit-apps.md)。

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 開發環境中設定這個編譯器選項

1. 開啟專案的 [屬性]  頁面。

2. 按一下 [建置] 屬性頁面。

3. 修改 [ **平臺目標** ] 屬性，並針對以 .NET Framework 4.5 或更新版本為目標的專案，選取或清除 [ **偏好 32** 位] 核取方塊。

> [!NOTE]
> `-platform` 無法在 Visual c # Express 的開發環境中使用。

如需如何以程式設計方式設定這個編譯器選項的資訊，請參閱 <xref:VSLangProj80.CSharpProjectConfigurationProperties3.PlatformTarget%2A>。

## <a name="example"></a>範例

下列範例示範如何使用 **-platform** 選項，指定應用程式應該在 64 位元 Windows 作業系統上以 64 位元 CLR 執行。

```console
csc -platform:anycpu filename.cs
```

## <a name="see-also"></a>另請參閱

- [C# 編譯器選項](index.md)
- [管理專案和方案屬性](/visualstudio/ide/managing-project-and-solution-properties)
