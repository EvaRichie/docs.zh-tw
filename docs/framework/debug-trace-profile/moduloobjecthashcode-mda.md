---
title: moduloObjectHashcode MDA
description: 請參閱 moduloObjectHashcode managed 偵錯工具（MDA），這會變更物件類別，以取得 GetHashCode 方法結果的餘數值。
ms.date: 03/30/2017
helpviewer_keywords:
- managed debugging assistants (MDAs), hashcode modulus
- Modulo object hash code
- moduloObjectHashcode MDA
- hashcode modulus
- MDAs (managed debugging assistants), hashcode modulus
- GetHashCode method
- modulus of hashcodes
ms.assetid: b45366ff-2a7a-4b8e-ab01-537b72e9de68
ms.openlocfilehash: a929ec2b9196f1f6cad0528fdf7323839a86fa55
ms.sourcegitcommit: 0edbeb66d71b8df10fcb374cfca4d731b58ccdb2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/07/2020
ms.locfileid: "86052061"
---
# <a name="moduloobjecthashcode-mda"></a><span data-ttu-id="a646b-103">moduloObjectHashcode MDA</span><span class="sxs-lookup"><span data-stu-id="a646b-103">moduloObjectHashcode MDA</span></span>
<span data-ttu-id="a646b-104">`moduloObjectHashcode` Managed 偵錯助理 (MDA) 會變更 <xref:System.Object> 類別對 <xref:System.Object.GetHashCode%2A> 方法所傳回之雜湊碼執行模數作業的行為。</span><span class="sxs-lookup"><span data-stu-id="a646b-104">The `moduloObjectHashcode` managed debugging assistant (MDA) changes the behavior of the <xref:System.Object> class to perform a modulo operation on the hash code returned by the <xref:System.Object.GetHashCode%2A> method.</span></span> <span data-ttu-id="a646b-105">此 MDA 的預設模數是 1，讓 <xref:System.Object.GetHashCode%2A> 針對所有物件都傳回 0。</span><span class="sxs-lookup"><span data-stu-id="a646b-105">The default modulus for this MDA is 1, which causes <xref:System.Object.GetHashCode%2A> to return 0 for all objects.</span></span>  
  
## <a name="symptoms"></a><span data-ttu-id="a646b-106">徵狀</span><span class="sxs-lookup"><span data-stu-id="a646b-106">Symptoms</span></span>  
 <span data-ttu-id="a646b-107">移至新版的 Common Language Runtime (CLR) 之後，就無法再正確地執行程式：</span><span class="sxs-lookup"><span data-stu-id="a646b-107">After moving to a new version of the common language runtime (CLR), a program no longer executes properly:</span></span>  
  
- <span data-ttu-id="a646b-108">程式會從 <xref:System.Collections.Hashtable> 取得錯誤的物件。</span><span class="sxs-lookup"><span data-stu-id="a646b-108">The program is getting the wrong object from a <xref:System.Collections.Hashtable>.</span></span>  
  
- <span data-ttu-id="a646b-109"><xref:System.Collections.Hashtable> 中的列舉順序包含中斷程式的變更。</span><span class="sxs-lookup"><span data-stu-id="a646b-109">The order of enumeration from a <xref:System.Collections.Hashtable> has a change that breaks the program.</span></span>  
  
- <span data-ttu-id="a646b-110">兩個相等的物件不再相等。</span><span class="sxs-lookup"><span data-stu-id="a646b-110">Two objects that used to be equal are no longer equal.</span></span>  
  
- <span data-ttu-id="a646b-111">兩個不相等的物件現在相等。</span><span class="sxs-lookup"><span data-stu-id="a646b-111">Two objects that used to not be equal are now equal.</span></span>  
  
