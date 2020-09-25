---
title: Connection 的事件
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 5a29de74-acfc-4134-8616-829dd7ce0710
ms.openlocfilehash: fd935306a493bf5a20f5cd6cd61a175c02d8bbba
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91203757"
---
# <a name="connection-events"></a><span data-ttu-id="eee31-102">Connection 的事件</span><span class="sxs-lookup"><span data-stu-id="eee31-102">Connection Events</span></span>

<span data-ttu-id="eee31-103">所有 .NET Framework 資料提供者都有具有兩個事件的 **連接** 物件，可讓您用來從資料來源抓取參考用訊息，或判斷 **連接** 的狀態是否已變更。</span><span class="sxs-lookup"><span data-stu-id="eee31-103">All of the .NET Framework data providers have **Connection** objects with two events that you can use to retrieve informational messages from a data source or to determine if the state of a **Connection** has changed.</span></span> <span data-ttu-id="eee31-104">下表描述 **連接** 物件的事件。</span><span class="sxs-lookup"><span data-stu-id="eee31-104">The following table describes the events of the **Connection** object.</span></span>  
  
|<span data-ttu-id="eee31-105">事件</span><span class="sxs-lookup"><span data-stu-id="eee31-105">Event</span></span>|<span data-ttu-id="eee31-106">描述</span><span class="sxs-lookup"><span data-stu-id="eee31-106">Description</span></span>|  
|-----------|-----------------|  
|<span data-ttu-id="eee31-107">**InfoMessage**</span><span class="sxs-lookup"><span data-stu-id="eee31-107">**InfoMessage**</span></span>|<span data-ttu-id="eee31-108">會在資訊訊息從資料來源傳回時發生。</span><span class="sxs-lookup"><span data-stu-id="eee31-108">Occurs when an informational message is returned from a data source.</span></span> <span data-ttu-id="eee31-109">資訊訊息是從資料來源傳回，且不會造成擲回例外狀況息。</span><span class="sxs-lookup"><span data-stu-id="eee31-109">Informational messages are messages from a data source that do not result in an exception being thrown.</span></span>|  
|<span data-ttu-id="eee31-110">**StateChange**</span><span class="sxs-lookup"><span data-stu-id="eee31-110">**StateChange**</span></span>|<span data-ttu-id="eee31-111">當 **連接** 的狀態變更時發生。</span><span class="sxs-lookup"><span data-stu-id="eee31-111">Occurs when the state of the **Connection** changes.</span></span>|  
  
## <a name="working-with-the-infomessage-event"></a><span data-ttu-id="eee31-112">使用 InfoMessage 事件</span><span class="sxs-lookup"><span data-stu-id="eee31-112">Working with the InfoMessage Event</span></span>  

 <span data-ttu-id="eee31-113">您可以使用 <xref:System.Data.SqlClient.SqlConnection.InfoMessage> 物件的 <xref:System.Data.SqlClient.SqlConnection> 事件，從 SQL Server 資料來源擷取警告和資訊訊息。</span><span class="sxs-lookup"><span data-stu-id="eee31-113">You can retrieve warnings and informational messages from a SQL Server data source using the <xref:System.Data.SqlClient.SqlConnection.InfoMessage> event of the <xref:System.Data.SqlClient.SqlConnection> object.</span></span> <span data-ttu-id="eee31-114">如果資料來源傳回嚴重性層級 11 到 16 的錯誤，則可能會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="eee31-114">Errors returned from the data source with a severity level of 11 through 16 cause an exception to be thrown.</span></span> <span data-ttu-id="eee31-115">不過，您可以使用 <xref:System.Data.SqlClient.SqlConnection.InfoMessage> 事件，從與錯誤無關的資料來源取得訊息。</span><span class="sxs-lookup"><span data-stu-id="eee31-115">However, the <xref:System.Data.SqlClient.SqlConnection.InfoMessage> event can be used to obtain messages from the data source that are not associated with an error.</span></span> <span data-ttu-id="eee31-116">以 Microsoft SQL Server 為例，任何嚴重性為 10 或以下的錯誤都視為資訊訊息，而且可以使用 <xref:System.Data.SqlClient.SqlConnection.InfoMessage> 事件進行擷取。</span><span class="sxs-lookup"><span data-stu-id="eee31-116">In the case of Microsoft SQL Server, any error with a severity of 10 or less is considered to be an informational message, and can be captured by using the <xref:System.Data.SqlClient.SqlConnection.InfoMessage> event.</span></span> <span data-ttu-id="eee31-117">如需詳細資訊，請參閱 [資料庫引擎錯誤嚴重性](/sql/relational-databases/errors-events/database-engine-error-severities) 文章。</span><span class="sxs-lookup"><span data-stu-id="eee31-117">For more information, see the [Database Engine Error Severities](/sql/relational-databases/errors-events/database-engine-error-severities) article.</span></span>
  
 <span data-ttu-id="eee31-118">此 <xref:System.Data.SqlClient.SqlConnection.InfoMessage> 事件會 <xref:System.Data.SqlClient.SqlInfoMessageEventArgs> 在其 [ **錯誤** ] 屬性中，接收來自資料來源之訊息集合的物件。</span><span class="sxs-lookup"><span data-stu-id="eee31-118">The <xref:System.Data.SqlClient.SqlConnection.InfoMessage> event receives an <xref:System.Data.SqlClient.SqlInfoMessageEventArgs> object containing, in its **Errors** property, a collection of the messages from the data source.</span></span> <span data-ttu-id="eee31-119">您可以在此集合中查詢 **錯誤物件的錯誤號碼** 和郵件內文，以及錯誤的來源。</span><span class="sxs-lookup"><span data-stu-id="eee31-119">You can query the **Error** objects in this collection for the error number and message text, as well as the source of the error.</span></span> <span data-ttu-id="eee31-120">SQL Server 的 .NET Framework 資料提供者也包含訊息來源處的資料庫、預存程序和行號等詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="eee31-120">The .NET Framework Data Provider for SQL Server also includes detail about the database, stored procedure, and line number that the message came from.</span></span>  
  
