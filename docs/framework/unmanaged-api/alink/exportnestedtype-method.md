---
title: ExportNestedType 方法
ms.date: 03/30/2017
api_name:
- IALink.ExportNestedType
- ExportNestedType
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- ExportNestedType
helpviewer_keywords:
- ExportNestedType method
ms.assetid: dec7df60-4d30-47c8-99db-72e0419e5f76
topic_type:
- apiref
ms.openlocfilehash: 69c99e2facfcb9077c3fc4131186ba3882c7cef6
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95684833"
---
# <a name="exportnestedtype-method"></a><span data-ttu-id="73a6a-102">ExportNestedType 方法</span><span class="sxs-lookup"><span data-stu-id="73a6a-102">ExportNestedType Method</span></span>

<span data-ttu-id="73a6a-103">將巢狀型別指定為可匯出。</span><span class="sxs-lookup"><span data-stu-id="73a6a-103">Specifies nested types as exportable.</span></span> <span data-ttu-id="73a6a-104">[ExportType 方法](exporttype-method.md)也可以匯出巢狀型別，但這個方法更快。</span><span class="sxs-lookup"><span data-stu-id="73a6a-104">The [ExportType Method](exporttype-method.md) can also export nested types, but this method is faster.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="73a6a-105">語法</span><span class="sxs-lookup"><span data-stu-id="73a6a-105">Syntax</span></span>  
  
```cpp  
HRESULT ExportNestedType(  
    mdAssembly      AssemblyID,  
    mdToken         FileToken,  
    mdTypeDef       TypeToken,  
    mdExportedType  ParentType,  
    LPCWSTR         pszTypename,  
    DWORD           dwFlags,  
    mdExportedType* pType  
) PURE;
```  
  
## <a name="parameters"></a><span data-ttu-id="73a6a-106">參數</span><span class="sxs-lookup"><span data-stu-id="73a6a-106">Parameters</span></span>  

 `AssemblyID`  
 <span data-ttu-id="73a6a-107">要從中匯出之元件的識別碼。</span><span class="sxs-lookup"><span data-stu-id="73a6a-107">ID of assembly to export from.</span></span>  
  
 `FileToken`  
 <span data-ttu-id="73a6a-108">檔案的檔案 token 或元件，其定義要成為可匯出的型別。</span><span class="sxs-lookup"><span data-stu-id="73a6a-108">File token or Assembly of file that defines the type to be made exportable.</span></span>  
  
 `TypeToken`  
 <span data-ttu-id="73a6a-109">要成為可匯出的型別權杖型別。</span><span class="sxs-lookup"><span data-stu-id="73a6a-109">Type token of type to be made exportable.</span></span>  
  
 `ParentType`  
 <span data-ttu-id="73a6a-110">父類型的標記。</span><span class="sxs-lookup"><span data-stu-id="73a6a-110">Token of parent type.</span></span>  
  
 `pszTypename`  
 <span data-ttu-id="73a6a-111">要匯出的完整型別名稱。</span><span class="sxs-lookup"><span data-stu-id="73a6a-111">Fully qualified type name to export.</span></span>  
  
 `dwFlags`  
 <span data-ttu-id="73a6a-112">`ComType` 旗標，例如 `tdPublic` 或 `tdNested` 。</span><span class="sxs-lookup"><span data-stu-id="73a6a-112">`ComType` flags such as `tdPublic` or `tdNested`.</span></span> <span data-ttu-id="73a6a-113">這個值可以傳遞給 [DefineExportedType 方法](../metadata/imetadataassemblyemit-defineexportedtype-method.md)。</span><span class="sxs-lookup"><span data-stu-id="73a6a-113">This value may be passed to [DefineExportedType Method](../metadata/imetadataassemblyemit-defineexportedtype-method.md).</span></span>  
  
 `pType`  
 <span data-ttu-id="73a6a-114">接收匯出類型的權杖。</span><span class="sxs-lookup"><span data-stu-id="73a6a-114">Receives token for exported type.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="73a6a-115">傳回值</span><span class="sxs-lookup"><span data-stu-id="73a6a-115">Return Value</span></span>  

 <span data-ttu-id="73a6a-116">如果方法成功，則傳回 S_OK。</span><span class="sxs-lookup"><span data-stu-id="73a6a-116">Returns S_OK if the method succeeds.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="73a6a-117">需求</span><span class="sxs-lookup"><span data-stu-id="73a6a-117">Requirements</span></span>  

 <span data-ttu-id="73a6a-118">需要 alink。h</span><span class="sxs-lookup"><span data-stu-id="73a6a-118">Requires alink.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="73a6a-119">另請參閱</span><span class="sxs-lookup"><span data-stu-id="73a6a-119">See also</span></span>

- [<span data-ttu-id="73a6a-120">IALink 介面</span><span class="sxs-lookup"><span data-stu-id="73a6a-120">IALink Interface</span></span>](ialink-interface.md)
- [<span data-ttu-id="73a6a-121">IALink2 介面</span><span class="sxs-lookup"><span data-stu-id="73a6a-121">IALink2 Interface</span></span>](ialink2-interface.md)
- [<span data-ttu-id="73a6a-122">ALink API</span><span class="sxs-lookup"><span data-stu-id="73a6a-122">ALink API</span></span>](index.md)