## <a name="cause"></a><span data-ttu-id="a646b-112">原因</span><span class="sxs-lookup"><span data-stu-id="a646b-112">Cause</span></span>  
 <span data-ttu-id="a646b-113">您的程式可能從 <xref:System.Collections.Hashtable> 取得錯誤物件，因為 <xref:System.Collections.Hashtable> 中索引鍵類別上的 <xref:System.Object.Equals%2A> 方法實作會比較 <xref:System.Object.GetHashCode%2A> 方法呼叫的結果，來測試物件是否相等。</span><span class="sxs-lookup"><span data-stu-id="a646b-113">Your program may be getting the wrong object from a <xref:System.Collections.Hashtable> because the implementation of the <xref:System.Object.Equals%2A> method on the class for the key into the <xref:System.Collections.Hashtable> tests for equality of objects by comparing the results of the call to the <xref:System.Object.GetHashCode%2A> method.</span></span> <span data-ttu-id="a646b-114">雜湊碼不應該用來測試物件是否相等，因為兩個物件可能有相同的雜湊碼，即使其個別欄位具有不同的值也是一樣。</span><span class="sxs-lookup"><span data-stu-id="a646b-114">Hash codes should not be used to test for object equality because two objects may have the same hash code even if their respective fields have different values.</span></span> <span data-ttu-id="a646b-115">雖然實務上十分罕見，但確實會發生這些雜湊碼衝突。</span><span class="sxs-lookup"><span data-stu-id="a646b-115">These hash code collisions, although rare in practice, do occur.</span></span> <span data-ttu-id="a646b-116">這對 <xref:System.Collections.Hashtable> 查閱的影響是兩個不相等的索引鍵顯示為相等，並且從 <xref:System.Collections.Hashtable> 傳回錯誤的物件。</span><span class="sxs-lookup"><span data-stu-id="a646b-116">The effect this has on a <xref:System.Collections.Hashtable> lookup is that two keys which are not equal appear to be equal, and the wrong object is returned from the <xref:System.Collections.Hashtable>.</span></span> <span data-ttu-id="a646b-117">基於效能考量，<xref:System.Object.GetHashCode%2A> 實作可以在執行階段版本之間變更，因此某個版本可能不會發生的衝突可能會在後續版本上發生。</span><span class="sxs-lookup"><span data-stu-id="a646b-117">For performance reasons, the implementation of <xref:System.Object.GetHashCode%2A> can change between runtime versions, so collisions that might not occur on one version might occur on subsequent versions.</span></span> <span data-ttu-id="a646b-118">讓此 MDA 測試在雜湊碼衝突時，您的程式碼是否有 Bug。</span><span class="sxs-lookup"><span data-stu-id="a646b-118">Enable this MDA to test whether your code has bugs when hash codes collide.</span></span> <span data-ttu-id="a646b-119">啟用時，此 MDA 會讓 <xref:System.Object.GetHashCode%2A> 方法傳回 0，因而導致所有雜湊碼衝突。</span><span class="sxs-lookup"><span data-stu-id="a646b-119">When enabled, this MDA causes the <xref:System.Object.GetHashCode%2A> method to return 0, resulting in all hash codes colliding.</span></span> <span data-ttu-id="a646b-120">啟用此 MDA 對程式的唯一影響，在於您程式的執行速度會變慢。</span><span class="sxs-lookup"><span data-stu-id="a646b-120">The only effect enabling this MDA should have on your program is that your program runs slower.</span></span>  
  
 <span data-ttu-id="a646b-121">如果演算法是用來計算索引鍵變更的雜湊碼，則 <xref:System.Collections.Hashtable> 中的列舉順序可能會從執行階段的某個版本變更為另一個版本。</span><span class="sxs-lookup"><span data-stu-id="a646b-121">The order of enumeration from a <xref:System.Collections.Hashtable> may change from one version of the runtime to another if the algorithm used to compute the hash codes for the key change.</span></span> <span data-ttu-id="a646b-122">若要測試程式是否依存於索引鍵或值列舉順序，您可以啟用這個 MDA。</span><span class="sxs-lookup"><span data-stu-id="a646b-122">To test whether your program has taken a dependency on the order of enumeration of keys or values out of a hash table, you can enable this MDA.</span></span>  
  
## <a name="resolution"></a><span data-ttu-id="a646b-123">解決方案</span><span class="sxs-lookup"><span data-stu-id="a646b-123">Resolution</span></span>  
 <span data-ttu-id="a646b-124">永遠不要使用雜湊碼來取代物件身分識別。</span><span class="sxs-lookup"><span data-stu-id="a646b-124">Never use hash codes as a substitute for object identity.</span></span> <span data-ttu-id="a646b-125">實作 <xref:System.Object.Equals%2A?displayProperty=nameWithType> 方法的覆寫，不比較雜湊碼。</span><span class="sxs-lookup"><span data-stu-id="a646b-125">Implement the override of the <xref:System.Object.Equals%2A?displayProperty=nameWithType> method to not compare hash codes.</span></span>  
  
 <span data-ttu-id="a646b-126">請不要建立與雜湊表中之索引鍵或值列舉順序的相依性。</span><span class="sxs-lookup"><span data-stu-id="a646b-126">Do not create dependencies on the order of enumerations of keys or values in hash tables.</span></span>  
  
## <a name="effect-on-the-runtime"></a><span data-ttu-id="a646b-127">對執行階段的影響</span><span class="sxs-lookup"><span data-stu-id="a646b-127">Effect on the Runtime</span></span>  
 <span data-ttu-id="a646b-128">啟用此 MDA 時，應用程式的執行速度會更慢。</span><span class="sxs-lookup"><span data-stu-id="a646b-128">Applications run more slowly when this MDA is enabled.</span></span> <span data-ttu-id="a646b-129">此 MDA 只會採用已傳回的雜湊碼，並改成在除以模數時傳回餘數。</span><span class="sxs-lookup"><span data-stu-id="a646b-129">This MDA simply takes the hash code that would have been returned and instead returns the remainder when divided by a modulus.</span></span>  
  
## <a name="output"></a><span data-ttu-id="a646b-130">輸出</span><span class="sxs-lookup"><span data-stu-id="a646b-130">Output</span></span>  
 <span data-ttu-id="a646b-131">沒有此 MDA 的輸出。</span><span class="sxs-lookup"><span data-stu-id="a646b-131">There is no output for this MDA.</span></span>  
  
## <a name="configuration"></a><span data-ttu-id="a646b-132">設定</span><span class="sxs-lookup"><span data-stu-id="a646b-132">Configuration</span></span>  
 <span data-ttu-id="a646b-133">`modulus` 屬性指定雜湊碼上所使用的模數。</span><span class="sxs-lookup"><span data-stu-id="a646b-133">The `modulus` attribute specifies the modulus used on the hash code.</span></span> <span data-ttu-id="a646b-134">預設值為 1。</span><span class="sxs-lookup"><span data-stu-id="a646b-134">The default value is 1.</span></span>  
  
```xml  
<mdaConfig>  
  <assistants>  
    <moduloObjectHashcode modulus="1" />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a><span data-ttu-id="a646b-135">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a646b-135">See also</span></span>

- <xref:System.Object.GetHashCode%2A?displayProperty=nameWithType>
- <xref:System.Object.Equals%2A?displayProperty=nameWithType>
- [<span data-ttu-id="a646b-136">使用 Managed 偵錯助理診斷錯誤</span><span class="sxs-lookup"><span data-stu-id="a646b-136">Diagnosing Errors with Managed Debugging Assistants</span></span>](diagnosing-errors-with-managed-debugging-assistants.md)
