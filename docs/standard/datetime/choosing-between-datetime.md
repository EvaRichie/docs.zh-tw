---
title: 比較 DateTime、DateTimeOffset、TimeSpan 和 TimeZoneInfo
description: 瞭解 DateTime、DateTimeOffset、TimeSpan 和 TimeZoneInfo 類型之間的差異，以代表 .NET 中的日期和時間資訊。
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DateTimeOffset structure
- TimeZoneInfo class
- time zones [.NET], common uses
- date and time classes [.NET]
- time zones [.NET], type options
- DateTime structure
ms.assetid: 07f17aad-3571-4014-9ef3-b695a86f3800
ms.openlocfilehash: 5d6173642e88165bb52d5d9cfc85c8889ce763a5
ms.sourcegitcommit: b1442669f1982d3a1cb18ea35b5acfb0fc7d93e4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/30/2020
ms.locfileid: "93063868"
---
# <a name="choose-between-datetime-datetimeoffset-timespan-and-timezoneinfo"></a><span data-ttu-id="96e53-103">在 DateTime、DateTimeOffset、TimeSpan 和 TimeZoneInfo 之間進行選擇</span><span class="sxs-lookup"><span data-stu-id="96e53-103">Choose between DateTime, DateTimeOffset, TimeSpan, and TimeZoneInfo</span></span>

<span data-ttu-id="96e53-104">.NET 應用程式可以透過數種方式使用日期和時間資訊。</span><span class="sxs-lookup"><span data-stu-id="96e53-104">.NET applications can use date and time information in several ways.</span></span> <span data-ttu-id="96e53-105">日期和時間資訊的常見用法包括：</span><span class="sxs-lookup"><span data-stu-id="96e53-105">The more common uses of date and time information include:</span></span>

- <span data-ttu-id="96e53-106">只反映日期，使時間資訊不重要。</span><span class="sxs-lookup"><span data-stu-id="96e53-106">To reflect a date only, so that time information is not important.</span></span>

- <span data-ttu-id="96e53-107">只反映時間，使日期資訊不重要。</span><span class="sxs-lookup"><span data-stu-id="96e53-107">To reflect a time only, so that date information is not important.</span></span>

- <span data-ttu-id="96e53-108">反映抽象的日期和時間，這些並不會和特定時間或位置密切相關 (例如大多數國際連鎖的商店在工作日上午 9 點開始營業)。</span><span class="sxs-lookup"><span data-stu-id="96e53-108">To reflect an abstract date and time that is not tied to a specific time and place (for example, most stores in an international chain open on weekdays at 9:00 A.M.).</span></span>

- <span data-ttu-id="96e53-109">若要從 .NET 以外的來源中取出日期和時間資訊，通常會將日期和時間資訊儲存在單一資料型別中。</span><span class="sxs-lookup"><span data-stu-id="96e53-109">To retrieve date and time information from sources outside of .NET, typically where date and time information is stored in a simple data type.</span></span>

- <span data-ttu-id="96e53-110">若要唯一且明確地識別單一時間點。</span><span class="sxs-lookup"><span data-stu-id="96e53-110">To uniquely and unambiguously identify a single point in time.</span></span> <span data-ttu-id="96e53-111">有些應用程式只需要在主機系統上具有明確的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="96e53-111">Some applications require that a date and time be unambiguous only on the host system.</span></span> <span data-ttu-id="96e53-112">其他應用程式需要在不同的系統之間明確地 (也就是說，在一個系統上序列化的日期可以有意義地還原序列化，並在世界各地的另一個系統上使用) 。</span><span class="sxs-lookup"><span data-stu-id="96e53-112">Other apps require that it be unambiguous across systems (that is, a date serialized on one system can be meaningfully deserialized and used on another system anywhere in the world).</span></span>

- <span data-ttu-id="96e53-113">若要保留多個相關時間 (例如要求者的當地時間和 Web 要求的回條之伺服器時間)。</span><span class="sxs-lookup"><span data-stu-id="96e53-113">To preserve multiple related times (such as the requestor's local time and the server's time of receipt for a Web request).</span></span>

