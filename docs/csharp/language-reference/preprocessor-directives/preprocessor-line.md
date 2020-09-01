---
description: '#line - C# 參考'
title: '#line - C# 參考'
ms.date: 07/20/2015
f1_keywords:
- '#line'
helpviewer_keywords:
- '#line directive [C#]'
ms.assetid: 6439e525-5dd5-4acb-b8ea-efabb32ff95b
ms.openlocfilehash: e2a5ecb6c29184123b8a88ae1b12caf24ec7296a
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89137990"
---
# <a name="line-c-reference"></a><span data-ttu-id="12426-103">#line (C# 參考)</span><span class="sxs-lookup"><span data-stu-id="12426-103">#line (C# Reference)</span></span>

<span data-ttu-id="12426-104">`#line` 可讓您修改編譯器的行號以及 (選擇性) 錯誤和警告的檔案名稱輸出。</span><span class="sxs-lookup"><span data-stu-id="12426-104">`#line` lets you modify the compiler's line numbering and (optionally) the file name output for errors and warnings.</span></span>

<span data-ttu-id="12426-105">下列範例示範如何報告兩個與行號建立關聯的警告。</span><span class="sxs-lookup"><span data-stu-id="12426-105">The following example shows how to report two warnings associated with line numbers.</span></span> <span data-ttu-id="12426-106">`#line 200` 指示詞會將下一行的行號強制為 200 (但預設值為 #6)，而且在下一個 `#line` 指示詞之前，檔案名稱將會回報為 "Special"。</span><span class="sxs-lookup"><span data-stu-id="12426-106">The `#line 200` directive forces the next line's number to be 200 (although the default is #6), and until the next `#line` directive, the filename will be reported as "Special".</span></span> <span data-ttu-id="12426-107">`#line default` 指示詞會將行編號還原為其預設編號，這會計算已由先前的指示詞重新編號的行。</span><span class="sxs-lookup"><span data-stu-id="12426-107">The `#line default` directive returns the line numbering to its default numbering, which counts the lines that were renumbered by the previous directive.</span></span>

```csharp
class MainClass
{
    static void Main()
    {
#line 200 "Special"
        int i;
        int j;
#line default
        char c;
        float f;
#line hidden // numbering not affected
        string s;
        double d;
    }
}
```

<span data-ttu-id="12426-108">編譯會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="12426-108">Compilation produces the following output:</span></span>

```console
Special(200,13): warning CS0168: The variable 'i' is declared but never used
Special(201,13): warning CS0168: The variable 'j' is declared but never used
MainClass.cs(9,14): warning CS0168: The variable 'c' is declared but never used
MainClass.cs(10,15): warning CS0168: The variable 'f' is declared but never used
MainClass.cs(12,16): warning CS0168: The variable 's' is declared but never used
MainClass.cs(13,16): warning CS0168: The variable 'd' is declared but never used
```

## <a name="remarks"></a><span data-ttu-id="12426-109">備註</span><span class="sxs-lookup"><span data-stu-id="12426-109">Remarks</span></span>

<span data-ttu-id="12426-110">`#line` 指示詞可以用於建置程序中的自動化中繼步驟。</span><span class="sxs-lookup"><span data-stu-id="12426-110">The `#line` directive might be used in an automated, intermediate step in the build process.</span></span> <span data-ttu-id="12426-111">例如，如果已從原始程式碼檔中移除行，但您仍然想要編譯器根據檔案中的原始行編號來產生輸出，則可以移除行，然後模擬具有 `#line` 的原始行編號。</span><span class="sxs-lookup"><span data-stu-id="12426-111">For example, if lines were removed from the original source code file, but you still wanted the compiler to generate output based on the original line numbering in the file, you could remove lines and then simulate the original line numbering with `#line`.</span></span>

<span data-ttu-id="12426-112">`#line hidden` 指示詞會隱藏偵錯工具中的後續行，如此一來，開發人員逐步執行程式碼時，會逐步執行 `#line hidden` 與下一個 `#line` 指示詞 (假設它不是另一個 `#line hidden` 指示詞) 之間的任何行。</span><span class="sxs-lookup"><span data-stu-id="12426-112">The `#line hidden` directive hides the successive lines from the debugger, such that when the developer steps through the code, any lines between a `#line hidden` and the next `#line` directive (assuming that it is not another `#line hidden` directive) will be stepped over.</span></span> <span data-ttu-id="12426-113">此選項也可用來讓 ASP.NET 區分使用者定義的程式碼與電腦產生的程式碼。</span><span class="sxs-lookup"><span data-stu-id="12426-113">This option can also be used to allow ASP.NET to differentiate between user-defined and machine-generated code.</span></span> <span data-ttu-id="12426-114">雖然 ASP.NET 是這項功能的主要取用者，但是可能會有更多來源產生器利用它。</span><span class="sxs-lookup"><span data-stu-id="12426-114">Although ASP.NET is the primary consumer of this feature, it is likely that more source generators will make use of it.</span></span>

<span data-ttu-id="12426-115">`#line hidden` 指示詞不會影響錯誤報告中的檔案名稱或行號。</span><span class="sxs-lookup"><span data-stu-id="12426-115">A `#line hidden` directive does not affect file names or line numbers in error reporting.</span></span> <span data-ttu-id="12426-116">也就是說，如果隱藏區塊中發生錯誤，則編譯器會報告錯誤的目前檔案名稱和行號。</span><span class="sxs-lookup"><span data-stu-id="12426-116">That is, if an error is encountered in a hidden block, the compiler will report the current file name and line number of the error.</span></span>

<span data-ttu-id="12426-117">`#line filename` 指示詞指定您想要在編譯器輸出中顯示的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="12426-117">The `#line filename` directive specifies the file name you want to appear in the compiler output.</span></span> <span data-ttu-id="12426-118">預設會使用原始程式碼檔的實際名稱。</span><span class="sxs-lookup"><span data-stu-id="12426-118">By default, the actual name of the source code file is used.</span></span> <span data-ttu-id="12426-119">檔案名稱必須以雙引號 ("") 括住，而且前面必須有行號。</span><span class="sxs-lookup"><span data-stu-id="12426-119">The file name must be in double quotation marks ("") and must be preceded by a line number.</span></span>

<span data-ttu-id="12426-120">原始程式碼檔可以有任意數目的 `#line` 指示詞。</span><span class="sxs-lookup"><span data-stu-id="12426-120">A source code file can have any number of `#line` directives.</span></span>

## <a name="example-1"></a><span data-ttu-id="12426-121">範例 1</span><span class="sxs-lookup"><span data-stu-id="12426-121">Example 1</span></span>

<span data-ttu-id="12426-122">下列範例示範偵錯工具如何忽略程式碼中的隱藏行。</span><span class="sxs-lookup"><span data-stu-id="12426-122">The following example shows how the debugger ignores the hidden lines in the code.</span></span> <span data-ttu-id="12426-123">當您執行範例時，會顯示三行文字。</span><span class="sxs-lookup"><span data-stu-id="12426-123">When you run the example, it will display three lines of text.</span></span> <span data-ttu-id="12426-124">不過，如果您設定中斷點 (如此範例所示)，並按 F10 逐步執行程式碼，則會注意到偵錯工具忽略隱藏行。</span><span class="sxs-lookup"><span data-stu-id="12426-124">However, when you set a break point, as shown in the example, and hit F10 to step through the code, you will notice that the debugger ignores the hidden line.</span></span> <span data-ttu-id="12426-125">另請注意，即使您在隱藏行設定中斷點，偵錯工具仍然會忽略它。</span><span class="sxs-lookup"><span data-stu-id="12426-125">Notice also that even if you set a break point at the hidden line, the debugger will still ignore it.</span></span>

```csharp
// preprocessor_linehidden.cs
using System;
class MainClass
{
    static void Main()
    {
        Console.WriteLine("Normal line #1."); // Set break point here.
#line hidden
        Console.WriteLine("Hidden line.");
#line default
        Console.WriteLine("Normal line #2.");
    }
}
```

## <a name="see-also"></a><span data-ttu-id="12426-126">另請參閱</span><span class="sxs-lookup"><span data-stu-id="12426-126">See also</span></span>

- [<span data-ttu-id="12426-127">C # 參考</span><span class="sxs-lookup"><span data-stu-id="12426-127">C# Reference</span></span>](../index.md)
- [<span data-ttu-id="12426-128">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="12426-128">C# Programming Guide</span></span>](../../programming-guide/index.md)
- [<span data-ttu-id="12426-129">C # 預處理器指示詞</span><span class="sxs-lookup"><span data-stu-id="12426-129">C# Preprocessor Directives</span></span>](./index.md)
