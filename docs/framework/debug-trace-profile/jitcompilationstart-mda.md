---
title: jitCompilationStart MDA
description: 使用 jitCompilationStart managed 偵錯工具（MDA），此功能會在即時（JIT）編譯器開始編譯 .NET 函式時開始報告。
ms.date: 03/30/2017
helpviewer_keywords:
- JIT compilation
- MDAs (managed debugging assistants), JIT compilation
- JitCompilationStart MDA
- managed debugging assistants (MDAs), JIT compilation
ms.assetid: 5ffd2857-d0ba-4342-9824-9ffe04ec135d
ms.openlocfilehash: bf2d09f433f0b8e4056fecd1f4e82bf3b91dd2bc
ms.sourcegitcommit: 3824ff187947572b274b9715b60c11269335c181
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84904126"
---
# <a name="jitcompilationstart-mda"></a>jitCompilationStart MDA
當 Just-In-time (JIT) 編譯器開始編譯函式時，會啟動 `jitCompilationStart` Managed 偵錯助理 (MDA)。  
  
## <a name="symptoms"></a>徵狀  
 因為 mscorjit.dll 已載入至處理序，所以已經是原生映像格式的程式的工作集大小會增加。  
  
## <a name="cause"></a>原因  
 並非所有與程式相依的組件都是以原生格式產生，或者以原生格式產生的組件未正確登錄。  
  
## <a name="resolution"></a>解決方案  
 啟用此 MDA 可讓您判斷哪一個函式正在進行 JIT 編譯。 判斷包含函式的組件是否以原生格式產生，並已正確登錄。  
  
## <a name="effect-on-the-runtime"></a>對執行階段的影響  
 此 MDA 會在方法剛要進行 JIT 編譯之前記錄訊息，所以啟用此 MDA 會對效能造成重大影響。 請注意，如果是內嵌的方法，這個 MDA 就不會另行產生訊息。  
  
## <a name="output"></a>輸出  
 下列程式碼範例會顯示範例輸出。 在本例中，輸出會顯示在組件 Test 中，類別 "ns2.CO" 上的方法 "m" 已經 JIT 編譯過。  
  
```output
method name="Test!ns2.C0::m"  
```  
  
## <a name="configuration"></a>設定  
 下列組態檔顯示的各種篩選器，可用來篩選出第一次 JIT 編譯時要報告哪些方法。 您可以將 name 屬性的值設定為，以指定報告所有方法 \* 。  
  
```xml  
<mdaConfig>  
  <assistants>  
    <jitCompilationStart>  
      <methods>  
        <match name="C0::m" />  
        <match name="MyMethod" />  
        <match name="C2::*" />  
        <match name="ns0::*" />  
        <match name="ns1.C0::*" />  
        <match name="ns2.C0::m" />  
        <match name="ns2.C0+N0::m" />  
      </methods>  
    </jitCompilationStart >  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a>範例  
 下列程式碼範例是用來搭配先前的組態檔。  
  
```csharp
using System;  
using System.Reflection;  
using System.Runtime.CompilerServices;  
using System.Runtime.InteropServices;  
  
public class Entry  
{  
    public static void Main(string[] args)  
    {  
        C0.m();  
        C1.MyMethod();  
        C2.m();  
  
        ns0.C0.m();  
        ns0.C0.N0.m();  
        ns0.C1.m();  
  
        ns1.C0.m();  
        ns1.C0.N0.m();  
  
        ns2.C0.m();  
        ns2.C0.N0.m();  
    }  
}  
  
public class C0  
{  
    [MethodImpl(MethodImplOptions.NoInlining)]  
    public static void m() { }  
}  
  
public class C1  
{  
    [MethodImpl(MethodImplOptions.NoInlining)]  
    public static void MyMethod() { }  
}  
  
public class C2  
{  
    [MethodImpl(MethodImplOptions.NoInlining)]  
    public static void m() { }  
}  
  
namespace ns0  
{  
    public class C0  
    {  
        [MethodImpl(MethodImplOptions.NoInlining)]  
        public static void m() { }  
  
        public class N0  
        {  
            [MethodImpl(MethodImplOptions.NoInlining)]  
            public static void m() { }  
        }  
    }  
  
    public class C1  
    {  
        [MethodImpl(MethodImplOptions.NoInlining)]  
        public static void m() { }  
    }  
}  
  
namespace ns1  
{  
    public class C0  
    {  
        [MethodImpl(MethodImplOptions.NoInlining)]  
        public static void m() { }  
        public class N0  
        {  
            [MethodImpl(MethodImplOptions.NoInlining)]  
            public static void m() { }  
        }  
    }  
}  
  
namespace ns2  
{  
    public class C0  
    {  
        [MethodImpl(MethodImplOptions.NoInlining)]  
        public static void m() { }  
  
        public class N0  
        {  
            [MethodImpl(MethodImplOptions.NoInlining)]  
            public static void m() { }  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [使用 Managed 偵錯助理診斷錯誤](diagnosing-errors-with-managed-debugging-assistants.md)
- [Interop 封送處理](../interop/interop-marshaling.md)
