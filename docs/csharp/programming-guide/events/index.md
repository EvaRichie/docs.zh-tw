---
title: 事件 - C# 程式設計手冊
description: 瞭解事件。 事件可讓類別或物件在某些相關的事情發生時，告知其他類別或物件。
ms.date: 07/20/2015
helpviewer_keywords:
- classes [C#], events
- C# language, events
- events [C#]
ms.assetid: a8e51b22-d294-44fb-9539-0072f06c4cb3
ms.openlocfilehash: f56de15dd2c7b0a10e40a886dbd82a4147a03014
ms.sourcegitcommit: e7acba36517134238065e4d50bb4a1cfe47ebd06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2020
ms.locfileid: "89466153"
---
# <a name="events-c-programming-guide"></a>事件 (C# 程式設計手冊)
事件可讓 [類別](../../language-reference/keywords/class.md) 或物件在某些相關的事情發生時，告知其他類別或物件。 傳送 (或 *引發*) 事件的類別稱為「 *發行者* 」，以及接收 (或 *處理*) 事件的類別，稱為「 *訂閱者*」。  
  
在典型的 C# Windows Forms 或 Web 應用程式中，您可訂閱由控制項 (如按鈕和清單方塊) 引發的事件。 您可以使用 Visual C# 整合式開發環境 (IDE) 來瀏覽控制項發行的事件，並選擇您想要處理的事件。 IDE 提供一種簡單的方式來自動新增空的事件處理常式方法，及用來訂閱該事件的程式碼。 如需詳細資訊，請參閱 [如何訂閱和取消訂閱事件](./how-to-subscribe-to-and-unsubscribe-from-events.md)。
  
## <a name="events-overview"></a>事件概觀  
 事件有下列屬性：  
  
- 發行者會判斷引發事件的時間，而訂閱者則決定要採取什麼動作來回應該事件。  
  
- 一個事件可以有多個訂閱者， 而訂閱者可以處理來自多個發行者的多個事件。  
  
- 沒有訂閱者的事件永遠不會被引發。  
  
- 事件通常用於對使用者的動作 (例如在圖形化使用者介面內按一下按鈕或選取功能表) 發出信號。  
  
- 當某事件擁有多個訂閱者時，便會在事件引發的同時叫用事件處理常式。 若要以非同步方式叫用事件，請參閱 [Calling Synchronous Methods Asynchronously](../../../standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously.md)。  
  
- 在 .NET 類別庫中，事件是以 <xref:System.EventHandler> 委派和基類為基礎 <xref:System.EventArgs> 。  
  
## <a name="related-sections"></a>相關章節  
 如需詳細資訊，請參閱：  
  
- [如何訂閱及取消訂閱事件](./how-to-subscribe-to-and-unsubscribe-from-events.md)

- [如何發佈符合 .NET 指導方針的事件](./how-to-publish-events-that-conform-to-net-framework-guidelines.md)

- [如何在衍生類別中引發基底類別事件](./how-to-raise-base-class-events-in-derived-classes.md)

- [如何實作介面事件](./how-to-implement-interface-events.md)

- [如何實作自訂事件存取子](./how-to-implement-custom-event-accessors.md)

## <a name="c-language-specification"></a>C# 語言規格  

如需詳細資訊，請參閱 [C# 語言規格](/dotnet/csharp/language-reference/language-specification/introduction)中的[事件](~/_csharplang/spec/classes.md#events)。 語言規格是 C# 語法及用法的限定來源。
  
## <a name="featured-book-chapters"></a>精選書籍章節  
 [C# 3.0 Cookbook, Third Edition: More than 250 solutions for C# 3.0 programmers](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/ff518994%28v=orm.10%29) (C# 3.0 Cookbook 第三版：250 個以上 C# 3.0 程式設計人員適用的方案) 中的 [Delegates, Events, and Lambda Expressions](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/ff518995%28v=orm.10%29)  
  
 [Delegates and Events](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/ff652490%28v=orm.10%29) in [Learning C# 3.0: Master the fundamentals of C# 3.0](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/ff652493%28v=orm.10%29)  
  
## <a name="see-also"></a>另請參閱

- <xref:System.EventHandler>
- [C # 程式設計指南](../index.md)
- [委派](../delegates/index.md)
- [在 Windows Form 中建立事件處理常式](../../../framework/winforms/creating-event-handlers-in-windows-forms.md)
