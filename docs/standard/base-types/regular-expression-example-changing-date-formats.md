---
title: 規則運算式範例：變更日期格式
ms.date: 06/30/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- searching with regular expressions, examples
- parsing text with regular expressions, examples
- regular expressions, examples
- .NET regular expressions, examples
- regular expressions [.NET], examples
- pattern-matching with regular expressions, examples
ms.assetid: 5fcc75a5-09d7-45ae-a4c0-9ad6085ac83d
ms.openlocfilehash: b5eca8c294349fada9cfb1cb3ed8e2012edd8bda
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/28/2020
ms.locfileid: "92889409"
---
# <a name="regular-expression-example-changing-date-formats"></a>規則運算式範例：變更日期格式
下列程式碼範例會使用 <xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=nameWithType> 方法，將 *mm* dd yy 格式的日期取代為 / *dd* / *yy* *dd* - *mm* - *yy* 格式的日期。  

[!INCLUDE [regex](../../../includes/regex.md)]

## <a name="example"></a>範例  
 [!code-csharp[RegularExpressions.Examples.ChangeDateFormats#1](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.ChangeDateFormats/cs/Example_ChangeDateFormats1.cs#1)]
 [!code-vb[RegularExpressions.Examples.ChangeDateFormats#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.ChangeDateFormats/vb/Example_ChangeDateFormats1.vb#1)]  
  
 以下程式碼將說明如何在應用程式中呼叫 `MDYToDMY` 方法。  
  
 [!code-csharp[RegularExpressions.Examples.ChangeDateFormats#2](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.ChangeDateFormats/cs/Example_ChangeDateFormats1.cs#2)]
 [!code-vb[RegularExpressions.Examples.ChangeDateFormats#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.ChangeDateFormats/vb/Example_ChangeDateFormats1.vb#2)]  
  
## <a name="comments"></a>註解  
 規則運算式模式 `\b(?<month>\d{1,2})/(?<day>\d{1,2})/(?<year>\d{2,4})\b` 的解譯方式如下表所示。  
  
|模式|描述|  
|-------------|-----------------|  
|`\b`|開始字緣比對。|  
|`(?<month>\d{1,2})`|比對一個或兩個十進位數字。 這是 `month` 擷取群組。|  
|`/`|比對斜線符號。|  
|`(?<day>\d{1,2})`|比對一個或兩個十進位數字。 這是 `day` 擷取群組。|  
|`/`|比對斜線符號。|  
|`(?<year>\d{2,4})`|比對兩個到四個十進位數字。 這是 `year` 擷取群組。|  
|`\b`|結束字緣比對。|  
  
 模式 `${day}-${month}-${year}` 會定義取代字串，如下表所示。  
  
|模式|描述|  
|-------------|-----------------|  
|`$(day)`|加入 `day` 擷取群組所擷取的字串。|  
|`-`|加入連字號。|  
|`$(month)`|加入 `month` 擷取群組所擷取的字串。|  
|`-`|加入連字號。|  
|`$(year)`|加入 `year` 擷取群組所擷取的字串。|  
  
## <a name="see-also"></a>請參閱

- [.NET 規則運算式](regular-expressions.md)
