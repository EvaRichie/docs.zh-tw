---
title: Declared Element Names
ms.date: 07/20/2015
helpviewer_keywords:
- declared elements [Visual Basic], case sensitivity
- names [Visual Basic], Visual Basic rules
- naming conventions [Visual Basic]
- element names [Visual Basic]
- declared elements [Visual Basic], identifiers
- declarations [Visual Basic], elements
- declared elements [Visual Basic], valid names
- '[] escape characters [Visual Basic]'
- names [Visual Basic], elements
- declaration statements [Visual Basic], declared elements
- declaring elements [Visual Basic]
- identifiers [Visual Basic], declared elements
- case sensitivity, declared element names
- escape characters [Visual Basic]
- names [Visual Basic], declared elements
- declared elements [Visual Basic], about declared elements
- escaped names [Visual Basic]
- declared elements [Visual Basic], names
- names [Visual Basic], naming conventions
- identifiers [Visual Basic], elements
ms.assetid: 09d8843b-c0dc-4afe-9dab-87c439a69e66
ms.openlocfilehash: 327a18644c1dc1d8dae59016b8e30600357d2ca9
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91086175"
---
# <a name="declared-element-names-visual-basic"></a>宣告項目名稱 (Visual Basic)

每個宣告的專案都有名稱，也稱為 *識別碼*，程式碼會使用它來參考它。  
  
## <a name="rules"></a>規則  

 Visual Basic 中的元素名稱必須遵守下列規則：  
  
- 它必須以字母字元或底線 (`_`) 開頭。  
  
- 它只能包含字母字元、小數位數和底線。  
  
- 如果開頭為底線，則必須包含至少一個字母字元或十進位數。  
  
- 長度不得超過1023個字元。  
  
 1023個字元的長度限制也適用于完整名稱的整個字串，例如 `outerNamespace.middleNamespace.innerNamespace.thisClass.thisElement` 。  
  
 下列範例顯示一些有效的元素名稱。  
  
 `aB123__45`  
  
 `_567`  
  
 下列範例顯示一些不正確元素名稱。 第一個只包含底線，第二個開頭是十進位數，而第三個則包含不正確字元 ($) 。  
  
 `' Three INVALID element names`  
  
 `_`  
  
 `12ABC`  
  
 `xyz$wv`  
  
> [!CAUTION]
> 以底線 (開頭的元素名稱 `_`) 不是 [語言獨立性和語言獨立元件](../../../../standard/language-independence-and-language-independent-components.md) (CLS) 的一部分，因此符合 cls 標準的程式碼無法使用定義這類名稱的元件。 不過，專案名稱中其他位置的底線符合 CLS 標準。  
  
### <a name="name-length-guidelines"></a>名稱長度指導方針  

 實際來說，您的名稱應該越短越好，同時仍然清楚地識別元素的本質。 這可提升程式碼的可讀性，並減少行長度和原始程式檔大小。  
  
 另一方面，您的名稱應該不太簡短，因為它不會充分描述專案所代表的專案，以及您的程式碼使用它的方式。 這對您的程式碼可讀性相當重要。 如果有其他人嘗試瞭解它，或您想要在撰寫後很長一段時間，則適當的專案名稱可以節省相當長的時間。  
  
## <a name="escaped-names"></a>轉義名稱  

 一般來說，元素名稱不能符合 Visual Basic 所保留的任何關鍵字，例如 `Case` 或 `Friend` 。 不過，您可以定義以括弧括住的 *轉義名稱* (`[ ]`) 。 因為括弧移除任何不明確的，所以可將任何 Visual Basic 關鍵字對應到一個轉義名稱。 當您稍後在程式碼中參考該名稱時，您也可以使用括弧。  
  
 一般而言，您應該只在下列情況使用轉義名稱：  
  
- 您的程式碼已從舊版的 Visual Basic 遷移，而該版本並未保留作為名稱使用的關鍵字;或  
  
- 您正在使用以另一種語言撰寫的程式碼，而不會保留指定的關鍵字。  
  
 否則，如果專案的名稱與關鍵字衝突，您應該考慮重新命名元素。 整合式開發環境 (IDE) 提供簡單的方法來進行這種作法。 如需詳細資訊，請參閱 [重構](/visualstudio/ide/refactoring-in-visual-studio)。  
  
## <a name="case-sensitivity-in-names"></a>名稱中的區分大小寫  

 Visual Basic 中的元素名稱不區分大小寫。 這表示當編譯器比較兩個名稱（僅限字母大小寫不同）時，它會將它們解釋為相同的名稱。 例如，它會將 `ABC` 和 `abc` 視為相同的宣告元素。  
  
 不過，Common Language Runtime (CLR) 使用區分大小寫 的繫結。 因此，當您產生一個組件或 DLL 並讓其他組件使用時，您的名稱將會區分大小寫。 例如，如果您使用名為 `ABC`的元素來定義類別，而其他組件透過 Common Language Runtime 使用您的類別，則這些組件必須以 `ABC`來表示該元素。 如果您接著重新編譯類別，並將元素的名稱變更為 `abc` ，其他使用您類別的元件就無法再存取該專案。 因此，當您發行組件的更新版本時，不應該變更任何公用元素的字母大小寫。  
  
## <a name="names-and-locales"></a>名稱和地區設定  

 名稱的比較與地區設定無關。 如果兩個名稱在一個地區設定中相符，它們保證會在所有地區設定中相符。  
  
## <a name="see-also"></a>另請參閱

- [宣告的元素](index.md)
- [宣告項目特性](declared-element-characteristics.md)
- [References to Declared Elements](references-to-declared-elements.md)
- [陳述式](../../../language-reference/statements/index.md)
