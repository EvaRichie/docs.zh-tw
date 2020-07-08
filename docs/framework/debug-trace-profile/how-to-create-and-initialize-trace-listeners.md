---
title: 如何：建立和初始設定追蹤接聽項
description: 瞭解如何在 .NET 中使用 Defaulttracelistener 這種類別來建立和初始化追蹤接聽項。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- initializing trace listeners
- trace listeners, creating
- trace listeners, initializing
- tracing [.NET Framework], trace listeners
- logs, trace listeners
ms.assetid: 21726de1-61ee-4fdc-9dd0-3be49324d066
ms.openlocfilehash: 752306124e41a7fb7458daccc8c2891631eb9616
ms.sourcegitcommit: 0edbeb66d71b8df10fcb374cfca4d731b58ccdb2
ms.contentlocale: zh-TW
ms.lasthandoff: 07/07/2020
ms.locfileid: "86051203"
---
# <a name="how-to-create-and-initialize-trace-listeners"></a><span data-ttu-id="9c069-103">如何：建立和初始設定追蹤接聽項</span><span class="sxs-lookup"><span data-stu-id="9c069-103">How to: Create and Initialize Trace Listeners</span></span>

<span data-ttu-id="9c069-104"><xref:System.Diagnostics.Debug?displayProperty=nameWithType> 和 <xref:System.Diagnostics.Trace?displayProperty=nameWithType> 類別會將訊息傳送給名稱為接聽程式的物件，以接收和處理這些訊息。</span><span class="sxs-lookup"><span data-stu-id="9c069-104">The <xref:System.Diagnostics.Debug?displayProperty=nameWithType> and <xref:System.Diagnostics.Trace?displayProperty=nameWithType> classes send messages to objects called listeners that receive and process these messages.</span></span> <span data-ttu-id="9c069-105"><xref:System.Diagnostics.DefaultTraceListener?displayProperty=nameWithType> 就是這類接聽程式之一，其會在啟用追蹤或偵錯時自動建立與初始化。</span><span class="sxs-lookup"><span data-stu-id="9c069-105">One such listener, the <xref:System.Diagnostics.DefaultTraceListener?displayProperty=nameWithType>, is automatically created and initialized when tracing or debugging is enabled.</span></span> <span data-ttu-id="9c069-106">如果您要將 <xref:System.Diagnostics.Trace> 或 <xref:System.Diagnostics.Debug> 輸出導向任何其他來源，您必須建立和初始化其他的追蹤接聽程式。</span><span class="sxs-lookup"><span data-stu-id="9c069-106">If you want <xref:System.Diagnostics.Trace> or <xref:System.Diagnostics.Debug> output to be directed to any additional sources, you must create and initialize additional trace listeners.</span></span>

<span data-ttu-id="9c069-107">您建立的接聽程式應反映出您應用程式的需求。</span><span class="sxs-lookup"><span data-stu-id="9c069-107">The listeners you create should reflect your application's needs.</span></span> <span data-ttu-id="9c069-108">例如，如果您想要取得所有追蹤輸出的文字記錄，可建立 <xref:System.Diagnostics.TextWriterTraceListener> 接聽程式，以在啟用時，將所有輸出寫入新的文字檔。</span><span class="sxs-lookup"><span data-stu-id="9c069-108">For example, if you want a text record of all trace output, create a <xref:System.Diagnostics.TextWriterTraceListener> listener, which writes all output to a new text file when it is enabled.</span></span> <span data-ttu-id="9c069-109">反之，如果您只想在應用程式執行期間檢視輸出，可建立 <xref:System.Diagnostics.ConsoleTraceListener> 接聽程式，將所有輸出導向主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="9c069-109">On the other hand, if you want to view output only during application execution, create a <xref:System.Diagnostics.ConsoleTraceListener> listener, which directs all output to a console window.</span></span> <span data-ttu-id="9c069-110"><xref:System.Diagnostics.EventLogTraceListener> 可以將追蹤輸出導向事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="9c069-110">The <xref:System.Diagnostics.EventLogTraceListener> can direct trace output to an event log.</span></span> <span data-ttu-id="9c069-111">如需詳細資訊，請參閱[追蹤接聽項](trace-listeners.md)。</span><span class="sxs-lookup"><span data-stu-id="9c069-111">For more information, see [Trace Listeners](trace-listeners.md).</span></span>

<span data-ttu-id="9c069-112">您可以在[應用程式組態檔](../configure-apps/index.md)或程式碼中建立追蹤接聽項。</span><span class="sxs-lookup"><span data-stu-id="9c069-112">You can create trace listeners in an [application configuration file](../configure-apps/index.md) or in your code.</span></span> <span data-ttu-id="9c069-113">建議您使用應用程式組態檔，因為它們可讓您新增、修改或移除追蹤接聽程式，而不必變更程式碼。</span><span class="sxs-lookup"><span data-stu-id="9c069-113">We recommend the use of application configuration files, because they let you add, modify, or remove trace listeners without having to change your code.</span></span>

### <a name="to-create-and-use-a-trace-listener-by-using-a-configuration-file"></a><span data-ttu-id="9c069-114">若要使用組態檔建立及使用追蹤接聽程式</span><span class="sxs-lookup"><span data-stu-id="9c069-114">To create and use a trace listener by using a configuration file</span></span>

