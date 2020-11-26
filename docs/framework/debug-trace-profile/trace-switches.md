---
title: 追蹤參數
description: 探索可讓您啟用、停用和篩選追蹤輸出的追蹤參數。 .NET 提供 BooleanSwitch、TraceSwitch 和 SourceSwitch 類別。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tracing [.NET Framework], trace switches
- trace switches, about trace switches
- tracing [.NET Framework], level of detail
- switches, trace
- trace switches
- trace switches, creating custom
ms.assetid: 8ab913aa-f400-4406-9436-f45bc6e54fbe
ms.openlocfilehash: dfbff0a78b3c6c1318224ccc9608c1b816f9d5f1
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96238050"
---
# <a name="trace-switches"></a><span data-ttu-id="d6116-104">追蹤參數</span><span class="sxs-lookup"><span data-stu-id="d6116-104">Trace Switches</span></span>

<span data-ttu-id="d6116-105">追蹤參數可讓您啟用、停用和篩選追蹤輸出。</span><span class="sxs-lookup"><span data-stu-id="d6116-105">Trace switches enable you to enable, disable, and filter tracing output.</span></span> <span data-ttu-id="d6116-106">它們是存在於您的程式碼中的物件，並可透過 .config 檔案在外部設定。</span><span class="sxs-lookup"><span data-stu-id="d6116-106">They are objects that exist in your code and can be configured externally through the .config file.</span></span> <span data-ttu-id="d6116-107">.NET Framework 中提供三種類型的追蹤參數： <xref:System.Diagnostics.BooleanSwitch> 類別、 <xref:System.Diagnostics.TraceSwitch> 類別和 <xref:System.Diagnostics.SourceSwitch> 類別。</span><span class="sxs-lookup"><span data-stu-id="d6116-107">There are three types of trace switches provided in the .NET Framework: the <xref:System.Diagnostics.BooleanSwitch> class, the <xref:System.Diagnostics.TraceSwitch> class, and the <xref:System.Diagnostics.SourceSwitch> class.</span></span> <span data-ttu-id="d6116-108"><xref:System.Diagnostics.BooleanSwitch> 類別是做為切換參數，可啟用或停用各種追蹤陳述式。</span><span class="sxs-lookup"><span data-stu-id="d6116-108">The <xref:System.Diagnostics.BooleanSwitch> class acts as a toggle switch, either enabling or disabling a variety of trace statements.</span></span> <span data-ttu-id="d6116-109"><xref:System.Diagnostics.TraceSwitch> 和 <xref:System.Diagnostics.SourceSwitch> 類別可讓您針對特定追蹤層級啟用追蹤參數，以顯示針對該層級及其下所有層級指定的 <xref:System.Diagnostics.Trace> 或 <xref:System.Diagnostics.TraceSource> 訊息。</span><span class="sxs-lookup"><span data-stu-id="d6116-109">The <xref:System.Diagnostics.TraceSwitch> and <xref:System.Diagnostics.SourceSwitch> classes allow you to enable a trace switch for a particular tracing level so that the <xref:System.Diagnostics.Trace> or <xref:System.Diagnostics.TraceSource> messages specified for that level and all levels below it appear.</span></span> <span data-ttu-id="d6116-110">如果您停用此參數，就不會顯示追蹤訊息。</span><span class="sxs-lookup"><span data-stu-id="d6116-110">If you disable the switch, the trace messages will not appear.</span></span> <span data-ttu-id="d6116-111">所有這些類別都是衍生自抽象 (**MustInherit**) 類別 **Switch**，如同任何使用者開發的參數。</span><span class="sxs-lookup"><span data-stu-id="d6116-111">All these classes derive from the abstract (**MustInherit**) class **Switch**, as should any user-developed switches.</span></span>  
  
 <span data-ttu-id="d6116-112">追蹤參數對於篩選資訊很有用。</span><span class="sxs-lookup"><span data-stu-id="d6116-112">Trace switches can be useful for filtering information.</span></span> <span data-ttu-id="d6116-113">比方說，您可能想要查看資料存取模組中的每個追蹤訊息，但只查看應用程式其餘部分的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="d6116-113">For example, you might want to see every tracing message in a data access module, but only error messages in the rest of the application.</span></span> <span data-ttu-id="d6116-114">在此情況下，您會對資料存取模組使用一個追蹤參數，對應用程式的其餘部分使用一個參數。</span><span class="sxs-lookup"><span data-stu-id="d6116-114">In that case, you would use one trace switch for the data access module and one switch for the rest of the application.</span></span> <span data-ttu-id="d6116-115">使用 .config 檔案將參數設為適當的設定，即可控制您所接收的追蹤訊息類型。</span><span class="sxs-lookup"><span data-stu-id="d6116-115">By using the .config file to configure the switches to the appropriate settings, you could control what types of trace message you received.</span></span> <span data-ttu-id="d6116-116">如需詳細資訊，請參閱[如何：建立、初始化和設定追蹤參數](how-to-create-initialize-and-configure-trace-switches.md)。</span><span class="sxs-lookup"><span data-stu-id="d6116-116">For more information, see [How to: Create, Initialize and Configure Trace Switches](how-to-create-initialize-and-configure-trace-switches.md).</span></span>  
  
 <span data-ttu-id="d6116-117">一般而言，執行已部署的應用程式時，會停用其參數，這樣使用者就不需要觀察應用程式執行時，出現在螢幕上或塞滿記錄檔的許多無關的追蹤訊息。</span><span class="sxs-lookup"><span data-stu-id="d6116-117">Typically, a deployed application is executed with its switches disabled, so that users need not observe a lot of irrelevant trace messages appearing on a screen or filling up a log file as the application runs.</span></span> <span data-ttu-id="d6116-118">如果在應用程式執行期間發生問題，您可以停止應用程式、啟用參數，並重新啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="d6116-118">If a problem arises during application execution, you can stop the application, enable the switches, and restart the application.</span></span> <span data-ttu-id="d6116-119">然後就會顯示追蹤訊息。</span><span class="sxs-lookup"><span data-stu-id="d6116-119">Then the tracing messages will be displayed.</span></span>  
  
 <span data-ttu-id="d6116-120">若要使用參數，您必須先從 **BooleanSwitch** 類別、 **TraceSwitch** 類別或開發人員定義的參數類別建立參數物件。</span><span class="sxs-lookup"><span data-stu-id="d6116-120">To use a switch you must first create a switch object from a **BooleanSwitch** class, a **TraceSwitch** class, or a developer-defined switch class.</span></span> <span data-ttu-id="d6116-121">如需建立開發人員定義參數的詳細資訊，請參閱 .NET Framework 參考中的 <xref:System.Diagnostics.Switch> 類別。</span><span class="sxs-lookup"><span data-stu-id="d6116-121">For more information about creating developer-defined switches, see the <xref:System.Diagnostics.Switch> class in the .NET Framework reference.</span></span> <span data-ttu-id="d6116-122">然後您可以設定組態值，指定何時要使用該參數物件。</span><span class="sxs-lookup"><span data-stu-id="d6116-122">Then you set a configuration value that specifies when the switch object is to be used.</span></span> <span data-ttu-id="d6116-123">再於各種 **Trace** (或 **Debug**) 追蹤方法中測試參數物件的設定。</span><span class="sxs-lookup"><span data-stu-id="d6116-123">You then test the setting of the switch object in various **Trace** (or **Debug**) tracing methods.</span></span>  
  
