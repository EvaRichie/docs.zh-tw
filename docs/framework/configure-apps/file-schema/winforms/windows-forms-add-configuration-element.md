---
title: Windows Forms 新增 Configuration 元素
ms.date: 04/07/2017
helpviewer_keywords:
- Windows Forms Add configuration element
- configuring Windows Forms applications
ms.assetid: 3e3e04de-99d1-4658-b716-44cb669d9589
ms.openlocfilehash: 26b806f84c3e1bc44e0437a8f8806316b14897b8
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "73109653"
---
# <a name="windows-forms-add-configuration-element"></a>Windows Forms 新增 Configuration 元素

`<add>`元素會新增預先定義的索引鍵，指定您的 Windows Form 應用程式是否支援在 .NET Framework 4.7 或更新版本中新增至 Windows Forms 應用程式的功能。

## <a name="syntax"></a>語法

```xml
<System.Windows.Forms.ApplicationConfigurationSection>
  <add key="key-name" value="key-value" />
</System.Windows.Forms.ApplicationConfigurationSection>
```

## <a name="attributes-and-elements"></a>屬性和元素

下列章節說明屬性、子元素和父元素。

### <a name="attributes"></a>屬性

| 屬性 | 描述 |
| --------- | ----------- |
| `key`     | 必要屬性。 預先定義的索引鍵名稱，對應到特定 Windows Forms 可自訂的功能。 |
| `value`   | 必要屬性。 要指派給 `key` 的值。 |

### <a name="key-attribute-names-and-associated-values"></a>`key`屬性名稱和相關聯的值

| `key` 名稱 | 值 | 描述 |
| ---------- | ------ | ----------- |
| "AnchorLayout.DisableSinglePassControlScaling" | "true" &#124; "false" | 指出錨定控制項是否會在單一階段中縮放。 "true" 表示停用單一傳遞調整;否則為 false。 如需詳細資訊，請參閱[備註](#remarks)中的「單一傳遞調整」一節。 |
| "DpiAwareness" | "PerMonitorV2" &#124; "false" | 指出應用程式是否為 DPI 感知。 將金鑰設為 "PerMonitorV2" 以支援 Dpi 感知;否則，請將它設定為 "false"。 DPI 感知是加入宣告的功能;若要利用 Windows Forms 的高 DPI 支援，您應該將其值設定為 "PerMonitorV2"。 如需詳細資訊，請參閱[備註](#remarks)一節。 |
| "CheckedListBox. DisableHighDpiImprovements" | "true" &#124; "false" | 指出控制項是否 <xref:System.Windows.Forms.CheckedListBox> 利用 .NET Framework 4.7 中引進的縮放和版面配置改良功能。 「true」可選擇不進行調整和版面配置改善;否則為 "false"。 |
| "DataGridView. DisableHighDpiImprovements" | "true" &#124; "false" | 指出是否在 <xref:System.Windows.Forms.DataGridView> .NET Framework 4.7 中導入控制項縮放和版面配置改進。 "true" 表示退出 DPI 感知;否則為 "false"。 |
| "DisableDpiChangedMessageHandling" | "true" &#124; "false" | "true" 表示選擇不接收與 DPI 縮放比例變更相關的訊息;否則為 "false"。 如需詳細資訊，請參閱[備註](#remarks)一節。 |
| EnableWindowsFormsHighDpiAutoResizing | "true" &#124; "false" | 指出是否因為 DPI 縮放比例變更，而自動調整 Windows Forms 應用程式的大小。 "true" 表示啟用自動調整大小;否則為 false。 |
| "Form. DisableSinglePassControlScaling" | "true" &#124; "false" | 指出是否要 <xref:System.Windows.Forms.Form> 在單一階段中縮放。 "true" 表示停用單一傳遞調整;否則為 false。 如需詳細資訊，請參閱[備註](#remarks)中的「單一傳遞調整」一節。 |
| "MonthCalendar. DisableSinglePassControlScaling" | "true" &#124; "false" | 指出控制項是否 <xref:System.Windows.Forms.MonthCalendar> 在單一階段中縮放。 "true" 表示停用單一傳遞調整;否則為 false。 如需詳細資訊，請參閱[備註](#remarks)中的「單一傳遞調整」一節。 |
| "Toolstrip. DisableHighDpiImprovements" | "true" &#124; "false" | 指出控制項是否 <xref:System.Windows.Forms.ToolStrip> 利用 .NET Framework 4.7 中引進的縮放和版面配置改良功能。 "true" 表示退出 DPI 感知;否則為 "false"。 |

### <a name="child-elements"></a>子元素

無。

### <a name="parent-elements"></a>父元素

| 元素 | 描述 |
| ------- | ----------- |
| [`<System.Windows.Forms.ApplicationConfigurationSection>`](index.md) | 設定新 Windows Forms 應用程式功能的支援。 |

## <a name="remarks"></a>備註

從 .NET Framework 4.7 開始，`<System.Windows.Forms.ApplicationConfigurationSection>` 元素能允許您設定 Windows Forms 應用程式，以利用 .NET Framework 最新版本中的新增功能。

