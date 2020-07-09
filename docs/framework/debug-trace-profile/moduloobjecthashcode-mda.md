---
title: moduloObjectHashcode MDA
description: 請參閱 moduloObjectHashcode managed 偵錯工具（MDA），這會變更物件類別，以取得 GetHashCode 方法結果的餘數值。
ms.date: 03/30/2017
helpviewer_keywords:
- managed debugging assistants (MDAs), hashcode modulus
- Modulo object hash code
- moduloObjectHashcode MDA
- hashcode modulus
- MDAs (managed debugging assistants), hashcode modulus
- GetHashCode method
- modulus of hashcodes
ms.assetid: b45366ff-2a7a-4b8e-ab01-537b72e9de68
ms.openlocfilehash: a929ec2b9196f1f6cad0528fdf7323839a86fa55
ms.sourcegitcommit: 0edbeb66d71b8df10fcb374cfca4d731b58ccdb2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/07/2020
ms.locfileid: "86052061"
---
# <a name="moduloobjecthashcode-mda"></a>moduloObjectHashcode MDA
`moduloObjectHashcode` Managed 偵錯助理 (MDA) 會變更 <xref:System.Object> 類別對 <xref:System.Object.GetHashCode%2A> 方法所傳回之雜湊碼執行模數作業的行為。 此 MDA 的預設模數是 1，讓 <xref:System.Object.GetHashCode%2A> 針對所有物件都傳回 0。  
  
## <a name="symptoms"></a>徵狀  
 移至新版的 Common Language Runtime (CLR) 之後，就無法再正確地執行程式：  
  
- 程式會從 <xref:System.Collections.Hashtable> 取得錯誤的物件。  
  
- <xref:System.Collections.Hashtable> 中的列舉順序包含中斷程式的變更。  
  
- 兩個相等的物件不再相等。  
  
- 兩個不相等的物件現在相等。  
  
## <a name="cause"></a>原因  
 您的程式可能從 <xref:System.Collections.Hashtable> 取得錯誤物件，因為 <xref:System.Collections.Hashtable> 中索引鍵類別上的 <xref:System.Object.Equals%2A> 方法實作會比較 <xref:System.Object.GetHashCode%2A> 方法呼叫的結果，來測試物件是否相等。 雜湊碼不應該用來測試物件是否相等，因為兩個物件可能有相同的雜湊碼，即使其個別欄位具有不同的值也是一樣。 雖然實務上十分罕見，但確實會發生這些雜湊碼衝突。 這對 <xref:System.Collections.Hashtable> 查閱的影響是兩個不相等的索引鍵顯示為相等，並且從 <xref:System.Collections.Hashtable> 傳回錯誤的物件。 基於效能考量，<xref:System.Object.GetHashCode%2A> 實作可以在執行階段版本之間變更，因此某個版本可能不會發生的衝突可能會在後續版本上發生。 讓此 MDA 測試在雜湊碼衝突時，您的程式碼是否有 Bug。 啟用時，此 MDA 會讓 <xref:System.Object.GetHashCode%2A> 方法傳回 0，因而導致所有雜湊碼衝突。 啟用此 MDA 對程式的唯一影響，在於您程式的執行速度會變慢。  
  
 如果演算法是用來計算索引鍵變更的雜湊碼，則 <xref:System.Collections.Hashtable> 中的列舉順序可能會從執行階段的某個版本變更為另一個版本。 若要測試程式是否依存於索引鍵或值列舉順序，您可以啟用這個 MDA。  
  
## <a name="resolution"></a>解決方案  
 永遠不要使用雜湊碼來取代物件身分識別。 實作 <xref:System.Object.Equals%2A?displayProperty=nameWithType> 方法的覆寫，不比較雜湊碼。  
  
 請不要建立與雜湊表中之索引鍵或值列舉順序的相依性。  
  
## <a name="effect-on-the-runtime"></a>對執行階段的影響  
 啟用此 MDA 時，應用程式的執行速度會更慢。 此 MDA 只會採用已傳回的雜湊碼，並改成在除以模數時傳回餘數。  
  
## <a name="output"></a>輸出  
 沒有此 MDA 的輸出。  
  
## <a name="configuration"></a>設定  
 `modulus` 屬性指定雜湊碼上所使用的模數。 預設值為 1。  
  
```xml  
<mdaConfig>  
  <assistants>  
    <moduloObjectHashcode modulus="1" />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Object.GetHashCode%2A?displayProperty=nameWithType>
- <xref:System.Object.Equals%2A?displayProperty=nameWithType>
- [使用 Managed 偵錯助理診斷錯誤](diagnosing-errors-with-managed-debugging-assistants.md)
