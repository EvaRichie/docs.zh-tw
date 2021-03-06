---
title: 重大變更： RC2 中的參數名稱已變更
description: 瞭解核心 .NET 程式庫中的 .NET 5.0 重大變更，其中某些參考元件參數名稱已從預覽和發行候選版本的 .NET 5.0 變更。
ms.date: 11/01/2020
ms.openlocfilehash: 554a4fa9e08fdb504f380465496d7e7e9df85814
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760686"
---
# <a name="parameter-names-changed-in-rc2"></a>RC2 中的參數名稱已變更

某些參考元件參數名稱已變更，以符合實元件中的參數名稱。

## <a name="change-description"></a>變更描述

在舊版的 .NET 5.0 preview 和 RC 版本中，某些 [參考元件](../../../../standard/assembly/reference-assemblies.md) 參數名稱與其在執行元件中的對應參數不同。 這可能會在使用具名引數和反映時造成問題。

在 .NET 5.0 RC2 中，這些不相符的參數名稱已在參考元件中更新，以完全符合執行元件中的對應參數名稱。

下表顯示變更的 Api 和參數名稱。

| API | 舊的參數名稱 | 新參數名稱 |
| - | - | - |
| <xref:System.Diagnostics.ActivityContext.%23ctor(System.Diagnostics.ActivityTraceId,System.Diagnostics.ActivitySpanId,System.Diagnostics.ActivityTraceFlags,System.String,System.Boolean)> | `traceOptions` | `traceFlags` |
| <xref:System.Globalization.CompareInfo.IsPrefix(System.ReadOnlySpan{System.Char},System.ReadOnlySpan{System.Char},System.Globalization.CompareOptions,System.Int32@)?displayProperty=nameWithType> | `suffix` | `prefix` |

## <a name="reason-for-change"></a>變更的原因

變更參數名稱的一致性，並避免在使用具名引數和反映時失敗。

## <a name="version-introduced"></a>引進的版本

5.0 RC2

## <a name="recommended-action"></a>建議的動作

如果您因為參數名稱變更而發生編譯器錯誤，請據以更新參數名稱。

## <a name="affected-apis"></a>受影響的 API

- <xref:System.Diagnostics.ActivityContext.%23ctor(System.Diagnostics.ActivityTraceId,System.Diagnostics.ActivitySpanId,System.Diagnostics.ActivityTraceFlags,System.String,System.Boolean)>
- <xref:System.Globalization.CompareInfo.IsPrefix(System.ReadOnlySpan{System.Char},System.ReadOnlySpan{System.Char},System.Globalization.CompareOptions,System.Int32@)?displayProperty=fullName>

<!--

#### Category

Core .NET libraries

### Affected APIs

- `M:System.Diagnostics.ActivityContext.#ctor(System.Diagnostics.ActivityTraceId,System.Diagnostics.ActivitySpanId,System.Diagnostics.ActivityTraceFlags,System.String,System.Boolean)`
- `M:System.Globalization.CompareInfo.IsPrefix(System.ReadOnlySpan{System.Char},System.ReadOnlySpan{System.Char},System.Globalization.CompareOptions,System.Int32@)`

-->
