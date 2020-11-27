---
title: 存取自訂屬性
description: 存取 .NET 中的自訂屬性。 當屬性與程式專案相關聯之後，您就可以使用反映來查詢其存在和值。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- custom attributes, accessibility
- attributes [.NET Framework], accessing
- reflection, custom attributes
ms.assetid: 1d8e3398-00d8-47d5-a084-214f9859d3d7
ms.openlocfilehash: d441bad7d4af3a88c4ede507d1bce7bdd1ab3215
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96266814"
---
# <a name="accessing-custom-attributes"></a><span data-ttu-id="89cae-104">存取自訂屬性</span><span class="sxs-lookup"><span data-stu-id="89cae-104">Accessing Custom Attributes</span></span>

<span data-ttu-id="89cae-105">建立屬性與程式項目的關聯之後，就可以使用反映來查詢其存在狀況和值。</span><span class="sxs-lookup"><span data-stu-id="89cae-105">After attributes have been associated with program elements, reflection can be used to query their existence and values.</span></span> <span data-ttu-id="89cae-106">在 .NET Framework 1.0 和 1.1 版中，會檢查執行內容中的自訂屬性。</span><span class="sxs-lookup"><span data-stu-id="89cae-106">In the .NET Framework version 1.0 and 1.1, custom attributes are examined in the execution context.</span></span> <span data-ttu-id="89cae-107">.NET Framework 2.0 版提供新的載入內容，就是僅限反映的內容，這可以用來檢查無法載入來執行的程式碼。</span><span class="sxs-lookup"><span data-stu-id="89cae-107">The .NET Framework version 2.0 provides a new load context, the reflection-only context, which can be used to examine code that cannot be loaded for execution.</span></span>  
  
## <a name="the-reflection-only-context"></a><span data-ttu-id="89cae-108">僅限反映的內容</span><span class="sxs-lookup"><span data-stu-id="89cae-108">The Reflection-Only Context</span></span>  

 <span data-ttu-id="89cae-109">無法執行載入僅限反映內容的程式碼。</span><span class="sxs-lookup"><span data-stu-id="89cae-109">Code loaded into the reflection-only context cannot be executed.</span></span> <span data-ttu-id="89cae-110">這表示無法建立自訂屬性的執行個體，因為這將需要執行其建構函式。</span><span class="sxs-lookup"><span data-stu-id="89cae-110">This means that instances of custom attributes cannot be created, because that would require executing their constructors.</span></span> <span data-ttu-id="89cae-111">若要載入和檢查僅限反映內容中的自訂屬性，請使用 <xref:System.Reflection.CustomAttributeData> 類別。</span><span class="sxs-lookup"><span data-stu-id="89cae-111">To load and examine custom attributes in the reflection-only context, use the <xref:System.Reflection.CustomAttributeData> class.</span></span> <span data-ttu-id="89cae-112">您可以使用靜態 <xref:System.Reflection.CustomAttributeData.GetCustomAttributes%2A?displayProperty=nameWithType> 方法的適當多載，以取得此類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="89cae-112">You can obtain instances of this class by using the appropriate overload of the static <xref:System.Reflection.CustomAttributeData.GetCustomAttributes%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="89cae-113">請參閱[如何：將組件載入僅限反映的內容](how-to-load-assemblies-into-the-reflection-only-context.md)。</span><span class="sxs-lookup"><span data-stu-id="89cae-113">See [How to: Load Assemblies into the Reflection-Only Context](how-to-load-assemblies-into-the-reflection-only-context.md).</span></span>  
  
