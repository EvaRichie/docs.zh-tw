---
title: 作法：設定要求的快取原則
description: 瞭解如何在 .NET Framework 中設定要求的快取原則。 此快取原則可讓您從快取中使用資源一天。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- request cache policies
ms.assetid: 39c15e40-586b-4ac9-9cce-146f74b7e545
ms.openlocfilehash: cbb8f2eaf618cb9faaca1375d829478a645962a7
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96253410"
---
# <a name="how-to-set-cache-policy-for-a-request"></a><span data-ttu-id="ca50e-104">作法：設定要求的快取原則</span><span class="sxs-lookup"><span data-stu-id="ca50e-104">How to: Set Cache Policy for a Request</span></span>

<span data-ttu-id="ca50e-105">下列範例示範如何設定要求的快取原則。</span><span class="sxs-lookup"><span data-stu-id="ca50e-105">The following example demonstrates setting a cache policy for a request.</span></span> <span data-ttu-id="ca50e-106">範例的輸入是如 `http://www.contoso.com/` 之類的 URI。</span><span class="sxs-lookup"><span data-stu-id="ca50e-106">The example input is a URI such as `http://www.contoso.com/`.</span></span>  
  
## <a name="example"></a><span data-ttu-id="ca50e-107">範例</span><span class="sxs-lookup"><span data-stu-id="ca50e-107">Example</span></span>  

 <span data-ttu-id="ca50e-108">下列程式碼範例會建立一個快取原則，允許所要求的資源在快取中的時間尚未超過一天時，從快取使用該資源。</span><span class="sxs-lookup"><span data-stu-id="ca50e-108">The following code example creates a cache policy that allows the requested resource to be used from the cache if it has not been in the cache for longer than one day.</span></span> <span data-ttu-id="ca50e-109">此範例會顯示一個訊息，指出是否已從快取使用資源 (例如，`"The response was retrieved from the cache : False."`)，然後顯示該資源。</span><span class="sxs-lookup"><span data-stu-id="ca50e-109">The example displays a message that indicates whether the resource was used from the cache—for example, `"The response was retrieved from the cache : False."`—and then displays the resource.</span></span> <span data-ttu-id="ca50e-110">用戶端與伺服器之間的任何快取都可以滿足要求。</span><span class="sxs-lookup"><span data-stu-id="ca50e-110">A request can be fulfilled by any cache between the client and server.</span></span>  
  
```csharp  
using System;  
using System.Net;  
using System.Net.Cache;  
using System.IO;  
  
namespace Examples.System.Net.Cache  
{  
    public class CacheExample  
    {
        public static void UseCacheForOneDay(Uri resource)  
        {  
            // Create a policy that allows items in the cache  
            // to be used if they have been cached one day or less.  
            HttpRequestCachePolicy requestPolicy =
                new HttpRequestCachePolicy (HttpCacheAgeControl.MaxAge,  
                TimeSpan.FromDays(1));  
  
            WebRequest request = WebRequest.Create (resource);  
            // Set the policy for this request only.  
            request.CachePolicy = requestPolicy;  
            HttpWebResponse response = (HttpWebResponse)request.GetResponse();  
            // Determine whether the response was retrieved from the cache.  
            Console.WriteLine ("The response was retrieved from the cache : {0}.",  
               response.IsFromCache);  
            Stream s = response.GetResponseStream ();  
            StreamReader reader = new StreamReader (s);  
            // Display the requested resource.  
            Console.WriteLine(reader.ReadToEnd());  
            reader.Close ();  
            s.Close();  
            response.Close();  
        }  
        public static void Main(string[] args)  
        {  
            if (args == null || args.Length != 1)  
            {  
                Console.WriteLine ("You must specify the URI to retrieve.");  
                return;  
            }  
            UseCacheForOneDay (new Uri(args[0]));  
        }  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.Net  
Imports System.Net.Cache  
Imports System.IO  
Namespace Examples.System.Net.Cache  
    Public Class CacheExample  
        Public Shared Sub UseCacheForOneDay(ByVal resource As Uri)  
            ' Create a policy that allows items in the cache  
            ' to be used if they have been cached one day or less.  
            Dim requestPolicy As New HttpRequestCachePolicy _  
                  (HttpCacheAgeControl.MaxAge, TimeSpan.FromDays(1))  
            Dim request As WebRequest = WebRequest.Create(resource)  
            ' Set the policy for this request only.  
            request.CachePolicy = requestPolicy  
            Dim response As HttpWebResponse = _  
             CType(request.GetResponse(), HttpWebResponse)  
            ' Determine whether the response was retrieved from the cache.  
            Console.WriteLine("The response was retrieved from the cache : {0}.", _  
                response.IsFromCache)  
            Dim s As Stream = response.GetResponseStream()  
            Dim reader As New StreamReader(s)  
            ' Display the requested resource.  
            Console.WriteLine(reader.ReadToEnd())  
            reader.Close()  
            s.Close()  
            response.Close()  
        End Sub  
        Public Shared Sub Main(ByVal args() As String)  
            If args Is Nothing OrElse args.Length <> 1 Then  
                Console.WriteLine("You must specify the URI to retrieve.")  
                Return  
            End If  
            UseCacheForOneDay(New Uri(args(0)))  
        End Sub  
    End Class  
End Namespace  
```  
  
## <a name="see-also"></a><span data-ttu-id="ca50e-111">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ca50e-111">See also</span></span>

- [<span data-ttu-id="ca50e-112">網路應用程式的快取管理</span><span class="sxs-lookup"><span data-stu-id="ca50e-112">Cache Management for Network Applications</span></span>](cache-management-for-network-applications.md)
- [<span data-ttu-id="ca50e-113">快取原則</span><span class="sxs-lookup"><span data-stu-id="ca50e-113">Cache Policy</span></span>](cache-policy.md)
- [<span data-ttu-id="ca50e-114">以位置為基礎的快取原則</span><span class="sxs-lookup"><span data-stu-id="ca50e-114">Location-Based Cache Policies</span></span>](location-based-cache-policies.md)
- [<span data-ttu-id="ca50e-115">以時間為基礎的快取原則</span><span class="sxs-lookup"><span data-stu-id="ca50e-115">Time-Based Cache Policies</span></span>](time-based-cache-policies.md)
- [<span data-ttu-id="ca50e-116">\<requestCaching> (網路設定的元素) </span><span class="sxs-lookup"><span data-stu-id="ca50e-116">\<requestCaching> Element (Network Settings)</span></span>](../configure-apps/file-schema/network/requestcaching-element-network-settings.md)
