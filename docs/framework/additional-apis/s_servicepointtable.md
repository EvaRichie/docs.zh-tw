---
title: ServicePointManager。 s_ServicePointTable] 欄位
description: 閱讀 .NET 中 s_ServicePointTable ServicePointManager 欄位的相關資訊。 此雜湊表欄位包含 AppDomain 中的作用中 HTTP 連接（ServicePoints）。
ms.date: 05/01/2017
topic_type:
- apiref
api_name:
- System.Net.ServicePointManager.s_ServicePointTable
api_location:
- System.dll
api_type:
- Assembly
ms.assetid: 24459679-291c-401a-9def-e42b29466fcf
ms.openlocfilehash: 9462ae10125dd37706f786a1f2cef78e62fbabcc
ms.sourcegitcommit: 45c8eed045779b70a47b23169897459d0323dc89
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "84989540"
---
# <a name="servicepointmanagers_servicepointtable-field"></a>ServicePointManager. s \_ ServicePointTable 欄位

`ServicePointManager.s_ServicePointTable`是 <xref:System.Collections.Hashtable> ，其中包含中的使用中 HTTP 連接清單 <xref:System.Net.ServicePoint> <xref:System.AppDomain> 。

## <a name="syntax"></a>Syntax
  
```csharp  
private static Hashtable s_ServicePointTable
```

> [!WARNING]
> `ServicePointManager.s_ServicePointTable`欄位是私用的，不適合直接在程式碼中使用。
>
> 在任何情況下，Microsoft 不支援在生產應用程式中使用此欄位。

## <a name="requirements"></a>需求

**命名空間：** <xref:System.Net>

**元件：** 系統（在 System.dll 中）

**.NET Framework 版本：** 自2.0 開始提供。
