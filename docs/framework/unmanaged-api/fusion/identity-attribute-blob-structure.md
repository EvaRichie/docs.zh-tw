---
title: IDENTITY_ATTRIBUTE_BLOB 結構
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- IDENTITY_ATTRIBUTE_BLOB
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IDENTITY_ATTRIBUTE_BLOB
helpviewer_keywords:
- IDENTITY_ATTRIBUTE_BLOB structure [.NET Framework fusion]
ms.assetid: af14ae5f-d226-47dd-ba90-8fc6e6605d4d
topic_type:
- apiref
ms.openlocfilehash: 9a59e70257064220e8138f9d267a815fcdbf3929
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95729027"
---
# <a name="identity_attribute_blob-structure"></a><span data-ttu-id="0712f-102">IDENTITY_ATTRIBUTE_BLOB 結構</span><span class="sxs-lookup"><span data-stu-id="0712f-102">IDENTITY_ATTRIBUTE_BLOB Structure</span></span>

<span data-ttu-id="0712f-103">包含元件中單一屬性的相關資訊，由三個組成 `DWORD` 。</span><span class="sxs-lookup"><span data-stu-id="0712f-103">Contains information about a single attribute in an assembly, and consists of three `DWORD`s.</span></span> <span data-ttu-id="0712f-104">每個 `DWORD` 都是 `CurrentIntoBuffer` [IEnumIDENTITY_ATTRIBUTE](ienumidentity-attribute-interface.md) 介面的方法所產生之字元緩衝區的位移。</span><span class="sxs-lookup"><span data-stu-id="0712f-104">Each `DWORD` is an offset into a character buffer produced by the `CurrentIntoBuffer` method of the [IEnumIDENTITY_ATTRIBUTE](ienumidentity-attribute-interface.md) interface</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="0712f-105">語法</span><span class="sxs-lookup"><span data-stu-id="0712f-105">Syntax</span></span>  
  
```cpp  
typedef struct _IDENTITY_ATTRIBUTE_BLOB {  
    DWORD  ofsNamespace;  
    DWORD  ofsName;  
    DWORD  ofsValue;  
}   IDENTITY_ATTRIBUTE_BLOB;  
```  
  
## <a name="members"></a><span data-ttu-id="0712f-106">成員</span><span class="sxs-lookup"><span data-stu-id="0712f-106">Members</span></span>  
  
|<span data-ttu-id="0712f-107">member</span><span class="sxs-lookup"><span data-stu-id="0712f-107">Member</span></span>|<span data-ttu-id="0712f-108">描述</span><span class="sxs-lookup"><span data-stu-id="0712f-108">Description</span></span>|  
|------------|-----------------|  
|`ofsNamespace`|<span data-ttu-id="0712f-109">字元緩衝區的第一個位移。</span><span class="sxs-lookup"><span data-stu-id="0712f-109">The first offset into the character buffer.</span></span> <span data-ttu-id="0712f-110">這個位移後面沒有屬性的命名空間，而是由一系列的 null 字元所組成。</span><span class="sxs-lookup"><span data-stu-id="0712f-110">This offset is not followed by the attribute's namespace, but by a series of null characters.</span></span> <span data-ttu-id="0712f-111">因此，它不會使用。</span><span class="sxs-lookup"><span data-stu-id="0712f-111">Therefore, it is not used.</span></span>|  
|`ofsName`|<span data-ttu-id="0712f-112">字元緩衝區的第二個位移。</span><span class="sxs-lookup"><span data-stu-id="0712f-112">The second offset into the character buffer.</span></span> <span data-ttu-id="0712f-113">這個位置會標示屬性名稱的開頭。</span><span class="sxs-lookup"><span data-stu-id="0712f-113">This location marks the start of the attribute's name.</span></span>|  
|`ofsValue`|<span data-ttu-id="0712f-114">字元緩衝區的第三個位移。</span><span class="sxs-lookup"><span data-stu-id="0712f-114">The third offset into the character buffer.</span></span> <span data-ttu-id="0712f-115">這個位置會標示屬性值的開頭。</span><span class="sxs-lookup"><span data-stu-id="0712f-115">This location marks the start of the attribute's value.</span></span>|  
  
