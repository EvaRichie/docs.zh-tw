---
title: ICeeFileGen 類別
ms.date: 03/30/2017
api_name:
- ICeeFileGen
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICeeFileGen
helpviewer_keywords:
- ICeeFileGen class [.NET Framework hosting]
ms.assetid: 90368606-506e-40df-be1f-8d595159203f
topic_type:
- apiref
ms.openlocfilehash: fc0de164b9489c9661bc6cb0ffb681f75e88ea26
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83617005"
---
# <a name="iceefilegen-class"></a><span data-ttu-id="e782b-102">ICeeFileGen 類別</span><span class="sxs-lookup"><span data-stu-id="e782b-102">ICeeFileGen Class</span></span>
<span data-ttu-id="e782b-103">提供建立原生可移植執行檔（PE）檔案的功能。</span><span class="sxs-lookup"><span data-stu-id="e782b-103">Provides functionality for creating a native portable executable (PE) file.</span></span> <span data-ttu-id="e782b-104">編譯器通常會使用此介面來產生其已編譯的輸出可執行檔。</span><span class="sxs-lookup"><span data-stu-id="e782b-104">The interface will typically be used by compilers to generate their compiled output executable.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="e782b-105">`ICeeFileGen`支援 .NET Framework 的基礎結構，但不適合直接從您的程式碼使用。</span><span class="sxs-lookup"><span data-stu-id="e782b-105">`ICeeFileGen` supports the .NET Framework infrastructure and is not intended to be used directly from your code.</span></span>  
  
 <span data-ttu-id="e782b-106">這個介面已被取代，將在未來的版本中移除。</span><span class="sxs-lookup"><span data-stu-id="e782b-106">This interface has been deprecated and will be removed in a future release.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="e782b-107">語法</span><span class="sxs-lookup"><span data-stu-id="e782b-107">Syntax</span></span>  
  
