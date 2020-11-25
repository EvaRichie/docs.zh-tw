---
title: INotifyConnection2::UnregisterNotifySource 方法
ms.date: 03/30/2017
api_name:
- INotifyConnection2.UnregisterNotifySource
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- INotifyConnection2::UnregisterNotifySource
helpviewer_keywords:
- INotifyConnection2::UnregisterNotifySource method [.NET Framework debugging]
- UnregisterNotifySource method [.NET Framework debugging]
ms.assetid: 2fc6c715-646f-41fd-9c12-c59b40575269
topic_type:
- apiref
ms.openlocfilehash: 90220c2bfea683ff0472473e180c9e11ea568672
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95720031"
---
# <a name="inotifyconnection2unregisternotifysource-method"></a><span data-ttu-id="93b30-102">INotifyConnection2::UnregisterNotifySource 方法</span><span class="sxs-lookup"><span data-stu-id="93b30-102">INotifyConnection2::UnregisterNotifySource Method</span></span>

<span data-ttu-id="93b30-103">從連接中移除指定的通知來源物件。</span><span class="sxs-lookup"><span data-stu-id="93b30-103">Removes a specified notification source object from the connection.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="93b30-104">語法</span><span class="sxs-lookup"><span data-stu-id="93b30-104">Syntax</span></span>  
  
```cpp  
HRESULT UnregisterNotifySource  
(  
    [in]  INotifySource2*  in_pNotifySource  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="93b30-105">參數</span><span class="sxs-lookup"><span data-stu-id="93b30-105">Parameters</span></span>  

 `in_pNotifySource`  
 <span data-ttu-id="93b30-106">在要取消註冊的通知物件。</span><span class="sxs-lookup"><span data-stu-id="93b30-106">[in] Notification object to be unregistered.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="93b30-107">傳回值</span><span class="sxs-lookup"><span data-stu-id="93b30-107">Return Value</span></span>  

 <span data-ttu-id="93b30-108">如果方法成功，則為 S_OK。</span><span class="sxs-lookup"><span data-stu-id="93b30-108">S_OK if the method succeeds.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="93b30-109">需求</span><span class="sxs-lookup"><span data-stu-id="93b30-109">Requirements</span></span>  

 <span data-ttu-id="93b30-110">**標頭：** ProtocolNotify2 .idl</span><span class="sxs-lookup"><span data-stu-id="93b30-110">**Header:** ProtocolNotify2.idl</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="93b30-111">另請參閱</span><span class="sxs-lookup"><span data-stu-id="93b30-111">See also</span></span>

- [<span data-ttu-id="93b30-112">INotifyConnection2 介面</span><span class="sxs-lookup"><span data-stu-id="93b30-112">INotifyConnection2 Interface</span></span>](inotifyconnection2-interface.md)
- [<span data-ttu-id="93b30-113">INotifySource2 介面</span><span class="sxs-lookup"><span data-stu-id="93b30-113">INotifySource2 Interface</span></span>](inotifysource2-interface.md)
- [<span data-ttu-id="93b30-114">INotifySink2 介面</span><span class="sxs-lookup"><span data-stu-id="93b30-114">INotifySink2 Interface</span></span>](inotifysink2-interface.md)
- [<span data-ttu-id="93b30-115">RegisterNotifySource 方法</span><span class="sxs-lookup"><span data-stu-id="93b30-115">RegisterNotifySource Method</span></span>](inotifyconnection2-registernotifysource-method.md)
