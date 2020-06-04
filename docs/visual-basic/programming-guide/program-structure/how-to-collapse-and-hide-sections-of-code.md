---
title: 作法：摺疊及隱藏程式碼區段
ms.date: 07/20/2015
helpviewer_keywords:
- Visual Basic, code collapsing
- Visual Basic, code hiding
- Visual Basic code, collapsing and hiding
ms.assetid: b770e8f5-e07d-491a-ab4b-a977980f9ba2
ms.openlocfilehash: c11affe9c4dd4251ba8ff4b87029d314970b5fcb
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404845"
---
# <a name="how-to-collapse-and-hide-sections-of-code-visual-basic"></a>如何：摺疊和隱藏程式碼區段 (Visual Basic)

指示詞可 `#Region` 讓您折迭和隱藏 Visual Basic 檔案中的程式碼區段。 指示詞可 `#Region` 讓您指定程式碼區塊，當您使用 Visual Studio 程式碼編輯器時，可以展開或折迭。 可以選擇性地隱藏程式碼，讓您的檔案更容易管理且更易於閱讀。 如需詳細資訊，請參閱[大綱](/visualstudio/ide/outlining)。

`#Region`指示詞支援程式碼區塊的語義，例如 `#If...#End If` 。 這表示它們不能在一個區塊中開始，也不能在另一個區塊中結束;開始和結束必須在相同的區塊中。 `#Region`函數中不支援指示詞。

## <a name="to-collapse-and-hide-a-section-of-code"></a>折迭和隱藏程式碼區段

將程式碼區段放在 `#Region` 和 `#End Region` 語句之間，如下列範例所示：

[!code-vb[VbVbalrConditionalComp#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConditionalComp/VB/Class1.vb#6)]

`#Region`區塊可以在程式碼檔案中多次使用，因此，使用者可以定義自己的程式和類別區塊，然後再折迭。 `#Region`區塊也可以嵌套在其他 `#Region` 區塊內。

> [!NOTE]
> 隱藏程式碼不會使其無法編譯，也不會影響 `#If...#End If` 語句。

## <a name="see-also"></a>另請參閱

- [條件式編譯](conditional-compilation.md)
- [#Region 指示詞](../../language-reference/directives/region-directive.md)
- [#If .。。Then ... #Else 指示詞](../../language-reference/directives/if-then-else-directives.md)
- [大綱](/visualstudio/ide/outlining)
