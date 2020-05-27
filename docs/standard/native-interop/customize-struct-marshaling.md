---
title: 自訂結構封送處理 - .NET
description: 了解如何自訂 .NET 如何以原生表示法封送處理您的結構。
ms.date: 01/18/2019
dev_langs:
- csharp
- cpp
ms.openlocfilehash: 8248ca589f41967a9112ba61c09599b337814de7
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "84003889"
---
# <a name="customizing-structure-marshaling"></a><span data-ttu-id="13203-103">自訂結構封送處理</span><span class="sxs-lookup"><span data-stu-id="13203-103">Customizing structure marshaling</span></span>

<span data-ttu-id="13203-104">有時候，結構的預設封送處理規則並不是完全如您所需要。</span><span class="sxs-lookup"><span data-stu-id="13203-104">Sometimes the default marshaling rules for structures aren't exactly what you need.</span></span> <span data-ttu-id="13203-105">.NET 執行階段提供一些延伸點，讓您自訂您結構的配置以及封送處理欄位的方式。</span><span class="sxs-lookup"><span data-stu-id="13203-105">The .NET runtimes provide a few extension points for you to customize your structure's layout and how fields are marshaled.</span></span>

## <a name="customizing-structure-layout"></a><span data-ttu-id="13203-106">自訂結構配置</span><span class="sxs-lookup"><span data-stu-id="13203-106">Customizing structure layout</span></span>

<span data-ttu-id="13203-107">.NET 提供 <xref:System.Runtime.InteropServices.StructLayoutAttribute?displayProperty=nameWithType> 屬性與 <xref:System.Runtime.InteropServices.LayoutKind?displayProperty=nameWithType> 列舉，讓您可以自訂欄位在記憶體中的放置方式。</span><span class="sxs-lookup"><span data-stu-id="13203-107">.NET provides the <xref:System.Runtime.InteropServices.StructLayoutAttribute?displayProperty=nameWithType> attribute and the <xref:System.Runtime.InteropServices.LayoutKind?displayProperty=nameWithType> enumeration to allow you to customize how fields are placed in memory.</span></span> <span data-ttu-id="13203-108">下列指導方針將可協助您避免常見問題。</span><span class="sxs-lookup"><span data-stu-id="13203-108">The following guidance will help you avoid common issues.</span></span>

<span data-ttu-id="13203-109">✔️ 考慮使用 `LayoutKind.Sequential` (若可行)。</span><span class="sxs-lookup"><span data-stu-id="13203-109">✔️ CONSIDER using `LayoutKind.Sequential` whenever possible.</span></span>

<span data-ttu-id="13203-110">只有 `LayoutKind.Explicit` 當您的原生結構也有明確的配置（例如等位）時，✔️才會在封送處理中使用。</span><span class="sxs-lookup"><span data-stu-id="13203-110">✔️ DO only use `LayoutKind.Explicit` in marshaling when your native struct also has an explicit layout, such as a union.</span></span>

<span data-ttu-id="13203-111">❌`LayoutKind.Explicit`如果您需要以 .Net Core 3.0 之前的執行時間為目標，請避免在非 Windows 平臺上封送處理結構時使用。</span><span class="sxs-lookup"><span data-stu-id="13203-111">❌ AVOID using `LayoutKind.Explicit` when marshaling structures on non-Windows platforms if you need to target runtimes before .NET Core 3.0.</span></span> <span data-ttu-id="13203-112">3.0 之前的 .NET Core 執行時間不支援在 Intel 或 AMD 64 位非 Windows 系統上，以傳值方式將明確結構傳遞至原生函式。</span><span class="sxs-lookup"><span data-stu-id="13203-112">The .NET Core runtime before 3.0 doesn't support passing explicit structures by value to native functions on Intel or AMD 64-bit non-Windows systems.</span></span> <span data-ttu-id="13203-113">不過，執行階段支援在所有平台上以傳參考方式傳遞明確結構。</span><span class="sxs-lookup"><span data-stu-id="13203-113">However, the runtime supports passing explicit structures by reference on all platforms.</span></span>

## <a name="customizing-boolean-field-marshaling"></a><span data-ttu-id="13203-114">自訂布林值欄位封送處理</span><span class="sxs-lookup"><span data-stu-id="13203-114">Customizing boolean field marshaling</span></span>

