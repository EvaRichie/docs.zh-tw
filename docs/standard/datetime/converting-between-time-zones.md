---
title: 在各時區間轉換時間
description: 瞭解如何在 .NET 中將時間從一個時區轉換為另一個時區。 此外，也要瞭解如何轉換具有有限時區感知的 DateTimeOffset 值。
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- times [.NET Framework], converting
- time zones [.NET Framework], conversions
- UTC times, converting
- converting times
- local time conversions
ms.assetid: a51e1a3b-c983-4320-b31a-1f9fa3cf824a
ms.openlocfilehash: 156c3d8b360d62ba72f9a4447646fafe170ea658
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90547326"
---
# <a name="converting-times-between-time-zones"></a>在各時區間轉換時間

對於使用日期和時間來處理時區差異的任何應用程式，它會變得越來越重要。 應用程式無法再假設所有時間都是以當地時程表示，也就是從結構中可用的時間 <xref:System.DateTime> 。 例如，顯示美國東部目前時間的網頁對東亞地區的客戶不具公信力。 本主題說明如何將時間從某個時區轉換為另一個時區，以及如何轉換 <xref:System.DateTimeOffset> 具有有限時區感知的值。

## <a name="converting-to-coordinated-universal-time"></a>轉換為國際標準時間

國際標準時間 (UTC) 是高精確度且不可部分完成的時間標準。 全世界的時區都會表示為與 UTC 的正或負位移。 因此，UTC 提供一種無時區或時區中性時間。 跨電腦的日期和時間可攜性十分重要時，建議使用 UTC 時間。  (如需使用日期和時間的詳細資訊和其他最佳做法，請參閱 [.NET Framework 中使用 DateTime 的編碼最佳作法](/previous-versions/dotnet/articles/ms973825(v=msdn.10))。 ) 將個別時區轉換成 UTC，可讓時間比較輕鬆。

> [!NOTE]
> 您也可以將 <xref:System.DateTimeOffset> 結構序列化，以明確地表示單一時間點。 因為 <xref:System.DateTimeOffset> 物件會儲存日期和時間值以及其與 utc 的位移，所以一律會以 utc 的關聯性表示特定時間點。

