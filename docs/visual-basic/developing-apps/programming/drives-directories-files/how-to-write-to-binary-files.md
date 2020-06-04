---
title: 作法：寫入二進位檔案
ms.date: 07/20/2015
helpviewer_keywords:
- files [Visual Basic], binary access
- WriteAllBytes method [Visual Basic]
- binary files [Visual Basic], writing in Visual Basic
ms.assetid: 59fae125-de5b-4c96-883c-209f4a55112c
ms.openlocfilehash: b36da82060b930101cb54dd852d050ac0155bd10
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84411547"
---
# <a name="how-to-write-to-binary-files-in-visual-basic"></a>如何：在 Visual Basic 中寫入二進位檔案

<xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllBytes%2A> 方法會將資料寫入二進位檔案。 如果 `append` 參數為 `True`，它會將資料附加至檔案；若否，則會覆寫檔案中的資料。

如果指定路徑 (不含檔案名稱) 無效，則會擲回 <xref:System.IO.DirectoryNotFoundException> 例外狀況。 如果此路徑有效，但檔案不存在，則系統會建立檔案。

## <a name="to-write-to-a-binary-file"></a>若要寫入二進位檔案

使用 `WriteAllBytes` 方法，同時提供檔案路徑、檔案名稱以及要寫入的位元組。 這個範例會將資料陣列 `CustomerData` 附加至名為 `CollectedData.dat` 的檔案。

[!code-vb[VbVbcnMyFileSystem#27](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#27)]

## <a name="robust-programming"></a>穩固程式設計

以下條件可能會造成例外狀況：

- 因下列其中一項原因而導致路徑無效：它是長度為零的字串、它只包含空白字元，或者它包含無效的字元。 (<xref:System.ArgumentException>).

- 路徑無效，因為它是 `Nothing` (<xref:System.ArgumentNullException>)。

- `File` 指向不存在的路徑 (<xref:System.IO.FileNotFoundException> 或 <xref:System.IO.DirectoryNotFoundException>)。

- 檔案正由另一個處理序使用中，或發生 I/O 錯誤 (<xref:System.IO.IOException>)。

- 路徑超過系統定義的最大長度 (<xref:System.IO.PathTooLongException>)。

- 路徑中的檔案或目錄名稱含有冒號 (:)，或者是無效的格式 (<xref:System.NotSupportedException>)。

- 使用者缺乏必要的使用權限來檢視路徑 (<xref:System.Security.SecurityException>)。

## <a name="see-also"></a>另請參閱

- <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllBytes%2A>
- [作法：將文字寫入檔案](how-to-write-text-to-files.md)
