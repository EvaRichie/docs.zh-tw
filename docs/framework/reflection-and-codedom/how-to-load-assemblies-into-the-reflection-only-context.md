---
title: 作法：將組件載入僅限反映的內容
description: 瞭解如何在 .NET 中將元件載入僅限反映的內容的範例。 檢查針對其他平臺或 .NET 版本編譯的元件。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- reflection, reflection-only loader context
- assemblies [.NET Framework], loading for reflection
- attributes [.NET Framework], retrieving
- assemblies [.NET Framework], reflection-only loader context
- reflection-only loader context
ms.assetid: 9818b660-52f5-423d-a9af-e75163aa7068
ms.openlocfilehash: 92f847f6c61ba39bf8621af6080baccfdabe514a
ms.sourcegitcommit: 3d84eac0818099c9949035feb96bbe0346358504
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/21/2020
ms.locfileid: "86865069"
---
# <a name="how-to-load-assemblies-into-the-reflection-only-context"></a><span data-ttu-id="06efe-104">作法：將組件載入僅限反映的內容</span><span class="sxs-lookup"><span data-stu-id="06efe-104">How to: Load Assemblies into the Reflection-Only Context</span></span>

<span data-ttu-id="06efe-105">僅限反映的載入內容可讓您檢查針對其他平台或其他 .NET Framework 版本所編譯的組件。</span><span class="sxs-lookup"><span data-stu-id="06efe-105">The reflection-only load context allows you to examine assemblies compiled for other platforms or for other versions of the .NET Framework.</span></span> <span data-ttu-id="06efe-106">只能檢查載入至此內容的程式碼，而無法執行。</span><span class="sxs-lookup"><span data-stu-id="06efe-106">Code loaded into this context can only be examined; it cannot be executed.</span></span> <span data-ttu-id="06efe-107">這表示無法建立物件，因為無法執行建構函式。</span><span class="sxs-lookup"><span data-stu-id="06efe-107">This means that objects cannot be created, because constructors cannot be executed.</span></span> <span data-ttu-id="06efe-108">因為無法執行程式碼，所以不會自動載入相依性。</span><span class="sxs-lookup"><span data-stu-id="06efe-108">Because the code cannot be executed, dependencies are not automatically loaded.</span></span> <span data-ttu-id="06efe-109">如果您需要檢查它們，則必須自行載入。</span><span class="sxs-lookup"><span data-stu-id="06efe-109">If you need to examine them, you must load them yourself.</span></span>

## <a name="to-load-an-assembly-into-the-reflection-only-load-context"></a><span data-ttu-id="06efe-110">將組件載入僅限反映的載入內容</span><span class="sxs-lookup"><span data-stu-id="06efe-110">To load an assembly into the reflection-only load context</span></span>

1. <span data-ttu-id="06efe-111">使用 <xref:System.Reflection.Assembly.ReflectionOnlyLoad%28System.String%29> 方法多載來載入組件並提供其顯示名稱，或 <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A> 方法來載入組件並提供其路徑。</span><span class="sxs-lookup"><span data-stu-id="06efe-111">Use the <xref:System.Reflection.Assembly.ReflectionOnlyLoad%28System.String%29> method overload to load the assembly given its display name, or the <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A> method to load the assembly given its path.</span></span> <span data-ttu-id="06efe-112">如果組件是二進位映像，請使用 <xref:System.Reflection.Assembly.ReflectionOnlyLoad%28System.Byte%5B%5D%29> 方法多載。</span><span class="sxs-lookup"><span data-stu-id="06efe-112">If the assembly is a binary image, use the <xref:System.Reflection.Assembly.ReflectionOnlyLoad%28System.Byte%5B%5D%29> method overload.</span></span>

    > [!NOTE]
    > <span data-ttu-id="06efe-113">您無法使用僅限反映的內容，從執行內容中的版本以外的 .NET Framework 版本載入 mscorlib.dll 版本。</span><span class="sxs-lookup"><span data-stu-id="06efe-113">You cannot use the reflection-only context to load a version of mscorlib.dll from a version of the .NET Framework other than the version in the execution context.</span></span>

2. <span data-ttu-id="06efe-114">如果組件具有相依性，則 <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A> 方法不會載入它們。</span><span class="sxs-lookup"><span data-stu-id="06efe-114">If the assembly has dependencies, the <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A> method does not load them.</span></span> <span data-ttu-id="06efe-115">如果您需要檢查它們，則必須自行載入。</span><span class="sxs-lookup"><span data-stu-id="06efe-115">If you need to examine them, you must load them yourself.</span></span>

