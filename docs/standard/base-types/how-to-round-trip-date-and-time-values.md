---
title: 作法：反覆存取日期和時間值
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- round-trip date and time values
- dates [.NET Framework], round-trip values
- time zones [.NET Framework], round-trip date and time values
- time [.NET Framework], round-trip values
- formatting strings [.NET Framework], round-trip values
ms.assetid: b609b277-edc6-4c74-b03e-ea73324ecbdb
ms.openlocfilehash: 60483a6e29c65fc0c5803e8084053d53d9fc3c37
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84290444"
---
# <a name="how-to-round-trip-date-and-time-values"></a><span data-ttu-id="522c4-102">作法：反覆存取日期和時間值</span><span class="sxs-lookup"><span data-stu-id="522c4-102">How to: Round-trip Date and Time Values</span></span>

<span data-ttu-id="522c4-103">在許多應用程式中，日期和時間值的用途都是要明確地識別單一時間點。</span><span class="sxs-lookup"><span data-stu-id="522c4-103">In many applications, a date and time value is intended to unambiguously identify a single point in time.</span></span> <span data-ttu-id="522c4-104">本文說明如何儲存和還原 <xref:System.DateTime> 值、 <xref:System.DateTimeOffset> 值，以及具有時區資訊的日期和時間值，讓還原的值識別與儲存值相同的時間。</span><span class="sxs-lookup"><span data-stu-id="522c4-104">This article shows how to save and restore a <xref:System.DateTime> value, a <xref:System.DateTimeOffset> value, and a date and time value with time zone information so that the restored value identifies the same time as the saved value.</span></span>

## <a name="round-trip-a-datetime-value"></a><span data-ttu-id="522c4-105">來回行程日期時間值</span><span class="sxs-lookup"><span data-stu-id="522c4-105">Round-trip a DateTime value</span></span>

1. <span data-ttu-id="522c4-106">搭配 "o" 格式規範呼叫 <xref:System.DateTime.ToString%28System.String%29?displayProperty=nameWithType> 方法，以將 <xref:System.DateTime> 值轉換為其字串表示。</span><span class="sxs-lookup"><span data-stu-id="522c4-106">Convert the <xref:System.DateTime> value to its string representation by calling the <xref:System.DateTime.ToString%28System.String%29?displayProperty=nameWithType> method with the "o" format specifier.</span></span>

2. <span data-ttu-id="522c4-107">將 <xref:System.DateTime> 值的字串表示儲存至檔案，或跨處理序、應用程式定義域或電腦界限進行傳遞。</span><span class="sxs-lookup"><span data-stu-id="522c4-107">Save the string representation of the <xref:System.DateTime> value to a file, or pass it across a process, application domain, or machine boundary.</span></span>

3. <span data-ttu-id="522c4-108">擷取代表 <xref:System.DateTime> 值的字串。</span><span class="sxs-lookup"><span data-stu-id="522c4-108">Retrieve the string that represents the <xref:System.DateTime> value.</span></span>

4. <span data-ttu-id="522c4-109">呼叫 <xref:System.DateTime.Parse%28System.String%2CSystem.IFormatProvider%2CSystem.Globalization.DateTimeStyles%29?displayProperty=nameWithType> 方法，然後傳遞 <xref:System.Globalization.DateTimeStyles.RoundtripKind?displayProperty=nameWithType> 作為 `styles` 參數值。</span><span class="sxs-lookup"><span data-stu-id="522c4-109">Call the <xref:System.DateTime.Parse%28System.String%2CSystem.IFormatProvider%2CSystem.Globalization.DateTimeStyles%29?displayProperty=nameWithType> method, and pass <xref:System.Globalization.DateTimeStyles.RoundtripKind?displayProperty=nameWithType> as the value of the `styles` parameter.</span></span>

<span data-ttu-id="522c4-110">下列範例說明如何反覆存取 <xref:System.DateTime> 值。</span><span class="sxs-lookup"><span data-stu-id="522c4-110">The following example illustrates how to round-trip a <xref:System.DateTime> value.</span></span>

