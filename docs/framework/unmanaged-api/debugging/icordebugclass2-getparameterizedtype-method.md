---
title: ICorDebugClass2::GetParameterizedType 方法
ms.date: 03/30/2017
api_name:
- ICorDebugClass2.GetParameterizedType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugClass2::GetParameterizedType
helpviewer_keywords:
- GetParameterizedType method [.NET Framework debugging]
- ICorDebugClass2::GetParameterizedType method [.NET Framework debugging]
ms.assetid: 94b591c4-9302-4af2-a510-089496afb036
topic_type:
- apiref
ms.openlocfilehash: 139181975d16c2cdacec10ed646cfc2b8fb31a20
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95717990"
---
# <a name="icordebugclass2getparameterizedtype-method"></a><span data-ttu-id="e051f-102">ICorDebugClass2::GetParameterizedType 方法</span><span class="sxs-lookup"><span data-stu-id="e051f-102">ICorDebugClass2::GetParameterizedType Method</span></span>

<span data-ttu-id="e051f-103">取得這個類別的類型宣告。</span><span class="sxs-lookup"><span data-stu-id="e051f-103">Gets the type declaration for this class.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="e051f-104">語法</span><span class="sxs-lookup"><span data-stu-id="e051f-104">Syntax</span></span>  
  
