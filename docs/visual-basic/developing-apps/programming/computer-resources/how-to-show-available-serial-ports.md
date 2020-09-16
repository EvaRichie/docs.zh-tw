---
title: 作法：顯示可用的序列埠
ms.date: 07/20/2015
helpviewer_keywords:
- serial ports, availability
- My.Computer.Ports.SerialPortNames property
- My.Computer.Ports object
- ports, serial port availability
ms.assetid: eaf2ee5a-8103-4e10-a205-ed1d4db120ba
ms.openlocfilehash: b19bdd56311ab7029fb224256d138a0dc0dd8ddc
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90557342"
---
# <a name="how-to-show-available-serial-ports-in-visual-basic"></a>如何：在 Visual Basic 中顯示可用的序列埠

本主題描述如何在 Visual Basic 中使用 `My.Computer.Ports` 來顯示電腦的可用序列埠。  
  
 為了允許使用者選取所要使用的序列埠，序列埠的名稱放在 <xref:System.Windows.Forms.ListBox> 控制項中。  
  
## <a name="example"></a>範例  

 此範例會針對 `My.Computer.Ports.SerialPortNames` 屬性傳回的所有字串執行迴圈。 這些字串是電腦上可用序列埠的名稱。  
  
 一般而言，使用者會從可用的序列埠清單中，選取應用程式應該使用的序列埠。 在這個範例中，序列埠名稱會儲存在 <xref:System.Windows.Forms.ListBox> 控制項中。 如需詳細資訊，請參閱 [ListBox 控制項](/dotnet/desktop/winforms/controls/listbox-control-windows-forms)。  
  
 [!code-vb[VbVbalrMyComputer#45](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyComputer/VB/Class2.vb#45)]  
  
 這個程式碼範例也可用為 IntelliSense 程式碼片段。 在程式碼片段選擇器中，該程式碼片段會位於 [連接和網路] 中。**** 如需詳細資訊，請參閱[程式碼片段](/visualstudio/ide/code-snippets)。  
  
## <a name="compiling-the-code"></a>編譯程式碼  

 這個範例需要：  
  
- System.Windows.Forms.dll 的專案參考。  
  
- <xref:System.Windows.Forms> 命名空間成員的存取權。 新增 `Imports` 陳述式 (如果未在程式碼中完整限定成員名稱)。 如需詳細資訊，請參閱 [Imports 陳述式 (.NET 命名空間和類型)](../../../language-reference/statements/imports-statement-net-namespace-and-type.md)。  
  
- 您的表單會有名為 `ListBox1` 的 <xref:System.Windows.Forms.ListBox> 控制項。  
  
## <a name="robust-programming"></a>穩固程式設計  

 您不一定要使用 <xref:System.Windows.Forms.ListBox> 控制項來顯示可用的序列埠名稱。 相反地，您可以使用 <xref:System.Windows.Forms.ComboBox> 或其他控制項。 如果應用程式不需要使用者的回應，您還可以使用 <xref:System.Windows.Forms.TextBox> 控制項來顯示資訊。  
  
> [!NOTE]
> 在 Windows 98 上執行時，`My.Computer.Ports.SerialPortNames` 所傳回的序列埠名稱可能不正確。 為了避免應用程式錯誤，請在使用序列埠名稱開啟序列埠時，使用例外狀況處理，例如 `Try...Catch...Finally` 陳述式或 `Using` 陳述式。  
  
## <a name="see-also"></a>另請參閱

- <xref:Microsoft.VisualBasic.Devices.Ports>
- [作法：撥接與序列埠連接的數據機](how-to-dial-modems-attached-to-serial-ports.md)
- [作法：將字串傳送至序列埠](how-to-send-strings-to-serial-ports.md)
- [作法：接收來自序列埠的字串](how-to-receive-strings-from-serial-ports.md)
