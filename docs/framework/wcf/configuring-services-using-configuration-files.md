---
title: 使用組態檔設定服務
description: 瞭解 WCF 服務的設定檔如何讓您在部署期間提供端點和服務行為資料的彈性。
ms.date: 03/30/2017
helpviewer_keywords:
- configuring services [WCF]
ms.assetid: c9c8cd32-2c9d-4541-ad0d-16dff6bd2a00
ms.openlocfilehash: 25a6891564054878e7bdf7f43d431547ea1dee6c
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96253345"
---
# <a name="configuring-services-using-configuration-files"></a><span data-ttu-id="2cc19-103">使用組態檔設定服務</span><span class="sxs-lookup"><span data-stu-id="2cc19-103">Configuring Services Using Configuration Files</span></span>

<span data-ttu-id="2cc19-104">使用設定檔設定 Windows Communication Foundation (WCF) 服務，可讓您在部署時提供端點和服務行為資料的彈性，而不是在設計階段提供。</span><span class="sxs-lookup"><span data-stu-id="2cc19-104">Configuring a Windows Communication Foundation (WCF) service with a configuration file gives you the flexibility of providing endpoint and service behavior data at the point of deployment instead of at design time.</span></span> <span data-ttu-id="2cc19-105">本主題概要說明可用的主要技巧。</span><span class="sxs-lookup"><span data-stu-id="2cc19-105">This topic outlines the primary techniques available.</span></span>  
  
 <span data-ttu-id="2cc19-106">WCF 服務可使用 .NET Framework 設定技術來設定。</span><span class="sxs-lookup"><span data-stu-id="2cc19-106">A WCF service is configurable using the .NET Framework configuration technology.</span></span> <span data-ttu-id="2cc19-107">最常見的 XML 元素會加入至裝載 WCF 服務的 Internet Information Services (IIS) 網站的 Web.config 檔案中。</span><span class="sxs-lookup"><span data-stu-id="2cc19-107">Most commonly, XML elements are added to the Web.config file for an Internet Information Services (IIS) site that hosts a WCF service.</span></span> <span data-ttu-id="2cc19-108">這些項目允許您變更詳細資料，例如各電腦的端點位址 (用於與服務通訊的實際位址)。</span><span class="sxs-lookup"><span data-stu-id="2cc19-108">The elements allow you to change details such as the endpoint addresses (the actual addresses used to communicate with the service) on a machine-by-machine basis.</span></span> <span data-ttu-id="2cc19-109">此外，WCF 還包含數個系統提供的元素，可讓您快速選取服務的最基本功能。</span><span class="sxs-lookup"><span data-stu-id="2cc19-109">In addition, WCF includes several system-provided elements that allow you to quickly select the most basic features for a service.</span></span> <span data-ttu-id="2cc19-110">從 .NET Framework 4 開始，WCF 隨附新的預設設定模型，可簡化 WCF 設定需求。</span><span class="sxs-lookup"><span data-stu-id="2cc19-110">Starting with .NET Framework 4, WCF comes with a new default configuration model that simplifies WCF configuration requirements.</span></span> <span data-ttu-id="2cc19-111">如果您沒有為特定服務提供任何 WCF 設定，則執行時間會自動使用一些標準端點和預設系結/行為來設定您的服務。</span><span class="sxs-lookup"><span data-stu-id="2cc19-111">If you do not provide any WCF configuration for a particular service, the runtime automatically configures your service with some standard endpoints and default binding/behavior.</span></span> <span data-ttu-id="2cc19-112">在實務上，撰寫設定是 WCF 應用程式程式設計的主要部分。</span><span class="sxs-lookup"><span data-stu-id="2cc19-112">In practice, writing configuration is a major part of programming WCF applications.</span></span>  
  
 <span data-ttu-id="2cc19-113">如需詳細資訊，請參閱設定 [服務的](configuring-bindings-for-wcf-services.md)系結。</span><span class="sxs-lookup"><span data-stu-id="2cc19-113">For more information, see [Configuring Bindings for Services](configuring-bindings-for-wcf-services.md).</span></span> <span data-ttu-id="2cc19-114">如需最常使用的元素清單，請參閱 [系統提供](system-provided-bindings.md)的系結。</span><span class="sxs-lookup"><span data-stu-id="2cc19-114">For a list of the most commonly used elements, see [System-Provided Bindings](system-provided-bindings.md).</span></span> <span data-ttu-id="2cc19-115">如需預設端點、繫結和行為的詳細資訊，請參閱[簡化的組態](simplified-configuration.md)和 [WCF 服務的簡化組態](./samples/simplified-configuration-for-wcf-services.md)。</span><span class="sxs-lookup"><span data-stu-id="2cc19-115">For more information about default endpoints, bindings, and behaviors, see [Simplified Configuration](simplified-configuration.md) and [Simplified Configuration for WCF Services](./samples/simplified-configuration-for-wcf-services.md).</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="2cc19-116">部署並存案例時，如果部署了兩個不同的服務版本，您就必須指定組態檔所參考之組件的部分名稱。</span><span class="sxs-lookup"><span data-stu-id="2cc19-116">When deploying side by side scenarios where two different versions of a service are deployed, it is necessary to specify partial names of assemblies referenced in configuration files.</span></span> <span data-ttu-id="2cc19-117">這是因為組態檔會在所有服務版本之間共用，而且它們可能會在不同的 .NET Framework 版本底下執行。</span><span class="sxs-lookup"><span data-stu-id="2cc19-117">This is because the configuration file is shared across all versions of a service and they could be running under different versions of the .NET Framework.</span></span>  
  
