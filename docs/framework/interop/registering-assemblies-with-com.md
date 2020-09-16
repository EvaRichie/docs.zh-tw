---
title: 向 COM 註冊組件
description: '使用元件註冊工具 ( # A0) 註冊或取消註冊元件，這會將類別的相關資訊新增至系統登錄。'
ms.date: 03/30/2017
helpviewer_keywords:
- COM interop, registering assemblies
- unregistering assemblies
- interoperation with unmanaged code, registering assemblies
- registering assemblies
ms.assetid: 87925795-a3ae-4833-b138-125413478551
ms.openlocfilehash: 0adae4db393c4c01620ea896c4451c3279272fca
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90559274"
---
# <a name="registering-assemblies-with-com"></a><span data-ttu-id="31424-103">向 COM 註冊組件</span><span class="sxs-lookup"><span data-stu-id="31424-103">Registering Assemblies with COM</span></span>
<span data-ttu-id="31424-104">您可以執行稱為[組件註冊工具 (Regasm.exe)](../tools/regasm-exe-assembly-registration-tool.md) 的命令列工具，註冊或取消登錄與 COM 搭配使用的組件。</span><span class="sxs-lookup"><span data-stu-id="31424-104">You can run a command-line tool called the [Assembly Registration Tool (Regasm.exe)](../tools/regasm-exe-assembly-registration-tool.md) to register or unregister an assembly for use with COM.</span></span> <span data-ttu-id="31424-105">Regasm.exe 會將此類別的相關資訊新增至容器登錄，讓 COM 用戶端可以明確地使用 .NET Framework 類別。</span><span class="sxs-lookup"><span data-stu-id="31424-105">Regasm.exe adds information about the class to the system registry so COM clients can use the .NET Framework class transparently.</span></span> <span data-ttu-id="31424-106"><xref:System.Runtime.InteropServices.RegistrationServices> 類別提供對等功能。</span><span class="sxs-lookup"><span data-stu-id="31424-106">The <xref:System.Runtime.InteropServices.RegistrationServices> class provides the equivalent functionality.</span></span>  
  
 <span data-ttu-id="31424-107">必須先在 Windows 登錄中註冊 Managed 元件，才能從 COM 用戶端進行啟用。</span><span class="sxs-lookup"><span data-stu-id="31424-107">A managed component must be registered in the Windows registry before it can be activated from a COM client.</span></span> <span data-ttu-id="31424-108">下表顯示 Regasm.exe 通常會新增至 Windows 登錄的機碼</span><span class="sxs-lookup"><span data-stu-id="31424-108">The following table shows the keys that Regasm.exe typically adds to the Windows registry.</span></span> <span data-ttu-id="31424-109">(000000 表示實際 GUID 值)。</span><span class="sxs-lookup"><span data-stu-id="31424-109">(000000 indicates the actual GUID value.)</span></span>  
  
|<span data-ttu-id="31424-110">GUID</span><span class="sxs-lookup"><span data-stu-id="31424-110">GUID</span></span>|<span data-ttu-id="31424-111">描述</span><span class="sxs-lookup"><span data-stu-id="31424-111">Description</span></span>|<span data-ttu-id="31424-112">登錄機碼</span><span class="sxs-lookup"><span data-stu-id="31424-112">Registry key</span></span>|  
|----------|-----------------|------------------|  
|<span data-ttu-id="31424-113">CLSID</span><span class="sxs-lookup"><span data-stu-id="31424-113">CLSID</span></span>|<span data-ttu-id="31424-114">類別識別碼</span><span class="sxs-lookup"><span data-stu-id="31424-114">Class identifier</span></span>|<span data-ttu-id="31424-115">HKEY_CLASSES_ROOT\CLSID\\{000…000}</span><span class="sxs-lookup"><span data-stu-id="31424-115">HKEY_CLASSES_ROOT\CLSID\\{000…000}</span></span>|  
|<span data-ttu-id="31424-116">IID</span><span class="sxs-lookup"><span data-stu-id="31424-116">IID</span></span>|<span data-ttu-id="31424-117">介面識別碼</span><span class="sxs-lookup"><span data-stu-id="31424-117">Interface identifier</span></span>|<span data-ttu-id="31424-118">HKEY_CLASSES_ROOT\Interface\\{000…000}</span><span class="sxs-lookup"><span data-stu-id="31424-118">HKEY_CLASSES_ROOT\Interface\\{000…000}</span></span>|  
|<span data-ttu-id="31424-119">LIBID</span><span class="sxs-lookup"><span data-stu-id="31424-119">LIBID</span></span>|<span data-ttu-id="31424-120">程式庫識別碼</span><span class="sxs-lookup"><span data-stu-id="31424-120">Library identifier</span></span>|<span data-ttu-id="31424-121">HKEY_CLASSES_ROOT\TypeLib\\{000…000}</span><span class="sxs-lookup"><span data-stu-id="31424-121">HKEY_CLASSES_ROOT\TypeLib\\{000…000}</span></span>|  
|<span data-ttu-id="31424-122">ProgID</span><span class="sxs-lookup"><span data-stu-id="31424-122">ProgID</span></span>|<span data-ttu-id="31424-123">程式設計識別碼</span><span class="sxs-lookup"><span data-stu-id="31424-123">Programmatic identifier</span></span>|<span data-ttu-id="31424-124">HKEY_CLASSES_ROOT\000…000</span><span class="sxs-lookup"><span data-stu-id="31424-124">HKEY_CLASSES_ROOT\000…000</span></span>|  
  
 <span data-ttu-id="31424-125">在 HKCR\CLSID\\{0000…0000} 機碼下，預設值設定為類別的 ProgID，並新增兩個新具名值：類別和組件。</span><span class="sxs-lookup"><span data-stu-id="31424-125">Under the HKCR\CLSID\\{0000…0000} key, the default value is set to the ProgID of the class, and two new named values, Class and Assembly, are added.</span></span> <span data-ttu-id="31424-126">執行階段會從登錄讀取 Assembly 值，並將它傳入執行階段組件解析程式。</span><span class="sxs-lookup"><span data-stu-id="31424-126">The runtime reads the Assembly value from the registry and passes it on to the runtime assembly resolver.</span></span> <span data-ttu-id="31424-127">組件解析程式會根據名稱和版本號碼這類組件資訊來嘗試找出組件。</span><span class="sxs-lookup"><span data-stu-id="31424-127">The assembly resolver attempts to locate the assembly, based on assembly information such as the name and version number.</span></span> <span data-ttu-id="31424-128">若要讓組件解析程式找到組件，組件必須位在下列其中一個位置：</span><span class="sxs-lookup"><span data-stu-id="31424-128">For the assembly resolver to locate an assembly, the assembly has to be in one of the following locations:</span></span>  
  