- <span data-ttu-id="96e53-114">若要執行日期和時間運算，且該運算可能有會唯一明確地識別單一時間點的結果。</span><span class="sxs-lookup"><span data-stu-id="96e53-114">To perform date and time arithmetic, possibly with a result that uniquely and unambiguously identifies a single point in time.</span></span>

<span data-ttu-id="96e53-115">.Net 包含 <xref:System.DateTime> 、 <xref:System.DateTimeOffset> 、 <xref:System.TimeSpan> 和 <xref:System.TimeZoneInfo> 類型，這些都可以用來建立使用日期和時間的應用程式。</span><span class="sxs-lookup"><span data-stu-id="96e53-115">.NET includes the <xref:System.DateTime>, <xref:System.DateTimeOffset>, <xref:System.TimeSpan>, and <xref:System.TimeZoneInfo> types, all of which can be used to build applications that work with dates and times.</span></span>

> [!NOTE]
> <span data-ttu-id="96e53-116">本主題不會討論 <xref:System.TimeZone> ，因為其功能幾乎全部併入 <xref:System.TimeZoneInfo> 類別中。</span><span class="sxs-lookup"><span data-stu-id="96e53-116">This topic doesn't discuss <xref:System.TimeZone> because its functionality is almost entirely incorporated in the <xref:System.TimeZoneInfo> class.</span></span> <span data-ttu-id="96e53-117">盡可能使用 <xref:System.TimeZoneInfo> 類別，而不是 <xref:System.TimeZone> 類別。</span><span class="sxs-lookup"><span data-stu-id="96e53-117">Whenever possible, use the <xref:System.TimeZoneInfo> class instead of the <xref:System.TimeZone> class.</span></span>

## <a name="the-datetimeoffset-structure"></a><span data-ttu-id="96e53-118">DateTimeOffset 結構</span><span class="sxs-lookup"><span data-stu-id="96e53-118">The DateTimeOffset structure</span></span>

<span data-ttu-id="96e53-119"><xref:System.DateTimeOffset> 結構代表日期和時間值，以及表示該值與 UTC 差異大小的位移。</span><span class="sxs-lookup"><span data-stu-id="96e53-119">The <xref:System.DateTimeOffset> structure represents a date and time value, together with an offset that indicates how much that value differs from UTC.</span></span> <span data-ttu-id="96e53-120">因此，該值一律明確地識別單一時間點。</span><span class="sxs-lookup"><span data-stu-id="96e53-120">Thus, the value always unambiguously identifies a single point in time.</span></span>

<span data-ttu-id="96e53-121"><xref:System.DateTimeOffset> 類型包含 <xref:System.DateTime> 類型的所有功能並感知時區。</span><span class="sxs-lookup"><span data-stu-id="96e53-121">The <xref:System.DateTimeOffset> type includes all of the functionality of the <xref:System.DateTime> type along with time zone awareness.</span></span> <span data-ttu-id="96e53-122">這可讓它適用于下列應用程式：</span><span class="sxs-lookup"><span data-stu-id="96e53-122">This makes it suitable for applications that:</span></span>

- <span data-ttu-id="96e53-123">唯一且明確地識別單一時間點。</span><span class="sxs-lookup"><span data-stu-id="96e53-123">Uniquely and unambiguously identify a single point in time.</span></span> <span data-ttu-id="96e53-124"><xref:System.DateTimeOffset> 類型可用來明確定義「現在」的意義，以記錄交易的時間、記錄系統或應用程式事件的時間以及記錄檔案建立及修改的時間。</span><span class="sxs-lookup"><span data-stu-id="96e53-124">The <xref:System.DateTimeOffset> type can be used to unambiguously define the meaning of "now", to log transaction times, to log the times of system or application events, and to record file creation and modification times.</span></span>

- <span data-ttu-id="96e53-125">執行一般日期和時間運算。</span><span class="sxs-lookup"><span data-stu-id="96e53-125">Perform general date and time arithmetic.</span></span>

