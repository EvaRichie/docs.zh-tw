---
title: 作法：從全域組件快取移除組件
description: 瞭解如何使用全域組件快取工具（Gacutil.exe）或 Windows Installer，從 .NET 中的全域組件快取移除元件。
ms.date: 03/30/2017
helpviewer_keywords:
- assemblies [.NET Framework], global assembly cache
- Gacutil.exe
- global assembly cache, removing assemblies
- strong-named assemblies, global assembly cache
- removing assemblies from global assembly cache
- deleting assemblies in global assembly cache
- Global Assembly Cache tool
- GAC (global assembly cache), removing assemblies
ms.assetid: acdcc588-b458-436d-876c-726de68244c1
ms.openlocfilehash: e3a596ea6029ded190c33032e96b601de9d4012d
ms.sourcegitcommit: 1c37a894c923bea021a3cc38ce7cba946357bbe1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2020
ms.locfileid: "85104761"
---
# <a name="how-to-remove-an-assembly-from-the-global-assembly-cache"></a>作法：從全域組件快取移除組件

從全域組件快取 (GAC) 移除組件的方式有兩種：

- 使用[全域組件快取工具 (Gacutil.exe)](../tools/gacutil-exe-gac-tool.md)。 若要解除安裝開發和測試期間放在 GAC 中的組件，可使用這個選項。

- 使用 [Windows Installer](/windows/desktop/Msi/windows-installer-portal)。 若要解除安裝測試安裝套件時及針對生產系統所使用的組件，則應該使用這個選項。

## <a name="removing-an-assembly-with-gacutilexe"></a>使用 Gacutil.exe 移除組件

在命令提示字元中，輸入下列命令：

**gacutil – u**\<*assembly name*>

在這個命令中，「組件名稱」** 是要從全域組件快取移除的組件名稱。

> [!WARNING]
> 您不應該使用 Gacutil.exe 移除生產系統上的組件，因為某個應用程式可能仍需要這個組件。 您應該改用 Windows Installer，以維護安裝在 GAC 中之每個組件的參考計數。

下列範例會 `hello.dll` 從全域組件快取中移除名為的元件：

```console
gacutil -u hello
```

## <a name="removing-an-assembly-with-windows-installer"></a>使用 Windows Installer 移除組件

從 [控制台]**** 中的 [程式和功能]**** 應用程式，選取您要解除安裝的應用程式。 如果安裝套件將組件放在 GAC 中，Windows Installer 會在其他應用程式未使用這些組件時，將組件移除。

> [!NOTE]
> Windows Installer 會維護安裝在 GAC 中之組件的參考計數。 只有在組件的參考計數到達零時 (表示 Windows Installer 套件所安裝的任何應用程式都未使用這個組件)，才能從 GAC 中移除組件。

## <a name="see-also"></a>另請參閱

- [使用組件和全域組件快取](working-with-assemblies-and-the-gac.md)
- [如何：將元件安裝到全域組件快取中](install-assembly-into-gac.md)
- [Gacutil.exe （全域組件快取工具）](../tools/gacutil-exe-gac-tool.md)