## <a name="trace-levels"></a><span data-ttu-id="d6116-124">追蹤層級</span><span class="sxs-lookup"><span data-stu-id="d6116-124">Trace Levels</span></span>  

 <span data-ttu-id="d6116-125">當您使用 **TraceSwitch** 時，還有其他考量。</span><span class="sxs-lookup"><span data-stu-id="d6116-125">When you use **TraceSwitch**, there are additional considerations.</span></span> <span data-ttu-id="d6116-126">**TraceSwitch** 物件有四個會傳回 **布林** 值的屬性，指出該參數是否至少設定為某個特定層級：</span><span class="sxs-lookup"><span data-stu-id="d6116-126">A **TraceSwitch** object has four properties that return **Boolean** values indicating whether the switch is set to at least a particular level:</span></span>  
  
- <xref:System.Diagnostics.TraceSwitch.TraceError%2A?displayProperty=nameWithType>  
  
- <xref:System.Diagnostics.TraceSwitch.TraceWarning%2A?displayProperty=nameWithType>  
  
- <xref:System.Diagnostics.TraceSwitch.TraceInfo%2A?displayProperty=nameWithType>  
  
- <xref:System.Diagnostics.TraceSwitch.TraceVerbose%2A?displayProperty=nameWithType>  
  
 <span data-ttu-id="d6116-127">層級可讓您將所接收的追蹤資訊量，僅限於解決問題所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="d6116-127">Levels allow you to limit the amount of tracing information you receive to only that information needed to solve a problem.</span></span> <span data-ttu-id="d6116-128">您可以將追蹤參數設為適當的追蹤層級，以指定您想要的追蹤輸出詳細程度。</span><span class="sxs-lookup"><span data-stu-id="d6116-128">You specify the level of detail you want in your tracing output by setting and configuring trace switches to the appropriate trace level.</span></span> <span data-ttu-id="d6116-129">您可以接收錯誤訊息、警告訊息、告知性訊息、詳細的追蹤訊息，或沒有任何訊息。</span><span class="sxs-lookup"><span data-stu-id="d6116-129">You can receive error messages, warning messages, informational messages, verbose tracing messages, or no message at all.</span></span>  
  
 <span data-ttu-id="d6116-130">哪種訊息要與每個層級相關聯，完全由您決定。</span><span class="sxs-lookup"><span data-stu-id="d6116-130">It is entirely up to you to decide what kind of message to associate with each level.</span></span> <span data-ttu-id="d6116-131">一般而言，追蹤訊息的內容取決於與每個層級相關聯的項目，但您可以決定層級之間的差異。</span><span class="sxs-lookup"><span data-stu-id="d6116-131">Typically, the content of tracing messages depends on what you associate with each level, but you determine the differences between levels.</span></span> <span data-ttu-id="d6116-132">例如，您可能想要提供問題層級 3 (**資訊**) 的詳細說明，但在層級 1 (**錯誤**) 只提供錯誤參考編號。</span><span class="sxs-lookup"><span data-stu-id="d6116-132">You might want to provide detailed descriptions of a problem at level 3 (**Info**), for example, but provide only an error reference number at level 1 (**Error**).</span></span> <span data-ttu-id="d6116-133">哪種配置最適合您的應用程式，完全由您決定。</span><span class="sxs-lookup"><span data-stu-id="d6116-133">It is entirely up to you to decide what scheme works best in your application.</span></span>  
  
 <span data-ttu-id="d6116-134">這些屬性對應於 **TraceLevel** 列舉的值 1 到 4。</span><span class="sxs-lookup"><span data-stu-id="d6116-134">These properties correspond to the values 1 through 4 of the **TraceLevel** enumeration.</span></span> <span data-ttu-id="d6116-135">下表列出 **TraceLevel** 列舉及其值的層級。</span><span class="sxs-lookup"><span data-stu-id="d6116-135">The following table lists the levels of the **TraceLevel** enumeration and their values.</span></span>  
  
