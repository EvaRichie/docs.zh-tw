---
title: 陣列維度
ms.date: 07/20/2015
helpviewer_keywords:
- dimensions, arrays
- arrays [Visual Basic], dimensions
- arrays [Visual Basic], rectangular
- arrays [Visual Basic], rank
- rectangular arrays
- ranking, arrays
ms.assetid: 385e911b-18c1-4e98-9924-c6d279101dd9
ms.openlocfilehash: f971f0c3693177adbcb8869d487e3ad41d49ddc2
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84413100"
---
# <a name="array-dimensions-in-visual-basic"></a><span data-ttu-id="d6308-102">Array Dimensions in Visual Basic</span><span class="sxs-lookup"><span data-stu-id="d6308-102">Array Dimensions in Visual Basic</span></span>

<span data-ttu-id="d6308-103">*維度*是一種可以改變陣列元素規格的方向。</span><span class="sxs-lookup"><span data-stu-id="d6308-103">A *dimension* is a direction in which you can vary the specification of an array's elements.</span></span> <span data-ttu-id="d6308-104">保存當月每一天之銷售總額的陣列，有一個維度（當月的第一天）。</span><span class="sxs-lookup"><span data-stu-id="d6308-104">An array that holds the sales total for each day of the month has one dimension (the day of the month).</span></span> <span data-ttu-id="d6308-105">每個月的銷售總額依部門保存的陣列有兩個維度（部門編號和月份的日期）。</span><span class="sxs-lookup"><span data-stu-id="d6308-105">An array that holds the sales total by department for each day of the month has two dimensions (the department number and the day of the month).</span></span> <span data-ttu-id="d6308-106">陣列所擁有的維度數目稱為其*次序*。</span><span class="sxs-lookup"><span data-stu-id="d6308-106">The number of dimensions an array has is called its *rank*.</span></span>

> [!NOTE]
> <span data-ttu-id="d6308-107">您可以使用 <xref:System.Array.Rank%2A> 屬性來判斷陣列具有多少維度。</span><span class="sxs-lookup"><span data-stu-id="d6308-107">You can use the <xref:System.Array.Rank%2A> property to determine the how many dimensions an array has.</span></span>

## <a name="working-with-dimensions"></a><span data-ttu-id="d6308-108">使用維度</span><span class="sxs-lookup"><span data-stu-id="d6308-108">Working with Dimensions</span></span>

<span data-ttu-id="d6308-109">您可以為每個維度提供*索引*或注*標*，藉以指定陣列的元素。</span><span class="sxs-lookup"><span data-stu-id="d6308-109">You specify an element of an array by supplying an *index* or *subscript* for each of its dimensions.</span></span> <span data-ttu-id="d6308-110">元素是從索引0到該維度的最高索引的每個維度的連續。</span><span class="sxs-lookup"><span data-stu-id="d6308-110">The elements are contiguous along each dimension from index 0 through the highest index for that dimension.</span></span>

<span data-ttu-id="d6308-111">下圖顯示具有不同排名之陣列的概念結構。</span><span class="sxs-lookup"><span data-stu-id="d6308-111">The following illustrations show the conceptual structure of arrays with different ranks.</span></span> <span data-ttu-id="d6308-112">圖例中的每個元素都會顯示存取它的索引值。</span><span class="sxs-lookup"><span data-stu-id="d6308-112">Each element in the illustrations shows the index values that access it.</span></span> <span data-ttu-id="d6308-113">例如，您可以藉由指定索引來存取二維陣列中第二個數據列的第一個元素 `(1, 0)` 。</span><span class="sxs-lookup"><span data-stu-id="d6308-113">For example, you can access the first element of the second row of the two-dimensional array by specifying indexes `(1, 0)`.</span></span>

![顯示一維陣列的圖表。](./media/array-dimensions/one-dimensional-array.gif)

![顯示二維陣列的圖表。](./media/array-dimensions/two-dimensional-array.gif)

![顯示三維陣列的圖表。](./media/array-dimensions/three-dimensional-array.gif)

### <a name="one-dimension"></a><span data-ttu-id="d6308-117">一個維度</span><span class="sxs-lookup"><span data-stu-id="d6308-117">One Dimension</span></span>

