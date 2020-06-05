---
title: 以零為基底與以一為基底的字串存取
ms.date: 07/20/2015
helpviewer_keywords:
- strings [Visual Basic], indexing
ms.assetid: 0ed39f35-d68e-421d-ae14-460a5c0373b8
ms.openlocfilehash: ce2fcb2610c09a9591a5fd79da4baa74cc533c99
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84363652"
---
# <a name="zero-based-vs-one-based-string-access-in-visual-basic"></a><span data-ttu-id="57d4b-102">Visual Basic 中以零起始與以一起始的字串存取之比較</span><span class="sxs-lookup"><span data-stu-id="57d4b-102">Zero-based vs. One-based String Access in Visual Basic</span></span>
<span data-ttu-id="57d4b-103">本主題比較 Visual Basic 和 .NET Framework 如何提供字串中字元的存取權。</span><span class="sxs-lookup"><span data-stu-id="57d4b-103">This topic compares how Visual Basic and the .NET Framework provide access to the characters in a string.</span></span> <span data-ttu-id="57d4b-104">.NET Framework 一律會以零為基底的方式存取字串中的字元，而 Visual Basic 提供以零為基底的存取，視函式而定。</span><span class="sxs-lookup"><span data-stu-id="57d4b-104">The .NET Framework always provides zero-based access to the characters in a string, whereas Visual Basic provides zero-based and one-based access, depending on the function.</span></span>  
  
## <a name="one-based"></a><span data-ttu-id="57d4b-105">以一為基礎</span><span class="sxs-lookup"><span data-stu-id="57d4b-105">One-Based</span></span>  
 <span data-ttu-id="57d4b-106">如需以一為基礎 Visual Basic 函式的範例，請考慮使用 `Mid` 函數。</span><span class="sxs-lookup"><span data-stu-id="57d4b-106">For an example of a one-based Visual Basic function, consider the `Mid` function.</span></span> <span data-ttu-id="57d4b-107">它會採用引數，指出子字串開始的字元位置，從位置1開始。</span><span class="sxs-lookup"><span data-stu-id="57d4b-107">It takes an argument that indicates the character position at which the substring will start, starting with position 1.</span></span> <span data-ttu-id="57d4b-108">.NET Framework <xref:System.String.Substring%2A?displayProperty=nameWithType> 方法會在字串中接受子字串的索引字元，從位置0開始。</span><span class="sxs-lookup"><span data-stu-id="57d4b-108">The .NET Framework <xref:System.String.Substring%2A?displayProperty=nameWithType> method takes an index of the character in the string at which the substring is to start, starting with position 0.</span></span> <span data-ttu-id="57d4b-109">因此，如果您有字串 "ABCDE"，則個別字元的編號為1、2、3、4、5以搭配函式使用 `Mid` ，但0、1、2、3、4用於 <xref:System.String.Substring%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="57d4b-109">Thus, if you have a string "ABCDE", the individual characters are numbered 1,2,3,4,5 for use with the `Mid` function, but 0,1,2,3,4 for use with the <xref:System.String.Substring%2A?displayProperty=nameWithType> method.</span></span>  
  
## <a name="zero-based"></a><span data-ttu-id="57d4b-110">以零為基底</span><span class="sxs-lookup"><span data-stu-id="57d4b-110">Zero-Based</span></span>  
 <span data-ttu-id="57d4b-111">如需以零為基底的 Visual Basic 函式的範例，請考慮使用 `Split` 函數。</span><span class="sxs-lookup"><span data-stu-id="57d4b-111">For an example of a zero-based Visual Basic function, consider the `Split` function.</span></span> <span data-ttu-id="57d4b-112">它會分割字串，並傳回包含子字串的陣列。</span><span class="sxs-lookup"><span data-stu-id="57d4b-112">It splits a string and returns an array containing the substrings.</span></span> <span data-ttu-id="57d4b-113">.NET Framework <xref:System.String.Split%2A?displayProperty=nameWithType> 方法也會分割字串，並傳回包含子字串的陣列。</span><span class="sxs-lookup"><span data-stu-id="57d4b-113">The .NET Framework <xref:System.String.Split%2A?displayProperty=nameWithType> method also splits a string and returns an array containing the substrings.</span></span> <span data-ttu-id="57d4b-114">因為函式 `Split` 和 <xref:System.String.Split%2A> 方法會傳回 .NET Framework 陣列，所以它們必須是以零為基底。</span><span class="sxs-lookup"><span data-stu-id="57d4b-114">Because the `Split` function and <xref:System.String.Split%2A> method return .NET Framework arrays, they must be zero-based.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="57d4b-115">另請參閱</span><span class="sxs-lookup"><span data-stu-id="57d4b-115">See also</span></span>

- <xref:Microsoft.VisualBasic.Strings.Mid%2A>
- <xref:Microsoft.VisualBasic.Strings.Split%2A>
- <xref:System.String.Substring%2A>
- <xref:System.String.Split%2A>
- [<span data-ttu-id="57d4b-116">Visual Basic 中的字串簡介</span><span class="sxs-lookup"><span data-stu-id="57d4b-116">Introduction to Strings in Visual Basic</span></span>](introduction-to-strings.md)
