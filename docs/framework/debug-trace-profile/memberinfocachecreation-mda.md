---
title: memberInfoCacheCreation MDA
description: 瞭解 .NET 中的 memberInfoCacheCreation managed 偵錯工具（MDA），這會在建立 MemberInfo 快取時啟動。
ms.date: 03/30/2017
helpviewer_keywords:
- member info cache creation
- MemberInfoCacheCreation MDA
- reflection, run-time errors
- MDAs (managed debugging assistants), cache
- cache [.NET Framework], reflection
- managed debugging assistants (MDAs), cache
- MemberInfo cache
ms.assetid: 5abdad23-1335-4744-8acb-934002c0b6fe
ms.openlocfilehash: c48be7ac8632b8072981be01e01997ee8c34b6b3
ms.sourcegitcommit: 0edbeb66d71b8df10fcb374cfca4d731b58ccdb2
ms.contentlocale: zh-TW
ms.lasthandoff: 07/07/2020
ms.locfileid: "86051138"
---
# <a name="memberinfocachecreation-mda"></a>memberInfoCacheCreation MDA
建立 <xref:System.Reflection.MemberInfo> 快取時，會啟用 `memberInfoCacheCreation` Managed 偵錯助理 (MDA)。 這明顯指出利用耗用大量資源之反映功能的程式。  
  
## <a name="symptoms"></a>徵狀  
 程式的工作集會增加，因為程式正在使用耗用大量資源的反映。  
  
## <a name="cause"></a>原因  
 包含 <xref:System.Reflection.MemberInfo> 物件的反映作業會耗用大量資源，因為它們必須讀取冷頁面中所儲存的中繼資料，而且一般會指出程式正在使用某種類型的晚期繫結案例。  
  
## <a name="resolution"></a>解決方案  
 您可以啟用此 MDA，然後在偵錯工具中執行程式碼，或在啟用 MDA 時使用偵錯工具附加，來判斷將在程式中使用反映的位置。 透過偵錯工具，您將取得堆疊追蹤以顯示 <xref:System.Reflection.MemberInfo> 快取建立位置，並且您可以在該處判斷程式將使用反映的位置。  
  
 解決方式取決於程式碼目標。 此 MDA 會提醒您程式具有晚期繫結案例。 您可能想要決定是否可以替代早期繫結案例，或考慮晚期繫結案例的效能。  
  
## <a name="effect-on-the-runtime"></a>對執行階段的影響  
 會針對每個建立的 <xref:System.Reflection.MemberInfo> 快取啟用此 MDA。 效能影響微不足道。  
  
## <a name="output"></a>輸出  
 MDA 會輸出訊息，指出已建立 <xref:System.Reflection.MemberInfo> 快取。 使用偵錯工具取得堆疊追蹤，以顯示將在程式中使用反映的位置。  
  
## <a name="configuration"></a>組態  
  
```xml  
<mdaConfig>  
  <assistants>  
    <memberInfoCacheCreation/>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a>範例  
 此範例程式碼將會啟用 `memberInfoCacheCreation` MDA。  
  
```csharp
using System;  
  
public class Exe  
{  
    public static void Main()  
    {  
        typeof(object).GetMethods();  
    }  
}  
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Reflection.MemberInfo>
- [使用 Managed 偵錯助理診斷錯誤](diagnosing-errors-with-managed-debugging-assistants.md)