<span data-ttu-id="13203-115">機器碼有許多不同的布林值表示法。</span><span class="sxs-lookup"><span data-stu-id="13203-115">Native code has many different boolean representations.</span></span> <span data-ttu-id="13203-116">在 Windows 上，有三種方式可以代表布林值。</span><span class="sxs-lookup"><span data-stu-id="13203-116">On Windows alone, there are three ways to represent boolean values.</span></span> <span data-ttu-id="13203-117">執行階段不知道您結構的原生定義，因此它可以做到的最佳程度是猜測如何封送處理您的布林值。</span><span class="sxs-lookup"><span data-stu-id="13203-117">The runtime doesn't know the native definition of your structure, so the best it can do is make a guess on how to marshal your boolean values.</span></span> <span data-ttu-id="13203-118">.NET 執行階段提供一種方式來指出如何封送處理您的布林值欄位。</span><span class="sxs-lookup"><span data-stu-id="13203-118">The .NET runtime provides a way to indicate how to marshal your boolean field.</span></span> <span data-ttu-id="13203-119">下列範例示範如何將 .NET `bool` 封送處理為不同的原生布林值類型。</span><span class="sxs-lookup"><span data-stu-id="13203-119">The following examples show how to marshal .NET `bool` to different native boolean types.</span></span>

