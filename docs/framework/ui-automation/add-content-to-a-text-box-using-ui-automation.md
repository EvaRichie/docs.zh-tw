---
title: 使用 UI 自動化將內容加入至文字方塊
description: 請參閱範例，以瞭解如何在 .NET 中使用 Microsoft UI 自動化，將內容新增至單一行文字方塊。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- adding content to text boxes
- text boxes, adding content
- UI Automation, adding content to text boxes
ms.assetid: 8bdd1a73-1ecb-4a05-a891-a7827ebb767f
ms.openlocfilehash: 4136d460de7091a515580cade16f06e54699727a
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87166908"
---
# <a name="add-content-to-a-text-box-using-ui-automation"></a>使用 UI 自動化將內容加入至文字方塊
> [!NOTE]
> 這份文件適用於想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空間中定義之 Managed <xref:System.Windows.Automation> 類別的 .NET Framework 開發人員。 如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新資訊，請參閱 [Windows Automation API：UI 自動化](/windows/win32/winauto/entry-uiauto-win32)。  
  
 本主題包含範例程式碼，示範如何使用 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 將文字插入單行文字方塊。 另一種方法是針對不適用的多行和 rtf 文字控制項提供 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 。 為了進行比較，此範例也會示範如何使用 Win32 方法來完成相同的結果。  
  
## <a name="example"></a>範例  
 下列範例會逐步解說目標應用程式中的一連串文字控制項。 測試每個文字控制項，以查看是否 <xref:System.Windows.Automation.ValuePattern> 可以使用方法從它取得物件 <xref:System.Windows.Automation.AutomationElement.TryGetCurrentPattern%2A> 。 如果文字控制項支援 <xref:System.Windows.Automation.ValuePattern> ，則 <xref:System.Windows.Automation.ValuePattern.SetValue%2A> 會使用方法將使用者定義的字串插入至文字控制項。 否則， <xref:System.Windows.Forms.SendKeys.SendWait%2A?displayProperty=nameWithType> 會使用方法。  
  
 [!code-csharp[InsertText#InsertText](../../../samples/snippets/csharp/VS_Snippets_Wpf/InsertText/CSharp/Window1.xaml.cs#inserttext)]
 [!code-vb[InsertText#InsertText](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/InsertText/VisualBasic/Window1.xaml.vb#inserttext)]  
  
## <a name="see-also"></a>另請參閱

- [TextPattern 插入文字範例](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms771478(v=vs.90))
