---
title: 如何：建立使用者定義的例外狀況
description: 瞭解如何建立使用者定義的例外狀況，這是從 .NET 中的例外狀況基類衍生的例外狀況類別階層的替代方法。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- user-defined exceptions
- exceptions, examples
- exceptions, user-defined
ms.assetid: 25819a5a-f915-4fc8-b924-a76915674e04
ms.openlocfilehash: b0a8549c9bacf322a0685c7b505185ab1d1101f6
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94828123"
---
# <a name="how-to-create-user-defined-exceptions"></a>如何建立使用者定義的例外狀況

.NET 提供基本上衍生自基底類別 <xref:System.Exception> 之例外狀況類別的階層架構。 不過，如果沒有預先定義的例外狀況符合您的需求，您可以藉由衍生自 <xref:System.Exception> 類別，建立您自己的例外狀況類別。

建立您自己的例外狀況時，請以文字 "Exception" 作為使用者定義例外狀況類別名稱的結尾，並實作三種常見的建構函式，如下列範例所示。 此範例會定義名為 `EmployeeListNotFoundException` 的新例外狀況類別。 此類別衍生自 <xref:System.Exception>，包含三個建構函式。

[!code-cpp[dg_exceptionDesign#14](../../../samples/snippets/cpp/VS_Snippets_CLR/dg_exceptionDesign/cpp/example2.cpp#14)]
[!code-csharp[dg_exceptionDesign#14](../../../samples/snippets/csharp/VS_Snippets_CLR/dg_exceptionDesign/cs/example2.cs#14)]
[!code-vb[dg_exceptionDesign#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/dg_exceptionDesign/vb/example2.vb#14)]  

> [!NOTE]
> 在您使用遠端功能的情況下，您必須確定任何使用者定義例外狀況的中繼資料是由伺服器 (被呼叫端) 提供，並提供給用戶端 (Proxy 物件或呼叫端)。 如需詳細資訊，請參閱[例外狀況的最佳做法](best-practices-for-exceptions.md)。

## <a name="see-also"></a>請參閱

- [例外狀況](index.md)
