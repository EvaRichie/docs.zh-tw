---
title: 共用 Web 裝載的最佳化
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- garbage collection, Web hosting
- garbage collection, optimizing
- garbage collection, shared Web hosting
ms.assetid: be98c0ab-7ef8-409f-8a0d-cb6e5b75ff20
ms.openlocfilehash: ccaacd44f8aaed9c3178cb94f98b0f58d4d3c7d4
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84285985"
---
# <a name="optimization-for-shared-web-hosting"></a>共用 Web 裝載的最佳化
如果您是透過裝載數個小型 Web 站台所共用之伺服器的系統管理員，則可以將下列 `gcTrimCommitOnLowMemory` 設定加入 .NET 目錄中 Aspnet.config 檔案的 `runtime` 節點，以最佳化效能與增加站台的容量：  
  
 `<gcTrimCommitOnLowMemory enabled="true|false"/>`  
  
> [!NOTE]
> 此設定僅建議針對共用 Web 裝載案例使用。  
  
 因為記憶體回收行程會保留供未來配置使用的記憶體，其認可空間可以超過嚴格需要的空間。 您可以減少這個空間，以容納系統記憶體負載過重的時間。 減少此認可空間會改善效能，並擴充容量以裝載更多站台。  
  
 當啟用 `gcTrimCommitOnLowMemory` 設定時，記憶體回收行程會評估系統記憶體負載，並在負載達到 90% 時進入調整模式。 它會維持調整模式，直到負載降至 85%。  
  
 當情況允許時，記憶體回收行程可以決定 `gcTrimCommitOnLowMemory` 設定不會協助目前的應用程式並忽略它。  
  
## <a name="example"></a>範例  
 下列 XML 片段會示範如何啟用 `gcTrimCommitOnLowMemory` 設定。 省略符號表示 `runtime` 節點中可能有的其他設定。  
  
```xml  
<?xml version="1.0" encoding="UTF-8"?>  
<configuration>  
    <runtime>  
    . . .  
    <gcTrimCommitOnLowMemory enabled="true"/>  
    </runtime>  
    . . .  
</configuration>  
```  
  
## <a name="see-also"></a>另請參閱

- [記憶體回收](index.md)
