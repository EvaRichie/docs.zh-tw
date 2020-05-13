---
title: 使用 UDP 服務
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- protocols, UDP
- network resources, UDP
- requesting data from Internet, UDP
- UDP
- receiving data, UDP
- Internet, UDP
- broadcasting messages to multiple addresses
- data requests, UDP
- UdpClient class, about UdpClient class
- sending data, UDP
- application protocols, UDP
ms.assetid: d5c3477a-e798-454c-a890-738ba14c5707
ms.openlocfilehash: 5ff40e8759b1732d4ad228b1414f96f9c37e5ac5
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83209769"
---
# <a name="use-udp-services"></a><span data-ttu-id="b4875-102">使用 UDP 服務</span><span class="sxs-lookup"><span data-stu-id="b4875-102">Use UDP services</span></span>

<span data-ttu-id="b4875-103"><xref:System.Net.Sockets.UdpClient> 類別使用 UDP 與網路服務通訊。</span><span class="sxs-lookup"><span data-stu-id="b4875-103">The <xref:System.Net.Sockets.UdpClient> class communicates with network services using UDP.</span></span> <span data-ttu-id="b4875-104"><xref:System.Net.Sockets.UdpClient> 類別屬性和方法使用 UDP 取出建立 <xref:System.Net.Sockets.Socket> 來要求和接收資料的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b4875-104">The properties and methods of the <xref:System.Net.Sockets.UdpClient> class abstract the details of creating a <xref:System.Net.Sockets.Socket> for requesting and receiving data using UDP.</span></span>

<span data-ttu-id="b4875-105">使用者資料包通訊協定 (UDP) 是一種簡單的通訊協定，致力於將資料傳遞到遠端主機。</span><span class="sxs-lookup"><span data-stu-id="b4875-105">User Datagram Protocol (UDP) is a simple protocol that makes a best effort to deliver data to a remote host.</span></span> <span data-ttu-id="b4875-106">不過，因為 UDP 通訊協定是一種無連線的通訊協定，所以傳送到遠端端點的 UDP 資料包不保證會送達，也不保證會以傳送的相同順序送達。</span><span class="sxs-lookup"><span data-stu-id="b4875-106">However, because the UDP protocol is a connectionless protocol, UDP datagrams sent to the remote endpoint are not guaranteed to arrive, nor are they guaranteed to arrive in the same sequence in which they are sent.</span></span> <span data-ttu-id="b4875-107">使用 UDP 應用程式必須準備好處理遺失、重複和不依順序的資料包。</span><span class="sxs-lookup"><span data-stu-id="b4875-107">Applications that use UDP must be prepared to handle missing, duplicate, and out-of-sequence datagrams.</span></span>

<span data-ttu-id="b4875-108">若要使用 UDP 傳送資料包，您必須知道裝載所需服務的網路裝置的網路位址，以及服務用來通訊的 UDP 連接埠編號。</span><span class="sxs-lookup"><span data-stu-id="b4875-108">To send a datagram using UDP, you must know the network address of the network device hosting the service you need and the UDP port number that the service uses to communicate.</span></span> <span data-ttu-id="b4875-109">網際網路指派的號碼授權單位（IANA）定義了泛型服務的埠號碼（請參閱[服務名稱和傳輸通訊協定埠號碼](https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml)登錄）。</span><span class="sxs-lookup"><span data-stu-id="b4875-109">The Internet Assigned Numbers Authority (IANA) defines port numbers for common services (see [Service Name and Transport Protocol Port Number Registry](https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml)).</span></span> <span data-ttu-id="b4875-110">不在 IANA 清單上的服務，其埠號碼會在1024到65535的範圍內。</span><span class="sxs-lookup"><span data-stu-id="b4875-110">Services not on the IANA list can have port numbers in the range 1,024 to 65,535.</span></span>

