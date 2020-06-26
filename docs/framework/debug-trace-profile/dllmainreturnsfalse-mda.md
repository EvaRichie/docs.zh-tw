---
title: dllMainReturnsFalse MDA
description: 閱讀有關 .NET 中 dllMainReturnsFalse managed 偵錯工具的資訊。 如果 DLL 初始化失敗，就會啟用此 MDA。
ms.date: 03/30/2017
helpviewer_keywords:
- managed debugging assistants (MDAs), DllMain returns false
- DllMainReturnsFalse MDA
- DllMain function
- MDAs (managed debugging assistants), DllMain returns false
ms.assetid: e2abdd04-f571-4b97-8c16-2221b8588429
ms.openlocfilehash: 21d5e37d6823876e07cf5b2cbb881c1cf8b47b11
ms.sourcegitcommit: a2c8b19e813a52b91facbb5d7e3c062c7188b457
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85416053"
---
# <a name="dllmainreturnsfalse-mda"></a>dllMainReturnsFalse MDA
如果以理由 DLL_PROCESS_ATTACH 呼叫的使用者組件 Managed `DllMain` 函式，傳回 FALSE，就會啟動 `dllMainReturnsFalse` Managed 偵錯助理 (MDA)。  
  
## <a name="symptoms"></a>徵狀  
 `DllMain` 函式傳回 FALSE，指出未正確執行。 因為 `DllMain` 函式通常會包含重要的初始化程式碼，所以這會造成未定的問題。  
  
## <a name="cause"></a>原因  
 因為在載入時 DLL 初始化發生 DLL_PROCESS_ATTACH，所以呼叫 `DllMain` 函式。 如果它傳回 FALSE，表示該 DLL 初始化失敗。  
  
## <a name="resolution"></a>解決方案  
 分析失敗 DLL 的 `DllMain` 函式程式碼，找出初始化失敗的原因。  
  
## <a name="effect-on-the-runtime"></a>對執行階段的影響  
 此 MDA 對 CLR 沒有影響。 它只報告 `DllMain` 傳回值的相關資料。  
  
## <a name="output"></a>輸出  
 訊息，指出因為 DLL_PROCESS_ATTACH 而呼叫的 `DllMain` 函式傳回 FALSE。 請注意，只有在 Managed 程式碼中實作 `DllMain` 時，才會啟用這個 MDA。  
  
## <a name="configuration"></a>設定  
  
```xml  
<mdaConfig>  
  <assistants>  
    <dllMainReturnsFalse />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>另請參閱

- [使用 Managed 偵錯助理診斷錯誤](diagnosing-errors-with-managed-debugging-assistants.md)
