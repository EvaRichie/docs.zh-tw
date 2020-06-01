---
title: '如何使用反映查詢元件的中繼資料（LINQ）（c #）'
ms.date: 07/20/2015
ms.assetid: c4cdce49-b1c8-4420-b12a-9ff7e6671368
ms.openlocfilehash: 092cb386af0c3f2e2241c2c2ac8e50eab74cc43b
ms.sourcegitcommit: a241301495a84cc8c64fe972330d16edd619868b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/01/2020
ms.locfileid: "84241535"
---
# <a name="how-to-query-an-assemblys-metadata-with-reflection-linq-c"></a>如何使用反映查詢元件的中繼資料（LINQ）（c #）

.NET 反映 Api 可用來檢查 .NET 元件中的中繼資料，並建立該元件中的類型、類型成員、參數等等的集合。 因為這些集合支援泛型 <xref:System.Collections.Generic.IEnumerable%601> 介面，所以可以使用 LINQ 進行查詢。  
  
下列範例示範如何搭配使用 LINQ 與反射，來擷取符合所指定搜尋準則之方法的特定中繼資料。 在此情況下，查詢會尋找組件中所有方法的名稱，而這些方法會傳回陣列這類可列舉類型。  
  
## <a name="example"></a>範例  
  
```csharp  
using System;
using System.Linq;
using System.Reflection;  

class ReflectionHowTO  
{  
    static void Main()  
    {  
        Assembly assembly = Assembly.Load("System.Core, Version=3.5.0.0, Culture=neutral, PublicKeyToken= b77a5c561934e089");  
        var pubTypesQuery = from type in assembly.GetTypes()  
                    where type.IsPublic  
                        from method in type.GetMethods()  
                        where method.ReturnType.IsArray == true
                            || ( method.ReturnType.GetInterface(  
                                typeof(System.Collections.Generic.IEnumerable<>).FullName ) != null  
                            && method.ReturnType.FullName != "System.String" )  
                        group method.ToString() by type.ToString();  

        foreach (var groupOfMethods in pubTypesQuery)  
        {  
            Console.WriteLine("Type: {0}", groupOfMethods.Key);  
            foreach (var method in groupOfMethods)  
            {  
                Console.WriteLine("  {0}", method);  
            }  
        }  

        Console.WriteLine("Press any key to exit... ");  
        Console.ReadKey();  
    }  
}
```  

這個範例會使用 <xref:System.Reflection.Assembly.GetTypes%2A?displayProperty=nameWithType> 方法，以傳回所指定組件中的類型陣列。 會套用 [where](../../../language-reference/keywords/where-clause.md) 篩選，只傳回公用類型。 對於每一個公用類型，會使用從 <xref:System.Type.GetMethods%2A?displayProperty=nameWithType> 呼叫傳回的 <xref:System.Reflection.MethodInfo> 陣列來產生子查詢。 這些結果會進行篩選，僅傳回其傳回型別為陣列的方法，或為實作 <xref:System.Collections.Generic.IEnumerable%601> 之類型的方法。 最後，會使用類型名稱作為索引鍵來群組這些結果。  
  
## <a name="see-also"></a>另請參閱

- [LINQ to Objects (C#)](./linq-to-objects.md)