1. <span data-ttu-id="9c069-115">在應用程式組態檔中，宣告您的追蹤接聽程式。</span><span class="sxs-lookup"><span data-stu-id="9c069-115">Declare your trace listener in your application configuration file.</span></span> <span data-ttu-id="9c069-116">如果您要建立的接聽程式需要任何其他物件，請一併將其宣告。</span><span class="sxs-lookup"><span data-stu-id="9c069-116">If the listener you are creating requires any other objects, declare them as well.</span></span> <span data-ttu-id="9c069-117">下列範例示範如何建立名稱為 `myListener` 的接聽程式，以進行文字檔 `TextWriterOutput.log` 的寫入作業。</span><span class="sxs-lookup"><span data-stu-id="9c069-117">The following example shows how to create a listener called `myListener` that writes to the text file `TextWriterOutput.log`.</span></span>

    ```xml
    <configuration>
      <system.diagnostics>
        <trace autoflush="false" indentsize="4">
          <listeners>
            <add name="myListener" type="System.Diagnostics.TextWriterTraceListener" initializeData="TextWriterOutput.log" />
            <remove name="Default" />
          </listeners>
        </trace>
      </system.diagnostics>
    </configuration>
    ```

2. <span data-ttu-id="9c069-118">使用程式碼中的 <xref:System.Diagnostics.Trace> 類別，將訊息寫入追蹤接聽程式。</span><span class="sxs-lookup"><span data-stu-id="9c069-118">Use the <xref:System.Diagnostics.Trace> class in your code to write a message to the trace listeners.</span></span>

    ```vb
    Trace.TraceInformation("Test message.")
    ' You must close or flush the trace to empty the output buffer.
    Trace.Flush()
    ```

    ```csharp
    Trace.TraceInformation("Test message.");
    // You must close or flush the trace to empty the output buffer.
    Trace.Flush();
    ```

### <a name="to-create-and-use-a-trace-listener-in-code"></a><span data-ttu-id="9c069-119">若要建立及使用程式碼中的追蹤接聽程式</span><span class="sxs-lookup"><span data-stu-id="9c069-119">To create and use a trace listener in code</span></span>

- <span data-ttu-id="9c069-120">將追蹤接聽程式加入 <xref:System.Diagnostics.Trace.Listeners%2A> 集合，並傳送追蹤資訊給接聽程式。</span><span class="sxs-lookup"><span data-stu-id="9c069-120">Add the trace listener to the <xref:System.Diagnostics.Trace.Listeners%2A> collection and send trace information to the listeners.</span></span>

    ```vb
    Trace.Listeners.Add(New TextWriterTraceListener("TextWriterOutput.log", "myListener"))
    Trace.TraceInformation("Test message.")
    ' You must close or flush the trace to empty the output buffer.
    Trace.Flush()
    ```

    ```csharp
    Trace.Listeners.Add(new TextWriterTraceListener("TextWriterOutput.log", "myListener"));
    Trace.TraceInformation("Test message.");
    // You must close or flush the trace to empty the output buffer.
    Trace.Flush();
    ```

    <span data-ttu-id="9c069-121">\- 或 -</span><span class="sxs-lookup"><span data-stu-id="9c069-121">\- or -</span></span>

- <span data-ttu-id="9c069-122">如果您不想讓接聽程式接收追蹤輸出，請不要將它加入 <xref:System.Diagnostics.Trace.Listeners%2A> 集合。</span><span class="sxs-lookup"><span data-stu-id="9c069-122">If you do not want your listener to receive trace output, do not add it to the <xref:System.Diagnostics.Trace.Listeners%2A> collection.</span></span> <span data-ttu-id="9c069-123">您可以呼叫接聽程式自己的輸出方法，透過獨立於 <xref:System.Diagnostics.Trace.Listeners%2A> 集合的接聽程式來發出輸出。</span><span class="sxs-lookup"><span data-stu-id="9c069-123">You can emit output through a listener independent of the <xref:System.Diagnostics.Trace.Listeners%2A> collection by calling the listener's own output methods.</span></span> <span data-ttu-id="9c069-124">下列範例示範如何將指令行寫入不在 <xref:System.Diagnostics.Trace.Listeners%2A> 集合內的接聽程式。</span><span class="sxs-lookup"><span data-stu-id="9c069-124">The following example shows how to write a line to a listener that is not in the <xref:System.Diagnostics.Trace.Listeners%2A> collection.</span></span>

    ```vb
    Dim myListener As New TextWriterTraceListener("TextWriterOutput.log", "myListener")
    myListener.WriteLine("Test message.")
    ' You must close or flush the trace listener to empty the output buffer.
    myListener.Flush()
    ```

    ```csharp
    TextWriterTraceListener myListener = new TextWriterTraceListener("TextWriterOutput.log", "myListener");
    myListener.WriteLine("Test message.");
    // You must close or flush the trace listener to empty the output buffer.
    myListener.Flush();
    ```

## <a name="see-also"></a><span data-ttu-id="9c069-125">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9c069-125">See also</span></span>

- [<span data-ttu-id="9c069-126">追蹤接聽程式</span><span class="sxs-lookup"><span data-stu-id="9c069-126">Trace Listeners</span></span>](trace-listeners.md)
- [<span data-ttu-id="9c069-127">追蹤參數</span><span class="sxs-lookup"><span data-stu-id="9c069-127">Trace Switches</span></span>](trace-switches.md)
- [<span data-ttu-id="9c069-128">如何：將追蹤陳述式加入至應用程式程式碼</span><span class="sxs-lookup"><span data-stu-id="9c069-128">How to: Add Trace Statements to Application Code</span></span>](how-to-add-trace-statements-to-application-code.md)
- [<span data-ttu-id="9c069-129">追蹤和稽核應用程式</span><span class="sxs-lookup"><span data-stu-id="9c069-129">Tracing and Instrumenting Applications</span></span>](tracing-and-instrumenting-applications.md)
