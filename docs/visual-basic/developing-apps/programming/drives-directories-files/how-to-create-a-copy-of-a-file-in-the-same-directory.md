---
title: 作法：在相同目錄中建立檔案複本
ms.date: 07/20/2015
f1_keywords:
- File.Copy
helpviewer_keywords:
- My.Computer.FileSystem.CopyFile method, copying files [Visual Basic]
- files [Visual Basic], copying
- CopyFile method [Visual Basic], copying files in Visual Basic
- I/O [Visual Basic], copying files
ms.assetid: b2fdda86-e666-42c2-9706-9527e9fa68ff
ms.openlocfilehash: 741f0c80ba268369ebdd598460e9d5fa13d09571
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401676"
---
# <a name="how-to-create-a-copy-of-a-file-in-the-same-directory-in-visual-basic"></a>如何：在 Visual Basic 中於相同目錄內建立檔案複本

使用 `My.Computer.FileSystem.CopyFile` 方法來複製檔案。 這些參數可讓您覆寫現有檔案、重新命名檔案、顯示作業進度，並讓使用者取消作業。  
  
### <a name="to-create-a-copy-of-a-file-in-the-same-folder"></a>在相同資料夾中建立檔案複本  
  
- 使用 `CopyFile` 方法，並提供目標檔案和位置。 下列範例會建立稱為 `test2.txt` 的 `test.txt` 複本。  
  
     [!code-vb[VbVbcnMyFileSystem#51](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#51)]  
  
### <a name="to-create-a-copy-of-a-file-in-the-same-folder-overwriting-existing-files"></a>在相同資料夾中建立檔案複本，以覆寫現有檔案  
  
- 使用 `CopyFile` 方法，並提供目標檔案和位置，以及將 `overwrite` 設定為 `True`。 下列範例會建立稱為 `test2.txt` 的 `test.txt` 複本，並以該名稱覆寫任何現有檔案。  
  
     [!code-vb[VbVbcnMyFileSystem#52](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#52)]  
  
## <a name="robust-programming"></a>穩固程式設計  

 下列條件可能會造成擲回例外狀況：  
  
- 因下列其中一項原因而導致路徑無效：它是長度為零的字串、它只包含空白字元、它包含無效的字元，或者它是裝置路徑 (開頭為 \\\\.\\) (<xref:System.ArgumentException>)。  
  
- 系統無法擷取絕對路徑 (<xref:System.ArgumentException>)。  
  
- 路徑無效，因為它是 `Nothing` (<xref:System.ArgumentNullException>)。  
  
- 來源檔案無效或不存在 (<xref:System.IO.FileNotFoundException>)。  
  
- 合併的路徑指向現有目錄 (<xref:System.IO.IOException>)。  
  
- 目的地檔案存在且 `overwrite` 設定為 `False` (<xref:System.IO.IOException>)。  
  
- 使用者沒有足夠權限以存取檔案 (<xref:System.IO.IOException>)。  
  
- 正在使用目標資枓夾中同名的檔案 (<xref:System.IO.IOException>)。  
  
- 路徑中的檔案或資料夾名稱包含冒號 (:)，或者是無效的格式 (<xref:System.NotSupportedException>)。  
  
- `ShowUI` 設定為 `True`、`onUserCancel` 設定為 `ThrowException`，而且使用者已取消作業 (<xref:System.OperationCanceledException>)。  
  
- `ShowUI` 設定為 `True`、`onUserCancel` 設定為 `ThrowException`，而且發生未指定的 I/O 錯誤 (<xref:System.OperationCanceledException>)。  
  
- 路徑超過系統定義的最大長度 (<xref:System.IO.PathTooLongException>)。  
  
- 使用者沒有必要的權限 (<xref:System.UnauthorizedAccessException>)。  
  
- 使用者缺乏必要的使用權限來檢視路徑 (<xref:System.Security.SecurityException>)。  
  
## <a name="see-also"></a>另請參閱

- <xref:Microsoft.VisualBasic.FileIO.FileSystem>
- <xref:Microsoft.VisualBasic.FileIO.FileSystem.CopyFile%2A>
- <xref:Microsoft.VisualBasic.FileIO.UICancelOption>
- [作法：將具有特定模式的檔案複製到目錄](how-to-copy-files-with-a-specific-pattern-to-a-directory.md)
- [作法：在不同目錄中建立檔案複本](how-to-create-a-copy-of-a-file-in-a-different-directory.md)
- [作法：將目錄複製到另一個目錄](how-to-copy-a-directory-to-another-directory.md)
- [作法：重新命名檔案](how-to-rename-a-file.md)
