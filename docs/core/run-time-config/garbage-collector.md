---
title: 垃圾收集行程 config 設定
description: 瞭解用來設定垃圾收集行程如何管理 .NET Core 應用程式記憶體的執行時間設定。
ms.date: 07/10/2020
ms.topic: reference
ms.openlocfilehash: 91d155b638c7e69b3d2c0216266a7c0c0410db4c
ms.sourcegitcommit: ef50c99928183a0bba75e07b9f22895cd4c480f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87915994"
---
# <a name="run-time-configuration-options-for-garbage-collection"></a>用於垃圾收集的執行時間設定選項

此頁面包含垃圾收集行程 (GC) 設定的相關資訊，可在執行時間變更。 如果您正嘗試達到執行中應用程式的尖峰效能，請考慮使用這些設定。 不過，在一般情況下，預設值可為大部分的應用程式提供最佳效能。

這些設定會依此頁面的群組排列。 每個群組內的設定通常會彼此搭配使用，以達成特定結果。

> [!NOTE]
>
> - 這些設定也可以在應用程式執行時動態變更，因此您設定的任何執行時間設定可能會遭到覆寫。
> - 某些設定（例如[延遲層級](../../standard/garbage-collection/latency.md)）通常只會在設計階段透過 API 進行設定。 此頁面會省略這類設定。
> - 針對 [數值]，在 [檔案中的*runtimeconfig.js* ] 和 [用於環境變數的十六進位標記法] 設定中，使用十進位標記來進行設定。 若為十六進位值，您可以使用或不搭配 "0x" 前置詞來指定它們。

## <a name="flavors-of-garbage-collection"></a>垃圾收集的種類

垃圾收集的兩個主要類別是工作站 GC 和伺服器 GC。 如需兩者之間差異的詳細資訊，請參閱[工作站和伺服器垃圾收集](../../standard/garbage-collection/workstation-server-gc.md)。

垃圾收集的 subflavors 是背景和非並行的。

使用下列設定來選取垃圾收集的種類：

