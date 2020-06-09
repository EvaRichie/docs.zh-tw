---
title: 作法：從字串中刪除無效的字元
description: 閱讀範例，其中示範如何使用靜態 Regex. Replace 方法，從字串中去除可能有害的字元。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- regular expressions, examples
- cleaning input
- user input, examples
- .NET Framework regular expressions, examples
- regular expressions [.NET Framework], examples
- Regex.Replace method
- stripping invalid characters
- Replace method
- validating user input
ms.assetid: b4319c8a-9032-4129-a9d5-6f6fc28e7f32
ms.openlocfilehash: f9d671587d174a1eb2bb6a5dac24bdd0220be3dd
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600824"
---
# <a name="how-to-strip-invalid-characters-from-a-string"></a>作法：從字串中刪除無效的字元
下列範例會使用靜態 <xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=nameWithType> 方法，從字串中去除無效的字元。  
  
## <a name="example"></a>範例  
 您可以使用此範例中定義的 `CleanInput` 方法，去除使用者在文字欄位中可能已輸入的有害字元。 在此情況下，`CleanInput` 會去除句點 (.)、符號 (@) 以及連字號 (-) 以外的所有非英數字元，並傳回剩餘的字串。 不過，您可以修改規則運算式模式，讓它去除輸入字串中不應包含的任何字元。  
  
 [!code-csharp[RegularExpressions.Examples.StripChars#1](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.StripChars/cs/Example.cs#1)]
 [!code-vb[RegularExpressions.Examples.StripChars#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.StripChars/vb/Example.vb#1)]  
  
 規則運算式模式 `[^\w\.@-]` 會比對任何非文字字元的字元、句號、@ 符號或連字號。 文字字元是指任何字母、十進位數字或底線這類標點符號連接子。 任何符合這個模式的字元都會使用 <xref:System.String.Empty?displayProperty=nameWithType> (這是由取代模式所定義的字串) 來取代。 若要允許使用者輸入其他字元，可將這些字元新增至規則運算式模式中的字元類別。 例如，規則運算式模式 `[^\w\.@-\\%]` 也允許在輸入字串中使用百分比符號與反斜線。  
  
## <a name="see-also"></a>請參閱

- [.NET 規則運算式](regular-expressions.md)
