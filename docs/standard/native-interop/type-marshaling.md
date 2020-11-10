---
title: 類型封送處理 - .NET
description: 了解 .NET 如何將您的類型封送處理至原生表示法。
ms.date: 01/18/2019
ms.openlocfilehash: 7fc3dfe950ecd3ed0ff5e4eb0e101c1596a831e1
ms.sourcegitcommit: 30a686fd4377fe6472aa04e215c0de711bc1c322
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/10/2020
ms.locfileid: "94440994"
---
# <a name="type-marshaling"></a>類型封送處理

當類型需要跨越受控程式碼和機器碼之間的界限時， **封送處理** 便是轉換類型的程序。

之所以需要進行封送處理，是因受控程式碼和非受控程式碼中的類型並不相同。 比方說，在 managed 程式碼中，您有一個 `String` ，而非受控世界的字串可以是 Unicode ( 「寬」 ) 、非 Unicode、以 null 終止的、ASCII 等等。根據預設，P/Invoke 子系統會根據本文所述的預設行為，嘗試進行正確的動作。 不過，在您需要進行額外控制的情況下，您可以運用 [MarshalAs](xref:System.Runtime.InteropServices.MarshalAsAttribute) 屬性來指定非受控端的預期類型。 比方說，如果您想要用以 null 終止的 ANSI 字串形式來傳送字串，您可以下列方式執行它︰

```csharp
[DllImport("somenativelibrary.dll")]
static extern int MethodA([MarshalAs(UnmanagedType.LPStr)] string parameter);
```

## <a name="default-rules-for-marshaling-common-types"></a>對常見類型進行封送處理的預設規則

一般而言，執行階段會在封送處理期間嘗試執行「正確動作」，以將您所需進行的工作減至最少。 下表描述每個類型在用於參數或欄位時，對其進行封送處理的預設值。 C99/C++11 固定寬度整數和字元類型是用來確保下表針對所有平台都是正確的。 您可以使用和這些類型具有相同對齊和大小需求的任何原生類型。

第一個表格會描述 P/Invoke 和欄位封送處理的封送處理皆相同之各種不同類型的對應。

| .NET 類型 | 原生類型  |
|-----------|-------------------------|
| `byte`    | `uint8_t`               |
| `sbyte`   | `int8_t`                |
| `short`   | `int16_t`               |
| `ushort`  | `uint16_t`              |
| `int`     | `int32_t`               |
| `uint`    | `uint32_t`              |
| `long`    | `int64_t`               |
| `ulong`   | `uint64_t`              |
| `char`    | `char` 或 `char16_t`，取決於 P/Invoke 或結構的 `CharSet`。 請參閱[字元集文件](charset.md)。 |
| `string`  | `char*` 或 `char16_t*`，取決於 P/Invoke 或結構的 `CharSet`。 請參閱[字元集文件](charset.md)。 |
| `System.IntPtr` | `intptr_t`        |
| `System.UIntPtr` | `uintptr_t`      |
| .NET 指標類型 (例如 `void*`)  | `void*` |
| 衍生自 `System.Runtime.InteropServices.SafeHandle` 的類型 | `void*` |
| 衍生自 `System.Runtime.InteropServices.CriticalHandle` 的類型 | `void*`          |
| `bool`    | Win32 `BOOL` 類型       |
| `decimal` | COM `DECIMAL` 結構 |
| .NET 委派 | 原生函式指標 |
| `System.DateTime` | Win32 `DATE` 類型 |
| `System.Guid` | Win32 `GUID` 類型 |

如果您是以參數或結構的形式進行封送處理，則有幾個封送處理類別具有不同的預設值。

| .NET 類型 | 原生類型 (參數) | 原生類型 (欄位) |
|-----------|-------------------------|---------------------|
| .NET 陣列 | 針對陣列元素原生表示法之陣列開頭的指標。 | 需要有 `[MarshalAs]` 屬性，否則不允許|
| 具有 `Sequential` 或 `Explicit`之 `LayoutKind` 的類別 | 針對類別之原生表示法的指標 | 類別的原生表示法 |

下表包含僅限 Windows 的預設封送處理規則。 在非 Windows 平台上，您無法對這些類型進行封送處理。