```cpp  
class ICeeFileGen {  
public:  
    virtual HRESULT CreateCeeFile(HCEEFILE *ceeFile);  
  
    virtual HRESULT EmitMetaData (HCEEFILE ceeFile,  
        IMetaDataEmit *emitter, mdScope scope);  
  
    virtual HRESULT EmitLibraryName (HCEEFILE ceeFile,  
        IMetaDataEmit *emitter, mdScope scope);  
  
    virtual HRESULT EmitMethod ();  
  
    virtual HRESULT GetMethodRVA (HCEEFILE ceeFile,  
        ULONG codeOffset, ULONG *codeRVA);  
  
    virtual HRESULT EmitSignature ();  
  
    virtual HRESULT EmitString (HCEEFILE ceeFile,  
        __in LPWSTR strValue, ULONG *strRef);  
  
    virtual HRESULT GenerateCeeFile (HCEEFILE ceeFile);  
  
    virtual HRESULT SetOutputFileName (HCEEFILE ceeFile,  
        __in LPWSTR outputFileName);  
  
    virtual HRESULT GetOutputFileName (HCEEFILE ceeFile,  
        __out LPWSTR *outputFileName);  
  
    virtual HRESULT SetResourceFileName (HCEEFILE ceeFile,  
        __in LPWSTR resourceFileName);  
  
    virtual HRESULT GetResourceFileName (HCEEFILE ceeFile,  
        __out LPWSTR *resourceFileName);  
  
    virtual HRESULT SetImageBase(HCEEFILE ceeFile, size_t imageBase);  
  
    virtual HRESULT SetSubsystem(HCEEFILE ceeFile, DWORD subsystem,  
        DWORD major, DWORD minor);  
  
    virtual HRESULT SetEntryClassToken ();  
  
    virtual HRESULT GetEntryClassToken ();  
  
    virtual HRESULT SetEntryPointDescr ();  
  
    virtual HRESULT GetEntryPointDescr ();  
  
    virtual HRESULT SetEntryPointFlags ();  
  
    virtual HRESULT GetEntryPointFlags ();  
  
    virtual HRESULT SetDllSwitch (HCEEFILE ceeFile, BOOL dllSwitch);  
  
    virtual HRESULT GetDllSwitch (HCEEFILE ceeFile, BOOL *dllSwitch);  
  
    virtual HRESULT SetLibraryName (HCEEFILE ceeFile,  
        __in LPWSTR LibraryName);  
  
    virtual HRESULT GetLibraryName (HCEEFILE ceeFile,  
        __out LPWSTR *LibraryName);  
  
    virtual HRESULT SetLibraryGuid (HCEEFILE ceeFile,  
        __in LPWSTR LibraryGuid);  
  
    virtual HRESULT DestroyCeeFile(HCEEFILE *ceeFile);  
  
    virtual HRESULT GetSectionCreate (HCEEFILE ceeFile,  
        const char *name, DWORD flags, HCEESECTION *section);  
  
    virtual HRESULT GetIlSection (HCEEFILE ceeFile,  
        HCEESECTION *section);  
  
    virtual HRESULT GetRdataSection (HCEEFILE ceeFile,  
        HCEESECTION *section);  
  
    virtual HRESULT GetSectionDataLen (HCEESECTION section,  
        ULONG *dataLen);  
  
    virtual HRESULT GetSectionBlock (HCEESECTION section, ULONG len,  
        ULONG align=1, void **ppBytes=0);  
  
    virtual HRESULT TruncateSection (HCEESECTION section, ULONG len);  
  
    virtual HRESULT AddSectionReloc (HCEESECTION section,  
        ULONG offset, HCEESECTION relativeTo,  
        CeeSectionRelocType relocType);  
  
    virtual HRESULT SetSectionDirectoryEntry (HCEESECTION section,  
        ULONG num);  
  
    virtual HRESULT CreateSig ();  
  
    virtual HRESULT AddSigArg ();  
  
    virtual HRESULT SetSigReturnType ();  
  
    virtual HRESULT SetSigCallingConvention ();  
  
    virtual HRESULT DeleteSig ();  
  
    virtual HRESULT SetEntryPoint (HCEEFILE ceeFile,  
        mdMethodDef method);  
  
    virtual HRESULT GetEntryPoint (HCEEFILE ceeFile,  
        mdMethodDef *method);  
  
    virtual HRESULT SetComImageFlags (HCEEFILE ceeFile, DWORD mask);  
  
    virtual HRESULT GetComImageFlags (HCEEFILE ceeFile, DWORD *mask);  
  
    virtual HRESULT GetIMapTokenIface(HCEEFILE ceeFile,  
        IMetaDataEmit *emitter, IUnknown **pIMapToken);  
  
    virtual HRESULT SetDirectoryEntry (HCEEFILE ceeFile,  
        HCEESECTION section, ULONG num, ULONG size, ULONG offset = 0);  
  
    virtual HRESULT EmitMetaDataEx (HCEEFILE ceeFile,  
        IMetaDataEmit *emitter);
  
    virtual HRESULT EmitLibraryNameEx (HCEEFILE ceeFile,  
        IMetaDataEmit *emitter);  
  
    virtual HRESULT GetIMapTokenIfaceEx(HCEEFILE ceeFile,  
        IMetaDataEmit *emitter, IUnknown **pIMapToken);  
  
    virtual HRESULT EmitMacroDefinitions(HCEEFILE ceeFile,  
        void *pData, DWORD cData);  
  
    virtual HRESULT CreateCeeFileFromICeeGen(ICeeGen *pFromICeeGen,  
        HCEEFILE *ceeFile, DWORD createFlags =  
        ICEE_CREATE_FILE_PURE_IL);  
  
    virtual HRESULT SetManifestEntry(HCEEFILE ceeFile, ULONG size,  
        ULONG offset);  
  
    virtual HRESULT SetEnCRVABase(HCEEFILE ceeFile, ULONG dataBase,  
        ULONG rdataBase);  
  
    virtual HRESULT GenerateCeeMemoryImage (HCEEFILE ceeFile,  
        void **ppImage);  
  
    virtual HRESULT ComputeSectionOffset(HCEESECTION section,  
        __in char *ptr, unsigned *offset);  
  
    virtual HRESULT ComputeOffset(HCEEFILE file, __in char *ptr,  
        HCEESECTION *pSection, unsigned *offset);  
  
    virtual HRESULT GetCorHeader(HCEEFILE ceeFile,  
        IMAGE_COR20_HEADER **header);  
  
    virtual HRESULT LinkCeeFile (HCEEFILE ceeFile);  
  
    virtual HRESULT FixupCeeFile (HCEEFILE ceeFile);  
  
    virtual HRESULT GetSectionRVA (HCEESECTION section, ULONG *rva);  
  
    virtual HRESULT ComputeSectionPointer(HCEESECTION section,  
        ULONG offset, __out char **ptr);  
  
    virtual HRESULT SetObjSwitch (HCEEFILE ceeFile, BOOL objSwitch);  
  
    virtual HRESULT GetObjSwitch (HCEEFILE ceeFile, BOOL *objSwitch);  
  
    virtual HRESULT SetVTableEntry(HCEEFILE ceeFile, ULONG size,  
        ULONG offset);  
  
    virtual HRESULT SetStrongNameEntry(HCEEFILE ceeFile, ULONG size,  
        ULONG offset);  
  
    virtual HRESULT EmitMetaDataAt (HCEEFILE ceeFile,  
        IMetaDataEmit *emitter, HCEESECTION section, DWORD offset,  
        BYTE* buffer, unsigned buffLen);  
  
    virtual HRESULT GetFileTimeStamp (HCEEFILE ceeFile,  
        DWORD *pTimeStamp);  
  
    virtual HRESULT AddNotificationHandler(HCEEFILE ceeFile,  
        IUnknown *pHandler);  
  
    virtual HRESULT SetFileAlignment(HCEEFILE ceeFile,  
        ULONG fileAlignment);  
  
    virtual HRESULT ClearComImageFlags (HCEEFILE ceeFile, DWORD mask);  
  
    virtual HRESULT CreateCeeFileEx(HCEEFILE *ceeFile,  
        ULONG createFlags);  
  
    virtual HRESULT SetImageBase64(HCEEFILE ceeFile,  
        ULONGLONG imageBase);  
  
    virtual HRESULT GetHeaderInfo (HCEEFILE ceeFile,  
        PIMAGE_NT_HEADERS *ppNtHeaders,  
        PIMAGE_SECTION_HEADER *ppSections, ULONG *pNumSections);  
  
    virtual HRESULT CreateCeeFileEx2(HCEEFILE *ceeFile,  
        ULONG createFlags, LPCWSTR seedFileName = NULL);  
  
    virtual HRESULT SetVTableEntry64(HCEEFILE ceeFile, ULONG size,  
        void* ptr);  
};  
```  
  
## <a name="requirements"></a><span data-ttu-id="e782b-108">需求</span><span class="sxs-lookup"><span data-stu-id="e782b-108">Requirements</span></span>  
 <span data-ttu-id="e782b-109">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="e782b-109">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="e782b-110">**標頭：** ICeeFileGen。h</span><span class="sxs-lookup"><span data-stu-id="e782b-110">**Header:** ICeeFileGen.h</span></span>  
  
 <span data-ttu-id="e782b-111">**.NET Framework 版本：** 1。0</span><span class="sxs-lookup"><span data-stu-id="e782b-111">**.NET Framework Version:** 1.0</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e782b-112">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e782b-112">See also</span></span>

- [<span data-ttu-id="e782b-113">裝載介面</span><span class="sxs-lookup"><span data-stu-id="e782b-113">Hosting Interfaces</span></span>](hosting-interfaces.md)
