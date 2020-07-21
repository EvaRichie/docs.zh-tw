---
title: 風險降低︰以指標為基礎的觸控及手寫筆支援
description: 瞭解針對以 .NET Framework 4.7 為目標的 WPF 應用程式啟用選用的 WPF 觸控/手寫筆堆疊的效果。
ms.date: 04/07/2017
helpviewer_keywords:
- retargeting changes
- .NET Framework 4.7 retargeting changes
- WPF retargeting changes
- WPF pointer-based touch and stylus stack
ms.assetid: f99126b5-c396-48f9-8233-8f36b4c9e717
ms.openlocfilehash: d0c0effeaa727c615dddc3b92cdd34aafde65705
ms.sourcegitcommit: cf5a800a33de64d0aad6d115ffcc935f32375164
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/20/2020
ms.locfileid: "86475420"
---
# <a name="mitigation-pointer-based-touch-and-stylus-support"></a>風險降低︰以指標為基礎的觸控及手寫筆支援

以 .NET Framework 4.7 為目標，且從 Windows 10 建立者更新開始在 Windows 上執行的 WPF 應用程式，可以啟用選擇性 `WM_POINTER` 的 wpf 觸控/手寫筆堆疊。

## <a name="impact"></a>影響

開發人員若未明確地啟用以指標為基礎的觸控/手寫筆支援，應該不會看到任何 WPF 觸控/手寫筆行為的變更。

以下是選擇性的 `WM_POINTER` 式觸控/手寫筆堆疊目前已知的問題︰

- 不支援即時筆跡。

   雖然筆跡和手寫筆外掛程式還能運作，但它們是在 UI 執行緒上處理，可能會導致效能不佳。

- 從觸控/手寫筆事件提升為滑鼠事件的變更，因而產生行為變更。

  - 操作可能有不同的行為。

  - 拖放動作無法對觸控輸入顯示適當的回應。 (這不影響手寫筆輸入。)

  - 無法再針對觸控/手寫筆事件起始拖放動作。

      這可能會導致應用程式停止回應，直到偵測到滑鼠輸入為止。 開發人員應改為從滑鼠事件起始拖放動作。

## <a name="opting-in-to-wm_pointer-based-touchstylus-support"></a>選擇加入 WM_POINTER 式觸控/手寫筆支援

想要啟用此堆疊的開發人員可以將下列新增至其應用程式的*app.config*檔案。

```xml
<configuration>
    <runtime>
        <AppContextSwitchOverrides value="Switch.System.Windows.Input.Stylus.EnablePointerSupport=true"/>
    </runtime>
</configuration>
```

移除此項目或將其值設為 `false` 可關閉這個選擇性的堆疊。

## <a name="see-also"></a>另請參閱

- [應用程式相容性](application-compatibility.md)
