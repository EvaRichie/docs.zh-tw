---
title: 作法：將具有特定模式的檔案複製到目錄
ms.date: 07/20/2015
helpviewer_keywords:
- My.Computer.FileSystem.CopyFile method, copying files [Visual Basic]
- files [Visual Basic], copying
- CopyFile method [Visual Basic], copying files in Visual Basic
- I/O [Visual Basic], copying files
ms.assetid: f205d2ad-bbe5-4d55-8a40-acda21aa82dd
ms.openlocfilehash: 7e263e2c9035db54dbb58c6c78c0647d5442504e
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401702"
---
# <a name="how-to-copy-files-with-a-specific-pattern-to-a-directory-in-visual-basic"></a>如何：在 Visual Basic 中將具有特定模式的檔案複製到目錄

<xref:Microsoft.VisualBasic.MyServices.FileSystemProxy.GetFiles%2A> 方法會傳回代表檔案路徑名稱的唯讀字串集合。 您可以使用 `wildCards` 參數指定特定模式。  
  
 如果找不到相符的檔案，則會傳回空集合。  
  
 您可以使用 <xref:Microsoft.VisualBasic.FileIO.FileSystem.CopyFile%2A> 方法，將檔案複製至目錄。  
  
### <a name="to-copy-files-with-a-specific-pattern-to-a-directory"></a>將具有特定模式的檔案複製至目錄  
  
1. 使用 `GetFiles` 方法來傳回檔案清單。 這個範例會傳回所指定目錄中的所有 .rtf 檔案。  
  
     [!code-vb[VbFileIOMisc#36](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIOMisc/VB/Class1.vb#36)]  
  
2. 使用 `CopyFile` 方法來複製檔案。 這個範例會將檔案複製至名稱為 `testdirectory`的目錄中。  
  
     [!code-vb[VbVbcnMyFileSystem#88](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#88)]  
  
3. 使用 `For` 陳述式來關閉 `Next` 陳述式。  
  
     [!code-vb[VbVbcnMyFileSystem#89](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#89)]  
  
## <a name="example"></a>範例  

 下列範例 (以完整形式呈現上述程式碼片段) 會將所指定目錄中的所有 .rtf 檔案複製至名稱為 `testdirectory`的目錄中。  
  
 [!code-vb[VbFileIOMisc#37](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIOMisc/VB/Class1.vb#37)]  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  

 以下條件可能會造成例外狀況：  
  
- 因下列其中一項原因而導致路徑無效：它是長度為零的字串、它只包含空白字元、它包含無效的字元，或者它是裝置路徑 (開頭為 \\\\.\\) (<xref:System.ArgumentException>)。  
  
- 路徑無效，因為它是 `Nothing` (<xref:System.ArgumentNullException>)。  
  
- 目錄不存在 (<xref:System.IO.DirectoryNotFoundException>)。  
  
- 目錄指向現有檔案 (<xref:System.IO.IOException>)。  
  
- 路徑超過系統定義的最大長度 (<xref:System.IO.PathTooLongException>)。  
  
- 路徑中的檔案或目錄名稱含有冒號 (:)，或者是無效的格式 (<xref:System.NotSupportedException>)。  
  
- 使用者缺乏必要的使用權限來檢視路徑 (<xref:System.Security.SecurityException>)。 使用者缺乏必要的權限 (<xref:System.UnauthorizedAccessException>)。  
  
## <a name="see-also"></a>另請參閱

- <xref:Microsoft.VisualBasic.FileIO.FileSystem.CopyFile%2A>
- <xref:Microsoft.VisualBasic.MyServices.FileSystemProxy.GetFiles%2A>
- [作法：尋找具有特定模式的子目錄](how-to-find-subdirectories-with-a-specific-pattern.md)
- [疑難排解：讀取和寫入文字檔](troubleshooting-reading-from-and-writing-to-text-files.md)
- [作法：取得目錄中的檔案集合](how-to-get-the-collection-of-files-in-a-directory.md)
