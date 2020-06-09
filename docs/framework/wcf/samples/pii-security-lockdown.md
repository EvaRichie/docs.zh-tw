---
title: PII 安全性鎖定
ms.date: 03/30/2017
ms.assetid: c44fb338-9527-4dd0-8607-b8787d15acb4
ms.openlocfilehash: 64c07825f0756b029781e173eb2098711cdbe60a
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600473"
---
# <a name="pii-security-lockdown"></a><span data-ttu-id="38311-102">PII 安全性鎖定</span><span class="sxs-lookup"><span data-stu-id="38311-102">PII Security Lockdown</span></span>
<span data-ttu-id="38311-103">這個範例會示範如何藉由下列方式，控制 Windows Communication Foundation （WCF）服務的數個安全性相關功能：</span><span class="sxs-lookup"><span data-stu-id="38311-103">This sample demonstrates how to control several security-related features of a Windows Communication Foundation (WCF) service by:</span></span>  
  
- <span data-ttu-id="38311-104">加密服務組態檔中的敏感性資訊。</span><span class="sxs-lookup"><span data-stu-id="38311-104">Encrypting sensitive information in a service's configuration file.</span></span>  
  
- <span data-ttu-id="38311-105">鎖定組態檔中的項目，讓巢狀服務子目錄無法覆寫設定。</span><span class="sxs-lookup"><span data-stu-id="38311-105">Locking elements in the configuration file so that nested service subdirectories cannot override settings.</span></span>  
  
