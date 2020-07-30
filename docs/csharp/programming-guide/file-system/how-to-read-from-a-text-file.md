---
title: '如何從文字檔讀取-c # 程式設計手冊'
description: 瞭解如何使用 File 類別的靜態方法，從文字檔讀取。 查看程式碼範例，並查看其他可用的資源。
ms.date: 07/20/2015
f1_keywords:
- StreamReader.ReadToEnd
helpviewer_keywords:
- text files, writing to
- reading text files
- reading data, text files
- text files, reading
ms.assetid: 92246c5b-e819-4eea-9370-1a9460e12de3
ms.openlocfilehash: 80ac6f8412f456b23d05ee87882dca8e16a132c3
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87301654"
---
# <a name="how-to-read-from-a-text-file-c-programming-guide"></a>如何從文字檔讀取（c # 程式設計手冊）
這個範例會使用 <xref:System.IO.File?displayProperty=nameWithType> 類別中的靜態方法 <xref:System.IO.File.ReadAllText%2A> 和 <xref:System.IO.File.ReadAllLines%2A>，來讀取文字檔的內容。  
  
如需使用的範例 <xref:System.IO.StreamReader> ，請參閱[如何一次一行讀取文字檔](./how-to-read-a-text-file-one-line-at-a-time.md)。
  
> [!NOTE]
> 本範例中使用的檔案是在[如何寫入文字檔](./how-to-write-to-a-text-file.md)主題中建立。
  
## <a name="example"></a>範例  
 [!code-csharp[csFilesandFolders#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csFilesAndFolders/CS/FileIteration.cs#4)]  
  
## <a name="compiling-the-code"></a>編譯程式碼  
 將程式碼複製並貼到 C# 主控台應用程式中。  
  
如果您不是使用[如何寫入文字檔](./how-to-write-to-a-text-file.md)中的文字檔，請以 `ReadAllText` `ReadAllLines` 您電腦上的適當路徑和檔案名取代和的引數。
  
## <a name="robust-programming"></a>穩固程式設計  
 以下條件可能會造成例外狀況：  
  
- 檔案不存在或不在指定的位置。 請檢查路徑和檔案名稱的拼字。  
  
## <a name="net-security"></a>.NET 安全性  
 請勿依賴檔案的名稱來判斷檔案的內容。 例如，`myFile.cs` 檔案可能不是 C# 原始程式檔。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.IO?displayProperty=nameWithType>
- [C # 程式設計指南](../index.md)
- [檔案系統和登錄 (C# 程式設計手冊)](./index.md)
