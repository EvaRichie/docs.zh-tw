---
title: 加密資料
description: 瞭解如何在 .NET 中加密資料。 您可以在資料流程上使用對稱式加密，也可以在少量的位元組上使用非對稱式加密。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- encryption [.NET Framework], symmetric
- symmetric encryption
- cryptography [.NET Framework], asymmetric
- asymmetric encryption
ms.assetid: 7ecce51f-db5f-4bd4-9321-cceb6fcb2a77
ms.openlocfilehash: 6cebdecd461f28f8228ebb8440dbff218dc211db
ms.sourcegitcommit: 7137e12f54c4e83a94ae43ec320f8cf59c1772ea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/10/2020
ms.locfileid: "84662520"
---
# <a name="encrypting-data"></a>加密資料
對稱式加密和非對稱式加密是使用不同的程序執行。 對稱式加密在資料流上執行，因此適用於加密大量資料。 非對稱式加密在少數的位元組上執行，因此只適用於小量的資料。  
  
## <a name="symmetric-encryption"></a>對稱加密  
 Managed 對稱式密碼編譯類別可搭配特殊的資料流類別，稱為 <xref:System.Security.Cryptography.CryptoStream> ，它會加密讀入資料流的資料。 **CryptoStream** 類別初始化時具有 Managed 資料流類別初始化、實作 <xref:System.Security.Cryptography.ICryptoTransform> 介面 (從實作密碼編譯演算法的類別建立) 的類別，以及描述允許對 <xref:System.Security.Cryptography.CryptoStreamMode> CryptoStream **執行之存取類型的**列舉。 **CryptoStream**類別可以使用衍生自類別的任何類別初始化 <xref:System.IO.Stream> ，包括 <xref:System.IO.FileStream> 、 <xref:System.IO.MemoryStream> 和 <xref:System.Net.Sockets.NetworkStream> 。 使用這些類別，您可以在各種不同的資料流物件上執行對稱式加密。  
  
 下列範例說明如何建立 <xref:System.Security.Cryptography.RijndaelManaged> 類別的新執行個體，它會實作 Rijndael 加密演算法，並使用它對 **CryptoStream** 類別執行加密。 在此範例中， **CryptoStream** 以稱為 `myStream` 的資料流物件初始化，它是任何類型的 Managed 資料流。 會傳遞金鑰和加密所用 IV 給來自 **RijndaelManaged** 類別的 **CreateEncryptor** 方法。 在此情況下，會使用從 `rmCrypto` 產生的預設金鑰和 IV。 最後，會傳遞 **CryptoStreamMode.Write** ，並指定對資料流的寫入權限。  
  
```vb  
Dim rmCrypto As New RijndaelManaged()  
Dim cryptStream As New CryptoStream(myStream, rmCrypto.CreateEncryptor(rmCrypto.Key, rmCrypto.IV), CryptoStreamMode.Write)  
```  
  
```csharp  
RijndaelManaged rmCrypto = new RijndaelManaged();  
CryptoStream cryptStream = new CryptoStream(myStream, rmCrypto.CreateEncryptor(), CryptoStreamMode.Write);  
```  
  
 此程式碼執行之後，寫入 **CryptoStream** 物件的任何資料會使用 Rijndael 演算法進行加密。  
  
 下列範例顯示建立資料流、加密資料流、寫入資料流，然後關閉資料流的整個程序。 這個範例會建立使用 **CryptoStream** 類別和 **RijndaelManaged** 類別加密的網路資料流。 訊息會使用 <xref:System.IO.StreamWriter> 類別寫入至加密的資料流。  
  
> [!NOTE]
> 您也可以使用此範例寫入至檔案。 若要這樣做，請刪除 <xref:System.Net.Sockets.TcpClient> 參考，並將 <xref:System.Net.Sockets.NetworkStream> 取代為 <xref:System.IO.FileStream>。  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Security.Cryptography  
Imports System.Net.Sockets  
  