- <span data-ttu-id="38311-106">控制追蹤和訊息記錄檔中個人可識別資訊 (PII) 的記錄。</span><span class="sxs-lookup"><span data-stu-id="38311-106">Controlling the logging of Personally Identifiable Information (PII) in trace and message logs.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="38311-107">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="38311-107">The samples may already be installed on your computer.</span></span> <span data-ttu-id="38311-108">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="38311-108">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="38311-109">如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="38311-109">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="38311-110">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="38311-110">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Management\SecurityLockdown`  
  
## <a name="discussion"></a><span data-ttu-id="38311-111">討論區</span><span class="sxs-lookup"><span data-stu-id="38311-111">Discussion</span></span>  
 <span data-ttu-id="38311-112">您可以單獨或一起使用這些功能，以控制服務安全性的各個方面。</span><span class="sxs-lookup"><span data-stu-id="38311-112">Each of these features can be used separately or together to control aspects of a service's security.</span></span> <span data-ttu-id="38311-113">這不是保護 WCF 服務的最終指引。</span><span class="sxs-lookup"><span data-stu-id="38311-113">This is not a definitive guide to securing a WCF service.</span></span>  
  
 <span data-ttu-id="38311-114">.NET Framework 組態檔中包含敏感性資訊，例如連接至資料庫的連線字串。</span><span class="sxs-lookup"><span data-stu-id="38311-114">The .NET Framework configuration files can contain sensitive information such as connection strings to connect to databases.</span></span> <span data-ttu-id="38311-115">在共用的 Web 裝載案例中，可能需要針對服務在組態檔中加密此資訊，因此組態檔所含的資料便不會任意讓人檢視。</span><span class="sxs-lookup"><span data-stu-id="38311-115">In shared, Web-hosted scenarios it may be desirable to encrypt this information in the configuration file for a service so that the data contained within the configuration file is resistant to casual viewing.</span></span> <span data-ttu-id="38311-116">.NET Framework 2.0 和更新版本可以使用 Windows Data Protection 應用程式開發介面 (DPAPI) 或 RSA 密碼編譯提供者，加密組態檔的各個部分。</span><span class="sxs-lookup"><span data-stu-id="38311-116">.NET Framework 2.0 and later has the ability to encrypt portions of the configuration file using the Windows Data Protection application programming interface (DPAPI) or the RSA Cryptographic provider.</span></span> <span data-ttu-id="38311-117">使用 DPAPI 或 RSA 的 aspnet_regiis.exe 可以加密組態檔的選取部分。</span><span class="sxs-lookup"><span data-stu-id="38311-117">The aspnet_regiis.exe using the DPAPI or RSA can encrypt select portions of a configuration file.</span></span>  
  
 <span data-ttu-id="38311-118">在 Web 裝載的案例中，可能在其他服務的子目錄中還有服務。</span><span class="sxs-lookup"><span data-stu-id="38311-118">In Web-hosted scenarios it is possible to have services in subdirectories of other services.</span></span> <span data-ttu-id="38311-119">判斷組態值的預設語意可允許巢狀目錄中的組態檔複寫上層目錄中的組態值。</span><span class="sxs-lookup"><span data-stu-id="38311-119">The default semantic for determining configuration values allows configuration files in the nested directories to override the configuration values in the parent directory.</span></span> <span data-ttu-id="38311-120">在特定情況下，有許多原因都顯示不應該這樣做。</span><span class="sxs-lookup"><span data-stu-id="38311-120">In certain situations this may be undesirable for a variety of reasons.</span></span> <span data-ttu-id="38311-121">WCF 服務設定支援鎖定設定值，如此一來，當使用覆寫的設定值來執行嵌套的服務時，嵌套的設定就會產生例外狀況。</span><span class="sxs-lookup"><span data-stu-id="38311-121">WCF service configuration supports the locking of configuration values so that nested configuration generates exceptions when a nested service is run using overridden configuration values.</span></span>  
  
 <span data-ttu-id="38311-122">這個範例示範如何控制在追蹤與訊息記錄檔中的已知個人可識別資訊 (PII) 記錄，例如使用者名稱與密碼。</span><span class="sxs-lookup"><span data-stu-id="38311-122">This sample demonstrates how to control the logging of known Personally Identifiable Information (PII) in trace and message logs, such as username and password.</span></span> <span data-ttu-id="38311-123">根據預設，已停用記錄已知 PII，不過在特定情況下，記錄 PII 在偵錯應用程式時相當重要。</span><span class="sxs-lookup"><span data-stu-id="38311-123">By default, logging of known PII is disabled however in certain situations logging of PII can be important in debugging an application.</span></span> <span data-ttu-id="38311-124">這個範例是以[消費者入門](getting-started-sample.md)為基礎。</span><span class="sxs-lookup"><span data-stu-id="38311-124">This sample is based on the [Getting Started](getting-started-sample.md).</span></span> <span data-ttu-id="38311-125">此外，這個範例會使用追蹤和訊息記錄。</span><span class="sxs-lookup"><span data-stu-id="38311-125">In addition, this sample uses tracing and message logging.</span></span> <span data-ttu-id="38311-126">如需詳細資訊，請參閱[追蹤和訊息記錄](tracing-and-message-logging.md)範例。</span><span class="sxs-lookup"><span data-stu-id="38311-126">For more information, see the [Tracing and Message Logging](tracing-and-message-logging.md) sample.</span></span>  
  
## <a name="encrypting-configuration-file-elements"></a><span data-ttu-id="38311-127">加密組態檔項目</span><span class="sxs-lookup"><span data-stu-id="38311-127">Encrypting Configuration File Elements</span></span>  
 <span data-ttu-id="38311-128">針對安全性目的，在共用的 Web 裝載環境中，可能需要加密特定組態項目，例如包含敏感性資訊的資料庫連線字串。</span><span class="sxs-lookup"><span data-stu-id="38311-128">For security purposes in a shared Web-hosting environment, it may be desirable to encrypt certain configuration elements, such as database connection strings that may contain sensitive information.</span></span> <span data-ttu-id="38311-129">您可以使用在 .NET Framework 資料夾中找到的 aspnet_regiis .exe 工具來加密 configuration 元素，例如%WINDIR%\Microsoft.NET\Framework\v4.0.20728。</span><span class="sxs-lookup"><span data-stu-id="38311-129">A configuration element may be encrypted using the aspnet_regiis.exe tool found in the .NET Framework folder For example, %WINDIR%\Microsoft.NET\Framework\v4.0.20728.</span></span>  
  
#### <a name="to-encrypt-the-values-in-the-appsettings-section-in-webconfig-for-the-sample"></a><span data-ttu-id="38311-130">若要加密範例 Web.config 中 appSettings 區段的值</span><span class="sxs-lookup"><span data-stu-id="38311-130">To encrypt the values in the appSettings section in Web.config for the sample</span></span>  
  
1. <span data-ttu-id="38311-131">使用 [開始->執行 ...] 開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="38311-131">Open a command prompt by using Start->Run….</span></span> <span data-ttu-id="38311-132">輸入 `cmd` ，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="38311-132">Type in `cmd` and click **OK**.</span></span>  
  
2. <span data-ttu-id="38311-133">發出下列命令，巡覽至目前的 .NET Framework 目錄：`cd %WINDIR%\Microsoft.NET\Framework\v4.0.20728`。</span><span class="sxs-lookup"><span data-stu-id="38311-133">Navigate to the current .NET Framework directory by issuing the following command: `cd %WINDIR%\Microsoft.NET\Framework\v4.0.20728`.</span></span>  
  
3. <span data-ttu-id="38311-134">發出下列命令，加密 Web.config 資料夾中的 appSettings 組態設定：`aspnet_regiis -pe "appSettings" -app "/servicemodelsamples" -prov "DataProtectionConfigurationProvider"`。</span><span class="sxs-lookup"><span data-stu-id="38311-134">Encrypt the appSettings configuration settings in the Web.config folder by issuing the following command: `aspnet_regiis -pe "appSettings" -app "/servicemodelsamples" -prov "DataProtectionConfigurationProvider"`.</span></span>  
  
 <span data-ttu-id="38311-135">如需加密設定檔區段的詳細資訊，請參閱 ASP.NET 設定中的 DPAPI （[建立安全 ASP.NET 應用程式：驗證、授權和安全通訊](https://docs.microsoft.com/previous-versions/msp-n-p/ff649248(v=pandp.10))）和 ASP.NET 設定中的 RSA 作法（[如何：使用 RSA 加密 ASP.NET 2.0 中](https://docs.microsoft.com/previous-versions/msp-n-p/ff650304(v=pandp.10))的設定區段）。</span><span class="sxs-lookup"><span data-stu-id="38311-135">More information about encrypting sections of configuration files can be found by reading a how-to on DPAPI in ASP.NET configuration ([Building Secure ASP.NET Applications: Authentication, Authorization, and Secure Communication](https://docs.microsoft.com/previous-versions/msp-n-p/ff649248(v=pandp.10))) and a how-to on RSA in ASP.NET configuration ([How To: Encrypt Configuration Sections in ASP.NET 2.0 Using RSA](https://docs.microsoft.com/previous-versions/msp-n-p/ff650304(v=pandp.10))).</span></span>  
  
## <a name="locking-configuration-file-elements"></a><span data-ttu-id="38311-136">鎖定組態檔項目</span><span class="sxs-lookup"><span data-stu-id="38311-136">Locking configuration file elements</span></span>  
 <span data-ttu-id="38311-137">在 Web 裝載的案例中，可能在服務的子目錄中還有服務。</span><span class="sxs-lookup"><span data-stu-id="38311-137">In Web-hosted scenarios, it is possible to have services in subdirectories of services.</span></span> <span data-ttu-id="38311-138">在這些情況中，便會計算子目錄中服務的組態值，方法則是先檢查 Machine.config 中的值，接著合併上層目錄到下層目錄樹狀結構中的 Web.config 檔，最後合併其中包含服務之目錄中的 Web.config 檔。</span><span class="sxs-lookup"><span data-stu-id="38311-138">In these situations, configuration values for the service in the subdirectory are calculated by examining values in Machine.config and successively merging with any Web.config files in parent directories moving down the directory tree and finally merging the Web.config file in the directory that contains the service.</span></span> <span data-ttu-id="38311-139">大多數組態項目的預設行為是允許子目錄中的組態檔覆寫上層目錄中的值組。</span><span class="sxs-lookup"><span data-stu-id="38311-139">The default behavior for most configuration elements is to allow configuration files in subdirectories to override the values set in parent directories.</span></span> <span data-ttu-id="38311-140">在特定情況中，可能會防止子目錄中的組態檔覆寫上層目錄組態的值組。</span><span class="sxs-lookup"><span data-stu-id="38311-140">In certain situations it may be desirable to prevent configuration files in subdirectories from overriding values set in parent directory configuration.</span></span>  
  
 <span data-ttu-id="38311-141">.NET Framework 會提供鎖定組態檔項目的方法，因此覆寫已鎖定組態項目的組態會擲回執行階段例外狀況。</span><span class="sxs-lookup"><span data-stu-id="38311-141">The .NET Framework provides a way to lock configuration file elements so that configurations that override locked configuration elements throw run-time exceptions.</span></span>  
  
 <span data-ttu-id="38311-142">對組態檔中的節點指定 `lockItem` 屬性，即可鎖定組態項目。例如，若要鎖定組態檔中的 CalculatorServiceBehavior 節點，讓巢狀組態檔中的計算機服務無法變更行為，則可以使用下列組態。</span><span class="sxs-lookup"><span data-stu-id="38311-142">A configuration element can be locked by specifying the `lockItem` attribute for a node in the configuration file, for example, to lock the CalculatorServiceBehavior node in the configuration file so that calculator services in nested configuration files cannot change the behavior, the following configuration can be used.</span></span>  
  
```xml  
<configuration>  
   <system.serviceModel>  
      <behaviors>
          <serviceBehaviors>
             <behavior name="CalculatorServiceBehavior" lockItem="true">
               <serviceMetadata httpGetEnabled="True"/>
               <serviceDebug includeExceptionDetailInFaults="False" />
             </behavior>
          </serviceBehaviors>
       </behaviors>
    </system.serviceModel>  