<span data-ttu-id="d6308-118">許多陣列只有一個維度，例如每個年齡的人員人數。</span><span class="sxs-lookup"><span data-stu-id="d6308-118">Many arrays have only one dimension, such as the number of people of each age.</span></span> <span data-ttu-id="d6308-119">唯一指定專案的需求是該元素持有計數的年齡。</span><span class="sxs-lookup"><span data-stu-id="d6308-119">The only requirement to specify an element is the age for which that element holds the count.</span></span> <span data-ttu-id="d6308-120">因此，這類陣列只會使用一個索引。</span><span class="sxs-lookup"><span data-stu-id="d6308-120">Therefore, such an array uses only one index.</span></span> <span data-ttu-id="d6308-121">下列範例會宣告一個變數，以保留*一維*的年齡計數陣列，用於年齡0到120。</span><span class="sxs-lookup"><span data-stu-id="d6308-121">The following example declares a variable to hold a *one-dimensional array* of age counts for ages 0 through 120.</span></span>

```vb
Dim ageCounts(120) As UInteger
```

### <a name="two-dimensions"></a><span data-ttu-id="d6308-122">兩個維度</span><span class="sxs-lookup"><span data-stu-id="d6308-122">Two Dimensions</span></span>

<span data-ttu-id="d6308-123">有些陣列有兩個維度，例如校園上每個建築物的每個樓層的辦公室數目。</span><span class="sxs-lookup"><span data-stu-id="d6308-123">Some arrays have two dimensions, such as the number of offices on each floor of each building on a campus.</span></span> <span data-ttu-id="d6308-124">元素的規格需要建築物編號和樓層，而且每個專案都包含該建築物和樓層的計算計數。</span><span class="sxs-lookup"><span data-stu-id="d6308-124">The specification of an element requires both the building number and the floor, and each element holds the count for that combination of building and floor.</span></span> <span data-ttu-id="d6308-125">因此，這類陣列會使用兩個索引。</span><span class="sxs-lookup"><span data-stu-id="d6308-125">Therefore, such an array uses two indexes.</span></span> <span data-ttu-id="d6308-126">下列範例會宣告一個變數，以保存一維的 office 計數*陣列*，適用于建築物0到40，而樓層0到5的一個。</span><span class="sxs-lookup"><span data-stu-id="d6308-126">The following example declares a variable to hold a *two-dimensional array* of office counts, for buildings 0 through 40 and floors 0 through 5.</span></span>

```vb
Dim officeCounts(40, 5) As Byte
```

<span data-ttu-id="d6308-127">二維陣列也稱為「*矩形陣列*」。</span><span class="sxs-lookup"><span data-stu-id="d6308-127">A two-dimensional array is also called a *rectangular array*.</span></span>

### <a name="three-dimensions"></a><span data-ttu-id="d6308-128">三個維度</span><span class="sxs-lookup"><span data-stu-id="d6308-128">Three Dimensions</span></span>

<span data-ttu-id="d6308-129">幾個陣列有三個維度，例如3d 空間中的值。</span><span class="sxs-lookup"><span data-stu-id="d6308-129">A few arrays have three dimensions, such as values in three-dimensional space.</span></span> <span data-ttu-id="d6308-130">這類陣列使用三個索引，在此案例中代表實體空間的 x、y 和 z 座標。</span><span class="sxs-lookup"><span data-stu-id="d6308-130">Such an array uses three indexes, which in this case represent the x, y, and z coordinates of physical space.</span></span> <span data-ttu-id="d6308-131">下列範例會宣告一個變數，以在三維磁片區中的不同點上保留一維空氣溫度*陣列*。</span><span class="sxs-lookup"><span data-stu-id="d6308-131">The following example declares a variable to hold a *three-dimensional array* of air temperatures at various points in a three-dimensional volume.</span></span>

```vb
Dim airTemperatures(99, 99, 24) As Single
```

### <a name="more-than-three-dimensions"></a><span data-ttu-id="d6308-132">三個以上的維度</span><span class="sxs-lookup"><span data-stu-id="d6308-132">More than Three Dimensions</span></span>

<span data-ttu-id="d6308-133">雖然陣列最多可以有32個維度，但很少會有三個以上的大小。</span><span class="sxs-lookup"><span data-stu-id="d6308-133">Although an array can have as many as 32 dimensions, it is rare to have more than three.</span></span>

> [!NOTE]
> <span data-ttu-id="d6308-134">當您將維度新增至陣列時，陣列所需的總儲存空間會大幅增加，因此請小心使用多維陣列。</span><span class="sxs-lookup"><span data-stu-id="d6308-134">When you add dimensions to an array, the total storage needed by the array increases considerably, so use multidimensional arrays with care.</span></span>

