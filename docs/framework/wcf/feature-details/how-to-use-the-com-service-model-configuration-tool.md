---
title: 作法：使用 COM+ 服務模型組態工具
ms.date: 03/30/2017
helpviewer_keywords:
- COM+ [WCF], using service model configuration tool
ms.assetid: 7e68cd8d-5fda-4641-b92f-290db874376e
ms.openlocfilehash: 2d21ec8ccf84a7c9af235af8e0afd444044cf81b
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95729383"
---
# <a name="how-to-use-the-com-service-model-configuration-tool"></a><span data-ttu-id="44396-102">作法：使用 COM+ 服務模型組態工具</span><span class="sxs-lookup"><span data-stu-id="44396-102">How to: Use the COM+ Service Model Configuration Tool</span></span>

<span data-ttu-id="44396-103">一旦您選取了適當的裝載模式，請使用 COM+ 服務模型組態命令列工具 (ComSvcConfig.exe) 來設定將公開為 Web 服務的應用程式介面。</span><span class="sxs-lookup"><span data-stu-id="44396-103">Once you have selected an appropriate hosting mode, use the COM+ Service Model Configuration command-line tool (ComSvcConfig.exe) to configure the application interfaces that will be exposed as Web services.</span></span>

> [!NOTE]
> <span data-ttu-id="44396-104">您必須是電腦的系統管理員，才能執行下列任何一項工作。</span><span class="sxs-lookup"><span data-stu-id="44396-104">You must be an administrator on the machine to perform any of the following tasks.</span></span>

 <span data-ttu-id="44396-105">在 Windows 7 電腦上使用 ComSvcConfig.exe 設定 Web 服務以使用最新的服務模型版本 (目前為 4.5 版) 時，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="44396-105">When using ComSvcConfig.exe on a Windows 7 machine to configure a web service to use the latest service model version (currently v4.5), perform the following steps:</span></span>

1. <span data-ttu-id="44396-106">將登錄機碼設定  `[HKEY_LOCAL_COMPUTER\SOFTWARE\Microsoft\.NETFramework]\OnlyUseLatestCLR` 為 DWORD 值0x00000001</span><span class="sxs-lookup"><span data-stu-id="44396-106">Set the registry key  `[HKEY_LOCAL_COMPUTER\SOFTWARE\Microsoft\.NETFramework]\OnlyUseLatestCLR` to a DWORD value of 0x00000001</span></span>

2. <span data-ttu-id="44396-107">執行 comsvcconfig.exe</span><span class="sxs-lookup"><span data-stu-id="44396-107">Run comsvcconfig.exe</span></span>

3. <span data-ttu-id="44396-108">將步驟 1 新增的登錄機碼還原成其原始值，或將它刪除 (如果不存在的話)。</span><span class="sxs-lookup"><span data-stu-id="44396-108">Revert the registry key added in step 1 back to its original value, or delete it if did not exist.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44396-109">將這個登錄機碼還原是非常重要的步驟。</span><span class="sxs-lookup"><span data-stu-id="44396-109">Reverting this registry key is important.</span></span> <span data-ttu-id="44396-110">此為相容性的關鍵。</span><span class="sxs-lookup"><span data-stu-id="44396-110">This is a compatibility key.</span></span> <span data-ttu-id="44396-111">未還原這項變更可能會導致在電腦上執行的其他 .NET 應用程式發生問題)。</span><span class="sxs-lookup"><span data-stu-id="44396-111">Not reverting this change may cause issues with other .NET applications running on the machine).</span></span>

