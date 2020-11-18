---
title: 尋找定義於本機系統的時區
ms.date: 04/10/2017
helpviewer_keywords:
- time zones [.NET], local
- time zones [.NET], finding local system time zones
- time zone identifiers [.NET]
- local time zone access
- time zones [.NET], retrieving
- UTC times, finding local system time zones
- time zones [.NET], UTC
ms.assetid: 3f63b1bc-9a4b-4bde-84ea-ab028a80d3e1
ms.openlocfilehash: 02467e10494e72c83ad9521228f6c4151c4a6bd1
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94817935"
---
# <a name="finding-the-time-zones-defined-on-a-local-system"></a>尋找定義於本機系統的時區

<xref:System.TimeZoneInfo> 類別不會公開公用建構函式。 如此一來，`new` 關鍵字不能用來建立新的 <xref:System.TimeZoneInfo> 物件。 相反地，<xref:System.TimeZoneInfo> 物件可從登錄擷取預先定義時區的詳細資訊，或建立自訂的時區來具現化。 本主題討論從儲存在登錄中的資料具現化時區。 此外，<xref:System.TimeZoneInfo> 類別的 `static` (在 Visual Basic 中為 `shared`) 屬性提供國際標準時間 (UTC) 及當地時區的存取。

> [!NOTE]
> 對於在登錄中未定義的時區，您可以呼叫 <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> 方法的多載來建立自訂時區。 [如何：建立沒有調整規則的時區](create-time-zones-without-adjustment-rules.md)和[如何：建立具有調整規則的](create-time-zones-with-adjustment-rules.md)時區主題中會討論建立自訂時區。 此外，您可以在序列化字串中使用 <xref:System.TimeZoneInfo.FromSerializedString%2A> 方法還原 <xref:System.TimeZoneInfo> 物件，對其具現化。 <xref:System.TimeZoneInfo>[如何：將時區儲存到內嵌資源](save-time-zones-to-an-embedded-resource.md)和[如何：從內嵌資源還原時區](restore-time-zones-from-an-embedded-resource.md)主題中會討論序列化和還原序列化物件。

## <a name="accessing-individual-time-zones"></a>存取個別時區

<xref:System.TimeZoneInfo> 類別提供兩個預先定義的時區物件，該物件代表 UTC 時間和當地時區。 它們分別由 <xref:System.TimeZoneInfo.Utc%2A> 和 <xref:System.TimeZoneInfo.Local%2A> 屬性所提供。 如需存取 UTC 或當地時區的指示，請參閱 [如何：存取預先定義的 utc 和當地時區物件](access-utc-and-local.md)。

您也可以具現化 <xref:System.TimeZoneInfo> 物件，該物件代表在登錄中所定義的任何時區。 如需將特定時區物件具現化的指示，請參閱 [如何：具現化 TimeZoneInfo 物件](instantiate-time-zone-info.md)。

## <a name="time-zone-identifiers"></a>時區識別碼

時區識別項是唯一識別時區的索引鍵欄位。 雖然大部分的索引鍵相對較短，但時區識別項相較之下就很長。 在大部分情況下，其值會對應到 <xref:System.TimeZoneInfo.StandardName%2A?displayProperty=nameWithType> 屬性，用來提供時區標準時間的名稱。 不過仍有例外狀況。 若要確定您提供了有效的識別項，最好是列舉系統上可用的時區，並記下其相關聯的識別項。

## <a name="see-also"></a>請參閱

- [日期、時間和時區](index.md)
- [如何：存取預先定義的 UTC 和當地時區物件](access-utc-and-local.md)
- [如何：具現化 TimeZoneInfo 物件](instantiate-time-zone-info.md)
- [在各時區之間轉換時間](converting-between-time-zones.md)
