---
title: 使用日期和時間執行算術運算
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- times [.NET Framework], arithmetic operations
- dates [.NET Framework], arithmetic operations
- time zones [.NET Framework], arithmetic operations
- arithmetic operations [.NET Framework], dates and times
- dates [.NET Framework], comparing
- DateTime structure, arithmetic operations
- DateTimeOffset structure, arithmetic operations
ms.assetid: 87c7ddf2-f15e-48af-8602-b3642237e6d0
ms.openlocfilehash: c212397f99bd09195f298d7d704c879705b14f02
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84281540"
---
# <a name="performing-arithmetic-operations-with-dates-and-times"></a>使用日期和時間執行算術運算

雖然 <xref:System.DateTime> 和 <xref:System.DateTimeOffset> 結構都會提供對其值執行算數運算的成員，但算數運算的結果會非常不同。 本主題將探討這些差異、將它們與日期和時間資料中的時區感知程度產生關聯，並討論如何使用日期和時間資料執行全時區感知作業。

## <a name="comparisons-and-arithmetic-operations-with-datetime-values"></a>使用 DateTime 值的比較和算數運算

屬性可讓您將 <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> <xref:System.DateTimeKind> 值指派給日期和時間，以指出它是否代表當地時間、國際標準時間（UTC）或未指定時區的時間。 不過，比較或在值上執行日期和時間運算時，會忽略這個有限的時區資訊 <xref:System.DateTimeKind> 。 下列範例會比較目前當地時間與目前 UTC 時間，以說明這點。

