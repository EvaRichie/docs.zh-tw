---
title: 作法：執行物件的延遲初始設定
description: 瞭解如何使用 system.string 類別來執行物件的延遲初始化 <T> 。 延遲初始化表示不需要物件就會建立。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- lazy initialization in .NET, how to perform
ms.assetid: 8cd68620-dcc3-4f20-8835-c728a6820e71
ms.openlocfilehash: 3de0d8ea8266931c2bcda5c59c1fef97602673d5
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96278124"
---
# <a name="how-to-perform-lazy-initialization-of-objects"></a><span data-ttu-id="e1e51-104">作法：執行物件的延遲初始設定</span><span class="sxs-lookup"><span data-stu-id="e1e51-104">How to: Perform Lazy Initialization of Objects</span></span>

<span data-ttu-id="e1e51-105"><xref:System.Lazy%601?displayProperty=nameWithType> 類別可簡化執行物件延遲初始化和具現化的工作。</span><span class="sxs-lookup"><span data-stu-id="e1e51-105">The <xref:System.Lazy%601?displayProperty=nameWithType> class simplifies the work of performing lazy initialization and instantiation of objects.</span></span> <span data-ttu-id="e1e51-106">以延遲方式初始化物件時，您可以避免必須在永不需要這些物件時完全建立它們，也可以延後其初始化作業，直到第一次存取這些物件為止。</span><span class="sxs-lookup"><span data-stu-id="e1e51-106">By initializing objects in a lazy manner, you can avoid having to create them at all if they are never needed, or you can postpone their initialization until they are first accessed.</span></span> <span data-ttu-id="e1e51-107">如需詳細資訊，請參閱[延遲初始化](lazy-initialization.md)。</span><span class="sxs-lookup"><span data-stu-id="e1e51-107">For more information, see [Lazy Initialization](lazy-initialization.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="e1e51-108">範例</span><span class="sxs-lookup"><span data-stu-id="e1e51-108">Example</span></span>  

 <span data-ttu-id="e1e51-109">下列範例示範如何使用 <xref:System.Lazy%601> 來初始化值。</span><span class="sxs-lookup"><span data-stu-id="e1e51-109">The following example shows how to initialize a value with <xref:System.Lazy%601>.</span></span> <span data-ttu-id="e1e51-110">假設可能不需要延遲變數，這取決於某個將 `someCondition` 變數設定為 true 或 false 的其他程式碼。</span><span class="sxs-lookup"><span data-stu-id="e1e51-110">Assume that the lazy variable might not be needed, depending on some other code that sets the `someCondition` variable to true or false.</span></span>  
  
```vb  
Dim someCondition As Boolean = False  
  
Sub Main()  
    'Initializing a value with a big computation, computed in parallel  
    Dim _data As Lazy(Of Integer) = New Lazy(Of Integer)(Function()  
                                                             Dim result =  
                                                                 ParallelEnumerable.Range(0, 1000).  
                                                                 Aggregate(Function(x, y)  
                                                                               Return x + y  
                                                                           End Function)  
                                                             Return result  
                                                         End Function)  
  
    '  do work that may or may not set someCondition to True  
    ' ...  
    '  Initialize the data only if needed  
    If someCondition = True Then  
  
        If (_data.Value > 100) Then  
  
            Console.WriteLine("Good data")  
        End If  
    End If  
End Sub  
```  
  
```csharp  
  static bool someCondition = false;
  //Initializing a value with a big computation, computed in parallel  
  Lazy<int> _data = new Lazy<int>(delegate  
  {  
      return ParallelEnumerable.Range(0, 1000).  
          Select(i => Compute(i)).Aggregate((x,y) => x + y);  
  }, LazyExecutionMode.EnsureSingleThreadSafeExecution);  
  
  // Do some work that may or may not set someCondition to true.  
  //  ...  
  // Initialize the data only if necessary  
  if (someCondition)  
  {  
    if (_data.Value > 100)  
      {  
          Console.WriteLine("Good data");  
      }  
  }  
```  
  
## <a name="example"></a><span data-ttu-id="e1e51-111">範例</span><span class="sxs-lookup"><span data-stu-id="e1e51-111">Example</span></span>  

 <span data-ttu-id="e1e51-112">下列範例示範如何使用 <xref:System.Threading.ThreadLocal%601?displayProperty=nameWithType> 類別來初始化類型，只有在目前執行緒上的目前物件執行個體中才能看見該類型。</span><span class="sxs-lookup"><span data-stu-id="e1e51-112">The following example shows how to use the <xref:System.Threading.ThreadLocal%601?displayProperty=nameWithType> class to initialize a type that is visible only to the current object instance on the current thread.</span></span>  
  
 [!code-csharp[CDS#13](../../../samples/snippets/csharp/VS_Snippets_Misc/cds/cs/cds2.cs#13)]
 [!code-vb[CDS#13](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds/vb/lazyhowto.vb#13)]  
  
## <a name="see-also"></a><span data-ttu-id="e1e51-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e1e51-113">See also</span></span>

- <xref:System.Threading.LazyInitializer?displayProperty=nameWithType>
- [<span data-ttu-id="e1e51-114">延遲初始設定</span><span class="sxs-lookup"><span data-stu-id="e1e51-114">Lazy Initialization</span></span>](lazy-initialization.md)
