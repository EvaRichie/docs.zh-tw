---
title: CALL_ID 結構
ms.date: 03/30/2017
api_name:
- CALL_ID
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- CALL_ID
helpviewer_keywords:
- CALL_ID structure [.NET Framework debugging]
ms.assetid: bfd46324-afec-4782-9c18-586d81fb4740
topic_type:
- apiref
ms.openlocfilehash: 1c795ee536483a7def9c0339efae66a013898a77
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83420626"
---
# <a name="call_id-structure"></a><span data-ttu-id="d59a8-102">CALL_ID 結構</span><span class="sxs-lookup"><span data-stu-id="d59a8-102">CALL_ID Structure</span></span>
<span data-ttu-id="d59a8-103">提供有關所呼叫函式之偵錯工具的資訊。</span><span class="sxs-lookup"><span data-stu-id="d59a8-103">Provides information to a debugger about a function that is being called.</span></span> <span data-ttu-id="d59a8-104">如需詳細資訊，請參閱[INotifySink2](inotifysink2-interface.md)介面。</span><span class="sxs-lookup"><span data-stu-id="d59a8-104">See the [INotifySink2](inotifysink2-interface.md) interface for more information.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="d59a8-105">語法</span><span class="sxs-lookup"><span data-stu-id="d59a8-105">Syntax</span></span>  
  
```cpp  
typedef struct tagCALL_ID  
{  
    LPCOLESTR       szMachine;  
    DWORD           dwPid;  
    USER_THREAD     *pUserThread;  
    STACK_ADDRESS   addrStackPointer;  
    LPCOLESTR       szEntryPoint;  
    LPCOLESTR       szDestinationMachine;  
} CALL_ID;  
```  
  
## <a name="members"></a><span data-ttu-id="d59a8-106">成員</span><span class="sxs-lookup"><span data-stu-id="d59a8-106">Members</span></span>  
  
|<span data-ttu-id="d59a8-107">成員</span><span class="sxs-lookup"><span data-stu-id="d59a8-107">Member</span></span>|<span data-ttu-id="d59a8-108">說明</span><span class="sxs-lookup"><span data-stu-id="d59a8-108">Description</span></span>|  
|------------|-----------------|  
|`szMachine`|<span data-ttu-id="d59a8-109">識別正在進行呼叫的電腦。</span><span class="sxs-lookup"><span data-stu-id="d59a8-109">Identifies the machine that is making the call.</span></span>|  
|`dwPid`|<span data-ttu-id="d59a8-110">識別機器處理器。</span><span class="sxs-lookup"><span data-stu-id="d59a8-110">Identifies the machine processor.</span></span>|  
|`pUserThread`|<span data-ttu-id="d59a8-111">識別正在執行呼叫的執行緒。</span><span class="sxs-lookup"><span data-stu-id="d59a8-111">Identifies the thread that is executing the call.</span></span>|  
|`addrStackPointer`|<span data-ttu-id="d59a8-112">指定呼叫堆疊的位址。</span><span class="sxs-lookup"><span data-stu-id="d59a8-112">Specifies the address of the call stack.</span></span>|  
|`szEntryPoint`|<span data-ttu-id="d59a8-113">指定呼叫的位址。</span><span class="sxs-lookup"><span data-stu-id="d59a8-113">Specifies the address of the call.</span></span>|  
|`szDestinationMachine`|<span data-ttu-id="d59a8-114">識別將執行呼叫的電腦。</span><span class="sxs-lookup"><span data-stu-id="d59a8-114">Identifies the machine that will execute the call.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="d59a8-115">需求</span><span class="sxs-lookup"><span data-stu-id="d59a8-115">Requirements</span></span>  
 <span data-ttu-id="d59a8-116">**標頭：** ProtocolNotify2 .idl</span><span class="sxs-lookup"><span data-stu-id="d59a8-116">**Header:** ProtocolNotify2.idl</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d59a8-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d59a8-117">See also</span></span>

- [<span data-ttu-id="d59a8-118">INotifySink2 介面</span><span class="sxs-lookup"><span data-stu-id="d59a8-118">INotifySink2 Interface</span></span>](inotifysink2-interface.md)
- [<span data-ttu-id="d59a8-119">診斷符號存放區結構</span><span class="sxs-lookup"><span data-stu-id="d59a8-119">Diagnostics Symbol Store Structures</span></span>](diagnostics-symbol-store-structures.md)
