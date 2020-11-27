---
title: 3551 - BufferOutOfOrderMessageNoBookmark
ms.date: 03/30/2017
ms.assetid: 7930d6c4-c843-4a83-933a-cecd71b80d1e
ms.openlocfilehash: 5e6a5f9d21435fee8309bd222443407e50ec2cee
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96263603"
---
# <a name="3551---bufferoutofordermessagenobookmark"></a><span data-ttu-id="b19e8-102">3551 - BufferOutOfOrderMessageNoBookmark</span><span class="sxs-lookup"><span data-stu-id="b19e8-102">3551 - BufferOutOfOrderMessageNoBookmark</span></span>

## <a name="properties"></a><span data-ttu-id="b19e8-103">屬性</span><span class="sxs-lookup"><span data-stu-id="b19e8-103">Properties</span></span>  
  
|||  
|-|-|  
|<span data-ttu-id="b19e8-104">識別碼</span><span class="sxs-lookup"><span data-stu-id="b19e8-104">ID</span></span>|<span data-ttu-id="b19e8-105">3551</span><span class="sxs-lookup"><span data-stu-id="b19e8-105">3551</span></span>|  
|<span data-ttu-id="b19e8-106">關鍵字</span><span class="sxs-lookup"><span data-stu-id="b19e8-106">Keywords</span></span>|<span data-ttu-id="b19e8-107">WFServices</span><span class="sxs-lookup"><span data-stu-id="b19e8-107">WFServices</span></span>|  
|<span data-ttu-id="b19e8-108">層級</span><span class="sxs-lookup"><span data-stu-id="b19e8-108">Level</span></span>|<span data-ttu-id="b19e8-109">資訊</span><span class="sxs-lookup"><span data-stu-id="b19e8-109">Information</span></span>|  
|<span data-ttu-id="b19e8-110">通路</span><span class="sxs-lookup"><span data-stu-id="b19e8-110">Channel</span></span>|<span data-ttu-id="b19e8-111">Microsoft-Windows-Application Server-Applications/Analytic</span><span class="sxs-lookup"><span data-stu-id="b19e8-111">Microsoft-Windows-Application Server-Applications/Analytic</span></span>|  
  
## <a name="description"></a><span data-ttu-id="b19e8-112">描述</span><span class="sxs-lookup"><span data-stu-id="b19e8-112">Description</span></span>  

 <span data-ttu-id="b19e8-113">表示書籤繼續執行失敗。</span><span class="sxs-lookup"><span data-stu-id="b19e8-113">Indicates a bookmark resumption has failed.</span></span> <span data-ttu-id="b19e8-114">當服務執行個體準備好處理這個特定作業時，就會再次嘗試緩衝接收作業。</span><span class="sxs-lookup"><span data-stu-id="b19e8-114">The buffered receive operation will be attempted again when the service instance is ready to process this particular operation.</span></span>  
  
## <a name="message"></a><span data-ttu-id="b19e8-115">訊息</span><span class="sxs-lookup"><span data-stu-id="b19e8-115">Message</span></span>  

 <span data-ttu-id="b19e8-116">目前無法在服務執行個體 '%1' 上執行作業 '%2'。</span><span class="sxs-lookup"><span data-stu-id="b19e8-116">Operation '%2' on service instance '%1' cannot be performed at this time.</span></span> <span data-ttu-id="b19e8-117">將在服務執行個體準備就緒可以處理這個特定作業時，再次嘗試。</span><span class="sxs-lookup"><span data-stu-id="b19e8-117">Another attempt will be made when the service instance is ready to process this particular operation.</span></span>  
  
## <a name="details"></a><span data-ttu-id="b19e8-118">詳細資料</span><span class="sxs-lookup"><span data-stu-id="b19e8-118">Details</span></span>  
  
|<span data-ttu-id="b19e8-119">資料項目名稱</span><span class="sxs-lookup"><span data-stu-id="b19e8-119">Data Item Name</span></span>|<span data-ttu-id="b19e8-120">資料項目型別</span><span class="sxs-lookup"><span data-stu-id="b19e8-120">Data Item Type</span></span>|<span data-ttu-id="b19e8-121">描述</span><span class="sxs-lookup"><span data-stu-id="b19e8-121">Description</span></span>|  
|--------------------|--------------------|-----------------|  
|<span data-ttu-id="b19e8-122">OperationName</span><span class="sxs-lookup"><span data-stu-id="b19e8-122">OperationName</span></span>|<span data-ttu-id="b19e8-123">xs:string</span><span class="sxs-lookup"><span data-stu-id="b19e8-123">xs:string</span></span>|<span data-ttu-id="b19e8-124">作業的名稱。</span><span class="sxs-lookup"><span data-stu-id="b19e8-124">The name of the operation.</span></span>|  
|<span data-ttu-id="b19e8-125">ServiceInstanceId</span><span class="sxs-lookup"><span data-stu-id="b19e8-125">ServiceInstanceId</span></span>|<span data-ttu-id="b19e8-126">xs:string</span><span class="sxs-lookup"><span data-stu-id="b19e8-126">xs:string</span></span>|<span data-ttu-id="b19e8-127">服務執行個體的 ID。</span><span class="sxs-lookup"><span data-stu-id="b19e8-127">The id of the service instance.</span></span>|  
|<span data-ttu-id="b19e8-128">AppDomain</span><span class="sxs-lookup"><span data-stu-id="b19e8-128">AppDomain</span></span>|<span data-ttu-id="b19e8-129">xs:string</span><span class="sxs-lookup"><span data-stu-id="b19e8-129">xs:string</span></span>|<span data-ttu-id="b19e8-130">由 AppDomain.CurrentDomain.FriendlyName 傳回的字串。</span><span class="sxs-lookup"><span data-stu-id="b19e8-130">The string returned by AppDomain.CurrentDomain.FriendlyName.</span></span>|