## <a name="sample"></a><span data-ttu-id="0712f-116">範例</span><span class="sxs-lookup"><span data-stu-id="0712f-116">Sample</span></span>  

 <span data-ttu-id="0712f-117">下列範例說明幾個基本步驟，最後會產生已填入的 `IDENTITY_ATTRIBUTE_BLOB` 結構：</span><span class="sxs-lookup"><span data-stu-id="0712f-117">The following example illustrates several basic steps, which eventually result in a populated `IDENTITY_ATTRIBUTE_BLOB` structure:</span></span>  
  
1. <span data-ttu-id="0712f-118">取得元件的 [IReferenceIdentity](ireferenceidentity-interface.md) 。</span><span class="sxs-lookup"><span data-stu-id="0712f-118">Obtain an [IReferenceIdentity](ireferenceidentity-interface.md) for the assembly.</span></span>  
  
2. <span data-ttu-id="0712f-119">呼叫 `IReferenceIdentity::EnumAttributes` 方法，並取得 [IEnumIDENTITY_ATTRIBUTE](ienumidentity-attribute-interface.md)。</span><span class="sxs-lookup"><span data-stu-id="0712f-119">Call the `IReferenceIdentity::EnumAttributes` method, and obtain an [IEnumIDENTITY_ATTRIBUTE](ienumidentity-attribute-interface.md).</span></span>  
  
3. <span data-ttu-id="0712f-120">建立字元緩衝區，並將其轉換成 `IDENTITY_ATTRIBUTE_BLOB` 結構。</span><span class="sxs-lookup"><span data-stu-id="0712f-120">Create a character buffer, and cast it as an `IDENTITY_ATTRIBUTE_BLOB` structure.</span></span>  
  
4. <span data-ttu-id="0712f-121">呼叫 `CurrentIntoBuffer` 介面的方法 `IEnumIDENTITY_ATTRIBUTE` 。</span><span class="sxs-lookup"><span data-stu-id="0712f-121">Call the `CurrentIntoBuffer` method of the `IEnumIDENTITY_ATTRIBUTE` interface.</span></span> <span data-ttu-id="0712f-122">這個方法會將屬性 `Namespace` 、 `Name` 和複製 `Value` 到字元緩衝區。</span><span class="sxs-lookup"><span data-stu-id="0712f-122">This method copies the attributes `Namespace`, `Name`, and `Value` into the character buffer.</span></span> <span data-ttu-id="0712f-123">這些字串的三個位移將會出現在 `IDENTITY_ATTRIBUTE_BLOB` 結構中。</span><span class="sxs-lookup"><span data-stu-id="0712f-123">The three offsets to those strings will become available in the `IDENTITY_ATTRIBUTE_BLOB` structure.</span></span>  
  