## <a name="systemconfiguration-webconfig-and-appconfig"></a><span data-ttu-id="2cc19-118">System.Configuration：Web.config 和 App.config</span><span class="sxs-lookup"><span data-stu-id="2cc19-118">System.Configuration: Web.config and App.config</span></span>  

 <span data-ttu-id="2cc19-119">WCF 會使用 .NET Framework 的 System.Configuration 設定系統。</span><span class="sxs-lookup"><span data-stu-id="2cc19-119">WCF uses the System.Configuration configuration system of the .NET Framework.</span></span>  
  
 <span data-ttu-id="2cc19-120">在 Visual Studio 中設定服務時，請使用 Web.config 檔或 App.config 檔來指定設定。</span><span class="sxs-lookup"><span data-stu-id="2cc19-120">When configuring a service in Visual Studio, use either a Web.config file or an App.config file to specify the settings.</span></span> <span data-ttu-id="2cc19-121">組態檔名稱的選擇取決於您為服務選擇的裝載環境。</span><span class="sxs-lookup"><span data-stu-id="2cc19-121">The choice of the configuration file name is determined by the hosting environment you choose for the service.</span></span> <span data-ttu-id="2cc19-122">如果您選擇使用 IIS 來裝載服務，請使用 Web.config 檔。</span><span class="sxs-lookup"><span data-stu-id="2cc19-122">If you are using IIS to host your service, use a Web.config file.</span></span> <span data-ttu-id="2cc19-123">如果您使用其他任何裝載環境，請使用 App.config 檔。</span><span class="sxs-lookup"><span data-stu-id="2cc19-123">If you are using any other hosting environment, use an App.config file.</span></span>  
  
 <span data-ttu-id="2cc19-124">在 Visual Studio 中，會使用名為 App.config 的檔案來建立最終的設定檔。</span><span class="sxs-lookup"><span data-stu-id="2cc19-124">In Visual Studio, the file named App.config is used to create the final configuration file.</span></span> <span data-ttu-id="2cc19-125">最後實際使用的組態名稱取決於組件名稱。</span><span class="sxs-lookup"><span data-stu-id="2cc19-125">The final name actually used for the configuration depends on the assembly name.</span></span> <span data-ttu-id="2cc19-126">例如，名為 "Cohowinery.exe" 的組件，其最後的組態檔名為 "Cohowinery.exe.config"。</span><span class="sxs-lookup"><span data-stu-id="2cc19-126">For example, an assembly named "Cohowinery.exe" has a final configuration file name of "Cohowinery.exe.config".</span></span> <span data-ttu-id="2cc19-127">但是，您只需要修改 App.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="2cc19-127">However, you only need to modify the App.config file.</span></span> <span data-ttu-id="2cc19-128">對該檔案進行的變更，會在編譯階段自動套用至最後的應用程式組態檔中。</span><span class="sxs-lookup"><span data-stu-id="2cc19-128">Changes made to that file are automatically made to the final application configuration file at compile time.</span></span>  
  
 <span data-ttu-id="2cc19-129">在使用 App.config 檔案時，一旦應用程式啟動且套用了組態，組態系統會將 App.config 檔案與 Machine.config 檔案的內容合併。</span><span class="sxs-lookup"><span data-stu-id="2cc19-129">In using an App.config, file the configuration system merges the App.config file with content of the Machine.config file when the application starts and the configuration is applied.</span></span> <span data-ttu-id="2cc19-130">這項機制可讓您透過 Machine.config 檔案來設定整部電腦。</span><span class="sxs-lookup"><span data-stu-id="2cc19-130">This mechanism allows machine-wide settings to be defined in the Machine.config file.</span></span> <span data-ttu-id="2cc19-131">App.config 檔案可以用來覆寫 Machine.config 檔案的設定，您也可以鎖定 Machine.config 檔案的設定以便加以取用。</span><span class="sxs-lookup"><span data-stu-id="2cc19-131">The App.config file can be used to override the settings of the Machine.config file; you can also lock in the settings in Machine.config file so that they get used.</span></span> <span data-ttu-id="2cc19-132">在 Web.config 情況中，組態系統會將所有目錄乃至應用程式目錄中的 Web.config 檔案合併至已套用的組態。</span><span class="sxs-lookup"><span data-stu-id="2cc19-132">In the Web.config case, the configuration system merges the Web.config files in all directories leading up to the application directory into the configuration that gets applied.</span></span> <span data-ttu-id="2cc19-133">如需設定和設定優先順序的詳細資訊，請參閱命名空間中的主題 <xref:System.Configuration> 。</span><span class="sxs-lookup"><span data-stu-id="2cc19-133">For more information about configuration and the setting priorities, see topics in the <xref:System.Configuration> namespace.</span></span>  
  
