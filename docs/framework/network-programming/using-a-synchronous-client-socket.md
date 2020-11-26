---
title: 使用同步用戶端通訊端
description: 此範例顯示 .NET Framework 中的同步用戶端通訊端，此通訊端會在網路作業完成時暫停應用程式。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- application protocols, sockets
- sending data, sockets
- data requests, sockets
- requesting data from Internet, sockets
- synchronous client sockets
- Socket class, synchronous client sockets
- receiving data, sockets
- sockets, synchronous client sockets
- protocols, sockets
- Internet, sockets
- client sockets
ms.assetid: 945d00c6-7202-466c-9df9-140b84156d43
ms.openlocfilehash: f198f283f2acfdcfbafed25baecb02a64e9d1e26
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96236308"
---
# <a name="using-a-synchronous-client-socket"></a><span data-ttu-id="b827b-103">使用同步用戶端通訊端</span><span class="sxs-lookup"><span data-stu-id="b827b-103">Using a Synchronous Client Socket</span></span>

<span data-ttu-id="b827b-104">在網路作業完成時，同步用戶端通訊端會暫止應用程式。</span><span class="sxs-lookup"><span data-stu-id="b827b-104">A synchronous client socket suspends the application program while the network operation completes.</span></span> <span data-ttu-id="b827b-105">同步通訊端不適用於大量使用網路以進行作業的應用程式，但它們可以啟用其他應用程式的網路服務簡單存取。</span><span class="sxs-lookup"><span data-stu-id="b827b-105">Synchronous sockets are not suitable for applications that make heavy use of the network for their operation, but they can enable simple access to network services for other applications.</span></span>  
  
 <span data-ttu-id="b827b-106">若要傳送資料，請傳遞位元組陣列給其中一個 <xref:System.Net.Sockets.Socket> 類別的資料傳送方法 (<xref:System.Net.Sockets.Socket.Send%2A> 和 <xref:System.Net.Sockets.Socket.SendTo%2A>)。</span><span class="sxs-lookup"><span data-stu-id="b827b-106">To send data, pass a byte array to one of the <xref:System.Net.Sockets.Socket> class's send-data methods (<xref:System.Net.Sockets.Socket.Send%2A> and <xref:System.Net.Sockets.Socket.SendTo%2A>).</span></span> <span data-ttu-id="b827b-107">下列範例會使用 <xref:System.Text.Encoding.ASCII%2A?displayProperty=nameWithType> 屬性將字串編碼成位元組陣列緩衝區，然後使用 **Send** 方法將緩衝區傳送給網路裝置。</span><span class="sxs-lookup"><span data-stu-id="b827b-107">The following example encodes a string into a byte array buffer using the <xref:System.Text.Encoding.ASCII%2A?displayProperty=nameWithType> property and then transmits the buffer to the network device using the **Send** method.</span></span> <span data-ttu-id="b827b-108">**Send** 方法會傳回送給網路裝置的位元組數目。</span><span class="sxs-lookup"><span data-stu-id="b827b-108">The **Send** method returns the number of bytes sent to the network device.</span></span>  
  
```vb  
Dim msg As Byte() = _  
    System.Text.Encoding.ASCII.GetBytes("This is a test.")  
Dim bytesSent As Integer = s.Send(msg)  
```  
  
