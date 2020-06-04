---
title: 需要組件 '<assemblyidentity>' (包含類型 '<typename>') 的參考，但是由於專案 '<projectname1>' 和 '<projectname2>' 之間模稜兩可，所以找不到適合的參考
ms.date: 07/20/2015
f1_keywords:
- bc30969
- vbc30969
helpviewer_keywords:
- BC30969
ms.assetid: 1b29dbc5-8268-45fe-bfc2-b2070a5c845c
ms.openlocfilehash: 4b9f74f0627268752b0ba3c3816fe9d4cc8a231b
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404819"
---
# <a name="reference-required-to-assembly-assemblyidentity-containing-type-typename-but-a-suitable-reference-could-not-be-found-due-to-ambiguity-between-projects-projectname1-and-projectname2"></a>需要組件 '\<assemblyidentity>' (包含類型 '\<typename>') 的參考，但是由於專案 '\<projectname1>' 和 '\<projectname2>' 之間模稜兩可，所以找不到適合的參考
運算式使用專案外部定義的類型 (例如類別、結構、介面、列舉或委派)。 不過，專案參考超過一個定義其類型的組件。  
  
 上述專案會產生具有相同名稱的組件。 因此，編譯器無法判斷要針對您正在存取的類型使用哪個組件。  
  
 若要存取另一個元件中所定義的類型，Visual Basic 編譯器必須有該元件的參考。 這必須是單一的明確參考，不會在專案之間造成循環參考。  
  
 **錯誤 ID︰** BC30969  
  
## <a name="to-correct-this-error"></a>更正這個錯誤  
  
1. 決定哪些專案產生的最佳組件供專案參考。 這項決策可能會使用輕鬆存取檔案和更新頻率等準則。  
  
2. 在專案屬性中，加入包含組件之檔案的參考，而這個組件定義所使用的類型。  
  
## <a name="see-also"></a>另請參閱

- [管理專案中的參考](/visualstudio/ide/managing-references-in-a-project)
- [References to Declared Elements](../../programming-guide/language-features/declared-elements/references-to-declared-elements.md)

- [管理專案和方案屬性](/visualstudio/ide/managing-project-and-solution-properties)
- [針對中斷參考進行疑難排解](/visualstudio/ide/troubleshooting-broken-references)
