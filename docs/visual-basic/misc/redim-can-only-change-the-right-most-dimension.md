---
title: "'ReDim' 只能變更最右側的維度"
ms.date: 07/20/2015
f1_keywords:
- vbrArray_TypeMismatch
ms.assetid: d53cf41b-7a7a-466c-a29a-920d99698fa9
ms.openlocfilehash: 8e42e0df7b97fb96f468ce37dd4cfc52fad8c596
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84358292"
---
# <a name="redim-can-only-change-the-right-most-dimension"></a>'ReDim' 只能變更最右側的維度
`ReDim` 陳述式嘗試使用 `Preserve` 關鍵字來變更不是最後一個維度的陣列的維度。 使用 `Preserve`時，您只能調整陣列的最後一個維度。 對於所有其他維度，您必須指定與現有陣列相同的大小。  
  
## <a name="to-correct-this-error"></a>更正這個錯誤  
  
- 請移除 `Preserve` 關鍵字。  
  
## <a name="see-also"></a>另請參閱

- [Visual Basic 中的陣列](../programming-guide/language-features/arrays/index.md)
- [Visual Basic 中的陣列維度](../programming-guide/language-features/arrays/array-dimensions.md)
- [ReDim 陳述式](../language-reference/statements/redim-statement.md)
- [Dim 陳述式](../language-reference/statements/dim-statement.md)