- <span data-ttu-id="31424-129">全域組件快取 (必須是強式名稱組件)。</span><span class="sxs-lookup"><span data-stu-id="31424-129">The global assembly cache (must be a strong-named assembly).</span></span>  
  
- <span data-ttu-id="31424-130">在應用程式目錄中。</span><span class="sxs-lookup"><span data-stu-id="31424-130">In the application directory.</span></span> <span data-ttu-id="31424-131">只有從該應用程式才能存取從應用程式路徑載入的組件。</span><span class="sxs-lookup"><span data-stu-id="31424-131">Assemblies loaded from the application path are only accessible from that application.</span></span>  
  
- <span data-ttu-id="31424-132">使用 **/codebase** 選項所指定之 Regasm.exe 的檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="31424-132">Along an file path specified with the **/codebase** option to Regasm.exe.</span></span>  
  
 <span data-ttu-id="31424-133">Regasm.exe 也會在 HKCR\CLSID\\{0000…0000} 機碼下建立 InProcServer32 機碼。</span><span class="sxs-lookup"><span data-stu-id="31424-133">Regasm.exe also creates the InProcServer32 key under the HKCR\CLSID\\{0000…0000} key.</span></span> <span data-ttu-id="31424-134">索引鍵的預設值設為初始化 Common Language Runtime 的 DLL 名稱 (Mscoree.dll)。</span><span class="sxs-lookup"><span data-stu-id="31424-134">The default value for the key is set to the name of the DLL that initializes the common language runtime (Mscoree.dll).</span></span>  
  
## <a name="examining-registry-entries"></a><span data-ttu-id="31424-135">檢查登錄項目</span><span class="sxs-lookup"><span data-stu-id="31424-135">Examining Registry Entries</span></span>  
 <span data-ttu-id="31424-136">COM Interop 提供標準 Class Factory 實作，來建立任何 .NET Framework 類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="31424-136">COM interop provides a standard class factory implementation to create an instance of any .NET Framework class.</span></span> <span data-ttu-id="31424-137">用戶端可以在 Managed DLL 上呼叫 **DllGetClassObject**，來取得 Class Factory 以及建立物件，就像使用任何其他 COM 元件一樣。</span><span class="sxs-lookup"><span data-stu-id="31424-137">Clients can call **DllGetClassObject** on the managed DLL to get a class factory and create objects, just as they would with any other COM component.</span></span>  
  
 <span data-ttu-id="31424-138">針對 `InprocServer32` 索引鍵，Mscoree.dll 的參考會取代傳統 COM 型別程式庫，以指出 Common Language Runtime 建立 Managed 物件。</span><span class="sxs-lookup"><span data-stu-id="31424-138">For the `InprocServer32` subkey, a reference to Mscoree.dll appears in place of a traditional COM type library to indicate that the common language runtime creates the managed object.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="31424-139">另請參閱</span><span class="sxs-lookup"><span data-stu-id="31424-139">See also</span></span>

- [<span data-ttu-id="31424-140">將 .NET Framework 元件公開給 COM</span><span class="sxs-lookup"><span data-stu-id="31424-140">Exposing .NET Framework Components to COM</span></span>](exposing-dotnet-components-to-com.md)
- [<span data-ttu-id="31424-141">作法：參考 COM 的 .NET 類型</span><span class="sxs-lookup"><span data-stu-id="31424-141">How to: Reference .NET Types from COM</span></span>](how-to-reference-net-types-from-com.md)
- <span data-ttu-id="31424-142">[呼叫 .NET 物件](/previous-versions/dotnet/netframework-4.0/8hw8h46b(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="31424-142">[Calling a .NET Object](/previous-versions/dotnet/netframework-4.0/8hw8h46b(v=vs.100))</span></span>
- <span data-ttu-id="31424-143">[部署供 COM 存取的應用程式](/previous-versions/dotnet/netframework-4.0/c2850st8(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="31424-143">[Deploying an Application for COM Access](/previous-versions/dotnet/netframework-4.0/c2850st8(v=vs.100))</span></span>