3. <span data-ttu-id="06efe-116">判斷是否使用組件的 <xref:System.Reflection.Assembly.ReflectionOnly%2A> 屬性，將組件載入僅限反映的內容。</span><span class="sxs-lookup"><span data-stu-id="06efe-116">Determine whether an assembly is loaded into the reflection-only context by using the assembly's <xref:System.Reflection.Assembly.ReflectionOnly%2A> property.</span></span>

4. <span data-ttu-id="06efe-117">如果已將屬性套用至組件或組件中的類型，請使用 <xref:System.Reflection.CustomAttributeData> 類別來檢查這些屬性，確保不會嘗試在僅限反映的內容中執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="06efe-117">If attributes have been applied to the assembly or to types in the assembly, examine those attributes by using the <xref:System.Reflection.CustomAttributeData> class to ensure that no attempt is made to execute code in the reflection-only context.</span></span> <span data-ttu-id="06efe-118">使用 <xref:System.Reflection.CustomAttributeData.GetCustomAttributes%2A?displayProperty=nameWithType> 方法的適當多載來取得 <xref:System.Reflection.CustomAttributeData> 物件，這些物件代表套用至組件、成員、模組或參數的屬性。</span><span class="sxs-lookup"><span data-stu-id="06efe-118">Use the appropriate overload of the <xref:System.Reflection.CustomAttributeData.GetCustomAttributes%2A?displayProperty=nameWithType> method to obtain <xref:System.Reflection.CustomAttributeData> objects representing the attributes applied to an assembly, member, module, or parameter.</span></span>

    > [!NOTE]
    > <span data-ttu-id="06efe-119">套用至組件或其內容的屬性可能定義於組件中，或可能定義於另一個載入僅限反映內容的組件中。</span><span class="sxs-lookup"><span data-stu-id="06efe-119">Attributes applied to the assembly or to its contents might be defined in the assembly, or they might be defined in another assembly loaded into the reflection-only context.</span></span> <span data-ttu-id="06efe-120">沒有方法事先知道定義屬性的位置。</span><span class="sxs-lookup"><span data-stu-id="06efe-120">There is no way to tell in advance where the attributes are defined.</span></span>

## <a name="example"></a><span data-ttu-id="06efe-121">範例</span><span class="sxs-lookup"><span data-stu-id="06efe-121">Example</span></span>

<span data-ttu-id="06efe-122">下列程式碼範例示範如何檢查套用至載入僅限反映內容之組件的屬性。</span><span class="sxs-lookup"><span data-stu-id="06efe-122">The following code example shows how to examine the attributes applied to an assembly loaded into the reflection-only context.</span></span>

<span data-ttu-id="06efe-123">此程式碼範例會定義具有兩個建構函式和一個屬性 (property) 的自訂屬性 (attribute)。</span><span class="sxs-lookup"><span data-stu-id="06efe-123">The code example defines a custom attribute with two constructors and one property.</span></span> <span data-ttu-id="06efe-124">屬性會套用至組件、組件中宣告的類型、類型的方法，以及方法的參數。</span><span class="sxs-lookup"><span data-stu-id="06efe-124">The attribute is applied to the assembly, to a type declared in the assembly, to a method of the type, and to a parameter of the method.</span></span> <span data-ttu-id="06efe-125">執行時，組件會將它自己載入僅限反映的內容，並顯示已套用至它以及它所含類型和成員之自訂屬性的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="06efe-125">When executed, the assembly loads itself into the reflection-only context and displays information about the custom attributes that were applied to it and to the types and members it contains.</span></span>

> [!NOTE]
> <span data-ttu-id="06efe-126">為了簡化程式碼範例，組件會載入並檢查本身。</span><span class="sxs-lookup"><span data-stu-id="06efe-126">To simplify the code example, the assembly loads and examines itself.</span></span> <span data-ttu-id="06efe-127">一般來說，您不會想要找到同時載入執行內容和僅限反映內容的相同組件。</span><span class="sxs-lookup"><span data-stu-id="06efe-127">Normally, you would not expect to find the same assembly loaded into both the execution context and the reflection-only context.</span></span>

[!code-cpp[CustomAttributeData#1](../../../samples/snippets/cpp/VS_Snippets_CLR/CustomAttributeData/CPP/source.cpp#1)]
[!code-csharp[CustomAttributeData#1](../../../samples/snippets/csharp/VS_Snippets_CLR/CustomAttributeData/CS/source.cs#1)]
[!code-vb[CustomAttributeData#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CustomAttributeData/VB/source.vb#1)]

## <a name="see-also"></a><span data-ttu-id="06efe-128">另請參閱</span><span class="sxs-lookup"><span data-stu-id="06efe-128">See also</span></span>

- <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A>
- <xref:System.Reflection.Assembly.ReflectionOnly%2A>
- <xref:System.Reflection.CustomAttributeData>
