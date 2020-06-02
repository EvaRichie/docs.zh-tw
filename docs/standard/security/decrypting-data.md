---
title: 解密資料
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data [.NET Framework], decryption
- symmetric decryption
- asymmetric decryption
- decryption
ms.assetid: 9b266b6c-a9b2-4d20-afd8-b3a0d8fd48a0
ms.openlocfilehash: 844561c0d207106a183243f5f2b3e0cea3e70422
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288364"
---
# <a name="decrypting-data"></a><span data-ttu-id="727b4-102">解密資料</span><span class="sxs-lookup"><span data-stu-id="727b4-102">Decrypting Data</span></span>

<span data-ttu-id="727b4-103">解密是加密的反向作業。</span><span class="sxs-lookup"><span data-stu-id="727b4-103">Decryption is the reverse operation of encryption.</span></span> <span data-ttu-id="727b4-104">針對秘密金鑰加密，您必須同時知道金鑰和用來加密資料的 IV。</span><span class="sxs-lookup"><span data-stu-id="727b4-104">For secret-key encryption, you must know both the key and IV that were used to encrypt the data.</span></span> <span data-ttu-id="727b4-105">針對公開金鑰加密，您必須知道公開金鑰 (如果使用私密金鑰來加密資料) 或私密金鑰 (如果使用公開金鑰來加密資料)。</span><span class="sxs-lookup"><span data-stu-id="727b4-105">For public-key encryption, you must know either the public key (if the data was encrypted using the private key) or the private key (if the data was encrypted using the public key).</span></span>

## <a name="symmetric-decryption"></a><span data-ttu-id="727b4-106">對稱解密</span><span class="sxs-lookup"><span data-stu-id="727b4-106">Symmetric Decryption</span></span>

<span data-ttu-id="727b4-107">以對稱演算法加密的資料解密類似於用來以對稱演算法加密資料的程序。</span><span class="sxs-lookup"><span data-stu-id="727b4-107">The decryption of data encrypted with symmetric algorithms is similar to the process used to encrypt data with symmetric algorithms.</span></span> <span data-ttu-id="727b4-108"><xref:System.Security.Cryptography.CryptoStream> 類別與 .NET Framework 所提供的對稱式密碼編譯類別一起用來解密從任何 Managed 資料流物件讀取的資料。</span><span class="sxs-lookup"><span data-stu-id="727b4-108">The <xref:System.Security.Cryptography.CryptoStream> class is used with symmetric cryptography classes provided by the .NET Framework to decrypt data read from any managed stream object.</span></span>

<span data-ttu-id="727b4-109">下列範例說明如何建立 <xref:System.Security.Cryptography.RijndaelManaged> 類別的新執行個體，並使用它對 <xref:System.Security.Cryptography.CryptoStream> 物件執行解密。</span><span class="sxs-lookup"><span data-stu-id="727b4-109">The following example illustrates how to create a new instance of the <xref:System.Security.Cryptography.RijndaelManaged> class and use it to perform decryption on a <xref:System.Security.Cryptography.CryptoStream> object.</span></span> <span data-ttu-id="727b4-110">此範例會先建立 **RijndaelManaged** 類別的新執行個體。</span><span class="sxs-lookup"><span data-stu-id="727b4-110">This example first creates a new instance of the **RijndaelManaged** class.</span></span> <span data-ttu-id="727b4-111">接下來它會建立 **CryptoStream** 物件，並將它初始化為稱為 `myStream`的 Managed 資料流的值。</span><span class="sxs-lookup"><span data-stu-id="727b4-111">Next it creates a **CryptoStream** object and initializes it to the value of a managed stream called `myStream`.</span></span> <span data-ttu-id="727b4-112">接下來，會傳遞用於加密的相同金鑰和 IV 給 **RijndaelManaged** 類別的 **CreateDecryptor** 方法，然後傳遞至 **CryptoStream** 建構函式。</span><span class="sxs-lookup"><span data-stu-id="727b4-112">Next, the **CreateDecryptor** method from the **RijndaelManaged** class is passed the same key and IV that was used for encryption and is then passed to the **CryptoStream** constructor.</span></span> <span data-ttu-id="727b4-113">最後， **CryptoStreamMode.Read** 列舉會傳遞至 **CryptoStream** 建構函式，指定資料流的讀取權限。</span><span class="sxs-lookup"><span data-stu-id="727b4-113">Finally, the **CryptoStreamMode.Read** enumeration is passed to the **CryptoStream** constructor to specify read access to the stream.</span></span>

