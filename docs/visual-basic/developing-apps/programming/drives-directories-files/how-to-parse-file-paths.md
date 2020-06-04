---
title: 作法：剖析檔案路徑
ms.date: 07/20/2015
helpviewer_keywords:
- file names [Visual Basic], parsing [Visual Basic]
- parsing, file paths [Visual Basic]
ms.assetid: c1bd99c9-8160-456a-b5ab-60a49139b923
ms.openlocfilehash: eb7714a8594c0bce344eb2e48ebc5053dc3bfbb4
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84359938"
---
# <a name="how-to-parse-file-paths-in-visual-basic"></a>如何：在 Visual Basic 中剖析檔案路徑

<xref:Microsoft.VisualBasic.FileIO.FileSystem> 物件提供剖析檔案路徑時的數種有用方法。  
  
- <xref:Microsoft.VisualBasic.FileIO.FileSystem.CombinePath%2A> 方法會採用兩個路徑，並傳回格式正確的合併路徑。  
  
- <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetParentPath%2A> 方法會傳回所提供路徑之上層的絕對路徑。  
  
- <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFileInfo%2A> 方法會傳回 <xref:System.IO.FileInfo> 物件，這個物件可以進行查詢來判斷檔案的屬性 (例如其名稱和路徑)。  
  
 請不要根據副檔名來判斷檔案內容。 例如，檔案 Form1.vb 可能不是 Visual Basic 來源檔案。  
  
### <a name="to-determine-a-files-name-and-path"></a>判斷檔案的名稱和路徑  
  
- 使用 <xref:System.IO.FileInfo.DirectoryName%2A> 物件的 <xref:System.IO.FileInfo.Name%2A> 和 <xref:System.IO.FileInfo> 屬性來判斷檔案的名稱和路徑。 這個範例會判斷名稱和路徑，並予以顯示。  
  
     [!code-vb[VbVbcnMyFileSystem#54](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#54)]  
  
### <a name="to-combine-a-files-name-and-directory-to-create-the-full-path"></a>合併檔案的名稱和目錄以建立完整路徑  
  
- 使用 `CombinePath` 方法，並提供目錄和名稱。 這個範例會採用前一個範例中所建立的字串 `folderPath` 和 `fileName` 、合併它們，並顯示結果。  
  
     [!code-vb[VbVbcnMyFileSystem#55](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#55)]  
  
## <a name="see-also"></a>另請參閱

- <xref:Microsoft.VisualBasic.FileIO.FileSystem>
- <xref:Microsoft.VisualBasic.FileIO.FileSystem.CombinePath%2A>
- <xref:System.IO.FileInfo>
- <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFileInfo%2A>
- [作法：取得目錄中的檔案集合](how-to-get-the-collection-of-files-in-a-directory.md)
