---
title: 由於內部錯誤，無法取得記憶體資訊
ms.date: 07/20/2015
f1_keywords:
- vbrDiagnosticInfo_Memory
ms.assetid: 1ba8f774-5858-438e-914e-99fddc9e5e7e
ms.openlocfilehash: 550ac0345d54c8a78e805b224ffaba47a3970ea9
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91076275"
---
# <a name="could-not-obtain-memory-information-due-to-internal-error"></a>由於內部錯誤，無法取得記憶體資訊

呼叫 `My.Computer.Info` 物件的其中一個記憶體資訊屬性失敗。  
  
## <a name="to-correct-this-error"></a>更正這個錯誤  
  
- 在 `Try...Catch` 物件之記憶體資訊屬性的呼叫周圍加入 `My.Computer.Info` 區塊。  
  
## <a name="see-also"></a>另請參閱

- [My.Computer.Info](xref:Microsoft.VisualBasic.Devices.ComputerInfo)
- [Try...Catch...Finally 陳述式](../language-reference/statements/try-catch-finally-statement.md)