## <a name="major-sections-of-the-configuration-file"></a><span data-ttu-id="2cc19-134">組態檔的主要區段</span><span class="sxs-lookup"><span data-stu-id="2cc19-134">Major Sections of the Configuration File</span></span>  

 <span data-ttu-id="2cc19-135">組態檔的主要區段包含下列項目。</span><span class="sxs-lookup"><span data-stu-id="2cc19-135">The main sections in the configuration file include the following elements.</span></span>  
  
```xml  
<system.ServiceModel>  
  
   <services>  
   <!-- Define the service endpoints. This section is optional in the new  
    default configuration model in .NET Framework 4. -->  
      <service>  
         <endpoint/>  
      </service>  
   </services>  
  
   <bindings>  
   <!-- Specify one or more of the system-provided binding elements,  
    for example, <basicHttpBinding> -->
   <!-- Alternatively, <customBinding> elements. -->  
      <binding>  
      <!-- For example, a <BasicHttpBinding> element. -->  
      </binding>  
   </bindings>  
  
   <behaviors>  
   <!-- One or more of the system-provided or custom behavior elements. -->  
      <behavior>  
      <!-- For example, a <throttling> element. -->  
      </behavior>  
   </behaviors>  
  
</system.ServiceModel>  
```  
  
> [!NOTE]
> <span data-ttu-id="2cc19-136">繫結和行為區段都是選用的，而且只會在必要時才納入。</span><span class="sxs-lookup"><span data-stu-id="2cc19-136">The bindings and behaviors sections are optional and are only included if required.</span></span>  
  
### <a name="the-services-element"></a><span data-ttu-id="2cc19-137">\<services>元素</span><span class="sxs-lookup"><span data-stu-id="2cc19-137">The \<services> Element</span></span>  

 <span data-ttu-id="2cc19-138">`services` 項目包含所有由應用程式裝載的服務規格。</span><span class="sxs-lookup"><span data-stu-id="2cc19-138">The `services` element contains the specifications for all services the application hosts.</span></span> <span data-ttu-id="2cc19-139">從 .NET Framework 4 的簡化設定模型開始，此區段是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="2cc19-139">Starting with the simplified configuration model in .NET Framework 4, this section is optional.</span></span>  
  
 [\<services>](../configure-apps/file-schema/wcf/services.md)  
  
### <a name="the-service-element"></a><span data-ttu-id="2cc19-140">\<service>元素</span><span class="sxs-lookup"><span data-stu-id="2cc19-140">The \<service> Element</span></span>  

 <span data-ttu-id="2cc19-141">每項服務都有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="2cc19-141">Each service has these attributes:</span></span>  
  
