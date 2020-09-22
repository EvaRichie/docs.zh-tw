---
title: "'System.Nullable(Of T)' 的方法不可以當做 'AddressOf' 運算子的運算元使用。"
ms.date: 07/20/2015
f1_keywords:
- vbc32126
- bc32126
helpviewer_keywords:
- BC32126
ms.assetid: 2325668b-e2ad-40ee-a1ec-30450236c20d
ms.openlocfilehash: 421766918c03c2378bbf906f85c5855f44ffbdea
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90873744"
---
# <a name="methods-of-systemnullableof-t-cannot-be-used-as-operands-of-the-addressof-operator"></a><span data-ttu-id="1f68c-102">'System.Nullable(Of T)' 的方法不可以當做 'AddressOf' 運算子的運算元使用。</span><span class="sxs-lookup"><span data-stu-id="1f68c-102">Methods of 'System.Nullable(Of T)' cannot be used as operands of the 'AddressOf' operator</span></span>

<span data-ttu-id="1f68c-103">語句使用運算子搭配 `AddressOf` 代表結構程式的運算元 <xref:System.Nullable%601> 。</span><span class="sxs-lookup"><span data-stu-id="1f68c-103">A statement uses the `AddressOf` operator with an operand that represents a procedure of the <xref:System.Nullable%601> structure.</span></span>  
  
 <span data-ttu-id="1f68c-104">**錯誤識別碼：** BC32126</span><span class="sxs-lookup"><span data-stu-id="1f68c-104">**Error ID:** BC32126</span></span>  
  
## <a name="to-correct-this-error"></a><span data-ttu-id="1f68c-105">更正這個錯誤</span><span class="sxs-lookup"><span data-stu-id="1f68c-105">To correct this error</span></span>  
  
- <span data-ttu-id="1f68c-106">`AddressOf`以不是成員的運算元取代子句中的程式名稱 <xref:System.Nullable%601> 。</span><span class="sxs-lookup"><span data-stu-id="1f68c-106">Replace the procedure name in the `AddressOf` clause with an operand that is not a member of <xref:System.Nullable%601>.</span></span>  
  
- <span data-ttu-id="1f68c-107">撰寫類別，包裝 <xref:System.Nullable%601> 您要使用的方法。</span><span class="sxs-lookup"><span data-stu-id="1f68c-107">Write a class that wraps the method of <xref:System.Nullable%601> that you want to use.</span></span> <span data-ttu-id="1f68c-108">在下列範例中， `NullableWrapper` 類別會定義名為的新方法 `GetValueOrDefault` 。</span><span class="sxs-lookup"><span data-stu-id="1f68c-108">In the following example, the `NullableWrapper` class defines a new method named `GetValueOrDefault`.</span></span> <span data-ttu-id="1f68c-109">因為這個新的方法不是的成員 <xref:System.Nullable%601> ，所以可以套用至可 `nullInstance` 為 null 型別的實例，以形成的引數 `AddressOf` 。</span><span class="sxs-lookup"><span data-stu-id="1f68c-109">Because this new method is not a member of <xref:System.Nullable%601>, it can be applied to `nullInstance`, an instance of a nullable type, to form an argument for `AddressOf`.</span></span>  
  
```vb  
Module Module1  
  
    Delegate Function Deleg() As Integer  
  
    Sub Main()  
        Dim nullInstance As New Nullable(Of Integer)(1)  
  
        Dim del As Deleg  
  
        ' GetValueOrDefault is a method of the Nullable generic  
        ' type. It cannot be used as an operand of AddressOf.  
        ' del = AddressOf nullInstance.GetValueOrDefault  
  
        ' The following line uses the GetValueOrDefault method  
        ' defined in the NullableWrapper class.  
        del = AddressOf (New NullableWrapper(  
            Of Integer)(nullInstance)).GetValueOrDefault  
  
        Console.WriteLine(del.Invoke())  
    End Sub  
  
    Class NullableWrapper(Of T As Structure)  
        Private m_Value As Nullable(Of T)  
  
        Sub New(ByVal Value As Nullable(Of T))  
            m_Value = Value  
        End Sub  
  
        Public Function GetValueOrDefault() As T  
            Return m_Value.Value  
        End Function  
    End Class  
End Module  
```  
  
## <a name="see-also"></a><span data-ttu-id="1f68c-110">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1f68c-110">See also</span></span>

- <xref:System.Nullable%601>
- [<span data-ttu-id="1f68c-111">AddressOf 運算子</span><span class="sxs-lookup"><span data-stu-id="1f68c-111">AddressOf Operator</span></span>](../operators/addressof-operator.md)
- [<span data-ttu-id="1f68c-112">可為 null 的實數值型別</span><span class="sxs-lookup"><span data-stu-id="1f68c-112">Nullable Value Types</span></span>](../../programming-guide/language-features/data-types/nullable-value-types.md)
- [<span data-ttu-id="1f68c-113">Generic Types in Visual Basic</span><span class="sxs-lookup"><span data-stu-id="1f68c-113">Generic Types in Visual Basic</span></span>](../../programming-guide/language-features/data-types/generic-types.md)
