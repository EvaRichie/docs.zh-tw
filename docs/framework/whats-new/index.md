---
title: .NET Framework 的新功能
description: 請參閱各種 .NET Framework 版本的新功能。 閱讀每個版本的重要新功能和增強功能的摘要。
ms.date: 04/18/2019
dev_langs:
- csharp
- vb
helpviewer_keywords:
- what's new [.NET Framework]
ms.assetid: 1d971dd7-10fc-4692-8dac-30ca308fc0fa
ms.openlocfilehash: 1e9657c60ef2ff0ef30ae1607a0e7f2cedd01187
ms.sourcegitcommit: a8a205034eeffc7c3e1bdd6f506a75b0f7099ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2020
ms.locfileid: "91756074"
---
# <a name="whats-new-in-net-framework"></a><span data-ttu-id="7a824-104">.NET Framework 的新功能</span><span class="sxs-lookup"><span data-stu-id="7a824-104">What's new in .NET Framework</span></span>

<span data-ttu-id="7a824-105">本文摘要說明下列 .NET Framework 版本中重要的新功能和增強功能：</span><span class="sxs-lookup"><span data-stu-id="7a824-105">This article summarizes key new features and improvements in the following versions of the .NET Framework:</span></span>

- [<span data-ttu-id="7a824-106">.NET Framework 4.8</span><span class="sxs-lookup"><span data-stu-id="7a824-106">.NET Framework 4.8</span></span>](#v48)
- [<span data-ttu-id="7a824-107">.NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="7a824-107">.NET Framework 4.7.2</span></span>](#v472)
- [<span data-ttu-id="7a824-108">.NET Framework 4.7.1</span><span class="sxs-lookup"><span data-stu-id="7a824-108">.NET Framework 4.7.1</span></span>](#v471)
- [<span data-ttu-id="7a824-109">.NET Framework 4.7</span><span class="sxs-lookup"><span data-stu-id="7a824-109">.NET Framework 4.7</span></span>](#v47)
- [<span data-ttu-id="7a824-110">.NET Framework 4.6.2</span><span class="sxs-lookup"><span data-stu-id="7a824-110">.NET Framework 4.6.2</span></span>](#v462)
- [<span data-ttu-id="7a824-111">.NET Framework 4.6.1</span><span class="sxs-lookup"><span data-stu-id="7a824-111">.NET Framework 4.6.1</span></span>](#v461)
- [<span data-ttu-id="7a824-112">.NET 2015 與 .NET Framework 4.6</span><span class="sxs-lookup"><span data-stu-id="7a824-112">.NET 2015 and .NET Framework 4.6</span></span>](#v46)
- [<span data-ttu-id="7a824-113">.NET Framework 4.5.2</span><span class="sxs-lookup"><span data-stu-id="7a824-113">.NET Framework 4.5.2</span></span>](#v452)
- [<span data-ttu-id="7a824-114">.NET Framework 4.5。1</span><span class="sxs-lookup"><span data-stu-id="7a824-114">.NET Framework 4.5.1</span></span>](#v451)
- [<span data-ttu-id="7a824-115">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="7a824-115">.NET Framework 4.5</span></span>](#v45)

<span data-ttu-id="7a824-116">此文章並不會提供每一個新功能的完整資料，且內容可能會隨時變更。</span><span class="sxs-lookup"><span data-stu-id="7a824-116">This article does not provide comprehensive information about each new feature and is subject to change.</span></span> <span data-ttu-id="7a824-117">如需 .NET Framework 的一般資訊，請參閱[使用者入門](../get-started/index.md)。</span><span class="sxs-lookup"><span data-stu-id="7a824-117">For general information about the .NET Framework, see [Getting Started](../get-started/index.md).</span></span> <span data-ttu-id="7a824-118">若要了解支援的平台，請參閱[系統需求](../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="7a824-118">For supported platforms, see [System Requirements](../get-started/system-requirements.md).</span></span> <span data-ttu-id="7a824-119">如需下載連結和安裝指示，請參閱[安裝指南](../install/guide-for-developers.md)。</span><span class="sxs-lookup"><span data-stu-id="7a824-119">For download links and installation instructions, see [Installation Guide](../install/guide-for-developers.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7a824-120">.NET Framework 小組也會不定期隨著 NuGet 發行相關功能，以擴充平台支援並引進新功能，例如不可變的集合和支援 SIMD 的向量類型。</span><span class="sxs-lookup"><span data-stu-id="7a824-120">The .NET Framework team also releases features out of band with NuGet to expand platform support and to introduce new functionality, such as immutable collections and SIMD-enabled vector types.</span></span> <span data-ttu-id="7a824-121">如需詳細資訊，請參閱[其他類別庫和 API](../additional-apis/index.md) 以及 [.NET Framework 和不定期發行](../get-started/the-net-framework-and-out-of-band-releases.md)。</span><span class="sxs-lookup"><span data-stu-id="7a824-121">For more information, see [Additional Class Libraries and APIs](../additional-apis/index.md) and [The .NET Framework and Out-of-Band Releases](../get-started/the-net-framework-and-out-of-band-releases.md).</span></span>
> <span data-ttu-id="7a824-122">請參閱 .NET Framework 的 [NuGet 套件完整清單](https://www.nuget.org/profiles/dotnetframework)。</span><span class="sxs-lookup"><span data-stu-id="7a824-122">See a [complete list of NuGet packages](https://www.nuget.org/profiles/dotnetframework) for the .NET Framework.</span></span>

<a name="v48"></a>

## <a name="introducing-net-framework-48"></a><span data-ttu-id="7a824-123">.NET Framework 4.8 簡介</span><span class="sxs-lookup"><span data-stu-id="7a824-123">Introducing .NET Framework 4.8</span></span>

<span data-ttu-id="7a824-124">.NET Framework 4.8 建置於舊版 .NET Framework 4.x 的基礎上，方法是新增許多新的修正和多個新功能，同時保有產品的高穩定性。</span><span class="sxs-lookup"><span data-stu-id="7a824-124">.NET Framework 4.8 builds on previous versions of the .NET Framework 4.x by adding many new fixes and several new features while remaining a very stable product.</span></span>

### <a name="download-and-install-net-framework-48"></a><span data-ttu-id="7a824-125">下載並安裝 .NET Framework 4。8</span><span class="sxs-lookup"><span data-stu-id="7a824-125">Download and install .NET Framework 4.8</span></span>

<span data-ttu-id="7a824-126">您可以從下列位置下載 .NET Framework 4.8：</span><span class="sxs-lookup"><span data-stu-id="7a824-126">You can download .NET Framework 4.8  from the following locations:</span></span>

- [<span data-ttu-id="7a824-127">.NET Framework 4.8 Web 安裝程式</span><span class="sxs-lookup"><span data-stu-id="7a824-127">.NET Framework 4.8 Web Installer</span></span>](https://dotnet.microsoft.com/download/dotnet-framework/net48)

- [<span data-ttu-id="7a824-128">NET Framework 4.8 離線安裝程式</span><span class="sxs-lookup"><span data-stu-id="7a824-128">NET Framework 4.8 Offline Installer</span></span>](https://dotnet.microsoft.com/download/dotnet-framework/net48)

<span data-ttu-id="7a824-129">.NET Framework 4.8 可以安裝在 Windows 10、Windows 8.1、Windows 7 SP1，以及自 Windows Server 2008 R2 SP1 起的相對應伺服器平台上。</span><span class="sxs-lookup"><span data-stu-id="7a824-129">.NET Framework 4.8 can be installed on Windows 10, Windows 8.1, Windows 7 SP1, and the corresponding server platforms starting with Windows Server 2008 R2 SP1.</span></span> <span data-ttu-id="7a824-130">您可以使用 Web 安裝程式或離線安裝程式來安裝 .NET Framework 4.8。</span><span class="sxs-lookup"><span data-stu-id="7a824-130">You can install .NET Framework 4.8 by using either the web installer or the offline installer.</span></span> <span data-ttu-id="7a824-131">針對大部分的使用者，我們建議使用 Web 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="7a824-131">The recommended way for most users is to use the web installer.</span></span>

<span data-ttu-id="7a824-132">透過安裝 [.NET Framework 4.8 開發人員套件](https://go.microsoft.com/fwlink/?LinkId=2085167)，即能以 Visual Studio 2012 或更新版本中的 .NET Framework 4.8 為目標。</span><span class="sxs-lookup"><span data-stu-id="7a824-132">You can target .NET Framework 4.8 in Visual Studio 2012 or later by installing the [.NET Framework 4.8 Developer Pack](https://go.microsoft.com/fwlink/?LinkId=2085167).</span></span>

### <a name="whats-new-in-net-framework-48"></a><span data-ttu-id="7a824-133">.NET Framework 4.8 中的新功能</span><span class="sxs-lookup"><span data-stu-id="7a824-133">What's new in .NET Framework 4.8</span></span>

<span data-ttu-id="7a824-134">.NET Framework 4.8 引進下列領域的新功能：</span><span class="sxs-lookup"><span data-stu-id="7a824-134">.NET Framework 4.8 introduces new features in the following areas:</span></span>

- [<span data-ttu-id="7a824-135">基底類別</span><span class="sxs-lookup"><span data-stu-id="7a824-135">Base classes</span></span>](#core48)
- [<span data-ttu-id="7a824-136">Windows Communication Foundation (WCF)</span><span class="sxs-lookup"><span data-stu-id="7a824-136">Windows Communication Foundation (WCF)</span></span>](#wcf48)
- [<span data-ttu-id="7a824-137">Windows Presentation Foundation (WPF)</span><span class="sxs-lookup"><span data-stu-id="7a824-137">Windows Presentation Foundation (WPF)</span></span>](#wpf48)
- [<span data-ttu-id="7a824-138">Common language runtime</span><span class="sxs-lookup"><span data-stu-id="7a824-138">Common language runtime</span></span>](#clr48)

<span data-ttu-id="7a824-139">改善的協助工具，允許應用程式為輔助技術使用者提供適當的體驗，這仍是 .NET Framework 4.8 的主要焦點。</span><span class="sxs-lookup"><span data-stu-id="7a824-139">Improved accessibility, which allows an application to provide an appropriate experience for users of Assistive Technology, continues to be a major focus of .NET Framework 4.8.</span></span> <span data-ttu-id="7a824-140">如需 .NET Framework 4.8 中協助工具改善的資訊；請參閱 [.NET Framework 協助工具的新功能](whats-new-in-accessibility.md)。</span><span class="sxs-lookup"><span data-stu-id="7a824-140">For information on accessibility improvements in .NET Framework 4.8, see [What's new in accessibility in the .NET Framework](whats-new-in-accessibility.md).</span></span>

<a name="core48"></a>

#### <a name="base-classes"></a><span data-ttu-id="7a824-141">基底類別</span><span class="sxs-lookup"><span data-stu-id="7a824-141">Base classes</span></span>

<span data-ttu-id="7a824-142">**降低對密碼編譯的 FIPS 影響**。</span><span class="sxs-lookup"><span data-stu-id="7a824-142">**Reduced FIPS impact on Cryptography**.</span></span> <span data-ttu-id="7a824-143">在舊版的 .NET Framework 中，受控密碼編譯提供者類別（例如在「 <xref:System.Security.Cryptography.SHA256Managed> <xref:System.Security.Cryptography.CryptographicException> FIPS 模式」中設定系統密碼編譯程式庫時，會擲回）。</span><span class="sxs-lookup"><span data-stu-id="7a824-143">In previous versions of the .NET Framework, managed cryptographic provider classes such as <xref:System.Security.Cryptography.SHA256Managed> throw a <xref:System.Security.Cryptography.CryptographicException> when the system cryptographic libraries are configured in "FIPS mode".</span></span> <span data-ttu-id="7a824-144">擲回這些例外狀況的原因是受控密碼編譯提供者類別版本不像系統密碼編譯程式庫一樣已通過 FIPS (聯邦資訊處理標準) 140-2 認證。</span><span class="sxs-lookup"><span data-stu-id="7a824-144">These exceptions are thrown because the managed versions of the cryptographic provider classes, unlike the system cryptographic libraries, have not undergone FIPS (Federal Information Processing Standards) 140-2 certification.</span></span> <span data-ttu-id="7a824-145">因為一些提供者將其開發機器設定為 FIPS 模式，在生產系統中通常會擲回該例外狀況。</span><span class="sxs-lookup"><span data-stu-id="7a824-145">Because few developers have their development machines in FIPS mode, the exceptions are commonly thrown in production systems.</span></span>

<span data-ttu-id="7a824-146">根據預設，在以 .NET Framework 4.8 為目標的應用程式中，下列受控密碼編譯類別在此案例中已不會再擲回 a <xref:System.Security.Cryptography.CryptographicException>：</span><span class="sxs-lookup"><span data-stu-id="7a824-146">By default in applications that target .NET Framework 4.8, the following managed cryptography classes no longer throw a <xref:System.Security.Cryptography.CryptographicException> in this case:</span></span>

- <xref:System.Security.Cryptography.MD5Cng>
- <xref:System.Security.Cryptography.MD5CryptoServiceProvider>
- <xref:System.Security.Cryptography.RC2CryptoServiceProvider>
- <xref:System.Security.Cryptography.RijndaelManaged>
- <xref:System.Security.Cryptography.RIPEMD160Managed>
- <xref:System.Security.Cryptography.SHA256Managed>

<span data-ttu-id="7a824-147">相反地，這些類別會將密碼編譯作業重新導向到系統密碼編譯程式庫。</span><span class="sxs-lookup"><span data-stu-id="7a824-147">Instead, these classes redirect cryptographic operations to a system cryptography library.</span></span> <span data-ttu-id="7a824-148">此變更有效地去除了開發人員環境與生產環境之間的潛在混淆，而且讓原生元件與受控元件在相同的密碼編譯原則下執行。</span><span class="sxs-lookup"><span data-stu-id="7a824-148">This change effectively removes a potentially confusing difference between developer environments and production environments and makes native components and managed components operate under the same cryptographic policy.</span></span> <span data-ttu-id="7a824-149">相依於這些例外狀況的應用程式可以透過將 AppContext 切換參數 `Switch.System.Security.Cryptography.UseLegacyFipsThrow` 設定為 `true` 以還原先前的行為。</span><span class="sxs-lookup"><span data-stu-id="7a824-149">Applications that depend on these exceptions can restore the previous behavior by setting the AppContext switch `Switch.System.Security.Cryptography.UseLegacyFipsThrow` to `true`.</span></span> <span data-ttu-id="7a824-150">如需詳細資訊，請參閱[受控密碼編譯類別在 FIPS 模式中不會擲回 CryptographyException](../migration-guide/retargeting/4.7.2-4.8.md#managed-cryptography-classes-do-not-throw-a-cryptographyexception-in-fips-mode) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="7a824-150">For more information, see [Managed cryptography classes do not throw a CryptographyException in FIPS mode](../migration-guide/retargeting/4.7.2-4.8.md#managed-cryptography-classes-do-not-throw-a-cryptographyexception-in-fips-mode).</span></span>

<span data-ttu-id="7a824-151">**ZLib 更新版本的使用**</span><span class="sxs-lookup"><span data-stu-id="7a824-151">**Use of updated version of ZLib**</span></span>

<span data-ttu-id="7a824-152">從 .NET Framework 4.5 開始，clrcompression.dll 組件使用原生的資料壓縮外部程式庫 [ZLib](https://www.zlib.net) 來提供 Deflate 演算法的實作。</span><span class="sxs-lookup"><span data-stu-id="7a824-152">Starting with .NET Framework 4.5, the clrcompression.dll assembly uses [ZLib](https://www.zlib.net), a native external library for data compression, in order to provide an implementation for the deflate algorithm.</span></span> <span data-ttu-id="7a824-153">在 .NET Framework 4.8 中，clrcompression.dll 已更新為使用 ZLib 1.2.11 版，這包括數個重要改進與修正。</span><span class="sxs-lookup"><span data-stu-id="7a824-153">The .NET Framework 4.8, clrcompression.dll is updated to use ZLib Version 1.2.11, which includes several key improvements and fixes.</span></span>

<a name="wcf48"></a>

#### <a name="windows-communication-foundation-wcf"></a><span data-ttu-id="7a824-154">Windows Communication Foundation (WCF)</span><span class="sxs-lookup"><span data-stu-id="7a824-154">Windows Communication Foundation (WCF)</span></span>

<span data-ttu-id="7a824-155">**ServiceHealthBehavior 簡介**</span><span class="sxs-lookup"><span data-stu-id="7a824-155">**Introduction of ServiceHealthBehavior**</span></span>

<span data-ttu-id="7a824-156">協調流程工具廣為使用健康情況端點根據服務的健康情況狀態來管理服務。</span><span class="sxs-lookup"><span data-stu-id="7a824-156">Health endpoints are widely used by orchestration tools to manage services based on their health status.</span></span> <span data-ttu-id="7a824-157">也可以透過監視要追蹤的工具並提供有關服務可用性與效能的通知，來使用健康情況檢查。</span><span class="sxs-lookup"><span data-stu-id="7a824-157">Health checks can also be used by monitoring tools to track and provide notifications about the availability and performance of a service.</span></span>

<span data-ttu-id="7a824-158">**ServiceHealthBehavior** 是 WCF 服務行為，它會延伸 <xref:System.ServiceModel.Description.IServiceBehavior>。</span><span class="sxs-lookup"><span data-stu-id="7a824-158">**ServiceHealthBehavior** is a WCF service behavior that extends <xref:System.ServiceModel.Description.IServiceBehavior>.</span></span>  <span data-ttu-id="7a824-159">當新增到 <xref:System.ServiceModel.Description.ServiceDescription.Behaviors?displayProperty=nameWithType> 集合時，服務行為會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="7a824-159">When added to the <xref:System.ServiceModel.Description.ServiceDescription.Behaviors?displayProperty=nameWithType> collection, a service behavior does the following:</span></span>

- <span data-ttu-id="7a824-160">傳回具有 HTTP 回應碼的服務健康情況狀態。</span><span class="sxs-lookup"><span data-stu-id="7a824-160">Returns service health status with HTTP response codes.</span></span> <span data-ttu-id="7a824-161">您可以在查詢字串中指定 HTTP/GET 健康情況探查要求的 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="7a824-161">You can specify in a query string the HTTP status code for a HTTP/GET health probe request.</span></span>

- <span data-ttu-id="7a824-162">發佈服務健康情況相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7a824-162">Publishes information about service health.</span></span> <span data-ttu-id="7a824-163">服務特定詳細資料 (包括服務狀態、節流計數與容量) 可以透過 `?health` 查詢字串使用 HTTP/GET 來顯示。</span><span class="sxs-lookup"><span data-stu-id="7a824-163">Service-specific details, including service state, throttle counts, and capacity can be displayed by using an HTTP/GET request with the `?health` query string.</span></span> <span data-ttu-id="7a824-164">針對行為不當的 WCF 服務進行疑難排解時，能否輕鬆存取此類資訊非常重要。</span><span class="sxs-lookup"><span data-stu-id="7a824-164">Ease of access to such information is important when troubleshooting a misbehaving WCF service.</span></span>

<span data-ttu-id="7a824-165">有兩種方式可公開健康情況端點及發佈 WCF 服務健康情況資訊：</span><span class="sxs-lookup"><span data-stu-id="7a824-165">There are two ways to expose the health endpoint and publish WCF service health information:</span></span>

- <span data-ttu-id="7a824-166">透過程式碼。</span><span class="sxs-lookup"><span data-stu-id="7a824-166">Through code.</span></span> <span data-ttu-id="7a824-167">例如：</span><span class="sxs-lookup"><span data-stu-id="7a824-167">For example:</span></span>

  ```csharp
  ServiceHost host = new ServiceHost(typeof(Service1),
                     new Uri("http://contoso:81/Service1"));
  ServiceHealthBehavior healthBehavior =
      host.Description.Behaviors.Find<ServiceHealthBehavior>();
  healthBehavior ??= new ServiceHealthBehavior();
  host.Description.Behaviors.Add(healthBehavior);
  ```

  ```vb
  Dim host As New ServiceHost(GetType(Service1),
              New Uri("http://contoso:81/Service1"))
  Dim healthBehavior As ServiceHealthBehavior =
     host.Description.Behaviors.Find(Of ServiceHealthBehavior)()
  If healthBehavior Is Nothing Then
     healthBehavior = New ServiceHealthBehavior()
  End If
  host.Description.Behaviors.Add(healthBehavior)
  ```

- <span data-ttu-id="7a824-168">透過使用設定檔。</span><span class="sxs-lookup"><span data-stu-id="7a824-168">By using a configuration file.</span></span> <span data-ttu-id="7a824-169">例如：</span><span class="sxs-lookup"><span data-stu-id="7a824-169">For example:</span></span>

  ```xml
  <behaviors>
    <serviceBehaviors>
      <behavior name="DefaultBehavior">
        <serviceHealth httpsGetEnabled="true"/>
      </behavior>
    </serviceBehaviors>
  </behaviors>
  ```

<span data-ttu-id="7a824-170">您可以透過使用查詢參數 (例如 `OnServiceFailure`、`OnDispatcherFailure`、`OnListenerFailure`、`OnThrottlePercentExceeded`) 來查詢服務的健康情況狀態，而且可以為每個查詢參數指定 HTTP 回應碼。</span><span class="sxs-lookup"><span data-stu-id="7a824-170">A service's health status can be queried by using query parameters such as `OnServiceFailure`, `OnDispatcherFailure`, `OnListenerFailure`, `OnThrottlePercentExceeded`), and an HTTP response code can be specified for each query parameter.</span></span> <span data-ttu-id="7a824-171">若針對查詢參數忽略 HTTP 回應碼，預設會使用 503 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="7a824-171">If the HTTP response code is omitted for a query parameter, a 503 HTTP response code is used by default.</span></span> <span data-ttu-id="7a824-172">例如：</span><span class="sxs-lookup"><span data-stu-id="7a824-172">For example:</span></span>

- <span data-ttu-id="7a824-173">OnServiceFailure：`https://contoso:81/Service1?health&OnServiceFailure=450`</span><span class="sxs-lookup"><span data-stu-id="7a824-173">OnServiceFailure: `https://contoso:81/Service1?health&OnServiceFailure=450`</span></span>

  <span data-ttu-id="7a824-174">當 [ServiceHost.State](xref:System.ServiceModel.Channels.CommunicationObject.State) 大於 <xref:System.ServiceModel.CommunicationState.Opened?displayProperty=nameWithType> 時，會傳回 450 HTTP 回應狀態碼。</span><span class="sxs-lookup"><span data-stu-id="7a824-174">A 450 HTTP response status code is returned when [ServiceHost.State](xref:System.ServiceModel.Channels.CommunicationObject.State) is greater than <xref:System.ServiceModel.CommunicationState.Opened?displayProperty=nameWithType>.</span></span>
<span data-ttu-id="7a824-175">查詢參數與範例：</span><span class="sxs-lookup"><span data-stu-id="7a824-175">Query parameters and examples:</span></span>

- <span data-ttu-id="7a824-176">OnDispatcherFailure：`https://contoso:81/Service1?health&OnDispatcherFailure=455`</span><span class="sxs-lookup"><span data-stu-id="7a824-176">OnDispatcherFailure: `https://contoso:81/Service1?health&OnDispatcherFailure=455`</span></span>

  <span data-ttu-id="7a824-177">當任何通道發送器的狀態大於 <xref:System.ServiceModel.CommunicationState.Opened?displayProperty=nameWithType> 時，會傳回 455 HTTP 回應狀態碼。</span><span class="sxs-lookup"><span data-stu-id="7a824-177">A 455 HTTP response status code is returned when the state of any of the channel dispatchers is greater than <xref:System.ServiceModel.CommunicationState.Opened?displayProperty=nameWithType>.</span></span>

- <span data-ttu-id="7a824-178">OnListenerFailure：`https://contoso:81/Service1?health&OnListenerFailure=465`</span><span class="sxs-lookup"><span data-stu-id="7a824-178">OnListenerFailure: `https://contoso:81/Service1?health&OnListenerFailure=465`</span></span>

  <span data-ttu-id="7a824-179">當任何通道接聽程式的狀態大於 <xref:System.ServiceModel.CommunicationState.Opened?displayProperty=nameWithType> 時，會傳回 465 HTTP 回應狀態碼。</span><span class="sxs-lookup"><span data-stu-id="7a824-179">A 465 HTTP response status code is returned when the state of any of the channel listeners is greater than <xref:System.ServiceModel.CommunicationState.Opened?displayProperty=nameWithType>.</span></span>

- <span data-ttu-id="7a824-180">OnThrottlePercentExceeded：`https://contoso:81/Service1?health&OnThrottlePercentExceeded= 70:350,95:500`</span><span class="sxs-lookup"><span data-stu-id="7a824-180">OnThrottlePercentExceeded: `https://contoso:81/Service1?health&OnThrottlePercentExceeded= 70:350,95:500`</span></span>

  <span data-ttu-id="7a824-181">指定觸發回應的百分比 {1 – 100} 與其 HTTP 回應碼 {200 – 599}。</span><span class="sxs-lookup"><span data-stu-id="7a824-181">Specifies the percentage {1 – 100} that triggers the response and its HTTP response code {200 – 599}.</span></span> <span data-ttu-id="7a824-182">在此範例中：</span><span class="sxs-lookup"><span data-stu-id="7a824-182">In this example:</span></span>

  - <span data-ttu-id="7a824-183">若百分比大於 95，會傳回 500 HTTP 回應碼。</span><span class="sxs-lookup"><span data-stu-id="7a824-183">If the percentage is greater than 95, a 500 HTTP response code is returned.</span></span>

  - <span data-ttu-id="7a824-184">若百分比介於 70 到 95 之間，會傳回 350。</span><span class="sxs-lookup"><span data-stu-id="7a824-184">If the percentage or between 70 and 95, 350 is returned.</span></span>

  - <span data-ttu-id="7a824-185">否則，會傳回 200。</span><span class="sxs-lookup"><span data-stu-id="7a824-185">Otherwise, 200 is returned.</span></span>

<span data-ttu-id="7a824-186">您可以透過指定如 `https://contoso:81/Service1?health` 的查詢字串以使用 HTML 方式顯示服務健康情況狀態，或透過指定如 `https://contoso:81/Service1?health&Xml` 的查詢字串以使用 XML 方式顯示服務健康情況狀態。</span><span class="sxs-lookup"><span data-stu-id="7a824-186">The service health status can be displayed either in HTML by specifying a query string like `https://contoso:81/Service1?health` or in XML by specifying a query string like `https://contoso:81/Service1?health&Xml`.</span></span> <span data-ttu-id="7a824-187">如 `https://contoso:81/Service1?health&NoContent` 的查詢字串會傳回空的 HTML 頁面。</span><span class="sxs-lookup"><span data-stu-id="7a824-187">A query string like `https://contoso:81/Service1?health&NoContent` returns an empty HTML page.</span></span>

<a name="wpf48"></a>

#### <a name="windows-presentation-foundation-wpf"></a><span data-ttu-id="7a824-188">Windows Presentation Foundation (WPF)</span><span class="sxs-lookup"><span data-stu-id="7a824-188">Windows Presentation Foundation (WPF)</span></span>

<span data-ttu-id="7a824-189">**高 DPI 增強功能**</span><span class="sxs-lookup"><span data-stu-id="7a824-189">**High DPI enhancements**</span></span>

<span data-ttu-id="7a824-190">在 .NET Framework 4.8 中，WPF 已加入對「個別監視器 V2 DPI 感知」與「混合模式 DPI 縮放比例」的支援。</span><span class="sxs-lookup"><span data-stu-id="7a824-190">In .NET Framework 4.8, WPF adds support for Per-Monitor V2 DPI Awareness and Mixed-Mode DPI scaling.</span></span> <span data-ttu-id="7a824-191">如需有關高 DPI 開發的詳細資訊，請參閱 [Windows 上的高 DPI 傳統型應用程式開發](/windows/win32/hidpi/high-dpi-desktop-application-development-on-windows) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="7a824-191">See [High DPI Desktop Application Development on Windows](/windows/win32/hidpi/high-dpi-desktop-application-development-on-windows) for additional information about high DPI development.</span></span>

<span data-ttu-id="7a824-192">.NET Framework 4.8 已改善對支援「混合模式 DPI 縮放比例」之平台上裝載之 HWNDs 與 Windows Forms 交互操作 (在高 DPI WPF 應用程式中) 的支援 (從 Windows 10 April 2018 Update 開始)。</span><span class="sxs-lookup"><span data-stu-id="7a824-192">.NET Framework 4.8 improves support for hosted HWNDs and Windows Forms interoperation in High-DPI WPF applications on platforms that support Mixed-Mode DPI scaling (starting with Windows 10 April 2018 Update).</span></span> <span data-ttu-id="7a824-193">當裝載的 HWNDs 或 Windows Forms 控制項建立為「混合模式 DPI 縮放」視窗 (透過呼叫 [SetThreadDpiHostingBehavior](/windows/desktop/api/winuser/nf-winuser-setthreaddpihostingbehavior) 與 [SetThreadDpiAwarenessContext](/windows/desktop/api/winuser/nf-winuser-setthreaddpiawarenesscontext)) 時，它們可以裝載在個別監視器 V2 WPF 應用程式中，並適當地調整大小及比例。</span><span class="sxs-lookup"><span data-stu-id="7a824-193">When hosted HWNDs or Windows Forms controls are created as Mixed-Mode DPI-scaled windows by calling [SetThreadDpiHostingBehavior](/windows/desktop/api/winuser/nf-winuser-setthreaddpihostingbehavior) and [SetThreadDpiAwarenessContext](/windows/desktop/api/winuser/nf-winuser-setthreaddpiawarenesscontext), they can be hosted in a Per-Monitor V2 WPF application and are sized and scaled appropriately.</span></span> <span data-ttu-id="7a824-194">此類裝載內容不會以原生 DPI 轉譯；相反地，作業系統會將裝載內容調整為適當的大小。</span><span class="sxs-lookup"><span data-stu-id="7a824-194">Such hosted content is not rendered at the native DPI; instead, the operating system scales the hosted content to the appropriate size.</span></span> <span data-ttu-id="7a824-195">對「個別監視器 v2 DPI 感知」的支援也允許在高 DPI 應用程式的原生視窗中裝載 WPF 控制項 (亦即，父項化)。</span><span class="sxs-lookup"><span data-stu-id="7a824-195">The support for Per-Monitor v2 DPI awareness mode also allows WPF controls to be hosted (i.e., parented) in a native window in a high-DPI application.</span></span>

<span data-ttu-id="7a824-196">為啟用對「混合模式高 DPI 縮放比例」的支援，您可以在應用程式設定檔中設定下列 [AppContext](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) 切換參數：</span><span class="sxs-lookup"><span data-stu-id="7a824-196">To enable support for Mixed-Mode High DPI scaling, you can set the following [AppContext](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) switches the application configuration file:</span></span>

```xml
<runtime>
   <AppContextSwitchOverrides value = "Switch.System.Windows.DoNotScaleForDpiChanges=false; Switch.System.Windows.DoNotUsePresentationDpiCapabilityTier2OrGreater=false"/>
</runtime>
```

<a name="clr48"></a>

#### <a name="common-language-runtime"></a><span data-ttu-id="7a824-197">Common Language Runtime</span><span class="sxs-lookup"><span data-stu-id="7a824-197">Common language runtime</span></span>

<span data-ttu-id="7a824-198">.NET Framework 4.8 中的執行階段包括下列變更與改良功能：</span><span class="sxs-lookup"><span data-stu-id="7a824-198">The runtime in .NET Framework 4.8 includes the following changes and improvements:</span></span>

<span data-ttu-id="7a824-199">**JIT 編譯器的改良功能**。</span><span class="sxs-lookup"><span data-stu-id="7a824-199">**Improvements to the JIT compiler**.</span></span> <span data-ttu-id="7a824-200">.NET Framework 4.8 中的 Just-In-Time (JIT) 編譯器是以 .NET Core 2.1 中的 JIT 編譯器為基礎。</span><span class="sxs-lookup"><span data-stu-id="7a824-200">The Just-in-time (JIT) compiler in .NET Framework 4.8 is based on the JIT compiler in .NET Core 2.1.</span></span> <span data-ttu-id="7a824-201">.NET Framework 4.8 JIT 編譯器中包括對 .NET Core 2.1 JIT 編譯器進行的許多最佳化與所有錯誤 (Bug) 修正。</span><span class="sxs-lookup"><span data-stu-id="7a824-201">Many of the optimizations and all of the bug fixes made to the .NET Core 2.1 JIT compiler are included in the .NET Framework 4.8 JIT compiler.</span></span>

<span data-ttu-id="7a824-202">**NGEN 改良功能**。</span><span class="sxs-lookup"><span data-stu-id="7a824-202">**NGEN improvements**.</span></span> <span data-ttu-id="7a824-203">執行階段已針對 [Native Image Generator](../tools/ngen-exe-native-image-generator.md) (NGEN) 映像改良其記憶體管理，以便從 NGEN 映像對應的資料不會常駐在記憶體中。</span><span class="sxs-lookup"><span data-stu-id="7a824-203">The runtime has improved its memory management for [Native Image Generator](../tools/ngen-exe-native-image-generator.md) (NGEN) images so that data mapped from NGEN images are not memory-resident.</span></span> <span data-ttu-id="7a824-204">這有效減少受攻擊面，以防止攻擊者嘗試透過修正將執行的記憶體來執行任意程式碼。</span><span class="sxs-lookup"><span data-stu-id="7a824-204">This reduces the surface area available to attacks that attempt to execute arbitrary code by modifying memory that will be executed.</span></span>

<span data-ttu-id="7a824-205">**所有組件的反惡意程式碼軟體掃描**。</span><span class="sxs-lookup"><span data-stu-id="7a824-205">**Antimalware scanning for all assemblies**.</span></span> <span data-ttu-id="7a824-206">在舊版 .NET Framework 中，執行階段會使用 Windows Defender 或第三方反惡意程式碼軟體來掃描從磁碟載入的所有組件。</span><span class="sxs-lookup"><span data-stu-id="7a824-206">In previous versions of the .NET Framework, the runtime scans all assemblies loaded from disk using either Windows Defender or third-party antimalware software.</span></span> <span data-ttu-id="7a824-207">不過，不會掃描從其他來源 (例如透過 <xref:System.Reflection.Assembly.Load(System.Byte[])?displayProperty=nameWithType> 方法) 載入的組件，因此這些組件可能包含未經偵測的惡意程式碼。</span><span class="sxs-lookup"><span data-stu-id="7a824-207">However, assemblies loaded from other sources, such as by the <xref:System.Reflection.Assembly.Load(System.Byte[])?displayProperty=nameWithType> method, are not scanned and can potentially contain undetected malware.</span></span> <span data-ttu-id="7a824-208">從在 Windows 10 上執行的 .NET Framework 4.8 開始，執行階段會觸發由實作[反惡意程式碼掃描介面 (AMSI)](/windows/desktop/AMSI/antimalware-scan-interface-portal) 之反惡意程式碼解決方案進行的掃描。</span><span class="sxs-lookup"><span data-stu-id="7a824-208">Starting with .NET Framework 4.8 running on Windows 10, the runtime triggers a scan by antimalware solutions that implement the [Antimalware Scan Interface (AMSI)](/windows/desktop/AMSI/antimalware-scan-interface-portal).</span></span>

<a name="v472"></a>

## <a name="whats-new-in-net-framework-472"></a><span data-ttu-id="7a824-209">.NET Framework 4.7.2 中的新功能</span><span class="sxs-lookup"><span data-stu-id="7a824-209">What's new in .NET Framework 4.7.2</span></span>

<span data-ttu-id="7a824-210">.NET Framework 4.7.2 包含下列領域的新功能：</span><span class="sxs-lookup"><span data-stu-id="7a824-210">.NET Framework 4.7.2 includes new features in the following areas:</span></span>

- [<span data-ttu-id="7a824-211">基底類別</span><span class="sxs-lookup"><span data-stu-id="7a824-211">Base classes</span></span>](#core-472)
- [<span data-ttu-id="7a824-212">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7a824-212">ASP.NET</span></span>](#asp-net472)
- [<span data-ttu-id="7a824-213">網路功能</span><span class="sxs-lookup"><span data-stu-id="7a824-213">Networking</span></span>](#net472)
- [<span data-ttu-id="7a824-214">SQL</span><span class="sxs-lookup"><span data-stu-id="7a824-214">SQL</span></span>](#sql472)
- [<span data-ttu-id="7a824-215">WPF</span><span class="sxs-lookup"><span data-stu-id="7a824-215">WPF</span></span>](#wpf472)
- [<span data-ttu-id="7a824-216">ClickOnce</span><span class="sxs-lookup"><span data-stu-id="7a824-216">ClickOnce</span></span>](#clickonce)

<span data-ttu-id="7a824-217">.NET Framework 4.7.2 中的主要焦點是改善協助工具，以允許應用程式為輔助技術使用者提供適當的體驗。</span><span class="sxs-lookup"><span data-stu-id="7a824-217">A continuing focus in .NET Framework 4.7.2 is improved accessibility, which allows an application to provide an appropriate experience for users of Assistive Technology.</span></span> <span data-ttu-id="7a824-218">如需 .NET Framework 4.7.2 中協助工具改善的資訊；請參閱 [.NET Framework 協助工具的新功能](whats-new-in-accessibility.md)。</span><span class="sxs-lookup"><span data-stu-id="7a824-218">For information on accessibility improvements in .NET Framework 4.7.2, see [What's new in accessibility in the .NET Framework](whats-new-in-accessibility.md).</span></span>

<a name="core-472"></a>

#### <a name="base-classes"></a><span data-ttu-id="7a824-219">基底類別</span><span class="sxs-lookup"><span data-stu-id="7a824-219">Base classes</span></span>

<span data-ttu-id="7a824-220">.NET Framework 4.7.2 具有大量的密碼編譯增強功能、更好的 ZIP 封存解壓縮支援，以及其他集合 API。</span><span class="sxs-lookup"><span data-stu-id="7a824-220">.NET Framework 4.7.2 features a large number of cryptographic enhancements, better decompression support for ZIP archives, and additional collection APIs.</span></span>

<span data-ttu-id="7a824-221">**RRSA.Create 和 DSA.Create 的新多載**</span><span class="sxs-lookup"><span data-stu-id="7a824-221">**New overloads of RSA.Create and DSA.Create**</span></span>

<span data-ttu-id="7a824-222"><xref:System.Security.Cryptography.DSA.Create(System.Security.Cryptography.DSAParameters)?displayProperty=nameWithType> 和 <xref:System.Security.Cryptography.RSA.Create(System.Security.Cryptography.RSAParameters)?displayProperty=nameWithType> 方法可讓您在具現化新的<xref:System.Security.Cryptography.DSA> 或 <xref:System.Security.Cryptography.RSA> 機碼時提供機碼參數。</span><span class="sxs-lookup"><span data-stu-id="7a824-222">The <xref:System.Security.Cryptography.DSA.Create(System.Security.Cryptography.DSAParameters)?displayProperty=nameWithType> and <xref:System.Security.Cryptography.RSA.Create(System.Security.Cryptography.RSAParameters)?displayProperty=nameWithType> methods let you supply key parameters when instantiating a new <xref:System.Security.Cryptography.DSA> or <xref:System.Security.Cryptography.RSA> key.</span></span> <span data-ttu-id="7a824-223">它們可讓您將下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="7a824-223">They allow you to replace code like the following:</span></span>

```csharp
// Before .NET Framework 4.7.2
using (RSA rsa = RSA.Create())
{
   rsa.ImportParameters(rsaParameters);
   // Other code to execute using the RSA instance.
}
```

```vb
' Before .NET Framework 4.7.2
Using rsa = RSA.Create()
   rsa.ImportParameters(rsaParameters)
   ' Other code to execute using the rsa instance.
End Using
```

<span data-ttu-id="7a824-224">取代為如下的程式碼：</span><span class="sxs-lookup"><span data-stu-id="7a824-224">with code like this:</span></span>

```csharp
// Starting with .NET Framework 4.7.2
using (RSA rsa = RSA.Create(rsaParameters))
{
   // Other code to execute using the rsa instance.
}
```

```vb
' Starting with .NET Framework 4.7.2
Using rsa = RSA.Create(rsaParameters)
   ' Other code to execute using the rsa instance.
End Using
```

<span data-ttu-id="7a824-225"><xref:System.Security.Cryptography.DSA.Create(System.Int32)?displayProperty=nameWithType> 和 <xref:System.Security.Cryptography.RSA.Create(System.Int32)?displayProperty=nameWithType> 方法可讓您產生具有特定金鑰大小的新 <xref:System.Security.Cryptography.DSA> 或 <xref:System.Security.Cryptography.RSA> 金鑰。</span><span class="sxs-lookup"><span data-stu-id="7a824-225">The <xref:System.Security.Cryptography.DSA.Create(System.Int32)?displayProperty=nameWithType> and <xref:System.Security.Cryptography.RSA.Create(System.Int32)?displayProperty=nameWithType> methods let you generate new <xref:System.Security.Cryptography.DSA> or <xref:System.Security.Cryptography.RSA> keys with a specific key size.</span></span> <span data-ttu-id="7a824-226">例如：</span><span class="sxs-lookup"><span data-stu-id="7a824-226">For example:</span></span>

```csharp
using (DSA dsa = DSA.Create(2048))
{
   // Other code to execute using the dsa instance.
}
```

```vb
Using dsa = DSA.Create(2048)
   ' Other code to execute using the dsa instance.
End Using
```

<span data-ttu-id="7a824-227">**Rfc2898DeriveBytes 建構函式接受雜湊演算法名稱**</span><span class="sxs-lookup"><span data-stu-id="7a824-227">**Rfc2898DeriveBytes constructors accept a hash algorithm name**</span></span>

<span data-ttu-id="7a824-228"><xref:System.Security.Cryptography.Rfc2898DeriveBytes> 類別有三個新的建構函式，這些建構函式使用 <xref:System.Security.Cryptography.HashAlgorithmName> 參數以識別衍生金鑰時所要使用的 HMAC 演算法。</span><span class="sxs-lookup"><span data-stu-id="7a824-228">The <xref:System.Security.Cryptography.Rfc2898DeriveBytes> class has three new constructors with a <xref:System.Security.Cryptography.HashAlgorithmName> parameter that identifies the HMAC algorithm to use when deriving keys.</span></span> <span data-ttu-id="7a824-229">開發人員不應使用 SHA-1，而應使用 SHA-256 之類的 SHA-2 式 HMAC，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="7a824-229">Instead of using SHA-1, developers should use a SHA-2-based HMAC like SHA-256, as shown in the following example:</span></span>

```csharp
private static byte[] DeriveKey(string password, out int iterations, out byte[] salt,
                                out HashAlgorithmName algorithm)
{
   iterations = 100000;
   algorithm = HashAlgorithmName.SHA256;

   const int SaltSize = 32;
   const int DerivedValueSize = 32;

   using (Rfc2898DeriveBytes pbkdf2 = new Rfc2898DeriveBytes(password, SaltSize,
                                                             iterations, algorithm))
   {
      salt = pbkdf2.Salt;
      return pbkdf2.GetBytes(DerivedValueSize);
   }
}
```

```vb
Private Shared Function DeriveKey(password As String, ByRef iterations As Integer,
                                  ByRef salt AS Byte(), ByRef algorithm As HashAlgorithmName) As Byte()
   iterations = 100000
   algorithm = HashAlgorithmName.SHA256

   Const SaltSize As Integer = 32
   Const  DerivedValueSize As Integer = 32

   Using pbkdf2 = New Rfc2898DeriveBytes(password, SaltSize, iterations, algorithm)
      salt = pbkdf2.Salt
      Return pbkdf2.GetBytes(DerivedValueSize)
   End Using
End Function
```

<span data-ttu-id="7a824-230">**支援暫時金鑰**</span><span class="sxs-lookup"><span data-stu-id="7a824-230">**Support for ephemeral keys**</span></span>

<span data-ttu-id="7a824-231">PFX 匯入可以選擇性地從記憶體中直接載入私密金鑰，並略過硬碟。</span><span class="sxs-lookup"><span data-stu-id="7a824-231">PFX import can optionally load private keys directly from memory, bypassing the hard drive.</span></span><span data-ttu-id="7a824-232">在 <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> 建構函式或 <xref:System.Security.Cryptography.X509Certificates.X509Certificate2.Import%2A?displayProperty=nameWithType> 方法的其中一個多載中指定了 <xref:System.Security.Cryptography.X509Certificates.X509KeyStorageFlags.EphemeralKeySet?displayProperty=nameWithType> 旗標時，私密金鑰將載入為暫時金鑰。</span><span class="sxs-lookup"><span data-stu-id="7a824-232"> When the new <xref:System.Security.Cryptography.X509Certificates.X509KeyStorageFlags.EphemeralKeySet?displayProperty=nameWithType> flag is specified in an <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> constructor or one of the overloads of the <xref:System.Security.Cryptography.X509Certificates.X509Certificate2.Import%2A?displayProperty=nameWithType> method, the private keys will be loaded as ephemeral keys.</span></span> <span data-ttu-id="7a824-233">這可防止在磁碟上顯示金鑰。</span><span class="sxs-lookup"><span data-stu-id="7a824-233">This prevents the keys from being visible on the disk.</span></span> <span data-ttu-id="7a824-234">但是：</span><span class="sxs-lookup"><span data-stu-id="7a824-234">However:</span></span>

- <span data-ttu-id="7a824-235">由於金鑰不會保存到磁碟，使用這個旗標載入的憑證就不是新增至 X509Store 的適當候選項目。</span><span class="sxs-lookup"><span data-stu-id="7a824-235">Since the keys are not persisted to disk, certificates loaded with this flag are not good candidates to add to an X509Store.</span></span>

- <span data-ttu-id="7a824-236">以這種方式載入的金鑰幾乎一律都是透過 Windows CNG 載入。</span><span class="sxs-lookup"><span data-stu-id="7a824-236">Keys loaded in this manner are almost always loaded via Windows CNG.</span></span> <span data-ttu-id="7a824-237">因此，呼叫端必須透過呼叫擴充方法 (例如 [cert.GetRSAPrivateKey()](xref:System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPrivateKey%2A)) 來存取私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="7a824-237">Therefore, callers must access the private key by calling extension methods, such as [cert.GetRSAPrivateKey()](xref:System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPrivateKey%2A).</span></span> <span data-ttu-id="7a824-238"><xref:System.Security.Cryptography.X509Certificates.X509Certificate2.PrivateKey?displayProperty=nameWithType> 屬性沒有作用。</span><span class="sxs-lookup"><span data-stu-id="7a824-238">The <xref:System.Security.Cryptography.X509Certificates.X509Certificate2.PrivateKey?displayProperty=nameWithType> property does not function.</span></span>

- <span data-ttu-id="7a824-239">由於舊版 <xref:System.Security.Cryptography.X509Certificates.X509Certificate2.PrivateKey?displayProperty=nameWithType> 屬性不適用於憑證，開發人員應該先執行嚴格的測試，再切換至暫時金鑰。</span><span class="sxs-lookup"><span data-stu-id="7a824-239">Since the legacy <xref:System.Security.Cryptography.X509Certificates.X509Certificate2.PrivateKey?displayProperty=nameWithType> property does not work with certificates, developers should perform rigorous testing before switching to ephemeral keys.</span></span>

<span data-ttu-id="7a824-240">**以程式設計方式建立 PKCS#10 憑證簽署要求時和 X.509 公開金鑰憑證**</span><span class="sxs-lookup"><span data-stu-id="7a824-240">**Programmatic creation of PKCS#10 certification signing requests and X.509 public key certificates**</span></span>

<span data-ttu-id="7a824-241">從 .NET Framework 4.7.2 開始，工作負載可以產生憑證簽署要求 (CSR)，這可讓憑證要求產生作業暫存到現有工具中。</span><span class="sxs-lookup"><span data-stu-id="7a824-241">Starting with .NET Framework 4.7.2, workloads can generate certificate signing requests (CSRs), which allows certificate request generation to be staged into existing tooling.</span></span> <span data-ttu-id="7a824-242">這在測試案例中通常很有用。</span><span class="sxs-lookup"><span data-stu-id="7a824-242">This is frequently useful in test scenarios.</span></span>

<span data-ttu-id="7a824-243">如需詳細資訊與程式碼範例，請參閱 [.NET 部落格](https://devblogs.microsoft.com/dotnet/net-framework-4-7-2-developer-pack-early-access-build-3056-is-available/)中的＜以程式設計方式建立 PKCS#10 憑證簽署要求和 X.509 公開金鑰憑證＞。</span><span class="sxs-lookup"><span data-stu-id="7a824-243">For more information and code examples, see "Programmatic creation of PKCS#10 certification signing requests and X.509 public key certificates" in the [.NET Blog](https://devblogs.microsoft.com/dotnet/net-framework-4-7-2-developer-pack-early-access-build-3056-is-available/).</span></span>

<span data-ttu-id="7a824-244">**新的 SignerInfo 成員**</span><span class="sxs-lookup"><span data-stu-id="7a824-244">**New SignerInfo members**</span></span>

<span data-ttu-id="7a824-245">從 .NET Framework 4.7.2 開始，<xref:System.Security.Cryptography.Pkcs.SignerInfo> 類別會公開簽章的相關詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7a824-245">Starting with .NET Framework 4.7.2, the <xref:System.Security.Cryptography.Pkcs.SignerInfo> class exposes more information about the signature.</span></span> <span data-ttu-id="7a824-246">您可以擷取 <xref:System.Security.Cryptography.Pkcs.SignerInfo.SignatureAlgorithm?displayProperty=fullName> 屬性的值來判斷簽署者使用的簽章演算法。</span><span class="sxs-lookup"><span data-stu-id="7a824-246">You can retrieve the value of the <xref:System.Security.Cryptography.Pkcs.SignerInfo.SignatureAlgorithm?displayProperty=fullName> property to determine the signature algorithm used by the signer.</span></span> <span data-ttu-id="7a824-247">可以呼叫 <xref:System.Security.Cryptography.Pkcs.SignerInfo.GetSignature%2A?displayProperty=nameWithType> 來取得此簽署者的密碼編譯簽章的複本。</span><span class="sxs-lookup"><span data-stu-id="7a824-247"><xref:System.Security.Cryptography.Pkcs.SignerInfo.GetSignature%2A?displayProperty=nameWithType> can be called to get a copy of the cryptographic signature for this signer.</span></span>

<span data-ttu-id="7a824-248">**在處置 CryptoStream 之後保持包裝資料流開啟**</span><span class="sxs-lookup"><span data-stu-id="7a824-248">**Leaving a wrapped stream open after CryptoStream is disposed**</span></span>

<span data-ttu-id="7a824-249">從 .NET Framework 4.7.2 開始，<xref:System.Security.Cryptography.CryptoStream> 類別具有其他建構函式，可讓 <xref:System.Security.Cryptography.CryptoStream.Dispose%2A> 不關閉包裝資料流。</span><span class="sxs-lookup"><span data-stu-id="7a824-249">Starting with .NET Framework 4.7.2, the <xref:System.Security.Cryptography.CryptoStream> class has an additional constructor that allows <xref:System.Security.Cryptography.CryptoStream.Dispose%2A> to not close the wrapped stream.</span></span><span data-ttu-id="7a824-250">若要在處置 <xref:System.Security.Cryptography.CryptoStream> 執行個體之後將包裝資料流保持開啟，請呼叫新的 <xref:System.Security.Cryptography.CryptoStream> 建構函式，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7a824-250"> To leave the wrapped stream open after the <xref:System.Security.Cryptography.CryptoStream> instance is disposed, call the new <xref:System.Security.Cryptography.CryptoStream> constructor as follows:</span></span>

```csharp
var cStream = new CryptoStream(stream, transform, mode, leaveOpen: true);
```

```vb
Dim cStream = New CryptoStream(stream, transform, mode, leaveOpen:=true)
```

<span data-ttu-id="7a824-251">**DeflateStream 中的解壓縮變更**</span><span class="sxs-lookup"><span data-stu-id="7a824-251">**Decompression changes in DeflateStream**</span></span>

<span data-ttu-id="7a824-252">從 .NET Framework 4.7.2 開始，<xref:System.IO.Compression.DeflateStream> 類別中的解壓縮作業實作已變更為預設使用原生 Windows API。</span><span class="sxs-lookup"><span data-stu-id="7a824-252">Starting with .NET Framework 4.7.2, the implementation of decompression operations in the <xref:System.IO.Compression.DeflateStream> class has changed to use native Windows APIs by default.</span></span> <span data-ttu-id="7a824-253">一般而言，這會導致顯著的效能改善。</span><span class="sxs-lookup"><span data-stu-id="7a824-253">Typically, this results in a substantial performance improvement.</span></span>

<span data-ttu-id="7a824-254">以 .NET Framework 4.7.2 為目標的應用程式，預設會啟用使用 Windows API 進行解壓縮的支援。</span><span class="sxs-lookup"><span data-stu-id="7a824-254">Support for decompression by using Windows APIs is enabled by default for applications that target .NET Framework 4.7.2.</span></span> <span data-ttu-id="7a824-255">如果應用程式是以舊版 .NET Framework 為目標，但卻在 .NET Framework 4.7.2 下執行，則可在應用程式組態檔中新增下列 [AppContext 參數](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md)，以選擇加入此行為：</span><span class="sxs-lookup"><span data-stu-id="7a824-255">Applications that target earlier versions of .NET Framework but are running under .NET Framework 4.7.2 can opt into this behavior by adding the following [AppContext switch](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) to the application configuration file:</span></span>

```xml
<AppContextSwitchOverrides value="Switch.System.IO.Compression.DoNotUseNativeZipLibraryForDecompression=false" />
```

<span data-ttu-id="7a824-256">**其他集合 API**</span><span class="sxs-lookup"><span data-stu-id="7a824-256">**Additional collection APIs**</span></span>

<span data-ttu-id="7a824-257">.NET Framework 4.7.2 將一些新的 API 新增至 <xref:System.Collections.Generic.SortedSet%601> 和 <xref:System.Collections.Generic.HashSet%601> 類型。</span><span class="sxs-lookup"><span data-stu-id="7a824-257">.NET Framework 4.7.2 adds a number of new APIs to the <xref:System.Collections.Generic.SortedSet%601> and <xref:System.Collections.Generic.HashSet%601> types.</span></span> <span data-ttu-id="7a824-258">其中包括：</span><span class="sxs-lookup"><span data-stu-id="7a824-258">These include:</span></span>

- <span data-ttu-id="7a824-259">`TryGetValue` 方法，可將其他集合類型使用的 try 模式擴充為下列兩種類型。</span><span class="sxs-lookup"><span data-stu-id="7a824-259">`TryGetValue` methods, which extend the try pattern used in other collection types to these two types.</span></span> <span data-ttu-id="7a824-260">這些方法為：</span><span class="sxs-lookup"><span data-stu-id="7a824-260">The methods are:</span></span>

  - [<span data-ttu-id="7a824-261">public bool HashSet\<T>.TryGetValue(T equalValue, out T actualValue)</span><span class="sxs-lookup"><span data-stu-id="7a824-261">public bool HashSet\<T>.TryGetValue(T equalValue, out T actualValue)</span></span>](xref:System.Collections.Generic.SortedSet%601.TryGetValue%2A)
  - [<span data-ttu-id="7a824-262">public bool SortedSet\<T>.TryGetValue(T equalValue, out T actualValue)</span><span class="sxs-lookup"><span data-stu-id="7a824-262">public bool SortedSet\<T>.TryGetValue(T equalValue, out T actualValue)</span></span>](xref:System.Collections.Generic.SortedSet%601.TryGetValue%2A)

- <span data-ttu-id="7a824-263">`Enumerable.To*` 擴充方法，可將集合轉換為 <xref:System.Collections.Generic.HashSet%601>：</span><span class="sxs-lookup"><span data-stu-id="7a824-263">`Enumerable.To*` extension methods, which convert a collection to a <xref:System.Collections.Generic.HashSet%601>:</span></span>

  - [<span data-ttu-id="7a824-264">public static HashSet\<TSource> ToHashSet\<TSource>(此 IEnumerable\<TSource> 來源)</span><span class="sxs-lookup"><span data-stu-id="7a824-264">public static HashSet\<TSource> ToHashSet\<TSource>(this IEnumerable\<TSource> source)</span></span>](xref:System.Linq.Enumerable.ToHashSet%2A)
  - [<span data-ttu-id="7a824-265">public static HashSet\<TSource> ToHashSet\<TSource>(此 IEnumerable\<TSource> 來源, IEqualityComparer\<TSource> 比較子)</span><span class="sxs-lookup"><span data-stu-id="7a824-265">public static HashSet\<TSource> ToHashSet\<TSource>(this IEnumerable\<TSource> source, IEqualityComparer\<TSource> comparer)</span></span>](xref:System.Linq.Enumerable.ToHashSet%2A)

- <span data-ttu-id="7a824-266">可讓您設定集合容量的新 <xref:System.Collections.Generic.HashSet%601> 建構函式，當您事先知道 <xref:System.Collections.Generic.HashSet%601> 的大小時，便能產生效能優勢：</span><span class="sxs-lookup"><span data-stu-id="7a824-266">New <xref:System.Collections.Generic.HashSet%601> constructors that let you set the collection's capacity, which yields a performance benefit when you know the size of the <xref:System.Collections.Generic.HashSet%601> in advance:</span></span>

  - <span data-ttu-id="7a824-267">[public HashSet(int capacity)](xref:System.Collections.Generic.HashSet%601.%23ctor(System.Int32))</span><span class="sxs-lookup"><span data-stu-id="7a824-267">[public HashSet(int capacity)](xref:System.Collections.Generic.HashSet%601.%23ctor(System.Int32))</span></span>
  - <span data-ttu-id="7a824-268">[public HashSet(int capacity, IEqualityComparer\<T> comparer)](xref:System.Collections.Generic.HashSet%601.%23ctor(System.Int32,System.Collections.Generic.IEqualityComparer%7B%600%7D))</span><span class="sxs-lookup"><span data-stu-id="7a824-268">[public HashSet(int capacity, IEqualityComparer\<T> comparer)](xref:System.Collections.Generic.HashSet%601.%23ctor(System.Int32,System.Collections.Generic.IEqualityComparer%7B%600%7D))</span></span>

<span data-ttu-id="7a824-269"><xref:System.Collections.Concurrent.ConcurrentDictionary%602> 類別包今 <xref:System.Collections.Concurrent.ConcurrentDictionary%602.AddOrUpdate%2A> 和 <xref:System.Collections.Concurrent.ConcurrentDictionary%602.GetOrAdd%2A> 方法的新多載，可從字典擷取值或在找不到值時新增它，以及將值新增至字典或在值已存在時進行更新。</span><span class="sxs-lookup"><span data-stu-id="7a824-269">The <xref:System.Collections.Concurrent.ConcurrentDictionary%602> class includes new overloads of the <xref:System.Collections.Concurrent.ConcurrentDictionary%602.AddOrUpdate%2A> and <xref:System.Collections.Concurrent.ConcurrentDictionary%602.GetOrAdd%2A> methods to retrieve a value from the dictionary or to add it if it is not found, and to add a value to the dictionary or to update it if it already exists.</span></span>

```csharp
public TValue AddOrUpdate<TArg>(TKey key, Func<TKey, TArg, TValue> addValueFactory, Func<TKey, TValue, TArg, TValue> updateValueFactory, TArg factoryArgument)

public TValue GetOrAdd<TArg>(TKey key, Func<TKey, TArg, TValue> valueFactory, TArg factoryArgument)
```

```vb
Public AddOrUpdate(Of TArg)(key As TKey, addValueFactory As Func(Of TKey, TArg, TValue), updateValueFactory As Func(Of TKey, TValue, TArg, TValue), factoryArgument As TArg) As TValue

Public GetOrAdd(Of TArg)(key As TKey, valueFactory As Func(Of TKey, TArg, TValue), factoryArgument As TArg) As TValue
```

<a name="asp-net472"></a>

#### <a name="aspnet"></a><span data-ttu-id="7a824-270">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7a824-270">ASP.NET</span></span>

<span data-ttu-id="7a824-271">**支援 Web Forms 中的相依性插入**</span><span class="sxs-lookup"><span data-stu-id="7a824-271">**Support for dependency injection in Web Forms**</span></span>

<span data-ttu-id="7a824-272">[相依性插入 (DI)](/aspnet/core/fundamentals/dependency-injection#overview-of-dependency-injection) 可分離物件和其相依性，讓物件的程式碼不再需要只因相依性變更而變更。</span><span class="sxs-lookup"><span data-stu-id="7a824-272">[Dependency injection (DI)](/aspnet/core/fundamentals/dependency-injection#overview-of-dependency-injection) decouples objects and their dependencies so that an object's code no longer needs to be changed just because a dependency has changed.</span></span> <span data-ttu-id="7a824-273">開發以 .NET Framework 4.7.2 為目標的 ASP.NET 應用程式時，您可以：</span><span class="sxs-lookup"><span data-stu-id="7a824-273">When developing ASP.NET applications that target .NET Framework 4.7.2, you can:</span></span>

- <span data-ttu-id="7a824-274">在 ASP.NET Web 應用程式專案的[處理常式和模組](/previous-versions/aspnet/bb398986(v=vs.100))、[網頁執行個體](xref:System.Web.UI.Page)和[使用者控制項](/previous-versions/aspnet/y6wb1a0e(v=vs.100))中使用 Setter 型、介面型和建構函式型插入。</span><span class="sxs-lookup"><span data-stu-id="7a824-274">Use setter-based, interface-based, and constructor-based injection in [handlers and modules](/previous-versions/aspnet/bb398986(v=vs.100)), [Page instances](xref:System.Web.UI.Page), and [user controls](/previous-versions/aspnet/y6wb1a0e(v=vs.100)) of ASP.NET web application projects.</span></span>

- <span data-ttu-id="7a824-275">在 ASP.NET 網站專案的[處理常式和模組](/previous-versions/aspnet/bb398986(v=vs.100))、[網頁執行個體](xref:System.Web.UI.Page)和[使用者控制項](/previous-versions/aspnet/y6wb1a0e(v=vs.100))中使用 Setter 型和介面型插入。</span><span class="sxs-lookup"><span data-stu-id="7a824-275">Use setter-based and interface-based injection in [handlers and modules](/previous-versions/aspnet/bb398986(v=vs.100)), [Page instances](xref:System.Web.UI.Page), and [user controls](/previous-versions/aspnet/y6wb1a0e(v=vs.100)) of ASP.NET web site projects.</span></span>

- <span data-ttu-id="7a824-276">在不同的相依性插入架構中插入。</span><span class="sxs-lookup"><span data-stu-id="7a824-276">Plug in different dependency injection frameworks.</span></span>

<span data-ttu-id="7a824-277">**支援相同網站 Cookie**</span><span class="sxs-lookup"><span data-stu-id="7a824-277">**Support for same-site cookies**</span></span>

<span data-ttu-id="7a824-278">[SameSite](https://tools.ietf.org/html/draft-west-first-party-cookies-07) 可防止瀏覽器將 Cookie 與跨站台要求一起傳送。</span><span class="sxs-lookup"><span data-stu-id="7a824-278">[SameSite](https://tools.ietf.org/html/draft-west-first-party-cookies-07) prevents a browser from sending a cookie along with a cross-site request.</span></span> <span data-ttu-id="7a824-279">.NET Framework 4.7.2 會新增其值是 <xref:System.Web.SameSiteMode?displayProperty=nameWithType> 列舉成員的 <xref:System.Web.HttpCookie.SameSite?displayProperty=nameWithType> 屬性。</span><span class="sxs-lookup"><span data-stu-id="7a824-279">.NET Framework 4.7.2 adds a <xref:System.Web.HttpCookie.SameSite?displayProperty=nameWithType> property whose value is a <xref:System.Web.SameSiteMode?displayProperty=nameWithType> enumeration member.</span></span> <span data-ttu-id="7a824-280">如果其值為 <xref:System.Web.SameSiteMode.Strict?displayProperty=nameWithType> 或 <xref:System.Web.SameSiteMode.Lax?displayProperty=nameWithType>，ASP.NET 會將 `SameSite` 屬性新增至 set-cookie 標頭。</span><span class="sxs-lookup"><span data-stu-id="7a824-280">If its value is <xref:System.Web.SameSiteMode.Strict?displayProperty=nameWithType> or <xref:System.Web.SameSiteMode.Lax?displayProperty=nameWithType>, ASP.NET adds the `SameSite` attribute to the set-cookie header.</span></span> <span data-ttu-id="7a824-281">SameSite 支援適用於 <xref:System.Web.HttpCookie> 物件，以及適用於 <xref:System.Web.Security.FormsAuthentication> 和 <xref:System.Web.SessionState> Cookie。</span><span class="sxs-lookup"><span data-stu-id="7a824-281">SameSite support applies to <xref:System.Web.HttpCookie> objects, as well as to <xref:System.Web.Security.FormsAuthentication> and <xref:System.Web.SessionState> cookies.</span></span>

<span data-ttu-id="7a824-282">您可以為 <xref:System.Web.HttpCookie> 物件設定 SameSite，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7a824-282">You can set SameSite for an <xref:System.Web.HttpCookie> object as follows:</span></span>

```csharp
var c = new HttpCookie("secureCookie", "same origin");
c.SameSite = SameSiteMode.Lax;
```

```vb
Dim c As New HttpCookie("secureCookie", "same origin")
c.SameSite = SameSiteMode.Lax
```

<span data-ttu-id="7a824-283">您也可以修改 web.config 檔案，來設定應用程式層級的 SameSite Cookie：</span><span class="sxs-lookup"><span data-stu-id="7a824-283">You can also configure SameSite cookies at the application level by modifying the web.config file:</span></span>

```xml
<system.web>
   <httpCookies sameSite="Strict" />
</system.web>
```

<span data-ttu-id="7a824-284">您可以藉由修改網頁組態檔，為 <xref:System.Web.Security.FormsAuthentication> 和 <xref:System.Web.SessionState> Cookie 新增 SameSite：</span><span class="sxs-lookup"><span data-stu-id="7a824-284">You can add SameSite for <xref:System.Web.Security.FormsAuthentication> and <xref:System.Web.SessionState> cookies by modifying the web config file:</span></span>

```xml
<system.web>
   <authentication mode="Forms">
      <forms cookieSameSite="Lax">
         <!-- ...   -->
      </forms>
   </authentication>
   <sessionState cookieSameSite="Lax"></sessionState>
</system.web>
```

<a name="net472"></a>

#### <a name="networking"></a><span data-ttu-id="7a824-285">網路</span><span class="sxs-lookup"><span data-stu-id="7a824-285">Networking</span></span>

<span data-ttu-id="7a824-286">**實作 HttpClientHandler 屬性**</span><span class="sxs-lookup"><span data-stu-id="7a824-286">**Implementation of HttpClientHandler properties**</span></span>

<span data-ttu-id="7a824-287">.NET Framework 4.7.1 已將八個屬性新增至 <xref:System.Net.Http.HttpClientHandler?displayProperty=nameWithType> 類別。</span><span class="sxs-lookup"><span data-stu-id="7a824-287">.NET Framework 4.7.1 added eight properties to the <xref:System.Net.Http.HttpClientHandler?displayProperty=nameWithType> class.</span></span> <span data-ttu-id="7a824-288">不過，兩個會擲回 <xref:System.PlatformNotSupportedException>。</span><span class="sxs-lookup"><span data-stu-id="7a824-288">However, two threw a <xref:System.PlatformNotSupportedException>.</span></span> <span data-ttu-id="7a824-289">.NET Framework 4.7.2 現在會提供這些屬性的實作。</span><span class="sxs-lookup"><span data-stu-id="7a824-289">.NET Framework 4.7.2 now provides an implementation for these properties.</span></span> <span data-ttu-id="7a824-290">屬性如下︰</span><span class="sxs-lookup"><span data-stu-id="7a824-290">The properties are:</span></span>

- <xref:System.Net.Http.HttpClientHandler.CheckCertificateRevocationList>
- <xref:System.Net.Http.HttpClientHandler.SslProtocols>

<a name="sql472"></a>

#### <a name="sqlclient"></a><span data-ttu-id="7a824-291">SQLClient</span><span class="sxs-lookup"><span data-stu-id="7a824-291">SQLClient</span></span>

<span data-ttu-id="7a824-292">**支援 Azure Active Directory 通用驗證和多重要素驗證**</span><span class="sxs-lookup"><span data-stu-id="7a824-292">**Support for Azure Active Directory Universal Authentication and Multi-Factor authentication**</span></span>

<span data-ttu-id="7a824-293">持續成長的合規性和安全性需求需要許多客戶使用多重要素驗證 (MFA)。</span><span class="sxs-lookup"><span data-stu-id="7a824-293">Growing compliance and security demands require that many customers use multi-factor authentication (MFA).</span></span> <span data-ttu-id="7a824-294">此外，目前的最佳作法建議不要在連接字串中直接包括使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="7a824-294">In addition, current best practices discourage including user passwords directly in connection strings.</span></span> <span data-ttu-id="7a824-295">為支援這些變更，.NET Framework 4.7.2 透過為現有的 "Authentication" 關鍵字新增新值 "Active Directory Interactive" 來擴充 [SQLClient 連接字串](xref:System.Data.SqlClient.SqlConnection.ConnectionString)，以支援 MFA 和 [Azure AD 驗證](/azure/sql-database/sql-database-aad-authentication-configure)。</span><span class="sxs-lookup"><span data-stu-id="7a824-295">To support these changes, .NET Framework 4.7.2 extends [SQLClient connection strings](xref:System.Data.SqlClient.SqlConnection.ConnectionString) by adding a new value, "Active Directory Interactive", for the existing "Authentication" keyword to support MFA and [Azure AD Authentication](/azure/sql-database/sql-database-aad-authentication-configure).</span></span> <span data-ttu-id="7a824-296">新的互動式方法支援原生和同盟的 Azure AD 使用者，以及 Azure AD 來賓使用者。</span><span class="sxs-lookup"><span data-stu-id="7a824-296">The new interactive method supports native and federated Azure AD users as well as Azure AD guest users.</span></span> <span data-ttu-id="7a824-297">使用這個方法時，SQL 資料庫支援 Azure AD 所強制執行的 MFA 驗證。</span><span class="sxs-lookup"><span data-stu-id="7a824-297">When this method is used, the MFA authentication imposed by Azure AD is supported for SQL databases.</span></span> <span data-ttu-id="7a824-298">此外，驗證程序會要求使用者密碼遵循安全性最佳作法。</span><span class="sxs-lookup"><span data-stu-id="7a824-298">In addition, the authentication process requests a user password to adhere to security best practices.</span></span>

<span data-ttu-id="7a824-299">在舊版 .NET Framework 中，SQL 連接性只支援 <xref:System.Data.SqlClient.SqlAuthenticationMethod.ActiveDirectoryPassword?displayProperty=nameWithType> 和 <xref:System.Data.SqlClient.SqlAuthenticationMethod.ActiveDirectoryIntegrated?displayProperty=nameWithType> 選項。</span><span class="sxs-lookup"><span data-stu-id="7a824-299">In previous versions of the .NET Framework, SQL connectivity supported only the <xref:System.Data.SqlClient.SqlAuthenticationMethod.ActiveDirectoryPassword?displayProperty=nameWithType> and <xref:System.Data.SqlClient.SqlAuthenticationMethod.ActiveDirectoryIntegrated?displayProperty=nameWithType> options.</span></span> <span data-ttu-id="7a824-300">這兩種屬於非互動式 [ADAL 通訊協定](/azure/active-directory/develop/active-directory-authentication-libraries)，因此不支援 MFA。</span><span class="sxs-lookup"><span data-stu-id="7a824-300">Both of these are part of the non-interactive [ADAL protocol](/azure/active-directory/develop/active-directory-authentication-libraries), which does not support MFA.</span></span> <span data-ttu-id="7a824-301">利用新的 <xref:System.Data.SqlClient.SqlAuthenticationMethod.ActiveDirectoryInteractive?displayProperty=nameWithType> 選項，SQL 連接性支援 MFA 以及現有的驗證方法 (密碼和整合式驗證)，可讓使用者以互動方式輸入使用者密碼，而不需要將密碼保存到連接字串中。</span><span class="sxs-lookup"><span data-stu-id="7a824-301">With the new <xref:System.Data.SqlClient.SqlAuthenticationMethod.ActiveDirectoryInteractive?displayProperty=nameWithType> option, SQL connectivity supports MFA as well as existing authentication methods (password and integrated authentication), which allows users to enter user passwords interactively without persisting passwords in the connection string.</span></span>

<span data-ttu-id="7a824-302">如需詳細資訊和範例，請參閱 [.NET 部落格](https://devblogs.microsoft.com/dotnet/net-framework-4-7-2-developer-pack-early-access-build-3056-is-available/)中的＜Azure AD 通用和多重要素驗證＞。</span><span class="sxs-lookup"><span data-stu-id="7a824-302">For more information and an example, see "SQL -- Azure AD Universal and Multi-factor Authentication Support" in the [.NET Blog](https://devblogs.microsoft.com/dotnet/net-framework-4-7-2-developer-pack-early-access-build-3056-is-available/).</span></span>

<span data-ttu-id="7a824-303">**支援 Always Encrypted 第 2 版**</span><span class="sxs-lookup"><span data-stu-id="7a824-303">**Support for Always Encrypted version 2**</span></span>

<span data-ttu-id="7a824-304">NET Framework 4.7.2 會新增飛地式 Always Encrypted 的支援。</span><span class="sxs-lookup"><span data-stu-id="7a824-304">NET Framework 4.7.2 adds supports for enclave-based Always Encrypted.</span></span> <span data-ttu-id="7a824-305">Always Encrypted 的原始版本是加密金鑰絕不會離開用戶端的用戶端加密技術。</span><span class="sxs-lookup"><span data-stu-id="7a824-305">The original version of Always Encrypted is a client-side encryption technology in which encryption keys never leave the client.</span></span> <span data-ttu-id="7a824-306">在飛地式 Always Encrypted 中，用戶端可以選擇性地將加密金鑰傳送至安全飛地，也就是可視為 SQL Server 一部分，但 SQL Server 程式碼無法竄改的安全計算實體。</span><span class="sxs-lookup"><span data-stu-id="7a824-306">In enclave-based Always Encrypted, the client can optionally send the encryption keys to a secure enclave, which is a secure computational entity that can be considered part of SQL Server but that SQL Server code cannot tamper with.</span></span> <span data-ttu-id="7a824-307">為支援飛地式 Always Encrypted，.NET Framework 4.7.2 將下列類型和成員新增至 <xref:System.Data.SqlClient> 命名空間：</span><span class="sxs-lookup"><span data-stu-id="7a824-307">To support enclave-based Always Encrypted, .NET Framework 4.7.2 adds the following types and members to the <xref:System.Data.SqlClient> namespace:</span></span>

- <span data-ttu-id="7a824-308"><xref:System.Data.SqlClient.SqlConnectionStringBuilder.EnclaveAttestationUrl?displayProperty=nameWithType>，其可指定飛地式 Always Encrypted 的 URL。</span><span class="sxs-lookup"><span data-stu-id="7a824-308"><xref:System.Data.SqlClient.SqlConnectionStringBuilder.EnclaveAttestationUrl?displayProperty=nameWithType>, which specifies the Uri for enclave-based Always Encrypted.</span></span>

- <span data-ttu-id="7a824-309"><xref:System.Data.SqlClient.SqlColumnEncryptionEnclaveProvider>，這是所有飛地提供者衍生來源的抽象類別。</span><span class="sxs-lookup"><span data-stu-id="7a824-309"><xref:System.Data.SqlClient.SqlColumnEncryptionEnclaveProvider>, which is an abstract class from which all enclave providers are derived.</span></span>

- <span data-ttu-id="7a824-310"><xref:System.Data.SqlClient.SqlEnclaveSession>，其可封裝指定的飛地工作階段的狀態。</span><span class="sxs-lookup"><span data-stu-id="7a824-310"><xref:System.Data.SqlClient.SqlEnclaveSession>, which encapsulates the state for a given enclave session.</span></span>

- <span data-ttu-id="7a824-311"><xref:System.Data.SqlClient.SqlEnclaveAttestationParameters>，其可提供 SQL Server 用來取得執行特定證明通訊協定所需資訊的證明參數。</span><span class="sxs-lookup"><span data-stu-id="7a824-311"><xref:System.Data.SqlClient.SqlEnclaveAttestationParameters>, which provides the attestation parameters used by SQL Server to get information required to execute a particular Attestation Protocol.</span></span>

<span data-ttu-id="7a824-312">應用程式組態檔則指定抽象 <xref:System.Data.SqlClient.SqlColumnEncryptionEnclaveProvider?displayProperty=nameWithType> 類別的具象實作，以針對飛地提供者提供功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-312">The application configuration file then specifies a concrete implementation of the abstract <xref:System.Data.SqlClient.SqlColumnEncryptionEnclaveProvider?displayProperty=nameWithType> class that provides the functionality for the enclave provider.</span></span> <span data-ttu-id="7a824-313">例如：</span><span class="sxs-lookup"><span data-stu-id="7a824-313">For example:</span></span>

```xml
<configuration>
  <configSections>
    <section name="SqlColumnEncryptionEnclaveProviders" type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection,System.Data,Version=4.0.0.0,Culture=neutral,PublicKeyToken=b77a5c561934e089"/>
  </configSections>
  <SqlColumnEncryptionEnclaveProviders>
    <providers>
      <add name="Azure" type="Microsoft.SqlServer.Management.AlwaysEncrypted.AzureEnclaveProvider,MyApp"/>
      <add name="HGS" type="Microsoft.SqlServer.Management.AlwaysEncrypted.HGSEnclaveProvider,MyApp" />
    </providers>
  </SqlColumnEncryptionEnclaveProviders >
</configuration>
```

<span data-ttu-id="7a824-314">飛地式 Always Encrypted 的基本流程如下：</span><span class="sxs-lookup"><span data-stu-id="7a824-314">The basic flow of enclave-based Always Encrypted is:</span></span>

1. <span data-ttu-id="7a824-315">使用者會建立與 SQL Server 的 Always Encrypted 連線，以支援飛地式 Always Encrypted。</span><span class="sxs-lookup"><span data-stu-id="7a824-315">The user creates an AlwaysEncrypted connection to SQL Server that supported enclave-based Always Encrypted.</span></span> <span data-ttu-id="7a824-316">驅動程式會連絡證明服務，以確保它連接到正確的飛地。</span><span class="sxs-lookup"><span data-stu-id="7a824-316">The driver contacts the attestation service to ensure that it is connecting to right enclave.</span></span>

1. <span data-ttu-id="7a824-317">一旦飛地經過證明，驅動程式就會與 SQL Server 上所裝載的安全飛地建立安全通道。</span><span class="sxs-lookup"><span data-stu-id="7a824-317">Once the enclave has been attested, the driver establishes a secure channel with the secure enclave hosted on SQL Server.</span></span>

1. <span data-ttu-id="7a824-318">在 SQL 連線期間，驅動程式會與安全飛地共用用戶端所授權的加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="7a824-318">The driver shares encryption keys authorized by the client with the secure enclave for the duration of the SQL connection.</span></span>

<a name="wpf472"></a>

#### <a name="windows-presentation-foundation"></a><span data-ttu-id="7a824-319">Windows Presentation Foundation</span><span class="sxs-lookup"><span data-stu-id="7a824-319">Windows Presentation Foundation</span></span>

<span data-ttu-id="7a824-320">**依來源尋找 ResourceDictionary**</span><span class="sxs-lookup"><span data-stu-id="7a824-320">**Finding ResourceDictionaries by Source**</span></span>

<span data-ttu-id="7a824-321">從 .NET Framework 4.7.2 開始，診斷小幫手可以找出從指定來源 URI 建立的  <xref:System.Windows.Xps.Packaging.IXpsFixedPageReader.ResourceDictionaries>。</span><span class="sxs-lookup"><span data-stu-id="7a824-321">Starting with .NET Framework 4.7.2, a diagnostic assistant can locate the <xref:System.Windows.Xps.Packaging.IXpsFixedPageReader.ResourceDictionaries> that have been created from a given source Uri.</span></span><span data-ttu-id="7a824-322"> (這項功能是供診斷助理使用，而不是由實際執行應用程式使用。 ) 診斷小幫手（例如 Visual Studio 的「編輯後繼續」設備），可讓其使用者使用將變更套用至執行中應用程式的意圖來編輯 ResourceDictionary。</span><span class="sxs-lookup"><span data-stu-id="7a824-322"> (This feature is for use by diagnostic assistants, not by production applications.) A diagnostic assistant such as Visual Studio's "Edit-and-Continue" facility lets its user edit a ResourceDictionary with the intent that the changes be applied to the running application.</span></span> <span data-ttu-id="7a824-323">達成此目標的其中一個步驟，是尋找執行中的應用程式從正在編輯的字典中建立的所有 Resourcedictionary。</span><span class="sxs-lookup"><span data-stu-id="7a824-323">One step in achieving this is finding all the ResourceDictionaries that the running application has created from the dictionary that's being edited.</span></span> <span data-ttu-id="7a824-324">例如，應用程式可以宣告其內容是從指定來源 URI 複製而來的 ResourceDictionary：</span><span class="sxs-lookup"><span data-stu-id="7a824-324">For example, an application can declare a ResourceDictionary whose content is copied from a given source URI:</span></span>

```xml
<ResourceDictionary Source="MyRD.xaml" />
```

<span data-ttu-id="7a824-325">在 *>myrd.xaml*中編輯原始標記的診斷小幫手   可以使用新功能來找出字典。</span><span class="sxs-lookup"><span data-stu-id="7a824-325">A diagnostic assistant that edits the original markup in *MyRD.xaml* can use the new feature to locate the dictionary.</span></span><span data-ttu-id="7a824-326">此功能是透過新的靜態方法 <xref:System.Windows.Diagnostics.ResourceDictionaryDiagnostics.GetResourceDictionariesForSource%2A?displayProperty=nameWithType> 來實作。</span><span class="sxs-lookup"><span data-stu-id="7a824-326"> The feature is implemented by a new static method, <xref:System.Windows.Diagnostics.ResourceDictionaryDiagnostics.GetResourceDictionariesForSource%2A?displayProperty=nameWithType>.</span></span> <span data-ttu-id="7a824-327">診斷小幫手會使用可識別原始標記的絕對 URI 來呼叫新方法，如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="7a824-327">The diagnostic assistant calls the new method using an absolute Uri that identifies the original markup, as illustrated by the following code:</span></span>

```csharp
IEnumerable<ResourceDictionary> dictionaries = ResourceDictionaryDiagnostics.GetResourceDictionariesForSource(new Uri("pack://application:,,,/MyApp;component/MyRD.xaml"));
```

```vb
Dim dictionaries As IEnumerable(Of ResourceDictionary) = ResourceDictionaryDiagnostics.GetResourceDictionariesForSource(New Uri("pack://application:,,,/MyApp;component/MyRD.xaml"))
```

<span data-ttu-id="7a824-328">除非  <xref:System.Windows.Diagnostics.VisualDiagnostics> 已啟用且已 [`ENABLE_XAML_DIAGNOSTICS_SOURCE_INFO`](xref:System.Windows.Diagnostics.VisualDiagnostics.GetXamlSourceInfo%2A)   設定環境變數，否則此方法會傳回空的可列舉。</span><span class="sxs-lookup"><span data-stu-id="7a824-328">The method returns an empty enumerable unless <xref:System.Windows.Diagnostics.VisualDiagnostics> is enabled and the [`ENABLE_XAML_DIAGNOSTICS_SOURCE_INFO`](xref:System.Windows.Diagnostics.VisualDiagnostics.GetXamlSourceInfo%2A) environment variable is set.</span></span>

<span data-ttu-id="7a824-329">**尋找 ResourceDictionary 擁有者**</span><span class="sxs-lookup"><span data-stu-id="7a824-329">**Finding ResourceDictionary owners**</span></span>

<span data-ttu-id="7a824-330">從 .NET Framework 4.7.2 開始，診斷小幫手可以找出給定 <xref:Windows.UI.Xaml.ResourceDictionary> 的擁有者。</span><span class="sxs-lookup"><span data-stu-id="7a824-330">Starting with .NET Framework 4.7.2, a diagnostic assistant can locate the owners of a given <xref:Windows.UI.Xaml.ResourceDictionary>.</span></span><span data-ttu-id="7a824-331"> (功能用於診斷助理，而不是由實際執行應用程式使用。 ) 每次變更時 <xref:Windows.UI.Xaml.ResourceDictionary> ，WPF 會自動尋找可能受變更影響的所有 [DynamicResource](/dotnet/desktop/wpf/advanced/dynamicresource-markup-extension) 參考。</span><span class="sxs-lookup"><span data-stu-id="7a824-331"> (The feature is for use by diagnostic assistants and not by production applications.) Whenever a change is made to a <xref:Windows.UI.Xaml.ResourceDictionary>, WPF automatically finds all [DynamicResource](/dotnet/desktop/wpf/advanced/dynamicresource-markup-extension) references that might be affected by the change.</span></span>

<span data-ttu-id="7a824-332">診斷小幫手（例如 Visual Studio 的「編輯後繼續」設備）可能會想要擴充此功能以處理 [StaticResource](/dotnet/desktop/wpf/advanced/staticresource-markup-extension) 參考。</span><span class="sxs-lookup"><span data-stu-id="7a824-332">A diagnostic assistant such as Visual Studio's "Edit-and-Continue" facility may want to extend this to handle [StaticResource](/dotnet/desktop/wpf/advanced/staticresource-markup-extension) references.</span></span> <span data-ttu-id="7a824-333">此程序的第一個步驟是尋找字典的擁有者；也就是尋找其 `Resources` 屬性參考字典 (直接或間接透過 <xref:System.Windows.ResourceDictionary.MergedDictionaries?displayProperty=nameWithType> 屬性) 的所有物件。</span><span class="sxs-lookup"><span data-stu-id="7a824-333">The first step in this process is to find the owners of the dictionary; that is, to find all the objects whose `Resources` property refers to the dictionary (either directly, or indirectly via the <xref:System.Windows.ResourceDictionary.MergedDictionaries?displayProperty=nameWithType> property).</span></span> <span data-ttu-id="7a824-334">在 <xref:System.Windows.Diagnostics.ResourceDictionaryDiagnostics?displayProperty=nameWithType> 類別上實作的三個新靜態方法 (每個具有 `Resources` 屬性的基底類型各有一個) 支援此步驟：</span><span class="sxs-lookup"><span data-stu-id="7a824-334">Three new static methods implemented on the <xref:System.Windows.Diagnostics.ResourceDictionaryDiagnostics?displayProperty=nameWithType> class, one for each of the base types that has a `Resources` property, support this step:</span></span>

- [`public static IEnumerable<FrameworkElement> GetFrameworkElementOwners(ResourceDictionary dictionary);`](xref:System.Windows.Diagnostics.ResourceDictionaryDiagnostics.GetFrameworkElementOwners%2A)

- [`public static IEnumerable<FrameworkContentElement> GetFrameworkContentElementOwners(ResourceDictionary dictionary);`](xref:System.Windows.Diagnostics.ResourceDictionaryDiagnostics.GetFrameworkContentElementOwners%2A)

- [`public static IEnumerable<Application> GetApplicationOwners(ResourceDictionary dictionary);`](xref:System.Windows.Diagnostics.ResourceDictionaryDiagnostics.GetApplicationOwners%2A)

<span data-ttu-id="7a824-335">除非  <xref:System.Windows.Diagnostics.VisualDiagnostics> 已啟用且已 [`ENABLE_XAML_DIAGNOSTICS_SOURCE_INFO`](xref:System.Windows.Diagnostics.VisualDiagnostics.GetXamlSourceInfo%2A)   設定環境變數，否則這些方法會傳回空的可列舉。</span><span class="sxs-lookup"><span data-stu-id="7a824-335">These methods return an empty enumerable unless <xref:System.Windows.Diagnostics.VisualDiagnostics> is enabled and the [`ENABLE_XAML_DIAGNOSTICS_SOURCE_INFO`](xref:System.Windows.Diagnostics.VisualDiagnostics.GetXamlSourceInfo%2A) environment variable is set.</span></span>

<span data-ttu-id="7a824-336">**尋找 StaticResource 參考**</span><span class="sxs-lookup"><span data-stu-id="7a824-336">**Finding StaticResource references**</span></span>

<span data-ttu-id="7a824-337">診斷小幫手現在可以在每次解析 [StaticResource](/dotnet/desktop/wpf/advanced/staticresource-markup-extension) 參照時收到通知。</span><span class="sxs-lookup"><span data-stu-id="7a824-337">A diagnostic assistant can now receive a notification whenever a [StaticResource](/dotnet/desktop/wpf/advanced/staticresource-markup-extension) reference is resolved.</span></span><span data-ttu-id="7a824-338"> (功能用於診斷助理，而不是由實際執行應用程式使用。 ) 診斷小幫手（例如 Visual Studio 的「編輯後繼續」功能），可能會想要在變更時更新資源的所有使用。 <xref:Windows.UI.Xaml.ResourceDictionary></span><span class="sxs-lookup"><span data-stu-id="7a824-338"> (The feature is for use by diagnostic assistants, not by production applications.) A diagnostic assistant such as Visual Studio's "Edit-and-Continue" facility may want to update all uses of a resource when its value in a <xref:Windows.UI.Xaml.ResourceDictionary> changes.</span></span> <span data-ttu-id="7a824-339">WPF 會自動為 [DynamicResource](/dotnet/desktop/wpf/advanced/dynamicresource-markup-extension) 參考執行此作業，但不會針對 [StaticResource](/dotnet/desktop/wpf/advanced/staticresource-markup-extension) 參考刻意這麼做。</span><span class="sxs-lookup"><span data-stu-id="7a824-339">WPF does this automatically for [DynamicResource](/dotnet/desktop/wpf/advanced/dynamicresource-markup-extension) references, but it intentionally does not do so for [StaticResource](/dotnet/desktop/wpf/advanced/staticresource-markup-extension) references.</span></span> <span data-ttu-id="7a824-340">從 .NET Framework 4.7.2 開始，診斷小幫手可以使用這些通知，來找出靜態資源的這些使用項目。</span><span class="sxs-lookup"><span data-stu-id="7a824-340">Starting with .NET Framework 4.7.2, the diagnostic assistant can use these notifications to locate those uses of the static resource.</span></span>

<span data-ttu-id="7a824-341">通知是透過新的 <xref:System.Windows.Diagnostics.ResourceDictionaryDiagnostics.StaticResourceResolved?displayProperty=nameWithType> 事件進行實作：</span><span class="sxs-lookup"><span data-stu-id="7a824-341">The notification is implemented by the new <xref:System.Windows.Diagnostics.ResourceDictionaryDiagnostics.StaticResourceResolved?displayProperty=nameWithType> event:</span></span>

```csharp
public static event EventHandler<StaticResourceResolvedEventArgs> StaticResourceResolved;
```

```vb
Public Shared Event StaticResourceResolved As EventHandler(Of StaticResourceResolvedEventArgs)
```

<span data-ttu-id="7a824-342">每當執行階段解析 [StaticResource](/dotnet/desktop/wpf/advanced/staticresource-markup-extension) 參考時，即會引發這個事件。</span><span class="sxs-lookup"><span data-stu-id="7a824-342">This event is raised whenever the runtime resolves a [StaticResource](/dotnet/desktop/wpf/advanced/staticresource-markup-extension) reference.</span></span><span data-ttu-id="7a824-343"><xref:System.Windows.Diagnostics.StaticResourceResolvedEventArgs> 引數會描述解析方式，並指出裝載 [StaticResource](/dotnet/desktop/wpf/advanced/staticresource-markup-extension) 參考的物件和屬性與用於解析的  <xref:Windows.UI.Xaml.ResourceDictionary> 和索引鍵：</span><span class="sxs-lookup"><span data-stu-id="7a824-343"> The <xref:System.Windows.Diagnostics.StaticResourceResolvedEventArgs> arguments describe the resolution, and indicate the object and property that host the [StaticResource](/dotnet/desktop/wpf/advanced/staticresource-markup-extension) reference and the <xref:Windows.UI.Xaml.ResourceDictionary> and key used for the resolution:</span></span>

```csharp
public class StaticResourceResolvedEventArgs : EventArgs
{
   public Object TargetObject { get; }

   public Object TargetProperty { get; }

   public ResourceDictionary ResourceDictionary { get; }

   public object ResourceKey { get; }
}
```

```vb
Public Class StaticResourceResolvedEventArgs : Inherits EventArgs
   Public ReadOnly Property TargetObject As Object
   Public ReadOnly Property TargetProperty As Object
   Public ReadOnly Property ResourceDictionary As ResourceDictionary
   Public ReadOnly Property ResourceKey As Object
End Class
```

<span data-ttu-id="7a824-344">此事件不會引發 (除非已 `add`  <xref:System.Windows.Diagnostics.VisualDiagnostics> 啟用且已 [`ENABLE_XAML_DIAGNOSTICS_SOURCE_INFO`](xref:System.Windows.Diagnostics.VisualDiagnostics.GetXamlSourceInfo%2A) 設定環境變數，否則會忽略其存取子)   。</span><span class="sxs-lookup"><span data-stu-id="7a824-344">The event is not raised (and its `add` accessor is ignored) unless <xref:System.Windows.Diagnostics.VisualDiagnostics> is enabled and the [`ENABLE_XAML_DIAGNOSTICS_SOURCE_INFO`](xref:System.Windows.Diagnostics.VisualDiagnostics.GetXamlSourceInfo%2A) environment variable is set.</span></span>

#### <a name="clickonce"></a><span data-ttu-id="7a824-345">ClickOnce</span><span class="sxs-lookup"><span data-stu-id="7a824-345">ClickOnce</span></span>

<span data-ttu-id="7a824-346">適用於 Windows Forms、Windows Presentation Foundation (WPF) 和 Visual Studio Tools for Office (VSTO) 的 HDPI 感知應用程式都可以使用 ClickOnce 進行部署。</span><span class="sxs-lookup"><span data-stu-id="7a824-346">HDPI-aware applications for Windows Forms, Windows Presentation Foundation (WPF), and Visual Studio Tools for Office (VSTO) can all be deployed by using ClickOnce.</span></span> <span data-ttu-id="7a824-347">如果在應用程式資訊清單中找到下列項目，將會在 .NET Framework 4.7.2 下成功完成部署：</span><span class="sxs-lookup"><span data-stu-id="7a824-347">If the following entry is found in the application manifest, deployment will succeed under .NET Framework 4.7.2:</span></span>

```xml
<windowsSettings>
   <dpiAware xmlns="http://schemas.microsoft.com/SMI/2005/WindowsSettings">true</dpiAware>
</windowsSettings>
```

<span data-ttu-id="7a824-348">如果是 Windows Forms 應用程式，不再需要執行之前的因應措施 (於應用程式組態檔而不是應用程式資訊清單中設定 DPI 感知)，ClickOnce 部署就能成功完成。</span><span class="sxs-lookup"><span data-stu-id="7a824-348">For Windows Forms application, the previous workaround of setting DPI awareness in the application configuration file rather than the application manifest is no longer necessary for ClickOnce deployment to succeed.</span></span>

<a name="v471"></a>

## <a name="whats-new-in-net-framework-471"></a><span data-ttu-id="7a824-349">.NET Framework 4.7.1 中的新功能</span><span class="sxs-lookup"><span data-stu-id="7a824-349">What's new in .NET Framework 4.7.1</span></span>

<span data-ttu-id="7a824-350">.NET Framework 4.7.1 包含下列領域的新功能：</span><span class="sxs-lookup"><span data-stu-id="7a824-350">.NET Framework 4.7.1 includes new features in the following areas:</span></span>

- [<span data-ttu-id="7a824-351">基底類別</span><span class="sxs-lookup"><span data-stu-id="7a824-351">Base classes</span></span>](#core471)
- [<span data-ttu-id="7a824-352">Common language runtime (CLR) </span><span class="sxs-lookup"><span data-stu-id="7a824-352">Common language runtime (CLR)</span></span>](#clr)
- [<span data-ttu-id="7a824-353">網路功能</span><span class="sxs-lookup"><span data-stu-id="7a824-353">Networking</span></span>](#net471)
- [<span data-ttu-id="7a824-354">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7a824-354">ASP.NET</span></span>](#asp-net471)

<span data-ttu-id="7a824-355">此外，.NET Framework 4.7.1 中的主要焦點是改善協助工具，以允許應用程式為輔助技術使用者提供適當的體驗。</span><span class="sxs-lookup"><span data-stu-id="7a824-355">In addition, a major focus in .NET Framework 4.7.1 is improved accessibility, which allows an application to provide an appropriate experience for users of Assistive Technology.</span></span> <span data-ttu-id="7a824-356">如需 .NET Framework 4.7.1 中協助工具改善的資訊；請參閱 [.NET Framework 協助工具的新功能](whats-new-in-accessibility.md)。</span><span class="sxs-lookup"><span data-stu-id="7a824-356">For information on accessibility improvements in .NET Framework 4.7.1, see [What's new in accessibility in the .NET Framework](whats-new-in-accessibility.md).</span></span>

<a name="core471"></a>

#### <a name="base-classes"></a><span data-ttu-id="7a824-357">基底類別</span><span class="sxs-lookup"><span data-stu-id="7a824-357">Base classes</span></span>

<span data-ttu-id="7a824-358">**針對 .NET Standard 2.0 的支援**</span><span class="sxs-lookup"><span data-stu-id="7a824-358">**Support for .NET Standard 2.0**</span></span>

<span data-ttu-id="7a824-359">[.NET Standard](../../standard/net-standard.md) 定義一組必須在每個 .NET 實作上提供的 API，而 .NET 實作支援該版本的標準。</span><span class="sxs-lookup"><span data-stu-id="7a824-359">[.NET Standard](../../standard/net-standard.md) defines a set of APIs that must be available on each .NET implementation that supports that version of the standard.</span></span> <span data-ttu-id="7a824-360">.NET Framework 4.7.1 完全支援 .NET Standard 2.0，並新增[大約 200 個 API](https://github.com/dotnet/standard/blob/master/src/netstandard/src/ApiCompatBaseline.net461.txt)，而這些 API 定義於 .NET Standard 2.0，在 .NET Framework 4.6.1、4.6.2 和 4.7 中則不提供。</span><span class="sxs-lookup"><span data-stu-id="7a824-360">.NET Framework 4.7.1 fully supports .NET Standard 2.0 and adds [about 200 APIs](https://github.com/dotnet/standard/blob/master/src/netstandard/src/ApiCompatBaseline.net461.txt) that are defined in .NET Standard 2.0 and are missing from .NET Framework 4.6.1, 4.6.2, and 4.7.</span></span> <span data-ttu-id="7a824-361"> (請注意，只有在目標系統上同時部署其他 .NET Standard 支援檔案時，這些 .NET Framework 版本才支援 .NET Standard 2.0。如需詳細資訊，請參閱 [) 4.7.1 執行時間和編譯器功能](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-runtime-and-compiler-features/) 的 blog 文章中的「BCL-.NET Standard 2.0 支援」。</span><span class="sxs-lookup"><span data-stu-id="7a824-361">(Note that these versions of the .NET Framework support .NET Standard 2.0 only if additional .NET Standard support files are also deployed on the target system.) For more information, see "BCL - .NET Standard 2.0 Support" in the [.NET Framework 4.7.1 Runtime and Compiler Features](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-runtime-and-compiler-features/) blog post.</span></span>

<span data-ttu-id="7a824-362">**設定產生器的支援**</span><span class="sxs-lookup"><span data-stu-id="7a824-362">**Support for configuration builders**</span></span>

<span data-ttu-id="7a824-363">組態產生器可讓開發人員在執行階段動態插入和建置應用程式的組態設定。</span><span class="sxs-lookup"><span data-stu-id="7a824-363">Configuration builders allow developers to inject and build configuration settings for applications dynamically at run time.</span></span> <span data-ttu-id="7a824-364">自訂組態產生器可以用來修改組態區段中的現有資料，或從頭開始全新建置組態區段。</span><span class="sxs-lookup"><span data-stu-id="7a824-364">Custom configuration builders can be used to modify existing data in a configuration section or to build a configuration section entirely from scratch.</span></span> <span data-ttu-id="7a824-365">如果沒有組態產生器，則 .config 檔案是靜態的，而且在啟動應用程式之前的某個時間定義其設定。</span><span class="sxs-lookup"><span data-stu-id="7a824-365">Without configuration builders, .config files are static, and their settings are defined some time before an application is launched.</span></span>

<span data-ttu-id="7a824-366">若要建立自訂組態產生器，您可以從抽象 <xref:System.Configuration.ConfigurationBuilder> 類別衍生產生器，並覆寫其 <xref:System.Configuration.ConfigurationBuilder.ProcessConfigurationSection%2A?displayProperty=nameWithType> 和 <xref:System.Configuration.ConfigurationBuilder.ProcessRawXml%2A?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="7a824-366">To create a custom configuration builder, you derive your builder from the abstract <xref:System.Configuration.ConfigurationBuilder> class and override its <xref:System.Configuration.ConfigurationBuilder.ProcessConfigurationSection%2A?displayProperty=nameWithType> and <xref:System.Configuration.ConfigurationBuilder.ProcessRawXml%2A?displayProperty=nameWithType>.</span></span> <span data-ttu-id="7a824-367">您也可以在 .config 檔案中定義產生器。</span><span class="sxs-lookup"><span data-stu-id="7a824-367">You also define your builders in your .config file.</span></span> <span data-ttu-id="7a824-368">如需詳細資訊，請參閱 [.NET Framework 4.7.1 ASP.NET 和組態功能](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-asp-net-and-configuration-features/)部落格文章中的＜組態產生器＞一節。</span><span class="sxs-lookup"><span data-stu-id="7a824-368">For more information, see the "Configuration Builders" section in the [.NET Framework 4.7.1 ASP.NET and Configuration Features](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-asp-net-and-configuration-features/) blog post.</span></span>

<span data-ttu-id="7a824-369">**執行階段功能偵測**</span><span class="sxs-lookup"><span data-stu-id="7a824-369">**Run-time feature detection**</span></span>

<span data-ttu-id="7a824-370"><xref:System.Runtime.CompilerServices.RuntimeFeature?displayProperty=nameWithType> 類別提供機制，來判斷在編譯階段或執行階段，特定 .NET 實作上是否支援預先定義的功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-370">The <xref:System.Runtime.CompilerServices.RuntimeFeature?displayProperty=nameWithType> class provides a mechanism for determine whether a predefined feature is supported on a given .NET implementation at compile time or run time.</span></span> <span data-ttu-id="7a824-371">在編譯階段，編譯器可以檢查是否有指定的欄位來判斷是否支援此功能；如果支援，則可以發出利用該功能的程式碼。</span><span class="sxs-lookup"><span data-stu-id="7a824-371">At compile time, a compiler can check whether a specified field exists to determine whether the feature is supported; if so, it can emit code that takes advantage of that feature.</span></span> <span data-ttu-id="7a824-372">在執行階段，應用程式可以先呼叫 <xref:System.Runtime.CompilerServices.RuntimeFeature.IsSupported%2A?displayProperty=nameWithType> 方法，再於執行階段發出程式碼。</span><span class="sxs-lookup"><span data-stu-id="7a824-372">At run time, an application can call the <xref:System.Runtime.CompilerServices.RuntimeFeature.IsSupported%2A?displayProperty=nameWithType> method before emitting code at runtime.</span></span> <span data-ttu-id="7a824-373">如需詳細資訊，請參閱[新增協助程式方法來描述執行階段所支援的功能](https://github.com/dotnet/corefx/issues/17116)。</span><span class="sxs-lookup"><span data-stu-id="7a824-373">For more information, see [Add helper method to describe features supported by the runtime](https://github.com/dotnet/corefx/issues/17116).</span></span>

<span data-ttu-id="7a824-374">**實值元組類型為可序列化**</span><span class="sxs-lookup"><span data-stu-id="7a824-374">**Value tuple types are serializable**</span></span>

<span data-ttu-id="7a824-375">從 .NET Framework 4.7.1 開始，<xref:System.ValueTuple?displayProperty=nameWithType> 和其相關聯泛型型別會標示為 [Serializable](xref:System.SerializableAttribute)，以允許二進位序列化。</span><span class="sxs-lookup"><span data-stu-id="7a824-375">Starting with .NET Framework 4.7.1, <xref:System.ValueTuple?displayProperty=nameWithType> and its associated generic types are marked as [Serializable](xref:System.SerializableAttribute), which allows binary serialization.</span></span> <span data-ttu-id="7a824-376">這應該會讓將元組類型 (例如 <xref:System.Tuple%603> 和 <xref:System.Tuple%604>) 移轉至實值元組類型更為簡單。</span><span class="sxs-lookup"><span data-stu-id="7a824-376">This should make migrating Tuple types, such as <xref:System.Tuple%603> and <xref:System.Tuple%604>, to value tuple types easier.</span></span> <span data-ttu-id="7a824-377">如需詳細資訊，請參閱 [.NET Framework 4.7.1 執行階段和編譯器功能](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-runtime-and-compiler-features/)部落格文章中的＜編譯器 - ValueTuple 可序列化＞。</span><span class="sxs-lookup"><span data-stu-id="7a824-377">For more information, see "Compiler -- ValueTuple is Serializable" in the [.NET Framework 4.7.1 Runtime and Compiler Features](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-runtime-and-compiler-features/) blog post.</span></span>

<span data-ttu-id="7a824-378">**唯讀參考的支援**</span><span class="sxs-lookup"><span data-stu-id="7a824-378">**Support for read-only references**</span></span>

<span data-ttu-id="7a824-379">.NET Framework 4.7.1 新增 <xref:System.Runtime.CompilerServices.IsReadOnlyAttribute?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="7a824-379">.NET Framework 4.7.1 adds the <xref:System.Runtime.CompilerServices.IsReadOnlyAttribute?displayProperty=nameWithType>.</span></span> <span data-ttu-id="7a824-380">語言編譯器會使用此屬性來標示具有唯讀 ref 傳回類型或參數的成員。</span><span class="sxs-lookup"><span data-stu-id="7a824-380">This attribute is used by language compilers to mark members that have read-only ref return types or parameters.</span></span> <span data-ttu-id="7a824-381">如需詳細資訊，請參閱 [.NET Framework 4.7.1 執行階段和編譯器功能](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-runtime-and-compiler-features/)部落格文章中的＜編譯器 - ReadOnlyReferences 支援＞。</span><span class="sxs-lookup"><span data-stu-id="7a824-381">For more information, see "Compiler -- Support for ReadOnlyReferences" in the [.NET Framework 4.7.1 Runtime and Compiler Features](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-runtime-and-compiler-features/) blog post.</span></span> <span data-ttu-id="7a824-382">如需 ref 傳回值的資訊，請參閱 [ref 傳回值和 ref 區域變數 (C# 指南)](../../csharp/programming-guide/classes-and-structs/ref-returns.md) 和 [ref 傳回值 (Visual Basic)](../../visual-basic/programming-guide/language-features/procedures/ref-return-values.md)。</span><span class="sxs-lookup"><span data-stu-id="7a824-382">For information on ref return values, see [Ref return values and ref locals (C# Guide)](../../csharp/programming-guide/classes-and-structs/ref-returns.md) and [Ref return values (Visual Basic)](../../visual-basic/programming-guide/language-features/procedures/ref-return-values.md).</span></span>

<a name="clr"></a>

#### <a name="common-language-runtime-clr"></a><span data-ttu-id="7a824-383">Common Language Runtime (CLR)</span><span class="sxs-lookup"><span data-stu-id="7a824-383">Common language runtime (CLR)</span></span>

<span data-ttu-id="7a824-384">**記憶體回收效能改善**</span><span class="sxs-lookup"><span data-stu-id="7a824-384">**Garbage collection performance improvements**</span></span>

<span data-ttu-id="7a824-385">.NET Framework 4.7.1 中垃圾收集 (GC) 的變更會改善整體效能，特別是針對大型物件堆積 (LOH) 配置。</span><span class="sxs-lookup"><span data-stu-id="7a824-385">Changes to garbage collection (GC) in .NET Framework 4.7.1 improve overall performance, especially for large object heap (LOH) allocations.</span></span> <span data-ttu-id="7a824-386">在 .NET Framework 4.7.1 中，小型物件堆積會使用不同的鎖定 (SOH) 和 LOH 配置，如此可在背景 GC 清除 SOH 時，進行 LOH 配置。</span><span class="sxs-lookup"><span data-stu-id="7a824-386">In .NET Framework 4.7.1, separate locks are used for small object heap (SOH) and LOH allocations, which allows LOH allocations to occur when background GC is sweeping the SOH.</span></span> <span data-ttu-id="7a824-387">因此，進行大量 LOH 配置的應用程式應該會看到配置鎖定爭用降低並改善效能。</span><span class="sxs-lookup"><span data-stu-id="7a824-387">As a result, applications that make a large number of LOH allocations should see a reduction in allocation lock contention and improved performance.</span></span> <span data-ttu-id="7a824-388">如需詳細資訊，請參閱 [.NET Framework 4.7.1 執行階段和編譯器功能](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-runtime-and-compiler-features/)部落格文章中的＜執行階段 -- GC 效能改善＞。</span><span class="sxs-lookup"><span data-stu-id="7a824-388">For more information, see the "Runtime -- GC Performance Improvements" section in the [.NET Framework 4.7.1 Runtime and Compiler Features](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-runtime-and-compiler-features/) blog post.</span></span>

<a name="net471"/>

#### <a name="networking"></a><span data-ttu-id="7a824-389">網路</span><span class="sxs-lookup"><span data-stu-id="7a824-389">Networking</span></span>

<span data-ttu-id="7a824-390">**Message.HashAlgorithm 的 SHA-2 支援**</span><span class="sxs-lookup"><span data-stu-id="7a824-390">**SHA-2 support for Message.HashAlgorithm**</span></span>

<span data-ttu-id="7a824-391">在 .NET Framework 4.7 和更舊版本中，<xref:System.Messaging.Message.HashAlgorithm%2A?displayProperty=nameWithType> 屬性只支援 <xref:System.Messaging.HashAlgorithm.Md5?displayProperty=nameWithType> 和 <xref:System.Messaging.HashAlgorithm.Sha?displayProperty=nameWithType> 的值。</span><span class="sxs-lookup"><span data-stu-id="7a824-391">In .NET Framework 4.7 and earlier versions, the <xref:System.Messaging.Message.HashAlgorithm%2A?displayProperty=nameWithType> property supported values of <xref:System.Messaging.HashAlgorithm.Md5?displayProperty=nameWithType> and <xref:System.Messaging.HashAlgorithm.Sha?displayProperty=nameWithType> only.</span></span> <span data-ttu-id="7a824-392">從 .NET Framework 4.7.1 開始，也支援 <xref:System.Messaging.HashAlgorithm.Sha256?displayProperty=nameWithType>、<xref:System.Messaging.HashAlgorithm.Sha384?displayProperty=nameWithType> 和 <xref:System.Messaging.HashAlgorithm.Sha512?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="7a824-392">Starting with .NET Framework 4.7.1, <xref:System.Messaging.HashAlgorithm.Sha256?displayProperty=nameWithType>, <xref:System.Messaging.HashAlgorithm.Sha384?displayProperty=nameWithType>, and <xref:System.Messaging.HashAlgorithm.Sha512?displayProperty=nameWithType> are also supported.</span></span> <span data-ttu-id="7a824-393">實際使用的這個值取決於 MSMQ，因為 <xref:System.Messaging.Message> 執行個體本身不會進行任何雜湊處理，而只會將值傳入 MSMQ。</span><span class="sxs-lookup"><span data-stu-id="7a824-393">Whether this value is actually used depends on MSMQ, since the <xref:System.Messaging.Message> instance itself does no hashing but simply passes on values to MSMQ.</span></span> <span data-ttu-id="7a824-394">如需詳細資訊，請參閱 [.NET Framework 4.7.1 ASP.NET 和組態功能](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-asp-net-and-configuration-features/)部落格文章中的＜Message.HashAlgorithm 的 SHA-2 支援＞一節。</span><span class="sxs-lookup"><span data-stu-id="7a824-394">For more information, see the "SHA-2 support for Message.HashAlgorithm" section in the [.NET Framework 4.7.1 ASP.NET and Configuration features](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-asp-net-and-configuration-features/) blog post.</span></span>

<a name="asp-net471"></a>

#### <a name="aspnet"></a><span data-ttu-id="7a824-395">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7a824-395">ASP.NET</span></span>

<span data-ttu-id="7a824-396">**ASP.NET 應用程式中的執行步驟**</span><span class="sxs-lookup"><span data-stu-id="7a824-396">**Execution steps in ASP.NET applications**</span></span>

<span data-ttu-id="7a824-397">ASP.NET 會在包含 23 個事件的預先定義管線中處理要求。</span><span class="sxs-lookup"><span data-stu-id="7a824-397">ASP.NET processes requests in a predefined pipeline that includes 23 events.</span></span> <span data-ttu-id="7a824-398">ASP.NET 會將每個事件處理常式執行為執行步驟。</span><span class="sxs-lookup"><span data-stu-id="7a824-398">ASP.NET executes each event handler as an execution step.</span></span> <span data-ttu-id="7a824-399">在 .NET Framework 4.7 之前的 ASP.NET 版本中，ASP.NET 因切換原生與受控執行緒而無法讓執行內容流動。</span><span class="sxs-lookup"><span data-stu-id="7a824-399">In versions of ASP.NET up to .NET Framework 4.7, ASP.NET can't flow the execution context due to switching between native and managed threads.</span></span> <span data-ttu-id="7a824-400">相反地，ASP.NET 選擇性地只會讓 <xref:System.Web.HttpContext> 流動。</span><span class="sxs-lookup"><span data-stu-id="7a824-400">Instead, ASP.NET selectively flows only the <xref:System.Web.HttpContext>.</span></span> <span data-ttu-id="7a824-401">從 .NET Framework 4.7.1 開始，<xref:System.Web.HttpApplication.OnExecuteRequestStep(System.Action{System.Web.HttpContextBase,System.Action})?displayProperty=nameWithType> 方法也允許模組還原環境資料。</span><span class="sxs-lookup"><span data-stu-id="7a824-401">Starting with .NET Framework 4.7.1, the <xref:System.Web.HttpApplication.OnExecuteRequestStep(System.Action{System.Web.HttpContextBase,System.Action})?displayProperty=nameWithType> method also allows modules to restore ambient data.</span></span> <span data-ttu-id="7a824-402">此功能的目標是關注於追蹤、分析、診斷或異動的程式庫，例如關心應用程式的執行流程。</span><span class="sxs-lookup"><span data-stu-id="7a824-402">This feature is targeted at libraries concerned with tracing, profiling, diagnostics, or transactions, for example, that care about the execution flow of the application.</span></span> <span data-ttu-id="7a824-403">如需詳細資訊，請參閱 [.NET Framework 4.7.1 ASP.NET 和組態功能](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-asp-net-and-configuration-features/)部落格文章中的＜ASP.NET 執行步驟功能＞一節。</span><span class="sxs-lookup"><span data-stu-id="7a824-403">For more information, see the "ASP.NET Execution Step Feature" in the [.NET Framework 4.7.1 ASP.NET and Configuration Features](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-asp-net-and-configuration-features/) blog post.</span></span>

<span data-ttu-id="7a824-404">**ASP.NET HttpCookie 剖析**</span><span class="sxs-lookup"><span data-stu-id="7a824-404">**ASP.NET HttpCookie parsing**</span></span>

<span data-ttu-id="7a824-405">.NET Framework 4.7.1 包含的新方法 <xref:System.Web.HttpCookie.TryParse%2A?displayProperty=nameWithType> 提供標準化方式，以從字串建立 <xref:System.Web.HttpCookie> 物件，並精確地指派 Cookie 值 (例如到期日和路徑)。</span><span class="sxs-lookup"><span data-stu-id="7a824-405">.NET Framework 4.7.1 includes a new method, <xref:System.Web.HttpCookie.TryParse%2A?displayProperty=nameWithType>, that provides a standardized way to create an <xref:System.Web.HttpCookie> object from a string and accurately assign cookie values such as expiration date and path.</span></span> <span data-ttu-id="7a824-406">如需詳細資訊，請參閱 [.NET Framework 4.7.1 ASP.NET 和組態功能](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-asp-net-and-configuration-features/)部落格文章中的＜ASP.NET HttpCookie 剖析＞一節。</span><span class="sxs-lookup"><span data-stu-id="7a824-406">For more information, see "ASP.NET HttpCookie parsing" in the [.NET Framework 4.7.1 ASP.NET and Configuration Features](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-asp-net-and-configuration-features/) blog post.</span></span>

<span data-ttu-id="7a824-407">**ASP.NET 表單驗證認證的 SHA-2 雜湊選項**</span><span class="sxs-lookup"><span data-stu-id="7a824-407">**SHA-2 hash options for ASP.NET forms authentication credentials**</span></span>

<span data-ttu-id="7a824-408">在 .NET Framework 4.7 和更舊版本中，ASP.NET 已允許開發人員使用 MD5 或 SHA1，將使用者認證與雜湊密碼儲存至組態檔。</span><span class="sxs-lookup"><span data-stu-id="7a824-408">In .NET Framework 4.7 and earlier versions, ASP.NET allowed developers to store user credentials with hashed passwords in configuration files using either MD5 or SHA1.</span></span> <span data-ttu-id="7a824-409">從 .NET Framework 4.7.1 開始，ASP.NET 也支援新安全 SHA-2 雜湊選項 (例如 SHA256、SHA384 和 SHA512)。</span><span class="sxs-lookup"><span data-stu-id="7a824-409">Starting with .NET Framework 4.7.1, ASP.NET also supports new secure SHA-2 hash options such as SHA256, SHA384, and SHA512.</span></span> <span data-ttu-id="7a824-410">SHA1 會保持預設值，而且可以在 Web 組態檔中定義非預設雜湊演算法。</span><span class="sxs-lookup"><span data-stu-id="7a824-410">SHA1 remains the default, and a non-default hash algorithm can be defined in the web configuration file.</span></span> <span data-ttu-id="7a824-411">例如：</span><span class="sxs-lookup"><span data-stu-id="7a824-411">For example:</span></span>

```xml
<system.web>
    <authentication mode="Forms">
        <forms loginUrl="~/login.aspx">
          <credentials passwordFormat="SHA512">
            <user name="jdoe" password="6D003E98EA1C7F04ABF8FCB375388907B7F3EE06F278DB966BE960E7CBBD103DF30CA6D61F7E7FD981B2E4E3A64D43C836A4BEDCA165C33B163E6BCDC538A664" />
          </credentials>
        </forms>
    </authentication>
</system.web>
```

<a name="v47"></a>

## <a name="whats-new-in-net-framework-47"></a><span data-ttu-id="7a824-412">.NET Framework 4.7 中的新功能</span><span class="sxs-lookup"><span data-stu-id="7a824-412">What's new in .NET Framework 4.7</span></span>

<span data-ttu-id="7a824-413">.NET Framework 4.7 包含下列領域的新功能：</span><span class="sxs-lookup"><span data-stu-id="7a824-413">.NET Framework 4.7 includes new features in the following areas:</span></span>

- [<span data-ttu-id="7a824-414">基底類別</span><span class="sxs-lookup"><span data-stu-id="7a824-414">Base classes</span></span>](#Core47)
- [<span data-ttu-id="7a824-415">網路功能</span><span class="sxs-lookup"><span data-stu-id="7a824-415">Networking</span></span>](#net47)
- [<span data-ttu-id="7a824-416">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7a824-416">ASP.NET</span></span>](#ASP-NET47)
- [<span data-ttu-id="7a824-417">Windows Communication Foundation (WCF)</span><span class="sxs-lookup"><span data-stu-id="7a824-417">Windows Communication Foundation (WCF)</span></span>](#wcf47)
- [<span data-ttu-id="7a824-418">Windows Forms</span><span class="sxs-lookup"><span data-stu-id="7a824-418">Windows Forms</span></span>](#wf47)
- [<span data-ttu-id="7a824-419">Windows Presentation Foundation (WPF)</span><span class="sxs-lookup"><span data-stu-id="7a824-419">Windows Presentation Foundation (WPF)</span></span>](#WPF47)

<span data-ttu-id="7a824-420">如需 .NET Framework 4.7 中加入的新 API 清單，請參閱 GitHub 上的 [.NET Framework 4.7 API 變更](https://github.com/Microsoft/dotnet/blob/master/releases/net47/dotnet47-api-changes.md) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="7a824-420">For a list of new APIs added to .NET Framework 4.7, see [.NET Framework 4.7 API Changes](https://github.com/Microsoft/dotnet/blob/master/releases/net47/dotnet47-api-changes.md) on GitHub.</span></span> <span data-ttu-id="7a824-421">如需 .NET Framework 4.7 中的功能改進以及錯誤 (Bug) 修正清單，請參閱 GitHub 上的 [.NET Framework 4.7 變更清單](https://github.com/Microsoft/dotnet/blob/master/releases/net47/dotnet47-changes.md) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="7a824-421">For a list of feature improvements and bug fixes in .NET Framework 4.7, see [.NET Framework 4.7 List of Changes](https://github.com/Microsoft/dotnet/blob/master/releases/net47/dotnet47-changes.md) on GitHub.</span></span> <span data-ttu-id="7a824-422">如需詳細資訊，請參閱在 .NET blog 中 [宣佈 .NET Framework 4.7](https://devblogs.microsoft.com/dotnet/announcing-the-net-framework-4-7/) 。</span><span class="sxs-lookup"><span data-stu-id="7a824-422">For more information, see [Announcing the .NET Framework 4.7](https://devblogs.microsoft.com/dotnet/announcing-the-net-framework-4-7/) in the .NET blog.</span></span>

<a name="Core47"></a>

#### <a name="base-classes"></a><span data-ttu-id="7a824-423">基底類別</span><span class="sxs-lookup"><span data-stu-id="7a824-423">Base classes</span></span>

<span data-ttu-id="7a824-424">.NET Framework 4.7 改進了 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 所執行的序列化：</span><span class="sxs-lookup"><span data-stu-id="7a824-424">.NET Framework 4.7 improves serialization by the <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>:</span></span>

<span data-ttu-id="7a824-425">\*\*使用橢圓曲線密碼編譯 (ECC) 的增強功能 \*\*\*</span><span class="sxs-lookup"><span data-stu-id="7a824-425">**Enhanced functionality with Elliptic Curve Cryptography (ECC)**\*</span></span>

<span data-ttu-id="7a824-426">在 .NET Framework 4.7 中，已將 `ImportParameters(ECParameters)` 方法新增到 <xref:System.Security.Cryptography.ECDsa> 和 <xref:System.Security.Cryptography.ECDiffieHellman> 類別，以允許物件代表已經建立的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="7a824-426">In .NET Framework 4.7, `ImportParameters(ECParameters)` methods were added to the <xref:System.Security.Cryptography.ECDsa> and <xref:System.Security.Cryptography.ECDiffieHellman> classes to allow for an object to represent an already-established key.</span></span> <span data-ttu-id="7a824-427">也加入 `ExportParameters(Boolean)` 方法以使用明確的曲線參數匯出索引鍵。</span><span class="sxs-lookup"><span data-stu-id="7a824-427">An `ExportParameters(Boolean)` method was also added for exporting the key using explicit curve parameters.</span></span>

<span data-ttu-id="7a824-428">.NET Framework 4.7 也新增了對其他曲線 (包括 Brainpool 曲線套件) 的支援，並已新增預先定義的定義，可透過新的 <xref:System.Security.Cryptography.ECDsa.Create%2A> 和 <xref:System.Security.Cryptography.ECDiffieHellman.Create%2A> Factory 方法輕鬆建立。</span><span class="sxs-lookup"><span data-stu-id="7a824-428">.NET Framework 4.7 also adds support for additional curves (including the Brainpool curve suite), and has added predefined definitions for ease-of-creation through the new <xref:System.Security.Cryptography.ECDsa.Create%2A> and <xref:System.Security.Cryptography.ECDiffieHellman.Create%2A> factory methods.</span></span>

<span data-ttu-id="7a824-429">您可以在 GitHub 上看到 [.NET Framework 4.7 密碼編譯增強功能的範例](https://gist.github.com/richlander/5a182899895a87a296c21ada97f7a54e)。</span><span class="sxs-lookup"><span data-stu-id="7a824-429">You can see an [example of .NET Framework 4.7 cryptography improvements](https://gist.github.com/richlander/5a182899895a87a296c21ada97f7a54e) on GitHub.</span></span>

<span data-ttu-id="7a824-430">**DataContractJsonSerializer 對控制字元有更好的支援**</span><span class="sxs-lookup"><span data-stu-id="7a824-430">**Better support for control characters by the DataContractJsonSerializer**</span></span>

<span data-ttu-id="7a824-431">在 .NET Framework 4.7 中， <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 類別會將控制字元序列化以符合 ECMAScript 6 標準。</span><span class="sxs-lookup"><span data-stu-id="7a824-431">In .NET Framework 4.7, the <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> class serializes control characters in conformity with the ECMAScript 6 standard.</span></span> <span data-ttu-id="7a824-432">預設會為以 .NET Framework 4.7 為目標的應用程式啟用此行為，而且是在 .NET Framework 4.7 下執行但以舊版 .NET Framework 為目標之應用程式的加入宣告功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-432">This behavior is enabled by default for applications that target .NET Framework 4.7, and is an opt-in feature for applications that are running under .NET Framework 4.7 but target a previous version of .NET Framework.</span></span> <span data-ttu-id="7a824-433">如需詳細資訊，請參閱 [應用程式相容性](../migration-guide/application-compatibility.md) 一節。</span><span class="sxs-lookup"><span data-stu-id="7a824-433">For more information, see the [Application compatibility](../migration-guide/application-compatibility.md) section.</span></span>

<a name="net47"></a>

#### <a name="networking"></a><span data-ttu-id="7a824-434">網路</span><span class="sxs-lookup"><span data-stu-id="7a824-434">Networking</span></span>

<span data-ttu-id="7a824-435">.NET Framework 4.7 新增與網路有關的下列功能︰</span><span class="sxs-lookup"><span data-stu-id="7a824-435">.NET Framework 4.7 adds the following network-related feature:</span></span>

<span data-ttu-id="7a824-436">**TLS 通訊協定的預設作業系統支援**\*</span><span class="sxs-lookup"><span data-stu-id="7a824-436">**Default operating system support for TLS protocols**\*</span></span>

<span data-ttu-id="7a824-437"><xref:System.Net.Security.SslStream?displayProperty=nameWithType> 和向上堆疊元件 (例如 HTTP、FTP 和 SMTP) 所使用的 TLS 堆疊可讓開發人員使用作業系統支援的預設 TLS 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="7a824-437">The TLS stack, which is used by <xref:System.Net.Security.SslStream?displayProperty=nameWithType> and up-stack components such as HTTP, FTP, and SMTP, allows developers to use the default TLS protocols supported by the operating system.</span></span> <span data-ttu-id="7a824-438">開發人員不再需要為 TLS 版本進行硬式編碼。</span><span class="sxs-lookup"><span data-stu-id="7a824-438">Developers need no longer hard-code a TLS version.</span></span>

<a name="ASP-NET47"></a>

#### <a name="aspnet"></a><span data-ttu-id="7a824-439">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7a824-439">ASP.NET</span></span>

<span data-ttu-id="7a824-440">在 .NET Framework 4.7 中，ASP.NET 包含下列新功能：</span><span class="sxs-lookup"><span data-stu-id="7a824-440">In .NET Framework 4.7, ASP.NET includes the following new features:</span></span>

<span data-ttu-id="7a824-441">**物件快取擴充性**</span><span class="sxs-lookup"><span data-stu-id="7a824-441">**Object Cache Extensibility**</span></span>

<span data-ttu-id="7a824-442">從 .NET Framework 4.7 開始，ASP.NET 加入一組新的 API 讓開發人員取代預設的 ASP.NET 實作以快取記憶體內部物件和監視記憶體。</span><span class="sxs-lookup"><span data-stu-id="7a824-442">Starting with .NET Framework 4.7, ASP.NET adds a new set of APIs that allow developers to replace the default ASP.NET implementations for in-memory object caching and memory monitoring.</span></span> <span data-ttu-id="7a824-443">如果 ASP.NET 實作不適用，開發人員現在可以取代下列三個元件當中的任何一個元件︰</span><span class="sxs-lookup"><span data-stu-id="7a824-443">Developers can now replace any of the following three components if the ASP.NET implementation is not adequate:</span></span>

- <span data-ttu-id="7a824-444">**物件快取存放區**。</span><span class="sxs-lookup"><span data-stu-id="7a824-444">**Object Cache Store**.</span></span> <span data-ttu-id="7a824-445">開發人員可以使用新的 **ICacheStoreProvider** 介面，透過新的快取提供者組態區段，為 ASP.NET 應用程式插入新的物件快取實作。</span><span class="sxs-lookup"><span data-stu-id="7a824-445">By using the new cache providers configuration section, developers can plug in new implementations of an object cache for an ASP.NET application by using the new **ICacheStoreProvider** interface.</span></span>

- <span data-ttu-id="7a824-446">**記憶體監視**。</span><span class="sxs-lookup"><span data-stu-id="7a824-446">**Memory monitoring**.</span></span> <span data-ttu-id="7a824-447">ASP.NET 中的預設記憶體監視器會在應用程式執行到接近針對處理序所設定的私用位元組上限時，或在電腦可用的總實體 RAM 不足時，通知應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a824-447">The default memory monitor in ASP.NET notifies applications when they are running close to the configured private bytes limit for the process, or when the machine is low on total available physical RAM.</span></span> <span data-ttu-id="7a824-448">接近這些限制時，就會引發通知。</span><span class="sxs-lookup"><span data-stu-id="7a824-448">When these limits are near, notifications are fired.</span></span> <span data-ttu-id="7a824-449">對於某些應用程式，通知在太接近設定的限制時才引發，將無法提供有用的反應。</span><span class="sxs-lookup"><span data-stu-id="7a824-449">For some applications, notifications are fired too close to the configured limits to allow for useful reactions.</span></span> <span data-ttu-id="7a824-450">開發人員現在可以使用 <xref:System.Web.Hosting.ApplicationMonitors.MemoryMonitor%2A?displayProperty=nameWithType> 屬性來撰寫自己的記憶體監視器，以取代預設的監視器。</span><span class="sxs-lookup"><span data-stu-id="7a824-450">Developers can now write their own memory monitors to replace the default by using the <xref:System.Web.Hosting.ApplicationMonitors.MemoryMonitor%2A?displayProperty=nameWithType> property.</span></span>

- <span data-ttu-id="7a824-451">**記憶體限制反應**。</span><span class="sxs-lookup"><span data-stu-id="7a824-451">**Memory Limit Reactions**.</span></span> <span data-ttu-id="7a824-452">ASP.NET 預設會在快達到私用位元組處理限制時，嘗試修剪物件快取並定期呼叫 <xref:System.GC.Collect%2A?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="7a824-452">By default, ASP.NET attempts to trim the object cache and periodically call <xref:System.GC.Collect%2A?displayProperty=nameWithType> when the private byte process limit is near.</span></span> <span data-ttu-id="7a824-453">就某些應用程式而言，呼叫 <xref:System.GC.Collect%2A?displayProperty=nameWithType> 的頻率或所修剪的快取量會沒有效率。</span><span class="sxs-lookup"><span data-stu-id="7a824-453">For some applications, the frequency of calls to <xref:System.GC.Collect%2A?displayProperty=nameWithType> or the amount of cache that is trimmed are inefficient.</span></span> <span data-ttu-id="7a824-454">開發人員現在可以向應用程式的記憶體監視器訂閱 **IObserver** 實作來取代或補充預設行為。</span><span class="sxs-lookup"><span data-stu-id="7a824-454">Developers can now replace or supplement the default behavior by subscribing **IObserver** implementations to the application's memory monitor.</span></span>

<a name="wcf47"></a>

#### <a name="windows-communication-foundation-wcf"></a><span data-ttu-id="7a824-455">Windows Communication Foundation (WCF)</span><span class="sxs-lookup"><span data-stu-id="7a824-455">Windows Communication Foundation (WCF)</span></span>

<span data-ttu-id="7a824-456">Windows Communication Foundation (WCF) 加入下列功能和變更：</span><span class="sxs-lookup"><span data-stu-id="7a824-456">Windows Communication Foundation (WCF) adds the following features and changes:</span></span>

<span data-ttu-id="7a824-457">**能夠將預設的訊息安全性設定設定為 TLS 1.1 或 TLS 1.2**</span><span class="sxs-lookup"><span data-stu-id="7a824-457">**Ability to configure the default message security settings to TLS 1.1 or TLS 1.2**</span></span>

<span data-ttu-id="7a824-458">從 .NET Framework 4.7 開始，除了 SSL 3.0 和 TLS 1.0 之外，WCF 還可讓您設定 TLS 1.1 或 TLS 1.2 作為預設的訊息安全性通訊協定。</span><span class="sxs-lookup"><span data-stu-id="7a824-458">Starting with .NET Framework 4.7, WCF allows you to configure TLS 1.1 or TLS 1.2 in addition to SSL 3.0 and TLS 1.0 as the default message security protocol.</span></span> <span data-ttu-id="7a824-459">這是選擇性的設定。若要啟用，您必須在應用程式組態檔中加入下列項目︰</span><span class="sxs-lookup"><span data-stu-id="7a824-459">This is an opt-in setting; to enable it, you must add the following entry to your application configuration file:</span></span>

```xml
<runtime>
   <AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;Switch.System.Net.DontEnableSchUseStrongCrypto=false" />
</runtime>
```

<span data-ttu-id="7a824-460">**改進 WCF 應用程式和 WCF 序列化的可靠性**</span><span class="sxs-lookup"><span data-stu-id="7a824-460">**Improved reliability of WCF applications and WCF serialization**</span></span>

<span data-ttu-id="7a824-461">WCF 包含許多可消除競爭情形的程式碼變更，因此可改善效能和序列化選項的可靠性。</span><span class="sxs-lookup"><span data-stu-id="7a824-461">WCF includes a number of code changes that eliminate race conditions, thereby improving performance and the reliability of serialization options.</span></span> <span data-ttu-id="7a824-462">其中包括：</span><span class="sxs-lookup"><span data-stu-id="7a824-462">These include:</span></span>

- <span data-ttu-id="7a824-463">在呼叫 **SocketConnection.BeginRead** 和 **SocketConnection.Read** 時更有效地支援混合非同步和同步程式碼。</span><span class="sxs-lookup"><span data-stu-id="7a824-463">Better support for mixing asynchronous and synchronous code in calls to **SocketConnection.BeginRead** and **SocketConnection.Read**.</span></span>
- <span data-ttu-id="7a824-464">改善中止與 **SharedConnectionListener** 和 **DuplexChannelBinder** 連線時的可靠性。</span><span class="sxs-lookup"><span data-stu-id="7a824-464">Improved reliability when aborting a connection with **SharedConnectionListener** and **DuplexChannelBinder**.</span></span>
- <span data-ttu-id="7a824-465">改善呼叫 <xref:System.Runtime.Serialization.FormatterServices.GetSerializableMembers%28System.Type%29?displayProperty=nameWithType> 方法時的序列化作業可靠性。</span><span class="sxs-lookup"><span data-stu-id="7a824-465">Improved reliability of serialization operations when calling the <xref:System.Runtime.Serialization.FormatterServices.GetSerializableMembers%28System.Type%29?displayProperty=nameWithType> method.</span></span>
- <span data-ttu-id="7a824-466">改善呼叫 **ChannelSynchronizer.RemoveWaiter** 方法移除等候者時的可靠性。</span><span class="sxs-lookup"><span data-stu-id="7a824-466">Improved reliability when removing a waiter by calling the **ChannelSynchronizer.RemoveWaiter** method.</span></span>

<a name="wf47"></a>

#### <a name="windows-forms"></a><span data-ttu-id="7a824-467">Windows Forms</span><span class="sxs-lookup"><span data-stu-id="7a824-467">Windows Forms</span></span>

<span data-ttu-id="7a824-468">在 .NET Framework 4.7 中，Windows Forms 改善對高 DPI 監視器的支援。</span><span class="sxs-lookup"><span data-stu-id="7a824-468">In .NET Framework 4.7, Windows Forms improves support for high DPI monitors.</span></span>

<span data-ttu-id="7a824-469">**高 DPI 支援**</span><span class="sxs-lookup"><span data-stu-id="7a824-469">**High DPI support**</span></span>

<span data-ttu-id="7a824-470">從針對 .NET Framework 4.7 設計的應用程式開始，.NET Framework 具備 Windows Forms 應用程式的高 DPI 與動態 DPI 支援。</span><span class="sxs-lookup"><span data-stu-id="7a824-470">Starting with applications that target .NET Framework 4.7, the .NET Framework features high DPI and dynamic DPI support for Windows Forms applications.</span></span> <span data-ttu-id="7a824-471">高 DPI 支援可改善高 DPI 監視器上表單和控制項的配置和外觀。</span><span class="sxs-lookup"><span data-stu-id="7a824-471">High DPI support improves the layout and appearance of forms and controls on high DPI monitors.</span></span> <span data-ttu-id="7a824-472">動態 DPI 則可在使用者變更執行中應用程式的 DPI 或顯示比例時，變更表單和控制項的配置和外觀。</span><span class="sxs-lookup"><span data-stu-id="7a824-472">Dynamic DPI changes the layout and appearance of forms and controls when the user changes the DPI or display scale factor of a running application.</span></span>

<span data-ttu-id="7a824-473">高 DPI 支援是加入宣告的功能，您可以 [\<System.Windows.Forms.ConfigurationSection>](../configure-apps/file-schema/winforms/index.md) 在應用程式佈建檔中定義區段來進行設定。</span><span class="sxs-lookup"><span data-stu-id="7a824-473">High DPI support is an opt-in feature that you configure by defining a [\<System.Windows.Forms.ConfigurationSection>](../configure-apps/file-schema/winforms/index.md) section in your application configuration file.</span></span> <span data-ttu-id="7a824-474">如需有關如何將高 DPI 支援和動態 DPI 支援加入至 Windows Forms 應用程式的詳細資訊，請參閱 [Windows Forms 中的高 DPI 支援](/dotnet/desktop/winforms/high-dpi-support-in-windows-forms)。</span><span class="sxs-lookup"><span data-stu-id="7a824-474">For more information on adding high DPI support and dynamic DPI support to your Windows Forms application, see [High DPI Support in Windows Forms](/dotnet/desktop/winforms/high-dpi-support-in-windows-forms).</span></span>

<a name="WPF47"></a>

#### <a name="windows-presentation-foundation-wpf"></a><span data-ttu-id="7a824-475">Windows Presentation Foundation (WPF)</span><span class="sxs-lookup"><span data-stu-id="7a824-475">Windows Presentation Foundation (WPF)</span></span>

<span data-ttu-id="7a824-476">在 .NET Framework 4.7 中，WPF 包含下列增強功能︰</span><span class="sxs-lookup"><span data-stu-id="7a824-476">In .NET Framework 4.7, WPF includes the following enhancements:</span></span>

<span data-ttu-id="7a824-477">**根據 Windows WM_POINTER 訊息對觸控/手寫筆堆疊的支援**</span><span class="sxs-lookup"><span data-stu-id="7a824-477">**Support for a touch/stylus stack based on Windows WM_POINTER messages**</span></span>

<span data-ttu-id="7a824-478">您現在可以選擇根據 [WM_POINTER 訊息 (英文)](/previous-versions/windows/desktop/InputMsg/messages) 來使用觸控/手寫筆堆疊，而不是根據 Windows Ink Services Platform (WISP)。</span><span class="sxs-lookup"><span data-stu-id="7a824-478">You now have the option of using a touch/stylus stack based on [WM_POINTER messages](/previous-versions/windows/desktop/InputMsg/messages) instead of the Windows Ink Services Platform (WISP).</span></span> <span data-ttu-id="7a824-479">這是 .NET Framework 中的加入宣告功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-479">This is an opt-in feature in .NET Framework.</span></span> <span data-ttu-id="7a824-480">如需詳細資訊，請參閱 [應用程式相容性](../migration-guide/application-compatibility.md) 一節。</span><span class="sxs-lookup"><span data-stu-id="7a824-480">For more information, see the [Application compatibility](../migration-guide/application-compatibility.md) section.</span></span>

<span data-ttu-id="7a824-481">**新的 WPF 列印 API 實作**</span><span class="sxs-lookup"><span data-stu-id="7a824-481">**New implementation for WPF printing APIs**</span></span>

<span data-ttu-id="7a824-482">WPF 在 <xref:System.Printing.PrintQueue?displayProperty=nameWithType> 類別中的列印 API 會呼叫 Windows [列印文件套件 API](/windows/desktop/printdocs/tailored-app-printing-api)，而不是已被取代的 [XPS 列印 API](/windows/desktop/printdocs/xps-printing)。</span><span class="sxs-lookup"><span data-stu-id="7a824-482">WPF's printing APIs in the <xref:System.Printing.PrintQueue?displayProperty=nameWithType> class call the Windows [Print Document Package API](/windows/desktop/printdocs/tailored-app-printing-api) instead of the deprecated [XPS Print API](/windows/desktop/printdocs/xps-printing).</span></span> <span data-ttu-id="7a824-483">如需這項變更對應用程式相容性的影響，請參閱 [應用程式相容性](../migration-guide/application-compatibility.md) 一節。</span><span class="sxs-lookup"><span data-stu-id="7a824-483">For the impact of this change on application compatibility, see the [Application compatibility](../migration-guide/application-compatibility.md) section.</span></span>

<a name="v462"></a>

## <a name="whats-new-in-net-framework-462"></a><span data-ttu-id="7a824-484">.NET Framework 4.6.2 中的新功能</span><span class="sxs-lookup"><span data-stu-id="7a824-484">What's new in .NET Framework 4.6.2</span></span>

<span data-ttu-id="7a824-485">.NET Framework 4.6.2 包含下列領域的新功能：</span><span class="sxs-lookup"><span data-stu-id="7a824-485">The .NET Framework 4.6.2 includes new features in the following areas:</span></span>

- [<span data-ttu-id="7a824-486">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7a824-486">ASP.NET</span></span>](#ASPNET462)

- [<span data-ttu-id="7a824-487">字元類別</span><span class="sxs-lookup"><span data-stu-id="7a824-487">Character categories</span></span>](#Strings)

- [<span data-ttu-id="7a824-488">碼編譯</span><span class="sxs-lookup"><span data-stu-id="7a824-488">Cryptography</span></span>](#Crypto462)

- [<span data-ttu-id="7a824-489">SqlClient</span><span class="sxs-lookup"><span data-stu-id="7a824-489">SqlClient</span></span>](#SQLClient)

- [<span data-ttu-id="7a824-490">Windows Communication Foundation</span><span class="sxs-lookup"><span data-stu-id="7a824-490">Windows Communication Foundation</span></span>](#WCF)

- [<span data-ttu-id="7a824-491">Windows Presentation Foundation (WPF)</span><span class="sxs-lookup"><span data-stu-id="7a824-491">Windows Presentation Foundation (WPF)</span></span>](#WPF462)

- [<span data-ttu-id="7a824-492">Windows Workflow Foundation (WF)</span><span class="sxs-lookup"><span data-stu-id="7a824-492">Windows Workflow Foundation (WF)</span></span>](#WF462)

- [<span data-ttu-id="7a824-493">ClickOnce</span><span class="sxs-lookup"><span data-stu-id="7a824-493">ClickOnce</span></span>](#clickonce-1)

- [<span data-ttu-id="7a824-494">將 Windows Forms 和 WPF 應用程式轉換成 UWP 應用程式</span><span class="sxs-lookup"><span data-stu-id="7a824-494">Converting Windows Forms and WPF apps to UWP apps</span></span>](#UWPConvert)

- [<span data-ttu-id="7a824-495">調試增強功能</span><span class="sxs-lookup"><span data-stu-id="7a824-495">Debugging improvements</span></span>](#Debug462)

<span data-ttu-id="7a824-496">如需 .NET Framework 4.6.2 中加入的新 API 清單，請參閱 GitHub 上的 [.NET Framework 4.6.2 API 變更](https://github.com/Microsoft/dotnet/blob/master/releases/net462/dotnet462-api-changes.md) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="7a824-496">For a list of new APIs added to .NET Framework 4.6.2, see [.NET Framework 4.6.2 API Changes](https://github.com/Microsoft/dotnet/blob/master/releases/net462/dotnet462-api-changes.md) on GitHub.</span></span> <span data-ttu-id="7a824-497">如需 .NET Framework 4.6.2 中的功能改進以及錯誤 (Bug) 修正清單，請參閱 GitHub 上的 [.NET Framework 4.6.2 變更清單](https://github.com/Microsoft/dotnet/blob/master/releases/net462/dotnet462-changes.md) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="7a824-497">For a list of feature improvements and bug fixes in .NET Framework 4.6.2, see [.NET Framework 4.6.2 List of Changes](https://github.com/Microsoft/dotnet/blob/master/releases/net462/dotnet462-changes.md) on GitHub.</span></span> <span data-ttu-id="7a824-498">如需詳細資訊，請參閱 .NET blog 中的 [宣佈 .NET Framework 4.6.2](https://devblogs.microsoft.com/dotnet/announcing-net-framework-4-6-2/) 。</span><span class="sxs-lookup"><span data-stu-id="7a824-498">For more information, see [Announcing .NET Framework 4.6.2](https://devblogs.microsoft.com/dotnet/announcing-net-framework-4-6-2/) in the .NET blog.</span></span>

<a name="ASPNET462"></a>

### <a name="aspnet"></a><span data-ttu-id="7a824-499">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7a824-499">ASP.NET</span></span>

<span data-ttu-id="7a824-500">在 .NET Framework 4.6.2 中，ASP.NET 包含下列增強功能：</span><span class="sxs-lookup"><span data-stu-id="7a824-500">In the .NET Framework 4.6.2, ASP.NET includes the following enhancements:</span></span>

<span data-ttu-id="7a824-501">**改進對資料註解驗證程式的當地語系化錯誤訊息的支援**</span><span class="sxs-lookup"><span data-stu-id="7a824-501">**Improved support for localized error messages in data annotation validators**</span></span>

<span data-ttu-id="7a824-502">資料註解驗證程式可讓您藉由將一或多個屬性加入類別內容來執行驗證。</span><span class="sxs-lookup"><span data-stu-id="7a824-502">Data annotation validators enable you to perform validation by adding one or more attributes to a class property.</span></span> <span data-ttu-id="7a824-503">屬性的 <xref:System.ComponentModel.DataAnnotations.ValidationAttribute.ErrorMessage%2A?displayProperty=nameWithType> 項目定義了驗證失敗時的錯誤訊息文字。</span><span class="sxs-lookup"><span data-stu-id="7a824-503">The attribute's <xref:System.ComponentModel.DataAnnotations.ValidationAttribute.ErrorMessage%2A?displayProperty=nameWithType> element defines the text of the error message if validation fails.</span></span> <span data-ttu-id="7a824-504">從 .NET Framework 4.6.2 開始，ASP.NET 可讓您輕鬆地將錯誤訊息當地語系化。</span><span class="sxs-lookup"><span data-stu-id="7a824-504">Starting with the .NET Framework 4.6.2, ASP.NET makes it easy to localize error messages.</span></span> <span data-ttu-id="7a824-505">錯誤訊息將會當地語系化，如果︰</span><span class="sxs-lookup"><span data-stu-id="7a824-505">Error messages will be localized if:</span></span>

1. <span data-ttu-id="7a824-506"><xref:System.ComponentModel.DataAnnotations.ValidationAttribute.ErrorMessage%2A?displayProperty=nameWithType> 提供在驗證屬性中。</span><span class="sxs-lookup"><span data-stu-id="7a824-506">The <xref:System.ComponentModel.DataAnnotations.ValidationAttribute.ErrorMessage%2A?displayProperty=nameWithType> is provided in the validation attribute.</span></span>

2. <span data-ttu-id="7a824-507">資源檔儲存在 App_LocalResources 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="7a824-507">The resource file is stored in the App_LocalResources folder.</span></span>

3. <span data-ttu-id="7a824-508">當地語系化資源檔的名稱具有表單 `DataAnnotation.Localization.{` *名稱* `}.resx` ，其中*name*是*languageCode* `-` *country/地區碼*或*languageCode*格式的文化特性名稱。</span><span class="sxs-lookup"><span data-stu-id="7a824-508">The name of the localized resources file has the form `DataAnnotation.Localization.{`*name*`}.resx`, where *name* is a culture name in the format *languageCode*`-`*country/regionCode* or *languageCode*.</span></span>

4. <span data-ttu-id="7a824-509">資源的索引鍵名稱是指派給 <xref:System.ComponentModel.DataAnnotations.ValidationAttribute.ErrorMessage%2A?displayProperty=nameWithType> 屬性的字串，其值是當地語系化的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="7a824-509">The key name of the resource is the string assigned to the <xref:System.ComponentModel.DataAnnotations.ValidationAttribute.ErrorMessage%2A?displayProperty=nameWithType> attribute,  and its value is the localized error message.</span></span>

<span data-ttu-id="7a824-510">例如，下列資料註解屬性可針對無效評等，定義預設文化特性的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="7a824-510">For example, the following data annotation attribute defines the default culture's error message for an invalid rating.</span></span>

```csharp
public class RatingInfo
{
   [Required(ErrorMessage = "The rating must be between 1 and 10.")]
   [Display(Name = "Your Rating")]
   public int Rating { get; set; }
}
```

```vb
Public Class RatingInfo
   <Required(ErrorMessage = "The rating must be between 1 and 10.")>
   <Display(Name = "Your Rating")>
   Public Property Rating As Integer = 1
End Class
```

<span data-ttu-id="7a824-511">然後，您可以建立 DataAnnotation.Localization.fr.resx 資源檔，其索引鍵為錯誤訊息字串，而其值為當地語系化的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="7a824-511">You can then create a resource file, DataAnnotation.Localization.fr.resx, whose key is the error message string and whose value is the localized error message.</span></span> <span data-ttu-id="7a824-512">檔案必須位於 `App.LocalResources` 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="7a824-512">The file must be found in the `App.LocalResources` folder.</span></span> <span data-ttu-id="7a824-513">例如，下列是索引鍵和其法文 (fr) 當地語系化錯誤訊息的值︰</span><span class="sxs-lookup"><span data-stu-id="7a824-513">For example, the following is the key and its value in a localized French (fr) language error message:</span></span>

| <span data-ttu-id="7a824-514">Name</span><span class="sxs-lookup"><span data-stu-id="7a824-514">Name</span></span>                                 | <span data-ttu-id="7a824-515">值</span><span class="sxs-lookup"><span data-stu-id="7a824-515">Value</span></span>                                     |
| ------------------------------------ | ----------------------------------------- |
| <span data-ttu-id="7a824-516">The rating must be between 1 and 10.</span><span class="sxs-lookup"><span data-stu-id="7a824-516">The rating must be between 1 and 10.</span></span> | <span data-ttu-id="7a824-517">La note doit être comprise entre 1 et 10.</span><span class="sxs-lookup"><span data-stu-id="7a824-517">La note doit être comprise entre 1 et 10.</span></span> |

 <span data-ttu-id="7a824-518">此外，資料註解當地語系化是可延伸的。</span><span class="sxs-lookup"><span data-stu-id="7a824-518">In addition, data annotation localization is extensible.</span></span> <span data-ttu-id="7a824-519">開發人員可以藉由實作 <xref:System.Web.Globalization.IStringLocalizerProvider> 介面，在資源檔以外的位置儲存當地語系化字串，而插入他們自己的字串當地語系化程式提供者。</span><span class="sxs-lookup"><span data-stu-id="7a824-519">Developers can plug in their own string localizer provider by implementing the <xref:System.Web.Globalization.IStringLocalizerProvider> interface to store localization string somewhere other than in a resource file.</span></span>

 <span data-ttu-id="7a824-520">**對工作階段狀態存放區提供者的非同步支援**</span><span class="sxs-lookup"><span data-stu-id="7a824-520">**Async support with session-state store providers**</span></span>

 <span data-ttu-id="7a824-521">ASP.NET 現在可允許使用工作傳回方法，搭配工作階段狀態存放區提供者，藉此可讓 ASP.NET 應用程式獲得非同步處理的延展性優勢。</span><span class="sxs-lookup"><span data-stu-id="7a824-521">ASP.NET now allows task-returning methods to be used with session-state store providers, thereby allowing ASP.NET apps to get the scalability benefits of async.</span></span> <span data-ttu-id="7a824-522">為了支援工作階段狀態存放區提供者的非同步作業，ASP.NET 包含新介面 <xref:System.Web.SessionState.ISessionStateModule?displayProperty=nameWithType>，它繼承自 <xref:System.Web.IHttpModule>，可讓開發人員實作自己的工作階段狀態模組和非同步工作階段存放區提供者。</span><span class="sxs-lookup"><span data-stu-id="7a824-522">To supports asynchronous operations with session state store providers, ASP.NET includes  a new interface, <xref:System.Web.SessionState.ISessionStateModule?displayProperty=nameWithType>, which inherits from <xref:System.Web.IHttpModule> and allows developers to implement their own session-state module and async session store providers.</span></span> <span data-ttu-id="7a824-523">介面定義如下：</span><span class="sxs-lookup"><span data-stu-id="7a824-523">The interface is defined as follows:</span></span>

```csharp
public interface ISessionStateModule : IHttpModule {
    void ReleaseSessionState(HttpContext context);
    Task ReleaseSessionStateAsync(HttpContext context);
}
```

```vb
Public Interface ISessionStateModule : Inherits IHttpModule
   Sub ReleaseSessionState(context As HttpContext)
   Function ReleaseSessionStateAsync(context As HttpContext) As Task
End Interface
```

 <span data-ttu-id="7a824-524">此外，<xref:System.Web.SessionState.SessionStateUtility> 類別包含兩個新方法：<xref:System.Web.SessionState.SessionStateUtility.IsSessionStateReadOnly%2A> 和 <xref:System.Web.SessionState.SessionStateUtility.IsSessionStateRequired%2A>，它們可用來支援非同步作業。</span><span class="sxs-lookup"><span data-stu-id="7a824-524">In addition, the <xref:System.Web.SessionState.SessionStateUtility> class includes two new methods, <xref:System.Web.SessionState.SessionStateUtility.IsSessionStateReadOnly%2A> and <xref:System.Web.SessionState.SessionStateUtility.IsSessionStateRequired%2A>, that can be used to support asynchronous operations.</span></span>

 <span data-ttu-id="7a824-525">**輸出快取提供者的非同步支援**</span><span class="sxs-lookup"><span data-stu-id="7a824-525">**Async support for output-cache providers**</span></span>

 <span data-ttu-id="7a824-526">從 .NET Framework 4.6.2 開始，工作傳回方法可以用於輸出快取提供者，以提供非同步處理的延展性優勢。</span><span class="sxs-lookup"><span data-stu-id="7a824-526">Starting with the .NET Framework 4.6.2, task-returning methods can be used with output-cache providers to provide the scalability benefits of async.</span></span>  <span data-ttu-id="7a824-527">實作這些方法的提供者能減少 Web 伺服器上的執行緒阻斷，並改善 ASP.NET 服務的延展性。</span><span class="sxs-lookup"><span data-stu-id="7a824-527">Providers that implement these methods reduce thread-blocking on a web server and improve the scalability of an ASP.NET service.</span></span>

 <span data-ttu-id="7a824-528">已新增下列 API 來支援非同步輸出快取提供者︰</span><span class="sxs-lookup"><span data-stu-id="7a824-528">The following APIs have been added to support asynchronous output-cache providers:</span></span>

- <span data-ttu-id="7a824-529"><xref:System.Web.Caching.OutputCacheProviderAsync?displayProperty=nameWithType> 類別，繼承自 <xref:System.Web.Caching.OutputCacheProvider?displayProperty=nameWithType>，並可讓開發人員實作非同步的輸出快取提供者。</span><span class="sxs-lookup"><span data-stu-id="7a824-529">The <xref:System.Web.Caching.OutputCacheProviderAsync?displayProperty=nameWithType> class, which inherits from <xref:System.Web.Caching.OutputCacheProvider?displayProperty=nameWithType> and allows developers to implement an asynchronous output-cache provider.</span></span>

- <span data-ttu-id="7a824-530"><xref:System.Web.Caching.OutputCacheUtility> 類別，可提供用於設定輸出快取的 helper 方法。</span><span class="sxs-lookup"><span data-stu-id="7a824-530">The <xref:System.Web.Caching.OutputCacheUtility> class, which provides helper methods for configuring the output cache.</span></span>

- <span data-ttu-id="7a824-531"><xref:System.Web.HttpCachePolicy?displayProperty=nameWithType> 類別內的 18 個新方法。</span><span class="sxs-lookup"><span data-stu-id="7a824-531">18 new methods in the <xref:System.Web.HttpCachePolicy?displayProperty=nameWithType> class.</span></span> <span data-ttu-id="7a824-532">這些包括 <xref:System.Web.HttpCachePolicy.GetCacheability%2A>、<xref:System.Web.HttpCachePolicy.GetCacheExtensions%2A>、<xref:System.Web.HttpCachePolicy.GetETag%2A>、<xref:System.Web.HttpCachePolicy.GetETagFromFileDependencies%2A>、<xref:System.Web.HttpCachePolicy.GetMaxAge%2A>、<xref:System.Web.HttpCachePolicy.GetMaxAge%2A>、<xref:System.Web.HttpCachePolicy.GetNoStore%2A>、<xref:System.Web.HttpCachePolicy.GetNoTransforms%2A>、<xref:System.Web.HttpCachePolicy.GetOmitVaryStar%2A>、<xref:System.Web.HttpCachePolicy.GetProxyMaxAge%2A>、<xref:System.Web.HttpCachePolicy.GetRevalidation%2A>、<xref:System.Web.HttpCachePolicy.GetUtcLastModified%2A>、<xref:System.Web.HttpCachePolicy.GetVaryByCustom%2A>、<xref:System.Web.HttpCachePolicy.HasSlidingExpiration%2A> 和 <xref:System.Web.HttpCachePolicy.IsValidUntilExpires%2A>。</span><span class="sxs-lookup"><span data-stu-id="7a824-532">These include <xref:System.Web.HttpCachePolicy.GetCacheability%2A>, <xref:System.Web.HttpCachePolicy.GetCacheExtensions%2A>, <xref:System.Web.HttpCachePolicy.GetETag%2A>, <xref:System.Web.HttpCachePolicy.GetETagFromFileDependencies%2A>, <xref:System.Web.HttpCachePolicy.GetMaxAge%2A>, <xref:System.Web.HttpCachePolicy.GetMaxAge%2A>, <xref:System.Web.HttpCachePolicy.GetNoStore%2A>, <xref:System.Web.HttpCachePolicy.GetNoTransforms%2A>, <xref:System.Web.HttpCachePolicy.GetOmitVaryStar%2A>, <xref:System.Web.HttpCachePolicy.GetProxyMaxAge%2A>, <xref:System.Web.HttpCachePolicy.GetRevalidation%2A>, <xref:System.Web.HttpCachePolicy.GetUtcLastModified%2A>, <xref:System.Web.HttpCachePolicy.GetVaryByCustom%2A>, <xref:System.Web.HttpCachePolicy.HasSlidingExpiration%2A>, and <xref:System.Web.HttpCachePolicy.IsValidUntilExpires%2A>.</span></span>

- <span data-ttu-id="7a824-533"><xref:System.Web.HttpCacheVaryByContentEncodings?displayProperty=nameWithType> 類別內的 2 個新方法：<xref:System.Web.HttpCacheVaryByContentEncodings.GetContentEncodings%2A> 和 <xref:System.Web.HttpCacheVaryByContentEncodings.SetContentEncodings%2A>。</span><span class="sxs-lookup"><span data-stu-id="7a824-533">2 new methods in the <xref:System.Web.HttpCacheVaryByContentEncodings?displayProperty=nameWithType> class:  <xref:System.Web.HttpCacheVaryByContentEncodings.GetContentEncodings%2A> and <xref:System.Web.HttpCacheVaryByContentEncodings.SetContentEncodings%2A>.</span></span>

- <span data-ttu-id="7a824-534"><xref:System.Web.HttpCacheVaryByHeaders?displayProperty=nameWithType> 類別內的 2 個新方法：<xref:System.Web.HttpCacheVaryByHeaders.GetHeaders%2A> 和 <xref:System.Web.HttpCacheVaryByHeaders.SetHeaders%2A>。</span><span class="sxs-lookup"><span data-stu-id="7a824-534">2 new methods in the <xref:System.Web.HttpCacheVaryByHeaders?displayProperty=nameWithType> class: <xref:System.Web.HttpCacheVaryByHeaders.GetHeaders%2A> and <xref:System.Web.HttpCacheVaryByHeaders.SetHeaders%2A>.</span></span>

- <span data-ttu-id="7a824-535"><xref:System.Web.HttpCacheVaryByParams?displayProperty=nameWithType> 類別內的 2 個新方法：<xref:System.Web.HttpCacheVaryByParams.GetParams%2A> 和 <xref:System.Web.HttpCacheVaryByParams.SetParams%2A>。</span><span class="sxs-lookup"><span data-stu-id="7a824-535">2 new methods in the <xref:System.Web.HttpCacheVaryByParams?displayProperty=nameWithType> class: <xref:System.Web.HttpCacheVaryByParams.GetParams%2A> and <xref:System.Web.HttpCacheVaryByParams.SetParams%2A>.</span></span>

- <span data-ttu-id="7a824-536"><xref:System.Web.Caching.AggregateCacheDependency?displayProperty=nameWithType> 類別中的 <xref:System.Web.Caching.AggregateCacheDependency.GetFileDependencies%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="7a824-536">In the <xref:System.Web.Caching.AggregateCacheDependency?displayProperty=nameWithType> class, the <xref:System.Web.Caching.AggregateCacheDependency.GetFileDependencies%2A> method.</span></span>

- <span data-ttu-id="7a824-537"><xref:System.Web.Caching.CacheDependency> 中的 <xref:System.Web.Caching.CacheDependency.GetFileDependencies%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="7a824-537">In the <xref:System.Web.Caching.CacheDependency>, the <xref:System.Web.Caching.CacheDependency.GetFileDependencies%2A> method.</span></span>

<a name="Strings"></a>

### <a name="character-categories"></a><span data-ttu-id="7a824-538">字元類別</span><span class="sxs-lookup"><span data-stu-id="7a824-538">Character categories</span></span>

<span data-ttu-id="7a824-539">.NET Framework 4.6.2 中的字元是根據 [Unicode 標準8.0.0 版](https://www.unicode.org/versions/Unicode8.0.0/)進行分類。</span><span class="sxs-lookup"><span data-stu-id="7a824-539">Characters in the .NET Framework 4.6.2 are classified based on the [Unicode Standard, Version 8.0.0](https://www.unicode.org/versions/Unicode8.0.0/).</span></span> <span data-ttu-id="7a824-540">在 .NET Framework 4.6 和 .NET Framework 4.6.1 中，字元是根據 Unicode 6.3 字元類別分類。</span><span class="sxs-lookup"><span data-stu-id="7a824-540">In .NET Framework 4.6 and .NET Framework 4.6.1, characters were classified based on Unicode 6.3 character categories.</span></span>

<span data-ttu-id="7a824-541">對 Unicode 8.0 的支援僅限於 <xref:System.Globalization.CharUnicodeInfo> 類別的字元分類，以及依賴它的類型和方法。</span><span class="sxs-lookup"><span data-stu-id="7a824-541">Support for Unicode 8.0 is limited to the classification of characters by the <xref:System.Globalization.CharUnicodeInfo> class and to types and methods that rely on it.</span></span> <span data-ttu-id="7a824-542">這些包括 <xref:System.Globalization.StringInfo> 類別、多載 <xref:System.Char.GetUnicodeCategory%2A?displayProperty=nameWithType> 方法，以及 .NET Framework 規則運算式引擎可辨識的[字元類別](../../standard/base-types/character-classes-in-regular-expressions.md)。</span><span class="sxs-lookup"><span data-stu-id="7a824-542">These include the <xref:System.Globalization.StringInfo> class, the overloaded <xref:System.Char.GetUnicodeCategory%2A?displayProperty=nameWithType> method, and the [character classes](../../standard/base-types/character-classes-in-regular-expressions.md) recognized by the .NET Framework regular expression engine.</span></span>  <span data-ttu-id="7a824-543">字元和字串比較和排序不會受到此變更的影響，並且會繼續依賴基礎作業系統，在 Windows 7 系統上則是依賴 .NET Framework 所提供的字元資料。</span><span class="sxs-lookup"><span data-stu-id="7a824-543">Character and string comparison and sorting is unaffected by this change and continues to rely on the underlying operating system or, on Windows 7 systems, on character data provided by the .NET Framework.</span></span>

<span data-ttu-id="7a824-544">若要了解從 Unicode 6.0 到 Unicode 7.0 的字元類別變更，請參閱 Unicode 協會網站上的 [The Unicode Standard, Version 7.0.0 (Unicode 標準 7.0.0 版)](https://www.unicode.org/versions/Unicode7.0.0/)。</span><span class="sxs-lookup"><span data-stu-id="7a824-544">For changes in character categories from Unicode 6.0 to Unicode 7.0, see [The Unicode Standard, Version 7.0.0](https://www.unicode.org/versions/Unicode7.0.0/) at The Unicode Consortium website.</span></span> <span data-ttu-id="7a824-545">若要了解從 Unicode 7.0 到 Unicode 8.0 的變更，請參閱 Unicode 協會網站上的 [The Unicode Standard, Version 8.0.0 (Unicode 標準 8.0.0 版)](https://www.unicode.org/versions/Unicode8.0.0/)。</span><span class="sxs-lookup"><span data-stu-id="7a824-545">For changes from Unicode 7.0 to Unicode 8.0, see [The Unicode Standard, Version 8.0.0](https://www.unicode.org/versions/Unicode8.0.0/) at The Unicode Consortium website.</span></span>

<a name="Crypto462"></a>

### <a name="cryptography"></a><span data-ttu-id="7a824-546">密碼編譯</span><span class="sxs-lookup"><span data-stu-id="7a824-546">Cryptography</span></span>

<span data-ttu-id="7a824-547">**支援包含 FIPS 186-3 DSA 的 X509 憑證**</span><span class="sxs-lookup"><span data-stu-id="7a824-547">**Support for X509 certificates containing FIPS 186-3 DSA**</span></span>

<span data-ttu-id="7a824-548">.NET Framework 4.6.2 新增對 DSA (數位簽章演算法) X509 憑證的支援，X509 憑證的金鑰超過 FIPS 186-2 1024 位元的限制。</span><span class="sxs-lookup"><span data-stu-id="7a824-548">The .NET Framework 4.6.2 adds support for DSA (Digital Signature Algorithm) X509 certificates whose keys exceed the FIPS 186-2 1024-bit limit.</span></span>

<span data-ttu-id="7a824-549">除了支援較大的 FIPS 186-3 金鑰大小，.NET Framework 4.6.2 也允許使用 SHA-2 系列雜湊演算法 (SHA256、SHA384 及 SHA512) 的運算簽章。</span><span class="sxs-lookup"><span data-stu-id="7a824-549">In addition to supporting the larger key sizes of FIPS 186-3, the .NET Framework 4.6.2 allows computing signatures with the SHA-2 family of hash algorithms (SHA256, SHA384, and SHA512).</span></span> <span data-ttu-id="7a824-550">FIPS 186-3 支援是由新的 <xref:System.Security.Cryptography.DSACng?displayProperty=nameWithType> 類別所提供。</span><span class="sxs-lookup"><span data-stu-id="7a824-550">FIPS 186-3 support is provided by the new <xref:System.Security.Cryptography.DSACng?displayProperty=nameWithType> class.</span></span>

<span data-ttu-id="7a824-551">為了保持 .NET Framework 4.6 中 <xref:System.Security.Cryptography.RSA> 類別和 .NET Framework 4.6.1 中 <xref:System.Security.Cryptography.ECDsa> 類別的最新變更，.NET Framework 4.6.2 中的 <xref:System.Security.Cryptography.DSA> 抽象基底類別有額外的方法，可讓呼叫者使用此功能，而不用轉換。</span><span class="sxs-lookup"><span data-stu-id="7a824-551">In keeping with recent changes to the <xref:System.Security.Cryptography.RSA> class in .NET Framework 4.6 and the <xref:System.Security.Cryptography.ECDsa> class in .NET Framework 4.6.1, the <xref:System.Security.Cryptography.DSA> abstract base class in .NET Framework 4.6.2 has additional methods to allow callers to use this functionality without casting.</span></span> <span data-ttu-id="7a824-552">您可以呼叫 <xref:System.Security.Cryptography.X509Certificates.DSACertificateExtensions.GetDSAPrivateKey%2A?displayProperty=nameWithType> 擴充方法來簽署資料，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="7a824-552">You can call the <xref:System.Security.Cryptography.X509Certificates.DSACertificateExtensions.GetDSAPrivateKey%2A?displayProperty=nameWithType> extension method to sign data, as the following example shows.</span></span>

```csharp
public static byte[] SignDataDsaSha384(byte[] data, X509Certificate2 cert)
{
    using (DSA dsa = cert.GetDSAPrivateKey())
    {
        return dsa.SignData(data, HashAlgorithmName.SHA384);
    }
}
```

```vb
Public Shared Function SignDataDsaSha384(data As Byte(), cert As X509Certificate2) As Byte()
    Using DSA As DSA = cert.GetDSAPrivateKey()
        Return DSA.SignData(data, HashAlgorithmName.SHA384)
    End Using
End Function
```

<span data-ttu-id="7a824-553">然後您可以呼叫 <xref:System.Security.Cryptography.X509Certificates.DSACertificateExtensions.GetDSAPublicKey%2A?displayProperty=nameWithType> 擴充方法來確認簽署的資料，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="7a824-553">And you can call the <xref:System.Security.Cryptography.X509Certificates.DSACertificateExtensions.GetDSAPublicKey%2A?displayProperty=nameWithType> extension method to verify signed data, as the following example shows.</span></span>

```csharp
public static bool VerifyDataDsaSha384(byte[] data, byte[] signature, X509Certificate2 cert)
{
    using (DSA dsa = cert.GetDSAPublicKey())
    {
        return dsa.VerifyData(data, signature, HashAlgorithmName.SHA384);
    }
}
```

```vb
 Public Shared Function VerifyDataDsaSha384(data As Byte(), signature As Byte(), cert As X509Certificate2) As Boolean
    Using dsa As DSA = cert.GetDSAPublicKey()
        Return dsa.VerifyData(data, signature, HashAlgorithmName.SHA384)
    End Using
End Function
```

<span data-ttu-id="7a824-554">**ECDiffieHellman 金鑰衍生常式的輸入更加清楚**</span><span class="sxs-lookup"><span data-stu-id="7a824-554">**Increased clarity for inputs to ECDiffieHellman key derivation routines**</span></span>

<span data-ttu-id="7a824-555">.NET Framework 3.5 以三個不同的金鑰衍生函數 (KDF) 常式，新增了對橢圓曲線 Diffie-Hellman 金鑰合約的支援。</span><span class="sxs-lookup"><span data-stu-id="7a824-555">.NET Framework 3.5 added support for Elliptic Curve Diffie-Hellman Key Agreement with three different Key Derivation Function (KDF) routines.</span></span> <span data-ttu-id="7a824-556">常式的輸入以及常式本身，是透過 <xref:System.Security.Cryptography.ECDiffieHellmanCng> 物件上的屬性設定。</span><span class="sxs-lookup"><span data-stu-id="7a824-556">The inputs to the routines, and the routines themselves, were configured via properties on the <xref:System.Security.Cryptography.ECDiffieHellmanCng> object.</span></span> <span data-ttu-id="7a824-557">但由於不是每個常式都會讀取每個輸入屬性，所以很有可能對過去的開發人員造成混淆。</span><span class="sxs-lookup"><span data-stu-id="7a824-557">But since not every routine read every input property, there was ample room for confusion on the past of the developer.</span></span>

<span data-ttu-id="7a824-558">為了解決 .NET Framework 4.6.2 中的這個問題，我們對 <xref:System.Security.Cryptography.ECDiffieHellman> 基底類別新增了下列三種方法，以更清楚地表示這些 KDF 常式和其輸入︰</span><span class="sxs-lookup"><span data-stu-id="7a824-558">To address this in the .NET Framework 4.6.2, the following three methods have been added to the  <xref:System.Security.Cryptography.ECDiffieHellman> base class to more clearly represent these KDF routines and their inputs:</span></span>

|<span data-ttu-id="7a824-559">ECDiffieHellman 方法</span><span class="sxs-lookup"><span data-stu-id="7a824-559">ECDiffieHellman method</span></span>|<span data-ttu-id="7a824-560">描述</span><span class="sxs-lookup"><span data-stu-id="7a824-560">Description</span></span>|
|----------------------------|-----------------|
|<xref:System.Security.Cryptography.ECDiffieHellman.DeriveKeyFromHash%28System.Security.Cryptography.ECDiffieHellmanPublicKey%2CSystem.Security.Cryptography.HashAlgorithmName%2CSystem.Byte%5B%5D%2CSystem.Byte%5B%5D%29>|<span data-ttu-id="7a824-561">使用公式衍生金鑰內容</span><span class="sxs-lookup"><span data-stu-id="7a824-561">Derives key material using the formula</span></span><br /><br /> <span data-ttu-id="7a824-562">HASH(secretPrepend &#124;&#124; *x* &#124;&#124; secretAppend)</span><span class="sxs-lookup"><span data-stu-id="7a824-562">HASH(secretPrepend &#124;&#124; *x* &#124;&#124; secretAppend)</span></span><br /><br /> <span data-ttu-id="7a824-563">HASH(secretPrepend OrElse *x* OrElse secretAppend)</span><span class="sxs-lookup"><span data-stu-id="7a824-563">HASH(secretPrepend OrElse *x* OrElse secretAppend)</span></span><br /><br /> <span data-ttu-id="7a824-564">其中 *x* 是 EC Diffie-Hellman 演算法的計算結果。</span><span class="sxs-lookup"><span data-stu-id="7a824-564">where *x* is the computed result of the EC Diffie-Hellman algorithm.</span></span>|
|<xref:System.Security.Cryptography.ECDiffieHellman.DeriveKeyFromHmac%28System.Security.Cryptography.ECDiffieHellmanPublicKey%2CSystem.Security.Cryptography.HashAlgorithmName%2CSystem.Byte%5B%5D%2CSystem.Byte%5B%5D%2CSystem.Byte%5B%5D%29>|<span data-ttu-id="7a824-565">使用公式衍生金鑰內容</span><span class="sxs-lookup"><span data-stu-id="7a824-565">Derives key material using the formula</span></span><br /><br /> <span data-ttu-id="7a824-566">HMAC(hmacKey, secretPrepend &#124;&#124; *x* &#124;&#124; secretAppend)</span><span class="sxs-lookup"><span data-stu-id="7a824-566">HMAC(hmacKey, secretPrepend &#124;&#124; *x* &#124;&#124; secretAppend)</span></span><br /><br /> <span data-ttu-id="7a824-567">HMAC(hmacKey, secretPrepend OrElse *x* OrElse secretAppend)</span><span class="sxs-lookup"><span data-stu-id="7a824-567">HMAC(hmacKey, secretPrepend OrElse *x* OrElse secretAppend)</span></span><br /><br /> <span data-ttu-id="7a824-568">其中 *x* 是 EC Diffie-Hellman 演算法的計算結果。</span><span class="sxs-lookup"><span data-stu-id="7a824-568">where *x* is the computed result of the EC Diffie-Hellman algorithm.</span></span>|
|<xref:System.Security.Cryptography.ECDiffieHellman.DeriveKeyTls%28System.Security.Cryptography.ECDiffieHellmanPublicKey%2CSystem.Byte%5B%5D%2CSystem.Byte%5B%5D%29>|<span data-ttu-id="7a824-569">使用 TLS 似隨機函式 (PRF) 衍生演算法衍生金鑰內容。</span><span class="sxs-lookup"><span data-stu-id="7a824-569">Derives key material using the TLS pseudo-random function (PRF) derivation algorithm.</span></span>|

<span data-ttu-id="7a824-570">**對必要金鑰對稱式加密的支援**</span><span class="sxs-lookup"><span data-stu-id="7a824-570">**Support for persisted-key symmetric encryption**</span></span>

<span data-ttu-id="7a824-571">Windows 密碼編譯程式庫 (CNG) 新增了儲存永久對稱金鑰和使用硬體儲存之對稱金鑰的支援，而 .NET Framework 4.6.2 可讓開發人員利用此功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-571">The Windows cryptography library (CNG) added support for storing persisted symmetric keys and using hardware-stored symmetric keys, and the .NET Framework 4.6.2 made it possible for developers to make use of this feature.</span></span>  <span data-ttu-id="7a824-572">由於金鑰名稱和金鑰提供者的概念是因實作而定，使用此功能需要使用實體實作類型的建構函式，而不是慣用的 factory 方法 (例如呼叫 `Aes.Create`)。</span><span class="sxs-lookup"><span data-stu-id="7a824-572">Since the notion of key names and key providers is implementation-specific, using this feature requires utilizing the constructor of the concrete implementation types instead of the preferred factory approach (such as calling `Aes.Create`).</span></span>

<span data-ttu-id="7a824-573">AES (<xref:System.Security.Cryptography.AesCng>) 及 3DES (<xref:System.Security.Cryptography.TripleDESCng>) 演算法具有必要金鑰的對稱加密支援。</span><span class="sxs-lookup"><span data-stu-id="7a824-573">Persisted-key symmetric encryption support exists for the AES (<xref:System.Security.Cryptography.AesCng>) and 3DES (<xref:System.Security.Cryptography.TripleDESCng>) algorithms.</span></span> <span data-ttu-id="7a824-574">例如：</span><span class="sxs-lookup"><span data-stu-id="7a824-574">For example:</span></span>

```csharp
public static byte[] EncryptDataWithPersistedKey(byte[] data, byte[] iv)
{
    using (Aes aes = new AesCng("AesDemoKey", CngProvider.MicrosoftSoftwareKeyStorageProvider))
    {
        aes.IV = iv;

        // Using the zero-argument overload is required to make use of the persisted key
        using (ICryptoTransform encryptor = aes.CreateEncryptor())
        {
            if (!encryptor.CanTransformMultipleBlocks)
            {
                throw new InvalidOperationException("This is a sample, this case wasn't handled...");
            }

            return encryptor.TransformFinalBlock(data, 0, data.Length);
        }
    }
}
```

```vb
Public Shared Function EncryptDataWithPersistedKey(data As Byte(), iv As Byte()) As Byte()
    Using Aes As Aes = New AesCng("AesDemoKey", CngProvider.MicrosoftSoftwareKeyStorageProvider)
        Aes.IV = iv

        ' Using the zero-argument overload Is required to make use of the persisted key
        Using encryptor As ICryptoTransform = Aes.CreateEncryptor()
            If Not encryptor.CanTransformMultipleBlocks Then
                Throw New InvalidOperationException("This is a sample, this case wasn't handled...")
            End If
            Return encryptor.TransformFinalBlock(data, 0, data.Length)
        End Using
    End Using
End Function
```

<span data-ttu-id="7a824-575">**SHA-2 雜湊的 SignedXml 支援**</span><span class="sxs-lookup"><span data-stu-id="7a824-575">**SignedXml support for SHA-2 hashing**</span></span>

<span data-ttu-id="7a824-576">.NET Framework 4.6.2 對 RSA-SHA256、RSA-SHA384 和 RSA-SHA512 PKCS#1 簽章方法，以及 SHA256、SHA384 和 SHA512 參考摘要演算法的 <xref:System.Security.Cryptography.Xml.SignedXml> 類別新增了支援。</span><span class="sxs-lookup"><span data-stu-id="7a824-576">The .NET Framework 4.6.2 adds support to  the <xref:System.Security.Cryptography.Xml.SignedXml> class for RSA-SHA256, RSA-SHA384, and RSA-SHA512 PKCS#1 signature methods, and SHA256, SHA384, and SHA512 reference digest algorithms.</span></span>

<span data-ttu-id="7a824-577">URI 常數會公開在 <xref:System.Security.Cryptography.Xml.SignedXml>：</span><span class="sxs-lookup"><span data-stu-id="7a824-577">The URI constants are all exposed on <xref:System.Security.Cryptography.Xml.SignedXml>:</span></span>

|<span data-ttu-id="7a824-578">SignedXml 欄位</span><span class="sxs-lookup"><span data-stu-id="7a824-578">SignedXml field</span></span>|<span data-ttu-id="7a824-579">常數</span><span class="sxs-lookup"><span data-stu-id="7a824-579">Constant</span></span>|
|---------------------|--------------|
|<xref:System.Security.Cryptography.Xml.SignedXml.XmlDsigSHA256Url>|<span data-ttu-id="7a824-580">"http://www.w3.org/2001/04/xmlenc#sha256"</span><span class="sxs-lookup"><span data-stu-id="7a824-580">"http://www.w3.org/2001/04/xmlenc#sha256"</span></span>|
|<xref:System.Security.Cryptography.Xml.SignedXml.XmlDsigRSASHA256Url>|<span data-ttu-id="7a824-581">"http://www.w3.org/2001/04/xmldsig-more#rsa-sha256"</span><span class="sxs-lookup"><span data-stu-id="7a824-581">"http://www.w3.org/2001/04/xmldsig-more#rsa-sha256"</span></span>|
|<xref:System.Security.Cryptography.Xml.SignedXml.XmlDsigSHA384Url>|<span data-ttu-id="7a824-582">"http://www.w3.org/2001/04/xmldsig-more#sha384"</span><span class="sxs-lookup"><span data-stu-id="7a824-582">"http://www.w3.org/2001/04/xmldsig-more#sha384"</span></span>|
|<xref:System.Security.Cryptography.Xml.SignedXml.XmlDsigRSASHA384Url>|<span data-ttu-id="7a824-583">"http://www.w3.org/2001/04/xmldsig-more#rsa-sha384"</span><span class="sxs-lookup"><span data-stu-id="7a824-583">"http://www.w3.org/2001/04/xmldsig-more#rsa-sha384"</span></span>|
|<xref:System.Security.Cryptography.Xml.SignedXml.XmlDsigSHA512Url>|<span data-ttu-id="7a824-584">"http://www.w3.org/2001/04/xmlenc#sha512"</span><span class="sxs-lookup"><span data-stu-id="7a824-584">"http://www.w3.org/2001/04/xmlenc#sha512"</span></span>|
|<xref:System.Security.Cryptography.Xml.SignedXml.XmlDsigRSASHA512Url>|<span data-ttu-id="7a824-585">"http://www.w3.org/2001/04/xmldsig-more#rsa-sha512"</span><span class="sxs-lookup"><span data-stu-id="7a824-585">"http://www.w3.org/2001/04/xmldsig-more#rsa-sha512"</span></span>|

 <span data-ttu-id="7a824-586">任何已註冊自訂 <xref:System.Security.Cryptography.SignatureDescription> 處理常式到 <xref:System.Security.Cryptography.CryptoConfig> 以新增這些演算法支援的程式，將會繼續如過去一般運作，但是因為現在有平台預設值，所以不再需要 <xref:System.Security.Cryptography.CryptoConfig> 註冊。</span><span class="sxs-lookup"><span data-stu-id="7a824-586">Any programs that have registered a custom <xref:System.Security.Cryptography.SignatureDescription> handler into <xref:System.Security.Cryptography.CryptoConfig> to add support for these algorithms will continue to function as they did in the past, but since there are now platform defaults, the <xref:System.Security.Cryptography.CryptoConfig> registration is no longer necessary.</span></span>

<a name="SQLClient"></a>

### <a name="sqlclient"></a><span data-ttu-id="7a824-587">SqlClient</span><span class="sxs-lookup"><span data-stu-id="7a824-587">SqlClient</span></span>

<span data-ttu-id="7a824-588">.NET Framework Data Provider for SQL Server (<xref:System.Data.SqlClient?displayProperty=nameWithType>) 包含下列 .NET Framework 4.6.2 中的新功能：</span><span class="sxs-lookup"><span data-stu-id="7a824-588">.NET Framework Data Provider for SQL Server (<xref:System.Data.SqlClient?displayProperty=nameWithType>) includes the following new features in the .NET Framework 4.6.2:</span></span>

<span data-ttu-id="7a824-589">**Azure SQL 資料庫的連接共用和逾時**</span><span class="sxs-lookup"><span data-stu-id="7a824-589">**Connection pooling and timeouts with Azure SQL databases**</span></span>

<span data-ttu-id="7a824-590">當連接共用已啟用，且發生超時或其他登入錯誤時，就會快取例外狀況，並在接下來的5秒到1分鐘的任何後續連接嘗試上擲回快取的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="7a824-590">When connection pooling is enabled and a timeout or other login error occurs, an exception is cached, and the cached exception is thrown on any subsequent connection attempt for the next 5 seconds to 1 minute.</span></span> <span data-ttu-id="7a824-591">如需詳細資訊，請參閱 [SQL Server 連線共用 (ADO.NET)](../data/adonet/sql-server-connection-pooling.md) \(機器翻譯\)。</span><span class="sxs-lookup"><span data-stu-id="7a824-591">For more information, see [SQL Server Connection Pooling (ADO.NET)](../data/adonet/sql-server-connection-pooling.md).</span></span>

<span data-ttu-id="7a824-592">連線到 Azure SQL 資料庫時，這個行為並不理想，因為連線嘗試可能會因暫時性錯誤而失敗，但暫時性錯誤通常很快就可復原。</span><span class="sxs-lookup"><span data-stu-id="7a824-592">This behavior is not desirable when connecting to Azure SQL Databases, since connection attempts can fail with transient errors that are typically recovered quickly.</span></span> <span data-ttu-id="7a824-593">為了進一步最佳化連線重試體驗，在 Azure SQL 資料庫連線失敗時，已移除連線集區封鎖期間行為。</span><span class="sxs-lookup"><span data-stu-id="7a824-593">To better optimize the connection retry experience, the connection pool blocking period behavior is removed when connections to Azure SQL Databases fail.</span></span>

<span data-ttu-id="7a824-594">新增 `PoolBlockingPeriod` 關鍵字可讓您選取最適合您應用程式的封鎖期間。</span><span class="sxs-lookup"><span data-stu-id="7a824-594">The addition of the new `PoolBlockingPeriod` keyword lets you select the blocking period best suited for your app.</span></span> <span data-ttu-id="7a824-595">數值包括：</span><span class="sxs-lookup"><span data-stu-id="7a824-595">Values include:</span></span>

<xref:System.Data.SqlClient.PoolBlockingPeriod.Auto>

<span data-ttu-id="7a824-596">對於連線到 Azure SQL 資料庫的應用程式，已停用連線集區封鎖期間，而對於連線到任何其他 SQL Server 執行個體的應用程式，已啟用連線集區封鎖期間。</span><span class="sxs-lookup"><span data-stu-id="7a824-596">The connection pool blocking period for an application that connects to an Azure SQL Database is disabled, and the connection pool blocking period for an application that connects to any other SQL Server instance is enabled.</span></span> <span data-ttu-id="7a824-597">這是預設值。</span><span class="sxs-lookup"><span data-stu-id="7a824-597">This is the default value.</span></span> <span data-ttu-id="7a824-598">如果伺服器端點名稱結尾是下列任一項，則會被視為 Azure SQL 資料庫︰</span><span class="sxs-lookup"><span data-stu-id="7a824-598">If the Server endpoint name ends with any of the following, they are considered Azure SQL Databases:</span></span>

- <span data-ttu-id="7a824-599">.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="7a824-599">.database.windows.net</span></span>

- <span data-ttu-id="7a824-600">.database.chinacloudapi.cn</span><span class="sxs-lookup"><span data-stu-id="7a824-600">.database.chinacloudapi.cn</span></span>

- <span data-ttu-id="7a824-601">.database.usgovcloudapi.net</span><span class="sxs-lookup"><span data-stu-id="7a824-601">.database.usgovcloudapi.net</span></span>

- <span data-ttu-id="7a824-602">.database.cloudapi.de</span><span class="sxs-lookup"><span data-stu-id="7a824-602">.database.cloudapi.de</span></span>

<xref:System.Data.SqlClient.PoolBlockingPeriod.AlwaysBlock>

<span data-ttu-id="7a824-603">一律啟用連線集區封鎖期間。</span><span class="sxs-lookup"><span data-stu-id="7a824-603">The connection pool blocking period is always enabled.</span></span>

<xref:System.Data.SqlClient.PoolBlockingPeriod.NeverBlock>

<span data-ttu-id="7a824-604">一律停用連線集區封鎖期間。</span><span class="sxs-lookup"><span data-stu-id="7a824-604">The connection pool blocking period is always disabled.</span></span>

<span data-ttu-id="7a824-605">**Always Encrypted 的增強功能**</span><span class="sxs-lookup"><span data-stu-id="7a824-605">**Enhancements for Always Encrypted**</span></span>

<span data-ttu-id="7a824-606">SQLClient 導入兩個 Always Encrypted 增強功能︰</span><span class="sxs-lookup"><span data-stu-id="7a824-606">SQLClient introduces two enhancements for Always Encrypted:</span></span>

- <span data-ttu-id="7a824-607">為了改善對加密資料庫資料行的參數化查詢效能，現在會快取查詢參數的加密中繼資料。</span><span class="sxs-lookup"><span data-stu-id="7a824-607">To improve performance of parameterized queries against encrypted database columns, encryption metadata for query parameters is now cached.</span></span> <span data-ttu-id="7a824-608">當 <xref:System.Data.SqlClient.SqlConnection.ColumnEncryptionQueryMetadataCacheEnabled%2A?displayProperty=nameWithType> 屬性設定為 `true` (此為預設值) 時，如果多次呼叫相同的查詢，則用戶端只會從伺服器擷取一次參數中繼資料。</span><span class="sxs-lookup"><span data-stu-id="7a824-608">With the <xref:System.Data.SqlClient.SqlConnection.ColumnEncryptionQueryMetadataCacheEnabled%2A?displayProperty=nameWithType> property set to `true` (which is the default value), if the same query is called multiple times, the client retrieves parameter metadata from the server only once.</span></span>

- <span data-ttu-id="7a824-609">金鑰快取中的資料行加密金鑰項目現在會在可設定的時間間隔之後收回，而此時間間隔是使用 <xref:System.Data.SqlClient.SqlConnection.ColumnEncryptionKeyCacheTtl%2A?displayProperty=nameWithType> 屬性設定。</span><span class="sxs-lookup"><span data-stu-id="7a824-609">Column encryption key entries in the key cache are now evicted after a configurable time interval, set using the <xref:System.Data.SqlClient.SqlConnection.ColumnEncryptionKeyCacheTtl%2A?displayProperty=nameWithType> property.</span></span>

<a name="WCF"></a>

### <a name="windows-communication-foundation"></a><span data-ttu-id="7a824-610">Windows Communication Foundation</span><span class="sxs-lookup"><span data-stu-id="7a824-610">Windows Communication Foundation</span></span>

<span data-ttu-id="7a824-611">在 .NET Framework 4.6.2 中，Windows Communication Foundation 已增強下列領域︰</span><span class="sxs-lookup"><span data-stu-id="7a824-611">In the .NET Framework 4.6.2, Windows Communication Foundation has been enhanced in the following areas:</span></span>

<span data-ttu-id="7a824-612">**使用 CNG 儲存之憑證的 WCF 傳輸安全性支援**</span><span class="sxs-lookup"><span data-stu-id="7a824-612">**WCF transport security support for certificates stored using CNG**</span></span>

<span data-ttu-id="7a824-613">WCF 傳輸安全性支援使用 Windows 密碼編譯程式庫 (CNG) 儲存的憑證。</span><span class="sxs-lookup"><span data-stu-id="7a824-613">WCF transport security supports certificates stored using the Windows cryptography library (CNG).</span></span> <span data-ttu-id="7a824-614">在 .NET Framework 4.6.2 中，此支援僅限於使用具有公開金鑰的憑證，且指數長度不能超過 32 位元。</span><span class="sxs-lookup"><span data-stu-id="7a824-614">In the .NET Framework 4.6.2, this support is limited to using certificates with a public key that has an exponent no more than 32 bits in length.</span></span> <span data-ttu-id="7a824-615">當應用程式以 .NET Framework 4.6.2 為目標時，此功能預設為開啟。</span><span class="sxs-lookup"><span data-stu-id="7a824-615">When an application targets the .NET Framework 4.6.2, this feature is on by default.</span></span>

<span data-ttu-id="7a824-616">針對以 .NET Framework 4.6.1 和更早版本為目標，但在 .NET Framework 4.6.2 上執行的應用程式，可以藉由將下列這一行新增至 app.config 或 web.config 檔案的區段來啟用這項功能 [\<runtime>](../configure-apps/file-schema/runtime/runtime-element.md) 。</span><span class="sxs-lookup"><span data-stu-id="7a824-616">For applications that target the .NET Framework 4.6.1 and earlier but are running on the .NET Framework 4.6.2, this feature can be enabled by adding the following line to the [\<runtime>](../configure-apps/file-schema/runtime/runtime-element.md) section of the app.config or web.config file.</span></span>

```xml
<AppContextSwitchOverrides
    value="Switch.System.ServiceModel.DisableCngCertificates=false"
/>
```

<span data-ttu-id="7a824-617">這也可以用程式設計方式，以如下的程式碼完成︰</span><span class="sxs-lookup"><span data-stu-id="7a824-617">This can also be done programmatically with code like the following:</span></span>

```csharp
private const string DisableCngCertificates = @"Switch.System.ServiceModel.DisableCngCertificates";
AppContext.SetSwitch(disableCngCertificates, false);
```

```vb
Const DisableCngCertificates As String = "Switch.System.ServiceModel.DisableCngCertificates"
AppContext.SetSwitch(disableCngCertificates, False)
```

<span data-ttu-id="7a824-618">**更妥善支援 DataContractJsonSerializer 類別的多個日光節約時間調整規則**</span><span class="sxs-lookup"><span data-stu-id="7a824-618">**Better support for multiple daylight saving time adjustment rules by the DataContractJsonSerializer class**</span></span>

<span data-ttu-id="7a824-619">客戶可以使用應用程式組態設定來判斷 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 類別是否支援對單一時區使用多個調整規則。</span><span class="sxs-lookup"><span data-stu-id="7a824-619">Customers can use an application configuration setting to determine whether the <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> class supports multiple adjustment rules for a single time zone.</span></span> <span data-ttu-id="7a824-620">這是一項選擇性功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-620">This is an opt-in feature.</span></span> <span data-ttu-id="7a824-621">若要啟用它，請將下列設定加入您的 app.config 檔︰</span><span class="sxs-lookup"><span data-stu-id="7a824-621">To enable it, add the following setting to your app.config file:</span></span>

```xml
<runtime>
     <AppContextSwitchOverrides value="Switch.System.Runtime.Serialization.DoNotUseTimeZoneInfo=false" />
</runtime>
```

<span data-ttu-id="7a824-622">啟用這項功能時，<xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 物件會使用 <xref:System.TimeZoneInfo> 類型，而非使用 <xref:System.TimeZone> 類型來將日期和時間資料還原序列化。</span><span class="sxs-lookup"><span data-stu-id="7a824-622">When this feature is enabled, a <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> object uses the <xref:System.TimeZoneInfo> type instead of the <xref:System.TimeZone> type to deserialize date and time data.</span></span> <span data-ttu-id="7a824-623"><xref:System.TimeZoneInfo> 支援多個調整規則，如此可讓您使用歷史時區資料；<xref:System.TimeZone> 則否。</span><span class="sxs-lookup"><span data-stu-id="7a824-623"><xref:System.TimeZoneInfo> supports multiple adjustment rules, which makes it possible to work with historic time zone data;   <xref:System.TimeZone> does not.</span></span>

<span data-ttu-id="7a824-624">如需有關 <xref:System.TimeZoneInfo> 結構和時區調整的詳細資訊，請參閱[時區概觀](../../standard/datetime/time-zone-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="7a824-624">For more information on the <xref:System.TimeZoneInfo> structure and time zone adjustments, see [Time Zone Overview](../../standard/datetime/time-zone-overview.md).</span></span>

<span data-ttu-id="7a824-625">**NetNamedPipeBinding 最符合項目**</span><span class="sxs-lookup"><span data-stu-id="7a824-625">**NetNamedPipeBinding best match**</span></span>

<span data-ttu-id="7a824-626">WCF 有新的應用程式設定，可以在用戶端應用程式上設定，以確保它們一律連線到在最符合所要求之 URI 上接聽的服務。</span><span class="sxs-lookup"><span data-stu-id="7a824-626">WCF has a new app setting that can be set on client applications to ensure they always connect to the service listening on the URI that best matches the one that they request.</span></span> <span data-ttu-id="7a824-627">當此應用程式設定設為 `false` (預設值) 時，用戶端可以使用 <xref:System.ServiceModel.NetNamedPipeBinding> 來嘗試連接到正在接聽所要求 URI 子字串之 URI 的服務。</span><span class="sxs-lookup"><span data-stu-id="7a824-627">With this app setting set to `false` (the default), it is possible for clients using <xref:System.ServiceModel.NetNamedPipeBinding> to attempt to connect to a service listening on a URI that is a substring of the requested URI.</span></span>

<span data-ttu-id="7a824-628">例如，用戶端嘗試連接到接聽 `net.pipe://localhost/Service1` 的服務，但該電腦上以系統管理員權限執行的不同服務正在接聽 `net.pipe://localhost`。</span><span class="sxs-lookup"><span data-stu-id="7a824-628">For example, a client tries to connect to a service listening at `net.pipe://localhost/Service1`, but a different service on that machine running with administrator privilege is listening at `net.pipe://localhost`.</span></span> <span data-ttu-id="7a824-629">當此應用程式設定是設為 `false` 時，用戶端會嘗試連線到錯誤的服務。</span><span class="sxs-lookup"><span data-stu-id="7a824-629">With this app setting set to `false`, the client would attempt to connect to the wrong service.</span></span> <span data-ttu-id="7a824-630">將應用程式設定設為 `true` 後，用戶端一律都會連接至最符合的服務。</span><span class="sxs-lookup"><span data-stu-id="7a824-630">After setting the app setting to `true`, the client will always connect to the best matching service.</span></span>

> [!NOTE]
> <span data-ttu-id="7a824-631">使用 <xref:System.ServiceModel.NetNamedPipeBinding> 的用戶端會根據服務的基底位址 (如果存在的話) 來尋找服務，而不是根據完整的端點位址。</span><span class="sxs-lookup"><span data-stu-id="7a824-631">Clients using <xref:System.ServiceModel.NetNamedPipeBinding> find services based on the service's base address (if it exists) rather than the full endpoint address.</span></span> <span data-ttu-id="7a824-632">為了確保此設定一律適用，服務應該使用唯一的基底位址。</span><span class="sxs-lookup"><span data-stu-id="7a824-632">To ensure this setting always works the service should use a unique base address.</span></span>

<span data-ttu-id="7a824-633">若要啟用此變更，請先將下列應用程式設定加入用戶端應用程式的 App.config 或 Web.config 檔案︰</span><span class="sxs-lookup"><span data-stu-id="7a824-633">To enable this change, add the following app setting to your client application's App.config or Web.config file:</span></span>

```xml
<configuration>
    <appSettings>
        <add key="wcf:useBestMatchNamedPipeUri" value="true" />
    </appSettings>
</configuration>
```

<span data-ttu-id="7a824-634">**SSL 3.0 不是預設的通訊協定**</span><span class="sxs-lookup"><span data-stu-id="7a824-634">**SSL 3.0 is not a default protocol**</span></span>

<span data-ttu-id="7a824-635">當使用 NetTcp 搭配傳輸安全性和憑證類型的認證時，SSL 3.0 已不再是用來交涉安全連線的預設通訊協定。</span><span class="sxs-lookup"><span data-stu-id="7a824-635">When using NetTcp with transport security and a credential type of certificate, SSL 3.0 is no longer a default protocol used for negotiating a secure connection.</span></span> <span data-ttu-id="7a824-636">在大部分的情況下，應該不會影響現有的應用程式，因為 TLS 1.0 已包含在 NetTcp 的通訊協定清單中。</span><span class="sxs-lookup"><span data-stu-id="7a824-636">In most cases, there should be no impact to existing apps, because TLS 1.0 is included in the protocol list for NetTcp.</span></span> <span data-ttu-id="7a824-637">所有現有的用戶端應該能夠使用至少 TLS 1.0 來交涉連線。</span><span class="sxs-lookup"><span data-stu-id="7a824-637">All existing clients should be able to negotiate a connection using at least TLS 1.0.</span></span> <span data-ttu-id="7a824-638">如果需要 SSL3，請使用下列組態機制之一，將它加入交涉通訊協定的清單。</span><span class="sxs-lookup"><span data-stu-id="7a824-638">If Ssl3 is required, use one of the following configuration mechanisms to add it to the list of negotiated protocols.</span></span>

- <span data-ttu-id="7a824-639"><xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement.SslProtocols%2A?displayProperty=nameWithType> 屬性</span><span class="sxs-lookup"><span data-stu-id="7a824-639">The <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement.SslProtocols%2A?displayProperty=nameWithType> property</span></span>

- <span data-ttu-id="7a824-640"><xref:System.ServiceModel.TcpTransportSecurity.SslProtocols%2A?displayProperty=nameWithType> 屬性</span><span class="sxs-lookup"><span data-stu-id="7a824-640">The <xref:System.ServiceModel.TcpTransportSecurity.SslProtocols%2A?displayProperty=nameWithType> property</span></span>

- <span data-ttu-id="7a824-641">[\<transport>](../configure-apps/file-schema/wcf/transport-of-nettcpbinding.md)區段的區段 [\<netTcpBinding>](../configure-apps/file-schema/wcf/nettcpbinding.md)</span><span class="sxs-lookup"><span data-stu-id="7a824-641">The [\<transport>](../configure-apps/file-schema/wcf/transport-of-nettcpbinding.md) section of the [\<netTcpBinding>](../configure-apps/file-schema/wcf/nettcpbinding.md) section</span></span>

- <span data-ttu-id="7a824-642">[\<sslStreamSecurity>](../configure-apps/file-schema/wcf/sslstreamsecurity.md)區段的區段 [\<customBinding>](../configure-apps/file-schema/wcf/custombinding.md)</span><span class="sxs-lookup"><span data-stu-id="7a824-642">The [\<sslStreamSecurity>](../configure-apps/file-schema/wcf/sslstreamsecurity.md) section of the [\<customBinding>](../configure-apps/file-schema/wcf/custombinding.md) section</span></span>

<a name="WPF462"></a>

### <a name="windows-presentation-foundation-wpf"></a><span data-ttu-id="7a824-643">Windows Presentation Foundation (WPF)</span><span class="sxs-lookup"><span data-stu-id="7a824-643">Windows Presentation Foundation (WPF)</span></span>

<span data-ttu-id="7a824-644">在 .NET Framework 4.6.2 中，Windows Presentation Foundation 已增強下列領域︰</span><span class="sxs-lookup"><span data-stu-id="7a824-644">In the .NET Framework 4.6.2, Windows Presentation Foundation has been enhanced in the following areas:</span></span>

<span data-ttu-id="7a824-645">**群組排序**</span><span class="sxs-lookup"><span data-stu-id="7a824-645">**Group sorting**</span></span>

<span data-ttu-id="7a824-646">使用 <xref:System.Windows.Data.CollectionView> 物件來分組資料的應用程式，現在可以明確地宣告如何排序群組。</span><span class="sxs-lookup"><span data-stu-id="7a824-646">An application that uses a <xref:System.Windows.Data.CollectionView> object to group data can now explicitly declare how to  sort the groups.</span></span> <span data-ttu-id="7a824-647">明確排序可以解決非直覺式排序的問題，此問題發生於應用程式以動態方式新增或移除群組時，或是變更分組時所干涉的項目屬性值時。</span><span class="sxs-lookup"><span data-stu-id="7a824-647">Explicit sorting addresses the problem of non-intuitive ordering that occurs when an app dynamically adds or removes groups, or when it changes the value of item properties involved in grouping.</span></span> <span data-ttu-id="7a824-648">它也可以藉由將分組屬性的比較從完整集合排序移至群組排序，改善群組建立程序的效能。</span><span class="sxs-lookup"><span data-stu-id="7a824-648">It can also improve the performance of the group creation process by moving comparisons of the grouping properties from the sort of the full collection to the sort of the groups.</span></span>

<span data-ttu-id="7a824-649">為了支援群組排序，新的 <xref:System.ComponentModel.GroupDescription.SortDescriptions%2A?displayProperty=nameWithType> 和 <xref:System.ComponentModel.GroupDescription.CustomSort%2A?displayProperty=nameWithType> 屬性會描述如何排序 <xref:System.ComponentModel.GroupDescription> 物件所產生的群組集合。</span><span class="sxs-lookup"><span data-stu-id="7a824-649">To support group sorting, the new <xref:System.ComponentModel.GroupDescription.SortDescriptions%2A?displayProperty=nameWithType> and <xref:System.ComponentModel.GroupDescription.CustomSort%2A?displayProperty=nameWithType> properties describe how to sort the collection of groups produced by the <xref:System.ComponentModel.GroupDescription> object.</span></span> <span data-ttu-id="7a824-650">這相當於同名 <xref:System.Windows.Data.ListCollectionView> 屬性描述如何排序資料項目的方式。</span><span class="sxs-lookup"><span data-stu-id="7a824-650">This is analogous to the way the identically named <xref:System.Windows.Data.ListCollectionView> properties describe how to sort the data items.</span></span>

<span data-ttu-id="7a824-651"><xref:System.Windows.Data.PropertyGroupDescription> 類別的兩個新靜態屬性，<xref:System.Windows.Data.PropertyGroupDescription.CompareNameAscending%2A> 和 <xref:System.Windows.Data.PropertyGroupDescription.CompareNameDescending%2A>，可用於大部分的案例。</span><span class="sxs-lookup"><span data-stu-id="7a824-651">Two new static properties of the <xref:System.Windows.Data.PropertyGroupDescription> class,  <xref:System.Windows.Data.PropertyGroupDescription.CompareNameAscending%2A> and <xref:System.Windows.Data.PropertyGroupDescription.CompareNameDescending%2A>, can be used for the most common cases.</span></span>

<span data-ttu-id="7a824-652">比方說，下列 XAML 會依年齡將資料分組、以遞增順序排序年齡群組，並依據姓氏將每個年齡群組內項目分組。</span><span class="sxs-lookup"><span data-stu-id="7a824-652">For example, the following XAML groups data by age, sort the age groups in ascending order, and group the items within each age group by last name.</span></span>

```xaml
<GroupDescriptions>
     <PropertyGroupDescription
         PropertyName="Age"
         CustomSort=
              "{x:Static PropertyGroupDescription.CompareNamesAscending}"/>
     </PropertyGroupDescription>
</GroupDescriptions>

<SortDescriptions>
     <SortDescription PropertyName="LastName"/>
</SortDescriptions>
```

<span data-ttu-id="7a824-653">**觸控鍵盤支援**</span><span class="sxs-lookup"><span data-stu-id="7a824-653">**Touch keyboard support**</span></span>

<span data-ttu-id="7a824-654">觸控鍵盤支援可讓 WPF 應用程式中的焦點追蹤，方法是在可接受文字輸入的控制項收到觸控輸入時，自動叫用並關閉 Windows 10 中的觸控鍵盤。</span><span class="sxs-lookup"><span data-stu-id="7a824-654">Touch keyboard support enables focus tracking in WPF applications by automatically invoking and dismissing the touch Keyboard in Windows 10 when the touch input is received by a control that can take textual input.</span></span>

<span data-ttu-id="7a824-655">在舊版 .NET Framework 中，WPF 應用程式無法加入宣告焦點追蹤，而不需要停用 WPF 畫筆/觸控手勢支援。</span><span class="sxs-lookup"><span data-stu-id="7a824-655">In previous versions of .NET Framework, WPF applications can't opt into the focus tracking without disabling WPF pen/touch gesture support.</span></span> <span data-ttu-id="7a824-656">如此一來，WPF 應用程式必須選擇完整 WPF 觸控支援，或是依賴 Windows 滑鼠升級。</span><span class="sxs-lookup"><span data-stu-id="7a824-656">As a result, WPF applications must choose between full WPF touch support or rely on Windows mouse promotion.</span></span>

<span data-ttu-id="7a824-657">**個別監視器 DPI**</span><span class="sxs-lookup"><span data-stu-id="7a824-657">**Per-monitor DPI**</span></span>

<span data-ttu-id="7a824-658">為了針對 WPF 應用程式支援最近激增的高 DPI 和混合式 DPI 環境，.NET Framework 4.6.2 啟用個別監視器感知。</span><span class="sxs-lookup"><span data-stu-id="7a824-658">To support the recent proliferation of high-DPI and hybrid-DPI environments for WPF apps, WPF in the .NET Framework 4.6.2 enables per-monitor awareness.</span></span> <span data-ttu-id="7a824-659">如需如何啟用 WPF 應用程式之個別監視器 DPI 感知功能的詳細資訊，請參閱 GitHub 上的[範例和開發人員指南](https://github.com/Microsoft/WPF-Samples/tree/master/PerMonitorDPI)。</span><span class="sxs-lookup"><span data-stu-id="7a824-659">See the [samples and developer guide](https://github.com/Microsoft/WPF-Samples/tree/master/PerMonitorDPI) on GitHub for more information about how to enable your WPF app to become per-monitor DPI aware.</span></span>

<span data-ttu-id="7a824-660">在舊版 .NET Framework 中，WPF 應用程式是系統 DPI 感知。</span><span class="sxs-lookup"><span data-stu-id="7a824-660">In previous versions of the .NET Framework, WPF apps are system-DPI aware.</span></span> <span data-ttu-id="7a824-661">換句話說，應用程式的 UI 會由作業系統進行適當的縮放，視應用程式呈現所在的監視器 DPI 而定。</span><span class="sxs-lookup"><span data-stu-id="7a824-661">In other words, the application's UI is scaled by the OS as appropriate, depending on the DPI of the monitor on which the app is rendered.</span></span>

<span data-ttu-id="7a824-662">針對在 .NET Framework 4.6.2 下執行的應用程式，您可以在 [\<runtime>](../configure-apps/file-schema/runtime/runtime-element.md) 應用程式佈建檔的區段中加入設定語句，以停用 WPF 應用程式中的個別監視器 DPI 變更，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7a824-662">For apps running under the .NET Framework 4.6.2, you can disable per-monitor DPI changes in WPF apps by adding a configuration statement to the [\<runtime>](../configure-apps/file-schema/runtime/runtime-element.md) section of your application configuration file, as follows:</span></span>

```xml
<runtime>
   <AppContextSwitchOverrides value="Switch.System.Windows.DoNotScaleForDpiChanges=false"/>
</runtime>
```

<a name="WF462"></a>

### <a name="windows-workflow-foundation-wf"></a><span data-ttu-id="7a824-663">Windows Workflow Foundation (WF)</span><span class="sxs-lookup"><span data-stu-id="7a824-663">Windows Workflow Foundation (WF)</span></span>

<span data-ttu-id="7a824-664">在 .NET Framework 4.6.2 中，Windows Workflow Foundation 已增強下列領域︰</span><span class="sxs-lookup"><span data-stu-id="7a824-664">In the .NET Framework 4.6.2, Windows Workflow Foundation has been enhanced in the following area:</span></span>

<span data-ttu-id="7a824-665">**重新裝載 WF 設計工具中的 c # 運算式和 IntelliSense 支援**</span><span class="sxs-lookup"><span data-stu-id="7a824-665">**Support for C# expressions and IntelliSense in the Rehosted WF Designer**</span></span>

<span data-ttu-id="7a824-666">從 .NET Framework 4.5 開始，WF 在 Visual Studio 設計工具和程式碼工作流程中都支援 c # 運算式。</span><span class="sxs-lookup"><span data-stu-id="7a824-666">Starting with .NET Framework 4.5, WF supports C# expressions in both the Visual Studio Designer and in code workflows.</span></span> <span data-ttu-id="7a824-667">重新裝載工作流程設計工具是 WF 的主要功能，可讓工作流程設計工具在 Visual Studio (的應用程式中，例如 WPF) 。</span><span class="sxs-lookup"><span data-stu-id="7a824-667">The Rehosted Workflow Designer is a key feature of WF that allows for the Workflow Designer to be in an application outside Visual Studio (for example, in WPF).</span></span>  <span data-ttu-id="7a824-668">Windows Workflow Foundation 提供在重新裝載工作流程設計工具中支援 c # 運算式和 IntelliSense 的功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-668">Windows Workflow Foundation provides the ability to support C# expressions and IntelliSense in the Rehosted Workflow Designer.</span></span> <span data-ttu-id="7a824-669">如需詳細資訊，請參閱 [Windows Workflow Foundation 部落格](/archive/blogs/workflowteam/building-c-expressions-support-and-intellisense-in-the-rehosted-workflow-designer)。</span><span class="sxs-lookup"><span data-stu-id="7a824-669">For more information, see the [Windows Workflow Foundation blog](/archive/blogs/workflowteam/building-c-expressions-support-and-intellisense-in-the-rehosted-workflow-designer).</span></span>

<span data-ttu-id="7a824-670">`Availability of IntelliSense when a customer rebuilds a workflow project from Visual Studio` 在4.6.2 之前的 .NET Framework 版本中，當客戶從 Visual Studio 重建工作流程專案時，WF 設計工具 IntelliSense 會中斷。</span><span class="sxs-lookup"><span data-stu-id="7a824-670">`Availability of IntelliSense when a customer rebuilds a workflow project from Visual Studio` In versions of the .NET Framework prior to 4.6.2, WF Designer IntelliSense is broken when a customer rebuilds a workflow project from Visual Studio.</span></span> <span data-ttu-id="7a824-671">雖然專案建置成功，但在設計工具中找不到工作流程類型，來自 IntelliSense 的遺漏工作流程類型警告也會出現在 [錯誤清單]\*\*\*\* 視窗中。</span><span class="sxs-lookup"><span data-stu-id="7a824-671">While the project build is successful, the workflow types are not found on the designer, and warnings from IntelliSense for the missing workflow types appear in the **Error List** window.</span></span> <span data-ttu-id="7a824-672">.NET Framework 4.6.2 可解決此問題，並讓 IntelliSense 可供使用。</span><span class="sxs-lookup"><span data-stu-id="7a824-672">.NET Framework 4.6.2 addresses this issue and makes IntelliSense available.</span></span>

<span data-ttu-id="7a824-673">**開啟工作流程追蹤的工作流程 V1 應用程式現在在 FIPS 模式下執行**</span><span class="sxs-lookup"><span data-stu-id="7a824-673">**Workflow V1 applications with Workflow Tracking on now run under FIPS-mode**</span></span>

<span data-ttu-id="7a824-674">啟用 FIPS 合規性模式的電腦，現在可以順利執行工作流程 V1 樣式的應用程式，並開啟工作流程追蹤。</span><span class="sxs-lookup"><span data-stu-id="7a824-674">Machines with FIPS Compliance Mode enabled can now successfully run a workflow Version 1-style application with Workflow tracking on.</span></span> <span data-ttu-id="7a824-675">若要啟用這種情況，您必須在 app.config 檔案中進行下列變更︰</span><span class="sxs-lookup"><span data-stu-id="7a824-675">To enable this scenario, you must make the following change to your app.config file:</span></span>

```xml
<add key="microsoft:WorkflowRuntime:FIPSRequired" value="true" />
```

<span data-ttu-id="7a824-676">如果未啟用這種情況，執行應用程式會繼續產生例外狀況，訊息為：「此實作不屬於 Windows Platform FIPS 已驗證密碼編譯演算法的一部分。」</span><span class="sxs-lookup"><span data-stu-id="7a824-676">If this scenario is not enabled, running the application continues to generate an exception with the message, "This implementation is not part of the Windows Platform FIPS validated cryptographic algorithms."</span></span>

<span data-ttu-id="7a824-677">**在 Visual Studio 工作流程設計工具中使用動態更新時的工作流程改進功能**</span><span class="sxs-lookup"><span data-stu-id="7a824-677">**Workflow Improvements when using Dynamic Update with Visual Studio Workflow Designer**</span></span>

<span data-ttu-id="7a824-678">工作流程設計工具、流程圖活動設計工具，以及其他工作流程活動設計工具，現在已順利載入和顯示在呼叫 <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.PrepareForUpdate%2A?displayProperty=nameWithType> 方法之後儲存的工作流程。</span><span class="sxs-lookup"><span data-stu-id="7a824-678">The Workflow Designer, FlowChart Activity Designer, and other Workflow Activity Designers now successfully load and display workflows that have been saved after calling  the <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.PrepareForUpdate%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="7a824-679">在 .NET Framework 4.6.2 之前的 .NET Framework 的版本中，在 Visual Studio 中，針對在呼叫 <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.PrepareForUpdate%2A?displayProperty=nameWithType> 之後儲存的工作流程載入 XAML 檔案，可能會導致下列問題︰</span><span class="sxs-lookup"><span data-stu-id="7a824-679">In versions of the .NET Framework before .NET Framework 4.6.2, loading a XAML file in Visual Studio for a workflow that has been saved after calling <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.PrepareForUpdate%2A?displayProperty=nameWithType> can result in the following issues:</span></span>

- <span data-ttu-id="7a824-680">工作流程設計工具無法正確載入 XAML 檔案 (當 <xref:System.Activities.Presentation.ViewState.ViewStateData.Id%2A?displayProperty=nameWithType> 在一行的結尾時)。</span><span class="sxs-lookup"><span data-stu-id="7a824-680">The Workflow Designer can't load the XAML file correctly (when the <xref:System.Activities.Presentation.ViewState.ViewStateData.Id%2A?displayProperty=nameWithType> is at the end of the line).</span></span>

- <span data-ttu-id="7a824-681">流程圖活動設計工具或其他工作流程活動設計工具可能會在預設位置顯示所有物件，而不是根據附加的屬性值。</span><span class="sxs-lookup"><span data-stu-id="7a824-681">Flowchart Activity Designer or other Workflow Activity Designers may display all objects in their default locations as opposed to attached property values.</span></span>

<a name="clickonce-1"></a>

### <a name="clickonce"></a><span data-ttu-id="7a824-682">ClickOnce</span><span class="sxs-lookup"><span data-stu-id="7a824-682">ClickOnce</span></span>

<span data-ttu-id="7a824-683">ClickOnce 已更新為除了已經支援的 TLS 1.0 通訊協定之外，還支援 TLS 1.1 和 TLS 1.2。</span><span class="sxs-lookup"><span data-stu-id="7a824-683">ClickOnce has been updated to support TLS 1.1 and TLS 1.2 in addition to the 1.0 protocol, which it already supports.</span></span> <span data-ttu-id="7a824-684">ClickOnce 會自動偵測需要哪個通訊協定。若要啟用 TLS 1.1 和 1.2 支援，並不需要在 ClickOnce 應用程式中執行額外的步驟。</span><span class="sxs-lookup"><span data-stu-id="7a824-684">ClickOnce automatically detects which protocol is required; no extra steps within the ClickOnce application are required to enable TLS 1.1 and 1.2 support.</span></span>

<a name="UWPConvert"></a>

### <a name="converting-windows-forms-and-wpf-apps-to--uwp-apps"></a><span data-ttu-id="7a824-685">將 Windows Forms 和 WPF 應用程式轉換成 UWP 應用程式</span><span class="sxs-lookup"><span data-stu-id="7a824-685">Converting Windows Forms and WPF apps to  UWP apps</span></span>

<span data-ttu-id="7a824-686">Windows 現在提供將現有 Windows 傳統型應用程式 (包括 WPF 和 Windows Forms 應用程式) 移植到通用 Windows 平台 (UWP) 的功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-686">Windows now offers capabilities to bring existing Windows desktop apps, including WPF and Windows Forms apps, to the Universal Windows Platform (UWP).</span></span> <span data-ttu-id="7a824-687">此技術可作為橋樑，讓您能逐漸將現有的程式碼基底移轉到 UWP，從而將您的應用程式帶到所有 Windows 10 裝置。</span><span class="sxs-lookup"><span data-stu-id="7a824-687">This technology acts as a bridge by enabling you to gradually migrate your existing code base to UWP, thereby bringing your app to all Windows 10 devices.</span></span>

<span data-ttu-id="7a824-688">轉換後的傳統型應用程式會取得類似於 UWP 應用程式的應用程式識別，如此便可存取 UWP API，以啟用例如動態磚和通知等功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-688">Converted desktop apps gain an app identity similar to the app identity of UWP apps, which makes UWP APIs accessible to enable features such as Live Tiles and notifications.</span></span> <span data-ttu-id="7a824-689">應用程式會繼續和之前一樣運作，而且會以完全信任應用程式的形式執行。</span><span class="sxs-lookup"><span data-stu-id="7a824-689">The app continues to behave as before and runs as a full trust app.</span></span> <span data-ttu-id="7a824-690">應用程式轉換後，應用程式容器處理序可以加入現有的完全信任處理序，以新增調適性使用者介面。</span><span class="sxs-lookup"><span data-stu-id="7a824-690">Once the app is converted, an app container process can be added to the existing full trust process to add an adaptive user interface.</span></span> <span data-ttu-id="7a824-691">當所有的功能都移至應用程式容器處理序時，便可以移除完全信任處理序，新的 UWP 應用程式也可以供所有 Windows 10 裝置使用。</span><span class="sxs-lookup"><span data-stu-id="7a824-691">When all functionality is moved to the app container process, the full trust process can be removed and the new UWP app can be made available to all Windows 10 devices.</span></span>

<a name="Debug462"></a>

### <a name="debugging-improvements"></a><span data-ttu-id="7a824-692">偵錯改進</span><span class="sxs-lookup"><span data-stu-id="7a824-692">Debugging improvements</span></span>

<span data-ttu-id="7a824-693">「受控偵錯 API」\*\* 在 .NET Framework 4.6.2 中已增強，可在擲回 <xref:System.NullReferenceException> 時執行額外的分析，因此可以判斷單行原始程式碼中哪個變數為 `null`。</span><span class="sxs-lookup"><span data-stu-id="7a824-693">The *unmanaged debugging API* has been enhanced in the .NET Framework 4.6.2 to perform additional analysis when a <xref:System.NullReferenceException> is thrown so that it is possible to determine which variable in a single line of source code is `null`.</span></span>   <span data-ttu-id="7a824-694">為了支援這種情況，下列 API 已加入 Unmanaged 偵錯 API。</span><span class="sxs-lookup"><span data-stu-id="7a824-694">To support this scenario, the following APIs have been added to the unmanaged debugging API.</span></span>

- <span data-ttu-id="7a824-695">[ICorDebugCode4](../unmanaged-api/debugging/icordebugcode4-interface.md)、[ICorDebugVariableHome](../unmanaged-api/debugging/icordebugvariablehome-interface.md) 和 [ICorDebugVariableHomeEnum](../unmanaged-api/debugging/icordebugvariablehomeenum-interface.md) 介面，它們會公開 Managed 變數的原生主資料夾。</span><span class="sxs-lookup"><span data-stu-id="7a824-695">The [ICorDebugCode4](../unmanaged-api/debugging/icordebugcode4-interface.md), [ICorDebugVariableHome](../unmanaged-api/debugging/icordebugvariablehome-interface.md), and [ICorDebugVariableHomeEnum](../unmanaged-api/debugging/icordebugvariablehomeenum-interface.md) interfaces, which expose the native homes of managed variables.</span></span> <span data-ttu-id="7a824-696">這可讓偵錯工具在 <xref:System.NullReferenceException> 發生時執行某些程式碼流程分析，以及回溯判斷對應至原生位置且為 `null` 的 Managed 變數。</span><span class="sxs-lookup"><span data-stu-id="7a824-696">This enables debuggers to do some code flow analysis when a  <xref:System.NullReferenceException> occurs and to work backwards to determine the managed variable that corresponds to the native location that was `null`.</span></span>

- <span data-ttu-id="7a824-697">[ICorDebugType2::GetTypeID](../unmanaged-api/debugging/icordebugtype2-gettypeid-method.md) 方法提供 ICorDebugType 到 [COR_TYPEID](../unmanaged-api/debugging/cor-typeid-structure.md) 的對應，可讓偵錯工具取得 [COR_TYPEID](../unmanaged-api/debugging/cor-typeid-structure.md)，而不需 ICorDebugType 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="7a824-697">The [ICorDebugType2::GetTypeID](../unmanaged-api/debugging/icordebugtype2-gettypeid-method.md) method provides a mapping for ICorDebugType to [COR_TYPEID](../unmanaged-api/debugging/cor-typeid-structure.md), which allows the debugger to obtain a [COR_TYPEID](../unmanaged-api/debugging/cor-typeid-structure.md) without an instance of the ICorDebugType.</span></span> <span data-ttu-id="7a824-698">[COR_TYPEID](../unmanaged-api/debugging/cor-typeid-structure.md) 上的現有 API 便可以用來判斷類型的類別配置。</span><span class="sxs-lookup"><span data-stu-id="7a824-698">Existing APIs on [COR_TYPEID](../unmanaged-api/debugging/cor-typeid-structure.md) can then be used to determine the class layout of the type.</span></span>

<a name="v461"></a>

## <a name="whats-new-in-net-framework-461"></a><span data-ttu-id="7a824-699">.NET Framework 4.6.1 中的新功能</span><span class="sxs-lookup"><span data-stu-id="7a824-699">What's new in .NET Framework 4.6.1</span></span>

<span data-ttu-id="7a824-700">.NET Framework 4.6.1 包含下列領域的新功能：</span><span class="sxs-lookup"><span data-stu-id="7a824-700">The .NET Framework 4.6.1 includes new features in the following areas:</span></span>

- [<span data-ttu-id="7a824-701">碼編譯</span><span class="sxs-lookup"><span data-stu-id="7a824-701">Cryptography</span></span>](#Crypto)

- [<span data-ttu-id="7a824-702">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="7a824-702">ADO.NET</span></span>](#ADO.NET461)

- [<span data-ttu-id="7a824-703">Windows Presentation Foundation (WPF)</span><span class="sxs-lookup"><span data-stu-id="7a824-703">Windows Presentation Foundation (WPF)</span></span>](#WPF461)

- [<span data-ttu-id="7a824-704">Windows Workflow Foundation</span><span class="sxs-lookup"><span data-stu-id="7a824-704">Windows Workflow Foundation</span></span>](#WWF461)

- [<span data-ttu-id="7a824-705">程式碼剖析</span><span class="sxs-lookup"><span data-stu-id="7a824-705">Profiling</span></span>](#Profile461)

- [<span data-ttu-id="7a824-706">NGen</span><span class="sxs-lookup"><span data-stu-id="7a824-706">NGen</span></span>](#NGEN461)

<span data-ttu-id="7a824-707">如需 .NET Framework 4.6.1 的詳細資訊，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="7a824-707">For more information on the .NET Framework 4.6.1, see the following topics:</span></span>

- [<span data-ttu-id="7a824-708">.NET Framework 4.6.1 變更清單</span><span class="sxs-lookup"><span data-stu-id="7a824-708">.NET Framework 4.6.1 list of changes</span></span>](https://github.com/Microsoft/dotnet/blob/master/releases/net461/dotnet461-changes.md)

- [<span data-ttu-id="7a824-709">4.6.1 中的應用程式相容性</span><span class="sxs-lookup"><span data-stu-id="7a824-709">Application Compatibility in 4.6.1</span></span>](../migration-guide/application-compatibility.md)

- <span data-ttu-id="7a824-710">[.NET Framework API diff](https://github.com/Microsoft/dotnet/blob/master/releases/net461/dotnet461-api-changes.md) (在 GitHub 上)</span><span class="sxs-lookup"><span data-stu-id="7a824-710">[.NET Framework API diff](https://github.com/Microsoft/dotnet/blob/master/releases/net461/dotnet461-api-changes.md) (on GitHub)</span></span>

<a name="Crypto"></a>

### <a name="cryptography-support-for-x509-certificates-containing-ecdsa"></a><span data-ttu-id="7a824-711">密碼編譯：支援包含 ECDSA 的 X509 憑證</span><span class="sxs-lookup"><span data-stu-id="7a824-711">Cryptography: Support for X509 certificates containing ECDSA</span></span>

<span data-ttu-id="7a824-712">.NET Framework 4.6 加入 X509 憑證的 RSACng 支援。</span><span class="sxs-lookup"><span data-stu-id="7a824-712">.NET Framework 4.6 added RSACng support for X509 certificates.</span></span> <span data-ttu-id="7a824-713">.NET Framework 4.6.1 加入 ECDSA (橢圓曲線數位簽章演算法) X509 憑證的支援。</span><span class="sxs-lookup"><span data-stu-id="7a824-713">The .NET Framework 4.6.1 adds support for ECDSA (Elliptic Curve Digital Signature Algorithm) X509 certificates.</span></span>

<span data-ttu-id="7a824-714">ECDSA 提供較佳的效能，其密碼編譯演算法比 RSA 更安全，為傳輸層安全性 (TLS) 的效能和延展性提供了絕佳的選擇。</span><span class="sxs-lookup"><span data-stu-id="7a824-714">ECDSA offers better performance and is a more secure cryptography algorithm than RSA, providing an excellent choice where Transport Layer Security (TLS) performance and scalability is a concern.</span></span> <span data-ttu-id="7a824-715">.NET Framework 實作會將呼叫包裝在現有的 Windows 功能中。</span><span class="sxs-lookup"><span data-stu-id="7a824-715">The .NET Framework implementation wraps calls into existing Windows functionality.</span></span>

<span data-ttu-id="7a824-716">下列範例程式碼示範使用 .NET Framework 4.6.1 包含的 ECDSA X509 憑證新支援，產生位元組資料流的簽章是多麼地輕鬆。</span><span class="sxs-lookup"><span data-stu-id="7a824-716">The following example code shows how easy it is to generate a signature for a byte stream by using the new  support for ECDSA  X509 certificates included in the .NET Framework 4.6.1.</span></span>

[!code-csharp[whatsnew.461.crypto#1](~/samples/snippets/csharp/VS_Snippets_CLR/whatsnew.461.crypto/cs/Code46.cs#1)]
[!code-vb[whatsnew.461.crypto#1](~/samples/snippets/visualbasic/VS_Snippets_CLR/whatsnew.461.crypto/vb/Code461.vb#1)]

<span data-ttu-id="7a824-717">這與在 .NET Framework 4.6 中用以產生簽章的程式碼形成鮮明的對比。</span><span class="sxs-lookup"><span data-stu-id="7a824-717">This offers a marked contrast to the code needed to generate a signature in .NET Framework 4.6.</span></span>

[!code-csharp[whatsnew.461.crypto#2](~/samples/snippets/csharp/VS_Snippets_CLR/whatsnew.461.crypto/cs/Code46.cs#2)]
[!code-vb[whatsnew.461.crypto#2](~/samples/snippets/visualbasic/VS_Snippets_CLR/whatsnew.461.crypto/vb/Code46.vb#2)]

<a name="ADO.NET461"></a>

### <a name="adonet"></a><span data-ttu-id="7a824-718">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="7a824-718">ADO.NET</span></span>

<span data-ttu-id="7a824-719">下列項目已加入 ADO.NET：</span><span class="sxs-lookup"><span data-stu-id="7a824-719">The following have been added to ADO.NET:</span></span>

<span data-ttu-id="7a824-720">**硬體保護金鑰的「一律加密」支援**</span><span class="sxs-lookup"><span data-stu-id="7a824-720">**Always Encrypted support for hardware protected keys**</span></span>

<span data-ttu-id="7a824-721">ADO.NET 現在支援在硬體安全模組 (HSM) 中以原生方式儲存 Always Encrypted 資料行主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="7a824-721">ADO.NET now supports storing Always Encrypted column master keys natively in Hardware Security Modules (HSMs).</span></span> <span data-ttu-id="7a824-722">透過此支援，客戶不需要撰寫自訂的資料行主要金鑰存放區提供者並向應用程式註冊，即可以使用儲存在 HSM 的非對稱金鑰。</span><span class="sxs-lookup"><span data-stu-id="7a824-722">With this support, customers can leverage asymmetric keys stored in HSMs without having to write custom column master key store providers and registering them in applications.</span></span>

<span data-ttu-id="7a824-723">客戶必須在應用程式伺服器或用戶端電腦上安裝 HSM 廠商提供的 CSP 提供者或 CNG 金鑰存放區提供者，才能存取受到儲存在 HSM 之資料行主要金鑰保護的 Always Encrypted 資料。</span><span class="sxs-lookup"><span data-stu-id="7a824-723">Customers need to install the HSM vendor-provided CSP provider or CNG key store providers on the app servers or client computers in order to access Always Encrypted data protected with column master keys stored in a HSM.</span></span>

<span data-ttu-id="7a824-724">**改進 <xref:System.Data.SqlClient.SqlConnectionStringBuilder.MultiSubnetFailover%2A> AlwaysOn 的連接行為**</span><span class="sxs-lookup"><span data-stu-id="7a824-724">**Improved <xref:System.Data.SqlClient.SqlConnectionStringBuilder.MultiSubnetFailover%2A> connection behavior for AlwaysOn**</span></span>

<span data-ttu-id="7a824-725">SqlClient 現在會自動提供更快的 AlwaysOn 可用性群組 (AG) 連線。</span><span class="sxs-lookup"><span data-stu-id="7a824-725">SqlClient now automatically provides faster connections to an AlwaysOn Availability Group (AG).</span></span> <span data-ttu-id="7a824-726">它會明確偵測應用程式是否連線到不同子網路上的 AlwaysOn 可用性群組 (AG)，並快速找到目前使用中的伺服器和提供伺服器連線。</span><span class="sxs-lookup"><span data-stu-id="7a824-726">It transparently detects whether your application is connecting to an AlwaysOn availability group (AG) on a different subnet and quickly discovers the current active server and provides a connection to the server.</span></span> <span data-ttu-id="7a824-727">在此版本之前，應用程式必須設定連接字串包含 `"MultisubnetFailover=true"`，以表示它要連線到 AlwaysOn 可用性群組。</span><span class="sxs-lookup"><span data-stu-id="7a824-727">Prior to this release, an application had to set the connection string to include `"MultisubnetFailover=true"` to indicate that it was connecting to an AlwaysOn Availability Group.</span></span> <span data-ttu-id="7a824-728">如果不在 `true` 設定連線關鍵字，應用程式可能會在連線到 AlwaysOn 可用性群組時發生逾時狀況。</span><span class="sxs-lookup"><span data-stu-id="7a824-728">Without setting the connection keyword to `true`, an application might experience a timeout while connecting to an AlwaysOn Availability Group.</span></span> <span data-ttu-id="7a824-729">使用此版本，應用程式就「不再」\*\* 需要將 <xref:System.Data.SqlClient.SqlConnectionStringBuilder.MultiSubnetFailover%2A> 設定為 `true`。</span><span class="sxs-lookup"><span data-stu-id="7a824-729">With this release, an application does *not* need to set <xref:System.Data.SqlClient.SqlConnectionStringBuilder.MultiSubnetFailover%2A> to `true` anymore.</span></span> <span data-ttu-id="7a824-730">如需 AlwaysOn 可用性群組的 SqlClient 支援詳細資訊，請參閱[高可用性、嚴重損壞修復的 SqlClient 支援](../data/adonet/sql/sqlclient-support-for-high-availability-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="7a824-730">For more information about SqlClient support for Always On Availability Groups, see [SqlClient Support for High Availability, Disaster Recovery](../data/adonet/sql/sqlclient-support-for-high-availability-disaster-recovery.md).</span></span>

<a name="WPF461"></a>

### <a name="windows-presentation-foundation-wpf"></a><span data-ttu-id="7a824-731">Windows Presentation Foundation (WPF)</span><span class="sxs-lookup"><span data-stu-id="7a824-731">Windows Presentation Foundation (WPF)</span></span>

<span data-ttu-id="7a824-732">Windows Presentation Foundation 包含數個改進和變更。</span><span class="sxs-lookup"><span data-stu-id="7a824-732">Windows Presentation Foundation includes a number of improvements and changes.</span></span>

<span data-ttu-id="7a824-733">**改善效能**</span><span class="sxs-lookup"><span data-stu-id="7a824-733">**Improved performance**</span></span>

<span data-ttu-id="7a824-734">.NET Framework 4.6.1 已修正引發觸控事件的延遲。</span><span class="sxs-lookup"><span data-stu-id="7a824-734">The delay in firing touch events has been fixed in the .NET Framework 4.6.1.</span></span> <span data-ttu-id="7a824-735">此外，<xref:System.Windows.Controls.RichTextBox> 控制項中的輸入也不會在快速輸入期間佔用呈現執行緒。</span><span class="sxs-lookup"><span data-stu-id="7a824-735">In addition, typing in a <xref:System.Windows.Controls.RichTextBox> control no longer ties up the render thread during fast input.</span></span>

<span data-ttu-id="7a824-736">**改善拼字檢查**</span><span class="sxs-lookup"><span data-stu-id="7a824-736">**Spell checking improvements**</span></span>

<span data-ttu-id="7a824-737">Windows 8.1 和更新版本已更新了 WPF 的拼字檢查程式，運用作業系統支援其他語言的拼字檢查。</span><span class="sxs-lookup"><span data-stu-id="7a824-737">The spell checker in WPF has been updated on Windows 8.1 and later versions to leverage operating system support for spell-checking additional languages.</span></span>  <span data-ttu-id="7a824-738">Windows 8.1 之前的 Windows 版本功能沒有任何變更。</span><span class="sxs-lookup"><span data-stu-id="7a824-738">There is no change in functionality on Windows versions prior to Windows 8.1.</span></span>

<span data-ttu-id="7a824-739">如同舊版的 .NET Framework，依下列順序尋找資訊會偵測到 <xref:System.Windows.Controls.TextBox> 控制項或 <xref:System.Windows.Controls.RichTextBox> 區塊的語言：</span><span class="sxs-lookup"><span data-stu-id="7a824-739">As in previous versions of the .NET Framework, the language for a <xref:System.Windows.Controls.TextBox> control ora <xref:System.Windows.Controls.RichTextBox> block is detected by looking for information in the following order:</span></span>

- <span data-ttu-id="7a824-740">`xml:lang` (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="7a824-740">`xml:lang`, if it is present.</span></span>

- <span data-ttu-id="7a824-741">目前的輸入語言。</span><span class="sxs-lookup"><span data-stu-id="7a824-741">Current input language.</span></span>

- <span data-ttu-id="7a824-742">目前的執行緒文化特性。</span><span class="sxs-lookup"><span data-stu-id="7a824-742">Current thread culture.</span></span>

<span data-ttu-id="7a824-743">如需有關 WPF 中語言支援的詳細資訊，請參閱 [.NET Framework 4.6.1 功能的 wpf blog 文章](https://devblogs.microsoft.com/wpf/wpf-in-net-4-6-1/)。</span><span class="sxs-lookup"><span data-stu-id="7a824-743">For more information on language support in WPF, see the [WPF blog post on .NET Framework 4.6.1 features](https://devblogs.microsoft.com/wpf/wpf-in-net-4-6-1/).</span></span>

<span data-ttu-id="7a824-744">**每個使用者自訂字典的額外支援**</span><span class="sxs-lookup"><span data-stu-id="7a824-744">**Additional support for per-user custom dictionaries**</span></span>

<span data-ttu-id="7a824-745">在 .NET Framework 4.6.1 中，WPF 能夠辨識已全域註冊的自訂字典。</span><span class="sxs-lookup"><span data-stu-id="7a824-745">In .NET Framework 4.6.1, WPF recognizes custom dictionaries that are registered globally.</span></span> <span data-ttu-id="7a824-746">這是除了依照每個控制項登錄它們之外的可用功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-746">This capability is available in addition to the ability to register them per-control.</span></span>

<span data-ttu-id="7a824-747">在舊版的 WPF 中，自訂的字典無法辨識 [已排除單字] 和 [自動校正] 清單。</span><span class="sxs-lookup"><span data-stu-id="7a824-747">In previous versions of WPF, custom dictionaries did not recognize Excluded Words and AutoCorrect lists.</span></span> <span data-ttu-id="7a824-748">Windows 8.1 和 Windows 10 透過可置於 `%AppData%\Microsoft\Spelling\<language tag>` 目錄之下使用的檔案支援它們。</span><span class="sxs-lookup"><span data-stu-id="7a824-748">They are supported on Windows 8.1 and Windows 10 through the use of files that can be placed under the `%AppData%\Microsoft\Spelling\<language tag>` directory.</span></span>  <span data-ttu-id="7a824-749">下列規則適用於這些檔案：</span><span class="sxs-lookup"><span data-stu-id="7a824-749">The following rules apply to these files:</span></span>

- <span data-ttu-id="7a824-750">檔案應有副檔名：.dic (用於加入的字詞)、.exc (用於排除的字詞) 或 .acl (用於自動校正)。</span><span class="sxs-lookup"><span data-stu-id="7a824-750">The files should have extensions of .dic (for added words), .exc (for excluded words), or .acl (for AutoCorrect).</span></span>

- <span data-ttu-id="7a824-751">檔案應為以位元組順序標記 (BOM) 開始的 UTF-16 LE 純文字。</span><span class="sxs-lookup"><span data-stu-id="7a824-751">The files should be UTF-16 LE plaintext that starts with the Byte Order Mark (BOM).</span></span>

- <span data-ttu-id="7a824-752">每一行的組成應為單字 (在新增和排除的字詞清單中)，或以分隔號 ("&#124;") 分隔的自動校正組合單字 (在 [自動校正] 單字清單中)。</span><span class="sxs-lookup"><span data-stu-id="7a824-752">Each line should consist of a word (in the added and excluded word lists), or an autocorrect pair with the words separated by a vertical bar ("&#124;") (in the AutoCorrect word list).</span></span>

- <span data-ttu-id="7a824-753">系統將這些檔案視為唯讀，而且不會加以修改。</span><span class="sxs-lookup"><span data-stu-id="7a824-753">These files are considered read-only and are not modified by the system.</span></span>

> [!NOTE]
> <span data-ttu-id="7a824-754">WPF 拼字檢查 API 不直接支援這些新的檔案格式，而應用程式中向 WPF 提供的自訂字典應該繼續使用 .lex 檔案。</span><span class="sxs-lookup"><span data-stu-id="7a824-754">These new file-formats are not directly supported by the WPF spell checking APIs, and the custom dictionaries supplied to WPF in applications should continue to use .lex files.</span></span>

<span data-ttu-id="7a824-755">**範例**</span><span class="sxs-lookup"><span data-stu-id="7a824-755">**Samples**</span></span>

<span data-ttu-id="7a824-756">[Microsoft/WPF-Samples](https://github.com/Microsoft/WPF-Samples) (Microsoft/WPF 範例) GitHub 存放庫上有數個 WPF 範例。</span><span class="sxs-lookup"><span data-stu-id="7a824-756">There are a number of WPF samples on the [Microsoft/WPF-Samples](https://github.com/Microsoft/WPF-Samples) GitHub repository.</span></span> <span data-ttu-id="7a824-757">您可以回傳意見調查表或提交 [GitHub 問題](https://github.com/Microsoft/WPF-Samples/issues)，以協助我們改進範例。</span><span class="sxs-lookup"><span data-stu-id="7a824-757">Help us improve our samples by sending us a pull-request or opening a [GitHub issue](https://github.com/Microsoft/WPF-Samples/issues).</span></span>

<span data-ttu-id="7a824-758">**DirectX 擴充功能**</span><span class="sxs-lookup"><span data-stu-id="7a824-758">**DirectX extensions**</span></span>

<span data-ttu-id="7a824-759">WPF 包含 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Wpf.Interop.DirectX-x86/)，提供新的 <xref:System.Windows.Interop.D3DImage> 實作，讓您輕鬆地與 DX10 和 Dx11 內容相互作用。</span><span class="sxs-lookup"><span data-stu-id="7a824-759">WPF includes a [NuGet package](https://www.nuget.org/packages/Microsoft.Wpf.Interop.DirectX-x86/) that provides new implementations of <xref:System.Windows.Interop.D3DImage> that make it easy for you to interoperate with DX10 and Dx11 content.</span></span> <span data-ttu-id="7a824-760">這個套件的程式碼為開放式原始碼，並可於 [GitHub](https://github.com/Microsoft/WPFDXInterop) 取得。</span><span class="sxs-lookup"><span data-stu-id="7a824-760">The code for this package has been open sourced and is available [on GitHub](https://github.com/Microsoft/WPFDXInterop).</span></span>

<a name="WWF461"></a>

### <a name="windows-workflow-foundation-transactions"></a><span data-ttu-id="7a824-761">Windows Workflow Foundation：交易</span><span class="sxs-lookup"><span data-stu-id="7a824-761">Windows Workflow Foundation: Transactions</span></span>

<span data-ttu-id="7a824-762"><xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A?displayProperty=nameWithType> 方法現在可以使用 MSDTC 以外的分散式交易管理員升級交易。</span><span class="sxs-lookup"><span data-stu-id="7a824-762">The <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A?displayProperty=nameWithType> method can now use a distributed transaction manager other than MSDTC to promote the transaction.</span></span> <span data-ttu-id="7a824-763">要想這麼做，請將 GUID 交易升級程式識別碼指定給新的 <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%28System.Transactions.IPromotableSinglePhaseNotification%2CSystem.Guid%29?displayProperty=nameWithType> 多載。</span><span class="sxs-lookup"><span data-stu-id="7a824-763">You do this by specifying a GUID transaction promoter identifier to the  new <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%28System.Transactions.IPromotableSinglePhaseNotification%2CSystem.Guid%29?displayProperty=nameWithType> overload .</span></span> <span data-ttu-id="7a824-764">如果此作業成功，交易的功能上就會加諸一些限制。</span><span class="sxs-lookup"><span data-stu-id="7a824-764">If this operation is successful, there are limitations placed on the capabilities of the transaction.</span></span> <span data-ttu-id="7a824-765">一旦登錄了非 MSDTC 的交易升級程式，下列方法就會擲回 <xref:System.Transactions.TransactionPromotionException>，因為這些方法需要升級至 MSDTC：</span><span class="sxs-lookup"><span data-stu-id="7a824-765">Once a non-MSDTC transaction promoter is enlisted, the following methods throw a <xref:System.Transactions.TransactionPromotionException> because these methods require promotion to MSDTC:</span></span>

- <xref:System.Transactions.Transaction.EnlistDurable%2A?displayProperty=nameWithType>

- <xref:System.Transactions.TransactionInterop.GetDtcTransaction%2A?displayProperty=nameWithType>

- <xref:System.Transactions.TransactionInterop.GetExportCookie%2A?displayProperty=nameWithType>

- <xref:System.Transactions.TransactionInterop.GetTransmitterPropagationToken%2A?displayProperty=nameWithType>

<span data-ttu-id="7a824-766">一旦登錄了非 MSDTC 的交易升級程式，即必須使用它定義的通訊協定，將它用於未來的永久性登錄。</span><span class="sxs-lookup"><span data-stu-id="7a824-766">Once a non-MSDTC transaction promoter is enlisted, it must be used for future durable enlistments by using protocols that it defines.</span></span> <span data-ttu-id="7a824-767">使用 <xref:System.Transactions.Transaction.PromoterType%2A> 屬性可取得交易升級程式的 <xref:System.Guid>。</span><span class="sxs-lookup"><span data-stu-id="7a824-767">The <xref:System.Guid> of the transaction promoter can be obtained by using the <xref:System.Transactions.Transaction.PromoterType%2A> property.</span></span> <span data-ttu-id="7a824-768">當交易升級時，交易升級程式會提供 <xref:System.Byte> 陣列，表示升級的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="7a824-768">When the transaction promotes, the transaction promoter provides a <xref:System.Byte> array that represents the promoted token.</span></span> <span data-ttu-id="7a824-769">應用程式可以 <xref:System.Transactions.Transaction.GetPromotedToken%2A> 方法取得非 MSDTC 已升級交易的已升級語彙基元。</span><span class="sxs-lookup"><span data-stu-id="7a824-769">An application can obtain the promoted token for a non-MSDTC promoted transaction with the <xref:System.Transactions.Transaction.GetPromotedToken%2A> method.</span></span>

<span data-ttu-id="7a824-770">新 <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%28System.Transactions.IPromotableSinglePhaseNotification%2CSystem.Guid%29?displayProperty=nameWithType> 多載的使用者必須遵循特定的呼叫序列，以便升級作業順利完成。</span><span class="sxs-lookup"><span data-stu-id="7a824-770">Users of the new <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%28System.Transactions.IPromotableSinglePhaseNotification%2CSystem.Guid%29?displayProperty=nameWithType> overload must follow a specific call sequence in order for the promotion operation to complete successfully.</span></span> <span data-ttu-id="7a824-771">這些規則都會記錄在於方法的文件中。</span><span class="sxs-lookup"><span data-stu-id="7a824-771">These rules are documented in the method's documentation.</span></span>

<a name="Profile461"></a>

### <a name="profiling"></a><span data-ttu-id="7a824-772">程式碼剖析</span><span class="sxs-lookup"><span data-stu-id="7a824-772">Profiling</span></span>

<span data-ttu-id="7a824-773">非受控分析 API 增強了下列功能：</span><span class="sxs-lookup"><span data-stu-id="7a824-773">The unmanaged profiling API has been enhanced as follows:</span></span>

- <span data-ttu-id="7a824-774">存取 [ICorProfilerInfo7](../unmanaged-api/profiling/icorprofilerinfo7-interface.md) 介面的 PDB 支援變得更好。</span><span class="sxs-lookup"><span data-stu-id="7a824-774">Better support for accessing PDBs in the [ICorProfilerInfo7](../unmanaged-api/profiling/icorprofilerinfo7-interface.md) interface.</span></span>

  <span data-ttu-id="7a824-775">在 ASP.NET Core 中，由 Roslyn 在記憶體中編譯組繹碼變得更為常見。</span><span class="sxs-lookup"><span data-stu-id="7a824-775">In ASP.NET Core, it is becoming much more common for assemblies to be compiled in-memory by Roslyn.</span></span> <span data-ttu-id="7a824-776">對於製作程式碼剖析工具的開發人員，這表示過去在磁碟上序列化的 PDB 可能不再存在。</span><span class="sxs-lookup"><span data-stu-id="7a824-776">For developers making profiling tools, this means that PDBs that historically were serialized on disk may no longer be present.</span></span> <span data-ttu-id="7a824-777">程式碼分析工具通常會使用 PDB 對應回工作原始程式行的程式碼，例如程式碼涵蓋範圍或逐行效能分析。</span><span class="sxs-lookup"><span data-stu-id="7a824-777">Profiler tools often use PDBs to map code back to source lines for tasks such as code coverage or line-by-line performance analysis.</span></span> <span data-ttu-id="7a824-778">[ICorProfilerInfo7](../unmanaged-api/profiling/icorprofilerinfo7-interface.md) 介面現在包含兩種新方法：[ICorProfilerInfo7::GetInMemorySymbolsLength](../unmanaged-api/profiling/icorprofilerinfo7-getinmemorysymbolslength-method.md) 和 [ICorProfilerInfo7::ReadInMemorySymbols](../unmanaged-api/profiling/icorprofilerinfo7-readinmemorysymbols.md)，讓這些分析工具能夠存取記憶體中的 PDB 資料。分析工具使用新的 API，即可取得記憶體內的 PDB 內容作為位元組陣列，然後予以處理或序列化至磁碟。</span><span class="sxs-lookup"><span data-stu-id="7a824-778">The [ICorProfilerInfo7](../unmanaged-api/profiling/icorprofilerinfo7-interface.md) interface now includes two new methods, [ICorProfilerInfo7::GetInMemorySymbolsLength](../unmanaged-api/profiling/icorprofilerinfo7-getinmemorysymbolslength-method.md) and [ICorProfilerInfo7::ReadInMemorySymbols](../unmanaged-api/profiling/icorprofilerinfo7-readinmemorysymbols.md), to provide these profiler tools with access to the in-memory PDB data, By using the new APIs, a profiler can obtain the contents of an in-memory PDB as a byte array and then process it or serialize it to disk.</span></span>

- <span data-ttu-id="7a824-779">ICorProfiler 介面的檢測設備變得更好。</span><span class="sxs-lookup"><span data-stu-id="7a824-779">Better instrumentation with the ICorProfiler interface.</span></span>

  <span data-ttu-id="7a824-780">使用 `ICorProfiler` API ReJit 功能進行動態檢測的分析工具，現在可以修改某些中繼資料。</span><span class="sxs-lookup"><span data-stu-id="7a824-780">Profilers that are using the `ICorProfiler` APIs ReJit functionality for dynamic instrumentation can now modify some metadata.</span></span> <span data-ttu-id="7a824-781">這類工具過去可以隨時檢測 IL，但只能在模組載入時修改中繼資料。</span><span class="sxs-lookup"><span data-stu-id="7a824-781">Previously such tools could instrument IL at any time, but metadata could only be modified at module load time.</span></span> <span data-ttu-id="7a824-782">因為 IL 參考中繼資料，這會限制能夠執行的檢測種類。</span><span class="sxs-lookup"><span data-stu-id="7a824-782">Because IL refers to metadata, this limited the kinds of instrumentation that could be done.</span></span> <span data-ttu-id="7a824-783">我們已藉由新增 [ICorProfilerInfo7：： ApplyMetaData](../unmanaged-api/profiling/icorprofilerinfo7-applymetadata-method.md) 方法來支援在載入模組之後編輯中繼資料的子集（特別是藉由加入新的、、、 `AssemblyRef` 、 `TypeRef` `TypeSpec` `MemberRef` `MemberSpec` 和 `UserString` 記錄），藉此提升部分限制。</span><span class="sxs-lookup"><span data-stu-id="7a824-783">We have lifted some of those limits by adding the [ICorProfilerInfo7::ApplyMetaData](../unmanaged-api/profiling/icorprofilerinfo7-applymetadata-method.md) method to support a subset of metadata edits after the module loads, in particular by adding new `AssemblyRef`, `TypeRef`, `TypeSpec`, `MemberRef`, `MemberSpec`, and `UserString` records.</span></span> <span data-ttu-id="7a824-784">此變更讓更大範圍的即時檢測變成可能。</span><span class="sxs-lookup"><span data-stu-id="7a824-784">This change makes a much broader range of on-the-fly instrumentation possible.</span></span>

<a name="NGEN461"></a>

### <a name="native-image-generator-ngen-pdbs"></a><span data-ttu-id="7a824-785">原生映像產生器 PDB</span><span class="sxs-lookup"><span data-stu-id="7a824-785">Native Image Generator (NGEN) PDBs</span></span>

<span data-ttu-id="7a824-786">跨電腦事件追蹤可讓客戶分析電腦 A 的程式，並使用電腦 B 上對應的原始程式查看程式碼剖析資料。使用舊版的 .NET Framework 時，使用者會將所有模組和原生映像從剖析的機器複製到包含 IL PDB 的分析機器，以建立來源與原生的對應。</span><span class="sxs-lookup"><span data-stu-id="7a824-786">Cross-machine event tracing allows customers to profile a program on Machine A and look at the profiling data with source line mapping on Machine B. Using previous versions of the .NET Framework, the user would copy all the modules and native images from the profiled machine to the analysis machine that contains the IL PDB to create the source-to-native mapping.</span></span> <span data-ttu-id="7a824-787">雖然這個程序能在檔案較小時運作良好 (例如手機應用程式)，但是桌上型系統的檔案可能非常巨大，而需要大量的複製時間。</span><span class="sxs-lookup"><span data-stu-id="7a824-787">While this process may work well when the files are relatively small, such as for phone applications, the files can be very large on desktop systems and require significant time to copy.</span></span>

<span data-ttu-id="7a824-788">使用 Ngen PDB，NGen 可以建立包含 IL 與原生對應的 PDB，不必依賴 IL PDB。</span><span class="sxs-lookup"><span data-stu-id="7a824-788">With Ngen PDBs, NGen can create a PDB that contains the IL-to-native mapping without a dependency on the IL PDB.</span></span> <span data-ttu-id="7a824-789">在我們的跨電腦事件追蹤案例中，您只需要將電腦 A 產生的原生映像 PDB 複製到電腦 B，並使用[偵錯介面存取 API](/visualstudio/debugger/debug-interface-access/debug-interface-access-sdk-reference)，讀取 IL PDB 的來源與 IL 對應及原生映像 PDB 的 IL 與原生對應。</span><span class="sxs-lookup"><span data-stu-id="7a824-789">In our cross-machine event tracing scenario, all that is needed is to copy the native image PDB that is generated by Machine A to Machine B and to use [Debug Interface Access APIs](/visualstudio/debugger/debug-interface-access/debug-interface-access-sdk-reference) to read the IL PDB's source-to-IL mapping and the native image PDB's IL-to-native mapping.</span></span> <span data-ttu-id="7a824-790">結合兩個對應可提供來源與原生對應。</span><span class="sxs-lookup"><span data-stu-id="7a824-790">Combining both mappings provides a source-to-native mapping.</span></span> <span data-ttu-id="7a824-791">由於原生映像 PDB 遠小於所有模組和原生映像，電腦 A 到電腦 B 的複製程序會更快。</span><span class="sxs-lookup"><span data-stu-id="7a824-791">Since the native image PDB is much smaller than all the modules and native images, the process of copying from Machine A to Machine B is much faster.</span></span>

<a name="v46"></a>

## <a name="whats-new-in-net-2015"></a><span data-ttu-id="7a824-792">.NET 2015 的新功能</span><span class="sxs-lookup"><span data-stu-id="7a824-792">What's new in .NET 2015</span></span>

<span data-ttu-id="7a824-793">.NET 2015 引進 Framework 4.6 和 .NET Core。</span><span class="sxs-lookup"><span data-stu-id="7a824-793">.NET 2015 introduces the .NET Framework 4.6 and .NET Core.</span></span> <span data-ttu-id="7a824-794">其中一些新功能適用於兩者，另一些功能則專屬於 .NET Framework 4.6 或 .NET Core。</span><span class="sxs-lookup"><span data-stu-id="7a824-794">Some new features apply to both, and other features are specific to .NET Framework 4.6 or .NET Core.</span></span>

- <span data-ttu-id="7a824-795">**ASP.NET Core**</span><span class="sxs-lookup"><span data-stu-id="7a824-795">**ASP.NET Core**</span></span>

  <span data-ttu-id="7a824-796">.NET 2015 包含 ASP.NET Core。這是一套精簡的 .NET 實作，可用於建置現代化雲端式應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a824-796">.NET 2015 includes ASP.NET Core, which is a lean .NET implementation for building modern cloud-based apps.</span></span> <span data-ttu-id="7a824-797">ASP.NET Core 已經過模組化，所以您只能依據您的應用程式需要加入這些功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-797">ASP.NET Core is modular so you can include only those features that are needed in your application.</span></span> <span data-ttu-id="7a824-798">這個平台可裝載於 IIS 上或自行裝載於自訂處理序中，而且您可以在同一部伺服器上執行具有不同 .NET Framework 版本的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a824-798">It can be hosted on IIS or self-hosted in a custom process, and you can run apps with different versions of the .NET Framework on the same server.</span></span> <span data-ttu-id="7a824-799">其中所包含的新環境組態系統是專為雲端部署所設計。</span><span class="sxs-lookup"><span data-stu-id="7a824-799">It includes a new environment configuration system that is designed for cloud deployment.</span></span>

  <span data-ttu-id="7a824-800">MVC、Web API 和網頁已整合成單一架構，稱為 MVC 6。</span><span class="sxs-lookup"><span data-stu-id="7a824-800">MVC, Web API, and Web Pages are unified into a single framework called MVC 6.</span></span> <span data-ttu-id="7a824-801">您可以使用 Visual Studio 2015 或更新版本中的工具建置 ASP.NET Core 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a824-801">You build ASP.NET Core apps through tools in Visual Studio 2015 or later.</span></span> <span data-ttu-id="7a824-802">您的現有應用程式將可在新的 .NET Framework 上運作；但若要建置使用 MVC 6 或 SignalR 3 的應用程式，必須使用 Visual Studio 2015 或更新版本中的專案系統。</span><span class="sxs-lookup"><span data-stu-id="7a824-802">Your existing applications will work on the new .NET Framework; however to build an app that uses MVC 6 or SignalR 3, you must use the project system in Visual Studio 2015 or later.</span></span>

  <span data-ttu-id="7a824-803">如需相關資訊，請參閱 [ASP.NET Core](/aspnet/core/)。</span><span class="sxs-lookup"><span data-stu-id="7a824-803">For information, see [ASP.NET Core](/aspnet/core/).</span></span>

- <span data-ttu-id="7a824-804">**ASP.NET 更新**</span><span class="sxs-lookup"><span data-stu-id="7a824-804">**ASP.NET Updates**</span></span>

  - <span data-ttu-id="7a824-805">**能執行非同步回應排清的工作型 API**</span><span class="sxs-lookup"><span data-stu-id="7a824-805">**Task-based API for Asynchronous Response Flushing**</span></span>

    <span data-ttu-id="7a824-806">ASP.NET 現在提供一個以工作為基礎的簡單 API 來進行非同步回應清除，亦即 <xref:System.Web.HttpResponse.FlushAsync%2A?displayProperty=nameWithType>，其可使用您語言的 `async/await` 支援來非同步清除回應。</span><span class="sxs-lookup"><span data-stu-id="7a824-806">ASP.NET now provides a simple task-based API for asynchronous response flushing, <xref:System.Web.HttpResponse.FlushAsync%2A?displayProperty=nameWithType>, that allows responses to be flushed asynchronously by using your language's `async/await` support.</span></span>

  - <span data-ttu-id="7a824-807">**模型繫結支援 task-returning 方法**</span><span class="sxs-lookup"><span data-stu-id="7a824-807">**Model binding supports task-returning methods**</span></span>

    <span data-ttu-id="7a824-808">在 .NET Framework 4.5 中，ASP.NET 加入「模型繫結」功能，可保障 Web Forms 頁面和使用者控制項中以 CRUD 為基礎之資料作業方式的可延伸性並以程式碼為重心。</span><span class="sxs-lookup"><span data-stu-id="7a824-808">In the .NET Framework 4.5, ASP.NET added the Model Binding feature that enabled an extensible, code-focused approach to CRUD-based data operations in Web Forms pages and user controls.</span></span> <span data-ttu-id="7a824-809">模型繫結系統現在支援由 <xref:System.Threading.Tasks.Task>傳回的模型繫結方法。</span><span class="sxs-lookup"><span data-stu-id="7a824-809">The Model Binding system now supports <xref:System.Threading.Tasks.Task>-returning model binding methods.</span></span> <span data-ttu-id="7a824-810">此功能可讓 Web Forms 開發人員在使用包括 Entity Framework 的較新版 ORM 時，透過簡單的資料繫結系統獲得非同步延展性的優勢。</span><span class="sxs-lookup"><span data-stu-id="7a824-810">This feature allows Web Forms developers to get the scalability benefits of async with the ease of the data-binding system when using newer versions of ORMs, including the Entity Framework.</span></span>

    <span data-ttu-id="7a824-811">非同步模型繫結是由 `aspnet:EnableAsyncModelBinding` 組態設定所控制。</span><span class="sxs-lookup"><span data-stu-id="7a824-811">Async model binding is controlled by the `aspnet:EnableAsyncModelBinding` configuration setting.</span></span>

    ```xml
    <appSettings>
        <add key=" aspnet:EnableAsyncModelBinding" value="true|false" />
    </appSettings>
    ```

    <span data-ttu-id="7a824-812">對於目標為 .NET Framework 4.6 的應用程式，它會預設為 `true`。</span><span class="sxs-lookup"><span data-stu-id="7a824-812">On apps the target the .NET Framework 4.6, it defaults to `true`.</span></span> <span data-ttu-id="7a824-813">對於目標為舊版 .NET Framework 但在 .NET Framework 4.6 上執行的應用程式，則預設為 `false`。</span><span class="sxs-lookup"><span data-stu-id="7a824-813">On apps running on the .NET Framework 4.6 that target an earlier version of the .NET Framework, it is `false` by default.</span></span> <span data-ttu-id="7a824-814">您可將組態設定設為 `true` 以將其啟用。</span><span class="sxs-lookup"><span data-stu-id="7a824-814">It can be enabled by setting the configuration setting to `true`.</span></span>

  - <span data-ttu-id="7a824-815">**HTTP/2 支援 (Windows 10)**</span><span class="sxs-lookup"><span data-stu-id="7a824-815">**HTTP/2 Support (Windows 10)**</span></span>

    <span data-ttu-id="7a824-816">[HTTP/2](https://www.wikipedia.org/wiki/HTTP/2) 是新版的 HTTP 通訊協定，可大幅改善連線的使用情況 (用戶端和伺服器之間較少往返)，並降低使用者網頁載入的延遲情形。</span><span class="sxs-lookup"><span data-stu-id="7a824-816">[HTTP/2](https://www.wikipedia.org/wiki/HTTP/2) is a new version of the HTTP protocol that provides much better connection utilization (fewer round-trips between client and server), resulting in lower latency web page loading for users.</span></span>  <span data-ttu-id="7a824-817">網頁 (與服務相反) 從 HTTP/2 獲益最明顯，因為通訊協定會針對做為單一體驗之一部分之要求的多個成品進行最佳化。</span><span class="sxs-lookup"><span data-stu-id="7a824-817">Web pages (as opposed to services) benefit the most from HTTP/2, since the protocol optimizes for multiple artifacts being requested as part of a single experience.</span></span> <span data-ttu-id="7a824-818">在 .NET Framework 4.6 中，HTTP/2 支援已加入 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="7a824-818">HTTP/2 support has been added to ASP.NET in .NET Framework 4.6.</span></span> <span data-ttu-id="7a824-819">由於網路功能存在於多個層，因此 Windows、IIS 和 ASP.NET中需要新功能以啟用 HTTP/2。</span><span class="sxs-lookup"><span data-stu-id="7a824-819">Because networking functionality exists at multiple layers, new features were required in Windows, in IIS, and in ASP.NET to enable HTTP/2.</span></span> <span data-ttu-id="7a824-820">您必須在 Windows 10 上執行才能搭配 ASP.NET 使用 HTTP/2。</span><span class="sxs-lookup"><span data-stu-id="7a824-820">You must be running on Windows 10 to use HTTP/2 with ASP.NET.</span></span>

    <span data-ttu-id="7a824-821">HTTP/2 也支援使用 <xref:System.Net.Http.HttpClient?displayProperty=nameWithType> API 的 Windows 10 通用平台 (UWP) 應用程式，並預設為啟用。</span><span class="sxs-lookup"><span data-stu-id="7a824-821">HTTP/2 is also supported and on by default for Windows 10 Universal Windows Platform (UWP) apps that use the <xref:System.Net.Http.HttpClient?displayProperty=nameWithType> API.</span></span>

    <span data-ttu-id="7a824-822">為了提供一個在 ASP.NET 應用程式中使用 [PUSH_PROMISE](https://httpwg.github.io/http2-spec/#PUSH_PROMISE) 功能的方式，已將含有 <xref:System.Web.HttpResponse.PushPromise%28System.String%29> 和 <xref:System.Web.HttpResponse.PushPromise%28System.String%2CSystem.String%2CSystem.Collections.Specialized.NameValueCollection%29> 這兩個多載的新方法新增到 <xref:System.Web.HttpResponse> 類別。</span><span class="sxs-lookup"><span data-stu-id="7a824-822">In order to provide a way to use the [PUSH_PROMISE](https://httpwg.github.io/http2-spec/#PUSH_PROMISE) feature in ASP.NET applications, a new method with two overloads, <xref:System.Web.HttpResponse.PushPromise%28System.String%29> and <xref:System.Web.HttpResponse.PushPromise%28System.String%2CSystem.String%2CSystem.Collections.Specialized.NameValueCollection%29>, has been added to the <xref:System.Web.HttpResponse> class.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7a824-823">ASP.NET Core 支援 HTTP/2，但尚未新增 PUSH PROMISE 功能的支援。</span><span class="sxs-lookup"><span data-stu-id="7a824-823">While ASP.NET Core supports HTTP/2, support for the PUSH PROMISE feature has not yet been added.</span></span>

    <span data-ttu-id="7a824-824">瀏覽器和網頁伺服器 (Windows 上的 IIS) 會執行所有工作。</span><span class="sxs-lookup"><span data-stu-id="7a824-824">The browser and the web server (IIS on Windows) do all the work.</span></span> <span data-ttu-id="7a824-825">您不需要為使用者進行任何繁重工作。</span><span class="sxs-lookup"><span data-stu-id="7a824-825">You don't have to do any heavy-lifting for your users.</span></span>

    <span data-ttu-id="7a824-826">大部分的[主要瀏覽器都支援 HTTP/2](https://www.wikipedia.org/wiki/HTTP/2)，因此如果您的伺服器也支援 HTTP/2，使用者便很可能獲得其中的益處。</span><span class="sxs-lookup"><span data-stu-id="7a824-826">Most of the [major browsers support HTTP/2](https://www.wikipedia.org/wiki/HTTP/2), so it's likely that your users will benefit from HTTP/2 support if your server supports it.</span></span>

  - <span data-ttu-id="7a824-827">**對權杖繫結通訊協定的支援**</span><span class="sxs-lookup"><span data-stu-id="7a824-827">**Support for the Token Binding Protocol**</span></span>

    <span data-ttu-id="7a824-828">Microsoft 與 Google 合作推出了驗證的新方法，稱為[權杖繫結通訊協定](https://github.com/TokenBinding/Internet-Drafts)。</span><span class="sxs-lookup"><span data-stu-id="7a824-828">Microsoft and Google have been collaborating on a new approach to authentication, called the [Token Binding Protocol](https://github.com/TokenBinding/Internet-Drafts).</span></span> <span data-ttu-id="7a824-829">前提是，您的流覽) 器快取中 (的驗證權杖，可能會被罪犯遭竊並用來存取安全的資源 (例如，您的銀行帳戶) 不需要您的密碼或任何其他特殊許可權的知識。</span><span class="sxs-lookup"><span data-stu-id="7a824-829">The premise is that authentication tokens (in your browser cache) can be stolen and used by criminals to access otherwise secure resources (for example, your bank account) without requiring your password or any other privileged knowledge.</span></span> <span data-ttu-id="7a824-830">新的通訊協定旨在減輕這個問題。</span><span class="sxs-lookup"><span data-stu-id="7a824-830">The new protocol aims to mitigate this problem.</span></span>

    <span data-ttu-id="7a824-831">權杖繫結通訊協定將在 Windows 10 中實作為瀏覽器功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-831">The Token Binding Protocol will be implemented in Windows 10 as a browser feature.</span></span> <span data-ttu-id="7a824-832">ASP.NET 應用程式將會參與通訊協定，以便驗證權杖能驗證為合法。</span><span class="sxs-lookup"><span data-stu-id="7a824-832">ASP.NET apps will participate in the protocol, so that authentication tokens are validated to be legitimate.</span></span> <span data-ttu-id="7a824-833">用戶端和伺服器實作會建立通訊協定所指定的端對端保護。</span><span class="sxs-lookup"><span data-stu-id="7a824-833">The client and the server implementations establish the end-to-end protection specified by the protocol.</span></span>

  - <span data-ttu-id="7a824-834">**隨機字串雜湊演算法**</span><span class="sxs-lookup"><span data-stu-id="7a824-834">**Randomized string hash algorithms**</span></span>

    <span data-ttu-id="7a824-835">.NET Framework 4.5 引進了[隨機字串雜湊演算法](../configure-apps/file-schema/runtime/userandomizedstringhashalgorithm-element.md)。</span><span class="sxs-lookup"><span data-stu-id="7a824-835">.NET Framework 4.5 introduced a [randomized string hash algorithm](../configure-apps/file-schema/runtime/userandomizedstringhashalgorithm-element.md).</span></span> <span data-ttu-id="7a824-836">不過，由於部分 ASP.NET 功能相依於穩定的雜湊程式碼，因此 ASP.NET 並不支援此演算法。</span><span class="sxs-lookup"><span data-stu-id="7a824-836">However, it was not supported by ASP.NET because of some ASP.NET features depended on a stable hash code.</span></span> <span data-ttu-id="7a824-837">在 .NET Framework 4.6 中，現已支援隨機字串雜湊演算法。</span><span class="sxs-lookup"><span data-stu-id="7a824-837">In .NET Framework 4.6, randomized string hash algorithms are now supported.</span></span> <span data-ttu-id="7a824-838">若要啟用此功能，請使用 `aspnet:UseRandomizedStringHashAlgorithm` 組態設定。</span><span class="sxs-lookup"><span data-stu-id="7a824-838">To enable this feature, use the `aspnet:UseRandomizedStringHashAlgorithm` config setting.</span></span>

    ```xml
    <appSettings>
        <add key="aspnet:UseRandomizedStringHashAlgorithm" value="true|false" />
    </appSettings>
    ```

- <span data-ttu-id="7a824-839">**ADO.NET**</span><span class="sxs-lookup"><span data-stu-id="7a824-839">**ADO.NET**</span></span>

  <span data-ttu-id="7a824-840">ADO.NET 現在支援 SQL Server 2016 Community Technology Preview 2 (CTP2) 提供的 Always Encrypted 功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-840">ADO .NET now supports the Always Encrypted feature available in SQL Server 2016 Community Technology Preview 2 (CTP2).</span></span> <span data-ttu-id="7a824-841">使用 Always Encrypted 時，SQL Server 可以對加密的資料執行作業，而且所有加密金鑰都與應用程式位於客戶信任的環境中，而不是在伺服器上。</span><span class="sxs-lookup"><span data-stu-id="7a824-841">With Always Encrypted, SQL Server can perform operations on encrypted data, and best of all the encryption key resides with the application inside the customer's trusted environment and not on the server.</span></span> <span data-ttu-id="7a824-842">永遠加密可保護客戶資料，所以 DBA 無法存取純文字資料。</span><span class="sxs-lookup"><span data-stu-id="7a824-842">Always Encrypted secures customer data so DBAs do not have access to plain text data.</span></span> <span data-ttu-id="7a824-843">資料的加密和解密透明地在驅動程式層級進行，以將變更現有應用程式的需求降到最少。</span><span class="sxs-lookup"><span data-stu-id="7a824-843">Encryption and decryption of data happens transparently at the driver level, minimizing changes that have to be made to existing applications.</span></span> <span data-ttu-id="7a824-844">如需詳細資訊，請參閱 [Always Encrypted (資料庫引擎)](/sql/relational-databases/security/encryption/always-encrypted-database-engine) 和 [Always Encrypted (用戶端開發)](/sql/relational-databases/security/encryption/always-encrypted-client-development)。</span><span class="sxs-lookup"><span data-stu-id="7a824-844">For details, see [Always Encrypted (Database Engine)](/sql/relational-databases/security/encryption/always-encrypted-database-engine) and [Always Encrypted (client development)](/sql/relational-databases/security/encryption/always-encrypted-client-development).</span></span>

- <span data-ttu-id="7a824-845">**Managed 程式碼的 64 位元 JIT 編譯器**</span><span class="sxs-lookup"><span data-stu-id="7a824-845">**64-bit JIT Compiler for managed code**</span></span>

  <span data-ttu-id="7a824-846">.NET Framework 4.6 提供 64 位元 JIT 編譯器的新版本 (原本的代號是 RyuJIT)。</span><span class="sxs-lookup"><span data-stu-id="7a824-846">.NET Framework 4.6 features a new version of the 64-bit JIT compiler (originally code-named RyuJIT).</span></span> <span data-ttu-id="7a824-847">全新的 64 位元編譯器比舊版 64 位元 JIT 編譯器更大幅提升效能。</span><span class="sxs-lookup"><span data-stu-id="7a824-847">The new 64-bit compiler provides significant performance improvements over the older 64-bit JIT compiler.</span></span> <span data-ttu-id="7a824-848">在 .NET Framework 4.6 之上執行的 64 位元處理序即會啟用全新的 64 位元編譯器。</span><span class="sxs-lookup"><span data-stu-id="7a824-848">The new 64-bit compiler is enabled for 64-bit processes running on top of .NET Framework 4.6.</span></span> <span data-ttu-id="7a824-849">若您的應用程式是編譯為 64 位元或 AnyCPU 並在 64 位元作業系統上執行，則會以 64 位元處理序執行。</span><span class="sxs-lookup"><span data-stu-id="7a824-849">Your app will run in a 64-bit process if it is compiled as 64-bit or AnyCPU and is running on a 64-bit operating system.</span></span> <span data-ttu-id="7a824-850">雖然我們已盡量讓新編譯器的轉換透明化，但仍可能會有行為上的變更。</span><span class="sxs-lookup"><span data-stu-id="7a824-850">While care has been taken to make the transition to the new compiler as transparent as possible, changes in behavior are possible.</span></span>

  <span data-ttu-id="7a824-851">新的 64 位元 JIT 編譯器也包含硬體 SIMD 加速功能，在與 <xref:System.Numerics> 命名空間中支援 SIMD 的類型結合時，可產生良好的效能改進。</span><span class="sxs-lookup"><span data-stu-id="7a824-851">The new 64-bit JIT compiler also includes hardware SIMD acceleration features when coupled with SIMD-enabled types in the <xref:System.Numerics> namespace, which can yield good performance improvements.</span></span>

- <span data-ttu-id="7a824-852">**組件載入器改進**</span><span class="sxs-lookup"><span data-stu-id="7a824-852">**Assembly loader improvements**</span></span>

  <span data-ttu-id="7a824-853">現在，組件載入器會在載入對應的 NGEN 映像之後即卸載 IL 組件，因此可以更有效率地使用記憶體。</span><span class="sxs-lookup"><span data-stu-id="7a824-853">The assembly loader now uses memory more efficiently by unloading IL assemblies after a corresponding NGEN image is loaded.</span></span> <span data-ttu-id="7a824-854">此變更會減少虛擬記憶體，這對大型的 32 位元應用程式 (例如 Visual Studio) 特別有幫助，也可節省實體記憶體。</span><span class="sxs-lookup"><span data-stu-id="7a824-854">This change decreases virtual memory, which is particularly beneficial for large 32-bit apps (such as Visual Studio), and also saves physical memory.</span></span>

- <span data-ttu-id="7a824-855">**基底類別庫變更**</span><span class="sxs-lookup"><span data-stu-id="7a824-855">**Base class library changes**</span></span>

  <span data-ttu-id="7a824-856">.NET Framework 4.6 已新增許多新的 API，以便能在重要情節中使用。</span><span class="sxs-lookup"><span data-stu-id="7a824-856">Many new APIs have been added around to .NET Framework 4.6 to enable key scenarios.</span></span> <span data-ttu-id="7a824-857">其中包括下列變更和新功能：</span><span class="sxs-lookup"><span data-stu-id="7a824-857">These include the following changes and additions:</span></span>

  - <span data-ttu-id="7a824-858">**IReadOnlyCollection 的 \<T> 實施**</span><span class="sxs-lookup"><span data-stu-id="7a824-858">**IReadOnlyCollection\<T> implementations**</span></span>

    <span data-ttu-id="7a824-859">額外的集合會實作 <xref:System.Collections.Generic.IReadOnlyCollection%601>，例如 <xref:System.Collections.Generic.Queue%601> 和 <xref:System.Collections.Generic.Stack%601>。</span><span class="sxs-lookup"><span data-stu-id="7a824-859">Additional collections implement <xref:System.Collections.Generic.IReadOnlyCollection%601> such as <xref:System.Collections.Generic.Queue%601> and <xref:System.Collections.Generic.Stack%601>.</span></span>

  - <span data-ttu-id="7a824-860">**CultureInfo.CurrentCulture 與 CultureInfo.CurrentUICulture**</span><span class="sxs-lookup"><span data-stu-id="7a824-860">**CultureInfo.CurrentCulture and CultureInfo.CurrentUICulture**</span></span>

    <span data-ttu-id="7a824-861"><xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType> 和 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=nameWithType> 屬性現在是讀寫，而不是唯讀。</span><span class="sxs-lookup"><span data-stu-id="7a824-861">The <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType> and <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=nameWithType> properties are now read-write rather than read-only.</span></span> <span data-ttu-id="7a824-862">如果您將新的 <xref:System.Globalization.CultureInfo> 物件指派給這些屬性，`Thread.CurrentThread.CurrentCulture` 屬性所定義的目前執行緒文化特性和 `Thread.CurrentThread.CurrentUICulture` 屬性所定義的目前 UI 執行緒文化特性也會隨著變更。</span><span class="sxs-lookup"><span data-stu-id="7a824-862">If you assign a new <xref:System.Globalization.CultureInfo> object to these properties, the current thread culture defined by the `Thread.CurrentThread.CurrentCulture` property and the current UI thread culture defined by the `Thread.CurrentThread.CurrentUICulture` properties also change.</span></span>

  - <span data-ttu-id="7a824-863">**記憶體回收 (GC) 的增強功能**</span><span class="sxs-lookup"><span data-stu-id="7a824-863">**Enhancements to garbage collection (GC)**</span></span>

    <span data-ttu-id="7a824-864"><xref:System.GC> 類別現在包含 <xref:System.GC.TryStartNoGCRegion%2A> 和 <xref:System.GC.EndNoGCRegion%2A> 方法，可讓您在執行關鍵路徑期間不允許記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="7a824-864">The <xref:System.GC> class now includes <xref:System.GC.TryStartNoGCRegion%2A> and <xref:System.GC.EndNoGCRegion%2A> methods that allow you to disallow garbage collection during the execution of a critical path.</span></span>

    <span data-ttu-id="7a824-865"><xref:System.GC.Collect%28System.Int32%2CSystem.GCCollectionMode%2CSystem.Boolean%2CSystem.Boolean%29?displayProperty=nameWithType> 方法的新多載可讓您控制是否要對小型物件堆積和大型物件堆積進行清理和壓縮，還是只要進行清理。</span><span class="sxs-lookup"><span data-stu-id="7a824-865">A new overload of the <xref:System.GC.Collect%28System.Int32%2CSystem.GCCollectionMode%2CSystem.Boolean%2CSystem.Boolean%29?displayProperty=nameWithType> method allows you to control whether both the small object heap and the large object heap are swept and compacted or swept only.</span></span>

  - <span data-ttu-id="7a824-866">**啟用 SIMD 的類型**</span><span class="sxs-lookup"><span data-stu-id="7a824-866">**SIMD-enabled types**</span></span>

    <span data-ttu-id="7a824-867"><xref:System.Numerics> 命名空間現在包含數種支援 SIMD 的類型，例如 <xref:System.Numerics.Matrix3x2>、<xref:System.Numerics.Matrix4x4>、<xref:System.Numerics.Plane>、<xref:System.Numerics.Quaternion>、<xref:System.Numerics.Vector2>、<xref:System.Numerics.Vector3> 和 <xref:System.Numerics.Vector4>。</span><span class="sxs-lookup"><span data-stu-id="7a824-867">The <xref:System.Numerics> namespace now includes a number of SIMD-enabled types, such as <xref:System.Numerics.Matrix3x2>, <xref:System.Numerics.Matrix4x4>, <xref:System.Numerics.Plane>, <xref:System.Numerics.Quaternion>, <xref:System.Numerics.Vector2>, <xref:System.Numerics.Vector3>, and <xref:System.Numerics.Vector4>.</span></span>

    <span data-ttu-id="7a824-868">因為新的 64 位元 JIT 編譯器也包含硬體 SIMD 加速功能，所以在搭配支援 SIMD 的類型與新的 64 位元 JIT 編譯器時有特別顯著的效能改進。</span><span class="sxs-lookup"><span data-stu-id="7a824-868">Because the new 64-bit JIT compiler also includes hardware SIMD acceleration features, there are especially significant performance improvements when using the SIMD-enabled types with the new 64-bit JIT compiler.</span></span>

  - <span data-ttu-id="7a824-869">**加密更新**</span><span class="sxs-lookup"><span data-stu-id="7a824-869">**Cryptography updates**</span></span>

    <span data-ttu-id="7a824-870">目前正在更新 <xref:System.Security.Cryptography?displayProperty=nameWithType> API 以支援 [Windows CNG 密碼編譯 API](/windows/desktop/SecCNG/cng-reference)。</span><span class="sxs-lookup"><span data-stu-id="7a824-870">The <xref:System.Security.Cryptography?displayProperty=nameWithType> API is being updated to support the [Windows CNG cryptography APIs](/windows/desktop/SecCNG/cng-reference).</span></span> <span data-ttu-id="7a824-871">舊版 .NET Framework 完全倚賴[舊版的 Windows 密碼編譯 API](/windows/desktop/SecCrypto/cryptography-portal)作為 <xref:System.Security.Cryptography?displayProperty=nameWithType> 實作的基礎。</span><span class="sxs-lookup"><span data-stu-id="7a824-871">Previous versions of the .NET Framework have relied entirely on an [earlier version of the Windows Cryptography APIs](/windows/desktop/SecCrypto/cryptography-portal) as the basis for the <xref:System.Security.Cryptography?displayProperty=nameWithType> implementation.</span></span> <span data-ttu-id="7a824-872">我們已經要求支援 CNG API，因為它支援[現代的加密演算法](/windows/desktop/SecCNG/cng-features#suite-b-support)，這些演算法對特定類別的應用程式來說非常重要。</span><span class="sxs-lookup"><span data-stu-id="7a824-872">We have had requests to support the CNG API, since it supports [modern cryptography algorithms](/windows/desktop/SecCNG/cng-features#suite-b-support), which are important for certain categories of apps.</span></span>

    <span data-ttu-id="7a824-873">.NET Framework 4.6 包含下列新的增強功能，可支援 Windows CNG 密碼編譯 API：</span><span class="sxs-lookup"><span data-stu-id="7a824-873">.NET Framework 4.6 includes the following new enhancements to support the Windows CNG cryptography APIs:</span></span>

    - <span data-ttu-id="7a824-874">一組適用於 `System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPublicKey(System.Security.Cryptography.X509Certificates.X509Certificate2)` 和 `System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPrivateKey(System.Security.Cryptography.X509Certificates.X509Certificate2)` X509 憑證的擴充方法，其會在可能時傳回以 CNG 為基礎的實作，而不是以 CAPI 為基礎的實作</span><span class="sxs-lookup"><span data-stu-id="7a824-874">A set of extension methods for X509 Certificates, `System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPublicKey(System.Security.Cryptography.X509Certificates.X509Certificate2)` and `System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPrivateKey(System.Security.Cryptography.X509Certificates.X509Certificate2)`, that return a CNG-based implementation rather than a CAPI-based implementation when possible.</span></span> <span data-ttu-id="7a824-875">(有些智慧卡仍需要 CAPI，因此 API 可處理這類後援。)</span><span class="sxs-lookup"><span data-stu-id="7a824-875">(Some smartcards, etc., still require CAPI, and the APIs handle the fallback).</span></span>

    - <span data-ttu-id="7a824-876"><xref:System.Security.Cryptography.RSACng?displayProperty=nameWithType> 類別，可提供的 RSA 演算法的 CNG 實作。</span><span class="sxs-lookup"><span data-stu-id="7a824-876">The <xref:System.Security.Cryptography.RSACng?displayProperty=nameWithType> class, which provides a CNG implementation of the RSA algorithm.</span></span>

    - <span data-ttu-id="7a824-877">RSA API 的增強功能，可讓一般動作不再需要轉型。</span><span class="sxs-lookup"><span data-stu-id="7a824-877">Enhancements to the RSA API so that common actions no longer require casting.</span></span> <span data-ttu-id="7a824-878">例如，當使用 <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> 物件來加密資料時，需使用類似舊版 .NET Framework 中的下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="7a824-878">For example, encrypting data using an <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> object requires code like the following in previous versions of the .NET Framework.</span></span>

      [!code-csharp[WhatsNew.Casting#1](~/samples/snippets/csharp/VS_Snippets_CLR/whatsnew.casting/cs/program.cs#1)]
      [!code-vb[WhatsNew.Casting#1](~/samples/snippets/visualbasic/VS_Snippets_CLR/whatsnew.casting/vb/module1.vb#1)]

      <span data-ttu-id="7a824-879">您可將使用 .NET Framework 4.6 中新加密 API 的程式碼改寫如下，以避免轉型。</span><span class="sxs-lookup"><span data-stu-id="7a824-879">Code that uses the new cryptography APIs in .NET Framework 4.6 can be rewritten as follows to avoid the cast.</span></span>

      [!code-csharp[WhatsNew.Casting#2](~/samples/snippets/csharp/VS_Snippets_CLR/whatsnew.casting/cs/program.cs#2)]
      [!code-vb[WhatsNew.Casting#2](~/samples/snippets/visualbasic/VS_Snippets_CLR/whatsnew.casting/vb/module1.vb#2)]

  - <span data-ttu-id="7a824-880">**支援日期和時間的 UNIX 時間來回轉換**</span><span class="sxs-lookup"><span data-stu-id="7a824-880">**Support for converting dates and times to or from Unix time**</span></span>

    <span data-ttu-id="7a824-881"><xref:System.DateTimeOffset> 結構已加入下列新方法，以支援日期和時間值的 Unix 時間來回轉換：</span><span class="sxs-lookup"><span data-stu-id="7a824-881">The following new methods have been added to the <xref:System.DateTimeOffset> structure to support converting date and time values to or from Unix time:</span></span>

    - <xref:System.DateTimeOffset.FromUnixTimeSeconds%2A?displayProperty=nameWithType>

    - <xref:System.DateTimeOffset.FromUnixTimeMilliseconds%2A?displayProperty=nameWithType>

    - <xref:System.DateTimeOffset.ToUnixTimeSeconds%2A?displayProperty=nameWithType>

    - <xref:System.DateTimeOffset.ToUnixTimeMilliseconds%2A?displayProperty=nameWithType>

  - <span data-ttu-id="7a824-882">**相容性參數**</span><span class="sxs-lookup"><span data-stu-id="7a824-882">**Compatibility switches**</span></span>

    <span data-ttu-id="7a824-883"><xref:System.AppContext>類別加入了新的相容性功能，可讓程式庫作者為使用者提供新功能的統一退出機制。</span><span class="sxs-lookup"><span data-stu-id="7a824-883">The <xref:System.AppContext> class adds a new compatibility feature that enables library writers to provide a uniform opt-out mechanism for new functionality for their users.</span></span> <span data-ttu-id="7a824-884">它會在元件之間建立鬆散結合的合約，以便傳達退出要求。</span><span class="sxs-lookup"><span data-stu-id="7a824-884">It establishes a loosely coupled contract between components in order to communicate an opt-out request.</span></span> <span data-ttu-id="7a824-885">變更現有的功能時，此功能通常特別重要。</span><span class="sxs-lookup"><span data-stu-id="7a824-885">This capability is typically important when a change is made to existing functionality.</span></span> <span data-ttu-id="7a824-886">相反地，已經有新功能的隱含選擇加入。</span><span class="sxs-lookup"><span data-stu-id="7a824-886">Conversely, there is already an implicit opt-in for new functionality.</span></span>

    <span data-ttu-id="7a824-887">使用 <xref:System.AppContext>，程式庫會定義並公開相容性參數，而依賴它們的程式碼則可以設定這些參數來影響程式庫行為。</span><span class="sxs-lookup"><span data-stu-id="7a824-887">With <xref:System.AppContext>, libraries define and expose compatibility switches, while code that depends on them can set those switches to affect the library behavior.</span></span> <span data-ttu-id="7a824-888">根據預設，程式庫可提供新的功能，且它們只會在已設定此參數時變更它 (亦即，它們提供先前的功能)。</span><span class="sxs-lookup"><span data-stu-id="7a824-888">By default, libraries provide the new functionality, and they only alter it (that is, they provide the previous functionality) if the switch is set.</span></span>

    <span data-ttu-id="7a824-889">應用程式 (或程式庫) 可以宣告相依程式庫定義之參數的值 (一律為 <xref:System.Boolean> 值)。</span><span class="sxs-lookup"><span data-stu-id="7a824-889">An application (or a library) can declare the value of a switch (which is always a <xref:System.Boolean> value) that a dependent library defines.</span></span> <span data-ttu-id="7a824-890">參數一律隱含為 `false`。</span><span class="sxs-lookup"><span data-stu-id="7a824-890">The switch is always implicitly `false`.</span></span> <span data-ttu-id="7a824-891">將參數設定為 `true` 可啟用它。</span><span class="sxs-lookup"><span data-stu-id="7a824-891">Setting the switch to `true` enables it.</span></span> <span data-ttu-id="7a824-892">明確地將參數設定為 `false` 提供了新行為。</span><span class="sxs-lookup"><span data-stu-id="7a824-892">Explicitly setting the switch to `false` provides the new behavior.</span></span>

    ```csharp
    AppContext.SetSwitch("Switch.AmazingLib.ThrowOnException", true);
    ```

    ```vb
    AppContext.SetSwitch("Switch.AmazingLib.ThrowOnException", True)
    ```

    <span data-ttu-id="7a824-893">程式庫必須檢查取用者是否已宣告參數的值，然後適當地處理它。</span><span class="sxs-lookup"><span data-stu-id="7a824-893">The library must check if a consumer has declared the value of the switch and then appropriately act on it.</span></span>

    ```csharp
    if (!AppContext.TryGetSwitch("Switch.AmazingLib.ThrowOnException", out shouldThrow))
    {
        // This is the case where the switch value was not set by the application.
        // The library can choose to get the value of shouldThrow by other means.
        // If no overrides nor default values are specified, the value should be 'false'.
        // A false value implies the latest behavior.
    }

    // The library can use the value of shouldThrow to throw exceptions or not.
    if (shouldThrow)
    {
        // old code
    }
    else
    {
        // new code
    }
    ```

    ```vb
    If Not AppContext.TryGetSwitch("Switch.AmazingLib.ThrowOnException", shouldThrow) Then
        ' This is the case where the switch value was not set by the application.
        ' The library can choose to get the value of shouldThrow by other means.
        ' If no overrides nor default values are specified, the value should be 'false'.
        ' A false value implies the latest behavior.
    End If

    ' The library can use the value of shouldThrow to throw exceptions or not.
    If shouldThrow Then
        ' old code
    Else
        ' new code
    End If
    ```

    <span data-ttu-id="7a824-894">使用一致的參數格式很有幫助，因為它們是程式庫公開的正式合約。</span><span class="sxs-lookup"><span data-stu-id="7a824-894">It's beneficial to use a consistent format for switches, since they are a formal contract exposed by a library.</span></span> <span data-ttu-id="7a824-895">以下是兩種明顯的格式。</span><span class="sxs-lookup"><span data-stu-id="7a824-895">The following are two obvious formats.</span></span>

    - <span data-ttu-id="7a824-896">*參數*.*命名空間*.*參數名稱*</span><span class="sxs-lookup"><span data-stu-id="7a824-896">*Switch*.*namespace*.*switchname*</span></span>

    - <span data-ttu-id="7a824-897">*參數*.*程式庫*.*參數名稱*</span><span class="sxs-lookup"><span data-stu-id="7a824-897">*Switch*.*library*.*switchname*</span></span>

  - <span data-ttu-id="7a824-898">**以工作為基礎的非同步模式 (TAP) 的變更**</span><span class="sxs-lookup"><span data-stu-id="7a824-898">**Changes to the task-based asynchronous pattern (TAP)**</span></span>

    <span data-ttu-id="7a824-899">在以 .NET Framework 4.6 為目標的應用程式中，<xref:System.Threading.Tasks.Task> 與 <xref:System.Threading.Tasks.Task%601> 物件會繼承呼叫端執行緒的文化特性和 UI 文化特性。</span><span class="sxs-lookup"><span data-stu-id="7a824-899">For apps that target the .NET Framework 4.6, <xref:System.Threading.Tasks.Task> and <xref:System.Threading.Tasks.Task%601> objects inherit the culture and UI culture of the calling thread.</span></span> <span data-ttu-id="7a824-900">以舊版 .NET Framework 為目標或未以特定 .NET Framework 版本為目標的應用程式行為則不會受到影響。</span><span class="sxs-lookup"><span data-stu-id="7a824-900">The behavior of apps that target previous versions of the .NET Framework, or that do not target a specific version of the .NET Framework, is unaffected.</span></span> <span data-ttu-id="7a824-901">如需詳細資訊，請參閱 <xref:System.Globalization.CultureInfo> 類別主題的＜文化特性和以工作為基礎的非同步作業＞一節。</span><span class="sxs-lookup"><span data-stu-id="7a824-901">For more information, see the "Culture and task-based asynchronous operations" section of the <xref:System.Globalization.CultureInfo> class topic.</span></span>

    <span data-ttu-id="7a824-902">若某環境資料是指定之非同步控制流程的本機環境資料，例如 `async` 方法，則可用 <xref:System.Threading.AsyncLocal%601?displayProperty=nameWithType> 類別來表示。</span><span class="sxs-lookup"><span data-stu-id="7a824-902">The <xref:System.Threading.AsyncLocal%601?displayProperty=nameWithType> class allows you to represent ambient data that is local to a given asynchronous control flow, such as an `async` method.</span></span> <span data-ttu-id="7a824-903">它可以用來跨執行緒保存資料。</span><span class="sxs-lookup"><span data-stu-id="7a824-903">It can be used to persist data across threads.</span></span> <span data-ttu-id="7a824-904">您也可以定義每當因 <xref:System.Threading.AsyncLocal%601.Value%2A?displayProperty=nameWithType> 屬性已明確變更或因執行緒發生內容切換時而變更環境資料時，接收通知的回撥方法。</span><span class="sxs-lookup"><span data-stu-id="7a824-904">You can also define a callback method that is notified whenever the ambient data changes either because the <xref:System.Threading.AsyncLocal%601.Value%2A?displayProperty=nameWithType> property was explicitly changed, or because the thread encountered a context transition.</span></span>

    <span data-ttu-id="7a824-905">以工作為基礎的非同步模式 (TAP) 中已加入 <xref:System.Threading.Tasks.Task.CompletedTask%2A?displayProperty=nameWithType>、<xref:System.Threading.Tasks.Task.FromCanceled%2A?displayProperty=nameWithType> 和 <xref:System.Threading.Tasks.Task.FromException%2A?displayProperty=nameWithType> 三種便利的方法，可傳回特定狀態中已完成的工作。</span><span class="sxs-lookup"><span data-stu-id="7a824-905">Three convenience methods, <xref:System.Threading.Tasks.Task.CompletedTask%2A?displayProperty=nameWithType>, <xref:System.Threading.Tasks.Task.FromCanceled%2A?displayProperty=nameWithType>, and <xref:System.Threading.Tasks.Task.FromException%2A?displayProperty=nameWithType>, have been added to the task-based asynchronous pattern (TAP) to return completed tasks in a particular state.</span></span>

    <span data-ttu-id="7a824-906"><xref:System.IO.Pipes.NamedPipeClientStream> 類別現可支援與其新的 <xref:System.IO.Pipes.NamedPipeClientStream.ConnectAsync%2A> 進行非同步通訊。</span><span class="sxs-lookup"><span data-stu-id="7a824-906">The <xref:System.IO.Pipes.NamedPipeClientStream> class now supports asynchronous communication with its new <xref:System.IO.Pipes.NamedPipeClientStream.ConnectAsync%2A>.</span></span> <span data-ttu-id="7a824-907">方法。</span><span class="sxs-lookup"><span data-stu-id="7a824-907">method.</span></span>

  - <span data-ttu-id="7a824-908">**EventSource 現在支援寫入事件記錄檔**</span><span class="sxs-lookup"><span data-stu-id="7a824-908">**EventSource now supports writing to the Event log**</span></span>

    <span data-ttu-id="7a824-909">不只電腦上建立的任何現有 ETW 工作階段，您現在還可以使用 <xref:System.Diagnostics.Tracing.EventSource> 類別，將管理或操作訊息記錄到事件記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="7a824-909">You now can use the <xref:System.Diagnostics.Tracing.EventSource> class to log administrative or operational messages to the event log, in addition to any existing ETW sessions created on the machine.</span></span> <span data-ttu-id="7a824-910">以往，您必須使用 Microsoft.Diagnostics.Tracing.EventSource NuGet 套件，才能使用這項功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-910">In the past, you had to use the Microsoft.Diagnostics.Tracing.EventSource NuGet package for this functionality.</span></span> <span data-ttu-id="7a824-911">.NET Framework 4.6 現已內建此功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-911">This functionality is now built-into .NET Framework 4.6.</span></span>

    <span data-ttu-id="7a824-912">NuGet 套件和 .NET Framework 4.6 已更新並支援下列功能：</span><span class="sxs-lookup"><span data-stu-id="7a824-912">Both the NuGet package and .NET Framework 4.6 have been updated with the following features:</span></span>

    - <span data-ttu-id="7a824-913">**動態事件**</span><span class="sxs-lookup"><span data-stu-id="7a824-913">**Dynamic events**</span></span>

      <span data-ttu-id="7a824-914">可「動態」定義事件，而不需建立事件方法。</span><span class="sxs-lookup"><span data-stu-id="7a824-914">Allows events defined "on the fly" without creating event methods.</span></span>

    - <span data-ttu-id="7a824-915">**豐富型裝載**</span><span class="sxs-lookup"><span data-stu-id="7a824-915">**Rich payloads**</span></span>

      <span data-ttu-id="7a824-916">允許專用類別和陣列，以及基本類型做為裝載傳遞</span><span class="sxs-lookup"><span data-stu-id="7a824-916">Allows specially attributed classes and arrays as well as primitive types to be passed as a payload</span></span>

    - <span data-ttu-id="7a824-917">**活動追蹤**</span><span class="sxs-lookup"><span data-stu-id="7a824-917">**Activity tracking**</span></span>

      <span data-ttu-id="7a824-918">可讓開始與結束事件使用識別碼來標記它們之間的事件，以代表目前作用中的所有活動。</span><span class="sxs-lookup"><span data-stu-id="7a824-918">Causes Start and Stop events to tag events between them with an ID that represents all currently active activities.</span></span>

    <span data-ttu-id="7a824-919">為了支援這些功能，已將多載 <xref:System.Diagnostics.Tracing.EventSource.Write%2A> 方法加入<xref:System.Diagnostics.Tracing.EventSource> 類別。</span><span class="sxs-lookup"><span data-stu-id="7a824-919">To support these features, the overloaded <xref:System.Diagnostics.Tracing.EventSource.Write%2A> method has been added to the <xref:System.Diagnostics.Tracing.EventSource> class.</span></span>

- <span data-ttu-id="7a824-920">**Windows Presentation Foundation (WPF)**</span><span class="sxs-lookup"><span data-stu-id="7a824-920">**Windows Presentation Foundation (WPF)**</span></span>

  - <span data-ttu-id="7a824-921">**HDPI 改進**</span><span class="sxs-lookup"><span data-stu-id="7a824-921">**HDPI improvements**</span></span>

    <span data-ttu-id="7a824-922">現在，WPF 提供比 .NET Framework 4.6 更好的 HDPI 支援。</span><span class="sxs-lookup"><span data-stu-id="7a824-922">HDPI support in WPF is now better in the .NET Framework 4.6.</span></span> <span data-ttu-id="7a824-923">已變更版面配置進位，以減少含邊界之控制項中的裁剪執行個體。</span><span class="sxs-lookup"><span data-stu-id="7a824-923">Changes have been made to layout rounding to reduce instances of clipping in controls with borders.</span></span> <span data-ttu-id="7a824-924">根據預設，這項功能只有當您將<xref:System.Runtime.Versioning.TargetFrameworkAttribute> 設為 .NET 4.6 時才會啟用。</span><span class="sxs-lookup"><span data-stu-id="7a824-924">By default, this feature is enabled only if your <xref:System.Runtime.Versioning.TargetFrameworkAttribute> is set to .NET 4.6.</span></span>  <span data-ttu-id="7a824-925">以舊版 framework 為目標但在 .NET Framework 4.6 上執行的應用程式，可以藉由將下列這一行新增至 app.config 檔的區段，以加入宣告新的行為 [\<runtime>](../configure-apps/file-schema/runtime/runtime-element.md) ：</span><span class="sxs-lookup"><span data-stu-id="7a824-925">Applications that target earlier versions of the framework but are running on the .NET Framework 4.6 can opt in to the new behavior by adding the following line to the [\<runtime>](../configure-apps/file-schema/runtime/runtime-element.md) section of the app.config file:</span></span>

    ```xml
    <AppContextSwitchOverrides
    value="Switch.MS.Internal.DoNotApplyLayoutRoundingToMarginsAndBorderThickness=false"
    />
    ```

    <span data-ttu-id="7a824-926">含不同 DPI 設定 (多 DPI 設定) 且跨多個監視器的 WPF 視窗，現可完全顯示，而不會有被遮蔽的區域。</span><span class="sxs-lookup"><span data-stu-id="7a824-926">WPF windows straddling multiple monitors with different DPI settings (Multi-DPI setup) are now completely rendered without blacked-out regions.</span></span> <span data-ttu-id="7a824-927">您可將下列這一行加入 app.config 檔的 `<appSettings>` 區段，以選擇停用這項新的行為：</span><span class="sxs-lookup"><span data-stu-id="7a824-927">You can opt out of this behavior by adding the following line to the `<appSettings>` section of the app.config file to disable this new behavior:</span></span>

    ```xml
    <add key="EnableMultiMonitorDisplayClipping" value="true"/>
    ```

    <span data-ttu-id="7a824-928"><xref:System.Windows.Input.Cursor?displayProperty=nameWithType> 已支援自動依據 DPI 設定載入正確的游標。</span><span class="sxs-lookup"><span data-stu-id="7a824-928">Support for automatically loading the right cursor based on DPI setting has been added to  <xref:System.Windows.Input.Cursor?displayProperty=nameWithType>.</span></span>

  - <span data-ttu-id="7a824-929">**觸控功能較佳**</span><span class="sxs-lookup"><span data-stu-id="7a824-929">**Touch is better**</span></span>

    <span data-ttu-id="7a824-930">.NET Framework 4.6 已將客戶對[連線](https://connect.microsoft.com/VisualStudio/feedback/details/903760/)回報的觸控行為異常問題解決。</span><span class="sxs-lookup"><span data-stu-id="7a824-930">Customer reports on [Connect](https://connect.microsoft.com/VisualStudio/feedback/details/903760/) that touch produces unpredictable behavior have been addressed in the .NET Framework 4.6.</span></span> <span data-ttu-id="7a824-931">Windows 市集應用程式和 WPF 應用程式的點兩下臨界值現與 Windows 8.1 和更新版本相同。</span><span class="sxs-lookup"><span data-stu-id="7a824-931">The double tap threshold for Windows Store applications and WPF applications is now the same in Windows 8.1 and above.</span></span>

  - <span data-ttu-id="7a824-932">**支援透明的子視窗**</span><span class="sxs-lookup"><span data-stu-id="7a824-932">**Transparent child window support**</span></span>

    <span data-ttu-id="7a824-933">.NET Framework 4.6 中的 WPF 支援 Windows 8.1 和更新版本的透明子視窗功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-933">WPF in the .NET Framework 4.6 supports transparent child windows in Windows 8.1 and above.</span></span> <span data-ttu-id="7a824-934">這可讓您在最上層視窗中建立非矩形和透明的子視窗。</span><span class="sxs-lookup"><span data-stu-id="7a824-934">This allows you to create non-rectangular and transparent child windows in your top-level windows.</span></span> <span data-ttu-id="7a824-935">您可以將 <xref:System.Windows.Interop.HwndSourceParameters.UsesPerPixelTransparency%2A?displayProperty=nameWithType> 屬性設為 `true`，藉此啟用這個功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-935">You can enable this feature by setting the <xref:System.Windows.Interop.HwndSourceParameters.UsesPerPixelTransparency%2A?displayProperty=nameWithType> property to `true`.</span></span>

- <span data-ttu-id="7a824-936">**Windows Communication Foundation (WCF)**</span><span class="sxs-lookup"><span data-stu-id="7a824-936">**Windows Communication Foundation (WCF)**</span></span>

  - <span data-ttu-id="7a824-937">**SSL 支援**</span><span class="sxs-lookup"><span data-stu-id="7a824-937">**SSL support**</span></span>

    <span data-ttu-id="7a824-938">搭配使用 NetTcp 與傳輸安全性和用戶端驗證時，除了 SSL 3.0 和 TLS 1.0 之外，WCF 現在還支援 TLS 1.1 和 TLS 1.2 的 SSL 版。</span><span class="sxs-lookup"><span data-stu-id="7a824-938">WCF now supports SSL version TLS 1.1 and TLS 1.2, in addition to SSL 3.0 and TLS 1.0, when using NetTcp with transport security and client authentication.</span></span> <span data-ttu-id="7a824-939">現在，您可以選取要使用哪一種通訊協定，或停用較不安全的舊版通訊協定。</span><span class="sxs-lookup"><span data-stu-id="7a824-939">It is now possible to select which protocol to use, or to disable old lesser secure protocols.</span></span> <span data-ttu-id="7a824-940">若要完成這項作業，您可設定 <xref:System.ServiceModel.TcpTransportSecurity.SslProtocols%2A> 屬性或於組態檔中加入下列內容。</span><span class="sxs-lookup"><span data-stu-id="7a824-940">This can be done either by setting the <xref:System.ServiceModel.TcpTransportSecurity.SslProtocols%2A> property or by adding the following to a configuration file.</span></span>

    ```xml
    <netTcpBinding>
        <binding>
          <security mode= "None|Transport|Message|TransportWithMessageCredential" >
              <transport clientCredentialType="None|Windows|Certificate"
                        protectionLevel="None|Sign|EncryptAndSign"
                        sslProtocols="Ssl3|Tls1|Tls11|Tls12">
                </transport>
          </security>
        </binding>
    </netTcpBinding>
    ```

  - <span data-ttu-id="7a824-941">**使用不同的 HTTP 連線傳送訊息**</span><span class="sxs-lookup"><span data-stu-id="7a824-941">**Sending messages using different HTTP connections**</span></span>

    <span data-ttu-id="7a824-942">現在，WCF 可讓使用者使用不同的底層 HTTP 連線以確保成功傳送特定訊息。</span><span class="sxs-lookup"><span data-stu-id="7a824-942">WCF now allows users to ensure certain messages are sent using different underlying HTTP connections.</span></span> <span data-ttu-id="7a824-943">作法有二：</span><span class="sxs-lookup"><span data-stu-id="7a824-943">There are two ways to do this:</span></span>

    - <span data-ttu-id="7a824-944">**使用連線群組名稱前置詞**</span><span class="sxs-lookup"><span data-stu-id="7a824-944">**Using a connection group name prefix**</span></span>

      <span data-ttu-id="7a824-945">使用者可以指定字串，讓 WCF 用作連線群組名稱的前置詞。</span><span class="sxs-lookup"><span data-stu-id="7a824-945">Users can specify a string that WCF will use as a prefix for the connection group name.</span></span> <span data-ttu-id="7a824-946">系統會使用不同的基礎 HTTP 連線來傳送含有不同前置詞的兩個訊息。</span><span class="sxs-lookup"><span data-stu-id="7a824-946">Two messages with different prefixes are sent using different underlying HTTP connections.</span></span> <span data-ttu-id="7a824-947">您可以將鍵/值組加入訊息的 <xref:System.ServiceModel.Channels.Message.Properties%2A?displayProperty=nameWithType> 屬性，以設定前置詞。</span><span class="sxs-lookup"><span data-stu-id="7a824-947">You set the prefix by adding a key/value pair to the message's <xref:System.ServiceModel.Channels.Message.Properties%2A?displayProperty=nameWithType> property.</span></span> <span data-ttu-id="7a824-948">索引鍵是 "HttpTransportConnectionGroupNamePrefix"；值則為所需的前置詞。</span><span class="sxs-lookup"><span data-stu-id="7a824-948">The key is "HttpTransportConnectionGroupNamePrefix"; the value is the desired prefix.</span></span>

    - <span data-ttu-id="7a824-949">**使用不同的通道處理站**</span><span class="sxs-lookup"><span data-stu-id="7a824-949">**Using different channel factories**</span></span>

      <span data-ttu-id="7a824-950">使用者也可以啟用功能，針對使用不同通道處理站建立之通道所傳送的訊息，使用不同的底層 HTTP 連線。</span><span class="sxs-lookup"><span data-stu-id="7a824-950">Users can also enable a feature that ensures that messages sent using channels created by different channel factories will use different underlying HTTP connections.</span></span> <span data-ttu-id="7a824-951">若要啟用此功能，使用者必須將下列 `appSetting` 設定為 `true`：</span><span class="sxs-lookup"><span data-stu-id="7a824-951">To enable this feature, users must set the following `appSetting` to `true`:</span></span>

      ```xml
      <appSettings>
          <add key="wcf:httpTransportBinding:useUniqueConnectionPoolPerFactory" value="true" />
      </appSettings>
      ```

- <span data-ttu-id="7a824-952">**Windows Workflow Foundation (WWF)**</span><span class="sxs-lookup"><span data-stu-id="7a824-952">**Windows Workflow Foundation (WWF)**</span></span>

  <span data-ttu-id="7a824-953">現在，若有未處理的「非通訊協定」書籤時，您可以指定工作流程服務在不按照順序的作業要求逾時之前會保存該要求的秒數。</span><span class="sxs-lookup"><span data-stu-id="7a824-953">You can now specify the number of seconds a workflow service will hold on to an out-of-order operation request when there is an outstanding "non-protocol" bookmark before timing out the request.</span></span> <span data-ttu-id="7a824-954">「非通訊協定」書籤是指與未處理的 Receive 活動無關的書籤。</span><span class="sxs-lookup"><span data-stu-id="7a824-954">A "non-protocol" bookmark is a bookmark that is not related to outstanding Receive activities.</span></span> <span data-ttu-id="7a824-955">有些活動會在其實作中建立非通訊協定書籤，因此可能不容易察覺到非通訊協定書籤的存在。</span><span class="sxs-lookup"><span data-stu-id="7a824-955">Some activities create non-protocol bookmarks within their implementation, so it may not be obvious that a non-protocol bookmark exists.</span></span> <span data-ttu-id="7a824-956">這些活動包括 State 和 Pick。</span><span class="sxs-lookup"><span data-stu-id="7a824-956">These include State and Pick.</span></span> <span data-ttu-id="7a824-957">因此如果您有使用狀態機器或包含 Pick 活動的工作流程服務實作，就很可能會有非通訊協定書籤。</span><span class="sxs-lookup"><span data-stu-id="7a824-957">So if you have a workflow service implemented with a state machine or containing a Pick activity, you will most likely have non-protocol bookmarks.</span></span> <span data-ttu-id="7a824-958">您可將如下一行加入 app.config 檔案的 `appSettings` 區段，以指定間隔：</span><span class="sxs-lookup"><span data-stu-id="7a824-958">You specify the interval by adding a line like the following to the `appSettings` section of your app.config file:</span></span>

  ```xml
  <add key="microsoft:WorkflowServices:FilterResumeTimeoutInSeconds" value="60"/>
  ```

  <span data-ttu-id="7a824-959">預設值為 60 秒。</span><span class="sxs-lookup"><span data-stu-id="7a824-959">The default value is 60 seconds.</span></span> <span data-ttu-id="7a824-960">如果 `value` 設定為 0，系統會立即拒絕不按照順序的要求，並顯示如下的錯誤文字：</span><span class="sxs-lookup"><span data-stu-id="7a824-960">If `value` is set to 0, out-of-order requests are immediately rejected with a fault with text that looks like this:</span></span>

  ```console
  Operation 'Request3|{http://tempuri.org/}IService' on service instance with identifier '2b0667b6-09c8-4093-9d02-f6c67d534292' cannot be performed at this time. Please ensure that the operations are performed in the correct order and that the binding in use provides ordered delivery guarantees.
  ```

  <span data-ttu-id="7a824-961">如果收到不按照順序的作業訊息，但沒有非通訊協定書籤時，也會收到相同的訊息。</span><span class="sxs-lookup"><span data-stu-id="7a824-961">This is the same message that you receive if an out-of-order operation message is received and there are no non-protocol bookmarks.</span></span>

  <span data-ttu-id="7a824-962">如果 `FilterResumeTimeoutInSeconds` 項目的值是非零，並有非通訊協定的書籤，而逾時間隔也已過期，則作業會失敗並顯示逾時訊息。</span><span class="sxs-lookup"><span data-stu-id="7a824-962">If the value of the `FilterResumeTimeoutInSeconds` element is non-zero, there are non-protocol bookmarks, and the timeout interval expires, the operation fails with a timeout message.</span></span>

- <span data-ttu-id="7a824-963">**交易**</span><span class="sxs-lookup"><span data-stu-id="7a824-963">**Transactions**</span></span>

  <span data-ttu-id="7a824-964">現在，若交易導致衍生自 <xref:System.Transactions.TransactionException> 的例外狀況擲回時，您可以針對該交易包含分散式的交易識別碼。</span><span class="sxs-lookup"><span data-stu-id="7a824-964">You can now include the distributed transaction identifier for the transaction that has caused an exception derived from <xref:System.Transactions.TransactionException> to be thrown.</span></span> <span data-ttu-id="7a824-965">您可以在 app.config 檔的`appSettings` 區段中加入下列索引鍵，以完成這項作業：</span><span class="sxs-lookup"><span data-stu-id="7a824-965">You do this by adding the following key to the `appSettings` section of your app.config file:</span></span>

  ```xml
  <add key="Transactions:IncludeDistributedTransactionIdInExceptionMessage" value="true"/>
  ```

  <span data-ttu-id="7a824-966">預設值是 `false`。</span><span class="sxs-lookup"><span data-stu-id="7a824-966">The default value is `false`.</span></span>

- <span data-ttu-id="7a824-967">**網路功能**</span><span class="sxs-lookup"><span data-stu-id="7a824-967">**Networking**</span></span>

  - <span data-ttu-id="7a824-968">**通訊端重複使用**</span><span class="sxs-lookup"><span data-stu-id="7a824-968">**Socket reuse**</span></span>

    <span data-ttu-id="7a824-969">Windows 10 包含新的高延展性網路功能演算法，其可重複為對外 TCP 連線使用本機連接埠，以更妥善運用電腦資源。</span><span class="sxs-lookup"><span data-stu-id="7a824-969">Windows 10 includes a new high-scalability networking algorithm that makes better use of machine resources by reusing local ports for outbound TCP connections.</span></span> <span data-ttu-id="7a824-970">.NET Framework 4.6 支援新的演算法，可讓 .NET 應用程式利用這個新行為。</span><span class="sxs-lookup"><span data-stu-id="7a824-970">.NET Framework 4.6 supports the new algorithm, enabling .NET apps to take advantage of the new behavior.</span></span> <span data-ttu-id="7a824-971">在舊版的 Windows 中，並沒有人為的並行連線限制 (通常為動態連接埠範圍的預設大小 16,384)，因此當負載下的連接埠耗盡時，可能會限制服務的延展性。</span><span class="sxs-lookup"><span data-stu-id="7a824-971">In previous versions of Windows, there was an artificial concurrent connection limit (typically 16,384, the default size of the dynamic port range), which could limit the scalability of a service by causing port exhaustion when under load.</span></span>

    <span data-ttu-id="7a824-972">在 .NET Framework 4.6 中，已加入兩個 Api 來啟用埠重複使用，如此可有效地移除並行連線的 64 KB 限制：</span><span class="sxs-lookup"><span data-stu-id="7a824-972">In .NET Framework 4.6, two APIs have been added to enable port reuse, which effectively removes the 64 KB limit on concurrent connections:</span></span>

    - <span data-ttu-id="7a824-973"><xref:System.Net.Sockets.SocketOptionName?displayProperty=nameWithType> 列舉值。</span><span class="sxs-lookup"><span data-stu-id="7a824-973">The <xref:System.Net.Sockets.SocketOptionName?displayProperty=nameWithType> enumeration value.</span></span>

    - <span data-ttu-id="7a824-974"><xref:System.Net.ServicePointManager.ReusePort%2A?displayProperty=nameWithType> 屬性。</span><span class="sxs-lookup"><span data-stu-id="7a824-974">The <xref:System.Net.ServicePointManager.ReusePort%2A?displayProperty=nameWithType> property.</span></span>

    <span data-ttu-id="7a824-975">除非 `HKLM\SOFTWARE\Microsoft\.NETFramework\v4.0.30319` 登錄機碼的 `HWRPortReuseOnSocketBind` 值設定為 0x1，否則 <xref:System.Net.ServicePointManager.ReusePort%2A?displayProperty=nameWithType> 屬性皆預設為 `false`。</span><span class="sxs-lookup"><span data-stu-id="7a824-975">By default, the <xref:System.Net.ServicePointManager.ReusePort%2A?displayProperty=nameWithType> property is `false` unless the `HWRPortReuseOnSocketBind` value of the `HKLM\SOFTWARE\Microsoft\.NETFramework\v4.0.30319` registry key is set to 0x1.</span></span> <span data-ttu-id="7a824-976">若要啟用 HTTP 連線上的本機連接埠重複使用，請將 <xref:System.Net.ServicePointManager.ReusePort%2A?displayProperty=nameWithType> 屬性設為 `true`。</span><span class="sxs-lookup"><span data-stu-id="7a824-976">To enable local port reuse on HTTP connections, set the <xref:System.Net.ServicePointManager.ReusePort%2A?displayProperty=nameWithType> property to `true`.</span></span> <span data-ttu-id="7a824-977">這會使得所有從 <xref:System.Net.Http.HttpClient> 和 <xref:System.Net.HttpWebRequest> 傳出的 TCP 通訊端連線都使用新的 Windows 10 通訊端選項 ([SO_REUSE_UNICASTPORT](/windows/desktop/WinSock/sol-socket-socket-options))，而能夠重複使用本機連接埠。</span><span class="sxs-lookup"><span data-stu-id="7a824-977">This causes all outgoing TCP socket connections from <xref:System.Net.Http.HttpClient> and <xref:System.Net.HttpWebRequest> to use a new Windows 10 socket option, [SO_REUSE_UNICASTPORT](/windows/desktop/WinSock/sol-socket-socket-options), that enables local port reuse.</span></span>

    <span data-ttu-id="7a824-978">如果開發人員撰寫僅限通訊端的應用程式，即可在呼叫 <xref:System.Net.Sockets.Socket.SetSocketOption%2A?displayProperty=nameWithType> 之類的方法時指定 <xref:System.Net.Sockets.SocketOptionName?displayProperty=nameWithType> 選項，以讓對外的通訊端在繫結期間重複使用本機連接埠。</span><span class="sxs-lookup"><span data-stu-id="7a824-978">Developers writing a sockets-only application can specify the <xref:System.Net.Sockets.SocketOptionName?displayProperty=nameWithType> option when calling a method such as <xref:System.Net.Sockets.Socket.SetSocketOption%2A?displayProperty=nameWithType> so that outbound sockets reuse local ports during binding.</span></span>

  - <span data-ttu-id="7a824-979">**支援國際網域名稱和 PunyCode**</span><span class="sxs-lookup"><span data-stu-id="7a824-979">**Support for international domain names and PunyCode**</span></span>

    <span data-ttu-id="7a824-980"><xref:System.Uri> 類別中已加入新屬性 <xref:System.Uri.IdnHost%2A>，可更妥善支援國際化網域名稱和 PunyCode。</span><span class="sxs-lookup"><span data-stu-id="7a824-980">A new property, <xref:System.Uri.IdnHost%2A>, has been added to the <xref:System.Uri> class to better support international domain names and PunyCode.</span></span>

- <span data-ttu-id="7a824-981">**調整 Windows Forms 控制項的大小。**</span><span class="sxs-lookup"><span data-stu-id="7a824-981">**Resizing in Windows Forms controls.**</span></span>

  <span data-ttu-id="7a824-982">此功能在 .NET Framework 4.6 中已擴充以包含 <xref:System.Windows.Forms.DomainUpDown>、<xref:System.Windows.Forms.NumericUpDown>、<xref:System.Windows.Forms.DataGridViewComboBoxColumn>、<xref:System.Windows.Forms.DataGridViewColumn> 與 <xref:System.Windows.Forms.ToolStripSplitButton> 型別，而且當繪製 <xref:System.Drawing.Design.UITypeEditor> 時會使用由 <xref:System.Drawing.Design.PaintValueEventArgs.Bounds%2A> 屬性所指定的矩形。</span><span class="sxs-lookup"><span data-stu-id="7a824-982">This feature has been expanded in .NET Framework 4.6 to include the <xref:System.Windows.Forms.DomainUpDown>, <xref:System.Windows.Forms.NumericUpDown>, <xref:System.Windows.Forms.DataGridViewComboBoxColumn>, <xref:System.Windows.Forms.DataGridViewColumn> and <xref:System.Windows.Forms.ToolStripSplitButton> types and the rectangle specified by the <xref:System.Drawing.Design.PaintValueEventArgs.Bounds%2A> property used when drawing a <xref:System.Drawing.Design.UITypeEditor>.</span></span>

  <span data-ttu-id="7a824-983">這是一項選擇性功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-983">This is an opt-in feature.</span></span> <span data-ttu-id="7a824-984">若要啟用此功能，請將應用程式組態檔 (app.config) 中的 `EnableWindowsFormsHighDpiAutoResizing` 項目設定為 `true`：</span><span class="sxs-lookup"><span data-stu-id="7a824-984">To enable it, set the `EnableWindowsFormsHighDpiAutoResizing` element to `true` in the application configuration (app.config) file:</span></span>

  ```xml
  <appSettings>
      <add key="EnableWindowsFormsHighDpiAutoResizing" value="true" />
  </appSettings>
  ```

- <span data-ttu-id="7a824-985">**字碼頁編碼方式的支援**</span><span class="sxs-lookup"><span data-stu-id="7a824-985">**Support for code page encodings**</span></span>

  <span data-ttu-id="7a824-986">.NET Core 主要支援 Unicode 編碼方式，並且預設會提供字碼頁編碼方式的有限支援。</span><span class="sxs-lookup"><span data-stu-id="7a824-986">.NET Core primarily supports the Unicode encodings and by default provides limited support for code page encodings.</span></span> <span data-ttu-id="7a824-987">您可以透過使用 <xref:System.Text.Encoding.RegisterProvider%2A?displayProperty=nameWithType> 方法註冊字碼頁編碼方式，來加入 .NET Framework 中可用但不受 .NET Core 支援之字碼頁編碼方式的支援。</span><span class="sxs-lookup"><span data-stu-id="7a824-987">You can add support for code page encodings available in .NET Framework but unsupported in .NET Core by registering code page encodings with the <xref:System.Text.Encoding.RegisterProvider%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="7a824-988">如需詳細資訊，請參閱<xref:System.Text.CodePagesEncodingProvider?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="7a824-988">For more information, see <xref:System.Text.CodePagesEncodingProvider?displayProperty=nameWithType>.</span></span>

- <span data-ttu-id="7a824-989">**.NET Native**</span><span class="sxs-lookup"><span data-stu-id="7a824-989">**.NET Native**</span></span>

  <span data-ttu-id="7a824-990">以 .NET Core 為目標並以 C# 或 Visual Basic 撰寫的 Windows 10 應用程式，現在可以利用將應用程式編譯成機器碼的新技術，而不是使用 IL。</span><span class="sxs-lookup"><span data-stu-id="7a824-990">Windows apps for Windows 10 that target .NET Core and are written in C# or Visual Basic can take advantage of a new technology that compiles apps to native code rather than IL.</span></span> <span data-ttu-id="7a824-991">所產生之應用程式的特色是啟動和執行都更快。</span><span class="sxs-lookup"><span data-stu-id="7a824-991">They produce apps characterized by faster startup and execution times.</span></span> <span data-ttu-id="7a824-992">如需詳細資訊，請參閱[使用 .NET Native 編譯應用程式](../net-native/index.md)。</span><span class="sxs-lookup"><span data-stu-id="7a824-992">For more information, see [Compiling Apps with .NET Native](../net-native/index.md).</span></span> <span data-ttu-id="7a824-993">如需 .NET Native 概觀，請參閱 [.NET Native 和編譯](../net-native/net-native-and-compilation.md)，其中探討 .NET Native 與 JIT 編譯和 NGEN 之間的差異，以及對您的程式碼所代表的意義。</span><span class="sxs-lookup"><span data-stu-id="7a824-993">For an overview of .NET Native that examines how it differs from both JIT compilation and NGEN and what that means for your code, see [.NET Native and Compilation](../net-native/net-native-and-compilation.md).</span></span>

  <span data-ttu-id="7a824-994">根據預設，當您使用 Visual Studio 2015 或更新版本編繹應用程式時，應用程式會編譯成機器碼。</span><span class="sxs-lookup"><span data-stu-id="7a824-994">Your apps are compiled to native code by default when you compile them with Visual Studio 2015 or later.</span></span> <span data-ttu-id="7a824-995">如需詳細資訊，請參閱 [.NET Native 使用者入門](../net-native/getting-started-with-net-native.md)。</span><span class="sxs-lookup"><span data-stu-id="7a824-995">For more information, see [Getting Started with .NET Native](../net-native/getting-started-with-net-native.md).</span></span>

  <span data-ttu-id="7a824-996">為了支援對 .NET Native 應用程式進行偵錯，Unmanaged 偵錯 API 已新增許多介面和列舉。</span><span class="sxs-lookup"><span data-stu-id="7a824-996">To support debugging .NET Native apps, a number of new interfaces and enumerations have been added to the unmanaged debugging API.</span></span> <span data-ttu-id="7a824-997">如需詳細資訊，請參閱[偵錯 (Unmanaged API 參考)](../unmanaged-api/debugging/index.md) 主題。</span><span class="sxs-lookup"><span data-stu-id="7a824-997">For more information, see the [Debugging (Unmanaged API Reference)](../unmanaged-api/debugging/index.md) topic.</span></span>

- <span data-ttu-id="7a824-998">**開放原始碼 .NET Framework 套件**</span><span class="sxs-lookup"><span data-stu-id="7a824-998">**Open-source .NET Framework packages**</span></span>

  <span data-ttu-id="7a824-999">.NET Core 套件（例如，在命名空間中找到的不可變集合、 [SIMD api](https://www.nuget.org/packages/Microsoft.Bcl.Simd)和網路 api） <xref:System.Net.Http> 現在可在 [GitHub](https://github.com/)上以開放原始碼套件的形式提供。</span><span class="sxs-lookup"><span data-stu-id="7a824-999">.NET Core packages such as the immutable collections, [SIMD APIs](https://www.nuget.org/packages/Microsoft.Bcl.Simd), and networking APIs such as those found in the <xref:System.Net.Http> namespace are now available as open-source packages on [GitHub](https://github.com/).</span></span> <span data-ttu-id="7a824-1000">若要存取程式碼，請參閱 [GitHub 上的 .net](https://github.com/dotnet/runtime)。</span><span class="sxs-lookup"><span data-stu-id="7a824-1000">To access the code, see [.NET on GitHub](https://github.com/dotnet/runtime).</span></span> <span data-ttu-id="7a824-1001">如需詳細資訊以及如何參與這些套件的建立，請前往 [itHub 上的 .NET 首頁](https://github.com/dotnet/home)，並參閱 [.NET Core 和開放原始碼](../get-started/net-core-and-open-source.md)。</span><span class="sxs-lookup"><span data-stu-id="7a824-1001">For more information and how to contribute to these packages, see [.NET Core and Open-Source](../get-started/net-core-and-open-source.md), [.NET Home Page on GitHub](https://github.com/dotnet/home).</span></span>

<a name="v452"></a>

## <a name="whats-new-in-net-framework-452"></a><span data-ttu-id="7a824-1002">.NET Framework 4.5.2 中的新功能</span><span class="sxs-lookup"><span data-stu-id="7a824-1002">What's new in .NET Framework 4.5.2</span></span>

- <span data-ttu-id="7a824-1003">**ASP.NET 應用程式的全新 API。**</span><span class="sxs-lookup"><span data-stu-id="7a824-1003">**New APIs for ASP.NET apps.**</span></span> <span data-ttu-id="7a824-1004">新的 <xref:System.Web.HttpResponse.AddOnSendingHeaders%2A?displayProperty=nameWithType> 和 <xref:System.Web.HttpResponseBase.AddOnSendingHeaders%2A?displayProperty=nameWithType> 方法可讓您在回應清除至用戶端應用程式時，檢查及修改回應標頭和狀態碼。</span><span class="sxs-lookup"><span data-stu-id="7a824-1004">The new <xref:System.Web.HttpResponse.AddOnSendingHeaders%2A?displayProperty=nameWithType> and <xref:System.Web.HttpResponseBase.AddOnSendingHeaders%2A?displayProperty=nameWithType> methods let you inspect and modify response headers and status code as the response is being flushed to the client app.</span></span> <span data-ttu-id="7a824-1005">請考慮使用這些方法來取代 <xref:System.Web.HttpApplication.PreSendRequestHeaders> 和 <xref:System.Web.HttpApplication.PreSendRequestContent> 事件，這些方法的效率更高且更可靠。</span><span class="sxs-lookup"><span data-stu-id="7a824-1005">Consider using these methods instead of the <xref:System.Web.HttpApplication.PreSendRequestHeaders> and <xref:System.Web.HttpApplication.PreSendRequestContent> events; they are more efficient and reliable.</span></span>

  <span data-ttu-id="7a824-1006"><xref:System.Web.Hosting.HostingEnvironment.QueueBackgroundWorkItem%2A?displayProperty=nameWithType> 方法可讓您排程小型背景工作項目。</span><span class="sxs-lookup"><span data-stu-id="7a824-1006">The <xref:System.Web.Hosting.HostingEnvironment.QueueBackgroundWorkItem%2A?displayProperty=nameWithType> method lets you schedule small background work items.</span></span> <span data-ttu-id="7a824-1007">完成所有背景工作項目之前，ASP.NET 會追蹤這些項目，並防止 IIS 突然終止背景工作處理序。</span><span class="sxs-lookup"><span data-stu-id="7a824-1007">ASP.NET tracks these items and prevents IIS from abruptly terminating the worker process until all background work items have completed.</span></span> <span data-ttu-id="7a824-1008">此方法只能在 ASP.NET Managed 應用程式網域內呼叫。</span><span class="sxs-lookup"><span data-stu-id="7a824-1008">This method can't be called outside an ASP.NET managed app domain.</span></span>

  <span data-ttu-id="7a824-1009">新的 <xref:System.Web.HttpResponse.HeadersWritten?displayProperty=nameWithType> 和 <xref:System.Web.HttpResponseBase.HeadersWritten?displayProperty=nameWithType> 屬性傳回布林值，指出是否已寫入回應標頭。</span><span class="sxs-lookup"><span data-stu-id="7a824-1009">The new <xref:System.Web.HttpResponse.HeadersWritten?displayProperty=nameWithType> and <xref:System.Web.HttpResponseBase.HeadersWritten?displayProperty=nameWithType> properties return Boolean values that indicate whether the response headers have been written.</span></span> <span data-ttu-id="7a824-1010">您可以使用這些屬性確定 <xref:System.Web.HttpResponse.StatusCode%2A?displayProperty=nameWithType> 等的 API 呼叫成功 (如果已寫入標頭，則擲回例外狀況)。</span><span class="sxs-lookup"><span data-stu-id="7a824-1010">You can use these properties to make sure that calls to APIs such as <xref:System.Web.HttpResponse.StatusCode%2A?displayProperty=nameWithType> (which throw exceptions if the headers have been written) will succeed.</span></span>

- <span data-ttu-id="7a824-1011">**調整 Windows Forms 控制項的大小。**</span><span class="sxs-lookup"><span data-stu-id="7a824-1011">**Resizing in Windows Forms controls.**</span></span> <span data-ttu-id="7a824-1012">此功能已擴充。</span><span class="sxs-lookup"><span data-stu-id="7a824-1012">This feature has been expanded.</span></span> <span data-ttu-id="7a824-1013">您現在可以使用系統 DPI 設定來調整下列其他控制項的元件大小 (例如下拉式方塊中的下拉式箭頭)：</span><span class="sxs-lookup"><span data-stu-id="7a824-1013">You can now use the system DPI setting to resize components of the following additional controls (for example, the drop-down arrow in combo boxes):</span></span>

  - <xref:System.Windows.Forms.ComboBox>
  - <xref:System.Windows.Forms.ToolStripComboBox>
  - <xref:System.Windows.Forms.ToolStripMenuItem>
  - <xref:System.Windows.Forms.Cursor>
  - <xref:System.Windows.Forms.DataGridView>
  - <xref:System.Windows.Forms.DataGridViewComboBoxColumn>

  <span data-ttu-id="7a824-1014">這是一項選擇性功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1014">This is an opt-in feature.</span></span> <span data-ttu-id="7a824-1015">若要啟用此功能，請將應用程式組態檔 (app.config) 中的 `EnableWindowsFormsHighDpiAutoResizing` 項目設定為 `true`：</span><span class="sxs-lookup"><span data-stu-id="7a824-1015">To enable it, set the `EnableWindowsFormsHighDpiAutoResizing` element to `true` in the application configuration (app.config) file:</span></span>

  ```xml
  <appSettings>
      <add key="EnableWindowsFormsHighDpiAutoResizing" value="true" />
  </appSettings>
  ```

- <span data-ttu-id="7a824-1016">**新工作流程功能。**</span><span class="sxs-lookup"><span data-stu-id="7a824-1016">**New workflow feature.**</span></span> <span data-ttu-id="7a824-1017">使用 <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A> 方法 (進而實作 <xref:System.Transactions.IPromotableSinglePhaseNotification> 介面) 的資源管理員可使用新的 <xref:System.Transactions.Transaction.PromoteAndEnlistDurable%2A?displayProperty=nameWithType> 方法來要求下列作業：</span><span class="sxs-lookup"><span data-stu-id="7a824-1017">A resource manager that's using the <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A> method (and therefore implementing the <xref:System.Transactions.IPromotableSinglePhaseNotification> interface) can use the new <xref:System.Transactions.Transaction.PromoteAndEnlistDurable%2A?displayProperty=nameWithType> method to request the following:</span></span>

  - <span data-ttu-id="7a824-1018">將交易提升至 Microsoft 分散式交易協調器 (MSDTC) 交易。</span><span class="sxs-lookup"><span data-stu-id="7a824-1018">Promote the transaction to a Microsoft Distributed Transaction Coordinator (MSDTC) transaction.</span></span>

  - <span data-ttu-id="7a824-1019">以支援單一階段認可的永久性登記 <xref:System.Transactions.IPromotableSinglePhaseNotification> 取代 <xref:System.Transactions.ISinglePhaseNotification>。</span><span class="sxs-lookup"><span data-stu-id="7a824-1019">Replace <xref:System.Transactions.IPromotableSinglePhaseNotification> with an <xref:System.Transactions.ISinglePhaseNotification>, which is a durable enlistment that supports single phase commits.</span></span>

  <span data-ttu-id="7a824-1020">您可以在相同的應用程式網域中完成這些作業，而不需要任何額外的 Unmanaged 程式碼來與 MSDTC 互動以進行提升。</span><span class="sxs-lookup"><span data-stu-id="7a824-1020">This can be done within the same app domain, and doesn't require any extra unmanaged code to interact with MSDTC to perform the promotion.</span></span> <span data-ttu-id="7a824-1021">僅當 <xref:System.Transactions?displayProperty=nameWithType> 對可提升登記未實作之 <xref:System.Transactions.IPromotableSinglePhaseNotification>`Promote` 方法的呼叫未完成時，才會呼叫此新方法。</span><span class="sxs-lookup"><span data-stu-id="7a824-1021">The new method can be called only when there's an outstanding call from <xref:System.Transactions?displayProperty=nameWithType> to the <xref:System.Transactions.IPromotableSinglePhaseNotification>`Promote` method that's implemented by the promotable enlistment.</span></span>

- <span data-ttu-id="7a824-1022">**程式碼剖析改進。**</span><span class="sxs-lookup"><span data-stu-id="7a824-1022">**Profiling improvements.**</span></span> <span data-ttu-id="7a824-1023">下列新的 Unmanaged 程式碼分析 API 提供更強大的程式碼分析功能：</span><span class="sxs-lookup"><span data-stu-id="7a824-1023">The following new unmanaged profiling APIs provide more robust profiling:</span></span>

  - [<span data-ttu-id="7a824-1024">COR_PRF_ASSEMBLY_REFERENCE_INFO 結構</span><span class="sxs-lookup"><span data-stu-id="7a824-1024">COR_PRF_ASSEMBLY_REFERENCE_INFO Structure</span></span>](../unmanaged-api/profiling/cor-prf-assembly-reference-info-structure.md)
  - [<span data-ttu-id="7a824-1025">COR_PRF_HIGH_MONITOR 列舉</span><span class="sxs-lookup"><span data-stu-id="7a824-1025">COR_PRF_HIGH_MONITOR Enumeration</span></span>](../unmanaged-api/profiling/cor-prf-high-monitor-enumeration.md)
  - [<span data-ttu-id="7a824-1026">GetAssemblyReferences 方法</span><span class="sxs-lookup"><span data-stu-id="7a824-1026">GetAssemblyReferences Method</span></span>](../unmanaged-api/profiling/icorprofilercallback6-getassemblyreferences-method.md)
  - [<span data-ttu-id="7a824-1027">GetEventMask2 方法</span><span class="sxs-lookup"><span data-stu-id="7a824-1027">GetEventMask2 Method</span></span>](../unmanaged-api/profiling/icorprofilerinfo5-geteventmask2-method.md)
  - [<span data-ttu-id="7a824-1028">SetEventMask2 方法</span><span class="sxs-lookup"><span data-stu-id="7a824-1028">SetEventMask2 Method</span></span>](../unmanaged-api/profiling/icorprofilerinfo5-seteventmask2-method.md)
  - [<span data-ttu-id="7a824-1029">AddAssemblyReference 方法</span><span class="sxs-lookup"><span data-stu-id="7a824-1029">AddAssemblyReference Method</span></span>](../unmanaged-api/profiling/icorprofilerassemblyreferenceprovider-addassemblyreference-method.md)

  <span data-ttu-id="7a824-1030">之前的 `ICorProfiler` 實作支援相依組件的消極式載入。</span><span class="sxs-lookup"><span data-stu-id="7a824-1030">Previous `ICorProfiler` implementations supported lazy loading of dependent assemblies.</span></span> <span data-ttu-id="7a824-1031">新程式碼分析 API 要求可立即載入分析工具插入的相依組件，而不是在完全初始化應用程式之後才載入。</span><span class="sxs-lookup"><span data-stu-id="7a824-1031">The new profiling APIs require dependent assemblies that are injected by the profiler to be loadable immediately, instead of being loaded after the app is fully initialized.</span></span> <span data-ttu-id="7a824-1032">此變更不會影響現有 `ICorProfiler` API 的使用者。</span><span class="sxs-lookup"><span data-stu-id="7a824-1032">This change doesn't affect users of the existing `ICorProfiler` APIs.</span></span>

- <span data-ttu-id="7a824-1033">**偵錯改進。**</span><span class="sxs-lookup"><span data-stu-id="7a824-1033">**Debugging improvements.**</span></span> <span data-ttu-id="7a824-1034">下列新的 Unmanaged 偵錯 API 提供與分析工具更佳的整合。</span><span class="sxs-lookup"><span data-stu-id="7a824-1034">The following new unmanaged debugging APIs provide better integration with a profiler.</span></span> <span data-ttu-id="7a824-1035">您現在可以存取分析工具插入的中繼資料，並存取偵錯傾印時編譯器 ReJIT 要求所產生的區域變數和程式碼。</span><span class="sxs-lookup"><span data-stu-id="7a824-1035">You can now access metadata inserted by the profiler as well as local variables and code produced by compiler ReJIT requests when dump debugging.</span></span>

  - [<span data-ttu-id="7a824-1036">SetWriteableMetadataUpdateMode 方法</span><span class="sxs-lookup"><span data-stu-id="7a824-1036">SetWriteableMetadataUpdateMode Method</span></span>](../unmanaged-api/debugging/icordebugprocess7-setwriteablemetadataupdatemode-method.md)
  - [<span data-ttu-id="7a824-1037">EnumerateLocalVariablesEx 方法</span><span class="sxs-lookup"><span data-stu-id="7a824-1037">EnumerateLocalVariablesEx Method</span></span>](../unmanaged-api/debugging/icordebugilframe4-enumeratelocalvariablesex-method.md)
  - [<span data-ttu-id="7a824-1038">GetLocalVariableEx 方法</span><span class="sxs-lookup"><span data-stu-id="7a824-1038">GetLocalVariableEx Method</span></span>](../unmanaged-api/debugging/icordebugilframe4-getlocalvariableex-method.md)
  - [<span data-ttu-id="7a824-1039">GetCodeEx 方法</span><span class="sxs-lookup"><span data-stu-id="7a824-1039">GetCodeEx Method</span></span>](../unmanaged-api/debugging/icordebugilframe4-getcodeex-method.md)
  - [<span data-ttu-id="7a824-1040">GetActiveReJitRequestILCode 方法</span><span class="sxs-lookup"><span data-stu-id="7a824-1040">GetActiveReJitRequestILCode Method</span></span>](../unmanaged-api/debugging/icordebugfunction3-getactiverejitrequestilcode-method.md)
  - [<span data-ttu-id="7a824-1041">GetInstrumentedILMap 方法</span><span class="sxs-lookup"><span data-stu-id="7a824-1041">GetInstrumentedILMap Method</span></span>](../unmanaged-api/debugging/icordebugilcode2-getinstrumentedilmap-method.md)

- <span data-ttu-id="7a824-1042">**事件追蹤變更。**</span><span class="sxs-lookup"><span data-stu-id="7a824-1042">**Event tracing changes.**</span></span> <span data-ttu-id="7a824-1043">.NET Framework 4.5.2 可對更大的表面區域進行 Windows 事件追蹤 (ETW) 的跨處理序活動追蹤。</span><span class="sxs-lookup"><span data-stu-id="7a824-1043">.NET Framework 4.5.2 enables out-of-process, Event Tracing for Windows (ETW)-based activity tracing for a larger surface area.</span></span> <span data-ttu-id="7a824-1044">此功能可讓進階電源管理 (APM) 廠商提供輕量型工具，以精確追蹤跨執行緒之個別要求和活動的成本。</span><span class="sxs-lookup"><span data-stu-id="7a824-1044">This enables Advanced Power Management (APM) vendors to provide lightweight tools that accurately track the costs of individual requests and activities that cross threads.</span></span>  <span data-ttu-id="7a824-1045">僅當 ETW 控制器啟用這些事件時，才會引發事件；因此，這些變更不會影響之前撰寫的 ETW 程式碼或停用 ETW 時所執行的程式碼。</span><span class="sxs-lookup"><span data-stu-id="7a824-1045">These events are raised only when ETW controllers enable them; therefore, the changes don't affect previously written ETW code or code that runs with ETW disabled.</span></span>

- <span data-ttu-id="7a824-1046">**升級交易並將它轉換成永久性登記**</span><span class="sxs-lookup"><span data-stu-id="7a824-1046">**Promoting a transaction and converting it to a durable enlistment**</span></span>

  <span data-ttu-id="7a824-1047"><xref:System.Transactions.Transaction.PromoteAndEnlistDurable%2A?displayProperty=nameWithType> 是新加入 .NET Framework 4.5.2 和 4.6 的新 API：</span><span class="sxs-lookup"><span data-stu-id="7a824-1047"><xref:System.Transactions.Transaction.PromoteAndEnlistDurable%2A?displayProperty=nameWithType> is a new API added to .NET Framework 4.5.2 and 4.6:</span></span>

  ```csharp
  [System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name = "FullTrust")]
  public Enlistment PromoteAndEnlistDurable(Guid resourceManagerIdentifier,
                                            IPromotableSinglePhaseNotification promotableNotification,
                                            ISinglePhaseNotification enlistmentNotification,
                                            EnlistmentOptions enlistmentOptions)
  ```

  ```vb
  <System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name:="FullTrust")>
  public Function PromoteAndEnlistDurable(resourceManagerIdentifier As Guid,
                                          promotableNotification As IPromotableSinglePhaseNotification,
                                          enlistmentNotification As ISinglePhaseNotification,
                                          enlistmentOptions As EnlistmentOptions) As Enlistment
  ```

  <span data-ttu-id="7a824-1048">此方法可讓先前由 <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A?displayProperty=nameWithType> 所建立的登錄用來回應 <xref:System.Transactions.ITransactionPromoter.Promote%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="7a824-1048">The method may be used by an enlistment that was previously created by <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A?displayProperty=nameWithType> in response to the <xref:System.Transactions.ITransactionPromoter.Promote%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="7a824-1049">它會要求 `System.Transactions` 將交易升級為 MSDTC 交易，並將可升級登記「轉換」為永久性登記。</span><span class="sxs-lookup"><span data-stu-id="7a824-1049">It asks `System.Transactions` to promote the transaction to an MSDTC transaction and to "convert" the promotable enlistment to a durable enlistment.</span></span> <span data-ttu-id="7a824-1050">這個方法成功完成之後，<xref:System.Transactions.IPromotableSinglePhaseNotification> 介面將不再受 `System.Transactions` 參考，且會將任何未來的通知送至所提供的  <xref:System.Transactions.ISinglePhaseNotification> 介面。</span><span class="sxs-lookup"><span data-stu-id="7a824-1050">After this method completes successfully, the <xref:System.Transactions.IPromotableSinglePhaseNotification> interface will no longer be referenced by `System.Transactions`, and any future notifications will arrive on the provided <xref:System.Transactions.ISinglePhaseNotification> interface.</span></span> <span data-ttu-id="7a824-1051">登記必須做為永久性登記，才可支援交易記錄和復原。</span><span class="sxs-lookup"><span data-stu-id="7a824-1051">The enlistment in question must act as a durable enlistment, supporting transaction logging and recovery.</span></span> <span data-ttu-id="7a824-1052">如需詳細資訊，請參閱 <xref:System.Transactions.Transaction.EnlistDurable%2A?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="7a824-1052">Refer to <xref:System.Transactions.Transaction.EnlistDurable%2A?displayProperty=nameWithType> for details.</span></span> <span data-ttu-id="7a824-1053">此外，登記必須支援 <xref:System.Transactions.ISinglePhaseNotification>。</span><span class="sxs-lookup"><span data-stu-id="7a824-1053">In addition, the enlistment must support <xref:System.Transactions.ISinglePhaseNotification>.</span></span>  <span data-ttu-id="7a824-1054">只有在處理 <xref:System.Transactions.ITransactionPromoter.Promote%2A?displayProperty=nameWithType> 呼叫時，「才」\*\* 可以呼叫此方法。</span><span class="sxs-lookup"><span data-stu-id="7a824-1054">This method can *only* be called while processing an <xref:System.Transactions.ITransactionPromoter.Promote%2A?displayProperty=nameWithType> call.</span></span> <span data-ttu-id="7a824-1055">若否，則會擲回 <xref:System.Transactions.TransactionException> 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="7a824-1055">If that is not the case, a <xref:System.Transactions.TransactionException> exception is thrown.</span></span>

<a name="v451"></a>

## <a name="whats-new-in-net-framework-451"></a><span data-ttu-id="7a824-1056">.NET Framework 4.5.1 中的新功能</span><span class="sxs-lookup"><span data-stu-id="7a824-1056">What's new in .NET Framework 4.5.1</span></span>

<span data-ttu-id="7a824-1057">**2014 年 4 月更新**：</span><span class="sxs-lookup"><span data-stu-id="7a824-1057">**April 2014 updates**:</span></span>

- <span data-ttu-id="7a824-1058">[Visual Studio 2013 Update 2](https://go.microsoft.com/fwlink/p/?LinkId=393658) 包含可攜式類別庫範本的更新，以便針對下列情況提供支援：</span><span class="sxs-lookup"><span data-stu-id="7a824-1058">[Visual Studio 2013 Update 2](https://go.microsoft.com/fwlink/p/?LinkId=393658) includes updates to the Portable Class Library templates to support these scenarios:</span></span>

  - <span data-ttu-id="7a824-1059">您可以使用以 Windows 8.1、Windows Phone 8.1 和 Windows Phone Silverlight 8.1 為目標之可攜式類別庫中的 Windows 執行階段 API。</span><span class="sxs-lookup"><span data-stu-id="7a824-1059">You can use Windows Runtime APIs in portable libraries that target Windows 8.1, Windows Phone 8.1, and Windows Phone Silverlight 8.1.</span></span>

  - <span data-ttu-id="7a824-1060">當您以 Windows 8.1 或 Windows Phone 8.1 為目標時，可將 XAML (Windows.UI.XAML 類別) 加入至可攜式類別庫中。</span><span class="sxs-lookup"><span data-stu-id="7a824-1060">You can include XAML (Windows.UI.XAML types) in portable libraries when you target Windows 8.1 or Windows Phone 8.1.</span></span> <span data-ttu-id="7a824-1061">支援下列 XAML 範本：「空白網頁」、「資源字典」、「樣板化控制項」和「使用者控制項」。</span><span class="sxs-lookup"><span data-stu-id="7a824-1061">The following XAML templates are supported:  Blank Page, Resource Dictionary, Templated Control, and User Control.</span></span>

  - <span data-ttu-id="7a824-1062">您可以建立可攜式 Windows 執行階段元件 (.winmd 檔案)，以便用於以 Windows 8.1 和 Windows Phone 8.1 為目標的市集應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a824-1062">You can create a portable Windows Runtime component (.winmd file) for use in Store apps that target Windows 8.1 and Windows Phone 8.1.</span></span>

  - <span data-ttu-id="7a824-1063">您可以像是可攜式類別庫一樣，重定 Windows 市集或 Windows Phone 市集類別庫的目標。</span><span class="sxs-lookup"><span data-stu-id="7a824-1063">You can retarget a Windows Store or Windows Phone Store class library like a Portable Class Library.</span></span>

  <span data-ttu-id="7a824-1064">如需這些變更的詳細資訊，請參閱[可攜式類別庫](../../standard/cross-platform/cross-platform-development-with-the-portable-class-library.md)。</span><span class="sxs-lookup"><span data-stu-id="7a824-1064">For more information about these changes, see [Portable Class Library](../../standard/cross-platform/cross-platform-development-with-the-portable-class-library.md).</span></span>

- <span data-ttu-id="7a824-1065">.NET Framework 內容集現在包含 .NET Native (用於建置及部署 Windows 應用程式的先行編譯技術) 的文件。</span><span class="sxs-lookup"><span data-stu-id="7a824-1065">The .NET Framework content set now includes documentation for .NET Native, which is a precompilation technology for building and deploying Windows apps.</span></span> <span data-ttu-id="7a824-1066">.NET Native 會將您的應用程式直接編譯為機器碼而不是中繼語言 (IL) 以提升效能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1066">.NET Native compiles your apps directly to native code, rather than to intermediate language (IL), for better performance.</span></span> <span data-ttu-id="7a824-1067">如需詳細資訊，請參閱[使用 .NET Native 編譯應用程式](../net-native/index.md)。</span><span class="sxs-lookup"><span data-stu-id="7a824-1067">For details, see [Compiling Apps with .NET Native](../net-native/index.md).</span></span>

- <span data-ttu-id="7a824-1068">[.NET Framework 參考來源](https://referencesource.microsoft.com/)提供新瀏覽體驗和增強功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1068">The [.NET Framework Reference Source](https://referencesource.microsoft.com/) provides a new browsing experience and enhanced functionality.</span></span> <span data-ttu-id="7a824-1069">您現在可以在線上瀏覽 .NET Framework 原始程式碼、[下載參考](https://referencesource.microsoft.com/download.html)以供離線檢視，並在偵錯時逐步執行原始程式碼 (包含修補程式和更新)。</span><span class="sxs-lookup"><span data-stu-id="7a824-1069">You can now browse through the .NET Framework source code online, [download the reference](https://referencesource.microsoft.com/download.html) for offline viewing, and step through the sources (including patches and updates) during debugging.</span></span> <span data-ttu-id="7a824-1070">如需詳細資訊，請參閱部落格文章：[.NET 參考來源的新風貌 (英文)](https://devblogs.microsoft.com/dotnet/a-new-look-for-net-reference-source/)。</span><span class="sxs-lookup"><span data-stu-id="7a824-1070">For more information, see the blog entry [A new look for .NET Reference Source](https://devblogs.microsoft.com/dotnet/a-new-look-for-net-reference-source/).</span></span>

<span data-ttu-id="7a824-1071">.NET Framework 4.5.1 中基底類別的新功能和增強功能包括：</span><span class="sxs-lookup"><span data-stu-id="7a824-1071">New features and enhancements in the base classes in .NET Framework 4.5.1 include:</span></span>

- <span data-ttu-id="7a824-1072">組件的自動繫結重新導向。</span><span class="sxs-lookup"><span data-stu-id="7a824-1072">Automatic binding redirection for assemblies.</span></span> <span data-ttu-id="7a824-1073">從 Visual Studio 2013 開始，當您編譯以 .NET Framework 4.5.1 為目標的應用程式時，如果您的應用程式或其元件參考相同組件的多個版本，就可能會將繫結重新導向加入至應用程式組態檔。</span><span class="sxs-lookup"><span data-stu-id="7a824-1073">Starting with Visual Studio 2013, when you compile an app that targets the .NET Framework 4.5.1, binding redirects may be added to the app configuration file if your app or its components reference multiple versions of the same assembly.</span></span> <span data-ttu-id="7a824-1074">您也可以對鎖定舊版 .NET Framework 的專案啟用這項功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1074">You can also enable this feature for projects that target older versions of the .NET Framework.</span></span> <span data-ttu-id="7a824-1075">如需詳細資訊，請參閱[操作說明：啟用和停用自動繫結重新導向](../configure-apps/how-to-enable-and-disable-automatic-binding-redirection.md)。</span><span class="sxs-lookup"><span data-stu-id="7a824-1075">For more information, see [How to: Enable and Disable Automatic Binding Redirection](../configure-apps/how-to-enable-and-disable-automatic-binding-redirection.md).</span></span>

- <span data-ttu-id="7a824-1076">可收集診斷資訊，協助開發人員改進伺服器和雲端應用程式效能的功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1076">Ability to collect diagnostics information to help developers improve the performance of server and cloud applications.</span></span> <span data-ttu-id="7a824-1077">如需詳細資訊，請參閱 <xref:System.Diagnostics.Tracing.EventSource.WriteEventWithRelatedActivityId%2A> 類別中的 <xref:System.Diagnostics.Tracing.EventSource.WriteEventWithRelatedActivityIdCore%2A> 和 <xref:System.Diagnostics.Tracing.EventSource> 方法。</span><span class="sxs-lookup"><span data-stu-id="7a824-1077">For more information, see the <xref:System.Diagnostics.Tracing.EventSource.WriteEventWithRelatedActivityId%2A> and <xref:System.Diagnostics.Tracing.EventSource.WriteEventWithRelatedActivityIdCore%2A> methods in the <xref:System.Diagnostics.Tracing.EventSource> class.</span></span>

- <span data-ttu-id="7a824-1078">可在記憶體回收期間明確壓縮大型物件堆積 (LOH) 的功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1078">Ability to explicitly compact the large object heap (LOH) during garbage collection.</span></span> <span data-ttu-id="7a824-1079">如需詳細資訊，請參閱 <xref:System.Runtime.GCSettings.LargeObjectHeapCompactionMode%2A?displayProperty=nameWithType> 屬性 (Property)。</span><span class="sxs-lookup"><span data-stu-id="7a824-1079">For more information, see the <xref:System.Runtime.GCSettings.LargeObjectHeapCompactionMode%2A?displayProperty=nameWithType> property.</span></span>

- <span data-ttu-id="7a824-1080">其他效能改進功能包括 ASP.NET 應用程式暫止、多核心 JIT 改進功能，以及 .NET Framework 更新後應用程式更快速啟動。</span><span class="sxs-lookup"><span data-stu-id="7a824-1080">Additional performance improvements such as ASP.NET app suspension, multi-core JIT improvements, and faster app startup after a .NET Framework update.</span></span> <span data-ttu-id="7a824-1081">如需詳細資訊，請參閱 [.NET Framework 4.5.1 公告 (英文)](https://devblogs.microsoft.com/dotnet/announcing-the-net-framework-4-5-1-preview/)和 [ASP.NET 應用程式暫止 (英文)](https://devblogs.microsoft.com/dotnet/asp-net-app-suspend-responsive-shared-net-web-hosting/) 部落格文章。</span><span class="sxs-lookup"><span data-stu-id="7a824-1081">For details, see the [.NET Framework 4.5.1 announcement](https://devblogs.microsoft.com/dotnet/announcing-the-net-framework-4-5-1-preview/) and the [ASP.NET app suspend](https://devblogs.microsoft.com/dotnet/asp-net-app-suspend-responsive-shared-net-web-hosting/) blog post.</span></span>

<span data-ttu-id="7a824-1082">Windows Forms 的增強功能包括：</span><span class="sxs-lookup"><span data-stu-id="7a824-1082">Improvements to Windows Forms include:</span></span>

- <span data-ttu-id="7a824-1083">調整 Windows Forms 控制項的大小。</span><span class="sxs-lookup"><span data-stu-id="7a824-1083">Resizing in Windows Forms controls.</span></span> <span data-ttu-id="7a824-1084">您可以透過在應用程式的應用程式組態檔中選擇加入一個項目，使用系統 DPI 設定來調整控制項的元件大小 (例如屬性方格中出現的圖示)。</span><span class="sxs-lookup"><span data-stu-id="7a824-1084">You can use the system DPI setting to resize components of controls (for example, the icons that appear in a property grid) by opting in with an entry in the application configuration file (app.config) for your app.</span></span> <span data-ttu-id="7a824-1085">目前支援此功能的 Windows Forms 控制項如下：</span><span class="sxs-lookup"><span data-stu-id="7a824-1085">This feature is currently supported in the following Windows Forms controls:</span></span>

  - <xref:System.Windows.Forms.PropertyGrid>
  - <xref:System.Windows.Forms.TreeView>
  - <span data-ttu-id="7a824-1086"><xref:System.Windows.Forms.DataGridView> 的某些部分 (請參閱 [4.5.2 的新功能](#v452)以了解其他支援的控制項)</span><span class="sxs-lookup"><span data-stu-id="7a824-1086">Some aspects of the <xref:System.Windows.Forms.DataGridView> (see [new features in 4.5.2](#v452) for additional controls supported)</span></span>

  <span data-ttu-id="7a824-1087">若要啟用這項功能，請將新的專案新增 \<appSettings> 至設定檔 ( # A0) ，然後將 `EnableWindowsFormsHighDpiAutoResizing` 元素設定為 `true` ：</span><span class="sxs-lookup"><span data-stu-id="7a824-1087">To enable this feature, add a new \<appSettings> element to the configuration file (app.config) and set the `EnableWindowsFormsHighDpiAutoResizing` element to `true`:</span></span>

  ```xml
  <appSettings>
      <add key="EnableWindowsFormsHighDpiAutoResizing" value="true" />
  </appSettings>
  ```

<span data-ttu-id="7a824-1088">在 Visual Studio 2013 中對您的 .NET Framework 應用程式進行偵錯時的改進功能包括：</span><span class="sxs-lookup"><span data-stu-id="7a824-1088">Improvements when debugging your .NET Framework apps in Visual Studio 2013 include:</span></span>

- <span data-ttu-id="7a824-1089">在 Visual Studio Debugger 中傳回值。</span><span class="sxs-lookup"><span data-stu-id="7a824-1089">Return values in the Visual Studio debugger.</span></span> <span data-ttu-id="7a824-1090">當您在 Visual Studio 2013 中對 Managed 應用程式進行偵錯時，[自動變數] 視窗會顯示方法的傳回類型和值。</span><span class="sxs-lookup"><span data-stu-id="7a824-1090">When you debug a managed app in Visual Studio 2013, the Autos window displays return types and values for methods.</span></span> <span data-ttu-id="7a824-1091">這項資訊適用於桌面、Windows 市集和 Windows Phone 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a824-1091">This information is available for desktop, Windows Store, and Windows Phone apps.</span></span> <span data-ttu-id="7a824-1092">如需詳細資訊，請參閱[檢查方法呼叫的傳回值](/previous-versions/visualstudio/visual-studio-2013/dn323257(v=vs.120))。</span><span class="sxs-lookup"><span data-stu-id="7a824-1092">For more information, see [Examine return values of method calls](/previous-versions/visualstudio/visual-studio-2013/dn323257(v=vs.120)).</span></span>

- <span data-ttu-id="7a824-1093">64 位元應用程式的 [編輯後繼續] 功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1093">Edit and Continue for 64-bit apps.</span></span> <span data-ttu-id="7a824-1094">Visual Studio 2013 對傳統型、Windows 市集和 Windows Phone 的 64 位元 Managed 應用程式支援「編輯後繼續」功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1094">Visual Studio 2013 supports the Edit and Continue feature for 64-bit managed apps for desktop, Windows Store, and Windows Phone.</span></span> <span data-ttu-id="7a824-1095">對 32 位元和 64 位元應用程式的現有限制仍然有效 (請參閱[支援的程式碼變更 (C#)](/visualstudio/debugger/supported-code-changes-csharp) 文章的最後一節)。</span><span class="sxs-lookup"><span data-stu-id="7a824-1095">The existing limitations remain in effect for both 32-bit and 64-bit apps (see the last section of the [Supported Code Changes (C#)](/visualstudio/debugger/supported-code-changes-csharp) article).</span></span>

- <span data-ttu-id="7a824-1096">非同步感知偵錯。</span><span class="sxs-lookup"><span data-stu-id="7a824-1096">Async-aware debugging.</span></span> <span data-ttu-id="7a824-1097">為了在 Visual Studio 2013 中更容易對非同步應用程式進行偵錯，呼叫堆疊會隱藏編譯器提供的基礎結構程式碼來支援非同步程式設計，以及提供邏輯父框架中的鏈結，讓您可以更清楚地了解邏輯程式執行的方式。</span><span class="sxs-lookup"><span data-stu-id="7a824-1097">To make it easier to debug asynchronous apps in Visual Studio 2013, the call stack hides the infrastructure code provided by compilers to support asynchronous programming, and also chains in logical parent frames so you can follow logical program execution more clearly.</span></span> <span data-ttu-id="7a824-1098">[工作] 視窗會取代 [平行工作] 視窗，並顯示與特定中斷點相關的工作，同時也會顯示應用程式中目前為作用中或已排程的任何其他工作。</span><span class="sxs-lookup"><span data-stu-id="7a824-1098">A Tasks window replaces the Parallel Tasks window and displays tasks that relate to a particular breakpoint, and also displays any other tasks that are currently active or scheduled in the app.</span></span> <span data-ttu-id="7a824-1099">您可以在 [.NET Framework 4.5.1 公告 (英文)](https://devblogs.microsoft.com/dotnet/announcing-the-net-framework-4-5-1-preview/)的＜Async-aware debugging＞ (非同步感知偵錯) 一節中，閱讀此功能的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7a824-1099">You can read about this feature in the "Async-aware debugging" section of the [.NET Framework 4.5.1 announcement](https://devblogs.microsoft.com/dotnet/announcing-the-net-framework-4-5-1-preview/).</span></span>

- <span data-ttu-id="7a824-1100">對 Windows 執行階段元件提供更佳的例外狀況支援。</span><span class="sxs-lookup"><span data-stu-id="7a824-1100">Better exception support for Windows Runtime components.</span></span> <span data-ttu-id="7a824-1101">在 Windows 8.1 中，Windows 市集應用程式所引發的例外狀況會保留造成例外狀況之錯誤的資訊，甚至跨語言界限。</span><span class="sxs-lookup"><span data-stu-id="7a824-1101">In Windows 8.1, exceptions that arise from Windows Store apps preserve information about the error that caused the exception, even across language boundaries.</span></span> <span data-ttu-id="7a824-1102">您可以在 [.NET Framework 4.5.1 公告](https://devblogs.microsoft.com/dotnet/announcing-the-net-framework-4-5-1-preview/)的＜Windows 市集應用程式開發＞一節中，閱讀這項功能的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7a824-1102">You can read about this feature in the "Windows Store app development" section of the [.NET Framework 4.5.1 announcement](https://devblogs.microsoft.com/dotnet/announcing-the-net-framework-4-5-1-preview/).</span></span>

<span data-ttu-id="7a824-1103">從 Visual Studio 2013 開始，您可以使用 [Managed 特性指引最佳化工具 (Mpgo.exe)](../tools/mpgo-exe-managed-profile-guided-optimization-tool.md)，針對 Windows 8.x 市集應用程式和傳統型應用程式進行最佳化。</span><span class="sxs-lookup"><span data-stu-id="7a824-1103">Starting with Visual Studio 2013, you can use the [Managed Profile Guided Optimization Tool (Mpgo.exe)](../tools/mpgo-exe-managed-profile-guided-optimization-tool.md) to optimize Windows 8.x Store apps as well as desktop apps.</span></span>

<span data-ttu-id="7a824-1104">若要了解 ASP.NET 4.5.1 的新功能，請參閱[適用於 Visual Studio 2013 的 ASP.NET 及 Web 工具版本資訊](/aspnet/visual-studio/overview/2013/release-notes)。</span><span class="sxs-lookup"><span data-stu-id="7a824-1104">For new features in ASP.NET 4.5.1, see [ASP.NET and Web Tools for Visual Studio 2013 Release Notes](/aspnet/visual-studio/overview/2013/release-notes).</span></span>

<a name="v45"></a>

## <a name="whats-new-in-net-framework-45"></a><span data-ttu-id="7a824-1105">.NET Framework 4.5 中的新功能</span><span class="sxs-lookup"><span data-stu-id="7a824-1105">What's new in .NET Framework 4.5</span></span>

### <a name="base-classes"></a><span data-ttu-id="7a824-1106">基底類別</span><span class="sxs-lookup"><span data-stu-id="7a824-1106">Base classes</span></span>

- <span data-ttu-id="7a824-1107">可透過在部署期間偵測及關閉 .NET Framework 4 應用程式的方式，減少系統重新啟動次數的功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1107">Ability to reduce system restarts by detecting and closing .NET Framework 4 applications during deployment.</span></span> <span data-ttu-id="7a824-1108">請參閱[在 .NET Framework 4.5 安裝期間減少系統重新啟動的次數](../deployment/reducing-system-restarts.md)。</span><span class="sxs-lookup"><span data-stu-id="7a824-1108">See [Reducing System Restarts During .NET Framework 4.5 Installations](../deployment/reducing-system-restarts.md).</span></span>

- <span data-ttu-id="7a824-1109">在 64 位元平台上支援大於 2 GB 的陣列。</span><span class="sxs-lookup"><span data-stu-id="7a824-1109">Support for arrays that are larger than 2 gigabytes (GB) on 64-bit platforms.</span></span> <span data-ttu-id="7a824-1110">這項功能可以在應用程式組態檔中啟用。</span><span class="sxs-lookup"><span data-stu-id="7a824-1110">This feature can be enabled in the application configuration file.</span></span> <span data-ttu-id="7a824-1111">請參閱[ \<gcAllowVeryLargeObjects> 元素](../configure-apps/file-schema/runtime/gcallowverylargeobjects-element.md)，這也會列出物件大小和陣列大小的其他限制。</span><span class="sxs-lookup"><span data-stu-id="7a824-1111">See the [\<gcAllowVeryLargeObjects> element](../configure-apps/file-schema/runtime/gcallowverylargeobjects-element.md), which also lists other restrictions on object size and array size.</span></span>

- <span data-ttu-id="7a824-1112">透過伺服器的背景記憶體回收改善效能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1112">Better performance through background garbage collection for servers.</span></span> <span data-ttu-id="7a824-1113">當您在 .NET Framework 4.5 中使用伺服器記憶體回收時，背景記憶體回收會自動啟用。</span><span class="sxs-lookup"><span data-stu-id="7a824-1113">When you use server garbage collection in the .NET Framework 4.5, background garbage collection is automatically enabled.</span></span> <span data-ttu-id="7a824-1114">請參閱[記憶體回收的基本概念](../../standard/garbage-collection/fundamentals.md)主題的＜背景伺服器記憶體回收＞一節。</span><span class="sxs-lookup"><span data-stu-id="7a824-1114">See the Background Server Garbage Collection section of the [Fundamentals of Garbage Collection](../../standard/garbage-collection/fundamentals.md) topic.</span></span>

- <span data-ttu-id="7a824-1115">背景 Just-in-Time (JIT) 編譯，它可在多核心處理器上選擇性提供，以改善應用程式效能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1115">Background just-in-time (JIT) compilation, which is optionally available on multi-core processors to improve application performance.</span></span> <span data-ttu-id="7a824-1116">請參閱 <xref:System.Runtime.ProfileOptimization>。</span><span class="sxs-lookup"><span data-stu-id="7a824-1116">See <xref:System.Runtime.ProfileOptimization>.</span></span>

- <span data-ttu-id="7a824-1117">能夠限制正則運算式引擎在超時之前將嘗試解析正則運算式的時間長度。請參閱 <xref:System.Text.RegularExpressions.Regex.MatchTimeout%2A?displayProperty=nameWithType> 屬性。</span><span class="sxs-lookup"><span data-stu-id="7a824-1117">Ability to limit how long the regular expression engine will attempt to resolve a regular expression before it times out. See the <xref:System.Text.RegularExpressions.Regex.MatchTimeout%2A?displayProperty=nameWithType> property.</span></span>

- <span data-ttu-id="7a824-1118">可定義應用程式定義域之預設文化特性的功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1118">Ability to define the default culture for an application domain.</span></span> <span data-ttu-id="7a824-1119">請參閱 <xref:System.Globalization.CultureInfo> 類別。</span><span class="sxs-lookup"><span data-stu-id="7a824-1119">See the <xref:System.Globalization.CultureInfo> class.</span></span>

- <span data-ttu-id="7a824-1120">對 Unicode (UTF-16) 編碼的主控台支援。</span><span class="sxs-lookup"><span data-stu-id="7a824-1120">Console support for Unicode (UTF-16) encoding.</span></span> <span data-ttu-id="7a824-1121">請參閱 <xref:System.Console> 類別。</span><span class="sxs-lookup"><span data-stu-id="7a824-1121">See the <xref:System.Console> class.</span></span>

- <span data-ttu-id="7a824-1122">支援文化特性字串順序和比較資料的版本控制。</span><span class="sxs-lookup"><span data-stu-id="7a824-1122">Support for versioning of cultural string ordering and comparison data.</span></span> <span data-ttu-id="7a824-1123">請參閱 <xref:System.Globalization.SortVersion> 類別。</span><span class="sxs-lookup"><span data-stu-id="7a824-1123">See the <xref:System.Globalization.SortVersion> class.</span></span>

- <span data-ttu-id="7a824-1124">改善擷取資源時的效能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1124">Better performance when retrieving resources.</span></span> <span data-ttu-id="7a824-1125">請參閱[封裝和部署資源](../resources/packaging-and-deploying-resources-in-desktop-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="7a824-1125">See [Packaging and Deploying Resources](../resources/packaging-and-deploying-resources-in-desktop-apps.md).</span></span>

- <span data-ttu-id="7a824-1126">改善 Zip 壓縮，縮減壓縮檔的大小。</span><span class="sxs-lookup"><span data-stu-id="7a824-1126">Zip compression improvements to reduce the size of a compressed file.</span></span> <span data-ttu-id="7a824-1127">請參閱 <xref:System.IO.Compression?displayProperty=nameWithType> 命名空間。</span><span class="sxs-lookup"><span data-stu-id="7a824-1127">See the <xref:System.IO.Compression?displayProperty=nameWithType> namespace.</span></span>

- <span data-ttu-id="7a824-1128">可透過 <xref:System.Reflection.Context.CustomReflectionContext> 類別自訂反映內容以覆寫預設反映行為的功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1128">Ability to customize a reflection context to override default reflection behavior through the <xref:System.Reflection.Context.CustomReflectionContext> class.</span></span>

- <span data-ttu-id="7a824-1129">在 Windows 8 上使用類別時，在應用程式中支援2008版的國際化功能變數名稱 (IDNA) 標準 <xref:System.Globalization.IdnMapping?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="7a824-1129">Support for the 2008 version of the Internationalized Domain Names in Applications (IDNA) standard when the <xref:System.Globalization.IdnMapping?displayProperty=nameWithType> class is used  on Windows 8.</span></span>

- <span data-ttu-id="7a824-1130">將字串比較作業委派給作業系統，該字串比較會在 Windows 8 上使用 .NET Framework 時實作 Unicode 6.0。</span><span class="sxs-lookup"><span data-stu-id="7a824-1130">Delegation of string comparison to the operating system, which implements Unicode 6.0, when the .NET Framework is used on Windows 8.</span></span> <span data-ttu-id="7a824-1131">在其他平台上執行時，.NET Framework 會包含自己的字串比較資料 (該資料會實作 Unicode 5.x)。</span><span class="sxs-lookup"><span data-stu-id="7a824-1131">When running on other platforms, the .NET Framework includes its own string comparison data, which implements Unicode 5.x.</span></span> <span data-ttu-id="7a824-1132">請參閱 <xref:System.String> 類別以及 <xref:System.Globalization.SortVersion> 類別的＜備註＞一節。</span><span class="sxs-lookup"><span data-stu-id="7a824-1132">See the <xref:System.String> class and the Remarks section of the <xref:System.Globalization.SortVersion> class.</span></span>

- <span data-ttu-id="7a824-1133">可用每個應用程式定義域做為基準，計算字串之雜湊碼的功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1133">Ability to compute the hash codes for strings on a per application domain basis.</span></span> <span data-ttu-id="7a824-1134">請參閱[ \<UseRandomizedStringHashAlgorithm> 元素](../configure-apps/file-schema/runtime/userandomizedstringhashalgorithm-element.md)。</span><span class="sxs-lookup"><span data-stu-id="7a824-1134">See [\<UseRandomizedStringHashAlgorithm> Element](../configure-apps/file-schema/runtime/userandomizedstringhashalgorithm-element.md).</span></span>

- <span data-ttu-id="7a824-1135">類型反映支援在 <xref:System.Type> 和 <xref:System.Reflection.TypeInfo> 類別之間分割。</span><span class="sxs-lookup"><span data-stu-id="7a824-1135">Type reflection support split between <xref:System.Type> and <xref:System.Reflection.TypeInfo> classes.</span></span> <span data-ttu-id="7a824-1136">請參閱[適用於 Windows 市集應用程式之 .NET Framework 中的反映](../reflection-and-codedom/reflection-for-windows-store-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="7a824-1136">See [Reflection in the .NET Framework for Windows Store Apps](../reflection-and-codedom/reflection-for-windows-store-apps.md).</span></span>

### <a name="managed-extensibility-framework-mef"></a><span data-ttu-id="7a824-1137">Managed Extensibility Framework (MEF)</span><span class="sxs-lookup"><span data-stu-id="7a824-1137">Managed Extensibility Framework (MEF)</span></span>

<span data-ttu-id="7a824-1138">在 .NET Framework 4.5 中，Managed Extensibility Framework (MEF) 提供下列新功能：</span><span class="sxs-lookup"><span data-stu-id="7a824-1138">In the .NET Framework 4.5, the Managed Extensibility Framework (MEF) provides the following new features:</span></span>

- <span data-ttu-id="7a824-1139">支援泛型類型。</span><span class="sxs-lookup"><span data-stu-id="7a824-1139">Support for generic types.</span></span>

- <span data-ttu-id="7a824-1140">以慣例為基礎的程式設計模型，可讓您依命名慣例而非屬性建立組件。</span><span class="sxs-lookup"><span data-stu-id="7a824-1140">Convention-based programming model that enables you to create parts based on naming conventions rather than attributes.</span></span>

- <span data-ttu-id="7a824-1141">多個範圍。</span><span class="sxs-lookup"><span data-stu-id="7a824-1141">Multiple scopes.</span></span>

- <span data-ttu-id="7a824-1142">可以在建立 Windows 8.x 市集應用程式時使用的 MEF 子集。</span><span class="sxs-lookup"><span data-stu-id="7a824-1142">A subset of MEF that you can use when you create Windows 8.x Store apps.</span></span> <span data-ttu-id="7a824-1143">您可透過 NuGet Gallery 取得這個子集的[可下載套件](https://www.nuget.org/packages/Microsoft.Composition)。</span><span class="sxs-lookup"><span data-stu-id="7a824-1143">This subset is available as a [downloadable package](https://www.nuget.org/packages/Microsoft.Composition) from the NuGet Gallery.</span></span> <span data-ttu-id="7a824-1144">若要安裝套件，請在 Visual Studio 中開啟您的專案，從 [專案]\*\*\*\* 功能表中選擇 [管理 NuGet 套件]\*\*\*\*，並於線上搜尋 `Microsoft.Composition` 套件。</span><span class="sxs-lookup"><span data-stu-id="7a824-1144">To install the package, open your project in Visual Studio, choose **Manage NuGet Packages** from the **Project** menu, and search online for the `Microsoft.Composition` package.</span></span>

<span data-ttu-id="7a824-1145">如需詳細資訊，請參閱 [Managed Extensibility Framework (MEF)](../mef/index.md)。</span><span class="sxs-lookup"><span data-stu-id="7a824-1145">For more information, see [Managed Extensibility Framework (MEF)](../mef/index.md).</span></span>

### <a name="asynchronous-file-operations"></a><span data-ttu-id="7a824-1146">非同步檔案作業</span><span class="sxs-lookup"><span data-stu-id="7a824-1146">Asynchronous file operations</span></span>

<span data-ttu-id="7a824-1147">在 .NET Framework 4.5 中，C# 和 Visual Basic 語言已加入新的非同步功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1147">In the .NET Framework 4.5, new asynchronous features were added to the C# and Visual Basic languages.</span></span> <span data-ttu-id="7a824-1148">這些功能會加入執行非同步作業的工作模型。</span><span class="sxs-lookup"><span data-stu-id="7a824-1148">These features add a task-based model for performing asynchronous operations.</span></span> <span data-ttu-id="7a824-1149">若要使用這個全新的模型，請使用 I/O 類別中的非同步方法。</span><span class="sxs-lookup"><span data-stu-id="7a824-1149">To use this new model, use the asynchronous methods in the I/O classes.</span></span> <span data-ttu-id="7a824-1150">請參閱[非同步檔案 I/O](../../standard/io/asynchronous-file-i-o.md)。</span><span class="sxs-lookup"><span data-stu-id="7a824-1150">See [Asynchronous File I/O](../../standard/io/asynchronous-file-i-o.md).</span></span>

<a name="tools"></a>

### <a name="tools"></a><span data-ttu-id="7a824-1151">工具</span><span class="sxs-lookup"><span data-stu-id="7a824-1151">Tools</span></span>

<span data-ttu-id="7a824-1152">在 .NET Framework 4.5 中，資源檔產生器 (Resgen.exe) 可讓您從 .NET Framework 組件中內嵌的 .resources 檔案建立 .resw 檔案，以供 Windows 8.x 市集應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="7a824-1152">In the .NET Framework 4.5, Resource File Generator (Resgen.exe) enables you to create a .resw file for use in Windows 8.x Store apps from a .resources file embedded in a .NET Framework assembly.</span></span> <span data-ttu-id="7a824-1153">如需詳細資訊，請參閱 [Resgen.exe (資源檔產生器)](../tools/resgen-exe-resource-file-generator.md)。</span><span class="sxs-lookup"><span data-stu-id="7a824-1153">For more information, see [Resgen.exe (Resource File Generator)](../tools/resgen-exe-resource-file-generator.md).</span></span>

<span data-ttu-id="7a824-1154">Managed 特性指引最佳化 (Mpgo.exe) 可讓您藉由最佳化原生映像組件，改善應用程式啟動時間、記憶體使用量 (工作集大小) 和輸送量。</span><span class="sxs-lookup"><span data-stu-id="7a824-1154">Managed Profile Guided Optimization (Mpgo.exe) enables you to improve application startup time, memory utilization (working set size), and throughput by optimizing native image assemblies.</span></span> <span data-ttu-id="7a824-1155">命令列工具會產生原生映像應用程式組件的設定檔資料。</span><span class="sxs-lookup"><span data-stu-id="7a824-1155">The command-line tool generates profile data for native image application assemblies.</span></span> <span data-ttu-id="7a824-1156">請參閱 [Mpgo.exe (Managed 特性指引最佳化工具)](../tools/mpgo-exe-managed-profile-guided-optimization-tool.md)。</span><span class="sxs-lookup"><span data-stu-id="7a824-1156">See [Mpgo.exe (Managed Profile Guided Optimization Tool)](../tools/mpgo-exe-managed-profile-guided-optimization-tool.md).</span></span> <span data-ttu-id="7a824-1157">從 Visual Studio 2013 開始，您可以使用 Mpgo.exe 針對 Windows 8.x 市集應用程式和傳統型應用程式進行最佳化。</span><span class="sxs-lookup"><span data-stu-id="7a824-1157">Starting with Visual Studio 2013, you can use Mpgo.exe to optimize Windows 8.x Store apps as well as desktop apps.</span></span>

<a name="parallel"></a>

### <a name="parallel-computing"></a><span data-ttu-id="7a824-1158">平行運算</span><span class="sxs-lookup"><span data-stu-id="7a824-1158">Parallel computing</span></span>

<span data-ttu-id="7a824-1159">.NET Framework 4.5 針對平行計算提供許多新功能和改進功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1159">The .NET Framework 4.5 provides several new features and improvements for parallel computing.</span></span> <span data-ttu-id="7a824-1160">這些功能包括提升效能、增強控制、改善非同步程式設計的支援、全新的資料流程程式庫，以及改善平行偵錯與效能分析的支援。</span><span class="sxs-lookup"><span data-stu-id="7a824-1160">These include improved performance, increased control, improved support for asynchronous programming, a new dataflow library, and improved support for parallel debugging and performance analysis.</span></span> <span data-ttu-id="7a824-1161">請參閱使用 .NET blog 進行平行程式設計時，.NET 4.5 中平行處理原則的 [新功能](https://devblogs.microsoft.com/pfxteam/whats-new-for-parallelism-in-net-4-5/) 。</span><span class="sxs-lookup"><span data-stu-id="7a824-1161">See the entry [What's New for Parallelism in .NET 4.5](https://devblogs.microsoft.com/pfxteam/whats-new-for-parallelism-in-net-4-5/) in the Parallel Programming with .NET blog.</span></span>

<a name="web"></a>

### <a name="web"></a><span data-ttu-id="7a824-1162">Web</span><span class="sxs-lookup"><span data-stu-id="7a824-1162">Web</span></span>

<span data-ttu-id="7a824-1163">ASP.NET 4.5 和 4.5.1 加入了 Web Forms、WebSocket 支援、非同步處理常式、效能增強功能及許多其他功能的模型繫結。</span><span class="sxs-lookup"><span data-stu-id="7a824-1163">ASP.NET 4.5 and 4.5.1 add model binding for Web Forms, WebSocket support, asynchronous handlers, performance enhancements, and many other features.</span></span> <span data-ttu-id="7a824-1164">如需詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="7a824-1164">For more information, see the following resources:</span></span>

- <span data-ttu-id="7a824-1165">[ASP.NET 4.5 與 Visual Studio 2012](/previous-versions/aspnet/hh420390(v=vs.110))</span><span class="sxs-lookup"><span data-stu-id="7a824-1165">[ASP.NET 4.5 and Visual Studio 2012](/previous-versions/aspnet/hh420390(v=vs.110))</span></span>

- [<span data-ttu-id="7a824-1166">適用於 Visual Studio 2013 的 ASP.NET 和 Web 工具版本資訊</span><span class="sxs-lookup"><span data-stu-id="7a824-1166">ASP.NET and Web Tools for Visual Studio 2013 Release Notes</span></span>](/aspnet/visual-studio/overview/2013/release-notes)

### <a name="networking"></a><span data-ttu-id="7a824-1167">網路功能<a name="networking"></a></span><span class="sxs-lookup"><span data-stu-id="7a824-1167">Networking <a name="networking"></a></span></span>

<span data-ttu-id="7a824-1168">.NET Framework 4.5 為 HTTP 應用程式提供新的程式設計介面。</span><span class="sxs-lookup"><span data-stu-id="7a824-1168">The .NET Framework 4.5 provides a new programming interface for HTTP applications.</span></span> <span data-ttu-id="7a824-1169">如需詳細資訊，請參閱新的 <xref:System.Net.Http?displayProperty=nameWithType> 和 <xref:System.Net.Http.Headers?displayProperty=nameWithType> 命名空間。</span><span class="sxs-lookup"><span data-stu-id="7a824-1169">For more information, see the new <xref:System.Net.Http?displayProperty=nameWithType> and <xref:System.Net.Http.Headers?displayProperty=nameWithType> namespaces.</span></span>

<span data-ttu-id="7a824-1170">另外還包括對新的程式設計介面的支援，可使用現有的 <xref:System.Net.HttpListener> 和相關類別接受 WebSocket 連接並進行互動。</span><span class="sxs-lookup"><span data-stu-id="7a824-1170">Support is also included for a new programming interface for accepting and interacting with a WebSocket connection by using the existing <xref:System.Net.HttpListener> and related classes.</span></span> <span data-ttu-id="7a824-1171">如需詳細資訊，請參閱新的 <xref:System.Net.WebSockets> 命名空間和 <xref:System.Net.HttpListener> 類別。</span><span class="sxs-lookup"><span data-stu-id="7a824-1171">For more information, see the new <xref:System.Net.WebSockets> namespace and the <xref:System.Net.HttpListener> class.</span></span>

<span data-ttu-id="7a824-1172">此外，.NET Framework 4.5 還包括下列網路功能改良：</span><span class="sxs-lookup"><span data-stu-id="7a824-1172">In addition, the .NET Framework 4.5 includes the following networking improvements:</span></span>

- <span data-ttu-id="7a824-1173">符合 RFC 標準的 URI 支援。</span><span class="sxs-lookup"><span data-stu-id="7a824-1173">RFC-compliant URI support.</span></span> <span data-ttu-id="7a824-1174">如需詳細資訊，請參閱 <xref:System.Uri> 和相關類別。</span><span class="sxs-lookup"><span data-stu-id="7a824-1174">For more information, see <xref:System.Uri> and related classes.</span></span>

- <span data-ttu-id="7a824-1175">支援國際化網域名稱 (IDN) 剖析。</span><span class="sxs-lookup"><span data-stu-id="7a824-1175">Support for Internationalized Domain Name (IDN) parsing.</span></span> <span data-ttu-id="7a824-1176">如需詳細資訊，請參閱 <xref:System.Uri> 和相關類別。</span><span class="sxs-lookup"><span data-stu-id="7a824-1176">For more information, see <xref:System.Uri> and related classes.</span></span>

- <span data-ttu-id="7a824-1177">支援電子郵件地址國際化 (EAI)。</span><span class="sxs-lookup"><span data-stu-id="7a824-1177">Support for Email Address Internationalization (EAI).</span></span> <span data-ttu-id="7a824-1178">如需詳細資訊，請參閱 <xref:System.Net.Mail>。</span><span class="sxs-lookup"><span data-stu-id="7a824-1178">For more information, see the <xref:System.Net.Mail> namespace.</span></span>

- <span data-ttu-id="7a824-1179">改進的 IPv6 支援。</span><span class="sxs-lookup"><span data-stu-id="7a824-1179">Improved IPv6 support.</span></span> <span data-ttu-id="7a824-1180">如需詳細資訊，請參閱 <xref:System.Net.NetworkInformation>。</span><span class="sxs-lookup"><span data-stu-id="7a824-1180">For more information, see the <xref:System.Net.NetworkInformation> namespace.</span></span>

- <span data-ttu-id="7a824-1181">雙重模式通訊端支援。</span><span class="sxs-lookup"><span data-stu-id="7a824-1181">Dual-mode socket support.</span></span> <span data-ttu-id="7a824-1182">如需詳細資訊，請參閱 <xref:System.Net.Sockets.Socket> 和 <xref:System.Net.Sockets.TcpListener> 類別。</span><span class="sxs-lookup"><span data-stu-id="7a824-1182">For more information, see the <xref:System.Net.Sockets.Socket> and <xref:System.Net.Sockets.TcpListener> classes.</span></span>

<a name="client"></a>

### <a name="windows-presentation-foundation-wpf"></a><span data-ttu-id="7a824-1183">Windows Presentation Foundation (WPF)</span><span class="sxs-lookup"><span data-stu-id="7a824-1183">Windows Presentation Foundation (WPF)</span></span>

<span data-ttu-id="7a824-1184">在 .NET Framework 4.5 中，Windows Presentation Foundation (WPF) 包含下列領域的變更與改進功能：</span><span class="sxs-lookup"><span data-stu-id="7a824-1184">In the .NET Framework 4.5, Windows Presentation Foundation (WPF) contains changes and improvements in the following areas:</span></span>

- <span data-ttu-id="7a824-1185">新的 <xref:System.Windows.Controls.Ribbon.Ribbon> 控制項可以讓您實作功能區使用者介面，其中裝載了 [快速存取工具列]、[應用程式功能表] 及索引標籤。</span><span class="sxs-lookup"><span data-stu-id="7a824-1185">The new <xref:System.Windows.Controls.Ribbon.Ribbon> control, which enables you to implement a ribbon user interface that hosts a Quick Access Toolbar, Application Menu, and tabs.</span></span>

- <span data-ttu-id="7a824-1186">新的 <xref:System.ComponentModel.INotifyDataErrorInfo> 介面支援同步和非同步資料驗證。</span><span class="sxs-lookup"><span data-stu-id="7a824-1186">The new <xref:System.ComponentModel.INotifyDataErrorInfo> interface, which supports synchronous and asynchronous data validation.</span></span>

- <span data-ttu-id="7a824-1187"><xref:System.Windows.Controls.VirtualizingPanel> 和 <xref:System.Windows.Threading.Dispatcher> 類別的新功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1187">New features for the <xref:System.Windows.Controls.VirtualizingPanel> and <xref:System.Windows.Threading.Dispatcher> classes.</span></span>

- <span data-ttu-id="7a824-1188">改善顯示大型群組資料集合時的效能，以及透過在非 UI 執行緒上存取集合提升效能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1188">Improved performance when displaying large sets of grouped data, and by accessing collections on non-UI threads.</span></span>

- <span data-ttu-id="7a824-1189">靜態屬性的資料繫結、實作 <xref:System.Reflection.ICustomTypeProvider> 介面之自訂類型的資料繫結，以及從繫結運算式擷取資料繫結資訊。</span><span class="sxs-lookup"><span data-stu-id="7a824-1189">Data binding to static properties, data binding to custom types that implement the <xref:System.Reflection.ICustomTypeProvider> interface, and retrieval of data binding information from a binding expression.</span></span>

- <span data-ttu-id="7a824-1190">隨著值變更重新調整資料的位置 (即時繪圖)。</span><span class="sxs-lookup"><span data-stu-id="7a824-1190">Repositioning of data as the values change (live shaping).</span></span>

- <span data-ttu-id="7a824-1191">可查看項目容器的資料內容是否已中斷連線的功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1191">Ability to check whether the data context for an item container is disconnected.</span></span>

- <span data-ttu-id="7a824-1192">可設定屬性變更與資料來源更新之間應該經過之時間長度的功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1192">Ability to set the amount of time that should elapse between property changes and data source updates.</span></span>

- <span data-ttu-id="7a824-1193">改進對實作弱式事件模式的支援。</span><span class="sxs-lookup"><span data-stu-id="7a824-1193">Improved support for implementing weak event patterns.</span></span> <span data-ttu-id="7a824-1194">此外，事件現在可以接受標記延伸。</span><span class="sxs-lookup"><span data-stu-id="7a824-1194">Also, events can now accept markup extensions.</span></span>

<a name="windows_communication_foundation"></a>

### <a name="windows-communication-foundation-wcf"></a><span data-ttu-id="7a824-1195">Windows Communication Foundation (WCF)</span><span class="sxs-lookup"><span data-stu-id="7a824-1195">Windows Communication Foundation (WCF)</span></span>

<span data-ttu-id="7a824-1196">在 .NET Framework 4.5 中已加入下列功能，讓撰寫和維護 Windows Communication Foundation (WCF) 應用程式更容易：</span><span class="sxs-lookup"><span data-stu-id="7a824-1196">In the .NET Framework 4.5, the following features have been added to make it simpler to write and maintain Windows Communication Foundation (WCF) applications:</span></span>

- <span data-ttu-id="7a824-1197">簡化產生的組態檔。</span><span class="sxs-lookup"><span data-stu-id="7a824-1197">Simplification of generated configuration files.</span></span>

- <span data-ttu-id="7a824-1198">支援合約優先開發。</span><span class="sxs-lookup"><span data-stu-id="7a824-1198">Support for contract-first development.</span></span>

- <span data-ttu-id="7a824-1199">可更輕鬆地設定 ASP.NET 相容性模式的功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1199">Ability to configure ASP.NET compatibility mode more easily.</span></span>

- <span data-ttu-id="7a824-1200">預設傳輸屬性值中所做的變更，可降低必須設定這些屬性的可能性。</span><span class="sxs-lookup"><span data-stu-id="7a824-1200">Changes in default transport property values to reduce the likelihood that you will have to set them.</span></span>

- <span data-ttu-id="7a824-1201">對 <xref:System.Xml.XmlDictionaryReaderQuotas> 類別的更新，可降低必須手動設定 XML 字典讀取器配額的可能性。</span><span class="sxs-lookup"><span data-stu-id="7a824-1201">Updates to the <xref:System.Xml.XmlDictionaryReaderQuotas> class to reduce the likelihood that you will have to manually configure quotas for XML dictionary readers.</span></span>

- <span data-ttu-id="7a824-1202">Visual Studio 會在建置流程中驗證 WCF 組態檔，如此您就可以在執行應用程式之前偵測組態錯誤。</span><span class="sxs-lookup"><span data-stu-id="7a824-1202">Validation of WCF configuration files by Visual Studio as part of the build process, so you can detect configuration errors before you run your application.</span></span>

- <span data-ttu-id="7a824-1203">新增非同步資料流支援。</span><span class="sxs-lookup"><span data-stu-id="7a824-1203">New asynchronous streaming support.</span></span>

- <span data-ttu-id="7a824-1204">新增 HTTPS 通訊協定對應，如此就能更容易使用 Internet Information Services (IIS) 透過 HTTPS 公開端點。</span><span class="sxs-lookup"><span data-stu-id="7a824-1204">New HTTPS protocol mapping to make it easier to expose an endpoint over HTTPS with Internet Information Services (IIS).</span></span>

- <span data-ttu-id="7a824-1205">可藉由將 `?singleWSDL` 附加至服務 URL 的方式，在單一 WSDL 文件中產生中繼資料的功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1205">Ability to generate metadata in a single WSDL document by appending `?singleWSDL` to the service URL.</span></span>

- <span data-ttu-id="7a824-1206">Websocket 支援，可透過與 TCP 傳輸類似的效能特性在連接埠 80 與 443 之間進行真正的雙向通訊。</span><span class="sxs-lookup"><span data-stu-id="7a824-1206">Websockets support to enable true bidirectional communication over ports 80 and 443 with performance characteristics similar to the TCP transport.</span></span>

- <span data-ttu-id="7a824-1207">支援在程式碼中設定服務。</span><span class="sxs-lookup"><span data-stu-id="7a824-1207">Support for configuring services in code.</span></span>

- <span data-ttu-id="7a824-1208">XML 編輯器工具提示。</span><span class="sxs-lookup"><span data-stu-id="7a824-1208">XML Editor tooltips.</span></span>

- <span data-ttu-id="7a824-1209"><xref:System.ServiceModel.ChannelFactory> 快取支援。</span><span class="sxs-lookup"><span data-stu-id="7a824-1209"><xref:System.ServiceModel.ChannelFactory> caching support.</span></span>

- <span data-ttu-id="7a824-1210">支援二進位編碼器壓縮。</span><span class="sxs-lookup"><span data-stu-id="7a824-1210">Binary encoder compression support.</span></span>

- <span data-ttu-id="7a824-1211">支援 UDP 傳輸，可讓開發人員撰寫使用「射後不理」(Fire and Forget) 傳訊功能的服務。</span><span class="sxs-lookup"><span data-stu-id="7a824-1211">Support for a UDP transport that enables developers to write services that use "fire and forget" messaging.</span></span> <span data-ttu-id="7a824-1212">用戶端傳送訊息給服務，而不期待服務發出任何回應。</span><span class="sxs-lookup"><span data-stu-id="7a824-1212">A client sends a message to a service and expects no response from the service.</span></span>

- <span data-ttu-id="7a824-1213">可在使用 HTTP 傳輸和傳輸安全性時，於單一 WCF 端點上支援多種驗證模式的功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1213">Ability to support multiple authentication modes on a single WCF endpoint when using the HTTP transport and transport security.</span></span>

- <span data-ttu-id="7a824-1214">支援使用國際化網域名稱 (IDN) 的 WCF 服務。</span><span class="sxs-lookup"><span data-stu-id="7a824-1214">Support for WCF services that use internationalized domain names (IDNs).</span></span>

<span data-ttu-id="7a824-1215">如需詳細資訊，請參閱 [Windows Communication Foundation 中的新增功能](../wcf/whats-new.md)。</span><span class="sxs-lookup"><span data-stu-id="7a824-1215">For more information, see [What's New in Windows Communication Foundation](../wcf/whats-new.md).</span></span>

<a name="windows_workflow_foundation"></a>

### <a name="windows-workflow-foundation-wf"></a><span data-ttu-id="7a824-1216">Windows Workflow Foundation (WF)</span><span class="sxs-lookup"><span data-stu-id="7a824-1216">Windows Workflow Foundation (WF)</span></span>

<span data-ttu-id="7a824-1217">在 .NET Framework 4.5 中，Windows Workflow Foundation (WF) 已加入數個新功能，包括：</span><span class="sxs-lookup"><span data-stu-id="7a824-1217">In the .NET Framework 4.5, several new features were added to Windows Workflow Foundation (WF), including:</span></span>

- <span data-ttu-id="7a824-1218">狀態機器工作流程，最初是在 .NET Framework 4.0.1 中引進 ([.NET Framework 4 Platform Update 1](/archive/blogs/endpoint/microsoft-net-framework-4-platform-update-1))。</span><span class="sxs-lookup"><span data-stu-id="7a824-1218">State machine workflows, which were first introduced as part of .NET Framework 4.0.1 ([.NET Framework 4 Platform Update 1](/archive/blogs/endpoint/microsoft-net-framework-4-platform-update-1)).</span></span> <span data-ttu-id="7a824-1219">這項更新包括數個可讓開發人員建立狀態機器工作流程的新類別和活動。</span><span class="sxs-lookup"><span data-stu-id="7a824-1219">This update included several new classes and activities that enabled developers to create state machine workflows.</span></span> <span data-ttu-id="7a824-1220">這些類別和活動已針對 .NET Framework 4.5 進行更新，包含：</span><span class="sxs-lookup"><span data-stu-id="7a824-1220">These classes and activities were updated for the .NET Framework 4.5 to include:</span></span>

  - <span data-ttu-id="7a824-1221">可設定狀態中斷點的功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1221">The ability to set breakpoints on states.</span></span>

  - <span data-ttu-id="7a824-1222">可在工作流程設計工具中複製和貼上轉換的功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1222">The ability to copy and paste transitions in the workflow designer.</span></span>

  - <span data-ttu-id="7a824-1223">設計工具支援建立共用的觸發程序轉換。</span><span class="sxs-lookup"><span data-stu-id="7a824-1223">Designer support for shared trigger transition creation.</span></span>

  - <span data-ttu-id="7a824-1224">建立狀態機器工作流程的活動，包括：<xref:System.Activities.Statements.StateMachine>、<xref:System.Activities.Statements.State> 和 <xref:System.Activities.Statements.Transition>。</span><span class="sxs-lookup"><span data-stu-id="7a824-1224">Activities for creating state machine workflows, including: <xref:System.Activities.Statements.StateMachine>, <xref:System.Activities.Statements.State>, and <xref:System.Activities.Statements.Transition>.</span></span>

- <span data-ttu-id="7a824-1225">增強的「工作流程設計工具」功能，例如：</span><span class="sxs-lookup"><span data-stu-id="7a824-1225">Enhanced Workflow Designer features such as the following:</span></span>

  - <span data-ttu-id="7a824-1226">增強 Visual Studio 中的工作流程搜尋功能，包括「快速尋找」\*\*\*\* 和「檔案中尋找」\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="7a824-1226">Enhanced workflow search capabilities in Visual Studio, including **Quick Find** and **Find in Files**.</span></span>

  - <span data-ttu-id="7a824-1227">可在第二個子活動加入至容器活動時自動建立「序列」活動，以及同時將這兩個活動包含在「序列」活動中的功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1227">Ability to automatically create a Sequence activity when a second child activity is added to a container activity, and to include both activities in the Sequence activity.</span></span>

  - <span data-ttu-id="7a824-1228">平移支援，不需使用捲軸就能變更工作流程的可見部分。</span><span class="sxs-lookup"><span data-stu-id="7a824-1228">Panning support, which enables the visible portion of a workflow to be changed without using the scroll bars.</span></span>

  - <span data-ttu-id="7a824-1229">新的 [文件大綱]\*\*\*\* 檢視，這個檢視會以樹狀樣式大綱檢視顯示工作流程的元件，並讓您在 [文件大綱]\*\*\*\* 檢視中選取元件。</span><span class="sxs-lookup"><span data-stu-id="7a824-1229">A new **Document Outline** view that shows the components of a workflow in a tree-style outline view and lets you select a component in the **Document Outline** view.</span></span>

  - <span data-ttu-id="7a824-1230">可將註釋加入至活動的功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1230">Ability to add annotations to activities.</span></span>

  - <span data-ttu-id="7a824-1231">可使用工作流程設計工具定義並取用活動委派的功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1231">Ability to define and consume activity delegates by using the workflow designer.</span></span>

  - <span data-ttu-id="7a824-1232">在狀態機器和流程圖工作流程中自動連接和自動插入活動和轉換。</span><span class="sxs-lookup"><span data-stu-id="7a824-1232">Auto-connect and auto-insert for activities and transitions in state machine and flowchart workflows.</span></span>

- <span data-ttu-id="7a824-1233">將工作流程的檢視狀態資訊儲存在 XAML 檔案的單一元素中，如此您就可以輕鬆尋找及編輯檢視狀態資訊。</span><span class="sxs-lookup"><span data-stu-id="7a824-1233">Storage of the view state information for a workflow in a single element in the XAML file, so you can easily locate and edit the view state information.</span></span>

- <span data-ttu-id="7a824-1234">NoPersistScope 容器活動，可防止保存子活動。</span><span class="sxs-lookup"><span data-stu-id="7a824-1234">A NoPersistScope container activity to prevent child activities from persisting.</span></span>

- <span data-ttu-id="7a824-1235">支援 C# 運算式：</span><span class="sxs-lookup"><span data-stu-id="7a824-1235">Support for C# expressions:</span></span>

  - <span data-ttu-id="7a824-1236">使用 Visual Basic 的工作流程專案會使用 Visual Basic 運算式，而 C# 工作流程專案則會使用 C# 運算式。</span><span class="sxs-lookup"><span data-stu-id="7a824-1236">Workflow projects that use Visual Basic will use Visual Basic expressions, and C# workflow projects will use C# expressions.</span></span>

  - <span data-ttu-id="7a824-1237">在 Visual Studio 2010 中建立且具有 Visual Basic 運算式的 C# 工作流程專案，能夠與使用 C# 運算式的 C# 工作流程專案相容。</span><span class="sxs-lookup"><span data-stu-id="7a824-1237">C# workflow projects that were created in Visual Studio 2010 and that have Visual Basic expressions are compatible with C# workflow projects that use C# expressions.</span></span>

- <span data-ttu-id="7a824-1238">版本控制增強功能：</span><span class="sxs-lookup"><span data-stu-id="7a824-1238">Versioning enhancements:</span></span>

  - <span data-ttu-id="7a824-1239">新的 <xref:System.Activities.WorkflowIdentity> 類別，可提供已保存工作流程執行個體與其工作流程定義之間的對應。</span><span class="sxs-lookup"><span data-stu-id="7a824-1239">The new  <xref:System.Activities.WorkflowIdentity> class, which provides a mapping between a persisted workflow instance and its workflow definition.</span></span>

  - <span data-ttu-id="7a824-1240">多個工作流程版本在相同主機中並存執行，包括 <xref:System.ServiceModel.Activities.WorkflowServiceHost>。</span><span class="sxs-lookup"><span data-stu-id="7a824-1240">Side-by-side execution of multiple workflow versions in the same host, including <xref:System.ServiceModel.Activities.WorkflowServiceHost>.</span></span>

  - <span data-ttu-id="7a824-1241">在動態更新中，修改所保存工作流程執行個體定義的功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1241">In Dynamic Update, the ability to modify the definition of a persisted workflow instance.</span></span>

- <span data-ttu-id="7a824-1242">開發合約優先 (Contract-first) 工作流程服務，可提供自動配合現有服務合約產生活動的支援。</span><span class="sxs-lookup"><span data-stu-id="7a824-1242">Contract-first workflow service development, which provides support for automatically generating activities to match an existing service contract.</span></span>

<span data-ttu-id="7a824-1243">如需詳細資訊，請參閱 [Windows Workflow Foundation 的新功能](../windows-workflow-foundation/whats-new-in-wf-in-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="7a824-1243">For more information, see [What's New in Windows Workflow Foundation](../windows-workflow-foundation/whats-new-in-wf-in-dotnet.md).</span></span>

<a name="tailored"></a>

### <a name="net-for-windows-8x-store-apps"></a><span data-ttu-id="7a824-1244">適用於 Windows 8.x 市集應用程式的 .NET</span><span class="sxs-lookup"><span data-stu-id="7a824-1244">.NET for Windows 8.x Store apps</span></span>

<span data-ttu-id="7a824-1245">Windows 8.x 市集應用程式是專為特定版型規格所設計，而且會利用 Windows 作業系統的強大功能。</span><span class="sxs-lookup"><span data-stu-id="7a824-1245">Windows 8.x Store apps are designed for specific form factors and leverage the power of the Windows operating system.</span></span> <span data-ttu-id="7a824-1246">.NET Framework 4.5 或 4.5.1 的子集可用於使用 C# 或 Visual Basic 建置適用於 Windows 的 Windows 8.x 市集應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a824-1246">A subset of the .NET Framework 4.5 or 4.5.1 is available for building Windows 8.x Store apps for Windows by using C# or Visual Basic.</span></span> <span data-ttu-id="7a824-1247">針對 Windows 8. x 儲存區應用程式，此子集稱為 .NET，將在 [總覽](/previous-versions/windows/apps/br230302(v=vs.140))中討論。</span><span class="sxs-lookup"><span data-stu-id="7a824-1247">This subset is called .NET for Windows 8.x Store apps and is discussed in an [overview](/previous-versions/windows/apps/br230302(v=vs.140)).</span></span>

### <a name="portable-class-libraries"></a><span data-ttu-id="7a824-1248">可攜式類別庫<a name="portable"></a></span><span class="sxs-lookup"><span data-stu-id="7a824-1248">Portable Class Libraries <a name="portable"></a></span></span>

<span data-ttu-id="7a824-1249">在 Visual Studio 2012 (含) 以後版本中的可攜式類別庫專案可讓您撰寫及建置可在多個 .NET Framework 平台上執行的 Managed 組件。</span><span class="sxs-lookup"><span data-stu-id="7a824-1249">The Portable Class Library project in Visual Studio 2012 (and later versions) enables you to write and build managed assemblies that work on multiple .NET Framework platforms.</span></span> <span data-ttu-id="7a824-1250">使用可移植的類別庫專案，您可以選擇平臺 (例如 Windows Phone 和 .NET，以) 目標的 Windows 8 x 商店應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a824-1250">Using a Portable Class Library project, you choose the platforms (such as Windows Phone and .NET for Windows 8.x Store apps) to target.</span></span> <span data-ttu-id="7a824-1251">專案中可用的類型和成員會自動限制為這些平台上的通用類型和成員。</span><span class="sxs-lookup"><span data-stu-id="7a824-1251">The available types and members in your project are automatically restricted to the common types and members across these platforms.</span></span> <span data-ttu-id="7a824-1252">如需詳細資訊，請參閱[可攜式類別庫](../../standard/cross-platform/cross-platform-development-with-the-portable-class-library.md)。</span><span class="sxs-lookup"><span data-stu-id="7a824-1252">For more information, see [Portable Class Library](../../standard/cross-platform/cross-platform-development-with-the-portable-class-library.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="7a824-1253">另請參閱</span><span class="sxs-lookup"><span data-stu-id="7a824-1253">See also</span></span>

- [<span data-ttu-id="7a824-1254">.NET Framework 和不定期發行</span><span class="sxs-lookup"><span data-stu-id="7a824-1254">The .NET Framework and Out-of-Band Releases</span></span>](../get-started/the-net-framework-and-out-of-band-releases.md)
- [<span data-ttu-id="7a824-1255">.NET Framework 協助工具的新功能</span><span class="sxs-lookup"><span data-stu-id="7a824-1255">What's new in accessibility in the .NET Framework</span></span>](whats-new-in-accessibility.md)
- [<span data-ttu-id="7a824-1256">Visual Studio 2017 的新功能</span><span class="sxs-lookup"><span data-stu-id="7a824-1256">What's New in Visual Studio 2017</span></span>](/visualstudio/ide/whats-new-visual-studio-2017)
- [<span data-ttu-id="7a824-1257">Visual Studio 2019 的新功能</span><span class="sxs-lookup"><span data-stu-id="7a824-1257">What's New in Visual Studio 2019</span></span>](/visualstudio/ide/whats-new-visual-studio-2019)
- [<span data-ttu-id="7a824-1258">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7a824-1258">ASP.NET</span></span>](/aspnet)
- [<span data-ttu-id="7a824-1259">Visual Studio 中 c + + 的新功能</span><span class="sxs-lookup"><span data-stu-id="7a824-1259">What's New for C++ in Visual Studio</span></span>](/cpp/what-s-new-for-visual-cpp-in-visual-studio)
