---
title: 如何：控制變數的可用性
ms.date: 07/20/2015
helpviewer_keywords:
- access levels, declared elements
- Private keyword [Visual Basic], accessing variables
- access levels, variables
- Public keyword [Visual Basic], accessing variables
- Friend keyword [Visual Basic], accessing variables
- variables [Visual Basic], access level
- declared elements [Visual Basic], access level
- Protected keyword [Visual Basic], accessing variables
ms.assetid: eaf4f073-7922-43ce-ae1e-90ff376ae947
ms.openlocfilehash: 0bfa7fa2bdac4746827884c1dad62734c549a48e
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84357383"
---
# <a name="how-to-control-the-availability-of-a-variable-visual-basic"></a>如何：控制變數的可用性 (Visual Basic)
您可以藉由指定其*存取層級*來控制變數的可用性。 存取層級會決定哪些程式碼有權讀取或寫入變數。  
  
- *成員變數*（定義于模組層級和在任何程式之外）預設為公用存取，這表示任何可查看它們的程式碼都可以存取它們。 您可以藉由指定存取修飾詞來變更此項。  
  
- *本機變數*（在程式內定義）名義上具有公用存取權，雖然只有其程式中的程式碼可以存取它們。 您不能變更本機變數的存取層級，但是可以變更包含它之程式的存取層級。  
  
 如需詳細資訊，請參閱[Visual Basic 中的存取層級](access-levels.md)。  
  
## <a name="private-and-public-access"></a>私用和公用存取  
  
#### <a name="to-make-a-variable-accessible-only-from-within-its-module-class-or-structure"></a>讓只能從其模組、類別或結構中存取的變數  
  
1. 將變數的[Dim 語句](../../../language-reference/statements/dim-statement.md)放在模組、類別或結構中，但在任何程式之外。  
  
2. 在語句中包含[Private](../../../language-reference/modifiers/private.md)關鍵字 `Dim` 。  
  
     您可以從模組、類別或結構內的任何位置讀取或寫入變數，而不是從外部進行。  
  
#### <a name="to-make-a-variable-accessible-from-any-code-that-can-see-it"></a>若要讓變數可以從任何可看到的程式碼存取  
  
1. 對於成員變數，請將變數的語句放在 `Dim` 模組、類別或結構中，但在任何程式之外。  
  
2. 在語句中包含[Public](../../../language-reference/modifiers/public.md)關鍵字 `Dim` 。  
  
     您可以從任何與您的元件互通的程式碼中讀取或寫入變數。  
  
 -或-  
  
1. 針對本機變數，請將變數的語句放在程式 `Dim` 內。  
  
2. 請勿 `Public` 在語句中包含關鍵字 `Dim` 。  
  
     您可以從程式內的任何位置讀取或寫入變數，而不是從外部進行。  
  
## <a name="protected-and-friend-access"></a>受保護和 Friend 存取  
 您可以將變數的存取層級限制為其類別和任何衍生類別，或其元件。 您也可以指定這些限制的聯集，允許從任何衍生類別中的程式碼，或在相同元件中的任何其他位置進行存取。 您可以在相同的宣告中結合和關鍵字來指定這個聯集 `Protected` `Friend` 。  
  
#### <a name="to-make-a-variable-accessible-only-from-within-its-class-and-any-derived-classes"></a>使變數只能從其類別和任何衍生類別中存取  
  
1. 將變數的語句放在 `Dim` 類別內，但在任何程式之外。  
  
2. 在語句中包含[Protected](../../../language-reference/modifiers/protected.md)關鍵字 `Dim` 。  
  
     您可以從類別內的任何位置讀取或寫入變數，以及從任何衍生自它的類別內，而不是從衍生鏈中的任何類別之外。  
  
#### <a name="to-make-a-variable-accessible-only-from-within-the-same-assembly"></a>使變數只能從相同的元件中存取  
  
1. 將變數的語句放在 `Dim` 模組、類別或結構中，但在任何程式之外。  
  
2. 在語句中包含[Friend](../../../language-reference/modifiers/friend.md)關鍵字 `Dim` 。  
  
     您可以從模組、類別或結構內的任何位置讀取或寫入變數，以及從相同元件中的任何程式碼，而不是從元件外部進行讀取或寫入。  
  
## <a name="example"></a>範例  
 下列範例顯示具有 `Public` 、 `Protected` 、 `Friend` 、 `Protected Friend` 和 `Private` 存取層級的變數宣告。 請注意，當 `Dim` 語句指定存取層級時，您不需要包含 `Dim` 關鍵字。  
  
```vb  
Public Class classForEverybody  
Protected Class classForMyHeirs  
Friend stringForThisProject As String  
Protected Friend stringForProjectAndHeirs As String  
Private numberForMeOnly As Integer  
```  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 變數的存取層級越嚴格，惡意程式碼就越有可能不適當地使用它。  
  
## <a name="see-also"></a>另請參閱

- [Visual Basic 中的存取層級](access-levels.md)
- [Dim 陳述式](../../../language-reference/statements/dim-statement.md)
- [公開](../../../language-reference/modifiers/public.md)
- [免受](../../../language-reference/modifiers/protected.md)
- [給](../../../language-reference/modifiers/friend.md)
- [私用](../../../language-reference/modifiers/private.md)
