---
title: 執行不區分文化特性的字串作業
ms.date: 08/22/2018
helpviewer_keywords:
- case mappings
- custom case mappings
- culture, custom sorting rules
- custom sorting rules
- culture-insensitive string operations, options for performing
- culture, custom case mappings
- culture-insensitive string operations, method overloads
ms.assetid: 579ef891-1f83-4c63-9ebd-2f40406b5b91
ms.openlocfilehash: 868f36a1025f0b121a8765edf50bb42679736240
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94829761"
---
# <a name="performing-culture-insensitive-string-operations"></a>執行不區分文化特性的字串作業

預設會執行區分文化特性的字串作業的大部分 .NET 方法都會提供方法多載，讓您可以藉由傳遞參數來明確指定要使用的文化特性 <xref:System.Globalization.CultureInfo> 。 這些多載可讓您消除大小寫對應和排序規則中的文化特性變化，保證您可以得到不區分文化特性的結果。  
  
 本節提供下列文章，以示範如何使用預設為區分文化特性的 .NET 方法，執行不區分文化特性的字串作業。  
  
## <a name="in-this-section"></a>本節內容  
 [執行不區分文化特性的字串比較](performing-culture-insensitive-string-comparisons.md)  
 描述如何使用 <xref:System.String.Compare%2A?displayProperty=nameWithType> 和 <xref:System.String.CompareTo%2A?displayProperty=nameWithType> 方法執行不區分文化特性的字串比較。  
  
 [執行不區分文化特性的大小寫變更](performing-culture-insensitive-case-changes.md)  
 描述如何使用 <xref:System.String.ToUpper%2A?displayProperty=nameWithType>、<xref:System.String.ToLower%2A?displayProperty=nameWithType>、<xref:System.Char.ToUpper%2A?displayProperty=nameWithType> 和 <xref:System.Char.ToLower%2A?displayProperty=nameWithType> 方法執行不區分文化特性的大小寫變更。  
  
 [在集合中執行不區分文化特性的字串作業](performing-culture-insensitive-string-operations-in-collections.md)  
 描述如何使用 <xref:System.Collections.CaseInsensitiveComparer>、<xref:System.Collections.CaseInsensitiveHashCodeProvider> 類別、<xref:System.Collections.SortedList>、<xref:System.Collections.ArrayList.Sort%2A?displayProperty=nameWithType> 和 <xref:System.Collections.Specialized.CollectionsUtil.CreateCaseInsensitiveHashtable%2A?displayProperty=nameWithType>，在集合中執行不區分文化特性的作業。  
  
 [在陣列中執行不區分文化特性的字串作業](performing-culture-insensitive-string-operations-in-arrays.md)  
 描述如何使用 <xref:System.Array.Sort%2A?displayProperty=nameWithType> 和 <xref:System.Array.BinarySearch%2A?displayProperty=nameWithType> 方法，在陣列中執行不區分文化特性的作業。  
  
## <a name="related-sections"></a>相關章節  
 [不區分文化特性的字串作業](culture-insensitive-string-operations.md)  
 描述為何您應該注意對字串執行作業時的文化特性，並提供指導方針來指出何時該執行區分文化特性的作業，何時該執行不區分文化特性的作業。

## <a name="see-also"></a>請參閱

- [排序權數資料表 (適用於 Windows 系統上的 .NET)](https://www.microsoft.com/download/details.aspx?id=10921)
- [預設 Unicode 定序元素資料表 (適用於 Linux 和 macOS 上的 .NET Core)](https://www.unicode.org/Public/UCA/latest/allkeys.txt)