Module Module1  
Sub Main()  
   Try  
      'Create a TCP connection to a listening TCP process.  
      'Use "localhost" to specify the current computer or  
      'replace "localhost" with the IP address of the
      'listening process.
      Dim tcp As New TcpClient("localhost", 11000)  
  
      'Create a network stream from the TCP connection.
      Dim netStream As NetworkStream = tcp.GetStream()  
  
      'Create a new instance of the RijndaelManaged class  
      'and encrypt the stream.  
      Dim rmCrypto As New RijndaelManaged()  
  
            Dim key As Byte() = {&H1, &H2, &H3, &H4, &H5, &H6, &H7, &H8, &H9, &H10, &H11, &H12, &H13, &H14, &H15, &H16}  
            Dim iv As Byte() = {&H1, &H2, &H3, &H4, &H5, &H6, &H7, &H8, &H9, &H10, &H11, &H12, &H13, &H14, &H15, &H16}  
  
      'Create a CryptoStream, pass it the NetworkStream, and encrypt
      'it with the Rijndael class.  
      Dim cryptStream As New CryptoStream(netStream, rmCrypto.CreateEncryptor(key, iv), CryptoStreamMode.Write)  
  
      'Create a StreamWriter for easy writing to the
      'network stream.  
      Dim sWriter As New StreamWriter(cryptStream)  
  
      'Write to the stream.  
      sWriter.WriteLine("Hello World!")  
  
      'Inform the user that the message was written  
      'to the stream.  
      Console.WriteLine("The message was sent.")  
  
      'Close all the connections.  
      sWriter.Close()  
      cryptStream.Close()  
      netStream.Close()  
      tcp.Close()  
   Catch  
      'Inform the user that an exception was raised.  
      Console.WriteLine("The connection failed.")  
   End Try  
End Sub  
End Module  
```  
  
```csharp  
using System;  
using System.IO;  
using System.Security.Cryptography;  
using System.Net.Sockets;  
  
public class main  
{  
   public static void Main(string[] args)  
   {  
      try  
      {  
         //Create a TCP connection to a listening TCP process.  
         //Use "localhost" to specify the current computer or  
         //replace "localhost" with the IP address of the
         //listening process.
         TcpClient tcp = new TcpClient("localhost",11000);  
  
         //Create a network stream from the TCP connection.
         NetworkStream netStream = tcp.GetStream();  
  
         //Create a new instance of the RijndaelManaged class  
         // and encrypt the stream.  
         RijndaelManaged rmCrypto = new RijndaelManaged();  
  
         byte[] key = {0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x10, 0x11, 0x12, 0x13, 0x14, 0x15, 0x16};  
         byte[] iv = {0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x10, 0x11, 0x12, 0x13, 0x14, 0x15, 0x16};  
  
         //Create a CryptoStream, pass it the NetworkStream, and encrypt
         //it with the Rijndael class.  
         CryptoStream cryptStream = new CryptoStream(netStream,
         rmCrypto.CreateEncryptor(key, iv),
         CryptoStreamMode.Write);  
  
         //Create a StreamWriter for easy writing to the
         //network stream.  
         StreamWriter sWriter = new StreamWriter(cryptStream);  
  
         //Write to the stream.  
         sWriter.WriteLine("Hello World!");  
  
         //Inform the user that the message was written  
         //to the stream.  
         Console.WriteLine("The message was sent.");  
  
         //Close all the connections.  
         sWriter.Close();  
         cryptStream.Close();  
         netStream.Close();  
         tcp.Close();  
      }  
      catch  
      {  
         //Inform the user that an exception was raised.  
         Console.WriteLine("The connection failed.");  
      }  
   }  
}  
```  
  
 前一個範例若要執行成功，必須有處理序在 <xref:System.Net.Sockets.TcpClient> 類別指定的 IP 位址和通訊埠號碼上接聽。 如果接聽的處理序存在，程式碼便會連接到接聽的處理序、使用 Rijndael 對稱演算法加密資料流，並將 "Hello World!" 寫入此資料流。 如果程式碼成功，它會顯示下列文字至主控台：  
  
```console  
The message was sent.  
```  
  
 不過，如果找不到接聽的處理序或引發了例外狀況，程式碼會顯示下列文字至主控台：  
  
```console  
The connection failed.  
```  
  
## <a name="asymmetric-encryption"></a>非對稱加密  
 非對稱演算法通常用來加密少量的資料，例如對稱金鑰和 IV 的加密。 一般來說，個別的執行中非對稱式加密會使用另一個合作對象所產生的公開金鑰。 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 類別由 .NET Framework 針對此目的所提供。  
  
 下列範例會使用公開金鑰資訊來加密對稱金鑰和 IV。 會初始化兩個代表第三方的公開金鑰的位元組陣列。 <xref:System.Security.Cryptography.RSAParameters> 物件會初始化為這些值。 接下來， **RSAParameters** (以及它所代表的公開金鑰) 的物件會使用 **方法匯入到** RSACryptoServiceProvider <xref:System.Security.Cryptography.RSACryptoServiceProvider.ImportParameters%2A?displayProperty=nameWithType> 。 最後， <xref:System.Security.Cryptography.RijndaelManaged> 類別所建立的私密金鑰和 IV 會被加密。 此範例會要求系統安裝 128 位元加密。  
  
```vb  
Imports System  
Imports System.Security.Cryptography  
  
