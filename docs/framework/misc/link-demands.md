---
title: 連結要求
description: 閱讀連結要求，這會在即時 (JIT) 編譯期間造成安全性檢查，並只檢查程式碼的立即呼叫元件。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- security [.NET Framework], demands
- demanded permissions
- permissions [.NET Framework], demands
- granting permissions, demands
- code access security, demands
- user demands for permission
- caller security checks
- link demands
ms.assetid: a33fd5f9-2de9-4653-a4f0-d9df25082c4d
ms.openlocfilehash: cd89c4ef27abb92fba567a1f3b490cb9d78fdddd
ms.sourcegitcommit: 97ce5363efa88179dd76e09de0103a500ca9b659
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/13/2020
ms.locfileid: "86282051"
---
# <a name="link-demands"></a><span data-ttu-id="77f9b-103">連結要求</span><span class="sxs-lookup"><span data-stu-id="77f9b-103">Link Demands</span></span>
[!INCLUDE[net_security_note](../../../includes/net-security-note-md.md)]  
  
 <span data-ttu-id="77f9b-104">連結要求會在 Just-In-Time 編譯期間進行安全性檢查，並且只檢查程式碼組件的即時呼叫者。</span><span class="sxs-lookup"><span data-stu-id="77f9b-104">A link demand causes a security check during just-in-time compilation and checks only the immediate calling assembly of your code.</span></span> <span data-ttu-id="77f9b-105">當您的程式碼繫結至類型參考，包括函式指標參考和方法呼叫時，連結就會發生。</span><span class="sxs-lookup"><span data-stu-id="77f9b-105">Linking occurs when your code is bound to a type reference, including function pointer references and method calls.</span></span> <span data-ttu-id="77f9b-106">如果呼叫的組件並沒有足夠權限可連結到您的程式碼，則程式碼載入和執行時不會允許連結且會擲回執行階段例外狀況。</span><span class="sxs-lookup"><span data-stu-id="77f9b-106">If the calling assembly does not have sufficient permission to link to your code, the link is not allowed and a runtime exception is thrown when the code is loaded and run.</span></span> <span data-ttu-id="77f9b-107">連結要求可以在繼承自您的程式碼的類別中被覆寫。</span><span class="sxs-lookup"><span data-stu-id="77f9b-107">Link demands can be overridden in classes that inherit from your code.</span></span>  
  
 <span data-ttu-id="77f9b-108">請注意，對這種類型的需求不會執行完整堆疊查核行程，而且您的程式碼仍會受到引誘攻擊。</span><span class="sxs-lookup"><span data-stu-id="77f9b-108">Note that a full stack walk is not performed with this type of demand and that your code is still susceptible to luring attacks.</span></span> <span data-ttu-id="77f9b-109">例如，如果元件 A 中的方法受到連結要求的保護，則元件 B 中的直接呼叫端會根據元件 B 的許可權進行評估。 不過，如果連結要求使用元件 B 中的方法間接呼叫元件 A 中的方法，則不會評估元件 C 中的方法。連結要求只會指定立即呼叫元件中的直接呼叫端許可權，必須連結至您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="77f9b-109">For example, if a method in assembly A is protected by a link demand, a direct caller in assembly B is evaluated based on the permissions of Assembly B.  However, the link demand will not evaluate a method in assembly C if it indirectly calls the method in assembly A using the method in assembly B. The link demand specifies only the permissions direct callers in the immediate calling assembly must have to link to your code.</span></span> <span data-ttu-id="77f9b-110">它並未指定所有呼叫端必須擁有以便執行程式碼的權限。</span><span class="sxs-lookup"><span data-stu-id="77f9b-110">It does not specify the permissions all callers must have to run your code.</span></span>  
  
 <span data-ttu-id="77f9b-111"><xref:System.Security.CodeAccessPermission.Assert%2A>、<xref:System.Security.CodeAccessPermission.Deny%2A> 和 <xref:System.Security.CodeAccessPermission.PermitOnly%2A> 堆疊查核行程修飾詞不會影響連結要求的評估。</span><span class="sxs-lookup"><span data-stu-id="77f9b-111">The <xref:System.Security.CodeAccessPermission.Assert%2A>, <xref:System.Security.CodeAccessPermission.Deny%2A>, and <xref:System.Security.CodeAccessPermission.PermitOnly%2A> stack walk modifiers do not affect the evaluation of link demands.</span></span>  <span data-ttu-id="77f9b-112">由於連結要求不會執行堆疊查核行程，堆疊查核行程修飾詞不會影響連結要求。</span><span class="sxs-lookup"><span data-stu-id="77f9b-112">Because link demands do not perform a stack walk, the stack walk modifiers have no effect on link demands.</span></span>  
  
 <span data-ttu-id="77f9b-113">如果受連結要求保護的方法是透過[反映](../reflection-and-codedom/reflection.md)來存取，則連結要求會檢查透過反映存取之程式碼的立即呼叫端。</span><span class="sxs-lookup"><span data-stu-id="77f9b-113">If a method protected by a link demand is accessed through [Reflection](../reflection-and-codedom/reflection.md), then a link demand checks the immediate caller of the code accessed through reflection.</span></span> <span data-ttu-id="77f9b-114">使用反映來執行的方法探索和方法引動過程都是如此。</span><span class="sxs-lookup"><span data-stu-id="77f9b-114">This is true both for method discovery and for method invocation performed using reflection.</span></span> <span data-ttu-id="77f9b-115">例如，假設程式碼使用反映來 <xref:System.Reflection.MethodInfo> 傳回物件，代表受連結要求保護的方法，然後將該**MethodInfo**物件傳遞給使用物件來叫用原始方法的其他程式碼。</span><span class="sxs-lookup"><span data-stu-id="77f9b-115">For example, suppose code uses reflection to return a <xref:System.Reflection.MethodInfo> object representing a method protected by a link demand and then passes that **MethodInfo** object to some other code that uses the object to invoke the original method.</span></span> <span data-ttu-id="77f9b-116">在此情況下，連結要求檢查會發生兩次：一次是針對傳回**MethodInfo**物件的程式碼，另一次是針對叫用它的程式碼。</span><span class="sxs-lookup"><span data-stu-id="77f9b-116">In this case the link demand check occurs twice: once for the code that returns the **MethodInfo** object and once for the code that invokes it.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="77f9b-117">在靜態類別建構函式上執行的連結要求不會保護建構函式，因為靜態建構函式由系統所呼叫，不在應用程式的程式碼執行路徑中。</span><span class="sxs-lookup"><span data-stu-id="77f9b-117">A link demand performed on a static class constructor does not protect the constructor because static constructors are called by the system, outside the application's code execution path.</span></span> <span data-ttu-id="77f9b-118">如此一來，當連結需求套用至整個類別時，它無法保護對靜態建構函式的存取權，不過它確實會保護類別的其餘部分。</span><span class="sxs-lookup"><span data-stu-id="77f9b-118">As a result, when a link demand is applied to an entire class, it cannot protect access to a static constructor, although it does protect the rest of the class.</span></span>  
  
 <span data-ttu-id="77f9b-119">下列程式碼片段以宣告方式指定連結至 `ReadData` 方法的任何程式碼都必須具有 `CustomPermission` 權限。</span><span class="sxs-lookup"><span data-stu-id="77f9b-119">The following code fragment declaratively specifies that any code linking to the `ReadData` method must have the `CustomPermission` permission.</span></span> <span data-ttu-id="77f9b-120">此權限是假設的自訂權限，並不存在於 .NET Framework 中。</span><span class="sxs-lookup"><span data-stu-id="77f9b-120">This permission is a hypothetical custom permission and does not exist in the .NET Framework.</span></span> <span data-ttu-id="77f9b-121">要求是藉由將**SecurityAction**旗標傳遞至來進行 `CustomPermissionAttribute` 。</span><span class="sxs-lookup"><span data-stu-id="77f9b-121">The demand is made by passing a **SecurityAction.LinkDemand** flag to the `CustomPermissionAttribute`.</span></span>  
  
```vb  
<CustomPermissionAttribute(SecurityAction.LinkDemand)> _  
Public Shared Function ReadData() As String  
    ' Access a custom resource.  
End Function
```  
  
```csharp  
[CustomPermissionAttribute(SecurityAction.LinkDemand)]  
public static string ReadData()  
{  
    // Access a custom resource.  
}  
```  
  
## <a name="see-also"></a><span data-ttu-id="77f9b-122">請參閱</span><span class="sxs-lookup"><span data-stu-id="77f9b-122">See also</span></span>

- [<span data-ttu-id="77f9b-123">屬性</span><span class="sxs-lookup"><span data-stu-id="77f9b-123">Attributes</span></span>](../../standard/attributes/index.md)
- [<span data-ttu-id="77f9b-124">代碼啟用安全性</span><span class="sxs-lookup"><span data-stu-id="77f9b-124">Code Access Security</span></span>](code-access-security.md)
