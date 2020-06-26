---
title: contextSwitchDeadlock MDA
description: 瞭解 .NET 中的 coNtextSwitchDeadlock managed 偵錯工具（MDA），這是在 COM 內容轉換期間偵測到鎖死時啟動的。
ms.date: 03/30/2017
helpviewer_keywords:
- deadlocks [.NET Framework]
- pumping messages
- STA message pumping
- single-threaded COM components
- MDAs (managed debugging assistants), context switching deadlocks
- managed debugging assistants (MDAs), context switching deadlocks
- ContextSwitchDeadlock MDA
- message pumping
- context switching deadlocks
ms.assetid: 26dfaa15-9ddb-4b0a-b6da-999bba664fa6
ms.openlocfilehash: 52db4f2c88bac4e8cac621cca989fa10acb43f94
ms.sourcegitcommit: a2c8b19e813a52b91facbb5d7e3c062c7188b457
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85416014"
---
# <a name="contextswitchdeadlock-mda"></a>contextSwitchDeadlock MDA

試圖進行 COM 內容轉換期間，偵測到死結時，會啟用 `contextSwitchDeadlock` Managed 偵錯助理 (MDA)。

## <a name="symptoms"></a>徵狀

最常見的徵兆是，在 Unmanaged COM 元件上從 Managed 程式碼進行的呼叫未傳回。  另一個徵兆是記憶體使用量隨著時間增加。

## <a name="cause"></a>原因

最有可能的原因是，單一執行緒 Apartment (STA) 執行緒沒有提取訊息。 STA 執行緒可能正在等待而沒有提取訊息，或是正在執行長時間作業，不允許訊息佇列提取。

記憶體使用量隨著時間增加的原因，是因為完成項執行緒試圖在 Unmanaged COM 元件上呼叫 `Release`，而該元件未傳回。  這會導致完成項無法回收其他物件。

根據預設，Visual Basic 主控台應用程式主要執行緒的執行緒模型為 STA。 如果 STA 執行緒直接或間接透過通用語言執行平台或協力廠商控制項來使用 COM 互通性，就會啟用此 MDA。  若要避免在 Visual Basic 主控台應用程式中啟用此 MDA，請將 <xref:System.MTAThreadAttribute> 屬性套用至 Main 方法，或修改應用程式來提取訊問。

在符合下列所有條件的情況下，有可能會錯誤地啟用此 MDA：

- 應用程式直接或間接透過程式庫，從 STA 執行緒建立 COM 元件。

- 已在偵錯工具中停止應用程式，而使用者繼續應用程式，或執行步驟作業。

- 未啟用 Unmanaged 偵錯。

若要判斷是否錯誤地啟用 MDA，請停用所有中斷點、重新啟動應用程式，並且讓它不間斷地執行。 如果未啟用 MDA，則可能初始啟用時發生錯誤。 若是如此，請停用 MDA，以避免阻礙偵錯工作階段。

> [!NOTE]
> 此 MDA 位於 Visual Studio 的預設集合中。 如需如何停用 Mda 的詳細資訊，請參閱[診斷 Managed 偵錯工具的錯誤](diagnosing-errors-with-managed-debugging-assistants.md#enable-and-disable-mdas)。

## <a name="resolution"></a>解決方案

遵循有關 STA 訊息幫浦的 COM 規則。

## <a name="effect-on-the-runtime"></a>對執行階段的影響

此 MDA 對 CLR 沒有影響。 它只會提報 COM 內容的相關資料。

## <a name="output"></a>輸出

描述目前內容和目標內容的訊息。

## <a name="configuration"></a>設定

```xml
<mdaConfig>
  <assistants>
    <contextSwitchDeadlock />
  </assistants>
</mdaConfig>
```

## <a name="see-also"></a>另請參閱

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [使用 Managed 偵錯助理診斷錯誤](diagnosing-errors-with-managed-debugging-assistants.md)
- [Interop 封送處理](../interop/interop-marshaling.md)
