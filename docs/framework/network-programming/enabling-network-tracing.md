---
title: 啟用網路追蹤
description: 瞭解如何啟用網路追蹤，以針對 .NET Framework 中的受控應用程式提供方法調用和網路流量的相關資訊。
ms.date: 03/30/2017
helpviewer_keywords:
- trace destinations
- sending traces to log file
- trace listeners, network tracing
- network tracing, enabling
- CLR Debugger
- default listeners
- logs, trace
- destination for tracing output
ms.assetid: 5fff458c-51a6-4134-ba47-8a6137ddc41e
ms.openlocfilehash: 246a975ead3cb9c1acb4fe0512dfa91d1b8a00c0
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96287419"
---
# <a name="enabling-network-tracing"></a>啟用網路追蹤

針對方法叫用及 Managed 應用程式所產生的網路流量，網路追蹤能提供對這些相關資訊的存取。 您必須完成下列工作，才能在您的應用程式中啟用網路追蹤：  
  
- 編譯程式碼並啟用追蹤。 如需啟用追蹤所需之編譯器參數的詳細資訊，請參閱[如何：使用追蹤和偵錯進行條件式編譯](../debug-trace-profile/how-to-compile-conditionally-with-trace-and-debug.md)。  
  
- 指定追蹤輸出的目的地。  
  
- 設定網路追蹤的行為。 如需詳細資訊，請參閱[如何：設定網路追蹤](how-to-configure-network-tracing.md)。  
  
 最常見的追蹤目的地，也稱為追蹤接聽項，是預設的接聽程式和記錄檔。  
  
 如未指定追蹤接聽項，追蹤就會使用預設的接聽程式。 您可以在啟用了 Managed 程式碼的偵錯工具中，例如隨附於 .NET Framework SDK 的 CLR 偵錯工具，或隨附於 Windows SDK 的 DBwin32.exe，執行您的程式碼，檢視傳送到預設接聽程式的訊息。 使用 CLR 偵錯工具，追蹤訊息會出現在 [輸出] 視窗中。  
  
 如果您偏好使用檔案來接收追蹤，您可以使用組態設定來指定記錄檔，如下列範例所示。 (如需組態檔的一般討論，請參閱[組態檔](../configure-apps/index.md)。)  
  
 若要將追蹤傳送至記錄檔，請將以下節點新增至適當 (應用程式或電腦) 組態檔的 `<system.diagnostics>` 節點。 您可以變更檔案名稱 (trace.log) 以符合您的需求。  
  
```xml  
<system.diagnostics>  
  <trace autoflush="true" indentsize="4">  
    <listeners>  
      <add name="file" type="System.Diagnostics.TextWriterTraceListener" initializeData="trace.log"/>  
    </listeners>
  </trace>  
</system.diagnostics>  
```  
  
## <a name="see-also"></a>另請參閱

- [解譯網路追蹤](interpreting-network-tracing.md)
- [以 .NET Framework 進行網路追蹤](network-tracing.md)
- [追蹤和檢測應用程式](../debug-trace-profile/tracing-and-instrumenting-applications.md) (機器翻譯)
