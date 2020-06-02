---
title: 如何：具現化 TimeZoneInfo 物件
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- instantiating time zone objects
- time zone objects [.NET Framework], instantiation
ms.assetid: 8cb620e5-c6a6-4267-a52e-beeb73cd1a34
ms.openlocfilehash: e8d50419dc21a1748a88c96c200806d0558f0e5a
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84276878"
---
# <a name="how-to-instantiate-a-timezoneinfo-object"></a>如何：具現化 TimeZoneInfo 物件

若要將 <xref:System.TimeZoneInfo> 物件具現化，最常見的方式是從登錄擷取其相關資訊。 本主題討論如何將 <xref:System.TimeZoneInfo> 物件從本機系統登錄具現化。

### <a name="to-instantiate-a-timezoneinfo-object"></a>將 TimeZoneInfo 物件具現化

1. 宣告 <xref:System.TimeZoneInfo> 物件。

2. 呼叫 `static` (Visual Basic 中的`Shared` ) <xref:System.TimeZoneInfo.FindSystemTimeZoneById%2A?displayProperty=nameWithType> 方法。

3. 處理由方法擲回的任何例外狀況，尤其是登錄中未定義時區時所擲回的 <xref:System.TimeZoneNotFoundException> 。

## <a name="example"></a>範例

下列程式碼會擷取 <xref:System.TimeZoneInfo> 物件，其代表美加東部標準時間區域，並顯示與本地時間對應的美加東部標準時間。

[!code-csharp[System.TimeZone2.Concepts#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#5)]
[!code-vb[System.TimeZone2.Concepts#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#5)]

<xref:System.TimeZoneInfo.FindSystemTimeZoneById%2A?displayProperty=nameWithType> 方法的單一參數是您想要擷取之時區的識別項，其對應至物件的 <xref:System.TimeZoneInfo.Id%2A?displayProperty=nameWithType> 屬性。 時區識別項是唯一識別時區的索引鍵欄位。 雖然大部分的索引鍵相對較短，但時區識別項相較之下就很長。 在大部分情況下，其值會對應到 <xref:System.TimeZoneInfo.StandardName%2A> 物件的 <xref:System.TimeZoneInfo> 屬性，其用來提供時區標準時間的名稱。 不過仍有例外狀況。 若要確定您提供了有效的識別項，最好的方法是列舉系統上可用的時區，並記下存在於其之上的時區識別項。 如需圖例，請參閱[如何：列舉電腦上存在的時區](enumerate-time-zones.md)。 [Finding the time zones defined on a local system](finding-the-time-zones-on-local-system.md) 主題同時包含所選取的時區識別碼的清單。

如果找到時區，此方法會傳回其 <xref:System.TimeZoneInfo> 物件。 如果找不到時區，方法會擲回 <xref:System.TimeZoneNotFoundException>。 如果找到時區，但其資料已損毀或不完整，則方法會擲回 <xref:System.InvalidTimeZoneException>。

如果您的應用程式依賴於必須存在的時區，則您應該先呼叫 <xref:System.TimeZoneInfo.FindSystemTimeZoneById%2A> 方法，以便從登錄擷取時區資訊。 如果方法呼叫失敗，則例外狀況處理常式應建立新的時區執行個體，或透過將序列化 <xref:System.TimeZoneInfo> 物件還原序列化，以重新建立時區執行個體。 如需範例，請參閱[如何：從內嵌資源還原時區](restore-time-zones-from-an-embedded-resource.md)。

## <a name="see-also"></a>另請參閱

- [日期、時間和時區](index.md)
- [尋找定義于本機系統的時區](finding-the-time-zones-on-local-system.md)
- [如何：存取預先定義的 UTC 和當地時區物件](access-utc-and-local.md)