<span data-ttu-id="b4875-111">特殊的網路位址可用來支援 IP 型網路上的 UDP 廣播訊息。</span><span class="sxs-lookup"><span data-stu-id="b4875-111">Special network addresses are used to support UDP broadcast messages on IP-based networks.</span></span> <span data-ttu-id="b4875-112">下列討論內容會以網際網路上使用的 IP 第 4 版位址系列作為範例。</span><span class="sxs-lookup"><span data-stu-id="b4875-112">The following discussion uses the IP version 4 address family used on the Internet as an example.</span></span>

<span data-ttu-id="b4875-113">IP 第 4 版位址會使用 32 位元來指定網路位址。</span><span class="sxs-lookup"><span data-stu-id="b4875-113">IP version 4 addresses use 32 bits to specify a network address.</span></span> <span data-ttu-id="b4875-114">對於使用網路遮罩 255.255.255.0 的類別 C 位址，這些位元會分成四個八位元。</span><span class="sxs-lookup"><span data-stu-id="b4875-114">For class C addresses using a netmask of 255.255.255.0, these bits are separated into four octets.</span></span> <span data-ttu-id="b4875-115">以十進位表示時，四個八位元會形成熟悉的四點區隔標記法，例如 192.168.100.2。</span><span class="sxs-lookup"><span data-stu-id="b4875-115">When expressed in decimal, the four octets form the familiar dotted-quad notation, such as 192.168.100.2.</span></span> <span data-ttu-id="b4875-116">前兩個八位元 (在此範例中為 192.168) 形成網路編號，第三個八位元 (100) 定義子網路，而最後一個八位元 (2) 主機識別碼。</span><span class="sxs-lookup"><span data-stu-id="b4875-116">The first two octets (192.168 in this example) form the network number, the third octet (100) defines the subnet, and the final octet (2) is the host identifier.</span></span>

<span data-ttu-id="b4875-117">將 IP 位址的所有位元設定為其中一個或 255.255.255.255，構成受限的廣播位址。</span><span class="sxs-lookup"><span data-stu-id="b4875-117">Setting all the bits of an IP address to one, or 255.255.255.255, forms the limited broadcast address.</span></span> <span data-ttu-id="b4875-118">將 UDP 資料包傳送到這個位址時，會將訊息傳遞到本機網路區段上的任何主機。</span><span class="sxs-lookup"><span data-stu-id="b4875-118">Sending a UDP datagram to this address delivers the message to any host on the local network segment.</span></span> <span data-ttu-id="b4875-119">因為路由器永遠不會轉送傳送到這個位址的訊息，所以只有網路區段上的主機會收到廣播訊息。</span><span class="sxs-lookup"><span data-stu-id="b4875-119">Because routers never forward messages sent to this address, only hosts on the network segment receive the broadcast message.</span></span>

<span data-ttu-id="b4875-120">藉由設定主機識別碼的所有位元，即可將廣播導向至網路的特定部分。</span><span class="sxs-lookup"><span data-stu-id="b4875-120">Broadcasts can be directed to specific portions of a network by setting all bits of the host identifier.</span></span> <span data-ttu-id="b4875-121">例如，若要將廣播傳送至開頭為 192.168.1 之 IP 位址所識別網路上的所有主機，請使用位址 192.168.1.255。</span><span class="sxs-lookup"><span data-stu-id="b4875-121">For example, to send a broadcast to all hosts on the network identified by IP addresses starting with 192.168.1, use the address 192.168.1.255.</span></span>

<span data-ttu-id="b4875-122">下列程式碼範例使用 <xref:System.Net.Sockets.UdpClient>，在連接埠 11,000 上接聽 UDP 資料包。</span><span class="sxs-lookup"><span data-stu-id="b4875-122">The following code example uses a <xref:System.Net.Sockets.UdpClient> to listen for UDP datagrams on port 11,000.</span></span> <span data-ttu-id="b4875-123">用戶端會接收訊息字串，並將訊息寫入至主控台。</span><span class="sxs-lookup"><span data-stu-id="b4875-123">The client receives a message string and writes the message to the console.</span></span>