- <span data-ttu-id="2cc19-142">`name`.</span><span class="sxs-lookup"><span data-stu-id="2cc19-142">`name`.</span></span> <span data-ttu-id="2cc19-143">指定用來提供服務合約實作的型別。</span><span class="sxs-lookup"><span data-stu-id="2cc19-143">Specifies the type that provides an implementation of a service contract.</span></span> <span data-ttu-id="2cc19-144">這是由命名空間、句號和型別名稱組成的完整名稱。</span><span class="sxs-lookup"><span data-stu-id="2cc19-144">This is a fully qualified name which consists of the namespace, a period, and then the type name.</span></span> <span data-ttu-id="2cc19-145">例如 `"MyNameSpace.myServiceType"` 。</span><span class="sxs-lookup"><span data-stu-id="2cc19-145">For example `"MyNameSpace.myServiceType"`.</span></span>  
  
- <span data-ttu-id="2cc19-146">`behaviorConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="2cc19-146">`behaviorConfiguration`.</span></span> <span data-ttu-id="2cc19-147">指定在 `behavior` 項目中找到的其中一個 `behaviors` 項目名稱。</span><span class="sxs-lookup"><span data-stu-id="2cc19-147">Specifies the name of one of the `behavior` elements found in the `behaviors` element.</span></span> <span data-ttu-id="2cc19-148">指定的行為會掌管服務是否允許模擬之類的動作。</span><span class="sxs-lookup"><span data-stu-id="2cc19-148">The specified behavior governs actions such as whether the service allows impersonation.</span></span> <span data-ttu-id="2cc19-149">如果其值為空白名稱或未提供 `behaviorConfiguration` ，則會將一組預設的服務行為加入至服務。</span><span class="sxs-lookup"><span data-stu-id="2cc19-149">If its value is the empty name or no `behaviorConfiguration` is provided then the default set of service behaviors is added to the service.</span></span>  
  
- [\<service>](../configure-apps/file-schema/wcf/service.md)  
  
### <a name="the-endpoint-element"></a><span data-ttu-id="2cc19-150">\<endpoint>元素</span><span class="sxs-lookup"><span data-stu-id="2cc19-150">The \<endpoint> Element</span></span>  

 <span data-ttu-id="2cc19-151">每個端點都需要下列屬性代表的位址、繫結和合約：</span><span class="sxs-lookup"><span data-stu-id="2cc19-151">Each endpoint requires an address, a binding, and a contract, which are represented by the following attributes:</span></span>  
  
- <span data-ttu-id="2cc19-152">`address`.</span><span class="sxs-lookup"><span data-stu-id="2cc19-152">`address`.</span></span> <span data-ttu-id="2cc19-153">指定服務的統一資源識別元 (URI)，此識別元可以是絕對位址，或是相對於服務基底位址的相對位址。</span><span class="sxs-lookup"><span data-stu-id="2cc19-153">Specifies the service's Uniform Resource Identifier (URI), which can be an absolute address or one that is given relative to the base address of the service.</span></span> <span data-ttu-id="2cc19-154">如果設為空字串，則代表在建立服務的 <xref:System.ServiceModel.ServiceHost> 時，指定的基底位址將有可用的端點。</span><span class="sxs-lookup"><span data-stu-id="2cc19-154">If set to an empty string, it indicates that the endpoint is available at the base address that is specified when creating the <xref:System.ServiceModel.ServiceHost> for the service.</span></span>  
  
- <span data-ttu-id="2cc19-155">`binding`.</span><span class="sxs-lookup"><span data-stu-id="2cc19-155">`binding`.</span></span> <span data-ttu-id="2cc19-156">一般來說，會指定系統提供的繫結，例如 <xref:System.ServiceModel.WSHttpBinding>，但是也可以指定使用者定義的繫結。</span><span class="sxs-lookup"><span data-stu-id="2cc19-156">Typically specifies a system-provided binding like <xref:System.ServiceModel.WSHttpBinding>, but can also specify a user-defined binding.</span></span> <span data-ttu-id="2cc19-157">指定的繫結會決定使用的傳輸類型、安全性和編碼，以及是否支援或啟用可靠工作階段、交易或資料流處理。</span><span class="sxs-lookup"><span data-stu-id="2cc19-157">The binding specified determines the type of transport, security and encoding used, and whether reliable sessions, transactions, or streaming is supported or enabled.</span></span>  
  
- <span data-ttu-id="2cc19-158">`bindingConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="2cc19-158">`bindingConfiguration`.</span></span> <span data-ttu-id="2cc19-159">如果必須修改預設的繫結值，可以藉由設定 `binding` 項目中的適當 `bindings` 項目來達成。</span><span class="sxs-lookup"><span data-stu-id="2cc19-159">If the default values of a binding must be modified, this can be done by configuring the appropriate `binding` element in the `bindings` element.</span></span> <span data-ttu-id="2cc19-160">此屬性應該被賦予與用來變更預設值時所用的 `name` 項目的 `binding` 屬性相同的值。</span><span class="sxs-lookup"><span data-stu-id="2cc19-160">This attribute should be given the same value as the `name` attribute of the `binding` element that is used to change the defaults.</span></span> <span data-ttu-id="2cc19-161">如果未指定名稱或在繫結中未指定 `bindingConfiguration` ，則會將繫結型別的預設繫結用於端點。</span><span class="sxs-lookup"><span data-stu-id="2cc19-161">If no name is given, or no `bindingConfiguration` is specified in the binding, then the default binding of the binding type is used in the endpoint.</span></span>  
  
