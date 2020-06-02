---
title: 抽象類別設計
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- type design guidelines, abstract classes
- abstract classes, design guidelines
- class library design guidelines [.NET Framework], classes
- classes [.NET Framework], abstract
- classes [.NET Framework], design guidelines
- type design guidelines, classes
ms.assetid: d3646e6d-5c1f-4922-8fb0-ec5effb30d60
ms.openlocfilehash: e6a5923f293ed536fb272f6fe6c805067aede0ab
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84280773"
---
# <a name="abstract-class-design"></a>抽象類別設計

❌請勿在抽象類別型中定義公用或受保護的內部函式。

 只有當使用者需要建立類型的實例時，才應該公開公用函式。 因為您無法建立抽象類別型的實例，所以具有公用函式的抽象類別型設計不正確，而且會誤導使用者。

 ✔️確實在抽象類別中定義受保護或內部的函式。

 受保護的函式較常見，只允許基類在建立子類型時執行自己的初始化。

 內部的函式可以用來將抽象類別的具體執行限制為定義類別的元件。

 ✔️確實提供了一個從您出貨之每個抽象類別繼承的具體型別。

 這麼做有助於驗證抽象類別的設計。 例如， <xref:System.IO.FileStream?displayProperty=nameWithType> 是 <xref:System.IO.Stream?displayProperty=nameWithType> 抽象類別的執行。

 *部分©2005、2009 Microsoft Corporation。已保留擁有權限。*

 獲 Pearson Education, Inc. 的授權再版，從 Krzysztof Cwalina 和 Brad Abrams 撰寫，並在 2008 年 10 月 22 日由 Addison-Wesley Professional 出版，作為 Microsoft Windows Development Series 一部份的 [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 節錄。**

## <a name="see-also"></a>另請參閱

- [類型設計方針](type.md)
- [架構設計方針](index.md)