## <a name="the-execution-context"></a><span data-ttu-id="89cae-114">執行內容</span><span class="sxs-lookup"><span data-stu-id="89cae-114">The Execution Context</span></span>  

 <span data-ttu-id="89cae-115">查詢執行內容中屬性的主要反映方法是 <xref:System.Reflection.MemberInfo.GetCustomAttributes%2A?displayProperty=nameWithType> 和 <xref:System.Attribute.GetCustomAttributes%2A?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="89cae-115">The main reflection methods to query attributes in the execution context are <xref:System.Reflection.MemberInfo.GetCustomAttributes%2A?displayProperty=nameWithType> and <xref:System.Attribute.GetCustomAttributes%2A?displayProperty=nameWithType>.</span></span>  
  
 <span data-ttu-id="89cae-116">會檢查自訂屬性有關附加組件的存取性。</span><span class="sxs-lookup"><span data-stu-id="89cae-116">The accessibility of a custom attribute is checked with respect to the assembly in which it is attached.</span></span> <span data-ttu-id="89cae-117">這相當於檢查附加自訂屬性中組件內之類型的方法是否可以呼叫自訂屬性的建構函式。</span><span class="sxs-lookup"><span data-stu-id="89cae-117">This is equivalent to checking whether a method on a type in the assembly in which the custom attribute is attached can call the constructor of the custom attribute.</span></span>  
  
 <span data-ttu-id="89cae-118"><xref:System.Reflection.Assembly.GetCustomAttributes%28System.Boolean%29?displayProperty=nameWithType> 這類方法會檢查型別引數的可視性和存取性。</span><span class="sxs-lookup"><span data-stu-id="89cae-118">Methods such as <xref:System.Reflection.Assembly.GetCustomAttributes%28System.Boolean%29?displayProperty=nameWithType> check the visibility and accessibility of the type argument.</span></span> <span data-ttu-id="89cae-119">只有包含使用者定義型別之組件中的程式碼才能使用 **GetCustomAttributes** 擷取類型的自訂屬性。</span><span class="sxs-lookup"><span data-stu-id="89cae-119">Only code in the assembly that contains the user-defined type can retrieve a custom attribute of that type using **GetCustomAttributes**.</span></span>  
  
 <span data-ttu-id="89cae-120">下列 C# 範例是典型自訂屬性設計模式。</span><span class="sxs-lookup"><span data-stu-id="89cae-120">The following C# example is a typical custom attribute design pattern.</span></span> <span data-ttu-id="89cae-121">它會說明執行階段自訂屬性反映模型。</span><span class="sxs-lookup"><span data-stu-id="89cae-121">It illustrates the runtime custom attribute reflection model.</span></span>  
  
```csharp
System.DLL  
public class DescriptionAttribute : Attribute  
{  
}  
  
System.Web.DLL  
internal class MyDescriptionAttribute : DescriptionAttribute  
{  
}  
  
public class LocalizationExtenderProvider  
{  
    [MyDescriptionAttribute(...)]  
    public CultureInfo GetLanguage(...)  
    {  
    }  
}  
```  
  
 <span data-ttu-id="89cae-122">如果執行階段嘗試擷取附加至 **GetLanguage** 方法之公開自訂屬性類型 <xref:System.ComponentModel.DescriptionAttribute> 的自訂屬性，則會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="89cae-122">If the runtime is attempting to retrieve the custom attributes for the public custom attribute type <xref:System.ComponentModel.DescriptionAttribute> attached to the **GetLanguage** method, it performs the following actions:</span></span>  
  
1. <span data-ttu-id="89cae-123">執行階段會檢查 **Type.GetCustomAttributes** 的型別引數 **DescriptionAttribute** (鍵入 *type*) 是公用的，因此可見且可供存取。</span><span class="sxs-lookup"><span data-stu-id="89cae-123">The runtime checks that the type argument **DescriptionAttribute** to **Type.GetCustomAttributes**(Type *type*) is public, and therefore is visible and accessible.</span></span>  
  
