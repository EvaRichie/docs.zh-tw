---
title: '如何建立檔案或資料夾-c # 程式設計手冊'
ms.date: 07/20/2015
helpviewer_keywords:
- folders [C#]
- creating files [C#]
- files [C#]
- creating folders [C#]
ms.assetid: 4582ee2d-d72d-4687-bcb9-08d336c62c25
ms.openlocfilehash: 5efe3b7dc600645488816d6f931df57fc236efc9
ms.sourcegitcommit: a241301495a84cc8c64fe972330d16edd619868b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/01/2020
ms.locfileid: "84241639"
---
# <a name="how-to-create-a-file-or-folder-c-programming-guide"></a>如何建立檔案或資料夾（c # 程式設計手冊）
您可以程式設計的方式在電腦上建立資料夾、建立子資料夾、在子資料夾中建立檔案，以及將資料寫入檔案。  
  
## <a name="example"></a>範例  
 [!code-csharp[csFilesandFolders#10](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csFilesAndFolders/CS/FileIteration.cs#10)]  
  
 若資料夾已經存在，<xref:System.IO.Directory.CreateDirectory%2A> 不會採取任何動作，也不會擲回任何例外狀況。 但 <xref:System.IO.File.Create%2A?displayProperty=nameWithType> 會以新的檔案取代現有的檔案。 此例使用 `if`-`else` 陳述式防止現有的檔案被取代。  
  
 透過在範例中進行下列變更，您可以根據是否已有具特定名稱的檔案來指定不同的結果。 如果沒有這類檔案，程式碼會建立一個。 如果有這類檔案，程式碼會將資料附加至該檔案。  
  
- 指定非隨機的檔案名稱。  
  
    ```csharp  
    // Comment out the following line.  
    //string fileName = System.IO.Path.GetRandomFileName();  
  
    // Replace that line with the following assignment.  
    string fileName = "MyNewFile.txt";  
    ```  
  
- 請在下列程式碼中以 `using` 陳述式取代 `if`-`else` 陳述式。  
  
    ```csharp  
    using (System.IO.FileStream fs = new System.IO.FileStream(pathString, FileMode.Append))
    {  
        for (byte i = 0; i < 100; i++)  
        {  
            fs.WriteByte(i);  
        }  
    }  
    ```  
  
 執行數次範例以確認資料是否每次都新增至檔案。  
  
 若要取得更多可以嘗試的 `FileMode` 值，請參考 <xref:System.IO.FileMode>。  
  
 以下條件可能會造成例外狀況：  
  
- 資料夾名稱的格式不正確。 舉例來說，其可能包含非法的字元，或是只有空白字元 (<xref:System.ArgumentException> 類別)。 請使用 <xref:System.IO.Path> 類別建立有效的路徑名稱。  
  
- 要建立之資料夾的父資料夾為唯讀 (<xref:System.IO.IOException> 類別)。  
  
- 資料夾名稱為 `null` (<xref:System.ArgumentNullException> 類別)。  
  
- 資料夾名稱過長 (<xref:System.IO.PathTooLongException> 類別)。  
  
- 資料夾名稱只是一個冒號 ":" (<xref:System.IO.PathTooLongException> 類別)。  
  
## <a name="net-security"></a>.NET 安全性  
 在部分信任的狀況下，可能會擲回 <xref:System.Security.SecurityException> 類別的執行個體。  
  
 如果您沒有建立資料夾的許可權，此範例會擲回類別的實例 <xref:System.UnauthorizedAccessException> 。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.IO?displayProperty=nameWithType>
- [C # 程式設計指南](../index.md)
- [檔案系統和登錄 (C# 程式設計手冊)](./index.md)