```vb
Imports System.Net
Imports System.Net.Sockets
Imports System.Text

Public Class UDPListener
   Private Const listenPort As Integer = 11000

   Private Shared Sub StartListener()
      Dim listener As New UdpClient(listenPort)
      Dim groupEP As New IPEndPoint(IPAddress.Any, listenPort)
      Try
         While True
            Console.WriteLine("Waiting for broadcast")
            Dim bytes As Byte() = listener.Receive(groupEP)
            Console.WriteLine("Received broadcast from {0} :", groupEP)
            Console.WriteLine(Encoding.ASCII.GetString(bytes, 0, bytes.Length))
         End While
      Catch e As SocketException
         Console.WriteLine(e)
      Finally
         listener.Close()
      End Try
   End Sub 'StartListener

   Public Shared Sub Main()
      StartListener()
   End Sub 'Main
End Class 'UDPListener
```

```csharp
using System;
using System.Net;
using System.Net.Sockets;
using System.Text;

public class UDPListener
{
    private const int listenPort = 11000;

    private static void StartListener()
    {
        UdpClient listener = new UdpClient(listenPort);
        IPEndPoint groupEP = new IPEndPoint(IPAddress.Any, listenPort);

        try
        {
            while (true)
            {
                Console.WriteLine("Waiting for broadcast");
                byte[] bytes = listener.Receive(ref groupEP);

                Console.WriteLine($"Received broadcast from {groupEP} :");
                Console.WriteLine($" {Encoding.ASCII.GetString(bytes, 0, bytes.Length)}");
            }
        }
        catch (SocketException e)
        {
            Console.WriteLine(e);
        }
        finally
        {
            listener.Close();
        }
    }

    public static void Main()
    {
        StartListener();
    }
}
```

<span data-ttu-id="b4875-124">下列程式碼範例使用 <xref:System.Net.Sockets.Socket>透過連接埠 11,000 將 UDP 資料包傳送到導向廣播位址 192.168.1.255。</span><span class="sxs-lookup"><span data-stu-id="b4875-124">The following code example uses a <xref:System.Net.Sockets.Socket> to send UDP datagrams to the directed broadcast address 192.168.1.255, using port 11,000.</span></span> <span data-ttu-id="b4875-125">用戶端會傳送命令列上指定的訊息字串。</span><span class="sxs-lookup"><span data-stu-id="b4875-125">The client sends the message string specified on the command line.</span></span>

```vb
Imports System.Net
Imports System.Net.Sockets
Imports System.Text

Public Class Program
    Public Shared Sub Main(args() As [String])
      Dim s As New Socket(AddressFamily.InterNetwork, SocketType.Dgram, ProtocolType.Udp)
      Dim broadcast As IPAddress = IPAddress.Parse("192.168.1.255")
      Dim sendbuf As Byte() = Encoding.ASCII.GetBytes(args(0))
      Dim ep As New IPEndPoint(broadcast, 11000)
      s.SendTo(sendbuf, ep)
      Console.WriteLine("Message sent to the broadcast address")
   End Sub 'Main
End Class
```

```csharp
using System;
using System.Net;
using System.Net.Sockets;
using System.Text;

class Program
{
    static void Main(string[] args)
    {
        Socket s = new Socket(AddressFamily.InterNetwork, SocketType.Dgram, ProtocolType.Udp);

        IPAddress broadcast = IPAddress.Parse("192.168.1.255");

        byte[] sendbuf = Encoding.ASCII.GetBytes(args[0]);
        IPEndPoint ep = new IPEndPoint(broadcast, 11000);

        s.SendTo(sendbuf, ep);

        Console.WriteLine("Message sent to the broadcast address");
    }
}
```

## <a name="see-also"></a><span data-ttu-id="b4875-126">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b4875-126">See also</span></span>

- <xref:System.Net.Sockets.UdpClient>
- <xref:System.Net.IPAddress>
