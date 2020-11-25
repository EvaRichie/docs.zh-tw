---
title: CorDebugRegister 列舉
ms.date: 03/30/2017
api_name:
- CorDebugRegister
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugRegister
helpviewer_keywords:
- CorDebugRegister enumeration [.NET Framework debugging]
ms.assetid: 003bb138-7960-4291-ac88-0d87e470ff70
topic_type:
- apiref
ms.openlocfilehash: 85df98e83396c9439c28dd41a3ffa02b820c9c3e
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95726050"
---
# <a name="cordebugregister-enumeration"></a><span data-ttu-id="3879b-102">CorDebugRegister 列舉</span><span class="sxs-lookup"><span data-stu-id="3879b-102">CorDebugRegister Enumeration</span></span>

<span data-ttu-id="3879b-103">指定與給定處理器架構相關聯的暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-103">Specifies the registers associated with a given processor architecture.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="3879b-104">語法</span><span class="sxs-lookup"><span data-stu-id="3879b-104">Syntax</span></span>  
  
```cpp  
typedef enum CorDebugRegister {  
  
    REGISTER_INSTRUCTION_POINTER = 0,  
    REGISTER_STACK_POINTER,  
    REGISTER_FRAME_POINTER,  
  
    REGISTER_X86_EIP = 0,  
    REGISTER_X86_ESP,  
    REGISTER_X86_EBP,  
  
    REGISTER_X86_EAX,  
    REGISTER_X86_ECX,  
    REGISTER_X86_EDX,  
    REGISTER_X86_EBX,  
  
    REGISTER_X86_ESI,  
    REGISTER_X86_EDI,  
  
    REGISTER_X86_FPSTACK_0,  
    REGISTER_X86_FPSTACK_1,  
    REGISTER_X86_FPSTACK_2,  
    REGISTER_X86_FPSTACK_3,  
    REGISTER_X86_FPSTACK_4,  
    REGISTER_X86_FPSTACK_5,  
    REGISTER_X86_FPSTACK_6,  
    REGISTER_X86_FPSTACK_7,  
  
    REGISTER_AMD64_RIP = 0,  
    REGISTER_AMD64_RSP,  
    REGISTER_AMD64_RBP,  
    REGISTER_AMD64_RAX,  
    REGISTER_AMD64_RCX,  
    REGISTER_AMD64_RDX,  
    REGISTER_AMD64_RBX,  
    REGISTER_AMD64_RSI,  
    REGISTER_AMD64_RDI,  
    REGISTER_AMD64_R8,  
    REGISTER_AMD64_R9,  
    REGISTER_AMD64_R10,  
    REGISTER_AMD64_R11,  
    REGISTER_AMD64_R12,  
    REGISTER_AMD64_R13,  
    REGISTER_AMD64_R14,  
    REGISTER_AMD64_R15,  
  
    REGISTER_AMD64_XMM0,  
    REGISTER_AMD64_XMM1,  
    REGISTER_AMD64_XMM2,  
    REGISTER_AMD64_XMM3,  
    REGISTER_AMD64_XMM4,  
    REGISTER_AMD64_XMM5,  
    REGISTER_AMD64_XMM6,  
    REGISTER_AMD64_XMM7,  
    REGISTER_AMD64_XMM8,  
    REGISTER_AMD64_XMM9,  
    REGISTER_AMD64_XMM10,  
    REGISTER_AMD64_XMM11,  
    REGISTER_AMD64_XMM12,  
    REGISTER_AMD64_XMM13,  
    REGISTER_AMD64_XMM14,  
    REGISTER_AMD64_XMM15,  
  
    REGISTER_IA64_BSP = REGISTER_FRAME_POINTER,  
    REGISTER_IA64_R0  = REGISTER_IA64_BSP + 1,  
    REGISTER_IA64_F0  = REGISTER_IA64_R0  + 128,  
    REGISTER_ARM_PC = 0,  
    REGISTER_ARM_SP,  
    REGISTER_ARM_R0,  
    REGISTER_ARM_R1,  
    REGISTER_ARM_R2,  
    REGISTER_ARM_R3,  
    REGISTER_ARM_R4,  
    REGISTER_ARM_R5,  
    REGISTER_ARM_R6,  
    REGISTER_ARM_R7,  
    REGISTER_ARM_R8,  
    REGISTER_ARM_R9,  
    REGISTER_ARM_R10,  
    REGISTER_ARM_R11,  
    REGISTER_ARM_R12,  
    REGISTER_ARM_LR,  
  
} CorDebugRegister;  
```  
  
