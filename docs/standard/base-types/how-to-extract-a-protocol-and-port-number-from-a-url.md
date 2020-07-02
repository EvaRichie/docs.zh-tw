---
title: 作法：從 URL 擷取通訊協定和連接埠號碼
ms.date: 06/30/2020
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
ms.openlocfilehash: c1d45dbcb2916af86d645d7813594f2b278bb7c2
ms.sourcegitcommit: c23d9666ec75b91741da43ee3d91c317d68c7327
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85803868"
---
# <a name="how-to-extract-a-protocol-and-port-number-from-a-url"></a><span data-ttu-id="2e351-102">作法：從 URL 擷取通訊協定和連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="2e351-102">How to: Extract a Protocol and Port Number from a URL</span></span>
<span data-ttu-id="2e351-103">下列範例會從 URL 擷取通訊協定和連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="2e351-103">The following example extracts a protocol and port number from a URL.</span></span>  

[!INCLUDE [regex](../../../includes/regex.md)]

## <a name="example"></a><span data-ttu-id="2e351-104">範例</span><span class="sxs-lookup"><span data-stu-id="2e351-104">Example</span></span>  
 <span data-ttu-id="2e351-105">此範例會使用 <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=nameWithType> 方法來傳回通訊協定和連接埠號碼 (中間以冒號隔開)。</span><span class="sxs-lookup"><span data-stu-id="2e351-105">The example uses the <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=nameWithType> method to return the protocol followed by a colon followed by the port number.</span></span>  
  
 [!code-csharp[RegularExpressions.Examples.Protocol#1](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.Protocol/cs/Example.cs#1)]
 [!code-vb[RegularExpressions.Examples.Protocol#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.Protocol/vb/Example.vb#1)]  
  
 <span data-ttu-id="2e351-106">規則運算式模式 `^(?<proto>\w+)://[^/]+?(?<port>:\d+)?/` 的解譯方式如下表所示。</span><span class="sxs-lookup"><span data-stu-id="2e351-106">The regular expression pattern `^(?<proto>\w+)://[^/]+?(?<port>:\d+)?/` can be interpreted as shown in the following table.</span></span>  
  
|<span data-ttu-id="2e351-107">模式</span><span class="sxs-lookup"><span data-stu-id="2e351-107">Pattern</span></span>|<span data-ttu-id="2e351-108">描述</span><span class="sxs-lookup"><span data-stu-id="2e351-108">Description</span></span>|  
|-------------|-----------------|  
|`^`|<span data-ttu-id="2e351-109">在字串開頭開始比對。</span><span class="sxs-lookup"><span data-stu-id="2e351-109">Begin the match at the start of the string.</span></span>|  
|`(?<proto>\w+)`|<span data-ttu-id="2e351-110">比對一個或多個文字字元。</span><span class="sxs-lookup"><span data-stu-id="2e351-110">Match one or more word characters.</span></span> <span data-ttu-id="2e351-111">將這個群組命名為 `proto`。</span><span class="sxs-lookup"><span data-stu-id="2e351-111">Name this group `proto`.</span></span>|  
|`://`|<span data-ttu-id="2e351-112">比對冒號加兩個斜線符號。</span><span class="sxs-lookup"><span data-stu-id="2e351-112">Match a colon followed by two slash marks.</span></span>|  
|`[^/]+?`|<span data-ttu-id="2e351-113">比對一個或多個 (但越少越好) 出現的任何字元，但不包括斜線符號。</span><span class="sxs-lookup"><span data-stu-id="2e351-113">Match one or more occurrences (but as few as possible) of any character other than a slash mark.</span></span>|  
|`(?<port>:\d+)?`|<span data-ttu-id="2e351-114">比對零個或一個出現的冒號外加一個或多個數字字元。</span><span class="sxs-lookup"><span data-stu-id="2e351-114">Match zero or one occurrence of a colon followed by one or more digit characters.</span></span> <span data-ttu-id="2e351-115">將這個群組命名為 `port`。</span><span class="sxs-lookup"><span data-stu-id="2e351-115">Name this group `port`.</span></span>|  
|`/`|<span data-ttu-id="2e351-116">比對斜線符號。</span><span class="sxs-lookup"><span data-stu-id="2e351-116">Match a slash mark.</span></span>|  
  
 <span data-ttu-id="2e351-117"><xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=nameWithType> 方法會展開 `${proto}${port}` 取代序列，以將規則運算式模式中所擷取之兩個具名群組的值串連在一起。</span><span class="sxs-lookup"><span data-stu-id="2e351-117">The <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=nameWithType> method expands the `${proto}${port}` replacement sequence, which concatenates the value of the two named groups captured in the regular expression pattern.</span></span> <span data-ttu-id="2e351-118">另一種方便的作法是將 <xref:System.Text.RegularExpressions.Match.Groups%2A?displayProperty=nameWithType> 屬性所傳回之集合物件中擷取的字串明確地串連在一起。</span><span class="sxs-lookup"><span data-stu-id="2e351-118">It is a convenient alternative to explicitly concatenating the strings retrieved from the collection object returned by the <xref:System.Text.RegularExpressions.Match.Groups%2A?displayProperty=nameWithType> property.</span></span>  
  
 <span data-ttu-id="2e351-119">此範例會使用 <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=nameWithType> 方法搭配兩個替代項目 `${proto}` 和 `${port}`，以便在輸出字串中包含擷取的群組。</span><span class="sxs-lookup"><span data-stu-id="2e351-119">The example uses the <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=nameWithType> method with two substitutions, `${proto}` and `${port}`, to include the captured groups in the output string.</span></span> <span data-ttu-id="2e351-120">您可以改為從相符項目的 <xref:System.Text.RegularExpressions.GroupCollection> 物件中擷取該群組，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="2e351-120">You can retrieve the captured groups from the match's <xref:System.Text.RegularExpressions.GroupCollection> object instead, as the following code shows.</span></span>  
  
 [!code-csharp[RegularExpressions.Examples.Protocol#2](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.Protocol/cs/example2.cs#2)]
 [!code-vb[RegularExpressions.Examples.Protocol#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.Protocol/vb/example2.vb#2)]  
  
## <a name="see-also"></a><span data-ttu-id="2e351-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2e351-121">See also</span></span>

- [<span data-ttu-id="2e351-122">.NET 規則運算式</span><span class="sxs-lookup"><span data-stu-id="2e351-122">.NET Regular Expressions</span></span>](regular-expressions.md)
