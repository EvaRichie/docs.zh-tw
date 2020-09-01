---
description: -publicsign (C# 編譯器選項)
title: -publicsign (C# 編譯器選項)
ms.date: 05/15/2018
f1_keywords:
- /publicsign
helpviewer_keywords:
- -publicsign compiler option [C#]
- publicsign compiler option [C#]
- /publicsign compiler option [C#]
ms.openlocfilehash: 525912c7f50aa6b51e602be7b9258f1f5907daac
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89124808"
---
# <a name="-publicsign-c-compiler-options"></a>-publicsign (C# 編譯器選項)

此選項會導致編譯器套用公開金鑰，但實際上不會簽署組件。 **-publicsign** 選項也會在組件中設定一個位元，以告知執行階段該檔案實際上已經過簽署。

## <a name="syntax"></a>語法

```console
-publicsign
```

## <a name="arguments"></a>引數

無。

## <a name="remarks"></a>備註

**-publicsign** 選項需要使用 [-keyfile](keyfile-compiler-option.md) 或 [-keycontainer](keycontainer-compiler-option.md)。 **Keyfile** 或 **keycontainer** 選項會指定公開金鑰。

**-publicsign** 和 **-delaysign** 選項是互斥的。

有時稱為「假簽署」或「OSS 簽署」，公開簽署會在輸出組件中包含公開金鑰並設定「已簽署」的旗標，但實際上不會使用私密金鑰來簽署組件。 這對開放原始碼專案非常實用。在這類專案中，人員想要建置可與已發行「完整簽署」組件相容的組件，但該組件無法存取可用來簽署組件的私密金鑰。 由於實際上幾乎沒有任何取用者需要檢查組件是否已完整簽署，因此，這些公開建置的組件幾乎適用於每個要使用完整簽署組件的案例。

### <a name="to-set-this-compiler-option-in-a-csproj-file"></a>若要在 .csproj 檔案中設定這個編譯器選項

開啟專案的 .csproj 檔案，然後加入下列元素：

```xml
<PublicSign>true</PublicSign>
```

## <a name="see-also"></a>另請參閱

- [C# 編譯器 -delaysign 選項](delaysign-compiler-option.md)
- [C# 編譯器 -keyfile 選項](keyfile-compiler-option.md)
- [C# 編譯器 -keycontainer 選項](keycontainer-compiler-option.md)
- [C # 編譯器選項](index.md)
- [管理專案和方案屬性](/visualstudio/ide/managing-project-and-solution-properties)
