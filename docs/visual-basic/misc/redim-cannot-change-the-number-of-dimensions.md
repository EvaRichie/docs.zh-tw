---
title: "'ReDim' 無法變更維度的數目"
ms.date: 07/20/2015
f1_keywords:
- vbrArray_RankMismatch
ms.assetid: 52505298-9985-4682-8f6e-ff7d56077f34
ms.openlocfilehash: b2404927c2faf30d1d058d2163fd5d67e1a52e1e
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84358163"
---
# <a name="redim-cannot-change-the-number-of-dimensions"></a>'ReDim' 無法變更維度的數目
作業嘗試使用 `ReDim` 陳述式變更陣列的陣序 (維度數目)。 `ReDim` 可以變更已正式宣告之陣列的一或多個維度大小，但無法變更陣列的陣序。  
  
## <a name="to-correct-this-error"></a>更正這個錯誤  
  
- 請確定您是要變更陣列的陣序，而不是其維度的大小，並且請盡可能地使用 `Dim` 來宣告具有所需陣序的新陣列。  
  
## <a name="see-also"></a>另請參閱

- [Visual Basic 中的陣列](../programming-guide/language-features/arrays/index.md)
- [Visual Basic 中的陣列維度](../programming-guide/language-features/arrays/array-dimensions.md)
- [ReDim 陳述式](../language-reference/statements/redim-statement.md)
- [Dim 陳述式](../language-reference/statements/dim-statement.md)