```cpp  
// EnumAssemblyAttributes.cpp : main project file.  
  
#include "stdafx.h"  
  
#include "fusion.h"  
#include "windows.h"  
#include "stdio.h"  
#include "mscoree.h"  
#include "isolation.h"  
  
typedef HRESULT (__stdcall *PFNGETREF)(LPCWSTR pwzFile, REFIID riid, IUnknown **ppUnk);  
typedef HRESULT (__stdcall *PFNGETAUTH)(IIdentityAuthority **ppIIdentityAuthority);  
  
PFNGETREF                   g_pfnGetAssemblyIdentityFromFile = NULL;  
PFNGETAUTH                  g_pfnGetIdentityAuthority = NULL;  
IUnknown                    *g_pUnk = NULL;  
  
bool Init()  
{  
    HRESULT     hr = S_OK;  
    DWORD       dwSize = 0;  
    bool        bRC = false;  
  
    hr = CorBindToRuntimeEx(NULL, L"wks", 0, CLSID_CorRuntimeHost,  
                           IID_ICorRuntimeHost, (void **)&g_pUnk);  
    if(FAILED(hr)) {  
        printf("Error: Failed to initialize CLR runtime! hr = 0x%0x\n",  
                hr);  
        goto Exit;  
    }  
  
    if (SUCCEEDED(hr)) {  
        hr = GetRealProcAddress("GetAssemblyIdentityFromFile",  
                         (VOID **)&g_pfnGetAssemblyIdentityFromFile);  
    }  
  
    if (SUCCEEDED(hr)) {  
        hr = GetRealProcAddress("GetIdentityAuthority",  
                                (VOID **)&g_pfnGetIdentityAuthority);  
    }  
  
    if (!g_pfnGetAssemblyIdentityFromFile ||
        !g_pfnGetIdentityAuthority)  
    {  
        printf("Error: Cannot get required APIs from fusion.dll!\n");  
        goto Exit;  
    }  
  
    bRC = true;  
  
Exit:  
    return bRC;  
}  
  
void Shutdown()  
{  
    if(g_pUnk) {  
        g_pUnk->Release();  
        g_pUnk = NULL;  
    }  
}  
  
void Usage()  
{  
    printf("EnumAssemblyAttributes: A tool to enumerate the identity
            attributes of a given assembly.\n\n");  
    printf("Usage: EnumAssemblyAttributes AssemblyFilePath\n");  
    printf("\n");  
}  
  
int _cdecl wmain(int argc, LPCWSTR argv[])  
{  
    int     iResult = 1;  
    IUnknown                    *pUnk  = NULL;  
    IReferenceIdentity          *pRef  = NULL;  
    HRESULT                     hr     = S_OK;
    IEnumIDENTITY_ATTRIBUTE     *pEnum = NULL;  
    BYTE                        abData[1024];  
    DWORD                       cbAvailable;  
    DWORD                       cbUsed;  
    IDENTITY_ATTRIBUTE_BLOB     *pBlob;  
  
    if(argc != 2) {  
        Usage();  
        goto Exit;  
    }  
  
    if(!Init()) {  
        printf("Failure initializing EnumIdAttr.\n");  
        goto Exit;  
    }  
  
    hr = g_pfnGetAssemblyIdentityFromFile(argv[1],
                            __uuidof(IReferenceIdentity), &pUnk);  
  
    if (FAILED(hr)) {  
        printf("GetAssemblyIdentityFromFile failed with hr = 0x%x",
                hr);  
        goto Exit;  
    }  
  
    hr = pUnk->QueryInterface(__uuidof(IReferenceIdentity),
                              (void**)&pRef);  
    if (FAILED(hr)) {  
        goto Exit;  
    }  
  
    hr = pRef->EnumAttributes(&pEnum);  
    if (FAILED(hr)) {  
        printf("IReferenceIdentity::EnumAttributes failed with hr =
                0x%x", hr);  
        goto Exit;  
    }  
  
    pBlob = (IDENTITY_ATTRIBUTE_BLOB *)(abData);  
    while (1) {  
        cbAvailable = sizeof(abData);  
        hr = pEnum->CurrentIntoBuffer(cbAvailable, abData, &cbUsed);  
        if (FAILED(hr)) {  
            printf("IEnumIDENTITY_ATTRIBUTE::CurrentIntoBuffer failed
                    with hr = 0x%x", hr);  
            goto Exit;  
        }  
  
        if (! cbUsed) {  
            break;  
        }  
  
        LPWSTR pwzNameSpace = (LPWSTR)(abData + pBlob->ofsNamespace);  
        LPWSTR pwzName      = (LPWSTR)(abData + pBlob->ofsName);  
        LPWSTR pwzValue     = (LPWSTR)(abData + pBlob->ofsValue);  
        printf("%ws: %ws = %ws\n", pwzNameSpace, pwzName, pwzValue);  
  
        hr = pEnum->Skip(1);  
        if (FAILED(hr)) {  
            printf("IEnumIDENTITY_ATTRIBUTE::Skip failed with hr =
                    0x%x", hr);  
            goto Exit;  
        }  
    }  
  
    iResult = 0;  
  
Exit:  
  
    Shutdown();  
  
    if (pUnk) {  
        pUnk->Release();  
    }  
  
    if (pRef) {  
        pRef->Release();  
    }  
  
    if (pEnum) {  
        pEnum->Release();  
    }  
  
    return iResult;  
}  
```  
  