```vb
Dim rmCrypto As New RijndaelManaged()
Dim cryptStream As New CryptoStream(myStream, rmCrypto.CreateDecryptor(rmCrypto.Key, rmCrypto.IV), CryptoStreamMode.Read)
```

```csharp
RijndaelManaged rmCrypto = new RijndaelManaged();
CryptoStream cryptStream = new CryptoStream(myStream, rmCrypto.CreateDecryptor(Key, IV), CryptoStreamMode.Read);
```

<span data-ttu-id="727b4-114">下列範例顯示建立資料流、解密資料流、從資料流讀取，然後關閉資料流的整個程序。</span><span class="sxs-lookup"><span data-stu-id="727b4-114">The following example shows the entire process of creating a stream, decrypting the stream, reading from the stream, and closing the streams.</span></span> <span data-ttu-id="727b4-115">會建立 <xref:System.Net.Sockets.TcpListener> 物件，它會在建立接聽物件的連線時初始化網路資料流。</span><span class="sxs-lookup"><span data-stu-id="727b4-115">A <xref:System.Net.Sockets.TcpListener> object is created that initializes a network stream when a connection to the listening object is made.</span></span> <span data-ttu-id="727b4-116">接著會使用 **CryptoStream** 類別和 **RijndaelManaged** 類別解密網路資料流。</span><span class="sxs-lookup"><span data-stu-id="727b4-116">The network stream is then decrypted using the **CryptoStream** class and the **RijndaelManaged** class.</span></span> <span data-ttu-id="727b4-117">這個範例假設金鑰和 IV 已成功傳輸，或是事先已同意。</span><span class="sxs-lookup"><span data-stu-id="727b4-117">This example assumes that the key and IV values have been either successfully transferred or previously agreed upon.</span></span> <span data-ttu-id="727b4-118">它不會顯示加密和傳輸這些值所需的程式碼。</span><span class="sxs-lookup"><span data-stu-id="727b4-118">It does not show the code needed to encrypt and transfer these values.</span></span>

```vb
Imports System.IO
Imports System.Net
Imports System.Net.Sockets
Imports System.Security.Cryptography
Imports System.Threading

Module Module1
    Sub Main()
            'The key and IV must be the same values that were used
            'to encrypt the stream.
            Dim key As Byte() = {&H1, &H2, &H3, &H4, &H5, &H6, &H7, &H8, &H9, &H10, &H11, &H12, &H13, &H14, &H15, &H16}
            Dim iv As Byte() = {&H1, &H2, &H3, &H4, &H5, &H6, &H7, &H8, &H9, &H10, &H11, &H12, &H13, &H14, &H15, &H16}
        Try
            'Initialize a TCPListener on port 11000
            'using the current IP address.
            Dim tcpListen As New TcpListener(IPAddress.Any, 11000)

            'Start the listener.
            tcpListen.Start()

            'Check for a connection every five seconds.
            While Not tcpListen.Pending()
                Console.WriteLine("Still listening. Will try in 5 seconds.")

                Thread.Sleep(5000)
            End While

            'Accept the client if one is found.
            Dim tcp As TcpClient = tcpListen.AcceptTcpClient()

            'Create a network stream from the connection.
            Dim netStream As NetworkStream = tcp.GetStream()

            'Create a new instance of the RijndaelManaged class
            'and decrypt the stream.
            Dim rmCrypto As New RijndaelManaged()

            'Create an instance of the CryptoStream class, pass it the NetworkStream, and decrypt
            'it with the Rijndael class using the key and IV.
            Dim cryptStream As New CryptoStream(netStream, rmCrypto.CreateDecryptor(key, iv), CryptoStreamMode.Read)

            'Read the stream.
            Dim sReader As New StreamReader(cryptStream)

            'Display the message.
            Console.WriteLine("The decrypted original message: {0}", sReader.ReadToEnd())

            'Close the streams.
            sReader.Close()
            netStream.Close()
            tcp.Close()
            'Catch any exceptions.
        Catch
            Console.WriteLine("The Listener Failed.")
        End Try
    End Sub
End Module
```