Module Module1  
  
    Sub Main()  
        'Initialize the byte arrays to the public key information.  
      Dim publicKey As Byte() =  {214, 46, 220, 83, 160, 73, 40, 39, 201, 155, 19,202, 3, 11, 191, 178, 56, 74, 90, 36, 248, 103, 18, 144, 170, 163, 145, 87, 54, 61, 34, 220, 222, 207, 137, 149, 173, 14, 92, 120, 206, 222, 158, 28, 40, 24, 30, 16, 175, 108, 128, 35, 230, 118, 40, 121, 113, 125, 216, 130, 11, 24, 90, 48, 194, 240, 105, 44, 76, 34, 57, 249, 228, 125, 80, 38, 9, 136, 29, 117, 207, 139, 168, 181, 85, 137, 126, 10, 126, 242, 120, 247, 121, 8, 100, 12, 201, 171, 38, 226, 193, 180, 190, 117, 177, 87, 143, 242, 213, 11, 44, 180, 113, 93, 106, 99, 179, 68, 175, 211, 164, 116, 64, 148, 226, 254, 172, 147}  
  
        Dim exponent As Byte() = {1, 0, 1}  
  
        'Create values to store encrypted symmetric keys.  
        Dim encryptedSymmetricKey() As Byte  
        Dim encryptedSymmetricIV() As Byte  
  
        'Create a new instance of the RSACryptoServiceProvider class.  
        Dim rsa As New RSACryptoServiceProvider()  
  
        'Create a new instance of the RSAParameters structure.  
        Dim rsaKeyInfo As New RSAParameters()  
  
        'Set rsaKeyInfo to the public key values.
        rsaKeyInfo.Modulus = publicKey  
        rsaKeyInfo.Exponent = exponent  
  
        'Import key parameters into rsa.  
        rsa.ImportParameters(rsaKeyInfo)  
  
        'Create a new instance of the RijndaelManaged class.  
        Dim RM As New RijndaelManaged()  
  
        'Encrypt the symmetric key and IV.  
        encryptedSymmetricKey = rsa.Encrypt(RM.Key, False)  
        encryptedSymmetricIV = rsa.Encrypt(RM.IV, False)  
    End Sub  
  
End Module  
```  
  
```csharp  
using System;  
using System.Security.Cryptography;  
  
class Class1  
{  
   static void Main()  
   {  
      //Initialize the byte arrays to the public key information.  
      byte[] publicKey = {214,46,220,83,160,73,40,39,201,155,19,202,3,11,191,178,56,  
            74,90,36,248,103,18,144,170,163,145,87,54,61,34,220,222,  
            207,137,149,173,14,92,120,206,222,158,28,40,24,30,16,175,  
            108,128,35,230,118,40,121,113,125,216,130,11,24,90,48,194,  
            240,105,44,76,34,57,249,228,125,80,38,9,136,29,117,207,139,  
            168,181,85,137,126,10,126,242,120,247,121,8,100,12,201,171,  
            38,226,193,180,190,117,177,87,143,242,213,11,44,180,113,93,  
            106,99,179,68,175,211,164,116,64,148,226,254,172,147};  
  
      byte[] exponent = {1,0,1};  
  
      //Create values to store encrypted symmetric keys.  
      byte[] encryptedSymmetricKey;  
      byte[] encryptedSymmetricIV;  
  
      //Create a new instance of the RSACryptoServiceProvider class.  
      RSACryptoServiceProvider rsa = new RSACryptoServiceProvider();  
  
      //Create a new instance of the RSAParameters structure.  
      RSAParameters rsaKeyInfo = new RSAParameters();  
  
      //Set rsaKeyInfo to the public key values.
      rsaKeyInfo.Modulus = publicKey;  
      rsaKeyInfo.Exponent = exponent;  
  
      //Import key parameters into RSA.  
      rsa.ImportParameters(rsaKeyInfo);  
  
      //Create a new instance of the RijndaelManaged class.  
      RijndaelManaged rm = new RijndaelManaged();  
  
      //Encrypt the symmetric key and IV.  
      encryptedSymmetricKey = rsa.Encrypt(rm.Key, false);  
      encryptedSymmetricIV = rsa.Encrypt(rm.IV, false);  
   }  
}  
```  
  
## <a name="see-also"></a>另請參閱

- [產生加密和解密金鑰](generating-keys-for-encryption-and-decryption.md)
- [解密資料](decrypting-data.md)
- [密碼編譯服務](cryptographic-services.md)
