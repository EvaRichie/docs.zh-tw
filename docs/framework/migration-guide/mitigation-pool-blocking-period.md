---
title: 風險降低︰集區封鎖期
description: 瞭解如何減輕因連線至 Azure SQL 資料庫而移除連線集區封鎖期間所造成的問題。
ms.date: 03/30/2017
ms.assetid: 92d2de20-79be-4df1-b182-144143a8866a
ms.openlocfilehash: be60fe87952697d964571176743a4e6f839c4894
ms.sourcegitcommit: cf5a800a33de64d0aad6d115ffcc935f32375164
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/20/2020
ms.locfileid: "86475407"
---
# <a name="mitigation-pool-blocking-period"></a>風險降低︰集區封鎖期
已移除 Azure SQL Database 連線的連線集區封鎖期。  
  
## <a name="additional-description"></a>其他描述  
 在 .NET Framework 4.6.1 和舊版中，如果應用程式在連線到資料庫時發生暫時性連線失敗，由於連線集區會快取此錯誤並在 5 秒鐘到 1 分鐘後重新擲回，因此無法很快就重試連線。如需詳細資訊，請參閱 [SQL Server 連線共用 (ADO.NET)](../data/adonet/sql-server-connection-pooling.md)。 此行為會對 Azure SQL Database 連線造成問題，連線通常會因暫時性錯誤而失敗，而且一般會在幾秒內復原。 連線集區封鎖功能表示應用程式有很長的一段時間無法連線到資料庫，即使資料庫可供使用也一樣。 此行為特別會對連線到 Azure SQL Database 且需要在幾秒內轉譯的 Web 應用程式造成問題。  
  
 從 .NET Framework 4.6.2 開始，針對已知 Azure SQL Database (*.database.windows.net、\*.database.chinacloudapi.cn、\*.database.usgovcloudapi.net、\*.database.cloudapi.de) 的連線開啟要求，不會快取連線開啟錯誤。 至於所有其他連線嘗試，則會繼續強制執行連線集區封鎖期。  
  
## <a name="impact"></a>影響  
 這項變更允許立即重試 Azure SQL Database 的連線開啟嘗試，因而提升啟用雲端功能的應用程式效能。  
  
## <a name="mitigation"></a>降低  
 如果這項變更會對應用程式造成負面影響，可以藉由設定新的 <xref:System.Data.SqlClient.SqlConnectionStringBuilder.PoolBlockingPeriod%2A?displayProperty=nameWithType> 屬性，來設定連線集區封鎖期。  屬性的值是 <xref:System.Data.SqlClient.PoolBlockingPeriod?displayProperty=nameWithType> 列舉的成員，可以採用三個值的其中一個值︰  
  
- <xref:System.Data.SqlClient.PoolBlockingPeriod.AlwaysBlock?displayProperty=nameWithType>
  
- <xref:System.Data.SqlClient.PoolBlockingPeriod.Auto?displayProperty=nameWithType>
  
- <xref:System.Data.SqlClient.PoolBlockingPeriod.NeverBlock?displayProperty=nameWithType>
  
 將 <xref:System.Data.SqlClient.SqlConnectionStringBuilder.PoolBlockingPeriod%2A> 屬性設為 <xref:System.Data.SqlClient.PoolBlockingPeriod.AlwaysBlock?displayProperty=nameWithType> 可以還原舊有行為。  
  
## <a name="see-also"></a>另請參閱

- [應用程式相容性](application-compatibility.md)