</configuration>  
```  
  
 <span data-ttu-id="38311-143">鎖定組態項目可以更加特定。</span><span class="sxs-lookup"><span data-stu-id="38311-143">Locking of configuration elements can be more specific.</span></span> <span data-ttu-id="38311-144">可以指定項目清單做為 `lockElements` 的值，進而鎖定子項目集合內的一組項目。</span><span class="sxs-lookup"><span data-stu-id="38311-144">A list of elements can be specified as the value to the `lockElements` to lock a set of elements within a collection of sub-elements.</span></span> <span data-ttu-id="38311-145">可以指定屬性清單做為 `lockAttributes` 的值，進而鎖定項目內的一組屬性。</span><span class="sxs-lookup"><span data-stu-id="38311-145">A list of attributes can be specified as the value to the `lockAttributes` to lock a set of attributes within an element.</span></span> <span data-ttu-id="38311-146">您可以藉由在節點上指定 `lockAllElementsExcept` 或 `lockAllAttributesExcept` 屬性，即可鎖定整個項目或屬性的集合，不過指定的清單則為例外。</span><span class="sxs-lookup"><span data-stu-id="38311-146">An entire collection of elements or attributes can be locked except for a specified list by specifying the `lockAllElementsExcept` or `lockAllAttributesExcept` attributes on a node.</span></span>  
  
## <a name="pii-logging-configuration"></a><span data-ttu-id="38311-147">PII 記錄組態</span><span class="sxs-lookup"><span data-stu-id="38311-147">PII Logging Configuration</span></span>  
 <span data-ttu-id="38311-148">PII 記錄是由兩個參數所控制：Machine.config 中找到的全電腦設定，可讓電腦系統管理員允許或拒絕記錄 PII。另一樣為應用程式設定，可讓應用程式管理員針對 Web.config 或 App.config 檔案中的每個來源切換 PII 記錄。</span><span class="sxs-lookup"><span data-stu-id="38311-148">Logging of PII is controlled by two switches: a computer-wide setting found in Machine.config that allows a computer administrator to permit or deny logging of PII and an application setting that allows an application administrator to toggle logging of PII for each source in a Web.config or App.config file.</span></span>  
  
 <span data-ttu-id="38311-149">在 `enableLoggingKnownPii` `true` machine.config 的 `false` 元素中，將設定為或，即可控制全電腦設定 `machineSettings` 。例如，下列可讓應用程式開啟 PII 的記錄功能。</span><span class="sxs-lookup"><span data-stu-id="38311-149">The computer-wide setting is controlled by setting `enableLoggingKnownPii` to `true` or `false`, in the `machineSettings` element in Machine.config. For example, the following allows applications to turn on logging of PII.</span></span>  
  
```xml  
<configuration>  
    <system.serviceModel>  
        <machineSettings enableLoggingKnownPii="true" />  
    </system.serviceModel>  