- <span data-ttu-id="96e53-126">只要時間已儲存為兩個不同的值或一個結構中的兩個成員，就可保留多個相關時間。</span><span class="sxs-lookup"><span data-stu-id="96e53-126">Preserve multiple related times, as long as those times are stored as two separate values or as two members of a structure.</span></span>

> [!NOTE]
> <span data-ttu-id="96e53-127"><xref:System.DateTimeOffset> 值的用途比 <xref:System.DateTime> 值的更為普遍。</span><span class="sxs-lookup"><span data-stu-id="96e53-127">These uses for <xref:System.DateTimeOffset> values are much more common than those for <xref:System.DateTime> values.</span></span> <span data-ttu-id="96e53-128">因此，請考慮 <xref:System.DateTimeOffset> 作為應用程式開發的預設日期和時間類型。</span><span class="sxs-lookup"><span data-stu-id="96e53-128">As a result, consider <xref:System.DateTimeOffset> as the default date and time type for application development.</span></span>

<span data-ttu-id="96e53-129"><xref:System.DateTimeOffset>值未系結至特定的時區，但可能來自各種不同的時區。</span><span class="sxs-lookup"><span data-stu-id="96e53-129">A <xref:System.DateTimeOffset> value isn't tied to a particular time zone, but can originate from a variety of time zones.</span></span> <span data-ttu-id="96e53-130">下列範例會列出數個 <xref:System.DateTimeOffset> 值 (包括當地太平洋標準時間) 可以屬於的時區。</span><span class="sxs-lookup"><span data-stu-id="96e53-130">The following example lists the time zones to which a number of <xref:System.DateTimeOffset> values (including a local Pacific Standard Time) can belong.</span></span>