### <a name="example"></a><span data-ttu-id="eee31-121">範例</span><span class="sxs-lookup"><span data-stu-id="eee31-121">Example</span></span>  

 <span data-ttu-id="eee31-122">下列程式碼範例會顯示如何加入 <xref:System.Data.SqlClient.SqlConnection.InfoMessage> 事件的事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="eee31-122">The following code example shows how to add an event handler for the <xref:System.Data.SqlClient.SqlConnection.InfoMessage> event.</span></span>  
  
```vb  
' Assumes that connection represents a SqlConnection object.  
  AddHandler connection.InfoMessage, _  
    New SqlInfoMessageEventHandler(AddressOf OnInfoMessage)  
  
Private Shared Sub OnInfoMessage(sender As Object, _  
  args As SqlInfoMessageEventArgs)  
  Dim err As SqlError  
  For Each err In args.Errors  
    Console.WriteLine("The {0} has received a severity {1}, _  
       state {2} error number {3}\n" & _  
      "on line {4} of procedure {5} on server {6}:\n{7}", _  
      err.Source, err.Class, err.State, err.Number, err.LineNumber, _  
    err.Procedure, err.Server, err.Message)  
  Next  
End Sub  
```  
  
```csharp  
// Assumes that connection represents a SqlConnection object.  
  connection.InfoMessage +=
    new SqlInfoMessageEventHandler(OnInfoMessage);  
  
protected static void OnInfoMessage(  
  object sender, SqlInfoMessageEventArgs args)  
{  
  foreach (SqlError err in args.Errors)  
  {  
    Console.WriteLine(  
  "The {0} has received a severity {1}, state {2} error number {3}\n" +  
  "on line {4} of procedure {5} on server {6}:\n{7}",  
   err.Source, err.Class, err.State, err.Number, err.LineNumber,
   err.Procedure, err.Server, err.Message);  
  }  
}  
```  
  
## <a name="handling-errors-as-infomessages"></a><span data-ttu-id="eee31-123">將錯誤視為 InfoMessage 處理</span><span class="sxs-lookup"><span data-stu-id="eee31-123">Handling Errors as InfoMessages</span></span>  

 <span data-ttu-id="eee31-124">只有在資訊訊息及警告訊息是從伺服器傳回時，才會正常地引發 <xref:System.Data.SqlClient.SqlConnection.InfoMessage> 事件。</span><span class="sxs-lookup"><span data-stu-id="eee31-124">The <xref:System.Data.SqlClient.SqlConnection.InfoMessage> event will normally fire only for informational and warning messages that are sent from the server.</span></span> <span data-ttu-id="eee31-125">不過，當實際的錯誤發生時，會停止執行起始伺服器作業的 **ExecuteNonQuery** 或 **ExecuteReader** 方法，並擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="eee31-125">However, when an actual error occurs, the execution of the **ExecuteNonQuery** or **ExecuteReader** method that initiated the server operation is halted and an exception is thrown.</span></span>  
  
 <span data-ttu-id="eee31-126">若要繼續處理命令中的其餘陳述式，而不理會伺服器產生的任何錯誤，請將 <xref:System.Data.SqlClient.SqlConnection.FireInfoMessageEventOnUserErrors%2A> 的 <xref:System.Data.SqlClient.SqlConnection> 屬性設定為 `true`。</span><span class="sxs-lookup"><span data-stu-id="eee31-126">If you want to continue processing the rest of the statements in a command regardless of any errors produced by the server, set the <xref:System.Data.SqlClient.SqlConnection.FireInfoMessageEventOnUserErrors%2A> property of the <xref:System.Data.SqlClient.SqlConnection> to `true`.</span></span> <span data-ttu-id="eee31-127">這麼做會使得連接引發錯誤的 <xref:System.Data.SqlClient.SqlConnection.InfoMessage> 事件，而非擲回例外狀況並中斷處理。</span><span class="sxs-lookup"><span data-stu-id="eee31-127">Doing this causes the connection to fire the <xref:System.Data.SqlClient.SqlConnection.InfoMessage> event for errors instead of throwing an exception and interrupting processing.</span></span> <span data-ttu-id="eee31-128">用戶端應用程式接下來處理這個事件並回應錯誤狀況。</span><span class="sxs-lookup"><span data-stu-id="eee31-128">The client application can then handle this event and respond to error conditions.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="eee31-129">必須將嚴重性層級 17 或以上的錯誤 (造成伺服器停止處理命令) 當做例外狀況處理。</span><span class="sxs-lookup"><span data-stu-id="eee31-129">An error with a severity level of 17 or above that causes the server to stop processing the command must be handled as an exception.</span></span> <span data-ttu-id="eee31-130">在此情況下會擲回例外狀況，而不理會<xref:System.Data.SqlClient.SqlConnection.InfoMessage> 事件中如何處理錯誤。</span><span class="sxs-lookup"><span data-stu-id="eee31-130">In this case, an exception is thrown regardless of how the error is handled in the <xref:System.Data.SqlClient.SqlConnection.InfoMessage> event.</span></span>  
  
