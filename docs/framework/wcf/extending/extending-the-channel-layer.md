---
title: 擴充通道層
ms.date: 03/30/2017
helpviewer_keywords:
- extending channels [WCF]
ms.assetid: 4238db74-2fb6-4dc8-a326-f58527230810
ms.openlocfilehash: 8d051ff84ea0562b3d7c810b2c884f4d8b787952
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96273018"
---
# <a name="extending-the-channel-layer"></a><span data-ttu-id="df46b-102">擴充通道層</span><span class="sxs-lookup"><span data-stu-id="df46b-102">Extending the Channel Layer</span></span>

<span data-ttu-id="df46b-103">通道層負責在用戶端與服務之間交換訊息。</span><span class="sxs-lookup"><span data-stu-id="df46b-103">The channel layer is responsible for the exchange of messages between clients and services.</span></span> <span data-ttu-id="df46b-104">通道擴充可以實作新的通訊協定功能，例如安全性，或者實作傳輸功能，例如實作新的網路傳輸以傳送 SOAP 訊息。</span><span class="sxs-lookup"><span data-stu-id="df46b-104">Channel extensions can implement new protocol functionality, such as security, or transport functionality, such as implementing a new network transport to carry SOAP messages.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="df46b-105">本節內容</span><span class="sxs-lookup"><span data-stu-id="df46b-105">In This Section</span></span>  

 [<span data-ttu-id="df46b-106">通道模型概觀</span><span class="sxs-lookup"><span data-stu-id="df46b-106">Channel Model Overview</span></span>](channel-model-overview.md)  
 <span data-ttu-id="df46b-107">提供有關通道的高階概觀、通道提供的功能，以及通道如何在服務和用戶端應用程式中運作。</span><span class="sxs-lookup"><span data-stu-id="df46b-107">Provides a high-level overview of what channels are, the features that they provide and how they work both in a service and a client application.</span></span>  
  
 [<span data-ttu-id="df46b-108">開發通道</span><span class="sxs-lookup"><span data-stu-id="df46b-108">Developing Channels</span></span>](developing-channels.md)  
 <span data-ttu-id="df46b-109">深入說明各種通道基礎結構扮演的角色、狀態引擎和狀態生命週期如何運作、如何處理例外狀況和錯誤、如何實作中繼資料支援，以及通道如何搭配訊息編碼器使用。</span><span class="sxs-lookup"><span data-stu-id="df46b-109">Describes in depth the roles that the various channel infrastructure types play, how the state engine and state lifecycle works, how to handle exceptions and faults, how to implement metadata support, and how channels work with message encoders.</span></span>  
  
 [<span data-ttu-id="df46b-110">自訂編碼器</span><span class="sxs-lookup"><span data-stu-id="df46b-110">Custom Encoders</span></span>](custom-encoders.md)  
 <span data-ttu-id="df46b-111">討論訊息編碼器在通道中扮演的角色，以及如何建立訊息編碼器。</span><span class="sxs-lookup"><span data-stu-id="df46b-111">Describes the role that message encoders play in channels and how to build one.</span></span>  
  
 [<span data-ttu-id="df46b-112">自訂資料流升級</span><span class="sxs-lookup"><span data-stu-id="df46b-112">Custom Stream Upgrades</span></span>](custom-stream-upgrades.md)  
 <span data-ttu-id="df46b-113">討論資料流導向的傳輸所提供之資料流的升級程序。</span><span class="sxs-lookup"><span data-stu-id="df46b-113">Describes the process of upgrading the streams provided by stream-oriented transports.</span></span>
