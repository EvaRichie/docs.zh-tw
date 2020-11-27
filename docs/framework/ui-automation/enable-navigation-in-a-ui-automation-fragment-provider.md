---
title: 在 UI 自動化片段提供者中啟用巡覽
description: 閱讀示範如何在消費者介面自動化提供者中為片段內的元素啟用導覽的範例。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- UI Automation, enabling navigation in provider
- navigation, enabling in UI Automation provider
ms.assetid: 3cb6092a-58c9-4ca0-84a5-0e54d5d00a0d
ms.openlocfilehash: d8fb67a84b7cba84fe65cd2f87baa6549122d2a2
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96276499"
---
# <a name="enable-navigation-in-a-ui-automation-fragment-provider"></a>在 UI 自動化片段提供者中啟用巡覽

> [!NOTE]
> 這份文件適用於想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空間中定義之 Managed <xref:System.Windows.Automation> 類別的 .NET Framework 開發人員。 如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新資訊，請參閱 [Windows Automation API：UI 自動化](/windows/win32/winauto/entry-uiauto-win32)。  
  
 本主題包含範例程式碼，顯示如何針對片段內的項目，在使用者介面自動化提供者中啟用巡覽。  
  
## <a name="example"></a>範例  

 下列範例程式碼針對清單內的清單項目實作 <xref:System.Windows.Automation.Provider.IRawElementProviderFragment.Navigate%2A> 。 父項目是清單方塊項目，同層級項目則是清單集合中的其他項目。 針對無效的方向，此方法會傳回 `null` (在 Visual Basic 中為`Nothing` )；在這個案例中，因為項目沒有子系，所以會傳回 <xref:System.Windows.Automation.Provider.NavigateDirection.FirstChild> 和 <xref:System.Windows.Automation.Provider.NavigateDirection.LastChild>。  
  
 [!code-csharp[UIAFragmentProvider_snip#103](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAFragmentProvider_snip/CSharp/ListItemFragment.cs#103)]
 [!code-vb[UIAFragmentProvider_snip#103](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAFragmentProvider_snip/VisualBasic/ListItemFragment.vb#103)]  
  
## <a name="see-also"></a>另請參閱

- [UI 自動化提供者概觀](ui-automation-providers-overview.md)
- [伺服器端 UI 自動化提供者實作](server-side-ui-automation-provider-implementation.md)
