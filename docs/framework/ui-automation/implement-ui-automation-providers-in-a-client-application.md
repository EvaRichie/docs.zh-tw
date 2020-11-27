---
title: 在用戶端應用程式中實作 UI 自動化提供者
description: 請參閱如何在應用程式中執行用戶端消費者介面自動化提供者的範例。 請注意，這是不常見的情況。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- client-side UI Automation provider, implementation within applications
- UI Automation, implementing client-side provider within application
ms.assetid: f325f0d8-1715-41ea-85ca-45b82ffea8bc
ms.openlocfilehash: 486e05f9080b686c48454dfcfceaaa666fa57f67
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96269583"
---
# <a name="implement-ui-automation-providers-in-a-client-application"></a>在用戶端應用程式中實作 UI 自動化提供者

> [!NOTE]
> 這份文件適用於想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空間中定義之 Managed <xref:System.Windows.Automation> 類別的 .NET Framework 開發人員。 如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新資訊，請參閱 [Windows Automation API：UI 自動化](/windows/win32/winauto/entry-uiauto-win32)。  
  
 本主題包含範例程式碼，說明如何在應用程式內實作用戶端的使用者介面自動化提供者。  
  
 這個情況較不常見。 通常，使用者介面自動化用戶端應用程式會使用伺服器端提供者，或位於 DLL 中的用戶端提供者。  
  
## <a name="example"></a>範例  

 下列範例程式碼會實作簡單的主控台視窗提供者。 這個程式碼並沒有太大的功用，只是用來展示在用戶端程式碼中設定提供者，以及使用 <xref:System.Windows.Automation.ClientSettings.RegisterClientSideProviders%2A>註冊的基本步驟。  
  
 [!code-csharp[UIAClientSideProvider_snip#201](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClientSideProvider_snip/CSharp/ClientImplementationProgram.cs#201)]
 [!code-vb[UIAClientSideProvider_snip#201](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClientSideProvider_snip/visualbasic/clientimplementationprogram.vb#201)]  
  
## <a name="see-also"></a>另請參閱

- [UI 自動化提供者概觀](ui-automation-providers-overview.md)
- [註冊用戶端提供者組件](register-a-client-side-provider-assembly.md)
- [建立用戶端 UI 自動化提供者](create-a-client-side-ui-automation-provider.md)
- [用戶端 UI 自動化提供者實作](client-side-ui-automation-provider-implementation.md)