> [!WARNING]
> <span data-ttu-id="44396-112">在 Windows 8 電腦上使用 ComSvcConfig.exe/install 時，會顯示一個對話方塊，指出「您電腦上的應用程式需要下列 Windows 功能： .NET Framework 3.5 (包括 .NET 2.0 和 .NET 3.0」（如果未安裝 .NET Framework 3.5）。</span><span class="sxs-lookup"><span data-stu-id="44396-112">When using ComSvcConfig.exe  /install on a Windows 8 machine, a dialog is displayed stating "An app on your PC needs the following Windows feature: .NET Framework 3.5 (includes .NET 2.0 and .NET 3.0" if .NET Framework 3.5 is not installed.</span></span> <span data-ttu-id="44396-113">您可以忽略這個對話方塊，</span><span class="sxs-lookup"><span data-stu-id="44396-113">This dialog may be ignored.</span></span> <span data-ttu-id="44396-114">也可以將 OnlyUseLatestCLR 登錄機碼設定為 DWORD 值 (0x00000001)</span><span class="sxs-lookup"><span data-stu-id="44396-114">Alternatively you can sed the OnlyUseLatestCLR registry key to a DWORD value of 0x00000001</span></span>

## <a name="add-an-interface-using-the-com-hosting-mode"></a><span data-ttu-id="44396-115">使用 COM + 裝載模式加入介面</span><span class="sxs-lookup"><span data-stu-id="44396-115">Add an interface using the COM+ hosting mode</span></span>

- <span data-ttu-id="44396-116">請使用 `/install` 和 `/hosting:complus` 選項來執行 ComSvcConfig，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="44396-116">Run ComSvcConfig using the `/install` and `/hosting:complus` options, as shown in the following example.</span></span>

    ```console
    ComSvcConfig.exe /install /application:OnlineStore /contract:ItemOrders.Financial,IFinances /hosting:complus /verbose
    ```

     <span data-ttu-id="44396-117">此命令會將 `IFinances` 元件的 `ItemOrders.IFinancial` 介面 (來自 OnlineStore COM+ 應用程式) 新增到即將公開為 Web 服務的介面集合。</span><span class="sxs-lookup"><span data-stu-id="44396-117">The command adds the `IFinances` interface of the `ItemOrders.IFinancial` component (from the OnlineStore COM+ application) to the set of interfaces that will be exposed as Web services.</span></span> <span data-ttu-id="44396-118">服務將使用 COM+ 裝載模式，因此需要明確的應用程式啟動。</span><span class="sxs-lookup"><span data-stu-id="44396-118">The service uses the COM+ hosting mode and therefore requires explicit application activation.</span></span>

     <span data-ttu-id="44396-119">雖然萬用字元星號 (\*) 字元可以用於元件和介面，但請避免使用它，因為您可能只想要將選取的功能公開為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="44396-119">While the wildcard asterisk (\*) character can be used for the component and the interface, avoid using it because you might want to expose only selected functionality as a Web service.</span></span> <span data-ttu-id="44396-120">如果與此元件的未來版本一起執行，使用萬用字元會不小心將決定組態語法時尚不存在的介面一併公開出來。</span><span class="sxs-lookup"><span data-stu-id="44396-120">If run with a future version of this component, using the wildcard may unintentionally expose interfaces that may not have been present when the configuration syntax was determined.</span></span>

     <span data-ttu-id="44396-121">/verbose 選項會指示工具在任何錯誤旁邊加上警告。</span><span class="sxs-lookup"><span data-stu-id="44396-121">The /verbose option instructs the tool to display warnings in addition to any errors.</span></span>

     <span data-ttu-id="44396-122">公開服務的合約將包含來自 `IFinances` 介面的所有方法。</span><span class="sxs-lookup"><span data-stu-id="44396-122">The contract for the exposed service will contain all of the methods from the `IFinances` interface.</span></span>

## <a name="add-specific-methods-from-an-interface-using-the-com-hosting-mode"></a><span data-ttu-id="44396-123">使用 COM + 裝載模式從介面新增特定方法</span><span class="sxs-lookup"><span data-stu-id="44396-123">Add specific methods from an interface using the COM+ hosting mode</span></span>

- <span data-ttu-id="44396-124">請使用包含必要方法之明確命名的 `/install` 和 `/hosting:complus` 選項來執行 ComSvcConfig，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="44396-124">Run ComSvcConfig using the `/install` and `/hosting:complus` options with explicit naming of the required methods, as shown in the following example.</span></span>

    ```console
    ComSvcConfig.exe /install /application:OnlineStore /contract:ItemOrders.Financial,IFinances.{Credit,Debit} /hosting:complus /verbose
    ```

     <span data-ttu-id="44396-125">此命令只會將來自 `Credit` 介面的 `Debit` 和 `IFinances` 方法當成作業新增至公開的服務合約中。</span><span class="sxs-lookup"><span data-stu-id="44396-125">The command adds only the `Credit` and `Debit` methods from the `IFinances` interface as operations to the exposed service contract.</span></span> <span data-ttu-id="44396-126">介面上的其他所有方法都會從合約中省略，而且無法透過 Web 服務用戶端來呼叫。</span><span class="sxs-lookup"><span data-stu-id="44396-126">All other methods on the interface will be omitted from the contract and will not be callable from Web service clients.</span></span>

## <a name="add-an-interface-using-the-web-hosting-mode"></a><span data-ttu-id="44396-127">使用虛擬主機模式新增介面</span><span class="sxs-lookup"><span data-stu-id="44396-127">Add an interface using the Web hosting mode</span></span>

- <span data-ttu-id="44396-128">請使用 `/install` 選項和 `/hosting:was` 選項來執行 ComSvcConfig，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="44396-128">Run ComSvcConfig using the `/install` option and the `/hosting:was` option, as shown in the following example.</span></span>

    ```console
    ComSvcConfig.exe /install /application:OnlineWarehouse /contract:ItemInventory.Warehouse,IStockLevels /hosting:was /webDirectory:root/OnlineWarehouse /mex /verbose
    ```

     <span data-ttu-id="44396-129">此命令會將 `IStockLevels` 元件上的 `ItemInventory.Warehouse` 介面 (來自 OnlineWarehouse COM+ 應用程式) 新增至即將公開為 Web 服務的介面集合。</span><span class="sxs-lookup"><span data-stu-id="44396-129">The command adds the `IStockLevels` interface on the `ItemInventory.Warehouse` component (from the OnlineWarehouse COM+ application) to the set of interfaces that will be exposed as Web services.</span></span> <span data-ttu-id="44396-130">此服務是由 Web 裝載到 IIS (而不是 COM+) 的 OnlineWarehouse 虛擬目錄，因此必要時會自動啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="44396-130">The service is Web hosted in the OnlineWarehouse virtual directory of IIS rather than in COM+, and thus the application is automatically activated as required.</span></span>

     <span data-ttu-id="44396-131">若要使用 Web 裝載的同處理序組態，必須將 COM+ 應用程式設定為透過元件服務系統管理主控台，並以程式庫應用程式身分，而不是以伺服器應用程式身分來執行。</span><span class="sxs-lookup"><span data-stu-id="44396-131">To use the Web-hosted in-process configuration, the COM+ application must be configured to run as a Library application rather than a Server application using the Component Services administration console.</span></span> <span data-ttu-id="44396-132">設定為伺服器應用程式身分的應用程式會使用標準 Web 裝載模式，並產生處理序躍點來處理每項要求。</span><span class="sxs-lookup"><span data-stu-id="44396-132">Applications configured as Server applications use the standard Web-hosted mode and incur a process hop to process each request.</span></span>

     <span data-ttu-id="44396-133">`/mex` 選項會新增使用相同傳輸的額外中繼資料交換 (MEX) 服務做為應用程式服務端點，以支援想要從服務中擷取合約定義的用戶端。</span><span class="sxs-lookup"><span data-stu-id="44396-133">The `/mex` option adds an additional Metadata Exchange (MEX) service endpoint that uses the same transport as the application's service endpoint to support clients that want to retrieve a contract definition from the service.</span></span>

## <a name="remove-a-web-service-for-a-specified-interface"></a><span data-ttu-id="44396-134">移除指定之介面的 Web 服務</span><span class="sxs-lookup"><span data-stu-id="44396-134">Remove a Web service for a specified interface</span></span>

- <span data-ttu-id="44396-135">請使用 `/uninstall` 選項來執行 ComSvcConfig，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="44396-135">Run ComSvcConfig using the `/uninstall` option, as shown in the following example.</span></span>

    ```console
    ComSvcConfig.exe /uninstall /application:OnlineStore /contract:ItemOrders.Financial,IFinances /hosting:complus
    ```

     <span data-ttu-id="44396-136">此命令會移除 `IFinances` 元件的 `ItemOrders.Financial` 介面 (來自 OnlineStore COM+ 應用程式)。</span><span class="sxs-lookup"><span data-stu-id="44396-136">The command removes the `IFinances` interface on the `ItemOrders.Financial` component (from the OnlineStore COM+ application).</span></span>

## <a name="list-currently-exposed-interfaces"></a><span data-ttu-id="44396-137">列出目前公開的介面</span><span class="sxs-lookup"><span data-stu-id="44396-137">List currently exposed interfaces</span></span>

- <span data-ttu-id="44396-138">請使用 `/list` 選項來執行 ComSvcConfig，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="44396-138">Run ComSvcConfig using the `/list` option, as shown in the following example.</span></span>

    ```console
    ComSvcConfig.exe /list
    ```

     <span data-ttu-id="44396-139">此命令會列出限定於本機電腦範圍內，目前公開的介面以及對應的位址與繫結詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="44396-139">The command lists the currently exposed interfaces, along with the corresponding address and binding details, scoped to the local machine.</span></span>

## <a name="list-specific-currently-exposed-interfaces"></a><span data-ttu-id="44396-140">列出特定目前公開的介面</span><span class="sxs-lookup"><span data-stu-id="44396-140">List specific currently exposed interfaces</span></span>

- <span data-ttu-id="44396-141">請使用 `/list` 選項來執行 ComSvcConfig，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="44396-141">Run ComSvcConfig using the `/list` option, as shown in the following example.</span></span>

    ```console
    ComSvcConfig.exe /list /application:OnlineStore /hosting:complus
    ```

     <span data-ttu-id="44396-142">此命令會列出本機電腦上 OnlineStore COM+ 應用程式目前公開的 COM+ 裝載介面，以及對應的位址與繫結詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="44396-142">The command lists currently exposed COM+-hosted interfaces, along with the corresponding address and binding details, for the OnlineStore COM+ application on the local machine.</span></span>

## <a name="display-help-for-options"></a><span data-ttu-id="44396-143">顯示選項的說明</span><span class="sxs-lookup"><span data-stu-id="44396-143">Display help for options</span></span>

- <span data-ttu-id="44396-144">請使用 /? 選項來執行 ComSvcConfig，</span><span class="sxs-lookup"><span data-stu-id="44396-144">Run ComSvcConfig using the /?</span></span> <span data-ttu-id="44396-145">如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="44396-145">option, as shown in the following example.</span></span>

    ```console
    ComSvcConfig.exe /?
    ```

## <a name="see-also"></a><span data-ttu-id="44396-146">另請參閱</span><span class="sxs-lookup"><span data-stu-id="44396-146">See also</span></span>

- [<span data-ttu-id="44396-147">與 COM + 應用程式整合總覽</span><span class="sxs-lookup"><span data-stu-id="44396-147">Integrating with COM+ Applications Overview</span></span>](integrating-with-com-plus-applications-overview.md)
