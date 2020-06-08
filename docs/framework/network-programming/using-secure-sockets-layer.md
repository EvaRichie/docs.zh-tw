---
title: 使用安全通訊端層
description: 深入瞭解 System.Net 和擴充類別如何使用安全通訊端層，為 .NET Framework 中的數個網路通訊協定加密連接。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Networking
- SSL
- Secure Sockets Layer
- requesting data from Internet, Secure Sockets Layer
- sending data, Secure Sockets Layer
- Network Resources
- data requests, Secure Sockets Layer
- receiving data, Secure Sockets Layer
- Internet, Secure Sockets Layer
ms.assetid: 6e4289e6-d1b7-4e82-ab0d-e83e3b6063ed
ms.openlocfilehash: 67330962382e768849cbf67d5f412ea80f65569d
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501985"
---
# <a name="using-secure-sockets-layer"></a>使用安全通訊端層
<xref:System.Net> 類別會使用安全通訊端層 (SSL) 來加密數個網路通訊協定的連線。  
  
 若為 HTTP 連線，<xref:System.Net.WebRequest> 和 <xref:System.Net.WebResponse> 類別會使用 SSL 來與支援 SSL 的 Web 主機通訊。 決定使用 SSL 與否是 <xref:System.Net.WebRequest> 類別根據給定的 URI 來進行。 如果 URI 開頭是 "https:"，則使用 SSL。如果 URI 開頭是 "http:"，則使用未加密的連線。  
  
 若要搭配使用 SSL 與檔案傳輸通訊協定 (FTP)，請將 <xref:System.Net.FtpWebRequest.EnableSsl> 屬性設定為 true，才能呼叫 <xref:System.Net.FtpWebRequest.GetResponse>。 同樣地，若要搭配使用 SSL 與簡易郵件傳輸通訊協定 (SMTP)，請將 <xref:System.Net.Mail.SmtpClient.EnableSsl> 屬性設定為 true，然後傳送電子郵件。  
  
 <xref:System.Net.Security.SslStream> 類別提供 SSL 以資料流為基礎的抽象概念，並提供許多方式來設定 SSL 交握。  
  
## <a name="example"></a>範例  
  
### <a name="code"></a>程式碼  
  
```vb  
Dim MyURI As String = "https://www.contoso.com/"  
Dim Wreq As WebRequest = WebRequest.Create(MyURI)  
  
Dim serverUri As String = "ftp://ftp.contoso.com/file.txt"  
Dim request As FtpWebRequest = CType(WebRequest.Create(serverUri), FtpWebRequest)  
request.Method = WebRequestMethods.Ftp.DeleteFile  
request.EnableSsl = True  
Dim response As FtpWebResponse = CType(request.GetResponse(), FtpWebResponse)  
```  
  
```csharp  
String MyURI = "https://www.contoso.com/";  
WebRequest WReq = WebRequest.Create(MyURI);  
  
String serverUri = "ftp://ftp.contoso.com/file.txt"  
FtpWebRequest request = (FtpWebRequest)WebRequest.Create(serverUri);  
request.EnableSsl = true;  
request.Method = WebRequestMethods.Ftp.DeleteFile;  
FtpWebResponse response = (FtpWebResponse)request.GetResponse();  
```  
  
## <a name="compiling-the-code"></a>編譯程式碼  
 這個範例需要：  
  
- 對 **System.Net** 命名空間的參考。  
  
## <a name="see-also"></a>另請參閱

- [網路程式設計的安全性](security-in-network-programming.md)
- [.NET Framework 中的網路程式設計](index.md)
- [憑證的選取和驗證](certificate-selection-and-validation.md)