[!code-csharp[Formatting.HowTo.RoundTrip#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/cs/RoundTrip.cs#1)]
[!code-vb[Formatting.HowTo.RoundTrip#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/vb/RoundTrip.vb#1)]

<span data-ttu-id="522c4-111">反覆存取 <xref:System.DateTime> 值時，這項技術可以成功保留所有當地和全球通用時間的時間。</span><span class="sxs-lookup"><span data-stu-id="522c4-111">When round-tripping a <xref:System.DateTime> value, this technique successfully preserves the time for all local and universal times.</span></span> <span data-ttu-id="522c4-112">例如，如果本地 <xref:System.DateTime> 值是儲存在美國太平洋標準時間時區系統中，並且還原為美國中央標準時間時區系統中，則還原的日期和時間會比原始時間多兩小時，反映出兩個時區之間的時差。</span><span class="sxs-lookup"><span data-stu-id="522c4-112">For example, if a local <xref:System.DateTime> value is saved on a system in the U.S. Pacific Standard Time zone and is restored on a system in the U.S. Central Standard Time zone, the restored date and time will be two hours later than the original time, which reflects the time difference between the two time zones.</span></span> <span data-ttu-id="522c4-113">不過，針對未指定的時間，這項技術並不一定準確。</span><span class="sxs-lookup"><span data-stu-id="522c4-113">However, this technique is not necessarily accurate for unspecified times.</span></span> <span data-ttu-id="522c4-114">所有 <xref:System.DateTime.Kind%2A> 屬性為 <xref:System.DateTimeKind.Unspecified> 的 <xref:System.DateTime> 值，都會被視為當地時間。</span><span class="sxs-lookup"><span data-stu-id="522c4-114">All <xref:System.DateTime> values whose <xref:System.DateTime.Kind%2A> property is <xref:System.DateTimeKind.Unspecified> are treated as if they are local times.</span></span> <span data-ttu-id="522c4-115">如果不是當地時間，就 <xref:System.DateTime> 不會成功地識別出正確的時間點。</span><span class="sxs-lookup"><span data-stu-id="522c4-115">If it's not a local time, the <xref:System.DateTime> doesn't successfully identify the correct point in time.</span></span> <span data-ttu-id="522c4-116">這項限制的因應措施，是將日期和時間值與其儲存和還原作業的時區緊密結合。</span><span class="sxs-lookup"><span data-stu-id="522c4-116">The workaround for this limitation is to tightly couple a date and time value with its time zone for the save and restore operation.</span></span>

## <a name="round-trip-a-datetimeoffset-value"></a><span data-ttu-id="522c4-117">來回存取 DateTimeOffset 值</span><span class="sxs-lookup"><span data-stu-id="522c4-117">Round-trip a DateTimeOffset value</span></span>

1. <span data-ttu-id="522c4-118">搭配 "o" 格式規範呼叫 <xref:System.DateTimeOffset.ToString%28System.String%29?displayProperty=nameWithType> 方法，以將 <xref:System.DateTimeOffset> 值轉換為其字串表示。</span><span class="sxs-lookup"><span data-stu-id="522c4-118">Convert the <xref:System.DateTimeOffset> value to its string representation by calling the <xref:System.DateTimeOffset.ToString%28System.String%29?displayProperty=nameWithType> method with the "o" format specifier.</span></span>

2. <span data-ttu-id="522c4-119">將 <xref:System.DateTimeOffset> 值的字串表示儲存至檔案，或跨處理序、應用程式定義域或電腦界限進行傳遞。</span><span class="sxs-lookup"><span data-stu-id="522c4-119">Save the string representation of the <xref:System.DateTimeOffset> value to a file, or pass it across a process, application domain, or machine boundary.</span></span>

3. <span data-ttu-id="522c4-120">擷取代表 <xref:System.DateTimeOffset> 值的字串。</span><span class="sxs-lookup"><span data-stu-id="522c4-120">Retrieve the string that represents the <xref:System.DateTimeOffset> value.</span></span>

4. <span data-ttu-id="522c4-121">呼叫 <xref:System.DateTimeOffset.Parse%28System.String%2CSystem.IFormatProvider%2CSystem.Globalization.DateTimeStyles%29?displayProperty=nameWithType> 方法，然後傳遞 <xref:System.Globalization.DateTimeStyles.RoundtripKind?displayProperty=nameWithType> 作為 `styles` 參數值。</span><span class="sxs-lookup"><span data-stu-id="522c4-121">Call the <xref:System.DateTimeOffset.Parse%28System.String%2CSystem.IFormatProvider%2CSystem.Globalization.DateTimeStyles%29?displayProperty=nameWithType> method, and pass <xref:System.Globalization.DateTimeStyles.RoundtripKind?displayProperty=nameWithType> as the value of the `styles` parameter.</span></span>

<span data-ttu-id="522c4-122">下列範例說明如何反覆存取 <xref:System.DateTimeOffset> 值。</span><span class="sxs-lookup"><span data-stu-id="522c4-122">The following example illustrates how to round-trip a <xref:System.DateTimeOffset> value.</span></span>

[!code-csharp[Formatting.HowTo.RoundTrip#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/cs/RoundTrip.cs#2)]
[!code-vb[Formatting.HowTo.RoundTrip#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/vb/RoundTrip.vb#2)]

<span data-ttu-id="522c4-123">這項技術一律會明確地將 <xref:System.DateTimeOffset> 值識別為單一時間點。</span><span class="sxs-lookup"><span data-stu-id="522c4-123">This technique always unambiguously identifies a <xref:System.DateTimeOffset> value as a single point in time.</span></span> <span data-ttu-id="522c4-124">接著可呼叫 <xref:System.DateTimeOffset.ToUniversalTime%2A?displayProperty=nameWithType> 方法來將值轉換為國際標準時間 (UTC)，或者可以呼叫 <xref:System.DateTimeOffset.ToOffset%2A?displayProperty=nameWithType> 或 <xref:System.TimeZoneInfo.ConvertTime%28System.DateTimeOffset%2CSystem.TimeZoneInfo%29?displayProperty=nameWithType> 方法來將它轉換為特定時區的時間。</span><span class="sxs-lookup"><span data-stu-id="522c4-124">The value can then be converted to Coordinated Universal Time (UTC) by calling the <xref:System.DateTimeOffset.ToUniversalTime%2A?displayProperty=nameWithType> method, or it can be converted to the time in a particular time zone by calling the <xref:System.DateTimeOffset.ToOffset%2A?displayProperty=nameWithType> or <xref:System.TimeZoneInfo.ConvertTime%28System.DateTimeOffset%2CSystem.TimeZoneInfo%29?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="522c4-125">這項技術有個主要限制：在表示特定時區之時間的 <xref:System.DateTimeOffset> 值上執行日期和時間算術時，可能不會產生該時區的精確結果。</span><span class="sxs-lookup"><span data-stu-id="522c4-125">The major limitation of this technique is that date and time arithmetic, when performed on a <xref:System.DateTimeOffset> value that represents the time in a particular time zone, may not produce accurate results for that time zone.</span></span> <span data-ttu-id="522c4-126">這是因為在將 <xref:System.DateTimeOffset> 值具現化時，就會解除它與其時區的關聯。</span><span class="sxs-lookup"><span data-stu-id="522c4-126">This is because when a <xref:System.DateTimeOffset> value is instantiated, it is disassociated from its time zone.</span></span> <span data-ttu-id="522c4-127">因此，當您執行日期和時間計算時，就無法再套用該時區的調整規則。</span><span class="sxs-lookup"><span data-stu-id="522c4-127">Therefore, that time zone's adjustment rules can no longer be applied when you perform date and time calculations.</span></span> <span data-ttu-id="522c4-128">若要解決這個問題，您可以定義自訂類型，以包含日期與時間值及其隨附的時區。</span><span class="sxs-lookup"><span data-stu-id="522c4-128">You can work around this problem by defining a custom type that includes both a date and time value and its accompanying time zone.</span></span>

## <a name="round-trip-a-date-and-time-value-with-its-time-zone"></a><span data-ttu-id="522c4-129">使用時區的日期和時間值來回行程</span><span class="sxs-lookup"><span data-stu-id="522c4-129">Round-trip a date and time value with its time zone</span></span>

1. <span data-ttu-id="522c4-130">定義包含兩個欄位的類別或結構。</span><span class="sxs-lookup"><span data-stu-id="522c4-130">Define a class or a structure with two fields.</span></span> <span data-ttu-id="522c4-131">第一個欄位是 <xref:System.DateTime> 或 <xref:System.DateTimeOffset> 物件，而第二個是 <xref:System.TimeZoneInfo> 物件。</span><span class="sxs-lookup"><span data-stu-id="522c4-131">The first field is either a <xref:System.DateTime> or a <xref:System.DateTimeOffset> object, and the second is a <xref:System.TimeZoneInfo> object.</span></span> <span data-ttu-id="522c4-132">下列範例是這種類型的簡單版本。</span><span class="sxs-lookup"><span data-stu-id="522c4-132">The following example is a simple version of such a type.</span></span>

    [!code-csharp[Formatting.HowTo.RoundTrip#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/cs/RoundTrip.cs#3)]
    [!code-vb[Formatting.HowTo.RoundTrip#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/vb/RoundTrip.vb#3)]

2. <span data-ttu-id="522c4-133">使用 <xref:System.SerializableAttribute> 屬性來標示類別。</span><span class="sxs-lookup"><span data-stu-id="522c4-133">Mark the class with the <xref:System.SerializableAttribute> attribute.</span></span>

3. <span data-ttu-id="522c4-134">使用 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Serialize%2A?displayProperty=nameWithType> 方法來將物件序列化。</span><span class="sxs-lookup"><span data-stu-id="522c4-134">Serialize the object using the <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Serialize%2A?displayProperty=nameWithType> method.</span></span>

4. <span data-ttu-id="522c4-135">使用 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize%2A> 方法來還原物件。</span><span class="sxs-lookup"><span data-stu-id="522c4-135">Restore the object using the <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize%2A> method.</span></span>

5. <span data-ttu-id="522c4-136">將還原序列化的物件轉型 (在 C# 中) 或轉換 (在 Visual Basic 中) 為適當類型的物件。</span><span class="sxs-lookup"><span data-stu-id="522c4-136">Cast (in C#) or convert (in Visual Basic) the deserialized object to an object of the appropriate type.</span></span>

<span data-ttu-id="522c4-137">下列範例說明如何反復存取儲存時區和日期和時間資訊的物件。</span><span class="sxs-lookup"><span data-stu-id="522c4-137">The following example illustrates how to round-trip an object that stores both time zone and date and time information.</span></span>

[!code-csharp[Formatting.HowTo.RoundTrip#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/cs/RoundTrip.cs#4)]
[!code-vb[Formatting.HowTo.RoundTrip#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/vb/RoundTrip.vb#4)]

<span data-ttu-id="522c4-138">假如組合的日期和時間及時區物件的實作不允許日期值變得與時區值不同步，這項技術應該在其儲存和還原前後，一律明確地反映正確的時間點。</span><span class="sxs-lookup"><span data-stu-id="522c4-138">This technique should always unambiguously reflect the correct point of time both before and after it is saved and restored, provided that the implementation of the combined date and time and time zone object does not allow the date value to become out of sync with the time zone value.</span></span>

## <a name="compile-the-code"></a><span data-ttu-id="522c4-139">編譯程式碼</span><span class="sxs-lookup"><span data-stu-id="522c4-139">Compile the code</span></span>

<span data-ttu-id="522c4-140">這些範例需要：</span><span class="sxs-lookup"><span data-stu-id="522c4-140">These examples require that:</span></span>

- <span data-ttu-id="522c4-141">使用 c # 指示詞或 Visual Basic 語句匯入下列命名空間 `using` `Imports` ：</span><span class="sxs-lookup"><span data-stu-id="522c4-141">The following namespaces be imported with C# `using` directives or Visual Basic `Imports` statements:</span></span>

  - <span data-ttu-id="522c4-142"><xref:System>（僅限 c #）</span><span class="sxs-lookup"><span data-stu-id="522c4-142"><xref:System> (C# only)</span></span>

  - <xref:System.Globalization?displayProperty=nameWithType>

  - <xref:System.IO?displayProperty=nameWithType>

  - <xref:System.Runtime.Serialization?displayProperty=nameWithType>

  - <xref:System.Runtime.Serialization.Formatters.Binary?displayProperty=nameWithType>

- <span data-ttu-id="522c4-143">除了類別以外，每個程式碼範例 `DateInTimeZone` 都包含在類別或 Visual Basic 模組中，包裝在方法中，並從 `Main` 方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="522c4-143">Each code example, other than the `DateInTimeZone` class, be included in a class or Visual Basic module, wrapped in methods, and called from the `Main` method.</span></span>

## <a name="see-also"></a><span data-ttu-id="522c4-144">另請參閱</span><span class="sxs-lookup"><span data-stu-id="522c4-144">See also</span></span>

- [<span data-ttu-id="522c4-145">在 DateTime、DateTimeOffset、TimeSpan 和 TimeZoneInfo 之間選擇</span><span class="sxs-lookup"><span data-stu-id="522c4-145">Choosing Between DateTime, DateTimeOffset, TimeSpan, and TimeZoneInfo</span></span>](../datetime/choosing-between-datetime.md)
- [<span data-ttu-id="522c4-146">標準日期和時間格式字串</span><span class="sxs-lookup"><span data-stu-id="522c4-146">Standard Date and Time Format Strings</span></span>](standard-date-and-time-format-strings.md)