[!code-csharp[System.DateTimeOffset.Conceptual#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual1.cs#1)]
[!code-vb[System.DateTimeOffset.Conceptual#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual1.vb#1)]

<span data-ttu-id="96e53-131">此輸出顯示在本範例中的每個日期和時間值可屬於至少三個不同時區。</span><span class="sxs-lookup"><span data-stu-id="96e53-131">The output shows that each date and time value in this example can belong to at least three different time zones.</span></span> <span data-ttu-id="96e53-132"><xref:System.DateTimeOffset>6/10/2007 的值顯示，如果日期和時間值代表日光節約時間，則其與 utc 的位移不一定會對應至原始時區的基底 UTC 位移，也不一定會對應到在其顯示名稱中找到的 UTC 時差。</span><span class="sxs-lookup"><span data-stu-id="96e53-132">The <xref:System.DateTimeOffset> value of 6/10/2007 shows that if a date and time value represents a daylight saving time, its offset from UTC doesn't even necessarily correspond to the originating time zone's base UTC offset or to the offset from UTC found in its display name.</span></span> <span data-ttu-id="96e53-133">因為單一 <xref:System.DateTimeOffset> 值未與時區緊密結合，所以它無法反映時區與日光節約時間之間的轉換。</span><span class="sxs-lookup"><span data-stu-id="96e53-133">Because a single <xref:System.DateTimeOffset> value isn't tightly coupled with its time zone, it can't reflect a time zone's transition to and from daylight saving time.</span></span> <span data-ttu-id="96e53-134">當使用日期和時間算術來操作值時，這可能會造成問題 <xref:System.DateTimeOffset> 。</span><span class="sxs-lookup"><span data-stu-id="96e53-134">This can be problematic when date and time arithmetic is used to manipulate a <xref:System.DateTimeOffset> value.</span></span> <span data-ttu-id="96e53-135">如需如何以考慮時區調整規則的方式來執行日期和時間運算的討論，請參閱 [使用日期和時間執行算數運算](performing-arithmetic-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="96e53-135">For a discussion of how to perform date and time arithmetic in a way that takes account of a time zone's adjustment rules, see [Performing arithmetic operations with dates and times](performing-arithmetic-operations.md).</span></span>

## <a name="the-datetime-structure"></a><span data-ttu-id="96e53-136">DateTime 結構</span><span class="sxs-lookup"><span data-stu-id="96e53-136">The DateTime structure</span></span>

<span data-ttu-id="96e53-137"><xref:System.DateTime> 值會定義特定的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="96e53-137">A <xref:System.DateTime> value defines a particular date and time.</span></span> <span data-ttu-id="96e53-138">它包含的 <xref:System.DateTime.Kind%2A> 屬性會提供該日期和時間所屬時區的有限資訊。</span><span class="sxs-lookup"><span data-stu-id="96e53-138">It includes a <xref:System.DateTime.Kind%2A> property that provides limited information about the time zone to which that date and time belongs.</span></span> <span data-ttu-id="96e53-139">由 <xref:System.DateTimeKind> 屬性傳回的 <xref:System.DateTime.Kind%2A> 值，表示 <xref:System.DateTime> 值是否代表當地時間 (<xref:System.DateTimeKind.Local?displayProperty=nameWithType>)、國際標準時間 (UTC) (<xref:System.DateTimeKind.Utc?displayProperty=nameWithType>) 或未指定的時間 (<xref:System.DateTimeKind.Unspecified?displayProperty=nameWithType>)。</span><span class="sxs-lookup"><span data-stu-id="96e53-139">The <xref:System.DateTimeKind> value returned by the <xref:System.DateTime.Kind%2A> property indicates whether the <xref:System.DateTime> value represents the local time (<xref:System.DateTimeKind.Local?displayProperty=nameWithType>), Coordinated Universal Time (UTC) (<xref:System.DateTimeKind.Utc?displayProperty=nameWithType>), or an unspecified time (<xref:System.DateTimeKind.Unspecified?displayProperty=nameWithType>).</span></span>

<span data-ttu-id="96e53-140">此 <xref:System.DateTime> 結構適用于具有下列一或多個特性的應用程式：</span><span class="sxs-lookup"><span data-stu-id="96e53-140">The <xref:System.DateTime> structure is suitable for applications with one or more of the following characteristics:</span></span>

- <span data-ttu-id="96e53-141">只使用日期。</span><span class="sxs-lookup"><span data-stu-id="96e53-141">Work with dates only.</span></span>

- <span data-ttu-id="96e53-142">只使用時間。</span><span class="sxs-lookup"><span data-stu-id="96e53-142">Work with times only.</span></span>

- <span data-ttu-id="96e53-143">使用抽象的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="96e53-143">Work with abstract dates and times.</span></span>

- <span data-ttu-id="96e53-144">使用遺漏時區資訊的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="96e53-144">Work with dates and times for which time zone information is missing.</span></span>

- <span data-ttu-id="96e53-145">只使用 UTC 日期和時間。</span><span class="sxs-lookup"><span data-stu-id="96e53-145">Work with UTC dates and times only.</span></span>

- <span data-ttu-id="96e53-146">從 .NET 以外的來源取得日期和時間資訊，例如 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="96e53-146">Retrieve date and time information from sources outside of .NET, such as SQL databases.</span></span> <span data-ttu-id="96e53-147">一般而言，這些來源會將日期和時間資訊以和 <xref:System.DateTime> 結構相容的簡單格式儲存。</span><span class="sxs-lookup"><span data-stu-id="96e53-147">Typically, these sources store date and time information in a simple format that is compatible with the <xref:System.DateTime> structure.</span></span>

- <span data-ttu-id="96e53-148">執行日期和時間運算，但關心其一般結果。</span><span class="sxs-lookup"><span data-stu-id="96e53-148">Perform date and time arithmetic, but are concerned with general results.</span></span> <span data-ttu-id="96e53-149">例如，在對特定日期和時間加入六個月的加法運算中，該結果是否對日光節約時間進行調整通常並不重要。</span><span class="sxs-lookup"><span data-stu-id="96e53-149">For example, in an addition operation that adds six months to a particular date and time, it is often not important whether the result is adjusted for daylight saving time.</span></span>

<span data-ttu-id="96e53-150">除非特定的 <xref:System.DateTime> 值代表 UTC，否則該日期和時間值的可攜性通常是模稜兩可或受限制的。</span><span class="sxs-lookup"><span data-stu-id="96e53-150">Unless a particular <xref:System.DateTime> value represents UTC, that date and time value is often ambiguous or limited in its portability.</span></span> <span data-ttu-id="96e53-151">例如，如果 <xref:System.DateTime> 值代表當地時間，則在該當地時區是可攜式的 (也就是說，如果值在相同時區的另一個系統上還原序列化，則該值仍會明確地識別單一時間點)。</span><span class="sxs-lookup"><span data-stu-id="96e53-151">For example, if a <xref:System.DateTime> value represents the local time, it is portable within that local time zone (that is, if the value is deserialized on another system in the same time zone, that value still unambiguously identifies a single point in time).</span></span> <span data-ttu-id="96e53-152">在當地時區外， <xref:System.DateTime> 的值可有多重解譯。</span><span class="sxs-lookup"><span data-stu-id="96e53-152">Outside the local time zone, that <xref:System.DateTime> value can have multiple interpretations.</span></span> <span data-ttu-id="96e53-153">如果該值的 <xref:System.DateTime.Kind%2A> 屬性是 <xref:System.DateTimeKind.Unspecified?displayProperty=nameWithType>，則它的可攜性更差：現在它於相同的時區中模稜兩可，即使在第一次序列化的同一個系統上也可能如此。</span><span class="sxs-lookup"><span data-stu-id="96e53-153">If the value's <xref:System.DateTime.Kind%2A> property is <xref:System.DateTimeKind.Unspecified?displayProperty=nameWithType>, it is even less portable: it is now ambiguous within the same time zone and possibly even on the same system on which it was first serialized.</span></span> <span data-ttu-id="96e53-154">只有當 <xref:System.DateTime> 值代表 UTC 時，該值才會明確地識別單一時間點，無論該值所使用的系統或時區為何。</span><span class="sxs-lookup"><span data-stu-id="96e53-154">Only if a <xref:System.DateTime> value represents UTC does that value unambiguously identify a single point in time regardless of the system or time zone in which the value is used.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="96e53-155">當儲存或共用 <xref:System.DateTime> 資料時應該使用 UTC，且 <xref:System.DateTime> 值的 <xref:System.DateTime.Kind%2A> 屬性應該設為 <xref:System.DateTimeKind.Utc?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="96e53-155">When saving or sharing <xref:System.DateTime> data, UTC should be used and the <xref:System.DateTime> value's <xref:System.DateTime.Kind%2A> property should be set to <xref:System.DateTimeKind.Utc?displayProperty=nameWithType>.</span></span>

## <a name="the-timespan-structure"></a><span data-ttu-id="96e53-156">TimeSpan 結構</span><span class="sxs-lookup"><span data-stu-id="96e53-156">The TimeSpan structure</span></span>

<span data-ttu-id="96e53-157"><xref:System.TimeSpan> 結構表示時間間隔。</span><span class="sxs-lookup"><span data-stu-id="96e53-157">The <xref:System.TimeSpan> structure represents a time interval.</span></span> <span data-ttu-id="96e53-158">其兩個一般用法為：</span><span class="sxs-lookup"><span data-stu-id="96e53-158">Its two typical uses are:</span></span>

- <span data-ttu-id="96e53-159">反映出兩個日期和時間值之間的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="96e53-159">Reflecting the time interval between two date and time values.</span></span> <span data-ttu-id="96e53-160">例如，從另一個值中減去 <xref:System.DateTime> 值會傳回 <xref:System.TimeSpan> 值。</span><span class="sxs-lookup"><span data-stu-id="96e53-160">For example, subtracting one <xref:System.DateTime> value from another returns a <xref:System.TimeSpan> value.</span></span>

- <span data-ttu-id="96e53-161">測量已耗用時間。</span><span class="sxs-lookup"><span data-stu-id="96e53-161">Measuring elapsed time.</span></span> <span data-ttu-id="96e53-162">例如， <xref:System.Diagnostics.Stopwatch.Elapsed%2A?displayProperty=nameWithType> 屬性會傳回一個 <xref:System.TimeSpan> 值，這個值會反映自呼叫開始測量已耗用時間的其中一個方法以來所經過的時間間隔 <xref:System.Diagnostics.Stopwatch> 。</span><span class="sxs-lookup"><span data-stu-id="96e53-162">For example, the <xref:System.Diagnostics.Stopwatch.Elapsed%2A?displayProperty=nameWithType> property returns a <xref:System.TimeSpan> value that reflects the time interval that has elapsed since the call to one of the <xref:System.Diagnostics.Stopwatch> methods that begins to measure elapsed time.</span></span>

<span data-ttu-id="96e53-163">值 <xref:System.TimeSpan> 也可以用來做為值的取代 <xref:System.DateTime> ，而該值會反映未參考特定日期的時間。</span><span class="sxs-lookup"><span data-stu-id="96e53-163">A <xref:System.TimeSpan> value can also be used as a replacement for a <xref:System.DateTime> value when that value reflects a time without reference to a particular day.</span></span> <span data-ttu-id="96e53-164">這種用法類似于 <xref:System.DateTime.TimeOfDay%2A?displayProperty=nameWithType> 和 <xref:System.DateTimeOffset.TimeOfDay%2A?displayProperty=nameWithType> 屬性，這些屬性會傳回 <xref:System.TimeSpan> 代表未參考日期之時間的值。</span><span class="sxs-lookup"><span data-stu-id="96e53-164">This usage is similar to the <xref:System.DateTime.TimeOfDay%2A?displayProperty=nameWithType> and <xref:System.DateTimeOffset.TimeOfDay%2A?displayProperty=nameWithType> properties, which return a <xref:System.TimeSpan> value that represents the time without reference to a date.</span></span> <span data-ttu-id="96e53-165">例如， <xref:System.TimeSpan> 結構可用來反映商店每日開始營業或打烊的時間，或可用來代表任何有規律事件發生的時間。</span><span class="sxs-lookup"><span data-stu-id="96e53-165">For example, the <xref:System.TimeSpan> structure can be used to reflect a store's daily opening or closing time, or it can be used to represent the time at which any regular event occurs.</span></span>

<span data-ttu-id="96e53-166">下列範例會定義 `StoreInfo` 結構，其中包含用來儲存開始營業和打烊時間的 <xref:System.TimeSpan> 物件，以及代表商店所在時區的 <xref:System.TimeZoneInfo> 物件。</span><span class="sxs-lookup"><span data-stu-id="96e53-166">The following example defines a `StoreInfo` structure that includes <xref:System.TimeSpan> objects for store opening and closing times, as well as a <xref:System.TimeZoneInfo> object that represents the store's time zone.</span></span> <span data-ttu-id="96e53-167">該結構也包含兩種方法， `IsOpenNow` 和 `IsOpenAt`，假定使用者處於當地時區，該結構會表示商店是否於使用者指定的時間開始營業。</span><span class="sxs-lookup"><span data-stu-id="96e53-167">The structure also includes two methods, `IsOpenNow` and `IsOpenAt`, that indicates whether the store is open at a time specified by the user, who is assumed to be in the local time zone.</span></span>

[!code-csharp[Conceptual.ChoosingDates#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.choosingdates/cs/datetimereplacement1.cs#1)]
[!code-vb[Conceptual.ChoosingDates#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.choosingdates/vb/datetimereplacement1.vb#1)]

<span data-ttu-id="96e53-168">然後 `StoreInfo` 結構可供用戶端程式碼使用，如下所示。</span><span class="sxs-lookup"><span data-stu-id="96e53-168">The `StoreInfo` structure can then be used by client code like the following.</span></span>

[!code-csharp[Conceptual.ChoosingDates#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.choosingdates/cs/datetimereplacement1.cs#2)]
[!code-vb[Conceptual.ChoosingDates#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.choosingdates/vb/datetimereplacement1.vb#2)]

## <a name="the-timezoneinfo-class"></a><span data-ttu-id="96e53-169">TimeZoneInfo 類別</span><span class="sxs-lookup"><span data-stu-id="96e53-169">The TimeZoneInfo class</span></span>

<span data-ttu-id="96e53-170"><xref:System.TimeZoneInfo> class represents any of the Earth's time zones, and enables the conversion of any date and time in one time zone to its equivalent in another time zone.</span><span class="sxs-lookup"><span data-stu-id="96e53-170">The <xref:System.TimeZoneInfo> class represents any of the Earth's time zones, and enables the conversion of any date and time in one time zone to its equivalent in another time zone.</span></span> <span data-ttu-id="96e53-171"><xref:System.TimeZoneInfo> 類別讓您能夠處理日期和時間，讓任何日期和時間值能明確地識別單一時間點。</span><span class="sxs-lookup"><span data-stu-id="96e53-171">The <xref:System.TimeZoneInfo> class makes it possible to work with dates and times so that any date and time value unambiguously identifies a single point in time.</span></span> <span data-ttu-id="96e53-172"><xref:System.TimeZoneInfo> 類別也可延伸。</span><span class="sxs-lookup"><span data-stu-id="96e53-172">The <xref:System.TimeZoneInfo> class is also extensible.</span></span> <span data-ttu-id="96e53-173">雖然這取決於提供給 Windows 系統和定義於登錄中的時區資訊，但它支援建立自訂的時區。</span><span class="sxs-lookup"><span data-stu-id="96e53-173">Although it depends on time zone information provided for Windows systems and defined in the registry, it supports the creation of custom time zones.</span></span> <span data-ttu-id="96e53-174">它也支援時區資訊的序列化和還原序列化。</span><span class="sxs-lookup"><span data-stu-id="96e53-174">It also supports the serialization and deserialization of time zone information.</span></span>

<span data-ttu-id="96e53-175">在某些情況下，欲充分利用 <xref:System.TimeZoneInfo> 類別可能需要進一步的開發工作。</span><span class="sxs-lookup"><span data-stu-id="96e53-175">In some cases, taking full advantage of the <xref:System.TimeZoneInfo> class may require further development work.</span></span> <span data-ttu-id="96e53-176">如果日期和時間值未與它們所屬的時區緊密結合，則需要進一步的工作。</span><span class="sxs-lookup"><span data-stu-id="96e53-176">If date and time values are not tightly coupled with the time zones to which they belong, further work is required.</span></span> <span data-ttu-id="96e53-177">除非您的應用程式提供某種機制，以將日期和時間與其相關聯的時區連結，否則特定日期和時間值很容易就會與其時區解除關聯。</span><span class="sxs-lookup"><span data-stu-id="96e53-177">Unless your application provides some mechanism for linking a date and time with its associated time zone, it's easy for a particular date and time value to become disassociated from its time zone.</span></span> <span data-ttu-id="96e53-178">連結此資訊的一種方法是定義類別或結構，其中包含日期和時間值，以及與其相關聯的時區物件。</span><span class="sxs-lookup"><span data-stu-id="96e53-178">One method of linking this information is to define a class or structure that contains both the date and time value and its associated time zone object.</span></span>

<span data-ttu-id="96e53-179">若要在 .NET 中利用時區支援，您必須知道當日期和時間物件具現化時，日期和時間值所屬的時區。</span><span class="sxs-lookup"><span data-stu-id="96e53-179">To take advantage of time zone support in .NET, you must know the time zone to which a date and time value belongs when that date and time object is instantiated.</span></span> <span data-ttu-id="96e53-180">時區通常是未知的，特別是在 web 或網路應用程式中。</span><span class="sxs-lookup"><span data-stu-id="96e53-180">The time zone is often not known, particularly in web or network apps.</span></span>

## <a name="see-also"></a><span data-ttu-id="96e53-181">另請參閱</span><span class="sxs-lookup"><span data-stu-id="96e53-181">See also</span></span>

- [<span data-ttu-id="96e53-182">日期、時間和時區</span><span class="sxs-lookup"><span data-stu-id="96e53-182">Dates, times, and time zones</span></span>](index.md)
