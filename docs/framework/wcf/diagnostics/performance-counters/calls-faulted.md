---
title: 發生錯誤的呼叫數
ms.date: 03/30/2017
ms.assetid: bb9e8045-6aeb-4b7f-a825-8283c44252a1
ms.openlocfilehash: cfd829c6229f4fb483e18cfcecf4d484fad64409
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96271404"
---
# <a name="calls-faulted"></a><span data-ttu-id="6d92d-102">發生錯誤的呼叫數</span><span class="sxs-lookup"><span data-stu-id="6d92d-102">Calls Faulted</span></span>

<span data-ttu-id="6d92d-103">計數器名稱：發生錯誤的呼叫數</span><span class="sxs-lookup"><span data-stu-id="6d92d-103">Counter Name: Calls Faulted</span></span>  
  
## <a name="description"></a><span data-ttu-id="6d92d-104">描述</span><span class="sxs-lookup"><span data-stu-id="6d92d-104">Description</span></span>  

 <span data-ttu-id="6d92d-105">傳回錯誤之這個作業的呼叫次數。</span><span class="sxs-lookup"><span data-stu-id="6d92d-105">Number of calls to this operation that returned faults.</span></span> <span data-ttu-id="6d92d-106">在 Windows Communication Foundation (WCF) 應用程式中，服務方法會使用 SOAP 錯誤訊息來溝通處理錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="6d92d-106">In Windows Communication Foundation (WCF) applications, service methods communicate processing error information using SOAP fault messages.</span></span> <span data-ttu-id="6d92d-107">SOAP 錯誤是包含在服務作業之中繼資料內的訊息類型，因此會建立錯誤合約，而用戶端可使用該合約來讓其執行作業更強固或更具互動性。</span><span class="sxs-lookup"><span data-stu-id="6d92d-107">SOAP faults are message types that are included in the metadata for a service operation and therefore create a fault contract that clients can use to make their execution more robust or interactive.</span></span> <span data-ttu-id="6d92d-108">由於 SOAP 錯誤會以 XML 表單的形式傳達給用戶端，所以其互通性很高。</span><span class="sxs-lookup"><span data-stu-id="6d92d-108">Since SOAP faults are expressed to clients in XML form, they are highly interoperable.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="6d92d-109">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6d92d-109">See also</span></span>

- [<span data-ttu-id="6d92d-110">指定與處理合約和服務中的錯誤</span><span class="sxs-lookup"><span data-stu-id="6d92d-110">Specifying and Handling Faults in Contracts and Services</span></span>](../../specifying-and-handling-faults-in-contracts-and-services.md)
