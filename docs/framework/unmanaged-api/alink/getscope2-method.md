---
title: GetScope2 方法
ms.date: 03/30/2017
api_name:
- IALink2.GetScope2
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- GetScope2
helpviewer_keywords:
- GetScope2 method
ms.assetid: 49435665-6f5a-4acd-9034-8c9244a04a63
topic_type:
- apiref
ms.openlocfilehash: e8c6fd7dca13afe7504e447caca9a217c8136c27
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95684521"
---
# <a name="getscope2-method"></a><span data-ttu-id="d63b3-102">GetScope2 方法</span><span class="sxs-lookup"><span data-stu-id="d63b3-102">GetScope2 Method</span></span>

<span data-ttu-id="d63b3-103">取得匯入範圍。</span><span class="sxs-lookup"><span data-stu-id="d63b3-103">Gets an import scope.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="d63b3-104">語法</span><span class="sxs-lookup"><span data-stu-id="d63b3-104">Syntax</span></span>  
  
```cpp  
HRESULT GetScope2(  
    mdAssembly AssemblyID,  
    mdToken FileToken,  
    DWORD dwScope,  
    IMetaDataImport2** ppImportScope  
) PURE;
```  
  
## <a name="parameters"></a><span data-ttu-id="d63b3-105">參數</span><span class="sxs-lookup"><span data-stu-id="d63b3-105">Parameters</span></span>  

 `AssemblyID`  
 <span data-ttu-id="d63b3-106">目標群組件的識別碼。</span><span class="sxs-lookup"><span data-stu-id="d63b3-106">ID of target assembly.</span></span>  
  
 `FileToken`  
 <span data-ttu-id="d63b3-107">要匯入之檔案的識別碼。</span><span class="sxs-lookup"><span data-stu-id="d63b3-107">ID of file from which to import.</span></span>  
  
 `dwScope`  
 <span data-ttu-id="d63b3-108">要匯入之以零為基底的範圍。</span><span class="sxs-lookup"><span data-stu-id="d63b3-108">Zero-based scope to import.</span></span>  
  
 `ppImportScope`  
 <span data-ttu-id="d63b3-109">接收指定範圍的 [IMetaDataImport2 介面](../metadata/imetadataimport2-interface.md) 介面指標。</span><span class="sxs-lookup"><span data-stu-id="d63b3-109">Receives pointer to [IMetaDataImport2 Interface](../metadata/imetadataimport2-interface.md) interface for indicated scope.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="d63b3-110">傳回值</span><span class="sxs-lookup"><span data-stu-id="d63b3-110">Return Value</span></span>  

 <span data-ttu-id="d63b3-111">如果方法成功，則傳回 S_OK。</span><span class="sxs-lookup"><span data-stu-id="d63b3-111">Returns S_OK if the method succeeds.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="d63b3-112">需求</span><span class="sxs-lookup"><span data-stu-id="d63b3-112">Requirements</span></span>  

 <span data-ttu-id="d63b3-113">需要 alink. h。</span><span class="sxs-lookup"><span data-stu-id="d63b3-113">Requires alink.h.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d63b3-114">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d63b3-114">See also</span></span>

- [<span data-ttu-id="d63b3-115">IALink2 介面</span><span class="sxs-lookup"><span data-stu-id="d63b3-115">IALink2 Interface</span></span>](ialink2-interface.md)
- [<span data-ttu-id="d63b3-116">IALink 介面</span><span class="sxs-lookup"><span data-stu-id="d63b3-116">IALink Interface</span></span>](ialink-interface.md)
- [<span data-ttu-id="d63b3-117">ALink API</span><span class="sxs-lookup"><span data-stu-id="d63b3-117">ALink API</span></span>](index.md)
