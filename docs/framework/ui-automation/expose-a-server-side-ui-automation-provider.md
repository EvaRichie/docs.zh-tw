---
title: 公開伺服器端 UI 自動化提供者
description: 查看示範如何公開裝載于 [系統管理] 視窗中之伺服器端消費者介面自動化提供者的範例。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- expose a server-side UI Automation provider
- UI Automation, server-side provider, exposing
- server-side UI Automation provider, exposing
ms.assetid: 55d419c0-2201-4101-90c9-2888df4dbb47
ms.openlocfilehash: be39130c7a91fc081256bf14a87f503d27f45129
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96276525"
---
# <a name="expose-a-server-side-ui-automation-provider"></a>公開伺服器端 UI 自動化提供者

> [!NOTE]
> 這份文件適用於想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空間中定義之 Managed <xref:System.Windows.Automation> 類別的 .NET Framework 開發人員。 如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新資訊，請參閱 [Windows Automation API：UI 自動化](/windows/win32/winauto/entry-uiauto-win32)。  
  
 本主題包含範例程式碼，顯示如何公開裝載在 <xref:System.Windows.Forms.Control?displayProperty=nameWithType> 視窗中的伺服器端使用者介面自動化提供者。  
  
 這段程式碼會覆寫視窗程序，在用戶端應用程式要求視窗相關資訊時，截取 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 核心服務所傳送的訊息 WM_GETOBJECT。  
  
## <a name="example"></a>範例  

 [!code-csharp[UIAFragmentProvider_snip#116](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAFragmentProvider_snip/CSharp/ListFragment.cs#116)]
 [!code-vb[UIAFragmentProvider_snip#116](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAFragmentProvider_snip/VisualBasic/ListFragment.vb#116)]  
  
## <a name="see-also"></a>另請參閱

- [UI 自動化提供者概觀](ui-automation-providers-overview.md)
- [伺服器端 UI 自動化提供者實作](server-side-ui-automation-provider-implementation.md)