- <span data-ttu-id="2cc19-162">`contract`.</span><span class="sxs-lookup"><span data-stu-id="2cc19-162">`contract`.</span></span> <span data-ttu-id="2cc19-163">指定可定義合約的介面。</span><span class="sxs-lookup"><span data-stu-id="2cc19-163">Specifies the interface that defines the contract.</span></span> <span data-ttu-id="2cc19-164">這個介面是由 `name` 項目的 `service` 屬性所指定的 Common Language Runtime (CLR) 型別所實作。</span><span class="sxs-lookup"><span data-stu-id="2cc19-164">This is the interface implemented in the common language runtime (CLR) type specified by the `name` attribute of the `service` element.</span></span>  
  
- [\<endpoint>](../configure-apps/file-schema/wcf/endpoint-element.md)  
  
### <a name="the-bindings-element"></a><span data-ttu-id="2cc19-165">\<bindings>元素</span><span class="sxs-lookup"><span data-stu-id="2cc19-165">The \<bindings> Element</span></span>  

 <span data-ttu-id="2cc19-166">`bindings` 項目包含所有繫結的規格，在任何服務中定義的任何端點都可以使用這些繫結。</span><span class="sxs-lookup"><span data-stu-id="2cc19-166">The `bindings` element contains the specifications for all bindings that can be used by any endpoint defined in any service.</span></span>  
  
 [\<bindings>](../configure-apps/file-schema/wcf/bindings.md)  
  
### <a name="the-binding-element"></a><span data-ttu-id="2cc19-167">\<binding>元素</span><span class="sxs-lookup"><span data-stu-id="2cc19-167">The \<binding> Element</span></span>  

 <span data-ttu-id="2cc19-168">專案 `binding` 中包含的專案 `bindings` 可以是系統提供的系結之一 (請參閱 [系統提供](system-provided-bindings.md) 的系結) 或自訂系結 (查看) 的 [自訂](./extending/custom-bindings.md) 系結。</span><span class="sxs-lookup"><span data-stu-id="2cc19-168">The `binding` elements contained in the `bindings` element can be either one of the system-provided bindings (see [System-Provided Bindings](system-provided-bindings.md)) or a custom binding (see [Custom Bindings](./extending/custom-bindings.md)).</span></span> <span data-ttu-id="2cc19-169">`binding` 項目具有的 `name` 屬性可將繫結與 `bindingConfiguration` 項目的 `endpoint` 屬性所指定的端點相互關聯。</span><span class="sxs-lookup"><span data-stu-id="2cc19-169">The `binding` element has a `name` attribute that correlates the binding with the endpoint specified in the `bindingConfiguration` attribute of the `endpoint` element.</span></span> <span data-ttu-id="2cc19-170">如果未指定名稱，則該繫結會對應於該繫結型別的預設值。</span><span class="sxs-lookup"><span data-stu-id="2cc19-170">If no name is specified then that binding corresponds to the default of that binding type.</span></span>  
  
<span data-ttu-id="2cc19-171">如需設定服務和用戶端的詳細資訊，請參閱設定 [WCF 服務](configuring-services.md)。</span><span class="sxs-lookup"><span data-stu-id="2cc19-171">For more information about configuring services and clients, see [Configuring WCF services](configuring-services.md).</span></span>
  
 [\<binding>](../configure-apps/file-schema/wcf/bindings.md)  
  
### <a name="the-behaviors-element"></a><span data-ttu-id="2cc19-172">\<behaviors>元素</span><span class="sxs-lookup"><span data-stu-id="2cc19-172">The \<behaviors> Element</span></span>  

 <span data-ttu-id="2cc19-173">這是定義服務行為之 `behavior` 項目的容器項目。</span><span class="sxs-lookup"><span data-stu-id="2cc19-173">This is a container element for the `behavior` elements that define the behaviors for a service.</span></span>  
  
 [\<behaviors>](../configure-apps/file-schema/wcf/behaviors.md)  
  
