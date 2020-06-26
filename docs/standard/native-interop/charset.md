---
title: 字元集與封送處理 - .NET
description: 了解 CharSet 的不同值如何變更 .NET 將您的資料封送處理為機器碼的方式。
ms.date: 01/18/2019
ms.openlocfilehash: 39566593aa38bacfa41b44a8af8cc2dfb294d766
ms.sourcegitcommit: a2c8b19e813a52b91facbb5d7e3c062c7188b457
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85416105"
---
# <a name="charsets-and-marshaling"></a>字元集與封送處理

`char` 值、`string` 物件與 `System.Text.StringBuilder` 物件封送處理方式取決於 P/Invoke 或結構上 `CharSet` 欄位的值。 您可以透過在宣告您的 P/Invoke 時設定 <xref:System.Runtime.InteropServices.DllImportAttribute.CharSet?displayProperty=nameWithType> 欄位，以設定 P/Invoke 的 `CharSet`。 若要設定 `CharSet` 類型的，請 <xref:System.Runtime.InteropServices.StructLayoutAttribute.CharSet?displayProperty=nameWithType> 在您的類別或結構宣告上設定欄位。 當這些屬性欄位未設定時，語言編譯器可決定要使用的 `CharSet`。 C # 和 Visual Basic 預設會使用 <xref:System.Runtime.InteropServices.CharSet.Ansi> 字元集。

下表顯示每個字元集與使用該字元集進行封送處理時，如何表示字元或字串：

| `CharSet` 值 | Windows            | UNIX 上的 .NET Core 2.2 及更早版本 | UNIX 上的 .NET Core 3.0、更新版本及 Mono |
|-----------------|--------------------|-----------------------------------|------------------------------------------|
| `Ansi`          | `char` (系統預設 [Windows (ANSI) 字碼頁](/windows/win32/intl/code-pages))      | `char` (UTF-8)                    | `char` (UTF-8)                           |
| `Unicode`       | `wchar_t` (UTF-16) | `char16_t` (UTF-16)               | `char16_t` (UTF-16)                      |
| `Auto`          | `wchar_t` (UTF-16) | `char16_t` (UTF-16)               | `char` (UTF-8)                           |

選擇您的字元集時，請確定您知道您原生代表的代表應該是什麼樣子。
