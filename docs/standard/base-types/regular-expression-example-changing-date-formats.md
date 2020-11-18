---
title: 規則運算式範例：變更日期格式
ms.date: 06/30/2020
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
ms.openlocfilehash: 51d2b773cc3149ddbf7d98409fd7b6947b379745
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94830294"
---
# <a name="regular-expression-example-changing-date-formats"></a><span data-ttu-id="e1db0-102">規則運算式範例：變更日期格式</span><span class="sxs-lookup"><span data-stu-id="e1db0-102">Regular Expression Example: Changing Date Formats</span></span>
<span data-ttu-id="e1db0-103">下列程式碼範例會使用 <xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=nameWithType> 方法，將 *mm* dd yy 格式的日期取代為 / *dd* / *yy* *dd* - *mm* - *yy* 格式的日期。</span><span class="sxs-lookup"><span data-stu-id="e1db0-103">The following code example uses the <xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=nameWithType> method to replace dates that have the form *mm*/*dd*/*yy* with dates that have the form *dd*-*mm*-*yy*.</span></span>  

[!INCLUDE [regex](../../../includes/regex.md)]

## <a name="example"></a><span data-ttu-id="e1db0-104">範例</span><span class="sxs-lookup"><span data-stu-id="e1db0-104">Example</span></span>  
 [!code-csharp[RegularExpressions.Examples.ChangeDateFormats#1](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.ChangeDateFormats/cs/Example_ChangeDateFormats1.cs#1)]
 [!code-vb[RegularExpressions.Examples.ChangeDateFormats#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.ChangeDateFormats/vb/Example_ChangeDateFormats1.vb#1)]  
  
 <span data-ttu-id="e1db0-105">以下程式碼將說明如何在應用程式中呼叫 `MDYToDMY` 方法。</span><span class="sxs-lookup"><span data-stu-id="e1db0-105">The following code shows how the `MDYToDMY` method can be called in an application.</span></span>  
  
 [!code-csharp[RegularExpressions.Examples.ChangeDateFormats#2](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.ChangeDateFormats/cs/Example_ChangeDateFormats1.cs#2)]
 [!code-vb[RegularExpressions.Examples.ChangeDateFormats#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.ChangeDateFormats/vb/Example_ChangeDateFormats1.vb#2)]  
  
## <a name="comments"></a><span data-ttu-id="e1db0-106">註解</span><span class="sxs-lookup"><span data-stu-id="e1db0-106">Comments</span></span>  
 <span data-ttu-id="e1db0-107">規則運算式模式 `\b(?<month>\d{1,2})/(?<day>\d{1,2})/(?<year>\d{2,4})\b` 的解譯方式如下表所示。</span><span class="sxs-lookup"><span data-stu-id="e1db0-107">The regular expression pattern  `\b(?<month>\d{1,2})/(?<day>\d{1,2})/(?<year>\d{2,4})\b` is interpreted as shown in the following table.</span></span>  
  
|<span data-ttu-id="e1db0-108">模式</span><span class="sxs-lookup"><span data-stu-id="e1db0-108">Pattern</span></span>|<span data-ttu-id="e1db0-109">描述</span><span class="sxs-lookup"><span data-stu-id="e1db0-109">Description</span></span>|  
|-------------|-----------------|  
|`\b`|<span data-ttu-id="e1db0-110">開始字緣比對。</span><span class="sxs-lookup"><span data-stu-id="e1db0-110">Begin the match at a word boundary.</span></span>|  
|`(?<month>\d{1,2})`|<span data-ttu-id="e1db0-111">比對一個或兩個十進位數字。</span><span class="sxs-lookup"><span data-stu-id="e1db0-111">Match one or two decimal digits.</span></span> <span data-ttu-id="e1db0-112">這是 `month` 擷取群組。</span><span class="sxs-lookup"><span data-stu-id="e1db0-112">This is the `month` captured group.</span></span>|  
|`/`|<span data-ttu-id="e1db0-113">比對斜線符號。</span><span class="sxs-lookup"><span data-stu-id="e1db0-113">Match the slash mark.</span></span>|  
|`(?<day>\d{1,2})`|<span data-ttu-id="e1db0-114">比對一個或兩個十進位數字。</span><span class="sxs-lookup"><span data-stu-id="e1db0-114">Match one or two decimal digits.</span></span> <span data-ttu-id="e1db0-115">這是 `day` 擷取群組。</span><span class="sxs-lookup"><span data-stu-id="e1db0-115">This is the `day` captured group.</span></span>|  
|`/`|<span data-ttu-id="e1db0-116">比對斜線符號。</span><span class="sxs-lookup"><span data-stu-id="e1db0-116">Match the slash mark.</span></span>|  
|`(?<year>\d{2,4})`|<span data-ttu-id="e1db0-117">比對兩個到四個十進位數字。</span><span class="sxs-lookup"><span data-stu-id="e1db0-117">Match from two to four decimal digits.</span></span> <span data-ttu-id="e1db0-118">這是 `year` 擷取群組。</span><span class="sxs-lookup"><span data-stu-id="e1db0-118">This is the `year` captured group.</span></span>|  
|`\b`|<span data-ttu-id="e1db0-119">結束字緣比對。</span><span class="sxs-lookup"><span data-stu-id="e1db0-119">End the match at a word boundary.</span></span>|  
  
 <span data-ttu-id="e1db0-120">模式 `${day}-${month}-${year}` 會定義取代字串，如下表所示。</span><span class="sxs-lookup"><span data-stu-id="e1db0-120">The pattern `${day}-${month}-${year}` defines the replacement string as shown in the following table.</span></span>  
  
|<span data-ttu-id="e1db0-121">模式</span><span class="sxs-lookup"><span data-stu-id="e1db0-121">Pattern</span></span>|<span data-ttu-id="e1db0-122">描述</span><span class="sxs-lookup"><span data-stu-id="e1db0-122">Description</span></span>|  
|-------------|-----------------|  
|`$(day)`|<span data-ttu-id="e1db0-123">加入 `day` 擷取群組所擷取的字串。</span><span class="sxs-lookup"><span data-stu-id="e1db0-123">Add the string captured by the `day` capturing group.</span></span>|  
|`-`|<span data-ttu-id="e1db0-124">加入連字號。</span><span class="sxs-lookup"><span data-stu-id="e1db0-124">Add a hyphen.</span></span>|  
|`$(month)`|<span data-ttu-id="e1db0-125">加入 `month` 擷取群組所擷取的字串。</span><span class="sxs-lookup"><span data-stu-id="e1db0-125">Add the string captured by the `month` capturing group.</span></span>|  
|`-`|<span data-ttu-id="e1db0-126">加入連字號。</span><span class="sxs-lookup"><span data-stu-id="e1db0-126">Add a hyphen.</span></span>|  
|`$(year)`|<span data-ttu-id="e1db0-127">加入 `year` 擷取群組所擷取的字串。</span><span class="sxs-lookup"><span data-stu-id="e1db0-127">Add the string captured by the `year` capturing group.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="e1db0-128">請參閱</span><span class="sxs-lookup"><span data-stu-id="e1db0-128">See also</span></span>

- [<span data-ttu-id="e1db0-129">.NET 規則運算式</span><span class="sxs-lookup"><span data-stu-id="e1db0-129">.NET Regular Expressions</span></span>](regular-expressions.md)