### <a name="the-behavior-element"></a><span data-ttu-id="2cc19-174">\<behavior>元素</span><span class="sxs-lookup"><span data-stu-id="2cc19-174">The \<behavior> Element</span></span>  

 <span data-ttu-id="2cc19-175">每個 `behavior` 元素都是由 `name` 屬性識別，並提供系統提供的行為，例如 <`throttling`> 或自訂行為。</span><span class="sxs-lookup"><span data-stu-id="2cc19-175">Each `behavior` element is identified by a `name` attribute and provides either a system-provided behavior, such as <`throttling`>, or a custom behavior.</span></span> <span data-ttu-id="2cc19-176">如果未指定名稱，則該行為項目會對應於預設服務或端點行為。</span><span class="sxs-lookup"><span data-stu-id="2cc19-176">If no name is given then that behavior element corresponds to the default service or endpoint behavior.</span></span>  
  
 [\<behavior>](../configure-apps/file-schema/wcf/behavior-of-servicebehaviors.md)  
  
## <a name="how-to-use-binding-and-behavior-configurations"></a><span data-ttu-id="2cc19-177">如何使用繫結與行為組態</span><span class="sxs-lookup"><span data-stu-id="2cc19-177">How to Use Binding and Behavior Configurations</span></span>  

 <span data-ttu-id="2cc19-178">WCF 可讓您輕鬆地使用設定中的參考系統，在端點之間共用設定。</span><span class="sxs-lookup"><span data-stu-id="2cc19-178">WCF makes it easy to share configurations between endpoints using a reference system in configuration.</span></span> <span data-ttu-id="2cc19-179">與其直接指派組態值給端點，繫結相關的組態值會被分類到 `bindingConfiguration` 區段的 `<binding>` 項目群組中。</span><span class="sxs-lookup"><span data-stu-id="2cc19-179">Rather than directly assigning configuration values to an endpoint, binding-related configuration values are grouped in `bindingConfiguration` elements in the `<binding>` section.</span></span> <span data-ttu-id="2cc19-180">一個繫結組態是繫結上的一個具名的設定群組。</span><span class="sxs-lookup"><span data-stu-id="2cc19-180">A binding configuration is a named group of settings on a binding.</span></span> <span data-ttu-id="2cc19-181">然後，端點可以依照名稱來參考 `bindingConfiguration` 。</span><span class="sxs-lookup"><span data-stu-id="2cc19-181">Endpoints can then reference the `bindingConfiguration` by name.</span></span>  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
 <system.serviceModel>  
  <bindings>  
    <basicHttpBinding>  
     <binding name="myBindingConfiguration1" closeTimeout="00:01:00" />  
     <binding name="myBindingConfiguration2" closeTimeout="00:02:00" />  
     <binding closeTimeout="00:03:00" />  <!-- Default binding for basicHttpBinding -->  
    </basicHttpBinding>  
     </bindings>  
     <services>  
      <service name="MyNamespace.myServiceType">  
       <endpoint
          address="myAddress" binding="basicHttpBinding"
          bindingConfiguration="myBindingConfiguration1"  
          contract="MyContract"  />  
       <endpoint
          address="myAddress2" binding="basicHttpBinding"
          bindingConfiguration="myBindingConfiguration2"  
          contract="MyContract" />  
       <endpoint
          address="myAddress3" binding="basicHttpBinding"
          contract="MyContract" />  
       </service>  
      </services>  
    </system.serviceModel>  
