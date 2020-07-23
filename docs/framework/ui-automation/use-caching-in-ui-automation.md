---
title: 使用 UI 自動化中的快取
description: 請參閱如何在 UI 自動化中使用快取。 檢查啟動快取要求、快取 AutomationElement 屬性和取得快取模式的步驟。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- caching, UI Automation
- UI Automation, caching
ms.assetid: ec722dff-6009-4279-b86a-e18d3fa94ebf
ms.openlocfilehash: 8dff9db77e39dc66a16b6a7b395c76a3c768d48e
ms.sourcegitcommit: 40de8df14289e1e05b40d6e5c1daabd3c286d70c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86924483"
---
# <a name="use-caching-in-ui-automation"></a>使用 UI 自動化中的快取
> [!NOTE]
> 這份文件適用於想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空間中定義之 Managed <xref:System.Windows.Automation> 類別的 .NET Framework 開發人員。 如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新資訊，請參閱 [Windows Automation API：UI 自動化](/windows/win32/winauto/entry-uiauto-win32)。  
  
 本節說明如何實作 <xref:System.Windows.Automation.AutomationElement> 屬性和控制項模式的快取。  
  
### <a name="activate-a-cache-request"></a>啟動快取要求  
  
1. 建立 <xref:System.Windows.Automation.CacheRequest>。  
  
2. 使用 <xref:System.Windows.Automation.CacheRequest.Add%2A>指定要快取的屬性和模式。  
  
3. 設定 <xref:System.Windows.Automation.CacheRequest.TreeScope%2A> 屬性，以指定快取的範圍。  
  
4. 設定 <xref:System.Windows.Automation.CacheRequest.TreeFilter%2A> 屬性，以指定樹狀子目錄的檢視。  
  
5. 如果要提高效率而不擷取物件的完整參考，可以將 <xref:System.Windows.Automation.CacheRequest.AutomationElementMode%2A> 屬性設為 <xref:System.Windows.Automation.AutomationElementMode.None> 。 (如此將無法從這些物件擷取目前值。)  
  
6. <xref:System.Windows.Automation.CacheRequest.Activate%2A> `using` 在區塊內使用（ `Using` 在 Microsoft Visual Basic .net 中）來啟動要求。  
  
 在取得 <xref:System.Windows.Automation.AutomationElement> 物件或訂閱事件之後，使用 <xref:System.Windows.Automation.CacheRequest.Pop%2A> (若使用 <xref:System.Windows.Automation.CacheRequest.Push%2A> ) 或處置 <xref:System.Windows.Automation.CacheRequest.Activate%2A>所建立的物件，以停用要求。 （在區塊中使用（ <xref:System.Windows.Automation.CacheRequest.Activate%2A> `using` `Using` 在 Microsoft Visual Basic .net 中）。  
  
### <a name="cache-automationelement-properties"></a>快取 AutomationElement 屬性  
  
1. 當 <xref:System.Windows.Automation.CacheRequest> 在作用中時，使用 <xref:System.Windows.Automation.AutomationElement> 或 <xref:System.Windows.Automation.AutomationElement.FindFirst%2A> 取得 <xref:System.Windows.Automation.AutomationElement.FindAll%2A>物件；或取得 <xref:System.Windows.Automation.AutomationElement> 做為 <xref:System.Windows.Automation.CacheRequest> 作用中時註冊之事件的來源。 (您也可以將 <xref:System.Windows.Automation.CacheRequest> 傳遞至 GetUpdatedCache 或其中一個 <xref:System.Windows.Automation.TreeWalker> 方法，以此方式建立快取。)  
  
2. 使用 <xref:System.Windows.Automation.AutomationElement.GetCachedPropertyValue%2A> ，或從 <xref:System.Windows.Automation.AutomationElement.Cached%2A> 的 <xref:System.Windows.Automation.AutomationElement>屬性擷取屬性。  
  
### <a name="obtain-cached-patterns-and-their-properties"></a>取得快取的模式及其屬性  
  
1. 當 <xref:System.Windows.Automation.CacheRequest> 在作用中時，使用 <xref:System.Windows.Automation.AutomationElement> 或 <xref:System.Windows.Automation.AutomationElement.FindFirst%2A> 取得 <xref:System.Windows.Automation.AutomationElement.FindAll%2A>物件；或取得 <xref:System.Windows.Automation.AutomationElement> 做為 <xref:System.Windows.Automation.CacheRequest> 作用中時註冊之事件的來源。 (您也可以將 <xref:System.Windows.Automation.CacheRequest> 傳遞至 GetUpdatedCache 或其中一個 <xref:System.Windows.Automation.TreeWalker> 方法，以此方式建立快取。)  
  
2. 使用 <xref:System.Windows.Automation.AutomationElement.GetCachedPattern%2A> 或 <xref:System.Windows.Automation.AutomationElement.TryGetCachedPattern%2A> 擷取快取的模式。  
  
3. 從控制項模式的 `Cached` 屬性擷取屬性值。  
  
## <a name="example"></a>範例  
 下列程式碼範例使用 <xref:System.Windows.Automation.CacheRequest.Activate%2A> 啟動 <xref:System.Windows.Automation.CacheRequest>，顯示快取的各個方面。  
  
 [!code-csharp[UIAClient_snip#107](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#107)]
 [!code-vb[UIAClient_snip#107](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#107)]  
  
## <a name="example"></a>範例  
 下列程式碼範例使用 <xref:System.Windows.Automation.CacheRequest.Push%2A> 啟動 <xref:System.Windows.Automation.CacheRequest>，顯示快取的各個方面。 要將快取要求進行巢狀處理時則例外，這時最好使用 <xref:System.Windows.Automation.CacheRequest.Activate%2A>。  
  
 [!code-csharp[UIAClient_snip#108](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#108)]
 [!code-vb[UIAClient_snip#108](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#108)]  
  
## <a name="see-also"></a>另請參閱

- [UI 自動化用戶端中的快取](caching-in-ui-automation-clients.md)