### <a name="to-run-the-sample"></a><span data-ttu-id="0712f-124">執行範例</span><span class="sxs-lookup"><span data-stu-id="0712f-124">To run the sample</span></span>  

 <span data-ttu-id="0712f-125">C： \\> EnumAssemblyAttributes.exe C:\WINDOWS\Microsoft.NET\Framework\v2.0.50727\System.dll</span><span class="sxs-lookup"><span data-stu-id="0712f-125">C:\\> EnumAssemblyAttributes.exe C:\WINDOWS\Microsoft.NET\Framework\v2.0.50727\System.dll</span></span>  
  
### <a name="sample-output"></a><span data-ttu-id="0712f-126">範例輸出</span><span class="sxs-lookup"><span data-stu-id="0712f-126">Sample output</span></span>  

 <span data-ttu-id="0712f-127">文化特性 = 中性</span><span class="sxs-lookup"><span data-stu-id="0712f-127">Culture = neutral</span></span>  
  
 <span data-ttu-id="0712f-128">名稱 = 系統</span><span class="sxs-lookup"><span data-stu-id="0712f-128">name = System</span></span>  
  
 <span data-ttu-id="0712f-129">processorArchitecture = MSIL</span><span class="sxs-lookup"><span data-stu-id="0712f-129">processorArchitecture = MSIL</span></span>  
  
 <span data-ttu-id="0712f-130">PublicKeyToken = b77a5c561934e089</span><span class="sxs-lookup"><span data-stu-id="0712f-130">PublicKeyToken = b77a5c561934e089</span></span>  
  
 <span data-ttu-id="0712f-131">Version = 2.0.0。0</span><span class="sxs-lookup"><span data-stu-id="0712f-131">Version = 2.0.0.0</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="0712f-132">需求</span><span class="sxs-lookup"><span data-stu-id="0712f-132">Requirements</span></span>  

 <span data-ttu-id="0712f-133">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="0712f-133">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="0712f-134">**標頭：** 隔離。h</span><span class="sxs-lookup"><span data-stu-id="0712f-134">**Header:** Isolation.h</span></span>  
  
 <span data-ttu-id="0712f-135">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="0712f-135">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="0712f-136">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0712f-136">See also</span></span>

- [<span data-ttu-id="0712f-137">IReferenceIdentity 介面</span><span class="sxs-lookup"><span data-stu-id="0712f-137">IReferenceIdentity Interface</span></span>](ireferenceidentity-interface.md)
- [<span data-ttu-id="0712f-138">IEnumIDENTITY_ATTRIBUTE 介面</span><span class="sxs-lookup"><span data-stu-id="0712f-138">IEnumIDENTITY_ATTRIBUTE Interface</span></span>](ienumidentity-attribute-interface.md)
- [<span data-ttu-id="0712f-139">IDENTITY_ATTRIBUTE 結構</span><span class="sxs-lookup"><span data-stu-id="0712f-139">IDENTITY_ATTRIBUTE Structure</span></span>](identity-attribute-structure.md)
- [<span data-ttu-id="0712f-140">融合結構</span><span class="sxs-lookup"><span data-stu-id="0712f-140">Fusion Structures</span></span>](fusion-structures.md)