2. <span data-ttu-id="89cae-124">執行階段會檢查衍生自 **DescriptionAttribute** 的使用者定義型別 **MyDescriptionAttribute** 是否可以在 **System.Web.DLL** 組件內顯示和存取，其中，它會附加至 **GetLanguage**() 方法。</span><span class="sxs-lookup"><span data-stu-id="89cae-124">The runtime checks that the user-defined type **MyDescriptionAttribute** that is derived from **DescriptionAttribute** is visible and accessible within the **System.Web.DLL** assembly, where it is attached to the method **GetLanguage**().</span></span>  
  
3. <span data-ttu-id="89cae-125">執行階段會檢查 **System.Web.DLL** 組件內 **MyDescriptionAttribute** 的建構函式可見且可供存取。</span><span class="sxs-lookup"><span data-stu-id="89cae-125">The runtime checks that the constructor of **MyDescriptionAttribute** is visible and accessible within the **System.Web.DLL** assembly.</span></span>  
  
4. <span data-ttu-id="89cae-126">執行階段會使用自訂屬性參數來呼叫 **MyDescriptionAttribute** 的建構函式，並將新物件傳回給呼叫者。</span><span class="sxs-lookup"><span data-stu-id="89cae-126">The runtime calls the constructor of **MyDescriptionAttribute** with the custom attribute parameters and returns the new object to the caller.</span></span>  
  
 <span data-ttu-id="89cae-127">自訂屬性反映模型可能會流失在其中定義使用者定義型別之組件外部的類型執行個體。</span><span class="sxs-lookup"><span data-stu-id="89cae-127">The custom attribute reflection model could leak instances of user-defined types outside the assembly in which the type is defined.</span></span> <span data-ttu-id="89cae-128">這與傳回使用者定義型別執行個體的執行階段系統程式庫成員沒有差異，例如 <xref:System.Type.GetMethods%2A?displayProperty=nameWithType> 傳回 **RuntimeMethodInfo** 物件的陣列。</span><span class="sxs-lookup"><span data-stu-id="89cae-128">This is no different from the members in the runtime system library that return instances of user-defined types, such as <xref:System.Type.GetMethods%2A?displayProperty=nameWithType> returning an array of **RuntimeMethodInfo** objects.</span></span> <span data-ttu-id="89cae-129">若要防止用戶端探索使用者定義自訂屬性類型的資訊，請將類型的成員定義為非公用。</span><span class="sxs-lookup"><span data-stu-id="89cae-129">To prevent a client from discovering information about a user-defined custom attribute type, define the type's members to be nonpublic.</span></span>  
  
 <span data-ttu-id="89cae-130">下列範例示範如何使用反映來存取自訂屬性的基本方式。</span><span class="sxs-lookup"><span data-stu-id="89cae-130">The following example demonstrates the basic way of using reflection to get access to custom attributes.</span></span>  
  
 [!code-cpp[CustomAttributeData#2](../../../samples/snippets/cpp/VS_Snippets_CLR/CustomAttributeData/CPP/source2.cpp#2)]
 [!code-csharp[CustomAttributeData#2](../../../samples/snippets/csharp/VS_Snippets_CLR/CustomAttributeData/CS/source2.cs#2)]
 [!code-vb[CustomAttributeData#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CustomAttributeData/VB/source2.vb#2)]  
  
## <a name="see-also"></a><span data-ttu-id="89cae-131">另請參閱</span><span class="sxs-lookup"><span data-stu-id="89cae-131">See also</span></span>

- <xref:System.Reflection.MemberInfo.GetCustomAttributes%2A?displayProperty=nameWithType>
- <xref:System.Attribute.GetCustomAttributes%2A?displayProperty=nameWithType>
- [<span data-ttu-id="89cae-132">檢視類型資訊</span><span class="sxs-lookup"><span data-stu-id="89cae-132">Viewing Type Information</span></span>](viewing-type-information.md)
- [<span data-ttu-id="89cae-133">反映的安全性考量</span><span class="sxs-lookup"><span data-stu-id="89cae-133">Security Considerations for Reflection</span></span>](security-considerations-for-reflection.md)
