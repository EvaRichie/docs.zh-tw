---
title: ICorDebugSymbolProvider 介面
ms.date: 03/30/2017
ms.assetid: 85b24196-b6c6-4bda-9de3-47180bd6ff96
ms.openlocfilehash: ff1f39be3d3db43f70cfa4a0711a3f42c180bc1a
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95672080"
---
# <a name="icordebugsymbolprovider-interface"></a><span data-ttu-id="3e7a4-102">ICorDebugSymbolProvider 介面</span><span class="sxs-lookup"><span data-stu-id="3e7a4-102">ICorDebugSymbolProvider Interface</span></span>

<span data-ttu-id="3e7a4-103">提供可用來擷取偵錯符號資訊的方法。</span><span class="sxs-lookup"><span data-stu-id="3e7a4-103">Provides methods that can be used to retrieve debug symbol information.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="3e7a4-104">方法</span><span class="sxs-lookup"><span data-stu-id="3e7a4-104">Methods</span></span>  
  
|<span data-ttu-id="3e7a4-105">方法</span><span class="sxs-lookup"><span data-stu-id="3e7a4-105">Method</span></span>|<span data-ttu-id="3e7a4-106">描述</span><span class="sxs-lookup"><span data-stu-id="3e7a4-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="3e7a4-107">GetAssemblyImageBytes 方法</span><span class="sxs-lookup"><span data-stu-id="3e7a4-107">GetAssemblyImageBytes Method</span></span>](icordebugsymbolprovider-getassemblyimagebytes-method.md)|<span data-ttu-id="3e7a4-108">如果合併組件中有相對虛擬位址 (RVA)，則會從合併組件讀取資料。</span><span class="sxs-lookup"><span data-stu-id="3e7a4-108">Reads data from a merged assembly given a relative virtual address (RVA) in the merged assembly.</span></span>|  
|[<span data-ttu-id="3e7a4-109">GetAssemblyImageMetadata 方法</span><span class="sxs-lookup"><span data-stu-id="3e7a4-109">GetAssemblyImageMetadata Method</span></span>](icordebugsymbolprovider-getassemblyimagemetadata-method.md)|<span data-ttu-id="3e7a4-110">從合併組件傳回中繼資料。</span><span class="sxs-lookup"><span data-stu-id="3e7a4-110">Returns the metadata from a merged assembly.</span></span>|  
|[<span data-ttu-id="3e7a4-111">GetCodeRange 方法</span><span class="sxs-lookup"><span data-stu-id="3e7a4-111">GetCodeRange Method</span></span>](icordebugsymbolprovider-getcoderange-method.md)|<span data-ttu-id="3e7a4-112">提供方法中的相對虛擬位址 (RVA)，以取得方法起始位址和大小。</span><span class="sxs-lookup"><span data-stu-id="3e7a4-112">Gets the method start address and size given a relative virtual address (RVA) in a method.</span></span>|  
|[<span data-ttu-id="3e7a4-113">GetInstanceFieldSymbols 方法</span><span class="sxs-lookup"><span data-stu-id="3e7a4-113">GetInstanceFieldSymbols Method</span></span>](icordebugsymbolprovider-getinstancefieldsymbols-method.md)|<span data-ttu-id="3e7a4-114">取得對應 TypeSpec 簽章的執行個體欄位符號。</span><span class="sxs-lookup"><span data-stu-id="3e7a4-114">Gets the instance field symbols that correspond to a typespec signature.</span></span>|  
|[<span data-ttu-id="3e7a4-115">GetMergedAssemblyRecords 方法</span><span class="sxs-lookup"><span data-stu-id="3e7a4-115">GetMergedAssemblyRecords Method</span></span>](icordebugsymbolprovider-getmergedassemblyrecords-method.md)|<span data-ttu-id="3e7a4-116">取得所有合併組件的符號記錄。</span><span class="sxs-lookup"><span data-stu-id="3e7a4-116">Gets the symbol records for all the merged assemblies.</span></span>|  
|[<span data-ttu-id="3e7a4-117">GetMethodLocalSymbols 方法</span><span class="sxs-lookup"><span data-stu-id="3e7a4-117">GetMethodLocalSymbols Method</span></span>](icordebugsymbolprovider-getmethodlocalsymbols-method.md)|<span data-ttu-id="3e7a4-118">提供方法的相對虛擬位址 (RVA)，取得該方法的本機符號。</span><span class="sxs-lookup"><span data-stu-id="3e7a4-118">Gets a method's local symbols given the relative virtual address (RVA) of that method.</span></span>|  
|[<span data-ttu-id="3e7a4-119">GetMethodParameterSymbols 方法</span><span class="sxs-lookup"><span data-stu-id="3e7a4-119">GetMethodParameterSymbols Method</span></span>](icordebugsymbolprovider-getmethodparametersymbols-method.md)|<span data-ttu-id="3e7a4-120">提供方法的相對虛擬位址 (RVA)，取得該方法的參數符號。</span><span class="sxs-lookup"><span data-stu-id="3e7a4-120">Gets a method's parameter symbols given the relative virtual address (RVA) of that method.</span></span>|  
|[<span data-ttu-id="3e7a4-121">GetMethodProps 方法</span><span class="sxs-lookup"><span data-stu-id="3e7a4-121">GetMethodProps Method</span></span>](icordebugsymbolprovider-getmethodprops-method.md)|<span data-ttu-id="3e7a4-122">傳回方法屬性的相關資訊，例如方法的中繼資料語彙基元，以及其泛型參數的相關資訊 (假設該方法中有相對虛擬位址 (RVA))。</span><span class="sxs-lookup"><span data-stu-id="3e7a4-122">Returns information about method properties, such as the method's metadata token and information about its generic parameters, given a relative virtual address (RVA) in that method.</span></span>|  
|[<span data-ttu-id="3e7a4-123">GetObjectSize 方法</span><span class="sxs-lookup"><span data-stu-id="3e7a4-123">GetObjectSize Method</span></span>](icordebugsymbolprovider-getobjectsize-method.md)|<span data-ttu-id="3e7a4-124">傳回根據某物件之 typespec 簽章的該物件大小。</span><span class="sxs-lookup"><span data-stu-id="3e7a4-124">Returns the object size for an object based on its typespec signature.</span></span>|  
|[<span data-ttu-id="3e7a4-125">GetStaticFieldSymbols 方法</span><span class="sxs-lookup"><span data-stu-id="3e7a4-125">GetStaticFieldSymbols Method</span></span>](icordebugsymbolprovider-getstaticfieldsymbols-method.md)|<span data-ttu-id="3e7a4-126">取得對應至 TypeSpec 簽章的靜態欄位符號。</span><span class="sxs-lookup"><span data-stu-id="3e7a4-126">Gets the static field symbols that correspond to a typespec signature.</span></span>|  
|[<span data-ttu-id="3e7a4-127">GetTypeProps 方法</span><span class="sxs-lookup"><span data-stu-id="3e7a4-127">GetTypeProps Method</span></span>](icordebugsymbolprovider-gettypeprops-method.md)|<span data-ttu-id="3e7a4-128">根據 vtable 中指定的相對虛擬位址 (RVA)，傳回類型之屬性的相關資訊，例如其泛型參數的簽章數目。</span><span class="sxs-lookup"><span data-stu-id="3e7a4-128">Returns information about a type's properties, such as the number of signature of its generic parameters, given a relative virtual address (RVA) in a vtable.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="3e7a4-129">備註</span><span class="sxs-lookup"><span data-stu-id="3e7a4-129">Remarks</span></span>  
  