```csharp
using System;
using System.IO;
using System.Net;
using System.Net.Sockets;
using System.Security.Cryptography;
using System.Threading;

class Class1
{
   static void Main(string[] args)
   {
      //The key and IV must be the same values that were used
      //to encrypt the stream.
      byte[] key = {0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x10, 0x11, 0x12, 0x13, 0x14, 0x15, 0x16};
      byte[] iv = {0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x10, 0x11, 0x12, 0x13, 0x14, 0x15, 0x16};
      try
      {
         //Initialize a TCPListener on port 11000
         //using the current IP address.
         TcpListener tcpListen = new TcpListener(IPAddress.Any, 11000);

         //Start the listener.
         tcpListen.Start();

         //Check for a connection every five seconds.
         while(!tcpListen.Pending())
         {
            Console.WriteLine("Still listening. Will try in 5 seconds.");
            Thread.Sleep(5000);
         }

         //Accept the client if one is found.
         TcpClient tcp = tcpListen.AcceptTcpClient();

         //Create a network stream from the connection.
         NetworkStream netStream = tcp.GetStream();

         //Create a new instance of the RijndaelManaged class
         // and decrypt the stream.
         RijndaelManaged rmCrypto = new RijndaelManaged();

         //Create a CryptoStream, pass it the NetworkStream, and decrypt
         //it with the Rijndael class using the key and IV.
         CryptoStream cryptStream = new CryptoStream(netStream,
            rmCrypto.CreateDecryptor(key, iv),
            CryptoStreamMode.Read);

         //Read the stream.
         StreamReader sReader = new StreamReader(cryptStream);

         //Display the message.
         Console.WriteLine("The decrypted original message: {0}", sReader.ReadToEnd());

         //Close the streams.
         sReader.Close();
         netStream.Close();
         tcp.Close();
      }
      //Catch any exceptions.
      catch
      {
         Console.WriteLine("The Listener Failed.");
      }
   }
}
```

<span data-ttu-id="727b4-119">先前的範例要能運作，必須建立接聽程式的加密連線。</span><span class="sxs-lookup"><span data-stu-id="727b4-119">For the previous sample to work, an encrypted connection must be made to the listener.</span></span> <span data-ttu-id="727b4-120">連線必須使用接聽程式中使用的相同金鑰、IV 和演算法。</span><span class="sxs-lookup"><span data-stu-id="727b4-120">The connection must use the same key, IV, and algorithm used in the listener.</span></span> <span data-ttu-id="727b4-121">建立這樣的連線之後，訊息會經過解密並顯示到主控台。</span><span class="sxs-lookup"><span data-stu-id="727b4-121">If such a connection is made, the message is decrypted and displayed to the console.</span></span>

## <a name="asymmetric-decryption"></a><span data-ttu-id="727b4-122">非對稱解密</span><span class="sxs-lookup"><span data-stu-id="727b4-122">Asymmetric Decryption</span></span>