</configuration>  
```  
  
> [!NOTE]
> <span data-ttu-id="38311-150">Machine.config 檔的預設位置為：%WINDIR%\Microsoft.NET\Framework\v2.0.50727\CONFIG。</span><span class="sxs-lookup"><span data-stu-id="38311-150">The Machine.config file has a default location: %WINDIR%\Microsoft.NET\Framework\v2.0.50727\CONFIG.</span></span>  
  
 <span data-ttu-id="38311-151">如果 Machine.config 中沒有 `enableLoggingKnownPii` 屬性，則不允許記錄 PII。</span><span class="sxs-lookup"><span data-stu-id="38311-151">If the `enableLoggingKnownPii` attribute is not present in Machine.config, logging of PII is not allowed.</span></span>  
  
 <span data-ttu-id="38311-152">在 Web.config 或 App.config 檔案中將來源項目的 `logKnownPii` 屬性設定為 `true` 或 `false`，即可啟用應用程式的 PII 記錄。</span><span class="sxs-lookup"><span data-stu-id="38311-152">Enabling logging of PII for an application is done by setting the `logKnownPii` attribute of the source element to `true` or `false` in the Web.config or App.config file.</span></span> <span data-ttu-id="38311-153">例如，下列各項會針對訊息記錄和追蹤記錄啟用 PII 記錄。</span><span class="sxs-lookup"><span data-stu-id="38311-153">For example, the following enables logging of PII for both message logging and trace logging.</span></span>  
  
```xml  
<configuration>  
    <system.diagnostics>  
        <sources>  
            <source name="System.ServiceModel.MessageLogging" logKnownPii="true">  
                <listeners>
                ...
                </listeners>  
            </source>  
            <source name="System.ServiceModel" switchValue="Verbose, ActivityTracing">  
            <listeners>  
        ...
            </listeners>  
            </source>  
        </sources>  
    </system.diagnostics>  
