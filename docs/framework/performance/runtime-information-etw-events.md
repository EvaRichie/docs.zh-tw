---
title: 執行階段資訊 ETW 事件
description: 請參閱「執行時間資訊 ETW 事件」，其會記錄 SKU、版本號碼、執行時間的啟用方式 (包括) 的命令列參數、GUID 等等。
ms.date: 03/30/2017
helpviewer_keywords:
- runtime information events [.NET Framework]
- ETW, runtime information events
ms.assetid: 68b4edbc-7f3b-45f6-ab75-4fd066d6af9a
ms.openlocfilehash: 354740b36ccab742022058288da84b22d460edc5
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96245610"
---
# <a name="runtime-information-etw-events"></a>執行階段資訊 ETW 事件

執行階段的這些 ETW 事件記錄資訊，包含 SKU、版本號碼、執行階段啟用方式、用來啟動它的命令列參數、GUID (適用時)，以及其他相關資訊。 如果多個執行階段是在某個處理序內執行，則這些事件所提供的資訊 (ClrInstanceID) 有助於釐清執行階段。  
  
 下表顯示兩個執行階段資訊事件。 事件可能會透過任何關鍵字或遮罩引發。 (如需詳細資訊，請參閱 [CLR ETW Keywords and Levels](clr-etw-keywords-and-levels.md))。  
  
|事件|事件識別碼|提供者|描述|  
|-----------|--------------|--------------|-----------------|  
|`RuntimeInformationEvent`|187|CLRRuntime|在載入執行階段時引發。|  
|`RuntimeInformationDCStart`|187|CLRRundown|列舉已載入的執行階段。|  
  
 下表顯示事件資料。  
  
|欄位名稱|資料類型|描述|  
|----------------|---------------|-----------------|  
|ClrInstanceID|win:UInt16|CLR 或 CoreCLR 執行個體的唯一 ID。|  
|SKU|win:UInt16|1 - 桌面 CLR。<br /><br /> 2 - CoreCLR。|  
|BclVersion - 主要版本|win:UInt16|mscorlib.dll 的主要版本。|  
|BclVersion - 次要版本|win:UInt16|mscorlib.dll 的次要版本號碼。|  
|BclVersion - 組建編號|win:UInt16|mscorlib.dll. 的組建編號。|  
|BclVersion - QFE|win:UInt16|mscorlib.dll 的 Hotfix 版本號碼。|  
|VMVersion - 主要版本|win:UInt16|clr.dll 或 coreclr.dll 的版本 (視 SKU 而定)。|  
|VMVersion - 次要版本|win:UInt16|clr.dll 或 coreclr.dll 的次要版本 (視 SKU 而定)。|  
|VMVersion - 組建編號|win:UInt16|clr.dll 或 coreclr.dll 的組建編號。|  
|VMVersion - QFE|win:UInt16|clr.dll 或 coreclr.dll 的 Hotfix 版本號碼。|  
|StartupFlags|win:UInt32|啟動旗標定義於 mscoree.h 中。|  
|StartupMode|win:UInt8|0x01 - Managed 可執行檔。<br /><br /> 0x02 - 託管 CLR。<br /><br /> 0x04 - C++ Managed Interop。<br /><br /> 0x08 - COM 已啟用。<br /><br /> 0x10 - 其他。|  
|CommandLine|win:UnicodeString|只有在 StartupMode=0x01 時才為非 Null。|  
|ComObjectGUID|win:GUID|只有在 StartupMode=0x08 時才為非 Null。|  
|RuntimeDLLPath|win:UnicodeString|已載入處理序中之 CLR .dll 檔案的路徑。|  
  
## <a name="see-also"></a>另請參閱

- [CLR ETW 事件](clr-etw-events.md)
