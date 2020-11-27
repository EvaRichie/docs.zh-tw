---
title: 39456 - TrackingRecordDropped
ms.date: 03/30/2017
ms.assetid: da13d5bc-1736-47a4-b3fd-064ca8040326
ms.openlocfilehash: d958b506e057bc0d59f954debdc9da6015bf5f1f
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96273095"
---
# <a name="39456---trackingrecorddropped"></a>39456 - TrackingRecordDropped

## <a name="properties"></a>屬性  
  
|||  
|-|-|  
|識別碼|39456|  
|關鍵字|WFTracking|  
|層級|警告|  
|通路|Microsoft-Windows-Application Server-Applications/Debug|  
  
## <a name="description"></a>描述  

 表示追蹤記錄的大小已超出 ETW 工作階段提供者所允許的最大值而丟棄追蹤記錄。  
  
## <a name="message"></a>訊息  

 追蹤記錄 %1 的大小已超出提供者 %2 的 ETW 工作階段所允許的最大值  
  
## <a name="details"></a>詳細資料  
  
|資料項目名稱|資料項目型別|描述|  
|--------------------|--------------------|-----------------|  
|例外狀況|xs:string|例外狀況的例外狀況詳細資料|  
|AppDomain|xs:string|由 AppDomain.CurrentDomain.FriendlyName 傳回的字串。|