`<System.Windows.Forms.ApplicationConfigurationSection>`元素可讓您新增一或多個子專案 `<add>` ，每個專案都會定義特定的設定。

如需 Windows Forms 高 DPI 支援的總覽，請參閱[Windows Forms 中的高 Dpi 支援](../../../winforms/high-dpi-support-in-windows-forms.md)。

### <a name="dpiawareness"></a>DpiAwareness

從 Windows 10 建立者版本開始的 Windows 版本執行的應用程式，以及從 .NET Framework 4.7 開始的目標 .NET Framework 版本，都可以設定為利用 .NET Framework 4.7 中引進的高 DPI 改良功能。 Windows Forms 其中包括：

- 支援動態 DPI 案例，在這種情況下，使用者會在啟動 Windows Forms 應用程式之後變更 DPI 或縮放比例。

- 改善數個 Windows Forms 控制項（例如控制項和控制項）的縮放和版面配置 <xref:System.Windows.Forms.MonthCalendar> <xref:System.Windows.Forms.CheckedListBox> 。

高 DPI 感知是加入宣告功能;根據預設，的值 `DpiAwareness` 為 `false` 。 您可以 `PerMonitorV2` 在應用程式佈建檔中，將此機碼的值設定為，以選擇 Windows Forms ' DPI 感知的支援。 如果已啟用 DPI 感知，則也會啟用所有個別的 DPI 功能。 其中包括：

- DPI 變更的訊息，由索引鍵所控制 `DisableDpiChangedMessageHandling` 。

- 動態 DPI 支援，它是由金鑰所控制 `EnableWindowsFormsHighDpiAutoResizing` 。

- 單一傳遞控制項調整，由 `Form.DisableSinglePassControlScaling` 個別 <xref:System.Windows.Forms.Form> 控制項的、 `AnchorLayout.DisableSinglePassControlScaling` 錨定控制項的索引鍵，以及控制項的索引 `MonthCalendar.DisableSinglePassControlScaling` 鍵 <xref:System.Windows.Forms.MonthCalendar> 所控制

- 高 DPI 縮放比例和版面配置改進，由控制項的索引 `CheckListBox.DisableHighDpiImprovements` 鍵、 <xref:System.Windows.Forms.CheckedListBox> 控制項的索引鍵 `DataGridView.DisableHighDpiImprovements` <xref:System.Windows.Forms.DataGridView> ，以及控制項的索引 `Toolstrip.DisableHighDpiImprovements` 鍵 <xref:System.Windows.Forms.ToolStrip> 所控制。

將設定為所提供的單一預設加入宣告設定， `DpiAwareness` `PerMonitorV2` 通常適用于新的 Windows Forms 應用程式。 不過，您可以藉由將對應的索引鍵新增至應用程式佈建檔，來選擇不使用個別的高 DPI 增強功能。 例如，若要利用動態 DPI 支援以外的所有新 DPI 功能，您可以將下列內容新增至您的應用程式佈建檔：

```xml
<System.Windows.Forms.ApplicationConfigurationSection>
   <add key="DpiAwareness" value="PerMonitorV2" />
   <!-- Disable dynamic DPI support -->
   <add key="EnableWindowsFormsHighDpiAutoResizing" value="false" />
</System.Windows.Forms.ApplicationConfigurationSection>
```

您通常會選擇不使用特定功能，因為您已選擇以程式設計方式處理它。

如需利用 Windows Forms 應用程式中高 DPI 支援的詳細資訊，請參閱[Windows Forms 中的高 Dpi 支援](../../../winforms/high-dpi-support-in-windows-forms.md)。

### <a name="disabledpichangedmessagehandling"></a>DisableDpiChangedMessageHandling

從 .NET Framework 4.7 開始，Windows Forms 控制項會引發一些與 DPI 縮放比例變更相關的事件。 其中包括 <xref:System.Windows.Forms.Control.DpiChangedAfterParent> 、 <xref:System.Windows.Forms.Control.DpiChangedBeforeParent> 和 <xref:System.Windows.Forms.Form.DpiChanged> 事件。 索引鍵的值 `DisableDpiChangedMessageHandling` 會決定這些事件是否會在 Windows Forms 應用程式中引發。

### <a name="single-pass-scaling"></a>單一傳遞調整

單一或多重傳遞調整會影響使用者介面的觀察回應能力，以及使用者介面專案在調整時的視覺外觀。 從 .NET Framework 4.7 開始，Windows Forms 使用單一傳遞調整。 在舊版的 .NET Framework 中，縮放是透過多個階段來執行，這會導致某些控制項的縮放比例超出所需。 只有當您的應用程式相依于舊的行為時，才應該停用單一傳遞調整。

## <a name="see-also"></a>另請參閱

- [Windows Form 組態區段](index.md)
- [Windows Forms 中的高 DPI 支援](../../../winforms/high-dpi-support-in-windows-forms.md)
