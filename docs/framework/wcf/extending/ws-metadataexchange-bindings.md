---
title: WS-MetadataExchange 繫結
ms.date: 03/30/2017
ms.assetid: 10f8de5d-b81d-4ea7-b37e-7f2c00c39714
ms.openlocfilehash: 94f0ba602cd1f58f5491a44a64e24be8ea52895b
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96293984"
---
# <a name="ws-metadataexchange-bindings"></a><span data-ttu-id="f5f79-102">WS-MetadataExchange 繫結</span><span class="sxs-lookup"><span data-stu-id="f5f79-102">WS-MetadataExchange Bindings</span></span>

<span data-ttu-id="f5f79-103">本主題會說明如何為各種傳輸建構預設中繼資料交換繫結。</span><span class="sxs-lookup"><span data-stu-id="f5f79-103">This topic describes how the default metadata exchange bindings are constructed for various transports.</span></span>  
  
## <a name="the-default-bindings"></a><span data-ttu-id="f5f79-104">預設繫結</span><span class="sxs-lookup"><span data-stu-id="f5f79-104">The Default Bindings</span></span>  
  
|<span data-ttu-id="f5f79-105">預設繫結名稱</span><span class="sxs-lookup"><span data-stu-id="f5f79-105">Default Binding Name</span></span>|<span data-ttu-id="f5f79-106">繫結的建構方式</span><span class="sxs-lookup"><span data-stu-id="f5f79-106">How the binding is constructed</span></span>|  
|--------------------------|------------------------------------|  
|<span data-ttu-id="f5f79-107">mexHttpBinding</span><span class="sxs-lookup"><span data-stu-id="f5f79-107">mexHttpBinding</span></span>|<span data-ttu-id="f5f79-108">已停用傳輸層級安全性的 <xref:System.ServiceModel.WSHttpBinding>。</span><span class="sxs-lookup"><span data-stu-id="f5f79-108">A <xref:System.ServiceModel.WSHttpBinding> with transport-level security disabled.</span></span>|  
|<span data-ttu-id="f5f79-109">mexHttpsBinding</span><span class="sxs-lookup"><span data-stu-id="f5f79-109">mexHttpsBinding</span></span>|<span data-ttu-id="f5f79-110">支援傳輸層級安全性的 <xref:System.ServiceModel.WSHttpBinding>。</span><span class="sxs-lookup"><span data-stu-id="f5f79-110">A <xref:System.ServiceModel.WSHttpBinding> that supports transport-level security.</span></span>|  
|<span data-ttu-id="f5f79-111">mexNamedPipeBinding</span><span class="sxs-lookup"><span data-stu-id="f5f79-111">mexNamedPipeBinding</span></span>|<span data-ttu-id="f5f79-112">具有使用預設值之 的 。</span><span class="sxs-lookup"><span data-stu-id="f5f79-112">A  <xref:System.ServiceModel.Channels.CustomBinding> with a <xref:System.ServiceModel.Channels.NamedPipeTransportBindingElement> using the default values.</span></span>|  
|<span data-ttu-id="f5f79-113">mexTcpBinding</span><span class="sxs-lookup"><span data-stu-id="f5f79-113">mexTcpBinding</span></span>|<span data-ttu-id="f5f79-114">具有使用預設值之 <xref:System.ServiceModel.Channels.CustomBinding> 的 <xref:System.ServiceModel.Channels.TcpTransportBindingElement>。</span><span class="sxs-lookup"><span data-stu-id="f5f79-114">A <xref:System.ServiceModel.Channels.CustomBinding> with a <xref:System.ServiceModel.Channels.TcpTransportBindingElement> using default values.</span></span>|
