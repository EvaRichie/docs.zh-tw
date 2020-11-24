---
title: IMetaDataValidate 介面
ms.date: 03/30/2017
api_name:
- IMetaDataValidate
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataValidate
helpviewer_keywords:
- IMetaDataValidate interface [.NET Framework metadata]
ms.assetid: db98608a-e85c-4f50-9d7b-5f57a426ddb6
topic_type:
- apiref
ms.openlocfilehash: 518ee65bc684f643bf4f608223c0fa40ea3f0dd9
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95685522"
---
# <a name="imetadatavalidate-interface"></a><span data-ttu-id="a1944-102">IMetaDataValidate 介面</span><span class="sxs-lookup"><span data-stu-id="a1944-102">IMetaDataValidate Interface</span></span>

<span data-ttu-id="a1944-103">提供方法來驗證中繼資料的簽章。</span><span class="sxs-lookup"><span data-stu-id="a1944-103">Provides methods to validate metadata signatures.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="a1944-104">方法</span><span class="sxs-lookup"><span data-stu-id="a1944-104">Methods</span></span>  
  
|<span data-ttu-id="a1944-105">方法</span><span class="sxs-lookup"><span data-stu-id="a1944-105">Method</span></span>|<span data-ttu-id="a1944-106">描述</span><span class="sxs-lookup"><span data-stu-id="a1944-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="a1944-107">ValidateMetaData 方法</span><span class="sxs-lookup"><span data-stu-id="a1944-107">ValidateMetaData Method</span></span>](imetadatavalidate-validatemetadata-method.md)|<span data-ttu-id="a1944-108">驗證目前中繼資料範圍內物件的中繼資料簽章。</span><span class="sxs-lookup"><span data-stu-id="a1944-108">Validates the metadata signatures of the objects in the current metadata scope.</span></span>|  
|[<span data-ttu-id="a1944-109">ValidatorInit 方法</span><span class="sxs-lookup"><span data-stu-id="a1944-109">ValidatorInit Method</span></span>](imetadatavalidate-validatorinit-method.md)|<span data-ttu-id="a1944-110">設定會指定目前中繼資料範圍內模組類型的旗標，並註冊對於驗證錯誤的指定回呼方法。</span><span class="sxs-lookup"><span data-stu-id="a1944-110">Sets a flag that specifies the type of the module in the current metadata scope, and registers the specified callback method for validation errors.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="a1944-111">需求</span><span class="sxs-lookup"><span data-stu-id="a1944-111">Requirements</span></span>  

 <span data-ttu-id="a1944-112">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="a1944-112">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="a1944-113">**標頭：** Cor。h</span><span class="sxs-lookup"><span data-stu-id="a1944-113">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="a1944-114">連結 **庫：** 當做 MsCorEE.dll 中的資源使用</span><span class="sxs-lookup"><span data-stu-id="a1944-114">**Library:** Used as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="a1944-115">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="a1944-115">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a1944-116">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a1944-116">See also</span></span>

- [<span data-ttu-id="a1944-117">中繼資料介面</span><span class="sxs-lookup"><span data-stu-id="a1944-117">Metadata Interfaces</span></span>](metadata-interfaces.md)
