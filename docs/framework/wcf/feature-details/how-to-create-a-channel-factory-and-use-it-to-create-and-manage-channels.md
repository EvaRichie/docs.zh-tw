---
title: 作法：建立通道處理站並使用它來建立與管理通道
ms.date: 03/30/2017
ms.assetid: 018dcc30-9f61-419e-af8e-412a85e8d282
ms.openlocfilehash: 44b0f45d1a340b8e8229ded827ad3ded738ae677
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96256777"
---
# <a name="how-to-create-a-channel-factory-and-use-it-to-create-and-manage-channels"></a><span data-ttu-id="23af9-102">作法：建立通道處理站並使用它來建立與管理通道</span><span class="sxs-lookup"><span data-stu-id="23af9-102">How to: Create a Channel Factory and Use it to Create and Manage Channels</span></span>

<span data-ttu-id="23af9-103">針對可供用戶端用來傳送與接收在服務端點之間往返之訊息的不同雙工通道類型，<xref:System.ServiceModel.DuplexChannelFactory%601> 類別提供了這些雙工通道的建立與管理方式。</span><span class="sxs-lookup"><span data-stu-id="23af9-103">The <xref:System.ServiceModel.DuplexChannelFactory%601> class provides the means to create and manage duplex channels of different types that clients use to send and receive messages to and from service endpoints.</span></span>  
  
## <a name="example"></a><span data-ttu-id="23af9-104">範例</span><span class="sxs-lookup"><span data-stu-id="23af9-104">Example</span></span>  

 <span data-ttu-id="23af9-105">下列程式碼會顯示如何建立通道處理站，並使用它建立並管理通道。</span><span class="sxs-lookup"><span data-stu-id="23af9-105">The following code shows how to create a channel factory and use it to create and manage channels.</span></span>  
  
 [!code-csharp[S_CustomAuthentication#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_customauthentication/cs/instance.cs#1)]  
  
## <a name="see-also"></a><span data-ttu-id="23af9-106">另請參閱</span><span class="sxs-lookup"><span data-stu-id="23af9-106">See also</span></span>

- <xref:System.ServiceModel.DuplexChannelFactory%601>
