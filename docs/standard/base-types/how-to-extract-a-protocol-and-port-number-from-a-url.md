---
title: 作法：從 URL 擷取通訊協定和連接埠號碼
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- searching with regular expressions, examples
- parsing text with regular expressions, examples
- regular expressions, examples
- .NET Framework regular expressions, examples
- regular expressions [.NET Framework], examples
- pattern-matching with regular expressions, examples
ms.assetid: ab7f62b3-6d2c-4efb-8ac6-28600df5fd5c
ms.openlocfilehash: 48f2bf5c0d9af0a3fc286561ba978f86d1f11ac8
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84290483"
---
# <a name="how-to-extract-a-protocol-and-port-number-from-a-url"></a>作法：從 URL 擷取通訊協定和連接埠號碼
下列範例會從 URL 擷取通訊協定和連接埠號碼。  
  
## <a name="example"></a>範例  
 此範例會使用 <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=nameWithType> 方法來傳回通訊協定和連接埠號碼 (中間以冒號隔開)。  
  
 [!code-csharp[RegularExpressions.Examples.Protocol#1](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.Protocol/cs/Example.cs#1)]
 [!code-vb[RegularExpressions.Examples.Protocol#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.Protocol/vb/Example.vb#1)]  
  
 規則運算式模式 `^(?<proto>\w+)://[^/]+?(?<port>:\d+)?/` 的解譯方式如下表所示。  
  
|模式|描述|  
|-------------|-----------------|  
|`^`|在字串開頭開始比對。|  
|`(?<proto>\w+)`|比對一個或多個文字字元。 將這個群組命名為 `proto`。|  
|`://`|比對冒號加兩個斜線符號。|  
|`[^/]+?`|比對一個或多個 (但越少越好) 出現的任何字元，但不包括斜線符號。|  
|`(?<port>:\d+)?`|比對零個或一個出現的冒號外加一個或多個數字字元。 將這個群組命名為 `port`。|  
|`/`|比對斜線符號。|  
  
 <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=nameWithType> 方法會展開 `${proto}${port}` 取代序列，以將規則運算式模式中所擷取之兩個具名群組的值串連在一起。 另一種方便的作法是將 <xref:System.Text.RegularExpressions.Match.Groups%2A?displayProperty=nameWithType> 屬性所傳回之集合物件中擷取的字串明確地串連在一起。  
  
 此範例會使用 <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=nameWithType> 方法搭配兩個替代項目 `${proto}` 和 `${port}`，以便在輸出字串中包含擷取的群組。 您可以改為從相符項目的 <xref:System.Text.RegularExpressions.GroupCollection> 物件中擷取該群組，如下列程式碼所示。  
  
 [!code-csharp[RegularExpressions.Examples.Protocol#2](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.Protocol/cs/example2.cs#2)]
 [!code-vb[RegularExpressions.Examples.Protocol#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.Protocol/vb/example2.vb#2)]  
  
## <a name="see-also"></a>另請參閱

- [.NET 規則運算式](regular-expressions.md)
