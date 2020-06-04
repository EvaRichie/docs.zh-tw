---
title: -subsystemversion
ms.date: 03/13/2018
helpviewer_keywords:
- /subsystemversion compiler option [Visual Basic]
- -subsystemversion compiler option [Visual Basic]
- subsystemversion compiler option [Visual Basic]
ms.assetid: 08be22b2-f447-4cd3-8203-120b1b920b54
ms.openlocfilehash: 09ddc4bb735b645e09d34198c66dff78183592bf
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403079"
---
# <a name="-subsystemversion-visual-basic"></a>-subsystemversion （Visual Basic）

指定產生的可執行檔可在其上執行的最小子系統版本，進而決定可執行檔可在其上執行的 Windows 版本。 大多數情況下，此選項可確保可執行檔可以利用舊版 Windows 未提供的特定安全性功能。

> [!NOTE]
> 若要指定子系統本身，請使用 [-target](../../../csharp/language-reference/compiler-options/target-compiler-option.md) 編譯器選項。

## <a name="syntax"></a>語法

```vb
-subsystemversion:major.minor
```

## <a name="parameters"></a>參數

`major.minor`

最小必要版本的子系統，以點標記法表示主要和次要版本。 例如，如果您將此選項的值設定為 6.01，則可以指定應用程式無法在 Windows 7 之前的作業系統上執行，如本主題稍後的表格所述。 您必須將 `major` 和 `minor` 的值指定為整數。

`minor` 版本中的前置零不會變更版本，但尾端零則會。 例如，6.1 和 6.01 參照相同版本，但 6.10 參照不同版本。 建議您將次要版本表示為兩位數，以避免混淆。

## <a name="remarks"></a>備註

下表列出常見的 Windows 子系統版本。

|Windows 版本|子系統版本|
|---------------------|-----------------------|
|Windows 2000|5.00|
|Windows XP|5.01|
|Windows Server 2003|5.02|
|Windows Vista|6.00|
|Windows 7|6.01|
|Windows Server 2008|6.01|
|Windows 8|6.02|

## <a name="default-values"></a>預設值

**-subsystemversion** 編譯器選項的預設值取決於下列清單中的條件︰

- 如果設定下列清單中的任何編譯器選項，則預設值為 6.02：

  - [-target:appcontainerexe](target.md)

  - [-target:winmdobj](target.md)

  - [-platform:arm](platform.md)

- 如果您使用的是 MSBuild、以 .NET Framework 4.5 為目標，且尚未設定稍早在此清單中指定的任何編譯器選項，則預設值為 6.00。

- 如果先前的條件均非為 true，則預設值是 4.00。

## <a name="setting-this-option"></a>設定這個選項

若要在 Visual Studio 中設定 **-subsystemversion**編譯器選項，您必須開啟 vbproj 檔案，並 `SubsystemVersion` 在 MSBuild XML 中指定屬性的值。 您不能在 Visual Studio IDE 中設定此選項。 如需詳細資訊，請參閱本主題稍早的＜預設值＞或[通用的 MSBuild 專案屬性](/visualstudio/msbuild/common-msbuild-project-properties)。

## <a name="see-also"></a>另請參閱

- [Visual Basic 命令列編譯器](index.md)

- [MSBuild 屬性](/visualstudio/msbuild/msbuild-properties)