| .NET 類型 | 原生類型 (參數) | 原生類型 (欄位) |
|-----------|-------------------------|---------------------|
| `object`  | `VARIANT`               | `IUnknown*`         |
| `System.Array` | COM 介面 | 需要有 `[MarshalAs]` 屬性，否則不允許 |
| `System.ArgIterator` | `va_list` | 不允許 |
| `System.Collections.IEnumerator` | `IEnumVARIANT*` | 不允許 |
| `System.Collections.IEnumerable` | `IDispatch*` | 不允許 |
| `System.DateTimeOffset` | `int64_t` 代表從 1601 年 1 月 1 日午夜起的刻度數目 | `int64_t` 代表從 1601 年 1 月 1 日午夜起的刻度數目 |

某些類型只能以參數 (而非欄位) 的形式進行封送處理。 這些類型已列於下表中：

| .NET 類型 | 原生類型 (僅限參數) |
|-----------|------------------------------|
| `System.Text.StringBuilder` | `char*` 或 `char16_t*`，取決於 P/Invoke 的 `CharSet`。  請參閱[字元集文件](charset.md)。 |
| `System.ArgIterator` | `va_list` (僅限 Windows x86/x64/arm64) |
| `System.Runtime.InteropServices.ArrayWithOffset` | `void*` |
| `System.Runtime.InteropServices.HandleRef` | `void*` |

如果這些預設值無法達成您的目的，您可以自訂對參數進行封送處理的方式。 [參數封送處理](customize-parameter-marshaling.md)一文會引導您了解如何自訂對不同參數類型進行封送處理的方式。

## <a name="default-marshaling-in-com-scenarios"></a>COM 案例中的預設封送處理

當您對.NET 中的 COM 物件呼叫方法時，.NET 執行階段會依據常用的 COM 語意，變更此預設封送規則。 下表列出 .NET 執行階段在 COM 案例中使用的規則：

| .NET 類型 | 原生類型 (COM 方法呼叫) |
|-----------|--------------------------------|
| `bool`    | `VARIANT_BOOL`                 |
| `StringBuilder` | `LPWSTR`                 |
| `string`  | `BSTR`                         |
| 委派型別 | .NET Framework 中的 `_Delegate*`。 在 .NET Core 和 .NET 5 + 中不允許。 |
| `System.Drawing.Color` | `OLECOLOR`        |
| .NET 陣列 | `SAFEARRAY`                   |
| `string[]` | `BSTR` 的 `SAFEARRAY`        |

## <a name="marshaling-classes-and-structs"></a>封送處理類別和結構

封送處理類型的另一個層面是如何將結構傳遞給非受控方法。 比方說，有些 Unmanaged 方法需要結構以作為參數。 在這些情況下，您需要在世界的受控部分建立對應的結構或類別，以將它作為參數。 不過，只定義類別是不夠的，您也必須指示封送處理器如何將類別中的欄位對應至非受控結構。 在這裡，`StructLayout` 屬性將會變得很有用。

```csharp
[DllImport("kernel32.dll")]
static extern void GetSystemTime(SystemTime systemTime);

[StructLayout(LayoutKind.Sequential)]
class SystemTime {
    public ushort Year;
    public ushort Month;
    public ushort DayOfWeek;
    public ushort Day;
    public ushort Hour;
    public ushort Minute;
    public ushort Second;
    public ushort Milsecond;
}

public static void Main(string[] args) {
    SystemTime st = new SystemTime();
    GetSystemTime(st);
    Console.WriteLine(st.Year);
}
```

上述程式碼示範針對 `GetSystemTime()` 函式進行呼叫的簡單範例。 請注意第 4 行。 此屬性會指定類別的欄位應該循序對應至 Unmanaged 這一端上的結構。 這表示欄位的命名並不重要，只有其順序才重要，因為它需要對應至非受控結構，如下列範例所示︰

```c
typedef struct _SYSTEMTIME {
  WORD wYear;
  WORD wMonth;
  WORD wDayOfWeek;
  WORD wDay;
  WORD wHour;
  WORD wMinute;
  WORD wSecond;
  WORD wMilliseconds;
} SYSTEMTIME, *PSYSTEMTIME;
```

有時候，針對結構進行預設的封送處理並無法帶來您所需結果。 [自訂結構封送處理](./customize-struct-marshaling.md)一文會指導您如何自訂對結構進行封送處理的方式。