[!code-csharp[System.DateTimeOffset.Conceptual#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual2.cs#2)]
[!code-vb[System.DateTimeOffset.Conceptual#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual2.vb#2)]

<xref:System.DateTime.CompareTo%28System.DateTime%29> 方法會報告本地時間早於 (或晚於) UTC 時間，接著減法運算會指出 UTC 與本地時間之間的時差，以美國太平洋標準時間時區系統來說相差七個小時。 但因為這兩個值提供單一時間點的不同標記法，所以在此情況下，時間間隔會完全由當地時區與 UTC 的位移所組成。

更常見的是， <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> 屬性不會影響 <xref:System.DateTime.Kind> 比較和算術方法所傳回的結果（如果兩個相同時間點的比較指出），雖然它可能會影響這些結果的轉譯。 例如：

- 在兩個日期和時間值上執行的任何算數運算結果，其 <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> 屬性都相等 <xref:System.DateTimeKind> 反映兩個值之間的實際時間間隔。 同樣地，兩個這類日期和時間值的比較會精確地反映時間的關聯性。

- 在兩個日期和時間值上執行的任何算術或比較運算結果，其 <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> 屬性等於 <xref:System.DateTimeKind> 或在具有不同屬性值的兩個日期和時間值上，會 <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> 反映兩個值之間的時鐘時間差異。

- 當地日期和時間值的算術或比較作業不會考慮特定值是不明確或無效，也不會考慮當地時區與日光節約時間之轉換所產生的任何調整規則的影響。

- 任何比較或計算 UTC 與當地時間之差異的作業，都會在結果中包含等於當地時區與 UTC 之位移的時間間隔。

- 任何比較或計算未指定時間與 UTC 或當地時間之差異的作業，都會反映簡單時鐘時間。 不考慮時區差異，而且結果不會反映如何套用時區調整規則。

- 任何比較或計算兩個未指定時間之差異的作業都可能包含未知間隔，而未知間隔反映兩個不同時區的時間差異。

在許多情況下，時區差異不會影響日期和時間計算（如需其中某些部分的討論，請參閱[在 DateTime、DateTimeOffset、TimeSpan 和 TimeZoneInfo 之間進行選擇](choosing-between-datetime.md)），或日期和時間資料的內容定義比較或算數運算意義的情況。

## <a name="comparisons-and-arithmetic-operations-with-datetimeoffset-values"></a>使用 DateTimeOffset 值的比較和算數運算

<xref:System.DateTimeOffset>值不僅包含日期和時間，也包括明確定義相對於 UTC 之日期和時間的位移。 這可讓您定義與值稍有不同的相等性 <xref:System.DateTimeOffset> 。 <xref:System.DateTime>如果值具有相同的日期和時間值，則它們會相等，而 <xref:System.DateTimeOffset> 如果兩者都參考相同的時間點，則值會相等。 這可讓您 <xref:System.DateTimeOffset> 在比較中使用，以及在判斷兩個日期和時間之間間隔的大部分算數運算中，以更精確且更不需要解讀。 下列範例（等同于先前的範例，也就是 <xref:System.DateTimeOffset> 比較本機和 UTC <xref:System.DateTimeOffset> 值）會說明行為的差異。

[!code-csharp[System.DateTimeOffset.Conceptual#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual3.cs#3)]
[!code-vb[System.DateTimeOffset.Conceptual#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual3.vb#3)]

在此範例中， <xref:System.DateTimeOffset.CompareTo%2A> 方法會指出目前的當地時間和目前的 UTC 時間相等，而值的減法 <xref:System.DateTimeOffset.CompareTo(System.DateTimeOffset)> 表示兩個時間之間的差異是 <xref:System.TimeSpan.Zero?displayProperty=nameWithType> 。

<xref:System.DateTimeOffset>在日期和時間運算中使用值的主要限制是，雖然 <xref:System.DateTimeOffset> 值有一些時區感知，但它們並不是完整的時區感知。 雖然 <xref:System.DateTimeOffset> 值的位移會在第一次為變數指派值時，反映時區與 UTC 的位移 <xref:System.DateTimeOffset> ，但之後會變成與時區的解除關聯。 因為它不再與可識別時間直接關聯，所以加上和減去日期和時間間隔不會視為時區的調整規則。

為了說明，美國中部標準時區轉換為日光節約時間會在上午2:00 執行。 凌晨 2:00 加上兩個半小時。 這表示，中央標準時間 2008 年 3 月 9 日上午 1:30 加上兩個半小時的間隔， 就會產生 2008 年 3 月 9 日凌晨 5:00 的 凌晨 2:00 加上兩個半小時。 不過，如下列範例所示，加上兩個半小時後為 2008 年 3 月 9 日 凌晨 2:00 加上兩個半小時。 請注意，這項作業的結果代表正確的時間點，但不是我們感興趣的時區時間（也就是沒有預期的時區時差）。

[!code-csharp[System.DateTimeOffset.Conceptual#4](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual4.cs#4)]
[!code-vb[System.DateTimeOffset.Conceptual#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual4.vb#4)]

## <a name="arithmetic-operations-with-times-in-time-zones"></a>使用時區時間的算數運算

<xref:System.TimeZoneInfo>類別包含一些轉換方法，會在將時間從某個時區轉換為另一個時區時，自動套用調整。 這些選項包括：

- <xref:System.TimeZoneInfo.ConvertTime%2A>和 <xref:System.TimeZoneInfo.ConvertTimeBySystemTimeZoneId%2A> 方法，這會在任何兩個時區之間轉換時間。

- <xref:System.TimeZoneInfo.ConvertTimeFromUtc%2A>和 <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A> 方法，可將特定時區的時間轉換為 utc，或將 UTC 轉換為特定時區的時間。

如需詳細資訊，請參閱[在各時區之間轉換時間](converting-between-time-zones.md)。

<xref:System.TimeZoneInfo>當您執行日期和時間算術時，類別不會提供自動套用調整規則的任何方法。 不過，作法是將時區時間轉換為 UTC，並執行算術運算，然後從 UTC 轉換回時區時間。 如需詳細資訊，請參閱[如何：在日期和時間運算中使用時區](use-time-zones-in-arithmetic.md)。

例如，下列程式碼與前面的程式碼類似，也是將 2008 年 3 月 9 日 凌晨 2:00 加上兩個半小時。 不過，因為它會先將美加中部標準時間轉換為 UTC，再執行日期和時間運算，然後將 UTC 的結果轉換回美加中部標準時間，所以產生的時間會反映美加中部標準時區到日光節約時間的轉換。

[!code-csharp[System.DateTimeOffset.Conceptual#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual5.cs#5)]
[!code-vb[System.DateTimeOffset.Conceptual#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual5.vb#5)]

## <a name="see-also"></a>另請參閱

- [日期、時間和時區](index.md)
- [如何：在日期和時間運算中使用時區](use-time-zones-in-arithmetic.md)
