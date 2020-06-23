---
title: 作法：處理表單層級的鍵盤輸入
description: 瞭解如何在訊息到達控制項之前，在表單層級處理 Windows Forms 的鍵盤輸入。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- keyboard input [Windows Forms], at form level
- Windows Forms, handling keyboard input
- keyboards [Windows Forms], form-level input
ms.assetid: d7f8b390-dc91-42d2-ae0f-2ffa388127ad
ms.openlocfilehash: 6f0695b6f665a613e0e4e001a4f9bbfc09dd45ed
ms.sourcegitcommit: 3824ff187947572b274b9715b60c11269335c181
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84904152"
---
# <a name="how-to-handle-keyboard-input-at-the-form-level"></a>作法：處理表單層級的鍵盤輸入
在訊息到達控制項之前，Windows Form 提供在表單層級處理鍵盤訊息的能力。 本主題將示範如何完成這些工作。  
  
### <a name="to-handle-a-keyboard-message-at-the-form-level"></a>處理表單層級的鍵盤訊息  
  
- 處理啟動表單的 <xref:System.Windows.Forms.Control.KeyPress> 或 <xref:System.Windows.Forms.Control.KeyDown> 事件，並將表單的 <xref:System.Windows.Forms.Form.KeyPreview%2A> 屬性設為 `true`，讓鍵盤訊息到達表單上的任何控制項之前先由表單所接收。 下列程式碼範例會偵測所有數字鍵並使用 '1'、'4' 和 '7' 來處理 <xref:System.Windows.Forms.Control.KeyPress> 事件。  
  
     [!code-cpp[System.Windows.Forms.KeyboardInputForm#10](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInputForm/cpp/form1.cpp#10)]
     [!code-csharp[System.Windows.Forms.KeyboardInputForm#10](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInputForm/CS/form1.cs#10)]
     [!code-vb[System.Windows.Forms.KeyboardInputForm#10](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInputForm/VB/form1.vb#10)]  
  
## <a name="example"></a>範例  
 下列程式碼範例是上述程式碼範例的完整應用。 此應用程式包括 <xref:System.Windows.Forms.TextBox> 以及數個其他控制項，可讓您將焦點從 <xref:System.Windows.Forms.TextBox> 移動。 當顯示剩餘的按鍵時，主要 <xref:System.Windows.Forms.Form> 的 <xref:System.Windows.Forms.Control.KeyPress> 事件會使用 '1'、'4' 和 '7' ，而 <xref:System.Windows.Forms.TextBox> 的 <xref:System.Windows.Forms.Control.KeyPress> 事件會使用 '2'、'5' 和 '8'。 當您按數字鍵時的焦點是其他控制項的其中一個時，<xref:System.Windows.Forms.TextBox> 具有 <xref:System.Windows.Forms.MessageBox> 輸出的焦點，此時您按下數字鍵，請比較 <xref:System.Windows.Forms.MessageBox> 輸出。  
  
 [!code-cpp[System.Windows.Forms.KeyBoardInputForm#0](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInputForm/cpp/form1.cpp#0)]
 [!code-csharp[System.Windows.Forms.KeyBoardInputForm#0](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInputForm/CS/form1.cs#0)]
 [!code-vb[System.Windows.Forms.KeyBoardInputForm#0](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInputForm/VB/form1.vb#0)]  
  
## <a name="compiling-the-code"></a>編譯程式碼  
 這個範例需要：  
  
- System、System.Drawing 和 System.Windows.Forms 組件的參考。  
  
## <a name="see-also"></a>另請參閱

- [Windows Forms 應用程式中的鍵盤輸入](keyboard-input-in-a-windows-forms-application.md)
