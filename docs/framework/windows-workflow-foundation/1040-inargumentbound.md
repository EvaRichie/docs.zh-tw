---
title: 1040 - InArgumentBound
ms.date: 03/30/2017
ms.assetid: 7dfaad1b-36c0-4575-84c1-31d63b0eaf5d
ms.openlocfilehash: 04a61892ea817d5168ccbfccf68c0b74ee43e983
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96238947"
---
# <a name="1040---inargumentbound"></a>1040 - InArgumentBound

## <a name="properties"></a>屬性  
  
|||  
|-|-|  
|識別碼|1040|  
|關鍵字|WFActivities|  
|層級|「詳細資訊」|  
|通路|Microsoft-Windows-Application Server-Applications/Debug|  
  
## <a name="description"></a>描述  

 表示已繫結 In 引數。  
  
## <a name="message"></a>訊息  

 活動 '%2'、DisplayName：'%3'、InstanceId：'%4' 中的引數 '%1' 已與值 %5 繫結。  
  
## <a name="details"></a>詳細資料  
  
|資料項目名稱|資料項目型別|描述|  
|--------------------|--------------------|-----------------|  
|InArgument|xs:string|InArgument 的名稱。|  
|活動|xs:string|活動的型別名稱。|  
|DisplayName|xs:string|活動的顯示名稱。|  
|InstanceId|xs:string|活動的執行個體 ID。|  
|值|xs:string|該值繫結至 InArgument。|  
|AppDomain|xs:string|由 AppDomain.CurrentDomain.FriendlyName 傳回的字串。|
