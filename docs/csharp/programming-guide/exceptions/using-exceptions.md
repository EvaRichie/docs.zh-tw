---
title: 使用例外狀況 - C# 程式設計手冊
description: 瞭解如何使用例外狀況。 例外狀況是由遇到錯誤的程式碼所擲回，並由更正錯誤的程式碼所攔截。
ms.date: 07/20/2015
helpviewer_keywords:
- exception handling [C#], about exception handling
- exceptions [C#], about exceptions
ms.assetid: 71472c62-320a-470a-97d2-67995180389d
ms.openlocfilehash: fb45381f1c6cfa2f27d036ead8e662b7a0d8d924
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87303370"
---
# <a name="use-exceptions-c-programming-guide"></a><span data-ttu-id="dc714-104">使用例外狀況（c # 程式設計手冊）</span><span class="sxs-lookup"><span data-stu-id="dc714-104">Use exceptions (C# programming guide)</span></span>

<span data-ttu-id="dc714-105">在 C# 中，若程式在執行階段發生錯誤，會利用一種稱為例外狀況的機制，讓整個程式都得知此狀況。</span><span class="sxs-lookup"><span data-stu-id="dc714-105">In C#, errors in the program at run time are propagated through the program by using a mechanism called exceptions.</span></span> <span data-ttu-id="dc714-106">例外狀況是由遇到錯誤的程式碼所擲回，並由可以更正此錯誤的程式碼所攔截。</span><span class="sxs-lookup"><span data-stu-id="dc714-106">Exceptions are thrown by code that encounters an error and caught by code that can correct the error.</span></span> <span data-ttu-id="dc714-107">例外狀況可由 .NET 執行時間或程式中的程式碼擲回。</span><span class="sxs-lookup"><span data-stu-id="dc714-107">Exceptions can be thrown by the .NET runtime or by code in a program.</span></span> <span data-ttu-id="dc714-108">一旦擲回了例外狀況，便會在呼叫堆疊中將此訊息往上傳，直至找到例外狀況的 `catch` 陳述式為止。</span><span class="sxs-lookup"><span data-stu-id="dc714-108">Once an exception is thrown, it propagates up the call stack until a `catch` statement for the exception is found.</span></span> <span data-ttu-id="dc714-109">未被攔截的例外狀況會由系統提供的泛型例外處理常式負責處理，這時會顯示對話方塊。</span><span class="sxs-lookup"><span data-stu-id="dc714-109">Uncaught exceptions are handled by a generic exception handler provided by the system that displays a dialog box.</span></span>  
  
 <span data-ttu-id="dc714-110">例外狀況會以衍生自 <xref:System.Exception> 的類別表示。</span><span class="sxs-lookup"><span data-stu-id="dc714-110">Exceptions are represented by classes derived from <xref:System.Exception>.</span></span> <span data-ttu-id="dc714-111">此類別會識別例外狀況的類型，並包含具有例外狀況詳細資料的屬性。</span><span class="sxs-lookup"><span data-stu-id="dc714-111">This class identifies the type of exception and contains properties that have details about the exception.</span></span> <span data-ttu-id="dc714-112">擲回例外狀況的作業包括建立例外狀況衍生類別的執行個體、選擇性地設定例外狀況的屬性，然後使用 `throw` 關鍵字擲回物件。</span><span class="sxs-lookup"><span data-stu-id="dc714-112">Throwing an exception involves creating an instance of an exception-derived class, optionally configuring properties of the exception, and then throwing the object by using the `throw` keyword.</span></span> <span data-ttu-id="dc714-113">例如：</span><span class="sxs-lookup"><span data-stu-id="dc714-113">For example:</span></span>  
  
 [!code-csharp[csProgGuideExceptions#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExceptions/CS/Exceptions.cs#1)]  
  
 <span data-ttu-id="dc714-114">擲回例外狀況之後，執行階段會檢查目前的陳述式是否在 `try` 區塊內。</span><span class="sxs-lookup"><span data-stu-id="dc714-114">After an exception is thrown, the runtime checks the current statement to see whether it is within a `try` block.</span></span> <span data-ttu-id="dc714-115">如果是的話，便會檢查與 `try` 區塊關聯的任何 `catch` 區塊，以查看其是否能攔截該例外狀況。</span><span class="sxs-lookup"><span data-stu-id="dc714-115">If it is, any `catch` blocks associated with the `try` block are checked to see whether they can catch the exception.</span></span> <span data-ttu-id="dc714-116">`Catch` 區塊通常會指定例外狀況類型；如果 `catch` 區塊的類型與例外狀況或其基底類別的類型相同，`catch` 區塊便可處理此方法。</span><span class="sxs-lookup"><span data-stu-id="dc714-116">`Catch` blocks typically specify exception types; if the type of the `catch` block is the same type as the exception, or a base class of the exception, the `catch` block can handle the method.</span></span> <span data-ttu-id="dc714-117">例如：</span><span class="sxs-lookup"><span data-stu-id="dc714-117">For example:</span></span>  
  
 [!code-csharp[csProgGuideExceptions#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExceptions/CS/Exceptions.cs#2)]  
  
 <span data-ttu-id="dc714-118">如果擲回例外狀況的陳述式不在 `try` 區塊內，或是例外狀況所在的 `try` 區塊內沒有相符的 `catch` 區塊，執行階段便會檢查 `try` 陳述式和 `catch` 區塊的呼叫方法。</span><span class="sxs-lookup"><span data-stu-id="dc714-118">If the statement that throws an exception is not within a `try` block or if the `try` block that encloses it has no matching `catch` block, the runtime checks the calling method for a `try` statement and `catch` blocks.</span></span> <span data-ttu-id="dc714-119">執行階段會繼續在呼叫堆疊中往上搜尋，直到找到相容的 `catch` 區塊。</span><span class="sxs-lookup"><span data-stu-id="dc714-119">The runtime continues up the calling stack, searching for a compatible `catch` block.</span></span> <span data-ttu-id="dc714-120">找到並執行 `catch` 區塊之後，控制項就會傳遞至該 `catch` 區塊後面的下一個陳述式。</span><span class="sxs-lookup"><span data-stu-id="dc714-120">After the `catch` block is found and executed, control is passed to the next statement after that `catch` block.</span></span>  
  
 <span data-ttu-id="dc714-121">`try` 陳述式可以包含多個 `catch` 區塊。</span><span class="sxs-lookup"><span data-stu-id="dc714-121">A `try` statement can contain more than one `catch` block.</span></span> <span data-ttu-id="dc714-122">第一個可以處理例外狀況的 `catch` 陳述式會先執行，接在後面的任何 `catch` 陳述式不論相容與否，都會予以略過。</span><span class="sxs-lookup"><span data-stu-id="dc714-122">The first `catch` statement that can handle the exception is executed; any following `catch` statements, even if they are compatible, are ignored.</span></span> <span data-ttu-id="dc714-123">因此，catch 區塊一律會從最特殊 (最具衍生性) 的區塊，排列到最不特殊的區塊。</span><span class="sxs-lookup"><span data-stu-id="dc714-123">Therefore, catch blocks should always be ordered from most specific (or most-derived) to least specific.</span></span> <span data-ttu-id="dc714-124">例如：</span><span class="sxs-lookup"><span data-stu-id="dc714-124">For example:</span></span>  
  
 [!code-csharp[csProgGuideExceptions#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExceptions/CS/Exceptions.cs#3)]  
  
 <span data-ttu-id="dc714-125">執行 `catch` 之前，執行階段會檢查 `finally` 區塊。</span><span class="sxs-lookup"><span data-stu-id="dc714-125">Before the `catch` block is executed, the runtime checks for `finally` blocks.</span></span> <span data-ttu-id="dc714-126">`Finally` 區塊可讓程式設計人員清除任何中止之 `try` 區塊中所殘留的任何模稜兩可狀態，或是不用等候執行階段內的記憶體回收行程完成物件，便可釋放任何外部資源 (例如圖形控制代碼、資料庫連接或檔案資料流)。</span><span class="sxs-lookup"><span data-stu-id="dc714-126">`Finally` blocks enable the programmer to clean up any ambiguous state that could be left over from an aborted `try` block, or to release any external resources (such as graphics handles, database connections or file streams) without waiting for the garbage collector in the runtime to finalize the objects.</span></span> <span data-ttu-id="dc714-127">例如：</span><span class="sxs-lookup"><span data-stu-id="dc714-127">For example:</span></span>  
  
 [!code-csharp[csProgGuideExceptions#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExceptions/CS/Exceptions.cs#4)]  
  
 <span data-ttu-id="dc714-128">當 `WriteByte()` 擲回例外狀況時，如果未呼叫 `file.Close()`，則嘗試重新開啟檔案之第二個 `try` 區塊中的程式碼會失敗，而且該檔案會保持鎖定狀態。</span><span class="sxs-lookup"><span data-stu-id="dc714-128">If `WriteByte()` threw an exception, the code in the second `try` block that tries to reopen the file would fail if `file.Close()` is not called, and the file would remain locked.</span></span> <span data-ttu-id="dc714-129">由於即使擲回例外狀況也會執行 `finally` 區塊，因此上述範例中的 `finally` 區塊可讓檔案正常關閉，並協助避免發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="dc714-129">Because `finally` blocks are executed even if an exception is thrown, the `finally` block in the previous example allows for the file to be closed correctly and helps avoid an error.</span></span>  
  
 <span data-ttu-id="dc714-130">擲回例外狀況之後，如果在呼叫堆疊中找不到相容的 `catch` 區塊，則會發生下列三種情況的其中一種：</span><span class="sxs-lookup"><span data-stu-id="dc714-130">If no compatible `catch` block is found on the call stack after an exception is thrown, one of three things occurs:</span></span>  
  
- <span data-ttu-id="dc714-131">如果例外狀況在完成項內，就會中止完成項並呼叫基底完成項 (如果有)。</span><span class="sxs-lookup"><span data-stu-id="dc714-131">If the exception is within a finalizer, the finalizer is aborted and the base finalizer, if any, is called.</span></span>  
  
- <span data-ttu-id="dc714-132">如果呼叫堆疊包含靜態建構函式或靜態欄位初始設定式，則會擲回 <xref:System.TypeInitializationException>，同時將原始例外狀況指派給新例外狀況的 <xref:System.Exception.InnerException%2A> 屬性。</span><span class="sxs-lookup"><span data-stu-id="dc714-132">If the call stack contains a static constructor, or a static field initializer, a <xref:System.TypeInitializationException> is thrown, with the original exception assigned to the <xref:System.Exception.InnerException%2A> property of the new exception.</span></span>  
  
- <span data-ttu-id="dc714-133">如果到達執行緒的開頭，則會終止執行緒。</span><span class="sxs-lookup"><span data-stu-id="dc714-133">If the start of the thread is reached, the thread is terminated.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="dc714-134">另請參閱</span><span class="sxs-lookup"><span data-stu-id="dc714-134">See also</span></span>

- [<span data-ttu-id="dc714-135">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="dc714-135">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="dc714-136">例外狀況和例外狀況處理</span><span class="sxs-lookup"><span data-stu-id="dc714-136">Exceptions and Exception Handling</span></span>](./index.md)
