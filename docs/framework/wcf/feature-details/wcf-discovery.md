---
title: WCF 探索
ms.date: 03/30/2017
helpviewer_keywords:
- WCF [WCF], discovery
- Windows Communication Foundation [WCF], discovery
- discovery [WCF]
ms.assetid: 462c4913-f388-45a9-9042-28ae96a4e735
ms.openlocfilehash: 176e9760d98f9640bd9d1c7b059287dc29c0d666
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96289356"
---
# <a name="wcf-discovery"></a><span data-ttu-id="98448-102">WCF 探索</span><span class="sxs-lookup"><span data-stu-id="98448-102">WCF Discovery</span></span>

<span data-ttu-id="98448-103">Windows Communication Foundation (WCF) 提供的支援，可讓服務在執行時間以可互通的方式使用 WS-Discovery 通訊協定來進行探索。</span><span class="sxs-lookup"><span data-stu-id="98448-103">Windows Communication Foundation (WCF) provides support to enable services to be discoverable at runtime in an interoperable way using the WS-Discovery protocol.</span></span> <span data-ttu-id="98448-104">WCF 服務可以使用多播訊息或探索 proxy 伺服器，宣佈其對網路的可用性。</span><span class="sxs-lookup"><span data-stu-id="98448-104">WCF services can announce their availability to the network using a multicast message or to a discovery proxy server.</span></span> <span data-ttu-id="98448-105">用戶端應用程式可搜尋網路或探索 Proxy 伺服器，來尋找符合整組準則的服務。</span><span class="sxs-lookup"><span data-stu-id="98448-105">Client applications can search the network or a discovery proxy server to find services that meet a set of criteria.</span></span> <span data-ttu-id="98448-106">本節中的主題提供概要並詳細說明此功能的程式設計模型。</span><span class="sxs-lookup"><span data-stu-id="98448-106">The topics in this section provide an overview and describe the programming model for this feature in detail.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="98448-107">本節內容</span><span class="sxs-lookup"><span data-stu-id="98448-107">In This Section</span></span>  

 [<span data-ttu-id="98448-108">WCF 探索概觀</span><span class="sxs-lookup"><span data-stu-id="98448-108">WCF Discovery Overview</span></span>](wcf-discovery-overview.md)  
 <span data-ttu-id="98448-109">提供 WCF 所提供 WS-Discovery 支援的總覽。</span><span class="sxs-lookup"><span data-stu-id="98448-109">Provides an overview of WS-Discovery support provided by WCF.</span></span>  
  
 [<span data-ttu-id="98448-110">WCF 探索物件模型</span><span class="sxs-lookup"><span data-stu-id="98448-110">WCF Discovery Object Model</span></span>](wcf-discovery-object-model.md)  
 <span data-ttu-id="98448-111">說明物件模型中的類別以及 WS-Discovery 支援的擴充性。</span><span class="sxs-lookup"><span data-stu-id="98448-111">Describes the classes in the object model and extensibility of WS-Discovery support.</span></span>  
  
 [<span data-ttu-id="98448-112">作法：以程式設計方式將探索能力新增至 WCF 服務與用戶端</span><span class="sxs-lookup"><span data-stu-id="98448-112">How to: Programmatically Add Discoverability to a WCF Service and Client</span></span>](how-to-programmatically-add-discoverability-to-a-wcf-service-and-client.md)  
 <span data-ttu-id="98448-113">示範如何讓 Windows Communication Foundation (WCF) 可探索的服務。</span><span class="sxs-lookup"><span data-stu-id="98448-113">Shows how to make a Windows Communication Foundation (WCF) service discoverable.</span></span>  
  
 [<span data-ttu-id="98448-114">實作探索 Proxy</span><span class="sxs-lookup"><span data-stu-id="98448-114">Implementing a Discovery Proxy</span></span>](implementing-a-discovery-proxy.md)  
 <span data-ttu-id="98448-115">說明用來實作探索 Proxy 的必要步驟、使用探索 Proxy 註冊的可探索服務，以及使用探索 Proxy 來尋找服務的用戶端。</span><span class="sxs-lookup"><span data-stu-id="98448-115">Describes the steps required to implement a discovery proxy, a discoverable service that registers with the discovery proxy, and a client that uses the discovery proxy to find the discoverable service.</span></span>  
  
 [<span data-ttu-id="98448-116">探索版本控制</span><span class="sxs-lookup"><span data-stu-id="98448-116">Discovery Versioning</span></span>](discovery-versioning.md)  
 <span data-ttu-id="98448-117">簡要概述部分新探索功能的原型實作。</span><span class="sxs-lookup"><span data-stu-id="98448-117">Provides a brief overview of a prototype implementation of some new discovery features.</span></span> <span data-ttu-id="98448-118">同時也概要說明如何選取要使用的探索版本。</span><span class="sxs-lookup"><span data-stu-id="98448-118">It also gives an overview on how to select the discovery version to use.</span></span>  
  
 [<span data-ttu-id="98448-119">在組態檔中設定探索</span><span class="sxs-lookup"><span data-stu-id="98448-119">Configuring Discovery in a Configuration File</span></span>](configuring-discovery-in-a-configuration-file.md)  
 <span data-ttu-id="98448-120">示範如何設定組態中的探索。</span><span class="sxs-lookup"><span data-stu-id="98448-120">Shows how to configure Discovery in configuration.</span></span>  
  
 [<span data-ttu-id="98448-121">使用探索用戶端通道</span><span class="sxs-lookup"><span data-stu-id="98448-121">Using the Discovery Client Channel</span></span>](using-the-discovery-client-channel.md)  
 <span data-ttu-id="98448-122">顯示如何在撰寫 WCF 用戶端應用程式時使用探索用戶端通道。</span><span class="sxs-lookup"><span data-stu-id="98448-122">Shows how to use a Discovery Client Channel when writing a WCF client application.</span></span>