## <a name="members"></a><span data-ttu-id="3879b-105">成員</span><span class="sxs-lookup"><span data-stu-id="3879b-105">Members</span></span>  
  
|<span data-ttu-id="3879b-106">member</span><span class="sxs-lookup"><span data-stu-id="3879b-106">Member</span></span>|<span data-ttu-id="3879b-107">描述</span><span class="sxs-lookup"><span data-stu-id="3879b-107">Description</span></span>|  
|------------|-----------------|  
|`REGISTER_INSTRUCTION_POINTER`|<span data-ttu-id="3879b-108">處理器上的指令指標暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-108">An instruction pointer register on any processor.</span></span>|  
|`REGISTER_STACK_POINTER`|<span data-ttu-id="3879b-109">處理器上的堆疊指標暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-109">A stack pointer register on any processor.</span></span>|  
|`REGISTER_FRAME_POINTER`|<span data-ttu-id="3879b-110">處理器上的框架指標暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-110">A frame pointer register on any processor.</span></span>|  
|`REGISTER_X86_EIP`|<span data-ttu-id="3879b-111">x86 處理器上的指令指標暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-111">The instruction pointer register on the x86 processor.</span></span>|  
|`REGISTER_X86_ESP`|<span data-ttu-id="3879b-112">x86 處理器上的堆疊指標暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-112">The stack pointer register on the x86 processor.</span></span>|  
|`REGISTER_X86_EBP`|<span data-ttu-id="3879b-113">x86 處理器上的基底指標暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-113">The base pointer register on the x86 processor.</span></span>|  
|`REGISTER_X86_EAX`|<span data-ttu-id="3879b-114">x86 處理器上的 A 資料暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-114">The A data register on the x86 processor.</span></span>|  
|`REGISTER_X86_ECX`|<span data-ttu-id="3879b-115">x86 處理器上的 C 資料暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-115">The C data register on the x86 processor.</span></span>|  
|`REGISTER_X86_EDX`|<span data-ttu-id="3879b-116">x86 處理器上的 D 資料暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-116">The D data register on the x86 processor.</span></span>|  
|`REGISTER_X86_EBX`|<span data-ttu-id="3879b-117">x86 處理器上的 B 資料暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-117">The B data register on the x86 processor.</span></span>|  
|`REGISTER_X86_ESI`|<span data-ttu-id="3879b-118">x86 處理器上的來源索引暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-118">The source index register on the x86 processor.</span></span>|  
|`REGISTER_X86_EDI`|<span data-ttu-id="3879b-119">x86 處理器上的目的地索引暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-119">The destination index register on the x86 processor.</span></span>|  
|`REGISTER_X86_FPSTACK_0`|<span data-ttu-id="3879b-120">x86 浮點 (FP) 處理器上的堆疊暫存器 0。</span><span class="sxs-lookup"><span data-stu-id="3879b-120">The stack register 0 on the x86 floating-point (FP) processor.</span></span>|  
|`REGISTER_X86_FPSTACK_1`|<span data-ttu-id="3879b-121">x86 FP 處理器上的 #1 堆疊暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-121">The #1 stack register on the x86 FP processor.</span></span>|  
|`REGISTER_X86_FPSTACK_2`|<span data-ttu-id="3879b-122">x86 FP 處理器上的 #2 堆疊暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-122">The #2 stack register on the x86 FP processor.</span></span>|  
|`REGISTER_X86_FPSTACK_3`|<span data-ttu-id="3879b-123">x86 FP 處理器上的 #3 堆疊暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-123">The #3 stack register on the x86 FP processor.</span></span>|  
|`REGISTER_X86_FPSTACK_4`|<span data-ttu-id="3879b-124">x86 FP 處理器上的 #4 堆疊暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-124">The #4 stack register on the x86 FP processor.</span></span>|  
|`REGISTER_X86_FPSTACK_5`|<span data-ttu-id="3879b-125">x86 FP 處理器上的 #5 堆疊暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-125">The #5 stack register on the x86 FP processor.</span></span>|  
|`REGISTER_X86_FPSTACK_6`|<span data-ttu-id="3879b-126">x86 FP 處理器上的 #6 堆疊暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-126">The #6 stack register on the x86 FP processor.</span></span>|  
|`REGISTER_X86_FPSTACK_7`|<span data-ttu-id="3879b-127">x86 FP 處理器上的 #7 堆疊暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-127">The #7 stack register on the x86 FP processor.</span></span>|  
|`REGISTER_AMD64_RIP`|<span data-ttu-id="3879b-128">AMD64 處理器上的指令指標暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-128">The instruction pointer register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_RSP`|<span data-ttu-id="3879b-129">AMD64 處理器上的堆疊指標暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-129">The stack pointer register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_RBP`|<span data-ttu-id="3879b-130">AMD64 處理器上的基底指標暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-130">The base pointer register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_RAX`|<span data-ttu-id="3879b-131">AMD64 處理器上的 A 資料暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-131">The A data register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_RCX`|<span data-ttu-id="3879b-132">AMD64 處理器上的 C 資料暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-132">The C data register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_RDX`|<span data-ttu-id="3879b-133">AMD64 處理器上的 D 資料暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-133">The D data register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_RBX`|<span data-ttu-id="3879b-134">AMD64 處理器上的 B 資料暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-134">The B data register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_RSI`|<span data-ttu-id="3879b-135">AMD64 處理器上的來源索引暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-135">The source index register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_RDI`|<span data-ttu-id="3879b-136">AMD64 處理器上的目的地索引暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-136">The destination index register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_R8`|<span data-ttu-id="3879b-137">AMD64 處理器上的 #8 資料暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-137">The #8 data register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_R9`|<span data-ttu-id="3879b-138">AMD64 處理器上的 #9 資料暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-138">The #9 data register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_R10`|<span data-ttu-id="3879b-139">AMD64 處理器上的 #10 資料暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-139">The #10 data register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_R11`|<span data-ttu-id="3879b-140">AMD64 處理器上的 #11 資料暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-140">The #11 data register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_R12`|<span data-ttu-id="3879b-141">AMD64 處理器上的 #12 資料暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-141">The #12 data register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_R13`|<span data-ttu-id="3879b-142">AMD64 處理器上的 #13 資料暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-142">The #13 data register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_R14`|<span data-ttu-id="3879b-143">AMD64 處理器上的 #14 資料暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-143">The #14 data register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_R15`|<span data-ttu-id="3879b-144">AMD64 處理器上的 #15 資料暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-144">The #15 data register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_XMM0`|<span data-ttu-id="3879b-145">AMD64 處理器上的 #0 多媒體暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-145">The #0 multimedia register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_XMM1`|<span data-ttu-id="3879b-146">AMD64 處理器上的 #1 多媒體暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-146">The #1 multimedia register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_XMM2`|<span data-ttu-id="3879b-147">AMD64 處理器上的 #2 多媒體暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-147">The #2 multimedia register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_XMM3`|<span data-ttu-id="3879b-148">AMD64 處理器上的 #3 多媒體暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-148">The #3 multimedia register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_XMM4`|<span data-ttu-id="3879b-149">AMD64 處理器上的 #4 多媒體暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-149">The #4 multimedia register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_XMM5`|<span data-ttu-id="3879b-150">AMD64 處理器上的 #5 多媒體暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-150">The #5 multimedia register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_XMM6`|<span data-ttu-id="3879b-151">AMD64 處理器上的 #6 多媒體暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-151">The #6 multimedia register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_XMM7`|<span data-ttu-id="3879b-152">AMD64 處理器上的 #7 多媒體暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-152">The #7 multimedia register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_XMM8`|<span data-ttu-id="3879b-153">AMD64 處理器上的 #8 多媒體暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-153">The #8 multimedia register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_XMM9`|<span data-ttu-id="3879b-154">AMD64 處理器上的 #9 多媒體暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-154">The #9 multimedia register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_XMM10`|<span data-ttu-id="3879b-155">AMD64 處理器上的 #10 多媒體暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-155">The #10 multimedia register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_XMM11`|<span data-ttu-id="3879b-156">AMD64 處理器上的 #11 多媒體暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-156">The #11 multimedia register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_XMM12`|<span data-ttu-id="3879b-157">AMD64 處理器上的 #12 多媒體暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-157">The #12 multimedia register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_XMM13`|<span data-ttu-id="3879b-158">AMD64 處理器上的 #13 多媒體暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-158">The #13 multimedia register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_XMM14`|<span data-ttu-id="3879b-159">AMD64 處理器上的 #14 多媒體暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-159">The #14 multimedia register on the AMD64 processor.</span></span>|  
|`REGISTER_AMD64_XMM15`|<span data-ttu-id="3879b-160">AMD64 處理器上的 #15 多媒體暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-160">The #15 multimedia register on the AMD64 processor.</span></span>|  
|`REGISTER_IA64_BSP`|<span data-ttu-id="3879b-161">IA-64 處理器上的堆疊指標暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-161">The stack pointer register on the IA-64 processor.</span></span>|  
|`REGISTER_IA64_R0`|<span data-ttu-id="3879b-162">IA-64 處理器上的 #0 資料暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-162">The #0 data register on the IA-64 processor.</span></span>|  
|`REGISTER_IA64_F0`|<span data-ttu-id="3879b-163">IA-64 處理器上的 #0 FP 資料暫存器。</span><span class="sxs-lookup"><span data-stu-id="3879b-163">The #0 FP data register on the IA-64 processor.</span></span>|  
|`REGISTER_ARM_PC`|<span data-ttu-id="3879b-164">ARM 處理器上的程式計數器暫存器 (R15)。</span><span class="sxs-lookup"><span data-stu-id="3879b-164">The program counter register (R15) on the ARM processor.</span></span>|  
|`REGISTER_ARM_SP`|<span data-ttu-id="3879b-165">ARM 處理器上的堆疊指標暫存器 (R13)。</span><span class="sxs-lookup"><span data-stu-id="3879b-165">The stack pointer register (R13) on the ARM processor.</span></span>|  
|`REGISTER_ARM_R0`|<span data-ttu-id="3879b-166">ARM 處理器上的資料暫存器 R0。</span><span class="sxs-lookup"><span data-stu-id="3879b-166">Data register R0 on the ARM processor.</span></span>|  
|`REGISTER_ARM_R1`|<span data-ttu-id="3879b-167">ARM 處理器上的資料暫存器 R1。</span><span class="sxs-lookup"><span data-stu-id="3879b-167">Data register R1 on the ARM processor.</span></span>|  
|`REGISTER_ARM_R2`|<span data-ttu-id="3879b-168">ARM 處理器上的資料暫存器 R2。</span><span class="sxs-lookup"><span data-stu-id="3879b-168">Data register R2 on the ARM processor.</span></span>|  
|`REGISTER_ARM_R3`|<span data-ttu-id="3879b-169">ARM 處理器上的資料暫存器 R3。</span><span class="sxs-lookup"><span data-stu-id="3879b-169">Data register R3 on the ARM processor.</span></span>|  
|`REGISTER_ARM_R4`|<span data-ttu-id="3879b-170">ARM 處理器上的暫存器 R4。</span><span class="sxs-lookup"><span data-stu-id="3879b-170">Register R4 on the ARM processor.</span></span>|  
|`REGISTER_ARM_R5`|<span data-ttu-id="3879b-171">ARM 處理器上的暫存器 R5。</span><span class="sxs-lookup"><span data-stu-id="3879b-171">Register R5 on the ARM processor.</span></span>|  
|`REGISTER_ARM_R6`|<span data-ttu-id="3879b-172">ARM 處理器上的暫存器 R6。</span><span class="sxs-lookup"><span data-stu-id="3879b-172">Register R6 on the ARM processor.</span></span>|  
|`REGISTER_ARM_R7`|<span data-ttu-id="3879b-173">ARM 處理器上的暫存器 R7 (THUMB 框架指標)。</span><span class="sxs-lookup"><span data-stu-id="3879b-173">Register R7 (the THUMB frame pointer) on the ARM processor.</span></span>|  
|`REGISTER_ARM_R8`|<span data-ttu-id="3879b-174">ARM 處理器上的暫存器 R8。</span><span class="sxs-lookup"><span data-stu-id="3879b-174">Register R8 on the ARM processor.</span></span>|  
|`REGISTER_ARM_R9`|<span data-ttu-id="3879b-175">ARM 處理器上的暫存器 R9。</span><span class="sxs-lookup"><span data-stu-id="3879b-175">Register R9 on the ARM processor.</span></span>|  
|`REGISTER_ARM_R10`|<span data-ttu-id="3879b-176">ARM 處理器上的暫存器 R10。</span><span class="sxs-lookup"><span data-stu-id="3879b-176">Register R10 on the ARM processor.</span></span>|  
|`REGISTER_ARM_R11`|<span data-ttu-id="3879b-177">ARM 處理器上的框架指標。</span><span class="sxs-lookup"><span data-stu-id="3879b-177">The frame pointer on the ARM processor.</span></span>|  
|`REGISTER_ARM_R12`|<span data-ttu-id="3879b-178">ARM 處理器上的暫存器 R12。</span><span class="sxs-lookup"><span data-stu-id="3879b-178">Register R12 on the ARM processor.</span></span>|  
|`REGISTER_ARM_LR`|<span data-ttu-id="3879b-179">ARM 處理器上的連結暫存器 (R14)。</span><span class="sxs-lookup"><span data-stu-id="3879b-179">The link register (R14) on the ARM processor.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="3879b-180">備註</span><span class="sxs-lookup"><span data-stu-id="3879b-180">Remarks</span></span>  

 <span data-ttu-id="3879b-181">IA-64 處理器上共有 128 個一般用途的資料暫存器，以及 128 個浮點資料暫存器，但只會提供值 `REGISTER_IA64_R0` 與 `REGISTER_IA64_F0`。</span><span class="sxs-lookup"><span data-stu-id="3879b-181">There are 128 general-purpose data registers and 128 floating-point data registers on the IA-64 processor, but only values `REGISTER_IA64_R0` and `REGISTER_IA64_F0` are provided.</span></span> <span data-ttu-id="3879b-182">其他值可以透過下列方法指定：</span><span class="sxs-lookup"><span data-stu-id="3879b-182">The other values can be determined as follows:</span></span>  
  
