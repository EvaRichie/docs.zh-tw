---
title: RemoveHandler 陳述式
ms.date: 07/20/2015
f1_keywords:
- vb.RemoveHandlerMethod
- vb.RemoveHandler
- RemoveHandler
helpviewer_keywords:
- RemoveHandler keyword [Visual Basic]
- RemoveHandler statement [Visual Basic]
ms.assetid: 647cd825-e877-4910-b4f1-8d168beebe6a
ms.openlocfilehash: 3514a79f2430b148e6a3727b83029b4e207a677b
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404248"
---
# <a name="removehandler-statement"></a>RemoveHandler 陳述式
移除事件與事件處理常式之間的關聯。  
  
## <a name="syntax"></a>語法  
  
```vb  
RemoveHandler event, AddressOf eventhandler  
```  
  
## <a name="parts"></a>組件  
  
|詞彙|定義|  
|---|---|  
|`event`|正在處理的事件名稱。|  
|`eventhandler`|目前處理事件的程式名稱。|  
  
## <a name="remarks"></a>備註  
 `AddHandler`和 `RemoveHandler` 語句可讓您在程式執行期間的任何時間，啟動和停止特定事件的事件處理。  
  
> [!NOTE]
> 若為自訂事件，語句會叫用 `RemoveHandler` 事件的 `RemoveHandler` 存取子。 如需自訂事件的詳細資訊，請參閱[Event 語句](event-statement.md)。  
  
## <a name="example"></a>範例  
 [!code-vb[VbVbalrEvents#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#17)]  
  
## <a name="see-also"></a>另請參閱

- [AddHandler 陳述式](addhandler-statement.md)
- [控制代碼](handles-clause.md)
- [Event 陳述式](event-statement.md)
- [事件](../../programming-guide/language-features/events/index.md)
