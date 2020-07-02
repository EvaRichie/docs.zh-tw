---
title: pInvokeStackImbalance MDA
description: 檢查 PInvokeStackImbalance MDA，這在進行或遵循平台叫用呼叫時，可能會在存取違規或記憶體損毀期間啟用。
ms.date: 03/30/2017
helpviewer_keywords:
- signatures, platform invoke
- stack depth
- platform invoke stack imbalance
- MDAs (managed debugging assistants), platform invoke
- platform invoke, run-time errors
- PInvokeStackImbalance MDA
- managed debugging assistants (MDAs), platform invoke
ms.assetid: 34ddc6bd-1675-4f35-86aa-de1645d5c631
ms.openlocfilehash: 89afd3fce3f2a8bffe88d45991ceeb59fc5e5b76
ms.sourcegitcommit: c23d9666ec75b91741da43ee3d91c317d68c7327
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85803660"
---
# <a name="pinvokestackimbalance-mda"></a>PInvokeStackImbalance MDA

`PInvokeStackImbalance`當 CLR 偵測到平台叫用呼叫之後的堆疊深度不符合預期的堆疊深度時，就會啟動 managed 偵錯工具（MDA），前提是屬性中指定的呼叫慣例 <xref:System.Runtime.InteropServices.DllImportAttribute> 和 managed 簽章中的參數宣告。

`PInvokeStackImbalance` MDA 只會在 32 位元 x86 平台上實作。

> [!NOTE]
> `PInvokeStackImbalance`預設會停用 MDA。 在 Visual Studio 2017 和更新版本中， `PInvokeStackImbalance` MDA 會出現在 [**例外狀況設定**] 對話方塊的 [ **Managed 調試助理**] 清單中（當您選取 [ **Debug**  >  **Windows**  >  **例外狀況設定**] 時顯示）。 不過，選取或清除 [擲回**時中斷**] 核取方塊並不會啟用或停用 MDA。它只會控制 Visual Studio 在啟動 MDA 時是否擲回例外狀況。

## <a name="symptoms"></a>徵狀

應用程式在進行平台叫用呼叫期間或之後發生存取違規或記憶體損毀。

## <a name="cause"></a>原因

平台叫用呼叫的 Managed 簽章可能與所呼叫之方法的 Unmanaged 簽章不符。  當 Managed 簽章未宣告正確的參數數目，或未指定適當的參數大小時，便會造成這種不相符狀況。  MDA 也可能由於呼叫慣例 (可能由 <xref:System.Runtime.InteropServices.DllImportAttribute> 屬性指定) 與 Unmanaged 呼叫慣例不符而啟動。

## <a name="resolution"></a>解決方案

檢閱 Managed 平台叫用簽章和呼叫慣例，確認其與原生目標的簽章和呼叫慣例相符。  嘗試明確指定 Managed 和 Unmanaged 端的呼叫慣例。 Unmanaged 函式也可能 (雖然可能性不高) 因其他一些原因而使堆疊失去平衡，例如 Unmanaged 編譯器中的 Bug。

## <a name="effect-on-the-runtime"></a>對執行階段的影響

強制所有平台叫用呼叫採用 CLR 中未最佳化的路徑。

## <a name="output"></a>輸出

MDA 訊息會提供使堆疊失去平衡之平台叫用方法呼叫的名稱。 `SampleMethod` 方法之平台叫用呼叫的範例訊息為：

**對 PInvoke 函數 ' Sampleobject.samplemethod ' 的呼叫具有不對稱的堆疊。這很可能是因為受控 PInvoke 簽章與非受控目標籤章不相符。檢查 PInvoke 簽章的呼叫慣例和參數是否符合目標非受控簽章。**

## <a name="configuration"></a>組態

```xml
<mdaConfig>
  <assistants>
    <pInvokeStackImbalance />
  </assistants>
</mdaConfig>
```

## <a name="see-also"></a>另請參閱

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [使用 Managed 偵錯助理診斷錯誤](diagnosing-errors-with-managed-debugging-assistants.md)
- [Interop 封送處理](../interop/interop-marshaling.md)
