---
title: 作法：使用追蹤和偵錯進行條件式編譯
description: 瞭解如何在編譯 .NET 應用程式時，使用追蹤和調試條件屬性來有條件地編譯。
ms.date: 03/30/2017
helpviewer_keywords:
- trace compiler options
- trace statements
- compiling source code, trace statements
- tracing [.NET Framework], enabling or disabling
- tracing [.NET Framework], compiling conditionally
- TRACE directive
- conditional compilation, tracing code
ms.assetid: 56d051c3-012c-42c1-9a58-7270edc624aa
ms.openlocfilehash: 895e39593b5e84d708392d3d994267b25bc4eeea
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96244167"
---
# <a name="how-to-compile-conditionally-with-trace-and-debug"></a>作法：使用追蹤和偵錯進行條件式編譯

當您於開發期間偵錯應用程式時，追蹤及偵錯輸出都會移至 Visual Studio 中的 [輸出] 視窗。 然而，若要在已部署的應用程式中包含追蹤功能，您必須在啟用 **TRACE** 編譯器指示詞的情況下編譯已經過檢測的應用程式。 這可將追蹤程式碼編譯成應用程式的發行版本。 如果您沒有啟用 **TRACE** 指示詞，則在編譯期間會忽略所有的追蹤程式碼，並且不會在您將部署的可執行程式碼中包含追蹤程式碼。  
  
 追蹤和偵錯方法均具有相關聯的Conditional 屬性。 例如，如果追蹤的 Conditional 屬性為 **true**，則會在組件 (已編譯的 .exe 檔案或 .dll) 中包含所有的追蹤陳述式，如果 **Trace** Conditional 屬性為 **false**，則不會包含追蹤陳述式。  
  
 您可以為組建開啟 **Trace** 或 **Debug** Conditional 屬性，或兩者都開啟或都關閉。 因此，組建可分為四種類型：**Debug**、**Trace**、兩者都開啟或兩者都關閉。 部分產品部署的發行組建可能不含兩者；大部分的偵錯組建則包含兩者。  
  
 您可用數種方式來指定應用程式的編譯器設定：  
  
- 屬性頁  
  
- 命令列  
  
- **#CONST** (若為 Visual Basic) 和 **#define** (若為 C#)  
  
### <a name="to-change-compile-settings-from-the-property-pages-dialog-box"></a>從屬性頁對話方塊變更編譯設定  
  
1. 以滑鼠右鍵按一下方案總管 中的專案節點。  
  
2. 從捷徑功能表中選擇 [屬性]。  
  
    - 在 Visual Basic 中，按一下屬性頁左窗格內的 [編譯] 索引標籤，然後按一下 [進階編譯選項] 按鈕，即可顯示 [進階編譯器設定] 對話方塊。 請選取您想要啟用之編譯器設定的核取方塊。 清除您想要停用之設定值的核取方塊。  
  
    - 在 C# 中，按一下屬性頁左窗格內的 [建置] 索引標籤，然後選取您想要啟用之編譯器設定的核取方塊。 清除您想要停用之設定值的核取方塊。  
  
### <a name="to-compile-instrumented-code-using-the-command-line"></a>使用命令列來編譯已經過檢測的程式碼  
  
1. 在命令列上設定條件式編譯器參數。 編譯器會在可執行檔中包含追蹤或偵錯程式碼。  
  
     例如，在命令列上輸入下列編譯器指令會在已編譯可執行檔中包含追蹤程式碼：  
  
     針對 Visual Basic： **vbc -r:System.dll-d:TRACE = TRUE-d:DEBUG = FALSE MyApplication .vb**  
  
     若為 c #： **csc -r:System.dll-d:TRACE-d:DEBUG = FALSE MyApplication.cs**  
  
    > [!TIP]
    > 若要編譯一個以上的應用程式檔案，請在檔案名稱之間保留一個空格，例如，**MyApplication1.vb MyApplication2.vb MyApplication3.vb** 或 **MyApplication1.cs MyApplication2.cs MyApplication3.cs**。  
  
     上述範例中使用的條件式編譯指示詞的意義如下：  
  
    |指示詞|意義|  
    |---------------|-------------|  
    |`vbc`|Visual Basic 編譯器|  
    |`csc`|C# 編譯器|  
    |`-r:`|參考外部組件 (EXE 或 DLL)|  
    |`-d:`|定義條件式編譯的符號|  
  
    > [!NOTE]
    > 您必須使用大寫字母來拼寫 TRACE 或 DEBUG。 如需條件式編譯命令的詳細資訊，請在命令提示字元中輸入 `vbc /?` (若為 Visual Basic) 或 `csc /?` (若為 C#)。 如需詳細資訊，請參閱[從命令列建置](../../csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md) (C#) 或[叫用命令列編譯器](../../visual-basic/reference/command-line-compiler/how-to-invoke-the-command-line-compiler.md) (Visual Basic)。  
  
### <a name="to-perform-conditional-compilation-using-const-or-define"></a>使用 #CONST 或 #define 來執行條件式編譯  
  
1. 請在原始程式碼檔案上方輸入適用於您的程式語言之陳述式。  
  
    |語言|陳述式|結果|  
    |--------------|---------------|------------|  
    |**Visual Basic**|**#CONST TRACE = true**|啟用追蹤|  
    ||**#CONST TRACE = false**|停用追蹤|  
    ||**#CONST DEBUG = true**|啟用偵錯|  
    ||**#CONST DEBUG = false**|停用偵錯|  
    |**C#**|**#define TRACE**|啟用追蹤|  
    ||**#undef TRACE**|停用追蹤|  
    ||**#define DEBUG**|啟用偵錯|  
    ||**#undef DEBUG**|停用偵錯|  
  
### <a name="to-disable-tracing-or-debugging"></a>若要停用追蹤或偵錯  
  
請刪除原始程式碼中的編譯器指示詞。  
  
\- 或 -  
  
將編譯器指示詞標為註解。  
  
> [!NOTE]
> 當您準備編譯時，可從 [建置] 功能表中選取 [建置]，或使用命令列方法 (但不輸入 **d:**) 來定義條件式編譯的符號。  
  
## <a name="see-also"></a>另請參閱

- [追蹤和檢測應用程式](tracing-and-instrumenting-applications.md) (機器翻譯)
- [作法：建立、初始化和設定追蹤參數](how-to-create-initialize-and-configure-trace-switches.md)
- [追蹤參數](trace-switches.md)
- [追蹤接聽項](trace-listeners.md)
- [作法：將追蹤陳述式新增至應用程式程式碼](how-to-add-trace-statements-to-application-code.md)
- [如何為 Visual Studio 命令列設定環境變數](../../csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md)
- [作法：叫用命令列編譯器](../../visual-basic/reference/command-line-compiler/how-to-invoke-the-command-line-compiler.md)