- [工作站與伺服器 GC 的比較](#workstation-vs-server)
- [背景 GC](#background-gc)

### <a name="workstation-vs-server"></a>工作站與伺服器的比較

- 設定應用程式是否使用工作站垃圾收集或伺服器垃圾收集。
- 預設值：工作站垃圾收集。 這相當於將值設定為 `false` 。

| | 設定名稱 | 值 | 引進的版本 |
| - | - | - | - |
| **runtimeconfig.js于** | `System.GC.Server` | `false`-工作站<br/>`true`-伺服器 | .NET Core 1.0 |
| **MSBuild 屬性** | `ServerGarbageCollection` | `false`-工作站<br/>`true`-伺服器 | .NET Core 1.0 |
| **環境變數** | `COMPlus_gcServer` | `0`-工作站<br/>`1`-伺服器 | .NET Core 1.0 |
| **.NET Framework 的app.config** | [GCServer](../../framework/configure-apps/file-schema/runtime/gcserver-element.md) | `false`-工作站<br/>`true`-伺服器 |  |

#### <a name="examples"></a>範例

檔案*上的runtimeconfig.js* ：

```json
{
   "runtimeOptions": {
      "configProperties": {
         "System.GC.Server": true
      }
   }
}
```

專案檔：

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <ServerGarbageCollection>true</ServerGarbageCollection>
  </PropertyGroup>

</Project>
```

### <a name="background-gc"></a>背景 GC

- 設定是否啟用背景 (並行) 垃圾收集。
- 預設值：使用背景 GC。 這相當於將值設定為 `true` 。
- 如需詳細資訊，請參閱[背景垃圾收集](../../standard/garbage-collection/background-gc.md)。

| | 設定名稱 | 值 | 引進的版本 |
| - | - | - | - |
| **runtimeconfig.js于** | `System.GC.Concurrent` | `true`-背景 GC<br/>`false`-非並行 GC | .NET Core 1.0 |
| **MSBuild 屬性** | `ConcurrentGarbageCollection` | `true`-背景 GC<br/>`false`-非並行 GC | .NET Core 1.0 |
| **環境變數** | `COMPlus_gcConcurrent` | `1`-背景 GC<br/>`0`-非並行 GC | .NET Core 1.0 |
| **.NET Framework 的app.config** | [gcConcurrent](../../framework/configure-apps/file-schema/runtime/gcconcurrent-element.md) | `true`-背景 GC<br/>`false`-非並行 GC |  |

#### <a name="examples"></a>範例

檔案*上的runtimeconfig.js* ：

```json
{
   "runtimeOptions": {
      "configProperties": {
         "System.GC.Concurrent": false
      }
   }
}
```

專案檔：

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <ConcurrentGarbageCollection>false</ConcurrentGarbageCollection>
  </PropertyGroup>

</Project>
```

## <a name="manage-resource-usage"></a>管理資源使用量

使用下列設定來管理垃圾收集行程的記憶體和處理器使用量：

- [將相似化為](#affinitize)
- [將相似化為 mask](#affinitize-mask)
- [將相似化為範圍](#affinitize-ranges)
- [CPU 群組](#cpu-groups)
- [堆積計數](#heap-count)
- [堆積限制](#heap-limit)
- [堆積限制百分比](#heap-limit-percent)
- [高記憶體百分比](#high-memory-percent)
- [每個物件的堆積限制](#per-object-heap-limits)
- [每個物件堆積限制百分比](#per-object-heap-limit-percents)
- [保留 VM](#retain-vm)

如需有關這些設定的詳細資訊，請參閱[工作站與伺服器 GC 之間的中間](https://devblogs.microsoft.com/dotnet/middle-ground-between-server-and-workstation-gc/)專案 blog。

### <a name="heap-count"></a>堆積計數

- 限制垃圾收集行程所建立的堆積數目。
- 僅適用于伺服器垃圾收集。
- 如果已啟用[GC 處理器親和性](#affinitize)（這是預設值），則堆積計數會將如何 `n` GC 堆積/執行緒設定為第一個 `n` 處理器。  (使用[將相似化為 mask](#affinitize-mask)或[將相似化為範圍](#affinitize-ranges)設定，以確切指定要將相似化為的處理器。 ) 
- 如果停用[gc 處理器親和性](#affinitize)，這項設定會限制 gc 堆積的數目。
- 如需詳細資訊，請參閱[GCHeapCount 備註](../../framework/configure-apps/file-schema/runtime/gcheapcount-element.md#remarks)。

| | 設定名稱 | 值 | 引進的版本 |
| - | - | - | - |
| **runtimeconfig.js于** | `System.GC.HeapCount` | *十進位值* | .NET Core 3.0 |
| **環境變數** | `COMPlus_GCHeapCount` | *十六進位值* | .NET Core 3.0 |
| **.NET Framework 的app.config** | [GCHeapCount](../../framework/configure-apps/file-schema/runtime/gcheapcount-element.md) | *十進位值* | .NET Framework 4.6.2 |

範例：

```json
{
   "runtimeOptions": {
      "configProperties": {
         "System.GC.HeapCount": 16
      }
   }
}
```

> [!TIP]
> 如果您要在*runtimeconfig.js*中設定選項，請指定十進位值。 如果您要將選項設定為環境變數，請指定十六進位值。 例如，若要將堆積數目限制為16，JSON 檔案的值會是16，而環境變數的值則是0x10 或10。

### <a name="affinitize-mask"></a>將相似化為 mask

- 指定垃圾收集行程執行緒應該使用的確切處理器。
- 如果停用[GC 處理器親和性](#affinitize)，則會忽略此設定。
- 僅適用于伺服器垃圾收集。
- 值是一個位元遮罩，用來定義進程可用的處理器。 例如，如果您要使用環境) 變數，則十進位值 1023 (或十六進位值為0x3FF 或3FF，如果是二進位標記法，則為 0011 1111 1111。 這會指定要使用前10個處理器。 若要指定接下來的10個處理器（也就是處理器10-19），請指定十進位值 1047552 (或0xFFC00 或 FFC00) 的十六進位值，這相當於二進位值 1111 1111 1100 0000 0000。

| | 設定名稱 | 值 | 引進的版本 |
| - | - | - | - |
| **runtimeconfig.js于** | `System.GC.HeapAffinitizeMask` | *十進位值* | .NET Core 3.0 |
| **環境變數** | `COMPlus_GCHeapAffinitizeMask` | *十六進位值* | .NET Core 3.0 |
| **.NET Framework 的app.config** | [GCHeapAffinitizeMask](../../framework/configure-apps/file-schema/runtime/gcheapaffinitizemask-element.md) | *十進位值* | .NET Framework 4.6.2 |

範例：

```json
{
   "runtimeOptions": {
      "configProperties": {
         "System.GC.HeapAffinitizeMask": 1023
      }
   }
}
```

### <a name="affinitize-ranges"></a>將相似化為範圍

- 指定要用於垃圾收集行程執行緒的處理器清單。
- 此設定類似[HeapAffinitizeMask](#affinitize-mask)，不同之處在于它可讓您指定64個以上的處理器。
- 若是 Windows 作業系統，請在處理器編號或範圍前面加上對應的[CPU 群組](/windows/win32/procthread/processor-groups)，例如 "0： 1-10，0：12，1： 50-52，1： 70"。
- 如果停用[GC 處理器親和性](#affinitize)，則會忽略此設定。
- 僅適用于伺服器垃圾收集。
- 如需詳細資訊，請參閱 Maoni Stephens 的 blog 上的[針對具有 > 64 cpu 的電腦，讓 CPU 設定更好用於 GC](https://devblogs.microsoft.com/dotnet/making-cpu-configuration-better-for-gc-on-machines-with-64-cpus/) 。

| | 設定名稱 | 值 | 引進的版本 |
| - | - | - | - |
| **runtimeconfig.js于** | `System.GC.GCHeapAffinitizeRanges` | 以逗號分隔的處理器編號或處理器編號範圍清單。<br/>Unix 範例： "1-10，12，50-52，70"<br/>Windows 範例： "0： 1-10，0：12，1： 50-52，1： 70" | .NET Core 3.0 |
| **環境變數** | `COMPlus_GCHeapAffinitizeRanges` | 以逗號分隔的處理器編號或處理器編號範圍清單。<br/>Unix 範例： "1-10，12，50-52，70"<br/>Windows 範例： "0： 1-10，0：12，1： 50-52，1： 70" | .NET Core 3.0 |

範例：

```json
{
   "runtimeOptions": {
      "configProperties": {
         "System.GC.GCHeapAffinitizeRanges": "0:1-10,0:12,1:50-52,1:70"
      }
   }
}
```

### <a name="cpu-groups"></a>CPU 群組

- 設定垃圾收集行程是否使用[CPU 群組](/windows/win32/procthread/processor-groups)。

  當64位 Windows 電腦具有多個 CPU 群組（也就是，有超過64個處理器）時，啟用這個元素會延伸所有 CPU 群組的垃圾收集。 垃圾收集行程會使用所有核心來建立和平衡堆積。

- 僅適用于64位 Windows 作業系統上的伺服器垃圾收集。
- 預設值： GC 不會跨越 CPU 群組延伸。 這相當於將值設定為 `0` 。
- 如需詳細資訊，請參閱 Maoni Stephens 的 blog 上的[針對具有 > 64 cpu 的電腦，讓 CPU 設定更好用於 GC](https://devblogs.microsoft.com/dotnet/making-cpu-configuration-better-for-gc-on-machines-with-64-cpus/) 。

| | 設定名稱 | 值 | 引進的版本 |
| - | - | - | - |
| **runtimeconfig.js于** | `System.GC.CpuGroup` | `0`-已停用<br/>`1`-已啟用 | .NET 5。0 |
| **環境變數** | `COMPlus_GCCpuGroup` | `0`-已停用<br/>`1`-已啟用 | .NET Core 1.0 |
| **.NET Framework 的app.config** | [GCCpuGroup](../../framework/configure-apps/file-schema/runtime/gccpugroup-element.md) | `false`-已停用<br/>`true`-已啟用 |  |

> [!NOTE]
> 若要設定 common language runtime (CLR) 也將執行緒集區中的執行緒分散到所有 CPU 群組，請啟用[Thread_UseAllCpuGroups 元素](../../framework/configure-apps/file-schema/runtime/thread-useallcpugroups-element.md)選項。 針對 .NET Core 應用程式，您可以將環境變數的值設定為，以啟用此選項 `COMPlus_Thread_UseAllCpuGroups` `1` 。

### <a name="affinitize"></a>將相似化為

- 指定是否要使用處理器*將相似化為*垃圾收集執行緒。 若要將相似化為 GC 執行緒，這表示它只能在其特定的 CPU 上執行。 會針對每個 GC 執行緒建立堆積。
- 僅適用于伺服器垃圾收集。
- 預設值：使用處理器將相似化為垃圾收集執行緒。 這相當於將值設定為 `false` 。

| | 設定名稱 | 值 | 引進的版本 |
| - | - | - | - |
| **runtimeconfig.js于** | `System.GC.NoAffinitize` | `false`-將相似化為<br/>`true`-不將相似化為 | .NET Core 3.0 |
| **環境變數** | `COMPlus_GCNoAffinitize` | `0`-將相似化為<br/>`1`-不將相似化為 | .NET Core 3.0 |
| **.NET Framework 的app.config** | [GCNoAffinitize](../../framework/configure-apps/file-schema/runtime/gcnoaffinitize-element.md) | `false`-將相似化為<br/>`true`-不將相似化為 | .NET Framework 4.6.2 |

範例：

```json
{
   "runtimeOptions": {
      "configProperties": {
         "System.GC.NoAffinitize": true
      }
   }
}
```

### <a name="heap-limit"></a>堆積限制

- 指定 GC 堆積和 GC 簿記的認可大小上限（以位元組為單位）。
- 此設定僅適用于64位電腦。
- 如果設定了[每個物件堆積的限制](#per-object-heap-limits)，則會忽略此設定。
- 只有在特定情況下才適用的預設值是容器的 20 MB 或75% 的記憶體限制。 預設值適用于下列情況：

  - 進程在具有指定記憶體限制的容器內執行。
  - 未設定[HeapHardLimitPercent](#heap-limit-percent) 。

| | 設定名稱 | 值 | 引進的版本 |
| - | - | - | - |
| **runtimeconfig.js于** | `System.GC.HeapHardLimit` | *十進位值* | .NET Core 3.0 |
| **環境變數** | `COMPlus_GCHeapHardLimit` | *十六進位值* | .NET Core 3.0 |

範例：

```json
{
   "runtimeOptions": {
      "configProperties": {
         "System.GC.HeapHardLimit": 209715200
      }
   }
}
```

> [!TIP]
> 如果您要在*runtimeconfig.js*中設定選項，請指定十進位值。 如果您要將選項設定為環境變數，請指定十六進位值。 例如，若要指定200數量 (MiB) 的堆積固定限制，此值會是209715200，適用于 JSON 檔案，而0xC800000 或 C800000 則適用于環境變數。

### <a name="heap-limit-percent"></a>堆積限制百分比

- 指定允許的 GC 堆積使用量，以總實體記憶體的百分比表示。
- 如果也設定了[HeapHardLimit](#heap-limit) ，則會忽略此設定。
- 此設定僅適用于64位電腦。
- 如果處理常式是在具有指定記憶體限制的容器內執行，則會以該記憶體限制的百分比來計算百分比。
- 如果設定了[每個物件堆積的限制](#per-object-heap-limits)，則會忽略此設定。
- 只有在特定情況下才適用的預設值是容器上 20 MB 或75% 記憶體限制的較小者。 預設值適用于下列情況：

  - 進程在具有指定記憶體限制的容器內執行。
  - 未設定[HeapHardLimit](#heap-limit) 。

| | 設定名稱 | 值 | 引進的版本 |
| - | - | - | - |
| **runtimeconfig.js于** | `System.GC.HeapHardLimitPercent` | *十進位值* | .NET Core 3.0 |
| **環境變數** | `COMPlus_GCHeapHardLimitPercent` | *十六進位值* | .NET Core 3.0 |

範例：

```json
{
   "runtimeOptions": {
      "configProperties": {
         "System.GC.HeapHardLimitPercent": 30
      }
   }
}
```

> [!TIP]
> 如果您要在*runtimeconfig.js*中設定選項，請指定十進位值。 如果您要將選項設定為環境變數，請指定十六進位值。 例如，若要將堆積使用量限制為30%，JSON 檔案的值會是30，而0x1E 或1E 則適用于環境變數。

### <a name="per-object-heap-limits"></a>每個物件的堆積限制

您可以針對每個物件堆積指定 GC 的允許堆積使用方式。 不同的堆積是大型物件堆積 (LOH) 、小型物件堆積 (SOH) ，以及釘選的物件堆積 (POH) 。

- 如果您指定任何 `COMPLUS_GCHeapHardLimitSOH` 、 `COMPLUS_GCHeapHardLimitLOH` 或設定的值 `COMPLUS_GCHeapHardLimitPOH` ，您也必須指定和的值 `COMPLUS_GCHeapHardLimitSOH` `COMPLUS_GCHeapHardLimitLOH` 。 如果您沒有這麼做，執行時間將無法初始化。
- `COMPLUS_GCHeapHardLimitPOH` 的預設值為 0。 `COMPLUS_GCHeapHardLimitSOH`和 `COMPLUS_GCHeapHardLimitLOH` 沒有預設值。

| | 設定名稱 | 值 | 引進的版本 |
| - | - | - | - |
| **runtimeconfig.js于** | `System.GC.HeapHardLimitSOH` | *十進位值* | .NET 5。0 |
| **環境變數** | `COMPLUS_GCHeapHardLimitSOH` | *十六進位值* | .NET 5。0 |

| | 設定名稱 | 值 | 引進的版本 |
| - | - | - | - |
| **runtimeconfig.js于** | `System.GC.HeapHardLimitLOH` | *十進位值* | .NET 5。0 |
| **環境變數** | `COMPLUS_GCHeapHardLimitLOH` | *十六進位值* | .NET 5。0 |

| | 設定名稱 | 值 | 引進的版本 |
| - | - | - | - |
| **runtimeconfig.js于** | `System.GC.HeapHardLimitPOH` | *十進位值* | .NET 5。0 |
| **環境變數** | `COMPLUS_GCHeapHardLimitPOH` | *十六進位值* | .NET 5。0 |

> [!TIP]
> 如果您要在*runtimeconfig.js*中設定選項，請指定十進位值。 如果您要將選項設定為環境變數，請指定十六進位值。 例如，若要指定200數量 (MiB) 的堆積固定限制，此值會是209715200，適用于 JSON 檔案，而0xC800000 或 C800000 則適用于環境變數。

### <a name="per-object-heap-limit-percents"></a>每個物件堆積限制百分比

您可以針對每個物件堆積指定 GC 的允許堆積使用方式。 不同的堆積是大型物件堆積 (LOH) 、小型物件堆積 (SOH) ，以及釘選的物件堆積 (POH) 。

- 如果您指定任何 `COMPLUS_GCHeapHardLimitSOHPercent` 、 `COMPLUS_GCHeapHardLimitLOHPercent` 或設定的值 `COMPLUS_GCHeapHardLimitPOHPercent` ，您也必須指定和的值 `COMPLUS_GCHeapHardLimitSOHPercent` `COMPLUS_GCHeapHardLimitLOHPercent` 。 如果您沒有這麼做，執行時間將無法初始化。
- 如果 `COMPLUS_GCHeapHardLimitSOH` 指定、和，則會忽略這些設定 `COMPLUS_GCHeapHardLimitLOH` `COMPLUS_GCHeapHardLimitPOH` 。
- 值為1表示 GC 使用該物件堆積的總實體記憶體的1%。
- 每個值都必須大於零且小於100。 此外，這三個百分比值的總和必須小於100。 否則，執行時間將無法初始化。

| | 設定名稱 | 值 | 引進的版本 |
| - | - | - | - |
| **runtimeconfig.js于** | `System.GC.HeapHardLimitSOHPercent` | *十進位值* | .NET 5。0 |
| **環境變數** | `COMPLUS_GCHeapHardLimitSOHPercent` | *十六進位值* | .NET 5。0 |

| | 設定名稱 | 值 | 引進的版本 |
| - | - | - | - |
| **runtimeconfig.js于** | `System.GC.HeapHardLimitLOHPercent` | *十進位值* | .NET 5。0 |
| **環境變數** | `COMPLUS_GCHeapHardLimitLOHPercent` | *十六進位值* | .NET 5。0 |

| | 設定名稱 | 值 | 引進的版本 |
| - | - | - | - |
| **runtimeconfig.js于** | `System.GC.HeapHardLimitPOHPercent` | *十進位值* | .NET 5。0 |
| **環境變數** | `COMPLUS_GCHeapHardLimitPOHPercent` | *十六進位值* | .NET 5。0 |

> [!TIP]
> 如果您要在*runtimeconfig.js*中設定選項，請指定十進位值。 如果您要將選項設定為環境變數，請指定十六進位值。 例如，若要將堆積使用量限制為30%，JSON 檔案的值會是30，而0x1E 或1E 則適用于環境變數。

### <a name="high-memory-percent"></a>高記憶體百分比

記憶體負載會以使用中的實體記憶體百分比表示。 根據預設，當實體記憶體負載達到**90%** 時，垃圾收集會更積極地執行完整、壓縮垃圾收集，以避免分頁。 當記憶體負載低於90% 時，GC 會優先使用完整垃圾收集的背景集合，其暫停時間較短，但不會減少總堆積大小。 在具有大量記憶體 (80 GB 或更) 的電腦上，預設負載閾值介於90% 到97% 之間。

高記憶體負載閾值可以透過 `COMPlus_GCHighMemPercent` 環境變數或 JSON 設定來調整 `System.GC.HighMemoryPercent` 。 如果您想要控制堆積大小，請考慮調整閾值。 例如，針對具有64GB 記憶體的電腦上的主要進程，當有10% 的可用記憶體時，GC 就可以開始做出反應。 但是對於較小的進程（例如，只耗用1GB 記憶體的處理常式），GC 很容易就能在沒有10% 的記憶體可用的情況下執行。 針對這些較小的進程，請考慮設定較高的閾值。 另一方面，如果您想要讓較大的進程具有較小的堆積大小 (即使有足夠的實體記憶體可用) ，也能降低此臨界值，這是一個有效的方法，讓 GC 能夠更快地將堆積壓縮。

> [!NOTE]
> 針對在容器中執行的進程，GC 會根據容器限制來考慮實體記憶體。

| | 設定名稱 | 值 | 引進的版本 |
| - | - | - | - |
| **runtimeconfig.js于** | `System.GC.HighMemoryPercent` | *十進位值* | .NET 5。0 |
| **環境變數** | `COMPlus_GCHighMemPercent` | *十六進位值* | |

> [!TIP]
> 如果您要在*runtimeconfig.js*中設定選項，請指定十進位值。 如果您要將選項設定為環境變數，請指定十六進位值。 例如，若要將高記憶體閾值設定為75%，JSON 檔案的值會是75，而0x4B 或4B 則適用于環境變數。

### <a name="retain-vm"></a>保留 VM

- 設定是否要將應該刪除的區段放在待命清單上以供日後使用，或是釋放給作業系統 (作業系統) 。
- 預設值：將區段釋放回作業系統。 這相當於將值設定為 `false` 。

| | 設定名稱 | 值 | 引進的版本 |
| - | - | - | - |
| **runtimeconfig.js于** | `System.GC.RetainVM` | `false`-發行至 OS<br/>`true`-put 待命 | .NET Core 1.0 |
| **MSBuild 屬性** | `RetainVMGarbageCollection` | `false`-發行至 OS<br/>`true`-put 待命 | .NET Core 1.0 |
| **環境變數** | `COMPlus_GCRetainVM` | `0`-發行至 OS<br/>`1`-put 待命 | .NET Core 1.0 |

#### <a name="examples"></a>範例

檔案*上的runtimeconfig.js* ：

```json
{
   "runtimeOptions": {
      "configProperties": {
         "System.GC.RetainVM": true
      }
   }
}
```

專案檔：

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <RetainVMGarbageCollection>true</RetainVMGarbageCollection>
  </PropertyGroup>

</Project>
```

## <a name="large-pages"></a>大型頁面

- 指定在設定堆積固定限制時是否應該使用大型分頁。
- 預設值：設定堆積固定限制時，請勿使用大型頁面。 這相當於將值設定為 `0` 。
- 這是實驗性設定。

| | 設定名稱 | 值 | 引進的版本 |
| - | - | - | - |
| **runtimeconfig.js于** | N/A | N/A | N/A |
| **環境變數** | `COMPlus_GCLargePages` | `0`-已停用<br/>`1`-已啟用 | .NET Core 3.0 |

## <a name="allow-large-objects"></a>允許大型物件

- 針對大於 2 gb (GB) 大小的陣列，設定64位平臺上的垃圾收集行程支援。
- 預設值： GC 支援大於 2 GB 的陣列。 這相當於將值設定為 `1` 。
- 在未來的 .NET 版本中，此選項可能會過時。

| | 設定名稱 | 值 | 引進的版本 |
| - | - | - | - |
| **runtimeconfig.js于** | N/A | N/A | N/A |
| **環境變數** | `COMPlus_gcAllowVeryLargeObjects` | `1`-已啟用<br/> `0`-已停用 | .NET Core 1.0 |
| **.NET Framework 的app.config** | [Gcallowverylargeobjects>](../../framework/configure-apps/file-schema/runtime/gcallowverylargeobjects-element.md) | `1`-已啟用<br/> `0`-已停用 | .NET Framework 4.5 |

## <a name="large-object-heap-threshold"></a>大型物件堆積閾值

- 指定導致物件在大型物件堆積上執行的臨界值大小（以位元組為單位） (LOH) 。
- 預設閾值為85000個位元組。
- 您指定的值必須大於預設閾值。

| | 設定名稱 | 值 | 引進的版本 |
| - | - | - | - |
| **runtimeconfig.js于** | `System.GC.LOHThreshold` | *十進位值* | .NET Core 1.0 |
| **環境變數** | `COMPlus_GCLOHThreshold` | *十六進位值* | .NET Core 1.0 |
| **.NET Framework 的app.config** | [GCLOHThreshold](../../framework/configure-apps/file-schema/runtime/gclohthreshold-element.md) | *十進位值* | .NET Framework 4.8 |

範例：

```json
{
   "runtimeOptions": {
      "configProperties": {
         "System.GC.LOHThreshold": 120000
      }
   }
}
```

> [!TIP]
> 如果您要在*runtimeconfig.js*中設定選項，請指定十進位值。 如果您要將選項設定為環境變數，請指定十六進位值。 例如，若要設定120000個位元組的閾值大小，JSON 檔案的值會是120000，而環境變數的值則是0x1D4C0 或1D4C0。

## <a name="standalone-gc"></a>獨立 GC

- 指定包含執行時間打算載入之垃圾收集行程的程式庫路徑。
- 如需詳細資訊，請參閱[獨立 GC 載入器設計](https://github.com/dotnet/runtime/blob/master/docs/design/features/standalone-gc-loading.md)。

| | 設定名稱 | 值 | 引進的版本 |
| - | - | - | - |
| **runtimeconfig.js于** | N/A | N/A | N/A |
| **環境變數** | `COMPlus_GCName` | *string_path* | .NET Core 2.0 |
