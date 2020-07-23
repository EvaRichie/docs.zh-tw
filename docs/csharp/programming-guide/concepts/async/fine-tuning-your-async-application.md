---
title: 微調非同步應用程式 (C#)
description: '這些 c # 範例會使用 CancellationToken 和重要的工作方法（例如 System.threading.tasks.task.whenall 和 System.threading.tasks.task.whenany）來微調非同步應用程式。'
ms.date: 07/20/2015
ms.assetid: 97696eb9-81fc-4940-9655-84daa8eb4d5c
ms.openlocfilehash: 46457f889a78932e306d2bd21dca666625d744eb
ms.sourcegitcommit: 40de8df14289e1e05b40d6e5c1daabd3c286d70c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86925315"
---
# <a name="fine-tuning-your-async-application-c"></a>微調非同步應用程式 (C#)
您可以使用 <xref:System.Threading.Tasks.Task> 類型所提供的方法和屬性，來增加非同步應用程式的精確度和彈性。 本節的主題會示範使用 <xref:System.Threading.CancellationToken> 以及 <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> 和 <xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=nameWithType> 等重要 `Task` 方法的範例。  
  
 您可以使用 `WhenAny` 和 `WhenAll`，更輕鬆地啟動多個工作，並藉由監視單一工作等候其完成。  
  
- `WhenAny` 會在集合中的任何工作完成時，傳回一個完成的工作。  
  
     如需使用 `WhenAny` 的範例，請參閱[當其中一項工作完成時，取消剩餘的非同步工作 (C#)](./cancel-remaining-async-tasks-after-one-is-complete.md) 和[啟動多項非同步工作並在它們完成時進行處理 (C#)](./start-multiple-async-tasks-and-process-them-as-they-complete.md)。  
  
- `WhenAll` 會在集合中的所有工作完成時，傳回一個完成的工作。  
  
     如需詳細資訊和使用的範例 `WhenAll` ，請參閱[如何使用 system.threading.tasks.task.whenall 擴充非同步逐步解說（c #）](./how-to-extend-the-async-walkthrough-by-using-task-whenall.md)。
  
 本節包含下列範例。  
  
- [取消一項非同步工作或工作清單（c #）](./cancel-an-async-task-or-a-list-of-tasks.md)。  
  
- [在一段時間後取消非同步工作（c #）](./cancel-async-tasks-after-a-period-of-time.md)  
  
- [當其中一項工作完成時，取消剩餘的非同步工作 (C#)](./cancel-remaining-async-tasks-after-one-is-complete.md)  
  
- [啟動多項非同步工作並在它們完成時進行處理 (C#)](./start-multiple-async-tasks-and-process-them-as-they-complete.md)  
  
> [!NOTE]
> 若要執行範例，您必須在電腦上安裝 Visual Studio 2012 或更新版本以及 .NET Framework 4.5 或更新版本。  
  
 這些專案會建立 UI，其中包含一個啟動處理序的按鈕和一個取消處理序的按鈕，如下圖所示。 這兩個按鈕的名稱分別是 `startButton` 和 `cancelButton`。  
  
 ![具有 [取消] 按鈕的 WPF 視窗](./media/fine-tuning-your-async-application/cancellation-and-start-button.png "具有 [開始] 和 [停止] 按鈕的對話方塊")  
  
 您可以從 [Async Sample: Fine Tuning Your Application](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea) (非同步範例：微調應用程式) 下載完整 Windows Presentation Foundation (WPF) 專案。  
  
## <a name="see-also"></a>另請參閱

- [使用 Async 和 Await 進行非同步程式設計 (C#)](./index.md)
