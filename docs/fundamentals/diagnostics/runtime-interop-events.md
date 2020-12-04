---
title: Interop 運行時間事件
description: 請參閱收集 interop 特定診斷資訊的 .NET 運行時間事件。
ms.date: 11/13/2020
ms.topic: reference
helpviewer_keywords:
- Interop events (CoreCLR)
- ETW, EventPipe, LTTng interop events (CoreCLR)
ms.openlocfilehash: 5635fb55b3a6ffa3f5611da80cdb2909e226e2ea
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "96586636"
---
# <a name="net-runtime-interop-events"></a><span data-ttu-id="91501-103">.NET 執行時間 interop 事件</span><span class="sxs-lookup"><span data-stu-id="91501-103">.NET runtime interop events</span></span>

<span data-ttu-id="91501-104">這些運行時間事件會捕獲一般中繼語言 (CIL) 存根產生的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="91501-104">These runtime events capture information about Common Intermediate Language (CIL) stub generation.</span></span> <span data-ttu-id="91501-105">如需如何基於診斷目的使用這些事件的詳細資訊，請參閱[記錄和追蹤 .net 應用程式](../../core/diagnostics/logging-tracing.md)。</span><span class="sxs-lookup"><span data-stu-id="91501-105">For more information about how to use these events for diagnostic purposes, see [logging and tracing .NET applications](../../core/diagnostics/logging-tracing.md)</span></span>

## <a name="ilstubgenerated-event"></a><span data-ttu-id="91501-106">ILStubGenerated 事件</span><span class="sxs-lookup"><span data-stu-id="91501-106">ILStubGenerated event</span></span>

|<span data-ttu-id="91501-107">引發事件的關鍵字</span><span class="sxs-lookup"><span data-stu-id="91501-107">Keyword for raising the event</span></span>|<span data-ttu-id="91501-108">層級</span><span class="sxs-lookup"><span data-stu-id="91501-108">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="91501-109">`InteropKeyword` (0x2000)</span><span class="sxs-lookup"><span data-stu-id="91501-109">`InteropKeyword` (0x2000)</span></span>|<span data-ttu-id="91501-110">Informational(4)</span><span class="sxs-lookup"><span data-stu-id="91501-110">Informational(4)</span></span>|
  
|<span data-ttu-id="91501-111">事件</span><span class="sxs-lookup"><span data-stu-id="91501-111">Event</span></span>|<span data-ttu-id="91501-112">事件識別碼</span><span class="sxs-lookup"><span data-stu-id="91501-112">Event ID</span></span>|<span data-ttu-id="91501-113">引發的時機</span><span class="sxs-lookup"><span data-stu-id="91501-113">Raised when</span></span>|
|-----------|--------------|-----------------|
|`ILStubGenerated`|<span data-ttu-id="91501-114">88</span><span class="sxs-lookup"><span data-stu-id="91501-114">88</span></span>|<span data-ttu-id="91501-115">產生 IL 存根。</span><span class="sxs-lookup"><span data-stu-id="91501-115">An IL Stub is generated.</span></span>|

|<span data-ttu-id="91501-116">欄位名稱</span><span class="sxs-lookup"><span data-stu-id="91501-116">Field name</span></span>|<span data-ttu-id="91501-117">資料類型</span><span class="sxs-lookup"><span data-stu-id="91501-117">Data type</span></span>|<span data-ttu-id="91501-118">描述</span><span class="sxs-lookup"><span data-stu-id="91501-118">Description</span></span>|
|----------------|---------------|-----------------|
|`ModuleID`|`win:UInt16`|<span data-ttu-id="91501-119">模組識別碼。</span><span class="sxs-lookup"><span data-stu-id="91501-119">The module identifier.</span></span>|
|`StubMethodID`|`win:UInt64`|<span data-ttu-id="91501-120">虛設常式方法識別項。</span><span class="sxs-lookup"><span data-stu-id="91501-120">The stub method identifier.</span></span>|
|`StubFlags`|`win:UInt32`|<span data-ttu-id="91501-121">虛設常式的旗標：</span><span class="sxs-lookup"><span data-stu-id="91501-121">The flags for the stub:</span></span><br /><br /> <span data-ttu-id="91501-122">`0x1` -反向 interop。</span><span class="sxs-lookup"><span data-stu-id="91501-122">`0x1` - Reverse interop.</span></span><br /><br /> <span data-ttu-id="91501-123">`0x2` -COM interop。</span><span class="sxs-lookup"><span data-stu-id="91501-123">`0x2` - COM interop.</span></span><br /><br /> <span data-ttu-id="91501-124">`0x4` -NGen.exe 產生的存根。</span><span class="sxs-lookup"><span data-stu-id="91501-124">`0x4` - Stub generated by NGen.exe.</span></span><br /><br /> <span data-ttu-id="91501-125">`0x8` 授權.</span><span class="sxs-lookup"><span data-stu-id="91501-125">`0x8` - Delegate.</span></span><br /><br /> <span data-ttu-id="91501-126">`0x10` -Variable 引數。</span><span class="sxs-lookup"><span data-stu-id="91501-126">`0x10` - Variable argument.</span></span><br /><br /> <span data-ttu-id="91501-127">`0x20` -非受控被呼叫端。</span><span class="sxs-lookup"><span data-stu-id="91501-127">`0x20` - Unmanaged callee.</span></span><br /><br /> <span data-ttu-id="91501-128">`0x40` -結構封送處理</span><span class="sxs-lookup"><span data-stu-id="91501-128">`0x40` - Struct Marshal</span></span>|
|`ManagedInteropMethodToken`|`win:UInt32`|<span data-ttu-id="91501-129">Managed interop 方法的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="91501-129">The token for the managed interop method.</span></span>|
|`ManagedInteropMethodNameSpace`|`win:UnicodeString`|<span data-ttu-id="91501-130">Managed interop 方法的命名空間和封入類型。</span><span class="sxs-lookup"><span data-stu-id="91501-130">The namespace and enclosing type of the managed interop method.</span></span>|
|`ManagedInteropMethodName`|`win:UnicodeString`|<span data-ttu-id="91501-131">Managed interop 方法的名稱。</span><span class="sxs-lookup"><span data-stu-id="91501-131">The name of the managed interop method.</span></span>|
|`ManagedInteropMethodSignature`|`win:UnicodeString`|<span data-ttu-id="91501-132">Managed interop 方法的簽章。</span><span class="sxs-lookup"><span data-stu-id="91501-132">The signature of the managed interop method.</span></span>|
|`NativeMethodSignature`|`win:UnicodeString`|<span data-ttu-id="91501-133">原生方法簽章。</span><span class="sxs-lookup"><span data-stu-id="91501-133">The native method signature.</span></span>|
|`StubMethodSignature`|`win:UnicodeString`|<span data-ttu-id="91501-134">虛設常式方法簽章。</span><span class="sxs-lookup"><span data-stu-id="91501-134">The stub method signature.</span></span>|
|`StubMethodILCode`|`win:UnicodeString`|<span data-ttu-id="91501-135">存根方法的一般中繼語言 (CIL) 程式碼。</span><span class="sxs-lookup"><span data-stu-id="91501-135">The Common Intermediate Language (CIL) code for the stub method.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="91501-136">CLR 或 CoreCLR 執行個體的唯一 ID。</span><span class="sxs-lookup"><span data-stu-id="91501-136">Unique ID for the instance of CLR or CoreCLR.</span></span>|