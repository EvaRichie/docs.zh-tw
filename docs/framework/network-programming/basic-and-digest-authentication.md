---
title: 基本和摘要式驗證
description: 瞭解如何使用基本和摘要式驗證，其中應用程式會在用來要求資料的 WebRequest 物件中提供使用者名稱和密碼。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- authentication [.NET Framework], classes
- Basic authentication
- authentication [.NET Framework], basic
- client authentication, basic
- user authentication, basic
- authentication [.NET Framework], digest
- receiving data, authentication
- client authentication, digest
- Internet, authentication
- digest authentication
- sending data, authentication
- network resources, authentication
- user authentication, digest
ms.assetid: 8cce2742-8d52-4643-9dd2-64ddf38aa878
ms.openlocfilehash: e55dc58a7998824dbcfffa204008aacb815be03a
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96287575"
---
# <a name="basic-and-digest-authentication"></a><span data-ttu-id="5d69e-103">基本和摘要式驗證</span><span class="sxs-lookup"><span data-stu-id="5d69e-103">Basic and Digest Authentication</span></span>

<span data-ttu-id="5d69e-104">基本和摘要式驗證的 <xref:System.Net> 實作符合 RFC2617 - HTTP 驗證：基本和摘要式驗證 (可在[全球資訊網協會](https://www.w3.org)的網站上取得)。</span><span class="sxs-lookup"><span data-stu-id="5d69e-104">The <xref:System.Net> implementation of basic and digest authentication complies with RFC2617 – HTTP Authentication: Basic and Digest Authentication (available on the [World Wide Web Consortium's](https://www.w3.org) website).</span></span>  
  
 <span data-ttu-id="5d69e-105">若要使用基本和摘要式驗證，應用程式必須在 <xref:System.Net.WebRequest> 物件的 <xref:System.Net.WebRequest.Credentials%2A> 屬性中提供使用者名稱和密碼，以用來從網際網路要求資料，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="5d69e-105">To use basic and digest authentication, an application must provide a user name and password in the <xref:System.Net.WebRequest.Credentials%2A> property of the <xref:System.Net.WebRequest> object that it uses to request data from the Internet, as shown in the following example.</span></span>  
  
```vb  
Dim MyURI As String = "http://www.contoso.com/"  
Dim WReq As WebRequest = WebRequest.Create(MyURI)  
WReq.Credentials = New NetworkCredential(UserName, SecurelyStoredPassword)  
```  
  
```csharp  
String MyURI = "http://www.contoso.com/";  
WebRequest WReq = WebRequest.Create(MyURI);  
WReq.Credentials = new NetworkCredential(UserName, SecurelyStoredPassword);  
```  
  
> [!CAUTION]
> <span data-ttu-id="5d69e-106">使用基本與摘要式驗證傳送的資料不會經過加密，因此敵人可以看到資料。</span><span class="sxs-lookup"><span data-stu-id="5d69e-106">Data sent with Basic and Digest Authentication is not encrypted, so the data can be seen by an adversary.</span></span> <span data-ttu-id="5d69e-107">此外，基本驗證認證 (使用者名稱和密碼) 會以純文字傳送，而且可以被攔截。</span><span class="sxs-lookup"><span data-stu-id="5d69e-107">Additionally, Basic Authentication credentials (user name and password) are sent in the clear and can be intercepted.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="5d69e-108">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5d69e-108">See also</span></span>

- [<span data-ttu-id="5d69e-109">NTLM 與 Kerberos 驗證</span><span class="sxs-lookup"><span data-stu-id="5d69e-109">NTLM and Kerberos Authentication</span></span>](ntlm-and-kerberos-authentication.md)
- [<span data-ttu-id="5d69e-110">網際網路驗證</span><span class="sxs-lookup"><span data-stu-id="5d69e-110">Internet Authentication</span></span>](internet-authentication.md)
