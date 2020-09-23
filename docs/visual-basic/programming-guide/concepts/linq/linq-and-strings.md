---
title: LINQ 和字串
ms.date: 07/20/2015
ms.assetid: 75ddb201-d97a-4f98-8cdf-4ad51714529a
ms.openlocfilehash: 28c11dcc3c788ea85516e8b3fbafe2677b6d9b54
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91075339"
---
# <a name="linq-and-strings-visual-basic"></a>LINQ 與字串 (Visual Basic)

您可以使用 LINQ 查詢及轉換字串與字串集合。 針對文字檔案中的半結構化資料，這種做法特別有用。 LINQ 查詢可以結合傳統字串函式和規則運算式。 例如，您可以使用 <xref:System.String.Split%2A> 或 <xref:System.Text.RegularExpressions.Regex.Split%2A> 方法，來建立您接著可以使用 LINQ 查詢或修改的字串陣列。 您可以在 LINQ 查詢的 `where` 子句中使用 <xref:System.Text.RegularExpressions.Regex.IsMatch%2A> 方法。 您可以使用 LINQ 查詢或修改規則運算式所傳回的 <xref:System.Text.RegularExpressions.MatchCollection> 結果。  
  
 您也可以使用本節所述的技巧，將半結構化的文字資料轉換成 XML。 如需詳細資訊，請參閱[如何：從 CSV 檔案產生 XML](../../../../standard/linq/generate-xml-csv-files.md)。  
  
 本節中的範例分為兩類：  
  
## <a name="querying-a-block-of-text"></a>查詢文字區塊  

 您可以查詢和分析文字區塊，並使用 <xref:System.String.Split%2A> 方法或 <xref:System.Text.RegularExpressions.Regex.Split%2A> 方法將它們分割為可查詢的較小字串陣列來進行修改。 您可以將原始程式文字分割成單字、句子、段落、頁面或任何其他準則，再依據您的查詢需求執行其他分割。  
  
 [如何：在字串中計算單字的出現次數 (LINQ)  (Visual Basic) ](how-to-count-occurrences-of-a-word-in-a-string-linq.md)  
 示範如何使用 LINQ 進行簡單的文字查詢。  
  
 [如何：查詢包含指定字組的句子 (LINQ) (Visual Basic)](how-to-query-for-sentences-that-contain-a-specified-set-of-words.md)

 示範如何分割任意界限上的文字檔，以及如何針對每個部分執行查詢。  
  
 [如何：查詢字串中的字元 (LINQ)  (Visual Basic) ](how-to-query-for-characters-in-a-string-linq.md)  
 示範當字串為可查詢型別時的情況。  
  
 [如何使用正則運算式合併 LINQ 查詢 (Visual Basic) ](how-to-combine-linq-queries-with-regular-expressions.md)  
 示範如何在 LINQ 查詢中使用規則運算式，針對篩選的查詢結果進行複雜模式比對。  
  
## <a name="querying-semi-structured-data-in-text-format"></a>查詢半結構化的文字格式資料  

 通常，許多不同類型的文字檔案是由具有類似格式的數行所構成，例如 Tab 或逗號分隔的檔案或固定長度的行。 將文字檔案讀入記憶體之後，您可以使用 LINQ 來查詢及/或修改這些行。 LINQ 查詢也簡化了多種來源資料的結合工作。  
  
 [如何：尋找兩個清單之間的集合差異 (LINQ)  (Visual Basic) ](how-to-find-the-set-difference-between-two-lists-linq.md)  
 顯示如何尋找某份清單中有、但另一份清單中卻沒有的所有字串。  
  
 [如何：依任何字或欄位排序或篩選文字資料 (LINQ) (Visual Basic)](how-to-sort-or-filter-text-data-by-any-word-or-field-linq.md)  
 示範如何依任何字或欄位排序文字行。  
  
 [如何：將分隔檔的欄位重新排列 (LINQ)  (Visual Basic) ](how-to-reorder-the-fields-of-a-delimited-file.md)  
 示範如何重新排列 .csv 檔案行中的欄位。  
  
 [如何：合併和比較字串集合 (LINQ)  (Visual Basic) ](how-to-combine-and-compare-string-collections-linq.md)  
 示範結合字串清單的各種方式。  
  
 [如何：從多個來源填入物件集合 (LINQ)  (Visual Basic) ](how-to-populate-object-collections-from-multiple-sources-linq.md)  
 示範如何將多個文字檔案作為資料來源以建立物件集合。  
  
 [如何：從不同的檔案聯結內容 (LINQ)  (Visual Basic) ](how-to-join-content-from-dissimilar-files-linq.md)  
 示範如何使用相符的索引鍵，將兩份清單中的字串結合為單一字串。  
  
 [如何：使用群組將檔案分割成許多檔案 (LINQ)  (Visual Basic) ](how-to-split-a-file-into-many-files-by-using-groups-linq.md)  
 示範如何將單一檔案作為資料來源以建立新的檔案。  
  
 [如何：計算 CSV 文字檔中的資料行值 (LINQ)  (Visual Basic) ](how-to-compute-column-values-in-a-csv-text-file-linq.md)  
 示範如何針對 .csv 檔案中的文字資料執行數學計算。  
  
## <a name="see-also"></a>另請參閱

- [Language-Integrated Query (LINQ) (Visual Basic)](index.md)
- [如何：從 CSV 檔案產生 XML](../../../../standard/linq/generate-xml-csv-files.md)
