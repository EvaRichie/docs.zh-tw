---
title: <forcePerformanceCounterUniqueSharedMemoryReads> 項目
ms.date: 03/30/2017
helpviewer_keywords:
- forcePerformanceCounterUniqueSharedMemoryReads element
- <forcePerformanceCounterUniqueSharedMemoryReads> element
ms.assetid: 91149858-4810-4f65-9b48-468488172c9b
ms.openlocfilehash: 719448ba3de2aca0621fc17b9fadbdd3b8588f2e
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91178238"
---
# <a name="forceperformancecounteruniquesharedmemoryreads-element"></a>\<forcePerformanceCounterUniqueSharedMemoryReads> 項目

指定 PerfCounter.dll 是否在 .NET Framework 1.1 版的應用程式中使用 CategoryOptions 登錄設定，以決定要從類別特定共用記憶體或從全域記憶體載入效能計數器資料。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<forcePerformanceCounterUniqueSharedMemoryReads>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<forcePerformanceCounterUniqueSharedMemoryReads
enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  

 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|`enabled`|必要屬性。<br /><br /> 指出 PerfCounter.dll 是否使用 CategoryOptions 登錄設定來判斷是否要從類別專用的共用記憶體或全域記憶體載入效能計數器資料。|  
  
## <a name="enabled-attribute"></a>啟用屬性  
  
|值|描述|  
|-----------|-----------------|  
|`false`|PerfCounter.dll 不使用 CategoryOptions 登錄設定，這是預設值。|  
|`true`|PerfCounter.dll 會使用 CategoryOptions 登錄設定。|  
  
### <a name="child-elements"></a>子元素  

 無。  
  
### <a name="parent-elements"></a>父項目  
  
|項目|描述|  
|-------------|-----------------|  
|`configuration`|通用語言執行平台和 .NET Framework 應用程式所使用之每個組態檔中的根項目。|  
|`runtime`|包含有關組件繫結和記憶體回收的資訊。|  
  
## <a name="remarks"></a>備註  

 在 .NET Framework 4 之前的 .NET Framework 版本中，已載入的 PerfCounter.dll 版本會對應至在進程中載入的執行時間。 如果電腦同時安裝了 .NET Framework 1.1 版和 .NET Framework 2.0，則 .NET Framework 1.1 應用程式會載入 .NET Framework 1.1 版的 PerfCounter.dll。 從 .NET Framework 4 開始，會載入 PerfCounter.dll 的最新安裝版本。 這表示，如果電腦上已安裝 .NET Framework 4，.NET Framework 1.1 應用程式將會載入 .NET Framework 4 版的 PerfCounter.dll。  
  
 從 .NET Framework 4 開始，使用效能計數器時，PerfCounter.dll 會檢查每個提供者的 CategoryOptions 登錄專案，以判斷是否應該從類別特定的共用記憶體或全域共用記憶體讀取。 .NET Framework 1.1 PerfCounter.dll 不會讀取該登錄專案，因為它不知道類別專用的共用記憶體;它一律會從全域共用記憶體中讀取。  
  
 為了與舊版相容，.NET Framework 4 PerfCounter.dll 不會在 .NET Framework 1.1 應用程式中執行時檢查 CategoryOptions 登錄專案。 它只會使用全域共用記憶體，就像 .NET Framework 1.1 PerfCounter.dll 一樣。 不過，您可以藉由啟用元素來指示 .NET Framework 4 PerfCounter.dll 檢查登錄設定 `<forcePerformanceCounterUniqueSharedMemoryReads>` 。  
  
> [!NOTE]
> 啟用專案 `<forcePerformanceCounterUniqueSharedMemoryReads>` 並不保證將會使用類別特定的共用記憶體。 將啟用設定為 `true` 只會導致 PerfCounter.dll 參考 CategoryOptions 登錄設定。 CategoryOptions 的預設設定是使用類別專用的共用記憶體;不過，您可以變更 CategoryOptions，以指出應該使用全域共用記憶體。  
  
 包含 CategoryOptions 設定的登錄機碼是 HKEY_LOCAL_MACHINE \System\CurrentControlSet\Services \\<類別名稱 \> \Performance。 根據預設，CategoryOptions 會設定為3，這會指示 PerfCounter.dll 使用分類專屬的共用記憶體。 如果 CategoryOptions 設定為0，PerfCounter.dll 會使用全域共用記憶體。 只有當要建立的實例名稱與要重複使用的實例相同時，才會重複使用實例資料。 所有版本都將能夠寫入至類別目錄。 如果 CategoryOptions 設定為1，則會使用全域共用記憶體，但如果類別目錄名稱的長度與要重複使用的類別相同，則可重複使用實例資料。  
  
 設定0和1可能會導致記憶體流失，以及填滿效能計數器記憶體。  
  
## <a name="example"></a>範例  

 下列範例示範如何指定 PerfCounter.dll 應該參考 CategoryOptions 登錄專案，以判斷是否應該使用類別專用的共用記憶體。  
  
```xml  
<configuration>  
  <runtime>  
    <forcePerformanceCounterUniqueSharedMemoryReads enabled="true"/>  
  </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>另請參閱

- [執行階段設定結構描述](index.md)
- [設定檔架構](../index.md)
