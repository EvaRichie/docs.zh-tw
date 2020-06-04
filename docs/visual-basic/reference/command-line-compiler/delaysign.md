---
title: -delaysign
ms.date: 03/10/2018
helpviewer_keywords:
- delaysign compiler option [Visual Basic]
- -delaysign compiler option [Visual Basic]
- -delaysign compiler option [Visual Basic]
ms.assetid: c76e61a4-1884-4252-9fb2-377f99caa690
ms.openlocfilehash: c9bb302e2b34ebe1f51cf39bb3db1094d420d7f4
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84408695"
---
# <a name="-delaysign"></a>-delaysign

指定將要完整簽署還是部分簽署組件。

## <a name="syntax"></a>語法

```console
-delaysign[+ | -]
```

## <a name="arguments"></a>引數

`+` &#124; `-`  
選擇性。 如果要完整簽署組件，請使用 `-delaysign-`。 `-delaysign+`如果您想要將公開金鑰放在元件中，並為帶正負號的雜湊保留空間，請使用。 預設值為 `-delaysign-`。

## <a name="remarks"></a>備註

`-delaysign`除非搭配[-keyfile](keyfile.md)或[-keycontainer](keycontainer.md)使用，否則選項不會有任何作用。

當您要求完整簽署的組件時，編譯器會雜湊包含資訊清單 (組件中繼資料) 的檔案，並使用私密金鑰簽署該雜湊。 所產生的數位簽章會儲存在包含資訊清單的檔案中。 當元件延遲簽署時，編譯器不會計算和儲存簽章，但會在檔案中保留空間，以便稍後新增簽章。

例如，藉由使用 `-delaysign+` ，組織中的開發人員可以散發元件的未簽署測試版本，讓測試人員可以向全域組件快取註冊並使用。 當元件上的工作完成時，負責組織之私密金鑰的人員可以完整簽署元件。 這項區隔可保護組織的私密金鑰免于洩漏，同時允許所有開發人員處理元件。

如需簽署元件的詳細資訊，請參閱[建立和使用強式名稱的元件](../../../standard/assembly/create-use-strong-named.md)。

### <a name="to-set--delaysign-in-the-visual-studio-integrated-development-environment"></a>在 Visual Studio 的整合式開發環境中設定-delaysign

1. 在 **方案總管**中選取專案。 按一下 [專案]**** 功能表上的 [屬性]****。

2. 按一下 [ **簽署** ] 索引標籤。

3. 在 [**延遲簽署**] 方塊中設定值。

## <a name="see-also"></a>另請參閱

- [Visual Basic 命令列編譯器](index.md)
- [-keyfile](keyfile.md)
- [-keycontainer](keycontainer.md)
- [編譯命令列的範例](sample-compilation-command-lines.md)