|<span data-ttu-id="d6116-136">列舉值</span><span class="sxs-lookup"><span data-stu-id="d6116-136">Enumerated value</span></span>|<span data-ttu-id="d6116-137">整數值</span><span class="sxs-lookup"><span data-stu-id="d6116-137">Integer value</span></span>|<span data-ttu-id="d6116-138">顯示的訊息類型 (或寫入至指定的輸出目標)</span><span class="sxs-lookup"><span data-stu-id="d6116-138">Type of message displayed (or written to a specified output target)</span></span>|  
|----------------------|-------------------|---------------------------------------------------------------------------|  
|<span data-ttu-id="d6116-139">關閉</span><span class="sxs-lookup"><span data-stu-id="d6116-139">Off</span></span>|<span data-ttu-id="d6116-140">0</span><span class="sxs-lookup"><span data-stu-id="d6116-140">0</span></span>|<span data-ttu-id="d6116-141">無</span><span class="sxs-lookup"><span data-stu-id="d6116-141">None</span></span>|  
|<span data-ttu-id="d6116-142">錯誤</span><span class="sxs-lookup"><span data-stu-id="d6116-142">Error</span></span>|<span data-ttu-id="d6116-143">1</span><span class="sxs-lookup"><span data-stu-id="d6116-143">1</span></span>|<span data-ttu-id="d6116-144">只有錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="d6116-144">Only error messages</span></span>|  
|<span data-ttu-id="d6116-145">警告</span><span class="sxs-lookup"><span data-stu-id="d6116-145">Warning</span></span>|<span data-ttu-id="d6116-146">2</span><span class="sxs-lookup"><span data-stu-id="d6116-146">2</span></span>|<span data-ttu-id="d6116-147">警告訊息和錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="d6116-147">Warning messages and error messages</span></span>|  
|<span data-ttu-id="d6116-148">資訊</span><span class="sxs-lookup"><span data-stu-id="d6116-148">Info</span></span>|<span data-ttu-id="d6116-149">3</span><span class="sxs-lookup"><span data-stu-id="d6116-149">3</span></span>|<span data-ttu-id="d6116-150">告知性訊息、警告訊息和錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="d6116-150">Informational messages, warning messages, and error messages</span></span>|  
|<span data-ttu-id="d6116-151">「詳細資訊」</span><span class="sxs-lookup"><span data-stu-id="d6116-151">Verbose</span></span>|<span data-ttu-id="d6116-152">4</span><span class="sxs-lookup"><span data-stu-id="d6116-152">4</span></span>|<span data-ttu-id="d6116-153">詳細資訊訊息、告知性訊息、警告訊息和錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="d6116-153">Verbose messages, informational messages, warning messages, and error messages</span></span>|  
  
 <span data-ttu-id="d6116-154">**TraceSwitch** 屬性會指出參數的最大追蹤層級。</span><span class="sxs-lookup"><span data-stu-id="d6116-154">The **TraceSwitch** properties indicate the maximum trace level for the switch.</span></span> <span data-ttu-id="d6116-155">也就是說，會針對所指定的層級以及其下所有層級寫入追蹤資訊。</span><span class="sxs-lookup"><span data-stu-id="d6116-155">That is, tracing information is written for the level specified as well as for all lower levels.</span></span> <span data-ttu-id="d6116-156">例如，如果 **TraceInfo** 是 **true**，則 **TraceError** 和 **TraceWarning** 也是 **true** ，但 **TraceVerbose** 很可能是 **false**。</span><span class="sxs-lookup"><span data-stu-id="d6116-156">For example, if **TraceInfo** is **true**, then **TraceError** and **TraceWarning** are also **true** but **TraceVerbose** might well be **false**.</span></span>  
  
 <span data-ttu-id="d6116-157">這些屬性是唯讀的。</span><span class="sxs-lookup"><span data-stu-id="d6116-157">These properties are read-only.</span></span> <span data-ttu-id="d6116-158">設定 **TraceLevel** 屬性時， **TraceSwitch** 物件會自動設定這些屬性。</span><span class="sxs-lookup"><span data-stu-id="d6116-158">The **TraceSwitch** object automatically sets them when the **TraceLevel** property is set.</span></span> <span data-ttu-id="d6116-159">例如：</span><span class="sxs-lookup"><span data-stu-id="d6116-159">For example:</span></span>  
  
