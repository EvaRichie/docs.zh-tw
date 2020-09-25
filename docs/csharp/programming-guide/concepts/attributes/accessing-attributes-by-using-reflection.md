---
title: 使用反射存取屬性 (C#)
description: '使用反映來取得以 c # 中的自訂屬性定義的資訊，方法是使用 >getcustomattributes 方法。'
ms.date: 07/20/2015
ms.assetid: dce3a696-4ceb-489a-b5e4-322a83052f18
ms.openlocfilehash: 2ed4e844d1c98bcf265572f201bce6679fd642e9
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91202626"
---
# <a name="accessing-attributes-by-using-reflection-c"></a><span data-ttu-id="4500c-103">使用反射存取屬性 (C#)</span><span class="sxs-lookup"><span data-stu-id="4500c-103">Accessing Attributes by Using Reflection (C#)</span></span>

<span data-ttu-id="4500c-104">您可以定義自訂屬性並將它們放在原始程式碼的事實，對於擷取並處理該項資訊並沒有什麼幫助。</span><span class="sxs-lookup"><span data-stu-id="4500c-104">The fact that you can define custom attributes and place them in your source code would be of little value without some way of retrieving that information and acting on it.</span></span> <span data-ttu-id="4500c-105">使用反射，即可擷取已使用自訂屬性所定義的資訊。</span><span class="sxs-lookup"><span data-stu-id="4500c-105">By using reflection, you can retrieve the information that was defined with custom attributes.</span></span> <span data-ttu-id="4500c-106">重要方法是 `GetCustomAttributes`，這會傳回為來源程式碼屬性的執行階段對等項目的物件陣列。</span><span class="sxs-lookup"><span data-stu-id="4500c-106">The key method is `GetCustomAttributes`, which returns an array of objects that are the run-time equivalents of the source code attributes.</span></span> <span data-ttu-id="4500c-107">這個方法有數個多載的版本。</span><span class="sxs-lookup"><span data-stu-id="4500c-107">This method has several overloaded versions.</span></span> <span data-ttu-id="4500c-108">如需詳細資訊，請參閱<xref:System.Attribute>。</span><span class="sxs-lookup"><span data-stu-id="4500c-108">For more information, see <xref:System.Attribute>.</span></span>  
  
 <span data-ttu-id="4500c-109">屬性規格，例如︰</span><span class="sxs-lookup"><span data-stu-id="4500c-109">An attribute specification such as:</span></span>  
  
```csharp  
[Author("P. Ackerman", version = 1.1)]  
class SampleClass  
```  
  
 <span data-ttu-id="4500c-110">概念上相當於這個：</span><span class="sxs-lookup"><span data-stu-id="4500c-110">is conceptually equivalent to this:</span></span>  
  
```csharp  
Author anonymousAuthorObject = new Author("P. Ackerman");  
anonymousAuthorObject.version = 1.1;  
```  
  
 <span data-ttu-id="4500c-111">不過，程式碼會等到查詢 `SampleClass` 的屬性才會執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="4500c-111">However, the code is not executed until `SampleClass` is queried for attributes.</span></span> <span data-ttu-id="4500c-112">在 `SampleClass` 上呼叫 `GetCustomAttributes`，會如上建構和初始化 `Author` 物件。</span><span class="sxs-lookup"><span data-stu-id="4500c-112">Calling `GetCustomAttributes` on `SampleClass` causes an `Author` object to be constructed and initialized as above.</span></span> <span data-ttu-id="4500c-113">如果類別有其他屬性，則以類似的方式建構其他屬性物件。</span><span class="sxs-lookup"><span data-stu-id="4500c-113">If the class has other attributes, other attribute objects are constructed similarly.</span></span> <span data-ttu-id="4500c-114">`GetCustomAttributes` 接著會傳回 `Author` 物件以及陣列中的任何其他屬性物件。</span><span class="sxs-lookup"><span data-stu-id="4500c-114">`GetCustomAttributes` then returns the `Author` object and any other attribute objects in an array.</span></span> <span data-ttu-id="4500c-115">您接著可以逐一查看這個陣列、根據每個陣列項目的類型來決定已套用的屬性，以及從屬性物件擷取資訊。</span><span class="sxs-lookup"><span data-stu-id="4500c-115">You can then iterate over this array, determine what attributes were applied based on the type of each array element, and extract information from the attribute objects.</span></span>  
  
## <a name="example"></a><span data-ttu-id="4500c-116">範例</span><span class="sxs-lookup"><span data-stu-id="4500c-116">Example</span></span>  

 <span data-ttu-id="4500c-117">以下是完整範例。</span><span class="sxs-lookup"><span data-stu-id="4500c-117">Here is a complete example.</span></span> <span data-ttu-id="4500c-118">定義、套用至數個實體並透過反射來擷取自訂屬性。</span><span class="sxs-lookup"><span data-stu-id="4500c-118">A custom attribute is defined, applied to several entities, and retrieved via reflection.</span></span>  
  
```csharp  
// Multiuse attribute.  
[System.AttributeUsage(System.AttributeTargets.Class |  
                       System.AttributeTargets.Struct,  
                       AllowMultiple = true)  // Multiuse attribute.  
]  
public class Author : System.Attribute  
{  
    string name;  
    public double version;  
  
    public Author(string name)  
    {  
        this.name = name;  
  
        // Default value.  
        version = 1.0;  
    }  
  
    public string GetName()  
    {  
        return name;  
    }  
}  
  
// Class with the Author attribute.  
[Author("P. Ackerman")]  
public class FirstClass  
{  
    // ...  
}  
  
// Class without the Author attribute.  
public class SecondClass  
{  
    // ...  
}  
  
// Class with multiple Author attributes.  
[Author("P. Ackerman"), Author("R. Koch", version = 2.0)]  
public class ThirdClass  
{  
    // ...  
}  
  
class TestAuthorAttribute  
{  
    static void Test()  
    {  
        PrintAuthorInfo(typeof(FirstClass));  
        PrintAuthorInfo(typeof(SecondClass));  
        PrintAuthorInfo(typeof(ThirdClass));  
    }  
  
    private static void PrintAuthorInfo(System.Type t)  
    {  
        System.Console.WriteLine("Author information for {0}", t);  
  
        // Using reflection.  
        System.Attribute[] attrs = System.Attribute.GetCustomAttributes(t);  // Reflection.  
  
        // Displaying output.  
        foreach (System.Attribute attr in attrs)  
        {  
            if (attr is Author)  
            {  
                Author a = (Author)attr;  
                System.Console.WriteLine("   {0}, version {1:f}", a.GetName(), a.version);  
            }  
        }  
    }  
}  
/* Output:  
    Author information for FirstClass  
       P. Ackerman, version 1.00  
    Author information for SecondClass  
    Author information for ThirdClass  
       R. Koch, version 2.00  
       P. Ackerman, version 1.00  
*/  
```  
  
## <a name="see-also"></a><span data-ttu-id="4500c-119">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4500c-119">See also</span></span>

- <xref:System.Reflection>
- <xref:System.Attribute>
- [<span data-ttu-id="4500c-120">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="4500c-120">C# Programming Guide</span></span>](../../index.md)
- [<span data-ttu-id="4500c-121">擷取儲存於屬性中的資訊</span><span class="sxs-lookup"><span data-stu-id="4500c-121">Retrieving Information Stored in Attributes</span></span>](../../../../standard/attributes/retrieving-information-stored-in-attributes.md)
- [<span data-ttu-id="4500c-122">反映 (C#)</span><span class="sxs-lookup"><span data-stu-id="4500c-122">Reflection (C#)</span></span>](../reflection.md)
- [<span data-ttu-id="4500c-123">屬性 (C#)</span><span class="sxs-lookup"><span data-stu-id="4500c-123">Attributes (C#)</span></span>](./index.md)
- [<span data-ttu-id="4500c-124">建立自訂屬性 (C#)</span><span class="sxs-lookup"><span data-stu-id="4500c-124">Creating Custom Attributes (C#)</span></span>](./creating-custom-attributes.md)