將時間轉換為 UTC 的最簡單方式，就是 `static` `Shared` 在 Visual Basic) 方法中呼叫 (<xref:System.TimeZoneInfo.ConvertTimeToUtc%28System.DateTime%29?displayProperty=nameWithType> 。 方法所執行的確切轉換取決於 `dateTime` 參數的 <xref:System.DateTime.Kind%2A> 屬性值，如下表所示。

| `DateTime.Kind`            | 轉換                                                                     |
| -------------------------- | ------------------------------------------------------------------------------ |
| `DateTimeKind.Local`       | 將當地時間轉換為 UTC。                                                    |
| `DateTimeKind.Unspecified` | 假設 `dateTime` 參數是當地時間，並將當地時間轉換為 UTC。 |
| `DateTimeKind.Utc`         | 傳回未變更的 `dateTime` 參數。                                    |

下列程式碼會將目前當地時間轉換為 UTC，並將結果顯示到主控台。

[!code-csharp[System.TimeZone2.Concepts#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#6)]
[!code-vb[System.TimeZone2.Concepts#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#6)]

如果日期和時間值不是當地時間或 UTC，此 <xref:System.DateTime.ToUniversalTime%2A> 方法可能會傳回錯誤的結果。 不過，您可以使用 <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A?displayProperty=nameWithType> 方法，從指定的時區轉換日期和時間。  (如需有關如何取得 <xref:System.TimeZoneInfo> 代表目的地時區之物件的詳細資訊，請參閱 [尋找本機系統上定義的時區](finding-the-time-zones-on-local-system.md)) 。下列程式碼會使用 <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A?displayProperty=nameWithType> 方法將東部標準時間轉換成 UTC。

[!code-csharp[System.TimeZone2.Concepts#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#7)]
[!code-vb[System.TimeZone2.Concepts#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#7)]

請注意， <xref:System.ArgumentException> 如果 <xref:System.DateTime> 物件的 <xref:System.DateTime.Kind%2A> 屬性和時區不符，則這個方法會擲回。 如果 <xref:System.DateTime.Kind%2A> 屬性為 <xref:System.DateTimeKind.Local?displayProperty=nameWithType> <xref:System.TimeZoneInfo> ，但物件不代表本地時區，或 <xref:System.DateTime.Kind%2A> 屬性為 <xref:System.DateTimeKind.Utc?displayProperty=nameWithType> 但物件不 <xref:System.TimeZoneInfo> 相等， <xref:System.TimeZoneInfo.Utc?displayProperty=nameWithType> 則會發生不相符的情況。

所有這些方法都採用 <xref:System.DateTime> 值作為參數，並傳回 <xref:System.DateTime> 值。 針對 <xref:System.DateTimeOffset> 值， <xref:System.DateTimeOffset> 結構具有 <xref:System.DateTimeOffset.ToUniversalTime%2A> 實例方法，可將目前實例的日期和時間轉換為 UTC。 下列範例會呼叫 <xref:System.DateTimeOffset.ToUniversalTime%2A> 方法，將當地時間和數個其他時間轉換成國際標準時間 (UTC) 。

[!code-csharp[System.DateTimeOffset.Methods#16](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Methods/cs/Methods.cs#16)]
[!code-vb[System.DateTimeOffset.Methods#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Methods/vb/Methods.vb#16)]

## <a name="converting-utc-to-a-designated-time-zone"></a>將 UTC 轉換為指定的時區

若要將 UTC 轉換為當地時間，請參閱後面的「將 UTC 轉換為當地時間」一節。 若要將 UTC 轉換為您指定的任何時區時間，請呼叫 <xref:System.TimeZoneInfo.ConvertTimeFromUtc%2A> 方法。 此方法接受兩個參數：

- 要轉換的 UTC。 這必須是 <xref:System.DateTime> <xref:System.DateTime.Kind%2A> 屬性設定為或的值 `Unspecified` `Utc` 。

- 要將 UTC 轉換為的時區。

下列程式碼會將 UTC 轉換為美加中部標準時間。

[!code-csharp[System.TimeZone2.Concepts#8](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#8)]
[!code-vb[System.TimeZone2.Concepts#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#8)]

## <a name="converting-utc-to-local-time"></a>將 UTC 轉換為當地時間

若要將 UTC 轉換為當地時間，請呼叫 <xref:System.DateTime.ToLocalTime%2A> <xref:System.DateTime> 您要轉換其時間之物件的方法。 方法的確切行為取決於物件屬性的值 <xref:System.DateTime.Kind%2A> ，如下表所示。

| `DateTime.Kind`            | 轉換                                                                               |
| -------------------------- | ---------------------------------------------------------------------------------------- |
| `DateTimeKind.Local`       | 傳回未變更的 <xref:System.DateTime> 值。                                      |
| `DateTimeKind.Unspecified` | 假設 <xref:System.DateTime> 值為 utc，並將 utc 轉換為當地時間。 |
| `DateTimeKind.Utc`         | 將 <xref:System.DateTime> 值轉換為本地時間。                                 |

> [!NOTE]
> <xref:System.TimeZone.ToLocalTime%2A?displayProperty=nameWithType>方法的行為與方法相同 `DateTime.ToLocalTime` 。 它會採用單一參數，也就是要轉換的日期和時間值。

您也可以使用 `static` `Shared` Visual Basic) 方法中的 (，將任何指定時區的時間轉換為當地時間 <xref:System.TimeZoneInfo.ConvertTime%2A?displayProperty=nameWithType> 。 下一節將討論這項技術。

## <a name="converting-between-any-two-time-zones"></a>在兩個時區之間轉換

您可以使用 `static` `Shared` 類別的 Visual Basic) 方法中的下列兩個 (之一，在任何兩個時區之間進行轉換 <xref:System.TimeZoneInfo> ：

- <xref:System.TimeZoneInfo.ConvertTime%2A>

  這個方法的參數是要轉換的日期和時間值、 `TimeZoneInfo` 代表日期和時間值時區的物件，以及 `TimeZoneInfo` 代表要將日期和時間值轉換成之時區的物件。

- <xref:System.TimeZoneInfo.ConvertTimeBySystemTimeZoneId%2A>

  這個方法的參數是要轉換的日期和時間值、日期和時間值時區的識別碼，以及要將日期和時間值轉換成的時區識別碼。

這兩種方法都需要 <xref:System.DateTime.Kind%2A> 轉換日期和時間值的屬性，以及 <xref:System.TimeZoneInfo> 代表其時區的物件或時區識別碼彼此對應。 否則會擲回 <xref:System.ArgumentException>。 例如，如果 `Kind` 日期和時間值的屬性為 `DateTimeKind.Local` ，則如果 `TimeZoneInfo` 傳遞做為參數的物件不等於，則會擲回例外狀況 `TimeZoneInfo.Local` 。 如果以參數形式傳遞給方法的識別碼不等於，也會擲回例外狀況 `TimeZoneInfo.Local.Id` 。

下列範例會使用 <xref:System.TimeZoneInfo.ConvertTime%2A> 方法，從夏威夷標準時間轉換為當地時間。

[!code-csharp[System.TimeZone2.Concepts#9](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#9)]
[!code-vb[System.TimeZone2.Concepts#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#9)]

## <a name="converting-datetimeoffset-values"></a>轉換 DateTimeOffset 值

物件所代表的日期和時間值 <xref:System.DateTimeOffset> 不是完全時區感知，因為物件在具現化時與其時區解除關聯。 不過，在許多情況下，應用程式只需要根據與 UTC 的兩個不同位移來轉換日期和時間，而不是根據特定時區的時間。 若要執行這種轉換，您可以呼叫目前實例的 <xref:System.DateTimeOffset.ToOffset%2A> 方法。 方法的單一參數是方法要傳回之新日期和時間值的位移。

例如，如果網頁使用者要求的日期和時間已知且序列化為字串 (格式為 MM/dd/yyyy hh:mm:ss zzzz)，則下列 `ReturnTimeOnServer` 方法會將這個日期和時間值轉換為 Web 伺服器上的時間和日期。

[!code-csharp[System.DateTimeOffset.Conceptual.OffsetConversions#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.OffsetConversions/cs/TimeConversions.cs#1)]
[!code-vb[System.DateTimeOffset.Conceptual.OffsetConversions#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.OffsetConversions/vb/TimeConversions.vb#1)]

如果將字串 "9/1/2007 5:32:07 -05:00" 傳遞給這個方法，代表時區中的日期和時間比 UTC 早五個小時，就會傳回 9/1/2007 3:32:07 AM -07:00，代表伺服器位於美國「太平洋標準時間」時區。

<xref:System.TimeZoneInfo>類別也包含方法的多載 <xref:System.TimeZoneInfo.ConvertTime%28System.DateTimeOffset%2CSystem.TimeZoneInfo%29?displayProperty=nameWithType> ，此方法會使用值來執行時區轉換 <xref:System.DateTimeOffset.ToOffset(System.TimeSpan)> 。 方法的參數是 <xref:System.DateTimeOffset> 值，以及轉換時間的時區的參考。 方法呼叫會傳回 <xref:System.DateTimeOffset> 值。 例如， `ReturnTimeOnServer` 上一個範例中的方法可以重寫，如下所示，以呼叫 <xref:System.TimeZoneInfo.ConvertTime%28System.DateTimeOffset%2CSystem.TimeZoneInfo%29> 方法。

[!code-csharp[System.DateTimeOffset.Conceptual.OffsetConversions#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.OffsetConversions/cs/timeconversions2.cs#2)]
[!code-vb[System.DateTimeOffset.Conceptual.OffsetConversions#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.OffsetConversions/vb/TimeConversions2.vb#2)]

## <a name="see-also"></a>另請參閱

- <xref:System.TimeZoneInfo>
- [日期、時間和時區](index.md)
- [尋找定義於本機系統的時區](finding-the-time-zones-on-local-system.md)