> [!NOTE]
> <span data-ttu-id="3e7a4-130">這個介面僅適用於 .NET 原生。</span><span class="sxs-lookup"><span data-stu-id="3e7a4-130">This interface is available with .NET Native only.</span></span> <span data-ttu-id="3e7a4-131">如果您在 .NET 原生之外針對 ICorDebug 案例實作這個介面，Common Language Runtime 會忽略這個介面。</span><span class="sxs-lookup"><span data-stu-id="3e7a4-131">If you implement this interface for ICorDebug scenarios outside of .NET Native, the common language runtime will ignore this interface.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="3e7a4-132">需求</span><span class="sxs-lookup"><span data-stu-id="3e7a4-132">Requirements</span></span>  

 <span data-ttu-id="3e7a4-133">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="3e7a4-133">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="3e7a4-134">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="3e7a4-134">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="3e7a4-135">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="3e7a4-135">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="3e7a4-136">**.NET Framework 版本：**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span><span class="sxs-lookup"><span data-stu-id="3e7a4-136">**.NET Framework Versions:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3e7a4-137">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3e7a4-137">See also</span></span>

- [<span data-ttu-id="3e7a4-138">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="3e7a4-138">Debugging Interfaces</span></span>](debugging-interfaces.md)
- [<span data-ttu-id="3e7a4-139">偵錯</span><span class="sxs-lookup"><span data-stu-id="3e7a4-139">Debugging</span></span>](index.md)
