---
title: 作法：在日期與時間值中顯示毫秒
description: 在本文中，您將瞭解如何在 .NET 中的格式化日期和時間字串中包含日期和時間的毫秒元件。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DateTime.ToString method
- displaying date and time data
- time [.NET], milliseconds
- dates [.NET], milliseconds
- milliseconds [.NET]
ms.assetid: ae1a0610-90b9-4877-8eb6-4e30bc5e00cf
ms.openlocfilehash: 722334c324f663ba46a3c861885d4221fc566b8d
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95681258"
---
# <a name="how-to-display-milliseconds-in-date-and-time-values"></a>作法：在日期與時間值中顯示毫秒

預設的日期和時間格式化方法 (例如 <xref:System.DateTime.ToString?displayProperty=nameWithType>) 包括時間值的小時、分鐘和秒，但不包括它的毫秒元件。 本主題說明如何將日期和時間的毫秒部分加入格式化的日期和時間字串。  
  
### <a name="to-display-the-millisecond-component-of-a-datetime-value"></a>顯示 DateTime 值的毫秒部分  
  
1. 如果您要處理日期的字串表示法，請使用靜態 <xref:System.DateTime> 或 <xref:System.DateTimeOffset> 方法，將其轉換成 <xref:System.DateTime.Parse%28System.String%29?displayProperty=nameWithType> 或 <xref:System.DateTimeOffset.Parse%28System.String%29?displayProperty=nameWithType> 值。  
  
2. 若要擷取時間毫秒元件的字串表示，請呼叫日期和時間值的 <xref:System.DateTime.ToString%28System.String%29?displayProperty=nameWithType> 或 <xref:System.DateTimeOffset.ToString%2A> 方法，並單獨傳遞 `fff` 或 `FFF` 自訂格式模式，或是連同其他自訂格式規範作為 `format` 參數一併傳遞。  
  
## <a name="example"></a>範例  

 此範例會對主控台單獨顯示 <xref:System.DateTime> 和 <xref:System.DateTimeOffset> 值的毫秒元件，以及包含在較長的日期和時間字串中一併顯示。  
  
 [!code-csharp[Formatting.HowTo.Millisecond#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.Millisecond/cs/Millisecond.cs#1)]
 [!code-vb[Formatting.HowTo.Millisecond#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.Millisecond/vb/Millisecond.vb#1)]  
  
 `fff` 格式模式會包含毫秒值尾端的任何零。 `FFF` 格式模式則會加以隱藏。 下列範例會說明其間的差異。  
  
 [!code-csharp[Formatting.HowTo.Millisecond#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.Millisecond/cs/Millisecond.cs#2)]
 [!code-vb[Formatting.HowTo.Millisecond#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.Millisecond/vb/Millisecond.vb#2)]  
  
 定義包含日期和時間毫秒部分之完整自訂格式規範的問題在於，它會定義硬式編碼格式，而該格式可能不會對應至應用程式目前文化特性中時間項目的排列。 建議改為擷取目前文化特性之 <xref:System.Globalization.DateTimeFormatInfo> 物件所定義的其中一個日期和時間顯示模式，然後修改該模式以加入毫秒。 此範例也會說明這個方法。 它會從 <xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern%2A?displayProperty=nameWithType> 屬性擷取目前文化特性的完整日期和時間模式，接著在其秒模式之後插入自訂模式 `.ffff`。 請注意，此範例使用規則運算式，以單一方法呼叫來執行這項操作。  
  
 除了毫秒之外，您也可以使用自訂格式規範顯示秒的其他小數部分。 例如，`f` 或 `F` 自訂格式規範會顯示十分之一秒，`ff` 或 `FF` 自訂格式規範會顯示百分之一秒，而 `ffff` 或 `FFFF` 自訂格式規範會顯示萬分之一秒。 毫秒的小數部分會在傳回的字串中被截斷，而不是四捨五入。 下列範例會使用這些格式規範。  
  
 [!code-csharp[Formatting.HowTo.Millisecond#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.Millisecond/cs/Millisecond.cs#3)]
 [!code-vb[Formatting.HowTo.Millisecond#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.Millisecond/vb/Millisecond.vb#3)]  
  
> [!NOTE]
> 您可以使用非常小的小數單位來顯示秒，例如萬分之一秒或十萬分之一秒。 不過，這些值可能沒有太大的意義。 日期和時間值的精確度會根據系統時鐘的解析度而定。 在 Windows NT 3.5 和更新版本以及 Windows Vista 作業系統上，時鐘的解析度大約是10-15 毫秒。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Globalization.DateTimeFormatInfo>
- [自訂日期和時間格式字串](custom-date-and-time-format-strings.md)
