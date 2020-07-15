---
title: 爭用 ETW 事件-.NET
description: 取得爭用 ETW 事件的詳細資料，這會在每次發生爭用時引發，並會在執行時間所使用的執行緒監視器鎖定或原生鎖定時發生。
ms.date: 03/30/2017
helpviewer_keywords:
- contention events [.NET Framework]
- ETW, contention events (CLR)
ms.assetid: 6933e753-2f2a-425b-ae84-42138c957d76
ms.openlocfilehash: a36b091e0896562fffdb66e895d70049ce0667d7
ms.sourcegitcommit: 0fa2b7b658bf137e813a7f4d09589d64c148ebf5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/14/2020
ms.locfileid: "86309595"
---
# <a name="contention-etw-events"></a>爭用 ETW 事件

只要爭用執行階段所使用的 <xref:System.Threading.Monitor?displayProperty=nameWithType> 鎖定或原生鎖定，就會引發爭用事件。 如果某個執行緒等待鎖定，而另一個執行緒擁有該鎖定，則會發生爭用。

下表顯示引發爭用事件的關鍵字以及事件層級。 如需詳細資訊，請參閱[CLR ETW 關鍵字和層級](clr-etw-keywords-and-levels.md)。

|引發事件的關鍵字|層級|
|-----------------------------------|-----------|
|`ContentionKeyword` (0x4000)|告知性 (4)|

下表顯示事件資訊：

|事件|事件識別碼|引發的時機|
|-----------|--------------|-----------------|
|`ContentionStart_V1`|81|爭用開始。 此事件未包含執行緒等候取得鎖定之前的微調時間量；只有在執行緒等候取得鎖定時才會引發此事件。|
|`ContentionStop`|91|爭用結束。|

下表顯示事件資料：

|欄位名稱|資料類型|描述|
|----------------|---------------|-----------------|
|Flags|win:UInt8|0 表示 Managed；1 表示原生。|
|ClrInstanceID|win:UInt16|CLR 執行個體的唯一識別碼。|

## <a name="see-also"></a>另請參閱

- [CLR ETW 事件](clr-etw-events.md)
