---
title: set 關鍵字 - C# 參考
ms.date: 03/10/2017
f1_keywords:
- set
- set_CSharpKeyword
helpviewer_keywords:
- set keyword [C#]
ms.assetid: 30d7e4e5-cc2e-4635-a597-14a724879619
ms.openlocfilehash: cdd84c824cc4dc93f4433f07e9978d22cba3f245
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82795062"
---
# <a name="set-c-reference"></a><span data-ttu-id="e8946-102">set (C# 參考)</span><span class="sxs-lookup"><span data-stu-id="e8946-102">set (C# Reference)</span></span>

<span data-ttu-id="e8946-103">`set` 關鍵字會在屬性或索引子中定義「存取子」\*\* 方法，以將值指派給屬性或索引子項目。</span><span class="sxs-lookup"><span data-stu-id="e8946-103">The `set` keyword defines an *accessor* method in a property or indexer that assigns a value to the property or the indexer element.</span></span> <span data-ttu-id="e8946-104">如需詳細資訊和範例，請參閱[屬性](../../programming-guide/classes-and-structs/properties.md)、[自動實作的屬性](../../programming-guide/classes-and-structs/auto-implemented-properties.md)和[索引子](../../programming-guide/indexers/index.md)。</span><span class="sxs-lookup"><span data-stu-id="e8946-104">For more information and examples, see [Properties](../../programming-guide/classes-and-structs/properties.md), [Auto-Implemented Properties](../../programming-guide/classes-and-structs/auto-implemented-properties.md), and [Indexers](../../programming-guide/indexers/index.md).</span></span>

<span data-ttu-id="e8946-105">下列範例會為名為 `Seconds` 的屬性定義 `get` 和 `set` 存取子。</span><span class="sxs-lookup"><span data-stu-id="e8946-105">The following example defines both a `get` and a `set` accessor for a property named `Seconds`.</span></span> <span data-ttu-id="e8946-106">它使用名為 `_seconds` 的私用欄位來支援屬性值。</span><span class="sxs-lookup"><span data-stu-id="e8946-106">It uses a private field named `_seconds` to back the property value.</span></span>

[!code-csharp[set#1](~/samples/snippets/csharp/language-reference/keywords/get/get-1.cs)]

<span data-ttu-id="e8946-107">`set` 存取子通常是由指派值的單一陳述式所組成，如上述範例所示。</span><span class="sxs-lookup"><span data-stu-id="e8946-107">Often, the `set` accessor consists of a single statement that assigns a value, as it did in the previous example.</span></span> <span data-ttu-id="e8946-108">從 C# 7.0 開始，您可以將 `set` 存取子實作為運算式主體成員。</span><span class="sxs-lookup"><span data-stu-id="e8946-108">Starting with C# 7.0, you can implement the `set` accessor as an expression-bodied member.</span></span> <span data-ttu-id="e8946-109">下列範例會將 `get` 和 `set` 存取子實作為運算式主體成員。</span><span class="sxs-lookup"><span data-stu-id="e8946-109">The following example implements both the `get` and the `set` accessors as expression-bodied members.</span></span>

[!code-csharp[set#3](~/samples/snippets/csharp/language-reference/keywords/get/get-3.cs)]
  
<span data-ttu-id="e8946-110">如果屬性的 `get` 和 `set` 存取子只會設定或擷取私用支援欄位中的值，而不會執行其他作業，在此簡單的情況下，您可以利用 C# 編譯器的自動實作屬性支援。</span><span class="sxs-lookup"><span data-stu-id="e8946-110">For simple cases in which a property's `get` and `set` accessors perform no other operation than setting or retrieving a value in a private backing field, you can take advantage of the C# compiler's support for auto-implemented properties.</span></span> <span data-ttu-id="e8946-111">下列程式碼範例將 `Hours` 實作為自動實作屬性。</span><span class="sxs-lookup"><span data-stu-id="e8946-111">The following example implements `Hours` as an auto-implemented property.</span></span>

[!code-csharp[set#2](~/samples/snippets/csharp/language-reference/keywords/get/get-2.cs)]
  
## <a name="c-language-specification"></a><span data-ttu-id="e8946-112">C# 語言規格</span><span class="sxs-lookup"><span data-stu-id="e8946-112">C# language specification</span></span>

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a><span data-ttu-id="e8946-113">請參閱</span><span class="sxs-lookup"><span data-stu-id="e8946-113">See also</span></span>

- [<span data-ttu-id="e8946-114">C # 參考</span><span class="sxs-lookup"><span data-stu-id="e8946-114">C# Reference</span></span>](../index.md)
- [<span data-ttu-id="e8946-115">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="e8946-115">C# Programming Guide</span></span>](../../programming-guide/index.md)
- [<span data-ttu-id="e8946-116">C # 關鍵字</span><span class="sxs-lookup"><span data-stu-id="e8946-116">C# Keywords</span></span>](index.md)
- [<span data-ttu-id="e8946-117">屬性</span><span class="sxs-lookup"><span data-stu-id="e8946-117">Properties</span></span>](../../programming-guide/classes-and-structs/properties.md)