## <a name="working-with-the-statechange-event"></a><span data-ttu-id="eee31-131">使用 StateChange 事件</span><span class="sxs-lookup"><span data-stu-id="eee31-131">Working with the StateChange Event</span></span>  

 <span data-ttu-id="eee31-132">當**連接**的狀態變更時，就會發生**StateChange**事件。</span><span class="sxs-lookup"><span data-stu-id="eee31-132">The **StateChange** event occurs when the state of a **Connection** changes.</span></span> <span data-ttu-id="eee31-133">**StateChange**事件接收 <xref:System.Data.StateChangeEventArgs> ，可讓您使用**OriginalState**和**CurrentState**屬性來判斷**連接**狀態的變更。</span><span class="sxs-lookup"><span data-stu-id="eee31-133">The **StateChange** event receives <xref:System.Data.StateChangeEventArgs> that enable you to determine the change in state of the **Connection** by using the **OriginalState** and **CurrentState** properties.</span></span> <span data-ttu-id="eee31-134">**OriginalState**屬性是 <xref:System.Data.ConnectionState> 列舉，指出**連接**在變更之前的狀態。</span><span class="sxs-lookup"><span data-stu-id="eee31-134">The **OriginalState** property is a <xref:System.Data.ConnectionState> enumeration that indicates the state of the **Connection** before it changed.</span></span> <span data-ttu-id="eee31-135">**CurrentState** 是列舉型別 <xref:System.Data.ConnectionState> ，表示變更之後的 **連接** 狀態。</span><span class="sxs-lookup"><span data-stu-id="eee31-135">**CurrentState** is a <xref:System.Data.ConnectionState> enumeration that indicates the state of the **Connection** after it changed.</span></span>  
  
 <span data-ttu-id="eee31-136">下列程式碼範例會在**連接**狀態變更時，使用**StateChange**事件將訊息寫入主控台。</span><span class="sxs-lookup"><span data-stu-id="eee31-136">The following code example uses the **StateChange** event to write a message to the console when the state of the **Connection** changes.</span></span>  
  
```vb  
' Assumes connection represents a SqlConnection object.  
  AddHandler connection.StateChange, _  
    New StateChangeEventHandler(AddressOf OnStateChange)  
  
Protected Shared Sub OnStateChange( _  
  sender As Object, args As StateChangeEventArgs)  
  
  Console.WriteLine( _  
  "The current Connection state has changed from {0} to {1}.", _  
  args.OriginalState, args.CurrentState)  
End Sub  
```  
  
```csharp  
// Assumes connection represents a SqlConnection object.  
  connection.StateChange  += new StateChangeEventHandler(OnStateChange);  
  
protected static void OnStateChange(object sender,
  StateChangeEventArgs args)  
{  
  Console.WriteLine(  
    "The current Connection state has changed from {0} to {1}.",  
      args.OriginalState, args.CurrentState);  
}  
```  
  
## <a name="see-also"></a><span data-ttu-id="eee31-137">另請參閱</span><span class="sxs-lookup"><span data-stu-id="eee31-137">See also</span></span>

- [<span data-ttu-id="eee31-138">連接到資料來源</span><span class="sxs-lookup"><span data-stu-id="eee31-138">Connecting to a Data Source</span></span>](connecting-to-a-data-source.md)
- <span data-ttu-id="eee31-139">[ADO.NET 概觀](ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="eee31-139">[ADO.NET Overview](ado-net-overview.md)</span></span>
