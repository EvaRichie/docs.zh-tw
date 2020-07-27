---
title: UI 自動化用戶端的控制項模式對應
description: 查看使用者介面自動化用戶端的控制項模式對應表。 某些控制項類型的動作可能會受到支援、有條件地支援或不支援。
ms.date: 03/30/2017
helpviewer_keywords:
- control patterns, for UI Automation clients
- UI Automation, clients, control patterns for
ms.assetid: 8b81645b-8be3-4e26-9c98-4fb0fceca06b
ms.openlocfilehash: 7673ce4ac88cc36a7c35e2e946a31d23b2ce6eca
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87164181"
---
# <a name="control-pattern-mapping-for-ui-automation-clients"></a>UI 自動化用戶端的控制項模式對應
> [!NOTE]
> 這份文件適用於想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空間中定義之 Managed <xref:System.Windows.Automation> 類別的 .NET Framework 開發人員。 如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新資訊，請參閱 [Windows Automation API：UI 自動化](/windows/win32/winauto/entry-uiauto-win32)。  
  
 本主題列出控制項類型及其相關聯的控制項模式。  
  
 下表將控制項模式整理為下列類別：  
  
- 支援。 控制項必定支援此控制項模式。  
  
- 有條件支援。 控制項可依據控制項的狀態決定是否支援此控制項模式。  
  
- 不支援。 控制項不支援此控制項模式；自訂控制項可能支援此控制項模式。  
  
> [!NOTE]
> 有些控制項會依據其功能，有條件支援多種控制項模式。 例如，功能表項目控制項即依據其在功能表控制項中的功能，有條件支援 <xref:System.Windows.Automation.InvokePattern>、 <xref:System.Windows.Automation.ExpandCollapsePattern>、 <xref:System.Windows.Automation.TogglePattern>或 <xref:System.Windows.Automation.SelectionItemPattern> 控制項模式。  
  
<a name="control_mapping_clients"></a>
## <a name="ui-automation-control-patterns-for-clients"></a>用戶端的 UI 自動化控制項模式  
  
|控制項類型|支援|有條件支援。|不支援|  
|------------------|---------------|-------------------------|-------------------|  
|按鈕|None|叫用、切換、展開摺疊|None|  
|行事曆|方格、表格|選取、捲軸|值|  
|核取方塊|切換|None|None|  
|下拉式方塊|展開摺疊|選取、值|Scroll|  
|資料格線|Grid|捲軸、選取、表格|None|  
|Data Item|Selection Item|展開摺疊、方格項目、捲軸項目、表格、切換、值|None|  
|Document|Text|捲軸、值|None|  
|編輯|None|文字、範圍值、值|None|  
|群組|None|展開摺疊|None|  
|頁首|None|轉換|None|  
|標題項目|None|轉換、叫用|None|  
|Hyperlink|叫用|值|None|  
|映像|None|方格項目、表格項目|叫用、選取項目|  
|清單|None|方格、多重檢視、捲軸、選取|Table|  
|清單項目|Selection Item|展開摺疊、方格項目、叫用、捲軸項目 、切換、值|None|  
|功能表|None|None|None|  
|功能表列|None|展開摺疊、停駐、轉換|None|  
|功能表項目|None|展開摺疊、叫用、選取項目、切換|None|  
|窗格|None|停駐 捲軸、轉換|時間範圍|  
|進度列|None|範圍值、值|None|  
|選項按鈕|Selection Item|None|切換|  
|Scroll Bar|None|Range Value|Scroll|  
|Separator|None|None|None|  
|滑桿|None|範圍值、選取、值|None|  
|Spinner|None|範圍值、選取、值|None|  
|Split Button|叫用、展開摺疊|None|None|  
|狀態列|None|Grid|None|  
|索引標籤|選取|Scroll|None|  
|索引標籤項目|Selection Item|None|叫用|  
|Table|方格、方格項目、表格、表格項目|None|None|  
|Text|None|方格項目、表格項目、文字|值|  
|Thumb|轉換|None|None|  
|標題列|None|None|None|  
|工具列|None|停駐、展開摺疊、轉換|None|  
|工具提示|None|文字、視窗|None|  
|樹狀結構|None|捲軸、選取|None|  
|樹狀目錄項目|展開摺疊|叫用、捲軸項目、選取項目、切換|None|  
|時間範圍|轉換、視窗|Dock|None|  
  
> [!NOTE]
> 如果控制項類型沒有所列的受支援控制項模式，但有一或多個有條件支援的控制項模式，就會一律支援其中一個條件式控制項模式。  
  
## <a name="see-also"></a>另請參閱

- [UI 自動化概觀](ui-automation-overview.md)
