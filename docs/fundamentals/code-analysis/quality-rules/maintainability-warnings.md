---
title: '可維護性規則 (程式碼分析) '
description: 瞭解程式碼分析可維護性規則。
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.maintainabilityrules
helpviewer_keywords:
- rules, maintainability
- managed code analysis rules, maintainability rules
- maintainability rules
author: gewarren
ms.author: gewarren
ms.openlocfilehash: fc2ef2b42eeba241b7af66b579a60365ad2b88c7
ms.sourcegitcommit: 2e4adc490c1d2a705a0592b295d606b10b9f51f1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/25/2020
ms.locfileid: "96585236"
---
# <a name="maintainability-rules"></a>維護性規則

維護性規則支援程式庫和應用程式維護。

## <a name="in-this-section"></a>本節內容

| 規則 | 描述 |
|-----------|-----------------------------------|
| [CA1501:避免在物件間過度繼承](ca1501.md) | 類型在其繼承階層架構 (Inheritance Hierarchy) 中超過四個層級的深度。 太深的巢狀類型階層架構可能會難以依循、了解和維護。 |
| [CA1502:避免造成過度複雜的方法](ca1502.md) | 這個規則會測量整個方法中線性獨立路徑的數目，此數目是由條件分支的數目與複雜度決定。 |
| [CA1505:應避免撰寫無法維護的程式碼](ca1505.md) | 類型或方法的維護性指標值很低。 維護性指標很低代表類型或方法很可能會難以維護，而應該列為需要重新設計的候選目標。 |
| [CA1506:應避免使用結合過度的類別](ca1506.md) | 這個規則會測量類別的耦合，方法是計算類型或方法包含的唯一類型參考數目。 |
| [CA1507:使用 nameof 取代字串](ca1507.md) | 字串常值會用來做為可使用運算式的引數 `nameof` 。 |
| [CA1508:避免使用無作用條件式程式碼](ca1508.md) | 方法的條件式程式碼一律會 `true` `false` 在執行時間評估為或。 這會導致條件的分支中有不正確程式碼 `false` 。 |
| [CA1509：程式碼度量設定檔中的項目無效](ca1509.md) | 程式碼度量規則（例如 [CA1501](ca1501.md)、 [CA1502](ca1502.md)、 [CA1505](ca1505.md) 和 [CA1506](ca1506.md)）提供了名為的設定檔， `CodeMetricsConfig.txt` 其專案無效。 |

## <a name="see-also"></a>另請參閱

- [測量 Managed 程式碼的複雜性和可維護性](/visualstudio/code-quality/code-metrics-values)