```vb  
Dim myTraceSwitch As New TraceSwitch("SwitchOne", "The first switch")  
myTraceSwitch.Level = TraceLevel.Info  
' This message box displays true, because setting the level to  
' TraceLevel.Info sets all lower levels to true as well.  
MessageBox.Show(myTraceSwitch.TraceWarning.ToString())  
' This messagebox displays false.  
MessageBox.Show(myTraceSwitch.TraceVerbose.ToString())  
```  
  
```csharp  
System.Diagnostics.TraceSwitch myTraceSwitch =
   new System.Diagnostics.TraceSwitch("SwitchOne", "The first switch");  
myTraceSwitch.Level = System.Diagnostics.TraceLevel.Info;  
// This message box displays true, because setting the level to
// TraceLevel.Info sets all lower levels to true as well.  
MessageBox.Show(myTraceSwitch.TraceWarning.ToString());  
// This message box displays false.  
MessageBox.Show(myTraceSwitch.TraceVerbose.ToString());  
```  
  
## <a name="developer-defined-switches"></a><span data-ttu-id="d6116-160">開發人員定義的參數</span><span class="sxs-lookup"><span data-stu-id="d6116-160">Developer-Defined Switches</span></span>  

 <span data-ttu-id="d6116-161">除了提供 **BooleanSwitch** 和 **TraceSwitch**，您也可以從 **Switch** 類別繼承，再以自訂的方法來覆寫基底類別方法，以定義自己的參數。</span><span class="sxs-lookup"><span data-stu-id="d6116-161">In addition to providing **BooleanSwitch** and **TraceSwitch**, you can define your own switches by inheriting from the **Switch** class and overriding the base class methods with customized methods.</span></span> <span data-ttu-id="d6116-162">如需建立開發人員定義參數的詳細資訊，請參閱 .NET Framework 參考中的 <xref:System.Diagnostics.Switch> 類別。</span><span class="sxs-lookup"><span data-stu-id="d6116-162">For more information about creating developer-defined switches, see the <xref:System.Diagnostics.Switch> class in the .NET Framework reference.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d6116-163">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d6116-163">See also</span></span>

- [<span data-ttu-id="d6116-164">追蹤接聽項</span><span class="sxs-lookup"><span data-stu-id="d6116-164">Trace Listeners</span></span>](trace-listeners.md)
- [<span data-ttu-id="d6116-165">作法：將追蹤陳述式新增至應用程式程式碼</span><span class="sxs-lookup"><span data-stu-id="d6116-165">How to: Add Trace Statements to Application Code</span></span>](how-to-add-trace-statements-to-application-code.md)
- <span data-ttu-id="d6116-166">[追蹤和檢測應用程式](tracing-and-instrumenting-applications.md) (機器翻譯)</span><span class="sxs-lookup"><span data-stu-id="d6116-166">[Tracing and Instrumenting Applications](tracing-and-instrumenting-applications.md)</span></span>
