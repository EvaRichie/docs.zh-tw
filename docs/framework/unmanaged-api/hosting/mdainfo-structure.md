---
title: MDAInfo 結構
ms.date: 03/30/2017
api_name:
- MDAInfo
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- MDAInfo
helpviewer_keywords:
- MDAInfo structure [.NET Framework hosting]
ms.assetid: fb8c14f7-d461-43d1-8b47-adb6723b9b93
topic_type:
- apiref
ms.openlocfilehash: 517e0ae7fb5d5151f94f82d9146ebbf40bad2ef9
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503857"
---
# <a name="mdainfo-structure"></a>MDAInfo 結構
提供事件的相關詳細資料 `Event_MDAFired` ，這會觸發建立 managed 偵錯工具（MDA）。  
  
## <a name="syntax"></a>語法  
  
```cpp  
typedef struct _MDAInfo {  
    LPCWSTR  lpMDACaption;  
    LPCWSTR  lpMDAMessage  
} MDAInfo;  
```  
  
## <a name="members"></a>成員  
  
|成員|說明|  
|------------|-----------------|  
|`lpMDACaption`|目前 MDA 的標題。 標題描述觸發事件的失敗類型 `Event_MDAFired` 。|  
|`lpMDAMessage`|目前 MDA 所提供的輸出訊息。|  
  
## <a name="remarks"></a>備註  
 Managed 偵錯工具（Mda）是與 common language runtime （CLR）搭配使用的偵錯工具，可執行工作，例如識別執行時間執行引擎中的無效條件，或傾印引擎狀態的其他相關資訊。 Mda 會產生有關事件的 XML 訊息，而這種情況很容易被陷阱。 它們特別適用于在 managed 和非受控碼之間的轉換。  
  
 當觸發建立 MDA 的事件引發時，執行時間會採取下列步驟：  
  
- 如果主機未藉由呼叫[ICLROnEventManager：： RegisterActionOnEvent](iclroneventmanager-registeractiononevent-method.md)來註冊[IActionOnCLREvent](iactiononclrevent-interface.md)實例以收到事件的通知 `Event_MDAFired` ，執行時間會繼續執行其預設的非裝載行為。  
  
- 如果主機已註冊此事件的處理常式，執行時間會檢查偵錯工具是否已附加至進程。 如果是，執行時間會中斷偵錯工具。 當偵錯工具繼續時，它會呼叫主機。 如果未附加任何偵錯工具，執行時間會呼叫 `IActionOnCLREvent::OnEvent` ，並將實例的指標當做 `MDAInfo` 參數傳遞 `data` 。  
  
 主機可以選擇啟動 Mda，並在啟用 MDA 時收到通知。 這可讓主機有機會覆寫預設行為，並中止引發事件的 managed 執行緒，以防止它損毀進程狀態。 如需使用 Mda 的詳細資訊，請參閱[診斷 Managed 偵錯工具的錯誤](../../debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)。  
  
## <a name="requirements"></a>規格需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** Mscoree.dll .idl  
  
 連結**庫：** 包含為 Mscoree.dll 中的資源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [裝載結構](hosting-structures.md)
- [使用 Managed 偵錯助理診斷錯誤](../../debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)
