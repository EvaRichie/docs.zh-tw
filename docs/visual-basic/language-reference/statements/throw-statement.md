---
title: Throw 陳述式
ms.date: 07/20/2015
f1_keywords:
- vb.Throw
helpviewer_keywords:
- structured exception handling, throw statements
- try-catch exception handling, throw statements
- throw statement [Visual Basic], about throw statements
- throwing exceptions, throw statement
- exception handling, throw statement
- On Error statement [Visual Basic], throwing exceptions
- throwing exceptions
- exception handling, unstructured
- throw statement [Visual Basic]
ms.assetid: a6e07406-5c8a-4498-87a2-8339f3651d62
ms.openlocfilehash: 95572b1739490e90f53da6b6ec283bfb532c46d3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404131"
---
# <a name="throw-statement-visual-basic"></a>Throw 陳述式 (Visual Basic)

在程式中擲回例外狀況。

## <a name="syntax"></a>語法

```vb
Throw [ expression ]
```

## <a name="part"></a>部分

`expression`\
提供要擲回之例外狀況的相關資訊。 如果位於 `Catch` 語句中，則為選擇性，否則為必要項。

## <a name="remarks"></a>備註

`Throw`語句會擲回例外狀況，您可以處理結構化例外狀況處理常式代碼（ `Try` ... `Catch`...`Finally`)或非結構化例外狀況處理常式代碼（ `On Error GoTo` ）。 您可以使用 `Throw` 語句來攔截程式碼內的錯誤，因為 Visual Basic 會向上移動呼叫堆疊，直到找到適當的例外狀況處理常式代碼為止。

`Throw`沒有運算式的語句只能在語句中使用 `Catch` ，在此情況下，語句會重新擲回目前正由語句處理的例外狀況 `Catch` 。

`Throw`語句會重設例外狀況的呼叫堆疊 `expression` 。 如果 `expression` 未提供，則會將呼叫堆疊保持不變。 您可以透過屬性存取例外狀況的呼叫堆疊 <xref:System.Exception.StackTrace%2A> 。

## <a name="example"></a>範例

下列程式碼會使用 `Throw` 語句來擲回例外狀況：

[!code-vb[VbVbalrStatements#84](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#84)]

## <a name="see-also"></a>另請參閱

- [Try...Catch...Finally 陳述式](try-catch-finally-statement.md)
- [On Error 陳述式](on-error-statement.md)
