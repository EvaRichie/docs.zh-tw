---
title: '如何判斷字串是否代表數值-c # 程式設計手冊'
ms.date: 07/20/2015
helpviewer_keywords:
- numeric strings [C#]
- validating numeric input [C#]
- strings [C#], numeric
ms.assetid: a4e84e10-ea0a-489f-a868-503dded9d85f
ms.openlocfilehash: 37437460ea4c6ca216f2844d63af3688ccc984c6
ms.sourcegitcommit: a241301495a84cc8c64fe972330d16edd619868b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/01/2020
ms.locfileid: "84241717"
---
# <a name="how-to-determine-whether-a-string-represents-a-numeric-value-c-programming-guide"></a><span data-ttu-id="f1308-102">如何判斷字串是否代表數值（c # 程式設計手冊）</span><span class="sxs-lookup"><span data-stu-id="f1308-102">How to determine whether a string represents a numeric value (C# Programming Guide)</span></span>
<span data-ttu-id="f1308-103">若要判斷字串是否為所指定數值類型的有效呈現，請使用靜態 `TryParse` 方法，而這個方法是由所有基本數字類型以及 <xref:System.DateTime> 和 <xref:System.Net.IPAddress> 此等類型所實作。</span><span class="sxs-lookup"><span data-stu-id="f1308-103">To determine whether a string is a valid representation of a specified numeric type, use the static `TryParse` method that is implemented by all primitive numeric types and also by types such as <xref:System.DateTime> and <xref:System.Net.IPAddress>.</span></span> <span data-ttu-id="f1308-104">下列範例示範如何判斷 "108" 是否為有效 [int](../../language-reference/builtin-types/integral-numeric-types.md)。</span><span class="sxs-lookup"><span data-stu-id="f1308-104">The following example shows how to determine whether "108" is a valid [int](../../language-reference/builtin-types/integral-numeric-types.md).</span></span>  
  
```csharp  
int i = 0;
string s = "108";  
bool result = int.TryParse(s, out i); //i now = 108  
```  
  
 <span data-ttu-id="f1308-105">如果字串包含非數值字元，或所指定之特定類型的數值太大或太小，則 `TryParse` 會傳回 false，並將 out 參數設定為零。</span><span class="sxs-lookup"><span data-stu-id="f1308-105">If the string contains nonnumeric characters or the numeric value is too large or too small for the particular type you have specified, `TryParse` returns false and sets the out parameter to zero.</span></span> <span data-ttu-id="f1308-106">否則會傳回 true，並將 out 參數設定為字串的數值。</span><span class="sxs-lookup"><span data-stu-id="f1308-106">Otherwise, it returns true and sets the out parameter to the numeric value of the string.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="f1308-107">字串只能包含數值字元，而且仍然不適用於您所使用 `TryParse` 方法的類型。</span><span class="sxs-lookup"><span data-stu-id="f1308-107">A string may contain only numeric characters and still not be valid for the type whose `TryParse` method that you use.</span></span> <span data-ttu-id="f1308-108">例如，"256" 不是 `byte` 的有效值，但為 `int` 的有效值。</span><span class="sxs-lookup"><span data-stu-id="f1308-108">For example, "256" is not a valid value for `byte` but it is valid for `int`.</span></span> <span data-ttu-id="f1308-109">"98.6" 不是 `int` 的有效值，但為有效的 `decimal`。</span><span class="sxs-lookup"><span data-stu-id="f1308-109">"98.6" is not a valid value for `int` but it is a valid `decimal`.</span></span>  
  
## <a name="example"></a><span data-ttu-id="f1308-110">範例</span><span class="sxs-lookup"><span data-stu-id="f1308-110">Example</span></span>  
 <span data-ttu-id="f1308-111">下列範例示範如何搭配使用 `TryParse` 與 `long`、`byte` 和 `decimal` 值的字串呈現。</span><span class="sxs-lookup"><span data-stu-id="f1308-111">The following examples show how to use `TryParse` with string representations of `long`, `byte`, and `decimal` values.</span></span>  
  
 [!code-csharp[csProgGuideStrings#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStrings/CS/Strings.cs#14)]  
  
## <a name="robust-programming"></a><span data-ttu-id="f1308-112">穩固程式設計</span><span class="sxs-lookup"><span data-stu-id="f1308-112">Robust Programming</span></span>  
 <span data-ttu-id="f1308-113">基本數值類型也會實作 `Parse` 靜態方法，但如果字串不是有效數字，則會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f1308-113">Primitive numeric types also implement the `Parse` static method, which throws an exception if the string is not a valid number.</span></span> <span data-ttu-id="f1308-114">`TryParse` 通常更具效率，因為它在數字不正確時就會傳回 false。</span><span class="sxs-lookup"><span data-stu-id="f1308-114">`TryParse` is generally more efficient because it just returns false if the number is not valid.</span></span>  
  
## <a name="net-security"></a><span data-ttu-id="f1308-115">.NET 安全性</span><span class="sxs-lookup"><span data-stu-id="f1308-115">.NET Security</span></span>  
 <span data-ttu-id="f1308-116">請一律使用 `TryParse` 或 `Parse` 方法來驗證文字方塊和下拉式方塊這類控制項的使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="f1308-116">Always use the `TryParse` or `Parse` methods to validate user input from controls such as text boxes and combo boxes.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f1308-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f1308-117">See also</span></span>

- [<span data-ttu-id="f1308-118">如何將位元組陣列轉換成整數</span><span class="sxs-lookup"><span data-stu-id="f1308-118">How to convert a byte array to an int</span></span>](../types/how-to-convert-a-byte-array-to-an-int.md)
- [<span data-ttu-id="f1308-119">如何將字串轉換為數值</span><span class="sxs-lookup"><span data-stu-id="f1308-119">How to convert a string to a number</span></span>](../types/how-to-convert-a-string-to-a-number.md)
- [<span data-ttu-id="f1308-120">如何在十六進位字串和數字類型間轉換</span><span class="sxs-lookup"><span data-stu-id="f1308-120">How to convert between hexadecimal strings and numeric types</span></span>](../types/how-to-convert-between-hexadecimal-strings-and-numeric-types.md)
- [<span data-ttu-id="f1308-121">剖析數值字串</span><span class="sxs-lookup"><span data-stu-id="f1308-121">Parsing Numeric Strings</span></span>](../../../standard/base-types/parsing-numeric.md)
- [<span data-ttu-id="f1308-122">格式化類型</span><span class="sxs-lookup"><span data-stu-id="f1308-122">Formatting Types</span></span>](../../../standard/base-types/formatting-types.md)
