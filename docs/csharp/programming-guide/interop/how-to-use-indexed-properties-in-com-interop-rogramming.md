---
title: '如何在 COM Interop 程式設計中使用索引屬性-c # 程式設計手冊'
description: '瞭解索引屬性如何改善在此 c # 範例中使用具有參數的 COM 屬性的方式。'
ms.date: 07/20/2015
helpviewer_keywords:
- indexed properties [C#]
- Office programming [C#], indexed properties
- properties [C#], indexed
ms.assetid: 756bfc1e-7c28-4d4d-b114-ac9288c73882
ms.openlocfilehash: abd785864bd79d455024cb4501c76a21b349aa91
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87303006"
---
# <a name="how-to-use-indexed-properties-in-com-interop-programming-c-programming-guide"></a><span data-ttu-id="ca989-103">如何在 COM Interop 程式設計中使用已編制索引的屬性（c # 程式設計手冊）</span><span class="sxs-lookup"><span data-stu-id="ca989-103">How to use indexed properties in COM interop programming (C# Programming Guide)</span></span>
<span data-ttu-id="ca989-104">「索引的屬性」\*\* 改善具有參數的 COM 屬性在 C# 程式設計中的使用方式。</span><span class="sxs-lookup"><span data-stu-id="ca989-104">*Indexed properties* improve the way in which COM properties that have parameters are consumed in C# programming.</span></span> <span data-ttu-id="ca989-105">索引的屬性是與其他 Visual C# 功能 (例如[具名和選擇性引數](../classes-and-structs/named-and-optional-arguments.md)、新類型 ([dynamic](../../language-reference/builtin-types/reference-types.md)) 和[內嵌類型資訊](../../../standard/assembly/embed-types-visual-studio.md)) 搭配運作，以加強 Microsoft Office 程式設計。</span><span class="sxs-lookup"><span data-stu-id="ca989-105">Indexed properties work together with other features in Visual C#, such as [named and optional arguments](../classes-and-structs/named-and-optional-arguments.md), a new type ([dynamic](../../language-reference/builtin-types/reference-types.md)), and [embedded type information](../../../standard/assembly/embed-types-visual-studio.md), to enhance Microsoft Office programming.</span></span>  
  
 <span data-ttu-id="ca989-106">在舊版 C# 中，只有在 `get` 方法沒有參數以及 `set` 方法只有一個值參數時，才能將方法存取為屬性。</span><span class="sxs-lookup"><span data-stu-id="ca989-106">In earlier versions of C#, methods are accessible as properties only if the `get` method has no parameters and the `set` method has one and only one value parameter.</span></span> <span data-ttu-id="ca989-107">不過，並非所有 COM 屬性都符合這些限制。</span><span class="sxs-lookup"><span data-stu-id="ca989-107">However, not all COM properties meet those restrictions.</span></span> <span data-ttu-id="ca989-108">例如，Excel <xref:Microsoft.Office.Interop.Excel.Range.Range%2A> 屬性具有需要範圍名稱參數的 `get` 存取子。</span><span class="sxs-lookup"><span data-stu-id="ca989-108">For example, the Excel <xref:Microsoft.Office.Interop.Excel.Range.Range%2A> property has a `get` accessor that requires a parameter for the name of the range.</span></span> <span data-ttu-id="ca989-109">在過去，因為您無法直接存取 `Range` 屬性，所以必須改為使用 `get_Range` 方法，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="ca989-109">In the past, because you could not access the `Range` property directly, you had to use the `get_Range` method instead, as shown in the following example.</span></span>  
  
 [!code-csharp[csProgGuideIndexedProperties#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideindexedproperties/cs/program.cs#1)]  
  
 <span data-ttu-id="ca989-110">索引的屬性可讓您改為撰寫下列程式碼︰</span><span class="sxs-lookup"><span data-stu-id="ca989-110">Indexed properties enable you to write the following instead:</span></span>  
  
 [!code-csharp[csProgGuideIndexedProperties#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideindexedproperties/cs/program.cs#2)]  
  
> [!NOTE]
> <span data-ttu-id="ca989-111">先前的範例也會使用[選擇性引數](../classes-and-structs/named-and-optional-arguments.md)功能，以讓您略過 `Type.Missing`。</span><span class="sxs-lookup"><span data-stu-id="ca989-111">The previous example also uses the [optional arguments](../classes-and-structs/named-and-optional-arguments.md) feature, which enables you to omit `Type.Missing`.</span></span>  
  
 <span data-ttu-id="ca989-112">與在 C# 3.0 和更早版本中設定 <xref:Microsoft.Office.Interop.Excel.Range> 物件的 `Value` 屬性值類似，需要兩個引數。</span><span class="sxs-lookup"><span data-stu-id="ca989-112">Similarly to set the value of the `Value` property of a <xref:Microsoft.Office.Interop.Excel.Range> object in C# 3.0 and earlier, two arguments are required.</span></span> <span data-ttu-id="ca989-113">其中一個提供選擇性參數的引數，而選擇性參數指定範圍值類型。</span><span class="sxs-lookup"><span data-stu-id="ca989-113">One supplies an argument for an optional parameter that specifies the type of the range value.</span></span> <span data-ttu-id="ca989-114">另一個則提供 `Value` 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="ca989-114">The other supplies the value for the `Value` property.</span></span> <span data-ttu-id="ca989-115">下列範例說明這些技術。</span><span class="sxs-lookup"><span data-stu-id="ca989-115">The following examples illustrate these techniques.</span></span> <span data-ttu-id="ca989-116">兩個都將 A1 儲存格的值設定為 `Name`。</span><span class="sxs-lookup"><span data-stu-id="ca989-116">Both set the value of the A1 cell to `Name`.</span></span>
  
 [!code-csharp[csProgGuideIndexedProperties#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideindexedproperties/cs/program.cs#3)]  
  
 <span data-ttu-id="ca989-117">索引的屬性可讓您改為撰寫下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="ca989-117">Indexed properties enable you to write the following code instead.</span></span>  
  
 [!code-csharp[csProgGuideIndexedProperties#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideindexedproperties/cs/program.cs#4)]  
  
 <span data-ttu-id="ca989-118">您無法建立自己本身的編製過索引的屬性。</span><span class="sxs-lookup"><span data-stu-id="ca989-118">You cannot create indexed properties of your own.</span></span> <span data-ttu-id="ca989-119">這個功能僅支援使用現有已編製過索引的屬性。</span><span class="sxs-lookup"><span data-stu-id="ca989-119">The feature only supports consumption of existing indexed properties.</span></span>  
  
## <a name="example"></a><span data-ttu-id="ca989-120">範例</span><span class="sxs-lookup"><span data-stu-id="ca989-120">Example</span></span>  
 <span data-ttu-id="ca989-121">下列程式碼顯示完整範例。</span><span class="sxs-lookup"><span data-stu-id="ca989-121">The following code shows a complete example.</span></span> <span data-ttu-id="ca989-122">如需如何設定存取 Office API 之專案的詳細資訊，請參閱[如何使用 c # 功能存取 office interop 物件](./how-to-access-office-onterop-objects.md)。</span><span class="sxs-lookup"><span data-stu-id="ca989-122">For more information about how to set up a project that accesses the Office API, see [How to access Office interop objects by using C# features](./how-to-access-office-onterop-objects.md).</span></span>
  
 [!code-csharp[csProgGuideIndexedProperties#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideindexedproperties/cs/program.cs#5)]  
  
## <a name="see-also"></a><span data-ttu-id="ca989-123">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ca989-123">See also</span></span>

- [<span data-ttu-id="ca989-124">具名和選擇性引數</span><span class="sxs-lookup"><span data-stu-id="ca989-124">Named and Optional Arguments</span></span>](../classes-and-structs/named-and-optional-arguments.md)
- [<span data-ttu-id="ca989-125">動態</span><span class="sxs-lookup"><span data-stu-id="ca989-125">dynamic</span></span>](../../language-reference/builtin-types/reference-types.md)
- [<span data-ttu-id="ca989-126">使用動態類型</span><span class="sxs-lookup"><span data-stu-id="ca989-126">Using Type dynamic</span></span>](../types/using-type-dynamic.md)
- [<span data-ttu-id="ca989-127">如何在 Office 程式設計中使用具名和選擇性引數</span><span class="sxs-lookup"><span data-stu-id="ca989-127">How to use named and optional arguments in Office programming</span></span>](../classes-and-structs/how-to-use-named-and-optional-arguments-in-office-programming.md)
- [<span data-ttu-id="ca989-128">如何使用 C# 功能存取 Office Interop 物件</span><span class="sxs-lookup"><span data-stu-id="ca989-128">How to access Office interop objects by using C# features</span></span>](./how-to-access-office-onterop-objects.md)
- [<span data-ttu-id="ca989-129">逐步解說：Office 程式設計</span><span class="sxs-lookup"><span data-stu-id="ca989-129">Walkthrough: Office Programming</span></span>](./walkthrough-office-programming.md)