## <a name="using-different-dimensions"></a><span data-ttu-id="d6308-135">使用不同的維度</span><span class="sxs-lookup"><span data-stu-id="d6308-135">Using Different Dimensions</span></span>

<span data-ttu-id="d6308-136">假設您想要追蹤目前月份每天的銷售金額。</span><span class="sxs-lookup"><span data-stu-id="d6308-136">Suppose you want to track sales amounts for every day of the present month.</span></span> <span data-ttu-id="d6308-137">您可以宣告一維陣列，其中包含31個元素，每個月一天一個，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="d6308-137">You might declare a one-dimensional array with 31 elements, one for each day of the month, as the following example shows.</span></span>

```vb
Dim salesAmounts(30) As Double
```

<span data-ttu-id="d6308-138">現在假設您想要追蹤相同的資訊，而不只是每個月的一天，而且每個月都有。</span><span class="sxs-lookup"><span data-stu-id="d6308-138">Now suppose you want to track the same information not only for every day of a month but also for every month of the year.</span></span> <span data-ttu-id="d6308-139">您可以宣告具有12個數據列（適用于月份）和31個數據行（代表天）的二維陣列，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="d6308-139">You might declare a two-dimensional array with 12 rows (for the months) and 31 columns (for the days), as the following example shows.</span></span>

```vb
Dim salesAmounts(11, 30) As Double
```

<span data-ttu-id="d6308-140">現在假設您決定讓陣列保存超過一年的資訊。</span><span class="sxs-lookup"><span data-stu-id="d6308-140">Now suppose you decide to have your array hold information for more than one year.</span></span> <span data-ttu-id="d6308-141">如果您想要追蹤5年的銷售量，您可以宣告具有5個圖層、12個數據列和31個數據行的三維陣列，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="d6308-141">If you want to track sales amounts for 5 years, you could declare a three-dimensional array with 5 layers, 12 rows, and 31 columns, as the following example shows.</span></span>

```vb
Dim salesAmounts(4, 11, 30) As Double
```

<span data-ttu-id="d6308-142">請注意，因為每個索引的大小從0到最大值，所以的每個維度 `salesAmounts` 都會宣告為小於該維度所需的長度。</span><span class="sxs-lookup"><span data-stu-id="d6308-142">Note that, because each index varies from 0 to its maximum, each dimension of `salesAmounts` is declared as one less than the required length for that dimension.</span></span> <span data-ttu-id="d6308-143">另請注意，陣列的大小會隨著每個新的維度而增加。</span><span class="sxs-lookup"><span data-stu-id="d6308-143">Note also that the size of the array increases with each new dimension.</span></span> <span data-ttu-id="d6308-144">上述範例中的三個大小分別為31、372和1860個元素。</span><span class="sxs-lookup"><span data-stu-id="d6308-144">The three sizes in the preceding examples are 31, 372, and 1,860 elements respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="d6308-145">您可以建立陣列，而不使用 `Dim` 語句或 `New` 子句。</span><span class="sxs-lookup"><span data-stu-id="d6308-145">You can create an array without using the `Dim` statement or the `New` clause.</span></span> <span data-ttu-id="d6308-146">例如，您可以呼叫 <xref:System.Array.CreateInstance%2A> 方法，或另一個元件可以將以這種方式建立的陣列傳遞給您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="d6308-146">For example, you can call the <xref:System.Array.CreateInstance%2A> method, or another component can pass your code an array created in this manner.</span></span> <span data-ttu-id="d6308-147">這類陣列可以具有小於0的下限。</span><span class="sxs-lookup"><span data-stu-id="d6308-147">Such an array can have a lower bound other than 0.</span></span> <span data-ttu-id="d6308-148">您一律可以使用方法或函數，測試維度的下限 <xref:System.Array.GetLowerBound%2A> `LBound` 。</span><span class="sxs-lookup"><span data-stu-id="d6308-148">You can always test for the lower bound of a dimension by using the <xref:System.Array.GetLowerBound%2A> method or the `LBound` function.</span></span>

## <a name="see-also"></a><span data-ttu-id="d6308-149">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d6308-149">See also</span></span>

- [<span data-ttu-id="d6308-150">陣列</span><span class="sxs-lookup"><span data-stu-id="d6308-150">Arrays</span></span>](index.md)
- [<span data-ttu-id="d6308-151">針對陣列進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="d6308-151">Troubleshooting Arrays</span></span>](troubleshooting-arrays.md)
