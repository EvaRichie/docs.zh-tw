---
title: 如何：在背景執行作業
description: 瞭解如何使用 BackgroundWorker 類別，在背景中執行耗時的 Windows Forms 作業。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- background tasks
- forms [Windows Forms], multithreading
- forms [Windows Forms], background operations
- background threads
- BackgroundWorker class [Windows Forms], examples
- threading [Windows Forms], background operations
- background operations
ms.assetid: 5b56e2aa-dc05-444f-930c-2d7b23f9ad5b
ms.openlocfilehash: 6b2a97f5acf1e906dfe141aee62e99a4e50dca9f
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621570"
---
# <a name="how-to-run-an-operation-in-the-background"></a>如何：在背景執行作業
如果您有要花費較長時間才能完成的作業，但您不想導致使用者介面發生延遲，就可以使用 <xref:System.ComponentModel.BackgroundWorker> 類別在另一個執行緒上執行該作業。  
  
 下列程式碼範例示範如何在背景執行耗時的作業。 表單具有 [開始]**** 和 [取消]**** 按鈕。 按一下 [開始]**** 按鈕以執行非同步作業。 按一下 [取消]**** 按鈕以停止執行中的非同步作業。 每個作業的結果會顯示於 <xref:System.Windows.Forms.MessageBox>。  
  
 在 Visual Studio 中對於本工作有更詳盡的支援。  
  
 另請參閱[逐步解說：在背景執行作業](walkthrough-running-an-operation-in-the-background.md)。  
  
## <a name="example"></a>範例  
 [!code-csharp[System.ComponentModel.BackgroundWorker.Example#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/CS/Form1.cs#1)]
 [!code-vb[System.ComponentModel.BackgroundWorker.Example#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/VB/Form1.vb#1)]  
  
## <a name="compiling-the-code"></a>編譯程式碼  
 這個範例需要：  
  
- System、System.Drawing 和 System.Windows.Forms 組件的參考。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ComponentModel.BackgroundWorker>
- <xref:System.ComponentModel.DoWorkEventArgs>
- [操作說明：實作使用背景作業的表單](how-to-implement-a-form-that-uses-a-background-operation.md)
- [BackgroundWorker 元件](backgroundworker-component.md)
