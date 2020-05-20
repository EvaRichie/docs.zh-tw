---
title: LoggingLevelEnum 列舉
ms.date: 03/30/2017
api_name:
- LoggingLevelEnum
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- LoggingLevelEnum
helpviewer_keywords:
- LoggingLevelEnum enumeration [.NET Framework debugging]
ms.assetid: 09daac08-005a-46b2-beab-408d0820c5e5
topic_type:
- apiref
ms.openlocfilehash: 62ea982f30a6a73648d9bf36722c0b5a49a68896
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83420743"
---
# <a name="logginglevelenum-enumeration"></a><span data-ttu-id="b63fd-102">LoggingLevelEnum 列舉</span><span class="sxs-lookup"><span data-stu-id="b63fd-102">LoggingLevelEnum Enumeration</span></span>
<span data-ttu-id="b63fd-103">指出當 Managed 執行緒記錄事件時，寫入至事件記錄檔之描述性訊息的嚴重性層級。</span><span class="sxs-lookup"><span data-stu-id="b63fd-103">Indicates the severity level of a descriptive message that is written to the event log when a managed thread logs an event.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="b63fd-104">語法</span><span class="sxs-lookup"><span data-stu-id="b63fd-104">Syntax</span></span>  
  
```cpp  
typedef enum LoggingLevelEnum {  
    LTraceLevel0 = 0,  
    LTraceLevel1,  
    LTraceLevel2,  
    LTraceLevel3,  
    LTraceLevel4,  
    LStatusLevel0 = 20,  
    LStatusLevel1,  
    LStatusLevel2,  
    LStatusLevel3,  
    LStatusLevel4,  
    LWarningLevel = 40,  
    LErrorLevel = 50,  
    LPanicLevel = 100  
} LoggingLevelEnum;  
```  
  
## <a name="members"></a><span data-ttu-id="b63fd-105">成員</span><span class="sxs-lookup"><span data-stu-id="b63fd-105">Members</span></span>  
  
|<span data-ttu-id="b63fd-106">成員</span><span class="sxs-lookup"><span data-stu-id="b63fd-106">Member</span></span>|<span data-ttu-id="b63fd-107">說明</span><span class="sxs-lookup"><span data-stu-id="b63fd-107">Description</span></span>|  
|------------|-----------------|  
|`LTraceLevel0`|<span data-ttu-id="b63fd-108">訊息是追蹤層級0。</span><span class="sxs-lookup"><span data-stu-id="b63fd-108">The message is a trace level 0.</span></span>|  
|`LTraceLevel1`|<span data-ttu-id="b63fd-109">訊息是追蹤層級1。</span><span class="sxs-lookup"><span data-stu-id="b63fd-109">The message is a trace level 1.</span></span>|  
|`LTraceLevel2`|<span data-ttu-id="b63fd-110">訊息是追蹤層級2。</span><span class="sxs-lookup"><span data-stu-id="b63fd-110">The message is a trace level 2.</span></span>|  
|`LTraceLevel3`|<span data-ttu-id="b63fd-111">訊息是追蹤層級3。</span><span class="sxs-lookup"><span data-stu-id="b63fd-111">The message is a trace level 3.</span></span>|  
|`LTraceLevel4`|<span data-ttu-id="b63fd-112">訊息是追蹤層級4。</span><span class="sxs-lookup"><span data-stu-id="b63fd-112">The message is a trace level 4.</span></span>|  
|`LStatusLevel0`|<span data-ttu-id="b63fd-113">訊息是狀態層級0。</span><span class="sxs-lookup"><span data-stu-id="b63fd-113">The message is a status level 0.</span></span>|  
|`LStatusLevel1`|<span data-ttu-id="b63fd-114">訊息是狀態層級1。</span><span class="sxs-lookup"><span data-stu-id="b63fd-114">The message is a status level 1.</span></span>|  
|`LStatusLevel2`|<span data-ttu-id="b63fd-115">訊息是狀態層級2。</span><span class="sxs-lookup"><span data-stu-id="b63fd-115">The message is a status level 2.</span></span>|  
|`LStatusLevel3`|<span data-ttu-id="b63fd-116">訊息是狀態層級3。</span><span class="sxs-lookup"><span data-stu-id="b63fd-116">The message is a status level 3.</span></span>|  
|`LStatusLevel4`|<span data-ttu-id="b63fd-117">訊息是狀態層級4。</span><span class="sxs-lookup"><span data-stu-id="b63fd-117">The message is a status level 4.</span></span>|  
|`LWarningLevel`|<span data-ttu-id="b63fd-118">訊息是警告層級。</span><span class="sxs-lookup"><span data-stu-id="b63fd-118">The message is a warning level.</span></span>|  
|`LErrorLevel`|<span data-ttu-id="b63fd-119">訊息為錯誤層級。</span><span class="sxs-lookup"><span data-stu-id="b63fd-119">The message is an error level.</span></span>|  
|`LPanicLevel`|<span data-ttu-id="b63fd-120">訊息是一個驚慌層級。</span><span class="sxs-lookup"><span data-stu-id="b63fd-120">The message is a panic level.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="b63fd-121">備註</span><span class="sxs-lookup"><span data-stu-id="b63fd-121">Remarks</span></span>  
 <span data-ttu-id="b63fd-122">Common language runtime （CLR）會呼叫[ICorDebugManagedCallback：： LogMessage](icordebugmanagedcallback-logmessage-method.md)方法，以通知偵錯工具 managed 執行緒已記錄事件。</span><span class="sxs-lookup"><span data-stu-id="b63fd-122">The common language runtime (CLR) calls the [ICorDebugManagedCallback::LogMessage](icordebugmanagedcallback-logmessage-method.md) method to notify the debugger that a managed thread has logged an event.</span></span> <span data-ttu-id="b63fd-123">CLR 會傳遞列舉的值， `LoggingLevelEnum` 指出 managed 執行緒寫入事件記錄檔之訊息的嚴重性層級。</span><span class="sxs-lookup"><span data-stu-id="b63fd-123">The CLR passes a value of the `LoggingLevelEnum` enumeration to indicate the severity level of the message that the managed thread wrote to the event log.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="b63fd-124">需求</span><span class="sxs-lookup"><span data-stu-id="b63fd-124">Requirements</span></span>  
 <span data-ttu-id="b63fd-125">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="b63fd-125">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="b63fd-126">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="b63fd-126">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="b63fd-127">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="b63fd-127">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="b63fd-128">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="b63fd-128">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b63fd-129">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b63fd-129">See also</span></span>

- <xref:System.Diagnostics.EventLog>
- [<span data-ttu-id="b63fd-130">偵錯列舉</span><span class="sxs-lookup"><span data-stu-id="b63fd-130">Debugging Enumerations</span></span>](debugging-enumerations.md)
