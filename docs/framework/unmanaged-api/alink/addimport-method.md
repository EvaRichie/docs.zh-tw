---
title: AddImport 方法
ms.date: 03/30/2017
api_name:
- AddImport
- IALink.AddImport
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- AddImport
helpviewer_keywords:
- AddImport method
ms.assetid: 4fedf8a0-08c8-43d0-aa00-20f2a521c991
topic_type:
- apiref
ms.openlocfilehash: cf73ada36be66edb3fa267d61873ae9acb088a34
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95717041"
---
# <a name="addimport-method"></a><span data-ttu-id="8a3fc-102">AddImport 方法</span><span class="sxs-lookup"><span data-stu-id="8a3fc-102">AddImport Method</span></span>

<span data-ttu-id="8a3fc-103">將匯入新增至元件。</span><span class="sxs-lookup"><span data-stu-id="8a3fc-103">Adds imports to the assembly.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="8a3fc-104">語法</span><span class="sxs-lookup"><span data-stu-id="8a3fc-104">Syntax</span></span>  
  
```cpp  
HRESULT AddImport(  
    mdAssembly      AssemblyID,  
    mdToken         ImportToken,  
    DWORD           dwFlags,  
    mdFile*         pFileToken  
) PURE;  
```  
  
## <a name="parameters"></a><span data-ttu-id="8a3fc-105">參數</span><span class="sxs-lookup"><span data-stu-id="8a3fc-105">Parameters</span></span>  

 `AssemblyID`  
 <span data-ttu-id="8a3fc-106">要擴充之元件的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="8a3fc-106">Unique ID of assembly to be augmented.</span></span>  
  
 `ImportToken`  
 <span data-ttu-id="8a3fc-107">要匯入之檔案的唯一識別碼，取自 [ImportFile 方法](importfile-method.md)。</span><span class="sxs-lookup"><span data-stu-id="8a3fc-107">Unique ID, retrieved from [ImportFile Method](importfile-method.md), of file to be imported.</span></span>  
  
 `dwFlags`  
 <span data-ttu-id="8a3fc-108">COM + FileDef 旗標 `ffContainsNoMetaData` ，例如和 `ffWriteable` 。</span><span class="sxs-lookup"><span data-stu-id="8a3fc-108">COM+ FileDef flags such as `ffContainsNoMetaData` and `ffWriteable`.</span></span> <span data-ttu-id="8a3fc-109">`dwFlags` 會傳遞至 [DefineFile 方法](../metadata/imetadataassemblyemit-definefile-method.md)。</span><span class="sxs-lookup"><span data-stu-id="8a3fc-109">`dwFlags` is passed to [DefineFile Method](../metadata/imetadataassemblyemit-definefile-method.md).</span></span>  
  
 `pFileToken`  
 <span data-ttu-id="8a3fc-110">接收所產生檔案之識別碼的權杖指標。</span><span class="sxs-lookup"><span data-stu-id="8a3fc-110">Pointer to token that receives the ID for the resulting file.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="8a3fc-111">傳回值</span><span class="sxs-lookup"><span data-stu-id="8a3fc-111">Return Value</span></span>  

 <span data-ttu-id="8a3fc-112">如果方法成功，則傳回 S_OK。</span><span class="sxs-lookup"><span data-stu-id="8a3fc-112">Returns S_OK if the method succeeds.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="8a3fc-113">需求</span><span class="sxs-lookup"><span data-stu-id="8a3fc-113">Requirements</span></span>  

 <span data-ttu-id="8a3fc-114">需要 alink。h</span><span class="sxs-lookup"><span data-stu-id="8a3fc-114">Requires alink.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8a3fc-115">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8a3fc-115">See also</span></span>

- [<span data-ttu-id="8a3fc-116">IALink 介面</span><span class="sxs-lookup"><span data-stu-id="8a3fc-116">IALink Interface</span></span>](ialink-interface.md)
- [<span data-ttu-id="8a3fc-117">IALink2 介面</span><span class="sxs-lookup"><span data-stu-id="8a3fc-117">IALink2 Interface</span></span>](ialink2-interface.md)
- [<span data-ttu-id="8a3fc-118">ALink API</span><span class="sxs-lookup"><span data-stu-id="8a3fc-118">ALink API</span></span>](index.md)
