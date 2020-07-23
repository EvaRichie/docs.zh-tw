---
title: '如何使用屬性建立 C/c + + 等位（c #）'
description: '瞭解如何在 c # 中使用屬性來自訂結構在記憶體中的配置方式。 這個範例會從 C/c + + 執行等位的對等。'
ms.date: 07/20/2015
ms.assetid: 85f35e56-26e0-4d31-9f3a-89bd4005e71a
ms.openlocfilehash: 766a070105441630dfd8fecf7b9f68fa6818fe50
ms.sourcegitcommit: 40de8df14289e1e05b40d6e5c1daabd3c286d70c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86925068"
---
# <a name="how-to-create-a-cc-union-by-using-attributes-c"></a><span data-ttu-id="c82f5-104">如何使用屬性建立 C/c + + 等位（c #）</span><span class="sxs-lookup"><span data-stu-id="c82f5-104">How to create a C/C++ union by using attributes (C#)</span></span>

<span data-ttu-id="c82f5-105">藉由使用屬性，您可以自訂結構在記憶體中的配置方式。</span><span class="sxs-lookup"><span data-stu-id="c82f5-105">By using attributes, you can customize how structs are laid out in memory.</span></span> <span data-ttu-id="c82f5-106">例如，您可以使用 `StructLayout(LayoutKind.Explicit)` 和 `FieldOffset` 屬性，以 C/C++ 建立所謂的等位。</span><span class="sxs-lookup"><span data-stu-id="c82f5-106">For example, you can create what is known as a union in C/C++ by using the `StructLayout(LayoutKind.Explicit)` and `FieldOffset` attributes.</span></span>

## <a name="example"></a><span data-ttu-id="c82f5-107">範例</span><span class="sxs-lookup"><span data-stu-id="c82f5-107">Example</span></span>

<span data-ttu-id="c82f5-108">在此程式碼片段中，`TestUnion` 的所有欄位都在記憶體的同一位置開始。</span><span class="sxs-lookup"><span data-stu-id="c82f5-108">In this code segment, all of the fields of `TestUnion` start at the same location in memory.</span></span>

```csharp
// Add a using directive for System.Runtime.InteropServices.

[System.Runtime.InteropServices.StructLayout(LayoutKind.Explicit)]
struct TestUnion
{
    [System.Runtime.InteropServices.FieldOffset(0)]
    public int i;

    [System.Runtime.InteropServices.FieldOffset(0)]
    public double d;

    [System.Runtime.InteropServices.FieldOffset(0)]
    public char c;

    [System.Runtime.InteropServices.FieldOffset(0)]
    public byte b;
}
```

## <a name="example"></a><span data-ttu-id="c82f5-109">範例</span><span class="sxs-lookup"><span data-stu-id="c82f5-109">Example</span></span>

<span data-ttu-id="c82f5-110">以下是另一個範例，欄位從明確設定的不同位置開始。</span><span class="sxs-lookup"><span data-stu-id="c82f5-110">The following is another example where fields start at different explicitly set locations.</span></span>

```csharp
// Add a using directive for System.Runtime.InteropServices.

[System.Runtime.InteropServices.StructLayout(LayoutKind.Explicit)]
struct TestExplicit
{
    [System.Runtime.InteropServices.FieldOffset(0)]
    public long lg;

    [System.Runtime.InteropServices.FieldOffset(0)]
    public int i1;

    [System.Runtime.InteropServices.FieldOffset(4)]
    public int i2;

    [System.Runtime.InteropServices.FieldOffset(8)]
    public double d;

    [System.Runtime.InteropServices.FieldOffset(12)]
    public char c;

    [System.Runtime.InteropServices.FieldOffset(14)]
    public byte b;
}
```

<span data-ttu-id="c82f5-111">`i1` 和 `i2` 這兩個整數欄位和 `lg` 共用相同的記憶體位置。</span><span class="sxs-lookup"><span data-stu-id="c82f5-111">The two integer fields, `i1` and `i2`, share the same memory locations as `lg`.</span></span> <span data-ttu-id="c82f5-112">使用平台叫用時，這種結構配置控制項很有用。</span><span class="sxs-lookup"><span data-stu-id="c82f5-112">This sort of control over struct layout is useful when using platform invocation.</span></span>

## <a name="see-also"></a><span data-ttu-id="c82f5-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c82f5-113">See also</span></span>

- <xref:System.Reflection>
- <xref:System.Attribute>
- [<span data-ttu-id="c82f5-114">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="c82f5-114">C# Programming Guide</span></span>](../../index.md)
- [<span data-ttu-id="c82f5-115">屬性</span><span class="sxs-lookup"><span data-stu-id="c82f5-115">Attributes</span></span>](../../../../standard/attributes/index.md)
- [<span data-ttu-id="c82f5-116">反映 (C#)</span><span class="sxs-lookup"><span data-stu-id="c82f5-116">Reflection (C#)</span></span>](../reflection.md)
- [<span data-ttu-id="c82f5-117">屬性 (C#)</span><span class="sxs-lookup"><span data-stu-id="c82f5-117">Attributes (C#)</span></span>](index.md)
- [<span data-ttu-id="c82f5-118">建立自訂屬性 (C#)</span><span class="sxs-lookup"><span data-stu-id="c82f5-118">Creating Custom Attributes (C#)</span></span>](creating-custom-attributes.md)
- [<span data-ttu-id="c82f5-119">使用反映存取屬性 (C#)</span><span class="sxs-lookup"><span data-stu-id="c82f5-119">Accessing Attributes by Using Reflection (C#)</span></span>](accessing-attributes-by-using-reflection.md)
