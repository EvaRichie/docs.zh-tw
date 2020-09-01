---
description: -define (C# 編譯器選項)
title: -define (C# 編譯器選項)
ms.date: 07/20/2015
f1_keywords:
- /define
helpviewer_keywords:
- -define compiler option [C#]
- /define compiler option [C#]
- -d compiler option [C#]
- define compiler option [C#]
- /d compiler option [C#]
- d compiler option [C#]
ms.assetid: f17d7b4d-82d0-4133-8563-68cced1cac6e
ms.openlocfilehash: 3b7a1c6e92d2c60ce289f29044774c3aa42ca84f
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89125874"
---
# <a name="-define-c-compiler-options"></a><span data-ttu-id="ca753-103">-define (C# 編譯器選項)</span><span class="sxs-lookup"><span data-stu-id="ca753-103">-define (C# Compiler Options)</span></span>
<span data-ttu-id="ca753-104">**-define** 選項會將 `name` 定義為程式中所有原始程式碼檔的符號。</span><span class="sxs-lookup"><span data-stu-id="ca753-104">The **-define** option defines `name` as a symbol in all source code files your program.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="ca753-105">語法</span><span class="sxs-lookup"><span data-stu-id="ca753-105">Syntax</span></span>  
  
```console  
-define:name[;name2]  
```  
  
## <a name="arguments"></a><span data-ttu-id="ca753-106">引數</span><span class="sxs-lookup"><span data-stu-id="ca753-106">Arguments</span></span>  
 <span data-ttu-id="ca753-107">`name`, `name2`</span><span class="sxs-lookup"><span data-stu-id="ca753-107">`name`, `name2`</span></span>  
 <span data-ttu-id="ca753-108">您要定義的一或多個符號之名稱。</span><span class="sxs-lookup"><span data-stu-id="ca753-108">The name of one or more symbols that you want to define.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="ca753-109">備註</span><span class="sxs-lookup"><span data-stu-id="ca753-109">Remarks</span></span>  
 <span data-ttu-id="ca753-110">**-define** 選項的作用與使用 [#define](../preprocessor-directives/preprocessor-define.md) 前置處理器指示詞相同，不同之處在於編譯器選項對專案中的所有檔案都有效。</span><span class="sxs-lookup"><span data-stu-id="ca753-110">The **-define** option has the same effect as using a [#define](../preprocessor-directives/preprocessor-define.md) preprocessor directive except that the compiler option is in effect for all files in the project.</span></span> <span data-ttu-id="ca753-111">直到原始程式檔中的 [#undef](../preprocessor-directives/preprocessor-undef.md) 指示詞移除符號的定義之前，符號在原始程式檔中都會維持已定義狀態。</span><span class="sxs-lookup"><span data-stu-id="ca753-111">A symbol remains defined in a source file until an [#undef](../preprocessor-directives/preprocessor-undef.md) directive in the source file removes the definition.</span></span> <span data-ttu-id="ca753-112">使用 -define 選項時，某個檔案中的 `#undef` 指示詞不會對專案中的其他原始程式碼檔造成影響。</span><span class="sxs-lookup"><span data-stu-id="ca753-112">When you use the -define option, an `#undef` directive in one file has no effect on other source code files in the project.</span></span>  
  
 <span data-ttu-id="ca753-113">您可以使用此選項建立的符號，搭配 [#if](../preprocessor-directives/preprocessor-if.md)、[#else](../preprocessor-directives/preprocessor-else.md)、[#elif](../preprocessor-directives/preprocessor-elif.md) 和 [#endif](../preprocessor-directives/preprocessor-endif.md)，有條件地編譯原始程式檔。</span><span class="sxs-lookup"><span data-stu-id="ca753-113">You can use symbols created by this option with [#if](../preprocessor-directives/preprocessor-if.md), [#else](../preprocessor-directives/preprocessor-else.md), [#elif](../preprocessor-directives/preprocessor-elif.md), and [#endif](../preprocessor-directives/preprocessor-endif.md) to compile source files conditionally.</span></span>  
  
 <span data-ttu-id="ca753-114">**-d** 是 **-define** 的簡短形式。</span><span class="sxs-lookup"><span data-stu-id="ca753-114">**-d** is the short form of **-define**.</span></span>  
  
 <span data-ttu-id="ca753-115">您可以使用分號或逗號分隔符號名稱，以 **-define** 定義多個符號。</span><span class="sxs-lookup"><span data-stu-id="ca753-115">You can define multiple symbols with **-define** by using a semicolon or comma to separate symbol names.</span></span> <span data-ttu-id="ca753-116">例如：</span><span class="sxs-lookup"><span data-stu-id="ca753-116">For example:</span></span>  
  
```console  
-define:DEBUG;TUESDAY  
```  
  
 <span data-ttu-id="ca753-117">C# 編譯器本身不會定義任何您可以在原始程式碼中使用的符號或巨集；所有符號定義都必須是使用者定義。</span><span class="sxs-lookup"><span data-stu-id="ca753-117">The C# compiler itself defines no symbols or macros that you can use in your source code; all symbol definitions must be user-defined.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="ca753-118">C# `#define` 不允許指定數值給符號，這點和 C++ 語言相同。</span><span class="sxs-lookup"><span data-stu-id="ca753-118">The C# `#define` does not allow a symbol to be given a value, as in languages such as C++.</span></span> <span data-ttu-id="ca753-119">例如，`#define` 不能用來建立巨集或定義常數。</span><span class="sxs-lookup"><span data-stu-id="ca753-119">For example, `#define` cannot be used to create a macro or to define a constant.</span></span> <span data-ttu-id="ca753-120">如果您需要定義常數，請使用 `enum` 變數。</span><span class="sxs-lookup"><span data-stu-id="ca753-120">If you need to define a constant, use an `enum` variable.</span></span> <span data-ttu-id="ca753-121">如果您想要建立 C++ 樣式巨集，請考慮替代項目，例如泛型。</span><span class="sxs-lookup"><span data-stu-id="ca753-121">If you want to create a C++ style macro, consider alternatives such as generics.</span></span> <span data-ttu-id="ca753-122">由於巨集非常可能發生錯誤，因此 C# 不允許使用巨集，而是提供較為安全的替代項目。</span><span class="sxs-lookup"><span data-stu-id="ca753-122">Since macros are notoriously error-prone, C# disallows their use but provides safer alternatives.</span></span>  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a><span data-ttu-id="ca753-123">在 Visual Studio 開發環境中設定這個編譯器選項</span><span class="sxs-lookup"><span data-stu-id="ca753-123">To set this compiler option in the Visual Studio development environment</span></span>  
  
1. <span data-ttu-id="ca753-124">開啟專案的 [屬性]\*\*\*\* 頁面。</span><span class="sxs-lookup"><span data-stu-id="ca753-124">Open the project's **Properties** page.</span></span>  
  
2. <span data-ttu-id="ca753-125">在 [建置]\*\*\*\* 索引標籤的 [條件式編譯的符號]\*\*\*\* 方塊中，輸入要定義的符號。</span><span class="sxs-lookup"><span data-stu-id="ca753-125">On the **Build** tab, type the symbol that is to be defined in the **Conditional compilation symbols** box.</span></span> <span data-ttu-id="ca753-126">例如，如果您想要使用下列程式碼範例，只要在文字方塊中鍵入 `xx` 即可。</span><span class="sxs-lookup"><span data-stu-id="ca753-126">For example, if you are using the code example that follows, just type `xx` into the text box.</span></span>  
  
 <span data-ttu-id="ca753-127">如需如何以程式設計方式設定這個編譯器選項的資訊，請參閱 <xref:VSLangProj80.CSharpProjectConfigurationProperties3.DefineConstants%2A>。</span><span class="sxs-lookup"><span data-stu-id="ca753-127">For information on how to set this compiler option programmatically, see <xref:VSLangProj80.CSharpProjectConfigurationProperties3.DefineConstants%2A>.</span></span>  
  
## <a name="example"></a><span data-ttu-id="ca753-128">範例</span><span class="sxs-lookup"><span data-stu-id="ca753-128">Example</span></span>  
  
```csharp  
// preprocessor_define.cs  
// compile with: -define:xx  
// or uncomment the next line  
// #define xx  
using System;  
public class Test
{  
    public static void Main()
    {  
        #if (xx)
            Console.WriteLine("xx defined");  
        #else  
            Console.WriteLine("xx not defined");  
        #endif  
    }  
}  
```  
  
## <a name="see-also"></a><span data-ttu-id="ca753-129">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ca753-129">See also</span></span>

- [<span data-ttu-id="ca753-130">C # 編譯器選項</span><span class="sxs-lookup"><span data-stu-id="ca753-130">C# Compiler Options</span></span>](./index.md)
- [<span data-ttu-id="ca753-131">管理專案和方案屬性</span><span class="sxs-lookup"><span data-stu-id="ca753-131">Managing Project and Solution Properties</span></span>](/visualstudio/ide/managing-project-and-solution-properties)
