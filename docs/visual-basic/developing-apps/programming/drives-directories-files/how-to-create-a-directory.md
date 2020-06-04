---
title: 作法：建立目錄
ms.date: 07/20/2015
helpviewer_keywords:
- directories [Visual Basic], creating
- folders [Visual Basic], creating
ms.assetid: 0351a2ca-24d8-43b5-bb39-9b99e6401cff
ms.openlocfilehash: 0da915054a2e38c778f15bc0b472fe9b02521189
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401663"
---
# <a name="how-to-create-a-directory-in-visual-basic"></a>如何：在 Visual Basic 中建立目錄

使用 `My.Computer.FileSystem` 物件的 `CreateDirectory` 方法來建立目錄。  
  
 如果目錄已經存在，則不會擲回例外狀況。  
  
### <a name="to-create-a-directory"></a>建立目錄  
  
- 指定應該建立目錄之位置的完整路徑，以使用 `CreateDirectory` 方法。 這個範例會在 `C:\Documents and Settings\All Users\Documents` 中建立 `NewDirectory` 目錄。  
  
     [!code-vb[VbVbcnMyFileSystem#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#2)]  
  
## <a name="robust-programming"></a>穩固程式設計  

 以下條件可能會造成例外狀況：  
  
- 目錄名稱的格式不正確。 例如，它包含不合法的字元，或只有空白字元 (<xref:System.ArgumentException>)。  
  
- 要建立之目錄的父目錄為唯讀 (<xref:System.IO.IOException>)。  
  
- 目錄名稱為 `Nothing` (<xref:System.ArgumentNullException>)。  
  
- 目錄名稱太長 (<xref:System.IO.PathTooLongException>)。  
  
- 目錄名稱為冒號 ":" (<xref:System.NotSupportedException>)。  
  
- 使用者沒有權限，無法建立目錄 (<xref:System.UnauthorizedAccessException>)。  
  
- 使用者在部分信任狀況下的權限不足 (<xref:System.Security.SecurityException>)。  
  
## <a name="see-also"></a>另請參閱

- <xref:Microsoft.VisualBasic.FileIO.FileSystem.CreateDirectory%2A>
- [建立、刪除和移動檔案和目錄](creating-deleting-and-moving-files-and-directories.md)