- <span data-ttu-id="3879b-183">將值 `REGISTER_IA64_R0` 到 `REGISTER_IA64_R1` (對應到 IA-64 處理器上的資料暫存器 #1 到 #127) 的暫存器號碼加入 `REGISTER_IA64_R127`。</span><span class="sxs-lookup"><span data-stu-id="3879b-183">Add the register number to `REGISTER_IA64_R0` for values `REGISTER_IA64_R1` through `REGISTER_IA64_R127`, which correspond to the #1 data register through the #127 data register on the IA-64 processor.</span></span>  
  
- <span data-ttu-id="3879b-184">將值 `REGISTER_IA64_F0` 到 `REGISTER_IA64_F1` (對應到 IA-64 處理器上的資料暫存器 #1 FP 到 #127 FP) 的暫存器號碼加入 `REGISTER_IA64_F127`。</span><span class="sxs-lookup"><span data-stu-id="3879b-184">Add the register number to `REGISTER_IA64_F0` for values `REGISTER_IA64_F1` through `REGISTER_IA64_F127`, which correspond to the #1 FP data register through the #127 FP data register on the IA-64 processor.</span></span>  
  
 <span data-ttu-id="3879b-185">例如，若您需要指定 IA-64 處理器上的 #83 資料暫存器，可使用 `REGISTER_IA64_R0` + 83。</span><span class="sxs-lookup"><span data-stu-id="3879b-185">For example, if you need to specify the #83 data register on the IA-64 processor, use `REGISTER_IA64_R0` + 83.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="3879b-186">需求</span><span class="sxs-lookup"><span data-stu-id="3879b-186">Requirements</span></span>  

 <span data-ttu-id="3879b-187">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="3879b-187">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="3879b-188">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="3879b-188">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="3879b-189">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="3879b-189">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="3879b-190">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="3879b-190">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3879b-191">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3879b-191">See also</span></span>

- [<span data-ttu-id="3879b-192">偵錯列舉</span><span class="sxs-lookup"><span data-stu-id="3879b-192">Debugging Enumerations</span></span>](debugging-enumerations.md)