</configuration>  
```  
  
 <span data-ttu-id="2cc19-182">`name` 的 `bindingConfiguration` 會在 `<binding>` 項目中設定。</span><span class="sxs-lookup"><span data-stu-id="2cc19-182">The `name` of the `bindingConfiguration` is set in the `<binding>` element.</span></span> <span data-ttu-id="2cc19-183">`name`必須是系結型別範圍內的唯一字串，在此案例中是[<basicHttpBinding \> ](../configure-apps/file-schema/wcf/basichttpbinding.md)，或是參考預設系結的空值。</span><span class="sxs-lookup"><span data-stu-id="2cc19-183">The `name` must be a unique string within the scope of the binding type—in this case the [<basicHttpBinding\>](../configure-apps/file-schema/wcf/basichttpbinding.md), or an empty value to refer to the default binding.</span></span> <span data-ttu-id="2cc19-184">端點會將 `bindingConfiguration` 屬性設為此字串來連結至組態。</span><span class="sxs-lookup"><span data-stu-id="2cc19-184">The endpoint links to the configuration by setting the `bindingConfiguration` attribute to this string.</span></span>  
  
 <span data-ttu-id="2cc19-185">如下列範例所示， `behaviorConfiguration` 也是以同樣方式來實作。</span><span class="sxs-lookup"><span data-stu-id="2cc19-185">A `behaviorConfiguration` is implemented the same way, as illustrated in the following sample.</span></span>  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <endpointBehaviors>  
        <behavior name="myBehavior">  
           <callbackDebug includeExceptionDetailInFaults="true" />  
         </behavior>  
      </endpointBehaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="true" />  
        </behavior>  
      </serviceBehaviors>  
  
    </behaviors>  
    <services>  
     <service name="NewServiceType">  
       <endpoint
          address="myAddress3" behaviorConfiguration="myBehavior"  
          binding="basicHttpBinding"  
          contract="MyContract" />  
      </service>  
    </services>  
   </system.serviceModel>  
</configuration>  
```  
  
 <span data-ttu-id="2cc19-186">請注意，預設的服務行為集合會加入至服務。</span><span class="sxs-lookup"><span data-stu-id="2cc19-186">Note that the default set of service behaviors are added to the service.</span></span> <span data-ttu-id="2cc19-187">此系統允許端點共用組態，而不用重新定義設定。</span><span class="sxs-lookup"><span data-stu-id="2cc19-187">This system allows endpoints to share common configurations without redefining the settings.</span></span> <span data-ttu-id="2cc19-188">如果需要全電腦範圍，請在 Machine.config 中建立系結或行為設定。所有 App.config 檔案都可使用這些設定。</span><span class="sxs-lookup"><span data-stu-id="2cc19-188">If machine-wide scope is required, create the binding or behavior configuration in Machine.config. The configuration settings are available in all App.config files.</span></span> <span data-ttu-id="2cc19-189">[Configuration Editor Tool (SvcConfigEditor.exe)](configuration-editor-tool-svcconfigeditor-exe.md) 可讓您輕易地建立組態。</span><span class="sxs-lookup"><span data-stu-id="2cc19-189">The [Configuration Editor Tool (SvcConfigEditor.exe)](configuration-editor-tool-svcconfigeditor-exe.md) makes it easy to create configurations.</span></span>  
  
## <a name="behavior-merge"></a><span data-ttu-id="2cc19-190">行為合併</span><span class="sxs-lookup"><span data-stu-id="2cc19-190">Behavior Merge</span></span>  

 <span data-ttu-id="2cc19-191">當您想要以一致的方式使用一組通用行為時，行為合併功能可讓您輕鬆地管理行為。</span><span class="sxs-lookup"><span data-stu-id="2cc19-191">The behavior merge feature makes it easier to manage behaviors when you want a set of common behaviors to be used consistently.</span></span> <span data-ttu-id="2cc19-192">這項功能可讓您以不同的組態階層層級指定行為，並且讓服務從多個組態階層層級繼承行為。</span><span class="sxs-lookup"><span data-stu-id="2cc19-192">This feature allows you to specify behaviors at different levels of the configuration hierarchy and have services inherit behaviors from multiple levels of the configuration hierarchy.</span></span> <span data-ttu-id="2cc19-193">為了說明這項功能的運作方式，假設您在 IIS 中設有下列虛擬目錄配置：</span><span class="sxs-lookup"><span data-stu-id="2cc19-193">To illustrate how this works assume you have the following virtual directory layout in IIS:</span></span>  
  
 `~\Web.config~\Service.svc~\Child\Web.config~\Child\Service.svc`
  
 <span data-ttu-id="2cc19-194">檔案 `~\Web.config` 的內容如下：</span><span class="sxs-lookup"><span data-stu-id="2cc19-194">And your `~\Web.config` file has the following contents:</span></span>  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceDebug includeExceptionDetailInFaults="True" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
