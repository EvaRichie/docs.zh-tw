---
title: 無法從委派推斷型別引數
ms.date: 07/20/2015
f1_keywords:
- bc36564
- vbc36564
helpviewer_keywords:
- BC36564
ms.assetid: 21312807-e1cd-4ac1-ae1c-c28a9c25164d
ms.openlocfilehash: f29e92c8245e33c0418d9a387070b03f645c331e
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84362744"
---
# <a name="type-arguments-could-not-be-inferred-from-the-delegate"></a><span data-ttu-id="99071-102">無法從委派推斷型別引數</span><span class="sxs-lookup"><span data-stu-id="99071-102">Type arguments could not be inferred from the delegate</span></span>
<span data-ttu-id="99071-103">指派陳述式使用 `AddressOf` 將泛型程序的位址指派給委派，但未將任何類型引數提供給泛型程序。</span><span class="sxs-lookup"><span data-stu-id="99071-103">An assignment statement uses `AddressOf` to assign the address of a generic procedure to a delegate, but it does not supply any type arguments to the generic procedure.</span></span>  
  
 <span data-ttu-id="99071-104">通常，當您叫用泛型類型時，會針對泛型類型所定義的每個類型參數提供類型引數。</span><span class="sxs-lookup"><span data-stu-id="99071-104">Normally, when you invoke a generic type, you supply a type argument for each type parameter that the generic type defines.</span></span> <span data-ttu-id="99071-105">如果您未提供任何類型引數，編譯器會嘗試推斷要傳遞給類型參數的類型。</span><span class="sxs-lookup"><span data-stu-id="99071-105">If you do not supply any type arguments, the compiler attempts to infer the types to be passed to the type parameters.</span></span> <span data-ttu-id="99071-106">如果內容未提供足夠的資訊讓編譯器推斷類型，則會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="99071-106">If the context does not provide enough information for the compiler to infer the types, an error is generated.</span></span>  
  
 <span data-ttu-id="99071-107">**錯誤識別碼：** BC36564</span><span class="sxs-lookup"><span data-stu-id="99071-107">**Error ID:** BC36564</span></span>  
  
## <a name="to-correct-this-error"></a><span data-ttu-id="99071-108">更正這個錯誤</span><span class="sxs-lookup"><span data-stu-id="99071-108">To correct this error</span></span>  
  
- <span data-ttu-id="99071-109">在 `AddressOf` 運算式中指定泛型程序的類型引數。</span><span class="sxs-lookup"><span data-stu-id="99071-109">Specify the type arguments for the generic procedure in the `AddressOf` expression.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="99071-110">另請參閱</span><span class="sxs-lookup"><span data-stu-id="99071-110">See also</span></span>

- [<span data-ttu-id="99071-111">Generic Types in Visual Basic</span><span class="sxs-lookup"><span data-stu-id="99071-111">Generic Types in Visual Basic</span></span>](../../programming-guide/language-features/data-types/generic-types.md)
- [<span data-ttu-id="99071-112">AddressOf 運算子</span><span class="sxs-lookup"><span data-stu-id="99071-112">AddressOf Operator</span></span>](../operators/addressof-operator.md)
- [<span data-ttu-id="99071-113">Generic Procedures in Visual Basic</span><span class="sxs-lookup"><span data-stu-id="99071-113">Generic Procedures in Visual Basic</span></span>](../../programming-guide/language-features/data-types/generic-procedures.md)
- [<span data-ttu-id="99071-114">Type List</span><span class="sxs-lookup"><span data-stu-id="99071-114">Type List</span></span>](../statements/type-list.md)
- [<span data-ttu-id="99071-115">擴充方法</span><span class="sxs-lookup"><span data-stu-id="99071-115">Extension Methods</span></span>](../../programming-guide/language-features/procedures/extension-methods.md)
