---
title: 如何：將文字寫入檔案
description: 瞭解將文字寫入或附加至 .NET 應用程式檔案的方式。 使用 StreamWriter 或檔案類別中的方法，以同步或非同步方式撰寫文字。
ms.date: 01/04/2019
dev_langs:
- csharp
- vb
helpviewer_keywords:
- writing text to files
- I/O [.NET], writing text to files
- streams, writing text to files
- data streams, writing text to files
ms.assetid: 060cbe06-2adf-4337-9e7b-961a5c840208
ms.openlocfilehash: bd9abc2aac4b02f71e41f71e518a76b2477420da
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94829709"
---
# <a name="how-to-write-text-to-a-file"></a>如何：將文字寫入檔案

本主題說明針對 .NET 應用程式將文字寫入檔案的不同方式。

通常會使用下列類別和方法，將文字寫入至檔案：  
  
- <xref:System.IO.StreamWriter> 包含同步 (<xref:System.IO.StreamWriter.Write%2A> 和 <xref:System.IO.TextWriter.WriteLine%2A>) 或非同步 (<xref:System.IO.StreamWriter.WriteAsync%2A> 和 <xref:System.IO.StreamWriter.WriteLineAsync%2A>) 寫入檔案的方法。  
  
- <xref:System.IO.File> 所提供的靜態方法可將文字寫入檔案 (例如 <xref:System.IO.File.WriteAllLines%2A> 和 <xref:System.IO.File.WriteAllText%2A>)，或將文字附加至檔案 (例如 <xref:System.IO.File.AppendAllLines%2A>、<xref:System.IO.File.AppendAllText%2A> 或 <xref:System.IO.File.AppendText%2A>)。  
  
- <xref:System.IO.Path> 適用於含有檔案或目錄路徑資訊的字串。 它包含 <xref:System.IO.Path.Combine%2A> 方法 (在 .NET Core 2.1 和更新本中則包含 <xref:System.IO.Path.Join%2A> 和 <xref:System.IO.Path.TryJoin%2A> 方法)，可允許使用字串的串連來建置檔案或目錄路徑。

> [!NOTE]
> 下列範例只顯示所需的最少數量程式碼。 真實世界應用程式通常會提供更強大的錯誤檢查和例外狀況處理。  
  
## <a name="example-synchronously-write-text-with-streamwriter"></a>範例：使用 StreamWriter 同步寫入文字

下列範例示範如何使用 <xref:System.IO.StreamWriter> 類別，以同步方式一次一行將文字寫入新檔案。 由於 <xref:System.IO.StreamWriter> 物件是在 `using` 陳述式中宣告及具現化，因此會叫用 <xref:System.IO.StreamWriter.Dispose%2A> 方法，其會自動排清並關閉資料流。  

[!code-csharp[Conceptual.BasicIO.TextFiles#WriteLine](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.basicio.textfiles/cs/write.cs)]
[!code-vb[Conceptual.BasicIO.TextFiles#WriteLine](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.basicio.textfiles/vb/write.vb)]  

[!INCLUDE [localized code comments](../../../includes/code-comments-loc.md)]

## <a name="example-synchronously-append-text-with-streamwriter"></a>範例：使用 StreamWriter 同步附加文字

下列範例示範如何使用 <xref:System.IO.StreamWriter> 類別，以同步方式將文字附加至第一個範例中建立的文字檔。

[!code-csharp[Conceptual.BasicIO.TextFiles#WriteLine](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.basicio.textfiles/cs/append.cs)]
[!code-vb[Conceptual.BasicIO.TextFiles#WriteLine](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.basicio.textfiles/vb/append.vb)]  

## <a name="example-asynchronously-write-text-with-streamwriter"></a>範例：使用 StreamWriter 以非同步方式寫入文字

下列範例示範如何使用 <xref:System.IO.StreamWriter> 類別，以非同步方式將文字寫入至新檔案。 若要叫用 <xref:System.IO.StreamWriter.WriteAsync%2A> 方法，必須在 `async` 方法中呼叫此方法。 C# 範例需要 C# 7.1 或更新版本，它會在程式進入點新增對 `async` 修飾詞的支援。

[!code-csharp[Conceptual.BasicIO.TextFiles#WriteLine](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.basicio.textfiles/cs/async.cs)]
[!code-vb[Conceptual.BasicIO.TextFiles#WriteLine](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.basicio.textfiles/vb/async.vb)]  

## <a name="example-write-and-append-text-with-the-file-class"></a>範例：使用 File 類別撰寫和附加文字

下列範例示範如何使用 <xref:System.IO.File> 類別，將文字寫入至新檔案，並將新的文字行附加至相同的檔案。 <xref:System.IO.File.WriteAllText%2A> 和 <xref:System.IO.File.AppendAllLines%2A> 方法會自動開啟和關閉檔案。 如果提供給 <xref:System.IO.File.WriteAllText%2A> 方法的路徑已經存在，則會覆寫該檔案。  

[!code-csharp[Conceptual.BasicIO.TextFiles#WriteLine](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.basicio.textfiles/cs/file.cs)]
[!code-vb[Conceptual.BasicIO.TextFiles#WriteLine](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.basicio.textfiles/vb/file.vb)]  

## <a name="see-also"></a>請參閱

- <xref:System.IO.StreamWriter>
- <xref:System.IO.Path>
- <xref:System.IO.File.CreateText%2A?displayProperty=nameWithType>
- [如何：列舉目錄和檔案](how-to-enumerate-directories-and-files.md)
- [如何：讀取和寫入新建立的資料檔案](how-to-read-and-write-to-a-newly-created-data-file.md)
- [如何：開啟並附加至記錄檔](how-to-open-and-append-to-a-log-file.md)
- [如何：從檔案讀取文字](how-to-read-text-from-a-file.md)
- [檔案和資料流程 i/o](index.md)
