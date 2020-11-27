---
title: 建立用戶端 UI 自動化提供者
description: 觀看如何建立用戶端消費者介面自動化提供者的範例。 此範例會為主控台視窗執行簡單的用戶端提供者。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- UI Automation, creating client-side provider
- client-side UI Automation provider, creating
ms.assetid: d91edaf2-be28-41ec-a508-af421cb43c3d
ms.openlocfilehash: 17a6deca2efc67d1409e89f7accf7a3b89a27807
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96276538"
---
# <a name="create-a-client-side-ui-automation-provider"></a>建立用戶端 UI 自動化提供者

> [!NOTE]
> 這份文件適用於想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空間中定義之 Managed <xref:System.Windows.Automation> 類別的 .NET Framework 開發人員。 如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新資訊，請參閱 [Windows Automation API：UI 自動化](/windows/win32/winauto/entry-uiauto-win32)。  
  
 本主題包含範例程式碼，說明如何實作用戶端的使用者介面自動化提供者。  
  
## <a name="example"></a>範例  

 下列範例程式碼可以內建于動態連結程式庫 (DLL) ，以針對主控台視窗執行非常簡單的用戶端提供者。 這個程式碼並沒有任何實際用途，只是用來示範設定提供者組件的基本步驟 (這個組件可由使用者介面自動化用戶端應用程式註冊)。  
  
 [!code-csharp[UIAClientSideProvider_snip#101](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClientSideProvider_snip/CSharp/CSProviderProgram.cs#101)]
 [!code-vb[UIAClientSideProvider_snip#101](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClientSideProvider_snip/visualbasic/csproviderprogram.vb#101)]  
  
## <a name="see-also"></a>另請參閱

- [UI 自動化提供者概觀](ui-automation-providers-overview.md)
- [註冊用戶端提供者組件](register-a-client-side-provider-assembly.md)
