---
title: ISymUnmanagedWriter::SetUserEntryPoint 方法
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.SetUserEntryPoint
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::SetUserEntryPoint
helpviewer_keywords:
- ISymUnmanagedWriter::SetUserEntryPoint method [.NET Framework debugging]
- SetUserEntryPoint method [.NET Framework debugging]
ms.assetid: d4dcc575-3ac8-4453-9be1-2b24f47363d7
topic_type:
- apiref
ms.openlocfilehash: 8b51a9dc3a968c6bd2f5f9b149f13f88dc6a1e05
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614743"
---
# <a name="isymunmanagedwritersetuserentrypoint-method"></a><span data-ttu-id="4edfe-102">ISymUnmanagedWriter::SetUserEntryPoint 方法</span><span class="sxs-lookup"><span data-stu-id="4edfe-102">ISymUnmanagedWriter::SetUserEntryPoint Method</span></span>
<span data-ttu-id="4edfe-103">指定使用者定義的方法，這是此模組的進入點。</span><span class="sxs-lookup"><span data-stu-id="4edfe-103">Specifies the user-defined method that is the entry point for this module.</span></span> <span data-ttu-id="4edfe-104">例如，這個進入點可能是使用者的 main 方法，而不是編譯器在 main 之前產生的 stub。</span><span class="sxs-lookup"><span data-stu-id="4edfe-104">For example, this entry point could be the user's main method instead of compiler-generated stubs before main.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="4edfe-105">語法</span><span class="sxs-lookup"><span data-stu-id="4edfe-105">Syntax</span></span>  
  
```cpp  
HRESULT SetUserEntryPoint(  
    [in] mdMethodDef entryMethod);  
```  
  
## <a name="parameters"></a><span data-ttu-id="4edfe-106">參數</span><span class="sxs-lookup"><span data-stu-id="4edfe-106">Parameters</span></span>  
 `entryMethod`  
 <span data-ttu-id="4edfe-107">在使用者進入點之方法的元資料標記。</span><span class="sxs-lookup"><span data-stu-id="4edfe-107">[in] The metadata token for the method that is the user entry point.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="4edfe-108">傳回值</span><span class="sxs-lookup"><span data-stu-id="4edfe-108">Return Value</span></span>  
 <span data-ttu-id="4edfe-109">如果方法成功，則 S_OK;否則，E_FAIL 或一些其他錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="4edfe-109">S_OK if the method succeeds; otherwise, E_FAIL or some other error code.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="4edfe-110">需求</span><span class="sxs-lookup"><span data-stu-id="4edfe-110">Requirements</span></span>  
 <span data-ttu-id="4edfe-111">**標頭：** CorSym .idl，CorSym。h</span><span class="sxs-lookup"><span data-stu-id="4edfe-111">**Header:** CorSym.idl, CorSym.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="4edfe-112">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4edfe-112">See also</span></span>

- [<span data-ttu-id="4edfe-113">ISymUnmanagedWriter 介面</span><span class="sxs-lookup"><span data-stu-id="4edfe-113">ISymUnmanagedWriter Interface</span></span>](isymunmanagedwriter-interface.md)
