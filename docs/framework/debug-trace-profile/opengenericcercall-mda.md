---
title: openGenericCERCall MDA
description: 請參閱 openGenericCERCall managed 偵錯工具，如果線上程中止或應用程式域卸載時，CER 程式碼不會執行，這可能會啟用。
ms.date: 03/30/2017
helpviewer_keywords:
- MDAs (managed debugging assistants), CER calls
- open generic CER calls
- constrained execution regions
- openGenericCERCall MDA
- CER calls
- managed debugging assistants (MDAs), CER calls
- generics [.NET Framework], open generic CER calls
ms.assetid: da3e4ff3-2e67-4668-9720-fa776c97407e
ms.openlocfilehash: 4df33b0cdf9759edec47f02b3feb671d03284ec8
ms.sourcegitcommit: c23d9666ec75b91741da43ee3d91c317d68c7327
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85803933"
---
# <a name="opengenericcercall-mda"></a>openGenericCERCall MDA

啟用 `openGenericCERCall` Managed 偵錯助理，警告根方法有泛型型別變數的限制執行區域 (CER) 圖形將在 JIT 編譯或原生映像產生時間處理，而且至少一個泛型型別變數是物件參考型別。

## <a name="symptoms"></a>徵狀

中止執行緒或卸載應用程式定義域時，未執行 CER。

## <a name="cause"></a>原因

在 JIT 編譯期間，包含物件參考型別的具現化僅具有代表性，因為共用產生的程式碼，而且每個物件參考型別變數都可能是任何物件參考型別。 這可以避免事先準備一些執行階段資源。

特別的是，具有泛型型別變數的方法可以在背景緩慢地配置資源。 這些稱為泛型字典項目。 例如，對於 `List<T> list = new List<T>();` `T` 是泛型型別變數的語句，執行時間必須查閱，而且可能會在執行時間建立確切的具現化，例如，等等 `List<Object>, List<String>` 。 這可能會因超出開發人員控制的各種原因而失敗，例如記憶體不足。

只應該在 JIT 編譯期間啟用此 MDA，而不是有確切的具現化時。

啟用此 MDA 時，可能的徵兆是 CER 不會針對不正確的具現化作用。 事實上，執行階段尚未嘗試在造成 MDA 啟用的情況下實作 CER。 因此，如果開發人員使用 CER 的共用具現化，則攔截不到預定 CER 區域內的 JIT 編譯錯誤、泛型型別載入錯誤或執行緒中止。

## <a name="resolution"></a>解決方案

請不要使用泛型型別變數，而這些變數是可能包含 CER 之方法的物件參考型別。

## <a name="effect-on-the-runtime"></a>對執行階段的影響

此 MDA 對 CLR 沒有影響。

## <a name="output"></a>輸出

以下是此 MDA 的輸出範例：
  
 ```output
 Method 'GenericMethodWithCer', which contains at least one constrained execution region, cannot be prepared automatically since it has one or more unbound generic type parameters.
 The caller must ensure this method is prepared explicitly at run time prior to execution.
 method name="GenericMethodWithCer"
 declaringType name="OpenGenericCERCall"
 ```

## <a name="configuration"></a>組態

```xml
<mdaConfig>
  <assistants>
    <openGenericCERCall/>
  </assistants>
</mdaConfig>
```  

## <a name="example"></a>範例

未執行 CER 程式碼。

```csharp
using System;
using System.Collections.Generic;
using System.Runtime.CompilerServices;

class Program
{
    static void Main(string[] args)
    {
        CallGenericMethods();
    }
    static void CallGenericMethods()
    {
        // This call is correct. The instantiation of the method
        // contains only nonreference types.
        MyClass.GenericMethodWithCer<int>();

        // This call is incorrect. A shared version of the method that
        // cannot be completely analyzed will be JIT-compiled. The
        // MDA will be activated at JIT-compile time, not at run time.
        MyClass.GenericMethodWithCer<String>();
    }
}

class MyClass
{
    public static void GenericMethodWithCer<T>()
    {
        RuntimeHelpers.PrepareConstrainedRegions();
        try
        {

        }
        finally
        {
            // This is the start of the CER.
            Console.WriteLine("In finally block.");
        }
    }
}
```

## <a name="see-also"></a>另請參閱

- <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareMethod%2A>
- <xref:System.Runtime.ConstrainedExecution>
- [使用 Managed 偵錯助理診斷錯誤](diagnosing-errors-with-managed-debugging-assistants.md)
