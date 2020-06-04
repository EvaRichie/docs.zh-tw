---
title: 晚期繫結多載解析無法套用至 '<procedurename>'，因為進行存取的執行個體為介面類型
ms.date: 07/20/2015
f1_keywords:
- vbc30933
- bc30933
helpviewer_keywords:
- overload resolution [Visual Basic], with late-bound argument
- BC30933
ms.assetid: 8182eea0-dd34-4d6e-9ca0-41d8713e9dc4
ms.openlocfilehash: 4500a177c7a4729fe5131af1b007fd38e77afe07
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397333"
---
# <a name="latebound-overload-resolution-cannot-be-applied-to-procedurename-because-the-accessing-instance-is-an-interface-type"></a><span data-ttu-id="aebad-102">晚期繫結多載解析無法套用至 '\<procedurename>'，因為進行存取的執行個體為介面類型</span><span class="sxs-lookup"><span data-stu-id="aebad-102">Latebound overload resolution cannot be applied to '\<procedurename>' because the accessing instance is an interface type</span></span>

<span data-ttu-id="aebad-103">編譯器嘗試解析多載屬性或程式的參考，但參考失敗，因為引數是型別 `Object` ，而參考物件具有介面的資料型別。</span><span class="sxs-lookup"><span data-stu-id="aebad-103">The compiler is attempting to resolve a reference to an overloaded property or procedure, but the reference fails because an argument is of type `Object` and the referring object has the data type of an interface.</span></span> <span data-ttu-id="aebad-104">`Object`引數會強制編譯器將參考解析為晚期繫結。</span><span class="sxs-lookup"><span data-stu-id="aebad-104">The `Object` argument forces the compiler to resolve the reference as late-bound.</span></span>

<span data-ttu-id="aebad-105">在這些情況下，編譯器會透過執行類別（而不是透過基礎介面）來解析多載。</span><span class="sxs-lookup"><span data-stu-id="aebad-105">In these circumstances, the compiler resolves the overload through the implementing class instead of through the underlying interface.</span></span> <span data-ttu-id="aebad-106">如果類別重新命名其中一個多載版本，則編譯器不會將該版本視為多載，因為它的名稱不同。</span><span class="sxs-lookup"><span data-stu-id="aebad-106">If the class renames one of the overloaded versions, the compiler does not consider that version to be an overload because its name is different.</span></span> <span data-ttu-id="aebad-107">這會導致編譯器忽略重新命名的版本，因為它可能是解析參考的正確選擇。</span><span class="sxs-lookup"><span data-stu-id="aebad-107">This in turn causes the compiler to ignore the renamed version when it might have been the correct choice to resolve the reference.</span></span>

<span data-ttu-id="aebad-108">**錯誤識別碼：** BC30933</span><span class="sxs-lookup"><span data-stu-id="aebad-108">**Error ID:** BC30933</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="aebad-109">更正這個錯誤</span><span class="sxs-lookup"><span data-stu-id="aebad-109">To correct this error</span></span>

- <span data-ttu-id="aebad-110">使用 `CType` 將引數從轉換成您想要呼叫之多載的簽章所 `Object` 指定的類型。</span><span class="sxs-lookup"><span data-stu-id="aebad-110">Use `CType` to cast the argument from `Object` to the type specified by the signature of the overload you want to call.</span></span>

  <span data-ttu-id="aebad-111">請注意，它不會協助將參考物件轉換成基礎介面。</span><span class="sxs-lookup"><span data-stu-id="aebad-111">Note that it does not help to cast the referring object to the underlying interface.</span></span> <span data-ttu-id="aebad-112">您必須轉換引數，以避免發生這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="aebad-112">You must cast the argument to avoid this error.</span></span>

## <a name="example"></a><span data-ttu-id="aebad-113">範例</span><span class="sxs-lookup"><span data-stu-id="aebad-113">Example</span></span>

<span data-ttu-id="aebad-114">下列範例顯示呼叫 `Sub` 在編譯時期造成此錯誤的多載程式。</span><span class="sxs-lookup"><span data-stu-id="aebad-114">The following example shows a call to an overloaded `Sub` procedure that causes this error at compile time.</span></span>

```vb
Module m1
    Interface i1
        Sub s1(ByVal p1 As Integer)
        Sub s1(ByVal p1 As Double)
    End Interface
    Class c1
        Implements i1
        Public Overloads Sub s1(ByVal p1 As Integer) Implements i1.s1
        End Sub
        Public Overloads Sub s2(ByVal p1 As Double) Implements i1.s1
        End Sub
    End Class
    Sub Main()
        Dim refer As i1 = New c1
        Dim o1 As Object = 3.1415
        ' The following reference is INVALID and causes a compiler error.
        refer.s1(o1)
    End Sub
End Module
```

<span data-ttu-id="aebad-115">在上述範例中，如果編譯器允許以撰寫的呼叫 `s1` ，則會透過類別 `c1` 而不是介面來進行解析 `i1` 。</span><span class="sxs-lookup"><span data-stu-id="aebad-115">In the preceding example, if the compiler allowed the call to `s1` as written, the resolution would take place through the class `c1` instead of the interface `i1`.</span></span> <span data-ttu-id="aebad-116">這表示編譯器不會考慮 `s2` ，因為它的名稱在中是不同的 `c1` ，即使是由定義的正確選擇也是一樣 `i1` 。</span><span class="sxs-lookup"><span data-stu-id="aebad-116">This would mean that the compiler would not consider `s2` because its name is different in `c1`, even though it is the correct choice as defined by `i1`.</span></span>

<span data-ttu-id="aebad-117">您可以藉由將呼叫變更為下列任一行程式碼來更正錯誤：</span><span class="sxs-lookup"><span data-stu-id="aebad-117">You can correct the error by changing the call to either of the following lines of code:</span></span>

```vb
refer.s1(CType(o1, Integer))
refer.s1(CType(o1, Double))
```

<span data-ttu-id="aebad-118">上述程式碼的每一行都會明確地將 `Object` 變數轉換 `o1` 為多載所定義的其中一個參數類型。</span><span class="sxs-lookup"><span data-stu-id="aebad-118">Each of the preceding lines of code explicitly casts the `Object` variable `o1` to one of the parameter types defined for the overloads.</span></span>

## <a name="see-also"></a><span data-ttu-id="aebad-119">另請參閱</span><span class="sxs-lookup"><span data-stu-id="aebad-119">See also</span></span>

- [<span data-ttu-id="aebad-120">程序多載化</span><span class="sxs-lookup"><span data-stu-id="aebad-120">Procedure Overloading</span></span>](../../programming-guide/language-features/procedures/procedure-overloading.md)
- [<span data-ttu-id="aebad-121">多載解析</span><span class="sxs-lookup"><span data-stu-id="aebad-121">Overload Resolution</span></span>](../../programming-guide/language-features/procedures/overload-resolution.md)
- [<span data-ttu-id="aebad-122">CType Function</span><span class="sxs-lookup"><span data-stu-id="aebad-122">CType Function</span></span>](../functions/ctype-function.md)