```cpp  
HRESULT GetParameterizedType (  
    [in] CorElementType                      elementType,  
    [in] ULONG32                             nTypeArgs,  
    [in, size_is(nTypeArgs)] ICorDebugType  *ppTypeArgs[],  
    [out] ICorDebugType                    **ppType  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="e051f-105">參數</span><span class="sxs-lookup"><span data-stu-id="e051f-105">Parameters</span></span>  

 `elementType`  
 <span data-ttu-id="e051f-106">在CorElementType 列舉的值，指定這個類別的元素類型：如果這個 ICorDebugClass2 代表實值型別，請將此值設定為 ELEMENT_TYPE_VALUETYPE。</span><span class="sxs-lookup"><span data-stu-id="e051f-106">[in] A value of the CorElementType enumeration that specifies the element type for this class: Set this value to ELEMENT_TYPE_VALUETYPE if this ICorDebugClass2 represents a value type.</span></span> <span data-ttu-id="e051f-107">如果這代表複雜型別，請將此值設定為 ELEMENT_TYPE_CLASS `ICorDebugClass2` 。</span><span class="sxs-lookup"><span data-stu-id="e051f-107">Set this value to ELEMENT_TYPE_CLASS if this `ICorDebugClass2` represents a complex type.</span></span>  
  
 `nTypeArgs`  
 <span data-ttu-id="e051f-108">在如果類型為泛型，則為型別參數的數目。</span><span class="sxs-lookup"><span data-stu-id="e051f-108">[in] The number of type parameters, if the type is generic.</span></span> <span data-ttu-id="e051f-109">如果任何) 必須符合類別所需的數目，則 (類型參數的數目。</span><span class="sxs-lookup"><span data-stu-id="e051f-109">The number of type parameters (if any) must match the number required by the class.</span></span>  
  
 `ppTypeArgs`  
 <span data-ttu-id="e051f-110">在指標的陣列，每個指標都會指向代表型別參數的 ICorDebugType 物件。</span><span class="sxs-lookup"><span data-stu-id="e051f-110">[in] An array of pointers, each of which points to an ICorDebugType object that represents a type parameter.</span></span> <span data-ttu-id="e051f-111">如果類別為非泛型，則這個值為 null。</span><span class="sxs-lookup"><span data-stu-id="e051f-111">If the class is non-generic, this value is null.</span></span>  
  
 `ppType`  
 <span data-ttu-id="e051f-112">擴展代表類型宣告之物件的位址指標 `ICorDebugType` 。</span><span class="sxs-lookup"><span data-stu-id="e051f-112">[out] A pointer to the address of an `ICorDebugType` object that represents the type declaration.</span></span> <span data-ttu-id="e051f-113">此物件相當於 managed 程式 <xref:System.Type> 代碼中的物件。</span><span class="sxs-lookup"><span data-stu-id="e051f-113">This object is equivalent to a <xref:System.Type> object in managed code.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="e051f-114">備註</span><span class="sxs-lookup"><span data-stu-id="e051f-114">Remarks</span></span>  

 <span data-ttu-id="e051f-115">如果類別為非泛型，亦即，如果沒有型別參數，則只會 `GetParameterizedType` 取得對應至類別的執行時間型別物件。</span><span class="sxs-lookup"><span data-stu-id="e051f-115">If the class is non-generic, that is, if it has no type parameters, `GetParameterizedType` simply gets the runtime type object corresponding to the class.</span></span> <span data-ttu-id="e051f-116">`elementType`如果類別是實值型別，則應該將參數設定為正確的元素類型：如果類別是實值型別，則為 ELEMENT_TYPE_VALUETYPE，否則為 ELEMENT_TYPE_CLASS。</span><span class="sxs-lookup"><span data-stu-id="e051f-116">The `elementType` parameter should be set to the correct element type for the class: ELEMENT_TYPE_VALUETYPE if the class is a value type; otherwise, ELEMENT_TYPE_CLASS.</span></span>  
  
 <span data-ttu-id="e051f-117">如果類別接受型別參數 (例如 `ArrayList<T>`) ，您可以使用來為具現化的型別（例如） `GetParameterizedType` 建立型別物件 `ArrayList<int>` 。</span><span class="sxs-lookup"><span data-stu-id="e051f-117">If the class accepts type parameters (for example, `ArrayList<T>`), you can use `GetParameterizedType` to construct a type object for an instantiated type such as `ArrayList<int>`.</span></span>  
  
## <a name="background-information"></a><span data-ttu-id="e051f-118">背景資訊</span><span class="sxs-lookup"><span data-stu-id="e051f-118">Background Information</span></span>  

 <span data-ttu-id="e051f-119">在 .NET Framework 1.0 和1.1 版中，中繼資料中的每個型別都可以直接對應至執行中進程中的型別。</span><span class="sxs-lookup"><span data-stu-id="e051f-119">In the .NET Framework versions 1.0 and 1.1, every type in the metadata could be directly mapped to a type in the running process.</span></span> <span data-ttu-id="e051f-120">因此，元資料類型和執行時間類型在執行中的進程中具有單一標記法。</span><span class="sxs-lookup"><span data-stu-id="e051f-120">Thus, a metadata type and a runtime type had a single representation in the running process.</span></span> <span data-ttu-id="e051f-121">不過，中繼資料中的一個泛型型別可以對應至執行中進程中類型的許多不同具現化。</span><span class="sxs-lookup"><span data-stu-id="e051f-121">However, one generic type in metadata can be mapped to many different instantiations of the type in the running process.</span></span> <span data-ttu-id="e051f-122">例如，元資料類型 `SortedList<K,V>` 可以對應至 `SortedList<String, EmployeeRecord>` 、 `SortedList<Int32, String>` 、 `SortedList<String,Array<Int32>>` 等等。</span><span class="sxs-lookup"><span data-stu-id="e051f-122">For example, the metadata type `SortedList<K,V>` can map to `SortedList<String, EmployeeRecord>`, `SortedList<Int32, String>`, `SortedList<String,Array<Int32>>`, and so on.</span></span> <span data-ttu-id="e051f-123">因此，您需要一種方法來處理型別具現化。</span><span class="sxs-lookup"><span data-stu-id="e051f-123">Thus, you need a way to handle type instantiation.</span></span>  
  
 <span data-ttu-id="e051f-124">.NET Framework 2.0 版引進了 `ICorDebugType` 介面。</span><span class="sxs-lookup"><span data-stu-id="e051f-124">The .NET Framework version 2.0 introduces the `ICorDebugType` interface.</span></span> <span data-ttu-id="e051f-125">若為泛型型別， `ICorDebugClass` 或物件代表未具現 `ICorDebugClass2` 化的類型 (`SortedList<K,V>`) ， `ICorDebugType` 而物件代表各種具現化的類型。</span><span class="sxs-lookup"><span data-stu-id="e051f-125">For a generic type, an `ICorDebugClass` or `ICorDebugClass2` object represents the uninstantiated type (`SortedList<K,V>`), and an `ICorDebugType` object represents the various instantiated types.</span></span> <span data-ttu-id="e051f-126">指定 `ICorDebugClass` 或 `ICorDebugClass2` 物件之後，您可以藉 `ICorDebugType` 由呼叫方法，為任何具現化建立物件 `ICorDebugClass2::GetParameterizedType` 。</span><span class="sxs-lookup"><span data-stu-id="e051f-126">Given an `ICorDebugClass` or `ICorDebugClass2` object, you can create an `ICorDebugType` object for any instantiation by calling the `ICorDebugClass2::GetParameterizedType` method.</span></span> <span data-ttu-id="e051f-127">您也可以建立 `ICorDebugType` 簡單類型的物件，例如 Int32 或非泛型型別的物件。</span><span class="sxs-lookup"><span data-stu-id="e051f-127">You can also create an `ICorDebugType` object for a simple type, such as Int32, or for a non-generic type.</span></span>  
  
 <span data-ttu-id="e051f-128">引入 `ICorDebugType` 物件來代表類型的執行時間概念，在整個 API 中都有 ripple 效果。</span><span class="sxs-lookup"><span data-stu-id="e051f-128">The introduction of the `ICorDebugType` object to represent the run-time notion of a type has a ripple effect throughout the API.</span></span> <span data-ttu-id="e051f-129">先前 `ICorDebugClass` `ICorDebugClass2` 採用或物件或甚至是值的函式 `CorElementType` 會一般化以取得 `ICorDebugType` 物件。</span><span class="sxs-lookup"><span data-stu-id="e051f-129">Functions that previously took an `ICorDebugClass` or `ICorDebugClass2` object or even a `CorElementType` value are generalized to take an `ICorDebugType` object.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="e051f-130">需求</span><span class="sxs-lookup"><span data-stu-id="e051f-130">Requirements</span></span>  

 <span data-ttu-id="e051f-131">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="e051f-131">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="e051f-132">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="e051f-132">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="e051f-133">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="e051f-133">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="e051f-134">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="e051f-134">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>
