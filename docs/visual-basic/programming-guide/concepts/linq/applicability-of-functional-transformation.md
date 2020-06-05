---
title: 函式轉換的適用性
ms.date: 07/20/2015
ms.assetid: 3b74e134-e19b-44bc-8d06-e26c48305040
ms.openlocfilehash: db24871e3763c5acc79cf21b4afb90a93ed8bd53
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84383698"
---
# <a name="applicability-of-functional-transformation-visual-basic"></a>功能性轉換的適用性（Visual Basic）
純功能性轉換適用於各種情況。  
  
 功能性轉換方法最適合查詢與管理結構化資料；因此，最適合搭配 LINQ 技術使用。 不過，功能性轉換的適用性比搭配 LINQ 還要廣泛。 主要焦點放在將資料從一個表單轉換到另一個表單的任何處理都可能會被視為功能性轉換的候選。  
  
 這個方法適用於許多開始做為候選時可能不會出現的問題。 搭配 LINQ 使用或與 LINQ 分開使用時，應該針對下列區域考慮功能性轉換：  
  
- 以 XML 為基礎的文件。 格式正確的任何 XML 語言資料都可以透過功能性轉換輕鬆管理。 如需詳細資訊，請參閱[XML 的功能性轉換（Visual Basic）](functional-transformation-of-xml.md)。  
  
- 其他結構化檔案格式。 從 Windows.ini 檔案到純文字文件，大部分的檔案都有借用本身進行分析與轉換的特定結構。  
  
- 資料串流通訊協定。 將資料編碼到通訊協定，或從通訊協定解碼資料通常都可以透過簡單的功能性轉換表示。  
  
- RDBMS 和 OODBMS 資料。 關聯式資料庫與物件導向的資料庫 (例如 XML) 都是廣泛使用的結構化資料來源。  
  
- 數學、統計與科學解決方案。 這些欄位傾向管理大型資料集來協助使用者視覺化、估計或實際解決非一般的問題。  
  
 如[重構為純虛擬函式（Visual Basic）](refactoring-into-pure-functions.md)中所述，使用純虛擬函式是功能性程式設計的範例。 除了立即的益處之外，使用純虛擬函式會提供從功能性轉換觀點思考的珍貴經驗。 這個方法對於程式和類別設計也可能產生重大影響。 尤其是問題如上述般，將本身借用給資料轉換解決方案時，更是如此。  
  
 雖然這些超出此教學課程的範圍，但是受到功能性轉換觀點影響的設計傾向於著重程序而非當做行動的物件，而所產生的解決方案容易當做一系列的大規模轉換 (而非個別物件狀態的變更) 實作。  
  
 同樣地，請記住，Visual Basic 同時支援命令式和功能性方法，因此應用程式的最佳設計可能會納入兩者的元素。  
  
## <a name="see-also"></a>另請參閱

- [純功能性轉換簡介（Visual Basic）](introduction-to-pure-functional-transformations.md)
- [XML 函數式轉換 (Visual Basic)](functional-transformation-of-xml.md)
- [重構為純虛擬函式（Visual Basic）](refactoring-into-pure-functions.md)