<span data-ttu-id="727b4-123">一般而言，有一方 (A 方) 會同時產生公開和私密金鑰，並將金鑰儲存在記憶體或密碼編譯金鑰容器中。</span><span class="sxs-lookup"><span data-stu-id="727b4-123">Typically, a party (party A) generates both a public and private key and stores the key either in memory or in a cryptographic key container.</span></span> <span data-ttu-id="727b4-124">A 方接著會將公開金鑰傳送給另一方 (B 方)。</span><span class="sxs-lookup"><span data-stu-id="727b4-124">Party A then sends the public key to another party (party B).</span></span> <span data-ttu-id="727b4-125">使用公開金鑰時，合作物件 B 會加密資料，並將資料傳回給合作物件 A。在收到資料之後，合作物件 A 會使用對應的私密金鑰來解密它。</span><span class="sxs-lookup"><span data-stu-id="727b4-125">Using the public key, party B encrypts data and sends the data back to party A. After receiving the data, party A decrypts it using the private key that corresponds.</span></span> <span data-ttu-id="727b4-126">只有在 A 方使用的私密金鑰對應於 B 方用來加密資料的公開金鑰時，解密才會成功。</span><span class="sxs-lookup"><span data-stu-id="727b4-126">Decryption will be successful only if party A uses the private key that corresponds to the public key Party B used to encrypt the data.</span></span>

<span data-ttu-id="727b4-127">如需如何在安全的密碼編譯金鑰容器儲存非對稱金鑰，以及稍後如何擷取非對稱金鑰的相關資訊，請參閱 [How to: Store Asymmetric Keys in a Key Container](how-to-store-asymmetric-keys-in-a-key-container.md)。</span><span class="sxs-lookup"><span data-stu-id="727b4-127">For information on how to store an asymmetric key in secure cryptographic key container and how to later retrieve the asymmetric key, see [How to: Store Asymmetric Keys in a Key Container](how-to-store-asymmetric-keys-in-a-key-container.md).</span></span>

<span data-ttu-id="727b4-128">下列範例說明代表對稱金鑰和 IV 的兩個位元組陣列的解密。</span><span class="sxs-lookup"><span data-stu-id="727b4-128">The following example illustrates the decryption of two arrays of bytes that represent a symmetric key and IV.</span></span> <span data-ttu-id="727b4-129">如需如何從 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 物件擷取非對稱式公開金鑰，且使用的格式可以輕鬆地傳送給第三方的相關資訊，請參閱 [Encrypting Data](encrypting-data.md)的 Managed 資料流的值。</span><span class="sxs-lookup"><span data-stu-id="727b4-129">For information on how to extract the asymmetric public key from the <xref:System.Security.Cryptography.RSACryptoServiceProvider> object in a format that you can easily send to a third party, see [Encrypting Data](encrypting-data.md).</span></span>

```vb
'Create a new instance of the RSACryptoServiceProvider class.
Dim rsa As New RSACryptoServiceProvider()

' Export the public key information and send it to a third party.
' Wait for the third party to encrypt some data and send it back.

'Decrypt the symmetric key and IV.
symmetricKey = rsa.Decrypt(encryptedSymmetricKey, False)
symmetricIV = rsa.Decrypt(encryptedSymmetricIV, False)
```

```csharp
//Create a new instance of the RSACryptoServiceProvider class.
RSACryptoServiceProvider rsa = new RSACryptoServiceProvider();

// Export the public key information and send it to a third party.
// Wait for the third party to encrypt some data and send it back.

//Decrypt the symmetric key and IV.
symmetricKey = rsa.Decrypt(encryptedSymmetricKey, false);
symmetricIV = rsa.Decrypt(encryptedSymmetricIV , false);
```

## <a name="see-also"></a><span data-ttu-id="727b4-130">另請參閱</span><span class="sxs-lookup"><span data-stu-id="727b4-130">See also</span></span>

- [<span data-ttu-id="727b4-131">產生加密和解密金鑰</span><span class="sxs-lookup"><span data-stu-id="727b4-131">Generating Keys for Encryption and Decryption</span></span>](generating-keys-for-encryption-and-decryption.md)
- [<span data-ttu-id="727b4-132">加密資料</span><span class="sxs-lookup"><span data-stu-id="727b4-132">Encrypting Data</span></span>](encrypting-data.md)
- [<span data-ttu-id="727b4-133">密碼編譯服務</span><span class="sxs-lookup"><span data-stu-id="727b4-133">Cryptographic Services</span></span>](cryptographic-services.md)