```csharp  
byte[] msg = System.Text.Encoding.ASCII.GetBytes("This is a test");  
int bytesSent = s.Send(msg);  
```  
  
 <span data-ttu-id="b827b-109">**Send** 方法從緩衝區移除位元組，並將它們佇列到要傳送至網路裝置的網路介面。</span><span class="sxs-lookup"><span data-stu-id="b827b-109">The **Send** method removes the bytes from the buffer and queues them with the network interface to be sent to the network device.</span></span> <span data-ttu-id="b827b-110">網路介面可能不會立即傳送資料，但它終究會傳送，只要以 <xref:System.Net.Sockets.Socket.Shutdown%2A> 方法正常關閉連線。</span><span class="sxs-lookup"><span data-stu-id="b827b-110">The network interface might not send the data immediately, but it will send it eventually, as long as the connection is closed normally with the <xref:System.Net.Sockets.Socket.Shutdown%2A> method.</span></span>  
  
 <span data-ttu-id="b827b-111">若要從網路裝置接收資料，請傳遞緩衝區給其中一個 **Socket** 類別的資料接收方法 (<xref:System.Net.Sockets.Socket.Receive%2A> 和 <xref:System.Net.Sockets.Socket.ReceiveFrom%2A>)。</span><span class="sxs-lookup"><span data-stu-id="b827b-111">To receive data from a network device, pass a buffer to one of the **Socket** class's receive-data methods (<xref:System.Net.Sockets.Socket.Receive%2A> and <xref:System.Net.Sockets.Socket.ReceiveFrom%2A>).</span></span> <span data-ttu-id="b827b-112">同步通訊端會暫停應用程式，直到從網路收到位元組或通訊端關閉為止。</span><span class="sxs-lookup"><span data-stu-id="b827b-112">Synchronous sockets will suspend the application until bytes are received from the network or until the socket is closed.</span></span> <span data-ttu-id="b827b-113">下列範例會從網路接收資料，再將它顯示在主控台上。</span><span class="sxs-lookup"><span data-stu-id="b827b-113">The following example receives data from the network and then displays it on the console.</span></span> <span data-ttu-id="b827b-114">此範例假設來自網路的資料為 ASCII 編碼的文字。</span><span class="sxs-lookup"><span data-stu-id="b827b-114">The example assumes that the data coming from the network is ASCII-encoded text.</span></span> <span data-ttu-id="b827b-115">**Receive** 方法會傳回從網路收到的位元組數目。</span><span class="sxs-lookup"><span data-stu-id="b827b-115">The **Receive** method returns the number of bytes received from the network.</span></span>  
  
```vb  
Dim bytes(1024) As Byte  
Dim bytesRec = s.Receive(bytes)  
Console.WriteLine("Echoed text = {0}", _  
    System.Text.Encoding.ASCII.GetString(bytes, 0, bytesRec))  
```  
  
```csharp  
byte[] bytes = new byte[1024];  
int bytesRec = s.Receive(bytes);  
Console.WriteLine("Echoed text = {0}",  
    System.Text.Encoding.ASCII.GetString(bytes, 0, bytesRec));  
```  
  
 <span data-ttu-id="b827b-116">當不再需要通訊端時，您需要藉由呼叫 <xref:System.Net.Sockets.Socket.Shutdown%2A> 方法，然後呼叫 **Close** 方法釋放它。</span><span class="sxs-lookup"><span data-stu-id="b827b-116">When the socket is no longer needed, you need to release it by calling the <xref:System.Net.Sockets.Socket.Shutdown%2A> method and then calling the **Close** method.</span></span> <span data-ttu-id="b827b-117">下列範例會釋放 **通訊端**。</span><span class="sxs-lookup"><span data-stu-id="b827b-117">The following example releases a **Socket**.</span></span> <span data-ttu-id="b827b-118"><xref:System.Net.Sockets.SocketShutdown> 列舉定義常數，表示傳送、接收或是兩者時，是否應該關閉通訊端。</span><span class="sxs-lookup"><span data-stu-id="b827b-118">The <xref:System.Net.Sockets.SocketShutdown> enumeration defines constants that indicate whether the socket should be closed for sending, for receiving, or for both.</span></span>  
  
```vb  
s.Shutdown(SocketShutdown.Both)  
s.Close()  
```  
  
```csharp  
s.Shutdown(SocketShutdown.Both);  
s.Close();  
```  
  
## <a name="see-also"></a><span data-ttu-id="b827b-119">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b827b-119">See also</span></span>

- [<span data-ttu-id="b827b-120">使用非同步用戶端通訊端</span><span class="sxs-lookup"><span data-stu-id="b827b-120">Using an Asynchronous Client Socket</span></span>](using-an-asynchronous-client-socket.md)
- [<span data-ttu-id="b827b-121">透過通訊端接聽</span><span class="sxs-lookup"><span data-stu-id="b827b-121">Listening with Sockets</span></span>](listening-with-sockets.md)
- [<span data-ttu-id="b827b-122">同步用戶端通訊端範例</span><span class="sxs-lookup"><span data-stu-id="b827b-122">Synchronous Client Socket Example</span></span>](synchronous-client-socket-example.md)