</configuration>  
```  
  
 <span data-ttu-id="38311-154">如果未指定 `logKnownPii` 屬性，則不會記錄 PII。</span><span class="sxs-lookup"><span data-stu-id="38311-154">If the `logKnownPii` attribute is not specified, then PII is not logged.</span></span>  
  
 <span data-ttu-id="38311-155">只有當 `enableLoggingKnownPii` 設定為 `true` 而且 `logKnownPii` 設定為 `true` 時，才會記錄 PII。</span><span class="sxs-lookup"><span data-stu-id="38311-155">PII is only logged if both `enableLoggingKnownPii` is set to `true`, and `logKnownPii` is set to `true`.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="38311-156">System.Diagnostics 除了組態檔中列出的第一個屬性外，會忽略所有來源上的所有屬性。</span><span class="sxs-lookup"><span data-stu-id="38311-156">System.Diagnostics ignores all attributes on all sources except the first one listed in the configuration file.</span></span> <span data-ttu-id="38311-157">將 `logKnownPii` 屬性新增至組態檔的第二個來源也沒有作用。</span><span class="sxs-lookup"><span data-stu-id="38311-157">Adding the `logKnownPii` attribute to the second source in the configuration file has no effect.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="38311-158">若要執行此範例，需要手動修改 Machine.config。將 Machine.config 修改為不正確的值或語法可能會使所有 .NET Framework 應用程式無法執行時，請務必小心。</span><span class="sxs-lookup"><span data-stu-id="38311-158">To run this sample involves manual modification of Machine.config. Care should be taken when modifying Machine.config as incorrect values or syntax may prevent all .NET Framework applications from running.</span></span>  
  
 <span data-ttu-id="38311-159">也可能使用 DPAPI 和 RSA 加密組態檔項目。</span><span class="sxs-lookup"><span data-stu-id="38311-159">It is also possible to encrypt configuration file elements using DPAPI and RSA.</span></span> <span data-ttu-id="38311-160">如需詳細資訊，請參閱下列連結：</span><span class="sxs-lookup"><span data-stu-id="38311-160">For more information, see the following links:</span></span>  
  
- <span data-ttu-id="38311-161">[建置安全的 ASP.NET 應用程式：驗證、授權和安全通訊](https://docs.microsoft.com/previous-versions/msp-n-p/ff649248(v=pandp.10))</span><span class="sxs-lookup"><span data-stu-id="38311-161">[Building Secure ASP.NET Applications: Authentication, Authorization, and Secure Communication](https://docs.microsoft.com/previous-versions/msp-n-p/ff649248(v=pandp.10))</span></span>  
  
- <span data-ttu-id="38311-162">[HOW TO：使用 RSA 加密 ASP.NET 2.0 中的組態區段](https://docs.microsoft.com/previous-versions/msp-n-p/ff650304(v=pandp.10))</span><span class="sxs-lookup"><span data-stu-id="38311-162">[How To: Encrypt Configuration Sections in ASP.NET 2.0 Using RSA](https://docs.microsoft.com/previous-versions/msp-n-p/ff650304(v=pandp.10))</span></span>  
  
#### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="38311-163">若要設定、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="38311-163">To set up, build and run the sample</span></span>  
  
1. <span data-ttu-id="38311-164">請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="38311-164">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2. <span data-ttu-id="38311-165">編輯 Machine.config 以將 `enableLoggingKnownPii` 屬性設定為 `true`，需要時並新增父節點。</span><span class="sxs-lookup"><span data-stu-id="38311-165">Edit Machine.config to set the `enableLoggingKnownPii` attribute to `true`, adding the parent nodes if necessary.</span></span>  
  
3. <span data-ttu-id="38311-166">若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="38311-166">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
4. <span data-ttu-id="38311-167">若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="38311-167">To run the sample in a single- or cross-computer configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>  
  
#### <a name="to-clean-up-the-sample"></a><span data-ttu-id="38311-168">若要清除範例</span><span class="sxs-lookup"><span data-stu-id="38311-168">To clean up the sample</span></span>  
  
1. <span data-ttu-id="38311-169">編輯 Machine.config 以將 `enableLoggingKnownPii` 屬性設定為 `false`。</span><span class="sxs-lookup"><span data-stu-id="38311-169">Edit Machine.config to set the `enableLoggingKnownPii` attribute to `false`.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="38311-170">請參閱</span><span class="sxs-lookup"><span data-stu-id="38311-170">See also</span></span>

- <span data-ttu-id="38311-171">[AppFabric 監控範例](https://docs.microsoft.com/previous-versions/appfabric/ff383407(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="38311-171">[AppFabric Monitoring Samples](https://docs.microsoft.com/previous-versions/appfabric/ff383407(v=azure.10))</span></span>
