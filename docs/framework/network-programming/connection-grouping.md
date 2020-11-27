---
title: 連接群組
ms.date: 03/30/2017
helpviewer_keywords:
- Internet, connections
- connections [.NET Framework], grouping
- WebRequest class, connection grouping
- network resources, connections
- connection pooling
ms.assetid: 2ec502e8-4ba0-4c22-9410-f28eaf4eee63
ms.openlocfilehash: 8bd4412a4c13dd490fce3118f59b5bb1f0d3ea85
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96250563"
---
# <a name="connection-grouping"></a><span data-ttu-id="4ffac-102">連接群組</span><span class="sxs-lookup"><span data-stu-id="4ffac-102">Connection Grouping</span></span>

<span data-ttu-id="4ffac-103">連線群組會建立與單一應用程式內所定義連接集區之特定要求的關聯。</span><span class="sxs-lookup"><span data-stu-id="4ffac-103">Connection grouping associates specific requests within a single application to a defined connection pool.</span></span> <span data-ttu-id="4ffac-104">連線至代表使用者的後端伺服器並使用支援委派的驗證通訊協定 (例如 Kerberos) 的中介層應用程式，或者提供其專屬認證的中介層應用程式，可能需要這項作業，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="4ffac-104">This can be required by a middle-tier application that connects to a back-end server on behalf of a user and uses an authentication protocol that supports delegation, such as Kerberos, or by a middle-tier application that supplies its own credentials, as in the example below.</span></span> <span data-ttu-id="4ffac-105">例如，假設使用者 Joe 瀏覽內部網站，以顯示其薪資資訊。</span><span class="sxs-lookup"><span data-stu-id="4ffac-105">For example, suppose a user, Joe, visits an internal Web site that displays his payroll information.</span></span> <span data-ttu-id="4ffac-106">驗證 Joe 之後，中介層應用程式伺服器會使用 Joe 的認證來連線至後端伺服器，以擷取其薪資資訊。</span><span class="sxs-lookup"><span data-stu-id="4ffac-106">After authenticating Joe, the middle-tier application server uses Joe's credentials to connect to the back-end server to retrieve his payroll information.</span></span> <span data-ttu-id="4ffac-107">接下來，Susan 會瀏覽網站，並要求其薪資資訊。</span><span class="sxs-lookup"><span data-stu-id="4ffac-107">Next, Susan visits the site and requests her payroll information.</span></span> <span data-ttu-id="4ffac-108">因為中介層應用程式已經使用 Joe 的認證進行連線，所以後端伺服器會回應 Joe 的資訊。</span><span class="sxs-lookup"><span data-stu-id="4ffac-108">Because the middle-tier application has already made a connection using Joe's credentials, the back-end server responds with Joe's information.</span></span> <span data-ttu-id="4ffac-109">不過，如果應用程式將傳送至後端伺服器的每個要求指派給使用者名稱所組成的連線群組，則每位使用者都屬於不同的連接集區，因此不會意外與其他使用者共用驗證資訊。</span><span class="sxs-lookup"><span data-stu-id="4ffac-109">However, if the application assigns each request sent to the back-end server to a connection group formed from the user name, then each user belongs to a separate connection pool and cannot accidentally share authentication information with another user.</span></span>  
  
 <span data-ttu-id="4ffac-110">若要將要求指派給特定連線群組，您必須先將名稱指派給 <xref:System.Net.WebRequest> 的 <xref:System.Net.WebRequest.ConnectionGroupName%2A> 屬性，再提出要求。</span><span class="sxs-lookup"><span data-stu-id="4ffac-110">To assign a request to a specific connection group, you must assign a name to the <xref:System.Net.WebRequest.ConnectionGroupName%2A> property of your <xref:System.Net.WebRequest> before making the request.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="4ffac-111">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4ffac-111">See also</span></span>

- [<span data-ttu-id="4ffac-112">管理連接</span><span class="sxs-lookup"><span data-stu-id="4ffac-112">Managing Connections</span></span>](managing-connections.md)
- [<span data-ttu-id="4ffac-113">作法：將使用者資訊指派給群組連線</span><span class="sxs-lookup"><span data-stu-id="4ffac-113">How to: Assign User Information to Group Connections</span></span>](how-to-assign-user-information-to-group-connections.md)