```  
  
 <span data-ttu-id="2cc19-195">而且，您有一個位於 ~\Child\Web.config 的子系 Web.config，其中包含下列內容：</span><span class="sxs-lookup"><span data-stu-id="2cc19-195">And you have a child Web.config located at ~\Child\Web.config with the following contents:</span></span>  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="True" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
```  
  
 <span data-ttu-id="2cc19-196">位於 ~\Child\Service.svc 的服務會表現成同時具有 serviceDebug 和 serviceMetadata 行為。</span><span class="sxs-lookup"><span data-stu-id="2cc19-196">The service located at ~\Child\Service.svc will behave as though it has both the serviceDebug and serviceMetadata behaviors.</span></span> <span data-ttu-id="2cc19-197">位於 ~\Service.svc 的服務則只有 serviceDebug 行為。</span><span class="sxs-lookup"><span data-stu-id="2cc19-197">The service located at ~\Service.svc will only have the serviceDebug behavior.</span></span> <span data-ttu-id="2cc19-198">結果是，系統會合併這兩個具有相同名稱的行為集合 (在本例中，名稱為空字串)。</span><span class="sxs-lookup"><span data-stu-id="2cc19-198">What happens is that the two behavior collections with the same name (in this case the empty string) are merged.</span></span>  
  
 <span data-ttu-id="2cc19-199">您也可以使用標記來清除行為集合 \<clear> ，並使用標記移除集合中的個別行為 \<remove> 。</span><span class="sxs-lookup"><span data-stu-id="2cc19-199">You can also clear behavior collections by using the \<clear> tag and removed individual behaviors from the collection by using the \<remove> tag.</span></span> <span data-ttu-id="2cc19-200">例如，下列兩個組態會產生只有 serviceMetadata 行為的子服務：</span><span class="sxs-lookup"><span data-stu-id="2cc19-200">For example, the following two configuration results in the child service having only the serviceMetadata behavior:</span></span>  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <remove name="serviceDebug"/>  
          <serviceMetadata httpGetEnabled="True" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
```  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <clear/>  
          <serviceMetadata httpGetEnabled="True" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
```  
  
 <span data-ttu-id="2cc19-201">系統會針對沒有名稱的行為集合 (如上所示) 以及具名的行為集合進行行為合併。</span><span class="sxs-lookup"><span data-stu-id="2cc19-201">Behavior merge is done for nameless behavior collections as shown above and named behavior collections as well.</span></span>  
  
 <span data-ttu-id="2cc19-202">行為合併適用于 IIS 裝載環境，其中 Web.config 檔案以階層方式與根 Web.config 檔和 machine.config 合併。但它也適用于應用程式環境，其中 machine.config 可以與 App.config 檔案合併。</span><span class="sxs-lookup"><span data-stu-id="2cc19-202">Behavior merge works in the IIS hosting environment, in which Web.config files merge hierarchically with the root Web.config file and machine.config. But it also works in the application environment, where machine.config can merge with the App.config file.</span></span>  
  
 <span data-ttu-id="2cc19-203">行為合併會同時套用至組態中的端點行為和服務行為。</span><span class="sxs-lookup"><span data-stu-id="2cc19-203">Behavior merge applies to both endpoint behaviors and service behaviors in configuration.</span></span>  
  
 <span data-ttu-id="2cc19-204">如果子行為集合包含已經存在父行為集合中的行為，子行為就會覆寫父代。</span><span class="sxs-lookup"><span data-stu-id="2cc19-204">If a child behavior collection contains a behavior that’s already present in the parent behavior collection, the child behavior overrides the parent.</span></span> <span data-ttu-id="2cc19-205">因此，如果父行為集合具有 `<serviceMetadata httpGetEnabled="False" />` 和子行為集合 `<serviceMetadata httpGetEnabled="True" />` ，子行為就會覆寫行為集合中的父行為，而 HTTPGetEnabled 會是 "true"。</span><span class="sxs-lookup"><span data-stu-id="2cc19-205">So if a parent behavior collection had `<serviceMetadata httpGetEnabled="False" />` and a child behavior collection had `<serviceMetadata httpGetEnabled="True" />`, the child behavior would override the parent behavior in the behavior collection and httpGetEnabled would be "true".</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="2cc19-206">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2cc19-206">See also</span></span>

- [<span data-ttu-id="2cc19-207">簡化的組態</span><span class="sxs-lookup"><span data-stu-id="2cc19-207">Simplified Configuration</span></span>](simplified-configuration.md)
- [<span data-ttu-id="2cc19-208">設定 WCF 服務</span><span class="sxs-lookup"><span data-stu-id="2cc19-208">Configuring WCF services</span></span>](configuring-services.md)
- [\<service>](../configure-apps/file-schema/wcf/service.md)
- [\<binding>](../configure-apps/file-schema/wcf/bindings.md)
