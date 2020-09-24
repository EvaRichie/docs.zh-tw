---
description: '#pragma 總和檢查碼 - C# 參考'
title: '#pragma 總和檢查碼 - C# 參考'
ms.date: 07/20/2015
f1_keywords:
- '#pragma checksum'
helpviewer_keywords:
- '#pragma checksum [C#]'
ms.assetid: 3673e4ca-6098-4ec1-890f-8fceb2a794a2
ms.openlocfilehash: df665704ac813adbbf6473e81fad0a1c7ff616d0
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91168565"
---
# <a name="pragma-checksum-c-reference"></a>#pragma 總和檢查碼 (C# 參考)

產生原始程式檔的總和檢查碼，協助偵錯 ASP.NET 頁面。  
  
## <a name="syntax"></a>語法  
  
```csharp
#pragma checksum "filename" "{guid}" "checksum bytes"  
```  
  
## <a name="parameters"></a>參數  

 `"filename"`  
 需要監視是否有變更或更新的檔案名稱。  
  
 `"{guid}"`  
 雜湊演算法的全域唯一識別碼 (GUID)。  
  
 `"checksum_bytes"`  
 代表總和檢查碼位元組的十六進位數字字串。 必須是偶數的十六進位數字。 奇數的數字會導致編譯時期警告，並且忽略指示詞。  
  
## <a name="remarks"></a>備註  

 Visual Studio 偵錯工具會使用總和檢查碼來確定一定會找到正確的來源。 編譯器會計算來源檔案的總和檢查碼，然後將輸出發至程式資料庫 (PDB) 檔案。 然後偵錯工具會使用 PDB 比較總和檢查碼計算來源檔案。  
  
 這個解決方案不適用於 ASP.NET 專案，因為計算過的總和檢查碼適合所產生原始程式檔而不是 .aspx 檔案。 若要解決這個問題，`#pragma checksum` 會為 ASP.NET 頁面提供總和檢查碼支援。  
  
 當您在 Visual C# 中建立 ASP.NET 專案時，所產生原始程式檔會包含來源 .aspx 檔案的總和檢查碼。 接著編譯器會將這項資訊寫入 PDB 檔案中。  
  
 如果編譯器在檔案中未遇到任何 `#pragma checksum` 指示詞，它會計算總和檢查碼並將值寫入 PDB 檔案。  
  
## <a name="example"></a>範例  
  
```csharp
class TestClass  
{  
    static int Main()  
    {  
        #pragma checksum "file.cs" "{406EA660-64CF-4C82-B6F0-42D48172A799}" "ab007f1d23d9" // New checksum  
    }  
}  
```  
  
## <a name="see-also"></a>另請參閱

- [C # 參考](../index.md)
- [C # 程式設計指南](../../programming-guide/index.md)
- [C # 預處理器指示詞](./index.md)
