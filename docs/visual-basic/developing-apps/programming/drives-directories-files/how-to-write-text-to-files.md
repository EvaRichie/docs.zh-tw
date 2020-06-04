---
title: 作法：將文字寫入檔案
ms.date: 07/20/2015
helpviewer_keywords:
- files [Visual Basic], writing to
- text, writing to files
- writing to files [Visual Basic]
- examples [Visual Basic], text files
ms.assetid: 304956eb-530d-4df7-b48f-9b4d1f2581a0
ms.openlocfilehash: f95a0c4df4a2eab0069a6dab0d4c3fa338d1d8ef
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84411534"
---
# <a name="how-to-write-text-to-files-in-visual-basic"></a>如何：在 Visual Basic 中將文字寫入檔案

<xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllText%2A> 方法可用來將文字寫入檔案。 如果指定的檔案不存在，則會建立該檔案。  
  
## <a name="procedure"></a>程序  
  
#### <a name="to-write-text-to-a-file"></a>將文字寫入檔案  
  
- 使用 `WriteAllText` 方法，將文字寫入檔案中，並指定要寫入的檔案和文字。 這個範例會將 `"This is new text."` 行寫入名為 `test.txt` 的檔案，並將文字附加至檔案中的任何現有文字。  
  
     [!code-vb[VbFileIOWrite#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIOWrite/VB/Class1.vb#3)]  
  
#### <a name="to-write-a-series-of-strings-to-a-file"></a>將一連串的字串寫入檔案  
  
- 反覆執行字串集合。 使用 `WriteAllText` 方法，將文字寫入檔案，並指定要新增的目標檔案和字串以及將 `append` 設定為 `True`。  
  
     這個範例會將 `Documents and Settings` 目錄中的檔案名稱寫入 `FileList.txt`，並在每個之間插入換行符號，以增加可讀性。  
  
     [!code-vb[VbFileIOWrite#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIOWrite/VB/Class1.vb#4)]  
  
## <a name="robust-programming"></a>穩固程式設計  

 以下條件可能會造成例外狀況：  
  
- 因下列其中一項原因而導致路徑無效：它是長度為零的字串、它只包含空白字元、它包含無效的字元，或者它是裝置路徑 (開頭為 \\\\.\\) (<xref:System.ArgumentException>)。  
  
- 路徑無效，因為它是 `Nothing` (<xref:System.ArgumentNullException>)。  
  
- `File` 指向不存在的路徑 (<xref:System.IO.FileNotFoundException> 或 <xref:System.IO.DirectoryNotFoundException>)。  
  
- 檔案正由另一個處理序使用中，或發生 I/O 錯誤 (<xref:System.IO.IOException>)。  
  
- 路徑超過系統定義的最大長度 (<xref:System.IO.PathTooLongException>)。  
  
- 路徑中的檔案或目錄名稱含有冒號 (:)，或者是無效的格式 (<xref:System.NotSupportedException>)。  
  
- 使用者缺乏必要的使用權限來檢視路徑 (<xref:System.Security.SecurityException>)。  
  
- 磁碟已滿，且 `WriteAllText` 的呼叫失敗 (<xref:System.IO.IOException>)。  
  
 如果要在部分信任內容中執行，則程式碼可能會因權限不足而擲回例外狀況。 如需詳細資訊，請參閱 [Code Access Security Basics](../../../../framework/misc/code-access-security-basics.md)。  
  
## <a name="see-also"></a>另請參閱

- <xref:Microsoft.VisualBasic.FileIO.FileSystem>
- <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllText%2A>
- [如何：從文字檔讀取](how-to-read-from-text-files.md)
