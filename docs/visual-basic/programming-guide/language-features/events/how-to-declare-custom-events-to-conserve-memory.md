---
title: 如何：宣告自訂事件以節省記憶體
ms.date: 07/20/2015
helpviewer_keywords:
- declaring events [Visual Basic], custom
- events [Visual Basic], custom
- custom events [Visual Basic]
ms.assetid: 87ebee87-260c-462f-979c-407874debd19
ms.openlocfilehash: c9a049d3f15d5620152f064888a97bd0be5d46b0
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84405127"
---
# <a name="how-to-declare-custom-events-to-conserve-memory-visual-basic"></a>如何：宣告自訂事件以節省記憶體 (Visual Basic)
在幾種情況下，應用程式將其記憶體使用量保持在較低的情況是很重要的。 自訂事件可讓應用程式僅針對它所處理的事件使用記憶體。  
  
 根據預設，當類別宣告事件時，編譯器會為欄位配置記憶體來儲存事件資訊。 如果類別有許多未使用的事件，它們就會不必要地佔用記憶體。  
  
 您可以使用自訂事件，更仔細地管理記憶體使用量，而不是使用 Visual Basic 所提供的預設事件執行。  
  
## <a name="example"></a>範例  
 在此範例中，類別會使用 <xref:System.ComponentModel.EventHandlerList> 儲存在欄位中的一個類別實例， `Events` 來儲存所使用之事件的相關資訊。 <xref:System.ComponentModel.EventHandlerList>類別是設計用來保存委派的優化清單類別。  
  
 類別中的所有事件都會使用 `Events` 欄位來追蹤哪些方法正在處理每個事件。  
  
 [!code-vb[VbVbalrEvents#22](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#22)]  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ComponentModel.EventHandlerList>
- [事件](index.md)
- [如何：宣告自訂事件以避免封鎖](how-to-declare-custom-events-to-avoid-blocking.md)