<span data-ttu-id="13203-120">布林值預設為封送處理為原生4位元組 Win32 [`BOOL`](/windows/desktop/winprog/windows-data-types#BOOL) 值，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="13203-120">Boolean values default to marshaling as a native 4-byte Win32 [`BOOL`](/windows/desktop/winprog/windows-data-types#BOOL) value as shown in the following example:</span></span>

```csharp
public struct WinBool
{
    public bool b;
}
```

```cpp
struct WinBool
{
    public BOOL b;
};
```

<span data-ttu-id="13203-121">若要更為明確，您可以使用 <xref:System.Runtime.InteropServices.UnmanagedType.Bool?displayProperty=nameWithType> 值來取得與上面相同的行為：</span><span class="sxs-lookup"><span data-stu-id="13203-121">If you want to be explicit, you can use the <xref:System.Runtime.InteropServices.UnmanagedType.Bool?displayProperty=nameWithType> value to get the same behavior as above:</span></span>

```csharp
public struct WinBool
{
    [MarshalAs(UnmanagedType.Bool)]
    public bool b;
}
```

```cpp
struct WinBool
{
    public BOOL b;
};
```

<span data-ttu-id="13203-122">使用下面的 `UnmanagedType.U1` 或 `UnmanagedType.I1` 值，您可以告訴執行階段將 `b` 欄位封送處理為 1 位元的原生 `bool` 類型。</span><span class="sxs-lookup"><span data-stu-id="13203-122">Using the `UnmanagedType.U1` or `UnmanagedType.I1` values below, you can tell the runtime to marshal the `b` field as a 1-byte native `bool` type.</span></span>

```csharp
public struct CBool
{
    [MarshalAs(UnmanagedType.U1)]
    public bool b;
}
```

```cpp
struct CBool
{
    public bool b;
};
```

<span data-ttu-id="13203-123">在 Windows 上，您可以使用 <xref:System.Runtime.InteropServices.UnmanagedType.VariantBool?displayProperty=nameWithType> 值來告訴執行階段將您的布林值封送處理為 2 位元的 `VARIANT_BOOL` 值：</span><span class="sxs-lookup"><span data-stu-id="13203-123">On Windows, you can use the <xref:System.Runtime.InteropServices.UnmanagedType.VariantBool?displayProperty=nameWithType> value to tell the runtime to marshal your boolean value to a 2-byte `VARIANT_BOOL` value:</span></span>

```csharp
public struct VariantBool
{
    [MarshalAs(UnmanagedType.VariantBool)]
    public bool b;
}
```

```cpp
struct VariantBool
{
    public VARIANT_BOOL b;
};
```

> [!NOTE]
> <span data-ttu-id="13203-124">`VARIANT_BOOL` 與 `VARIANT_TRUE = -1` 和 `VARIANT_FALSE = 0` 中的大部分布林值類型不同。</span><span class="sxs-lookup"><span data-stu-id="13203-124">`VARIANT_BOOL` is different than most bool types in that `VARIANT_TRUE = -1` and `VARIANT_FALSE = 0`.</span></span> <span data-ttu-id="13203-125">此外，不等於 `VARIANT_TRUE` 的所有值都會被視為 False。</span><span class="sxs-lookup"><span data-stu-id="13203-125">Additionally, all values that aren't equal to `VARIANT_TRUE` are considered false.</span></span>

## <a name="customizing-array-field-marshaling"></a><span data-ttu-id="13203-126">自訂陣列欄位封送處理</span><span class="sxs-lookup"><span data-stu-id="13203-126">Customizing array field marshaling</span></span>

<span data-ttu-id="13203-127">.NET 也包含一些可用來自訂陣列封送處理的方式。</span><span class="sxs-lookup"><span data-stu-id="13203-127">.NET also includes a few ways to customize array marshaling.</span></span>

<span data-ttu-id="13203-128">根據預設，.NET 會將陣列封送處理為指向連續元素清單的指標：</span><span class="sxs-lookup"><span data-stu-id="13203-128">By default, .NET marshals arrays as a pointer to a contiguous list of the elements:</span></span>

```csharp
public struct DefaultArray
{
    public int[] values;
}
```

```cpp
struct DefaultArray
{
    int* values;
};
```

<span data-ttu-id="13203-129">若您與 COM API 進行介面連接，您可能必須將陣列封送處理為 `SAFEARRAY*` 物件。</span><span class="sxs-lookup"><span data-stu-id="13203-129">If you're interfacing with COM APIs, you may have to marshal arrays as `SAFEARRAY*` objects.</span></span> <span data-ttu-id="13203-130">您可以使用 <xref:System.Runtime.InteropServices.MarshalAsAttribute?displayProperty=nameWithType> 與 <xref:System.Runtime.InteropServices.UnmanagedType.SafeArray?displayProperty=nameWithType> 值告訴執行階段將陣列封送處理為 `SAFEARRAY*`：</span><span class="sxs-lookup"><span data-stu-id="13203-130">You can use the <xref:System.Runtime.InteropServices.MarshalAsAttribute?displayProperty=nameWithType> and the <xref:System.Runtime.InteropServices.UnmanagedType.SafeArray?displayProperty=nameWithType> value to tell the runtime to marshal an array as a `SAFEARRAY*`:</span></span>

```csharp
public struct SafeArrayExample
{
    [MarshalAs(UnmanagedType.SafeArray)]
    public int[] values;
}
```

```cpp
struct SafeArrayExample
{
    SAFEARRAY* values;
};
```

<span data-ttu-id="13203-131">若需要自訂 `SAFEARRAY` 中的元素類型，您可以使用 <xref:System.Runtime.InteropServices.MarshalAsAttribute.SafeArraySubType?displayProperty=nameWithType> 與 <xref:System.Runtime.InteropServices.MarshalAsAttribute.SafeArrayUserDefinedSubType?displayProperty=nameWithType> 欄位來自訂精確的 `SAFEARRAY` 元素類型。</span><span class="sxs-lookup"><span data-stu-id="13203-131">If you need to customize what type of element is in the `SAFEARRAY`, then you can use the <xref:System.Runtime.InteropServices.MarshalAsAttribute.SafeArraySubType?displayProperty=nameWithType> and <xref:System.Runtime.InteropServices.MarshalAsAttribute.SafeArrayUserDefinedSubType?displayProperty=nameWithType> fields to customize the exact element type of the `SAFEARRAY`.</span></span>

<span data-ttu-id="13203-132">若需要就地封送處理陣列，您可以使用 <xref:System.Runtime.InteropServices.UnmanagedType.ByValArray?displayProperty=nameWithType> 值告訴封送處理器就地封送處理陣列。</span><span class="sxs-lookup"><span data-stu-id="13203-132">If you need to marshal the array in-place, you can use the <xref:System.Runtime.InteropServices.UnmanagedType.ByValArray?displayProperty=nameWithType> value to tell the marshaler to marshal the array in-place.</span></span> <span data-ttu-id="13203-133">當您此用此封送處理時，您也必須提供值給 <xref:System.Runtime.InteropServices.MarshalAsAttribute.SizeConst?displayProperty=nameWithType> 欄位作為陣列中的項目數目，以便執行階段可以正確地為結構配置空間。</span><span class="sxs-lookup"><span data-stu-id="13203-133">When you're using this marshaling, you also must supply a value to the <xref:System.Runtime.InteropServices.MarshalAsAttribute.SizeConst?displayProperty=nameWithType> field  for the number of elements in the array so the runtime can correctly allocate space for the structure.</span></span>

```csharp
public struct InPlaceArray
{
    [MarshalAs(UnmanagedType.ByValArray, SizeConst = 4)]
    public int[] values;
}
```

```cpp
struct InPlaceArray
{
    int values[4];
};
```

> [!NOTE]
> <span data-ttu-id="13203-134">.NET 不支援將可變長度陣列欄位封送處理為 C99 彈性陣列成員。</span><span class="sxs-lookup"><span data-stu-id="13203-134">.NET doesn't support marshaling a variable length array field as a C99 Flexible Array Member.</span></span>

## <a name="customizing-string-field-marshaling"></a><span data-ttu-id="13203-135">自訂字串欄位封送處理</span><span class="sxs-lookup"><span data-stu-id="13203-135">Customizing string field marshaling</span></span>

<span data-ttu-id="13203-136">.NET 也為封送處理字串欄位提供各種自訂。</span><span class="sxs-lookup"><span data-stu-id="13203-136">.NET also provides a wide variety of customizations for marshaling string fields.</span></span>

<span data-ttu-id="13203-137">根據預設，.NET 會將字串封送處理為指向結尾為 Null 之字串的指標。</span><span class="sxs-lookup"><span data-stu-id="13203-137">By default, .NET marshals a string as a pointer to a null-terminated string.</span></span> <span data-ttu-id="13203-138">編碼取決於 <xref:System.Runtime.InteropServices.StructLayoutAttribute?displayProperty=nameWithType> 中 <xref:System.Runtime.InteropServices.StructLayoutAttribute.CharSet?displayProperty=nameWithType> 欄位的值。</span><span class="sxs-lookup"><span data-stu-id="13203-138">The encoding depends on the value of the <xref:System.Runtime.InteropServices.StructLayoutAttribute.CharSet?displayProperty=nameWithType> field in the <xref:System.Runtime.InteropServices.StructLayoutAttribute?displayProperty=nameWithType>.</span></span> <span data-ttu-id="13203-139">若未指定任何屬性，編碼會預設為 ANSI 編碼。</span><span class="sxs-lookup"><span data-stu-id="13203-139">If no attribute is specified, the encoding defaults to an ANSI encoding.</span></span>

```csharp
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Ansi)]
public struct DefaultString
{
    public string str;
}
```

```cpp
struct DefaultString
{
    char* str;
};
```

```csharp
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
public struct DefaultString
{
    public string str;
}
```

```cpp
struct DefaultString
{
    char16_t* str; // Could also be wchar_t* on Windows.
};
```

<span data-ttu-id="13203-140">若需要為不同的藍未使用不同的編碼或只是想要在您的結構定義中更為明確，您可以使用 <xref:System.Runtime.InteropServices.MarshalAsAttribute?displayProperty=nameWithType> 屬性上的 <xref:System.Runtime.InteropServices.UnmanagedType.LPStr?displayProperty=nameWithType> 或 <xref:System.Runtime.InteropServices.UnmanagedType.LPWStr?displayProperty=nameWithType> 值。</span><span class="sxs-lookup"><span data-stu-id="13203-140">If you need to use different encodings for different fields or just prefer to be more explicit in your struct definition, you can use the <xref:System.Runtime.InteropServices.UnmanagedType.LPStr?displayProperty=nameWithType> or <xref:System.Runtime.InteropServices.UnmanagedType.LPWStr?displayProperty=nameWithType> values on a <xref:System.Runtime.InteropServices.MarshalAsAttribute?displayProperty=nameWithType> attribute.</span></span>

```csharp
public struct AnsiString
{
    [MarshalAs(UnmanagedType.LPStr)]
    public string str;
}
```

```cpp
struct AnsiString
{
    char* str;
};
```

```csharp
public struct UnicodeString
{
    [MarshalAs(UnmanagedType.LPWStr)]
    public string str;
}
```

```cpp
struct UnicodeString
{
    char16_t* str; // Could also be wchar_t* on Windows.
};
```

<span data-ttu-id="13203-141">若想要使用 UTF-8 編碼來封送處理您的字串，您可以使用 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 中的 <xref:System.Runtime.InteropServices.UnmanagedType.LPUTF8Str?displayProperty=nameWithType> 值。</span><span class="sxs-lookup"><span data-stu-id="13203-141">If you want to marshal your strings using the UTF-8 encoding, you can use the <xref:System.Runtime.InteropServices.UnmanagedType.LPUTF8Str?displayProperty=nameWithType> value in your <xref:System.Runtime.InteropServices.MarshalAsAttribute>.</span></span>

```csharp
public struct UTF8String
{
    [MarshalAs(UnmanagedType.LPUTF8Str)]
    public string str;
}
```

```cpp
struct UTF8String
{
    char* str;
};
```

> [!NOTE]
> <span data-ttu-id="13203-142">使用 <xref:System.Runtime.InteropServices.UnmanagedType.LPUTF8Str?displayProperty=nameWithType> 需要 .NET Framework 4.7 (或更新版本) 或 .NET Core 1.1 (或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="13203-142">Using <xref:System.Runtime.InteropServices.UnmanagedType.LPUTF8Str?displayProperty=nameWithType> requires either .NET Framework 4.7 (or later versions) or .NET Core 1.1 (or later versions).</span></span> <span data-ttu-id="13203-143">它在 .NET Standard 2.0 中不提供。</span><span class="sxs-lookup"><span data-stu-id="13203-143">It isn't available in .NET Standard 2.0.</span></span>

<span data-ttu-id="13203-144">若您要處理 COM API，您可能必須將字串封送處理為 `BSTR`。</span><span class="sxs-lookup"><span data-stu-id="13203-144">If you're working with COM APIs, you may need to marshal a string as a `BSTR`.</span></span> <span data-ttu-id="13203-145">使用 <xref:System.Runtime.InteropServices.UnmanagedType.BStr?displayProperty=nameWithType> 值，您可以將字串封送處理為 `BSTR`。</span><span class="sxs-lookup"><span data-stu-id="13203-145">Using the <xref:System.Runtime.InteropServices.UnmanagedType.BStr?displayProperty=nameWithType> value, you can marshal a string as a `BSTR`.</span></span>

```csharp
public struct BString
{
    [MarshalAs(UnmanagedType.BStr)]
    public string str;
}
```

```cpp
struct BString
{
    BSTR str;
};
```

<span data-ttu-id="13203-146">使用 WinRT 型 API 時，您可能需要將字串封送處理為 `HSTRING`。</span><span class="sxs-lookup"><span data-stu-id="13203-146">When using a WinRT-based API, you may need to marshal a string as an `HSTRING`.</span></span>  <span data-ttu-id="13203-147">使用 <xref:System.Runtime.InteropServices.UnmanagedType.HString?displayProperty=nameWithType> 值，您可以將字串封送處理為 `HSTRING`。</span><span class="sxs-lookup"><span data-stu-id="13203-147">Using the <xref:System.Runtime.InteropServices.UnmanagedType.HString?displayProperty=nameWithType> value, you can marshal a string as a `HSTRING`.</span></span>

```csharp
public struct HString
{
    [MarshalAs(UnmanagedType.HString)]
    public string str;
}
```

```cpp
struct BString
{
    HSTRING str;
};
```

<span data-ttu-id="13203-148">若您的 API 要求您在結構中就地傳遞字串，您可以使用 <xref:System.Runtime.InteropServices.UnmanagedType.ByValTStr?displayProperty=nameWithType> 值。</span><span class="sxs-lookup"><span data-stu-id="13203-148">If your API requires you to pass the string in-place in the structure, you can use the <xref:System.Runtime.InteropServices.UnmanagedType.ByValTStr?displayProperty=nameWithType> value.</span></span> <span data-ttu-id="13203-149">請注意，由 `ByValTStr` 封送處理的字串編碼是由 `CharSet` 屬性決定。</span><span class="sxs-lookup"><span data-stu-id="13203-149">Do note that the encoding for a string marshaled by `ByValTStr` is determined from the `CharSet` attribute.</span></span> <span data-ttu-id="13203-150">此外，它要求字串長度必須由 <xref:System.Runtime.InteropServices.MarshalAsAttribute.SizeConst?displayProperty=nameWithType> 欄位傳遞。</span><span class="sxs-lookup"><span data-stu-id="13203-150">Additionally, it requires that a string length is passed by the <xref:System.Runtime.InteropServices.MarshalAsAttribute.SizeConst?displayProperty=nameWithType> field.</span></span>

```csharp
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Ansi)]
public struct DefaultString
{
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 4)]
    public string str;
}
```

```cpp
struct DefaultString
{
    char str[4];
};
```

```csharp
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
public struct DefaultString
{
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 4)]
    public string str;
}
```

```cpp
struct DefaultString
{
    char16_t str[4]; // Could also be wchar_t[4] on Windows.
};
```

## <a name="customizing-decimal-field-marshaling"></a><span data-ttu-id="13203-151">自訂十進位欄位封送處理</span><span class="sxs-lookup"><span data-stu-id="13203-151">Customizing decimal field marshaling</span></span>

<span data-ttu-id="13203-152">如果您使用的是 Windows，您可能會遇到一些使用原生[ `CY` 或 `CURRENCY` ](/windows/win32/api/wtypes/ns-wtypes-cy~r1)結構的 api。</span><span class="sxs-lookup"><span data-stu-id="13203-152">If you're working on Windows, you might encounter some APIs that use the native [`CY` or `CURRENCY`](/windows/win32/api/wtypes/ns-wtypes-cy~r1) structure.</span></span> <span data-ttu-id="13203-153">根據預設，.NET `decimal` 類型會封送處理至原生 [`DECIMAL`](/windows/win32/api/wtypes/ns-wtypes-decimal~r1) 結構。</span><span class="sxs-lookup"><span data-stu-id="13203-153">By default, the .NET `decimal` type marshals to the native [`DECIMAL`](/windows/win32/api/wtypes/ns-wtypes-decimal~r1) structure.</span></span> <span data-ttu-id="13203-154">不過，您可以使用 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 搭配 <xref:System.Runtime.InteropServices.UnmanagedType.Currency?displayProperty=nameWithType> 值來指示封送處理器將 `decimal` 值轉換為原生 `CY` 值。</span><span class="sxs-lookup"><span data-stu-id="13203-154">However, you can use a <xref:System.Runtime.InteropServices.MarshalAsAttribute> with the <xref:System.Runtime.InteropServices.UnmanagedType.Currency?displayProperty=nameWithType> value to instruct the marshaler to convert a `decimal` value to a native `CY` value.</span></span>

```csharp
public struct Currency
{
    [MarshalAs(UnmanagedType.Currency)]
    public decimal dec;
}
```

```cpp
struct Currency
{
    CY dec;
};
```

## <a name="marshaling-systemobjects"></a><span data-ttu-id="13203-155">封送處理 `System.Object`</span><span class="sxs-lookup"><span data-stu-id="13203-155">Marshaling `System.Object`s</span></span>

<span data-ttu-id="13203-156">在 Windows 上，您可以將 `object` 型別欄位封送處理為機器碼。</span><span class="sxs-lookup"><span data-stu-id="13203-156">On Windows, you can marshal `object`-typed fields to native code.</span></span> <span data-ttu-id="13203-157">您可以將這些欄位封送處理為下列三種類型的其中一種：</span><span class="sxs-lookup"><span data-stu-id="13203-157">You can marshal these fields to one of three types:</span></span>

- [`VARIANT`](/windows/win32/api/oaidl/ns-oaidl-variant)
- [`IUnknown*`](/windows/desktop/api/unknwn/nn-unknwn-iunknown)
- [`IDispatch*`](/windows/desktop/api/oaidl/nn-oaidl-idispatch)

<span data-ttu-id="13203-158">根據預設，`object` 類型欄位將會封送處理為會包裝物件的 `IUnknown*`。</span><span class="sxs-lookup"><span data-stu-id="13203-158">By default, an `object`-typed field will be marshaled to an `IUnknown*` that wraps the object.</span></span>

```csharp
public struct ObjectDefault
{
    public object obj;
}
```

```cpp
struct ObjectDefault
{
    IUnknown* obj;
};
```

<span data-ttu-id="13203-159">若要將物件欄位封送處理為 `IDispatch*`，請新增具有 <xref:System.Runtime.InteropServices.UnmanagedType.IDispatch?displayProperty=nameWithType> 值的 <xref:System.Runtime.InteropServices.MarshalAsAttribute>。</span><span class="sxs-lookup"><span data-stu-id="13203-159">If you want to marshal an object field to an `IDispatch*`, add a <xref:System.Runtime.InteropServices.MarshalAsAttribute> with the <xref:System.Runtime.InteropServices.UnmanagedType.IDispatch?displayProperty=nameWithType> value.</span></span>

```csharp
public struct ObjectDispatch
{
    [MarshalAs(UnmanagedType.IDispatch)]
    public object obj;
}
```

```cpp
struct ObjectDispatch
{
    IDispatch* obj;
};
```

<span data-ttu-id="13203-160">若要將它封送處理為 `VARIANT`，請新增具有 <xref:System.Runtime.InteropServices.UnmanagedType.Struct?displayProperty=nameWithType> 值的 <xref:System.Runtime.InteropServices.MarshalAsAttribute>。</span><span class="sxs-lookup"><span data-stu-id="13203-160">If you want to marshal it as a `VARIANT`, add a <xref:System.Runtime.InteropServices.MarshalAsAttribute> with the <xref:System.Runtime.InteropServices.UnmanagedType.Struct?displayProperty=nameWithType> value.</span></span>

```csharp
public struct ObjectVariant
{
    [MarshalAs(UnmanagedType.Struct)]
    public object obj;
}
```

```cpp
struct ObjectVariant
{
    VARIANT obj;
};
```

<span data-ttu-id="13203-161">下表說明 `obj` 的不同執行階段型別如何對應到 `VARIANT` 中儲存的各種型別：</span><span class="sxs-lookup"><span data-stu-id="13203-161">The following table describes how different runtime types of the `obj` field map to the various types stored in a `VARIANT`:</span></span>

| <span data-ttu-id="13203-162">.NET 類型</span><span class="sxs-lookup"><span data-stu-id="13203-162">.NET Type</span></span> | <span data-ttu-id="13203-163">VARIANT 型別</span><span class="sxs-lookup"><span data-stu-id="13203-163">VARIANT Type</span></span> | | <span data-ttu-id="13203-164">.NET 類型</span><span class="sxs-lookup"><span data-stu-id="13203-164">.NET Type</span></span> | <span data-ttu-id="13203-165">VARIANT 型別</span><span class="sxs-lookup"><span data-stu-id="13203-165">VARIANT Type</span></span> |
|------------|--------------|-|----------|--------------|
|  `byte`  | `VT_UI1` |     | `System.Runtime.InteropServices.BStrWrapper` | `VT_BSTR` |
| `sbyte`  | `VT_I1`  |     | `object`  | `VT_DISPATCH` |
| `short`  | `VT_I2`  |     | `System.Runtime.InteropServices.UnknownWrapper` | `VT_UNKNOWN` |
| `ushort` | `VT_UI2` |     | `System.Runtime.InteropServices.DispatchWrapper` | `VT_DISPATCH` |
| `int`    | `VT_I4`  |     | `System.Reflection.Missing` | `VT_ERROR` |
| `uint`   | `VT_UI4` |     | `(object)null` | `VT_EMPTY` |
| `long`   | `VT_I8`  |     | `bool` | `VT_BOOL` |
| `ulong`  | `VT_UI8` |     | `System.DateTime` | `VT_DATE` |
| `float`  | `VT_R4`  |     | `decimal` | `VT_DECIMAL` |
| `double` | `VT_R8`  |     | `System.Runtime.InteropServices.CurrencyWrapper` | `VT_CURRENCY` |
| `char`   | `VT_UI2` |     | `System.DBNull` | `VT_NULL` |
| `string` | `VT_BSTR`|
