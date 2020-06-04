---
title: 作法：移動檔案
ms.date: 07/20/2015
helpviewer_keywords:
- files [Visual Basic], moving
ms.assetid: 53a7457b-5815-41ad-b37d-28537c1fb77a
ms.openlocfilehash: 2dafeb3b5f8b8c3a8976b25c1a57f405aebb32b9
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401598"
---
# <a name="how-to-move-a-file-in-visual-basic"></a>如何：在 Visual Basic 中移動檔案

`My.Computer.FileSystem.MoveFile` 方法可以用來將檔案移至另一個資料夾。 如果目標結構不存在，則會予以建立。  
  
### <a name="to-move-a-file"></a>移動檔案  
  
- 使用 `MoveFile` 方法移動檔案，並指定來源檔案和目標檔案的檔案名稱和位置。 這個範例會將名稱為 `test.txt` 的檔案從 `TestDir1` 移至 `TestDir2`。 請注意，即使目標檔案名稱與來源檔案名稱相同，還是要指定目標檔案名稱。  
  
     [!code-vb[VbVbcnMyFileSystem#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#24)]  
  
### <a name="to-move-a-file-and-rename-it"></a>移動檔案並將它重新命名  
  
- 使用 `MoveFile` 方法移動檔案，並指定來源檔案名稱和位置、目標位置以及目標位置上的新名稱。 這個範例會將名稱為 `test.txt` 的檔案從 `TestDir1` 移至 `TestDir2` ，並將它重新命名為 `nexttest.txt`。  
  
     [!code-vb[VbVbcnMyFileSystem#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#25)]  
  
## <a name="robust-programming"></a>穩固程式設計  

 以下條件可能會造成例外狀況：  
  
- 因下列其中一項原因而導致路徑無效：它是長度為零的字串、它只包含空白字元、它包含無效的字元，或者它是裝置路徑 (開頭為 \\\\.\\) (<xref:System.ArgumentException>)。  
  
- 路徑無效，因為它是 `Nothing` (<xref:System.ArgumentNullException>)。  
  
- `destinationFileName` 為 `Nothing` 或空字串 (<xref:System.ArgumentNullException>)。  
  
- 來源檔案無效或不存在 (<xref:System.IO.FileNotFoundException>)。  
  
- 合併的路徑指向現有目錄、目的地檔案已存在，以及 `overwrite` 設為 `False`、正在使用目標目錄中同名的檔案，或使用者的權限不足無法存取檔案 (<xref:System.IO.IOException>)。  
  
- 路徑中的檔案或目錄名稱含有冒號 (:)，或者是無效的格式 (<xref:System.NotSupportedException>)。  
  
- `showUI` 設為 `True`、 `onUserCancel` 設為 `ThrowException`，以及使用者已取消作業，或發生未指定的 I/O 錯誤 (<xref:System.OperationCanceledException>)。  
  
- 路徑超過系統定義的最大長度 (<xref:System.IO.PathTooLongException>)。  
  
- 使用者缺乏必要的使用權限來檢視路徑 (<xref:System.Security.SecurityException>)。  
  
- 使用者沒有必要的權限 (<xref:System.UnauthorizedAccessException>)。  
  
## <a name="see-also"></a>另請參閱

- <xref:Microsoft.VisualBasic.FileIO.FileSystem.MoveFile%2A>
- [作法：重新命名檔案](how-to-rename-a-file.md)
- [作法：在不同目錄中建立檔案複本](how-to-create-a-copy-of-a-file-in-a-different-directory.md)
- [作法：剖析檔案路徑](how-to-parse-file-paths.md)
