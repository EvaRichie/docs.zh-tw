---
title: 如何：在執行階段使用 C# 讀取設定
description: '瞭解如何透過 Properties 物件，在執行時間使用 c # 讀取應用程式範圍和使用者範圍的設定。'
ms.date: 03/30/2017
helpviewer_keywords:
- application settings [Windows Forms], reading
- application settings [Windows Forms], run time
- application settings [Windows Forms], C#
ms.assetid: dbe8bf09-5e1c-49da-9192-154033d7240b
ms.openlocfilehash: d784544e018bb693c501e35ea36fcae1946ef5eb
ms.sourcegitcommit: 3824ff187947572b274b9715b60c11269335c181
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84903347"
---
# <a name="how-to-read-settings-at-run-time-with-c"></a>如何：在執行時間使用 C 讀取設定\#

您可以在執行階段透過屬性物件來讀取應用程式範圍和使用者範圍的設定。 Properties 物件會透過其定義所在之專案的預設命名空間中的屬性，來公開專案的所有預設設定。  
  
## <a name="to-read-settings-at-run-time-with-c"></a>若要在執行時間使用 C 讀取設定\#
  
透過 Properties.Settings.Default 成員存取適當的設定。 下列範例示範如何指派名為 `myColor` 的設定給 BackColor 屬性。 它會要求您具有先前建立的設定檔，其中包含 `System.Drawing.Color` 類型之名為 `myColor` 的設定。 如需建立設定檔的相關資訊，請參閱[如何：在設計階段建立新設定](how-to-create-a-new-setting-at-design-time.md)。  
  
```csharp
this.BackColor = Properties.Settings.Default.myColor;  
```  
  
## <a name="see-also"></a>另請參閱

- [使用應用程式設定和使用者設定](using-application-settings-and-user-settings.md)
- [操作說明：在執行階段使用 C# 撰寫使用者設定](how-to-write-user-settings-at-run-time-with-csharp.md)
- [應用程式設定總覽](application-settings-overview.md)
